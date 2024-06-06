# Labo04 - A first stateless microservice

## Pedagogical intent

This lab will certainly be a little more complex than the previous ones, but it's excellent preparation for the rest of the module project.

Here are the skills trained:
* Discover spring MVC architecture for REST api backend applications,
* Deploying a 2-tier application in Docker using a DockerCompose file,
* Use input parameters to launch containers,
* Test api calls to your Dockerized application via curl.

## Backlog

### Initial setup
* Clone this repository

```
git clone https://github.com/CPNV-VIR1/spring-rest-api.git
```

* Read the readme

* Deploy the app

* Test the app (manually)

### Docker setup

* Init docker

[INPUT]
```
docker init
```

[OUTPUT]
```
Welcome to the Docker Init CLI!

This utility will walk you through creating the following files with sensible defaults for your project:
  - .dockerignore
  - Dockerfile
  - compose.yaml
  - README.Docker.md

Let's get started!

? What application platform does your project use?  [Use arrows to move, type to filter]
  Java - (detected) suitable for a Java application that uses Maven and packages as an uber jar
  Go - suitable for a Go server application
  Python - suitable for a Python server application
  Node - suitable for a Node server application
  Rust - suitable for a Rust server application
  ASP.NET Core - suitable for an ASP.NET Core application
  PHP with Apache - suitable for a PHP web application
  Other - general purpose starting point for containerizing your application
  Don't see something you need? Let us know!
> Quit
```

### Deploy the app (single-tier)

[Source](https://docs.docker.com/language/java/develop/)


Ajouter dans le docker compose
```java
# Comments are provided throughout this file to help you get started.
# If you need more help, visit the Docker Compose reference guide at
# https://docs.docker.com/go/compose-spec-reference/

# Here the instructions define your application as a service called "server".
# This service is built from the Dockerfile in the current directory.
# You can add other services your application may depend on here, such as a
# database or a cache. For examples, see the Awesome Compose repository:
# https://github.com/docker/awesome-compose
services:
  server:
    build:
      context: .
    ports:
      - 8080:8080
    depends_on:
      db:
        condition: service_healthy
    environment:
      spring.datasource.url: jdbc:postgresql://db:5432/petclinic
      spring.datasource.username: petclinic
      spring.datasource.password: petclinic
      spring.jpa.database-platform: org.hibernate.dialect.PostgreSQLDialect
      spring.jpa.hibernate.ddl-auto: update
  db:
     image: postgres
     restart: always
#     secrets:
#       - db-password
     volumes:
       - db-data:/var/lib/postgresql/data
     environment:
       - POSTGRES_DB=petclinic
       - POSTGRES_USER=petclinic
       - POSTGRES_PASSWORD=petclinic
     expose:
       - 5432
     healthcheck:
       test: [ "CMD", "pg_isready", "-U", "petclinic"]
       interval: 10s
       timeout: 5s
       retries: 5
volumes:
  db-data:
# secrets:
#   db-password:
#     file: db/password.txt


# The commented out section below is an example of how to define a PostgreSQL
# database that your application can use. `depends_on` tells Docker Compose to
# start the database before your application. The `db-data` volume persists the
# database data between container restarts. The `db-password` secret is used
# to set the database password. You must create `db/password.txt` and add
# a password of your choosing to it before running `docker-compose up`.


```

build docker compose 
```java
docker compose up --build
```

Ajouter dans pom postgresql
```Java 
<dependency>
    <groupId>org.postgresql</groupId>
    <artifactId>postgresql</artifactId>
    <version>42.7.3</version>
</dependency>
```


