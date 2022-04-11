# Ejercicio 3

[TOC]

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

```
docker network create redbd
docker network inspect redbd
```

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





#### Pantallazo donde se entra a la consola del servidor web en modo texto y se comprueba que se ha creado la BD



![image-20220411142830010](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411142830010.png)

 Compruebo en adminer que se trata de la BD que he creado:

![image-20220411143032784](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411143032784.png)





#### Borrar los contenedores, la red, y los volúmenes utilizados



Los contenedores, los paro, los borro y listo para comprobar que ya no están:

```
docker stop mdb cadminer //paro los contenedores mdb y cadminer
docker rm mdb cadminer //borro los contenedores mdb y cadminer
docker ps -a //listo todos los contenedores para comprobar que se han borrado
```

![image-20220411143825241](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411143825241.png)



La red, listo para copiar su id, la borro y vuelvo a listar:

```
docker network ls //listo las redes para copiar la id de la redbd
docker network rm network_ID //borro la red identificándola por su ID
docker network ls  //listo para comprobar que se ha borrado
```

![image-20220411143918446](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411143918446.png)



El volumen datos, primero listo, tengo 4 volúmenes, borro el volumen utilizado en este ejercicio (datos) y vuelvo a listar comprobando que quedan los otros 3 volúmenes:

```
docker volume ls //listo volúmenes
docker volume rm datos //borro volumen datos
docker volume ls //listo para comprobar que el volumen datos ya no aparece
```

![image-20220411143940830](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411143940830.png)