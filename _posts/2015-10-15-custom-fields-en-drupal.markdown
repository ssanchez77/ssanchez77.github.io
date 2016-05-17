---
layout: post
title:  "Custom Fields en Drupal"
permalink: custom-fields-en-drupal
date:   2015-10-15 11:50:49
comments: true
categories:
- drupal
---

Este post también se podría haber llamado "Campos Personalizados en Drupal", lo cual sería una traducción correcta. Sin embargo lo dejé como "Custom Fields" porque en el código el término `field` se utiliza mucho, y creo que la explicación será más clara si simplemente lo dejamos como está en inglés.

Un `field` es un agregado que se le puede hacer a una entidad. Hablando de nodos, estos pueden tener título, fecha, descripción, etc. y cada uno de estos pedacitos de información es un `field`.

Drupal ya viene con gran cantidad de tipos de campo definidos en su core, y adicionalmente hay módulos que expanden las opciones según diferentes necesidades.

Pero como todo en el mundo de Drupal, llega el momento en que una situación se da donde ni los `fields` definidos en el core, ni los que encontramos en la comunidad, se ajustan a los requerimientos que tenemos.

Es entonces cuando tenemos que sentarnos a crear nuestros propios campos personalizados, o como se dice en el título `Custom Fields`.

<!--more-->

## Las tres partes de este asunto

Cuando queremos crear un `custom field` necesitamos reconocer y definir tres partes principales:

- La definición del campo para que Drupal lo reconozca.
- La creación del Widget, que es el elemento para administrarlo, es decir el componente gráfico de edición (generalmente un formulario).
- El formato con el cual se presentará la información a los visitantes del sitio web.

## Definición del field

Para que Drupal sepa que existe nuestro nuevo field, necesitamos hacérselo saber por medio de varios `hooks`.

Primeramente tenemos que indicarle cuál será la estructura de la tabla que guardará la información de las instancias de nuestro field en base de datos. Esto se hace implementando `hook_field_schema` en el archivo .install de nuestro módulo.

A continuación un ejemplo:

{% highlight php startinline=true %}
/**
 * Implements hook_field_schema().
 */
function demo_field_schema($field) {

  $schema = NULL;

  switch($field['type']) {
    case 'my_custom_field':
      $schema = array(
        'columns' => array (
          'my_textfield' => array(
            'type' => 'varchar',
            'length' => '255',
            'not null' => FALSE,
          ),
          'my_textarea' => array(
            'type' => 'text',
            'size' => 'big',
            'not null' => FALSE,
          ),
        ),
      );
      break;
  }

  return $schema;
}
{% endhighlight %}

Vamos a llamar a nuestro módulo hipotético `demo`, así que el nombre del hook quedar como `demo_field_schema`.

En el código anterior definimos que nuestro tipo de campo se llamará "my_custom_field", y el formulario para editarlo estará compuesto de dos elementos:

- Primeramente un textfield, para lo cual creamos una columna en base de datos que es un `varchar` de 255 caracteres, y que podría estar vacía (null).
- En segundo lugar tenemos un textarea, que requiere reservar una columna de tipo `text`, de tamaño `big`, y que también podría ser null.

Es importante definir las columnas tomando en cuenta el tipo de dato que tendrá cada elemento de nuestro custom field.

Este hook se carga cuando se instala el módulo `demo`, pero también cada vez que se guardan los settings de nuestro custom field cuando es utilizado por un tipo de contenido. Por esta razón, si hacemos un cambio y queremos verlo reflejado en la estructura de la base de datos, podemos ingresar a la edición del tipo de contenido, y de ahí a la edición del custom field, y guardarlo.

Sin embargo, esto es posible únicamente cuando la tabla está vacía, es decir, el etapa de pruebas. Luego que la tabla ya contiene datos, hacer cambios en el esquema y tratar de guardar el tipo de contenido producirá un error fatal en el sitio.

La única manera de actualizar el esquema de base de datos en ese caso es borrar el custom field de todos los tipos de contenido que lo usen, y volver a agregarlo, tomando en cuenta que la tabla se creará desde cero y todo lo que había en ella se pierde.

---
Enlaces de referencia:

* [Blog de Nicola Strappazzon](http://www.swapbytes.com/como-crear-un-campo-personalizado-en-drupal-7/#comment-108).
* [Artículo en ClikFocus](https://clikfocus.com/blog/how-set-custom-field-type-using-drupal-7-fields-api).
* [Blog de LevelTen Interactive](http://getlevelten.com/blog/ian-whitcomb/defining-custom-field-types-drupal).
* [Pregunta en StackOverflow](http://stackoverflow.com/questions/5705983/drupal-how-to-use-fieldsets-in-hook-field-widget-form).
