## Perdiendo el juego

¡Lo primero es lo primero! Necesitas una forma de hacer que el juego termine cuando el jugador se ha quedado sin vidas. Por el momento eso no sucede.

Puede que hayas notado que el bloque `pierde`{:class="block3myblocks"} **Mis bloques** en el código del sprite **personaje de jugador** están vacíos. Vas a completar esto y configurar todas las piezas necesarias para crear una buena pantalla de "Fin del juego".

\--- task \---

Primero, encuentra el bloque `pierde`{:class="block3myblocks"} y complétalo con el siguiente código:

```blocks3
    define lose
+    stop [other scripts in sprite v] :: control stack
+    broadcast [game over v]
+    go to x:(0) y:(0)
+    say [Game over!] for (2) secs
+    stop [all v]
```

\--- /task \---

## \--- collapse \---

## title: ¿Qué hace este código?

Ahora, siempre que el bloque `pierde`{:class="block3myblocks"} se ejecuta, lo que hace es:

1. Detiene la física y otros códigos del juego que actúan sobre el **Personaje del Jugador**
2. Dice a todos los demás objetos que el juego ha terminado **transmitiendo** el mensaje `fin del juego`{: class = "block3events"} para que puedan responder y cambiar lo que están haciendo
3. Mueve el **personaje del jugador** al centro del escenario y hace que le diga al jugador que el juego ha terminado
4. Detiene todos los scripts del juego

\--- /collapse \---

Ahora necesitas asegurarte de que todos los objetos saben qué hacer cuando el juego termina, y cómo reiniciarse cuando el jugador inicia una nueva partida. **¡No olvides que cualquier nuevo objeto que añadas también puede necesitar código para esto!**

### Esconde las plataformas y bordes

\--- task \---

Comienza con los objetos más fáciles. Las **Plataformas** y **Bordes**, ambos necesitan código para aparecer cuando el juego comienza y desaparecer cuando reciben la transmisión `fin del juego`{: class = "block3events"}, así que añade estos bloques a cada uno de ellos:

```blocks3
+    when I receive [game over  v]
+    hide
```

```blocks3
+    when green flag clicked
+    show
```

\--- /task \---

### Detiene las estrellas

Ahora, si observas el código del objeto **Coleccionable**, verás que funciona **clonándose** a sí mismo. Es decir, hace copias de sí mismo que siguen las instrucciones especiales `al comenzar como clon`{:class="block3events"}.

Hablaremos más sobre lo que hace que los clones sean especiales cuando lleguemos al paso de hacer nuevos y diferentes coleccionables. Por ahora, lo que necesitas saber es que los clones pueden hacer **casi** todo lo que hace un objeto normal, incluyendo recibir `mensajes`{:class="block3events"}.

Mira cómo funciona el objeto **Coleccionable**. Fíjate si puedes entender algo de su código:

```blocks3
    when green flag clicked
    hide
    set [collectable-value v] to [1]
    set [collectable-speed v] to [1]
    set [collectable-frequency v] to [1]
    set [create-collectables v] to [true]
    set [collectable-type v] to [1]
    repeat until <not <(create-collectables) = [true]>>
        wait (collectable-frequency) secs
        go to x: (pick random (-240) to (240)) y: (179)
        create clone of [myself v]
    end
```

1. Primero, hace invisible el objeto original **Coleccionable** escondiéndolo
2. Luego configura las variables de control — volveremos a éstas más tarde
3. La variable `crear-coleccionables`{:class="block3variables"} es el interruptor de encendido / apagado para la clonación: el bucle crea clones si `crear-coleccionables`{: class = "block3variables"} es `true`, y no hace nada si no lo es

\--- task \---

Ahora configura un bloque para el sprite **Coleccionable** para que reaccione a la transmisión de `fin del juego`:

```blocks3
+    when I receive [game over v]
+    hide
+    set [create-collectables v] to [false]
```

\--- /task \---

Este código es similar al código que controla los objetos **Plataformas** y **Bordes**. La única diferencia es que también estás configurando la variable `crear-coleccionable`{:class="block3variables"} a `false` para que no se creen nuevos clones cuando termine el juego.

Ten en cuenta que puedes usar la variable `crear-coleccionables`{:class="block3variables"} ¡para pasar mensajes de una parte de tu código a otra!