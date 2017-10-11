# Configuración del entorno #

En este directorio se encuentran todos los roles a usar por ansible para la configuración de los host (contenedores docker).

Se han creado 3 roles principales los cuales son:

1. Apache
2. MySQL
3. MediaWiki

Los cuales instalan e configuran todas las dependencias e requerimientos de MediaWiki que se puede encontrar en su documentación oficial [aquí](https://www.mediawiki.org/wiki/Manual:Installation_requirements)

Ademas de los roles, creamos el archivo [hosts](hosts) en el cual se configura el metodo de conexion a nuestros contenedores, y la llave a usar, especificandole los siguientes atributos

- **ansible_port=** Se especifica el puerto donde se realizara la conexion ssh
- **ansible_ssh_private_key_file=** Se especifica la ruta donde se encuentra la llave privada, si se requiere

## Ejecutando rol Apache ##

Para la ejecución del rol apache se utiliza el siguiente comando

```
ansible-playbook -i {{ ruta del directorio host }} {{ruta del playbook que ejecuta el rol}}

En nuestro caso si estuviera en el directorio Ansible/ el comando seria equivalente ha

$ ansible-playbook -i hosts Apache.yml
```

Al realizar lo anterior deberias tener una salida parecida a la siguiente

![alt-text](/img/Apache_rol.png)

Y al ingresar por nuestro navegador a http://localhost/ debemos apreciar lo siguiente

![alt-text](/img/Home_apache.png)

## Ejecutando rol MySQL ##

Para la ejecución del rol MySQL se utiliza el siguiente comando
```
ansible-playbook -i {{ ruta del directorio host }} {{ruta del playbook que ejecuta el rol}}

En nuestro caso si estuviera en el directorio Ansible/ el comando seria equivalente ha

$ ansible-playbook -i hosts Mysql.yml
```

Al ingresar lo anterior se deberia tener una salida parecida a la siguiente

![alt-text](/img/MySQL_role.png)

Si contamos con mysql-client con el siguiente comando

`$ mysql -h localhost -u mediaW -p --protocol=tcp`

Podriamos establecer conexion con Mysql, apreciariamos lo siguiente

![alt-text](/img/Mysql_connect.png)

## Ejecutando rol MediaWiki ##

Para la ejecución del rol apache se utiliza el siguiente comandos

```
ansible-playbook -i {{ ruta del directorio host }} {{ruta del playbook que ejecuta el rol}}

En nuestro caso si estuviera en el directorio Ansible/ el comando seria equivalente ha

$ ansible-playbook -i hosts MediaWiki.yml
```

Al ingresar lo anterior se deberia tener una salida parecida a la siguiente

![alt-text](/img/MediaWiki_role.png)


### Termiando configuranción MediaWiki ###

Con lo anterior hemos configurado la conexion con la base de datos y el nombre del sitio, pero no genera las tablas en la BD por ende debemos terminar la configuración, para esto nos dirigiremos a http://localhost/media/mw-config/index.php.

Y aparecerá lo siguiente

![alt-text](/img/MediaW_config1.png)

En lo cual seleccionaremos el idioma de nuestra Wiki y presionamos continuar.

Despues aparecerá lo siguiente solicitandonos la llave de actualización

![alt-text](/img/MediaW_config2.png)

La cual se puede encontrar en el template LocalSettings.php.js en la linea 106, pero para que no busquen aquí esta **cca018cf3ac53a62**, la pegamos y presionamos continuar.

En la siguiente pagina podemos dar siguiente, seguido se muestra la siguiente pagina

![alt-text](/img/MediaW_config3.png)

Simplemente cambiamos la codificación de los datos a **UTF-8** y presionamos seguir.

En la siguiente pagina la llenamos con los datos pertinenetes y seleccionamos la opcion de instalación (sino quieren que les hagan mas preguntas), quedaría así

![alt-text](/img/MediaW_config4.png)

Presionamos continuar y aparecerá.

![alt-text](/img/MediaW_config5.png)

*Continuar si desear terminar la configuración y atras si desean cambiar algo.*

Presionamos continuar y ESPERAMOS que cargue la web, al final debe aparecer el siguiente mensaje

![alt-text](/img/MediaW_config6.png)

No precionamos continuar, ya nuestro archivo de configurancin esta listo, accedemos a http://localhost/media y debe aparecer

![alt-text](/img/MediaW_config7.png)

Y si quieren pueden acceder con el usuario creado, una captura de mi acceso

![alt-text](/img/MediaW_config8.png)


y listo MediaWiki ha sido instalado.
