---
layout: wiki
previus_doc: /docs/Template.html
next_doc: /docs/Gestione file di configurazione.html
---
# Configurazione Routing

Il __Routing__ e' molto utilizzato nelle applicazioni web e permette di configurare
le richieste per richiamare automaticamente i controller passando dati aggiuntivi.

Ci sono diversi modi per configurare i __Route__ dell'applicazione:

* Codice PHP
* File di configurazione in PHP
* File di configurazione in YAML

Per la realizzazione di questa funzionalita' e' stato utilizzato [The Routing Component](https://symfony.com/doc/current/components/routing.html)
di __Symfony__.

Per utilizzare questo tipo di configurazione con __LoopHP__ si puo' utilizzare 
la classe [UrlMatcher](https://github.com/Pumahawk/LoopHP/blob/master/src/Matchable/UrlMatcher.php).

``UrlMatcher`` richiede un [RouteCollection](https://api.symfony.com/2.3/Symfony/Component/Routing/RouteCollection.html) di Symfony, quindi possiamo crearne uno seguendo il metodo fornito dalla documentazione
di Symfony oppure possiamo utilizzare [RouteGroup](https://github.com/Pumahawk/LoopHP/blob/master/src/Routing/RouteGroup.php) di
LoopHP molto piu' facile da utilizzare con LoopHP.

## Codice PHP

E' il metodo piu' veloce e non richiede il supporto di file aggiuntivi ma non e'
il piu' indicato per applicazioni di grandi dimensioni.

Come prima cosa creiamo un `RouteGroup` a cui passeremo i [Route](https://github.com/Pumahawk/LoopHP/blob/master/src/Routing/Route.php) di LoopHP.

```php
$routeGroup = new RouteGroup();
$routeToHome = new Route('home', '/home', new ControllerData('C\\Controller', 'home'));
$routeGroup -> add($routeToHome);

# RouteGroup::getRouteCollection converte l'oggetto in un RouteCollection
# RequestContext e' una classe di Symfony
$matcher = new UrlMatcher($routeGroup -> getRouteCollection(), new RequestContext('/'));
```

## File di configurazione in PHP

E' possibile creare un file di configurazione che venga processato in automatico
dall'applicazione.

```php
return [
  'router' => [
    [
      'name' => 'group',
      'pattern' => '/pathgroup',
      'address' => [
        [
          'name' => 'route',
          'pattern' => '/path',
          'data' => [
            'controller' => 'controller@action'
          ]
        ]
      ]
    ]
  ]
];
```

Per utilizzare questo file di configurazione bisogna settare il path della cartella
contenente i file di configurazione.

E' importante che il file abbia estensione .route.php cosi' che l'applicazione
possa convertire il contenuto automaticamente in un __RouteCollection__.

```php
$appConfiguration = new AppConfiguration();
$appConfiguration
  -> addConfigurationPath('path/to/config/dir');
$app = new App($appConfiguration);
```

Bisogna istanziare il matcher e passarlo all'applicazione.

```php
$this -> app -> setMatch(new UrlMatcher($this -> app -> loader() -> import('path/to/config/file.route.php'), new RequestContext('/')));

```

## File di configurazione in YAML

E' possibile creare un file di configurazione scritto in YAML che venga processato in automatico
dall'applicazione.

```yaml
router:
  - name: group
    pattern: /pathgroup
    address:
      - name: route
        pattern: /path
        data:
          controller: controller@action

```

Per utilizzare questo file di configurazione bisogna settare il path della cartella
contenente i file di configurazione.

E' importante che il file abbia estensione .route.yaml cosi' che l'applicazione
possa convertire il contenuto automaticamente in un __RouteCollection__.

```php
$appConfiguration = new AppConfiguration();
$appConfiguration
  -> addConfigurationPath('path/to/config/dir');
$app = new App($appConfiguration);
```

Bisogna istanziare il matcher e passarlo all'applicazione.

```php
$this -> app -> setMatch(new UrlMatcher($this -> app -> loader() -> import('path/to/config/file.route.yaml'), new RequestContext('/')));

```