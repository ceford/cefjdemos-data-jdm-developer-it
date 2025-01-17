<!-- Filename: J4.x:MVC_Anatomy:_Administrator_Edit_Files / Display title: Anatomia MVC: Modifica File Amministratore -->

## File di Dati del Paese

I file dell'amministratore includono quattro visualizzazioni, due visualizzazioni elenco per i dati dei paesi e i dati delle valute e due visualizzazioni di modifica per gestire l'immissione dei dati in ognuna delle due tabelle coinvolte. Le visualizzazioni elenco sono quasi identiche alla visualizzazione elenco dei paesi descritta per l'interfaccia del sito, quindi non verranno trattate nuovamente qui. Analogamente, le visualizzazioni di modifica sono quasi identiche, quindi ne verrà trattata solo una, la visualizzazione di immissione dati per un singolo paese.

## src/Controller/CountryController.php

Questo è estremamente semplice! A parte la dichiarazione della classe, è privo di contenuto. Tutto è gestito dalla classe madre.

```php
    class CountryController extends FormController
    {
    }
```

## src/View/Paese/HtmlView.php

Questo è il punto in cui i dati vengono recuperati dal modello per essere utilizzati nel modulo di inserimento dati. C'è una differenza significativa rispetto alla visualizzazione elenco descritta in precedenza: è prassi comune utilizzare una barra degli strumenti con pulsanti come Salva, Annulla, Aiuto, eccetera.

Quando si richiama il modulo di modifica selezionando il titolo di un elemento della lista, l'url contiene un id, ad esempio option=com_countrybase&view=country&layout=edit&id=1. L'id è il numero di record della tabella. Per un nuovo record richiamato tramite il pulsante Nuovo elenco l'id è assente. Se è presente, il modello compila il modulo di inserimento dati con i dati del record esistente.

```php
    public function display($tpl = null)
    {
        $this->form  = $this->get('Form');
        $this->item  = $this->get('Item');
        $this->state = $this->get('State');

        if (count($errors = $this->get('Errors')))
        {
            throw new GenericDataException(implode("\n", $errors), 500);
        }

        $this->addToolbar();

        return parent::display($tpl);
    }
```

### La Barra degli Strumenti

La funzione addToolbar() viene tipicamente utilizzata per impostare il titolo della pagina e aggiungere i pulsanti appropriati per i permessi di accesso della persona che utilizza il modulo. Nota l'uso della variabile \$isNew basata sull'id del record per modificare leggermente l'output.

```php
    protected function addToolbar()
    {
        Factory::getApplication()->input->set('hidemainmenu', true);
        $isNew      = ($this->item->id == 0);

        $canDo = ContentHelper::getActions('com_countrybase');

        $toolbar = Toolbar::getInstance();

        ToolbarHelper::title(
            Text::_('COM_COUNTRYBASE_COUNTRY_PAGE_TITLE_' . ($isNew ? 'ADD' : 'EDIT'))
        );

        if ($canDo->get('core.create')) {
            if ($isNew) {
                $toolbar->apply('country.save');
            } else {
                $toolbar->apply('country.apply');
            }
            $toolbar->save('country.save');
        }
        $toolbar->cancel('country.cancel', 'JTOOLBAR_CLOSE');

        ToolbarHelper::inlinehelp();
    }
```

**Note:**

- **hidemainmenu** è impostato su true per tutti i moduli di modifica per evitare di lasciare il modulo tramite il menu dell'Amministratore senza salvare.
- **ToolbarHelper::title()** imposta il titolo nella barra del titolo della pagina, in questo caso a Modifica Paese o Aggiungi Paese.
- I pulsanti **toolbar-\>action**, dove action può essere salva, applica, annulla o uno dei molti altri, prendono come argomenti (controller.funzione). Quindi, in questo caso, quando un pulsante è selezionato, action viene passato a una funzione di salvataggio o applicazione nella classe CountryController.
- **cancel** prende un argomento aggiuntivo, la chiave stringa usata per etichettare il pulsante.
- **inlinehelp()** mostra un pulsante che attiva o disattiva le descrizioni dei campi sotto ogni campo di inserimento dati.

## forms/country.xml

Questo file contiene la specifica dei campi del modulo, solitamente nell'ordine presentato nel modulo di modifica. La maggior parte dei campi è autoesplicativa, quindi ne vengono mostrati solo due di seguito. I valori dei nomi sono i nomi delle colonne utilizzati nelle tabelle del database.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<form>
        <field
            name="title"
            type="text"
            label="COM_COUNTRYBASE_COUNTRY_TITLE"
            required="true"
            maxlength="128"
        />

        <field
            name="iso_2"
            type="text"
            label="COM_COUNTRYBASE_COUNTRY_ISO_2"
            description="COM_COUNTRYBASE_COUNTRY_ISO_2_DESC"
            required="true"
            maxlength="3"
        />
