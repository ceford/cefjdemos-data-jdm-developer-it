<!-- Filename: J4.x:Using_Bootstrap_Components_in_Joomla_4 / Display title: Utilizzare i componenti di Bootstrap in Joomla 4 -->

## Introduzione

### Componenti di Bootstrap

Alcuni dei componenti descritti nella documentazione di Bootstrap utilizzano solo CSS. Ad esempio, il componente Breadcrumbs è reso con CSS e non richiede supporto JavaScript. Altri rispondono alle azioni dell'utente come clic o hover e necessitano di supporto JavaScript. Questi ultimi sono qui denominati Componenti Interattivi. Questo articolo spiega come utilizzarli negli Articoli e in un Modulo Personalizzato.

Vedi la [Documentazione di Bootstrap](https://getbootstrap.com/docs/5.0/getting-started/introduction/)

### Joomla 4 introduce un approccio modulare per componenti interattivi

- Che cos'è un approccio modulare?
- La funzionalità è suddivisa in singoli componenti supportati da singoli file. Non esiste un approccio **a file unico** come era con Bootstrap in Joomla 3. L'approccio modulare è più efficiente e offre vantaggi in termini di prestazioni (invia solamente il codice che è necessario invece di consegnare tutto nel caso in cui una pagina avrà bisogno di qualche componente).

### Utilizzo di Componenti Interattivi: Programmatori

- Carica ciò che ti serve per caso! Ci sono funzioni di supporto per configurare singoli componenti con argomenti appropriati.
- Vedi l'elenco dei Componenti Interattivi di Bootstrap.

### Utilizzo di Componenti Interattivi: Non Sviluppatori

- Usare i componenti negli articoli non è così facile perché le funzioni helper non possono essere chiamate da un articolo o da un modulo HTML Personalizzato standard. Più avanti in questo tutorial vengono suggerite tre possibili soluzioni:
  - Un modulo personalizzato
  - Un plugin personalizzato
  - Un override di modulo personalizzato
- Salta o esamina l'elenco dei Componenti Interattivi di Bootstrap. Non utilizzerai queste chiamate di funzione direttamente.

## Componenti Interattivi di Bootstrap

### Avviso

Presumendo di avere già la parte HTML nel tuo Layout, avrai anche bisogno di includere l'interattività (la parte JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.alert', '.selector');
```

- Il **.selector** si riferisce al selettore CSS per l'allerta. È possibile chiamare questa funzione più volte con diversi selettori CSS.
- Nessuna opzione extra disponibile.

### Pulsante

Assumendo che tu abbia già la parte HTML nel tuo Layout, dovrai anche includere l'interattività (la parte JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.button', '.selector');
```

- Il **.selector** si riferisce al selettore CSS per il pulsante. Puoi chiamare questa funzione più volte con selettori CSS diversi
- Nessuna opzione aggiuntiva disponibile

### Carosello

Supponendo che tu abbia già la parte HTML nel tuo Layout, dovrai includere anche l'interattività (la parte JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.carousel', '.selector', []);
```

- Il **.selector** si riferisce al selettore CSS per il carosello. Puoi chiamare questa funzione più volte con selettori CSS diversi
- Il terzo argomento si riferisce alle opzioni disponibili per il carosello

Opzioni per il carosello possono essere:

- **interval**, numero, predefinito:**5000**, La quantità di tempo da ritardare tra il cambio automatico di un elemento. Se impostato su false, il carosello non ciclerà automaticamente.
- **keyboard**, boolean, predefinito:**true** Indica se il carosello dovrebbe reagire agli eventi della tastiera.
- **pause**, stringa\|boolean, **hover** Ferma il ciclo del carosello al passaggio del mouse e riprende il ciclo quando il mouse esce.
- **slide**, stringa\|boolean, predefinito:**false** Avvia automaticamente il carosello dopo che l'utente ha cicliato manualmente il primo elemento. Se impostato su "carousel", avvia automaticamente il carosello al caricamento.

### Collasso

Presumendo che tu abbia già la parte HTML nel tuo Layout, dovrai includere anche l'interattività (la parte JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.collapse', '.selector', []);
```

- Il **.selector** si riferisce al selettore CSS per il collapse. Puoi chiamare questa funzione più volte con selettori CSS diversi.
- Il terzo argomento si riferisce alle opzioni disponibili per il collapse.

Opzioni per il collasso possono essere:

- **parent**, stringa, predefinito:**false** Se viene fornito un parent, tutti gli elementi comprimibili sotto il parent specificato saranno chiusi quando questo elemento comprimibile è mostrato.
- **toggle**, booleano predefinito:**true** Attiva/disattiva l'elemento comprimibile al richiamo.

### Menu a discesa

