<!-- Filename: J4.x:Joomla_Core_APIs / Display title: Joomla Core API -->

Questa pagina elenca gli endpoint disponibili in Joomla con esempi di comandi curl. È stata preparata per Joomla 4 e richiede una verifica di conformità con le versioni attuali di Joomla.

Ogni URL richiede l'autenticazione a meno che non sia designato come URL pubblico. Per
la sicurezza in Joomla 4.0.0, pianifichiamo di far sì che l'applicazione API di default
richieda un account Super User (poiché l'applicazione API è completamente nuova), questo
potrebbe essere allentato man mano che l'API si stabilizza ed è ben testata nella
comunità. Se stai utilizzando il plugin di autenticazione di base (attualmente
l'unico plugin fornito a partire da Joomla 4 alpha 10), è necessaria
l'aggiunta ai comandi curl sotto utilizzando --user user_name:password

Ogni URL deve essere preceduto dall'host di Joomla prima del percorso
(ad esempio, invece di `/api/index.php/v1/article` hai bisogno di
`http://example.com/api/index.php/v1/article`)

Qualsiasi nome di proprietà tra parentesi graffe ({}) indica che la proprietà è una variabile che deve essere sostituita.

Se non diversamente indicato, queste API sono state introdotte in Joomla 4. Per ulteriori informazioni sulla Specifica API di Joomla (a differenza di questo elenco di URL e opzioni) visitare [Joomla Api Specification](https://docs.joomla.org/Joomla_Api_Specification).

Dove i punti finali richiedono il valore di {app}, la variabile attualmente assume due valori: sito (front end) o amministratore (back end).

## Risorse utili

Sono state create numerose risorse gratuite per presentare i Servizi Web di Joomla e aiutarti a imparare come implementare i Servizi Web nel tuo progetto.

- Collezione Postman di chiamate [Joomla Web Services API](https://github.com/alexandreelise/j4x-api-collection) di Alexandre Elise.
- Tutorial Youtube Joomla 4: [Utilizzare l'API dei servizi web](https://www.youtube.com/watch?v=lT9qodsvfZg) con Eoin Oliver.
- Joomla Community Magazine: [Joomla Web Services API 101](https://magazine.joomla.org/all-issues/august-2020/joomla-web-services-api-101-tokens,-testing-and-a-taste-test) di Patrick Jackson.

## Componente Banner

### Striscioni

#### Ottieni l'elenco dei banner

curl -X GET /api/index.php/v1/banner

#### Ottieni un Singolo Banner

`curl -X GET /api/index.php/v1/banners/{banner_id}`

#### Elimina Banner

curl -X DELETE /api/index.php/v1/banner/{banner_id}

#### Crea Banner

curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/banners -d

```json
{
    "catid": 3,
    "clicks": 0,
    "custombannercode": "",
    "description": "Testo",
    "metakey": "",
    "name": "Nome",
    "params": {
        "alt": "",
        "height": "",
        "imageurl": "",
        "width": ""
    }
}
```

#### Aggiorna Banner

curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/banners/{banner_id} -d

{
    "alias": "nome",
    "catid": 3,
    "description": "Nuovo Testo",
    "name": "Nuovo Nome"
}

### Clienti

#### Ottieni l'elenco dei clienti

curl -X GET /api/index.php/v1/banners/clienti

#### Ottieni singolo cliente

curl -X GET /api/index.php/v1/banner/clienti/{client_id}

#### Elimina cliente

curl -X DELETE /api/index.php/v1/banners/clienti/{client_id}

#### Crea Cliente

curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/banner/clienti -d

```json
{
    "contact": "Nome",
    "email": "email@mail.com",
    "extrainfo": "",
    "metakey": "",
    "name": "Clienti",
    "state": 1
}
```

#### Aggiorna Cliente

curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/banners/clients/{client_id} -d

{
    "contact": "nuovo Nome",
    "email": "nuovaemail@mail.com",
    "name": "Clienti"
}

### Categorie di Banner

#### Ottieni l'elenco delle categorie

curl -X GET /api/index.php/v1/banners/categorie

#### Ottieni Singola Categoria

curl -X GET /api/index.php/v1/banners/categories/{category_id}

#### Elimina Categoria

curl -X DELETE /api/index.php/v1/banner/categorie/{category_id}

#### Crea Categoria

curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/banners/categorie -d

{
    "access": 1,
    "alias": "cat",
    "extension": "com_banners",
    "language": "*",
    "note": "",
    "parent_id": 1,
    "published": 1,
    "title": "Titolo"
}

#### Aggiorna categoria

curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/banners/categories/{category_id} -d

```json
{
    "alias": "cat",
    "note": "Alcuni Testi",
    "parent_id": 1,
    "title": "Nuovo Titolo"
}
```

### Cronologia del Contenuto dei Banner

#### Ottieni elenco delle cronologie dei contenuti

curl -X GET /api/index.php/v1/banners/contenthistory/{banner_id}

#### Attiva/Disattiva Cronologia Contenuti

curl -X PATCH -H "Content-Type: application/json"  
/api/index.php/v1/banners/contenthistory/keep/{contenthistory_id}

#### Elimina Cronologia Contenuti

curl -X DELETE
/api/index.php/v1/banners/contenthistory/{contenthistory_id}

## Componente di Configurazione

### Applicazione

#### Ottieni l'elenco delle configurazioni dell'applicazione

curl -X GET /api/index.php/v1/config/application

#### Aggiorna Configurazione Applicazione

curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/config/application -d

{
    "debug": true,
    "sitename": "123"
}

### Componente

#### Ottieni l'elenco delle configurazioni dei componenti

curl -X GET /api/index.php/v1/config/{nome_componente}

Esempio “component_name” è “com_content”.

#### Aggiorna Configurazione dell'Applicazione del Componente

```
curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/config/application -d
```

{
    "collegamento_titoli": 1
}

## Componente Contatti

### Contatto

#### Ottieni Elenco dei Contatti

curl -X GET /api/index.php/v1/contact

#### Ottieni Contatto Singolo

curl -X GET /api/index.php/v1/contact/{contact_id}

#### Elimina Contatto

curl -X DELETE /api/index.php/v1/contact/{contact_id}

#### Crea Contatto

curl -X POST -H "Content-Type: application/json" /api/index.php/v1/contact -d

{
    "alias": "contatto",
    "catid": 4,
    "language": "*",
    "name": "Contatto"
}

#### Aggiorna contatto

curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/contact/{contact_id} -d

```json
{
    "alias": "contatto",
    "catid": 4,
    "name": "Nuovo Contatto"
}
```

#### Invia modulo di contatto

curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/contact/form/{contact_id} -d

```json
{
    "contact_email": "email@mail.com",
    "contact_message": "alcuni testi",
    "contact_name": "nome",
    "contact_subject": "oggetto"
}
```

### Categorie di contatto

1. La Route per le Categorie di Contatto è: "v1/contact/categories"
2. Lavorare con esso è simile alle Categorie dei Banner.

### Contatti dei campi

#### Ottieni l'elenco dei campi contatto

curl -X GET /api/index.php/v1/fields/contact/contact

#### Ottieni un Contatto da Campo Singolo

curl -X GET /api/index.php/v1/fields/contact/contact/{field_id}

#### Elimina Campo Contatto

curl -X DELETE /api/index.php/v1/campi/contatto/contatto/{field_id}

#### Crea Contatto Campo

curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/fields/contact/contact -d

```json
{
    "access": 1,
    "context": "com_contact.contact",
    "default_value": "",
    "description": "",
    "group_id": 0,
    "label": "campo contatto",
    "language": "*",
    "name": "campo-contatto",
    "note": "",
    "params": {
        "class": "",
        "display": "2",
        "display_readonly": "2",
        "hint": "",
        "label_class": "",
        "label_render_class": "",
        "layout": "",
        "prefix": "",
        "render_class": "",
        "show_on": "",
        "showlabel": "1",
        "suffix": ""
    },
    "required": 0,
    "state": 1,
    "title": "campo contatto",
    "type": "text"
}
```

#### Aggiorna Contatto Campo

curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/fields/contact/contact/{field_id} -d

```json
{
    "title": "nuovo campo di contatto",
    "name": "campo-di-contatto",
    "label": "campo di contatto",
    "default_value": "",
    "type": "testo",
    "note": "",
    "description": "Alcuni nuovi testi"
}
```

### Campi Contatto Mail

1.  Il campo Route Fields Contact Mail è: "v1/fields/contact/mail"
2.  Lavorare con esso è simile a Fields Contact.

### Campi Categorie Contatti

1. Il percorso dei Campi Categorie Contatto è: "v1/fields/contact/categories"
2. Lavorare con esso è simile a Campi Contatto.

### Campi Gruppi Contatto

#### Ottieni Elenco dei Campi dei Gruppi di Contatto

curl -X GET /api/index.php/v1/fields/groups/contact/contact

#### Ottieni i campi contatto di un singolo gruppo

curl -X GET /api/index.php/v1/fields/groups/contact/contact/{group_id}

#### Elimina campi contatti del gruppo

curl -X DELETE
/api/index.php/v1/fields/groups/contact/contact/{group_id}

#### Crea Campi di Gruppo Contatto

```
curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/fields/groups/contact/contact -d
```

```json
{
    "access": 1,
    "context": "com_contact.contact",
    "default_value": "",
    "description": "",
    "group_id": 0,
    "label": "campo contatto",
    "language": "*",
    "name": "campo-contatto3",
    "note": "",
    "params": {
        "class": "",
        "display": "2",
        "display_readonly": "2",
        "hint": "",
        "label_class": "",
        "label_render_class": "",
        "layout": "",
        "prefix": "",
        "render_class": "",
        "show_on": "",
        "showlabel": "1",
        "suffix": ""
    },
    "required": 0,
    "state": 1,
    "title": "campo contatto",
    "type": "text"
}
```

#### Aggiorna i campi del contatto del gruppo

curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/fields/groups/contact/contact/{group_id} -d

```json
{
    "title": "nuovo gruppo di contatti",
    "note": "",
    "description": "nuova descrizione"
}
```

### Contatto e-mail dei campi del gruppo

1. Il campo gruppo Rotta Mail contatto è: "v1/fields/groups/contact/mail"
2. Lavorare con esso è simile al Gruppo campi contatto.

### Categorie di Contatto dei Campi di Gruppo

1. Route Group Fields Contact Categories è: "v1/fields/groups/contact/categories"
2. Lavorare con esso è simile a Group Fields Contact.

### Cronologia Contenuti Contatti

1. La cronologia dei contenuti della rotta è: "v1/contact/contenthistory"
2. Lavorarci è simile alla cronologia dei contenuti dei banner.

## Componente di Contenuto

### Articoli

#### Ottieni elenco di articoli

curl -X GET /api/index.php/v1/content/articoli

#### Ottieni Articolo Singolo

curl -X GET /api/index.php/v1/contenuto/articoli/{article_id}

#### Elimina Articolo

curl -X DELETE /api/index.php/v1/content/articles/{article_id}

#### Crea Articolo

```
curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/content/articles -d
```

```json
{
    "alias": "my-article",
    "articletext": "Il mio testo",
    "catid": 64,
    "language": "*",
    "metadesc": "",
    "metakey": "",
    "title": "Ecco un articolo"
}
```

Attualmente le opzioni menzionate qui sono proprietà richieste. Tuttavia l'intenzione è attualmente di rendere ALMENO metakey e metadesc opzionali nell'API.

#### Aggiorna Articolo

curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/content/articles/{article_id} -d

{
    "catid": 64,
    "title": "Articolo aggiornato"
}

### Categorie di Contenuti

1. La Route delle Categorie di Contenuto è: "v1/content/categories"
2. Lavorare con essa è simile a lavorare con le Categorie di Banner. Nota: se i flussi di lavoro sono abilitati, allora è necessario specificare un flusso di lavoro (in modo simile all'interfaccia utente)

### Articoli sui Campi

1. Route Fields Articoli è: "v1/fields/content/articles"
2. Lavorare con esso è simile a Fields Contact.

### Articoli sui campi dei gruppi

1.  Gli articoli dei campi dei gruppi di route sono: "v1/fields/groups/content/articles"
2.  Lavorarci è simile a Gruppi Campi Contatto.

### Categorie dei campi

1. Le categorie dei campi del percorso sono: "v1/fields/groups/content/categories"
2. Lavorare con esso è simile a Campi Contatto.

### Contenuto Componente Cronologia del Contenuto

1. La Cronologia del Contenuto del Percorso è:
    "v1/content/articles/{article_id}/contenthistory"

2. Lavorare con essa è simile alla Cronologia del Contenuto dei Banner.

## Componente Lingue

### Lingue

#### Ottieni l'elenco delle lingue

curl -X GET /api/index.php/v1/lingue

#### Installa lingua

curl -X POST -H "Content-Type: application/json" /api/index.php/v1/languages -d

{
        "package": "pkg_it-IT"
    }

### Lingue dei contenuti

#### Ottieni l'elenco delle lingue dei contenuti

curl -X GET /api/index.php/v1/languages/content

#### Ottieni la lingua del singolo contenuto

`curl -X GET /api/index.php/v1/v1/languages/content/{language_id}`

#### Elimina lingua del contenuto

`curl -X DELETE /api/index.php/v1/languages/content/{language_id}`

#### Crea Lingua Contenuto

curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/languages/content -d

{
    "accesso": 1,
    "descrizione": "",
    "immagine": "fr_FR",
    "codice_lingua": "fr-FR",
    "metadescrizione": "",
    "metachia": "",
    "ordinamento": 1,
    "pubblicato": 0,
    "sef": "fk",
    "nome_sito": "",
    "titolo": "Francese (FR)",
    "titolo_nativo": "Français (France)"
}

#### Aggiorna la Lingua del Contenuto

curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/languages/content/{language_id} -d

{ "description": "", "lang_code": "it-IT", "metadesc": "", "metakey": "", "sitename": "", "title": "Italiano (it-IT)", "title_native": "Italiano (Italia)" }

### Sovrascrive Lingue

#### Ottieni l'elenco delle costanti delle lingue degli override

curl -X GET /api/index.php/v1/languages/overrides/{app}/{lang_code}

#### Ottieni una Costante di Lingua di Sovrascrittura Singola

curl -X GET
/api/index.php/v1/lingue/sostituzioni/{app}/{codice_lingua}/{id_costante}

#### Elimina le Sostituzioni della Lingua del Contenuto

curl -X DELETE
/api/index.php/v1/lingue/sostituzioni/{app}/{codice_lingua}/{id_costante}

#### Crea Sostituzioni della Lingua dei Contenuti

curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/languages/overrides/{app}/{lang_code} -d

{
        "key":"new_key",
        "override": "testo"
    }

#### Aggiorna le Sovrascritture della Lingua del Contenuto

```markdown
curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/languages/overrides/{app}/{lang_code}/{constant_id} -d
```

```json
{
    "key":"nuova_chiave",
    "override": "nuovo testo"
}
```

var app - enum {"sito", "amministratore"}

var lang_code - string Esempio: “fr-FR“, “en-GB“ puoi ottenere lang_code
da v1/languages/content

#### Costante di Sovrascrittura Ricerca

curl -X POST -H "Content-Type: application/json"  
/api/index.php/v1/languages/overrides/search -d

```json
{
    "searchstring": "JLIB_APPLICATION_ERROR_SAVE_FAILED",
    "searchtype": "costante"
}
```

var searchtype - enum {“constant”, “value”}. “constant” ricerca per
nome costante, “value” - ricerca per valore costante

#### Aggiorna la Cache di Ricerca Sovrascritta

curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/lingue/sostituzioni/ricerca/cache/aggiorna

## Componente Menù

### Menu

#### Ottieni Elenco dei Menu

curl -X GET /api/index.php/v1/menù/{app}

#### Ottieni Menu Singolo

curl -X GET /api/index.php/v1/menu/{app}/{menu_id}

#### Elimina Menu

curl -X DELETE /api/index.php/v1/menus/{app}/{menu_id}

#### Crea Menu

curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/menus/{app} -d

```json
{
    "client_id": 0,
    "description": "Il menu per il sito",
    "menutype": "menu",
    "title": "Menu"
}
```

#### Aggiorna Menu

```
curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/menus/{app}/{menu_id} -d
```

```json
{
    "menutype": "menu",
    "title": "Nuovo Menu"
}
```

### Elementi del Menù

#### Ottieni l'elenco dei tipi di voci di menu

curl -X GET /api/index.php/v1/menus/{app}/items/tipi

#### Ottieni l'elenco degli articoli del menu

curl -X GET /api/index.php/v1/menus/{app}/elementi

#### Ottieni Voce di Menu Singola

curl -X GET /api/index.php/v1/menus/{app}/items/{menu_item_id}

#### Elimina Voce di Menu

curl -X DELETE /api/index.php/v1/menù/{app}/articoli/{menu_item_id}

#### Crea Voce di Menu

curl -X POST -H "Content-Type: application/json"  
/api/index.php/v1/menus/{app}/items -d

```json
{
    "accesso": "1",
    "alias": "",
    "associazioni": {
        "en-GB": "",
        "fr-FR": ""
    },
    "browserNav": "0",
    "component_id": "20",
    "home": "0",
    "lingua": "*",
    "link": "index.php?option=com_content&view=form&layout=edit",
    "tipo_menu": "mainmenu",
    "nota": "",
    "parametri": {
        "annulla_redirect_itemmenu": "",
        "catid": "",
        "redirect_personalizzato_annulla": "0",
        "abilita_categoria": "0",
        "menu-anchor_css": "",
        "menu-anchor_title": "",
        "menu-meta_descrizione": "",
        "menu-meta_parole_chiave": "",
        "menu_image": "",
        "menu_image_css": "",
        "menu_mostra": "1",
        "menu_testo": "1",
        "intestazione_pagina": "",
        "titolo_pagina": "",
        "pageclass_sfx": "",
        "redireziona_itemmenu": "",
        "robots": "",
        "mostra_intestazione_pagina": ""
    },
    "parent_id": "1",
    "pubblica_giù": "",
    "pubblica_sù": "",
    "pubblicato": "1",
    "id_stile_template": "0",
    "titolo": "titolo",
    "toggle_modules_assigned": "1",
    "toggle_modules_published": "1",
    "tipo": "componente"
}
```

Esempio per "Crea pagina articolo"

#### Aggiorna Voce del Menu

curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/menus/{app}/items/{menu_item_id} -d

```json
{
    "component_id": "20",
    "language": "*",
    "link": "index.php?option=com_content&view=form&layout=edit",
    "menutype": "menuprincipale",
    "note": "",
    "title": "nuovo titolo",
    "type": "componente"
}
```

Esempio per "Crea Pagina Articolo"

## Componente Messaggi

### Messaggi

#### Ottieni Elenco dei Messaggi

curl -X GET /api/index.php/v1/messages

#### Ottieni Messaggio Singolo

curl -X GET /api/index.php/v1/messages/{message_id}

#### Elimina Messaggio

curl -X DELETE /api/index.php/v1/messaggi/{message_id}

#### Crea Messaggio

curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/messaggi -d

```json
{
    "messaggio": "text",
    "stato": 0,
    "oggetto": "text",
    "id_utente_da": 773,
    "id_utente_a": 772
}
```

#### Aggiorna Messaggio

curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/messages/{message_id} -d

{
    "message": "nuovo testo",
    "subject": "nuovo testo",
    "user_id_from": 773,
    "user_id_to": 772
}

## Componente Moduli

### Moduli

#### Ottieni elenco dei tipi di moduli

curl -X GET /api/index.php/v1/modules/types/{app}

#### Ottieni l'elenco dei moduli

curl -X GET /api/index.php/v1/modules/{app}

#### Ottieni Modulo Singolo

curl -X GET /api/index.php/v1/modules/{app}/{module_id}

#### Elimina Modulo

curl -X DELETE /api/index.php/v1/modules/{app}/{module_id}

#### Crea Modulo

curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/moduli/{app} -d

```json
{
    "accesso": "1",
    "assegnato": [
        "101",
        "105"
    ],
    "assegnazione": "0",
    "client_id": "0",
    "lingua": "*",
    "modulo": "mod_articles_archive",
    "nota": "",
    "ordinamento": "1",
    "parametri": {
        "dimensione_bootstrap": "0",
        "cache": "1",
        "tempo_cache": "900",
        "modalità_cache": "statico",
        "conteggio": "10",
        "classe_header": "",
        "tag_header": "h3",
        "layout": "_:default",
        "tag_modulo": "div",
        "classe_sfx_modulo": "",
        "stile": "0"
    },
    "posizione": "",
    "pubblicazione_giù": "",
    "pubblicazione_su": "",
    "pubblicato": "1",
    "mostra_titolo": "1",
    "titolo": "Titolo"
}
```

Esempio per "Articoli - Archiviati"

#### Aggiorna Modulo

```
curl -X PATCH -H "Content-Type: application/json" /api/index.php/v1/modules/{app}/{module_id} -d
```

```json
{
    "access": "1",
    "client_id": "0",
    "language": "*",
    "module": "mod_articles_archive",
    "note": "",
    "ordering": "1",
    "title": "Nuovo Titolo"
}
```

Esempio per "Articoli - Archiviati"

## Componente dei Feed di Notizie

### Feed

#### Ottieni Elenco dei Feed

curl -X GET /api/index.php/v1/newsfeeds/feeds

#### Ottieni Feed Singolo

curl -X GET /api/index.php/v1/newsfeeds/feeds/{feed_id}

#### Elimina Feed

curl -X DELETE /api/index.php/v1/newsfeeds/feeds/{feed_id}

#### Crea Feed

curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/newsfeeds/feeds -d

```json
{
    "access": 1,
    "alias": "alias",
    "catid": 5,
    "description": "",
    "images": {
        "float_first": "",
        "float_second": "",
        "image_first": "",
        "image_first_alt": "",
        "image_first_caption": "",
        "image_second": "",
        "image_second_alt": "",
        "image_second_caption": ""
    },
    "language": "*",
    "link": "http://samoylov/joomla/gsoc19_webservices/index.php",
    "metadata": {
        "hits": "",
        "rights": "",
        "robots": "",
        "tags": {
            "tags": "",
            "typeAlias": null
        }
    },
    "metadesc": "",
    "metakey": "",
    "name": "Nome",
    "ordering": 1,
    "params": {
        "feed_character_count": "",
        "feed_display_order": "",
        "newsfeed_layout": "",
        "show_feed_description": "",
        "show_feed_image": "",
        "show_item_description": ""
    },
    "published": 1
}
```

#### Aggiornamento Feed

curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/newsfeeds/feeds/{feed_id} -d

```json
{
    "accesso": 1,
    "alias": "test2",
    "catid": 5,
    "descrizione": "",
    "collegamento": "http://samoylov/joomla/gsoc19_webservices/index.php",
    "metadesc": "",
    "metakey": "",
    "nome": "Test"
}
```

### Categorie dei Feed di Notizie

1. La route delle Categorie dei Flussi di Notizie è: "v1/newsfeeds/categories"
2. Lavorare con essa è simile alle Categorie dei Banner.

## Componente di Privacy

### Richiesta

#### Ottieni elenco delle richieste

curl -X GET /api/index.php/v1/privacy/request

#### Ottieni Richiesta Singola

curl -X GET /api/index.php/v1/privacy/request/{request_id}

#### Ottieni i Dati di Esportazione di una Singola Richiesta

`curl -X GET /api/index.php/v1/privacy/request/export/{request_id}`

#### Crea Richiesta

```
curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/privacy/richiesta -d
```

{
    "email":"somenewemail@com.ua",
    "request_type":"esporta"
}

### Consenso

#### Ottieni l'elenco dei consensi

curl -X GET /api/index.php/v1/privacy/consenso

#### Ottieni il singolo consenso

curl -X GET /api/index.php/v1/privacy/consent/{consent_id}

#### Elimina il consenso

curl -X DELETE /api/index.php/v1/privacy/consenso/{consent_id}

## Componente di Reindirizzamento

### Reindirizzamento

#### Ottieni elenco di reindirizzamenti

curl -X GET /api/index.php/v1/redirect

#### Ottieni Singolo Reindirizzamento

curl -X GET /api/index.php/v1/redirect/{redirect_id}

#### Elimina reindirizzamento

`curl -X DELETE /api/index.php/v1/redirect/{redirect_id}`

#### Crea Reindirizzamento

curl -X POST -H "Content-Type: application/json"
/api/index.php/v1/redirect -d

```json
{
    "comment": "",
    "header": 301,
    "hits": 0,
    "new_url": "/content/art/99",
    "old_url": "/content/art/12",
    "published": 1,
    "referer": ""
}
```

#### Aggiorna Reindirizzamento

curl -X PATCH -H "Content-Type: application/json" /api/index.php/v1/redirect/{redirect_id} -d

```json
{
    "new_url": "/content/art/4",
    "old_url": "/content/art/132"
}
```

## Componente Tag

### Tag

#### Ottieni l'elenco dei tag

curl -X GET /api/index.php/v1/tags

#### Ottieni Singolo Tag

curl -X GET /api/index.php/v1/tags/{tag_id}

#### Elimina Tag

curl -X DELETE /api/index.php/v1/tags/{tag_id}

#### Crea Tag

curl -X POST -H "Content-Type: application/json" /api/index.php/v1/tags -d

{
    "accesso": 1,
    "titolo_accesso": "Pubblico",
    "alias": "test",
    "descrizione": "",
    "lingua": "*",
    "nota": "",
    "id_genitore": 1,
    "percorso": "test",
    "pubblicato": 1,
    "titolo": "test"
}

#### Aggiorna Tag

curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/tags/{tag_id} -d

{
        "alias": "test",
        "title": "nuovo titolo"
}

## Modelli

### Stili dei modelli

#### Ottieni l'elenco degli stili dei modelli

curl -X GET /api/index.php/v1/templates/styles/{app}

#### Ottieni Stile Singolo del Modello

`curl -X GET /api/index.php/v1/templates/styles/{app}/{template_style_id}`

#### Elimina stile del modello

curl -X DELETE
/api/index.php/v1/templates/styles/{app}/{template_style_id}

#### Crea stile modello

curl -X POST -H "Content-Type: application/json" /api/index.php/v1/templates/styles/{app} -d

{
    "home": "0",
    "params": {
        "fluidContainer": "0",
        "logoFile": "",
        "sidebarLeftWidth": "3",
        "sidebarRightWidth": "3"
    },
    "template": "cassiopeia",
    "title": "cassiopeia - Alcuni Testi"
}

#### Aggiorna stile modello

curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/templates/styles/{app}/{template_style_id} -d

```json
{
    "template": "cassiopeia",
    "title": "nuova cassiopeia - Predefinito"
}
```

## Componente Utenti

### Utenti

#### Ottenere l'elenco degli utenti

curl -X GET /api/index.php/v1/utenti

#### Ottieni Singolo Utente

curl -X GET /api/index.php/v1/utenti/{user_id}

#### Elimina Utente

curl -X DELETE /api/index.php/v1/users/{user_id}

#### Crea Utente

curl -X POST -H "Content-Type: application/json" /api/index.php/v1/utenti -d

```json
{
    "blocco": "0",
    "email": "test@mail.com",
    "gruppi": [
        "2"
    ],
    "id": "0",
    "ultimoTempoReset": "",
    "ultimaDataVisita": "",
    "nome": "nnn",
    "parametri": {
        "lingua_admin": "",
        "stile_admin": "",
        "editor": "",
        "sito_aiuto": "",
        "lingua": "",
        "fuso_orario": ""
    },
    "password": "qwertyqwerty123",
    "password2": "qwertyqwerty123",
    "dataRegistrazione": "",
    "richiedeReset": "0",
    "conteggioReset": "0",
    "inviaEmail": "0",
    "nome_utente": "ad"
}
```

#### Aggiorna Utente

curl -X PATCH -H "Content-Type: application/json"
/api/index.php/v1/users/{user_id} -d

{
    "email": "nuovo@mail.com",
    "groups": [
        "2"
    ],
    "name": "nome",
    "username": "nomeutente"
}

### Campi Utenti

1.  Gli utenti dei campi di rotta sono: "v1/fields/users"
2.  Lavorare con esso è simile a lavorare con Contatti dei campi.

### Gruppi Campi Utenti

1. Route Groups Fields Users è: "v1/fields/groups/users"
2. Lavorare con esso è simile a Groups Fields Contact.

*Tradotto da openai.com*

