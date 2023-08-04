## Nivel 2

Con este paso, agregarás un nuevo nivel al juego al que el jugador puede acceder simplemente presionando un botón. Después, puedes cambiar tu código para hacer que necesite un cierto número de puntos, o algo más, para llegar.

### Pasando al siguiente nivel

--- task ---

Primero, crea un nuevo objeto como un botón, ya sea añadiendo uno de la biblioteca o dibujando el tuyo propio. Hice un poco de ambas cosas y este fue el resultado:

![El objeto botón para cambiar niveles](images/nivelButton.png)

--- /task ---

--- task ---

Ahora, el código para este botón es inteligente: está diseñado para que cada vez que hagas clic en él te lleve al siguiente nivel, sin importar cuántos niveles haya.

Añade estos scripts a tu objeto **Botón**. Necesitarás crear algunas variables mientras lo haces.

```blocks3
+    when green flag clicked
+    set [nivel-máximo v] to [2]
+    set [nivel-mínimo v] to [1]
+    set [nivel-actual v] to [1]
```

```blocks3
+    when this sprite clicked
+    change [cnivel-actual v] by (1)
+    if <(nivel-actual) > (nivel-máximo ::variables)> then
        set [nivel-actual v] to (nivel-mínimo ::variables)
    end
+    broadcast [limpieza-coleccionable v]
+    broadcast (join [nivel-](nivel-actual))
```

--- /task ---

¿Puedes ver cómo el programa usará las variables que creaste?

+ `nivel-máximo`{:class="block3variables"} almacena el nivel más alto
+ `nivel-mínimo`{:class="block3variables"} almacena el nivel más bajo
+ `nivel-actual`{:class="block3variables"} almacena el nivel en el que se encuentra el jugador en este momento

Todos estos deben ser configurados por el programador \(¡tú!\), de forma que si agregas un tercer nivel, no te olvides de cambiar el valor de `nivel-máximo`{:class="block3variables"}! `nivel-mínimo`{:class="block3variables"} nunca tendrá que cambiar, por supuesto.

Los mensajes se utilizan para indicar a los otros objetos qué nivel mostrar, y para limpiar los coleccionables cuando comienza un nuevo nivel.

### Haz que los objetos reaccionen

#### El objeto **Coleccionable**

¡Ahora tienes que conseguir que los otros objetos respondan a estos mensajes! Comienza con el más fácil: limpiar todos los coleccionables.

--- task ---

Agrega el siguiente código al script del objeto **Coleccionable** para decirle a todos sus clones que se deben `ocultar`{:class="block3vlooks"} cuando reciban el mensaje de limpieza:

```blocks3
+    when I receive [limpieza-coleccionable v]
+    hide
```

--- /task ---

Dado que una de las primeras cosas que hace cualquier clon nuevo es mostrarse, ¡no tienes que preocuparte por des-ocultar los coleccionables!

#### El objeto **Plataformas**

Ahora para cambiar el objeto **Plataformas**. Puedes diseñar tu propio nuevo nivel más tarde si lo deseas, pero por ahora usemos el que ya he incluido — ¡verás por qué en el siguiente paso!

--- task ---

Añade este código al objeto **Plataformas**:

```blocks3
+    when I receive [nivel-1 v]
+    switch costume to [nivel 1 v]
+    show
```

```blocks3
+    when I receive [nivel-2 v]
+    switch costume to [nivel 2 v]
+    show
```

--- /task ---

Este recibe los mensajes `unidos`{:class="block3operators"} de `nivel-`{:class="block3variables"} y `nivel-actual`{:class="block3variables"} que el objeto **Botón** envía, y responde cambiando el disfraz de **Plataformas**.

#### El objeto **Enemigo**

--- task ---

En el script del objeto **Enemigo**, solo asegúrate de que el objeto desaparezca cuando el jugador entre al nivel 2, así:

```blocks3
+    when I receive [nivel-1 v]
+    show
```

```blocks3
+    when I receive [nivel-2 v]
+    hide
```

--- /task ---

Si lo prefieres, puedes hacer que el enemigo se mueva a otra plataforma. En ese caso, usarías un bloque de `ir a`{:class="block3motion"} en lugar de los bloques de `mostrar`{:class="block3looks"} y `ocultar`{:class="block3looks"}.

### Haz que el **Personaje del jugador** aparezca en el lugar correcto

Cada vez que comienza un nuevo nivel, el objeto de **Personaje del jugador** necesita ir al lugar correcto para ese nivel. Para que esto suceda, debes cambiar de dónde el objeto obtiene sus coordenadas cuando aparece por primera vez en el escenario. Por el momento, hay valores fijos de `x` e `y` en el código.

--- task ---

Comienza creando variables para las coordenadas iniciales: `iniciar-x`{:class="block3variables"} e `iniciar-y`{:class="block3variables"}. Luego, insértalas al bloque `ir a`{:class="block3motion"} en el bloque de `reiniciar-personaje`{:class="block3myblocks"} de **Mis bloques** en lugar de los valores fijos de `x` e `y`:

```blocks3
    define reset-character
    set [puede-saltar v] to [true]
    set [x-speed v] to [0]
    set [y-speed v] to [-0]
+    go to x: (iniciar-x) y: (iniciar-y)
```

--- /task ---

--- task ---

Luego, para cada mensaje que anuncie el inicio de un nivel, configure las coordenadas `iniciar-x`{:class="block3variables"} e `iniciar-y`{:class="block3variables"} en respuesta, y agregue una **llamada** para `reiniciar-personaje`{:class="block3myblocks"}:

```blocks3
+    when I receive [nivel-1 v]
+    set [iniciar-x v] to [-183]
+    set [iniciar-y v] to [42]
+    reset-character :: custom
```

```blocks3
+    when I receive [nivel-2 v]
+    set [iniciar-x v] to [-218]
+    set [iniciar-y v] to [-143]
+    reset-character :: custom
```

--- /task ---

### Iniciar en el Nivel 1

También debes asegurarte de que cada vez que alguien comienza el juego, el primer nivel que juega es el nivel 1.

--- task ---

Ve al script de `reiniciar-juego`{:class="block3myblocks"} y elimina la llamada para `reiniciar-personaje`{:class="block3myblocks"}. En su lugar, envía el `nivel-mínimo`{:class="block3variables"}. El código que ya has agregado con esta tarjeta configurará las coordenadas iniciales correctas para el objeto **Personaje del jugador**, y también llamará a `reiniciar-personaje`{:class="block3myblocks"}.

```blocks3
    define reset-game
    set rotation style [left-right v]
    set [altura-del-salto v] to [15]
    set [gravedad v] to [2]
    set [x-speed-adjuster v] to [1]
    set [y-speed-adjuster v] to [1]
    set [vidas v] to [3]
    set [puntos v] to [0]
+    broadcast (join [nivel-](nivel-mínimo ::variables))
```

--- /task ---

--- collapse ---
---
title: Reiniciar el Personaje del jugador versus reiniciar el juego
---

Observa que el primer bloque en el script de bandera verde del objeto **Personaje del jugador** es una llamada al bloque `reiniciar-juego`{:class="block3myblocks"} de **Mis bloques**.

Este bloque configura todas las variables para un nuevo juego y luego llama al bloque `reiniciar-jugador`{:class="block3myblocks"} de **Mis bloques**, que vuelve a colocar al personaje en su posición inicial correcta.

Tener el código de `reiniciar-personaje`{:class="block3myblocks"} en su propio bloque separado de `reiniciar-juego`{:class="block3myblocks"} te permite restablecer el personaje a diferentes posiciones **sin** tener que reiniciar todo el juego.

--- /collapse ---