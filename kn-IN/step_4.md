## ಪವರ್-ಅಪ್ ಗಳು

ಈ ಸಮಯದಲ್ಲಿ ನೀವು ಕೇವಲ ಒಂದು ಬಗೆಯ ಸಂಗ್ರಹಯೋಗ್ಯತೆ(collectable) ಯನ್ನು ಹೊಂದಿದ್ದೀರಿ: ಅದು ನಿಮ್ಮದಾಗಿಸಿದರೆ ಒಂದು ಅಂಕೆ ಕೊಡುವ ನಕ್ಷತ್ರವಾಗಿರುತದೆ. ಈ ಕಾರ್ಡ್‌ನಲ್ಲಿ, ನೀವು ಹೊಸ ಪ್ರಕಾರದ ಸಂಗ್ರಹಯೋಗ್ಯತೆಯನ್ನು ರಚಿಸಲಿದ್ದೀರಿ, ಮತ್ತು ನೀವು ಅದನ್ನು ಇತರ ರೀತಿಯ ಸಂಗ್ರಹಣೆಯನ್ನು ಸುಲಭವಾಗಿ ಸೇರಿಸುವ ರೀತಿಯಲ್ಲಿ ಮಾಡುತ್ತೀರಿ. ನಂತರ ನೀವು ನಿಮ್ಮ ಸ್ವಂತ ಪವರ್-ಅಪ್‌ಗಳು ಮತ್ತು ಬೋನಸ್‌ಗಳನ್ನು ಆವಿಷ್ಕರಿಸಬಹುದು ಮತ್ತು ಆಟವನ್ನು ನಿಜವಾಗಿಯೂ ನಿಮ್ಮದಾಗಿಸಿಕೊಳ್ಳಬಹುದು!

ಇದನ್ನು ಮಾಡಲು ನಾವು ಈಗಾಗಲೇ `collectable-type`{:class="block3variables"} ವೇರಿಯಬಲ್ ಮತ್ತು `pick-costume`{:class="block3myblocks"} **My blocks** ಬ್ಲಾಕ್ ಗಳನ್ನು ಉಪಯೋಗಿಸಿ ಕೆಲವು ಭಾಗಗಳನ್ನು ಸೇರಿಸಿದ್ದೇವೆ. ಆದರೂ ನೀವು ಅವುಗಳನ್ನು ಸುಧಾರಿಸಬೇಕಾಗಿದೆ.

ಸಂಗ್ರಹಿಸಬಹುದಾದ ಕಾರ್ಯವು ಇದೀಗ ಹೇಗೆ ಕಾರ್ಯನಿರ್ವಹಿಸುತ್ತದೆ ಎಂಬುದನ್ನು ನೋಡೋಣ.

**Collectable** sprite ಸ್ಕ್ರಿಪ್ಟ್‌ಗಳಲ್ಲಿ, `when I start as a clone`{:class="block3events"} ಕೋಡ್ ಅನ್ನು ಹುಡುಕಿ. ನಕ್ಷತ್ರಗಳನ್ನು ಸಂಗ್ರಹಿಸುವ ಮೂಲಕ ನಿಮಗೆ ಅಂಕಗಳನ್ನು ಕೊಡುವ ಬ್ಲಾಕ್ ಗಳನ್ನು ಗಮನಿಸಿ:

```blocks3
    if <touching [Player Character v]?> then
        change [points v] by (collectable-value ::variables)
        delete this clone
```

ಮತ್ತು ಕ್ಲೋನ್‌ಗಾಗಿ ವೇಷಭೂಷಣವನ್ನು ಆಯ್ಕೆ ಮಾಡುವುದು ಇದು:

```blocks3
    pick-costume (collectable-type ::variables) :: custom
```

--- collapse ---
---
title: ವೇಷಭೂಷಣವನ್ನು ಆರಿಸುವುದು ಹೇಗೆ ಕೆಲಸ ಮಾಡುತ್ತದೆ?
---

