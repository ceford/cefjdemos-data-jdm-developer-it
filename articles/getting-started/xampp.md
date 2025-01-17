<!-- Filename: XAMPP / Display title: XAMPP -->

## Introduzione

XAMPP è un pacchetto facile da installare che include il server web Apache, PHP, XDEBUG e il database MySQL. Questo ti permette di creare l'ambiente necessario per eseguire Joomla! sulla tua macchina locale. L'ultima versione di XAMPP è disponibile sul <a href="http://www.apachefriends.org/en/index.html" class="external text" target="_blank" rel="nofollow noreferrer noopener">sito web di XAMPP</a>. I download sono disponibili per Linux, Windows, Mac OS X e Solaris. Scarica il pacchetto per la tua piattaforma.

*Nota importante riguardante XAMPP e Skype:* Apache e Skype utilizzano entrambi la porta 80 come alternativa per le connessioni in entrata. Se utilizzi Skype, vai nel pannello Strumenti-Opzioni-Avanzate-Connessione e deseleziona l'opzione "Usa 80 e 443 come alternative per le connessioni in entrata". Se Apache viene avviato come servizio, prenderà la porta 80 prima che Skype si avvii e non vedrai alcun problema. Ma, per sicurezza, disabilita l'opzione in Skype.

### Installazione su Windows

L'installazione per Windows è molto semplice. Puoi usare l'eseguibile dell'installer XAMPP (ad esempio, "xampp-windows-x64-7.4.4-0-VC15-installer.exe"). Le istruzioni dettagliate per l'installazione su Windows sono disponibili <a href="https://www.apachefriends.org/download.html" class="external text" target="_blank" rel="nofollow noreferrer noopener">qui</a>.

Se sei su Windows XP o 2003, non sono supportati dal pacchetto principale, ma ci sono versioni compatibili di XAMPP per queste piattaforme elencate nella pagina di download (ma sarai in grado di eseguire solo PHP 5.4 o versioni inferiori - e quindi potrai testare solo Joomla 3.x e inferiori).

Per Windows, si consiglia di installare XAMPP in "c:\xampp" (non in "c:\program files"). Se lo fai, il tuo Joomla! (e qualsiasi altra cartella di siti web locali) andrà nella cartella "c:\xampp\htdocs". (Per convenzione, tutti i contenuti web vanno sotto la cartella "htdocs".)

Se hai più server http (come IIS) puoi cambiare la porta di ascolto di xampp. In \apache\conf\httpd.conf, modifica la riga Listen 80 in Listen \[portnumber\] (es: "Listen 8080").

Tutorial della Rivista della Comunità Joomla

Puoi trovare un tutorial dettagliato su come installare XAMPP su Windows, insieme a Joomla 4 Beta, il Joomla Patch Tester e Git in questo <a href="https://magazine.joomla.org/all-issues/june-2020/github-installing-git" class="external text" target="_blank" rel="noreferrer noopener">articolo della Joomla Community Magazine</a>.

### Installazione su Linux

#### Installare XAMPP

Apri Terminale e inserisci:

```bash
    sudo tar xvfz xampp-linux-1.7.7.tar.gz -C /opt
```

(sostituire *xampp-linux-1.7.7.tar.gz* con la versione di xammp che hai
scaricato). È stato segnalato che il database MYSQL di xampp 1.7.4
non funziona con Joomla 1.5.22.

Questo installa ... Apache2, mysql e php5, oltre a un server ftp.

```bash
    sudo /opt/lampp/lampp start
```

e

```bash
    sudo /opt/lampp/lampp stop
```

avvia/arresta tutti i servizi

#### Testa il tuo server localhost XAMPP

Apri il tuo browser e indirizzalo a

```bash
    http://localhost
```

L'index.php reindirizzerà a

```bash
    http://localhost/xampp
```

Lì troverai istruzioni su come cambiare i nomi utente/password predefiniti. Su un PC che non serve file a Internet o LAN, cambiare i valori predefiniti è una decisione personale.

#### Scarica Joomla

Scarica l'ultima versione del file zip di installazione di Joomla
<a href="https://www.joomla.org/download.html"
class="external autonumber" target="_blank"
rel="noreferrer noopener">[1]</a>

Decomprimi sul tuo disco rigido

Connettiti a localhost con un client FTP predefinito

```
    nobody
    lampp
```

Crea una cartella per il tuo Joomla sul server locale.

FTP i file di installazione Joomla decompattati nella cartella Joomla appena creata.

