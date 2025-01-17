<!-- Filename: J4.x:Joomla_4_Tips_and_Tricks:_Form_Validation_Basics / Display title: Validazione del modulo -->

## Introduzione

Joomla ha uno script di validazione lato client che può essere utilizzato ed esteso da qualsiasi componente. Questo articolo riguarda il suo funzionamento e come usarlo. Ci sono quattro validatori standard per i tipi di campo nome utente, password, numerico e email. C'è anche un validatore di pattern più generico e un validatore per i campi obbligatori.

Nota che i browser moderni forniscono anche la validazione dei moduli per impostazione predefinita. La validazione del browser può essere disattivata includendo novalidate nel tag del modulo.

## Come invocare la convalida

All'inizio del file edit.php contenente il codice di generazione del modulo, includi la chiamata per caricare il file javascript del validatore:

```php
/** @var Joomla\CMS\WebAsset\WebAssetManager $wa */
$wa = $this->document->getWebAssetManager();
$wa->useScript('keepalive')
    ->useScript('form.validate');
```

nel tag form assicurati di includere class="form-validate". Questo esempio è dal modulo di modifica utente:

```html
<form action="<?php echo Route::_('index.php?option=com_users&layout=edit&id=' . (int) $this->item->id); ?>"
    method="post" name="adminForm" id="user-form"
    enctype="multipart/form-data"
    aria-label="<?php echo Text::_('COM_USERS_USER_FORM_' . ( (int) $this->item->id === 0 ? 'NEW' : 'EDIT'), true); ?>"
    class="form-validate">
```

Nel file di modulo XML includere le istruzioni che richiamano la convalida di ciascun campo. Questo esempio riguarda il campo email dell'utente:

```xml
        <field
            name="email"
            type="email"
            label="JGLOBAL_EMAIL"
            required="true"
            size="30"
            validate="email"
            validDomains="com_users.domains"
        />
```

## Le Espressioni di Validazione

Questa sezione è pensata per fornire una piccola comprensione delle espressioni di convalida per aiutare a spiegare l'uso. Tutte sono incluse nel codice di validator.js.

### Nome utente

```php
this.setHandler('username', value => {
      const regex = new RegExp('[<|>|"|\'|%|;|(|)|&]', 'i');
      return !regex.test(value);
    });
```

Ecco, l'espressione cerca l'occorrenza di uno qualsiasi dei caratteri alternativi all'interno della classe di caratteri [] e restituisce false (non valido) se ne trova qualcuno.

### Password

```pnp
this.setHandler('password', value => {
      const regex = /^\S[\S ]{2,98}\S$/;
      return regex.test(value);
    });
```

Qui l'espressione cerca un carattere iniziale che non è uno spazio e seguito da 2 a 98 caratteri che non sono spazi o uno spazio e termina con un carattere non di spazio bianco. Joomla ha un controllo delle password più sofisticato che garantisce un mix di tipi di carattere e una lunghezza minima.

### Email

```php
this.setHandler('email', value => {
      const newValue = punycode.toASCII(value);
      const regex = /^[a-zA-Z0-9.!#$%&’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/;
      return regex.test(newValue);
    }); // Attach all forms with a class 'form-validate'
```

Qui l'espressione regolare accetta qualsiasi stringa che inizi con uno o più caratteri nella classe di caratteri [], seguiti da @, seguiti da uno o più caratteri nella seconda classe di caratteri [], seguiti da zero o più punti seguiti da uno o più caratteri nel terzo gruppo di classi di caratteri, e terminando con uno dei gruppi dopo il @.

Anche se tecnicamente corretto, questo validatore permette alcuni indirizzi email piuttosto sciocchi come !@me - potresti voler creare un modello più restrittivo.

### Numerico

```php
this.setHandler('numeric', value => {
      const regex = /^(\d|-)?(\d|,)*\.?\d*$/;
      return regex.test(value);
    });
```

Qui il valore deve iniziare con una cifra o un segno meno zero o una volta, essere seguito da una cifra o una virgola zero o più volte, seguita da un punto zero o una volta, terminando con una cifra zero o più volte. Quindi corrisponderà a 3.142 o -10 o 100.000,0 e così via. Il numero effettivo deve corrispondere a qualsiasi sia il tipo di campo nel database. L'espressione non corrisponderà a numeri con esponenti, quindi 10e2 sarà rifiutato.

### Motivo

Supponiamo che tu voglia un campo di input che sia un numero intero positivo. Potresti usare il tuo modello inserito nel file xml del modulo:

```xml
        <field
            name="number"
            type="text"
            label="COM_MYCOMPONENT_CAMP_NUMBER_LABEL"
            description="COM_MYCOMPONENT_CAMP_NUMBER_DESC"
            class="w-auto"
            required="true"
            pattern="\d+"
        />
```

Qui il modello consente una o più cifre. Quindi -1 sarebbe non valido, così come 3.142.

### Richiesto

Assicurati di includere required="true" nella specifica del campo altrimenti l'etichetta del modulo ometterà l'asterisco * comunemente usato per indicare i campi obbligatori. Includere required nella classe non è sufficiente per la convalida.

*Tradotto da openai.com*

