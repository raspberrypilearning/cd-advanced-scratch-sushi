## Losing the game

First things first! You need a way to make the game end when the player has run out of lives. At the moment that doesn't happen.

You may have noticed that the `lose`{:class="block3myblocks"} **My blocks** block in the scripts for the **Player Character** sprite is empty. You’re going to fill this in and set up all the pieces needed for a nice 'Game over' screen.

+ First, find the `lose`{:class="block3myblocks"} block and complete it with the following code: 

![blocks_1546298722_611725](images/blocks_1546298722_611725.png)

--- collapse ---
---
title: What does this code do?
---

Whenever the `lose`{:class="block3myblocks"} block runs now, what it does is: 

1. Stop the physics and other game scripts acting on the **Player Character**
1. Tell all the other sprites that the game is over by **broadcasting** a `game over` message they can respond to and change what they're doing
1. Move the **Player Character** to the centre of the Stage and have them tell the player that the game is over
1. Stop all scripts in the game

--- /collapse ---

Now you need to make sure all the sprites know what to do when the game is over, and how to reset themselves when the player starts a new game. **Don’t forget that any new sprites you add also might need code for this!**

### Hiding the platforms and edges

+ Start with the easiest sprites ones. The **Platforms** and **Edges** sprites both need code for appearing when the game starts and disappearing when they receive the `game over` broadcast, so add these blocks to each of them:

![blocks_1546298725_630257](images/blocks_1546298725_630257.png)

![blocks_1546298726_7044969](images/blocks_1546298726_7044969.png)

### Stopping the stars

Now, if you look at the code for the **Collectable** sprite, you’ll see it works by **cloning** itself. That is, it makes copies of itself that follow the special `when I start as a clone`{:class="block3events"} instructions. 

We’ll talk more about what makes clones special when we get to the Card about making new and different collectables. For now, what you need to know is that clones can do **almost** everything a normal sprite can, including receiving `broadcast`{:class="block3events"} messages.

+ Let’s look at how the **Collectable** sprite works. See if you can understand some of its code: 

![blocks_1546298727_767671](images/blocks_1546298727_767671.png)

1. First it makes the original **Collectable** sprite invisible by hiding it
1. Then it sets up the control variables — we’ll come back to these later
1. The `create-collectables`{:class="block3variables"} variable is the on/off switch for cloning: the loop creates clones if `create-collectables`{:class="block3variables"} is `true`, and does nothing if it’s not

+ Now you need to set up a block for the **Collectable**  sprite so that it reacts to the `game over` broadcast:

![blocks_1546298728_940563](images/blocks_1546298728_940563.png)

This code is similar to the code controlling the **Platforms** and **Edges** sprites. The only difference is that you’re also setting the `create-collectables`{:class="block3variables"} variable to `false` so that no new clones get created when it's 'Game over'. 
 
+ Note that you can use the `create-collectables`{:class="block3variables"} variable to pass messages from one part of your code to another! 
