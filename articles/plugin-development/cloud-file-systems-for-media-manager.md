<!-- Filename: J4.x:Cloud_File_Systems_for_Media_Manager / Display title: Sistemi di File Cloud per il Gestore Multimediale -->

<span id="main-portal-heading">GSoC 2017
File System Cloud per Media Manager
Documentazione</span> [<img
src="https://docs.joomla.org/images/thumb/7/7d/Gsoc2016.png/75px-Gsoc2016.png"
decoding="async"
srcset="https://docs.joomla.org/images/thumb/7/7d/Gsoc2016.png/113px-Gsoc2016.png 1.5x, https://docs.joomla.org/images/thumb/7/7d/Gsoc2016.png/150px-Gsoc2016.png 2x"
data-file-width="373" data-file-height="373" width="75" height="75"
alt="Gsoc2016.png" />](https://docs.joomla.org/GSOC_2017 "GSOC 2017")
Joomla! 4.x

## Introduzione

**Joomla! 4.x** viene fornito con sistemi di file cloud per il **Media Manager** di default. Con la precedente API, creare sistemi di file personalizzati era un compito difficile. Grazie alla nuova API, ora è facile creare un sistema di file personalizzato. Se vuoi usare un Servizio Cloud con il nuovo Media Manager, è consigliato utilizzare **OAuth2.0**.

Questo documento ti guiderà attraverso i passaggi importanti per creare il tuo **Plugin del File System** per estendere il **Media Manager**. Prima di procedere, assicurati di avere una conoscenza di base su come sviluppare un plugin per Joomla. [Questo tutorial](https://docs.joomla.org/J3.x:Creating_a_Plugin_for_Joomla) dovrebbe aiutarti.

## Crea il tuo plugin Filesystem

### Configurazione

Prima di tutto, dobbiamo creare un plugin per il **filesystem** per estendere il Media Manager. Questo plugin dovrebbe contenere alcuni attributi importanti affinché possa funzionare con il Media Manager.

Assicurati che il tuo plugin contenga `group="filesystem"`. Quindi nel tuo
`[plugin-name].xml`, dovresti avere:

```xml
<?xml version="1.0" encoding="utf-8"?>
<extension version="4.0" type="plugin" group="filesystem" method="upgrade">
    <name>plg_filesystem_myplugin</name>
    <author>Joomla! Project</author>
    <creationDate>April 2017</creationDate>
    <copyright>Copyright (C) 2005 - 2017 Open Source Matters. All rights reserved.</copyright>
    <license>GNU General Public License version 2 or later; see LICENSE.txt</license>
    <authorEmail>admin@joomla.org</authorEmail>
    <authorUrl>www.joomla.org</authorUrl>
    <version>__DEPLOY_VERSION__</version>
    <description>Description</description>
    <files>
        <filename plugin="myplugin">myplugin.php</filename>
        <folder>SomeFolder</folder>
    </files>

    <config>
        <fields name="params">
            <fieldset name="basic">
                <field
                    name="display_name"
                    type="text"
                    label="YOUR_LABEL"
                    description="YOUR_DESCRIPTION"
                    default="DEFAULT_VALUE"
                />
            </fieldset>
        </fields>
    </config>
</extension>
```

Il parametro **display_name** aiuta il Media Manager a visualizzare il nome del tuo **File System** come nodo radice nel File Browser. Qualsiasi adattatore appartenente al tuo File System verrà visualizzato come figlio sotto la radice.

Includi tutti i parametri richiesti di cui potresti aver bisogno come `App Secret` con campi del modulo adatti.

### Eventi Plugin

- `onFileSystemGetAdapters()`
- `onFileSystemOAuthCallback(\Joomla\Component\Media\Administrator\Event\OAuthCallbackEvent $event)`

#### onFileSystemGetAdapters()

**Qualsiasi** plugin del filesystem dovrebbe contenere un evento chiamato `onFileSystemGetAdapters()` per la funzionalità. Questo evento dovrebbe restituire un **array** di `Joomla\Component\Media\Administrator\Adapter\AdapterInterface` quando viene chiamato. L'evento viene attivato quando si apre il Media Manager. Ogni `AdapterInterface` verrà montato sotto il nodo radice del tuo file system.

#### onFileSystemOAuthCallback()

Questo evento viene attivato quando si utilizza **OAuthCallbackHandler** di Media Manager per il processo di Autorizzazione e Autenticazione OAuth2.0 descritto di seguito nel documento. L'evento viene attivato solo sul plugin richiesto. Quindi non è necessario controllare `$context` in uno scenario tipico.

Un esempio di utilizzo dell'evento appare così:

```php
    public function onFileSystemOAuthCallback(\Joomla\Component\Media\Administrator\Event\OAuthCallbackEvent $event)
    {
        // Your context
        $context = $event->getContext();

        // Get the input
        $data = $event->getInput();

        // Your code goes here

        // Set result to be returned
        $result = [
            "action" => "control-panel"
        ];

        // Pass back the result to event
        $event->setArgument('result', $result);
    }
```

**OAuthCallbackEvent** contiene l'input inoltrato all'URI di Media Manager OAuthCallback. `$event->getInput()` restituisce un oggetto Input.

`$result` definisce come si comporta Joomla dopo un reindirizzamento al callback. Ci sono diverse soluzioni possibili disponibili:

- `action`
  - close: Chiude una finestra aperta da un JavaScript **usando window.open()**
  - redirect: Reindirizza alla pagina specificata dal **redirect_uri**
  - control-panel: Reindirizza al pannello di controllo
  - media-manager: Reindirizza al Media Manager
- `redirect_uri`
  - Utilizzato con l'azione **redirect** (richiesto)
- `message`
  - Il messaggio deve essere visualizzato dopo un'azione
- `message_type`
  - warning
  - notice
  - error
  - message(oppure lasciare vuoto)

Dopo aver impostato tutto, imposta l'argomento `$result` dell'`$event` per restituirlo al chiamante.

Un esempio per mostrare un messaggio all'utente sarebbe:

```php
    $result = [
        "action" => "media-manager",
        "message" => "Some message",
        "message-type" => "notice"
    ];
```

Questo reindirizzerà al Media Manager e solleverà un avviso con il testo in **messaggio**.

Questo metodo può essere tipicamente utilizzato per ottenere codici di autorizzazione per il processo **OAuth2.0**. In caso di **errore**, Joomla! tornerà al pannello di controllo e visualizzerà un messaggio di errore.

## Autenticazione e Autorizzazione

Joomla! 4.x ti consiglia di utilizzare OAuth2.0 per questo processo. È uno scenario comune che OAuth2.0 richieda un **URL di reindirizzamento** per passare i dati di autenticazione all'applicazione. Questo viene tipicamente fatto tramite un gestore di callback. Per il tuo plugin, non è necessario reinventare la ruota, puoi utilizzare il **Gestore di Callback** di **Media Manager** per svolgere il compito.

Tutto ciò che devi fare è impostare il **Redirect URI** come segue nel tuo
Provider OAuth2.0 e implementare il
`onFileSystemOAuthCallback(\Joomla\Component\Media\Administrator\Event\OAuthCallbackEvent $event)`
nel tuo plugin.

`[site-name]/administrator/index.php?option=com_media&task=plugin.oauthcallback&plugin=[your-plugin-name]`

In questo esempio:  
`[site-name]/administrator/index.php?option=com_media&task=plugin.oauthcallback&plugin=myplugin`

Ora, quando effettui un reindirizzamento dal tuo provider una volta raggiunto l'URL fornito, il **Controller** per il Gestore Media garantirà che il tuo plugin implementi `onFileSystemOAuthCallback(\Joomla\Component\Media\Administrator\Event\OAuthCallbackEvent $event)` prima di passare qualsiasi dato ad esso. In caso contrario, sarai reindirizzato al Pannello di Controllo con un messaggio di errore.

Se hai implementato tutti gli input che vengono passati, il Provider Cloud sarà incluso nel `$event`. Puoi accedervi usando `$event->getInput()` e trattarlo come un normale `input` per Joomla.

Dopo aver ricevuto l'`input`, puoi utilizzarlo per ottenere i dettagli del tuo servizio cloud come **Access Token**, **Refresh Token**, ecc.

Se vuoi distinguere più account, puoi usare `Session` per quello.

**Nota**: Si consiglia di verificare il **token CSRF** prima di procedere con la richiesta. La maggior parte dei provider cloud supporta il parametro `state` che può essere utilizzato per completare l'operazione.

### Errori Comuni

È necessario `urlencode()` il tuo redirect uri quando lo invii al provider cloud. Ti preghiamo di utilizzarlo per evitare comportamenti anomali del tuo cloud.

## Servire File dal tuo Adapter

Per servire i tuoi file multimediali dal Media Manager al **Sito Joomla!**
`Joomla\Component\Media\Administrator\Adapter\AdapterInterface` ti aiuta. Questa interfaccia contiene un metodo speciale chiamato `getUrl($path)`.

`$path : Il percorso è relativo alla tua root`

L'intenzione del metodo è fornire un **URL Assoluto Pubblico** per il file che hai richiesto di inserire nel sito. Ad esempio, supponiamo che il percorso del tuo file sia `/path/to/me.png` nel server cloud. Ora un URL pubblico potrebbe essere qualcosa del tipo `mycloud.com/share/u/myusername/path/to/me.png`. Come venga servito, dipende completamente da te. Quando un utente vuole inserire un URL generato per i media, verrà utilizzato questo metodo.

Maggiori dettagli su `Adapter Interface` possono essere trovati in `administrator/componenents/com_media/Adapter/AdapterInterface.php`

*Tradotto da openai.com*

