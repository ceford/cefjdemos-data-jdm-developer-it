<!-- Filename: How_to_use_JDate / Display title: Come utilizzare la classe Date -->

## Introduzione
La classe Date di Joomla è una classe di supporto, estesa dalla classe DateTime di PHP, che consente agli sviluppatori di gestire la formattazione delle date in modo più efficiente. La classe permette agli sviluppatori di formattare le date per stringhe leggibili, interazione con MySQL, calcolo dei timestamp UNIX, e fornisce anche metodi di supporto per lavorare in diversi fusi orari.

## Creare un'istanza di data

Tutti i metodi di aiuto per le date richiedono un'istanza della classe Date. Per iniziare, devi crearne una. Un oggetto Date può essere creato in due modi. Uno è il tipico metodo nativo di semplicemente creare una nuova istanza:

```php
use Joomla\CMS\Date\Date;

$date = new Date(); // Creates a new Date object equal to the current time.
```

Puoi anche creare un'istanza utilizzando il metodo statico definito in Date:

```php
use Joomla\CMS\Date\Date;

$date = Date::getInstance(); // Alias of 'new Date();'
```

Non c'è alcuna differenza tra questi metodi, poiché Date::getInstance crea semplicemente una nuova istanza di Date esattamente come il primo metodo mostrato.

Alternativamente, puoi anche recuperare la data corrente (come oggetto Date) dall'oggetto Application, utilizzando:
```php
use Joomla\CMS\Factory;

$date = Factory::getDate();
```

## Argomenti

Il costruttore Date (e il metodo statico getInstance) accetta due parametri opzionali: una stringa di data da formattare e un fuso orario. Non passare una stringa di data creerà un oggetto Date con la data e l'ora correnti, mentre non passare un fuso orario permetterà all'oggetto Date di utilizzare il fuso orario predefinito impostato.

Il primo argomento, se utilizzato, dovrebbe essere una stringa che può essere analizzata utilizzando il costruttore DateTime nativo di PHP. Ad esempio:
```php
use Joomla\CMS\Date\Date;

$currentTime = new Date('now'); // Current date and time
$tomorrowTime = new Date('now +1 day'); // Current date and time, + 1 day.
$plus1MonthTime = new Date('now +1 month'); // Current date and time, + 1 month.
$plus1YearTime = new Date('now +1 year'); // Current date and time, + 1 year.
$plus1YearAnd1MonthTime = new Date('now +1 year +1 month'); // Current date and time, + 1 year and 1 month.
$plusTimeToTime = new Date('now +1 hour +30 minutes +3 seconds'); // Current date and time, + 1 hour, 30 minutes and 3 seconds
$plusTimeToTime = new Date('now -1 hour +30 minutes +3 seconds'); // Current date and time, + 1 hour, 30 minutes and 3 seconds
$combinedTimeToTime = new Date('now -1 hour -30 minutes 23 seconds'); // Current date and time, - 1 hour, +30 minutes and +23 seconds

$date = new Date('2012-12-1 15:20:00'); // 3:20 PM, December 1st, 2012
```

Un timestamp Unix (in secondi) può anche essere passato come primo argomento, nel qual caso sarà internamente convertito in una data. Se un fuso orario è stato specificato come secondo argomento al costruttore, verrà convertito in quel fuso orario.

## Visualizzare le date

Una nota di cautela quando si emettono oggetti Date in un contesto utente: non stamparli semplicemente sullo schermo. Il metodo toString() dell'oggetto Date chiama semplicemente il metodo format() del suo genitore, senza considerazione per i fusi orari o la formattazione delle date localizzata. Questo non risulterà in una buona esperienza utente e porterà a incoerenze tra la formattazione nella tua estensione e altrove in Joomla. Invece, dovresti sempre emettere Date utilizzando i metodi mostrati di seguito.

### Formati di data comuni

Un certo numero di formati di data sono predefiniti in Joomla come parte dei pacchetti lingua di base. Ciò è vantaggioso perché significa che i formati di data possono essere facilmente internazionalizzati. Un esempio delle stringhe di formato disponibili è riportato di seguito, dal pacchetto lingua en-GB. Si raccomanda vivamente di utilizzare queste stringhe di formattazione quando si visualizzano date, in modo che le date vengano automaticamente riformattate in base alla località di un utente. Possono essere recuperate nello stesso modo di qualsiasi stringa di lingua (vedere gli esempi di seguito).