`pick-costume`{:class="block3myblocks"} ಬ್ಲಾಕ್ ಮತ್ತು `lose`{:class="block3myblocks"} ಬ್ಲಾಕ್ ಕೆಲವು ವಿಧದಲ್ಲಿ ಒಂದೇ ರೀತಿ ಕಾರ್ಯ ನಿರ್ವಹಿಸುತ್ತದೆ, ಆದರೆ ಇದರಲ್ಲಿ ಸ್ವಲ್ಪ ಹೆಚ್ಚಿನ ವಿಷಯ ಇದೆ: ಅಂದರೆ ಇದು `type`{:class="block3myblocks"} ಎಂದು ಕರೆಯಲ್ಪಡುವ ಇನ್ಪುಟ್ \(**input**\) ವೇರಿಯೇಬಲ್ ಅನ್ನು ಪಡೆಯುತದೆ.

```blocks3
    define pick-costume (type)
    if <(type ::variables) = [1]> then
        switch costume to [star1 v]
    end
```

`pick-costume`{:class="block3myblocks"} ಬ್ಲಾಕ್ ರನ್ ಆದಾಗ, ಅದು ಈ ಕೆಳಗಿನದನ್ನು ಮಾಡುತ್ತದೆ:

1. ಇದು `type`{:class="block3myblocks"} ಎಂಬ ಇನ್ಪುಟ್ ವೇರಿಯೇಬಲ್ ಅನ್ನು ಪರಿಶೀಲಿಸುತ್ತದೆ
2. `type`{:class="block3myblocks"} ನ ಮೌಲ್ಯವು `1`ಕ್ಕೆ ಸಮವಾಗಿದ್ದರೆ, ಇದು `star1` ವೇಷಭೂಷಣಕ್ಕೆ\(ಕಾಸ್ಟ್ಯೂಮ್\) ಬದಲಾಗುತ್ತದೆ

ಬ್ಲಾಕ್ ಅನ್ನು ಬಳಸುವ ಸ್ಕ್ರಿಪ್ಟ್‌ನ ಭಾಗವನ್ನು ನೋಡೋಣ:

```blocks3
    when I start as a clone
    pick-costume (collectable-type ::variables) :: custom
    show
    repeat until <(y position) < [-170]>
        change y by (collectable-speed ::variables)
        if <touching [Player Character v]?> then
            change [points v] by (collectable-value ::variables)
            delete this clone
```

`collectable-type`{:class="block3variables"} ವೇರಿಯೇಬಲ್ ಅನ್ನು, `pick-costume`{:class="block3myblocks"} ಬ್ಲಾಕ್ ಗೆ **ಹಸ್ತಾಂತರ** \(ಪಾಸ್\) ಮಾಡುವುದನ್ನು ನೀವು ಗಮನಿಸಿ. `pick-costume`{:class="block3myblocks"} ಕೋಡ್ ಒಳಗೆ `collectable-type`{:class="block3variables"} ಅನ್ನು (`type`{:class="block3myblocks"}) ಇನ್ಪುಟ್ ವೇರಿಯೇಬಲ್ ಆಗಿ ಉಪಯೋಗಿಸಲಾಗಿದೆ.

ಇದರ ಅರ್ಥ, `collectable-type`{:class="block3variables"}ದ ಮೌಲ್ಯವು ಸ್ಪ್ರೈಟ್ ತದ್ರೂಪಿ (clone) ಯಾವ ವೇಷಭೂಷಣ ಪಡೆಯುತ್ತದೆ ಎಂಬುದನ್ನು ನಿರ್ಧರಿಸುತದೆ.

--- /collapse ---

### ಹೊಸ ಪವರ್-ಅಪ್ ಗಾಗಿ ವೇಷಭೂಷಣವನ್ನು ಸೇರಿಸಿ

ಸಹಜವಾಗಿ, ಇದೀಗ **Collectable** sprite ಕೇವಲ ಒಂದು ವೇಷಭೂಷಣವನ್ನು ಹೊಂದಿದೆ, ಏಕೆಂದರೆ ಸಂಗ್ರಹಿಸಬಹುದಾದ ಒಂದು ವಿಧ ಮಾತ್ರ ಇದೆ. ನೀವು ಅದನ್ನು ಬದಲಾಯಿಸಲಿದ್ದೀರಿ.

--- task ---

ನಿಮ್ಮ ಹೊಸ ಪವರ್-ಅಪ್ಗಾಗಿ, ಹೊಸ ವೇಷಭೂಷಣವನ್ನು **Collectable** spriteಗೆ ಸೇರಿಸಿ. ನಾನು ಮಿಂಚನ್ನು ಇಷ್ಟಪಡುತ್ತೇನೆ, ಆದರೆ ನೀವು ನಿಮಗೆ ಇಷ್ಟಪಡುವದನ್ನು ಆರಿಸಿ.

