# Instrucciones para usar la aplicación.


## Acerca de.

Esta aplicación genera un listado de tareas por hacer. Implementando comunicación entre contenedores, volúmenes y networks.

## Información.

Se utilizará 1 red:

* goals-net

Se usarán 3 contenedores:

* mongodb para la base de datos.
* goals-backend para el backend.
* goals-frontend para el frontend.

Se pueden usar dos alternativas, crear todo paso a paso o usar docker-compose.
Cuando se opta por usar docker-compose se lee el archivo docker-compose.yaml donde vienen todas las instrucciones especificadas
en el apartado manual de este documento y se ejecutan con un solo comando.

## Método manual.


### Network.

Ejecutar el siguiente comando para crear la red:

* docker network create goals-net

### MongoDB.

Ejecutar los siguientes comandos:

* docker run --name mongodb -v data:/data/db --rm -d --network goals-net -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=secret mongo

Si el comando falla, puedes crear el usuario manualmente con los siguientes pasos:

* docker run --name mongodb -v data:/data/db --rm -d --network goals-net mongo
* docker exec -it mongodb bash
* mongo 127.0.0.1
* use admin
* db.createUser({user:"admin", pwd: "secret", roles: [{role: "userAdminAnyDatabase", db: "admin"}]})


### Backend.

Ejecutar los siguientes comandos:

* cd backend
* docker build -t goals-node .
* docker run --name goals-backend -v [Ruta completa terminando en directorio backend]:/app -v logs:/app/logs -v /app/node_modules -e MONGODB_USERNAME=[MONGODBUSER] --rm -d --network goals-net -p 80:80 goals-node

Ejemplo del comando:

* docker run --name goals-backend -v "C:\Users\alex0\Documents\Udemy\Docker and Kubernets\multi-01-starting-setup\backend:/app" -v logs:/app/logs -v /app/node_modules  -e MONGODB_USERNAME=admin --rm -d --network goals-net -p 80:80 goals-node


### Frontend.

Ejecutar los siguientes comandos:

* cd frontend
* docker build -t goals-react .
* docker run -v [Ruta completa terminando en el directorio src]:/app/src --name goals-frontend --rm -p 3000:3000 -it goals-react

Ejemplo del comando:

* docker run -v "C:\Users\alex0\Documents\Udemy\Docker and Kubernets\multi-01-starting-setup\frontend\src\:/app/src" --name goals-frontend --rm -p 3000:3000 -it goals-react

## Docker-compose

Ejecutar el siguiente comando:

* docker-compose up -d