```ini
DATE_FORMAT_LC="l, d F Y"
DATE_FORMAT_LC1="l, d F Y"
DATE_FORMAT_LC2="l, d F Y H:i"
DATE_FORMAT_LC3="d F Y"
DATE_FORMAT_LC4="Y-m-d"
DATE_FORMAT_LC5="Y-m-d H:i"
DATE_FORMAT_LC6="Y-m-d H:i:s"
DATE_FORMAT_JS1="y-m-d"
DATE_FORMAT_CALENDAR_DATE="%Y-%m-%d"
DATE_FORMAT_CALENDAR_DATETIME="%Y-%m-%d %H:%M:%S"
DATE_FORMAT_FILTER_DATE="Y-m-d"
DATE_FORMAT_FILTER_DATETIME="Y-m-d H:i:s"
```

### Il Metodo HtmlHelper (Consigliato)

Come con molti elementi di output comuni, la classe HtmlHelper è qui per... aiutare! Il metodo date() di HtmlHelper accetterà qualsiasi stringa di data e ora che il costruttore Date accetterebbe, insieme a una stringa di formattazione, e mostrerà la data in modo appropriato in base alle impostazioni del fuso orario dell'utente corrente. Pertanto, questo è il metodo consigliato per mostrare date all'utente.

```php
use Joomla\CMS\HTML\HTMLHelper;
use Joomla\CMS\Language\Text;

$myDateString = '2012-12-1 15:20:00';
echo HtmlHelper::date($myDateString, Text::_('DATE_FORMAT_FILTER_DATETIME'));
```

### Il metodo format() dell'oggetto Date

Un'altra opzione è formattare manualmente la Data. Se viene utilizzato questo metodo, dovrai anche recuperare e impostare manualmente il fuso orario dell'utente. Questo metodo è più utile per formattare le date al di fuori dell'interfaccia utente, come nei registri di sistema o nelle chiamate API.

```php
use Joomla\CMS\Language\Text;
use Joomla\CMS\Date\Date;
use Joomla\CMS\Factory;

$myDateString = '2012-12-1 15:20:00';
$timezone = Factory::getUser()->getTimezone();

$date = new Date($myDateString);
$date->setTimezone($timezone);
echo $date->format(Text::_('DATE_FORMAT_FILTER_DATETIME'));
```

## Altri Esempi di Codice Utili

### Visualizzare rapidamente l'ora corrente

Ci sono due modi semplici per farlo.
- Il metodo date() di HtmlHelper, se non viene fornito alcun valore di data, assumerà come predefinito l'ora corrente.
- Factory::getDate() ottiene la data corrente come un oggetto Date, che possiamo poi formattare.

```php
use Joomla\CMS\Factory;
use Joomla\CMS\HTML\HTMLHelper;
use Joomla\CMS\Language\Text;

// These two are functionally equivalent
echo HtmlHelper::date('now', Text::_('DATE_FORMAT_FILTER_DATETIME'));

$timezone = Factory::getUser()->getTimezone();
echo Factory::getDate()->setTimezone($timezone)->format(Text::_('DATE_FORMAT_FILTER_DATETIME'));
```

### Aggiungere e sottrarre dalle date

Poiché l'oggetto Data di Joomla estende l'oggetto DateTime di PHP, esso fornisce metodi per aggiungere e sottrarre date. Il più semplice di questi metodi da utilizzare è il metodo modify(), che accetta qualsiasi stringa di modifica relativa che il metodo PHP [strtotime](https://www.php.net/manual/en/function.strtotime.php) accetterebbe. Ad esempio:

```php
use Joomla\CMS\Date\Date;

$date = new Date('2012-12-1 15:20:00');
$date->modify('+1 year');
echo $date->toSQL(); // 2013-12-01 15:20:00
```

Ci sono anche metodi separati add() e sub(), per aggiungere o sottrarre tempo da un oggetto data rispettivamente. Questi accettano oggetti [DateInterval](https://www.php.net/manual/en/class.dateinterval.php) standard PHP:

```php
use Joomla\CMS\Date\Date;

$interval = new \DateInterval('P1Y1D'); // Interval represents 1 year and 1 day

$date1 = new Date('2012-12-1 15:20:00');
$date1->add($interval);
echo $date1->toSQL(); // 2013-12-02 15:20:00

$date2 = new Date('2012-12-1 15:20:00');
$date2->sub($interval);
echo $date2->toSQL(); // 2011-11-30 15:20:00
```

### Visualizzazione delle date in formato ISO 8601

```php
$date = new Date('2012-12-1 15:20:00');
$date->toISO8601(); // 20121201T152000Z
```

### Uscita delle date nel formato RFC 822

```php
$date = new Date('2012-12-1 15:20:00');
$date->toRFC822(); // Sat, 01 Dec 2012 15:20:00 +0000
```

### Restituire Date nel Formato Data-Ora SQL

```php
$date = new Date('20121201T152000Z');
$date->toSQL(); // 2012-12-01 15:20:00
```

### Produrre date come Unix Timestamp

Un timestamp Unix è espresso come il numero di secondi trascorsi dall'Epoch Unix (il primo secondo del 1° gennaio 1970).

*Tradotto da openai.com*