--- /task ---

--- task ---

ಮುಂದೆ, `pick-costume`{:class="block3myblocks"} **My blocks** ಬ್ಲಾಕ್ ಗೆ, ಯಾವಾಗೆಲ್ಲ `type`{:class="block3myblocks"} ಹೊಸ ಮೌಲ್ಯವನ್ನು ಪಡೆದಾಗ ಹೊಸ ವೇಷಭೂಷಣವನ್ನು ಹೊಂದಿಸಲು ನಿರ್ದೇಶ ಕೊಡಿ, ಈ ರೀತಿಯಾಗಿ, ಈ ರೀತಿ \(ನೀವು ಆರಿಸಿದ ಯಾವುದೇ ವೇಷಭೂಷಣ ಹೆಸರನ್ನು ಬಳಸಿ\):

```blocks3
    define pick-costume (type)
    if <(type ::variable) = [1]> then
        switch costume to [star1 v]
    end
+    if <(type ::variable) = [2]> then
+        switch costume to [lightning v]
+    end
```

--- /task ---

### ಪವರ್-ಅಪ್ ಕೋಡ್ ರಚಿಸಿ

ಹೊಸ ಸಂಗ್ರಹಯೋಗ್ಯ ಏನು ಮಾಡಬೇಕೆಂದು ಈಗ ನೀವು ನಿರ್ಧರಿಸಬೇಕು! ನಾವು ಸರಳವಾದದ್ದನ್ನು ಪ್ರಾರಂಭಿಸುತ್ತೇವೆ: ಆಟಗಾರನಿಗೆ ಹೊಸ ಜೀವವನ್ನು ನೀಡುತ್ತದೆ. ಮುಂದಿನ ಹಂತದಲ್ಲಿ, ನೀವು ಅದನ್ನು ಚೆನ್ನಾಗಿರುವ ಹಾಗೆ ಮಾಡುವಂತೆ ಮಾಡುತ್ತೀರಿ.

--- task ---

**My Blocks** ವಿಭಾಗಕ್ಕೆ ಹೋಗಿ **Make a Block** ಮೇಲೆ ಕ್ಲಿಕ್ ಮಾಡಿ. ಹೊಸ ಬ್ಲಾಕ್ ಅನ್ನು `react-to-player`{:class="block3myblocks"} ಎಂದು ಹೆಸರಿಸಿ ಮತ್ತು `type`{:class="block3myblocks"} ಎಂದು ಹೆಸರಿರುವ **number input** ಅನ್ನು ಸೇರಿಸಿ.

![ಬ್ಲಾಕ್ಗಾಗಿ ಹೆಸರನ್ನು ಟೈಪ್ ಮಾಡಿ](images/powerupMakeName.png)

**OK** ಒತ್ತಿರಿ.

--- /task ---

--- task ---

`react-to-player`{:class="block3myblocks"} **My blocks** ಬ್ಲಾಕ್ ನಲ್ಲಿ `type`{:class="block3myblocks"} ನ ಬೆಲೆಗೆ ಅನುಸರಿಸಿ, ಅಂಕೆಗಳು ಅಥವಾ ಆಟಗಾರನ ಲೈಫ್ \(ಜೀವ\) ಹೆಚ್ಚಾಗುವತೆ ಮಾಡಿ.

```blocks3
+    define react-to-player (type)
+    if <(type ::variable) = [1]> then
+        change [points v] by (collectable-value ::variables)
+    end
+    if <(type ::variable) = [2]> then
+        change [lives v] by [1]
+    end
```

--- /task ---

--- task ---

`when I start as a clone`{:class="block3events"} ಕೋಡ್ ನಲ್ಲಿ, `react-to-player`{:class="block3myblocks"}, ಅಂಕೆ ಸೇರಿಸುವ ಬ್ಲಾಕ್ ಅನ್ನು ಬದಲಾಯಿಸಿ, `collectable-type`{:class="block3variables"} ಅನ್ನು **ಹಸ್ತಾಂತರಿಸುವ** \(passing\) ಮೂಲಕ `react-to-player`{:class="block3myblocks"} ಅನ್ನು **ಕರೆ** \(call\) ಮಾಡಿ.