Supponendo che tu abbia già la parte HTML nel tuo Layout, dovrai anche includere l'interattività (la parte JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.dropdown', '.selector', []);
```

- Il **.selector** si riferisce al selettore CSS per il menu a tendina. Puoi chiamare questa funzione più volte con diversi selettori CSS.
- Il terzo argomento si riferisce alle opzioni disponibili per il menu a tendina.

Opzioni per il collasso possono essere:

- **flip**, booleano, predefinito:**true** Permette al Dropdown di capovolgersi in caso di sovrapposizione sull'elemento di riferimento.
- **boundary**, stringa, predefinito:**scrollParent** Limite di overflow del menu a discesa.
- **reference**, stringa, predefinito:**toggle** Elemento di riferimento del menu a discesa. Accetta **toggle** o **parent**.
- **display**, stringa, predefinito:**dynamic** Per impostazione predefinita, utilizziamo Popper per il posizionamento dinamico. Disabilitalo con **static**.

### Modale

Assumendo che tu abbia già la parte HTML nel tuo layout, dovrai anche includere l'interattività (la parte JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.modal', '.selector', []);
```

- Il **.selector** si riferisce al selettore CSS per il modal. Puoi chiamare questa funzione più volte con selettori CSS diversi.
- Il terzo argomento si riferisce alle opzioni disponibili per il modal.

Opzioni per il modale possono essere:

- **backdrop**, string\|boolean predefinito:**true** Include un elemento di sfondo modale. In alternativa, specifica static per uno sfondo che non chiude il modale al clic.
- **keyboard**, boolean predefinito:**true** Chiude il modale quando viene premuto il tasto escape.
- **focus**, boolean predefinito:**true** Chiude il modale quando viene premuto il tasto escape.

### Fuori canvas

Supponendo che tu abbia già la parte HTML nel tuo Layout, dovrai anche includere l'interattività (la parte JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.offcanvas', '.selector', []);
```

- Il **.selector** si riferisce al selettore CSS per l'offcanvas. Puoi chiamare questa funzione più volte con selettori CSS diversi.
- Il terzo argomento si riferisce alle opzioni disponibili per l'offcanvas.

Opzioni per l'offcanvas possono essere:

- **backdrop**, booleano, predefinito:**true** Applica uno sfondo sul corpo mentre l'offcanvas è aperto.
- **keyboard**, booleano, predefinito:**true** Chiude l'offcanvas quando viene premuto il tasto escape.
- **scroll**, booleano, predefinito:**false** Consenti lo scorrimento del corpo mentre l'offcanvas è aperto.

### Popover

Presumendo che tu abbia già la parte HTML nel tuo Layout, avrai anche bisogno di includere l'interattività (la parte JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.popover', '.selector', []);
```

- Il **.selector** si riferisce al selettore CSS per il popover. Puoi chiamare questa funzione più volte con diversi selettori CSS.
- Il terzo argomento si riferisce alle opzioni disponibili per il popover.

Opzioni per il popover possono essere:

- **animation**, booleano, valore predefinito:**true** Applica una transizione di dissolvenza CSS al popover.
- **container**, stringa\|booleano, valore predefinito:**false** Aggiunge il popover a un elemento specifico. Es.: **body**.
- **content**, stringa, valore predefinito:**null** Valore del contenuto predefinito se l'attributo data-bs-content non è presente.
- **delay**, numero, valore predefinito:**0** Ritardo nella visualizzazione e nell'occultamento del popover (ms) non si applica al tipo di trigger manuale.
- **html**, booleano, valore predefinito:**true** Inserisce HTML nel popover. Se **false**, verrà utilizzata la proprietà innerText per inserire il contenuto nel DOM.
- **placement**, stringa, valore predefinito:**right** Come posizionare il popover - **auto** \| **top** \| **bottom** \| **left** \| **right**. Quando è specificato auto, il popover verrà riorientato dinamicamente.
- **selector**, stringa, valore predefinito:**false** Se viene fornito un selettore, gli oggetti popover verranno delegati ai target specificati.
- **template**, stringa, valore predefinito:**null** HTML di base da usare quando si crea il popover.
- **title**, stringa, valore predefinito:**null** Valore del titolo predefinito se il tag **title** non è presente.
- **trigger**, stringa, valore predefinito:**click** Come viene attivato il popover - **click** \| **hover** \| **focus** \| **manual**.
- **offset**, intero, valore predefinito:**0** Spostamento del popover rispetto al suo target.

### Scrollspy

Presumendo che tu abbia già la parte HTML nel tuo layout, dovrai includere anche l'interattività (la parte JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.scrollspy', '.selector', []);
```

- Il **.selector** si riferisce al selettore CSS per lo scrollspy. È possibile chiamare questa funzione più volte con diversi selettori CSS.
- Il terzo argomento si riferisce alle opzioni disponibili per lo scrollspy.

Opzioni per Scrollspy possono essere:

- **offset** numero Pixel da sottrarre dall'alto quando si calcola la posizione di scorrimento.
- **method** stringa Trova in quale sezione si trova l'elemento spiato.
- **target** stringa Specifica l'elemento a cui applicare il plugin Scrollspy.

### Tabella

Supponendo che tu abbia già la parte HTML nel tuo Layout, dovrai includere anche l'interattività (la parte JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.tab', '.selector', []);
```

- Il **.selector** si riferisce al selettore CSS per la scheda. Puoi chiamare questa funzione più volte con selettori CSS diversi.
- Il terzo argomento si riferisce alle opzioni disponibili per la scheda.

Opzioni per la scheda possono essere:

