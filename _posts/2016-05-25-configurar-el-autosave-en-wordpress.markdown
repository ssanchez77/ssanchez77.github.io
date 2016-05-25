---
layout: post
title: "Configurar el Autosave en Wordpress"
permalink: configurar-el-autosave-en-wordpress
date: 2016-05-25 17:08:25
comments: true
categories:
- wordpress
---

Por defecto Wordpress viene con una característica que puede resultar un poco molesta: no hay límite para los borradores que se guardan automáticamente en la base de datos.

Cada cierto tiempo, el sistema guarda una copia (borrador) del post que se está editando, y si uno no toma precauciones pronto puede tener su base de datos llena de información basura.

Para tener control sobre esto, basta con editar el archivo `wp-config.php` y agregar algunas líneas de código.

<!--more-->

La característica de Autosave se puede deshabilitar completamente si se utiliza: `define('WP_POST_REVISIONS',false);`.

Si se desea mantener el Autosave activo, pero definir un máximo de copias que se almacenarán en la base de datos, se tiene la opción `define('WP_POST_REVISIONS', $num);` donde $num es la cantidad máxima de copias deseadas.

Para controlar cada cuánto se hace un Autosave, se puede usar `define('AUTOSAVE_INTERVAL', $num);` en donde $num es el periódo en segundos.

Lo recomendable es realizar este trabajito antes de empezar a publicar, pero también hay formas de limpiar la base de datos luego de haberse llenado de borradores viejos.

---

Fuentes de referencia:

* [Blog de Marc Witteveen](http://marcwitteveen.com/wordpress/limit-disable-wordpress-revisions/).
* [Creative Dev](http://www.thecreativedev.com/how-to-configure-wordpress-post-autosave-interval/).
* [Mundo Wordpress](http://www.mundowordpress.net/desactivar-el-autoguardado-de-wordpress/).
