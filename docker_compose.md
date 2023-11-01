## Utilizzo con Docker Run

con docker compose possiamo creare delle applicazioni complesse che vanno ad utilizzare più container per poter funzionare
per poterlo utilizzare abbiamo bisogno di un file chiamato docker-compose.yml

Dopo averlo creato possiamo lanciarlo con docker-compose up
È più facile da gestire, in quanto tutte le modifiche vengono fatte all'interno di un unico file yml piuttosto che in una complicata riga di comando che si basa su di un unico Dockerfile/immagine

È possibile farlo solo sullo stesso docker host, quindi container che devono lavorare insieme e vengono dichiarati sullo stesso file yml DEVONO essere sullo stesso host
Questa regola non si applica su servizi che COMUNICANO tra di loro ma non sono necessariamente dipendenti

Nell'esempio viene portato un semplice sistema prima tramite un sacco di docker run e successivamente tramite un singolo docker-compose.yml
Da subito è chiaro che farlo tramite dei docker run è molto più dispendioso e ha come prerogativa che tutte le immagini siano già pronte e disponibili o nell'hub o nell'host
![[compless_application_docker_run.png]]

Come si vede dall'immagine per ogni singolo servizio è necessario creare una riga con tutte le sue opzioni

Ma in questo caso non funzionerà, perché non abbiamo detto ai singoli container che devono comunicare tra di loro, infatti è possibile che ci siano centinaia di container di redis che stanno girando sulla stessa macchina, quindi il nostro container ( vote ) non sa bene con quale dovrebbe comunicare

In questo caso si utilizza il comando --link
![[compless_application_docker_run_link.png]]Nell'immagine si vede che all'interno cerca di utilizzare l'host "redis", ma l'unico modo per potergli far sapere che quello è il suo host redis è utilizzare il comando --link dove la struttura è così definita:
- --link ( il comando link )
- redis: (il nome che avrà il container redis per il container vote )
- :redis ( l'effettivo nome del container redis da utilizzare )

Quello che fa non è altro che andare ad inserire un nuovo host nel file hosts del container in questione
![[compless_application_docker_run_hosts_file.png]]

È possibile inserire più volte per lo stesso comando la flag --link ( per esempio un servizio che si deve collegare sia ad un db postgres che ad un db mysql )

## Utilizzo con Docker Compose

Di contro un file docker-compose.yml è molto più semplice
![[docker_compose_links.png]]

le chiavi ( redis, db, vote...) sono i NOMI dei container che vengono assegnati mentre innestati dentro queste chiavi sono presenti tutte le altre opzioni
come le porte, i link, l'immagine da utilizzare

![[docker_compose_images.png]]

Nel caso di vote e di worker non possono essere utilizzate delle immagini di base perché sono custom, quindi viene specificata una folder da cui prendere il codice ( anche quello dell'applicazione ) e un Dockerfile che si occupa di creare questa immagine
Quindi al buil vengono recuperate i dockerfile presenti dentro le cartelle, viene creata l'immagine e dopo questa immagine viene utilizzata per creare i container



Esistono diverse versioni per i docker-compose.yml file, questo che abbiamo visto fino ad ora è per la versione 1


