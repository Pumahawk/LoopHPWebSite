---
layout: wiki
title: Come contribuire alla libreria LoopHP
previus_doc: /docs/Home.html
next_doc: /docs/Organizzazione del codice sorgente.html
---
# Come contribuire alla libreria LoopHP

E' possibile contribuire alla creazione di LoopHP utilizzando le funzionalita'
di github.

Gli Issues e i Pull request creati verranno presi in considerazione.

## Contribuire a LoopHP

Se non si e' pratici all'utilizzo di Git, della piattaforma Github e di Composer
spieghero' brevemente come scaricare il codice sorgente e installare le dipendenze.

### Software necessari

* Git  
  Applicazione necessaria per potersi sincronizzare con il codice sorgente.  
  E' possibile scaricarlo dal sito ufficiale: [git-scm.com](https://git-scm.com/).
* Composer  
  Applicazione necessaria per risolvere le dipendenze di LoopHP con altre librerie
  in php.  
  E' possibile scaricarlo dal sito ufficiale: [getcomposer.org](https://getcomposer.org/).

### Scaricare il codice sorgente e installare le dipendenze

Scaricare il codice sorgente utilizzando Git.

`` git clone https://github.com/Pumahawk/LoopHP.git ``

Spostarsi all'interno della cartella principale

`` cd LoopHP ``

Installare le dipendence con composer 

`` composer install ``

### Note

Dopo aver modificato il codice sorgente accertarsi che i test non restituiscano 
errori utilizzando PhpUnit con il seguente comando:

`` ./vendor/bin/phpunit ``

Consiglio di utilizzare un editor di testo semplice come i seguenti:
* [Atom](https://atom.io/)
* [Notepad++](https://notepad-plus-plus.org/)


