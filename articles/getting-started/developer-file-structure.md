<!-- Filename: J4.x:Developer:_File_Structure / Display title: Esempio di Struttura dei File -->

## Introduzione

Come individuo che inizia a lavorare con lo sviluppo di estensioni Joomla su un computer personale, portatile o desktop, è necessario impostare una struttura di file adatta per il codice della tua estensione. La posizione del tuo sito Joomla è predefinita dal sistema operativo e dall'installazione di Apache. La posizione del codice che crei dipende da te.

## Posizione del sito web di prova

In questo esempio, i siti di test Joomla si trovano in sottocartelle della root del documento. Questo consente di creare molti siti web per vari tipi di progetti senza la necessità di creare host virtuali. Alcuni siti di test potrebbero non essere affatto correlati a Joomla. La root del sito per diverse piattaforme:

- Mac: /Utenti/nomeutente/Siti
- Linux: /home/nomeutente/public_html
- Windows: ...

Questa è un'istantanea di parte di un elenco della cartella Siti che mostra una selezione di molti siti di test:

![multiple sites on mac](../../../en/images/getting-started/developer-file-structure-mac-sites.png)

Ognuno è accessibile tramite il nome della sua sottocartella. Esempi:

- `http://localhost/j4test`
- `http://localhost/j520`

Ci sono circostanze in cui potresti preferire creare siti virtuali separati. Questo non è trattato qui.

## Struttura dei File del Sito Web di Test

Se non l'hai già fatto, dovrai familiarizzare con la struttura di un sito web Joomla. L'illustrazione seguente mostra una tipica struttura di file e cartelle Joomla, con la cartella Administrator espansa per mostrarne il contenuto.

![joomla file structure with administrator expanded](../../../en/images/getting-started/developer-file-structure-mac-joomla.png)

Questo è il luogo in cui verrà installato il codice funzionante. Il codice sorgente si trova altrove.

## Posizione del Codice dell'Estensione per Sviluppatori

La posizione del tuo codice di estensione è una scelta personale. Mi piace mantenere il mio codice di estensione in una struttura di file adatta alla creazione di un file zip installabile. La base della mia struttura è /Users/username/git perché so come scrivere git e utilizzo git per il controllo di versione. Non è necessario farlo - git sarà trattato in un tutorial separato. La mia cartella principale git contiene molte sottocartelle che possono utilizzare cartelle git separate per il controllo di versione. Questa è una schermata che mostra un elenco parziale di progetti:

![joomla file structure project folders](../../../en/images/getting-started/developer-file-structure-mac-project-folders.png)

Nota che alcuni dei nomi delle cartelle iniziano con `j4xdemos`, che ho adottato come prima parte dello spazio dei nomi utilizzato per i miei progetti creati a scopo di tutorial su Joomla 4. Non è necessario far parte del nome della cartella, ma è qualcosa a cui pensare: la prima parte del tuo spazio dei nomi deve essere qualcosa di unico per te o per la tua organizzazione. Successivamente, ho adottato `cefjdemos` come prefisso dello spazio dei nomi, in quanto è più personale e non specifico per una versione di Joomla.

### Struttura della Cartella del Progetto

Prendendo j4xdemos-com-mywalks come esempio, tutto il codice che andrà nell'estensione si trova all'interno della cartella com_mywalks. Quando questa è compressa, il file com_mywalks.zip creato viene utilizzato per l'installazione in Joomla. Nessuno degli altri file nella root è incluso nel file zip, ma possono essere inclusi nel Repository GitHub. Ad esempio, README.md è un file di testo in formato Markdown contenente una breve descrizione dell'estensione. Il nome della cartella j4xdemos-com-mywalks non è significativo. Non viene utilizzato altrove se non per ordinare le cartelle in ordine alfabetico.

Nell'illustrazione seguente, la cartella j4xdemos-com-mywalks è stata aperta in VSCodium per mostrare la struttura del codice del progetto. Il file mywalks.xml è un file manifesto che indica a Joomla cosa installare e dove. Le cartelle admin e site contengono il codice che andrà in administrator/components/com_mywalks e components/com_mywalks.

![Project folder open in vscodium](../../../en/images/getting-started/developer-file-structure-mac-vscodium.png)

Dovrebbe essere ovvio che anche un piccolo componente necessita di molti file e cartelle. Sono disponibili strumenti di base per la creazione di estensioni per creare rapidamente un componente scheletro. Sono trattati altrove. ToDo

Pronto a creare un po' di codice?

*Tradotto da openai.com*
