<!-- Filename: J4.x:J4_Module_example_-_Mydownmsg / Display title: Esempio: Messaggio di Sito Non Disponibile -->

## Introduzione

Questo articolo presenta un modulo completo per siti Joomla per i nuovi sviluppatori da smontare per vedere la sua struttura e come funziona. È una sostituzione per un modulo precedente che utilizzava convenzioni di codifica più vecchie. Questo è progettato per Joomla 5 e versioni successive.

Ci sono articoli introduttivi sui *Concetti Generali* e sui *Moduli* nella Documentazione per Programmatori di Joomla e riprodotti nel Jdocmanual per tua comodità. Questo articolo è simile al [Modulo Base](jdocmanual?article=docus/modules/basic-module) della JPD ma ha alcune funzionalità extra.

## Scopo

Il modulo è progettato per visualizzare un messaggio temporaneo in una delle diverse lingue per un breve periodo prima che il sito chiuda per la manutenzione del sistema. Ciò dà agli utenti l'opportunità di terminare ciò che stanno facendo prima che avvenga la chiusura.

Il nome del modulo è `mod_downmsg` e il messaggio che visualizza in inglese è simile a *Questo sito chiuderà per un breve periodo alle 12:00 GMT*. L'orario e il messaggio possono essere selezionati per adattarsi alla chiusura imminente del sito.

Il modulo può essere scaricato da GitHub per installarlo o esaminarlo secondo necessità.

## Struttura del Codice Sorgente

Quanto segue è un'illustrazione schematica della struttura del codice sorgente utilizzato per creare l'estensione:

```
cefjdemos-plg-toc
|-- .vscode (folder for build settings)
|-- mod_downmsg (folder compressed to create an installable zip file)
    |-- help
        |-- en-GB
            |-- downmsg.html (this is Help screen used in the backend module edit form)
    |-- language
        |-- de-DE
            |-- mod_downmsg.ini (only frontend strings are included)
        |-- en-GB (language folder, kept with the extension code)
            |-- mod_downmsg.ini
            |-- mod_downmsg.sys.ini
        |-- fr-FR
            |-- mod_downmsg.ini (only frontend strings are included)
    |-- services (folder for dependency injection)
        |-- provider.php (the DI code)
    |-- src (folder for namespaced classes)
        |-- Dispatcher (folder for extension specific code)
            |-- Dispatcher.php (the extension class code)
    |-- tmpl (folder for layouts)
        |-- default.php (the table of contents layout)
    |-- mod_downmsg.xml (the manifest file)
|-- .gitignore (items not to include in the git repository)
|-- build.xml (instructions for building the extension with phing)
|-- changelog.xml (record of changes)
|-- LICENSE (the license statement)
|-- README.md (brief description and instructions on use)
|-- updates.xml (update server specification)
```

Questa è la struttura come appare nell'IDE di VSCode o VSCodium:

![Plugin development file structure in vscodium](../../../en/images/modules/downmsg-module-vscodium.png)

## Il File Manifesto

