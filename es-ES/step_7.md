## Añadiendo algo de competencia

Tu juego funciona y ahora puedes recoger puntos, obtener poderes especiales, y perder. ¡Estamos llegando a alguna parte! Quizás sería divertido añadir algo de competencia, pero ¿Qué tal incluir un personaje que se mueva un poco, pero que se supone que no debes tocar? Esto será similar a los enemigos en los juegos de plataformas tradicionales, como Super Mario, que nos han dado la inspiración para este juego.

\--- task \---

Primero, elige un objeto para añadir como enemigo. Debido a que nuestro personaje jugador es un gato, elegí un perro. Hay muchos otros objetos que podrías añadir. También renombré el objeto **Enemigo**, solo para aclararme las cosas.

Cambia el tamaño del objeto al tamaño correcto y colócalo en un lugar apropiado para comenzar. Así es como se ve el mío:

![El objeto enemigo perro](images/enemySprite.png)

\--- /task \---

\--- task \---

Escribe el código más fácil primero: configura su bloque para responder al mensaje `fin del juego`{:class="events"} para hacer que el enemigo desaparezca cuando el jugador pierda la partida.

```blocks3
+    when I receive [game over v]
+    hide
```

\--- /task \---

\--- task \---

Ahora necesitas escribir el código para lo que hace el enemigo. Usa mi código aquí, ¡pero considera añadir bits extra! (¿Qué pasa si pueden teletransportarse a diferentes plataformas? ¿Qué pasa si hay un poder que los haga moverse más rápido o más lento?)

```blocks3
+    when green flag clicked
+    show
+    set [enemy-move-steps v] to [5]
+    set rotation style [left-right v]
+    go to x: (-25) y: (-9)
+    forever
        move (enemy-move-steps) steps
        if <not <touching [Platforms v] ?>> then
            set [enemy-move-steps v] to ((enemy-move-steps) * (-1))
        end
     end
```

**Nota**: si simplemente arrastras el bloque `ir a`{:class="block3motion"} al panel de objetos y no cambias los valores `x` e `y`. ¡Serán los valores para la ubicación actual del objeto**Enemigo**!

¡El código en el bloque `si...entonces`{:class="block3control"} hará que el objeto gire cuando llegue al final de la plataforma!

\--- /task \---

Lo siguiente que necesitarás es que el jugador pierda una vida cuando su **personaje** toque el objeto **Enemigo**. También, necesitas asegurarte de que los objetos **dejen** de tocarse muy rápidamente, ya que de lo contrario el código que comprueba el toque seguirá ejecutándose y el jugador seguirá perdiendo la vida.

\--- task \---

Así es como lo hice, ¡pero puedes intentar mejorar este código! He modificado el bloque principal del sprite del **personaje del jugador**. Añade el nuevo código antes del bloque `si`{:class="block3control"} que comprueba si se te terminaron las vidas.

```blocks3
    when green flag clicked
    reset-game :: custom
    forever
        main-physics :: custom
        if <(y position) < [-179]> then
            hide
            reset-character :: custom
            change [lives v] by (-1)
            wait (0.05) secs
            show
        end
+        if <touching [Enemy v] ?> then
            hide
            go to x: (-187) y: (42)
            change [lives v] by (-1)
            wait (0.5) secs
            show
+        end
        if <(lives) < [1]> then
            lose :: custom
        end
    end
```

\--- /task \---

El nuevo código oculta el objeto **del personaje del jugador**, lo mueve de vuelta a su posición inicial, reduce la variable `vidas`{:class="block3variables"} en `1`y después de medio segundo hace que el objeto vuelva a aparecer.