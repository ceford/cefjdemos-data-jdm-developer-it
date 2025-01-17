<!-- Filename: J4.x:Setting_Up_Your_Local_Environment / Display title: Configurare un ambiente locale -->

## Guida rapida all'avvio

Per una configurazione di test avrai bisogno di uno stack software che includa Apache, MySQL e PHP. I passaggi richiesti sono trattati altrove in questo manuale. In caso di dubbio, utilizza uno stack software appropriato per la tua piattaforma.

## Strumenti Aggiuntivi

Per testare le pull request di Joomla e contribuire al codice core di Joomla, avrai bisogno di strumenti aggiuntivi, tutti facilmente installabili, spesso con un solo comando:

1. **Composer** - per gestire le dipendenze PHP di Joomla. Leggi la [documentazione di Composer](https://getcomposer.org/doc/00-intro.md) per assistenza con l'installazione.
2. **Node.js** - per compilare i file JavaScript e SASS di Joomla. Leggi la [documentazione di Node.js](https://nodejs.org/en/) per assistenza con l'installazione.
3. **Git** - per la gestione delle versioni. Leggi la [documentazione di Git](https://git-scm.com/) per assistenza con l'installazione.

## Passaggi per configurare un sito di test locale

1. Vai al [repository di Joomla! su GitHub](https://github.com/joomla/joomla-cms).
2. Seleziona il branch di Joomla su cui lavorare. Questo seleziona le istruzioni appropriate del README.
3. Scorri verso il basso fino alla sezione **Passaggi per configurare l'ambiente locale:** del testo README.
4. Segui i passaggi elencati lì. Puoi cambiare il nome della cartella clonata di joomla-cms in modo da poter fare quanti più cloni vuoi per scopi diversi.
5. Crea un database e installa Joomla, ma non eliminare la cartella dell'installazione alla fine del processo di installazione.

## Aggiornamento di Joomla

Di tanto in tanto potresti aver bisogno di aggiornare un clone di Joomla. Questo è un comando di una sola riga che di solito è veloce. Tuttavia, è di solito necessario ricostruire i file CSS e JavaScript, un processo più complicato e lungo.

Gli utenti Linux e OSX possono configurare il seguente alias bash inserendo il seguente comando all'interno del *file ~/.bashrc*:

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
    alias jinstall="jclean; composer install; npm ci"
```

Questo eliminerà tutti i file compilati ed eseguirà una nuova installazione come comando unico chiamando `jinstall` all'interno della tua installazione di Joomla. Puoi anche usare il comando `jclean` per tornare a un diverso ramo di Joomla.

**Nota:** Potrebbe essere necessario eseguire `composer install` con l'opzione `--ignore-platform-reqs` per ignorare i requisiti di piattaforma specificati in Composer. Cioè, se non si ha installata l'estensione LDAP di PHP.

### Modifiche al database

Se un aggiornamento di Joomla include modifiche al database, potrebbe essere necessario trovare le modifiche individuali ed eseguirle manualmente oppure ricominciare con un nuovo clone.

## Scripti Node/npm

L'installazione di Joomla da un clone del repository ha utilizzato due comandi:

- **composer install** Installa tutti i pacchetti composer necessari.
- **npm ci** Installa tutti i pacchetti npm necessari.

Node.js viene fornito con un gestore di pacchetti chiamato NPM che ha un comando `run`. Alcuni script sono disponibili per rendere il processo di build più veloce se sono stati modificati solo i file CSS o JavaScript.

### npm run build:css

Questo comando compila i file SASS in CSS e crea anche i file minificati.

### npm run build:js

Questo comando compila e transpila i file JavaScript nel formato corretto e crea file minimizzati.

### npm run watch

Questo comando è lo stesso del comando `build:js`, ma controllerà le modifiche e costruirà automaticamente i file aggiornati nella directory media. I file SASS non sono ancora inclusi.

### npm esegui lint:js

Questo comando esegue un controllo della sintassi su tutti i file JavaScript ES6 rispetto allo standard del codice JavaScript. Per maggiori informazioni, consulta il [manuale degli standard di codifica Joomla](https://developer.joomla.org/coding-standards/introduction.html).

### npm run test

Questo comando eseguirà una suite di test JavaScript.

## Possibili Problemi

Quando esegui composer install puoi incontrare questi errori

```sh
    Problem 1
        - Installation request for joomla/ldap 2.0.0-beta -> satisfiable by joomla/ldap[2.0.0-beta].
        - joomla/ldap 2.0.0-beta requires ext-ldap * -> the requested PHP extension ldap is missing from your system.
    Problem 2
        - Installation request for symfony/ldap v5.1.5 -> satisfiable by symfony/ldap[v5.1.5].
        - symfony/ldap v5.1.5 requires ext-ldap * -> the requested PHP extension ldap is missing from your system.
```

La soluzione è eseguire il comando composer install con l'opzione `--ignore-platform-reqs` per ignorare i requisiti della piattaforma specificati in Composer. Cioè, se non hai installato l'estensione LDAP di PHP.

```sh
    composer install --ignore-platform-reqs
```

Se ricevi un errore di accesso, elimina il file `administrator/cache/autoload_psr4.php`.

*Tradotto da openai.com*

