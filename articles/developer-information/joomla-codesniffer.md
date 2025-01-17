<!-- Filename: Joomla_CodeSniffer / Display title: Standard di Codifica -->

<div class="alert alert-warning">
La parte finale di questo articolo deve essere aggiornata!
</div>

## Una panoramica sull'IA

Gli standard di codifica sono importanti per lo sviluppo del software perché:

- **Migliorare la qualità del codice**
  - Gli standard di codifica aiutano a garantire che il codice sia affidabile, sicuro e protetto. Possono anche aiutare a ridurre i problemi di prestazioni e le preoccupazioni sulla sicurezza che potrebbero derivare da pratiche di codifica scadenti.
- **Rendere il codice più leggibile e mantenibile**
  - Gli standard di codifica aiutano a rendere il codice più facile da comprendere, leggere e mantenere. Ciò può facilitare anche il lavoro dei nuovi sviluppatori con il codice.
- **Velocizzare lo sviluppo**
  - Gli standard di codifica possono aiutare gli sviluppatori a evitare errori comuni che possono rallentare i processi di codifica.
- **Migliorare la collaborazione**
  - Gli standard di codifica possono facilitare la collaborazione tra gli sviluppatori, anche in team numerosi.
- **Garantire la coerenza**
  - Gli standard di codifica aiutano a garantire che il codice sia coerente tra i progetti. Ciò può facilitare il lavoro congiunto degli sviluppatori sugli stessi progetti.
- **Migliorare la scalabilità**
  - Gli standard di codifica possono aiutare a garantire che il codice possa essere scalato senza diventare ingovernabile.
- **Fornire criteri chiari per le revisioni del codice**
  - Gli standard di codifica possono aiutare a fornire criteri chiari per le revisioni del codice, il che può portare a un feedback più efficace.

Gli standard di codifica spesso includono regole per l'indentazione, la lunghezza delle righe, il posizionamento delle parentesi e la spaziatura.

