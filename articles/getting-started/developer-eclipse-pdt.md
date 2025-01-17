<!-- Filename: J4.x:Developer:_Eclipse_PDT / Display title: Eclipse PDT -->

## Introduzione

Come sviluppatore PHP, avrai bisogno di alcuni strumenti per aiutarti nel tuo lavoro. Eclipse è un IDE (Integrated Development Environment) che può essere utilizzato per tutti i tipi di progetti in tutti i tipi di linguaggi di programmazione. Eclipse PDT (PHP Developer Tools) include le estensioni necessarie per lo sviluppo PHP. Alcune delle funzionalità menzionate nella sua pagina iniziale includono:

- Evidenziazione della sintassi
- Validazione della sintassi
- Assistenza al contenuto
- Navigazione del codice
- Debug PHP (Zend Debugger / Xdebug)
- Profilazione PHP (Zend Debugger / Xdebug)

Aggiungi a ciò la possibilità di copiare i file dove devono essere nel tuo sito web di test locale e creare un file zip, c'è abbastanza materiale su cui lavorare per anni. Imparare a usare Eclipse PDT richiede tempo, un giorno o giù di lì, ma ne vale la pena. Ci sono altri IDE e editor di codice disponibili!

### Alternative

**IDEs** hanno tutte le funzionalità necessarie per costruire progetti PHP. Esempi cross-platform noti per essere utilizzati da alcuni sviluppatori Joomla includono:

- **JetBrains PhpStorm** Commerciale, Multipiattaforma.
- **Apache NetBeans** Gratuito, Open Source, Multipiattaforma.
- **Visual Studio Code** Gratuito, Multipiattaforma.

**Editor PHP** sono ottimi per modificare il codice, ma mancano di alcuni fronzoli necessari per grandi progetti. Esempi includono:

- **Notepad++** Gratuito, solo per Windows.

## Installare Eclipse PDT

