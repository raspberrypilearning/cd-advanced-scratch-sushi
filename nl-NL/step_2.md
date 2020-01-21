## De voorbereidingen

Omdat je in Scratch leert programmeren en niet hoe je een natuurkundige machine moet bouwen (code die dingen in een computergame doet voorkomen als objecten uit de echte wereld, bijvoorbeeld dat ze niet door vloeren vallen), begin je met een project dat ik heb gemaakt en dat al de basis heeft voor bewegingen, springen en het zien van platforms.

Werp een blik op het project, inclusief de details op deze kaart, want je zult er later een aantal wijzigingen in aanbrengen, maar je hoeft niet alles te begrijpen wat het doet!

### Ga naar het project

\--- task \---

The first thing you’ll need to do is to get a copy of the Scratch code from [dojo.soy/advanced-scratch](http://dojo.soy/advanced-scratch){:target="_blank"} .

To use the project offline, download it by clicking **See Inside**, then go to the **File** menu and click **Download to your computer**. Then you can open the downloaded file in Scratch on your computer.

You can also use it directly in Scratch in your browser by just clicking **See Inside** and then **Remix**.

\--- /task \---

### Bekijk de code

The physics engine of the game has a variety of pieces in it, some of which work already and some of which don’t yet. You can test this out by running the game and trying to play it.

You'll see that you can lose lives, but nothing happens when you run out. Also, the game only has one level, one type of thing to collect, and no enemies. You’re going to fix all of that, and a then do a bit more!

\--- task \---

Take a look at how the code is put together.

\--- /task \---

It uses lots of **My blocks** blocks, which are great for splitting your code up into pieces so you can manage it better. A **My blocks** block is a block you make up out of a lot of other blocks, and you can give some instructions to it. You'll see how it works in an upcoming step!

![](images/setup2and3.png)

### 'Mijn blokken' blokken zijn erg handig

In the code above, the main game `forever`{:class="block3control"} loop calls the `main-physics`{:class="block3myblocks"} **My blocks** block to do a whole lot of stuff! Keeping the blocks separated like this makes it easy to read the main loop and understand what happens in the game, without worrying about **how** it happens.

\--- task \---

Now look at the `reset game`{:class="block3myblocks"} and `reset character`{:class="block3myblocks"} **My blocks** blocks.

\--- /task \---

They do pretty normal things, such as setting up variables and making sure the character rotates properly

- `reset-spel`{:class="block3myblocks"} **roept** `reset-speler`{:class="block3myblocks"} **aan**, en laat zien dat je een **Mijn blokken** blok kunt gebruiken binnen een ander <1>Mijn blokken</1> blok
- Het `reset-speler`{:class="block3myblocks"} **Mijn blokken** blok wordt op twee verschillende plaatsen in de hoofdlus gebruikt. Dit betekent dat je twee plaatsen in je hoofdgame-loop kunt wijzigen door alleen de code in het blok **Mijn blokken** te wijzigen. Dit bespaart je veel werk en helpt je fouten te voorkomen.