Joomla utilizza lo standard di codifica [PSR-12](https://www.php-fig.org/psr/psr-12/). Puoi abilitare questo standard di codifica nel tuo IDE e ottenere suggerimenti se non stai seguendo lo standard di codifica o utilizzare anche una correzione automatica. Raccomandiamo di seguire questo standard quando sviluppi le tue estensioni per rimanere compatibile con il core e garantire che il tuo codice funzioni possibilmente con le versioni future.

## PHP Code Sniffer

Si prega di consultare l'attuale [PHP_CodeSniffer](https://github.com/PHPCSStandards/PHP_CodeSniffer/) per informazioni su questa utilità e su come installarla. Si noti che la fonte originale è abbandonata, ma potrebbe essere elencata dai motori di ricerca. Ci sono due script:

- **phpcs** rileva violazioni di uno standard di codifica e produce un report.
- **phpcbf** tenta di correggere le violazioni degli standard di codifica e produce un report su ciò che ha fatto.

Puoi installare gli script individuali o utilizzare composer per installarli. Puoi anche trovarli in un clone di Joomla situato in libraries/vendor/bin insieme ad alcune altre utilità utili.

## Testare PHP Code Sniffer

Se inserisci un'installazione globale nel tuo `$PATH`, puoi eseguire il code sniffer dalla riga di comando nella radice di un progetto. Prova questo per visualizzare un elenco di standard di codifica:

```sh
phpcs -i
The installed coding standards are MySource, PEAR, PSR1, PSR2, PSR12, Squiz and Zend
```

Ad esempio il comando seguente è stato utilizzato in una cartella di progetto più vecchia che utilizzava il precedente standard di codifica personalizzato di Joomla. Tra le altre cose, usava tabulazioni anziché spazi per il layout. Molte linee simili sono state omesse di seguito per brevità.

```sh
phpcs --standard=PSR12 .

FILE: /Users/ceford/git/j4xdemos-plg-toc/j4xdemostoc/j4xdemostoc.php
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
FOUND 132 ERRORS AND 3 WARNINGS AFFECTING 116 LINES
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   1 | WARNING | [ ] A file should declare new symbols (classes, functions, constants, etc.) and cause no other side effects, or it should execute logic with side effects, but should not do both. The
     |         |     first symbol is defined on line 22 and the first side effect is on line 10.
   1 | ERROR   | [x] Header blocks must be separated by a single blank line
  22 | ERROR   | [ ] Each class must be in a namespace of at least one level (a top-level vendor name)
  24 | ERROR   | [x] Spaces must be used to indent lines; tabs are not allowed
  25 | ERROR   | [x] Spaces must be used to indent lines; tabs are not allowed
  26 | ERROR   | [x] Spaces must be used to indent lines; tabs are not allowed
  ...
  42 | ERROR   | [x] Expected 1 space after closing parenthesis; found newline
...
  48 | ERROR   | [x] No space found after comma in argument list
  48 | ERROR   | [x] Expected 1 space after closing parenthesis; found newline
...
  67 | ERROR   | [x] Expected 0 spaces before closing parenthesis; 1 found
...
  75 | ERROR   | [x] Space after opening parenthesis of function call prohibited
  75 | ERROR   | [x] Expected 0 spaces before closing parenthesis; 1 found
...
 138 | WARNING | [ ] Line exceeds 120 characters; contains 168 characters
 139 | ERROR   | [x] Spaces must be used to indent lines; tabs are not allowed
 139 | WARNING | [ ] Line exceeds 120 characters; contains 141 characters
...
 156 | ERROR   | [x] Spaces must be used to indent lines; tabs are not allowed
 157 | ERROR   | [x] Expected 1 newline at end of file; 0 found
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
PHPCBF CAN FIX THE 131 MARKED SNIFF VIOLATIONS AUTOMATICALLY
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Time: 123ms; Memory: 8MB
```

Il precedente esempio di progetto conteneva un singolo file php e nessun file css o js. phpcs produce un report per ciascun file php, css e js in un progetto. Ecco alcuni esempi per i file css e js:

```sh
FILE: /Users/ceford/git/j4x-demos-com-mediacat/com_mediacat/media/css/mediacat.css
----------------------------------------------------------------------------------
FOUND 33 ERRORS AFFECTING 32 LINES
----------------------------------------------------------------------------------
  3 | ERROR | [x] Spaces must be used to indent lines; tabs are not allowed
...
 51 | ERROR | [x] Whitespace found at end of line
...
 79 | ERROR | [x] Spaces must be used to indent lines; tabs are not allowed
----------------------------------------------------------------------------------
PHPCBF CAN FIX THE 33 MARKED SNIFF VIOLATIONS AUTOMATICALLY
----------------------------------------------------------------------------------

FILE: /Users/ceford/git/j4x-demos-com-mediacat/com_mediacat/media/css/file-icon-classic.min.css
-----------------------------------------------------------------------------------------------
FOUND 0 ERRORS AND 1 WARNING AFFECTING 1 LINE
-----------------------------------------------------------------------------------------------
 1 | WARNING | File appears to be minified and cannot be processed
-----------------------------------------------------------------------------------------------

FILE: /Users/ceford/git/j4x-demos-com-mediacat/com_mediacat/media/js/mediacat-site.js
-------------------------------------------------------------------------------------
FOUND 38 ERRORS AFFECTING 30 LINES
-------------------------------------------------------------------------------------
  3 | ERROR | [x] Spaces must be used to indent lines; tabs are not allowed
  5 | ERROR | [x] Expected 1 space after FUNCTION keyword; 0 found
  6 | ERROR | [x] Spaces must be used to indent lines; tabs are not allowed
...
 13 | ERROR | [x] Opening brace should be on a new line
...
 29 | ERROR | [x] Spaces must be used to indent lines; tabs are not allowed
 29 | ERROR | [x] Expected at least 1 space before "+"; 0 found
 29 | ERROR | [x] Expected at least 1 space after "+"; 0 found
...
 36 | ERROR | [x] Spaces must be used to indent lines; tabs are not allowed
-------------------------------------------------------------------------------------
PHPCBF CAN FIX THE 38 MARKED SNIFF VIOLATIONS AUTOMATICALLY
-------------------------------------------------------------------------------------
```

## Variazioni di Comando

È possibile ottenere aiuto con i comandi phpcs:

```sh
phpcs --help
```

### Escludere uno o più file

Usa un elenco di modelli di file separati da virgole per escludere i file dalla convalida dello stile del codice. Esempio

```php
phpcs --standard=PSR12 --ignore='libraries/*' .
```

### Escludi una o più regole

Joomla consente linee più lunghe rispetto allo standard PSR, 560 invece di 120. Il seguente comando può essere utilizzato per omettere gli avvisi di linee lunghe:

```sh
phpcs --standard=PSR12 --ignore='libraries/*' --exclude=Generic.Files.LineLength .
```

Puoi trovare la regola che viene violata con questo comando:

```sh
phpcs -s yourfile.php
```

### Eccezioni Joomla

Per lo sviluppo di un'estensione utilizzando un IDE, potresti decidere di utilizzare lo standard PSR12 senza alcuna eccezione. Joomla ha un [set di regole personalizzato](https://github.com/joomla/joomla-cms/blob/5.2-dev/ruleset.xml) che consente molte eccezioni. Viene utilizzato per la convalida dell'intera installazione di Joomla durante i test del sistema.

## Correzione delle violazioni

Il singolo file php che `FOUND 132 ERRORS AND 3 WARNINGS AFFECTING 116 LINES` mostrato sopra può essere in gran parte corretto come segue:

```sh
phpcbf --standard=PSR12 .

PHPCBF RESULT SUMMARY
-----------------------------------------------------------------------------------
FILE                                                               FIXED  REMAINING
-----------------------------------------------------------------------------------
/Users/ceford/git/j4xdemos-plg-toc/j4xdemostoc/j4xdemostoc.php     131    4
-----------------------------------------------------------------------------------
A TOTAL OF 131 ERRORS WERE FIXED IN 1 FILE
-----------------------------------------------------------------------------------

Time: 232ms; Memory: 8MB
```

Eseguendo nuovamente l'utilità phpcs viene mostrato quali problemi rimangono:

```sh
phpcs --standard=PSR12 .

FILE: /Users/ceford/git/j4xdemos-plg-toc/j4xdemostoc/j4xdemostoc.php
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
FOUND 1 ERROR AND 3 WARNINGS AFFECTING 4 LINES
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
   1 | WARNING | A file should declare new symbols (classes, functions, constants, etc.) and cause no other side effects, or it should execute logic with side effects, but should not do both. The first
     |         | symbol is defined on line 23 and the first side effect is on line 11.
  23 | ERROR   | Each class must be in a namespace of at least one level (a top-level vendor name)
 132 | WARNING | Line exceeds 120 characters; contains 168 characters
 133 | WARNING | Line exceeds 120 characters; contains 141 characters
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Time: 127ms; Memory: 8MB
```

Conclusione: un'estensione codificata per una versione precedente di Joomla e utilizzando un diverso standard di codifica ora necessita di qualche lavoro!

## Installazione negli IDE

La maggior parte degli Ambienti di Sviluppo Integrati può utilizzare il rilevatore di codice mentre lavori o quando salvi un file.

### Installazione in VSCode

In VSCode (e/o VScodium), seleziona l'icona delle Estensioni, cerca PHP_CodeSniffer e installalo. Ha bisogno di configurazione:

1. In **Impostazioni** trova PHP_CodeSniffer
2. Imposta il campo **PHP Code Sniffer → Exec:** in base alla posizione del tuo binario phpcs.
3. Nella lista **PHP Code Sniffer: Standard** seleziona **PSR12**.

Chiudi e sei pronto per l'azione.

Alcuni dei problemi mostrati sopra possono essere risolti con le direttive PSR1.

```php
<?php

/**
 * @package     Whatever
 *
 * @phpcs:disable PSR1.Classes.ClassDeclaration.MissingNamespace
 */

use joomla\CMS\...

// phpcs:disable PSR1.Files.SideEffects
\defined('_JEXEC') or die;
// phpcs:enable PSR1.Files.SideEffects
```

Altri hanno bisogno di un po' di riflessione!

Dopo l'installazione in VSCode, le violazioni dello stile del codice verranno rilevate e contrassegnate con una sottolineatura ondulata rossa. Passa il cursore sul problema per vedere un messaggio e una possibile soluzione, come in questo esempio:

```txt
Header blocks must be separated by a single blank line
PHP_CodeSniffer(PSR12.Files.FileHeader.SpacingAfterBlock)
```

<div class="alert alert-warning">
Le seguenti sezioni devono essere aggiornate!
</div>

### Installazione in PhpStorm

Code Sniffer è supportato di default in PhpStorm. Vai su Impostazioni e sotto **Editor → Ispezioni** vedrai l'elenco dei sniffatori che hai installato.

#### Imposta percorso a Code Sniffer

1. Apri Impostazioni (CTRL-ALT-S / CMD-,)  
2. Vai a Lingue e Strumenti di Sviluppo  
3. Clicca su PHP  
4. Clicca su Strumenti di Qualità  
5. Clicca sulla freccia a discesa di PHP cs fixer  
6. La configurazione è impostata su Locale per impostazione predefinita  
7. Clicca sui 3 punti dietro per aprire la schermata di configurazione  
8. La prima opzione è il percorso di PHP Code Sniffer (phpcs)  
9. Clicca sui 3 punti dietro il percorso per selezionare la posizione del file phpcs. Vedi sopra dove potrebbe essere installato phpcs sul tuo sito  
10. Clicca su Valida per assicurarti che il percorso sia corretto e che phpcs funzioni  
11. Clicca su OK

#### Attivare lo stile del codice

1. Apri Impostazioni (CTRL-ALT-S / CMD-,)
2. Vai a Editor
3. Clicca su Ispezioni
4. Nell'elenco, vai a PHP
5. Clicca su PHP Code Sniffer Validation
6. Clicca sulla casella di controllo accanto per attivarla
7. Clicca sul pulsante Ricarica (2 frecce) per forzare un ricaricamento delle regole dal disco
8. Joomla dovrebbe ora essere disponibile nell'elenco. Vedi immagine seguente.
9. Clicca OK

![CodeSniffer in PHPStorm](../../../en/images/getting-started/core-phpstorm-code-sniffer.png)

### Installazione in Netbeans

Netbeans ha la funzionalità sniffer integrata nel sistema principale.

1. Avvia il tuo IDE Netbeans  
2. Apri **Strumenti → Opzioni → PHP → Analisi del Codice → Code Sniffer**  
3. Devi impostare il percorso a *phpcs.bat* dal pacchetto PHP_CodeSniffer PEAR installato  
    - Per i sistemi basati su Unix il percorso è qualcosa come /usr/bin/phpcs  
    - In XAMPP (Windows) puoi trovare il file nella cartella radice di PHP (es. C:\xampp\php\phpcs.bat)  
4. Come "Standard Predefinito," scegli "Joomla" per utilizzare lo standard Joomla!  
5. Ora puoi cliccare *OK* per iniziare l'analisi  
6. Apri dal menu in alto **Sorgente → Ispeziona...**  
7. Divertiti  

### Installazione in Eclipse

1. **Aiuto → Installa nuovo software...**
2. **Lavora con** Inserisci uno degli URL del sito di aggiornamento.
3. Seleziona gli strumenti desiderati.
4. Riavvia Eclipse.
5. **Finestra → Preferenze**
6. **Strumenti PHP → PHP CodeSniffer**

![Eclipse PTI settings](../../../en/images/getting-started/core-eclipse-pti-settings.png)

Ora puoi annusare le violazioni del codice rispetto agli standard comuni.

![Codesniffer in Eclipse](../../../en/images/getting-started/core-eclipse-pti.png)

### Installazione in Geany

- Apri un file PHP. (Altrimenti il menu di costruzione non è accessibile.)
- Nel menu in alto, seleziona **Build → Set Build Commands**.
- Seleziona il secondo campo e assegnagli un nome a tuo piacimento. Inserisci questo codice nel Comando:<br>
  `phpcs --standard=Joomla "%f" | sed -e 's/^/%f |/' | egrep 'WARNING|ERROR'`
- Inserisci questo codice nel campo Regex delle Errori:  `(.+) [|]\s+([0-9]+)`
- Seleziona OK.
- Se la finestra dei messaggi non è aperta, visualizzala selezionandola nel menu Visualizzazione in alto.
- Quando visualizzi un qualsiasi file PHP, premi F9 per vedere gli errori trovati.

### Installazione in Atom

- Installa phpcs e gli standard Joomla come descritto sopra.
- In **Atom → Preferences → Install** installa **linter-phpcs** e tutti i suoi requisiti.
- In **Atom → Preferences → Packages → linter-phpcs → Settings** regola:
  - **Executable Path** al percorso del tuo phpcs
  - **Code Standard Or Config File**: PSR12
  - **Tab Width**: 4

*Tradotto da openai.com*

