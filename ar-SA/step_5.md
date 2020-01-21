## امدادات طاقة خارقة!

الآن بعد أن أصبح لديك عمل جديد قابل للتحصيل ، فقد حان الوقت لجعله يفعل شيئًا رائعًا حقًا: دعنا نجعله ينطلق من طاقة من الكهرباء لبضع ثوانٍ ، بدلاً من مجرد إعطاء حياة إضافية.

لهذا، ستقوم باستخدام رسالة `بث`{:class="block3events"} آخرى.

\--- task \---

First, change the `react-to-player`{:class="block3myblocks"} block to broadcast a message when the player character touches a type `2` collectable. Call the message `collectable-rain`{:class="block3events"}.

```blocks3
    حدد رد الفعل على اللاعب (النوع)
    إذا كان <(type::variable) = [1]> ثم
        [point v] بواسطة (قيم-المقتنيات::variables)
    end
    if <(type::variable) = [2]> ثم
- تغيير [lives v] بحلول [1]    
+ البث [تحصيل-المطر v]
    نهاية
```

\--- /task \---

Now you need to create a new piece of code inside the **Collectable** sprite scripts that will start whenever the `collectable-rain`{:class="block3events"} message is broadcast.

\--- task \---

Add this code for the **Collectable** sprite to make it listen out for the `collectable-rain`{:class="block3events"} broadcast.

```blocks3
+ عندما أتلقى [collectable-rain v]
+ مجموعة [collectable-frequency v] إلى [0.000001]
+ انتظر (1) ثوانٍ
+ مجموعة [collectable-frequency v] إلى [1]
```

\--- /task \---

## \--- collapse \---

## title: ماذا تفعل المقاطع الجديدة؟

This piece of code waits to receive a broadcast, and responds by setting the `collectable-frequency`{:class="block3variables"} variable to a very small number, then waiting for one second, and then changing the variable back to `1`.

Let's look at how the `collectable-frequency`{:class="block3variables"} variable is used to find out why this makes it rain collectables.

In the main game loop, the part of the code that makes **Collectable** sprite clones gets told by the `collectable-frequency`{:class="block3variables"} variable how long to wait between making one clone and the next:

```blocks3
    كرر حتى <not <(create-collectables ::variables) = [true]>>
        إذا < [50] = (pick random (1) to (50))> ثم
            مجموعة [collectable-type v] إلى [2]
        آخر
            مجموعة [collectable-type v] إلى [1]
        نهاية
        الانتظار (collectable-frequency ::variables) بالثواني
        انتقل إلى x: (pick random (-240) to (240)) y:(179)
        بإنشاء استنساخ لـ [myself v]
    النهاية
```

You can see that the `wait`{:class="block3control"} block here pauses the code for the length of time set by `collectable-frequency`{:class="block3variables"}.

If the value of `collectable-frequency`{:class="block3variables"} is `0.000001`, the `wait`{:class="block3control"} block only pauses for **one millionth** of a second, meaning that the `repeat until`{:class="block3control"} loop will run many more times than normal. As a result, the code is going to create **a lot** more power-ups than it normally would, until `collectable-frequency`{:class="block3variables"} is changed back `1`.

Can you think of any problems that might cause? There’ll be a lot more power-ups…what if you kept catching them?

\--- /collapse \---