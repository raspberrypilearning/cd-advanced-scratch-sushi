## Wedstrijdelement toevoegen

Je game werkt en nu kun je punten verzamelen, speciale power-ups verdienen en verliezen. Het wordt wat! Misschien is het leuk om een wedstrijdelement toe te voegen - zoals bijvoorbeeld een personage dat een beetje beweegt, maar dat je niet hoort aan te raken? Dit zal vergelijkbaar zijn met vijanden in de traditionele platformgames zoals Super Mario, waar we ons hier door laten inspireren.

\--- task \---

First, pick a sprite to add as your enemy. Because our player character is a cat, I chose a dog. There are lots of other sprites you could add though. I also renamed the sprite **Enemy**, just to make things clearer for me.

Resize the sprite to the right size, and place it somewhere appropriate to start. Here’s what mine looks like:

![The dog enemy sprite](images/enemySprite.png)

\--- /task \---

\--- task \---

Write the easiest code first: set up its block for reacting to the `game over`{:class="events"} message to make the enemy disappear when the player loses the game.

```blocks3
+ wanneer ik signaal [game over v] ontvang
+ verdwijn
```

\--- /task \---

\--- task \---

Now you need to write the code for what the enemy does. Use my code here, but consider adding extra bits! (What if they can teleport around to different platforms? What if there’s a power-up that makes them move faster, or slower?)

```blocks3
+ wanneer op groene vlag wordt geklikt
+ verschijn
+ maak [vijand-zet-stappen v] [5]
+ maak draaistijl [links-rechts v]
+ ga naar x: (-25) y: (-9)
+ herhaal
        neem (vijand-zet-stappen) stappen
        als <niet <raak ik [platforms v]>> dan
            maak [vijand-zet-stappen v] ((vijand-zet-stappen) * (-1))
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
    wanneer op groene vlag wordt geklikt
    reset-spel :: custom
    herhaal
        natuurkunde :: custom
        als <(y positie) < [-179]> dan
            verdwijn
            reset-speler :: custom
            verander [levens v] met (-1 )
            wacht (0.05) sec
            verschijn
        end
+ als <raak ik [Vijand v] ?> dan
            verdwijn
            ga naar x: (-187) y: (42)
            verander [levens v] met (-1)
            wacht (0.5) sec
            verschijn
+ end
        als <(levens) < [1]> dan
            verlies :: custom
        end
    end
```

\--- /task \---

The new code hides the **Player Character** sprite, moves it back to its starting position, reduces the `lives`{:class="block3variables"} variable by `1`, and after half a second makes the sprite re-appear.