<!-- Filename: J4.x:MVC_Anatomy:_Site_Files / Display title: MVC Anatomia: File del Sito -->

## Struttura dei file

Ci sono meno file nella parte del sito del componente rispetto alla parte dell'amministratore, quindi questo sembra un buon punto di partenza. Verranno trattate solo le parti di ciascun file che necessitano di spiegazione. È meglio aprire ogni file menzionato, dare un'occhiata al contenuto generale e poi trovare le parti spiegate. L'ordine alfabetico della struttura dei file è il seguente:

```bash
    site
    |- forms
        |- filter_countries.xml
    |- language
        |- en-GB
           |- com_countrybase.ini
    |- src
        |- Controller
           |- DisplayController
        |- Model
           |- CountriesModel.php
        |- Service
           |- Router.php
        |- View
           |- Countries
              |- HtmlView.php
    |- tmpl
        |- countries
           |- default.php
           |- default.xml
```

## DisplayContoller.php

```php
<?php

/**
 * @package     Countrybase.Site
 * @subpackage  com_countrybase
 *
 * @copyright   (C) 2025 Clifford E Ford
 * @license     GNU General Public License version 3 or later; see LICENSE.txt
 */

namespace Cefjdemos\Component\Countrybase\Site\Controller;

// phpcs:disable PSR1.Files.SideEffects
\defined('_JEXEC') or die;
// phpcs:enable PSR1.Files.SideEffects

use Joomla\CMS\MVC\Controller\BaseController;
use Joomla\CMS\Router\Route;
use Joomla\CMS\Session\Session;

/**
 * Countrybase Component Controller
 *
 * @since  1.0.0
 */
class DisplayController extends BaseController
{
    /**
     * The default view.
     *
     * @var    string
     */
    protected $default_view = 'countries';
}
```

Parti di questo file sono spiegate come segue:

### Avviso di Copyright

Ogni file php dovrebbe iniziare con un avviso di copyright come il seguente:

```php
<?php

/**
 * @package     Countrybase.Site
 * @subpackage  com_countrybase
 *
 * @copyright   (C) 2025 Clifford E Ford
 * @license     GNU General Public License version 3 or later; see LICENSE.txt
 */
```

Se crei frequentemente nuovi file e copi/incolli questa sezione, ricorda di aggiornare il nome del componente e l'avviso di copyright. Inoltre, il code sniffer richiede una riga vuota prima di un blocco di documentazione.

### Namespace e controllo definito

Dopo l'avviso di copyright, ogni file php deve contenere una riga con defined('_JEXEC') or die; tuttavia, i file con namespace devono dichiarare il namespace prima di qualsiasi altro codice php, quindi prima del controllo defined. I file php con namespace sono quelli che contengono classi php del componente nella cartella src o nelle sue sottocartelle.

```php
namespace Cefjemos\Component\Countrybase\Site\Controller;

// phpcs:disable PSR1.Files.SideEffects
\defined('_JEXEC') or die;
// phpcs:enable PSR1.Files.SideEffects
```

Il controllo `defined` impedisce che un file php venga eseguito chiamandolo direttamente tramite il suo URL. La costante `_JEXEC` viene definita quando l'applicazione inizia tramite il file index.php della radice o dell'amministratore. È un importante aiuto di sicurezza.

Il controllo `defined` è racchiuso in `phpcs:disable` e `phpcs:enable` per consentire una violazione dello standard di codifica PSR12.

Combinato con lo spazio dei nomi dichiarato nel file manifesto countrybase.xml, Joomla cercherà qualsiasi classe dichiarata nel file corrente in root/components/com_countrybase/src/Controller - in questo caso aggiungendo il nome di questo file, DisplayController.php.

### Istruzioni use

Le istruzioni use solitamente seguono il controllo definito e sono spesso elencate in ordine alfabetico. Le istruzioni use definiscono le posizioni delle classi utilizzate da questo file PHP. A volte, le istruzioni use sono presenti per errore, venendo dichiarate ma non usate. Questo non causa danni ma dovrebbe essere corretto. Ci sono due istruzioni inutilizzate qui:

```php
    use Joomla\CMS\Router\Route;
    use Joomla\CMS\Session\Session;
```

