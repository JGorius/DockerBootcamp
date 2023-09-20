# DockerBootcamp

<br>

Das DockerBootcamp soll ein generelles Verständnis für Docker und Portainer zu vermitteln und um eine Vertiefung des Verständnisses für Stack-Bereitstellung zu gewährleisten, u.a. anhand eines Beispiels einer Datenbank-Installation.

Dadurch soll die lokale Entwicklung vereinfacht werden, sowie der Bereitschaftseinsatz, eine  Containerisierte Anwendung neustarten zukönnen.

<br>

### Voraussetzungen
> Ein DockerHub-Account muss erstellt werden.
> <br>
> DockerDesktop sollte installiert sein: <br> https://docs.docker.com/desktop/install/windows-install/ <br>
> DB Visualizer sollte installiert sein: <br> https://www.dbvis.com/

<br>

### Installation Portainer
>  1. Die aktuellste Version des Stacks laden: https://downloads.portainer.io/ce2-19/portainer-agent-stack.yml 
>  2. Dies "speichern unter" in "Downloads" als "portainer-agent-stack.yml"
>  3. Terminal: cd Downloads
>  4. Befehl:  docker stack deploy -c portainer-agent-stack.yml portainer
>  5. Jetzt sieht man auf Docker Desktop die Container
>  6. Danach https://localhost:9443 aufrufen

<br>

In einem Stack können nun mehrere Container zusammengefasst werden oder auch orchestriert genannt.
<br>
Ein möglichst einfaches Beispiel wäre der Bestandteil einer Geschäftsanwendung:
<br>
Frontend - Backend - Datenbank

<br>
Nun folgen Beispiele, die während des Bootcamp verwendet werden sollen. <br>
Es wird nun Schritt für Schritt erläutert, wie eine Stack-Datei aufgebaut ist.

<br>

### Beispiel 0: HelloWorld 
````
version: "3.8"
services:

  HelloWorld:
    image: karthequian/helloworld:latest
````
> services : Darunter kommen alle Service, die in dieser Datei enthalten sind -> hier nur einer , können aber auch meherer sein!
> HelloWorld : Ist ein konkreter Service


<br>

### Beispiel 1: HelloWorld mit Ports
```
version: "3.8"
services:

  HelloWorld:
    image: karthequian/helloworld:latest
    ports:
      - "7001:80"
```

<br>

### Beispiel 2: Datenbank deployen

<br>

>   1. Nun bauen wir mit DB Visualizer eine Verbindung auf.
>   2. Wir erstellen Daten und fragen diese ab.
>   3. Löschen Container und starten diese neu.
>   4. Problem: nach Neustart der Container werden alle Daten verloren sein.
>   5. Um dieses Problem zu lösen erstellen wir dafür Docker Volumes (siehe Beispiel 3) bzw. geben diese in der Config-Datei an.

<br>

```
version: "3.8"

services: 

  Postgres:
    image: postgres:latest            
    ports:
      - "7002:5432"
    environment:
      POSTGRES_USER: postgres         
      POSTGRES_PASSWORD: admin
````

<br>

### Beispiel 3: Persistentes Volume hinzugefügt
   ```
version: "3.8"

services: 

  Postgres:
    image: postgres:latest            
    ports:
      - "7002:5432"
    environment:
      POSTGRES_USER: postgres         
      POSTGRES_PASSWORD: admin

    volumes:
      - postgres-data:/var/lib/postgresql/data

volumes:
  postgres-data:
```
