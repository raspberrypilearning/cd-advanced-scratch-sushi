## Super power-ups!

Nu je een nieuwe power-up prijs hebt, is het tijd om iets heel cools te maken: Laten we het een paar seconden power-ups 'regenen' in plaats van alleen maar een extra leven te geven.

Hiervoor gebruik je een ander `signaal`{:class="block3events"} bericht.

\--- task \---

First, change the `react-to-player`{:class="block3myblocks"} block to broadcast a message when the player character touches a type `2` collectable. Call the message `collectable-rain`{:class="block3events"}.

```blocks3
    definieer reageer-op-speler (type)
    als <(type ::variable) = [1]> dan
        verander [punten v] met (prijs-waarde ::variables)
    end
    als <(type ::variable) = [2]> dan
- verander [levens v] met [1]    
+ zend signaal [prijzen-regen v]
    end
```

\--- /task \---

Now you need to create a new piece of code inside the **Collectable** sprite scripts that will start whenever the `collectable-rain`{:class="block3events"} message is broadcast.

\--- task \---

Add this code for the **Collectable** sprite to make it listen out for the `collectable-rain`{:class="block3events"} broadcast.

```blocks3
+ wanneer ik signaal [prijzen-regen v] ontvang
+ maak [prijs-frequentie v] [0.000001]
+ wacht (1) sec
+ maak [prijs-frequentie v] [1]
```

\--- /task \---

## \--- collapse \---

## title: Wat doet de nieuwe code?

This piece of code waits to receive a broadcast, and responds by setting the `collectable-frequency`{:class="block3variables"} variable to a very small number, then waiting for one second, and then changing the variable back to `1`.

Let's look at how the `collectable-frequency`{:class="block3variables"} variable is used to find out why this makes it rain collectables.

In the main game loop, the part of the code that makes **Collectable** sprite clones gets told by the `collectable-frequency`{:class="block3variables"} variable how long to wait between making one clone and the next:

```blocks3
    herhaal tot <niet <(maak-prijzen ::variables)= [waar]>>
        als < [50] = (willekeurig getal tussen (1) en (50))> dan
            maak [prijs-type v] [2]
        anders
            maak [prijs-type v] [1]
        end
        wacht (prijs-frequentie ::variables) sec
        ga naar x: (willekeurig getal tussen (-240) en (240)) y: (179)
        maak een kloon van [mijzelf v]
    end
```

You can see that the `wait`{:class="block3control"} block here pauses the code for the length of time set by `collectable-frequency`{:class="block3variables"}.

If the value of `collectable-frequency`{:class="block3variables"} is `0.000001`, the `wait`{:class="block3control"} block only pauses for **one millionth** of a second, meaning that the `repeat until`{:class="block3control"} loop will run many more times than normal. As a result, the code is going to create **a lot** more power-ups than it normally would, until `collectable-frequency`{:class="block3variables"} is changed back `1`.

Can you think of any problems that might cause? There’ll be a lot more power-ups…what if you kept catching them?

\--- /collapse \---