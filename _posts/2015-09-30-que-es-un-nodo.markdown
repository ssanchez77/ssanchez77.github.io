---
layout: post
title:  "¿Qué es un nodo?"
permalink: que-es-un-nodo
date:   2015-09-30 19:42:05
comments: true
categories:
- drupal
---

Una de las cosas que me costó entender al principio sobre Drupal es cómo se maneja el contenido. En Wordpress es muy fácil: hay artículos y hay páginas, y aunque tienen sus leves diferencias, no es muy complicado entender cómo se maneja uno y otro.

Sin embargo en Drupal el asunto del contenido se vuelve mucho más elemental, incluso un poco abstracto al inicio. Una vez que uno entiende el concepto de nodo y cómo utilizarlo, ya tiene la perspectiva para hacer muchas cosas interesantes. El asunto es que toma un tiempo lograr visualizar bien el concepto para poder aplicarlo.

<!--more-->

## Definición

Todo el contenido en un sitio web de Drupal se almacena y se maneja como "nodos" (en inglés "nodes"). Un nodo es cualquier pieza de contenido individual, como una página, una encuesta, un artículo, un tema dentro de un foro, o una entrada de un blog.

Los comentarios no son almacenados como nodos, pero siempre están conectados a uno. Al manejar todo el contenido como nodos, se logra la flexibilidad de crear nuevos tipos de contenido o modificar los existentes.

Una vez que se realiza un cambio en un tipo de contenido, todos los nodos de dicho tipo son afectados.

El concepto de nodo se presta para desarrollar prácticamente cualquier idea que uno desee: un nodo puede ser un producto, o un elemento dentro de un directorio telefónico, o un anuncio comercial.

Una vez que el tipo de contenido específico, para el propósito específico que el usuario necesita, está creado, lo que hay que hacer es crear nodos de ese tipo. Así tendremos muchos elementos que se ajustan a una descripción determinada.

Los nodos no guardan ninguna información de formato, únicamente el contenido, y es cuando el usuario consulta la información, que Drupal organiza y presenta los datos de la forma adecuada.

## nid

Conforme se van creando nodos, el sistema les asigna un número de identificación único, el nid.

Por defecto los nodos creados quedan disponibles para ser visualizados en el URL: `dominio-del-sitio/?q=node/uid`, donde "dominio-del-sitio" obviamente es el dominio del sitio que estamos creado, y "uid" se sustituye por el número del nodo que queremos ver.

---
Enlaces de referencia:

* [Sitio oficial de Drupal](https://www.drupal.org/documentation/modules/node).
* [Cursos Drupal](http://www.cursosdrupal.com/content/nodos).
