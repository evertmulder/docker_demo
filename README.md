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

Voer het volgende commando uit. Dit start een container met de naam alpine. Alpine is een minimale linux distributie en wordt vaak gebruikt als basis voor andere containers.

```
docker run -i -t alpine
```

Overzichtje basic docker commando's.
```
#list running containers
docker ps 

#list running and stopped containers
docker ps -a

#verwijder een container
docker rm [naam/id]

#verwijder gestopted containers van disk (house keeping)
docker container prune

#list de locale beschikbare images
docker images
```

## Zelf een container bouwen

Met het commando docker build en een Dockerfile kunnen we een nieuw docker container bouwen. We gebruiken hier een zo minimale base image 'alpine linux' voor.

```
cd my_alpine

# Bekijk de inhoud van een Docerfile
cat Dockerfile

# Kun je zien wat de container gaat doen?

docker build . -t my_alpine
```

We hebben nu een image gebuild deze een naam gegeven door de -t toevoeging.
Het image hebben we nu beschilbaar. Controleer dit door het volgende commando uit te voeren:
```
docker images
```

Run de container
```
# de -d betekend, uitvoeren als achtergrond proces

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
docker run -d --name my_container my_alpine
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

Het is ook mogelijk om in een draaiende container een shell te starten
```
# voer het programma 'sh' uit binnen de container. SH is een terminal of command prompt.
docker exec -it [container naam of id] sh

# met apk kunnen extra packages geinstalleerd worden binnen alpine. Het volgende installeerd het programma htop
apk add htop

# htop is een linux applicatie die het memory en cpu verbruik kan weergeven en alle lopende processen binnen een container
htop



# Installeer nu mc, (midnight commander) een file explorer onder linux
apk add mc

# We hebben nu binnen de container en file explorer beschikbaar
mc
```

## Docker compose
Met docker compose kunnen we meerder containers tegelijk starten. Bijvoorbeeld een website en daarbij een database

Installeer docker compose (https://docs.docker.com/compose/install/)

```
cd my_wordpress

# start webserver en database
docker-compose up -d
```

Open de wordpress site http://localhost:8000


stop de stack
```
docker-compose stop
```

verwijder de stack
```
docker-compose kill
```
