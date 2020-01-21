## Plattformen verschieben

Der Grund, warum ich dich gebeten habe, meine Version von Level 2 zu verwenden, ist die Lücke, die du möglicherweise in der Mitte des Layouts bemerkt hast. Du wirst eine Plattform schaffen, die sich durch diese Lücke bewegt und auf die der Spieler springen und fahren kann!

![Ein anderes Level mit verschiedenen Plattformen](images/movingPlatforms.png)

Zunächst benötigst du die Figur für die Plattform.

\--- task \---

Add a new sprite, name it **Moving-Platform**, and using the costume customisation tools in the Costumes tab to make it look like the other platforms \(use vector mode\).

\--- /task \---

Now, let's add some code to the sprite.

Begin with the basics: to make a never-ending set of platforms moving up the screen, you’ll need to clone the platform at regular intervals. I picked `4` seconds as my interval. You also need to make sure that there’s an on/off switch for making the platforms, so that they don’t show up in level 1. I’m using a new variable called `create-platforms`{:class="block3variables"}.

\--- task \---

Add code to create clones of your platform sprite.

Here's how mine looks so far:

```blocks3
+ Wenn die grüne Flagge angeklickt 
+ verstecke dich
+ wiederhole fortlaufend
        warte (4) Sekunden
        falls <(erstelle-plattform ::variables) = [wahr]>, dann
            erzeuge Klon von [mir selbst v]
        Ende
    Ende
```

\--- /task \---

\--- task \---

Then add the clone's code:

```blocks3
+ Wenn ich als Klon entstehe
+ zeige dich
+ wiederhole fortlaufend
        falls <(y - Position) < [180]>, dann
            ändere y um (1)
            warte (0,02) Sekunden
        sonst
            lösche diesen Klon
        Ende
    Ende
```

\--- /task \---

This code makes the **Moving-Platform** clone move up to the top of the screen, slowly enough for the player to jump on and off, and then disappear.

\--- task \---

Now make the platforms disappear/reappear based on the broadcasts that change levels (so they're only on the level with space for them), and the `game over`{:class="block3events"} message.

```blocks3
+ wenn ich [Level-1 v] empfange
+ setze [erstelle-Plattform v] auf [falsch]
+ verstecke dich

+ wenn ich [Level-2 v] empfange
+ setze [erstelle-Plattform v] auf [wahr]

+ wenn ich [Game Over v] empfange 
+ verstecke dich
+ setze [erstelle-Plattform  v] auf [falsch]
```

\--- /task \---

Now, if you try to actually play the game, the **Player Character** falls through the platform! Any idea why?

It’s because the physics code doesn’t know about the platform. It’s actually a quick fix:

\--- task \---

In the **Player Character** sprite scripts, replace every `touching “Platforms”`{:class="block3sensing"} block with an `OR`{:class="block3operators"} operator that checks for **either** `touching “Platforms”`{:class="block3sensing"} **OR** `touching “Moving-Platform”`{:class="block3sensing"}.

Go through the code for the **Player Character** sprite and everywhere you see this block:

```blocks3
    <wird [Platform v] berührt?>
```

replace it with this one:

```blocks3
    <<wird [Platform v] berührt?> oder <wird [mobile-Platform v] berührt?>>
```

\--- /task \---