## ¡Super poderes!

Ahora que tienes un nuevo poder funcionando, es hora de hacer que haga algo realmente genial: Hagamos que "lluevan" poderes durante unos segundos, en lugar de simplemente dar una vida extra.

Para esto, vas a usar otro mensaje de `difusión`{:class="block3events"}.

\--- task \---

Primero, cambia el bloque `reaccion-a-jugador`{:class="block3myblocks"} para transmitir un mensaje cuando el personaje toque un coleccionable tipo `2`. Llama al mensaje `lluvia-coleccionable`{:class="block3events"}.

```blocks3
    define react-to-player (type)
    if <(type ::variable) = [1]> then
        change [points v] by (collectable-value ::variables)
    end
    if <(type ::variable) = [2]> then
-        change [lives v] by [1]    
+        broadcast [collectable-rain v]
    end
```

\--- /task \---

Ahora necesitas crear una nueva pieza de código dentro de los scripts de objeto **coleccionable** que comenzarán cada vez que el mensaje `lluvia-coleccionable`{:class="block3events"} se difunda.

\--- task \---

Añade este código para el objeto **Coleccionable** para que escuche la transmisión `lluvia-coleccionable`{:class="block3events"}.

```blocks3
+    when I receive [collectable-rain v]
+    set [collectable-frequency v] to [0.000001]
+    wait (1) secs
+    set [collectable-frequency v] to [1]
```

\--- /task \---

## \--- collapse \---

## title: ¿Qué hace el nuevo código?

Esta pieza de código espera para recibir una transmisión y responde configurando la variable `frecuencia-coleccionable`{:class="block3variables"} a un número muy pequeño. Luego espera un segundo y cambia la variable de vuelta a `1`.

Veamos cómo se utiliza la variable `frecuencia-coleccionable`{:class="block3variables"} para averiguar por qué esto hace que lluevan coleccionables.

En el bucle principal del juego, la parte del código que hace que los objetos clones **coleccionables** reciban información de la variable `frecuencia-coleccionable`{:class="block3variables"} acerca de cuánto tiempo esperar entre hacer un clon y el siguiente:

```blocks3
    repeat until <not <(create-collectables ::variables) = [true]>>
        if < [50] = (pick random (1) to (50))> then
            set [collectable-type v] to [2]
        else
            set [collectable-type v] to [1]
        end
        wait (collectable-frequency ::variables) secs
        go to x: (pick random (-240) to (240)) y:(179)
        create clone of [myself v]
    end
```

Puedes ver que el bloque `esperar`{:class="block3control"} aquí pausa el código durante el tiempo establecido por `frecuencia-coleccionable`{:class="block3variables"}.

Si el valor de `frecuencia-coleccionable`{:class="block3variables"} es `0. 00001`, el bloque `esperar`{:class="block3control"} sólo pausa **una millonésima** de segundo, lo que significa que el bucle `repetirá hasta`{:class="block3control"} se ejecutará muchas veces más de lo normal. Como resultado, el código va a crear **muchos** poderes más de lo que normalmente haría, hasta que `frecuencia-coleccionable`{: class = "block3variables"} vuelva a cambiar a `1`.

¿Puedes pensar en algún problema que pueda causar? Habrá muchos más poderes…¿qué pasa si los sigues capturando?

\--- /collapse \---