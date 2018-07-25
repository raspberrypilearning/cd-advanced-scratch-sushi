## Super power-ups!

Now that you have a new power-up collectable working, it’s time to make it do something really cool! Let's make it 'rain' power-ups for a few seconds, instead of just giving out an extra life.
 
For this, you need to create a new piece of code inside the **Collectable** sprite scripts that will start while the `react-to-player`{:class="blockmoreblocks"} block is running. To make that happen, you'll use a `receive`{:class="blockevents"} block to listen out for a broadcast from another piece of code inside the sprite. 

+ Add this code for the **Collectable** sprite. Let’s call the broadcast it's listening out for `collectable-rain`{:class="blockevents"}.

```blocks
    when I receive [collectable-rain v]
    set [collectable-frequency v] to [0.000001]
    wait (1) secs
    set [collectable-frequency v] to [1]
```

--- collapse ---
---
title: What does the new code do?
---

In the main game loop, the part of the code that makes **Collectable** sprite clones gets told by the `collectable-frequency`{:class="blockdata"} variable how long to wait between making one clone and the next.

All the code does is wait to receive a broadcast, and then respond by setting the `collectable-frequency`{:class="blockdata"} variable to a very small number \(change it to different values and see what happens!\), then waiting for one second, and then changing the variable back to `1`.

Think about what’s happening during the second when `collectable-frequency`{:class="blockdata"} is very small: the `when green flag clicked`{:class="blockevents"} code is still running, and the `repeat until`{:class="blockcontrol"} loop in it is looping. Look at the code in that loop: 

```blocks
    repeat until <not <(create-collectables) = [true]>>
        if < [50] = (pick random (1) to (50))> then
            set [collectable-type v] to [2]
        else
            set [collectable-type v] to [1]
        end
        wait (collectable-frequency) secs
        go to x: (pick random (-240) to (240)) y:(179)
        create clone of [myself v]
    end
```

You can see that the `wait` block here pauses the code for the length of time set by `collectable-frequency`{:class="blockdata"}. So if the value of `collectable-frequency`{:class="blockdata"} changes to `0.000001`, the `wait` block only pauses for **one millionth** of a second, meaning that the `repeat until`{:class="blockcontrol"} loop will run many more times than normal. As a result, the code is going to create **a lot** more power-ups than it normally would, until `collectable-frequency`{:class="blockdata"} changes back `1`.

Can you think of any problems that might cause? There’ll be a lot more power-ups…what if you kept catching them?

--- /collapse ---

Now you have the **Collectable** sprite ready to receive a `collectable-rain`{:class="blockevents"} broadcast, but you haven't made code for sending that broadcast yet!

+ This is very easy: inside the **Collectable** sprite scripts, update the `react-to-player`{:class="blockmoreblocks"} block to  broadcast the `collectable-rain`{:class="blockevents"} message when the player character touches a type `2` collectable. 

```blocks
    define react-to-player (type)
    if <(type) = [1]> then
        change [points v] by (collectable-value)
    end
    if <(type) = [2]> then
        broadcast [collectable-rain v]
    end
```

### Challenge: get creative!
 
+ Based on this card and the previous one, you can now make as many different power-up collectables as you want! What about one that gives out 20 times the usual number of points, or adds three lives, or makes it so the player can’t run out of lives for a period of time? Come up with some cool power-ups and see if you can make them!
