
# Variabili dell'ambiente

È possibile creare all'interno del proprio codice delle variabili ENV che successivamente possono essere popolate tramite il comando docker run
```docker run -e NOME_VARIABILE=VALORE_VARIABILE simple-webapp-color```

Quindi per lanciare diversi container che richiedono la stessa variabile, ma ogni volta deve essere modificata bisogna lanciare n volte il comando

Per recuperare le variabili da un container che sta già girando bisogna utilizzare il comando
```docker inspect CONTAINER_NAME``` che andrà a generare un JSON di informazioni per questo container
A questo punto alla chiave: CONFIG->ENV andremo a trovare le varibili
