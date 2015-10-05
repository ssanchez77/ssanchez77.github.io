---
layout: post
title:  "Descargar archivos con cURL"
permalink: descargar-archivos-con-curl
date:   2015-10-05 12:20:44
comments: true
categories:
- general
---

Posiblemente le ha pasado que está descargando un archivo desde su navegador favorito y cuando va por el 97% falla la conexión. Intenta volver a iniciar la descarga y... ¡No puede ser! ¡Volvió a empezar desde 0%!

> ¡Murphy, eres despreciable!

Peor aún si lo que estamos bajando es la imagen de una máquina virtual, el installador de una distribución de Linux, un disco de [Ektoplazm](http://www.ektoplazm.com/), o cualquier cosa que pese más de 100 MB.

¿Existe una manera fácil de reiniciar la descarga de un archivo sin mucho enredo? ¡Definitivamente! Y todo gracias a la todopoderosa consola y a un comando llamado `cURL`.

<!--more-->

# ¿Qué es cULR?

Es una herramienta software para transferencia de archivos con sintaxis URL. Es decir, sirve para realizar acciones sobre archivos que hay en URLs de Internet. Soporta los protocolos más comunes, como http, ftp, https, etc.

El principal propósito y uso para cURL es automatizar transferencias de archivos o secuencias de operaciones no supervisadas.

cURL existe como un comando disponible desde el intérprete (consola o terminal) y también como una librería (libcurl) que se puede usar desde lenguajes de programación como PHP.

Para nuestros efectos, lo que nos interesa de `cURL` es que sirve para encontrar un archivo cuya URL conocemos, y descargarlo a nuestra computadora.

# Instalando cURL en OSX

Si usted tiene OSX Yosemite, mala suerte: ya `cURL` viene instalado, así que no hay más diversión por este lado.

En caso que quiera ensuciarse las manos, puede intentar descargarlo desde el [sitio oficial](http://curl.haxx.se/download.html∫) y compilarlo nuevamente.

Para conocer la versión de `curl` que tiene instalada, simplemente ejecutamos esto desde la lína de comandos:

{% highlight bash %}
curl -V
{% endhighlight %}

# Ahora sí, a descargar nuestro archivote

Aunque `cURL` tiene chorromil [parámetros / opciones](http://curl.haxx.se/docs/manpage.html), nada más vamos a utilizar dos:

**-O, --remote-name**

Escribir el archivo local con el mismo nombre que se estaba usando en el servidor remoto.

**-C, --continue-at**

Continúa/Retoma una transferencia previa, dado un offset (número exacto de bytes que deben ser saltados para retomar la descarga). Si se usa la opción `-C -`, el comando automáticamente detectará desde dónde debe proseguir la descarga.

Por ejemplo: para descargar el disco [Chronos – Animo](http://www.ektoplazm.com/free-music/chronos-animo) de DJ Basilisk, lo que debo hacer es encontrar el URL del archivo.

Una vez que sabemos donde está en link para descargarlo, desde Chrome se hace clic derecho y luego seleccionando `Copy Link Address`. Con ese path, vamos a la terminal y usamos el URL para empezar la descarga:

{% highlight bash %}
curl -OC - http://www.ektoplazm.com/files/Chronos%20-%20Animo%20-%202015%20-%20MP3.zip
{% endhighlight %}

Si en algún punto se corta la comunicación, simplemente volvemos a ejecutar el mismo comando, y `cURL` retomará el proceso en el punto donde quedó.

---

Fuentes de referencia:

* [Wikipedia](https://es.wikipedia.org/wiki/CURL).
* [Desarrollo Web](http://www.desarrolloweb.com/faq/que-es-curl.html).
* [Mac Tips](http://best-mac-tips.com/2012/02/05/resuming-broken-downloads/).
* [Documentación de Apple Developer](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/curl.1.html).
