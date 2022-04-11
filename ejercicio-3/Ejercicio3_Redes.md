# Ejercicio 3

[TOC]

Ejercicio 3 - redes

Despliegue de contenedores en red: Adminer y MariaDB

1. Crea una red bridge redbd

2. Crea un contenedor con una imagen de mariaDB que estará en la red redbd . Este contenedor se
    ejecutará en segundo plano, y será accesible a través del puerto 3306. (Es necesario definir la
    contraseña del usuario root y un volumen de datos persistente)

3. Crea un contenedor con Adminer que se pueda conectar al contenedor de la BD

4. Comprueba que el contenedor Adminer puede conectar con el contenedor mysql abriendo un
    navegador web y accediendo a la URL: http://localhost:8080

  Entregar:

  Los siguientes pantallazos y los comandos empleados para resolver cada apartado:

  Pantallazos donde se vean los contenedores creados y en ejecución
  Pantallazo donde se vea el acceso a la BD a través de la interfaz web de Adminer
  Pantallazo donde se vea la creación de una BD con la interfaz web Adminer
  Pantallazo donde se entre a la consola del servidor web en modo texto y se compruebe que se ha creado la BD
  Borrar los contenedores, la red, y los volúmenes utilizados



#### Ejercicio 3 - redes 

#### Despliegue de contenedores en red: Adminer y MariaDB 

#### Crea una red bridge redbd

Comandos para crear la red redbd e inspeccionarla:



![image-20220411140351666](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411140351666.png)



#### Crea un contenedor con una imagen de mariaDB que estará en la red redbd . Este contenedor se ejecutará en segundo plano, y será accesible a través del puerto 3306. (Es necesario definir la contraseña del usuario root y un volumen de datos persistente)



Comandos para crear el volumen de datos y el contenedor mdb en la red redbd:

```
docker volume create datos //crea volumen llamado datos
docker run -d --name mdb --network redbd -p 3306:3306 -e MARIADB_ROOT_PASSWORD=root -v datos:/var/lib/mysql mariadb:latest  //crea contenedor mdb en la red redbd
```

![image-20220411140615712](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411140615712.png)



Comando para crear el contenedor cadminer en la red redbd:

```
docker run --name cadminer --network redbd --link mdb:db -p 8080:8080 adminer //crea contenedor cadminer que se puede conectar al contenedor de la BD
```

![image-20220411140638163](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411140638163.png)



Pantallazo donde se ven los contenedores creados y en ejecución:

```
docker ps -a //lista todos los contenedores
```

![image-20220411140659531](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411140659531.png)





#### Comprueba que el contenedor Adminer puede conectar con el contenedor mysql abriendo un navegador web y accediendo a la URL: http://localhost:8080



Abro un navegador y accedo a la URL:localhost:8080/adminer. Hago el login con el usuario root y su contraseña:

![image-20220411141650006](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411141650006.png)



Compruebo que tengo acceso a la base de datos mysql:

![image-20220411141741508](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411141741508.png)



#### Crea una BD con la interfaz web Adminer

Creo base de datos “alumnos” con 5 alumnos (los alumnos son mis hijos, mis gatos y mi marido):

![image-20220411141811282](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411141811282.png)