<!-- Filename: J4.x:MVC_Anatomy:_File_Structure / Display title: Anatomia MVC: Struttura dei File -->

## Configurazione dello Sviluppatore

Ci sono diversi modi per organizzare i file per scopi di sviluppo. Un metodo è utilizzare un clone di un repository GitHub come nella seguente struttura schematica:

```
cefjdemos-com-countrybase
|-- .vscode (folder for build settings)
|-- com_countrybase (folder compressed to create an installable zip file)
    |-- admin (the administrator files)
        |-- forms
        |-- help
            |-- countrybase.html (this is a Help screen used in the backend module edit form)
        |-- language
            |-- en-GB (language folder, kept with the extension code)
                |-- mod_downmsg.ini
                |-- mod_downmsg.sys.ini
        |-- services (folder for dependency injection)
            |-- provider.php (the DI code)
        |-- sql
            |-- updates
                |-- mysql
                    |-- index.html (an empty file required to avoid an installation error if there are no sql updates)
        |-- src (folder for namespaced classes)
            |-- more folders: Controller, Extension, Helper, Model, Table and View
        |-- tmpl (folder for layouts)
            |-- more folders: countries, country, currencies and currency
        |-- access.xml (standard list of access permissions)
        |-- config.xml (options parameters)
    |-- media
        |-- css (placeholder for CSS files - contains an empty index.html file)
        |-- js (placeholder for JavaScript files - contains an empty index.html file)
    |-- site (the site files, abbreviated here)
        |-- forms
        |-- language
        |-- src
        |-- tmpl
    |-- countrybase.xml (the manifest file)
    |-- script.php (a script to run on install, update or uninstall)
|-- .gitignore (items not to include in the git repository)
|-- build.xml (instructions for building the extension with phing)
|-- changelog.xml (record of changes)
|-- LICENSE (the license statement)
|-- README.md (brief description and instructions on use)
|-- updates.xml (update server specification)
```

Questa è la struttura nell'IDE VSCodium:

![Vscodium file structure view](../../../en/images/mvc-anatomy/com-countrybase-vscodium.png)

All'installazione, le parti del componente `com_countrybase` vengono distribuite in diverse posizioni nella struttura dei file di Joomla:
- I file dell'amministratore vanno in `root/administrator/components/com_countrybase`.
- I file del sito vanno in `root/components/com_countrybase`.
- I file multimediali, i file javascript e css (se presenti) vanno in `root/media/com_countrybase`.
- I file di lingua vanno nelle strutture del componente amministratore e sito. Una precedente convenzione li collocava nelle cartelle della lingua principale.

Solo dove vanno gli oggetti viene controllato dal file manifesto del componente, in questo caso countrybase.xml.

Nota che il file zip contiene tutto all'interno della cartella com_countrybase. Puoi creare un file zip semplicemente comprimendo quella cartella. Al di fuori di quella cartella ci sono build.xml, che è un file usato per costruire il componente ogni volta che viene apportata una modifica, e README.md, che è un file Markdown standard in formato Github che descrive il componente.

## Note

- Ci sono più di 40 file in questo semplice componente!
- Durante l'installazione il file countrybase.xml viene copiato in administrator/components/com_countrybase dove è necessario per gli aggiornamenti o per la disinstallazione.

*Tradotto da openai.com*

