<!-- Filename: J4.x:MVC_Anatomy:_Getting_Started / Display title: Anatomia MVC: Introduzione -->

## Introduzione

I componenti Joomla seguono l'approccio Model, View, Controller, o MVC in breve. Il Model è destinato a gestire il caricamento e l'archiviazione dei dati. La View è destinata a gestire la visualizzazione dei dati. E il Controller è destinato a gestire il flusso del programma, l'interazione tra il codice Model e View del componente.

Se vuoi costruire il tuo componente, ci sono due approcci all'apprendimento che potresti adottare:

- **Costruiscilo passo dopo passo:** seguendo un semplice tutorial che descrive ogni fase.
- **Dissezionalo file per file:** smontando un componente funzionante per imparare come funziona ogni parte.

Questo tutorial utilizza il secondo approccio. Il componente usato per il tutorial si chiama com_countrybase. Viene utilizzato per gestire e visualizzare alcuni dati base sui paesi del mondo. È effettivamente utile di per sé e potrebbe essere utilizzato come base per costruire qualcosa di più sofisticato.

## Obiettivi dell'Outline

Qualunque sia il tuo progetto, dovresti iniziare con una bozza dei tuoi obiettivi e magari chiederti se quegli obiettivi possono essere raggiunti con i componenti core di Joomla o con un'estensione disponibile. Per com_countrybase è necessaria una tabella di dati sui paesi, insieme a pagine di input e output. E forse un modulo per visualizzare un tasso di cambio monetario giornaliero. E anche un plugin chiamato da un comando cli per aggiornare i dati valutari a intervalli regolari. Questo tutorial copre solo il componente.

Il componente necessita di una tabella di database per memorizzare i dati dei paesi e una tabella per memorizzare i dati delle valute. Ognuna avrà bisogno di una vista elenco e di una vista modifica. Questo non è qualcosa che può essere realizzato con i componenti core di Joomla, quindi è chiaramente un caso per un componente personalizzato.

## Tabelle Iniziali

Ci sono molti dati sui paesi disponibili da tutti i tipi di fonti e in tutti i tipi di formati. Poiché ci sono almeno 250 paesi nel mondo, inserire i dati per ciascun paese uno per uno usando un modulo di inserimento dati sarebbe piuttosto tedioso. Quindi, ho preparato tabelle iniziali raccogliendo dati da diverse fonti, combinandoli in un foglio di calcolo e poi esportando istruzioni SQL per creare le tabelle.

I dati si basano sui codici paese ISO 3166, ma alcuni paesi molto noti non sono inclusi, ad esempio Inghilterra, Scozia e Galles. Non è necessario preoccuparsene. Le tabelle sono fornite con il componente com_countrybase.

I file per il componente com_countrybase sono disponibili su GitHub. Puoi scaricare un file [ZIP](https://github.com/ceford/j4xdemos-com-countrybase/archive/refs/heads/master.zip) e installarlo per vederlo funzionare nel menu Amministratore. Crea un elemento di menu se desideri vederlo funzionare nel modello del tuo sito. Inoltre, decomprimi il file zip nello spazio file del tuo progetto, non nell'albero del tuo sito web di prova, per esaminare la struttura dei file del componente e il contenuto dei file con il tuo IDE preferito o strumento di modifica del testo.

## Schermata

Questo elenco di amministratori dei paesi contiene cinque elementi per ridurre al minimo la dimensione dell'immagine. Joomla visualizza normalmente 20 elementi.

![List of countries](../../../en/images/mvc-anatomy/com-countrybase-countries.png)

## Componente Boilerplate

Per aiutarti a iniziare con il tuo componente, c'è un [componente boilerplate](https://github.com/ceford/j4xdemos-com-bpsrc/archive/refs/heads/master.zip) disponibile su Github. Scaricalo e decomprimilo nel tuo spazio di file di progetto, non nella struttura del sito web di test. Dopo il download, apporta tutte le modifiche indicate nel README e sei pronto per partire.

Ci sono anche diversi generatori di estensioni gratuiti e commerciali che potresti provare per generare un componente scheletro per i tuoi scopi. [Joomla! Component Builder](https://www.joomlacomponentbuilder.com/) è gratuito e sembra completo.

*Tradotto da openai.com*

