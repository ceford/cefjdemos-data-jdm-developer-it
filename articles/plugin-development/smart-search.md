<!-- Filename: Creating_a_Smart_Search_plug-in / Display title: Esempio: Ricerca Intelligente -->

## Introduzione

I plugin di Smart Search si trovano nel gruppo `finder` (in plugins/finder/xxxx). La codifica dei plugin finder è cambiata significativamente in Joomla 4 e 5. Per creare un nuovo plugin finder è probabilmente meglio copiare un plugin core esistente e modificarne il contenuto per adattarlo al suo nuovo scopo.

Questo articolo descrive un plugin finder progettato per supportare l'estensione *Jdocmanual*. Il contenuto da indicizzare si trova nella tabella `#__jdm_articles`. Il codice può essere trovato su [GitHub](https://github.com/ceford/cefjdemos-plg-finder-jdocmanual).

## Configurazione IDE - VSCode o VSCodium

Nel mio ambiente di sviluppo locale, il codice sorgente di questa estensione si trova in ~/git/cefjdemos-plg-jdm-finder. Il nome di questa cartella non ha alcun significato; è solo il mio modo di tenere in ordine le mie estensioni. La struttura schematica della cartella è la seguente:

```
cefjdemos-plg-finder-jdocmanual
|-- .vscode (folder for build settings)
|-- plg_finder_jdocmanual (folder compressed to create an installable zip file)
    |-- language/en-GB/ (language folder, kept with the extension code)
        |-- plg_finder_jdocmanual.ini
        |-- plg_finder_jdocmanual.sys.ini
    |-- services (folder for dependency injection)
        |-- provider.php (the DI code)
    |-- src (folder for namespaced classes)
        |-- Extension (folder for extension specific code)
            |-- Jdocmanual.php (the extension class code)
    |-- jdocmanual.xml (the manifest file)
|-- .gitignore (items not to include in the git repository)
|-- build.xml (instructions for building the extension with phing)
|-- LICENSE (the license statement)
|-- README.md (brief description and instructions on use)
```

In VSCodium appare così:

![Plugin development file structure in vscodium](../../../en/images/plugins/jdocmanual-vscodium.png)

## Personalizza il Codice

Avendo iniziato con un plugin di base per il finder, il primo compito è cambiare tutti i riferimenti al plugin originale con valori adatti per il nuovo plugin. In questo caso ci sono 63 istanze della parola `jdocmanual` in 7 file. C'è una buona possibilità che alcune vengano tralasciate al primo passaggio e il plugin non funzionerà.

## Costruire l'estensione

Ci sono due parti per la build. Ho un file build.xml che contiene istruzioni per [`phing`](https://www.phing.info/), uno strumento di build per progetti PHP. Può essere richiamato da VSCode/VSCodium o Eclipse o qualsiasi altro IDE.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project name="jdocmanual" basedir="." default="main">

    <property name="joomladir" value="/Users/ceford/public_html/jdm3"  override="true" />
    <property name="sitecomdir" value="${joomladir}/components" override="true" />
    <property name="admincomdir" value="${joomladir}/administrator/components" override="true" />
    <property name="adminmediadir" value="${joomladir}/media/com_jdocmanual" override="true" />
    <property name="plgdir" value="${joomladir}/plugins/finder/jdocmanual" override="true" />
    <property name="srcdir" value="${project.basedir}" override="true" />

    <property name="zipsdir" value="/Users/ceford/git/zips/cefjdemos"  override="true" />

    <!-- Fileset for plugin files -->
    <fileset dir="./plg_finder_jdocmanual" id="plgfiles">
        <include name="**" />
    </fileset>

    <!-- fileset for zip -->
    <fileset dir="./plg_finder_jdocmanual" id="plgfiles">
        <include name="**" />
    </fileset>

    <!-- ============================================  -->
    <!-- (DEFAULT) Target: main                        -->
    <!-- ============================================  -->
    <target name="main" description="main target">

        <copy todir="${plgdir}">
            <fileset refid="plgfiles" />
        </copy>

        <zip destfile="${zipsdir}/plg_finder_jdocmanual.zip">
            <fileset refid="plgfiles" />
        </zip>

    </target>
</project>
```

La seconda parte è un file `tasks.json` nella cartella .vscode. Indica a VSCode dove trovare il file phing.

```json
{
    // See https://go.microsoft.com/fwlink/?LinkId=733558
    // for the documentation about the tasks.json format
    "version": "2.0.0",
    "tasks": [
      {
        "label": "Build plg_finder_jdocmanual",
        "type": "shell",
        "command": "php ~/bin/phing-latest.phar",
        "windows": {
          "command": "php ~/bin/phing-latest.phar"
        },
        "group": "build",
        "presentation": {
          "reveal": "always",
          "panel": "shared"
        }
      }
    ]
}
```

In VSCode/VScodium seleziono **Terminale / Esegui attività di build...** dalla barra dei menu e seleziono l'attività appropriata.

## Installa l'estensione

Dopo la compilazione, il file zip dell'estensione deve essere installato nello stesso modo di qualsiasi altra estensione. Deve essere abilitato e devono essere impostate eventuali opzioni. Jdocmanual ha tre opzioni *Tassonomie da indicizzare*:

- **Manuale** uno o tutti i Manuali disponibili (Utente, Sviluppatore, ...)
- **Lingua** le ricerche sono limitate agli articoli nella stessa lingua della pagina.
- **Tipo** uno o tutti i tipi di contenuto (Jdocmanual, Contenuto, ...)

Nel caso del sito Jdocmanual, gli altri plugin di ricerca sono disabilitati perché non ci sono altri contenuti da indicizzare.

Dopo la prima installazione è normalmente sufficiente eseguire nuovamente il task di build dopo la correzione del codice. L'installazione del file zip è necessaria solo se ci sono modifiche al file manifest.xml.

## Indicizzare il contenuto

Jdocmanual è configurato per indicizzare i suoi articoli quando richiesto da un Super User. Questo è diverso dal normale plugin di Contenuto che indicizza il contenuto ogni volta che un articolo viene salvato. Una prima esecuzione richiede alcuni minuti per indicizzare i circa 5000 articoli di Jdocmanual in 8 lingue.

## Creare un Modulo di Ricerca Intelligente

Dalla sezione **Contenuti / Moduli del sito** seleziona **Nuovo** e installa un nuovo modulo **Ricerca Intelligente**. Regola le impostazioni per ottenere un aspetto adeguato.

## Testando

Alla fine, il tuo plugin di ricerca intelligente personalizzato dovrebbe funzionare. Questo è un esempio di pagina dei risultati per Jdocmanual che cerca un termine in questa pagina. La pagina dei risultati omette il modulo di ricerca dalla barra del titolo perché è presente nel corpo della pagina.

![Smart search result](../../../en/images/plugins/jdocmanual-search-result.png)

Un inciso: il plugin System - Joomla Accessibility Checker mostra che ci sono 3 errori relativi al modulo di inserimento dati *Search Terms*. È necessaria una correzione o un override nel core.

*Tradotto da openai.com*

