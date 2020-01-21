## Wettbewerb hinzufügen

Dein Spiel funktioniert und jetzt kannst du Punkte sammeln, besondere Kräfte von deinen Power-Ups erhalten und verlieren. Wir kommen weiter! Vielleicht wäre es Spaßig, ein wenig Konkurrenz hinzuzufügen - wie wäre es mit einer Figur, die sich ein wenig herum bewegt, die man aber nicht berühren sollte? Dies ist ähnlich zu Gegnern in traditionellen Plattformspielen wie Super Mario, die uns hier inspirieren.

\--- task \---

First, pick a sprite to add as your enemy. Because our player character is a cat, I chose a dog. There are lots of other sprites you could add though. I also renamed the sprite **Enemy**, just to make things clearer for me.

Resize the sprite to the right size, and place it somewhere appropriate to start. Here’s what mine looks like:

![The dog enemy sprite](images/enemySprite.png)

\--- /task \---

\--- task \---

Write the easiest code first: set up its block for reacting to the `game over`{:class="events"} message to make the enemy disappear when the player loses the game.

```blocks3
+ wenn ich [game over v] empfange
+ verstecke dich
```

\--- /task \---

\--- task \---

Now you need to write the code for what the enemy does. Use my code here, but consider adding extra bits! (What if they can teleport around to different platforms? What if there’s a power-up that makes them move faster, or slower?)

```blocks3
+ Wenn die grüne Flagge angeklickt
+ zeige dich
+ setze [Feindzugschritte v] auf [5]
+ setze Drehtyp auf [links-rechts v]
+ gehe zu x: (-25) y: (-9)
+ wiederhole fortlaufend 
  gehe (Feindzugschritte) er Schritt
  falls <nicht <wird [Platforms v] berührt?>> dann
  setze [Feindzugschritte v] auf ((Feindzugschritte) * (-1))
end

end
```

**Note**: if you just drag the `go to`{:class="block3motion"} block into the sprite panel and don’t change the `x` and `y` values, they’ll be the values for the current location of the **Enemy** sprite!

The code in the `if...then`{:class="block3control"} block will make the sprite turn around when they get to the end of the platform!

\--- /task \---

The next thing you’ll need is for the player to lose a life when their **Player Character** sprite touches the **Enemy** sprite. Also, you need to make sure the sprites **stop** touching really quickly, since otherwise the code that checks for touching will keep running and the player will keep losing lives.

\--- task \---

Here's how I did it, but you can try to improve on this code! I modified the **Player Character** sprite’s main block. Add the new code before the `if`{:class="block3control"} block that checks if you're out of lives.

```blocks3
    Wenn die grüne Flagge angeklickt
Spiel-zurücksetzen :: custom
wiederhole fortlaufend 
  Hauptphysik :: custom
  falls <(y-Position) < [-179]> , dann 
    verstecke dich
    Spieler-zurücksetzen:: custom
    ändere [Leben v] um (-1)
    warte (0.05) Sekunden
    zeige dich
  ende
  + falls <wird [Feind v] berührt?> , dann 
  +   verstecke dich
  +   gehe zu x: (-187) y: (42)
  +   ändere [Leben v] um (-1)
  +   warte (0.5) Sekunden
  +   zeige dich
  + ende
  falls <(Leben) < [1]> , dann 
    verlieren :: custom
  ende
ende
```

\--- /task \---

The new code hides the **Player Character** sprite, moves it back to its starting position, reduces the `lives`{:class="block3variables"} variable by `1`, and after half a second makes the sprite re-appear.