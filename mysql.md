# Crear un servidor de MySQL mediante Docker

### 1. Descargar la imagen de MySQL desde Docker Hub

```
- docker pull mysql:8
```

### 2. Verificar la imagen de MySQL dsde la lista de imagenes de docker

```
- docker images
- docker images | grep mysql (linux/mac)
- docker images | findStr mysql (filtrar listas con windows)
```

### 3. Crear un contenedor con la imagen de MySQL

```
- docker create mysql:8
- docker create --name mysqlserver mysql:8
```

### 4. Listando los contenedores de docker

```
- docker ps -a
- docker ps -a | findStr hugle
```

### 5. Eliminando un contenedor de docker

```
- docker rm -f reverent_hugle
```

### 6. Definiendo los comandos para inciciar un contenedor:

```
- docker start mysqlserver ó ID
```

### 7. Verificando los procesos dentro de un contenedor

```
- docker logs mysqlserver
```

### 8. Para crear variables de entorno y exponiendo el puerto fuera de la red de docker

```
- docker run -d --name mysqlserver -p 3310:3306 -e MYSQL_ROOT_PASSWORD=1234 -e MYSQL_USER=user -e MYSQL_PASSWORD=1234 -e MYSQL_DATABASE=mysqlhexa mysql:8
```

### 9. Para detener con subprocesos activos, reanudar y detener con sus subprocesos un contenedor

```
- docker stop mysqlserver

- docker start mysqlserver

- docker kill mysqlserver
```

### 10. Para buscar el directorio de persistencia, en el objeto "volumes"

```
- docker inspect mysql:8
```

### 11. Para vincular un volumen al contenedor - persistencia con vol. anónimo - Estos no se recomiendan porque com generan un id aleatorio, cuando se regenera el contenedor este al no tener una referencia fija, este genera un volumen nuevo que parte desde cero a partir de un nuevo id, entoces el volumen anterior esta persistente pero con un id diferente, la única ventaja de esta forma es que tu puedes eliminar el contenedor y el volumen en un mismo paso.

```
- docker run -d --name mysqlserver -p 3310:3306 -v /var/lib/mysql  -e MYSQL_ROOT_PASSWORD=1234 -e MYSQL_USER=user -e MYSQL_PASSWORD=1234 -e MYSQL_DATABASE=mysqlhexa mysql:8
```

### 11.1 Para eliminar un contenedor con su volumen anónimo (sólo para contenedores con volumen anónimos)

```
- docker rm -fv mysqlserver | id
```

### 12. Para vincular un volumen al contenedor - persistencia con vol. host (Este persiste en algun directorio en tu máquina, y la ruta a este directorio no debe contener ninguna letra mayúscula) NOTA: en windows la ruta se define con doble back slash y estos no se pueden listar porque viven fuera de la red de docker.

```
- docker run -d --name mysqlserver -p 3310:3306 -v D:\\development\\clean_architectures\\docker\\docker-mysql:/var/lib/mysql  -e MYSQL_ROOT_PASSWORD=1234 -e MYSQL_USER=user -e MYSQL_PASSWORD=1234 -e MYSQL_DATABASE=mysqlhexa mysql:8
```

### 13. Para vincular un volumen al contenedor - persistencia con vol. nombrado (recomendado)

```
- docker run -d --name mysqlserver -p 3310:3306 -v vol-mysql:/var/lib/mysql  -e MYSQL_ROOT_PASSWORD=1234 -e MYSQL_USER=user -e MYSQL_PASSWORD=1234 -e MYSQL_DATABASE=mysqlhexa mysql:8
```

### 14. Para listar volúmenes ó filtrados por alguna cadena

```
- docker volume ls
- docker volume ls | grep vol-mysql (linux/mac)
- docker volume ls | findStr vol-nginx (windows)
```

### 15. Para eliminar volúmenes anónimos o nombrados (para poder eliminar un volumen, el contenedor asociado a este debe estar elminado)

```
- docker volume rm vol-mysql
```

### 16. Para inspeccionar un volumen

```
- docker volume inspect vol-mysql
```

### 17. Para entrar a la red virtual de docker desde windows, en la ruta de directorios ingresar a la siguiente ruta y navegar en /docker-desktop-data

```
- \\wsl$
```

### 18. Para crear una red de contenedores, donde vivirá nuestra contenedor, tenemos 3 tipos:

```
tipos:
- bridge (default/named bridge) recomendada -> named bridge
- host
- none

comando:
- docker network create net-mysql -d bridge

nota: Un contenedor puede estar asociado a todas las redes que se requieran.
```

### 19. Para listar redes

```
- docker network ls
- docker network ls | grep net-mysql (linux/mac)
- docker network ls | findStr net-mysql (windows)
```

### 20. Para inspeccionar redes

```
- docker network inspect net-mysql
```

### 21. Para crear un contenedor asignado a una red

```
- docker run -d --name mysqlserver --network net-mysql -p 3310:3306 -v vol-mysql:/var/lib/mysql  -e MYSQL_ROOT_PASSWORD=1234 -e MYSQL_USER=user -e MYSQL_PASSWORD=1234 -e MYSQL_DATABASE=mysqlhexa mysql:8
```

### 22. Para desvincular de una red

```
- docker network disconnect net-mysql mysqlserver
```

### 22. Para conectarte un conetendor a una red sin eliminar a este.

```
- docker network connect net-mysql mysqlserver
```

### 23. DOCKER COMPOSE: Es una lista de instrucciones para administrar de forma automatizada varios contenedores a la vez.
