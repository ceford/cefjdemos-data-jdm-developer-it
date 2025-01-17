<!-- Filename: J4.x:MVC_Anatomy:_Manifest_File / Display title: Anatomia MVC: File Manifesto -->

## Metadati

Il file manifest del componente deve essere nominato manifest.xml o componentname.xml, in questo caso countrybase.xml. Nota che la parte com_ non è inclusa. La prima parte del file contiene i metadati:

```xml
<?xml version="1.0" encoding="utf-8"?>
<extension type="component" method="upgrade">
    <name>com_countrybase</name>
    <author>Clifford E Ford</author>
    <authorEmail>john.doe@example.com</authorEmail>
    <authorUrl>example.com</authorUrl>
    <creationDate>2025-01-02</creationDate>
    <copyright>(C) 2025 Clifford E Ford</copyright>
    <license>GNU General Public License version 3 or later; see LICENSE.txt</license>
    <version>0.0.1</version>
    <description>COM_COUNTRYBASE_DESCRIPTION</description>
    <namespace path="src">Cefjdemos\Component\Countrybase</namespace>
```

La maggior parte dei metadati è autoesplicativa. Elementi da notare:

- Il tipo di estensione in questo caso è **componente**. Esistono altri tipi di estensioni, come modulo o plugin.
- Il metodo può essere install o upgrade. Quest'ultimo consente la reinstallazione dopo l'aggiornamento del codice.
- Il numero di versione è importante! Dovrebbe rendere impossibile reinstallare una versione precedente. E viene utilizzato per controllare se sono necessari aggiornamenti del database.
- Il percorso dello spazio dei nomi src ha tre parti:
  - La prima parte è un prefisso definito dal fornitore, quindi Joomla per il codice fornito da Joomla, Acme per il codice fornito dal fornitore di estensioni di terze parti Acme, e in questo caso Cefjdemos, un nome scelto per le dimostrazioni di codice Joomla.
  - La seconda parte indica il tipo di estensione. Potrebbe essere Componente o Modulo o Plugin o ...
  - La terza parte è il nome specifico dell'estensione, in questo caso Countrybase.

## Database

Il file manifesto definisce le posizioni di eventuali file sql di installazione, aggiornamento o rimozione. Questi file finiscono in una cartella sql nella cartella dell'amministratore.

```xml
    <install>
        <sql>
            <file driver="mysql" charset="utf8">sql/install.mysql.sql</file>
        </sql>
    </install>
    <uninstall>
        <sql>
            <file driver="mysql" charset="utf8">sql/uninstall.mysql.sql</file>
        </sql>
    </uninstall>
    <update>
        <schemas>
            <schemapath type="mysql">sql/updates/mysql</schemapath>
        </schemas>
    </update>
```

## File Script

Un file script può essere utilizzato per scopi di pre-volo o post-volo. Ad esempio, potrebbe essere usato per verificare i requisiti di sistema minimi prima dell'installazione o per impostare i parametri dopo l'installazione.

## File multimediali

Il componente com_countrybase non richiede alcun CSS o JavaScript specifico del componente, ma il codice per installarli è incluso per ogni evenienza. Le cartelle css e js contengono solo file index.html vuoti. Senza questi file le cartelle non vengono create.

```xml
    <scriptfile>script.php</scriptfile>

    <media destination="com_countrybase" folder="media">
        <file>joomla.asset.json</file>
        <folder>css</folder>
        <folder>js</folder>
    </media>
```

Nota che il file joomla.asset.json è utilizzato dal gestore delle risorse web, solitamente chiamato da un file di template.

## File del sito

Questi sono i file che vengono copiati su root/components/com_countrybase. Nota che la cartella della lingua viene copiata nella cartella del componente e non nella cartella root/language:

```xml
    <files folder="site">
        <folder>language</folder>
        <folder>forms</folder>
        <folder>src</folder>
        <folder>tmpl</folder>
    </files>
```

## File dell'Amministratore

Ci sono più file nella parte di amministrazione del file manifest perché ha più compiti da svolgere:

```xml
    <administration>
        <files folder="admin">
            <filename>access.xml</filename>
            <filename>config.xml</filename>
            <folder>forms</folder>
            <folder>help</folder>
            <folder>language</folder>
            <folder>layouts</folder>
            <folder>services</folder>
            <folder>sql</folder>
            <folder>src</folder>
            <folder>tmpl</folder>
        </files>
        <menu img="class:default">countrybase</menu>
        <submenu>
            <!--
                Note that all & must be escaped to &amp; for the file to be valid
                XML and be parsed by the installer
            -->
            <menu
                link="option=com_countrybase&amp;view=countries"
                img="default"
            >
                COM_COUNTRYBASE_COUNTRIES
            </menu>
            <menu
                link="option=com_countrybase&amp;view=currencies"
                img="default"
            >
                COM_COUNTRYBASE_CURRENCIES
            </menu>
        </submenu>
    </administration>
```

Nota il metodo per creare gli elementi del menu Amministratore di Joomla. C'è un elemento di menu che non ha un collegamento. E due elementi di menu che collegano alle due viste di amministrazione disponibili: l'elenco dei Paesi e l'elenco delle Valute. Inoltre, le traduzioni delle chiavi delle stringhe devono essere nel file com_countrybase.sys.ini.

## Registro modifiche

Il changelog viene utilizzato per tenere traccia delle modifiche apportate a ciascuna versione dell'estensione. Consulta l'articolo [Changelogs](jdocmanual?article=docus/install-update/installation-change-log) per informazioni sul contenuto del changelog.

```xml
    <changelogurl>https://raw.githubusercontent.com/ceford/cefjdemos-com-countrybase/master/changelog.xml</changelogurl>
```

## Aggiorna Server

Il codice del server di aggiornamento indica a Joomla dove trovare le informazioni sugli aggiornamenti. Viene eseguito a intervalli regolari per verificare se è disponibile un aggiornamento. Lascia fuori questa sezione se non stai utilizzando un server di aggiornamento per il tuo componente.

```xml
    <updateservers>
        <!-- Note: No spaces or linebreaks allowed between the server tags -->
        <server type="extension" name="Countrybase Update Site">https://raw.githubusercontent.com/ceford/cefjdemos-com-countrybase/master/updates.xml</server>
    </updateservers>
```

*Tradotto da openai.com*

