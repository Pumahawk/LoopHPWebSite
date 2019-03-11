---
layout: wiki
previus_doc: /docs/Organizzazione del codice sorgente.html
next_doc: /docs/Creare un applicazione.html
---

# Configurazione oggetto App

La classe App e' l'elemento principale di LoopHP e va istanziato correttamente.

LoopHP permette di interfacciarsi con librerie create dall'utente, file di configurazione
e template, tutti in cartelle diverse. Per permette questo bisogna creare un oggetto 
di tipo **App** passandogli un altro oggetto importante di configurazione di tipo
**AppConfiguration** che permette di configurare in maniera semplice l'**App**.

Per fare un esempio di come si puo' instanziare una classe App e' utile vedere
una parte di codice nel file ``test/App/Exemple/SimpleApplicationTest.php``.

Il metodo ``testConfigurationApp`` crea un oggetto di tipo App configurandolo in una
maniera particolare.

Nella prima parte del metodo vediamo che viene creato un oggetto di tipo **AppConfiguration**
al quale vengono passati i percorsi utili per i test di questa classe.

```php
$appConfig = new AppConfiguration();
    $appConfig 
      -> setTemplate($baseDataTestPath.'/template')
      -> addApi('C\\', $baseDataTestPath.'/controller')
      -> setComposer(require(__DIR__.'/../../../vendor/autoload.php'));
```

In questo esempio viene esclusa la gestione dei file di configurazione ma soltanto
la creazione dei __Template__, la creazione di un __Controller__.

Bisogna notare il passaggio del percorso dell'autoload di composer, passaggio 
obbligatorio per la configurazione dell'oggetto.

Il passaggio successivo e' la creazione dell'__UrlMatcher__. Oggetto utile a LoopHP
per capire in base al contesto quale metodo del controllore lanciare. UrlMatcher non
e' l'unico Matcher disponibile e usiamo questo soltanto perche' in questo momento
e' utile per spiegare il funzionamento di LoopHP.

```php
$routeGroup = new RouteGroup();
    $routeGroup -> add(new Route('home', '/home', new ControllerData('C\\Controller', 'home')));
    $routeGroup -> add(new Route('homeTemplate', '/homeTemplate', new ControllerData('C\\Controller', 'homeTemplate')));
    $routeGroup -> add(new Route('productTemplate', '/productTemplate', new ControllerData('C\\Controller', 'productTemplate')));
    $routeGroup -> add(new Route('dinamicOutput', '/key/{number}', new ControllerData('C\\Controller', 'dinamicOutput'), 
    [
      'number' => '[0-9]+'
    ]));
    
    $matcher = new UrlMatcher($routeGroup -> getRouteCollection(), new RequestContext('/'));
```

Questo non e' il metodo piu' semplice per la creazione dell'applicazione ma e'
ricco di funzionalita'.

E' utile per imparare avere una visione globale della classe Controller presente nel file
`` resources/test/exemple/simple_application/controller/Controller.php `` .

```php

namespace C;
use LoopHP\Controller\BaseController;
class Controller extends BaseController {
  public function home(){...}
  public function homeTemplate() {...}
  public function productTemplate() {...}
  public function dinamicOutput() {...}
}

```

Da notare i riferimenti ai file passati durante la creazione dell'oggetto di configurazione
e dei riferimenti alla classe e ai metodi durante la configurazione del router.

L'ultimo passaggio per la creazione dell'oggetto App e' istanziarlo e inizializzarlo.

```php

  $app = new App($appConfig, $matcher);
  $app -> setApiLoader();
  
```

Al costruttore viene passato l'oggetto di configurazione e il matcher, ma un 
metodo fondamentale e' il richiamo al metodo `` setApiLoader `` che richiamando 
__Composer__ aggiunge le api personalizzate al suo autoload.

Questo ultimo passaggio e' fondamentale e spesso dimenticarlo e' la causa di 
numerosi problemi in esecuzione.