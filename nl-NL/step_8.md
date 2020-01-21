## Level 2

Met deze stap voeg je een nieuw level toe aan het spel dat de speler kan bereiken door eenvoudig op een knop te drukken. Later kun je jouw code wijzigen zodat een bepaald aantal punten of iets anders nodig zijn om daar te komen.

### Op naar het volgende level

\--- task \---

First, create a new sprite as a button by either adding one from the library or drawing your own. I did a bit of both and came up with this:

![The button sprite to switch levels](images/levelButton.png)

\--- /task \---

\--- task \---

Now, the code for this button is clever: it’s designed so that every time you click it it will take you to the next level, no matter how many levels there are.

Add these scripts to your **Button** sprite. You will need to create some variables as you do so.

```blocks3
+ wanneer op groene vlag wordt geklikt
+ maak [max-level v] [2]
+ maak [min-level v] [1]
+ maak [huidig niveau v] [1]
```

```blocks3
+ wanneer op deze deze sprite wordt geklikt
+ verander [huidig-level v] met (1)
+ als <(huidig-level) > (max-level ::variables)> dan
        maak [huidig-level v] (min-level ::variables)
    end
+ zend signaal [prijzen-schoonmaak v]
+ zend signaal (voeg [level-] en (huidig-level) samen)
```

\--- /task \---

Can you see how the program will use the variables you created?

+ `max-level`{:class="block3variables"} slaat het hoogste level op
+ `min-level`{:class="block3variables"} slaat het laagste level op
+ `huidig-level`{:class="block3variables"} slaat het level op waar de speler nu is

These all need to be set by the programmer \(you!\), so if you add a third level, don’t forget to change the value of `max-level`{:class="block3variables"}! `min-level`{:class="block3variables"} will never need to change, of course.

The broadcasts are used to tell the other sprites which level to display, and to clear up the collectables when a new level starts.

### Laat de sprites reageren

#### De **Prijs** sprite

Now you need to get the other sprites to respond to these broadcasts! Start with the easiest one: clearing all the collectables.

\--- task \---

Add the following code to the **Collectable** sprite scripts to tell all its clones to `hide`{:class="block3vlooks"} when they receive the cleanup broadcast:

```blocks3
+ wanneer ik signaal [prijzen-schoonmaak v] ontvang
+ verdwijn
```

\--- /task \---

Since one of the first things any new clone does is show itself, you don't have to worry about unhiding collectables!

#### De **Platform** sprite

Now to switch the **Platforms** sprite. You can design your own new level later if you like, but for now let’s use the one I’ve already included — you’ll see why on the next step!

\--- task \---

Add this code to the **Platforms** sprite:

```blocks3
+ wanneer ik signaal [level-1 v] ontvang
+ verander uiterlijk naar [Level 1 v]
+ verschijn
```

```blocks3
+ wanneer ik signaal [level-2 v] ontvang
+ verander uiterlijk naar [Level 2 v]
+ verschijn
```

\--- /task \---

It receives the `joined`{:class="block3operators"} messages of `level-`{:class="block3variables"} and `current-level`{:class="block3variables"} that the **Button** sprite sends out, and responds by changing the **Platforms** costume.

#### De **Vijand** sprite

\--- task \---

In the **Enemy** sprite scripts, just make sure the sprite disappears when the player enters level 2, like this:

```blocks3
+ wanneer ik signaal [level-1 v] ontvang
+ verschijn
```

```blocks3
+ wanneer ik signaal [level-2 v] ontvang
+ verdwijn
```

\--- /task \---

If you prefer, you can make the enemy move to another platform instead. In that case, you would use a `go to`{:class="block3motion"} block instead of the `show`{:class="block3looks"} and `hide`{:class="block3looks"} blocks.

### Laat de **Speler** op de juiste plaats verschijnen

Whenever a new level starts, the **Player Character** sprite needs to go to the right place for that level. To make this happen, you need to change where the sprite gets its coordinates from when it first appears on the Stage. At the moment, there are fixed `x` and `y` values in its code.

\--- task \---

Begin by creating variables for the starting coordinates: `start-x`{:class="block3variables"} and `start-y`{:class="block3variables"}. Then plug them into the `go to`{:class="block3motion"} block in the `reset-character`{:class="block3myblocks"} **My blocks** block instead of the fixed `x` and `y` values:

```blocks3
    definieer reset-speler
    maak [kan-springen v] [true]
    maak [x-vaart v] [0]
    maak [y-vaart v] [-0]
+ ga naar x: (start-x) y: (start- y)
```

\--- /task \---

\--- task \---

Then for each broadcast announcing the start of a level, set the right `start-x`{:class="block3variables"} and `start-y`{:class="block3variables"} coordinates in response, and add a **call** to `reset-character`{:class="block3myblocks"}:

```blocks3
+ wanneer ik signaal [level-1 v] ontvang
+ maak [start-x v] [-183]
+ maak [start-y v] [42]
+ reset-speler :: custom
```

```blocks3
+ wanneer ik signaal [level-2 v] ontvang
+ maak [start-x v] [-218]
+ maak [start-y v] [-143]
+ reset-speler :: custom
```

\--- /task \---

### Beginnen op Level 1

You also need to make sure that every time someone starts the game, the first level they play is level 1.

\--- task \---

Go to the `reset-game`{:class="block3myblocks"} script and remove the call to `reset-character`{:class="block3myblocks"} from it. In its place, broadcast the `min-level`{:class="block3variables"}. The code you've already added with this card will then set up the correct starting coordinates for the **Player Character** sprite, and also call `reset-character`{:class="block3myblocks"}.

```blocks3
    definieer reset-spel
    maak draaistijl [links-rechts v]
    maak [sprong-hoogte v] [15]
    maak [zwaartekracht v] [2]
    maak [x-snelheid v] [1]
    maak [y-snelheid v] [1]
    maak [levens v] [3]
    maak [punten v] [0]
+ zend signaal (voeg [level-] en (min-level ::variables) samen)
```

\--- /task \---

## \--- collapse \---

## title: Het personage van de speler of de game resetten

Notice that the first block in the **Player Character** sprite's main green flag script is a call to the `reset-game`{:class="block3myblocks"} **My blocks** block.

This block sets up all the variables for a new game and then calls the `reset-character`{:class="block3myblocks"} **My blocks** block, which places the character back in its correct starting position.

Having the `reset-character`{:class="block3myblocks"} code in its own block separate from `reset-game`{:class="block3myblocks"} allows you to reset the character to different positions **without** having to reset the whole game.

\--- /collapse \---