### Descrizione alternativa

Supponendo che tu abbia già la parte HTML nel tuo Layout, avrai anche bisogno di includere l'interattività (la parte JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.tooltip', '.selector', []);
```

- Il **.selector** si riferisce al selettore CSS per il tooltip. Puoi richiamare questa funzione più volte con selettori CSS diversi.
- Il terzo argomento si riferisce alle opzioni disponibili per il tooltip.

Opzioni per il tooltip possono essere:

- **animation**, boolean applica una transizione fade CSS al popover.
- **container**, string\|boolean Appende il popover a un elemento specifico: { container: **body** }.
- **delay**, number\|object ritarda la visualizzazione e l'occultamento del popover (ms) - non si applica al tipo di attivazione manuale. Se viene fornito un numero, il ritardo si applica sia alla visualizzazione che all'occultamento. La struttura dell'oggetto è: delay: { show: 500, hide: 100 }.
- **html**, boolean Inserisci HTML nel popover. Se falso, sarà utilizzato il metodo text di jQuery per inserire il contenuto nel dom.
- **placement**, string\|function come posizionare il popover - **top** \| **bottom** \| **left** \| **right**.
- **selector** string Se viene fornito un selettore, gli oggetti popover saranno delegati ai target specificati.
- **template**, string HTML di base da usare quando si crea il popover.
- **title**, string\|function valore predefinito del titolo se il tag **title** non è presente.
- **trigger**, string come viene attivato il popover - hover \| focus \| manual.
- **constraints**, array Un array di vincoli - passato a Popper.
- **offset**, string Offset del popover rispetto al suo target.

### Toast

Presumendo che tu abbia già la parte HTML nel tuo Layout, avrai anche bisogno di includere l'interattività (la parte JavaScript):

```php
    \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.toast', '.selector', []);
```

- Il **.selector** si riferisce al selettore CSS per il toast. Puoi chiamare questa funzione più volte con selettori CSS diversi.
- Il terzo argomento si riferisce alle opzioni disponibili per il toast.

Opzioni per il toast possono essere:

- **animazione**, booleano, default:**true** Applica una transizione fade CSS al toast.
- **nascondi automaticamente**, booleano, default:**true** Nasconde automaticamente il toast.
- **ritardo**, numero, default:**5000** Ritarda la scomparsa del toast (ms).

### Vedi Anche

- **Fisarmonica** utilizza Collapse per visualizzare pannelli di dati.
- **Gruppo di Elenchi** può essere combinato con Tab per visualizzare contenuti a schede.

## Uso dei componenti di Bootstrap negli articoli

Il markup HTML per la maggior parte dei componenti può essere incluso in un articolo o in un modulo che a sua volta può essere incluso in un articolo. Il problema è che la chiamata di HTMLHelper per configurare il supporto JavaScript non può essere inclusa lì. Ci sono diversi approcci possibili a questo problema. Qui vengono suggeriti tre approcci, utilizzando un modulo personalizzato, utilizzando un plugin o utilizzando un override di template.

**Attenzione:** Gli editor TinyMCE e JCE rimuovono gli spazi bianchi durante il salvataggio, rendendo difficile l'editing del codice! La soluzione semplice è andare in alto a destra dello schermo dell'Amministratore e selezionare **Menu Utente → Modifica Account** e impostare l'editor su Code Mirror.

## Approccio 1: Utilizzo di un Modulo Personalizzato

Questo è probabilmente l'approccio meno soggetto a errori perché le opzioni di supporto del componente Bootstrap sono selezionate con caselle di controllo. I passaggi coinvolti sono i seguenti:

- Scarica, installa e abilita questo [Modulo Personalizzato](https://github.com/ceford/j4xdemos-mod-custom-bscompos/raw/master/mod_custom_bscompos.zip)
- Dal menu dell'Amministratore vai a **Contenuti **→** Moduli Sito → Nuovo**
- Seleziona **Componenti BS Personalizzati**
- Inserisci un Titolo
- Cambia l'Editor in modalità testo semplice e incolla o digita il codice HTML per il componente che vuoi usare.
- Nella scheda Opzioni scorri fino all'elenco dei Componenti BS e seleziona il tipo di componente in questa istanza del modulo. Nota che puoi selezionare più di uno se stai usando più di un componente.
- Seleziona una Posizione del modulo: o
  - una posizione definita dal template se vuoi usare il modulo in una posizione specifica oppure
  - digita una posizione se desideri utilizzare il modulo all'interno di un articolo specifico: nell'articolo digita {loadposition qualsiasi}
- Salva e vai sul sito per Testare!

### Selettori

Per alcuni componenti l'azione JavaScript viene attivata da una **classe** specifica nel codice HTML. In altri componenti l'azione viene attivata da un attributo **data-bs-whatever**. I seguenti sono i trigger attuali e potrebbero cambiare:

- **Avviso** attivato da class="alert ..."
- **Pulsante** attivato da data-bs-toggle="button"
- **Carosello** attivato da data-bs-ride="whatever"
- **Collasso** attivato da data-bs-toggle="collapse"
- **Menu a discesa** attivato da data-bs-toggle="dropdown"
- **Finestra modale** attivata da data-bs-toggle="modal"
- **Fuori canvas** attivato da data-bs-toggle="offcanvas"
- **Popover** attivato da class="btn ..." o
  - tag (potrebbe essere cambiato in class="haspopover ...") E
  - data-bs-toggle="popover"
- **Spia di scorrimento** attivata da data-bs-spy="scroll"
- **Scheda** attivata da data-bs-toggle="tab"
- **Toast** attivato da class="toast ..."
- **Tooltip** attivato da class="btn ..." o
  - tag (potrebbe essere cambiato in class="hastooltip ...") E
  - data-bs-toggle="tooltip"

### Esempio 1: Avviso

Gli avvisi possono essere utilizzati nel codice HTML senza supporto JavaScript. Questo è necessario solo per la capacità di chiusura. Esempio di codice HTML:

```html
<div class="alert alert-warning alert-dismissible fade show" role="alert">
  <strong>Holy guacamole!</strong> You should check in on some of those fields below.
  <button type="button" class="btn-close" data-bs-dismiss="alert" aria-label="Close"></button>
