# Rol MySQL #

En este rol se buscara configurar un host instalando MySQL y el modulo de python para la ejecución del modulo mysql_user de ansible el cual es *python-mysqldb*.

## Instalación de MySQL ##

Para la instalación de mysql primero configuramos el entorno especificando la contraseña que se pregunta al momento de instalar el paquete correspondiente, para ello utilizamos el modulo *debconf*.

Al utilizar el modulo debconf los comando equivalentes en el sistema serian los siguientes
```
Preparando el sistema para que no sea interactivo

$ export DEBIAN_FRONTEND="noninteractive"

Especificando contraseña root para MySQL

$ sudo debconf-set-selections <<< "mysql-server mysql-server/root_password {{ contraseña }}"

Confirmando contraseña root de MySQL

$ sudo debconf-set-selections <<< "mysql-server mysql-server/root_password_again {{ contraseña }}"
```
despues instalamos el paquete **mysql-server** y el modulo para la ejecucion del modulo *mysql_user* de ansible, desde el manejador de respositorio apt, seleccionamos el directorio por defecto de mysql e copiamos nuestra configuracion de mysql y  se inicia el servicio.

La instalación simularia los siguientes comandos

```
Instalación
$ sudo apt install mysql-server python-mysqldb

Directorio por defecto
usermod -d /var/lib/mysql/ mysql

Copiando configuración (Realmente se utiliza scp para enviar archivos por ssh)

cp -R {{remote host}} /etc/mysql/mysql.conf.d/mysqld.cnf  (no tan cierto :D)

Inicio del servicio
$ sudo service mysql-server start
```

Y aqui termina la instalación de MySQL.

### Configuando usuario y base de datos para MediaWiki ###

Como paso de seguridad se eliminan todos los usuarios anonimos de mysql, creamos el usuario **mediaW** y la base de datos **MediaWiki**.

Gracias al modulo mysql_user y mysql_db los cuales nos proporcionan el promt de MySQL.

Lo equivalente realizado en el playbook en el promt de MySQL es lo siguiente:

```
Eliminando usuarios aninimos
> DELETE FROM mysql.user where User=”;
Creando usuario mediaW
> CREATE USER 'mediaW'@'localhost' IDENTIFIED BY 'pwd';

Dando permisos a login remoto del usuario mediaW
> GRANT ALL ON *.* to mediaW@'host_ip or % (for all)' IDENTIFIED BY 'pwd';

Creando base de datos MediaWiki
> CREATE DATABASE MediaWiki ENCODING utf8;
```
