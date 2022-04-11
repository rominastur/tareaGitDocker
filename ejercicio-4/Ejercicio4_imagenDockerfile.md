# Ejercicio 4

[TOC]

Ejercicio 4 - imagen con Dockerfile

Para la realización de este ejercicio es necesario tener una cuenta en Docker Hub.

Crear una imagen con un servidor web que sirva un sitio web
Basar la imagen en nginx o apache
Desplegar una plantilla, o un proyecto tuyo, que tenga, al menos, un index.html y una carpeta para
estilos, imágenes, etc.

Entregar:

Los siguientes pantallazos y los comandos empleados para resolver cada apartado:

1. Pantallazo/bloque de código con el Dockerfile
2. Pantallazo donde se vea el comando que crea la nueva imagen.
3. Pantallazo donde se ve el acceso al navegador con el sitio servido
4. Pantallazo donde se vea la imagen subida a tu cuenta de Docker Hub.



#### Pantallazo/bloque de código con el Dockerfile



Tengo una carpeta en el escritorio llamada apacheprueba, con los archivos de la plantilla dimensión de HTML5up dentro de un subdirectorio public-html. Dentro de la carpeta apacheprueba creo el archivo de texto plano Dockerfile, siguiendo las instrucciones de Docker Hub para la imagen httpd:2.4:

```
FROM httpd:2.4
COPY ./public-html/ /usr/local/apache2/htdocs/
```



![image-20220411145352921](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411145352921.png)



#### Pantallazo donde se vea el comando que crea la nueva imagen



Sigo las instrucciones de Docker Hub para construir el contenedor que servirá el contenido de la carpeta public-html:

```
docker build -t my-apache2 .
FROM httpd:2.4
COPY ./public-html/ /usr/local/apache2/htdocs/
```

![image-20220411145404199](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411145404199.png)



Arranco el contenedor, que ejecutará una instancia de la imagen my-apache2 y servirá la plantilla dimensión, descargada de HTML5up, por eso le he puesto el nombre apachedimension:

```
docker run -dit --name apachedimension -p 8080:80 my-apache2
```

![image-20220411145444886](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411145444886.png)



#### Pantallazo donde se ve el acceso al navegador con el sitio servido

Accedo desde el navegador a la URL http://localhost:8080

![image-20220411151055388](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411151055388.png)



#### Pantallazo donde se vea la imagen subida a tu cuenta de Docker Hub



Comandos para subir la imagen a mi cuenta de Dockerfile:

```
docker tag my-apache2 rominastur/apachedimension:v1
docker push rominastur/apachedimension:v1
```



![image-20220411152100993](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411152100993.png)





![image-20220411152120964](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411152120964.png)





![image-20220411152132685](C:\Users\Romina\AppData\Roaming\Typora\typora-user-images\image-20220411152132685.png)