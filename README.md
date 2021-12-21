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


### Network

Ejecutar el siguiente comando para crear la red:

* docker network create goals-net

### MongoDB

Ejecutar los siguientes comandos:

* docker run --name mongodb --rm -d --network goals-net mongo


### Backend

Ejecutar los siguientes comandos:

* cd backend
* docker build -t goals-node .
* docker run --name goals-backend --rm -d --network goals-net -p 80:80 goals-node


### Frontend

Ejecutar los siguientes comandos:

* cd frontend
* docker build -t goals-react .
* docker run --name goals-frontend --rm -p 3000:3000 -it goals-react