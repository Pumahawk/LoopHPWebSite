---
layout: wiki
previus_doc: /docs/Routing.html
next_doc:
---
# Gestione dei file di configurazione

Con LoopHP e' molto facile gestire i file di configurazione.

Questa funzionalita' e' stata realizzata utilizzando il componente 
[The Routing Component](https://symfony.com/doc/current/components/routing.html) di Symfony.

Una volta configurata l'applicazione e' possibile accedere
ai file di configurazione direttamente dal controllore.

Settiamo correttamente il percorso ai file di configurazione.

```php
$app = new AppConfiguration();
$app -> addConfigurationPath(__DIR__.'path/to/config/dir');
```

All'interno di un metodo di un controllore e' possibile utilizzare il metodo
`BaseController::config` per ottenere il `Loader` in grado di leggere i file di configurazione.

```php
$config = $this -> config() -> load('path/to/config/file');
```

Il loader di default e' in grado di leggere automaticamente i file di configurazione
con le seguenti estensioni.

* .yaml  
* .php
* .route.yaml
* .route.php

E' possibile creare dei Loader aggiuntivi e aggiungerli alla applicazione.

## Creare dei loader personalizzati

Per imparare a creare dei Loader consiglio di leggere la documentazione
sul componente [The Routing Component](https://symfony.com/doc/current/components/routing.html) di Symfony.

Tramite il metodo `App::getConfigLoader` si ottiene l'oggetto [LoaderResolver](https://api.symfony.com/3.1/Symfony/Component/Config/Loader/LoaderResolver.html)
al quale e' possibile aggiungere dei Loader personalizzati tramite il metodo 
`LoaderResolver::addLoader`.

Per creare un loader bisogna implementare l'interfaccia [LoaderInterface](https://api.symfony.com/3.1/Symfony/Component/Config/Loader/LoaderInterface.html).

Dopo aver creato il loader personalizzato si deve aggiungere all'applicazione direttamente
dal metodo `App::addConfigLoader`

```php
$app -> addConfigLoader(new PersonalLoader());
```