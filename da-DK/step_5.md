## Super power-ups!

Now that you have a new power-up collectable working, it’s time to make it do something really cool: Let's make it 'rain' power-ups for a few seconds, instead of just giving out an extra life.

For this, you're going to use another `broadcast`{:class="block3events"} message.

\--- task \--- First, change the `react-to-player`{:class="block3myblocks"} block to broadcast a message when the player character touches a type `2` collectable. Call the message `collectable-rain`{:class="block3events"}.

```blocks3
    define react-to-player (type)
    if <(type ::variable) = [1]> then
        change [points v] by (collectable-value ::variables)
    end
    if <(type ::variable) = [2]> then
-        change [lives v] by [1]    
+        broadcast [collectable-rain v]
    end
```

\--- /task \---

Now you need to create a new piece of code inside the **Collectable** sprite scripts that will start whenever the `collectable-rain`{:class="block3events"} message is broadcast.

\--- task \--- Add this code for the **Collectable** sprite to make it listen out for the `collectable-rain`{:class="block3events"} broadcast.

```blocks3
+    when I receive [collectable-rain v]
+    set [collectable-frequency v] to [0.000001]
+    wait (1) secs
+    set [collectable-frequency v] to [1]
```

\--- /task \---

## \--- collapse \---

## title: What does the new code do?

This piece of code waits to receive a broadcast, and responds by setting the `collectable-frequency`{:class="block3variables"} variable to a very small number, then waiting for one second, and then changing the variable back to `1`.

Let's look at how the `collectable-frequency`{:class="block3variables"} variable is used to find out why this makes it rain collectables.

In the main game loop, the part of the code that makes **Collectable** sprite clones gets told by the `collectable-frequency`{:class="block3variables"} variable how long to wait between making one clone and the next:

```blocks3
    repeat until <not <(create-collectables ::variables) = [true]>>
        if < [50] = (pick random (1) to (50))> then
            set [collectable-type v] to [2]
        else
            set [collectable-type v] to [1]
        end
        wait (collectable-frequency ::variables) secs
        go to x: (pick random (-240) to (240)) y:(179)
        create clone of [myself v]
    end
```

You can see that the `wait`{:class="block3control"} block here pauses the code for the length of time set by `collectable-frequency`{:class="block3variables"}.

If the value of `collectable-frequency`{:class="block3variables"} is `0.000001`, the `wait`{:class="block3control"} block only pauses for **one millionth** of a second, meaning that the `repeat until`{:class="block3control"} loop will run many more times than normal. As a result, the code is going to create **a lot** more power-ups than it normally would, until `collectable-frequency`{:class="block3variables"} is changed back `1`.

Can you think of any problems that might cause? There’ll be a lot more power-ups…what if you kept catching them?

\--- /collapse \---