</div>
```

Risultato esempio dell'inclusione di un modulo in un articolo:

![Bootstrap alert](../../../en/images/coding-examples/coding-examples-alert.png)

Nota che senza il supporto JavaScript, l'avviso apparirà esattamente come sopra, ma un clic sul pulsante di chiusura \[X\] non chiuderà l'avviso. Inoltre, l'avviso apparirà ad ogni caricamento della pagina.

### Esempio 2: Pulsanti

I pulsanti possono essere utilizzati nel codice HTML senza supporto JavaScript. Questo è necessario solo per il cambiamento di stile a volte sottile applicato ai pulsanti con un cambiamento di stato, stilizzato come attivo. Esempio di codice Bootstrap:

```html
<p><button type="button" class="btn btn-primary" data-bs-toggle="button" autocomplete="off">Toggle button</button>
<button type="button" class="btn btn-primary active" data-bs-toggle="button" autocomplete="off" aria-pressed="true">Active toggle button</button>
<button type="button" class="btn btn-primary" disabled data-bs-toggle="button" autocomplete="off">Disabled toggle button</button></p>
```

```html
<p><a href="#" class="btn btn-primary" role="button" data-bs-toggle="button">Toggle link</a>
<a href="#" class="btn btn-primary active" role="button" data-bs-toggle="button" aria-pressed="true">Active toggle link</a>
<a href="#" class="btn btn-primary disabled" tabindex="-1" aria-disabled="true" role="button" data-bs-toggle="button">Disabled toggle link</a></p>
```

Con questo stile nel modello user.css:

```css
    .btn.btn-primary.active {
        background-color: green;
    }
```

![Bootstrap buttons](../../../en/images/coding-examples/coding-examples-buttons.png)

I pulsanti alternano tra blu e verde.

### Esempio 3: Carosello

Il carosello offre uno slideshow che cicla attraverso una serie di immagini o pannelli di testo. Il seguente esempio utilizza immagini dal campione di Joomla 4. Codice Bootstrap:

```html
<div id="carouselExampleCaptions" class="carousel slide" data-bs-ride="carousel">
    <div class="carousel-indicators">
        <button class="active" type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="0" aria-current="true" aria-label="Slide 1"></button>
        <button type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="1" aria-label="Slide 2"></button>
        <button type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="2" aria-label="Slide 3"></button>
    </div>
    <div class="carousel-inner">
        <div class="carousel-item active"><img class="d-block w-100" src="images/sampledata/cassiopeia/nasa1-1200.jpg" alt="..." />
            <div class="carousel-caption d-none d-md-block">
                <h5>First slide label</h5>
                <p>Some representative placeholder content for the first slide.</p>
            </div>
        </div>
        <div class="carousel-item"><img class="d-block w-100" src="images/sampledata/cassiopeia/nasa2-1200.jpg" alt="..." />
            <div class="carousel-caption d-none d-md-block">
                <h5>Second slide label</h5>
                <p>Some representative placeholder content for the second slide.</p>
            </div>
        </div>
        <div class="carousel-item"><img class="d-block w-100" src="images/sampledata/cassiopeia/nasa3-1200.jpg" alt="..." />
            <div class="carousel-caption d-none d-md-block">
                <h5>Third slide label</h5>
                <p>Some representative placeholder content for the third slide.</p>
            </div>
        </div>
    </div>
    <button class="carousel-control-prev" type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide="prev">
        <span class="visually-hidden">Previous</span>
    </button>
    <button class="carousel-control-next" type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide="next">
        <span class="visually-hidden">Next</span>
    </button>
</div>
```

Risultato:

![Bootstrap carousel](../../../en/images/coding-examples/coding-examples-carousel.jpg)

### Esempio 4: Riduci

Il collasso è ampiamente utilizzato in Joomla e potresti non aver bisogno di usare un modulo o un plugin per attivare l'azione. Il clic apre un riquadro con informazioni aggiuntive. Codice di esempio di Bootstrap:

```html
<p>
    <a class="btn btn-primary" role="button" href="#collapseExample" data-bs-toggle="collapse" aria-expanded="false" aria-controls="collapseExample"> Link with href </a>
    <button class="btn btn-primary" type="button" data-bs-toggle="collapse" data-bs-target="#collapseExample" aria-expanded="false" aria-controls="collapseExample">
        Button with data-bs-target
    </button>
