<!-- Filename: J4.x:Developer:_Required_Software / Display title: Installa Joomla -->

## Sommario

Questo è solo un breve riepilogo dei passaggi coinvolti:

- **Scarica** l'ultima versione completa dalla pagina [Joomla Downloads](https://downloads.joomla.org/).
- **Salva** il file scaricato nella radice del documento o in una sottocartella della radice.
- **Decomprimi** il file scaricato nello stesso punto. Alcuni sistemi operativi creeranno una cartella con lo stesso nome del file zip scaricato, senza lo zip. Questo va bene - puoi semplicemente rinominare la cartella con un nome corto e spostarla se necessario. Altri sistemi operativi spacchetteranno i file e le cartelle nello stesso punto. Questo è negativo se hai messo il download nella tua cartella radice dove ci sono cartelle esistenti con altri siti. Dovrai creare un nome di cartella corto e spostare tutti i nuovi file e cartelle estratti al suo interno. L'obiettivo è ottenere una cartella a cui puoi accedere con il tuo browser web tramite localhost/j4test.
- **Installa** puntando il tuo browser su localhost/j4test e compila i moduli di installazione di Joomla.

## Configurazione

Alcuni suggerimenti:

- **Configurazione Globale / Sito / Cookie / Percorso Cookie** impostato sulla cartella contenente l'installazione di Joomla (/j4test).
- **Configurazione Globale / Sistema / Debug / Debug Sistema** impostato su Sì.
- **Configurazione Globale / Sistema / Durata Sessione** impostato su 60 - altrimenti vieni disconnesso mentre stai pensando.
- **Configurazione Globale / Server / Server / Segnalazione Errori** impostato su Massimo.
- **Plugin Sistema - Debug / Plugin / Aggiorna Risorse** impostato su No a meno che tu non stia eseguendo il debug di CSS o javascript.

Ecco fatto. Se Joomla funziona, sei pronto a usarlo per lo sviluppo di estensioni.

## Altri Siti

Puoi installare quanti siti desideri su un singolo computer. A seconda di come hai configurato il tuo server, potrebbe essere tramite diverse sottocartelle accessibili tramite localhost/test1, localhost/test2 e così via, oppure tramite host virtuali accessibili tramite test1.localhost, test2.localhost e così via. In entrambi i casi, puoi avere un nuovo database e un nuovo sito Joomla pulito in pochi minuti. Scegli nomi brevi significativi! *test1* e *test2* diventeranno presto fonte di confusione.

## Installazione per il Test

C'è una procedura diversa se vuoi aiutare con i test di Joomla. In questo caso dovresti installare **git** e seguire le istruzioni nel [GitHub Repository](https://github.com/joomla/joomla-cms).

- su GitHub, seleziona il branch di Joomla su cui lavorare. Questo modifica le istruzioni visualizzate più in basso nella pagina.
- Sul tuo laptop o desktop, segui le istruzioni a partire da *Clonare il repository:* in poi.
- Non eliminare la directory di installazione alla fine dell'installazione di Joomla!
- Rinomina il clone da joomla-cms a qualcos'altro così puoi rifarlo tutto di nuovo più tardi.
- Installa il Joomla Patchtester.

*Tradotto da openai.com*

