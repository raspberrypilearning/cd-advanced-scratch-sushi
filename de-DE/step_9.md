## Plattformen verschieben

Der Grund, warum ich dich gebeten habe, meine Version von Level 2 zu verwenden, ist die Lücke, die du möglicherweise in der Mitte des Layouts bemerkt hast. Du wirst eine Plattform schaffen, die sich durch diese Lücke bewegt und auf die der Spieler springen und fahren kann!

![Ein anderes Level mit verschiedenen Plattformen](images/movingPlatforms.png)

Zunächst benötigst du die Figur für die Plattform.

\--- task \---

Füge eine neue Figur hinzu, nenne sie **mobile-plattform** und benutze die Kostümanpassungs-Tools auf der Registerkarte Kostüme, damit sie wie die anderen Plattformen aussieht \(Vektormodus verwenden\).

\--- /task \---

Nun fügen wir der Figur etwas Code hinzu.

Beginne mit den Grundlagen: Um eine unendliche Anzahl von Plattformen, die sich auf dem Bildschirm nach oben bewegen, zu machen, musst du die Plattform in regelmäßigen Abständen klonen. Ich habe `4` Sekunden als Intervall ausgewählt. Du musst auch sicherstellen, dass es einen Ein/Aus-Schalter für die Herstellung der Plattformen gibt, damit sie nicht in Level 1 angezeigt werden. I’m using a new variable called `create-platforms`{:class="block3variables"}.

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