</p>
<div id="collapseExample" class="collapse">
    <div class="card card-body">
        Some placeholder content for the collapse component. This panel is hidden by default but revealed when the user activates the relevant trigger.
    </div>
</div>
```

Risultato:

![Bootstrap collapse](../../../en/images/coding-examples/coding-examples-collapse.png)

### Esempio 5: Menu a tendina

```
I menu a discesa sono sovrapposizioni contestuali attivabili per visualizzare elenchi di collegamenti e altro. Codice di esempio Bootstrap:
```

```html
<div class="btn-group">
    <button class="btn btn-danger dropdown-toggle" type="button" data-bs-toggle="dropdown" aria-expanded="false"> Action </button>
    <ul class="dropdown-menu">
        <li><a class="dropdown-item" href="#">Action</a></li>
        <li><a class="dropdown-item" href="#">Another action</a></li>
        <li><a class="dropdown-item" href="#">Something else here</a></li>
        <li><hr class="dropdown-divider" /></li>
        <li><a class="dropdown-item" href="#">Separated link</a></li>
    </ul>
</div>
```

Risultato:

![Bootstrap dropdown](../../../en/images/coding-examples/coding-examples-dropdown.png)

### Esempio 6: Modale

Il componente Modal apre una finestra di dialogo al centro dello schermo. Ci sono diverse opzioni per controllare la dimensione e il contenuto del modal. Consulta la documentazione di Bootstrap per ulteriori dettagli. Codice d'esempio di Bootstrap:

```html
<p><button class="btn btn-primary" type="button" data-bs-toggle="modal" data-bs-target="#exampleModal"> Launch demo modal </button></p>
<div id="exampleModal" class="modal fade" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
        <div class="modal-content">
            <div class="modal-header">
                <h5 id="exampleModalLabel" class="modal-title">Modal title</h5>
                <button class="btn-close" type="button" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
                ...
            </div>
            <div class="modal-footer">
                <button class="btn btn-secondary" type="button" data-bs-dismiss="modal">Close</button>
                <button class="btn btn-primary" type="button">Save changes</button>
            </div>
        </div>
    </div>
</div>
```

Risultato:

![Bootstrap modal](../../../en/images/coding-examples/coding-examples-modal.png)

### Esempio 7: Fuori Canvas

Al momento questo componente non è supportato in Joomla. Resta sintonizzato - presto in arrivo!

### Esempio 8: Popover

I popover sono simili ai Tooltip ma con un Titolo. Presentano alcuni problemi di accessibilità e prestazioni, quindi dovrebbero essere usati con cautela. Codice di esempio Bootstrap:

```html
<p><button class="btn btn-lg btn-danger" title="Popover title" type="button" data-bs-toggle="popover" data-bs-content="And here's some amazing content. It's very engaging. Right?">Click to toggle popover</button></p>
```

Risultato:

![Bootstrap alert](../../../en/images/coding-examples/coding-examples-popover.png)

### Esempio 9: Scrollspy

Esempio di codice:

```html
<div class="row">
    <div class="col-4">
        <nav id="navbar-example3" class="navbar navbar-light bg-light flex-column">
            <a class="navbar-brand" href="#">Navbar</a><nav class="nav nav-pills flex-column">
            <a class="nav-link active" href="#item-1">Item 1</a>
            <nav class="nav nav-pills flex-column">
                <a class="nav-link ms-3 my-1" href="#item-1-1">Item 1-1</a>
                <a class="nav-link ms-3 my-1" href="#item-1-2">Item 1-2</a>
            </nav>
            <a class="nav-link" href="#item-2">Item 2</a>
            <a class="nav-link" href="#item-3">Item 3</a>
            <nav class="nav nav-pills flex-column">
                <a class="nav-link ms-3 my-1" href="#item-3-1">Item 3-1</a>
                <a class="nav-link ms-3 my-1" href="#item-3-2">Item 3-2</a>
            </nav>
        </nav>
    </div>
    <div class="col-8">
        <div class="scrollspy-example" tabindex="0" data-bs-spy="scroll" data-bs-target="#navbar-example3" data-bs-offset="0">
            <h4 id="item-1">Item 1</h4>
            <p>Placeholder content for the scrollspy example. This one relates to item 1. Takes you miles high, so high, 'cause she’s got that one international smile. There's a stranger in my bed, there's a pounding in my head. Oh, no. In another life I would make you stay. ‘Cause I, I’m capable of anything. Suiting up for my crowning battle. Used to steal your parents' liquor and climb to the roof. Tone, tan fit and ready, turn it up cause its gettin' heavy. Her love is like a drug. I guess that I forgot I had a choice.</p>
            <h5 id="item-1-1">Item 1-1</h5>
            <p>Placeholder content for the scrollspy example. This one relates to the item 1-1. You got the finest architecture. Passport stamps, she's cosmopolitan. Fine, fresh, fierce, we got it on lock. Never planned that one day I'd be losing you. She eats your heart out. Your kiss is cosmic, every move is magic. I mean the ones, I mean like she's the one. Greetings loved ones let's take a journey. Just own the night like the 4th of July! But you'd rather get wasted.</p>
            <h5 id="item-1-2">Item 1-2</h5>
            <p>Placeholder content for the scrollspy example. This one relates to the item 1-2. Her love is like a drug. All my girls vintage Chanel baby. Got a motel and built a fort out of sheets. 'Cause she's the muse and the artist. (This is how we do) So you wanna play with magic. So just be sure before you give it all to me. I'm walking, I'm walking on air (tonight). Skip the talk, heard it all, time to walk the walk. Catch her if you can. Stinging like a bee I earned my stripes.</p>
            <h4 id="item-2">Item 2</h4>
            <p>Placeholder content for the scrollspy example. This one relates to item 2. Don't need apologies. There is no fear now, let go and just be free, I will love you unconditionally. Last Friday night. Don't be a shy kinda guy I'll bet it's beautiful. Summer after high school when we first met. 'Cause she's the muse and the artist. What? Wait. No, no, no, no. Thought that I was the exception.</p>
            <h4 id="item-3">Item 3</h4>
            <p>Placeholder content for the scrollspy example. This one relates to item 3. Word on the street, you got somethin' to show me, me. All this money can't buy me a time machine. Make it like your birthday everyday. So we hit the boulevard. You make me feel like I'm livin' a teenage dream, the way you turn me on Skip the talk, heard it all, time to walk the walk. Word on the street, you got somethin' to show me, me. It's no big deal, it's no big deal, it's no big deal.</p>
            <h5 id="item-3-1">Item 3-1</h5>
            <p>Placeholder content for the scrollspy example. This one relates to item 3-1. Baby do you dare to do this? This is no big deal. Yeah, you're lucky if you're on her plane. Just own the night like the 4th of July! Standing on the frontline when the bombs start to fall. So just be sure before you give it all to me.</p>
            <h5 id="item-3-2">Item 3-2</h5>
            <p>Placeholder content for the scrollspy example. This one relates to item 3-2. You're original, cannot be replaced. All night they're playing, your song. California girls we're undeniable. Like a bird without a cage. There is no fear now, let go and just be free, I will love you unconditionally. I can see the writing on the wall. You could travel the world but nothing comes close to the golden coast.</p>
        </div>
    </div>
