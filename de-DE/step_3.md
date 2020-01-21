## Das Spiel verlieren

Das Wichtigste zuerst! Du brauchst eine Möglichkeit, das Spiel zu beenden, wenn der Spieler keine Leben mehr hat. Im Moment passiert das nicht.

Du hast vielleicht bemerkt, dass der `verlieren`{:class="block3myblocks"}-**Meine Blöcke**-Block im Skript für die Figur **Spieler-Character** leer ist. Du wirst diese ausfüllen und alle Teile zusammenstellen, die für einen schönen 'Game over'-Bildschirm benötigt werden.

\--- task \---

First, find the `lose`{:class="block3myblocks"} block and complete it with the following code:

```blocks3
    Definiere verlieren
+ stoppe [andere Skripte der Figur v] :: control stack
+ Sende [Game Over v] an alle
+ gehe zu x: (0) y: (0)
+ sage [Game over!] für (2) Sekunden
+ stoppe [alles v]
```

\--- /task \---

## \--- collapse \---

## title: Was macht dieser Code?

Whenever the `lose`{:class="block3myblocks"} block runs now, what it does is:

1. Stoppe die Physik und andere Spielskripte, die den **Spieler-Charakter** beeinflussen
2. Sage alle anderen Figuren, das das Spiel vorbei ist und **sende** eine `Game Over`{:class="block3events"}-Botschaft, auf die sie reagieren und ändern können, was sie tun
3. Bewege den **Spieler-Charakter** in die Mitte der Bühne und lasse ihn den Spieler darüber informieren, dass das Spiel beendet ist
4. Stoppe alle Skripte im Spiel

\--- /collapse \---

Now you need to make sure all the sprites know what to do when the game is over, and how to reset themselves when the player starts a new game. **Don’t forget that any new sprites you add also might need code for this!**

### Plattformen und Kanten verstecken

\--- task \---

Start with the easiest sprites. The **Platforms** and **Edges** sprites both need code for appearing when the game starts and disappearing when they receive the `game over`{:class="block3events"} broadcast, so add these blocks to each of them:

```blocks3
+ wenn ich [Game Over v] empfange
+ verstecke dich
```

```blocks3
+ Wenn grüne Flagge angeklickt wird
+ zeige dich
```

\--- /task \---

### Die Sterne stoppen

Now, if you look at the code for the **Collectable** sprite, you’ll see it works by **cloning** itself. That is, it makes copies of itself that follow the special `when I start as a clone`{:class="block3events"} instructions.

We’ll talk more about what makes clones special when we get to the step about making new and different collectables. For now, what you need to know is that clones can do **almost** everything a normal sprite can, including receiving `broadcast`{:class="block3events"} messages.

Look at how the **Collectable** sprite works. See if you can understand some of its code:

```blocks3
    wenn grüne Fahne angeklickt wird
    verstecke dich
    setze [sammelobjekt-wert v] zu [1]
    setze [sammelobjekt-geschwindigkeit v] zu [1]
    setze [sammelobjekt-häufigkeit v] zu [1]
    setze [erzeuge-sammelobjekt v] zu [wahr]
    setze [sammelobjekt-typ v] auf [1]
    wiederholen bis <nicht <(create-collectables) = [wahr]>> 
        warten (sammelobjekt-häufigkeit) Sekunden
        gehe zu x: (Wähle zufällig (-240) bis (240)) y: (179)
        erzeuge einen Klon von [mir selbst]
    Ende
```

1. Zuerst wird die ursprüngliche **Sammelobjekt**-Figur durch das Ausblenden unsichtbar
2. Dann werden die Steuervariablen festgelegt - wir kommen später darauf zurück
3. Die Variable `erzeuge-sammelobjekt`{:class="block3variables"} ist der Ein-/Ausschalter für das Klonen: Die Schleife erstellt Klone, wenn `erzeuge-sammelobjekt`{:class="block3variables"} `wahr` ist und nichts wenn sie nicht wahr ist

\--- task \---

Now set up a block for the **Collectable** sprite so that it reacts to the `game over` broadcast:

```blocks3
+ Wenn ich [Game Over v] empfange
+ verstecke dich
+ setze [erzeuge-sammelobjekt v] auf [falsch]
```

\--- /task \---

This code is similar to the code controlling the **Platforms** and **Edges** sprites. The only difference is that you’re also setting the `create-collectables`{:class="block3variables"} variable to `false` so that no new clones get created when it's 'Game over'.

Note that you can use the `create-collectables`{:class="block3variables"} variable to pass messages from one part of your code to another!