### Classe Controller

Il controller di visualizzazione ha quasi nulla da fare poiché tutto il lavoro viene eseguito nella classe genitore. La cosa importante che fa è impostare la vista predefinita, in questo caso **countries**. Questo farà sì che la vista del componente predefinito utilizzi i file Countries/HtmlView.php e tmpl/countries/default.php per visualizzare i dati dei paesi.

```php
/**
 * Countrybase Component Controller
 *
 * @since  1.0.0 Created for first release.
 */
class DisplayController extends BaseController
{
    /**
     * The default view.
     *
     * @var    string
     */
    protected $default_view = 'countries';
}
```

Il blocco di documentazione (DocBlock) che precede l'istruzione `class` viene utilizzato per la documentazione automatica con strumenti come *Doxygen*. L'istruzione `@since` è un *tag* che indica il numero di versione dell'estensione in cui è stato introdotto questo elemento. Può essere seguita da una semplice spiegazione testuale. Qualsiasi elemento può avere un DocBlock con un numero qualsiasi di tag standard. È una buona pratica mantenere il proprio codice ben documentato!

Non dimenticare di impostare \$default_view per questo controller. Senza di esso, il DisplayController utilizzerà la vista predefinita definita nel file di configurazione del componente o, se questa non esiste, il nome del componente.

## src/View/Countries/HtmlView.php

Il controller ha impostato la vista predefinita su **countries**, quindi il passo successivo è caricare il codice corrispondente HtmlView.php. Parti di questo file richiedono qualche spiegazione.

### Variabili di classe

```php
class HtmlView extends BaseHtmlView
{
    /**
     * The model state
     *
     * @var  \Joomla\CMS\Object\CMSObject
     */
    protected $state = null;
    ...
    protected $items = null;
    ...
    protected $pagination = null;
    ...
    public $filterForm;
    ...
    public $activeFilters;
```

Le variabili della classe vengono utilizzate per memorizzare informazioni sulla pagina da visualizzare:

- `$state` - lo stato del modello, spesso avviato dall'input del modulo o della stringa di query.
- `$items` - l'elenco dei dati dei paesi recuperati dal database.
- `$pagination` - un oggetto utilizzato per visualizzare un meccanismo di navigazione delle pagine se ci sono più pagine rispetto al limite dell'elenco, normalmente 20 elementi.
- `$filterForm` - solitamente non presente nelle pagine del sito ma utilizzato in com_countrybase per filtrare per nome del paese o stato pubblicato.
- `$activeFilters` - utilizzato per tenere traccia di quali filtri sono in uso.

### funzione di visualizzazione

È abbastanza standard per una visualizzazione del sito, a parte le sezioni filterForm e activeFilters:

```php
    public function display($tpl = null)
    {
        $this->state      = $this->get('State');
        $this->items      = $this->get('Items');
        $this->pagination = $this->get('Pagination');
        $this->filterForm    = $this->get('FilterForm');
        $this->activeFilters = $this->get('ActiveFilters');

        // Flag indicates to not add limitstart=0 to URL
        $this->pagination->hideEmptyLimitstart = true;

        // Check for errors.
        if (count($errors = $this->get('Errors')))
        {
            throw new GenericDataException(implode("\n", $errors), 500);
        }

        parent::display($tpl);
    }
```

Le dichiarazioni della forma `$this->get('Xxxx')` fanno sì che Joomla cerchi in `CountriesModel.php` una funzione chiamata `getXxxx()` e restituisca qualsiasi dato prodotto da quel codice per la memorizzazione e l'uso nella vista. Spesso la funzione si trova nel genitore di CountriesModel. Ad esempio, la funzione getItems non è presente in CountriesModel.php ma è presente in ListModel da cui deriva.

In sintesi, la classe di visualizzazione recupera i dati dal modello e poi chiama la sua classe genitore per mostrare i dati.

## Modello/PaesiModello.php

Ci sono un numero ridotto di funzioni nel Modello che di solito devi completare tu stesso. Altre sono ereditate dal ListModel genitore.

### __costruisci

