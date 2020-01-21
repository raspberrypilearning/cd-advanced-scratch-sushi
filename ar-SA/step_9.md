## منصات متحركة

السبب في أنني طلبت منك استخدام نسختي من المستوى 2 هو الفجوة التي قد تكون لاحظتها في منتصف التصميم. ستقوم بإنشاء منصة تتحرك من خلال هذه الفجوة والتي يمكن للاعب القفز عليها وركوبها!

![مستوى آخر مع منصات مختلفة](images/movingPlatforms.png)

أولاً ، ستحتاج كائن للمنصة.

\--- task \---

Add a new sprite, name it **Moving-Platform**, and using the costume customisation tools in the Costumes tab to make it look like the other platforms \(use vector mode\).

\--- /task \---

Now, let's add some code to the sprite.

Begin with the basics: to make a never-ending set of platforms moving up the screen, you’ll need to clone the platform at regular intervals. I picked `4` seconds as my interval. You also need to make sure that there’s an on/off switch for making the platforms, so that they don’t show up in level 1. I’m using a new variable called `create-platforms`{:class="block3variables"}.

\--- task \---

Add code to create clones of your platform sprite.

Here's how mine looks so far:

```blocks3
+ عند نقر العلم الأخضر
+ إخفاء
+ إلى الأبد
       wait (4) secs
        if <(create-platforms ::variables) = [true]> then
            create clone of [myself v]
        end
    end
```

\--- /task \---

\--- task \---

Then add the clone's code:

```blocks3
+ عندما أبدأ كـ نسخة
+ إظهار
+ للأبد
       if <(y position) < [180]> then
            change y by (1)
            wait (0.02) secs
        else
            delete this clone
        end
    end
```

\--- /task \---

This code makes the **Moving-Platform** clone move up to the top of the screen, slowly enough for the player to jump on and off, and then disappear.

\--- task \---

Now make the platforms disappear/reappear based on the broadcasts that change levels (so they're only on the level with space for them), and the `game over`{:class="block3events"} message.

```blocks3
+ عندما أتلقى [level-1 v]
+ اضبط  [create-platform v] إلى [false]
+ اخفاء

+ عندما أتلقى [level-2 v]
+ اضبط  [create-platforms v] إلى [true]

+ تلقي [game over v]
+ اخفاء
+ اضبط [create-platform v] إلى [false]
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
    <<touching [Platforms v] ?> أو <touching [Moving-Platform v] ?>>
```

\--- /task \---