Vai al sito web di [Eclipse PDT](https://www.eclipse.org/pdt/) e scarica la versione disponibile per la tua piattaforma (Linux, Mac o Windows).

Segui le istruzioni di installazione per la tua piattaforma.

## L'area di lavoro di Eclipse

Ci sono almeno tre diversi luoghi in cui verrà situato il codice del tuo progetto:

- I **file sorgente del progetto** sono quelli che crei e modifichi tu stesso. Non dovrebbero essere nel tuo albero web. Dovrebbero essere nel tuo spazio personale di file. Esempi, dove ogni progetto sarà in una sottocartella separata:
  - /Users/username/git (Mac)
  - /home/username/git (Linux)
  - ... (Windows)
- La posizione dell'**albero web** dipende dall'installazione del tuo pacchetto software. Puoi usare il tuo spazio personale di file. Esempi:
  - /Users/username/Sites/j4test (Mac)
  - /home/username/public_html/j4test (Linux)
  - ... (Windows).
- Il **Workspace di Eclipse** è dove Eclipse memorizza le informazioni sui singoli progetti. La posizione standard è la radice del tuo spazio personale di file. Esempi:
  - /Users/username/eclipse-workspace (Mac)
  - /home/username/eclipse-workspace (Linux)
  - ... (Windows).

Pronto per iniziare Eclipse?

## Avvia Eclipse

Dopo l'avvio ti verrà chiesto di confermare varie impostazioni. A un certo punto ti verrà chiesto di scegliere uno spazio di lavoro. Il valore predefinito è /home/username/eclipse-workspace ma desideri creare una sottocartella per ogni progetto, quindi seleziona il pulsante Sfoglia e poi il pulsante Nuova cartella. Nell'esempio sottostante ho creato una cartella j4tutorials.

![Choose eclipse workspace location](../../../en/images/getting-started/eclipse-pdt-choose-workspace.png)

Seleziona il pulsante **Avvia**. Se qualcosa non va, puoi selezionare File / Cambia spazio di lavoro in un secondo momento e riprovarci. Puoi anche eliminare gli spazi di lavoro inutilizzati in seguito.

Al primo avvio viene visualizzata una schermata di benvenuto. Puoi anche accedere a questa schermata dai voci di menu **Aiuto / Benvenuto**.

![Eclipse welcome screen](../../../en/images/getting-started/eclipse-pdt-welcome.png)

Inizia con la revisione delle impostazioni di configurazione dell'IDE. Puoi contrassegnare o cancellare quelle che sembrano appropriate, o deselezionare o rimuovere il contrassegno o passare oltre se sei incerto. Puoi anche cambiare le impostazioni più tardi.

## Creare un nuovo progetto PHP

Il primo progetto da aggiungere è il codice del sito web di prova. Avrai bisogno di questo per verificare che i tuoi file siano copiati nei posti corretti e per il debug in seguito. Seleziona l'elemento nella schermata di benvenuto. Se sei passato alla workbench di Eclipse, seleziona Crea un progetto PHP dal Project Explorer. Nel modulo Nuovo Progetto PHP:

- Inserisci un Nome Progetto appropriato. Dovrebbe essere una parola breve che apparirà nell'Esplora Progetti.
- Seleziona il pulsante radio **Crea progetto in una posizione esistente (da sorgente esistente)**.
- **Sfoglia** per trovare la posizione del tuo sito web di test Joomla e selezionala.
- Seleziona **Fine**.

![Eclipse new php project](../../../en/images/getting-started/eclipse-pdt-new-project.png)

I file del tuo sito web verranno aggiunti a Project Explorer. Eclipse potrebbe impiegare un minuto o due per completare questo processo, poiché esegue alcune preparazioni in background. Puoi selezionare il progetto per espandere il primo livello della cartella.

Due file verranno aggiunti alla cartella del tuo sito: .buildpath e .project. Poiché iniziano con un punto (.), potresti non vederli e non devi preoccupartene. Sono file XML che contengono informazioni utilizzate da Eclipse.

## La Prospettiva PHP

La raccolta di pannelli nella schermata di Eclipse è conosciuta come prospettiva. Le due più comunemente usate sono la Prospettiva PHP e la Prospettiva Debug. Puoi passare da una all'altra utilizzando le icone in alto a destra della barra degli strumenti. Puoi anche usare il menu: Finestra / Prospettiva / Apri Prospettiva / PHP o Debug.

Le seguenti illustrazioni mostrano la prospettiva PHP con un paio di moduli di modifica aperti.

![Eclipse php perspective](../../../en/images/getting-started/eclipse-pdt-php-perspective.png)

I pannelli di Eclipse:

- Il pannello di sinistra è il Project Explorer dove puoi navigare nella struttura dei tuoi file.
- Il pannello centrale superiore è dove appaiono gli editor di testo aperti.
- Il pannello superiore destro solitamente mostra uno schema del pannello di modifica selezionato. Può mostrare altre informazioni.
- Il pannello inferiore destro mostra una delle tante Visualizzazioni, selezionabile dal menu Finestra / Mostra vista.

La vista Problemi dice Errori (100 di 791 elementi) e Avvertenze (100 di 11629). Sembrano molti ma non c'è nulla di cui preoccuparsi.

## Un nuovo progetto PHP Hello Universe

Sei ora pronto a creare un nuovo progetto PHP per l'estensione che intendi sviluppare. Per illustrazione, puoi iniziare con un semplice componente chiamato com_hellouniverse. Per me, il codice Hello Universe si troverà in /Users/username/git/j4xtutorials-com-hellouniverse e userò j4xtutorials come la mia affiliazione dello spazio dei nomi (la prima parola nello spazio dei nomi del componente).

Nel menu di Eclipse, seleziona File / Nuovo / Progetto PHP. Il modulo è quello illustrato sopra. I miei dati:

- Nome del progetto: HelloUniverse
- Contenuti: seleziona Crea progetto in una posizione esistente (da sorgente esistente).
- Sfoglia: Naviga a /Home/username/git e seleziona il pulsante Nuova cartella.
- Nella finestra di dialogo Nuova cartella inserisci j4xtutorials-com-hellouniverse e premi Crea.
- Con quella cartella vuota aperta, seleziona Apri.
- La directory selezionata dovrebbe dire: /Users/username/git/j4xtutorials-com-hellouniverse
- Seleziona Fine.

Vedrai ora il nuovo progetto nel Project Explorer insieme al progetto del tuo sito web. Il nuovo progetto contiene due elementi, entrambi correlati al supporto PHP. Ci sono alcuni elementi nascosti utilizzati da Eclipse: .settings(cartella), .buildpath e .project.

## Aggiungi cartella com_hellouniverse

Con il progetto HelloUniverse selezionato:

- Seleziona l'elemento del menu File oppure fai clic con il tasto destro sul nome del progetto.
- Seleziona gli elementi del menu Nuovo / Cartella.
- Nel modulo Nuova Cartella inserisci com_hellouniverse nel campo Nome cartella:.
- Seleziona Fine.

La cartella com_hellouniverse è dove andrà il codice della tua estensione. Qualsiasi cosa all'interno di quella cartella finirà in un file zip che puoi utilizzare per l'installazione in Joomla. Qualsiasi cosa al di fuori di quella cartella è utilizzata per altri scopi. Due file comuni a questo livello:

- README.md è un file di testo formattato in Markdown che descrive il componente. Tali file sono comunemente usati in combinazione con l'archiviazione remota del codice, come su Github (di più su questo altrove).
- build.xml è un file che contiene istruzioni su cosa fare dopo aver apportato modifiche al codice. Più comunemente, desidererai copiare i file modificati nei posti corretti nel tuo albero del sito web e rigenerare il file zip. Quindi, per la maggior parte delle modifiche, puoi semplicemente ricaricare la pagina web su cui stai lavorando. Non devi reinstallare il componente. Questo fa risparmiare un'enorme quantità di tempo!

## Aggiungi cartelle admin, sito e media

- Seleziona la cartella com_hellouniverse e usa le voci di menu File / Nuovo / Cartella per creare una nuova cartella chiamata admin.
- Ancora, questa volta crea una nuova cartella chiamata media. ATTENZIONE: assicurati che il genitore sia com_hellouniverse e non HelloUniverse.
- Ancora, questa volta crea una nuova cartella chiamata site. Se creata nel posto sbagliato, può essere trascinata nel posto corretto.

## build.xml

Il seguente codice contiene un esempio di file build.xml da inserire nella radice del tuo progetto HelloUniverse.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project name="hellouniverse" basedir="." default="main">
    <property file=".project" />

    <!-- Source and Destinations -->

    <property name="package"  value="${phing.project.name}" override="true" />
    <property name="srcdir" value="${project.basedir}/com_hellouniverse" override="true" />
    <property name="sitedir" value="/Users/username/Sites/j4tutorials"  override="true" />
    <property name="zipsdir" value="/Users/username/zips"  override="true" />

    <!-- Filesets -->

    <fileset dir="${srcdir}/admin" id="adminfiles">
        <include name="**" />
    </fileset>
    <fileset dir="${srcdir}/media" id="mediafiles">
        <include name="**" />
    </fileset>
    <fileset dir="${srcdir}/site" id="sitefiles">
        <include name="**" />
    </fileset>
    <fileset dir="${srcdir}" id="allfiles">
        <include name="**" />
    </fileset>

    <!-- Targets -->

    <target name="main" description="main target">
        <copy todir="${sitedir}/administrator/components/com_hellouniverse">
            <fileset refid="adminfiles" />
        </copy>
        <copy todir="${sitedir}/media/com_hellouniverse">
            <fileset refid="mediafiles" />
        </copy>
        <copy todir="${sitedir}/components/com_hellouniverse">
            <fileset refid="sitefiles" />
        </copy>
        <zip destfile="${zipsdir}/com_hellouniverse.zip">
            <fileset refid="allfiles" />
        </zip>
    </target>
</project>
```

Alcune spiegazioni:

- **srcdir** è la posizione nel file system del tuo codice sorgente, da cui vengono copiati i file.
- **sitedir** è la posizione nel file system del tuo sito di test, dove vengono copiati i file.
- **zipsdir** è una posizione per il file zip - trovo conveniente conservare i file zip di progetti diversi insieme in una cartella zips.
- **Filesets** sono gruppi di sorgenti da copiare a destinazioni diverse, ovvero tutte le cartelle e i file.
- **Targets** sono le destinazioni e ciò che deve essere copiato lì.

Crea un file build.xml contenente il codice sopra:

- Seleziona File / Nuovo / File XML dal menu di Eclipse.
- Assicurati che HelloUniverse sia selezionato come genitore e inserisci il nome build.xml (esattamente così).
- Seleziona Fine
- Nella vista di origine (scegli in basso a sinistra) copia e incolla il codice sopra al posto della riga già presente.
- Salva.

Per far funzionare questo, hai bisogno di uno strumento di build: Phing.

## Lo strumento di build Phing¶

Vai al sito web di [Phing](https://www.phing.info/) e scarica l'archivio Phar. Puoi usare questo [link diretto](https://www.phing.info/get/phing-latest.phar). Salva il file in una cartella phing nella tua cartella personale bin /Users/username/bin/phing. Cambia i permessi del file a 755 in modo che possa essere eseguito dalla riga di comando. Per testare, apri un terminale, cambia nella tua cartella bin/phing e inserisci ./phing-latest.phar -v per vedere il numero di versione. Ricorda il percorso completo al file:

- /Users/username/bin/phing/phing-latest.phar

Ti servirà più tardi.

## Preferenze di Eclipse - Costruttori

Qui è dove configuri Phing per costruire il tuo progetto ogni volta che apporti modifiche al codice.

- In Project Explorer, seleziona il progetto HelloUniverse.
- Seleziona i menu File / Proprietà.
- Nella finestra di dialogo Proprietà, seleziona Costruttori e poi il pulsante Nuovo.
- Nella finestra di dialogo Tipo di configurazione seleziona Programma e poi OK.
- Nella finestra di dialogo Modifica proprietà di configurazione di avvio inserisci un titolo appropriato: Compila HelloUniverse.
- Nel campo Posizione inserisci il percorso del programma phing o usa il pulsante Sfoglia file system per cercarlo: /Users/ceford/bin/phing/phing-latest.phar
- Per il campo Directory di lavoro, seleziona il pulsante Sfoglia area di lavoro e poi seleziona HelloUniverse.
- Clicca OK, poi Applica e Chiudi.

Per testare: seleziona le voci di menu Progetto / Compila Progetto. La vista Console nella parte inferiore dello schermo mostrerà il progresso della compilazione. In questa fase è probabile che mostri BUILD FAILED in rosso. È previsto - le cartelle dei componenti verranno create al momento dell'installazione del file zip. Non esiste ancora perché non c'è codice. Ma mostra che lo strumento di build Phing funziona.

## Come eseguire il debug

Quando qualcosa va storto, potresti voler esaminare il codice riga per riga per vedere cosa sta realmente accadendo. Se hai impostato Debug System su Sì e Error Reporting su Massimo nella Configurazione Globale di Joomla, potresti avere una traccia dello stack che mostra dove si verifica un errore nel codice. Oppure potresti vedere qualcosa di insolito nell'output e avere una buona idea di dove potrebbe trovarsi il problema. In entrambi i casi, è necessario impostare i punti di interruzione dove l'esecuzione si fermerà per permetterti di vedere i valori delle variabili e avanzare nel codice riga per riga.

### Imposta un punto di interruzione

I punti di interruzione devono essere impostati nel progetto del sito web, J4Tutorials. Ad esempio, nel pannello Project Explorer, espandi il progetto J4Tutorials e trova administrator / components / com_users / src / Model e fai doppio clic su UsersModel.php per aprirlo in una finestra di modifica. Vai alla linea 87 e fai doppio clic sul numero 87. Appare un piccolo marcatore blu per indicare che è stato impostato un punto di interruzione. L'esecuzione del codice dovrebbe fermarsi qui quando visualizzi l'elenco degli Utenti tramite gli elementi di menu Administrator / Users / Manage.

### Creare una configurazione di debug

Dal menu in alto seleziona Esegui / Configurazioni di Debug. Nel modulo inserisci un titolo riconoscibile, ad esempio Debug Admin, da selezionare successivamente da un elenco a discesa. Assicurati che il file selezionato sia /J4Tutorials/administrator/index.php. Nel modulo pannello Comune seleziona Debug dall'elenco del menu Visualizza nei preferiti. Verifica che Debugger sia impostato su Xdebug. Seleziona Applica e Chiudi.

Ora è possibile selezionare Debug Admin dall'elenco a discesa di debug nella Barra degli strumenti, l'icona del simbolo del bug.

![Eclipse debug tools](../../../en/images/getting-started/eclipse-pdt-debug-tools.png)

Icone di debug, passa il mouse per etichette:

- **Salta Tutti i Breakpoint** Un interruttore per saltare i breakpoint tranne la prima riga di index.php.
- **Riprendi** Continua l'esecuzione normale fino al prossimo breakpoint.
- **Termina** Interrompi il debug (ma devi anche rimuovere il cookie Xdebug).
- **Entra** Su una riga contenente una chiamata a funzione, entra in quella funzione.
- **Salta Sopra** Su una riga contenente una chiamata a funzione, non entrare in quella funzione.
- **Esci** In una funzione, evita di fermarti a ogni riga e ritorna al chiamante.

### Procedura di Debug

All'avvio di una sessione di debug, l'esecuzione si ferma alla prima riga di administrator/index.php. Questa è la pagina della Home Dashboard. È necessario selezionare il simbolo Riprendi (barra gialla e triangolo verde a destra). Dopo un ritardo di un secondo circa, c'è più attività e più lanci Remoti in pausa nel pannello Debug Admin a sinistra. Questa è la pagina Home che utilizza ajax per recuperare le informazioni di aggiornamento. Continua a fare clic su Riprendi finché l'attività non si ferma. Poi nel tuo browser, seleziona l'elemento Utenti dalla Home Dashboard. Eclipse si attiva e interrompe l'esecuzione al punto di interruzione che hai impostato.

![Eclipse PHP debug perspective](../../../en/images/getting-started/eclipse-pdt-debug-perspective.png)

Caratteristiche da notare:

- La riga di codice corrente è contrassegnata da uno sfondo verde pallido.
- Il pannello sinistro mostra una traccia dello stack - le chiamate di funzione precedenti che hanno portato alla funzione attuale. Seleziona qualsiasi elemento per vedere il codice padre.
- Il pannello destro può mostrare variabili attive o breakpoint. Espandi gli oggetti come richiesto per vedere i dettagli.

### Alcuni problemi

- Mancato arresto ai punti di interruzione: questo accade se si apre un altro programma PHP come phpMyAdmin. Per risolvere:
  - Vai a Esegui / Configurazioni di Debug e seleziona l'elemento Debug Admin.
  - Nella scheda Debugger seleziona Configura...
  - In Mapping dei percorsi seleziona e rimuovi qualsiasi percorso non correlato al tuo sito web di test.
  - Seleziona Fine - potrebbe essere necessario terminare e ricaricare la sessione di debug.
- Il debug riprende dopo aver selezionato il pulsante Termina. Per correggere:
  - Usa gli strumenti per sviluppatori del tuo browser per aprire una finestra di ispezione.
  - Trova i cookie che il tuo browser sta usando (Archiviazione in Firefox)
  - Seleziona ed elimina il cookie XDebug.

## Uso di Git

Git è un sistema di controllo delle versioni ampiamente utilizzato per gestire qualsiasi tipo di testo, principalmente codice, ma può essere qualsiasi cosa. Funziona da una riga di comando, ma di solito viene richiamato da strumenti grafici come Eclipse. Se desideri leggere di più su git, visita il [sito web di git](https://git-scm.com/).

Se vuoi usare git devi installarlo per la tua piattaforma. Poi in Eclipse, seleziona il tuo progetto HelloUniverse, fai clic con il tasto destro e seleziona Team / Condividi Progetto. Nella finestra di dialogo Condividi Progetto seleziona **Usa o crea repository nella cartella principale del progetto** e seleziona il progetto HelloUniverse dall'elenco. C'è un campo per indicare dove verrà creato il repository (/Users/ceford/git/j4xtutorials-com-hellouniverse) - seleziona il pulsante Crea Repository adiacente. Infine, seleziona il pulsante Fine.

![Configure Git Repository](../../../en/images/getting-started/eclipse-pdt-configure-git.png)

Noterai che alcune nuove decorazioni sono apparse accanto agli elementi nella vista Project Explorer:

- Il marcatore \> indica che c'è del contenuto che è cambiato ma non è stato ancora aggiunto al repository.
- Il marcatore ? indica che questo elemento non è stato aggiunto all'elenco degli elementi da tracciare.

![Git Markers](../../../en/images/getting-started/eclipse-pdt-git-markers.png)

Sei ora configurato per il controllo delle versioni. Fai clic con il tasto destro sul progetto e guarda come appare il menu Team. Troppo da trattare qui!

## Infine

Pronto per iniziare a lavorare sul tuo codice?

*Tradotto da openai.com*

