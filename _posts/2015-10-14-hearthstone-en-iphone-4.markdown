---
layout: post
title:  "Hearthstone en iPhone 4"
permalink: hearthstone-en-iphone-4
date:   2015-10-14 21:47:25
comments: true
categories:
- ios
- juegos
---

No soy muy aficionado a los videojuegos, a menos que sean de Blizzard...

Cuando estaba en el Instituto Tecnológico era adicto a Warcraft y más adelante el vicio fue por culpa de Starcraft. Con todo nunca fui muy artista: siempre me tarreaban todo.

Recientemente volví a revisar qué cosas nuevas habían hecho, según yo con cuidado para no volver a enviciarme, pero fue inevitable. Me encantó Hearthstone y ahora estoy empezando a jugar Heroes of the Storm.

Hearthstone está disponible para iPhone. Yo tengo un iPhone 4 que adquirí hace unos años cuando estaba aprendiendo a desarrollar aplicaciones para iOS. Nunca sentí necesidad de actualizarme a un modelo más reciente, y además no tengo plata. Incluso hasta hace un par de meses todavía estaba corriendo iOS 6.2.

Cuando finalmente decidí probar iOS 7.1 decidí que era un buen momento para instalar el jueguito. ¡Cuál fue mi sorpresa que luego de descargarlo, instalarlo y correrlo, me dice que sólo puede funcionar en iPhone 4S o superior!

> ¡Me awuevás!

Bueno, tenía que encontrar una forma de correrlo en mi perol de iPhone 4, así que me puse a buscar.

<!--more-->


Encontré que una Aplicación llamada `Anywhere!` permite virtualizar la plataforma sobre la cual una App "piensa" que está ejecutándose. Es decir, que uno puede engañar a Hearthstone para hacerlo creer que está corriendo sobre un iPhone 4S.

Sin embargo `Anywhere!` sólo se puede instalar si al dispositivo se le ha aplicado el `Jailbreak`.

## Jailbreak

Según Wikipedia:

> Se denomina Jailbreak (literalmente: "fuga de la cárcel", en español: "destraba") al proceso de suprimir algunas de las limitaciones impuestas por Apple en dispositivos que utilicen el sistema operativo iOS mediante el uso de kernels modificados.

La idea es permitir al usuario "descargar aplicaciones, extensiones y temas que no estén disponibles a través de la App Store oficial". O sea, todo lo que debe funcionar por medio de los canales oficiales sigue igual, pero adicionalmente se puede hacer instalaciones y configuraciones no oficiales.

¿Cómo rayos se hace eso? Pues con mucho cuidado y sabiendo que la integridad del dispositivo está en juego. Si algo malo pasa en el proceso, salado.

> Como medida preventiva, en caso que un incidente durante el Jailbreak nos dejara el teléfono inservible, es recomendable hacer un backup completo usando para ello la opción disponible en iTunes. Esta podría ser la única forma de resucitarlo si en el proceso se nos muere.

Lo que queremos lograr por medio del `Jailbreak` es tener en nuestro iPhone una aplicación llamada [Cydia](https://cydia.saurik.com/), que es el equivalente no oficial de la App Store, por medio de la cual vamos a conseguir todos estos recursos que no están disponibles a través de Apple.

## Pangu

Por dicha para instalar `Cydia` ya existe un software para Windows y para Mac, que uno descarga y ejecuta, y que se encargará de detectar el iPhone y guiarnos paso a paso. El nombre de este programa es [Pangu](http://en.pangu.io/), y está disponible para hacer `Jailbreak` de iOS 7, 8 y 9.

En mi caso, tuve que hacer varios intentos hasta que finalmente el procedimiento llegó a su punto final. Al principio hubo un timeout porque no me había dado cuenta que me estaba pidiendo realizar un ajuste manual en la configuración del teléfono (en la fecha).

Luego volvió a fallar porque el iPhone tardó mucho en reiniciarse. Como al tercer o cuarto intento ya todo salió bien, y `Cydia` me apareció entre las Apps disponibles. Lo bueno fue que no hubo ningún problema con el sistema cuando el proceso falló, así que al menos en mi caso, `Pangu` me funcionó de lo más bien.

## Anywhere! con Cydia

Una vez que ya pude abrir `Cydia`, busqué `Anywhere!` y no lo pude encontrar por ninguna parte (¡qué ironía!...). Luego de travesear un par de cosas, hice el refrescamiento (Actualizar) de las Fuentes, y ahora sí, ya encontré `Anywhere!`.

De forma similar a lo que me había pasado con `Pangu`, tuve que armarme de paciencia, porque el procedimiento de instalación de `Anywhere!` no funcionó bien las primeras veces. Creo que era un problema del servidor o repositorio en donde se hacía la consulta para descargarlo. Un par de días más tarde repetí el procedimiento y esta vez sí se instaló.

Al abrir `Anywhere!` lo que se topa uno es un mapa. Abajo entre los Tabs hay una opción llamada `Virtual Machine` que debemos activar y luego ir a `Modify the iPhone series models` que nos va a mostrar una lista de dispositivos. Al seleccionar cualquiera de ellos (por ejemplo iPhone 4S) aparece la lista de las Apps con las que cuenta el teléfono. Evidentemente para mi caso busqué HearthStone y la seleccioné, para que quedara asignado a la virtualización como iPhone 4S.

Una vez listo eso, HearthStone inicia y se puede jugar. Es bastante lento, pero es jugable, y para todos los efectos lo más importante (y divertido) fue el procedimiento por el cual se logró lo que no se podía hacer "oficialmente".

La verdad es que casi siempre juego desde mi Mac, pero algunas veces antes de dormir, le doy unas cuantas partidas en el iPhone. ¿Quién dijo que no se podía?...

---

Fuentes de referencia:

* [Conversación en ReddIt](https://www.reddit.com/r/jailbreak/comments/32xly5/question_how_to_get_hearthstone_to_work_on_iphone/).
* [Otra conversación en ReddIt](https://www.reddit.com/r/hearthstone/comments/32ttx4/hearthstone_is_playable_on_iphone_4_but_jailbreak/).