Il file manifesto controlla i processi di installazione, aggiornamento e disinstallazione dell'estensione:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<extension type="module" method="upgrade" client="site">
    <name>mod_downmsg</name>
    <creationDate>December 2024</creationDate>
    <author>Clifford E Ford</author>
    <authorEmail>cliff@xxx.yyy.co.uk</authorEmail>
    <authorUrl>http://jdocmanual.org/</authorUrl>
    <copyright>Copyright (C) 2024 Clifford E Ford, All rights reserved.</copyright>
    <license>GNU/GPLv3 http://www.gnu.org/licenses/gpl-3.0.html</license>
    <!--  The version string is recorded in the components table -->
    <version>0.1.0</version>
    <!-- The description is optional and defaults to the name -->
    <description>MOD_DOWNMSG_XML_DESCRIPTION</description>
    <namespace path="src">Cefjdemos\Module\Downmsg</namespace>
    <files>
        <folder>help</folder>
        <folder>language</folder>
        <folder module="mod_downmsg">services</folder>
        <folder>src</folder>
        <folder>tmpl</folder>
    </files>
    <help url="MOD_DOWNMSG_HELP_URL" />
    <changelogurl>https://raw.githubusercontent.com/ceford/cefjdemos-mod-downmsg/main/changelog.xml</changelogurl>
    <updateservers>
        <!-- Note: No spaces or linebreaks allowed between the server tags -->
        <server type="extension" priority="2" name="Mod Downmsg Update Site">https://raw.githubusercontent.com/ceford/cefjdemos-mod-downmsg/main/updates.xml</server>
    </updateservers>
    <config>
        <fields name="params">
            <fieldset name="basic">
                <field
                    name="msg_id"
                    type="list"
                    label="MOD_DOWNMSG_PARAMS_MSG_ID_LABEL"
                    description="MOD_DOWNMSG_PARAMS_MSG_ID_DESC"
                    default="v1"
                    required="true"
                >
                    <option value="v1">MOD_DOWNMSG_PARAMS_MSG_ID_OPTION_V1</option>
                    <option value="v2">MOD_DOWNMSG_PARAMS_MSG_ID_OPTION_V2</option>
                </field>
                <field
                    name="hour"
                    type="number"
                    label="MOD_DOWNMSG_PARAMS_HOUR_LABEL"
                    description="MOD_DOWNMSG_PARAMS_HOUR_DESC"
                    default="12"
                    min="0"
                    max="23"
                    required="true"
                />
                <field
                    name="minute"
                    type="number"
                    label="MOD_DOWNMSG_PARAMS_MINUTE_LABEL"
                    description="MOD_DOWNMSG_PARAMS_MINUTE_DESC"
                    default="00"
                    min="00"
                    max="59"
                    required="true"
                />
                <field
                    name="tz"
                    type="number"
                    label="MOD_DOWNMSG_PARAMS_TZ_LABEL"
                    description="MOD_DOWNMSG_PARAMS_TZ_DESC"
                    default="0"
                    min="-11"
                    max="11"
                    required="true"
                />
            </fieldset>
        </fields>
    </config>
</extension>
```

### Note sugli elementi

- Gli attributi dell'**estensione**:
    - **type="module"** indica il tipo di estensione.
    - **method="upgrade"** significa che questa estensione può essere installata e aggiornata se sono disponibili versioni più recenti.
    - **client="site"** dice a Joomla che si tratta di un modulo *Sito* piuttosto che di un modulo *Amministratore*.
- La dichiarazione di **versione** viene utilizzata per controllare l'aggiornamento. Se è disponibile un server di aggiornamento, viene confrontato con la versione registrata lì. Impedisce anche che una versione più vecchia sovrascriva una più recente.
- L'attributo del percorso dello **spazio dei nomi** indica a Joomla dove cercare le classi dello spazio dei nomi.
- La sezione dei **file** elenca cartelle e file per l'installazione. Se un elemento non è presente qui, non verrà installato anche se è presente nel file di installazione zip.
- L'attributo url del **supporto** consente di utilizzare un file di aiuto personalizzato nel modulo di modifica. Il percorso del file di aiuto è un valore per la chiave data nel file en-GB/mod_downmsg.ini.
- La sezione di **configurazione** mostra quali parametri sono necessari per questo modulo. Tutti dovrebbero avere impostazioni predefinite perché vengono impostati all'installazione.

## I File della Lingua

Questo modulo ha pochissime stringhe. Quelle nei file **sys.ini** vengono utilizzate durante l'installazione e per l'elenco tra altri moduli. I file **.ini** vengono utilizzati nel modulo Amministratore e nel rendering del modulo nel Sito. Nota le convenzioni nell'identificazione delle stringhe:

MOD\_\[nome\]\_\[scopo\]\_\[uso\]

I file qui sotto mostrano che le traduzioni in tedesco e francese includono solo le stringhe da visualizzare dai visitatori del sito, poiché il modulo dei Parametri sarà sempre gestito in inglese. Nel caso non lo sapessi: le stringhe en-GB vengono sempre caricate prima per impostazione predefinita per garantire che le stringhe non tradotte accidentalmente non appaiano come chiavi di stringa. Successivamente vengono caricate le stringhe della lingua richiesta che sovrascrivono le stringhe inglesi equivalenti.

Le versioni francesi e tedesche delle stringhe qui sono state ottenute utilizzando gli strumenti di traduzione di Google. Questo potrebbe funzionare meglio per le frasi che per le singole parole!

### en-GB/mod_downmsg.ini

```ini
MOD_DOWNMSG="System Down Message"
MOD_DOWNMSG_XML_DESCRIPTION="Show a message about imminent system down time."

