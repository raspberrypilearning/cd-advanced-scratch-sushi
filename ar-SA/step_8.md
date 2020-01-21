## المستوى ٢

مع هذه الخطوة ، ستقوم بإضافة مستوى جديد إلى اللعبة يمكن للاعب الوصول إليها بمجرد الضغط على الزر. في وقت لاحق ، يمكنك تغيير الكود الخاص بك لجعله يحتاج إلى عدد معين من النقاط ، أو أي شيء آخر ، للوصول إلى هناك.

### الانتقال إلى المستوى التالي

\--- task \---

First, create a new sprite as a button by either adding one from the library or drawing your own. I did a bit of both and came up with this:

![The button sprite to switch levels](images/levelButton.png)

\--- /task \---

\--- task \---

Now, the code for this button is clever: it’s designed so that every time you click it it will take you to the next level, no matter how many levels there are.

Add these scripts to your **Button** sprite. You will need to create some variables as you do so.

```blocks3
+    عند النقر على العلم الاخضر
+    set [max-level v] to [2]
+    set [min-level v] to [1]
+    set [current-level v] to [1]
```

```blocks3
+ عند النقر فوق هذا الكائن
+ قم بتغيير [المستوى-الحالي v] بمقدار (1)
+ إذا <(المستوى الحالي) > (المستوى الأعلى :: المتغيرات)> ثم
      set [current-level v] to (min-level ::variables)
    end  
+ نشر [تحصيل-الربح]
+ نشر (انضمام [level-](المستوى الحالي))
```

\--- /task \---

Can you see how the program will use the variables you created?

+ `المستوى الأقصى ` {: class = "block3variables"} يخزن أعلى مستوى
+ `المستوى الادنى` {: class = "block3variables"} يخزن أقل مستوى
+ ` المستوى الحالي ` {: class = "block3variables"} يخزن المستوى الذي يكون عليه اللاعب الآن

These all need to be set by the programmer \(you!\), so if you add a third level, don’t forget to change the value of `max-level`{:class="block3variables"}! `min-level`{:class="block3variables"} will never need to change, of course.

The broadcasts are used to tell the other sprites which level to display, and to clear up the collectables when a new level starts.

### اجعل الكائنات تتفاعل

#### كائنات الـ**مقتنيات**

Now you need to get the other sprites to respond to these broadcasts! Start with the easiest one: clearing all the collectables.

\--- task \---

Add the following code to the **Collectable** sprite scripts to tell all its clones to `hide`{:class="block3vlooks"} when they receive the cleanup broadcast:

```blocks3
+ عندما أتلقى [collectable-cleanup v]
+ اخفاء
```

\--- /task \---

Since one of the first things any new clone does is show itself, you don't have to worry about unhiding collectables!

#### كائنات الـ**منصات**

Now to switch the **Platforms** sprite. You can design your own new level later if you like, but for now let’s use the one I’ve already included — you’ll see why on the next step!

\--- task \---

Add this code to the **Platforms** sprite:

```blocks3
+ عندما أتلقى [المستوى 1 v]
+ بدل الزي إلى [المستوى 1 v]
+ العرض
```

```blocks3
+ عندما أتلقى [المستوى-2 v]
+ بدل الزي إلى [المستوى 2 v]
+ العرض
```

\--- /task \---

It receives the `joined`{:class="block3operators"} messages of `level-`{:class="block3variables"} and `current-level`{:class="block3variables"} that the **Button** sprite sends out, and responds by changing the **Platforms** costume.

#### كائن **العدو**

\--- task \---

In the **Enemy** sprite scripts, just make sure the sprite disappears when the player enters level 2, like this:

```blocks3
+ عندما أتلقى [المستوى-1 v]
+ العرض
```

```blocks3
+ عندما أتلقى [المستوى-2 v]
+ إخفاء
```

\--- /task \---

If you prefer, you can make the enemy move to another platform instead. In that case, you would use a `go to`{:class="block3motion"} block instead of the `show`{:class="block3looks"} and `hide`{:class="block3looks"} blocks.

### اجعل ** شخصية اللاعب** تظهر في المكان المناسب

Whenever a new level starts, the **Player Character** sprite needs to go to the right place for that level. To make this happen, you need to change where the sprite gets its coordinates from when it first appears on the Stage. At the moment, there are fixed `x` and `y` values in its code.

\--- task \---

Begin by creating variables for the starting coordinates: `start-x`{:class="block3variables"} and `start-y`{:class="block3variables"}. Then plug them into the `go to`{:class="block3motion"} block in the `reset-character`{:class="block3myblocks"} **My blocks** block instead of the fixed `x` and `y` values:

```blocks3
    حدد إعادة تعيين الشخصية
    set [can-jump v] to [true]
    set [x-velocity v] to [0]
    set [y-velocity v] to [-0]
+ انتقل إلى  x: (start-x) y: (start-y)
```

\--- /task \---

\--- task \---

Then for each broadcast announcing the start of a level, set the right `start-x`{:class="block3variables"} and `start-y`{:class="block3variables"} coordinates in response, and add a **call** to `reset-character`{:class="block3myblocks"}:

```blocks3
+ عندما أتلقى [level-1 v]
+ اضبط [start-x v] الى [-183]
+ set [start-y v] إلى [42]
+اعادة الشخصية :: الزي
```

```blocks3
+ عندما أتلقى [level-2 v]
+ set [start-x v] إلى [-218]
+ set [start-y v] إلى [-143]
+ اعادة الشخصية :: الزي
```

\--- /task \---

### بدءا من المستوى 1

You also need to make sure that every time someone starts the game, the first level they play is level 1.

\--- task \---

Go to the `reset-game`{:class="block3myblocks"} script and remove the call to `reset-character`{:class="block3myblocks"} from it. In its place, broadcast the `min-level`{:class="block3variables"}. The code you've already added with this card will then set up the correct starting coordinates for the **Player Character** sprite, and also call `reset-character`{:class="block3myblocks"}.

```blocks3
    تحديد اعادة تعيين اللعبة
    set rotation style [left-right v]
    set [jump-height v] to [15]
    set [gravity v] to [2]
    set [x-speed v] to [1]
    set [y-speed v] to [1]
    set [lives v] to [3]
    set [points v] to [0]
+ النشر (انضم [level-] (المستوى-المتوسط::المتغيرات))
```

\--- /task \---

## \--- collapse \---

## title: إعادة تعيين شخصية اللاعب مقابل إعادة تعيين اللعبة

Notice that the first block in the **Player Character** sprite's main green flag script is a call to the `reset-game`{:class="block3myblocks"} **My blocks** block.

This block sets up all the variables for a new game and then calls the `reset-character`{:class="block3myblocks"} **My blocks** block, which places the character back in its correct starting position.

Having the `reset-character`{:class="block3myblocks"} code in its own block separate from `reset-game`{:class="block3myblocks"} allows you to reset the character to different positions **without** having to reset the whole game.

\--- /collapse \---