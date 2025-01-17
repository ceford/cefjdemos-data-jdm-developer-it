<!-- Filename: J4.x:Http_Header_Management / Display title: Intestazioni HTTP -->

## Introduzione

Joomla 4 ha introdotto un sistema di intestazioni HTTP progettato per aiutare i proprietari dei siti a configurare le intestazioni di sicurezza HTTP. È implementato utilizzando un plugin *Sistema - Intestazioni HTTP*. Esiste un completo tutorial [Utente](jdocmanual?article=user/security/http-headers) su questo argomento. Questo tutorial è più breve e copre alcuni punti rilevanti per gli sviluppatori.

## Il Sistema - Plugin delle Intestazioni HTTP

### Scheda plugin

Vai su **Sistema → Plugin → Sistema - Intestazioni HTTP** per accedere al modulo di configurazione del plugin.

![System http headers plugin form](../../../en/images/security/security-http-headers-plugin.png)

- **X-Frame Options** Questo è abilitato per impostazione predefinita, ma la [documentazione](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options) afferma che è deprecato e dovrebbe essere utilizzata una politica di *frame-ancestors*.
- **Referrer-Policy** L'impostazione predefinita è *strict-origin-when-cross-origin*.
- **Cross-Origin-Opener-Policy** Il valore predefinito di Joomla è `same-origin`.
- **Force HTTP Headers** Non ci sono intestazioni forzate impostate di default. Qui è dove può essere specificata un'alternativa a *X-Frame Options*. Il valore di `Content-Security-Policy` può essere uno dei seguenti:
    - `'none'`
    - `'self' https://www.example.org;`
    - `'self' https://example.org https://example.com https://store.example.com;`

Usando il sottoform **Force HTTP Headers** puoi anche forzare i seguenti header:

- [Politica di Sicurezza dei Contenuti](https://scotthelme.co.uk/content-security-policy-an-introduction/)
- [Politica di Sicurezza dei Contenuti-Report Solo](https://scotthelme.co.uk/content-security-policy-an-introduction/#testingapolicy)
- [Politica di Apertura per Origini Diverse](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cross-Origin-Opener-Policy)
- [Aspettativa CT](https://scotthelme.co.uk/a-new-security-header-expect-ct/)
- [Politica delle Funzionalità & Politica dei Permessi](https://scotthelme.co.uk/a-new-security-header-feature-policy/)
- [NEL (Registrazione delle Risposte di Rete)](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/NEL)
- [Politica del Referer](https://scotthelme.co.uk/a-new-security-header-referrer-policy/)
- [Relazione a](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/report-to)
- [Trasporto Sicuro Rigoroso](https://scotthelme.co.uk/hsts-the-missing-link-in-tls/)
- [Opzioni X-Frame](https://scotthelme.co.uk/hardening-your-http-response-headers/#x-frame-options)

### Scheda Strict-Transport-Security (HSTS)

![strict transport security settings](../../../en/images/security/security-http-headers-hsts.png)

Usa il pulsante *Attiva/Disattiva Aiuto in Linea* per ottenere informazioni su ciascun parametro. Riferimento illustrato:

[Modulo per verificare o impostare lo stato di preload HSTS e l'idoneità](https://hstspreload.org/)

### Scheda Content-Security-Policy (CSP)

![Content security policy options](../../../en/images/security/security-http-headers-csp.png)

Una volta abilitato, puoi impostare il client in cui desideri applicare il CSP configurato, consentendoti di impostare `site`, `administrator` o `both`. Un CSP dovrebbe essere applicato sia al frontend che al backend. Riferimenti illustrati:

- [Politica di Sicurezza dei Contenuti](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP)
- [Nonce](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/nonce)
- [Hash di Script e Stile](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/script-src)
- Le descrizioni dei parametri della [Direttiva Politica](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/child-src) src sono disponibili nel menu di questa pagina.

L'opzione finale chiamata *Aggiungi Direttiva* ti consente di configurare la lista di autorizzazioni per direttiva secondo le tue esigenze. Ad esempio, per la direttiva *script-src* il campo *Valore* dovrebbe contenere le origini da cui vuoi consentire il caricamento degli script.

## Note

Quando hai configurato alcune intestazioni di sicurezza HTTP direttamente sul server, potrebbero esserci delle doppie voci.

Verifica l'output delle tue intestazioni HTTP nella console del browser. In Google Chrome o Firefox: Ispeziona → Rete → l'output sotto Intestazioni. Puoi quindi disabilitare le intestazioni che causano voci duplicate. Controlla anche la console del tuo browser per possibili errori.

## Sviluppatori di estensioni

Il grande vantaggio di una Content Security Policy si verifica quando l'Header blocca tutto il JavaScript inline e il CSS inline che influenzano i gestori di eventi JavaScript tramite attributi HTML. Con la protezione del browser abilitata, il JavaScript inline e il CSS inline sono bloccati anche per le estensioni. Questa protezione non è abilitata di default ma può essere attivata dagli utenti.

Dove sono richiesti JavaScript e CSS inline, il supporto per nonce e hash è incluso nelle API del Documento. Quando usati, il core si assicurerà che siano nella lista bianca ma bloccherà comunque il codice dannoso.

### Note importanti per gli sviluppatori di estensioni

A partire da Joomla 4.0 la Content Security Policy:

- è fornito con il core.
- è disabilitato di default.
- può essere abilitato dagli amministratori del sito.
- è fortemente raccomandato che il frontend e il backend della tua estensione funzionino con la Content Security Policy abilitata.

Con una rigorosa Politica di Sicurezza dei Contenuti abilitata le seguenti funzionalità saranno bloccate:

- L'esecuzione di JavaScript tramite i gestori di eventi HTML (gestori onXXX come onClick e simili).
- L'esecuzione di JavaScript nella pagina non passato alla pagina tramite l'API Document.
- L'esecuzione di codice JavaScript iniettato in API DOM come eval().
- L'uso di CSS inline nella pagina non passato alla pagina tramite l'API Document.
- L'uso di CSS inline utilizzando l'attributo style dell'HTML.

Per far funzionare le tue estensioni anche con una rigorosa Content Security Policy abilitata, il modo più semplice è utilizzare l'API Document per applicare il tuo JavaScript e CSS inline. Vedi gli esempi sotto.

### Aggiunta di JavaScript utilizzando l'API di Joomla

```php
    use Joomla\CMS\Factory;

    /** @var Joomla\CMS\WebAsset\WebAssetManager $wa */
    $wa = Factory::getApplication()->getDocument()->getWebAssetManager();

    // Add JavaScript from URL
    $wa->registerAndUseScript('com_example.sample', 'https://example.org/sample.js', [], ['defer' => true]);

    // Add inline JavaScript
    $wa->addInlineScript('
        document.addEventListener("DOMContentLoaded", function(event) {
            alert("An inline JavaScript Declaration");
        });
    ');
```

### Aggiungere CSS utilizzando l'API di Joomla

```php
    use Joomla\CMS\Factory;

    /** @var Joomla\CMS\WebAsset\WebAssetManager $wa */
    $wa = Factory::getApplication()->getDocument()->getWebAssetManager();

    // Add Style from URL
    $wa->registerAndUseStyle('com_example.sample', 'https://example.org/sample.css');

    // Add inline Style
    $wa->addInlineStyle('
        body {
            background: #00ff00;
            color: rgb(0,0,255);
        }
    ');
```

## Risorse aggiuntive

- [CSP Cheat Sheet](https://scotthelme.co.uk/csp-cheat-sheet/)
- [Introduzione alla Content Security Policy](https://scotthelme.co.uk/content-security-policy-an-introduction/)
- [Security Headers](https://securityheaders.com/) fa parte di Probely ed è stato originariamente creato da Scott Helme! È uno strumento gratuito e facile da usare progettato per aiutarti a distribuire e comprendere meglio le funzionalità di sicurezza moderne disponibili per il tuo sito web.
- [CSP Evaluator](https://csp-evaluator.withgoogle.com/)
- [Fondamenti Web Content Security Policy](https://developers.google.com/web/fundamentals/security/csp)
- [Documentazione CSP di Google](https://csp.withgoogle.com/docs/index.html)
- [CSP è morto, lunga vita a CSP!](https://research.google/pubs/pub45542/) Sull'insicurezza delle Whitelist e il futuro della Content Security Policy
- [Ricerca su web.dev per Sicurezza](https://web.dev/s/results?q=security#gsc.tab=0&gsc.q=security&gsc.sort=)

*Tradotto da openai.com*

