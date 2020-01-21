## Vorbereitungen

Du lernst, wie man in Scratch programmiert, und nicht wie man eine Physik-Engine erstellt (Code, der bewirkt, dass sich Dinge in einem Computerspiel wie realistische Objekte verhalten, z. B. fallen sie nicht durch Böden). Deswegen beginnst du mit einem Projekt, das ich erstellt habe und das bereits die Grundlagen für das Verschieben, Springen und Erkennen von Plattformen enthält.

Du solltest dir das Projekt einschließlich der Details auf dieser Karte kurz ansehen, da du später einige Änderungen daran vornehmen wirst, aber du musst nicht alles verstehen, was es tut!

### Das Projekt bekommen

\--- task \---

The first thing you’ll need to do is to get a copy of the Scratch code from [dojo.soy/advanced-scratch](http://dojo.soy/advanced-scratch){:target="_blank"} .

To use the project offline, download it by clicking **See Inside**, then go to the **File** menu and click **Download to your computer**. Then you can open the downloaded file in Scratch on your computer.

You can also use it directly in Scratch in your browser by just clicking **See Inside** and then **Remix**.

\--- /task \---

### Schaue dir den Code an

The physics engine of the game has a variety of pieces in it, some of which work already and some of which don’t yet. You can test this out by running the game and trying to play it.

You'll see that you can lose lives, but nothing happens when you run out. Also, the game only has one level, one type of thing to collect, and no enemies. You’re going to fix all of that, and a then do a bit more!

\--- task \---

Take a look at how the code is put together.

\--- /task \---

It uses lots of **My blocks** blocks, which are great for splitting your code up into pieces so you can manage it better. A **My blocks** block is a block you make up out of a lot of other blocks, and you can give some instructions to it. You'll see how it works in an upcoming step!

![](images/setup2and3.png)

### "Meine Blöcke"-Blöcke sind wirklich nützlich

In the code above, the main game `forever`{:class="block3control"} loop calls the `main-physics`{:class="block3myblocks"} **My blocks** block to do a whole lot of stuff! Keeping the blocks separated like this makes it easy to read the main loop and understand what happens in the game, without worrying about **how** it happens.

\--- task \---

Now look at the `reset game`{:class="block3myblocks"} and `reset character`{:class="block3myblocks"} **My blocks** blocks.

\--- /task \---

They do pretty normal things, such as setting up variables and making sure the character rotates properly

- `Spiel-zurücksetzen`{:class="block3myblocks"} **ruft** `Spieler-zurücksetzen`{:class="block3myblocks"} auf und zeigt, dass du einen **Meine Blöcke**-Block innerhalb eines weiteren **Meine Blöcke**-Blocks verwenden kannst
- Der `Spieler-zurücksetzen`{:class="block3myblocks"} **Meine Blöcke**-Block wird an zwei verschiedenen Stellen in der Hauptschleife verwendet. Dies bedeutet, dass du zwei Stellen in deiner Hauptspielschleife ändern kannst, indem du nur den Code innerhalb des **Meine Blöcke**-Blocks änderst. Dies erspart dir viel Arbeit und hilft, Fehler zu vermeiden.