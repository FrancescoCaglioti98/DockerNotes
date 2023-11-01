I container non sono creati per funzionare continuamente, vengono utilizzati maggiormente per piccole task
Se il programma che sta funzionando al suo interno finisce la task, oppure va in crash il container si ferma e lo vediamo nella lista dei container fermi ( ```docker run -a```)

Chi definisce quali programmi vivono all'interno di un container?

Se andiamo a vedere un Dockerfile di un container nginx vediamo alla fine questa riga:
CMD ["nginx"], questo definisce il programma o il comando da eseguire all'interno del container

Per un container mysql sarà CMD["mysqld"]

Se provassimo a lanciare un container di una semplice ubuntu image vedremo che il comando da eseguire sarà "bash", ma non è un vero programma, è la shell che aspetta delle istruzioni e necessità di un terminale, se non trova il terminale smette di funzionare ed chiude il programma
Chiudendo il programma termina anche il funzionamento del container e quindi viene chiuso

Un modo per fare un override di questo comando di default è ```docker run ubuntu [COMANDO DA ESEGUIRE]```

Per rendere questo comando permanente bisogna andare a modificare il Dockerfile o a creare uno nuovo con la precedente immagine come base. Bisogna quindi andare ad aggiungere una nuova riga in questi due formati:
- o in questo modo => CMD command param1
- oppure in questo => CMD ["command", "param1"]

Se volessimo cambiare il param 1 dopo aver creato la nuova image dovremmo:

andare ad aggiungere il nuovo comando alla chiamata del docker run, ma non avrebbe senso perché vorrebbe andare a dire tornare alla situazione originale.

In questo caso entra in gioco l'ENTRYPOINT, questo ci permette di precisare SOLO il param1 alla chiamata del docker run

Quindi nel caso di CMD il comando che inseriamo al termine del docker run va a sostituire completamente la riga CMD
Nel caso di un ENTRYPOINT il comando che inseriamo va ad APPENDERSI alla riga già presente

Per inserire invece un valore di default, nel caso non venga passato dalla chiamata bisogna:
ENTRYPOINT ["command"]
CMD ["paramDefault"]

Quindi se nella chiamata non specifichiamo nulla verrà utilizzato il paramDefault, altrimenti qualunque cosa abbiamo inserito

Se invece volessimo fare un override anche dell'entrypoint dovremmo utilizzare un comando simile a:
```docker run --entrypoint [COMMAND] image [PARAM]```

in questo modo l'entrypoint viene sovrascritto con [COMMAND] e gli viene aggiunto [PARAM]