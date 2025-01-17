<!-- Filename: J4.x:Web_Assets / Display title: Risorse Web -->

## Informazioni sugli asset web

C'è una descrizione completa delle Risorse Web nella Documentazione per Programmatori di Joomla!, riprodotta in [questo sito](jdocmanual?article=docus/web-asset-manager/index) o disponibile dalla [fonte originale](https://manual.joomla.org/docs/general-concepts/web-asset-manager/).

## Esempi Aggiuntivi

Nel Jdocmanual, molti degli articoli contengono blocchi di codice che beneficiano dell'evidenziazione della sintassi. Ecco come si ottiene:

```php
/** @var Joomla\CMS\WebAsset\WebAssetManager $wa */
$wa = $this->document->getWebAssetManager();

// Register and attach a custom item in one run
$wa->registerAndUseStyle('highlight', 'https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/styles/default.min.css', [], [], []);

// Register and attach a custom item in one run
$wa->registerAndUseScript('highlight','https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/highlight.min.js', [], [], ['core']);

// Add an inline content as usual, will be rendered in flow after all assets
$wa->addInlineScript('hljs.highlightAll();');
```

Questo codice si trova nel file `default.php` utilizzato per visualizzare questa pagina! È un po' complicato da implementare perché la chiamata `hljs.highlightAll()` deve essere effettuata dopo che i file `css` e `js` sono stati caricati e di nuovo ogni volta che il contenuto della pagina viene modificato con una chiamata JavaScript.

Altri evidenziatori di sintassi sono disponibili!

*Tradotto da openai.com*

