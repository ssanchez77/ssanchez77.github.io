---
layout: post
title:  "Virtual Host en Mac"
permalink: virtual-hosts-en-mac
date:   2015-10-01 10:35:24
comments: true
categories:
- general
- osx
---

Al instalar Apache localmente, nuestra computadora puede ser utilizada como servidor web. Por lo general esto se hace con el fin de desarrollar, no como hospedaje final de nuestros sitios, pues para eso resulta mucho más barato y práctico utilizar servicios de hospedaje comerciales.

Una vez configurado el servidor local, el directorio raíz de sistema será accesible por medio de la dirección [http://localhost/](http://localhost/). Si configuramos el directorio raíz para `usuario`, este se encontrará disponible en el URL `http://localhost/~usuario`. Sea cual sea nuestra forma de configurar el servidor web, a partir del directorio raíz podemos crear carpetas para cada uno de nuestros proyectos.

Pero, ¿qué pasa si se está trabajando con alguna característica que requiere ser probada bajo el nombre del dominio final que tendrá el sitio cuando esté publicado? ¿O quizá simplemente por un asunto de orden, queremos ver nuestros proyectos en su correspondiente dominio durante las pruebas?

<!--more-->

Los virtual hosts nos permiten utilizar nuestro servidor web para atender dominios locales (sólo disponibles para nosotros).

> Antes de configurar los Virtual Host en Yosemite, Mavericks o Mountain Lion, es necesario tener al menos [Apache](/amp-basico-en-osx) funcionando en nuestro ambiente de desarrollo local.

El primer paso es habilitar los vhosts desde el archivo de configuración de Apache `httpd.conf`.

{% highlight bash %}
sudo nano /etc/apache2/httpd.conf
{% endhighlight %}

Hay que quitar el comentario de la siguiente línea:

{% highlight bash %}
# Virtual hosts

Include /private/etc/apache2/extra/httpd-vhosts.conf
{% endhighlight %}

Esto nos permitirá utilizar el archivo `httpd-vhosts.conf` donde se definen los vhosts, así que el paso siguiente es editarlo:

{% highlight bash %}
sudo nano /etc/apache2/extra/httpd-vhosts.conf
{% endhighlight %}

Un ejemplo de configuración de los vhosts es el siguiente:

{% highlight bash %}
<VirtualHost *:80>
    ServerName sandbox.d7
    ServerAlias sandbox.d7
    DocumentRoot "/Users/ssanchez/Sites/sandbox.d7"
    ErrorLog "/private/var/log/apache2/sandbox.d7-error_log"
    CustomLog "/private/var/log/apache2/sandbox.d7-access_log" common
    ServerAdmin direccion-del-administrador@mi-dominio.com
        <Directory "/Users/ssanchez/Sites/sandbox.d7">
            Options Indexes FollowSymLinks
            AllowOverride All
            Order allow,deny
            Allow from all
        </Directory>
</VirtualHost>
{% endhighlight %}

En el caso anterior estoy configurando el dominio `sandbox.d7` para que al llamarlo desde un navegador, accese al contenido de mi carpeta `/Users/ssanchez/Sites/sandbox.d7`, en donde tengo los archivos de mi sitio de pruebas.

Sin embargo se requiere un paso más: hay que asociar este dominio con el IP, en el archivo de hosts.

{% highlight bash %}
sudo nano /etc/hosts
{% endhighlight %}

En mi ejemplo tendríamos que agregar esto:

{% highlight bash %}
# Sandboxes

127.0.0.1 sandbox.d7
{% endhighlight %}

Finalmente, hay que reiniciar Apache:

{% highlight bash %}
sudo apachectl restart
{% endhighlight %}

De esta manera hemos ligado el dominio `sandbox.d7` al IP de localhost, y al tener configurado el virtualhost en la carpeta `/Users/ssanchez/Sites/sandbox.d7`, podremos ver este contenido en el navegador al ingresar a `http://sandbox.d7`.

Esos son los pasos básicos que yo utilizo, sin embargo hay muchas opciones de configuración para casos especiales.

---
Enlaces de referencia:

* [Coolest Guides on the Planet](http://coolestguidesontheplanet.com/set-virtual-hosts-apache-mac-osx-10-10-yosemite/).
* [Tutoriales de Digital Ocean](https://www.digitalocean.com/community/tutorials/como-configurar-virtual-host-de-apache-en-ubuntu-14-04-lts-es).
* [Tutoriales de Styde](https://styde.net/como-crear-virtual-hosts-con-apache-para-linux-y-mac/).
