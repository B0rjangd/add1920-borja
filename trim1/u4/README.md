# Servicio de Directorio con comandos

## 2.3 Comprobar contenido del DS LDAP

* ***ldapsearch -b "dc=ldapXX,dc=curso1920" -x | grep dn***, muestra el contenido de nuestra base de datos LDAP.

 ![](img/1.png)

* *** ldapsearch -H ldap://localhost -b "dc=ldapXX,dc=curso1920" -W -D "cn=Directory Manager" | grep dn *** , en este caso hacemos la consulta usando usuario/clave.
 ![](img/2.png)

 ## 3.3 Comprobar nuevo usuario
* *** ldapsearch -W -D "cn=Directory Manager" -b "dc=ldapXX,dc=curso1920" "(uid=*)" ***, para comprobar si se ha creado el usuario en el LDAP.
  ![](img/3.png)

## 4.3 Comprobar los usuarios creados
* Ir a la MV cliente LDAP
![](img/4.png)

* Usuario Mazinger
 ![](img/5.png)

* Usuario Koji
![](img/6.png)
* Usuario Boss
![](img/7.png)
* Usuario Doctor Infierno
![](img/8.png)
