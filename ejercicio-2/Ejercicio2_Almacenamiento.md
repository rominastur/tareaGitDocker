# Ejercicio 2

[TOC]

Ejercicio 2 - almacenamiento

Bind mount para compartir datos

1. Crea una carpeta llamada saludo y dentro de ella crea un fichero llamado index.html con el
    siguiente contenido (Deberás sustituir ese XXXXX por tu nombre.):

2. Una vez hecho esto, arranca dos contenedores basados en la imagen php:7.4-apache que hagan un bind mount de la carpeta saludo en la carpeta /var/www/html del contenedor. Uno de ellos vamos a acceder con el puerto 8181 y el otro con el 8282. Y su nombres serán c1 y c2 .

3. Modifica el contenido del fichero ~/saludo/index.html .

4. Comprueba que puedes seguir accediendo a los contenedores, sin necesidad de reiniciarlos.

5. Borra los contenedores utilizados.

  Entregar:
  Un documento con los siguientes pantallazos y los comandos empleados para resolver cada apartado:
  Pantallazo con la orden correspondiente para arrancar el contenedor c1 (puerto 8181) realizando el bind
  mount solicitado.
  Pantallazo con la orden correspondiente para arrancar el contenedor c2 (puerto 8282) realizando el bind
  mount solicitado.
  Pantallazo donde se pueda apreciar que accediendo a c1 se puede ver el contenido de index.html .
  Pantallazo donde se pueda apreciar que accediendo a c2 se puede ver el contenido de index.html .
  Otros dos pantallazos donde se vea el acceso al fichero index.html después de modificarlo.
  Borrar los dos contenedores. Mostrar que se han borrado.



#### Bind mount para compartir datos

#### Crea una carpeta llamada saludo y dentro de ella crea un fichero llamado index.html con el siguiente contenido: HOLA SOY ROMINA SUAREZ CHAVES



Pantallazo para arrancar el contenedor c1 (puerto 8181) realizando bind mount con la carpeta saludo:

```
docker run -d --name c1 -v /home/romina/Escritorio saludo:/var/www/html -p 8181:80 php:7.4-apache
```

![image-20220411132513328](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411132513328.png)

Pantallazo para arrancar el contenedor c2 (puerto 8282) realizando bind mount con la carpeta saludo:

```
docker run -d --name c2 -v /home/romina/Escritorio saludo:/var/www/html -p 8282:80 php:7.4-apache
```

![image-20220411132533354](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411132533354.png)

Pantallazo que muestra el contenido de index.html accediendo a c1:

![image-20220411133224256](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411133224256.png)

Pantallazo que muestra el contenido de index.html accediendo a c2:

![image-20220411133245680](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411133245680.png)



#### Modifica el contenido del fichero ~/saludo/index.html.

Pasos para modificar index.html desde línea de comandos:

![image-20220411133405357](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411133405357.png)

Abro el archivo con el editor joe:

![image-20220411133424892](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411133424892.png)

Cambio el texto del encabezado:

![image-20220411133451304](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411133451304.png)

Salgo guardando los cambios:

![image-20220411133511832](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411133511832.png)