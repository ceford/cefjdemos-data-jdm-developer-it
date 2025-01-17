<!-- Filename: J4.x:J4_Plugin_example_-_Table_of_Contents / Display title: Esempio: Indice -->

## Introduzione

Questo articolo fornisce un esempio di plugin di contenuto per illustrare la codifica utilizzando le ultime convenzioni di codifica di Joomla. Il codice completo è disponibile su [GitHub](https://github.com/ceford/cefjdemos-plg-content-toc). Puoi scaricarlo e installarlo o semplicemente decomprimerlo per ispezionare il codice.

C'è una sezione sullo [Sviluppo di Plugin](https://manual.joomla.org/docs/building-extensions/plugins/) e ulteriori esempi nella Documentazione per Programmatori Joomla, [copiata su questo sito](jdocmanual?article=docus/plugins/index) per comodità.

Questo plugin genera un *Indice dei Contenuti* dalle intestazioni in qualsiasi articolo contenente un segnaposto `{cefjdemostoc}`. Il risultato è illustrato nell'ultima schermata di questo articolo.

## Struttura del Codice Sorgente

La seguente è un'illustrazione schematica della struttura del codice sorgente utilizzato per creare l'estensione:

```
cefjdemos-plg-toc
|-- .vscode (folder for build settings)
|-- plg_content_cefjdemostoc (folder compressed to create an installable zip file)
    |-- language/en-GB/ (language folder, kept with the extension code)
        |-- plg_content_cefjdemostoc.ini
        |-- plg_content_cefjdemostoc.sys.ini
    |-- media
        |-- css
            |-- cefjdemostoc.css (layout styles)
    |-- services (folder for dependency injection)
        |-- provider.php (the DI code)
    |-- src (folder for namespaced classes)
        |-- Extension (folder for extension specific code)
            |-- Cefjdemostoc.php (the extension class code)
    |-- tmpl (folder for layouts)
        |-- default.php (the table of contents layout)
    |-- cefjdemostoc.xml (the manifest file)
|-- .gitignore (items not to include in the git repository)
|-- build.xml (instructions for building the extension with phing)
|-- LICENSE (the license statement)
|-- README.md (brief description and instructions on use)
```

Questa è la struttura come appare nell'IDE VSCode o VSCodium:

![Plugin development file structure in vscodium](../../../en/images/plugins/cefjdemostoc-vscodium.png)

## Il File Manifesto

Ogni estensione deve avere un file di manifest in formato xml. Viene utilizzato da Joomla per scopi di installazione, aggiornamento e rimozione. Questo è il file di manifest per questa estensione:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<extension type="plugin" group="content" method="upgrade">
    <name>plg_content_cefjdemostoc</name>
    <author>Clifford E Ford</author>
    <creationDate>2024-12-23</creationDate>
    <copyright>(C) 2024 Clifford E Ford</copyright>
    <license>GNU General Public License version 2 or later; see LICENSE.txt</license>
    <authorEmail>cliff@xxxx.yyyy.co.uk</authorEmail>
    <authorUrl>jdocmanual.org</authorUrl>
    <version>0.2.2</version>
    <description>PLG_CONTENT_CEFJDEMOSTOC_XML_DESCRIPTION</description>
    <namespace path="src">Cefjdemos\Plugin\Content\Cefjdemostoc</namespace>
    <files>
        <folder plugin="cefjdemostoc">services</folder>
        <folder>src</folder>
        <folder>language</folder>
    </files>
    <media destination="plg_content_cefjdemostoc" folder="media">
        <folder>css</folder>
    </media>
    <changelogurl>https://raw.githubusercontent.com/ceford/cefjdemos-plg-content-toc/main/changelog.xml</changelogurl>
    <updateservers>
        <!-- Note: No spaces or linebreaks allowed between the server tags -->
        <server type="extension" priority="2" name="Cefjdemostoc Update Site">https://raw.githubusercontent.com/ceford/cefjdemos-plg-content-toc/main/updates.xml</server>
    </updateservers>
    <config>
        <fields name="params">
            <fieldset name="basic">
                <field
                    name="help"
                    type="list"
                    label="PLG_CONTENT_CEFJDEMOSTOC_PARAMS_APPLIES_LABEL"
                    description="PLG_CONTENT_CEFJDEMOSTOC_PARAMS_APPLIES_DESC"
                    default="PLG_CONTENT_CEFJDEMOSTOC_PARAMS_APPLIES_DEFAULT"
                >
                    <option value="">PLG_CONTENT_CEFJDEMOSTOC_PARAMS_APPLIES_DEFAULT</option>
                </field>

                <field
                    name="toc_class"
                    type="text"
                    label="PLG_CONTENT_CEFJDEMOSTOC_PARAMS_CARD_CLASS_LABEL"
                    description="PLG_CONTENT_CEFJDEMOSTOC_PARAMS_CARD_CLASS_DESC"
                />

                <field
                    name="toc_head_class"
                    type="list"
                    label="PLG_CONTENT_CEFJDEMOSTOC_PARAMS_CARD_HEAD_CLASS_LABEL"
                    description="PLG_CONTENT_CEFJDEMOSTOC_PARAMS_CARD_HEAD_CLASS_DESC"
                    default="center"
                >
                    <option value="text-center">text-center</option>
                    <option value="text-start">text-start</option>
                </field>
            </fieldset>
        </fields>
    </config>
</extension>
```

## Il file servizi/provider.php

Lo scopo di questo file è registrare un fornitore di servizi e dichiarare gli strumenti necessari. Questo plugin particolare non richiede molto. Se il tuo plugin personalizzato avesse bisogno di effettuare query al database, lo dichiari qui. Dai un'occhiata a un plugin di autenticazione. Richiedono strumenti per database e utenti.

```php
<?php

/**
 * @package     Cefjdemostoc.Plugin
 * @subpackage  Content.cefjdemostoc
 *
 * @copyright   (C) 2024 Clifford E Ford <https://jdocmanual.org>
 * @license     GNU General Public License version 2 or later; see LICENSE.txt
 */

\defined('_JEXEC') or die;

use Joomla\CMS\Extension\PluginInterface;
use Joomla\CMS\Factory;
use Joomla\CMS\Plugin\PluginHelper;
use Joomla\DI\Container;
use Joomla\DI\ServiceProviderInterface;
use Joomla\Event\DispatcherInterface;
use Cefjdemos\Plugin\Content\Cefjdemostoc\Extension\Cefjdemostoc;

return new class () implements ServiceProviderInterface {
    /**
     * Registers the service provider with a DI container.
     *
     * @param   Container  $container  The DI container.
     *
     * @return  void
     *
     * @since   4.3.0
     */
    public function register(Container $container)
    {
        $container->set(
            PluginInterface::class,
            function (Container $container) {
                $plugin     = new Cefjdemostoc(
                    $container->get(DispatcherInterface::class),
                    (array) PluginHelper::getPlugin('content', 'cefjdemostoc')
                );
                $plugin->setApplication(Factory::getApplication());

                return $plugin;
            }
        );
    }
};
```

## La Classe di Estensione

Lo scopo del file src/Extension/Cefjdemostoc.php è preparare i dati per l'output. Il file è lungo 91 righe, quindi non viene riprodotto qui. Tuttavia, alcune parti di esso meritano ulteriori spiegazioni.

### Direttive Codesniffer

Righe da 16 a 18 hanno questo:

```php
// phpcs:disable PSR1.Files.SideEffects
\defined('_JEXEC') or die;
// phpcs:enable PSR1.Files.SideEffects
```

Le righe commentate evitano segnalazioni di errori da parte del CodeSniffer. Non hanno altri scopi.

### funzione pubblica onContentPrepare()

Questo è l'evento a cui il plugin risponde. Viene passato un *contesto*, i dati dell'articolo e i parametri dell'articolo. Un *Indice* dovrebbe essere generato solo se la pagina resa è un singolo articolo. Altrimenti, il segnaposto `{cefjdemostoc}` deve essere rimosso.

Per generare un indice, alcuni parametri dell'articolo sono impostati e ogni titolo nell'articolo viene modificato per aggiungere un numero di sequenza **id**, quindi `<h2>Introduction</h2>` diventa `<h2 id="cefjemostoc0">Introduction</h2>`. Viene quindi caricata una template per aggiungere l'indice renderizzato.

### Il file tmpl/default.php

Lo scopo di questo file è quello di rendere l'output con i dati forniti. Il file può essere sovrascritto e lo vedrai tra le sostituzioni di **plugins/contents** per il modello Cassiopeia.

Il file è riprodotto di seguito. Nota che alcuni elementi hanno classi CSS hardcoded e alcuni ottenuti dai parametri dell'articolo. Le classi **fs-** sono dimensioni del carattere di Bootstrap. Le intestazioni sono memorizzate nell'array `$headings2`.

```php
<?php

/**
 * @package     Cefjdemostoc.Plugin
 * @subpackage  Content.cefjemostoc
 *
 * @copyright   (C) 2024 Clifford E Ford.
 * @license     GNU General Public License version 2 or later; see LICENSE.txt
 */

defined('_JEXEC') or die;

use Joomla\CMS\Language\Text;

/**
 * @var Joomla\CMS\WebAsset\WebAssetManager $wa
 * @var \Joomla\Plugin\Content\Cefjdemostoc\Extension\Cefjdemostoc $this
 */
$wa = $this->getApplication()->getDocument()->getWebAssetManager();
$wa->registerAndUseStyle('plg_content_cefjdemostoc', 'plg_content_cefjdemostoc/cefjdemostoc.css');

?>
<div class="card cefjdemostoc <?php echo $toc_class; ?>">
    <div class="card-header">
        <div class="<?php echo $toc_head_class; ?> fs-2">
            <?php echo Text::_('PLG_CONTENT_CEFJDEMOSTOC_CONTENTS'); ?>
        </div>
    </div>
    <div class="card-body">
        <ul class="list-group">
            <?php foreach ($headings2 as $i => $heading) : ?>
                <li class="list-group-item fs-<?php echo $heading[1] + 2; ?> ps-<?php echo $heading[1] + 2; ?>">
                    <a href="#cefjemostoc<?php echo $i; ?>" class="link-underline-light">
                        <?php echo $heading[2]; ?>
                    </a>
                </li>
            <?php endforeach; ?>
        </ul>
    </div>
</div>
```

#### Il gestore delle risorse web

Senza ulteriori stili, l'indice dei contenuti (ToC) occuperebbe l'intera larghezza dello schermo nella posizione del segnaposto `{cefjemostoc}` nel testo originale. Questo a volte si vede nelle pubblicazioni tecniche, ma potrebbe non essere quello che desideri. Su schermi ampi è spesso meglio spostare il ToC e permettere al testo dell'articolo di fluire intorno ad esso. Tuttavia, ciò può diventare inutilizzabile su schermi stretti. La soluzione migliore è fornire un foglio di stile con media query personalizzate. Su schermi ampi il ToC è spostato a destra, ma su schermi stretti non lo è.

Il codice `default.php` sopra mostra come includere un foglio di stile personalizzato per il plugin. Il CSS si trova nel file `media/css/cefjdemostoc.css`. I valori lì presenti sono a scopo illustrativo di questo tutorial.

## Risultato

![The resulting table of contents](../../../en/images/plugins/cefjdemostoc-result.png)

*Tradotto da openai.com*