È prassi normale includere nel costruttore eventuali campi di filtro che si desidera utilizzare. Senza di essi, i filtri potrebbero sembrare non avere effetto. Spesso vengono dimenticati quando si desidera aggiungere un filtro in un secondo momento. Ogni campo viene dato come nome del campo stesso e con un alias del nome della tabella, di solito a, b, c e così via, ma può essere qualsiasi cosa si scelga purché sia coerente con il codice altrove.

```php
       public function __construct($config = array())
        {
            if (empty($config['filter_fields']))
            {
                $config['filter_fields'] = array(
                        'id', 'a.id',
                        'title', 'a.title',
                        'iso_2', 'a.iso_2',
                        'iso_3', 'a.iso_3',
                        'country_code', 'a.country_code',
                        'region_code', 'a.region_code',
                        'state', 'a.state',
                        'subregion_code', 'a.subregion_code',
                        'phone_prefix', 'a.phone_prefix',
                        'currency_code', 'a.currency_code',
                );
            }

            parent::__construct($config);
        }
```

### popolaStato

Questa funzione prende i parametri di input e li prepara per l'uso in una query di database. Alcuni parametri sono gestiti nel genitore, quindi non è necessario fare nulla qui. Per esempio, se il campo di ricerca è **titolo**, questo viene gestito dal genitore, così come i campi **stato** e di paginazione **inizio** e **limite**.

```php
       protected function populateState($ordering = 'title', $direction = 'ASC')
        {
            // List state information.
            parent::populateState($ordering, $direction);
        }
```

### getStoreId

Questa funzione crea un hash per memorizzare una query da utilizzare altrove.

```php
       protected function getStoreId($id = '')
        {
            // Compile the store id.
            $id .= ':' . $this->getState('filter.search');
            $id .= ':' . $this->getState('filter.published');

            return parent::getStoreId($id);
        }
```

### getListQuery

Qui è dove viene creata la query per estrarre dati dal database. Richiede una certa comprensione di come vengono costruite le query.

```php
    protected function getListQuery()
    {
        // Create a new query object.
        $db = $this->getDatabase();
        $query = $db->getQuery(true);

        // Select the required fields from the table.
        $query->select(
            $this->getState(
                'list.select',
                [
                    $db->quoteName('a.title'),
                    $db->quoteName('a.iso_2'),
                    $db->quoteName('a.iso_3'),
                    $db->quoteName('a.country_code'),
                    $db->quoteName('a.region_code'),
                    $db->quoteName('a.subregion_code'),
                    $db->quoteName('a.phone_prefix'),
                    $db->quoteName('a.currency_code'),
                    $db->quoteName('a.state'),
                    $db->quoteName('b.title') . ' AS currency_title',
                    $db->quoteName('b.symbol'),
                    $db->quoteName('b.dollar_exchange_rate'),
                ]
            )
        )
            ->from($db->quoteName('#__countrybase_countries', 'a'))
            ->leftjoin($db->quoteName('#__countrybase_currencies', 'b') . 'ON a.currency_code = b.currency_code');

        // Filter by search in title.
        $search = $this->getState('filter.search');

        if (!empty($search)) {
            $search = '%' . str_replace(' ', '%', trim($search) . '%');
            $query->where($db->quoteName('a.title') . ' LIKE :search')
            ->bind(':search', $search, ParameterType::STRING);
        }

        // Filter by published state
        $published = (string) $this->getState('filter.published');

        if ($published !== '*') {
            if (is_numeric($published)) {
                $state = (int) $published;
                $query->where($db->quoteName('a.state') . ' = :state')
                    ->bind(':state', $state, ParameterType::INTEGER);
            }
        }

        // Add the list ordering clause.
        $orderCol = $this->state->get('list.ordering', 'a.title');
        $orderDirn = $this->state->get('list.direction', 'ASC');

        $query->order($db->escape($orderCol) . ' ' . $db->escape($orderDirn));
        return $query;
    }
```

Spiegazione

