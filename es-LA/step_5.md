## ¡Superpotenciadores!

Ahora que tienes un nuevo potenciador coleccionable funcionando, es hora de hacer que haga algo realmente genial: hagamos que 'lluevan' potenciadores durante unos segundos, en lugar de simplemente dar una vida extra.

Para esto, vas a `enviar`{:class="block3events"} otro mensaje.

--- task ---

Primero, cambia el bloque de `reaccionar-al-jugador`{:class="block3myblocks"} para enviar un mensaje cuando el personaje del jugador toca un coleccionable tipo `2`. Llame al mensaje `lluvia-coleccionable`{:class="block3events"}.

```blocks3
    define tipo (tipo)
    if <(tipo ::variable) = [1]> then
        change [puntos v] by (valor-coleccionable ::variables)
    end
    if <(tipo ::variable) = [2]> then
-        change [vidas v] by [1]    
+        broadcast [lluvia-coleccionable v]
    end
```

--- /task ---

Ahora necesitas crear una nueva pieza de código dentro del script del objeto **Coleccionable**, que comenzará cada vez que se envíe el mensaje `lluvia-coleccionable`{:class="block3events"}.

--- task ---

Agregue este código al objeto **Coleccionable** para que escuche al mensaje `lluvia-coleccionable`{:class="block3events"}.

```blocks3
+    when I receive [lluvia-coleccionable v]
+    set [frecuencia-coleccionable v] to [0.000001]
+    wait (1) secs
+    set [frecuencia-coleccionable v] to [1]
```

--- /task ---

--- collapse ---
---
title: ¿Qué hace el nuevo código?
---

Esta pieza de código espera recibir un mensaje, y responde configurando la variable `frecuencia-coleccionable`{:class="block3variables"} a un número muy pequeño, luego espera un segundo, y luego vuelve a cambiar la variable a `1`.

Veamos cómo se usa la variable `frecuencia-coleccionable`{:class="block3variables"} para descubrir por qué hace que lluevan coleccionables.

En el bucle principal del juego, la parte del código que genera los clones del objeto **Coleccionable** recibe información de la variable `frecuencia-coleccionable`{:class="block3variables"} acerca de cuánto tiempo esperar entre hacer un clon y el siguiente:

```blocks3
    repeat until <not <(crear-coleccionables ::variables) = [true]>>
        if < [50] = (pick random (1) to (50))> then
            set [tipo-coleccionable v] to [2]
        else
            set [tipo-coleccionable v] to [1]
        end
        wait (frecuencia-coleccionable ::variables) secs
        go to x: (pick random (-240) to (240)) y:(179)
        create clone of [mí mismo v]
    end
```

Puedes ver que el bloque `esperar`{:class="block3control"} aquí, detiene el código durante el tiempo establecido por `frecuencia-coleccionable`{:class="block3variables"}.

Si el valor de `frecuencia-coleccionable`{:class="block3variables"} es `0.000001`, el bloque `esperar`{:class="block3control"} solo se detiene por **una millonésima** de segundo, lo que significa que el blucle `repetir hasta que`{:class="block3control"} se ejecutará muchas más veces de lo normal. Como resultado, el código creará **muchos** más potenciadores de lo normal, hasta que `frecuencia-coleccionable`{:class="block3variables"} se cambie de nuevo a `1`.

¿Puedes pensar en algunos problemas que eso pueda causar? Habrá muchos más potenciadores…¿qué pasaría si los siguieras atrapando?

--- /collapse ---