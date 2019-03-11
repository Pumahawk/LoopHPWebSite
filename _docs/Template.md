---
layout: wiki
previus_doc: /docs/Creare un applicazione.html
next_doc: /docs/Routing.html
---
# Creazione e gestione Template

I template sono fondamentali per cambiare la logica di programmazione dall'interfaccia
grafica. Soprattutto nelle applicazioni web risulta essere molto utile scrivere 
codice HTML in file separati.

Con LoopHP e' possibile specificare la cartella contenente i file che dovranno funzionare
da template.

Il template non e' soltanto un testo scritto in html ma molto di piu'. Per ogni
tipo di template c'e' bisogno di TemplateEngine in grado di elaborarlo e restituire 
un output.

Il template engine utilizzato in LoopHP e' PHPEngine di Symfony ed e' possibile 
leggere la [documentazione ufficiale](https://symfony.com/doc/current/components/templating.html).

E' possibile aggiungere altri template engine con il metodo `` App::addTemplateEngine ``,
e' importante che tutti i template engine aggiunti implementino l'interfaccia
[EngineInterface](https://github.com/symfony/templating/blob/master/EngineInterface.php).

## Usare i template

Non bisogna dimenticarsi di configurare correttamente l'applicazione per permettere
l'accesso ai template usando il metodo `` AppConfiguration::setTemplate ``.

```php
# Impostare il percorso del template nella configurazione dell'applicazione
$appConfiguration -> setTemplate('path/to/template/folder');
```

Dopo aver istanziato l'applicazione possiamo aggiungere altri template engine.

```php
# $templateEngine implementa EngineInterface
$app -> addTemplateEngine($newTemplateEngine);
```

E' possibile utilizzare il template engine all'interno del controllore

```php
$this -> tEngine() -> render('template.php', $extraData);
```

## Creare i template

Per una guida approfondita consiglio di leggere l'articolo [How to Use PHP instead of Twig for Templates](https://symfony.com/doc/current/templating/PHP.html).

La comodita' nell'utilizzare un template in php sta nell'utilizzare un linguaggio
di cui abbiamo gia' dimestichezza. Possiamo utilizzare l'html e rendere la pagina dinamica
con php.

Esistono anche delle funzionalita' aggiuntive come la possibilita' di estendere 
altri template ed e' tutto descritto nell'articolo riportato sopra.

Una funzionalita' molto utile e semplice e' il passaggio di informazioni dal controller.

Nel momento in cui su usa ``EngineInterface::render`` si puo' passare un array
e le variabili al suo interno possono essere riutilizzare.

Per saperne di piu' e' possibile leggere la documentazione sull'articolo [The Templating Component](https://symfony.com/doc/current/components/templating.html)
