## Bewegende platforms

De reden waarom ik je heb gevraagd om mijn versie van level 2 te gebruiken, is de opening die je misschien midden in de opmaak hebt gezien. Je gaat een platform creëren dat zich door deze kloof beweegt en waar de speler op kan springen en rijden!

![Een ander level met verschillende platforms](images/movingPlatforms.png)

Ten eerste heb je de sprite voor het platform nodig.

\--- task \---

Add a new sprite, name it **Moving-Platform**, and using the costume customisation tools in the Costumes tab to make it look like the other platforms \(use vector mode\).

\--- /task \---

Now, let's add some code to the sprite.

Begin with the basics: to make a never-ending set of platforms moving up the screen, you’ll need to clone the platform at regular intervals. I picked `4` seconds as my interval. You also need to make sure that there’s an on/off switch for making the platforms, so that they don’t show up in level 1. I’m using a new variable called `create-platforms`{:class="block3variables"}.

\--- task \---

Add code to create clones of your platform sprite.

Here's how mine looks so far:

```blocks3
+ wanneer op groene vlag wordt geklikt
+ verdwijn
+ herhaal
        wacht (4) sec
        als <(maak-platforms ::variables) = [true]> dan
            maak een kloon van [mijzelf v]
        end
    end
```

\--- /task \---

\--- task \---

Then add the clone's code:

```blocks3
+ wanneer ik als kloon start
+ verschijn
+ herhaal
        als <(y positie) < [180]> dan
            verander y met (1)
            wacht (0.02) sec
        anders
            verwijder deze kloon
        end
    end
```

\--- /task \---

This code makes the **Moving-Platform** clone move up to the top of the screen, slowly enough for the player to jump on and off, and then disappear.

\--- task \---

Now make the platforms disappear/reappear based on the broadcasts that change levels (so they're only on the level with space for them), and the `game over`{:class="block3events"} message.

```blocks3
+ wanneer ik signaal [level-1 v] ontvang
+ maak [maak-platforms v] [false]
+ verdwijn

+ wanneer ik signaal [level-2 v] ontvang
+ maak [maak-platforms v] [true]

+ wanneer ik signaal [game over v] ontvang
+ verdwijn
+ maak [maak-platforms v] [false]
```

\--- /task \---

Now, if you try to actually play the game, the **Player Character** falls through the platform! Any idea why?

It’s because the physics code doesn’t know about the platform. It’s actually a quick fix:

\--- task \---

In the **Player Character** sprite scripts, replace every `touching “Platforms”`{:class="block3sensing"} block with an `OR`{:class="block3operators"} operator that checks for **either** `touching “Platforms”`{:class="block3sensing"} **OR** `touching “Moving-Platform”`{:class="block3sensing"}.

Go through the code for the **Player Character** sprite and everywhere you see this block:

```blocks3
    <raak ik [Platform v] ?>
```

replace it with this one:

```blocks3
    <<raak ik [Platform v] ?> of <raak ik [Bewegend-Platform v] ?>>
```

\--- /task \---