MOD_DOWNMSG_HELP_URL="../modules/mod_downmsg/help/en-GB/downmsg.html"

MOD_DOWNMSG_MSG_V1="This site will close for a short period at %s"
MOD_DOWNMSG_MSG_V2="Please log out. This site will close for one hour or more at %s"

MOD_DOWNMSG_PARAMS_MSG_ID_LABEL="Select Message version"
MOD_DOWNMSG_PARAMS_MSG_ID_DESC="The short downtime or long downtime message vesion."

MOD_DOWNMSG_PARAMS_MSG_ID_OPTION_V1="Short < 1 hour"
MOD_DOWNMSG_PARAMS_MSG_ID_OPTION_V2="Long > 1 hour"

MOD_DOWNMSG_PARAMS_HOUR_LABEL="Hour"
MOD_DOWNMSG_PARAMS_HOUR_DESC="Set the hour when the site will close"

MOD_DOWNMSG_PARAMS_MINUTE_LABEL="Minute"
MOD_DOWNMSG_PARAMS_MINUTE_DESC="Set the minutes when the site will close"

MOD_DOWNMSG_PARAMS_TZ_LABEL="Time Zone"
MOD_DOWNMSG_PARAMS_TZ_DESC="Set your time zone offset from GMT"
```

### en-GB/mod_downmsg.sys.ini

Questo file è utilizzato per la gestione del sistema.

```ini
MOD_DOWNMSG="System Down Message"
MOD_DOWNMSG_XML_DESCRIPTION="Show a message about imminent system down time."
```

### de-DE/mod_downmsg.ini

```ini
MOD_DOWNMSG_MSG_V1="Diese Seite wird für kurze Zeit um %s geschlossen"
MOD_DOWNMSG_MSG_V2="Bitte melden Sie sich ab. Diese Seite wird für eine Stunde oder länger um %s geschlossen"
MOD_DOWNMSG_HELP_URL="../modules/mod_downmsg/help/en-GB/downmsg.html"
```

### fr-FR/mod_downmsg.ini

```ini
MOD_DOWNMSG_MSG_V1="Ce site sera fermé pour une courte période à %s"
MOD_DOWNMSG_MSG_V2="Veuillez vous déconnecter. Ce site sera fermé pendant une heure ou plus à %s"
MOD_DOWNMSG_HELP_URL="../modules/mod_downmsg/help/en-GB/downmsg.html"
```

## Il Codice del Modulo

Il codice del modulo è incredibilmente semplice. Ci sono tre file PHP:

- services/provider.php (il codice per l'iniezione delle dipendenze).
- src/Dispatcher/Dispatcher.php (assembla i dati da utilizzare per la visualizzazione).
- tmpl/default.php (il template per visualizzare i dati, che può essere sovrascritto).

### servizi/provider.php

```php
<?php

/**
 * @package     Cefjdemos.Site
 * @subpackage  mod_downmsg
 *
 * @copyright   (C) 2023 Open Source Matters, Inc. <https://www.joomla.org>
 * @license     GNU General Public License version 2 or later; see LICENSE.txt
 */

\defined('_JEXEC') or die;

use Joomla\CMS\Extension\Service\Provider\Module;
use Joomla\CMS\Extension\Service\Provider\ModuleDispatcherFactory;
use Joomla\DI\Container;
use Joomla\DI\ServiceProviderInterface;

/**
 * The module Downmsg service provider.
 *
 * @since  4.4.0
 */
