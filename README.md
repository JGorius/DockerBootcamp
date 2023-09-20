# DockerBootcamp

<br>

## Beispiel 0: HelloWorld 
````
version: "3.8"
services:

  HelloWorld:
    image: karthequian/helloworld:latest
````

<br>

## Beispiel 1: HelloWorld mit Ports
```
version: "3.8"
services:

  HelloWorld:
    image: karthequian/helloworld:latest
    ports:
      - "7001:80"
```

<br>

## Beispiel 2: Datenbank deployen
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

## Beispiel 3: Stack updaten

<br>

## Beispiel 4: Persistentes Volume hinzugefügt
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
