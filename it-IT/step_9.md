## Piattaforme mobili

La ragione per cui ti ho chiesto di usare la mia versione di livello 2 è la differenza che potresti aver notato nel centro del layout. Creerai una piattaforma che si muove in questo spazio e che il giocatore può saltare e cavalcare!

![Un altro livello con diverse piattaforme](images/movingPlatforms.png)

Innanzitutto, avrai bisogno dello sprite per la piattaforma.

\--- task \---

Add a new sprite, name it **Moving-Platform**, and using the costume customisation tools in the Costumes tab to make it look like the other platforms \(use vector mode\).

\--- /task \---

Now, let's add some code to the sprite.

Begin with the basics: to make a never-ending set of platforms moving up the screen, you’ll need to clone the platform at regular intervals. I picked `4` seconds as my interval. You also need to make sure that there’s an on/off switch for making the platforms, so that they don’t show up in level 1. I’m using a new variable called `create-platforms`{:class="block3variables"}.

\--- task \---

Add code to create clones of your platform sprite.

Here's how mine looks so far:

```blocks3
+ quando si clicca sulla bandiera verde
+ nascondi
+ per sempre 
  attendi (4) secondi
  se <(crea-piattaforma :: variables) = [true]> allora 
    crea clone di [me stesso v]
end
end
```

\--- /task \---

\--- task \---

Then add the clone's code:

```blocks3
+ quando vengo clonato
+ mostra
+ per sempre 
  se <(posizione y) <[180]> allora 
    cambia y di (1)
    attendi (0.02) secondi
  altrimenti 
    elimina questo clone
  end
end
```

\--- /task \---

This code makes the **Moving-Platform** clone move up to the top of the screen, slowly enough for the player to jump on and off, and then disappear.

\--- task \---

Now make the platforms disappear/reappear based on the broadcasts that change levels (so they're only on the level with space for them), and the `game over`{:class="block3events"} message.

```blocks3
+ quando ricevo [livello-1 v]
+ porta [crea-piattaforma v] a [false]
+ nascondi

+ quando ricevo [livello-2 v]
+ porta [crea-piattaforma v] a [true]

+ quando ricevo [game over v]
+ nascondi
+ porta [crea-piattaforma v] a [false]
```

\--- /task \---

Now, if you try to actually play the game, the **Player Character** falls through the platform! Any idea why?

It’s because the physics code doesn’t know about the platform. It’s actually a quick fix:

\--- task \---

In the **Player Character** sprite scripts, replace every `touching “Platforms”`{:class="block3sensing"} block with an `OR`{:class="block3operators"} operator that checks for **either** `touching “Platforms”`{:class="block3sensing"} **OR** `touching “Moving-Platform”`{:class="block3sensing"}.

Go through the code for the **Player Character** sprite and everywhere you see this block:

```blocks3
    <touching [Platforms v] ?>
```

replace it with this one:

```blocks3
    <<touching [Platforms v] ?> o <touching [Moving-Platform v] ?>>
```

\--- /task \---