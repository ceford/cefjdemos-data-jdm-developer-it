<!-- Filename: Setting_up_Eclipse_PDT_2020_and_Git_for_Pulls / Display title: Impostare Eclipse PDT 2020 e Git per i Pull -->

## Introduzione

Ho iniziato a usare Eclipse molti anni fa per un progetto privato su Joomla e un repository git remoto privato non su Github. Ho letto i tutorial disponibili e sono andato avanti felicemente fino a quest'anno, quando ho deciso di provare ad aiutare con i test core e la correzione di bug per Joomla! 4. E poi alcune richieste di pull. È allora che mi sono reso conto di non aver capito esattamente cosa stavo facendo. Alla fine ho deciso di ricominciare da capo e documentare il processo per altri sviluppatori semi-esperti che sono nuovi a Joomla, specialmente le parti che non ho apprezzato pienamente la prima volta. Primo nella lista:

## Struttura dei file

Non è evidente prima di scaricare e installare Eclipse che ci sono almeno due luoghi in cui i dati vengono memorizzati, oltre al posto in cui si trova il codice di Eclipse.

### Lo Spazio di Lavoro

Questo è il posto in cui Eclipse memorizza i propri dati per ogni progetto. Non dovrebbe essere nell'albero web! Poiché lavoro principalmente su un laptop Mac, la posizione predefinita per me è **/Users/username/eclipse-workspace**. C’è una sottocartella per ogni progetto. Quindi una potrebbe essere **/Users/username/eclipse-workspace/joomla-cms**. Contiene una cartella: .metadata. Gli utenti Linux probabilmente sapranno sostituire home con Users.

### Il repository locale di git e il sito web di prova

Questo è il luogo in cui viene memorizzato il codice del progetto. Potrebbe essere nell'albero web locale se desideri usarlo per i test. Per me è **/Users/username/Sites/joomla-cms-4**. Gli utenti Linux probabilmente sapranno sostituire Sites con public_html. Attenzione ai passaggi extra necessari per far funzionare il repository locale come sito Joomla.

### Un sito web di prova separato

Questo è facoltativo ma richiede che il repository git abbia un file build.xml personalizzato, ad esempio build-local.xml, descritto nell'Appendice.

## Software Richiesto

Per configurare un sito web di sviluppo e test funzionante, dovrai prima installare il seguente software:

