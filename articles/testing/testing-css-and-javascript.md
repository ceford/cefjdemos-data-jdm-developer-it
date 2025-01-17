<!-- Filename: J4.x:SCSS_and_Sass / Display title: Testare CSS e JavaScript -->

## Introduzione

In un sito Joomla di produzione, Joomla fornisce file CSS e Javascript compressi (quelli con `.min` nel nome del file). I server invieranno le versioni gzipped se disponibili (quelle che terminano con un suffisso `.gz`). Questi file sono creati a partire da sorgenti non compressi. Nel caso dei file CSS, sono spesso creati elaborando precursori SCSS. Per testare il codice che include CSS o JavaScript nuovi o aggiornati, è necessario ricostruire i file CSS e le versioni compresse e minimizzate dalle sorgenti modificate.

## Test di Installazione

Per scopi di test, è necessario un server di prova che abbia installato Git, Node.js e Composer. Vai al repository [Joomla CMS](https://github.com/joomla/joomla-cms) su GitHub e segui le istruzioni su *Come ottenere un'installazione funzionante dal sorgente* verso la fine del testo README.

Al completamento dell'installazione di Joomla non eliminare la Directory di Installazione! Questo eliminerà anche la directory `build` necessaria per ricostruire i file CSS e JavaScript.

I file `.scss` principali si trovano nelle seguenti directory:

- media/modelli/sito/cassiopeia/scss
- media/modelli/amministratore/atum/scss

Il script di generazione CSS, il compilatore SCSS e altri strumenti di build simili si trovano nella directory `build/`. La directory di build è disponibile solo dalla fonte di Joomlaǃ, non è inclusa in una release ufficiale di Joomlaǃ.

Le istruzioni di installazione includono le seguenti:

```sh
git checkout 5.2-dev (or whatever branch you wish to work with)
composer install
npm ci
```

Il comando `npm ci` è un sinonimo di `npm clean-install` utilizzato in qualsiasi situazione in cui si desidera assicurarsi di eseguire un'installazione pulita delle proprie dipendenze.

## Uso quotidiano

Ci sono comandi alternativi da utilizzare in situazioni in cui sono stati modificati solo i file SCSS o JavaScript:

```sh
npm run build:css¶
    This command compiles SCSS files to CSS and also creates the minified files.

npm run build:js¶
    This command compiles and transpiles the JavaScript files to the correct format and creates minified files.
```

I comandi scansionano le directory media e template e costruiscono le versioni finali dei file richieste da un'installazione Joomla.

## Sass, SCSS e CSS

> Sass è un linguaggio di fogli di stile che viene compilato in CSS. Ti permette di usare variabili, regole annidate, mixin, funzioni e altro, tutto con una sintassi completamente compatibile con CSS. Sass aiuta a mantenere organizzati i fogli di stile di grandi dimensioni e facilita la condivisione del design all'interno e tra i progetti. I file Sass hanno il suffisso `scss`.

### CSS

Il codice CSS è espresso come segueː

```css
#header {
    margin: 0;
    border: 1px solid blue;
}
#header p {
    font-size: 14px;
    color: blue;
}
#header a {
    text-decoration: none;
}
```

### SCSS

`SCSS` è un'estensione della sintassi di CSS. È utilizzato nel core di Joomlaǃ

```css
$color:    blue;
#header {
    margin: 0;
    border: 1px solid $color;
    p {
        color: $colorRed;
        font: {
            size: 14px;
        }
    }
    a {
        text-decoration: none;
    }
}
```

Una sintassi `Sass` più vecchia offre un modo più conciso di scrivere CSS.

```css
$color:    blue
#header
    margin: 0
    border: 1px solid $color
        p
            color: $colorRed
            font:
                size: 14px
        a
            text-decoration: none
```

Puoi trovare maggiori informazioni nella [Documentazione Sass](http://sass-lang.com/documentation/syntax/).

## Da CSS esistente a SCSS

Se desideri personalizzare il modello Cassiopeia, è una buona idea copiare il modello e personalizzarlo successivamente in modo che gli aggiornamenti di Joomla! non sovrascrivano le tue personalizzazioni. Per aggiungere i tuoi file CSS a una copia del modello Cassiopeia, basta rinominare i tuoi file `.css` in `.scss`. Puoi quindi sfruttare le funzionalità che SCSS offre:

- Estensioni di linguaggio come variabili, annidamento e mixin
- Molte funzioni utili per manipolare colori e altri valori
- Funzionalità avanzate come direttive di controllo per librerie
- Output ben formattato e personalizzabile

Consulta il [sito di Sass](https://sass-lang.com/) per i dettagli completi.

### Importa i tuoi file .css come file .scss

Supponendo che tu voglia includere i tuoi file personalizzati e farli analizzare dal compilatore SCSS - NON hai bisogno di riscrivere il tuo .css in SCSS perché anche il semplice `.css` funziona. Quello che devi fare:

- rinomina i tuoi file `.css` in `.scss`
- prefissali con un `_`
- aggiungi un'istruzione `@import` in fondo a `media/templates/site/copy_of_cassiopeia/scss/template.scss` in modo che sovrascriva le dichiarazioni esistenti:

```css
// Bootstrap functions
@import "../../../media/vendor/bootstrap/scss/functions";
//...
// 50 or more lines of import statements
// Finally add the cassiopeia colours
:root {
  @each $color, $value in $cassiopeia-colors {
    --#{$color}: #{$value};
  }
// More lines containing scss color statements, then your own styles:
@import "mystyles";
}
```

Se ora compili il tuo file main template.scss, otterrai un unico main template.css ottimizzato e minificato. Hai anche ridotto le tue richieste http e il sito dovrebbe caricarsi più velocemente.

*Tradotto da openai.com*