</div>
```

Risultato:

![Bootstrap scrollspy](../../../en/images/coding-examples/coding-examples-scrollspy.png)

Inoltre, è necessario un po' di stile in user.css:

```css
    .scrollspy-example {
        height: 350px;
        overflow-y: scroll;
    }
```

Punto critico: il menu non si coordina bene con il contenuto in questo esempio!

### Esempio 10: Tabella

Le schede vengono spesso utilizzate come elementi di navigazione combinati con i menu a tendina. Esempio di codice Bootstrap:

```html
<ul class="nav nav-tabs">
    <li class="nav-item"><a class="nav-link active" href="#" aria-current="page">Active</a></li>
    <li class="nav-item dropdown"><a class="nav-link dropdown-toggle" role="button" href="#" data-bs-toggle="dropdown" aria-expanded="false">Dropdown</a>
        <ul class="dropdown-menu">
            <li><a class="dropdown-item" href="#">Action</a></li>
            <li><a class="dropdown-item" href="#">Another action</a></li>
            <li><a class="dropdown-item" href="#">Something else here</a></li>
            <li><hr class="dropdown-divider" /></li>
            <li><a class="dropdown-item" href="#">Separated link</a></li>
        </ul>
    </li>
    <li class="nav-item"><a class="nav-link" href="#">Link</a></li>
    <li class="nav-item"><a class="nav-link disabled" tabindex="-1" href="#" aria-disabled="true">Disabled</a></li>
</ul>
```

Risultato:

![Bootstrap tab](../../../en/images/coding-examples/coding-examples-tab.png)

Ricorda di controllare sia l'opzione Tab che quella a discesa affinché la parte a discesa funzioni.

### Esempio 11: Toast

I toast sono notifiche leggere progettate per imitare le notifiche push che sono state popolarizzate dai sistemi operativi mobili e desktop. Sono costruiti con flexbox, quindi sono facili da allineare e posizionare. Esempio di codice Bootstrap:

```html
<div class="toast fade show" role="alert" aria-live="assertive" aria-atomic="true">
    <div class="toast-header">
        <img class="rounded me-2" src="..." alt="..." />
        <strong class="me-auto">Bootstrap</strong> <small>11 mins ago</small>
        <button class="btn-close" type="button" data-bs-dismiss="toast" aria-label="Close"></button>
    </div>
    <div class="toast-body">Hello, world! This is a toast message.</div>
