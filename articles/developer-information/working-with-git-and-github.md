<!-- Filename: Working_with_git_and_github / Display title: Lavorare con git e github -->

## Introduzione

Questo documento fornirà informazioni su come contribuire al Joomla! CMS con l'aiuto di Git e GitHub. Se desideri fare una semplice modifica (un solo file), è più facile utilizzare questa documentazione: [Using the Github UI to Make Pull Requests](https://docs.joomla.org/Using_the_Github_UI_to_Make_Pull_Requests). Se vuoi aggiungere modifiche più complesse o sei semplicemente interessato a questo, continua a leggere!

## Cosa sono Git e GitHub?

Git è un sistema di controllo versioni distribuito. È un sistema che registra le modifiche nei file e conserva queste modifiche in un file di cronologia. Puoi sempre guardare indietro a una versione precedente del tuo codice e ripristinare le modifiche se lo desideri. Grazie all'archivio storico, Git è molto utile quando lavori con molte persone insieme sullo stesso progetto.

Ecco come può essere utilizzato GitHub. [GitHub](https://www.github.com) è un sito web che aiuta a gestire i progetti Git in modo visivo. Come proprietario di un progetto, puoi modificare il codice e confrontare diverse versioni. Come utente del progetto, puoi contribuire facendo una richiesta di pull. Una richiesta di pull è una richiesta al proprietario di inserire del codice nel progetto. Stai offrendo un pezzo di codice (forse una soluzione per un bug) e chiedendo se il proprietario del progetto desidera utilizzarlo. Se al proprietario piace, può unirlo (aggiungerlo) al suo progetto.

Joomla! utilizza GitHub e Git per mantenere il suo codice. Chiunque può contribuire al software Joomla! tramite il suo [repository Github](https://github.com/joomla/joomla-cms).

## Iscriviti su GitHub e installa Git

Innanzitutto, dovrai [registrarti su Github](http://www.github.com). È gratuito e facile da fare. Basta seguire i passaggi forniti.

Una volta registrato, è necessario installare Git sul computer che utilizzi per lo sviluppo (postazione di lavoro o laptop). Segui le istruzioni di installazione sul sito web di [git](http://git-scm.com). Git è un programma CLI (interfaccia a riga di comando). All'inizio può essere confuso e un po' spaventoso, ma questo documento ti guiderà attraverso il processo.

Se non sei un utente avanzato, esegui l'installer e premi i pulsanti "avanti" fino a quando il programma è installato. Git non danneggerà il tuo sistema. Puoi rimuoverlo più tardi come qualsiasi altro programma.

Con Git installato, apri un'applicazione Terminale. Inizia impostando il tuo nome e indirizzo email su Git. Git utilizzerà queste informazioni quando contribuisci a un progetto:

```sh
    git config --global user.name "Your name"
    git config --global user.email youremail@mail.com
```

Nei comandi sopra menzionati, e in tutti gli altri comandi forniti in questa documentazione, ogni riga è un nuovo comando. Quindi digita la prima riga, premi invio e poi digita la seconda riga e premi invio.

Sei ora pronto per utilizzare Git e procedere con l'impostazione della tua installazione di test.

## Configurazione di un'installazione di prova

Per la tua installazione di test hai bisogno di una pila software in modo da poter installare ed eseguire Joomla! sul tuo computer. Stack come MAMP, XAMP o WAMP sono trattati altrove in questa documentazione.

Dopo l'installazione del tuo stack software, è necessario installare l'ultima versione di Joomla!. Questa non è l'ultima versione stabile. L'ultima versione di Joomla! è il ramo di sviluppo su GitHub.

## Fork e Clona Joomla!

Su GitHub puoi trovare progetti nei cosiddetti Repository. All'interno di un progetto potresti trovare diverse versioni. Una tale versione è chiamata Branch. Joomla! ha i seguenti branch:

- **4.2-dev** File per lo sviluppo della versione corrente.
- **4.3-dev** File per lo sviluppo della prossima versione minore.
- **4.4-dev** File per lo sviluppo della versione minore successiva.
- **5.0-dev** File per lo sviluppo della prossima versione maggiore.

Sul tuo computer di test utilizzerai il ramo **4.2-dev**. Tuttavia, non puoi modificare questo ramo perché non ne sei il proprietario. Devi crearne una copia. Su GitHub questo è chiamato un Fork. Sei il proprietario di quella copia, quindi puoi modificarla. Dopo aver modificato il tuo fork, puoi fare una Pull Request per le modifiche che hai apportato. Maggiori informazioni su questo più avanti. Puoi fare un Fork di un ramo premendo il pulsante Fork nel [Joomla! CMS Github Repository](https://github.com/joomla/joomla-cms). Questo pulsante si trova in alto a destra della pagina.

![Fork joomla in github](../../../en/images/getting-started/core-git-fork-joomla.png)

Dopo aver eseguito il fork, devi installare Joomla! sul tuo computer locale. Vai alla cartella dove puoi posizionare i file utilizzati dal tuo server Web. Molti programmi usano una cartella chiamata `htdocs`. Alcuni usano `www` e altri usano cartelle completamente diverse. Tutto dipende dal fatto che tu stia usando Windows, Mac o Linux. Alla fine, la tua radice web conterrà cartelle diverse per siti web diversi. Una volta all'interno della cartella root web. O, in una finestra Terminale aperta, usa il comando cd per cambiare la directory corrente alla radice web. Oppure, nel tuo esploratore di file GUI, trova la cartella root web, premi il tasto destro del mouse e fai clic su: "Git Bash Here" o "Open Terminal" o qualcosa di simile.

Nel Terminale, con la cartella principale del sito impostata come cartella corrente, digita il seguente comando per scaricare i file dal tuo Fork del Joomla! CMS sul tuo computer. Si prega di sostituire *username* con il nome utente che stai utilizzando su GitHub.

```sh
    git clone https://github.com/username/joomla-cms.git
```

Il processo di clonazione potrebbe richiedere un po' di tempo. Al termine, la tua radice web conterrà una cartella chiamata joomla-cms. Devi rendere quella cartella l'attuale cartella per eseguire i comandi git per quella cartella:

```sh
    cd joomla-cms
```

Si prega di ricordare che per altri comandi in questa documentazione.

## Installare Joomla!

Il clone scaricato del tuo repository forked richiede ulteriori azioni prima di essere pronto per l'uso. Uno dei file scaricati si chiama README.md. Aprilo con un editor di testo e segui le istruzioni su **Come ottenere un'installazione funzionante dalla sorgente**.

Quando sei pronto, apri il tuo browser e vai all'installazione sul tuo localhost. Di solito l'URL è qualcosa del tipo:
`http://localhost/joomla-cms`. Ora vedrai il processo di installazione predefinito di Joomla!

## Apportare modifiche al codice

Tutte le modifiche che fai al codice Joomla sul tuo sito locale saranno registrate e monitorate da Git. In qualsiasi momento puoi digitare il comando `git status` per vedere quali file sono modificati o non tracciati. Non tracciato significa che il file in quella posizione è nuovo per Git.

In questa fase è probabilmente meglio utilizzare un Ambiente di Sviluppo Integrato (IDE) per lavorare sul codice di Joomla. Visual Studio Code (VSCode) è altamente raccomandato. È gratuito e funziona su tutte le piattaforme. Utilizzando VSCode puoi apportare modifiche, **Commit** al tuo clone Git locale e **Push** al tuo fork GitHub remoto.

## Invia le modifiche al fork

Il caricamento delle modifiche viene chiamato `push` in termini di Git. Prima di poterlo fare, devi eseguire qualcosa di molto importante. Devi creare un nuovo ramo per le tue modifiche. (Un ramo è una versione del tuo progetto, ricordi?) Se non lo fai e apporti la modifica direttamente al ramo attuale, la prima volta non ci sarà alcun problema. Ma se apporti modifiche una seconda volta e le modifiche che hai fatto la prima volta non sono ancora state integrate, tutte queste modifiche verranno registrate anche come nuove modifiche.

Puoi configurare VSCode per eseguire tutti i seguenti comandi con pochi clic. Ma se vuoi usare i comandi git dalla riga di comando del terminale:

Quindi, il primo comando che eseguirai creerà un nuovo branch. Sostituisci name-new-branch con il nome del nuovo branch. Questo nome deve essere breve e può contenere solo lettere minuscole e numeri. **NON** utilizzare spazi. Al posto degli spazi, utilizza - (meno).

```sh
    git checkout -b name-new-branch
```

Il prossimo comando dice a git che tutte le modifiche sono pronte per essere commit.

```sh
    git add --all
```

Il seguente comando aggiunge la tua modifica al ramo. Si prega di sostituire il messaggio con una breve descrizione delle modifiche apportate. Questa descrizione sarà il titolo della pull request che stai per creare.

```sh
    git commit -m "description"
```

Il comando finale caricherà (upload) le modifiche sul tuo fork. Sostituisci per favore name-new-branch con il nome del branch che hai creato alcuni passaggi sopra.

```sh
    git push origin name-new-branch
```

## Confronta i fork e fai una pull request

Dopo aver spinto la tua modifica su GitHub, vai al tuo fork del Joomla! CMS sul sito GitHub. Seleziona il tuo branch e crea una pull request.

Quando hai finito, nel tuo clone locale, torna al branch originale:

```sh
git checkout 4.2-dev
```

Ora puoi apportare nuove modifiche senza influenzare le modifiche nel tuo ramo precedente.

## Rimanere aggiornati

Poiché la versione attuale di Joomla! può cambiare ogni giorno, è importante mantenere il tuo fork aggiornato. Puoi farlo aggiungendo il repository originale di Joomla al tuo progetto forkato:

```sh
    git remote add upstream https://github.com/joomla/joomla-cms.git
```

Quindi aggiorna il tuo clone locale con il comando seguente:

```sh
    git pull upstream 4.2-dev
```

E aggiorna il tuo fork remoto:

```sh
    git push
```

*Tradotto da openai.com*

