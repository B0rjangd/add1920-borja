# 1. Salt-stack
Hay varias herramientas conocidas del tipo gestor de infrastructura como Puppet, Chef y Ansible. En esta actividad vamos a practicar Salt-stack con OpenSUSE.

# 2. Preparativos
Para esta realizar la siguiente práctica necesitaremos dos máquinas virtuales, una Master con a la cual le cambiaremos el hotsname a  **masterXXg** y otra Minion a la cual le cambiaremos el hostname a **minionXXg**. Ambas utilizaran como OS **OpenSUSE**

# 3. Master: instalar y configurar

Empezamos instalando en la mv Máster el software del Máster:

![](img/3.png)

Modificamos el fichero **/etc/salt/master** con la siguiente configuración:

![](img/4.png)

Habilitamos el servicio salt-master:

![](img/5.png)

Lo iniciamos:

![](img/6.png)

Consultamos los Minions aceptados por nuestro Máster. **salt-key -L** . No debería haber nada todavía

![](img/7.png)

# 4. Minion
> Los minios son los equípos que van a estar bajo control del Máster
## 4.1 Instalación y configuración
Instalamos el software del agente minion en nuestra máquina minionXXg

![](img/8.png)

Modificamos el fichero */etc/salt/minion* para definir quien será nustro Máster:

![](img/9.png)

Activamos el servicio del Minion:

![](img/10.png)

Iniciamoso el servicio:;

![](img/11.png)

Comprobamos que no tenemos instalado apache2 en el Minion:

![](img/12.png)

## 4.2 Aceptación desde el Máster

Desde la máquina del Máster y teniendo en cuenta que el cortafuegos acepta las peticiones del servicio Salt, ejecutamos el comando **salt-key -L** para ver la petición del Minion:

![](img/13.png)


Lanzamos el comando salt-key -a minionxxg para acceptar la petición:

![](img/14.png)

![](img/15.png)

## 4.3 Comprobación de conectividad

*  **salt '*' test.version**:

![](img/16.png)

* **salt '*' test.ping**

![](img/17.png)


# 5. Preparar el directorio para los estados

* Crear directorios **/srv/salt/base** para guardar nuestros estados y **/srv/salt/devel** para desarollo o para hacer pruebas :

![](img/18.png)

* Crear archivo **/etc/salt/master.d/roots.conf** con el siguiente contenido:

![](img/20.png)

Reiniciamos el servicio Máster:

![](img/21.png)

## 5.1 Crear un nuevo estado

* Crear fichero **/srv/salt/base/apache/init.sls** de la siguiente forma:

![](img/25.png)


## 5.2 Asociar Minions a estados

En el Máster, crear **/srv/salt/base/top.sls** donde asociamos a todos los Minions con el estado que acabamos de definir:

![](img/27.png)

## 5.3 Comprobar el estado definido

Comprobamos con **salt '*' state.show_states**:
![](img/28.png)

## 5.4 Aplicar el nuevo estado

En el Máster consultamos los estados en detalle y verificamos que no hay errores en las definiciones:

* **salt '*' state.show_lowstate**

![](img/29.png)

* **salt '*' state.show_highstate**

![](img/30.png)

Aplicamos el estado con en todos los minions usando el comando **salt '*' state.apply apache**

# 6. Crear más estados

Vamos a crear un estado llamado users que nos servirá para crear un grupo y usuarios en las máquinas Minions.

* Crear directorio **/srv/salt/base/users**:

![](img/31.png)

* Crear fichero **/srv/salt/base/users/init.sls**

![](img/32.png)

Dentro del mismo creamos el grupo mazingerz y los usuarios kojiXX y drinfernoXX:

![](img/34.1.png)

Aplicamos el estado:

![](img/34.png)

![](img/35.png)
![](img/36.png)

## 6.1 Crear estado directories

* Crear estado drectories para crear las carpetas private (700), public (755) y group (750) en el home del usuario koji.

![](img/37.png)
![](img/39.png)
![](img/40.png)
![](img/41.png)

* Aplicamos el estado:

![](img/42.png)
![](img/43.png)

# 7. Añadir Minion de otro SO

Desde una MV con SO Windows, instalar salt-minion y enviar una petición al Máster:

![](img/46.png)
![](img/45.png)

Comprobamos que se ha rellizado la petición con éxito:

![](img/47.png)
