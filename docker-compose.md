# Docker Compose Commands

### Para ejecutar un archivo docker-compose.yaml

```
Ejecuta el archivo docker-compose.yaml
- docker compose up -d
```

### Para eliminar todas las acciones que hayamos hecho en el docker-compose

```
Es decir, dar de baja a todos los contenedores especificados en el archivo y tambien todas sus redes, obviamente las imágenes y los volúmenes no las elimina ya que estas pueden vivir sin contenedor.

- docker compose down
```

### Para ver el estado de los contenedores generados por docker-compose (sin importar el estado)

```
- docker compose ps
- docker compose ps | grep mysqlserver (linux/mac)
- docker compose ps | findStr mysqlserver (windows)
```

### Para ejecutar solamente algunos servicios

```
Los servicios en docker-compose son los que van a representar finalmente cada marco de instrucción, por ejemplo, un marco de instrucción para rabbit, o para mongodb...

Entonces dentro de los servicios donde tu vas a especificar, se va a generar un contenedor, con nombre tal, que va a tener una imagen, con ciertos puertos, etc.

Entonces dentro del archivo docker-compose se referencia por servicio no por contenedor, ya que el contenedor viene siendo una instrucción dentro del servicio.

El siguiente comando va a revisar si hay contenedores dentro del docker-compose que ya se esten resolviendo, si eso es asi, va a devolver con una caché de ese servicio, y solamente ejecutará los restantes o los que se hayan agregado posteriormente.

- docker compose up -d

El siguiente comando solamente resolverá los servicios que se especifiquen, de la siguiente manera:

- docker compose up -d <nombre_servicio1> <nombre_servicio2>

```

### Archivo docker-compose.yaml , en este archivo tenemos todo el listado de instrucciones para tener un contenedor con todas las variables que necesita, con sus voumenes, puertos y redes.

```
version: "3.8"

services:
  mysql-server:
    image: mysql:8
    container_name: mysqlserver
    environment:
      - MYSQL_ROOT_PASSWORD=1234
      - MYSQL_USER=user
      - MYSQL_PASSWORD=1234
      - MYSQL_DATABASE=mysqlhexa
    ports:
      - "3310:3306"
    networks:
      - net-mysql
    volumes:
      - vol-mysql:/var/lib/mysql

networks:
  net-sql:

volumes:
  vol-mysql:


NOTA:En caso de que se tengan mas contenedores se tendrían que definir otro servicio con sus especificaciones dentro del archivo docker-compose.yml , y en caso de que se necesiten comunicar los contenedores no se mandan a llamar por el nombre del contenedor, sino que se apunta al nombre del servicio.
```

### Para buscar/listar un docker compose

```
- docker compose ps | findStr mysql
- docker compose ps | findStr 3306
```
