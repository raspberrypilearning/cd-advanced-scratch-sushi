## Preparando todo

Ya que estás aprendiendo a programar en Scratch y no a construir un motor de física (el código que hace que las cosas en un juego de computadora se comporten como objetos del mundo real, por ejemplo, no caen por los pisos), comenzarás con un proyecto que he creado que ya tiene lo básico para mover, saltar y detectar plataformas integradas.

Debes echarle un vistazo rápido al proyecto, incluyendo los detalles en esta tarjeta, ya que harás algunos cambios más adelante, ¡pero no es necesario que entiendas todo lo que está haciendo!

### Obtener el proyecto

\--- task \---

Lo primero que deberás hacer es obtener una copia del código de Scratch de [dojo.soy/advanced-scratch](http://dojo.soy/advanced-scratch){:target="_blank"} .

Para usar el proyecto sin conexión a Internet, descárgalo haciendo clic en **Ver dentro**, luego ir a**Archivo**menú y haz clic en **Guardar en tu ordenador**. Luego puedes abrir el archivo descargado en Scratch en tu computadora.

También puedes usarlo directamente en Scratch en tu navegador haciendo clic en **Ver dentro** y luego **Remix**.

\--- /task \---

### Echa un vistazo al código

El motor de física del juego tiene una variedad de piezas, algunas de las cuales ya funcionan y otras todavía no. Puedes probar esto ejecutando el juego e intentar jugarlo.

Verás que puedes perder vidas, pero no pasa nada cuando te quedas sin ellas. Además, el juego solo tiene un nivel, un tipo de cosa a recolectar, y no hay enemigos. ¡Vas a arreglar todo eso y luego harás un poco más!

\--- task \---

Por ahora, échale un vistazo a cómo se crea el código.

\--- /task \---

Usa muchos bloques de **Mis bloques**, que son excelentes para dividir tu código en partes y puedas administrarlo mejor. Un bloque de **Mis bloques** es un bloque que se compone de muchos otros bloques, y puedes darle algunas instrucciones. ¡Verás cómo funciona en un próximo paso!

![](images/setup2and3.png)

### Los bloques 'Mis bloques' son realmente útiles

In the code above, the main game `forever`{:class="block3control"} loop calls the `main-physics`{:class="block3myblocks"} **My blocks** block to do a whole lot of stuff! Mantenerlos los bloques separados de esta manera hace que sea fácil leer el ciclo principal y comprender qué sucede en el juego, sin preocuparse por **cómo** suceda.

\--- task \---

Now look at the `reset game`{:class="block3myblocks"} and `reset character`{:class="block3myblocks"} **My blocks** blocks.

\--- /task \---

Hacen cosas bastante normales, como configurar variables y asegurarse de que el personaje gire correctamente

- `reset-game`{:class="block3myblocks"} **calls** `reset-character`{:class="block3myblocks"}, showing you that you can use a **My blocks** block inside another **My blocks** block
- El bloque `reset-character`{:class="block3myblocks"} de **Mis bloques** se usa en dos lugares diferentes en el bucle principal. Esto significa que puedes cambiar en dos lugares del bucle principal del juego cambiando solo el código dentro del bloque **Mis bloques**, lo que te ahorra mucho trabajo y te ayuda a evitar errores.