**Importante:**

- L'installazione di xammp imposta correttamente la proprietà dei file e i permessi.
- Usare il **comando CHOWN** **causerà problemi di proprietà con xampp**.
- **Usare nautilus** per manipolare cartelle/file su localhost **causerà problemi di proprietà con xampp**.

**Informazioni sul database**

- Host: localhost
- Nome del Database predefinito: test
- Utente del Database predefinito: root
- **Nessuna** Password predefinita.

La password dell'Amministratore è a tua scelta.

Si consiglia di installare i Dati di Esempio per l'utente principiante.

Dopo l'installazione, elimina la directory di installazione e punta il tuo browser su:

```
    http://localhost/yournewjoomlafolder
```

per

```
    http://localhost/yournewjoomlafolder/administrator
```

#### Creare un collegamento nel menu di Ubuntu

**Per creare un GUI per xammp collegato al menu di Ubuntu**

Apri il Terminale e digita

```bash
    sudo gedit /usr/share/applications/xampp-control-panel.desktop
```

Quindi copia quanto segue in gedit e salva.

```bash
[Desktop Entry]
Encoding=UTF-8
Name=XAMPP Control Panel
Comment=Start and Stop XAMPP
Exec=gksudo "python /opt/lampp/share/xampp-control-panel/xampp-control-panel.py"
Icon=/usr/share/icons/Tango/scalable/devices/network-wired.svg
Terminal=false
Type=Application
Categories=GNOME;Application;Network;
StartupNotify=true
```

Se il pannello di controllo non riesce ad avviarsi, prova a eseguire il comando Exec direttamente nel terminale:

```bash
    gksudo "python /opt/lampp/share/xampp-control-panel/xampp-control-panel.py"
```

Se ricevi l'errore:

```bash
    Error importing pygtk2 and pygtk2-libglade
```

Installa le librerie mancanti:

```bash
    sudo apt-get install python-glade2
```

#### Debugger PHP XDebug

Il pacchetto XAMPP per Linux non include il debugger PHP XDebug.  
Per installare XDebug su Debian o Ubuntu:

- Installa il pacchetto *build-essential*:
```bash
    sudo apt-get update
    sudo apt-get install build-essential
    sudo apt-get install autoconf
```

- Scarica il
<a href="http://www.apachefriends.org/en/xampp-linux.html"
class="external text" target="_blank"
rel="nofollow noreferrer noopener">pacchetto di sviluppo</a> per la tua versione di XAMPP ed estrailo sulla tua installazione esistente:
```bash
    sudo tar xvfz xampp-linux-devel-1.7.7.tar.gz -C /opt 
```

- Compila XDebug:
```bash
    wget http://xdebug.org/files/xdebug-2.1.3.tgz
    tar xzf xdebug-2.1.3.tgz
    cd xdebug-2.1.3/
    /opt/lampp/bin/phpize
```

Dopo di ciò, avrai il seguente output sulla tua console…

```bash
    Configuring for:
    PHP Api Version:         20090626
    Zend Module Api No:      20090626
    Zend Extension Api No:   20090626 

    ./configure --with-php-config=/opt/lampp/bin/php-config
    make
    sudo make install 
```

Poi l'output sarà questo.. per favore monitora la directory specificata.

```bash
    Installing shared extensions:     /opt/lampp/lib/php/extensions/no-debug-non-zts-20090626/ 
```

Crea una cartella nella tua cartella temporanea che conterrà il file di dati generato da XDebug:

```bash
    sudo mkdir /opt/lampp/tmp/xdebug
    sudo chmod a+rwx -R /opt/lampp/tmp/xdebug 
```

Installazioni alternative:

Installa utilizzando la libreria delle estensioni PHP della comunità (PECL) inclusa in xampp:

```bash
    sudo /opt/lampp/bin/pecl install xdebug
```

Su Ubuntu/Debian è possibile installare utilizzando:

```bash
    apt-get install php5-xdebug 
```

(avviso: questo installerà anche Apache e PHP dai repository apt).

**Avviso per gli utenti a 64 bit**

Quando compili XDebug o lo installi tramite apt-get, riceverai un errore quando (ri)avvii xampp:

```bash
    /opt/lampp/lib/php/extensions/no-debug-non-zts-20090626/xdebug.so: wrong ELF class: ELFCLASS64
```

Questo perché xampp gira su 32 bit ma XDebug è a 64 bit. Per superare questo problema, crea xdebug.so su una macchina a 32 bit o scaricalo da:

