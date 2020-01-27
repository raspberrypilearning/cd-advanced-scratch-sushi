## امدادات طاقة خارقة!

الآن بعد أن أصبح لديك عمل جديد قابل للتحصيل ، فقد حان الوقت لجعله يفعل شيئًا رائعًا حقًا: دعنا نجعله ينطلق من طاقة من الكهرباء لبضع ثوانٍ ، بدلاً من مجرد إعطاء حياة إضافية.

لهذا، ستقوم باستخدام رسالة `بث`{:class="block3events"} آخرى.

\--- task \---

أولاً ، قم بتغيير كتلة `react-to-player`{:class="block3myblocks"} لبث رسالة عندما تلمس شخصية اللاعب النوع `2` تحصيل. استدعي الرسالة ` collectable-rain ` {:class="block3events"}.

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

أنت الآن بحاجة إلى إنشاء جزء جديد من التعليمات البرمجية داخل البرامج النصية العفوية **مقتنيات** التي ستبدأ كلما تم بث الرسالة `collectable-rain`{:class="block3events"}.

\--- task \---

أضف هذا الرمز للكائن **المقتنيات** لجعله يستمع إلى بث `collectable-rain`{:class="block3events"}.

```blocks3
+ عندما أتلقى [collectable-rain v]
+ مجموعة [collectable-frequency v] إلى [0.000001]
+ انتظر (1) ثوانٍ
+ مجموعة [collectable-frequency v] إلى [1]
```

\--- /task \---

## \--- collapse \---

## title: ماذا تفعل المقاطع الجديدة؟

ينتظر جزء الكود هذا تلقي بث ، ويستجيب عن طريق تعيين المتغير `collectable-frequency`{:class="block3variables"} على رقم صغير جدًا ، ثم الانتظار لثانية واحدة ، ثم تغيير المتغير إلى `1`.

دعونا نلقي نظرة على كيفية استخدام المتغير `collectable-frequency`{:class="block3variables"} لمعرفة سبب جعله أمطارًا قابلة للتحصيل.

في حلقة اللعبة الرئيسية ، يتم إخبار جزء الكود الذي يجعل نسخ الكائن **مقتنيات** بواسطة المتغير `collectable-frequency`{:class="block3variables"} كم من الوقت يجب الانتظار بين عمل نسخة والاخرى:

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

يمكنك أن ترى أن `الكتلة هنا `{:class="block3control"} تتوقف مؤقتًا عن الكود طول المدة المحددة بواسطة `collectable-frequency`{:class="block3variables"}.

إذا كانت قيمة `collectable-frequency`{:class="block3variables"} هي `0.000001`، و كتلة `الانتظار`{:class="block3control"} تتوقف لمدة **1000000** من الثانية، وهذا يعني أنه سيتم تشغيل الحلقة `كرر حتى`{:class="block3control"} مرات أكثر من المعتاد. ونتيجة لذلك، سيؤدي الى صنع **الكثير** والكثير من زيادة الطاقات ، حتى يتغير `collectable-frequency`{:class= "block3variables"} مجدداً الى `1`.

هل يمكنك التفكير في أي مشاكل قد تحدث؟ سيكون هناك الكثير من امدادات الطاقة…ماذا لو واصلت الإمساك بها؟

\--- /collapse \---