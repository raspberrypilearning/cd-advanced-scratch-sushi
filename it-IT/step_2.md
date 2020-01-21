## Impostare il tutto

Siccome stai imparando a scrivere codice in Scratch e non a costruire un motore fisico (codice che fa in modo che le cose in un gioco per computer si comportino come oggetti del mondo reale, ad esempio non cadano attraverso i pavimenti), inizierai con un progetto che ho creato che ha già le basi per spostare, saltare e rilevare le piattaforme integrate.

Dovresti dare una rapida occhiata al progetto, inclusi i dettagli su questa scheda, perché in seguito dovrai apportare alcune modifiche, ma non devi capire tutto ciò che sta facendo!

### Prendi il progetto

\--- task \---

The first thing you’ll need to do is to get a copy of the Scratch code from [dojo.soy/advanced-scratch](http://dojo.soy/advanced-scratch){:target="_blank"} .

To use the project offline, download it by clicking **See Inside**, then go to the **File** menu and click **Download to your computer**. Then you can open the downloaded file in Scratch on your computer.

You can also use it directly in Scratch in your browser by just clicking **See Inside** and then **Remix**.

\--- /task \---

### Dai un'occhiata al codice

The physics engine of the game has a variety of pieces in it, some of which work already and some of which don’t yet. You can test this out by running the game and trying to play it.

You'll see that you can lose lives, but nothing happens when you run out. Also, the game only has one level, one type of thing to collect, and no enemies. You’re going to fix all of that, and a then do a bit more!

\--- task \---

Take a look at how the code is put together.

\--- /task \---

It uses lots of **My blocks** blocks, which are great for splitting your code up into pieces so you can manage it better. A **My blocks** block is a block you make up out of a lot of other blocks, and you can give some instructions to it. You'll see how it works in an upcoming step!

![](images/setup2and3.png)

### I blocchi "I miei blocchi" sono davvero utili

In the code above, the main game `forever`{:class="block3control"} loop calls the `main-physics`{:class="block3myblocks"} **My blocks** block to do a whole lot of stuff! Keeping the blocks separated like this makes it easy to read the main loop and understand what happens in the game, without worrying about **how** it happens.

\--- task \---

Now look at the `reset game`{:class="block3myblocks"} and `reset character`{:class="block3myblocks"} **My blocks** blocks.

\--- /task \---

They do pretty normal things, such as setting up variables and making sure the character rotates properly

- `reset-partita`{:class="block3myblocks"} **chiama** `reset-personaggio`{:class="block3myblocks"}, mostrandoti che puoi usare un blocco de **I Miei Blocchi** all'interno di un altro blocco de **I Miei Blocchi**
- Il `reset-personaggio`{:class="block3myblocks"} de **I Miei Blocchi** viene utilizzato in due diversi punti del ciclo principale. Ciò significa che puoi modificare due posizioni nel tuo ciclo di gioco principale cambiando solo il codice all'interno del blocco ne **I Miei blocchi**, il che ti consente di risparmiare molto lavoro e ti aiuta a evitare errori.