- **getQuery(true)** ottiene un nuovo oggetto query vuoto.
- **\$query-\>select()** aggiunge un'istruzione SELECT. Possono esserci più istruzioni select - Joomla le concatena.
- **alias tabella a e b** notare che alcune colonne provengono da tabelle diverse.
- **-\>from()** definisce quale tabella è la tabella a. questo può essere in un'istruzione separata: \$query-\>from();
- **-\>leftjoin()** definisce la tabella b e come deve essere collegata alla tabella a.
- **\$query-\>where()** utilizza eventuali filtri definiti, uno per la **ricerca** e un altro per lo **stato**.
- **return \$query** non c'è chiamata parent, tutto nel query deve essere impostato qui.

## tmpl/paesi/default.php

Questa è la parte del codice in cui viene creato il contenuto HTML. Per l'elenco dei paesi è necessaria una tabella con una riga di intestazione e una riga per i dati su ciascun paese. Poiché ci sono 250 paesi, è necessario un meccanismo di paginazione per visualizzare un sottoinsieme di paesi pochi alla volta. Questo richiede un modulo. E in questo caso una barra standard **searchtools** di Joomla è utile. Ecco qui:

```php
<?php

/**
 * @package     Countrybase.Site
 * @subpackage  com_countrybase
 *
 * @copyright   (C) 2025 Clifford E Ford
 * @license     GNU General Public License version 3 or later; see LICENSE.txt
 */

// phpcs:disable PSR1.Files.SideEffects
\defined('_JEXEC') or die;
// phpcs:enable PSR1.Files.SideEffects

use Joomla\CMS\HTML\HTMLHelper;
use Joomla\CMS\Language\Text;
use Joomla\CMS\Layout\LayoutHelper;
use Joomla\CMS\Router\Route;

$listOrder = $this->escape($this->state->get('list.ordering'));
$listDirn  = $this->escape($this->state->get('list.direction'));

?>
<h1><?php echo Text::_('COM_COUNTRYBASE_COUNTRIES'); ?></h1>

<form action="<?php echo Route::_('index.php?option=com_countrybase'); ?>"
    method="post" name="adminForm" id="adminForm">

<?php echo LayoutHelper::render('joomla.searchtools.default', array('view' => $this)); ?>

<div class="table-responsive">
    <table class="table table-striped">
    <caption><?php echo Text::_('COM_COUNTRYBASE_COUNTRIES_TABLE_CAPTION'); ?></caption>
    <thead>
    <tr>
        <th scope="col">
            <?php echo HTMLHelper::_(
                'searchtools.sort',
                'COM_COUNTRYBASE_COUNTRIES_COUNTRY',
                'a.title',
                $listDirn,
                $listOrder
            ); ?>
        </th>
        <th scope="col"><?php echo Text::_('COM_COUNTRYBASE_COUNTRIES_ISO_2'); ?></th>
        <th scope="col"><?php echo Text::_('COM_COUNTRYBASE_COUNTRIES_ISO_3'); ?></th>
        <th scope="col"><?php echo Text::_('COM_COUNTRYBASE_COUNTRIES_CURRENCY_TITLE'); ?></th>
        <th scope="col"><?php echo Text::_('COM_COUNTRYBASE_COUNTRIES_CURRENCY_SYMBOL'); ?></th>
        <th scope="col"><?php echo Text::_('COM_COUNTRYBASE_COUNTRIES_CURRENCY_CODE'); ?></th>
        <th scope="col"><?php echo Text::_('COM_COUNTRYBASE_COUNTRIES_XRATE'); ?></th>
    </tr>
    </thead>
    <tbody>
    <?php foreach ($this->items as $id => $item) : ?>
    <tr>
        <td><?php echo $item->title; ?></td>
        <td><?php echo $item->iso_2; ?></td>
        <td><?php echo $item->iso_3; ?></td>
        <td><?php echo $item->currency_title; ?></td>
        <td><?php echo $item->symbol; ?></td>
        <td><?php echo $item->currency_code; ?></td>
        <td><?php echo $item->dollar_exchange_rate; ?></td>
    </tr>
    <?php endforeach; ?>
    </tbody>
    </table>
</div>

<?php echo $this->pagination->getListFooter(); ?>

<input type="hidden" name="task" value="">
<input type="hidden" name="boxchecked" value="0">
<?php echo HTMLHelper::_('form.token'); ?>

</form>
```

Punti da notare:

