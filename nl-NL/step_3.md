## Het spel verliezen

Ten eerste! Je hebt een manier nodig om het spel te laten eindigen als de speler geen levens meer heeft. Op dit moment gebeurt dat niet.

Je hebt misschien gemerkt dat het `verlies`{:class="block3myblocks"} **Mijn blokken** blok in het script voor de **Speler** sprite leeg is. Je gaat dit invullen en alle stukken instellen die nodig zijn voor een leuk 'Game over' scherm.

\--- task \---

First, find the `lose`{:class="block3myblocks"} block and complete it with the following code:

```blocks3
    definieer verlies
+ stop [andere scripts in sprite v] :: control stack
+ zend signaal [game over v]
+ ga naar x: (0) y: (0)
+ zeg [Game over!] voor (2) sec
+ stop [alle v]
```

\--- /task \---

## \--- collapse \---

## title: Wat doet deze code?

Whenever the `lose`{:class="block3myblocks"} block runs now, what it does is:

1. Stop de natuurkunde en andere spelscripts die de **Speler** aansturen
2. Vertel alle andere sprites dat de game afgelopen is door een `game over`{:class="block3events"} bericht **uit te zenden**, waar ze op kunnen reageren en aanpassen wat ze doen
3. Verplaats de **Speler** naar het midden van het werkgebied en vertel de speler dat het spel voorbij is
4. Stop alle scripts in het spel

\--- /collapse \---

Now you need to make sure all the sprites know what to do when the game is over, and how to reset themselves when the player starts a new game. **Don’t forget that any new sprites you add also might need code for this!**

### De platforms en randen verbergen

\--- task \---

Start with the easiest sprites. The **Platforms** and **Edges** sprites both need code for appearing when the game starts and disappearing when they receive the `game over`{:class="block3events"} broadcast, so add these blocks to each of them:

```blocks3
+ wanneer ik signaal [game over v] ontvang
+ verdwijn
```

```blocks3
+ wanneer op de groene vlag wordt geklikt
+ verschijn
```

\--- /task \---

### Stop de sterren

Now, if you look at the code for the **Collectable** sprite, you’ll see it works by **cloning** itself. That is, it makes copies of itself that follow the special `when I start as a clone`{:class="block3events"} instructions.

We’ll talk more about what makes clones special when we get to the step about making new and different collectables. For now, what you need to know is that clones can do **almost** everything a normal sprite can, including receiving `broadcast`{:class="block3events"} messages.

Look at how the **Collectable** sprite works. See if you can understand some of its code:

```blocks3
    wanneer op de groene vlag wordt geklikt
    verdwijn
    maak [prijs-waarde v] [1]
    maak [prijs-snelheid v] [1]
    maak [prijs-frequentie v] [1]
    maak [maak-prijzen v] [true]
    maak [prijs-type v] [1]
    herhaal tot < niet <(maak-prijzen) = [waar]>>
        wacht (prijs-frequentie) sec
        ga naar x: (willekeurig getal tussen (-240) tot (240)) y: (179)
        maak een kloon van [mijzelf v]
    end
```

1. Eerst maakt het de originele **Prijs** sprite onzichtbaar door deze te verbergen
2. Vervolgens worden de besturingsvariabelen ingesteld - we komen hier later op terug
3. De variabele `maak-prijzen`{:class="block3variables"} is de aan/uit schakelaar voor klonen: de lus maakt klonen als `maak-prijzen`{:class="block3variables"} `waar` is en doet niets als het niet waar is

\--- task \---

Now set up a block for the **Collectable** sprite so that it reacts to the `game over` broadcast:

```blocks3
+ wanneer ik signaal [game over v] ontvang
+ verdwijn
+ maak [maak-prijzen v] [false]
```

\--- /task \---

This code is similar to the code controlling the **Platforms** and **Edges** sprites. The only difference is that you’re also setting the `create-collectables`{:class="block3variables"} variable to `false` so that no new clones get created when it's 'Game over'.

Note that you can use the `create-collectables`{:class="block3variables"} variable to pass messages from one part of your code to another!