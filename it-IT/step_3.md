## Perdere al gioco

Cominciando dall'inizio! Hai bisogno di un metodo per far finire il gioco quando il giocatore ha esaurito le vite. Al momento ciò non succede.

Potresti aver notato che il blocco `perso`{:class="block3myblocks"} de **I Miei Blocchi** negli script per lo sprite di **Personaggio-giocatore** è vuoto. La riempirai e imposterai tutti i pezzi necessari per una bella schermata 'Game over'.

\--- task \---

First, find the `lose`{:class="block3myblocks"} block and complete it with the following code:

```blocks3
    definisci perso
+ ferma [other scripts in sprite v]
+ invia a tutti [game over v]
+ vai a x: (0) y: (0)
+ dire [Game over!] per (2) secondi
+ ferma [all v]
```

\--- /task \---

## \--- collapse \---

## title: Cosa fa questo codice?

Whenever the `lose`{:class="block3myblocks"} block runs now, what it does is:

1. Fermare le leggi fisiche e altri script di gioco che agiscono sul personaggio **Personaggio-giocatore**
2. Dice a tutti gli altri sprite che il gioco è finito trasmettendo con il **broadcasting** a `game over`{:class="block3events"} un messaggio a cui tutti gli sprite possono reagire, cambiando il loro comportamento
3. Muove il personaggio **Personaggio-giocatore** al centro dello schermo e gli fa dire al giocatore che il gioco è finito
4. Interrompe tutti gli script nel gioco

\--- /collapse \---

Now you need to make sure all the sprites know what to do when the game is over, and how to reset themselves when the player starts a new game. **Don’t forget that any new sprites you add also might need code for this!**

### Nascondere le piattaforme e i bordi

\--- task \---

Start with the easiest sprites. The **Platforms** and **Edges** sprites both need code for appearing when the game starts and disappearing when they receive the `game over`{:class="block3events"} broadcast, so add these blocks to each of them:

```blocks3
+ quando ricevo [game over v]
+ nascondi
```

```blocks3
+ quando si clicca sulla bandiera verde
+ mostra
```

\--- /task \---

### Fermare le stelle

Now, if you look at the code for the **Collectable** sprite, you’ll see it works by **cloning** itself. That is, it makes copies of itself that follow the special `when I start as a clone`{:class="block3events"} instructions.

We’ll talk more about what makes clones special when we get to the step about making new and different collectables. For now, what you need to know is that clones can do **almost** everything a normal sprite can, including receiving `broadcast`{:class="block3events"} messages.

Look at how the **Collectable** sprite works. See if you can understand some of its code:

```blocks3
    quando si clicca sulla bandiera verde
nascondi
porta [catturabili-valore v] a [1]
porta [catturabili-velocita v] a [1]
porta [catturabili-frequenza v] a [1]
porta [crea-catturabili v] a [true]
porta [catturabili-tipo v] a [1]
repeat until <not <(create-collectables) = [true]>>
attendi (collectable-frequenza) secondi
vai a x: (numero a caso tra (-240) e (240)) y: (179)
crea clone di [myself v]
end
```

1. Per prima cosa rende invisibile l'originale **Catturabili** nascondendolo
2. Quindi imposta le variabili di controllo - torneremo su queste più tardi
3. La variabile `crea-catturabili`{: class = "block3variables"} è l'interruttore on/off per la clonazione: il ciclo crea cloni se `crea-catturabili`{:class="block3variables"} è `true` e non fa nulla se non lo è

\--- task \---

Now set up a block for the **Collectable** sprite so that it reacts to the `game over` broadcast:

```blocks3
+ quando ricevo [game over v]
+ nascondi
+ porta [crea-catturabili v] a [false]
```

\--- /task \---

This code is similar to the code controlling the **Platforms** and **Edges** sprites. The only difference is that you’re also setting the `create-collectables`{:class="block3variables"} variable to `false` so that no new clones get created when it's 'Game over'.

Note that you can use the `create-collectables`{:class="block3variables"} variable to pass messages from one part of your code to another!