<!-- Filename: J4.x:Dependency_Injection_in_Joomla_4 / Display title: Iniezione delle dipendenze -->

## Introduzione

L'iniezione delle dipendenze (DI) è una tecnica di sviluppo software che fornisce a una classe le sue dipendenze dall'esterno, anziché crearle internamente. Migliora la flessibilità, la manutenibilità e la testabilità del codice. Tuttavia, è difficile da comprendere!

C'è una spiegazione di DI e dei contenitori per l'iniezione delle dipendenze nella documentazione di [Joomla Framework DI](https://github.com/joomla-framework/di/blob/4.x-dev/docs/why-dependency-injection.md). C'è anche una [Panoramica](https://github.com/joomla-framework/di/blob/4.x-dev/docs/overview.md) del suo utilizzo.

Le spiegazioni nella sezione [Iniezione di Dipendenze](jdocmanual?article=docus/dependency-injection/index) della Documentazione per Programmatori di Joomla! non sono così facili da comprendere!

## Esempi

Se il tuo obiettivo è iniziare a costruire un'estensione, i seguenti esempi presi dalle estensioni core di Joomla potrebbero aiutarti.

Il codice per l'iniezione delle dipendenze si trova in services/provider.php, ma l'esatta posizione di quel file dipende dal tipo di estensione.

### Esempio di componente

Il percorso completo del file services/provider.php è administrator/components/com_example/services/provider.php. Questo esempio è com_tags, che non utilizza categorie. Se il tuo componente utilizza categorie, dai un'occhiata al codice services/provider.php per com_content. Avrai bisogno di diverse dichiarazioni relative alle Categorie.

```php
<?php

/**
 * @package     Joomla.Administrator
 * @subpackage  com_tags
 *
 * @copyright   (C) 2018 Open Source Matters, Inc. <https://www.joomla.org>
 * @license     GNU General Public License version 2 or later; see LICENSE.txt
 */

\defined('_JEXEC') or die;

use Joomla\CMS\Component\Router\RouterFactoryInterface;
use Joomla\CMS\Dispatcher\ComponentDispatcherFactoryInterface;
use Joomla\CMS\Extension\ComponentInterface;
use Joomla\CMS\Extension\Service\Provider\ComponentDispatcherFactory;
use Joomla\CMS\Extension\Service\Provider\MVCFactory;
use Joomla\CMS\Extension\Service\Provider\RouterFactory;
use Joomla\CMS\MVC\Factory\MVCFactoryInterface;
use Joomla\Component\Tags\Administrator\Extension\TagsComponent;
use Joomla\DI\Container;
use Joomla\DI\ServiceProviderInterface;

/**
 * The tags service provider.
 *
 * @since  4.0.0
 */
return new class () implements ServiceProviderInterface {
    /**
     * Registers the service provider with a DI container.
     *
     * @param   Container  $container  The DI container.
     *
     * @return  void
     *
     * @since   4.0.0
     */
    public function register(Container $container)
    {
        $container->registerServiceProvider(new MVCFactory('\\Joomla\\Component\\Tags'));
        $container->registerServiceProvider(new ComponentDispatcherFactory('\\Joomla\\Component\\Tags'));
        $container->registerServiceProvider(new RouterFactory('\\Joomla\\Component\\Tags'));
        $container->set(
            ComponentInterface::class,
            function (Container $container) {
                $component = new TagsComponent($container->get(ComponentDispatcherFactoryInterface::class));
                $component->setMVCFactory($container->get(MVCFactoryInterface::class));
                $component->setRouterFactory($container->get(RouterFactoryInterface::class));

                return $component;
            }
        );
    }
};
```

### Esempio di Modulo

Questo è il modulo Versione che mostra la versione di Joomla nella barra del titolo delle pagine dell'Amministratore. Il codice si trova in administrator/modules/mod_version/services/provider.php

```php
<?php

/**
 * @package     Joomla.Administrator
 * @subpackage  mod_version
 *
 * @copyright   (C) 2024 Open Source Matters, Inc. <https://www.joomla.org>
 * @license     GNU General Public License version 2 or later; see LICENSE.txt
 */

\defined('_JEXEC') or die;

use Joomla\CMS\Extension\Service\Provider\HelperFactory;
use Joomla\CMS\Extension\Service\Provider\Module;
use Joomla\CMS\Extension\Service\Provider\ModuleDispatcherFactory;
use Joomla\DI\Container;
use Joomla\DI\ServiceProviderInterface;

return new class () implements ServiceProviderInterface {
    /**
     * Registers the service provider with a DI container.
     *
     * @param   Container  $container  The DI container.
     *
     * @return  void
     *
     * @since   5.1.0
     */
    public function register(Container $container)
    {
        $container->registerServiceProvider(new ModuleDispatcherFactory('\\Joomla\\Module\\Version'));
        $container->registerServiceProvider(new HelperFactory('\\Joomla\\Module\\Version\\Administrator\\Helper'));

        $container->registerServiceProvider(new Module());
    }
};
```

### Esempio di Plugin

Questo è il plugin che fornisce informazioni di contatto nelle pagine di contenuto. Il codice si trova in plugins/content/contact/services/provider.php

```php
<?php

/**
 * @package     Joomla.Plugin
 * @subpackage  Content.contact
 *
 * @copyright   (C) 2022 Open Source Matters, Inc. <https://www.joomla.org>
 * @license     GNU General Public License version 2 or later; see LICENSE.txt
 */

\defined('_JEXEC') or die;

use Joomla\CMS\Extension\PluginInterface;
use Joomla\CMS\Factory;
use Joomla\CMS\Plugin\PluginHelper;
use Joomla\Database\DatabaseInterface;
use Joomla\DI\Container;
use Joomla\DI\ServiceProviderInterface;
use Joomla\Event\DispatcherInterface;
use Joomla\Plugin\Content\Contact\Extension\Contact;

return new class () implements ServiceProviderInterface {
    /**
     * Registers the service provider with a DI container.
     *
     * @param   Container  $container  The DI container.
     *
     * @return  void
     *
     * @since   4.3.0
     */
    public function register(Container $container)
    {
        $container->set(
            PluginInterface::class,
            function (Container $container) {
                $plugin     = new Contact(
                    $container->get(DispatcherInterface::class),
                    (array) PluginHelper::getPlugin('content', 'contact')
                );
                $plugin->setApplication(Factory::getApplication());
                $plugin->setDatabase($container->get(DatabaseInterface::class));

                return $plugin;
            }
        );
    }
};
```

*Tradotto da openai.com*