```bash
    http://code.activestate.com/komodo/remotedebugging/
```

Scarica il file: "PHP Remote Debugging Client" per "Linux (x86)"  
Estrai il contenuto del file sul tuo computer, questo file compresso
contiene diverse cartelle con numeri di versione es: 4.4, 5.0, 5.1 ... 5.3
e così via, entra nella cartella con il numero di versione più alto o quella
che funziona per te, poi copia manualmente il file "xdebug.so" nella
seguente posizione, sovrascrivi se necessario

```bash
    /opt/lampp/lib/php/extensions/no-debug-non-zts-20090626/
```

Ricorda che questa posizione potrebbe essere diversa sul tuo computer

### Installazione su Mac OS X

Mac OS X include effettivamente un server Apache già pronto all'uso, ma la maggior parte degli sviluppatori preferirà utilizzare gli strumenti integrati e la configurabilità forniti da XAMPP.

Come con la maggior parte dei programmi su Mac, l'installazione è un gioco da ragazzi. Visita
<a href="https://www.apachefriends.org/en/download.html"
class="external text" target="_blank"
rel="nofollow noreferrer noopener">Apache Friends - Mac OS X</a> per il download del binario universale.

Una volta terminato il download del file, apri semplicemente l'immagine del disco e trascina la cartella XAMPP nell'alias della cartella "Applicazioni".

Per avviare il server, apri "XAMPP Control.app" e premi il pulsante di avvio accanto ad Apache.

##### Una piccola risoluzione dei problemi

Molti utenti Mac hanno qualche difficoltà a questo punto quando cercano di configurare un'altra istanza di Apache sulla loro macchina. Se non riesci ad avviare l'Apache di XAMPP, hai due opzioni:  
**Puoi cambiare la porta di ascolto di XAMPP.** In \Applications\XAMPP\xamppfiles\etc\httpd.conf, modifica la linea che dice, "Listen 80" in Listen \[portNumber\]. Ad esempio:

```bash
    Listen 8080
```

**Puoi modificare la porta di ascolto del server Apache preinstallato.** In Finder, vai a "/etc" (CMD+SHIFT+G); da qui sarai in grado di navigare tra i file Apache normalmente nascosti. Trova la cartella etichettata Apache2 e modifica il file "http.conf". Modifica la riga che dice, "Listen 80" in Listen \[numeroPorta\]. Ad esempio:

```bash
    Listen 8080
```

*Nota: Se scegli di cambiare la porta del server Apache pre-installato, potrebbe essere necessario riavviare il computer affinché le modifiche abbiano effetto. Dovrai inoltre autenticarti come amministratore per modificare questi file.*

### Verifica dell'installazione di XAMPP

Una volta installato XAMPP e avviato il servizio Apache con lo strumento XAMPP Control Panel, puoi testarlo aprendo il browser e navigando su "<a href="http://localhost" class="external free" target="_blank" rel="nofollow noreferrer noopener">http://localhost</a>". Dovresti vedere la schermata di benvenuto di XAMPP simile a quella riportata di seguito.

<img
src="https://docs.joomla.org/images/thumb/f/fc/Phpinfo_on_xampp.png/800px-Phpinfo_on_xampp.png"
decoding="async"
srcset="https://docs.joomla.org/images/thumb/f/fc/Phpinfo_on_xampp.png/1200px-Phpinfo_on_xampp.png 1.5x, https://docs.joomla.org/images/f/fc/Phpinfo_on_xampp.png 2x"
data-file-width="1498" data-file-height="883" width="800" height="472"
alt="Phpinfo su xampp.png" />

Seleziona il link chiamato "phpinfo()" nel menu in alto. Questo visualizzerà una lunga schermata di informazioni sulla configurazione di PHP, come mostrato di seguito.

<img
src="https://docs.joomla.org/images/thumb/d/db/Phpinfo.png/800px-Phpinfo.png"
decoding="async"
srcset="https://docs.joomla.org/images/thumb/d/db/Phpinfo.png/1200px-Phpinfo.png 1.5x, https://docs.joomla.org/images/d/db/Phpinfo.png 2x"
data-file-width="1432" data-file-height="1282" width="800" height="716"
alt="Phpinfo.png" />

A questo punto, XAMPP è stato installato con successo. Nota il "Loaded Configuration File". Modificheremo questo file nella sezione successiva per configurare XDebug.

*Tradotto da openai.com*