- **\$listOrder** e **\$listDirection** sono usati per ordinare per intestazione di colonna. Solo il titolo è stato impostato per farlo.
- **form action** è tipicamente impostato per riferirsi a se stesso.
- **LayoutHelper::render('joomla.searchtools.default',...)** crea una barra di ricerca del tipo visto nelle pagine di elenco dell'amministratore. **Ha bisogno di un modulo di filtro!**
- **\$this-\>pagination-\>getListFooter()** recupera il codice HTML per il widget di paginazione.
- **task** questo campo nascosto viene compilato da javascript quando il modulo viene inviato.
- **boxchecked** questo campo nascosto viene utilizzato quando una o più caselle di controllo delle righe sono selezionate per l'operazione batch. Non è veramente necessario qui!
- **HTMLHelper::\_('form.token');** ottiene il codice per un token di modulo utilizzato come dispositivo di sicurezza per l'invio di moduli che comportano l'invio di dati.

## tmpl/countries/default.xml

Questo file viene utilizzato per creare un elemento di menu. Ha lo stesso nome del file php, quindi default.xml in questo caso.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<metadata>
    <layout title="COM_COUNTRYBASE_VIEW_DEFAULT_MENU_LABEL"
        option="COM_COUNTRYBASE_VIEW_DEFAULT_OPTION">
        <help
            url="components/com_countrybase/help/en-GB/countrybase.html"
        />
        <message>
            <![CDATA[COM_COUNTRYBASE_VIEW_DEFAULT_MENU_DESC]]>
        </message>
    </layout>

    <!-- Add fields to the parameters object for the layout. -->
    <fields name="params">

        <!-- Options -->
        <fieldset name="options">
        </fieldset>

    </fields>
</metadata>
```

Note:

- **help url** punta a un file di aiuto nella cartella dell'amministratore. Ti consente di creare i tuoi file di aiuto locali, invocati dal pulsante Guida del modulo di modifica del menu dopo aver selezionato il tipo di menu Vista predefinita Countrybase.
- **params** ti permette di utilizzare parametri, ad esempio se mostrare o meno una particolare colonna nell'elenco dei paesi. Nessun parametro è stato ancora specificato.
- Le traduzioni di **key** devono essere nel file administrator/language/en-GB/countrybase.sys.ini. La chiave *COM_COUNTRYBASE_VIEW_DEFAULT_MENU_DESC*, tradotta in *Mostra una pagina Paesi.*, appare come descrittore nel modulo di selezione Tipo di voce del menu.

## forms/filter_countries.xml

Questo file è necessario per la barra di ricerca. Senza di esso, Joomla genererà un errore fatale. Il nome del file deve essere esattamente come mostrato: il nome della vista preceduto da filter\_. Il contenuto è semplice, solo definizioni per il campo di ricerca e qualsiasi altro filtro che si desidera utilizzare.

```xml
<?xml version="1.0" encoding="utf-8"?>
<form>
    <fields name="filter">
        <field
            name="search"
            type="text"
            label="COM_COUNTRYBASE_COUNTRIES_FILTER_SEARCH_LABEL"
            description="COM_COUNTRYBASE_COUNTRIES_FILTER_SEARCH_DESC"
            hint="JSEARCH_FILTER"
        />

        <field
            name="published"
            type="status"
            label="JOPTION_SELECT_PUBLISHED"
            onchange="this.form.submit();"
            >
            <option value="">JOPTION_SELECT_PUBLISHED</option>
        </field>

    </fields>

    <fields name="list">
        <field
            name="fullordering"
            type="list"
            label="JGLOBAL_SORT_BY"
            default="a.title ASC"
            onchange="this.form.submit();"
            >
            <option value="">JGLOBAL_SORT_BY</option>
            <option value="a.title ASC">COM_COUNTRYBASE_COUNTRIES_FILTER_COUNTRY_ASC</option>
            <option value="a.title DESC">COM_COUNTRYBASE_COUNTRIES_FILTER_COUNTRY_DESC</option>
            <option value="a.iso_2 ASC">ISO2 ASC</option>
            <option value="a.iso_2 DESC">ISO2 DESC</option>
            <option value="a.iso_3 ASC">ISO3 ASC</option>
            <option value="a.iso_3 DESC">ISO3 DESC</option>
            <option value="a.currency_code ASC">COM_COUNTRYBASE_COUNTRIES_FILTER_CURRENCY_CODE_ASC</option>
            <option value="a.currency_code DESC">COM_COUNTRYBASE_COUNTRIES_FILTER_CURRENCY_CODE_DESC</option>
            <option value="a.id ASC">JGRID_HEADING_ID_ASC</option>
            <option value="a.id DESC">JGRID_HEADING_ID_DESC</option>
        </field>

        <field
            name="limit"
            type="limitbox"
            label="JGLOBAL_LIST_LIMIT"
            default="25"
            onchange="this.form.submit();"
        />
    </fields>
