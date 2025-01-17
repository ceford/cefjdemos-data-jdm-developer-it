<!-- Filename: https://docs.joomla.org/Package / Display title: Pacchetti -->

## Introduzione ai pacchetti

A volte un modulo (o un plugin o un'altra estensione) utilizza i modelli o gli helper di un componente. In questi casi è meglio essere in grado di installare o disinstallare un modulo dipendente quando il componente stesso viene installato o disinstallato. In Joomla, questa funzionalità viene realizzata con un pacchetto, anche se l'uso dei pacchetti non è infallibile.

Un pacchetto è un'estensione utilizzata per installare più estensioni contemporaneamente. Combinarle in un pacchetto permette all'utente di installare e disinstallare due o più estensioni in un'unica operazione.

## Creazione del Pacchetto

Un pacchetto viene creato comprimendo tutti i singoli file di estensione `.zip` insieme a un file manifesto `.xml`. Ad esempio, per un pacchetto composto da:

* **componente** helloworld
* **modulo** helloworld
* **libreria** helloworld
* **plugin di sistema** helloworld
* **modello** helloworld

Il pacchetto avrebbe la seguente struttura nel file zip:

```sh
  -- pkg_helloworld.xml
  -- packages <dir>
      |-- com_helloworld.zip
      |-- mod_helloworld.zip
      |-- lib_helloworld.zip
      |-- plg_sys_helloworld.zip
      |-- tpl_helloworld.zip
  -- pkg_script.php
```

Il `pkg_helloworld.xml` potrebbe avere i seguenti contenuti:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<extension type="package" method="upgrade">
<name>Hello World Package</name>
<author>Hello World Package Team</author>
<creationDate>May 2022</creationDate>
<packagename>helloworld</packagename>
<version>1.0.0</version>
<url>http://www.yoururl.com/</url>
<packager>Hello World Package Team</packager>
<packagerurl>http://www.yoururl.com/</packagerurl>
<description>Example package to combine multiple extensions</description>
<update>http://www.updateurl.com/update</update>
<scriptfile>pkg_script.php</scriptfile>
<blockChildUninstall>true</blockChildUninstall>
<files folder="packages">
    <file type="component" id="com_helloworld">com_helloworld.zip</file>
    <file type="module" id="helloworld" client="site">mod_helloworld.zip</file>
    <file type="library" id="helloworld">lib_helloworld.zip</file>
    <file type="plugin" id="helloworld" group="system">plg_sys_helloworld.zip</file>
    <file type="template" id="helloworld" client="site">tpl_helloworld.zip</file>
</files>
</extension>
```

Quando compresso e installato, il pacchetto sarà visibile nell'elenco delle estensioni, in modo che un utente possa disinstallare tutte le estensioni contenute nel pacchetto.

Ricorda di utilizzare il disinstallatore del pacchetto invece dei singoli disinstallatori di sottopacchetti per evitare voci di estensioni orfane nel gestore delle estensioni. Questa è la parte che non è a prova di errore!

### ID del file

L'elemento id nel tag `<file ..>` **non** è arbitrario! L'`id=` dovrebbe essere impostato al valore della colonna `element` nella tabella `#__extensions`. Se non sono impostati correttamente, durante la disinstallazione del pacchetto, il `file` figlio **non** verrà trovato e disinstallato.

### Nome del file manifest e nome del pacchetto

Il nome del file manifesto e la capacità di disinstallare il file del pacchetto stesso sono strettamente correlati. Il file manifesto deve avere un prefisso **pkg_**. Il resto del nome del manifesto (senza l'estensione **.xml**) deve essere utilizzato come `<packagename>`. Oppure, al contrario, un pacchetto che desideri identificare come **blurpblurp_J3** ottiene tale identificativo come suo `<packagename>` e deve essere in un file manifesto chiamato **pkg_blurpblurp_J3.xml**. In caso contrario, sarà impossibile disinstallare il pacchetto stesso.

Un opzionale `<pkg_script.php>` che contiene una classe `pkg_<packagename>InstallerScript` con la funzione pubblica **postflight** può essere utilizzato.

### Tag di Estensione

Il tag `<extension>` deve includere `method="upgrade"` affinché un aggiornamento del pacchetto abbia successo nelle installazioni successive.

### Dipendenza per la Disinstallazione dell'Estensione

Un'estensione del pacchetto può dichiarare che i suoi elementi figli non possono essere disinstallati indipendentemente con un elemento `<blockChildUninstall>true</blockChildUninstall>` nel manifesto del pacchetto. Se il tuo pacchetto ha bisogno che tutte le sue estensioni funzionino efficacemente, imposta questo valore su true o 1.

*Tradotto da openai.com*

