## Nivel 2

Con este paso, vas a añadir un nuevo nivel al juego al que el jugador puede llegar pulsando un botón. Después, puedes cambiar tu código para hacer que necesiten un cierto número de puntos, o alguna otra cosa, para cambiar de nivel.

### Pasando al siguiente nivel

\--- task \---

Primero, crea un nuevo objeto como un botón, ya sea añadiendo uno de la biblioteca o dibujando el tuyo propio. Hice un poco de ambos y se me ocurrió esto:

![El objeto botón para cambiar niveles](images/levelButton.png)

\--- /task \---

\--- task \---

Ahora, el código para este botón es inteligente: está diseñado para que cada vez que hagas clic te lleve al siguiente nivel, no importa cuántos niveles haya.

Añade estos scripts a tu objeto **Botón**. Necesitarás crear algunas variables para hacerlo.

```blocks3
+    when green flag clicked
+    set [max-level v] to [2]
+    set [min-level v] to [1]
+    set [current-level v] to [1]
```

```blocks3
+    when this sprite clicked
+    change [current-level v] by (1)
+    if <(current-level) > (max-level ::variables)> then
        set [current-level v] to (min-level ::variables)
    end
+    broadcast [collectable-cleanup v]
+    broadcast (join [level-](current-level))
```

\--- /task \---

¿Puedes ver cómo el programa usará las variables que creaste?

+ `nivel-max`{:class="block3variables"} almacena el nivel más alto
+ `nivel-min`{:class="block3variables"} almacena el nivel más bajo
+ `nivel-actual`{:class="block3variables"} almacena el nivel en el que está el jugador ahora mismo

Todos estos deben ser configurados por el programador \ (¡tú! \), así que si agregas un tercer nivel, ¡no olvides cambiar el valor de `nivel-max`{:class="block3variables"}! Por supuesto, `nivel-min`{:class="block3variables"} nunca tendrá que cambiar.

Las emisiones se utilizan para decir a los otros objetos qué nivel mostrar, y para limpiar los coleccionables cuando comienza un nuevo nivel.

### Haz que los objetos reaccionen

#### El objeto **Coleccionable**

¡Ahora tienes que conseguir que los otros objetos respondan a estas transmisiones! Comienza con el más fácil: limpiar todos los coleccionables.

\--- task \---

Añade el siguiente código a los scripts del objeto**Coleccionable** para decirle a todos tus clones que se `escondan`{:class="block3vlooks"} cuando reciban la transmisión de limpieza:

```blocks3
+    when I receive [collectable-cleanup v]
+    hide
```

\--- /task \---

Como una de las primeras cosas que hace un clon nuevo es mostrarse a sí mismo, ¡no tienes que preocuparte por desocultar los coleccionables!

#### El objeto **plataformas**

Ahora para cambiar el objeto **plataformas**. Puedes diseñar tu propio nivel más tarde si quieres pero por ahora vamos a usar el que ya he incluido, ¡verás por qué en el siguiente paso!

\--- task \---

Añade este código al objeto **plataformas**:

```blocks3
+    when I receive [level-1 v]
+    switch costume to [Level 1 v]
+    show
```

```blocks3
+    when I receive [level-2 v]
+    switch costume to [Level 2 v]
+    show
```

\--- /task \---

Recibe los mensajes `unidos`{:class="block3operators"} de `nivel-`{:class="block3variables"} y `nivel-actual`{:class="block3variables"} que envía el objeto </strong>botón**, y responde cambiando el disfraz **Plataformas**.</p> 

#### El objeto **Enemigo**

\--- task \---

En el script del objeto**Enemigo**, asegúrate de que el objeto desaparezca cuando el jugador entre en el nivel 2, así:

```blocks3
+    when I receive [level-1 v]
+    show
```

```blocks3
+    when I receive [level-2 v]
+    hide
```

\--- /task \---

Si lo prefieres, puedes hacer que el enemigo se mueva a otra plataforma. En ese caso, usarías un bloque `ir a`{:class="block3motion"} en lugar de los bloques `mostrar`{:class="block3looks"} y `ocultar`{:class="block3looks"}.

### Haz que el **personaje del jugador** aparezca en el lugar correcto

Cada vez que comienza un nuevo nivel, el objeto **personaje del jugador** debe ir al lugar adecuado para ese nivel. Para que esto ocurra, necesitas cambiar la parte donde el objeto obtiene sus coordenadas en el momento en que aparece por primera vez en el escenario. Por el momento, hay valores fijos de `x` e `y` en tu código.

\--- task \---

Empieza por crear variables para las coordenadas iniciales: `x-inicio`{:class="block3variables"} e `y-inicio`{:class="block3variables"}. Luego insértalas en el bloque `ir a`{:class="block3motion"} en el bloque `recomenzar-personaje`{:class="block3myblocks"} **Mis bloques** en lugar de los valores fijos `x` e `y`:

```blocks3
    define reset-character
    set [can-jump v] to [true]
    set [x-speed v] to [0]
    set [y-speed v] to [-0]
+    go to x: (start-x) y: (start-y)
```

\--- /task \---

\--- task \---

Luego para cada transmisión que anuncia el comienzo del nivel, como respuesta establece las coordenadas de `x-inicio`{:class="block3variables"} e `y-inicio`{:class="block3variables"}, y añade una **llamada** a `recomenzar-personaje`{:class="block3myblocks"}:

```blocks3
+    when I receive [level-1 v]
+    set [start-x v] to [-183]
+    set [start-y v] to [42]
+    reset-character :: custom
```

```blocks3
+    when I receive [level-2 v]
+    set [start-x v] to [-218]
+    set [start-y v] to [-143]
+    reset-character :: custom
```

\--- /task \---

### Comenzando en el nivel 1

También necesitas asegurarte de que cada vez que alguien comienza el juego, el primer nivel que juegan es el nivel 1.

\--- task \---

Ve al script `recomenzar-juego`{:class="block3myblocks"} y elimina la llamada a `recomenzar-personaje`{:class="block3myblocks"}. En su lugar, transmite el `nivel-min`{:class="block3variables"}. El código que ya has añadido con esta tarjeta configurará las coordenadas iniciales correctas para el **personaje del jugador**, y también llama a `recomenzar-personaje`{:class="block3myblocks"}.

```blocks3
    define reset-game
    set rotation style [left-right v]
    set [jump-height v] to [15]
    set [gravity v] to [2]
    set [x-speed-adjuster v] to [1]
    set [y-speed-adjuster v] to [1]
    set [lives v] to [3]
    set [points v] to [0]
+    broadcast (join [level-](min-level ::variables))
```

\--- /task \---

## \--- collapse \---

## title: Reiniciar el personaje del jugador versus reiniciar el juego

Ten en cuenta que el primer bloque del script de bandera verde del **personaje del jugador** es una llamada al bloque `recomenzar-juego`{:class="block3myblocks"} **Mis bloques**.

Este bloque configura todas las variables para un nuevo juego y luego llama al bloque `recomenzar-personaje`{:class="block3myblocks"} **Mis bloques** que coloca al personaje de nuevo en su posición de partida correcta.

Tener el código `recomenzar-personaje`{:class="block3myblocks"} en su propio bloque separado de `recomenzar-juego`{:class="block3myblocks"} te permite restablecer el personaje a diferentes posiciones **sin tener que** reiniciar todo el juego.

\--- /collapse \---