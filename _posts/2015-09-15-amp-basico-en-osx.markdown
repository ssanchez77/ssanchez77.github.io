---
layout: post
title:  "AMP Básico en OSX"
permalink: amp-basico-en-osx
date:   2015-09-15 15:07:12
comments: true
categories:
- general
- osx
---

AMP son las conocidas siglas para referirse a un entorno de trabajo que incorpora _Apache, MySQL y PHP_. Esto se puede instalar y configurar en Windows, Linux y Mac OSX.

Un equipo en donde AMP esté operando correctamente funciona como _Servidor Web_, y se usa para desarrollar y probar sitios web localmente, simulando el comportamiento que tendrán luego cuando sean migrados a servidores de hospedaje, en los cuales harán uso de estas mismas tres tecnologías.

Aunque existen instaladores especiales que incluyen todos los elementos encapsulados para Windows ([WAMP](http://www.wampserver.com/)) y Mac OSX ([MAMP](https://www.mamp.info/)), la gracia es ver cómo se puede poner a funcionar todo por separado.

<!--more-->

Vamos a revisar el procedimiento para Mac, que luego de la actualización Yosemite es sumamente sencillo. En Linux este asunto es mucho más complicado (léase: _divertido_), pero puesto que OS X está construido sobre UNIX, mucho de lo que se aprende trabajando desde la consola de Mac también es aplicable (quizá con unos pequeños ajustes) en Linux.

Para empezar (y sorry por quitarles el impulso) Yosemite ya viene configurado con Apache 2.4 y PHP, así que nos enfocaremos la conexión de todas las partes para que el Servidor Web trabaje _con toda la pata_.

## Primeros pasos

Vamos a utilizar la consola, así que iniciamos la aplicación _Terminal_ y pasamos a la modalidad de usuario con privilegios (o _root_) para que no haya problemas de permisos al ejecutar los comandos.

> Será necesario ingresar la constraseña del administrador del equipo. Trabajar como _root_ es peligroso si uno no está seguro de lo que está haciendo. Por favor tenga cuidado porque podría dañar el sistema si borra o cambia algo que no debería.

{% highlight bash %}
sudo su -
{% endhighlight %}

Ahora arrancamos el proceso de Apache:

{% highlight bash %}
apachectl start
{% endhighlight %}

Para comprobar que Apache está activo, al ingresar a [http://localhost](http://localhost) deveriamos ver el siguiente mensaje: **"It works!"**

Desde la consola se puede ver cuál es la versión actual de Apache, por medio del siguiente comando:

{% highlight bash %}
httpd -v
{% endhighlight %}

## Directorio raíz de Apache

El _DocumentRoot_ (directorio raíz) es el lugar donde se almacenan los archivos que nuestro servidor va a compartir. Es el equivalente a `public_html` y `htdocs`.

OSX ha tenido históricamente dos directorios raíz: uno a nivel de sistema y otro a nivel de usuario. Podemos usar ambos o solamente trabajar con uno.

La ventaja de usar el de nivel de usuario es que cada usuario tiene su propia carpeta raíz independiente, mientras que el que está a nivel sistema es global para todos. Además cuando usamos el de nivel de usuario no hay que estar escribiendo la contraseña de administrador cada vez que queremos hacer una modificación a los archivos dentro de la carpeta raíz.

La ruta de la carpeta raíz a nivel de sistema es la siguiente:

{% highlight bash %}
/Library/WebServer/Documents/
{% endhighlight %}

La carpeta raíz de usuario puede estar donde uno desee, pero tradicionalmente se utiliza `~/Sites`, es decir una carpeta llamada `Sites` creada en la carpeta del usuario específico. Por ejemplo, en mi caso sería `\Users\ssanchez\Sites` porque `ssanchez` es mi nombre de usuario.

El directorio raíz de nivel de usuario no está habilitado por defecto, sino que hay que hacerlo manualmente.

Para eso debemos ingresar en `/etc/apache2/users` y crear un archivo que tenga el nombre de nuestro usuario y la extensión `.conf`.

En mi caso sería así:

{% highlight bash %}
cd /etc/apache2/users
nano ssanchez.conf
{% endhighlight %}

A este archivo le agregamos las siguientes líneas:

{% highlight bash %}
<Directory "direccion-de-la-carpeta">
AllowOverride All
Options Indexes MultiViews FollowSymLinks
Require all granted
</Directory>
{% endhighlight %}

> Recuerde cambiar `direccion-de-la-carpeta` por la dirección de SU carpeta. En mi caso ya vimos que es `/Users/ssanchez/Sites/`.

Finalmente hay que modificar los permisos del archivo y reiniciar Apache. Nuevamente uso el nombre de _mi_ archivo como ejemplo.

{% highlight bash %}
chmod 644 ssanchez.conf
apachectl restart
{% endhighlight %}

Ahora el contenido de `Sites` es accesible desde la URL: `http://localhost/~ssanchez/`

## Habilitar PHP para Apache

Hay que editar el archivo `httpd.conf` de Apache. La recomendación es realizar una copia de respaldo antes de hacer cualquier cambio.

{% highlight bash %}
cd /etc/apache2/
cp httpd.conf httpd.conf.bak
{% endhighlight %}

Para modificar el archivo se puede usar cualquier editor disponible desde la consola, como `vi` o `nano`.

{% highlight bash %}
nano httpd.conf
{% endhighlight %}

La idea es buscar la línea que carga el módulo de PHP, y remover el comentario (símbolo `#`) para que quede de la siguiente manera:

{% highlight bash %}
LoadModule php5_module libexec/apache2/libphp5.so
{% endhighlight %}

Luego de salvar el archivo con los cambios, salimos nuevamente a la consola y reiniciamos Apache.

{% highlight bash %}
apachectl restart
{% endhighlight %}

Para confirmar que PHP está funcionando se puede crear un archivo `phpinfo.php` que ejecute el comando `phpinfo()`, y colocarlo en la carpeta raíz de Apache.

<!-- @TODO: Agregar artículos sobre el archivo phpinfo.php y la carpeta raíz de Apache en Mac. -->

Si todo está bien, la información de PHP estará disponible en [http://localhost/phpinfo.php](http://localhost/phpinfo.php).

Al terminar esta parte es recomendable salir del modo _root_ con el comando `exit`.

## Instalar MySQL

Para instalar MySQL nada más hay que [descargar el paquete DMG](http://dev.mysql.com/downloads/mysql/) y ejecutar el procedimiento estándar. Por ejemplo, instalar MySQL 2.6.26 en OS X superior a 10.9 (Mavericks y Yosemite), el archivo requerido es `mysql-5.6.26-osx10.9-x86_64.dmg`.

> En caso que ya tenga una versión previa de MySQL, deberá seguir un [procedimiento de actualización](http://coolestguidesontheplanet.com/upgrade-mysql-database-5-5-5-6-osx-10-8-mountan-lion/) <!-- @TODO: verificar esto --> en lugar de instalar el DMG.

Luego de que la instalación está completa hay que editar la variable de usuario `$PATH` para que los comandos de MySQL estén disponibles desde la consola. Abrimos una terminal, y _SIN entrar como root_ ejecutamos este comando:

{% highlight bash %}
export PATH=/usr/local/mysql/bin:$PATH
{% endhighlight %}

Esto simplemente agrega la dirección `/usr/local/mysql/bin` a la lista de carpetas que `BASH` revisa cuando se le solicita ejecutar un comando.

## Conectar PHP y MySQL

Debemos estar seguros que PHP y MySQL pueden comunicarse entre ellos. Para eso la forma más directa es la siguiente:

{% highlight bash %}
cd /var
mkdir mysql
cd mysql
ln -s /tmp/mysql.sock mysql.sock
{% endhighlight %}

## ¿Y ahora qué?

Hay otras configuraciones de Apache que uno quizá podría querer modificar, pero no nos vamos a meter en eso por ahora.

Lo que sí sería más interesante y práctico para trabajar en desarrollo de proyectos localmente, es la creación de [Virtual Hosts](/virtual-hosts-en-mac).

---
Enlaces para referencias adicionales:

* [Blog de Jason McCreary](http://jason.pureconcepts.net/2014/11/install-apache-php-mysql-mac-os-x-yosemite/).
* [Coolest Guides on the Planet](http://coolestguidesontheplanet.com/upgrade-mysql-database-5-5-5-6-osx-10-8-mountan-lion/).
* [TechTastico](http://techtastico.com/post/instalar-apache-php-mysql-mavericks/).