```blocks3
+    if <touching [Player Character v] ?> then
+        react-to-player (collectable-type ::variables) :: custom
+        delete this clone
+    end
```

--- /task ---

ಈ ಹೊಸ `react-to-player`{:class="block3myblocks"} **My blocks** ಬ್ಲಾಕ್ ಅನ್ನು ಬಳಸುವ ಮೂಲಕ, ನಕ್ಷತ್ರಗಳು ಇನ್ನೂ ಒಂದೇ ಅಂಕೆಯನ್ನು ಸೇರಿಸುತ್ತವೆ, ಆದರೆ ನೀವು ರಚಿಸಿದ ಹೊಸ ಪವರ್-ಅಪ್, ಒಂದು ಲೈಫ್ ಅನ್ನು ಸೇರಿಸುತ್ತದೆ.

### `collectable-type`{:class="block3variables"} ಅನ್ನು ಉಪಯೋಗಿಸಿ ವಿಭಿನ್ನ ಸಂಗ್ರಹಯೋಗ್ಯಗಳನ್ನು ಯಾದೃಚ್ಛಿಕವಾಗಿ ಗೋಚರಿಸುವಂತೆ ಮಾಡುವುದು

ಇದೀಗ, ಸಂಗ್ರಹಿಸಬಹುದಾದ ಪ್ರತಿಯೊಂದು ಆಟವು ಯಾವ ಪ್ರಕಾರವಾಗಿರಬೇಕು ಎಂದು ನೀವು ಹೇಗೆ ಹೇಳುತ್ತೀರಿ ಎಂದು ನೀವು ಆಶ್ಚರ್ಯ ಪಡಬಹುದು.

ಇದನ್ನು ಮಾಡಲು `collectable-type`{:class="block3variables"}ದ ಬೆಲೆಯನ್ನು 0 ಗೆ ಹೊಂದಿಸಬೇಕು. ಈ ವೇರಿಯೇಬಲ್ ಕೇವಲ ಒಂದು ಸಂಖ್ಯೆ. ನೀವು ನೋಡಿದಂತೆ, ಇದನ್ನು `pick-costume`{:class="block3myblocks"} ಮತ್ತು `react-to-player`{:class="block3myblocks"} ಬ್ಲಾಕ್ ಗಳಿಗೆ ಯಾವ ವೇಷಭೂಷಣ, ನಿಯಮಗಳು ಇತ್ಯಾದಿಗಳನ್ನು ತಿಳಿಸುತ್ತದೆ. ಸಂಗ್ರಹಿಸಬಹುದಾದ ಬಳಕೆಗಾಗಿ.

--- collapse ---
---
title: ತದ್ರೂಪಿಗಳಲ್ಲಿ ವೇರಿಯೇಬಲ್ ನೊಂದಿಗೆ ಕೆಲಸ ಮಾಡುವುದು
---

ಪ್ರತಿಯೊಂದು cloneನ **Collectable** spriteಗೆ, ನೀವು `collectable-type`{:class="block3variables"} ನ ಮೌಲ್ಯವನ್ನು ಹೊಂದಿಸಬಹುದು.

**Collectable** ತದ್ರೂಪಿ ಉಂಟುಮಾಡಿದಾಗ, **Collectable** spriteನಹೊಸ ನಕಲನ್ನು `collectable-type`{:class="block3variables"} ರ ಮೌಲ್ಯವನ್ನು ಉಪಯೋಗಿಸಿ ರಚಿಸಿದಂತೆ ಯೋಚಿಸಿ.

