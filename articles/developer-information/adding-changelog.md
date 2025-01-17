<!-- Filename: Adding_changelog_to_your_manifest_file / Display title: Aggiunta di un Registro delle Modifiche -->

Dalla versione 4.0 di Joomla, gli sviluppatori di estensioni possono sfruttare la capacità di Joomla di leggere un file changelog e fornire una rappresentazione visiva del changelog. Se una determinata versione non è presente nel changelog, il pulsante del changelog non verrà mostrato.

Le modifiche in una versione saranno presentate in questo modo:

![changelog modal view](../../../en/images/developer-information/adding-changelog-example-1.png)

Il changelog è utilizzato in due diversi luoghi.

## Aggiorna Vista

L'installatore mostrerà il changelog della versione che può essere installata se disponibile.

![changelog installer view](../../../en/images/developer-information/adding-changelog-update-view.png)

Facendo clic sul pulsante Changelog qui, verrà mostrato il changelog della nuova versione disponibile.

## Gestisci Visualizzazione

Il gestore delle estensioni mostrerà il registro delle modifiche dell'estensione attualmente installata, se disponibile.

![changelog installer view](../../../en/images/developer-information/adding-changelog-extension-view.png)

Facendo clic sul numero di versione qui verrà visualizzato il changelog della versione attualmente installata.

## Aggiungere il tag changelogurl ai file di manifest

Il primo passo è aggiornare i file manifest che indicano a Joomla dove trovare i dettagli del changelog. Aggiungi il seguente nodo ai tuoi file XML manifest:

```
<changelogurl>https://example.com/updates/changelog.xml</changelogurl>
```

Si prega di notare: l'URL nel tag changelogurl non deve avere spazi o interruzioni di riga prima o dopo di esso. Vedere gli esempi di codice.

### Aggiorna il manifesto del server

Vedi questo esempio di un file manifesto del server di aggiornamento che informa Joomla su un aggiornamento di un componente chiamato "com_lists". In questo modo vedrai il pulsante del Registro delle modifiche nella vista di aggiornamento.

```
<?xml version="1.0" encoding="utf-8"?>
<updates>
 <update>
  <name>Student List</name>
  <description>List of students</description>
  <element>com_lists</element>
  <type>component</type>
  <version>4.0.0</version>

  <changelogurl>https://example.com/updates/changelog.xml</changelogurl>

  <tags>
   <tag>stable</tag>
  </tags>
  <maintainer>Example Miller</maintainer>
  <maintainerurl>https://example.com/</maintainerurl>
  <section>Updates</section>
  <targetplatform name="joomla" version="4.?" />
  <client>1</client>
  <folder></folder>
 </update>
</updates>
```

### Manifesto dell'estensione

Inoltre, aggiungi il tag changelogurl al file manifest XML dell'estensione. In questo modo, la versione dell'estensione sarà collegata ai registri delle modifiche nella vista di gestione.

```
<?xml version="1.0" encoding="utf-8"?>
<extension type="component" method="upgrade">
    <name>COM_LISTS</name>

... Other stuff ...

    <changelogurl>https://example.com/updates/changelog.xml</changelogurl>

    <updateservers>
        <server type="extension" name="My Extension's Updates">https://example.com/lists-updates.xml</server>
    </updateservers>
</extension>
```

## Crea file changelog

Il file changelog deve avere i seguenti 3 nodi:

* elemento
* tipo
* versione

Queste informazioni vengono utilizzate per identificare il changelog corretto per una determinata estensione.

Un nodo di versione all'interno di qualsiasi nodo di changelog è sempre obbligatorio. In caso contrario, vedrai un messaggio di errore come SyntaxError: JSON.parse: carattere inaspettato a riga 1 colonna 1 dei dati JSON.

```
<element>com_lists</element>
<type>component</type>
<version>4.0.0</version>
```

Ulteriormente, il changelog è popolato con uno o più tipi di modifiche. I seguenti tipi di modifiche sono supportati:

* sicurezza: Qualsiasi problema di sicurezza che è stato risolto
* correzione: Qualsiasi bug che è stato corretto
* lingua: Questo riguarda modifiche linguistiche
* aggiunta: Qualsiasi nuova funzionalità aggiunta
* modifica: Qualsiasi modifica
* rimozione: Qualsiasi funzionalità rimossa
* nota: Qualsiasi informazione aggiuntiva per informare l'utente

Ogni nodo può essere ripetuto tutte le volte necessarie.

Il formato del testo può essere testo semplice o HTML, ma in caso di HTML deve essere racchiuso nei tag CDATA come mostrato nell'esempio.

```
<changelogs>
    <changelog>
        <element>com_lists</element>
        <type>component</type>
        <version>4.0.0</version>
        <security>
            <item>Item A</item>
            <item><![CDATA[<h2>You MUST replace this file</h2>]]></item>
        </security>
        <fix>
            <item>Item A</item>
            <item>Item b</item>
        </fix>
        <language>
            <item>Item A</item>
            <item>Item b</item>
        </language>
        <addition>
            <item>Item A</item>
            <item>Item b</item>
        </addition>
        <change>
            <item>Item A</item>
            <item>Item b</item>
        </change>
        <remove>
            <item>Item A</item>
            <item>Item b</item>
        </remove>
        <note>
            <item>Item A</item>
            <item>Item b</item>
        </note>
</changelog>
<changelog>
    <element>com_lists</element>
    <type>component</type>
    <version>0.0.2</version>
    <security>
        <item>Big issue</item>
    </security>
</changelog>
</changelogs>
```

Questo file contiene 2 log delle modifiche:

* Versione 0.0.2 (per testare la vista di gestione)
* Versione 4.0.0 (per testare la vista di aggiornamento)

Un changelog può avere tutte le versioni necessarie.

*Tradotto da openai.com*

