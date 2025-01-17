<!-- Filename: API_Guides / Display title: Guide API -->

Questa pagina contiene un indice alla serie di Guide API di Joomla. Queste guide mirano ad aiutarti a comprendere come utilizzare queste funzioni Joomla nelle tue estensioni Joomla.

Ogni guida API include un esempio di codice che puoi copiare e installare nel tuo ambiente di sviluppo. Generalmente questi esempi di codice sono scritti per essere inclusi e installati come modulo Joomla, quindi se non hai familiarità con lo sviluppo di moduli Joomla potresti trovare utile consultare la breve serie [Creare un Modulo Semplice](https://docs.joomla.org/Creating_a_simple_module "Creating a simple module").

Intorno a Joomla 3.8, il team di sviluppo di Joomla ha iniziato a cambiare la convenzione di denominazione delle classi di Joomla per utilizzare gli spazi dei nomi, in modo che, ad esempio, JFactory sia cambiato in Factory nello spazio dei nomi Joomla\CMS. Mentre leggi il codice e la documentazione esistenti di Joomla, potresti trovare le classi che seguono sia il nuovo che il vecchio standard di denominazione. Puoi trovare la mappatura tra le due convenzioni di denominazione nel file `libraries/classmap.php` nella tua istanza di Joomla.

- Le classi base dell'Applicazione e la loro gerarchia e scopi sono descritti in [Understanding the Application classes](https://docs.joomla.org/J3.x:Understanding_the_Application_classes).
- La gestione Ajax all'interno dei Componenti Joomla è descritta in [JSON Responses with JResponseJson](https://docs.joomla.org/JSON_Responses_with_JResponseJson). L'Ajax può anche essere utilizzato all'interno dei Moduli e Plugin Joomla come descritto in [Using Joomla Ajax Interface](https://docs.joomla.org/Using_Joomla_Ajax_Interface).
- [Cache](https://docs.joomla.org/Cache_Basic_API_Guide) - come utilizzare il callback cache nel tuo codice.
- [Categorie](https://docs.joomla.org/Categories_and_CategoryNodes_API_Guide) Utilizzare le classi `Categories` e `CategoryNode` per accedere ai dati relativi alle categorie di Joomla.
- È possibile aggiungere CSS come descritto in [Adding JavaScript and CSS to the page](https://docs.joomla.org/Adding_JavaScript_and_CSS_to_the_page).
- Database / JDatabase. Ci sono due guide API, che trattano [Selecting data using JDatabase](https://docs.joomla.org/Selecting_data_using_JDatabase)
  e [Inserting, Updating and Removing data using JDatabase](https://docs.joomla.org/Inserting,_Updating_and_Removing_data_using_JDatabase).
- [Data/JDate](https://docs.joomla.org/How_to_use_JDate) è la classe Data di Joomla.
- File e Cartelle. Vedi [How to use the filesystem package](https://docs.joomla.org/How_to_use_the_filesystem_package).
- Form / JForm. C'è una [Guida base](https://docs.joomla.org/Basic_form_guide) all'utilizzo dell'API Form di Joomla e all'incorporazione dei form all'interno di un componente Joomla, e anche una [Guida avanzata](https://docs.joomla.org/Advanced_form_guide) che copre gli aspetti più avanzati delle API.
- FormField / JFormField. Questa classe e classi correlate come JFormFieldList che derivano da essa sono principalmente utili per definire campi modulo personalizzati, come descritto in [Creating a custom form field type](https://docs.joomla.org/Creating_a_custom_form_field_type).
- [Input / JInput](https://docs.joomla.org/Retrieving_request_data_using_JInput) Utilizzare la classe `Input` per ottenere i valori dei parametri nelle richieste HTTP GET e POST.
- È possibile aggiungere JavaScript come descritto in [Adding JavaScript and CSS to the page](https://docs.joomla.org/Adding_JavaScript_and_CSS_to_the_page).
- L'utilizzo dei Layout Joomla è descritto in [Sharing layouts across views or extensions with JLayout](https://docs.joomla.org/J3.x:Sharing_layouts_across_views_or_extensions_with_JLayout). La flessibilità è stata aumentata in Joomla 3.2, come descritto in [JLayout Improvements for Joomla!](https://docs.joomla.org/J3.x:JLayout_Improvements_for_Joomla!).
- [Log / JLog](https://docs.joomla.org/Using_JLog) Registra messaggi (ad es. messaggi di errore, messaggi di debug) in un file di log, e opzionalmente nella console di debug.
- [Menu e Voci di Menu](https://docs.joomla.org/Menu_and_Menuitems_API_Guide).
- [Set Annidati](https://docs.joomla.org/Using_nested_sets), che permettono di implementare una gerarchia ad albero nella tabella del database, sono utilizzati dai menu, articoli, categorie di Joomla, ecc.
- [Registro/JRegistry](https://github.com/joomla-framework/registry) è una classe utility molto utile per gestire array PHP, convertire in JSON, ecc.
- [JResponseJson](https://docs.joomla.org/JSON_Responses_with_JResponseJson) supporta la risposta in formato JSON alle richieste Ajax.
- Route / JRoute vedi [URL in Joomla](https://docs.joomla.org/URLs_in_Joomla).
- Table / JTable fornisce funzionalità per eseguire operazioni CRUD (e altro) sulle tabelle del database. La guida è divisa in una [Guida API Base](https://docs.joomla.org/Table_Basic_API_Guide)
  e una [Guida API Avanzata](https://docs.joomla.org/Table_Advanced_API_Guide).
- I [Controller](https://docs.joomla.org/Controllers) (BaseController, AdminController, FormController, ApiController) sono responsabili dell'analisi della richiesta dell'utente, controllando che l'utente sia autorizzato a eseguire quell'azione e determinando come soddisfare la richiesta.
- I [Modelli](https://docs.joomla.org/Models) (BaseModel, BaseDatabaseModel, ItemModel, ListModel, FormModel, AdminModel) incapsulano i dati utilizzati dal componente. Sono anche responsabili dell'aggiornamento del database quando appropriato.
- Le [Viste](https://docs.joomla.org/Views) (AbstractView, CategoriesView, CategoryFeedView, CategoryView, FormView, HtmlView, JsonApiView, JsonView, ListView) specificano ciò che dovrebbe apparire sulla pagina web e raccolgono tutti i dati necessari per emettere la risposta HTTP.
- [Tag](https://docs.joomla.org/Tags_API_Guide).
- Uri / JUri vedi [URL in Joomla](https://docs.joomla.org/URLs_in_Joomla).
- [Utente / JUser](https://docs.joomla.org/Accessing_the_current_user_object) API relativa all'Utente Joomla.

*Tradotto da openai.com*

