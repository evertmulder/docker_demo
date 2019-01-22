# Container workshop

In de workshop willen we handson met docker containers gaan verschillende aspecten van containers te belichten:
* Installatie Docker (PreRequisite)
  * Docker 4 desktop https://download.docker.com/win/stable/Docker%20for%20Windows%20Installer.exe of
  * Docker Machine
* Gebruiken van software (specifieke versie) zonder dit te installeren 
* Runnen van een container met een sample app
* Basic debuggen in container
* Container orchestratie met docker compose

## Installeer docker
Installeer docker vanaf de website.

To check that you have the latest release installed.
```
docker version
```
Verify that Docker is pulling images and running as expected.
```
docker run hello-world
```

## Software draaien
``` 
-i = Interactive
-t = terminal output
-d = draai als deamon (achtergrond proces)

docker run -i -t -d [container:tag] [commando] <commande argument>
```

Voer het volgende commando uit
```
docker run -i -t -d alpine
```

Overzichtje basic docker commando's.
```
#list running containers
docker ps 

#list running and stopped containers
docker ps -a

#verwijder een container
docker rm [naam/id]

#verwijder gestopted containers
docker container prune

#list de locale beschikbare images
docker images
```

## Zelf een container bouwen

Met het commando docker build en een Dockerfile kunnen we een nieuw docker container bouwen. We gebruiken hier een zo minimale base image 'alpine linux' voor.

```
cd my_alpine
docker build . -t my_alpine
```

We hebben nu een image gebuild deze een naam en een tag gegeven.
Het image hebben we nu beschilbaar. Controleer dit door het volgende commando uit te voeren:
```
docker images
```

Run de container
```
docker run -d my_alpine
```

Controleer of de container nog draait.
```
docker ps

en 

docker ps -a
```

Wat valt op?

Bekijk de Dockerfile en vervang het 1e CMD commando door de 2e die nu in commentaar staat. 

Run de container
```
docker run -d my_alpine
```

Controleer of de container nog draait.
```
docker ps
```

Wat valt op?

## Basic debugging
Oke container draait, maar hoe kan ik zien wat er zich afspeeld in de container.

Om de STDOUT te zien (de console output van het docker proces)
```
docker logs -f [container naam of id]
```

Het is ook mogelijk om in een draaiende container een shell te starten (voor de meeste images gebaseerd op een full OS)
```
docker exec -it [container naam of id] sh
apk add htop
htop
apk add mc
mc
```

## Docker compose
Met docker compose kunnen we meerder containers tegelijk starten. Bijvoorbeeld een website en daarbij een database

Installeer docker compose (https://docs.docker.com/compose/install/)

```
cd my_wordpress

# start webserver en database
docker-compose -d up
```


```
docker-compose -f docker-compose_2web.yml up -d
```
