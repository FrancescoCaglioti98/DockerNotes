# Immagini Docker

Per creare un'immagine di un servizio ( un'immagine di calypso ) bisogna prima di tutto capire gli step necessari alla sua creazione

i passaggi per la creazione sono:
- creare un file docker chiamato Dockerfile e mettere al suo interno le istruzioni da far eseguire per far partire correttamente il servizio, ([[Dockerfile]]) come ad esempio:
	- Installare le dependecies
	- da dove copiare il source code e dove metterlo
	- qual è l'entry point dell'applicazione
	- ecc
- Una volta fatto ciò possiamo fare il build dell'immagine utilizzando il comando:
	-  ```docker buil Dockerfile -t general/my-custom-app``` 

Questo andrà a creare un'immagine localmente, per andare a pubblicarla nell'hub di Docker bisogna invece lanciare il comando:
```docker push general/my-custom-app```


## Dockerfile

Il Dockerfile è un file di testo scritto in uno specifico formato che docker può capire
È formato da istruzioni e argomenti:

Prendendo d'esempio il [[Dockerfile]]: 
- Tutto ciò che sta sulla sinistra in maiuscolo è un istruzione ( FROM, RUN, COPY, ENTRYPOINT )
- Tutto il resto sono argomenti per queste istruzioni


Analizzando riga per riga:
- FROM Ubuntu => quale sistema operativo utilizzare come base ( docker image ) ( tutti i Dockerfile devono iniziare con questa riga)
- RUN apt-get update => comandi da eseguire su questa docker image di base richiamata nel punto precedente
- COPY . /opt/source-code => copia dei file dal docker host alla cartella specificata della docker image
- ENTRYPOINT .... => va ad indicare il comando che verrà lanciato non appena terminerà la creazione del container
- 