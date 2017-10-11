# Rol MediaWiki #

En este rol se buscara configurar un host con el servicio apache al cual le instalará MediaWiki y las dependencias de terceros, como lo son

- **git** : para control de versiones. *INSTALADO*
- **ImageMagik o Biblioteca GB** : para miniaturización de imagenes.
- **APCu, XCache o WinCache** : para manejar cache de objetos.

## Instalación de MediaWiki ##

Para la instalación de MediaWiki primero debemos descargar la version estable de este que se puede encontrar en la pagina oficial [aquí](https://www.mediawiki.org/wiki/MediaWiki).

Entonces el enlace se anexa a la variable **url_stable** en el archivo **main.yml** del directorio **vars/** de nuestro rol.

Extraer el archivo **tar.gz** y el contenido de este anexarlo al directorio web de apache, que comunmente es **/var/www/html/**.

Por ultimo se anexa la configuración de MediaWiki en esta se especifican, los datos de conexion de MySQL.

Las variables que se configuran en el archivo son las siguientes

- **mysql_media_usr:** Usuario para conexion con MySQL.
- **mysql_media_pwd:** Contraseña de usuario para conexion con MySQL.
- **mysql_media_db:** Nombre de la base de datos en MySQL.
- **mysql_db_prefix:** Prefix de las tablas que se crearán.
- **docker_ip_host:** Dirección ipv4 del adaptador docker.

Este ultimo dato se podria encontrar si se observa la dirección del adaptador de docker que se crea por defecto en el host.

Ejemplo ip docker

![alt-text](/img/Docker_ip.png)

por lo general es **172.17.0.1** o se encuentra en el ranto **172.0.0.0 - 172.255.255.255**.