`collectable-type`{:class="block3variables"} ನ ಬೆಲೆಯನ್ನು ಬದಲಾಯಿಸಿದರೆ ವೇದಿಕೆಯಲ್ಲಿರುವ ಎಲ್ಲ ವಸ್ತುಗಳು ಒಂದೇ ವಿಧವಾಗಿ ಬದಲಾಗುವುದೇ ಎಂದು ನೀವು ಯೋಚಿಸಬಹುದು. ಅದು ಸಂಭವಿಸುವುದಿಲ್ಲ, ಏಕೆಂದರೆ clones ವಿಶೇಷವಾಗಿಸುವ ಒಂದು ವಿಷಯವೆಂದರೆ ಅವರು ಪ್ರಾರಂಭಿಸುವ ಯಾವುದೇ ವೇರಿಯೇಬಲ್ ಮೌಲ್ಯಗಳನ್ನು ಬದಲಾಯಿಸಲು ಸಾಧ್ಯವಿಲ್ಲ. Sprite ತದ್ರೂಪಿಗಳು ಪರಿಣಾಮಕಾರಿಯಾಗಿ **ಸ್ಥಿರ**ವಾದ ಮೌಲ್ಯಗಳನ್ನು ಹೊಂದಿರುತ್ತವೆ. ಇದರರ್ಥ ನೀವು `collectable-type`{:class="block3variables"} ಮೌಲ್ಯವನ್ನು ಬದಲಾಯಿಸಿದಾಗ, ಇದು ಈಗಾಗಲೇ ಆಟದಲ್ಲಿರುವ **Collectable** sprite ತದ್ರೂಪಿಗಳ ಮೇಲೆ ಪರಿಣಾಮ ಬೀರುವುದಿಲ್ಲ.

--- /collapse ---

ಪ್ರತಿಯೊಂದು ಹೊಸ ತದ್ರೂಪಿಗಾಗಿ ನೀವು `collectable-type`{:class="block3variables"} `1` ಅಥವಾ `2` ನ್ನು ಹೊಂದಿಸಲಿದ್ದೀರಿ. ಆಟವನ್ನು ಆಸಕ್ತಿದಾಯಕವಾಗಿಡಲು, ಪ್ರತಿ ಬಾರಿಯೂ ಯಾದೃಚ್ಛಿಕವಾಗಿ ಸಂಗ್ರಹಿಸಬಹುದಾದಂತೆ ಮಾಡಲು ಯಾದೃಚ್ಛಿಕವಾಗಿ ಸಂಖ್ಯೆಗಳ ನಡುವೆ ಆರಿಸಿ.

--- task ---

**Collectable** spriteನ ಹಸಿರು ಧ್ವಜದ ಕೋಡ್ ಒಳಗೆ `repeat until`{:class="block3control"} ಲೂಪ್ ಅನ್ನು ಹುಡುಕಿ ಅದರೊಳಗೆ `if...else`{:class="block3control"} ಕೋಡ್ ಸೇರಿಸಿ.

```blocks3
    repeat until <not <(create-collectables ::variables) = [true]>>
+        if <[50] = (pick random (1) to (50))> then
+            set [collectable-type v] to [2]
+        else
+            set [collectable-type v] to [1]
+        end
        wait (collectable-frequency ::variables) secs
        go to x: (pick random (-240) to (240)) y: (179)
        create clone of [myself v]
```

--- /task ---

ಈ ಕೋಡ್ `collectable-type`{:class="block3variables"} `2`ಕ್ಕೆ ಹೊಂದಿಸಲು 1-ರಿಂದ -50 ಅವಕಾಶವನ್ನು ನೀಡುತ್ತದೆ. ಏನೇ ಆದರೂ, ಆಟಗಾರನಿಗೆ ಹೆಚ್ಚುವರಿ ಆಗಾಗ್ಗೆ ಜೀವನವನ್ನು ಸಂಗ್ರಹಿಸಲು ನೀವು ಅವಕಾಶವನ್ನು ನೀಡಲು ಬಯಸುವುದಿಲ್ಲ. ಹಾಗೆ ಮಾಡಿದರೆ ಆಟವು ತುಂಬಾ ಸುಲಭವಾಗುತ್ತದೆ.

ಈಗ ನೀವು ಹೊಸ ಪ್ರಕಾರದ ಸಂಗ್ರಹಯೋಗ್ಯವನ್ನು ಹೊಂದಿದ್ದೀರಿ, ಅದು ಕೆಲವೊಮ್ಮೆ ನಕ್ಷತ್ರದ ಬದಲು ತೋರಿಸುತ್ತದೆ, ಮತ್ತು ನೀವು ಅದನ್ನು ಸಂಗ್ರಹಿಸುವಾಗ ಒಂದು ಅಂಕೆಯ ಬದಲಾಗಿ ಹೆಚ್ಚುವರಿ ಜೀವವನ್ನು ನೀಡುತ್ತದೆ.