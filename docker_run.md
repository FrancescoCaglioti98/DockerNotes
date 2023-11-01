# Docker Run Commands

## TAG

I tag sono delle informazioni aggiuntive per le immagini, che vanno a specificare la versione, la distribuzione oppure aspetti di questa immagine
redis:4.0 => TAG = 4.0 ( forzatamente recupera la versione 4.0 )
httpd:alpine => TAG = alpine ( recupera l'istanza di httpd utilizzata su alpine )

Se non viene specificata alcuna tag docker di default utilizzerà la tag "latest" ( quindi andrà a prendere l'ultima versione )

Questo opzione per adesso viene utilizzata con [[docker_commands#^5c6838]] oppure con [[docker_commands#^07aea8]]


## -i
Sta ad indicare Interactive mode

## -t
flag per il terminale


## Port Mapping ( -p )

Al lancio di un un container è possibile specificare su quale porta deve restare in ascolto e su quale porta si deve interfacciare con il docker host

```docker run -p 8000:80 --name WebApp nginx```

-p sta ad indicare che si sta decidendo di mappare la porta
8000 è la porta del docker host da cui è accessibile il container
80 è la porta del container in ascolto che viene mappata sulla porta 8000



## Folder mapping ( -v )

Quando vengono fatte modifiche ad un container i file restano salvati al suo interno. Questo vuol dire che nel momento stesso in cui questo container viene cancellato ( docker rm CONTAINER ) tutto il suo contenuto viene perso, senza possibilità di recuperarlo
Per questo esiste la possibilità di mappare delle cartelle del docker host al docker container

```docker run -p 8000:80 -v /var/www/CalypsoDev:/var/www/CalypsoClienti --name WebApp nginx```

In questo modo i file non vengo persi, perché fanno sostanzialmente parte del docker host anche se virtualmente vengono utilizzati dal container



## Docker inspect

Questo comando viene utilizzato per ottenere maggiori informazioni su di un container, molte di più di quante potremmo averne con un semplice docker ps
```docker inspect WebApp```


## Docker Logs

viene utilizzato per stampare a terminale tutti i log di un container che viene lanciato in Detach mode