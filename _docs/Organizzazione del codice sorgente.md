---
layout: wiki
next_doc: /docs/Configurazione oggetto App.html
previus_doc: /docs/Contribuire alla libreria.html
---
# Organizzazione del codice sorgente

Il contenuto della repository si divide in 3 cartelle:
* __src__
* __test__
* __resources__

## src

Contiene il cuore del codice sorgente. In questa cartella sono contenute le classi
principali di LoopHP come:

* [App](https://github.com/Pumahawk/LoopHP/blob/master/src/App.php)
* [AppConfiguration](https://github.com/Pumahawk/LoopHP/blob/master/src/AppConfiguration.php)
* [ControllerData](https://github.com/Pumahawk/LoopHP/blob/master/src/ControllerData.php)
* [Matchable](https://github.com/Pumahawk/LoopHP/blob/master/src/Matchable.php)

Queste classi sono le principali di LoopHP ma da sole non bastano alla realizzazione
di una applicazione.

Per facilitare la creazione e la configurazione di una applicazione sono state 
create componenti aggiuntive che possono aiutare il programmatore nella realizzazione
di applicazioni comuni come applicazioni web o semplici pagine statiche.

Non e' obbligatorio conoscere tutti i componenti per poter lavorare con LoopHP
ma e' fortemente consigliato informarsi sul loro funzionamento.

I componenti messi a disposizione dello sviluppatore sono:

* __Config__  
  Componente che aiuta nell'accesso e organizzazione dei file di configurazione
  di una applicazione.
* __Controller__  
  Componente che facilita la creazione di controller per una applicazione.
* __Matchable__  
  Componente che mette a disposizione delle implementazioni utili dell'interfaccia
  Matchable.
* __Routing__  
  Componente che facilita la creazione dei RouterCollection di Synfony che si interfacciano
  facilmente con LoopHP.

## test

Cartella contenente i test delle varie classi. Sono presenti le cartella __App__
e __Code__. 

La cartella __App__ contiene semplici esempi sulla creazione di una applicazione mentre 
la cartella __Code__ contiene test sul codice sorgente.

## resources

Contiene file e configurazioni utili per lo sviluppo della libreria. Al momento 
contiene soltanto la cartella test con all'interno file di configurazioni utilizzati dai test.