---
layout: wiki
previus_doc: /docs/Configurazione oggetto App.html
next_doc: /docs/Template.html
---

# Creare un'applicazione

Nella creazione di un'applicazione possiamo decidere l'organizzazione dei 
file. E' possibile che a seconda delle limitazioni imposte dalla piattaforma che
stiamo utilizzando non sia possibile utilizzare sempre lo stesso schema per 
tutte le nostre applicazioni. Questo puo' capitare soprattutto in applicazioni
gia' iniziate alle quali dobbiamo apportare delle modifiche.

In questa guida immaginiamo di realizzare un'applicazione web per la visualizzazione
di un sito internet, prendendo spunto dal file di test ``test/App/Exemple/SimpleApplicationTest.php``.

A differenza della guida sulla [Configurazione dell'oggetto App](Configurazione-oggetto-App) mostriamo anche come 
l'organizzazione del controller e del template.

Possiamo immaginare di voler strutturare la nostra applicazione in questo modo,
dove _index.php_ e' la home del sito che stiamo creando.

```
/
├── index.php
└── src
    ├── api
    │   └── controller
    │       └── Controller.php
    └── template
        └── home.php

```

Una volta decisa la struttura della nostra applicazione non resta che scaricare le librerie
utilizzando composer.

Spostiamoci dentro la cartella src

`` cd src ``

Creiamo il file __composer.json__ e aggiungiamo il seguente contenuto.

```json
{
  "repositories": [
      {
          "type": "vcs",
          "url": "https://github.com/Pumahawk/LoopHP.git"
      }
  ],
    "require": {
      "Pumahawk/LoopHP": "dev-master"
    }
}

```

__Attenzione!! Durante la scrittura di questa wiki LoopHP non e' ancora presente
su [Packagist](https://packagist.org/).__

Avviamo composer e scarichiamo le librerie.

`` composer install ``

Adesso la struttura delle cartelle dovrebbe essere simile alla seguente struttura:

```
/
├── index.php
└── src
    ├── api
    │   └── controller
    │       └── Controller.php
    ├── composer.json
    ├── template
    │   └── home.php
    └── vendor
        └── autoload.php

```

Rimangono soltanto da modificare i seguenti file:

* _index.php_
* _src/template/home.php_
* _src/api/controller/Controller.php_

__src/template/home.php__

```html

<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Ciao mondo!</title>
  </head>
  <body>
    Ciao mondo!
  </body>
</html>

```

__src/api/controller/Controller.php__

```php
namespace C;

use LoopHP\Controller\BaseController;

class Controller extends BaseController {
  public function home(){
    echo $this -> tEngine() -> render('home.php');
  }
}

```
__index.php__

```php

require __DIR__.'/src/vendor/autoload.php';

use LoopHP\App;
use LoopHP\AppConfiguration;
use LoopHP\Matchable\StaticMatch;
use LoopHP\ControllerData;

$srcDir = __DIR__.'/src';

$appConfig = new AppConfiguration();
    $appConfig 
      -> setTemplate($srcDir.'/template')
      -> addApi('C\\', $srcDir.'/api/controller')
      -> setComposer(require(__DIR__.'/src/vendor/autoload.php'));

$controllerData = new ControllerData('C\\Controller', 'home');
$matcher = new StaticMatch($controllerData);

$app = new App($appConfig, $matcher);
$app -> setApiLoader();

$app -> start();

```

Nel file _index.php_ e' stato utilizzato ``StaticMatch`` perche' non richiede particolari
configurazioni del server.