</div>
```

Risultato:

![Bootstrap toast](../../../en/images/coding-examples/coding-examples-toast.png)

Si noti che la demo di Bootstrap che utilizza un pulsante per mostrare il messaggio Toast necessita di ulteriore JavaScript. Sembra che questo componente richieda un programmatore per essere utilizzato al meglio!

### Esempio 12: Tooltip

Un tooltip è un piccolo testo che appare quando si passa il mouse su un pulsante o un elemento di collegamento per spiegare cosa sia o cosa faccia. Il tooltip può essere posizionato sopra o sotto, a sinistra o a destra dell'elemento. Se non specificato, la posizione predefinita è in alto. Il tooltip cambierà posizione se non c'è spazio sufficiente nella posizione specificata. Codice di esempio di Bootstrap:

```html
<p><button class="btn btn-secondary" title="Tooltip on left" type="button" data-bs-toggle="tooltip" data-bs-placement="left"> Tooltip on left </button>
<button class="btn btn-secondary" title="Tooltip" type="button" data-bs-toggle="tooltip"> Tooltip </button>
<button class="btn btn-secondary" title="Tooltip on top" type="button" data-bs-toggle="tooltip" data-bs-placement="top"> Tooltip on top </button>
<button class="btn btn-secondary" title="Tooltip on right" type="button" data-bs-toggle="tooltip" data-bs-placement="right"> Tooltip on right </button>
<button class="btn btn-secondary" title="Tooltip on bottom" type="button" data-bs-toggle="tooltip" data-bs-placement="bottom"> Tooltip on bottom </button>
<button class="btn btn-secondary" title="<em>Tooltip</em> <u>with</u> <b>HTML</b>" type="button" data-bs-toggle="tooltip" data-bs-html="true"> Tooltip with HTML </button></p>
<p>Tooltip triggered by class: <button class="btn btn-warning" title="Tooltip Message">Alert!</button></p>
```

Risultato:

![Bootstrap tooltip](../../../en/images/coding-examples/coding-examples-tooltip.png)

## Approccio 2: Utilizzo di un plugin di contenuto

I passaggi coinvolti:

- Scaricare, installare e abilitare questo [plugin](https://github.com/ceford/j4xdemos-plg-bscompos/raw/master/plg_j4xdemos_bscompos.zip)
- Nell'articolo aggiungere il testo su cui il plugin agisce, ad esempio {bscompos modal carousel} attiverà il caricamento del JavaScript necessario per supportare un dialogo modale e un carosello. Il plugin rimuove il testo di attivazione e racchiude (ora) i tag vuoti.
- Includere il codice HTML del Componente Bootstrap direttamente nell'articolo o in un modulo incluso nell'articolo. C'è un esempio di codice HTML qui sotto per un semplice Modale e un Modale contenente un Carosello. Si noti che questo non funzionerà se il codice HTML si trova in un modulo in una posizione del template.
- Questo funzionerà anche per un modulo Personalizzato standard se l'opzione Prepara Contenuto è impostata su Sì.
- Provalo!

## Approccio 3: Utilizzare un Override del Modello

I passaggi coinvolti:

- Crea un override del template di mod_custom.
- Aggiungi un modulo mod_custom contenente il markup del componente e le classi trigger.
- Includi il modulo in un articolo.

### L'override del modello mod_custom

- Nell'interfaccia Amministratore, vai su **Sistema → Template del sito → Dettagli e file di Cassiopeia**.
- Seleziona **Crea Override **→** mod_custom **→** default.php**.
- Nella riga successiva a defined('\_JEXEC') or die; aggiungi il seguente codice:

```php
    $module_class = $params->get('moduleclass_sfx');
    if (!empty($module_class))
    {
        $classes = explode(' ', $module_class);
        foreach ($classes as $class)
        {
        switch ($class)
            {
              case 'bs-alert':
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.alert', '.alert');
                break;
              case 'bs-button':
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.button', '.btn');
                break;
              case 'bs-carousel':
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.carousel', '.selector', []);
                break;
              case 'bs-collapse':
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.collapse', '.selector', []);
                break;
              case 'bs-dropdown':
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.dropdown', '.selector', []);
                break;
              case 'bs-modal':
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.modal', '.selector', []);
                break;
              case 'bs-offcanvas':
                // Not Found
                //\Joomla\CMS\HTML\HTMLHelper::_('bootstrap.offcanvas', '.btn', []);
                break;
              case 'bs-popover':
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.popover', '.btn', []);
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.popover', 'a', []);
                break;
              case 'bs-scrollspy':
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.scrollspy', '.selector', []);
                break;
              case 'bs-tab':
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.tab', '.selector', []);
                break;
              case 'bs-tooltip':
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.tooltip', '.btn', []);
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.tooltip', 'a', []);
                break;
              case 'bs-toast':
                \Joomla\CMS\HTML\HTMLHelper::_('bootstrap.toast', '.selector', []);
                break;
              default:
                // do nothing
            }
        }
    }
