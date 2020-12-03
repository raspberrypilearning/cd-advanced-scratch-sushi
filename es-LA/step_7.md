## Añadiendo algo de competencia

Tu juego funciona y ahora puedes recoger puntos, obtener poderes especiales, y perder. ¡Estamos llegando a alguna parte! Quizás sería divertido añadir algo de competencia — ¿qué tal incluir un personaje que se mueve alrededor, pero que se supone que no debes tocar? Esto será similar a los enemigos en los juegos de plataformas tradicionales, como Super Mario, en el cual nos hemos inspirado aquí.

\--- task \---

Primero, elige un objeto para agregar como tu enemigo. Como nuestro personaje es un gato, yo he elegido a un perro. Sin embargo, hay muchos otros objetos que podrías añadir. También renombré el objeto **Enemigo**, solo para hacer las cosas más claras para mí.

Cambia el tamaño del objeto al tamaño correcto y colócalo en un lugar apropiado para comenzar. Así es como se ve el mío:

![El objeto perro enemigo](images/enemySprite.png)

\--- /task \---

\--- task \---

Escribe primero el código más fácil: configura su bloque para reaccionar al mensaje `fin del juego`{:class="events"} para hacer desaparecer al enemigo cuando el jugador pierde el juego.

```blocks3
+    when I receive [game over v]
+    hide
```

\--- /task \---

\--- task \---

Ahora necesitas escribir el código de lo que hace el enemigo. Usa mi código aquí, ¡pero considera añadir bits extra! (¿Y si pueden teletransportarse alrededor de diferentes plataformas? ¿Qué pasa si hay un potenciador que los haga moverse más rápido, o más lento?)

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

**Nota**: si solo arrastras el bloque `ir a`{:class="block3motion"} en el objeto y no cambias los valores `x` e `y`, ¡estos serán los valores para la ubicación actual del objeto **Enemigo**!

¡El código en el bloque `si...entonces`{:class="block3control"} hará que el objeto gire cuando llegue al final de la plataforma!

\--- /task \---

Lo siguiente que necesitarás es que el jugador pierda una vida cuando el **Personaje del jugador** toque el objeto **Enemigo**. Además, debes asegurarte de que los objetos **dejen** de tocarse realmente rápido, ya que de lo contrario el código que verifica el contacto seguirá ejecutándose y el jugador seguirá perdiendo vidas.

\--- task \---

Así es como lo hice, ¡pero puedes intentar mejorar este código! He modificado el bloque principal del objeto **Personaje del jugador**. Agrega el nuevo código antes del bloque `si`{:class="block3control"} que comprueba si te has quedado sin vida.

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

El nuevo código oculta el objeto **Personaje del jugador**, lo mueve de nuevo a su posición inicial, reduce la variable `vidas`{:class="block3variables"} en `1`, y después de medio segundo hace que el objeto vuelva a aparecer.