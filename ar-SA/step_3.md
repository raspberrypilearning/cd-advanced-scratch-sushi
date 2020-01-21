## خسارة اللعبة

اهم الاشياء اولا! تحتاج إلى طريقة لإنهاء اللعبة عندما تنفذ ارواح اللاعب. في الوقت الحالي لا يحدث ذلك.

ربما لاحظت أن كتلة `اخسر`{: class = "block3myblocks"} في كتل **لبناتي** في النص البرمجي للكائن **شخصية اللاعب** فارغة. ستقوم بملئها وإعداد جميع القطع اللازمة لشاشة جميلة لـ"انتهت اللعبة".

\--- task \---

First, find the `lose`{:class="block3myblocks"} block and complete it with the following code:

```blocks3
    define اخسر
+   اوقف  [المقاطع الاخرى في الكائن v] :: control stack
+    بث [انتهت اللعبة v]
+    go to x:(0) y:(0)
+    say [انتهت اللعبة!] for (2) secs
+    stop [الكل v]
```

\--- /task \---

## \--- collapse \---

## title: ماذا يفعل هذا الرمز؟

Whenever the `lose`{:class="block3myblocks"} block runs now, what it does is:

1. وقف الفيزياء وغيرها من النصوص البرمجية للعبة والتي تعمل على **شخصية اللاعب**
2. تخبر كل الكائنات ألاخرى أن اللعبة قد انتهت عن طريق **بث** الرسالة `انتهت اللعبة` {:class="block3events"} والتي يستجيبوا لها ويغيروا ما كانوا يقومون به
3. تنقل **شخصية اللاعب** إلى مركز المسرح وتطلب منهم إخبار اللاعب بأن اللعبة قد انتهت
4. وقف جميع النصوص النصية في اللعبة

\--- /collapse \---

Now you need to make sure all the sprites know what to do when the game is over, and how to reset themselves when the player starts a new game. **Don’t forget that any new sprites you add also might need code for this!**

### إخفاء المنصات والحواف

\--- task \---

Start with the easiest sprites. The **Platforms** and **Edges** sprites both need code for appearing when the game starts and disappearing when they receive the `game over`{:class="block3events"} broadcast, so add these blocks to each of them:

```blocks3
+ عندما أتلقى [انتهت اللعبة v]
+ إخفاء
```

```blocks3
+ عندما نقر العلم الأخضر
+ عرض
```

\--- /task \---

### وقف النجوم

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

1. أولا يجعل كائن **تجميع** الاصلي غير مرئي عن طريق إخفائه
2. يقوم بإعداد متغيرات التحكم - سنعود إليها لاحقًا
3. إن متغير `create-collectables` {:class="block3variables"} هو مفتاح التشغيل/الاطفاء للاستنساخ: الحلقة التكرارية تقوم بانشاء نسخ اذا كان `create-collectables`{:class="block3variables"} `true` ولا تعمل شيء اذا لم يكن كذلك

\--- task \---

Now set up a block for the **Collectable** sprite so that it reacts to the `game over` broadcast:

```blocks3
+ عندما أتلقى [انتهت اللعبة v]
+ إخفاء
+ set [create-collectables v] إلى [false]
```

\--- /task \---

This code is similar to the code controlling the **Platforms** and **Edges** sprites. The only difference is that you’re also setting the `create-collectables`{:class="block3variables"} variable to `false` so that no new clones get created when it's 'Game over'.

Note that you can use the `create-collectables`{:class="block3variables"} variable to pass messages from one part of your code to another!