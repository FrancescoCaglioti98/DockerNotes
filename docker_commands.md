# Docker Commands

1. Docker Run (```docker run nginx```) ^5c6838
	1. viene utilizzato per lanciare un container da un'immagine
	2. Se questa immagine non è presente all'interno dell'host viene recuperata automaticamente dall'HUB, ma viene fatto solo la prima volta
2. Docker ps (```docker ps```) ^aed670
	1. crea una lista di tutti gli attuali container in esecuzione
	2. Inserisce alcune ulteriori informazioni sui container
		1. CONTAINER ID
		2. IMAGE
		3. COMMAND
		4. CREATED
		5. STATUS
		6. PORT
		7. NAME
	3. Utilizzando ```docker ps -a``` vengono mostrati anche tutti i container che sono stati precedentemente stoppati ma non ancora cancellati o rimossi
3. Docker Stop (```docker stop CONTAINER_NAME```)
	1. Comando utilizzato per fermare un container in particolare
	2. Per utilizzarlo è necessario fornire il nome del container
	3. al successo dell'operazione verrà mostrato il nome del container
4. Docker rm (```docker rm CONTAINER_NAME```)
	1. Viene utilizzato per rimuovere completamente un container ( permanentemente )
	2. Al successo verrà mostrato il nome del container
5. Docker images ( ```docker images```)
	1. comando per far visualizzare una lista delle immagini presenti nel nostro host
	2. le informazioni vengono accompagnate dalla dimensione, dai tag, dalla data di creazione ...
6. docker rmi (```docker rmi```)
	1. comando per cancellare completamente un'immagine dall'host
	2. !!! ASSICURARSI CHE NESSUN CONTAINER UTILIZZI L'IMMAGINE !!!
7. docker pull image_name ( ```docker pull IMAGE_NAME```) ^07aea8
	1. comando per scaricare un'immagine da docker
	2. a differenza del run questo non lancia automaticamente un container ma va solo a scaricare un immagine da utilizzare successivamente
8. docker exec CONTAINER NAME COMANDO_DA_ESEGUIRE ( ```docker exec test apt update```)
	1. serve per eseguire un comando all'interno di un qualsiasi container
9. docker run -d nome_container
	1. lancia il container in modalità DETACH quindi lasciando la console libera
10. docker attach ID_CONTAINER
	1. server per fare l'attach del container alla console