- Apache
- MySQL o Maridb
- PHP
- phpMyAdmin - [PhpMyAdmin Home page](https://www.phpmyadmin.net/)
- Composer - [Composer Home page](https://getcomposer.org/)
- Node.js - [Node.js Home page](https://nodejs.org/en/)
- Eclipse PDT - [Eclipse PHP Development Tools](https://www.eclipse.org/pdt/)
- git (opzionale per utenti git da riga di comando) - [git Home page](https://git-scm.com/)
- phing (opzionale per build personalizzati) - [phing Home page](https://www.phing.info/)

I primi tre o quattro spesso vengono come un pacchetto per la tua piattaforma, noto come LAMP, WAMP o XAMP stack. Usa semplicemente ciò che la tua piattaforma offre o dai un'occhiata ad Apache Friends [XAMPP](https://www.apachefriends.org/)

Diciamo che hai installato tutto tranne Eclipse.

## Biforca joomla-cms su Github

C'è un flusso di lavoro descritto in [My first pull request to Joomla! on Github](https://docs.joomla.org/My_first_pull_request_to_Joomla!_on_Github "Special:MyLanguage/My first pull request to Joomla! on Github") che non posso lodare abbastanza. Mostra esattamente cosa devi fare:

![Github work flow](../../../en/images/getting-started/core-work-flow-joomla.png)

Passaggi

- Vai su [Github](https://github.com/) e crea un account, gratuito e veloce.
- Nel tuo account github, vai al repository joomla/joomla-cms: digita joomla/joo... nella casella di ricerca in alto a sinistra e seleziona quando appaiono le opzioni.
- Nel repository joomla/joomla-cms clicca sul pulsante fork in alto a destra. Questo ti darà una copia fork di tutto il codice per Joomla 4, Joomla 5, ..., tutto, nel tuo account Github.

Torna alla tua postazione di lavoro.

## Installa Eclipse

Ho già installato due versioni di Eclipse, Oxygen di qualche anno fa e Cocoa del 2020. Da qui in poi sto installando una seconda istanza di Cocoa. Vediamo cosa succede:

- Vai al [sito di Eclipse](https://www.eclipse.org/pdt/) e scarica la versione per la tua piattaforma.
- Segui la procedura di installazione e alla fine avvia l'applicazione Eclipse, per me **Eclipse 2.app**.
- Avviso: *Eclipse 2.app* è un'app scaricata da internet. Sei sicuro di volerla aprire? **Apri**
- Seleziona una directory come workspace - Il default è /Users/username/eclipse-workspace. **Sfoglia** e crea una sottocartella joomla-cms-4.
- Avvia: Eclipse è installato e visualizza la pagina di benvenuto.
- Rivedi le impostazioni di configurazione dell'IDE. Imposta gli elementi 1, 2, 5 e 6.
- Seleziona l'icona della Workbench in alto a destra.

Invece di installare un'altra versione di Eclipse avrei potuto aprire un nuovo spazio di lavoro vuoto.

Finora tutto bene!

## Importa fork in Eclipse

Nella tua nuova installazione locale di Eclipse:

- Apri Preferenze e imposta Team / Git / Cartella repository predefinita su /Users/username/git (puoi anche non utilizzare quella posizione)
- Apri File / Importa / Git / Progetti da Git (con importazione intelligente). Avanti ...
- Clona URI. Avanti ...
- Copia la barra URL dal **tuo fork di Github** e incollala nel campo URL. Non è necessario aggiungere credenziali di autenticazione. Avanti ...
- Rami da importare ... ehm ... Probabilmente è meglio importare tutto. Avanti ...
- Directory. Qui potresti scegliere una posizione diversa per conservare il codice. Ho navigato fino a /Users/username/public_html/joomla-cms-4, creando la cartella se necessario.
- Ramo iniziale - se hai importato tutti i rami. Sto lavorando su Joomla 4 quindi ho selezionato 4.0-dev. E ho notato che il mio clone sarà **origin**. Avanti ...
- Sorso di caffè. La clonazione richiederà alcuni minuti.
- Importare sorgente. La sorgente dovrebbe essere la posizione del codice. Fine.
- Eclipse ora mostra la radice dell'albero del codice nel pannello Esplora Progetto. Clicca per vedere di più sull'albero. Nota che questo codice non funzionerà ancora come sito Joomla. Tra le altre cose, non c'è la cartella media.

## Aggiungi il repository joomla-cms originale a Eclipse

- Mostra la finestra dei repository Git: seleziona Finestra / Mostra Vista / Altro
- Seleziona Git / Repository Git - la finestra appare nella parte inferiore dello schermo.
- Espandi joomla-cms / remoti / origine - se apporti modifiche al tuo codice e le invii all'origine, è qui che andranno.
- Fai clic con il tasto destro su Remoti e seleziona Crea Remoto...
- Imposta il nome del Remoto su **joomla-origin** e seleziona **Configura fetch**.
- In Configura Fetch seleziona **Cambia**.
- In Seleziona un URI incolla l'url del repository originale joomla-cms: `https://github.com/joomla/`
- Lascia le Credenziali vuote. Termina.
- in Configura Fetch: **Salva e Fetch**.

## Creare un sito funzionante

La tua copia del codice joomla-cms necessita di ulteriori passaggi per renderla utilizzabile come sito web.

- Apri un terminale e passa alla cartella che contiene il tuo codice clonato.  
- Esegui composer install:
  - Gli utenti Linux e OSX possono configurare il seguente alias bash inserendo quanto segue all'interno del file `~/.bash_profile` o `~/.zsh` (`\$ source ~/.bash_profile` per applicare immediatamente):
```sh
    alias jclean="rm -rf administrator/templates/atum/css; \
    rm -rf templates/cassiopeia/css; \
    rm -rf administrator/templates/system/css; \
    rm -rf templates/system/css; \
    rm -rf media/; \
    rm -rf node_modules/; \
    rm -rf libraries/vendor/; \
    rm -f administrator/cache/autoload_psr4.php; \
    rm -rf installation/template/css"
    alias jinstall="jclean; composer install --ignore-platform-reqs; npm ci"
```

- composer non è nel mio percorso quindi ho sostituito php ~/composer/composer.phar
- jinstall
- che recupera tutte le dipendenze PHP di Joomla, le dipendenze Javascript, compila tutto il Javascript ES6 e mette i file nelle loro posizioni appropriate.
- sorseggia un caffè mentre le dipendenze vengono scaricate e i file multimediali creati.
- In Eclipse fai clic destro sulla radice del progetto e seleziona Aggiorna. Vedrai che il tuo codice ora ha una cartella media.
- Se sei interessato, usa un gestore di file per vedere che la radice contiene anche un file chiamato .gitignore e la cartella media è menzionata in esso. Ciò significa che non verrà eseguito il commit ai tuoi repository git locali o remoti biforcati.

Sei ora pronto per un'installazione di Joomla:

- Crea un database utilizzando phpMyAdmin (o la riga di comando mysql se preferisci).
- Ho creato un database chiamato joomla-cms-4 con la collazione utf8mb4-unicode-ci.
- Crea un nuovo utente: il mio è jcms4 con una password generata casualmente (GAOC26r77bBLkkdA). Devi annotare la password per utilizzarla durante l'installazione. Verrà salvata in testo normale nel file di configurazione.
- Concedi tutti i privilegi sul database a questo utente - l'impostazione predefinita.
- Nel tuo browser preferito vai alla radice del nuovo sito: localhost/joomla-cms-4/

### Sul mio Mac con macOS Catalina

- Configurazione dell'ambiente incompleta: Maggiori dettagli. Ah - basta sistemarlo e controllare che la barra degli indirizzi contenga l'url che hai digitato - il mio aveva in qualche modo aggiunto caratteri extra.
- Altrimenti va su un sito funzionante - non eliminare la cartella di installazione.

### Sul mio desktop Linux che esegue Linux Mint 20

Oops! Qualcosa è andato storto!

Lo svantaggio è che ho il mio codice Joomla nel mio spazio file personale per l'accesso in lettura/scrittura da parte di Eclipse. Il server web ha anche bisogno dell'accesso in scrittura per scrivere file di configurazione, cache e log, ma sta girando come un utente e un gruppo con privilegi bassi. Poiché sono su una rete domestica privata, ho modificato /etc/apache2/apache2.conf per commentare User \${APACHE_RUN_USER} e Group \${APACHE_RUN_GROUP} e aggiungere User ilmiousername e Group ilmionomegruppo. Riavvia apache, poi...

- Passa a un sito funzionante - non eliminare la cartella di installazione.

## Revisione del Codice

In breve:

- Recupera da joomla-origin per assicurarti che il mio clone locale sia aggiornato.
- Team / Unisci / Seleziona il branch da unire - attenzione - ho selezionato joomla-origin/4.0-dev
- Spingi su origin per assicurarti che il mio fork remoto sia aggiornato.
- Crea un branch per alcune modifiche al codice che voglio apportare.
- Apporta le modifiche al codice.
- Se le modifiche riguardano file sorgente css o js (quelli in sass o es6) apri una finestra del terminale ed esegui di nuovo jinstall.
- TESTA la tua installazione locale per vedere se ci sono problemi.
- Effettua il commit delle modifiche al codice.
- Spingi su origin per aggiornare il mio fork remoto con le mie modifiche.
- Vai al tuo account su Github e seleziona il branch che hai creato con il codice aggiornato. Qualcosa di spaventoso: dice **Questo branch è avanti di 11084 commit, indietro di 134 commit rispetto a joomla:staging.** Ho fatto qualcosa di sbagliato? Apparentemente no!
- Seleziona il pulsante Pull Request. Assicurati di selezionare il branch joomla corretto su cui unire. Per me è 4.0-dev. E assicurati di aver selezionato il tuo branch con il codice modificato. Procedi!
- La pull request deve essere testata e approvata e può richiedere giorni, settimane o mesi. E la modifica potrebbe essere rifiutata!

## Nel frattempo

Torna sulla tua postazione di lavoro:

- Torna al tuo ramo originale, per me: Team / Switch To / 4.0-dev
- Ricostruisci: per me Progetto / Costruisci Progetto
- Vedi i file precedentemente modificati essere copiati di nuovo nel tuo sito di lavoro.
- TEST: il tuo sito di lavoro è tornato allo stato in cui era prima delle modifiche al codice.

Sei ora pronto a creare un altro branch per un altro insieme di modifiche al codice.

## Se Si Verifica un Disastro

A un certo punto il mio clone locale in qualche modo si è corrotto e non avevo idea di come risolvere il problema. Quindi ho eliminato il mio clone locale e tutti i file associati, svuotato il database e poi sono tornato allo stage **Importa fork in Eclipse** sopra. Questo ha sincronizzato il mio clone locale con il mio fork remoto, inclusi tutti i rami che ho creato per le pull request. La nuova installazione ha funzionato senza intoppi e sono stato felice!

## Altre risorse

- [Configurare Eclipse per lo sviluppo di Joomla](https://docs.joomla.org/Configuring_Eclipse_for_joomla_development "Special:MyLanguage/Configuring Eclipse for joomla development") (2012-2013) Ma ottieni l'ultima versione di Eclipse PDT!
- [La mia prima pull request a Joomla! su Github](https://docs.joomla.org/My_first_pull_request_to_Joomla!_on_Github "Special:MyLanguage/My first pull request to Joomla! on Github") (2011-2014) Buona panoramica sebbene un po' datata.
- [Lavorare con git e github](https://docs.joomla.org/Working_with_git_and_github "Special:MyLanguage/Working with git and github") (2011-2015)
- [Configurare il tuo ambiente locale](https://docs.joomla.org/J4.x:Setting_Up_Your_Local_Environment "Special:MyLanguage/J4.x:Setting Up Your Local Environment") (2018-2020)
- [Configurare Eclipse e Xdebug](https://docs.joomla.org/Configuring_Eclipse_and_Xdebug "Special:MyLanguage/Configuring Eclipse and Xdebug") (2013) Tutto sul debugging.
- [Lavorare con Git ed Eclipse](https://docs.joomla.org/Working_with_Git_and_Eclipse "Special:MyLanguage/Working with Git and Eclipse") (2014) Metodo per edizioni vecchie di Eclipse.
- [Eseguire test automatizzati da Eclipse](https://docs.joomla.org/Running_Automated_Tests_from_Eclipse "Special:MyLanguage/Running Automated Tests from Eclipse") (2020) Per utenti avanzati?
- [Configurare Xdebug per lo sviluppo PHP/Linux](https://docs.joomla.org/Configuring_Xdebug_for_PHP_development/Linux "Special:MyLanguage/Configuring Xdebug for PHP development/Linux") (2016) Installa e configura.
- [Configurare Eclipse IDE per lo sviluppo PHP/Linux](https://docs.joomla.org/Configuring_Eclipse_IDE_for_PHP_development/Linux "Special:MyLanguage/Configuring Eclipse IDE for PHP development/Linux") (2019) Installa e configura per Linux.
- [Configurare Xdebug per lo sviluppo PHP](https://docs.joomla.org/Configuring_Xdebug_for_PHP_development "Special:MyLanguage/Configuring Xdebug for PHP development") (2014) Passaggi per Linux, Windows e Mac OS X.
- [Webinar: Usare Eclipse per lo sviluppo di Joomla!](https://docs.joomla.org/Webinar:_Using_Eclipse_for_Joomla!_Development "Special:MyLanguage/Webinar: Using Eclipse for Joomla! Development") (2014) Questo webinar video di 45 minuti, registrato il 30 aprile 2009, fornisce una panoramica delle funzionalità di Eclipse per lo sviluppo di Joomla!.
- [Configurare la tua postazione di lavoro per lo sviluppo di Joomla](https://docs.joomla.org/Setting_up_your_workstation_for_Joomla_development "Special:MyLanguage/Setting up your workstation for Joomla development") (2020) Breve panoramica del software necessario e IDE alternativi.

## Appendice

Ad un certo punto avevo il mio repository git locale al di fuori della radice web e dovevo copiare le modifiche apportate a un sito locale installato separatamente. Questo richiedeva un file di build personalizzato, mostrato qui per riferimento:

### Creare un file build-local.xml

Il clone di Eclipse contiene un file build.xml ma viene utilizzato per testare e costruire un file zip scaricabile per una nuova installazione. Quello che voglio fare è copiare qualsiasi modifica apportata al mio codice clonato nel mio sito di test sul mio portatile. Nota che voglio apportare modifiche solo al codice PHP e non a Javascript o CSS. Per fare ciò ho creato un file separato chiamato build-local.xml nella radice del progetto:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project name="joomla-cms" basedir="." default="main">
    <property file=".project" />

    <property name="joomladir" value="/Users/username/public_html/joomla-cms"  override="true" />

    <property name="srcdir" value="${project.basedir}" override="true" />

    <!-- Fileset for all files -->
    <fileset dir="${srcdir}" id="allfiles">
        <include name="administrator/**" />
        <include name="api/**" />
        <include name="cli/**" />
        <include name="components/**" />
        <include name="images/**" />
        <include name="includes/**" />
        <include name="language/**" />
        <include name="layouts/**" />
        <include name="libraries/**" />
        <include name="modules/**" />
        <include name="plugins/**" />
        <include name="templates/**" />
        <include name="index.php" />

        <exclude name="**/.*" />
    </fileset>

    <!-- ============================================  -->
    <!-- (DEFAULT) Target: main                        -->
    <!-- ============================================  -->
    <target name="main" description="main target">
        <copy todir="${joomladir}">
            <fileset refid="allfiles" />
        </copy>
    </target>
</project>
```

### Aggiungi uno strumento di build

- Fare clic con il tasto destro sulla radice del progetto e selezionare Proprietà.
- Seleziona Builders / New / Program / OK.
- Nome: Build locale con phing
- Posizione: ovunque sia installato phing. Per me è /usr/local/php5/bin/phing anche se sto usando PHP 7.4.
- Directory di lavoro: Sfoglia Workspace e seleziona joomla-cms - viene fuori come \${workspace_loc:/joomla-cms}
- Argomenti: -f build-local.xml
- Applica / OK
- In Builders: Applica e Chiudi
- Progetto / Costruisci Progetto
- Guarda cosa succede:

```sh
    Buildfile: /Users/username/git/joomla-cms/build-local.xml
     [property] Loading /Users/username/git/joomla-cms/.project

    joomla-cms > main:

    BUILD FINISHED

    Total time: 0.2121 seconds
```

*Tradotto da openai.com*

