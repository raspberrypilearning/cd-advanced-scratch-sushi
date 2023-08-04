## Perdiendo el juego

¡Primero lo primero! Necesitas una forma de terminar el juego cuando el jugador se ha quedado sin vidas. Por el momento eso no sucede.

Puede que hayas notado que el bloque `perder`{:class="block3myblocks"} de **Mis bloques** en el script para el objeto **Personaje del jugador** está vacío. Vas a completar esto y configurar todas las piezas necesarias para una buena pantalla de 'Fin del juego'.

--- task ---

Primero, encuentra el bloque `perder`{:class="block3myblocks"} y complétalo con el siguiente código:

```blocks3
    define perder
+    stop [otros programas en el objeto v] :: control stack
+    broadcast [fin del juego v]
+    go to x:(0) y:(0)
+    say [¡Fin del juego!] for (2) secs
+    stop [todos v]
```

--- /task ---

--- collapse ---
---
title: ¿Qué hace este código?
---

Siempre que el bloque `perder`{:class="block3myblocks"} se ejecuta, lo que hace es:

1. Detener la física y otros scripts del juego actuando en el **Personaje del jugador**
2. Decir a todos los otros objetos que el juego terminó **enviando** un mensaje `fin del juego`{:class="block3events"} al que pueden responder y cambiar lo que están haciendo
3. Mover al **Personaje del jugador** al centro de la pantalla y hacer que le digan al jugador que el juego ha terminado
4. Detener todos los scripts en el juego

--- /collapse ---

Ahora necesitas asegurarte de que todos los objetos sepan qué hacer cuando el juego haya terminado, y cómo reiniciarse a sí mismos cuando el jugador inicie una nueva partida. **¡No olvides que cualquier objeto nuevo que añadas también puede necesitar un código para esto!**

### Ocultar plataformas y bordes

--- task ---

Comienza con los objetos más sencillos. Los objetos **Plataformas** y **Bordes** necesitan código para aparecer cuando el juego comienza y desaparecer cuando reciben el mensaje de `fin del juego`{:class="block3events"}, así que añade estos bloques a cada uno de ellos:

```blocks3
+    when I receive [fin del juego  v]
+    hide
```

```blocks3
+    when green flag clicked
+    show
```

--- /task ---

### Detener las estrellas

Ahora, si miras el código del objeto **Coleccionable**, verás que funciona al **clonarse** a si mismo. Es decir, hace copias de sí mismo que siguen las instrucciones especiales de `al comenzar como clon`{:class="block3events"}.

Hablaremos más sobre lo que hace que los clones sean especiales cuando lleguemos al paso de hacer nuevos y diferentes coleccionables. Por ahora, lo que necesitas saber es que los clones pueden hacer **casi** todo lo que un objeto normal puede, incluyendo recibir `mensajes`{:class="block3events"}.

Mira cómo funciona el objeto **Coleccionable**. Comprueba si puedes entender algo de su código:

```blocks3
    when green flag clicked
    hide
    set [fin del juego v] to [1]
    set [velocidad-coleccionable v] to [1]
    set [frecuencia-coleccionable v] to [1]
    set [crear-coleccionables v] to [true]
    set [tipo-coleccionable v] to [1]
    repeat until <not <(crear-coleccionables) = [true]>>
        wait (frecuencia-coleccionable) secs
        go to x: (pick random (-240) to (240)) y: (179)
        create clone of [mí mismo v]
    end
```

1. Primero hace invisible el objeto **Coleccionable** original ocultándolo
2. Luego configura las variables de control; volveremos a estas más adelante
3. La variable `crear-coleccionables`{:class="block3variables"} es el interruptor de encendido/apagado para clonar: el bucle crea clones si `crear-coleccionables`{:class="block3variables"} es `verdadero`, y no hace nada si no lo es

--- task ---

Ahora configura un bloque en el objeto **Coleccionable** para que reaccione al mensaje `fin del juego`:

```blocks3
+    when I receive [fin del juego v]
+    hide
+    set [crear-coleccionables v] to [false]
```

--- /task ---

Este código es similar al código que controla los objetos **Plataformas** y **Bordes**. La única diferencia es que también estás configurando la variable `crear-coleccionables`{:class="block3variables"} a `falso` para que no se creen nuevos clones cuando llegue el 'fin del juego'.

¡Ten en cuenta que puedes usar la variable `crear-coleccionables`{:class="block3variables"} para pasar mensajes de una parte de tu código a otra!