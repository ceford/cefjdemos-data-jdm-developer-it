<!-- Filename: J4.x:Developer:_Required_Software / Display title: Software Richiesto -->

## Introduzione

Questo tutorial è rivolto ai nuovi arrivati nello sviluppo del codice Joomla che desiderano preparare estensioni su un computer locale. Non importa se usi Windows, Mac o Linux. Tutto il software richiesto è disponibile per tutte queste piattaforme. Per iniziare sul tuo laptop o computer desktop, che di solito ha il nome di dominio *localhost*, sarà necessario installare un set standard di componenti software separati.

- **Apache**, un server web. Altri server web sono disponibili, ma i nuovi arrivati dovrebbero attenersi ad Apache.
- **MySQL** o **MariaDB**, server di database. PostgreSQL è anche supportato ma non è per i nuovi arrivati.
- **PHP**, l'ultima versione raccomandata da Joomla o la versione minima per la tua piattaforma.
- **phpMyAdmin**, uno strumento utilizzato per gestire i database MySQL e MariaDB.
- **xDebug**, un'estensione di PHP utilizzata per il debugging.
- Un IDE come **VSCode**. Altri sono disponibili e trattati in un articolo separato.

## Stack Software

I primi quattro elementi di questo elenco sono spesso indicati come uno stack e possono essere chiamati LAMP, MAMP o WAMP, dove le lettere nell'acronimo significano quanto segue:

- **Piattaforma L, M o W**. L per Linux, M per Mac e W per Windows.
- **A: Apache** server web.
- **M: MySQL o MariaDB** database. I due sono intercambiabili.
- **P: PHP** linguaggio di scripting. Un linguaggio di scripting ampiamente utilizzato. Non ci sono alternative poiché Joomla è codificato in PHP.

## Stack Confezionati

Un buon modo per iniziare è utilizzare un pacchetto che combina il software essenziale:

- **WAMP** per Windows è gratuito dal sito [Wampserver](https://www.wampserver.com/en/).
- **Bearsampp** per Windows è gratuito dal sito [Bearsampp](https://bearsampp.com/). Ha più strumenti.
- **XAMPP** per Windows, Mac e Linux è gratuito dal sito [Apache Friends](https://www.apachefriends.org/). C'è un tutorial locale per [XAMPP](jdocmanual?article=user/hosting/local-hosting-with-xampp).
- **MAMP** per Mac e Windows è disponibile in versioni gratuite e commerciali dal sito [MAMP](https://www.mamp.info/en/mac/).

## Nessuna pila

Se hai un computer Linux o Macintosh, scoprirai che puoi installare ciascuno degli elementi software richiesti indipendentemente dai repository remoti che supportano il tuo sistema operativo. È possibile che siano già installati e pronti all'uso. Per verificare, apri il tuo browser web preferito e inserisci **localhost** nella barra degli URL. Vedrai una pagina segnaposto o una pagina di errore di connessione.

## Directory principale del documento del server web

All'installazione, il tuo server Apache avrà impostato una directory radice del documento predefinita. La posizione varia a seconda della piattaforma e devi sapere dove si trova o creare un host virtuale per posizionarlo dove desideri. Esempi di posizioni predefinite:

- Mac OS: "/Library/WebServer/Documents"
- Linux: /var/www/html
- Windows: ...

Per evitare problemi successivi con i permessi dei file, è spesso conveniente creare un host virtuale che punti alla directory public_html del proprio spazio file. Questo potrebbe essere /home/username/public_html su Linux o /Users/username/Sites su Mac.

Questo è un esempio di voce di host virtuale Mac nel file /etc/apache2/vhosts/localhost.conf:

```bash
<VirtualHost *:80>
        DocumentRoot "/Users/username/Sites"
        ServerName localhost
        ErrorLog "/private/var/log/apache2/localhost-error_log"
        CustomLog "/private/var/log/apache2/localhost-access_log" common
        <Directory "/Users/username/Sites">
            AllowOverride All
            Require all granted
        </Directory>
</VirtualHost>
```

In alternativa, potresti essere in grado di creare un collegamento simbolico dalla directory principale predefinita al folder public_html del tuo spazio file personale.

*Tradotto da openai.com*

