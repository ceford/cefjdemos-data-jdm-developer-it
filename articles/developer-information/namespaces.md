<!-- Filename: J4.x:Namespace_Conventions_In_Joomla / Display title: Namespace -->

## Introduzione

L'uso dei **Namespace PHP** è un modo per raggruppare classi, interfacce, funzioni e costanti correlate per evitare conflitti di nome in progetti più grandi. Consentono agli sviluppatori di organizzare il codice in modo più efficace, soprattutto quando si lavora con librerie di terze parti o basi di codice di grandi dimensioni che potrebbero avere nomi di classi duplicati.

C'è più informazione nella sezione [Namespace](jdocmanual?article=docus/namespaces/index) della Documentazione per Programmatori di Joomla!.

### Caratteristiche Principali dei Namespace PHP

1. **Evitare Conflitti di Nome**:
   - Senza namespace, se due classi hanno lo stesso nome, PHP genererà un errore. I namespace forniscono un contesto per identificare in modo univoco classi o altri elementi.
2. **Organizzare il Codice**:
   - I namespace consentono di raggruppare logicamente classi o funzioni correlate, rendendo il codice più facile da leggere e mantenere.
3. **Accesso tramite Nomi Completamente Qualificati**:
   - Le classi e le funzioni all'interno di un namespace possono essere accessibili utilizzando il loro nome completamente qualificato, che include il percorso del namespace.

### Pratiche Comuni:
- Usa gli spazi dei nomi per rispecchiare la struttura delle cartelle del tuo progetto per coerenza.
- Importa gli spazi dei nomi utilizzando la parola chiave `use` per un codice più pulito.

## Il File Manifesto

La dichiarazione iniziale di uno spazio dei nomi di estensione si trova in un file manifesto di estensione, come in questo esempio:

```xml
    <namespace path="src">Acme\Component\Wonderful</namespace>
```

Gli articoli in questa dichiarazione sono i seguenti:

- **path="src"** indica al class loader che le classi con spazio dei nomi si trovano nella cartella **src** dell'estensione, per esempio com_wonderful/src.
- **Acme** è il prefisso del fornitore. Per le estensioni del core di Joomla sarebbe *Joomla*. Devi inventare il tuo prefisso univoco del fornitore.
- **Component** indica il tipo di estensione (componente, modulo, plugin, template, libreria, ...).
- **Wonderful** è il nome dell'estensione. Scegli un nome per l'estensione che sia breve, significativo e probabilmente unico.

## Il File della Classe

La dichiarazione dello spazio dei nomi deve essere la prima istruzione nel file in cui viene utilizzata. Per esempio:

```php
<?php

/**
 * @package     Wonderful
 * @subpackage  Site
 *
 * @copyright   (C) 2024 Merlin. All rights reserved.
 * @license     GNU General Public License version 2 or later; see LICENSE.txt
 */

namespace Acme\Component\Wonderful\Controller;

use Joomla\CMS\MVC\Controller\BaseController;

// phpcs:disable PSR1.Files.SideEffects
\defined('_JEXEC') or die;
// phpcs:enable PSR1.Files.SideEffects

/**
 * Controller to display the default page - display of wonderful items
 *
 * @since  1.0.0
 */
class MagicController extends BaseController
{
    public function dosomething($wonderful)
    {
        // ... output something wonderful!
    }
}
```

## Utilizzo del file di classe

Quando hai bisogno di utilizzare la classe, ad esempio in un template, inserisci un'istruzione **use** all'inizio del template:

```
use Acme\Component\Wonderful\Controller\MagicController;
```

E poi istanzia la classe e chiama la funzione:

```
$magic = new MagicController;
$result = $magic->dosomething('wonderful');
```

## Il file autoload_psr4.php

Questo file si trova nella cartella administrator/cache del sito Joomla. Contiene una mappa completa degli spazi dei nomi estratti dai file manifest. Viene generato durante l'installazione e rigenerato ogni volta che un'estensione viene installata o reinstallata. Puoi eliminare questo file e verrà rigenerato al caricamento della pagina successiva. A volte è necessario farlo se l'installazione dell'estensione è stata tentata con un metodo insolito. Il file contiene 275 o più percorsi a posizioni di classi con namespace.

**PSR** è un acronimo per [**PHP Standards Recommendation**](https://www.php-fig.org/psr/) e [**PSR-4: Autoloader**](https://www.php-fig.org/psr/psr-4/) è uno standard accettato per caricare le classi PHP.

*Tradotto da openai.com*