```

Questo codice cerca i nomi delle classi impostate in mod_custom e effettua la chiamata a HTMLHelper per configurare il supporto JavaScript. Nota che l'ultimo elemento in ogni chiamata è un selettore che può o non può essere utilizzato per attivare l'azione. Molti dei componenti sono attivati da attributi dati nel mark-up e non utilizzano i selettori qui. Per alcuni, il selettore è necessario. Ad esempio, ha senso utilizzare la classe **.btn** e il tag **a** per attivare i suggerimenti.

### Un Modulo mod_custom per un Componente Modale

- Vai a **Contenuto** → **Moduli del sito** → **Nuovo**.
- Seleziona il modulo **Custom**.
- Compila il modulo:
  - Titolo: Demo Modal
  - Nel campo Posizione digita **demomodal** per l'uso in un articolo;
  - Contenuto del modulo: Attiva/Disattiva Editor per l'inserimento di testo semplice.
  - Incolla il seguente codice dalla documentazione di Bootstrap:

```html
<h2>Modal</h2>
<!-- Button trigger modal -->
<p><button class="btn btn-primary" type="button" data-bs-toggle="modal" data-bs-target="#exampleModal"> Launch demo modal </button></p>
<!-- Modal -->
<div id="exampleModal" class="modal fade" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
        <div class="modal-content">
            <div class="modal-header">
                <h5 id="exampleModalLabel" class="modal-title">Modal title</h5>
                <button class="btn-close" type="button" data-bs-dismiss="modal" aria-label="Close"></button>
            </div>
            <div class="modal-body">
                ...
            </div>
            <div class="modal-footer">
                <button class="btn btn-secondary" type="button" data-bs-dismiss="modal">Close</button>
                <button class="btn btn-primary" type="button">Save changes</button>
            </div>
        </div>
    </div>
</div>
```

- Seleziona la scheda Avanzate e nel campo Classe Modulo inserisci **bs-modal**
- Facoltativo: imposta Titolo su Nascondi per utilizzare l'H2 nel codice incollato.
- Salva e Chiudi (non preoccuparti se il modale appare sbagliato nell'editor).

### Creare un Articolo e un Elemento di Menu

- Crea un nuovo articolo, Modalità Demo, e in modalità di inserimento testo normale imposta il contenuto su

```html
<div>{loadposition demomodal}</div>
```

- Crea un elemento di menu Articolo Singolo.
- Provalo:

![Bootstrap modal module in article](../../../en/images/coding-examples/coding-examples-modal-module.png)

### Un Componente Modale Contenente un Carousel

- Crea un nuovo modulo personalizzato con un nuovo titolo: Demo Modal Carousel
- Posizione: demomodalcarousel
- **Scheda Avanzato**→**Classe del Modulo**: bs-modal bs-carousel
- Contenuto personalizzato del modulo in testo semplice:

```html
<h2>Modal with Carousel</h2>
<div class="mod-custom custom">
    <!-- Button trigger modal -->
    <button class="btn btn-primary" type="button" data-bs-toggle="modal" data-bs-target="#exampleModal"> Launch demo modal </button>
</div>
<div id="exampleModal" class="modal fade" style="display: none;" tabindex="-1" aria-hidden="true">
    <div class="modal-dialog" role="document">
        <div class="modal-content">
            <div class="modal-header">
                <button class="close" type="button" data-bs-dismiss="modal" aria-label="Close">
                    <span aria-hidden="true">×</span>
                </button>
            </div>
            <div class="modal-body">
                <div id="carouselExampleCaptions" class="carousel slide" data-bs-ride="carousel">
                    <div class="carousel-indicators">
                        <button class="active" type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="0" aria-current="true" aria-label="Slide 1"></button>
                        <button type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="1" aria-label="Slide 2"></button>
                        <button type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide-to="2" aria-label="Slide 3"></button>
                    </div>
                    <div class="carousel-inner">
                        <div class="carousel-item active">
                            <img class="d-block w-100" src="images/sampledata/cassiopeia/nasa1-1200.jpg" alt="..." />
                            <div class="carousel-caption d-none d-md-block">
                                <h5>First slide label</h5>
                                <p>Some representative placeholder content for the first slide.</p>
                            </div>
                        </div>
                        <div class="carousel-item">
                            <img class="d-block w-100" src="images/sampledata/cassiopeia/nasa2-1200.jpg" alt="..." />
                            <div class="carousel-caption d-none d-md-block">
                                <h5>Second slide label</h5>
                                <p>Some representative placeholder content for the second slide.</p>
                            </div>
                        </div>
                        <div class="carousel-item">
                            <img class="d-block w-100" src="images/sampledata/cassiopeia/nasa3-1200.jpg" alt="..." />
                            <div class="carousel-caption d-none d-md-block">
                                <h5>Third slide label</h5>
                                <p>Some representative placeholder content for the third slide.</p>
                            </div>
                        </div>
                    </div>
                    <button class="carousel-control-prev" type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide="prev">
                        <span class="visually-hidden">Previous</span>
                    </button>
                    <button class="carousel-control-next" type="button" data-bs-target="#carouselExampleCaptions" data-bs-slide="next">
                        <span class="visually-hidden">Next</span>
                    </button>
                </div>
            </div>
        </div>
    </div>
</div>
```

- Crea un nuovo Articolo con {loadposition demomodalcarousel} nel contenuto.
- Crea un nuovo elemento di menu per un singolo articolo: Demo Modal Carousel
- Testalo:

![Bootstrap modal carousel](../../../en/images/coding-examples/coding-examples-modal-carousel.png)

*Tradotto da openai.com*
