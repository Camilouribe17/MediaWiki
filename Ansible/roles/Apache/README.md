# Rol Apache #

En este rol se buscara configurar un host instalando PHP y los modulos usado por MediaWiki los cuales se han enlistado en la explicación principal, a continuación referenciare el estado de los modulos en PHP 7.0 la cual se instalará.

- Perl Compatible Regular Expressions PCRE (Instalado por defecto)
- Session (Instalado por defecto)
- JSON (Instalación manual)
- mbstring (Instalación Manual)
- intl (Instalación Manual)
- OpenSSL (Instalado por defecto)
- php7.0-xml (Instalacion manual)
- php7.0-mysql (Instalacion manual, ya que usaremos mysql si se utilizara otro motor de base de datos seria distinto)

Por requerimiento de Apache se debe instalar el modulo libapache2-mod-php7 para que este pueda ejecutar codigo PHP.

## Instalación de Apache ##

Para la instalación de apache instalamos el paquete **apache2**, desde el manejador de respositorio apt, e se inicia el servicio.

La instalación simularia los siguientes comandos

```
Instalación
$ sudo apt install apache2

Inicio del servicio
$ sudo service apache2 start
```
