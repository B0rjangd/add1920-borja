# 1. Contenedores con Docker
Docker nos permite crear "contenedores", que son aplicaciones empaquetadas auto-suficientes, muy livianas, capaces de funcionar en prácticamente cualquier ambiente, ya que tiene su propio sistema de archivos, librerías, terminal, etc.

Docker es una tecnología contenedor de aplicaciones construida sobre LXC.

# 2. Configuraciones pertinentes e instalación

Si queremos que nuestro contenedor tenga acceso a la red exterior, debemos activar tener activada la opción IP_FORWARD

![](img/1.png)

## 2.1 instalación

Comenzamos instalando la herramienta Docker.

![](img/2.png)

Iniciamos el servicio

![](img/3.png)

Comprobamos la versión cliente y servidor.

![](img/4.png)

## 2.2 Primera prueba

Mostramos las imágenes descargadas hasta ahora(No debe de haber ninguna)

![](img/5.png)

Mostramos los contenedores creados(No debe de haber ninguna)

![](img/6.png)

Procedemos a descargar la imagen **hello-world**.

![](img/7.png)

Mostramos la imagen descargada.

![](img/8.png)

Comprobamos que hay un contenedor en estado "Exited"

![](img/9.png)


# 3. Crear un contenedor manualmente

Con el comando **docker search debian** Buscamos en los repositorios de Docker Hub contenedores con la etiqueta Debian

Descargamos una imagen Debian en local y comprobamos la descarga

![](img/2.1.png)

Creamos un contenedor de nombre con_debian utilizando la imagen anterior y ejecutaremos el programa /bin/bash dentro del contenedor

![](img/3.1.png)

## 3.1 Personalizar el contenedor

Comprobamos que estamos en Debian.

![](img/4.1.1.png)

Actualizamos los repositorios del contenedor.

![](img/5.1.png)

Instalamos el servidor Nginx en el contenedor.

![](img/6.1.png)

Instalamos el editor vim.

![](img/7.1.png)

Creamos el fichero HTML holamundo.html en /var/www/html/

![](img/9.1.png)

Creamos un script /root/server.sh.

![](img/10.1.png)

Introducimos el siguiente contenido.

![](img/11.png)

Le damos permisos de ejecución.

![](img/12.png)

## 3.2 Crear una imagen a partir del contenedor

En otra ventana de terminal ejecutar **docker commit con_debian nombre-del-alumno/nginx1**.

![](img/13.png)

Comprobamos que la imagen se ha creado.

![](img/14.png)

# 4. Crear contenedor a partir de nuestra imagen.
## 4.1 Crear contenedor con Nginx

* Ejecutamos: **docker run --name=con_nginx1 -p 80 -t nombre_imagen /root/server.sh** para iniciar el contenedor a partir de la imagen anterior.

![](img/15.png)

## 4.2 Comprobamos

En otro terminal, ejecutamos **docker ps** para mostrar el contenedor en ejecución y la redirección a un puerto local.

![](img/16.png)

Abrimos el navegador e introducimos 0.0.0.0:puerto del contenedor.

![](img/17.1.png)

Comprobamos el acceso a holamundo.html.

![](img/17.png)

Paramos el contenedor y lo eliminamos.

![](img/18.png)
![](img/19.png)
![](img/20.png)

## 4.3 Migrar la imágen a otra máquina

Exportamos la imagen en un fichero tar utilizando **docker save -o ~/alumnoXX.tar nombre-alumno/nginx1,**

![](img/21.png)





# 5 Dockerfile

Ahora vamos a conseguir el mismo resultado del apartado anterior, pero usando un fichero de configuración. Esto es, vamos a crear un contenedor a partir de un fichero Dockerfile. El fichero Dockerfile contiene toda la información necesaria para construir el contenedor

## 5.1 Preparar ficheros

Creamos el direcctorio /home/nombre-alumno/dockerXXa y entramos en el mismo.

![](img/22.png)

Creamos el fichero holamundo.html anterior

![](img/23.png)

De la misma forma, también creamos el fichero server.sh anterior.

![](img/24.png)

Creamos un fichero **Dockerfile** e introducimos el siguiente contenido.

![](img/25.png)


## 5.2 Crear la imagen a partir del Dockerfile

Dentro del directorio dockerXXa, ejecutar **docker build -t nombre-alumno/nginx2 .**

![](img/26.png)

Comprobamos que se ha creado nuestra imagen.

![](img/28.png)

## 5.3 Crear contenedor y comprobar

Creamos un contenedor con el nombre con_nginx2, a partir de la imagen nombre_alumno/nginx2. Para ello utilizaremos el siguiente comando **docker run --name=con_nginx2 -p 8080:80 -t nombre-alumno/nginx2**

![](img/29.png)

Desde otra terminal, ejecutamos el comando docker ps para averiguar el puerto de escucha del servidor Nginx

![](img/31.png)

Comprobamos desde el navegador.

![](img/32.png)

## 5.4 Usar imágen ya creadas

Creamos el directorio dockerXXb. Entrar al directorio.

![](img/33.png)

Creamos el fichero de configuración Dockerfile con lo siguiente en su interior.

![](img/34.png)

Creamos la imagen nombre_alumno/nginx3 y Creamos el contenedor utilizando la imagen.

![](img/40.png)

Comprobamos:

![](img/41.png)
