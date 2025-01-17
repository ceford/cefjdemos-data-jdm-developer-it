<!-- Filename: J4.x:CLI_example_-_Onoffbydate / Display title: Esempio CLI - Onoffbydate -->

## Introduzione

Ci sono occasioni in cui un sito deve mostrare o nascondere un modulo a seconda della data. Un esempio potrebbe essere un modulo HTML personalizzato che visualizza un messaggio durante l'inverno. Un altro potrebbe essere l'alternanza di moduli personalizzati a seconda del giorno della settimana, ad esempio uno per i giorni feriali e un altro per i fine settimana. L'esempio presentato qui utilizza un plugin, un comando cli e un cron per ottenere l'effetto desiderato.

Il codice è disponibile su [GitHub](https://github.com/ceford/cefjdemos-plg-onoffbydate)

Ci sono più articoli sull'uso della CLI nel [Manuale utente](http://localhost/jdm4/jdocmanual?article=user/command-line-interface/using-the-cli) e nella Documentazione Joomla! Programmatori [copia locale](jdocmanual?article=docus/plugins/plugin-examples-console-plugin-sqlfile) o [origine originale](https://manual.joomla.org/docs/building-extensions/plugins/plugin-examples/console-plugin-sqlfile/);

## Standard di Joomla

Nelle versioni precedenti di Joomla, il sistema di plugin utilizzava un'implementazione del pattern Observable/Observer. Di conseguenza, ogni plugin caricato avrebbe registrato immediatamente tutti i suoi metodi pubblici come osservatori. Questo potrebbe causare problemi.

Joomla 4 e versioni successive utilizzano il pacchetto Joomla Framework Event per gestire gli Eventi dei plugin. Questo garantisce migliori prestazioni e sicurezza. In termini pratici, significa che la struttura dei file di un plugin Joomla 4/5/6 è diversa dalla struttura del plugin Legacy delle versioni precedenti.

## La Struttura del Plugin

Il plugin si chiama **onoffbydate**. Il seguente schema mostra la struttura dei file utilizzata per lo sviluppo locale del plugin:

```
cefjdemos-plg-onoffbydate
|-- .vscode (folder for build settings)
|-- cefjdemos-plg-onoffbydate (folder compressed to create an installable zip file)
    |-- language
        |-- en-GB (language folder, kept with the extension code)
            |-- plg_system_onoffbydate.ini
            |-- plg_system_onoffbydate.sys.ini
    |-- services (folder for dependency injection)
        |-- provider.php (the DI code)
    |-- src (folder for namespaced classes)
        |-- Console (folder for extension specific code)
            |-- OnoffbydateCommand.php (the plugin execution code)
        |-- Extension
            |-- Onoffbydate.php (the plugin register code)
    |-- onoffbydate.xml (the manifest file)
|-- .gitignore (items not to include in the git repository)
|-- build.xml (instructions for building the extension with phing)
|-- changelog.xml (a record of changes in each release)
|-- README.md (brief description and instructions on use)
|-- updates.xml (the update server specification)
```

## Il file manifesto onoffbydate.xml

Questo è il file di installazione - un elemento standard per qualsiasi estensione.

```xml
<?xml version="1.0" encoding="utf-8"?>
<extension type="plugin" group="console" method="upgrade">
    <name>plg_console_onoffbydate</name>
    <author>Clifford E Ford</author>
    <creationDate>Jamuary 2025</creationDate>
    <copyright>(C) Clifford E Ford</copyright>
    <license>GNU General Public License version 3 or later</license>
    <authorEmail>cliff@xxx.yyy.co.uk</authorEmail>
    <version>0.3.0</version>
    <description>PLG_CONSOLE_ONOFFBYDATE_DESCRIPTION</description>
    <namespace path="src">Cefjdemos\Plugin\Console\Onoffbydate</namespace>
    <files>
        <folder>language</folder>
        <folder plugin="onoffbydate">services</folder>
        <folder>src</folder>
    </files>
    <changelogurl>https://raw.githubusercontent.com/ceford/cefjdemos-plg-onoffbydate/main/changelog.xml</changelogurl>
    <updateservers>
        <!-- Note: No spaces or linebreaks allowed between the server tags -->
        <server type="extension" priority="2" name="Cefjdemosonoffbydate Update Site">https://raw.githubusercontent.com/ceford/cefjdemos-plg-onoffbydate/main/updates.xml</server>
    </updateservers>
    <config>
        <fields>

        </fields>
    </config>
</extension>
```

- La linea **namespace** indica a Joomla dove trovare il codice con namespace per questo plugin.
- La cartella **language** è mantenuta con il codice del plugin.
- Un **updateserver** è necessario per soddisfare i requisiti del JED.
- Non ci sono opzioni di **config** per questo plugin ma potrebbe essere modificato in futuro. Ad esempio, l'utente potrebbe preferire impostare i mesi invernali utilizzando caselle di controllo anziché averli codificati in modo fisso.

## Registrazione: services/provider.php

Questo è il punto di ingresso per il codice del plugin.

```php
<?php

/**
 * @package     Cefjdemos.Plugin
 * @subpackage  Console.Onoffbydate
 *
 * @copyright   Copyright (C) 2025 Clifford E Ford.
 * @license     GNU General Public License version 3 or later.
 */

// phpcs:disable PSR1.Files.SideEffects
\defined('_JEXEC') or die;
// phpcs:enable PSR1.Files.SideEffects

use Joomla\CMS\Extension\PluginInterface;
use Joomla\CMS\Plugin\PluginHelper;
use Joomla\DI\Container;
use Joomla\DI\ServiceProviderInterface;
use Joomla\CMS\Factory;
use Joomla\Event\DispatcherInterface;
use Cefjdemos\Plugin\Console\Onoffbydate\Extension\Onoffbydate;

return new class implements ServiceProviderInterface {
    /**
     * Registers the service provider with a DI container.
     *
     * @param   Container  $container  The DI container.
     *
     * @return  void
     *
     * @since   4.2.0
     */
    public function register(Container $container)
    {
        $container->set(
            PluginInterface::class,
            function (Container $container) {
                $dispatcher = $container->get(DispatcherInterface::class);
                $plugin     = new Onoffbydate(
                    $dispatcher,
                    (array) PluginHelper::getPlugin('console', 'onoffbydate')
                );
                $plugin->setApplication(Factory::getApplication());

                return $plugin;
            }
        );
    }
};
```

## Iscrizione all'evento: src/Extension/Onoffbydate.php

Questo è il luogo in cui viene registrato l'evento che attiva il plugin e viene impostata la posizione del codice che gestirà l'evento.

```php
<?php

/**
 * @package     Cefjdemos.Plugin
 * @subpackage  Console.Onoffbydate
 *
 * @copyright   Copyright (C) 2025 Clifford E Ford.
 * @license     GNU General Public License version 3 or later.
 */

namespace Cefjdemos\Plugin\Console\Onoffbydate\Extension;

// phpcs:disable PSR1.Files.SideEffects
\defined('_JEXEC') or die;
// phpcs:enable PSR1.Files.SideEffects

use Joomla\CMS\Plugin\CMSPlugin;
use Joomla\Event\SubscriberInterface;
use Cefjdemos\Plugin\Console\Onoffbydate\Console\OnoffbydateCommand;

final class Onoffbydate extends CMSPlugin implements SubscriberInterface
{
    /**
     * Returns the event this subscriber will listen to.
     *
     * @return  array
     */
    public static function getSubscribedEvents(): array
    {
        return [
                \Joomla\Application\ApplicationEvents::BEFORE_EXECUTE => 'registerCommands',
        ];
    }

    /**
     * Returns the command class for the Onoffbydate CLI plugin.
     *
     * @return  void
     */
    public function registerCommands(): void
    {
        $myCommand = new OnoffbydateCommand();
        $myCommand->setParams($this->params);
        $this->getApplication()->addCommand($myCommand);
    }
}
```

La classe **OnoffbydateCommand** si trova nella cartella *src/Console* poiché i comandi della Console integrata di Joomla si trovano in una cartella Console. Avrebbe potuto essere posizionata in una cartella *Extension*.

## Il File di Comando: src/Console/OnoffbydateCommand.php

Questo file contiene il codice che svolge tutto il lavoro per questa estensione.

```php
<?php

/**
 * @package     Cefjdemos.Plugin
 * @subpackage  Console.Onoffbydate
 *
 * @copyright   Copyright (C) 2025 Clifford E Ford.
 * @license     GNU General Public License version 3 or later.
 */

namespace Cefjdemos\Plugin\Console\Onoffbydate\Console;

// phpcs:disable PSR1.Files.SideEffects
\defined('_JEXEC') or die;
// phpcs:enable PSR1.Files.SideEffects

use Joomla\CMS\Factory;
use Joomla\CMS\Language\Text;
use Joomla\Console\Command\AbstractCommand;
use Joomla\Database\DatabaseInterface;
use Symfony\Component\Console\Input\InputArgument;
use Symfony\Component\Console\Input\InputInterface;
use Symfony\Component\Console\Output\OutputInterface;
use Symfony\Component\Console\Style\SymfonyStyle;
use Joomla\Database\DatabaseAwareTrait;

class OnoffbydateCommand extends AbstractCommand
{
    use DatabaseAwareTrait;

    /**
     * The default command name
     *
     * @var    string
     *
     * @since  4.0.0
     */
    protected static $defaultName = 'onoffbydate:action';

    /**
     * @var InputInterface
     * @since version
     */
    private $cliInput;

    /**
     * SymfonyStyle Object
     * @var SymfonyStyle
     * @since 4.0.0
     */
    private $ioStyle;

    /**
     * The params associated with the plugin, plus getter and setter
     * These are injected into this class by the plugin instance
     */
    protected $params;

    protected function getParams()
    {
        return $this->params;
    }

    public function setParams($params)
    {
        $this->params = $params;
    }

    /**
     * Initialise the command.
     *
     * @return  void
     *
     * @since   4.0.0
     */
    protected function configure(): void
    {
        $lang = Factory::getApplication()->getLanguage();
        $test = $lang->load(
            'plg_console_onoffbydate',
            JPATH_BASE . '/plugins/console/onoffbydate'
        );

        $this->addArgument(
            'season',
            InputArgument::REQUIRED,
            'winter or weekend'
        );
        $this->addArgument(
            'action',
            InputArgument::REQUIRED,
            'publish or unpublish'
        );

        $this->addArgument(
            'module_id',
            InputArgument::REQUIRED,
            'module id'
        );

        $help = Text::_('PLG_CONSOLE_ONOFFBYDATE_HELP_1');
        $help .= Text::_('PLG_CONSOLE_ONOFFBYDATE_HELP_2');
        $help .= Text::_('PLG_CONSOLE_ONOFFBYDATE_HELP_3');
        $help .= Text::_('PLG_CONSOLE_ONOFFBYDATE_HELP_4');
        $help .= Text::_('PLG_CONSOLE_ONOFFBYDATE_HELP_5');

        $this->setDescription(Text::_('PLG_CONSOLE_ONOFFBYDATE_DESCRIPTION'));
        $this->setHelp($help);
    }

    /**
     * Internal function to execute the command.
     *
     * @param   InputInterface   $input   The input to inject into the command.
     * @param   OutputInterface  $output  The output to inject into the command.
     *
     * @return  integer  The command exit code
     *
     * @since   4.0.0
     */
    protected function doExecute(InputInterface $input, OutputInterface $output): int
    {
        $this->configureIO($input, $output);

        $season = $this->cliInput->getArgument('season');
        $action = $this->cliInput->getArgument('action');
        $module_id = $this->cliInput->getArgument('module_id');

        switch ($season) {
            case 'winter':
                $result = $this->winter($module_id, $action);
                break;
            case 'weekend':
                $result = $this->weekend($module_id, $action);
                break;
            default:
                $result = Text::_('PLG_CONSOLE_ONOFFBYDATE_ERROR', $season);
                $this->ioStyle->error($result);
                return 0;
        }

        return 1;
    }

    protected function publish($module_id, $published)
    {
        $db = Factory::getContainer()->get(DatabaseInterface::class);
        //$db    = $this->getDatabase();
        $query = $db->getQuery(true);
        $query->update('#__modules')
            ->set('published = ' . $published)
            ->where('id = ' . $module_id);
        $db->setQuery($query);
        $db->execute();
    }

    protected function weekend($module_id, $action)
    {
        // get the day of the week
        $day = date('w');
        if (in_array($day, array(0,6))) {
            $msg = Text::_('PLG_CONSOLE_ONOFFBYDATE_TODAY_IS_IN_A_WEEKEND');
            $published = $action === 'publish' ? 1 : 0;
        } else {
            $msg = Text::_('PLG_CONSOLE_ONOFFBYDATE_TODAY_IS_NOT_IN_A_WEEKEND');
            $published = $action === 'publish' ? 0 : 1;
        }

        $this->publish($module_id, $published);

        $state = empty($published) ? Text::_('JUNPUBLISHED') : Text::_('JPUBLISHED');
        $result = Text::sprintf('PLG_CONSOLE_ONOFFBYDATE_SUCCESS', $msg, $module_id, $state);

        $this->ioStyle->success($result);
    }

    protected function winter($module_id, $action)
    {
        // get the month of the month
        $month = date('n');
        if (in_array($month, array(1,2,11,12))) {
            $msg = Text::_('PLG_CONSOLE_ONOFFBYDATE_TODAY_IS_IN_WINTER');
            $published = $action === 'publish' ? 1 : 0;
        } else {
            $msg = Text::_('PLG_CONSOLE_ONOFFBYDATE_TODAY_IS_NOT_IN_WINTER');
            $published = $action === 'publish' ? 0 : 1;
        }

        $this->publish($module_id, $published);

        $state = empty($published) ? Text::_('JUNPUBLISHED') : Text::_('JPUBLISHED');

        $state = empty($published) ? Text::_('JUNPUBLISHED') : Text::_('JPUBLISHED');
        $result = Text::sprintf('PLG_CONSOLE_ONOFFBYDATE_SUCCESS', $msg, $module_id, $state);

        $this->ioStyle->success($result);
    }

    /**
     * Configures the IO
     *
     * @param   InputInterface   $input   Console Input
     * @param   OutputInterface  $output  Console Output
     *
     * @return void
     *
     * @since 4.0.0
     *
     */
    private function configureIO(InputInterface $input, OutputInterface $output)
    {
        $this->cliInput = $input;
        $this->ioStyle = new SymfonyStyle($input, $output);
    }
}
```

- La funzione `configure` stabilisce che sono richiesti tre argomenti da riga di comando:
    - `season` deve essere uno tra `weekend` o `winter`.
    - `action` deve essere uno tra `publish` o `unpublish`
    - `module_id` deve essere l'ID intero del modulo da pubblicare o non pubblicare.
- La funzione `doExecute` è dove viene eseguito il lavoro. Sono riconosciute due opzioni di azione:
    - `winter` chiama una funzione per pubblicare o non pubblicare un modulo se oggi è nei mesi invernali.
    - `weekend` chiama una funzione per pubblicare o non pubblicare un modulo se oggi è un giorno del weekend.
- La funzione `publish` effettua una chiamata al database per impostare il campo `publishes` del modulo a `0` o `1` come appropriato.
- Le funzioni `winter` e `weekend` effettuano alcuni calcoli sulla data per determinare se oggi è in inverno (o meno) o in un weekend (o meno) per passare i parametri appropriati alla funzione di pubblicazione.
- La chiamata alla funzione `$this->ioStyle->success()` produce un messaggio di testo nella console con testo nero e sfondo verde. `$this->ioStyle->error()` produce un messaggio di ERRORE con testo bianco su sfondo marrone.

## file di lingua

Ci sono due file di lingua utilizzati durante l'installazione e la configurazione del plugin. Il file en-GB/plg_console_onoffbydate.sys.ini contiene le stringhe visualizzate durante l'installazione e la gestione:

```ini
PLG_CONSOLE_ONOFFBYDATE="Console - Onoffbydate"
PLG_CONSOLE_ONOFFBYDATE_DESCRIPTION="Set date-dependent enabled state of a module via cli"
```

Il file en-GB/plg_console_onoffbydate.ini contiene le stringhe in uso:

```ini
PLG_CONSOLE_ONOFFBYDATE="Console - Onoffbydate"
PLG_CONSOLE_ONOFFBYDATE_DESCRIPTION="Set date-dependent enabled state of a module via cli"
PLG_CONSOLE_ONOFFBYDATE_ERROR="Unknown season: %s."
PLG_CONSOLE_ONOFFBYDATE_HELP_1="<info>%command.name%</info> Toggles module Enabled/Disabled state\n"
PLG_CONSOLE_ONOFFBYDATE_HELP_2="Usage: <info>php %command.full_name% season action module_id where\n"
PLG_CONSOLE_ONOFFBYDATE_HELP_3="    season is one of winter or weekend,\n"
PLG_CONSOLE_ONOFFBYDATE_HELP_4="    action is one of publish or unpublish and\n"
PLG_CONSOLE_ONOFFBYDATE_HELP_5="    module_id is the id of the module to publish or unpublish.</info>\n"
PLG_CONSOLE_ONOFFBYDATE_SUCCESS="That seemed to work. %s Module %s has been %s."
PLG_CONSOLE_ONOFFBYDATE_TODAY_IS_IN_A_WEEKEND="Today is in a weekend."
PLG_CONSOLE_ONOFFBYDATE_TODAY_IS_IN_WINTER="Today is in winter."
PLG_CONSOLE_ONOFFBYDATE_TODAY_IS_NOT_IN_A_WEEKEND="Today is not in a weekend."
PLG_CONSOLE_ONOFFBYDATE_TODAY_IS_NOT_IN_WINTER="Today is not in winter."
```

Nota che l'output del comando è visibile solo a te sulla tua installazione di Joomla.

## Il Modulo

Questo codice modifica semplicemente lo stato pubblicato di un modulo a seconda di una funzione della data. Quindi hai bisogno dell'id del modulo come illustrato nella colonna di destra della pagina dell'elenco Moduli (Sito).

## La Riga di Comando

Installa il plugin nella tua installazione di test Joomla e abilitato. Se causa un arresto del sito, utilizza phpMyAdmin per trovare il plugin appena installato nella tabella #__extensions e imposta il suo parametro enabled su 0. Risolvi il problema e riprova.

In una finestra del terminale, cambia la directory alla radice del tuo sito ed usa il seguente comando:

```sh
php cli/joomla.php list
```

Se qualcosa va storto in questa fase, verifica che la versione PHP invocata sia quella della riga di comando e non quella utilizzata dal server web. Puoi sopprimere i messaggi di deprecazione con questa versione della riga di comando.

```sh
php -d error_reporting="E_ALL & ~E_DEPRECATED" cli/joomla.php onoffbydate:action garbage publish 133
```

Se il codice funziona vedrai `onoffbydate` tra l'elenco dei comandi disponibili e puoi invocare l'aiuto per vedere come deve essere utilizzato:

```sh
php cli/joomla.php onoffbydate:action --help
Usage:
  onoffbydate:action <season> <action> <module_id>

Arguments:
  season                       winter or summer or weekday or weekend
  action                       publish or unpublish
  module_id                    module id

Options:
  -h, --help                   Display the help information
  -q, --quiet                  Flag indicating that all output should be silenced
  -V, --version                Displays the application version
      --ansi                   Force ANSI output
      --no-ansi                Disable ANSI output
  -n, --no-interaction         Flag to disable interacting with the user
      --live-site[=LIVE-SITE]  The URL to your site, e.g. https://www.example.com
  -v|vv|vvv, --verbose         Increase the verbosity of messages: 1 for normal output, 2 for more verbose output and 3 for debug

Help:
  onoffbydate:action Toggles module Enabled/Disabled state
  Usage: php joomla.php onoffbydate:action season action module_id where
      season is one of winter or summer or weekday or weekend,
      action is one of publish or unpublish and
      module_id is the id of the module to publish or unpublish.
```

E poi provatelo:

```sh
php cli/joomla.php onoffbydate:action weekend publish 133

     [OK] That seemed to work. Today is not a weekend. Module 133 has been Unpublished
```

### In uso

Questa logica di utilizzo è un po' illogica! Se hai un modulo che dovrebbe essere pubblicato solo nei fine settimana, i parametri da usare ogni giorno sono `weekend publish module_id`. Questo pubblica il modulo nei giorni del fine settimana e lo depubblica nei giorni non del fine settimana. Per un modulo che deve essere pubblicato nei giorni feriali, i parametri da usare ogni giorno sono `weekend unpublish module_id`. Questo depubblica il modulo nei giorni del fine settimana e lo pubblica nei giorni non del fine settimana. La stessa logica si applica alla versione `winter`.

## Il cron

Il comando può essere testato in una finestra del terminale, ma probabilmente vorrai usarlo da un cron. L'opzione `winter` potrebbe essere eseguita il primo giorno di ogni mese. L'opzione `weekend` verrebbe eseguita quotidianamente. Il punto importante è che puoi avere quanti cron vuoi per cambiare lo stato pubblicato di quanti moduli desideri a qualsiasi intervallo appropriato. Lo stesso codice funziona per tutti.

Su un servizio di hosting, è necessario fornire i percorsi completi all'eseguibile php e al comando cli di joomla. Esempio:

```sh
/usr/local/bin/php /home/username/public_html/pathtojoomla/cli/joomla.php onoffbydate:action winter publish 130
```

A seconda di come hai configurato il tuo cron e il tuo sistema, potresti ricevere un'email rassicurante contenente esattamente le stesse informazioni che vedi nella riga di comando.

## Verifica

E naturalmente: vai alla tua pagina principale e verifica che il modulo sia stato effettivamente pubblicato o non pubblicato.

*Tradotto da openai.com*

