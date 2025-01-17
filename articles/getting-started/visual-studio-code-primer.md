<!-- Filename: Visual_Studio_Code_Primer / Display title: Visual Studio Code -->

## VS Code - Un Popolare IDE Gratuito

Da [Wikipedia](https://en.wikipedia.org/wiki/Visual_Studio_Code):

Visual Studio Code, comunemente noto come VS Code, è un editor di codice sorgente realizzato da Microsoft per Windows, Linux e macOS. Le funzionalità includono supporto per il debugging, evidenziazione della sintassi, completamento intelligente del codice, frammenti, refactoring del codice e Git incorporato. Gli utenti possono cambiare il tema, i collegamenti da tastiera, le preferenze e installare estensioni che aggiungono funzionalità aggiuntive.

## Installazione

La pagina predefinita del sito [VS Code](https://code.visualstudio.com/) ha un elenco a discesa per ciascuna piattaforma supportata. È probabile che la tua piattaforma sia preselezionata. Quindi, scarica e installa e sei pronto per iniziare.

### Iniziare

La pagina *Get Started* di VS Code contiene alcuni elementi *Start*, un elenco di elementi *Recent* e un breve elenco di *Walkthroughs*. Se sei completamente nuovo a VS Code, ti consigliamo di visualizzarli. Richiedono solo pochi minuti.

La documentazione di VS Code è disponibile dal menu *Aiuto / Documentazione*. I video introduttivi meritano davvero di essere visti. Ognuno dura dai 2 ai 6 minuti e offre un'eccellente introduzione alle funzionalità di VS Code:

[Video di VS Code](https://code.visualstudio.com/docs/getstarted/introvideos)

La documentazione ufficiale è il posto giusto dove andare se vuoi cercare informazioni specifiche.

### Estensioni di VS Code

VS Code può essere utilizzato per qualsiasi tipo di testo, inclusa una vasta gamma di linguaggi di programmazione. Funziona con JavaScript senza l'aggiunta di estensioni. Altri linguaggi vengono rilevati dal contesto, quindi se inizi a creare e salvare codice PHP è probabile che ti venga chiesto di installare un pacchetto di supporto PHP.

Fai clic sull'icona *Estensioni* nella *Barra delle attività* a sinistra per vedere cosa hai installato e cosa è consigliato. Avrai bisogno dell'estensione PHP Debug!

### Il layout dello schermo di VS Code

Alcuni termini usati nelle istruzioni successive:

- **Barra delle attività:** la barra stretta a sinistra dello schermo. Seleziona qualsiasi icona per aprire o chiudere la barra laterale principale.
- **Barra laterale principale:** quando è aperta mostra i dettagli dell'attività selezionata.
- **Barra di stato:** in fondo allo schermo. Mostra cosa sta succedendo.
- **Pannello:** un'area sotto gli editor di testo per mostrare altre informazioni.

Seleziona un'icona di layout in alto a destra per aprire o chiudere uno di questi elementi.

## Codifica di un'estensione Joomla

Per creare un'estensione, il tuo obiettivo è creare un file zip che puoi installare su un sito Joomla funzionante. Quindi hai bisogno di una cartella per contenere il tuo codice. Questa dovrebbe trovarsi all'interno del tuo spazio file personale sul tuo laptop o computer desktop utilizzato per lo sviluppo locale. Non dovrebbe essere nell'albero del tuo sito web. Ad esempio, potresti usare *~/jextensions* per contenere sottocartelle per diverse estensioni. Io uso *~/git* perché è breve e facile da scrivere, anche se potenzialmente confuso perché ogni sottocartella utilizza un repository git separato.

### Codice di esempio

Se desideri del codice di esempio su cui lavorare, è disponibile un'estensione su GitHub chiamata *mod_debugme*. Come suggerisce il nome, si tratta di un modulo con alcuni bug. Oltre al codice del modulo, c'è un file *build.xml* per illustrare un modo per automatizzare la compilazione per il test e la creazione di un file zip.

Il modulo è progettato per mostrare i prossimi pochi (3 per impostazione predefinita) eventi (compleanni) da un elenco memorizzato in una tabella del database. Potreste immaginare che venga usato in un sito per ufficio o per famiglie con l'aspettativa di una torta.

Potrebbe essere meglio iniziare utilizzando i comandi git dalla riga di comando. Per prima cosa crea una cartella per il tuo codice e poi clona il repository remoto:

```sh
    mkdir ~/git
    cd ~/git
    git clone https://github.com/ceford/j4xdemos-mod-debugme
```

La risposta dovrebbe richiedere solo pochi secondi:

```sh
    Cloning into 'j4xdemos-mod-debugme'...
    remote: Enumerating objects: 23, done.
    remote: Counting objects: 100% (23/23), done.
    remote: Compressing objects: 100% (16/16), done.
    remote: Total 23 (delta 3), reused 23 (delta 3), pack-reused 0
    Unpacking objects: 100% (23/23), done.
```

Dovresti prenderti un momento per guardare il contenuto della cartella:

```sh
    cd j4xdemos-mod-debugme
    ls -al
    total 16
    drwxr-xr-x   6 ceford  staff   192  2 Sep 17:48 .
    drwxr-xr-x   3 ceford  staff    96  2 Sep 17:48 ..
    drwxr-xr-x  12 ceford  staff   384  2 Sep 17:48 .git
    -rw-r--r--   1 ceford  staff  1402  2 Sep 17:48 README.md
    -rw-r--r--   1 ceford  staff   927  2 Sep 17:48 build.xml
    drwxr-xr-x   8 ceford  staff   256  2 Sep 17:48 mod_debugme
```

La cartella *.git* contiene informazioni sul repository. Il file *README.md* è un documento markdown che descrive questo repository. Il file *build.xml* è un file utilizzato per costruire l'estensione con uno strumento esterno, Phing - descritto successivamente. La cartella *mod_debugme* contiene il codice dell'estensione.

### Installare in Joomla

Comprimi la cartella dell'estensione per creare un file zip installabile:

```sh
    zip -r mod_debugme.zip mod_debugme
```

Ora puoi installare il file zip nel sito Joomla che utilizzi per i test. Dopo l'installazione, devi creare un modulo del sito e assegnargli una posizione di modulo. Poiché si tratta di un modulo difettoso, potresti assegnarlo a una posizione su *Tutte le pagine* mentre ci lavori; oppure potresti assegnarlo a una posizione su una singola pagina; oppure potresti posizionarlo in un articolo che ha il proprio elemento di menu.

Dopo l'installazione, elimina il file zip.

### Attiva la Modalità Debug

Nella Configurazione Globale di Joomla, imposta *Debug del Sistema* su *Sì* e *Segnalazione Errori* su *Massimo*.

Quando apri una pagina contenente il modulo difettoso, vedrai un traceback che ti indicherà dove è stato attivato un errore.

![Stack trace](../../../en/images/getting-started/vscode-primer-stack-trace.png)

A volte l'errore di codice si trova sulla prima riga dello stack trace. Altrimenti, se l'errore viene attivato nel codice della libreria, ad esempio passando dati non validi a una funzione del database, l'errore di codice potrebbe trovarsi più in basso nell'elenco delle chiamate di funzione.

## Apri Cartella Estensioni in VS Code

In VS Code, utilizza l'elemento di menu File / Apri cartella per individuare e aprire la cartella contenente la tua copia locale del codice dell'estensione *mod_debugme*. Dovresti vedere qualcosa di simile al seguente:

![VS Code screen](../../../en/images/getting-started/vscode-primer-screen.png)

Potresti essere in grado di diagnosticare il problema semplicemente leggendo il codice. Nel caso dell'errore *Class "DebugHelper" not found* vedrai che un'istruzione *use* è stata commentata poche righe sopra. Dimenticare di inserire un'istruzione *use* è un errore comune durante lo sviluppo iniziale!

Risolvi quel problema e poi comprimi e installa nuovamente il modulo. Quel passaggio diventa un po' noioso quando hai più problemi. Ed è qui che gli strumenti di build diventano utili.

## Lo strumento di build Phing

Phing è uno strumento da riga di comando, disponibile per tutte le piattaforme, utilizzato per costruire pacchetti software utilizzando istruzioni memorizzate in un file xml, chiamato build.xml per impostazione predefinita. Per lavorare con il codice di estensione può essere utilizzato per fare due cose:

- copia i file modificati dalla cartella sorgente dell'estensione ai luoghi corretti nella cartella del tuo sito web.
- genera un nuovo file zip per le nuove installazioni.

Scarica e installa [Phing](https://www.phing.info/). Altri strumenti di costruzione sono disponibili! Puoi installare Phing nella tua cartella bin personale o in una cartella bin di sistema. Devi annotare il percorso al tuo codice Phing. In questo esempio è *~/bin/phing-latest.phar*. Puoi provarlo dalla linea di comando dopo essere entrato nella cartella contenente il codice della tua estensione:

```sh
    cd ~/git/j4xdemos-mod-debugme
    php ~/bin/phing-latest.phar
```

Risposta:

```sh
    Buildfile: /Users/ceford/git/j4xdemos-mod-debugme/build.xml

    mod_debugme > main:
          ... Any copied files will be mentioned here
          [zip] Building zip: /Users/ceford/zips/mod_debugme.zip

    BUILD FINISHED

    Total time: 0.0863 seconds
```

## Attività di VS Code

Per eseguire Phing all'interno di VS Code, è necessario creare un file *tasks.json* nella cartella *.vscode* nella radice della cartella *j4xdemos-mod-debugme*. Se quest'ultima non esiste, creala prima. Quindi crea il file *tasks.json* e inserisci il seguente codice:

```json
    {
        // See https://go.microsoft.com/fwlink/?LinkId=733558
        // for the documentation about the tasks.json format
        "version": "2.0.0",
        "tasks": [
          {
            "label": "Build mod_debugme",
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

Gli utenti Windows devono correggere il comando specifico per Windows. Ora puoi costruire l'estensione utilizzando il menu *Terminale / Esegui attività di compilazione*. Il risultato del comando dovrebbe apparire nel Pannello Terminale sotto l'area di modifica.

```sh
      *  Executing task: php ~/bin/phing-latest.phar

    Buildfile: /Users/ceford/git/gitdemo/j4xdemos-mod-debugme/build.xml

    mod_debugme > main:

          [zip] Nothing to do: /Users/ceford/zips/mod_debugme.zip is up to date.

    BUILD FINISHED

    Total time: 0.1031 seconds

     *  Terminal will be reused by tasks, press any key to close it.
```

Potrebbero esserci messaggi di errore incomprensibili. La causa più probabile è avere percorsi non validi alle cartelle nel file *build.xml* o una cartella non è stata creata. Solo un altro tipo di problema da debug!

## Debugging

Dovresti essere in grado di risolvere il primo bug tramite l'ispezione del codice. Problemi più complicati richiedono di eseguire il codice con il debugger. Ciò ti permette di ispezionare le variabili per vedere se contengono i valori che ti aspetti, ad esempio quando passi argomenti a funzioni di libreria.

### Impostazioni di *php.ini*

Per configurare il debug con Xdebug, è necessario inserire alcune voci all'inizio del file *php.ini*.

```sh
    zend_extension="xdebug.so"
    xdebug.mode="debug"
    xdebug.client_port=9003
    xdebug.start_with_request=yes
    xdebug.log_level=0
```

Dopo aver salvato le modifiche, riavvia il tuo server Apache.

### Aggiungi Finestra Sito Web

La cartella dell'estensione contiene solo pochi file, le ***sorgenti*** dei file installati nel tuo sito web. Il debug in esecuzione comporta l'impostazione di punti di interruzione nei file del tuo ***sito***, pertanto è necessario accedere a quei file. Potresti utilizzare il menu *File / Aggiungi cartella allo spazio di lavoro...* per aggiungere la cartella del sito al tuo Spazio di lavoro. Tuttavia, è molto probabile che finirai per apportare modifiche ai file del sito invece che ai file sorgente. Quindi è probabilmente meglio aprire una finestra separata di VS Code per il debug.

- **Apri nuova finestra:** Dal menu di VS Code, seleziona *File / Nuova Finestra* e seleziona la cartella contenente il tuo sito web Joomla.
- **Apri cartella:** Nella nuova finestra aperta, seleziona *File / Apri Cartella...* dal menu di VS Code. Trova la cartella del tuo sito web e selezionala. Dovresti vedere un elenco di tutti i file del tuo sito web Joomla nella barra laterale principale.

### Configurazione di Lancio

Affinché il debug funzioni effettivamente in VS Code, è necessaria una configurazione di lancio. Nella radice del tuo sito web, crea una cartella denominata *.vscode* (nota il punto iniziale) contenente un file chiamato *launch.json* con il seguente contenuto:

```json
    {
        "configurations": [
            {
                "name": "Listen for XDebug",
                "type": "php",
                "request": "launch",
                "hostname": "0.0.0.0",
                "port": 9003,
                "stopOnEntry": true,
                "pathMappings": {
                    "/Users/ceford/Sites/j421rc2": "${workspaceFolder}"
                }
            }
        ]
    }
```

Ricorda di sostituire l'elemento pathMappings in questo esempio con i pathMappings effettivi sul tuo sito. L'elemento stopOnEntry interromperà l'esecuzione alla primissima riga di codice PHP eseguita.

### Debug *mod_debugme*

Ora sei pronto per trovare e correggere gli errori nel modulo installato.

- **Trova il codice del modulo:** Trova il primo bug alla linea 16 di JROOT/modules/mod_debugme/mod_debugme.php.
- **Imposta punto di interruzione:** Clicca nello spazio a sinistra del numero 16. Apparirà un piccolo cerchio rosso chiaro mentre ci passi sopra col mouse e diventerà completamente rosso dopo che avrai cliccato per indicare che è stato impostato un punto di interruzione.
- **Avvia debug:** Dal menu di VS Code seleziona *Esegui / Avvia Debugging*. Nel tuo browser ricarica il sito. La finestra di VS Code dovrebbe riapparire con il codice fermo alla prima linea del file *index.php* del sito. In alto sullo schermo ci sono alcune icone per controllare il processo di debug. Dovrebbero essere autoesplicative. In caso contrario, consultale nella Guida / Documentazione di VS Code.
- **Continua:** Seleziona il pulsante continua - il codice verrà eseguito fino al tuo primo punto di interruzione. Esamina il codice per vedere qual è il problema.
- **Sospendi il mouse:** Se passi il mouse su una variabile a cui è stato assegnato un valore, apparirà un piccolo Tooltip che riassume gli attributi di quella variabile. Non c'è Tooltip per le variabili a cui non sono stati assegnati valori.
- **Variabili:** La colonna di sinistra contiene più informazioni sullo stato del codice al punto di interruzione. Ce ne sono troppe per essere coperte qui. Esplorale secondo necessità!
- **Interrompi Debugging:** È probabilmente meglio selezionare l'icona Continua, altrimenti la pagina web viene consegnata vuota. Altrimenti puoi usare il pulsante Stop o il menu Esegui / Interrompi Debugging.

### Risolvere un bug

**Ricorda:** Non correggere il bug nel codice del sito web! Correggilo nel codice sorgente!

Correggi il codice sorgente e poi usa *Terminale / Esegui attività di creazione...*.

Riavvia debug.

### Suggerimenti

Alcuni problemi non così ovvi:

- Risolvi il primo bug ma si arresta ancora in quella linea. Guarda in mod_debugme.xml per vedere dove è definita la src delle classi con namespace. Quando viene corretto nel sorgente, devi reinstallare il file zip o eliminare *administrator/cache/autoload_psr4.php*. Quando assente, Joomla ricostruisce quel file dai file manifest. Ma se ha una voce errata o mancante, non viene corretto finché l'estensione non viene reinstallata.
- A volte devi impostare un punto di interruzione poche righe prima della linea in cui si verifica l'errore, specialmente se desideri controllare i valori passati alle chiamate di funzione.
- La tabella *xxx.yyy\\debugme* non esiste. Ah sì, il codice per creare una tabella all'installazione e rimuoverla alla disinstallazione non è mai stato creato. Dovrai eseguire una query sql in phpMyAdmin utilizzando il contenuto del file *mod\\debugme.sql*. Ricorda di cambiare *\#\\* nei nomi delle tabelle con il prefisso del tuo database. E quando ancora fallisce, controlla il nome della tabella nel codice.

## Screenshot

Quando tutto è sistemato, questo è ciò che potresti vedere:

![Site view of debugged module working](../../../en/images/getting-started/vscode-primer-debugme-fixed.png)

Giorni delle torte?

## Riferimenti

Dalla documentazione di Joomla!: [Visual Studio Code](https://docs.joomla.org/Visual_Studio_Code "Visual Studio Code") che copre anche la configurazione di altri strumenti, ad esempio CodeSniffer e PHPUnit.

*Tradotto da openai.com*

