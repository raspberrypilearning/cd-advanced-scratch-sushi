## Perdre la partie

Premières choses d'abord ! Tu dois trouver un moyen de mettre fin au jeu lorsque le joueur est à court de vies. Pour le moment, cela ne se produit pas.

Tu as peut-être remarqué que le bloc `perdre`{: class = "block3myblocks"} de **Mes blocs** dans les scripts du sprite **Personnage du Joueur** est vide. You’re going to fill this in and set up all the pieces needed for a nice 'Game over' screen.

\--- task \---

First, find the `lose`{:class="block3myblocks"} block and complete it with the following code:

```blocks3
    define lose
+    stop [other scripts in sprite v] :: control stack
+    broadcast [game over v]
+    go to x:(0) y:(0)
+    say [Game over!] for (2) secs
+    stop [all v]
```

\--- /task \---

## \--- collapse \---

## title: What does this code do?

Whenever the `lose`{:class="block3myblocks"} block runs now, what it does is:

1. Stop the physics and other game scripts acting on the **Player Character**
2. Tell all the other sprites that the game is over by **broadcasting** a `game over`{:class="block3events"} message they can respond to and change what they're doing
3. Move the **Player Character** to the centre of the Stage and have them tell the player that the game is over
4. Stop all scripts in the game

\--- /collapse \---

Now you need to make sure all the sprites know what to do when the game is over, and how to reset themselves when the player starts a new game. **Don’t forget that any new sprites you add also might need code for this!**

### Hiding the platforms and edges

\--- task \---

Start with the easiest sprites. The **Platforms** and **Edges** sprites both need code for appearing when the game starts and disappearing when they receive the `game over`{:class="block3events"} broadcast, so add these blocks to each of them:

```blocks3
+    when I receive [game over  v]
+    hide
```

```blocks3
+    when green flag clicked
+    show
```

\--- /task \---

### Stopping the stars

Now, if you look at the code for the **Collectable** sprite, you’ll see it works by **cloning** itself. That is, it makes copies of itself that follow the special `when I start as a clone`{:class="block3events"} instructions.

We’ll talk more about what makes clones special when we get to the step about making new and different collectables. For now, what you need to know is that clones can do **almost** everything a normal sprite can, including receiving `broadcast`{:class="block3events"} messages.

Look at how the **Collectable** sprite works. See if you can understand some of its code:

```blocks3
    when green flag clicked
    hide
    set [collectable-value v] to [1]
    set [collectable-speed v] to [1]
    set [collectable-frequency v] to [1]
    set [create-collectables v] to [true]
    set [collectable-type v] to [1]
    repeat until <not <(create-collectables) = [true]>>
        wait (collectable-frequency) secs
        go to x: (pick random (-240) to (240)) y: (179)
        create clone of [myself v]
    end
```

1. First it makes the original **Collectable** sprite invisible by hiding it
2. Then it sets up the control variables — we’ll come back to these later
3. The `create-collectables`{:class="block3variables"} variable is the on/off switch for cloning: the loop creates clones if `create-collectables`{:class="block3variables"} is `true`, and does nothing if it’s not

\--- task \---

Now set up a block for the **Collectable** sprite so that it reacts to the `game over` broadcast:

```blocks3
+    when I receive [game over v]
+    hide
+    set [create-collectables v] to [false]
```

\--- /task \---

This code is similar to the code controlling the **Platforms** and **Edges** sprites. The only difference is that you’re also setting the `create-collectables`{:class="block3variables"} variable to `false` so that no new clones get created when it's 'Game over'.

Note that you can use the `create-collectables`{:class="block3variables"} variable to pass messages from one part of your code to another!