```

## src/Model/CountryModel.php

Le funzioni in questo file sono piuttosto standard. Tuttavia, la funzione getTable() richiede alcune spiegazioni.

```php
    public function getTable($name = '', $prefix = '', $options = array())
    {
        $name = 'Countries';
        $prefix = 'Table';

        if ($table = $this->_createTable($name, $prefix, $options)) {
            return $table;
        }

        throw new \Exception(Text::sprintf('JLIB_APPLICATION_ERROR_TABLE_NAME_NOT_SUPPORTED', $name), 0);
    }
```

Questa funzione non si riferisce alla tabella stessa! Si riferisce al costruttore di src/Table/CountriesTable.php. Questo può essere un po' confuso perché viene chiamata dalla classe CountryModel.

## src/Table/CountriesTable.php

Quindi questo è il punto in cui è definito il nome della tabella per l'elenco dei paesi.

```php
    class CountriesTable extends Table
    {
        /**
         * Constructor
         *
         * @param   DatabaseDriver  $db  Database connector object
         *
         * @since   1.6
         */
        public function __construct(DatabaseDriver $db)
        {
            parent::__construct('#__countrybase_countries', 'id', $db);

            $this->setColumnAlias('published', 'state');
        }
    }
```

Avviso la dichiarazione dell'alias della colonna. Questo è utilizzato perché il modulo usa un campo di inserimento dati denominato **published**, ma il campo utilizzato per l'archiviazione è denominato **status**.

## tmpl/country/edit.php

Questo è il file che crea l'output HTML. Inizia con due helper: HTMLHelper::_('behavior.formvalidator'); carica il javascript necessario per la validazione del modulo lato client. Anche se i browser moderni applicano la validazione del modulo, ciò non impedisce l'invio del modulo. HTMLHelper::_('behavior.keepalive'); carica il javascript per inviare ping al server per prevenire la scadenza della sessione durante la compilazione di moduli complessi.

**Note:**

- LayoutHelper::render('joomla.edit.title_alias', \$this); rende un campo titolo standard di Joomla.
- \$this-\>form-\>renderField('iso_2'); rende il campo specificato, in questo caso iso_2.
- LayoutHelper::render('joomla.edit.global', \$this); rende i campi sul lato destro della scheda Dettagli.

```php
<?php

/**
 * @package     Countrybase.Administrator
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

HTMLHelper::_('behavior.formvalidator');
HTMLHelper::_('behavior.keepalive');

?>

<form action="<?php echo Route::_('index.php?option=com_countrybase&view=country&layout=edit&id=' .
        (int) $this->item->id); ?>"
    method="post" name="adminForm" id="country-form" class="form-validate">

    <?php echo LayoutHelper::render('joomla.edit.title_alias', $this); ?>

    <div>
        <?php echo HTMLHelper::_('uitab.startTabSet', 'myTab', array('active' => 'details')); ?>

        <?php echo HTMLHelper::_('uitab.addTab', 'myTab', 'details', Text::_('COM_COUNTRYBASE_COUNTRY_TAB_DETAILS')); ?>
        <div class="row">
            <div class="col-md-9">
                <div class="row">
                    <div class="col-md-6">
                        <?php echo $this->form->renderField('iso_2'); ?>
                        <?php echo $this->form->renderField('iso_3'); ?>
                        <?php echo $this->form->renderField('country_code'); ?>
                        <?php echo $this->form->renderField('region_code'); ?>
                        <?php echo $this->form->renderField('subregion_code'); ?>
                        <?php echo $this->form->renderField('phone_prefix'); ?>
                        <?php echo $this->form->renderField('currency_code'); ?>
                        <?php echo $this->form->renderField('id'); ?>
                    </div>
                </div>
            </div>
            <div class="col-md-3">
                <div class="card card-light">
                    <div class="card-body">
                        <?php echo LayoutHelper::render('joomla.edit.global', $this); ?>
                    </div>
                </div>
            </div>
        </div>
        <?php echo HTMLHelper::_('uitab.endTab'); ?>

        <?php echo HTMLHelper::_('uitab.endTabSet'); ?>
    </div>
    <input type="hidden" name="task" value="">
    <?php echo HTMLHelper::_('form.token'); ?>
</form>
```

Puoi scorrere tra i fieldset del modulo e i campi all'interno di ciascun fieldset. Ciò può semplificare l'output di moduli complessi con molte schede.

![country edit form](../../../en/images/mvc-anatomy/com-countrybase-edit-country.png)

*Tradotto da openai.com*