return new class () implements ServiceProviderInterface {
    /**
     * Registers the service provider with a DI container.
     *
     * @param   Container  $container  The DI container.
     *
     * @return  void
     *
     * @since   4.4.0
     */
    public function register(Container $container): void
    {
        $container->registerServiceProvider(new ModuleDispatcherFactory('\\Cefjdemos\\Module\\Downmsg'));
        $container->registerServiceProvider(new Module());
    }
};
```

### src/Dispatcher/Dispatcher.php

```php
<?php

/**
 * @package     Cefjdemos.Site
 * @subpackage  mod_downmsg
 *
 * @copyright   (C) 2023 Open Source Matters, Inc. <https://www.joomla.org>
 * @license     GNU General Public License version 2 or later; see LICENSE.txt
 */

namespace Cefjdemos\Module\Downmsg\Site\Dispatcher;

use Joomla\CMS\Dispatcher\AbstractModuleDispatcher;

// phpcs:disable PSR1.Files.SideEffects
\defined('_JEXEC') or die;
// phpcs:enable PSR1.Files.SideEffects

/**
 * Dispatcher class for mod_downmsg
 *
 * @since  4.4.0
 */
class Dispatcher extends AbstractModuleDispatcher
{
    /**
     * Returns the layout data.
     *
     * @return  array
     *
     * @since   4.4.0
     */
    protected function getLayoutData()
    {
        $data = parent::getLayoutData();

        return $data;
    }
}
```

### tmpl/default.php

```php
<?php

/**
 * @package     Cefjdemos.Module
 * @subpackage  mod_downmsg
 *
 * @copyright   Copyright (C) 2019 Clifford E Ford. All rights reserved.
 * @license     GNU/GPLv3 http://www.gnu.org/licenses/gpl-3.0.html
 */

defined('_JEXEC') or die;

use Joomla\CMS\Language\Text;

// the $msg string contains a %s placeholder to be replaced in a sprintf statement
$msg = Text::_('MOD_DOWNMSG_MSG_' . strtoupper($params->get('msg_id')));

$tod = $params->get('hour') . ':' . $params->get('minute');
$tz = $params->get('tz');

if ($tz > 0) {
    $tz = '(+' . $tz . ')';
} elseif ($tz < 0) {
    $tz = '(-' . $tz . ')';
} else {
    $tz = '';
}

$tod .= ' GMT ' . $tz;

?>

<div class="alert alert-warning text-center" role="alert">
    <?php echo sprintf($msg, $tod); ?>
</div>
```

## Installazione

Dal menu Amministratore, vai alla pagina Sistema / Installa / Estensioni e utilizza la scheda Carica file pacchetto per caricare il file zip. Quindi vai a Contenuti / Moduli del sito e modifica il modulo appena installato.

Nel modulo di modifica:

1. Inserisci un titolo. Ricorda che un modulo può avere più di un'istanza, quindi potrebbero apparire in posizioni diverse o avere parametri differenti.
2. Imposta l'ora in cui il sito sarà offline.
3. Imposta il fuso orario (probabilmente c'è un modo migliore rispetto all'uso dell'ora GMT +- n ore).

Nella lista dei parametri comuni a destra

1. Imposta il **Titolo** su **nascondi**.  
2. Seleziona una **Posizione** del modello - in Cassiopeia **topbar** mette il messaggio sopra il contenuto della pagina, perfetto.  
3. Imposta lo **Stato** su **Pubblicato**.  
4. Nella scheda **Assegnazione menu** seleziona **Su tutte le pagine**.  
5. **Salva** e sei pronto a controllare l'aspetto del sito.

![the module edit form](../../../en/images/modules/downmsg-module-edit-form.png)

## Testando

Ecco come appare il messaggio in inglese:

![site down message in english](../../../en/images/modules/downmsg-module-result-en.png)

In tedesco:

![site down message in english](../../../en/images/modules/downmsg-module-result-de.png)

E Francese:

![site down message in english](../../../en/images/modules/downmsg-module-result-fr.png)

## Aggiorna sito e registro modifiche

Questi elementi sono inclusi nella fonte ma non sono trattati qui.

*Tradotto da openai.com*

