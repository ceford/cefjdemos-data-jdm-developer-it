<!-- Filename: J4.x:Developer:_Required_Software / Display title: Configurazione del Database -->

## Informazioni su MySQL e MariaDB

I nuovi arrivati possono avere l'impressione che MySQL e MariaDB siano database e potrebbero confondersi quando le istruzioni dicono *creare un nuovo database*. In realtà, entrambi sono Sistemi di Gestione di Database Relazionali (RDBMS) che possono gestire molti database individuali. Il tuo sito di test locale può avere molte installazioni Joomla individuali, ciascuna con il proprio database. Ad esempio, potresti voler testare la tua estensione nella versione attuale di Joomla e separatamente in una prossima release candidate.

Lo screenshot seguente mostra parte di un elenco di oltre 30 database creati per testare varie installazioni di Joomla e progetti di estensioni.

![Phypadmin screenshot of list of databases](../../../en/images/getting-started/phpmyadmin-databases.png)

Una nota a margine: le collazioni sono principalmente utf8mb4_0900_ai_ci:

- utf8mb4 significa che ogni carattere è memorizzato con un massimo di 4 byte nello schema di codifica UTF-8.
- 0900 si riferisce alla versione dell'Algoritmo di Collazione Unicode.
- ai si riferisce all'insensibilità agli accenti, non c'è differenza tra e, è, é, ê ed ë durante l'ordinamento.
- ci si riferisce all'insensibilità alle maiuscole, non c'è differenza tra p e P durante l'ordinamento.

Le tabelle e le colonne individuali possono avere una diversa intercalazione. Le tabelle di Joomla in genere hanno l'intercalazione utf8mb4_unicode_ci.

## Configurazione del Database con phpMyAdmin

Prima di installare Joomla, è necessario avere un database vuoto pronto per essere popolato. È inoltre necessario un utente del database.

### Creare un database

- **Avvia phpMyAdmin** Inserisci localhost/phpmyadmin nella barra degli URL del tuo browser.
- **Accedi** A seconda di come è stato installato, il nome utente sarà root o admin e potrebbe esserci o meno una password.
- Seleziona **Basi di dati** dal menu in alto nella pagina principale di phpMyAdmin.
- In **Crea database** inserisci un breve nome al posto del suggerimento **Nome database**, ad esempio, jtest.
- Seleziona **utf8mb4_0900_ai_ci** dall'elenco a discesa della Collazione.
- Seleziona **Crea** per creare il database.

Questo ti porterà a un database vuoto. In alto c'è un messaggio: *Nessuna tabella trovata nel database.*

### Crea un utente

- Seleziona l'icona **Home** in alto a sinistra di phpMyAdmin per andare alla pagina principale.
- Seleziona **Account Utenti** dal menu principale della Home.
- Seleziona **Aggiungi Account Utente** dal pannello Nuovo sotto l'elenco degli utenti correnti (se presenti).
- Inserisci un **Nome utente** che può essere un nome breve che ti servirà durante l'installazione di Joomla. Esempio: jtest. Puoi usare questo stesso utente per altri database creati in seguito!
- Seleziona **Locale** dall'elenco del campo Hostname. Imposterà localhost nel campo di valore adiacente.
- Usa il pulsante **Genera** per generare una password. Devi copiare il valore generato e incollarlo in un editor di testo per utilizzarlo in seguito. Non è necessario ricordarlo a lungo termine poiché sarà memorizzato come testo semplice nel file configuration.php di Joomla. Esempio: 8t8mGQq.gw\[\]8lp(
- **Salva** salta le sezioni Database per l'utente e Prerogative globali del modulo. Il pulsante **Vai** (Salva) si trova in basso.

### Assegna le autorizzazioni del database all'utente

- Nella pagina **Account Utente** seleziona l'utente (jtest), se necessario tramite Home / Account Utente / Nome Utente.
- Seleziona **Database** vicino alla parte superiore della pagina. Ciò mostrerà un elenco di database ai quali a questo utente sono stati concessi i permessi di accesso e, in fondo, un elenco di database ai quali non è stato concesso l'accesso.
- **Seleziona** il database al quale si desidera concedere l'accesso e seleziona il pulsante **Vai**.
- **Privilegi specifici del database** Seleziona **Seleziona tutto** e poi **Vai** per salvare.

Ecco fatto! Ora puoi disconnetterti da phpMyAdmin. Hai dimenticato di annotare la password dell'utente del database? Torna indietro e modifica l'account utente che hai creato per cambiarla. Se utilizzi lo stesso utente del database per più database Joomla, troverai la password in un file configuration.php di Joomla.

*Tradotto da openai.com*

