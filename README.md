# Instrucciones para usar la aplicación.

## Información.

Se usarán 3 contenedores:
* mongodb para la base de datos.
* nodeapp para el backend.
* reactapp para el frontend.

### MongoDB

Ejecutar los siguientes comandos:

* docker run --name mongodb --rm -d mongo


### Backend

Ejecutar los siguientes comandos:

* cd backend
* docker build -t goals-node .
* docker run --name goals-backend --rm -d -p 80:80 goals-node