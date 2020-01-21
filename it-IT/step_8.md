## Livello 2

Seguendo questa scheda, aggiungerai un nuovo livello al gioco a cui il giocatore può accedere premendo semplicemente un pulsante. Più tardi, potrai cambiare il tuo codice per fare in modo che sia necessario ottenere un punteggio minimo, o qualcos'altro, per arrivarci.

### Passaggio al livello successivo

\--- task \---

First, create a new sprite as a button by either adding one from the library or drawing your own. I did a bit of both and came up with this:

![The button sprite to switch levels](images/levelButton.png)

\--- /task \---

\--- task \---

Now, the code for this button is clever: it’s designed so that every time you click it it will take you to the next level, no matter how many levels there are.

Add these scripts to your **Button** sprite. You will need to create some variables as you do so.

```blocks3
+ quando si clicca sulla bandiera verde
+ porta [max-livello v] a [2]
+ porta [min-livello v] a [1]
+ porta [livello-attuale v] a [1]
```

```blocks3
+ quando si clicca questo sprite
+ cambia [livello-attuale v] di (1)
+ se <(livello-attuale) > (max-livello :: variables)> allora 
  porta [livello-attuale v] a (min-livello :: variables)
end
+ invia a tutti [catturabili-ripulisci v]
+ invia a tutti (unione di [livello-] e (livello-attuale))
```

\--- /task \---

Can you see how the program will use the variables you created?

+ `max-livello`{:class="block3variables"} memorizza il livello più alto
+ `min-livello`{:class="block3variables"} memorizza il livello più basso
+ `livello-attuale`{:class="block3variables"} memorizza il livello al quale il giocatore si trova in questo momento

These all need to be set by the programmer \(you!\), so if you add a third level, don’t forget to change the value of `max-level`{:class="block3variables"}! `min-level`{:class="block3variables"} will never need to change, of course.

The broadcasts are used to tell the other sprites which level to display, and to clear up the collectables when a new level starts.

### Fai reagire gli sprite

#### Lo sprite **Catturabili**

Now you need to get the other sprites to respond to these broadcasts! Start with the easiest one: clearing all the collectables.

\--- task \---

Add the following code to the **Collectable** sprite scripts to tell all its clones to `hide`{:class="block3vlooks"} when they receive the cleanup broadcast:

```blocks3
+ quando ricevo [catturabili-ripulisci v]
+ nascondi
```

\--- /task \---

Since one of the first things any new clone does is show itself, you don't have to worry about unhiding collectables!

#### Gli sprite **Piattaforme**

Now to switch the **Platforms** sprite. You can design your own new level later if you like, but for now let’s use the one I’ve already included — you’ll see why on the next step!

\--- task \---

Add this code to the **Platforms** sprite:

```blocks3
+ quando ricevo [livello-1 v]
+ passa al costume [Livello 1 v]
+ mostra
```

```blocks3
+ quando ricevo [livello-2 v]
+ passa al costume [Livello 2 v]
+ mostra
```

\--- /task \---

It receives the `joined`{:class="block3operators"} messages of `level-`{:class="block3variables"} and `current-level`{:class="block3variables"} that the **Button** sprite sends out, and responds by changing the **Platforms** costume.

#### Lo sprite nemico **Nemico**

\--- task \---

In the **Enemy** sprite scripts, just make sure the sprite disappears when the player enters level 2, like this:

```blocks3
+ quando ricevo [livello-1 v]
+ mostra
```

```blocks3
+ quando ricevo [livello-2 v]
+ nascondi
```

\--- /task \---

If you prefer, you can make the enemy move to another platform instead. In that case, you would use a `go to`{:class="block3motion"} block instead of the `show`{:class="block3looks"} and `hide`{:class="block3looks"} blocks.

### Fai apparire il personaggio **Personaggio-giocatore** nel posto giusto

Whenever a new level starts, the **Player Character** sprite needs to go to the right place for that level. To make this happen, you need to change where the sprite gets its coordinates from when it first appears on the Stage. At the moment, there are fixed `x` and `y` values in its code.

\--- task \---

Begin by creating variables for the starting coordinates: `start-x`{:class="block3variables"} and `start-y`{:class="block3variables"}. Then plug them into the `go to`{:class="block3motion"} block in the `reset-character`{:class="block3myblocks"} **My blocks** block instead of the fixed `x` and `y` values:

```blocks3
    definisci reset-character
porta [puo-saltare v] a [true]
porta [x-velocita v] a [0]
porta [y-velocita v] a [-0]
+ vai a x: (partenza-x) y: (partenza-y)
```

\--- /task \---

\--- task \---

Then for each broadcast announcing the start of a level, set the right `start-x`{:class="block3variables"} and `start-y`{:class="block3variables"} coordinates in response, and add a **call** to `reset-character`{:class="block3myblocks"}:

```blocks3
+ quando ricevo [livello-1 v]
+ porta [partenza-x v] a [-183]
+ porta [partenza-y v] a [42]
+ reset-personaggio :: custom
```

```blocks3
+ quando ricevo [livello-2 v]
+ porta [partenza-x v] a [-218]
+ porta [partenza-y v] a [-143]
+ reset-personaggio :: custom
```

\--- /task \---

### Partenza dal livello 1

You also need to make sure that every time someone starts the game, the first level they play is level 1.

\--- task \---

Go to the `reset-game`{:class="block3myblocks"} script and remove the call to `reset-character`{:class="block3myblocks"} from it. In its place, broadcast the `min-level`{:class="block3variables"}. The code you've already added with this card will then set up the correct starting coordinates for the **Player Character** sprite, and also call `reset-character`{:class="block3myblocks"}.

```blocks3
    definisci reset-partita
usa stile rotazione [sinistra-destra v]
porta [salto-altezza v] a [15]
porta [gravita v] a [2]
porta [x-velocita v] a [1]
porta [y-velocita v] a [1]
porta [vite v] a [3]
porta [punteggio v] a [0]
+ invia a tutti (unione di [livello-] e (min-livello :: variables))
```

\--- /task \---

## \--- collapse \---

## title: Reset del personaggio del giocatore rispetto al reset della partita

Notice that the first block in the **Player Character** sprite's main green flag script is a call to the `reset-game`{:class="block3myblocks"} **My blocks** block.

This block sets up all the variables for a new game and then calls the `reset-character`{:class="block3myblocks"} **My blocks** block, which places the character back in its correct starting position.

Having the `reset-character`{:class="block3myblocks"} code in its own block separate from `reset-game`{:class="block3myblocks"} allows you to reset the character to different positions **without** having to reset the whole game.

\--- /collapse \---