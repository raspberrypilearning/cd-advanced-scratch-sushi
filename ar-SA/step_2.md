## ضبط الأمور

نظرًا لأنك تتعلم كيفية الترميز في Scratch وليس كيفية إنشاء محرك للفيزياء (الكود الذي يجعل الأشياء في لعبة كمبيوتر تتصرف مثل الكائنات في العالم الحقيقي ، على سبيل المثال ، لا تتساقط خلال الأرضيات) ، فسوف تبدأ بـ مشروع قمت بإنشائه يحتوي بالفعل على أساسيات الحركة والقفز واكتشاف الأنظمة الأساسية المضمنة.

يجب إلقاء نظرة سريعة على المشروع ، بما في ذلك التفاصيل الموجودة في هذه البطاقة ، لأنك ستجري بعض التغييرات عليه لاحقًا ، لكنك لست بحاجة إلى فهم كل ما يتم فعله!

### الحصول على المشروع

\--- task \---

The first thing you’ll need to do is to get a copy of the Scratch code from [dojo.soy/advanced-scratch](http://dojo.soy/advanced-scratch){:target="_blank"} .

To use the project offline, download it by clicking **See Inside**, then go to the **File** menu and click **Download to your computer**. Then you can open the downloaded file in Scratch on your computer.

You can also use it directly in Scratch in your browser by just clicking **See Inside** and then **Remix**.

\--- /task \---

### ألقِ نظرة على الكود

The physics engine of the game has a variety of pieces in it, some of which work already and some of which don’t yet. You can test this out by running the game and trying to play it.

You'll see that you can lose lives, but nothing happens when you run out. Also, the game only has one level, one type of thing to collect, and no enemies. You’re going to fix all of that, and a then do a bit more!

\--- task \---

Take a look at how the code is put together.

\--- /task \---

It uses lots of **My blocks** blocks, which are great for splitting your code up into pieces so you can manage it better. A **My blocks** block is a block you make up out of a lot of other blocks, and you can give some instructions to it. You'll see how it works in an upcoming step!

![](images/setup2and3.png)

### كتل "لبناتي" مفيدة حقاً

In the code above, the main game `forever`{:class="block3control"} loop calls the `main-physics`{:class="block3myblocks"} **My blocks** block to do a whole lot of stuff! Keeping the blocks separated like this makes it easy to read the main loop and understand what happens in the game, without worrying about **how** it happens.

\--- task \---

Now look at the `reset game`{:class="block3myblocks"} and `reset character`{:class="block3myblocks"} **My blocks** blocks.

\--- /task \---

They do pretty normal things, such as setting up variables and making sure the character rotates properly

- إن كتلة ` إعادة-تعيين-لعبة ` {: class = "block3myblocks"} ** تستدعي الكتلة ** ` إعادة-تعيين-شخصية ` {: class = "block3myblocks"} ، وهذا يوضح لك أنه يمكنك استخدام كتلة ** لبناتي ** داخل كتلة **لبناتي ** اخرى
- كتلة ` إعادة-تعيين-شخصية` {: class = "block3myblocks"} في كتل**لبناتي** يستخدم في مكانين مختلفين في اللبنة الرئيسية. هذا يعني أنه يمكنك تغيير مكانين في حلقة اللعبة الرئيسية عن طريق تغيير الكود داخل قائمة **لبناتي** ، مما يوفر لك الكثير من العمل ويساعدك على تجنب الأخطاء.