</form>
```

Nota che qualsiasi chiave di stringa che inizia con J è definita da Joomla e non dovresti includerla nei tuoi file di lingua.

## language/it-IT/com_countrybase.ini

Joomla carica sempre le traduzioni delle chiavi della lingua inglese prima di qualsiasi altra lingua. Questo garantisce che le chiavi non appaiano nel risultato se una lingua è tradotta in modo incompleto. Poiché le chiavi della lingua sono parole lunghe in pseudo-inglese, si ritiene sia meglio avere una miscela di inglese e un'altra lingua piuttosto che una miscela di chiavi e un'altra lingua. Se un'altra lingua è in uso, Joomla sovrascrive le stringhe inglesi con quelle dell'altra lingua.

Nota che è prassi comune elencare le stringhe in ordine alfabetico delle chiavi:

```ini
    ; Joomla! Project
    ; (C) 2005 Open Source Matters, Inc. https://www.joomla.org
    ; License GNU General Public License version 2 or later; see LICENSE.txt
    ; Note : All ini files need to be saved as UTF-8

    COM_COUNTRYBASE_COUNTRIES_COUNTRY="Country"
    COM_COUNTRYBASE_COUNTRIES_CURRENCY_CODE="Code"
    COM_COUNTRYBASE_COUNTRIES_CURRENCY_SYMBOL="Symbol"
    COM_COUNTRYBASE_COUNTRIES_CURRENCY_TITLE="Currency"
    COM_COUNTRYBASE_COUNTRIES_FILTER_COUNTRY_ASC="Country ASC"
    COM_COUNTRYBASE_COUNTRIES_FILTER_COUNTRY_DESC="Country DESC"
    COM_COUNTRYBASE_COUNTRIES_FILTER_CURRENCY_CODE_ASC="Currency code ASC"
    COM_COUNTRYBASE_COUNTRIES_FILTER_CURRENCY_CODE_DESC="Currency code DESC"
    COM_COUNTRYBASE_COUNTRIES_FILTER_SEARCH_DESC="Search in Country Name"
    COM_COUNTRYBASE_COUNTRIES_FILTER_SEARCH_LABEL="Search"
    COM_COUNTRYBASE_COUNTRIES_ISO_2="ISO2"
    COM_COUNTRYBASE_COUNTRIES_ISO_3="ISO3"
    COM_COUNTRYBASE_COUNTRIES_TABLE_CAPTION="Table of Country Currencies"
    COM_COUNTRYBASE_COUNTRIES_XRATE="Exchange Rate"
    COM_COUNTRYBASE_COUNTRIES="Countries"
```

## src/Service/Router.php

Il Router è necessario per gli URL SEO. Senza di esso, un link di menu potrebbe apparire come option=com_countrybase&view=countries. Con esso, un link apparirà come country-base.html o qualunque nome tu scelga per l'alias del titolo del link.

```php
    public function __construct(
        SiteApplication $app,
        AbstractMenu $menu
    ) {

        $countries = new RouterViewConfiguration('countries');
        $countries->setKey('id');
        $this->registerView($countries);

        parent::__construct($app, $menu);

        $this->attachRule(new MenuRules($this));
        $this->attachRule(new StandardRules($this));
        $this->attachRule(new NomenuRules($this));
    }
```

Se ci sono più viste, ad esempio una tabella di valute, definiresti ogni vista qui prima dell'istruzione parent::\_\_construct().

*Tradotto da openai.com*

