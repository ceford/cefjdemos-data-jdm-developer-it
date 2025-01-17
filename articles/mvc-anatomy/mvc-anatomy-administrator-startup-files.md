<!-- Filename: J4.x:MVC_Anatomy:_Administrator_Startup_Files / Display title: Anatomia MVC: File di Avvio dell'Amministratore -->

## Panoramica dei File dell'Amministratore

Ci sono più file nella parte amministrativa del componente, in parte perché ci sono due tabelle, ciascuna con una vista elenco e di modifica, e in parte perché alcuni dei file controllano aspetti del comportamento del componente sia nelle interfacce del sito che dell'amministratore.

La creazione del codice per una vista elenco è stata trattata nella parte del tutorial che si occupa dei file del sito, quindi non verrà ripetuta qui. Questa sezione tratterà i file comuni alla maggior parte dei componenti. Un tutorial successivo coprirà una delle viste di modifica necessarie per aggiornare o aggiungere nuovi record.

## servizi/fornitore.php

Questo file viene utilizzato quando l'applicazione Joomla chiama il ComponentHelper per renderizzare il componente. È il primissimo codice del componente eseguito sia per il Sito che per l'Amministratore. Il suo ruolo è registrare il componente:

```php
    public function register(Container $container)
    {
        $container->registerServiceProvider(new MVCFactory('\\Cefjdemos\\Component\\Countrybase'));
        $container->registerServiceProvider(new ComponentDispatcherFactory('\\Cefjdemos\\Component\\Countrybase'));
        $container->registerServiceProvider(new RouterFactory('\\Cefjdemos\\Component\\Countrybase'));
        $container->set(
            ComponentInterface::class,
            function (Container $container) {
                $component = new CountrybaseComponent($container->get(ComponentDispatcherFactoryInterface::class));
                $component->setMVCFactory($container->get(MVCFactoryInterface::class));
                $component->setRouterFactory($container->get(RouterFactoryInterface::class));

                return $component;
            }
        );
    }
```

## src/Estensione/CountrybaseComponent.php

La funzione di registrazione di questo file viene chiamata dalla dichiarazione \$component = new CountrybaseComponent(...); nel file services/provider.php. Il suo scopo è avviare il componente in entrambe le interfacce Sito e Amministratore.

```php
       public function boot(ContainerInterface $container)
        {
        }
```

## access.xml

Questo file imposta i controlli di accesso utilizzati in questo componente. Gli elementi elencati qui appaiono nella scheda Opzioni Permessi del componente.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<access component="com_countrybase">
    <section name="component">
        <action name="core.admin" title="JACTION_ADMIN" />
        <action name="core.options" title="JACTION_OPTIONS" />
        <action name="core.manage" title="JACTION_MANAGE" />
        <action name="core.create" title="JACTION_CREATE" />
        <action name="core.delete" title="JACTION_DELETE" />
        <action name="core.edit" title="JACTION_EDIT" />
    </section>
</access>
```

## config.xml

Questo file viene utilizzato per controllare se alcune opzioni appaiono nel modulo *Opzioni* del componente e sotto quale scheda compaiono. Per com_countrybase non ci sono opzioni diverse da quelle delle autorizzazioni standard di Joomla. Sarebbe possibile aggiungere opzioni qui, ad esempio, per mostrare o nascondere una colonna particolare nella visualizzazione dell'output. Questo andrebbe in un fieldset separato chiamato Opzioni.

```xml
<?xml version="1.0" encoding="utf-8"?>
<config>

    <fieldset
        name="permissions"
        label="JCONFIG_PERMISSIONS_LABEL"
        description="JCONFIG_PERMISSIONS_DESC"
        >

        <field
            name="rules"
            type="rules"
            label="JCONFIG_PERMISSIONS_LABEL"
            filter="rules"
            validate="rules"
            component="com_countrybase"
            section="component"
         />
    </fieldset>
</config>
```

*Tradotto da openai.com*

