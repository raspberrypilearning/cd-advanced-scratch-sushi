## ಹಂತ 2

ಈ ಹಂತದ ಮೂಲಕ, ನೀವು ಕೇವಲ ಒಂದು ಬಟನನ್ನು ಒತ್ತುವ ಮೂಲಕ ಆಟಗಾರನು ಪಡೆಯಬಹುದಾದ ಹೊಸ ಮಟ್ಟವನ್ನು ಸೇರಿಸಲು ಹೊರಟಿದ್ದೀರಿ. ನಂತರ, ನಿಮ್ಮ ಕೋಡ್ ಅನ್ನು ಮಾಡಲು ನೀವು ಅದನ್ನು ಬದಲಾಯಿಸಬಹುದು ಆದ್ದರಿಂದ ಅವರಿಗೆ ಅಲ್ಲಿಗೆ ಹೋಗಲು ನಿರ್ದಿಷ್ಟ ಸಂಖ್ಯೆಯ ಅಂಕಗಳು ಅಥವಾ ಇನ್ನೇನಾದರೂ ಅಗತ್ಯವಿರುತ್ತದೆ.

### ಮುಂದಿನ ಹಂತಕ್ಕೆ ಚಲಿಸುವುದು

--- task ---

ಮೊದಲಿಗೆ, ಲೈಬ್ರರಿಯಿಂದ ಒಂದನ್ನು ಸೇರಿಸುವ ಮೂಲಕ ಅಥವಾ ನಿಮ್ಮದೇ ಆದದನ್ನು ಸೆಳೆಯುವ ಮೂಲಕ ಹೊಸ sprite ಅನ್ನು ಬಟನ್ ಆಗಿ ರಚಿಸಿ. ನಾನು ಎರಡನ್ನೂ ಸ್ವಲ್ಪಮಟ್ಟಿಗೆ ಮಾಡಿದ್ದೇನೆ ಮತ್ತು ಇಲ್ಲಿಯ ತನಕ ಬಂದಿದ್ದೇನೆ:

![The button sprite to switch levels](images/levelButton.png)

--- /task ---

--- task ---

ಈಗ, ಈ ಬಟನ್ ಕೋಡ್ ಬುದ್ಧಿವಂತವಾಗಿದೆ: ಇದನ್ನು ಹೇಗೆ ವಿನ್ಯಾಸಗೊಳಿಸಲಾಗಿದೆ ಎಂದರೆ ನೀವು ಅದನ್ನು ಕ್ಲಿಕ್ ಮಾಡಿದಾಗಲೆಲ್ಲಾ ಅದು ನಿಮ್ಮನ್ನು ಮುಂದಿನ ಹಂತಕ್ಕೆ ಕೊಂಡೊಯ್ಯುತ್ತದೆ, ಎಷ್ಟೇ ಹಂತಗಳಿದ್ದರೂ ಸಹ.

ನಿಮ್ಮ **Button** sprite ‌ಗೆ ಈ ಸ್ಕ್ರಿಪ್ಟ್‌ಗಳನ್ನು ಸೇರಿಸಿ. ನೀವು ಹಾಗೆ ಕೆಲವು ವೇರಿಯೇಬಲ್ ಗಳನ್ನು ರಚಿಸಬೇಕಾಗುತ್ತದೆ.

```blocks3
+    when green flag clicked
+    set [max-level v] to [2]
+    set [min-level v] to [1]
+    set [current-level v] to [1]
```

```blocks3
+    when this sprite clicked
+    change [current-level v] by (1)
+    if <(current-level) > (max-level ::variables)> then
        set [current-level v] to (min-level ::variables)
    end
+    broadcast [collectable-cleanup v]
+    broadcast (join [level-](current-level))
```

--- /task ---

ನೀವು ರಚಿಸಿದ ಅಸ್ಥಿರಗಳನ್ನು ಪ್ರೋಗ್ರಾಂ ಹೇಗೆ ಬಳಸುತ್ತದೆ ಎಂಬುದನ್ನು ನೀವು ನೋಡಬಹುದೇ?

+ `max-level`{:class="block3variables"} ಅತ್ಯುನ್ನತ ಮಟ್ಟವನ್ನು ಸಂಗ್ರಹಿಸುತ್ತದೆ
+ `min-level`{:class="block3variables"} ಅತ್ಯಂತ ಕಡಿಮೆ ಮಟ್ಟವನ್ನು ಸಂಗ್ರಹಿಸುತ್ತದೆ
+ `current-level`{:class="block3variables"} ಆಟಗಾರನು ಇದೀಗ ಇರುವ ಮಟ್ಟವನ್ನು ಸಂಗ್ರಹಿಸುತ್ತದೆ

ಇವೆಲ್ಲವನ್ನೂ ಪ್ರೋಗ್ರಾಮರ್ \(ನೀವು!\) ಹೊಂದಿಸಬೇಕಾಗಿದೆ, ಆದ್ದರಿಂದ ನೀವು ಮೂರನೇ ಹಂತವನ್ನು ಸೇರಿಸಿದರೆ, `max-level`{:class="block3variables"} ನ ಮೌಲ್ಯವನ್ನು ಬದಲಾಯಿಸಲು ಮರೆಯಬೇಡಿ! `min-level`{:class="block3variables"} ಅನ್ನು ಎಂದಿಗೂ ಬದಲಾಯಿಸಬೇಕಾಗಿಲ್ಲ.

ಯಾವ ಮಟ್ಟವನ್ನು ಪ್ರದರ್ಶಿಸಬೇಕು ಎಂದು ಇತರ sprites‌ ಗಳಿಗೆ ಹೇಳಲು ಮತ್ತು ಹೊಸ ಮಟ್ಟ ಪ್ರಾರಂಭವಾದಾಗ ಸಂಗ್ರಹಯೋಗ್ಯ ವಸ್ತುಗಳನ್ನು ತೆರವುಗೊಳಿಸಲು ಪ್ರಸಾರಗಳನ್ನು ಬಳಸಲಾಗುತ್ತದೆ.

### Sprites ಪ್ರತಿಕ್ರಿಯಿಸುವಂತೆ ಮಾಡಿ

#### **Collectable** sprite

ಈ ಪ್ರಸಾರಗಳಿಗೆ ಪ್ರತಿಕ್ರಿಯಿಸಲು ಈಗ ನೀವು ಇತರ sprites ‌ಗಳನ್ನು ಪಡೆಯಬೇಕು! ಸುಲಭವಾದದರೊಂದಿಗೆ ಪ್ರಾರಂಭಿಸಿ: ಎಲ್ಲಾ ಸಂಗ್ರಹಯೋಗ್ಯ ವಸ್ತುಗಳನ್ನು ತೆರವುಗೊಳಿಸುವುದು.

--- task ---

ಸಂದೇಶವನ್ನು ಸ್ವೀಕರಿಸಿದಾಗ ಎಲ್ಲಾ ತದ್ರೂಪಿಗಳನ್ನು `hide`{:class="block3vlooks"} (ಮರೆ) ಮಾಡಲು ಈ ಕೆಳಗಿನ ಕೋಡ್ ಅನ್ನು **Collectable** sprite ಸ್ಕ್ರಿಪ್ಟ್‌ಗಳಿಗೆ ಸೇರಿಸಿ:

```blocks3
+    when I receive [collectable-cleanup v]
+    hide
```

--- /task ---

ಯಾವುದೇ ಹೊಸ ತದ್ರೂಪಿ ಮಾಡುವ ಮೊದಲ ಕೆಲಸ, ಸ್ವತಃ ತೋರಿಸುವುದು ಆಗಿರುವುದರಿಂದ, ಸಂಗ್ರಹಯೋಗ್ಯ ವಸ್ತುಗಳನ್ನು ಮರೆಮಾಚುವ ಬಗ್ಗೆ ನೀವು ಚಿಂತಿಸಬೇಕಾಗಿಲ್ಲ!

#### **Platforms**sprite

ಈಗ **Platforms** sprite ಅನ್ನು ಬದಲಾಯಿಸಲು. ನೀವು ಬಯಸಿದರೆ ನಂತರ ನಿಮ್ಮ ಸ್ವಂತ ಹೊಸ ಮಟ್ಟವನ್ನು ನೀವು ವಿನ್ಯಾಸಗೊಳಿಸಬಹುದು, ಆದರೆ ಇದೀಗ ನಾನು ಈಗಾಗಲೇ ಸೇರಿಸಿದ್ದನ್ನು ಬಳಸೋಣ - ಮುಂದಿನ ಹಂತದಲ್ಲಿ ಏಕೆ ಎಂದು ನೀವು ನೋಡುತ್ತೀರಿ!

--- task ---

ಈ ಕೋಡ್ ಅನ್ನು **Platform** spriteಗೆ ಸೇರಿಸಿ:

```blocks3
+    when I receive [level-1 v]
+    switch costume to [Level 1 v]
+    show
```

```blocks3
+    when I receive [level-2 v]
+    switch costume to [Level 2 v]
+    show
```

--- /task ---

ಇದು **Button** sprite ಕಳುಹಿಸುವ `level-`{:class="block3variables"} ಮತ್ತು `current-level`{:class="block3variables"} ಗಳ `joined`{:class="block3operators"} ಸಂದೇಶಗಳನ್ನು ಪಡೆಯುತ್ತದೆ. ಮತ್ತು **Platforms** ವಸ್ತ್ರವಿನ್ಯಾಸಗಳನ್ನು ಬದಲಾಯಿಸುವ ಮೂಲಕ ಸ್ಪಂದಿಸುತ್ತದೆ.

#### **Enemy** sprite

--- task ---

**Enemy** sprite ಸ್ಕ್ರಿಪ್ಟ್‌ಗಳಲ್ಲಿ, ಆಟಗಾರನು 2 ನೇ ಹಂತಕ್ಕೆ ಪ್ರವೇಶಿಸಿದಾಗ sprite ಕಣ್ಮರೆಯಾಗುತ್ತದೆ ಎಂದು ಈ ರೀತಿಯಲ್ಲಿ ಖಚಿತಪಡಿಸಿಕೊಳ್ಳಿ:

```blocks3
+    when I receive [level-1 v]
+    show
```

```blocks3
+    when I receive [level-2 v]
+    hide
```

--- /task ---

ನೀವು ಬಯಸಿದಲ್ಲಿ, ನೀವು ಶತ್ರುಗಳನ್ನು ಮತ್ತೊಂದು ಪ್ಲಾಟ್‌ಫಾರ್ಮ್‌ಗೆ ಚಲಿಸುವಂತೆ ಮಾಡಬಹುದು. ಅಂತಹ ಸಂದರ್ಭದಲ್ಲಿ, ನೀವು `show`{:class="block3looks"} ಮತ್ತು `hide`{:class="block3looks"} ಬದಲಿಗೆ `go to`{:class="block3motion"} ಬ್ಲಾಕ್ ಅನ್ನು ಉಪಯೋಗಿಸಿ.

### **Player Character** ಸರಿಯಾದ ಸ್ಥಳದಲ್ಲಿ ಕಾಣಿಸಿಕೊಳ್ಳುವಂತೆ ಮಾಡಿ

ಹೊಸ ಮಟ್ಟ ಪ್ರಾರಂಭವಾದಾಗ, **Player Character** sprite ಆ ಮಟ್ಟದ ಸರಿಯಾದ ಸ್ಥಳಕ್ಕೆ ಹೋಗಬೇಕಾಗಿದೆ. ಇದನ್ನು ಮಾಡಲು, sprite ಮೊದಲ ಬಾರಿಗೆ ವೇದಿಕೆಯಲ್ಲಿ ಕಾಣಿಸಿಕೊಂಡಾಗ ಅದರ ನಿರ್ದೇಶಾಂಕಗಳನ್ನು ಎಲ್ಲಿ ಪಡೆಯುತ್ತದೆ ಎಂಬುದನ್ನು ನೀವು ಬದಲಾಯಿಸಬೇಕಾಗಿದೆ. ಈ ಸಮಯದಲ್ಲಿ, ಅದರ ಕೋಡ್‌ನಲ್ಲಿನ ಮೌಲ್ಯಗಳು `x` ಮತ್ತು `y` ಸ್ಥಿರವಾಗಿರುತ್ತದೆ.

--- task ---

ಆರಂಭಿಕ ನಿರ್ದೇಶಾಂಕಗಳಿಗಾಗಿ ವೇರಿಯೇಬಲ್ ಗಳನ್ನು ರಚಿಸುವ ಮೂಲಕ ಪ್ರಾರಂಭಿಸಿ: `start-x`{:class="block3variables"} ಮತ್ತು `start-y`{:class="block3variables"}. ನಂತರ ಸ್ಥಿರವಾದ `x` ಮತ್ತು `y` ಗಳನ್ನು ಉಪಯೋಗಿಸುವ ಬದಲು, ಅವುಗಳನ್ನು, `reset-character`{:class="block3myblocks"} **My blocks** ಬ್ಲಾಕ್ ನ `go to`{:class="block3motion"} ಬ್ಲಾಕಿಗೆ ಸೇರಿಸಿ:

```blocks3
    define reset-character
    set [can-jump v] to [true]
    set [x-velocity v] to [0]
    set [y-velocity v] to [-0]
+    go to x: (start-x) y: (start-y)
```

--- /task ---

--- task ---

ಒಂದು ಹಂತದ ಪ್ರಾರಂಭವನ್ನು ಘೋಷಿಸುವ ಪ್ರತಿ ಪ್ರಸಾರಕ್ಕೂ ಪ್ರತಿಕ್ರಿಯೆಯಾಗಿ, ಸರಿಯಾದ `start-x`{:class="block3variables"} ಮತ್ತು `start-y`{:class="block3variables"} ಅನ್ನು ಹೊಂದಿಸಿ ಮತ್ತು `reset-character`{:class="block3myblocks"} ಗೆ ಒಂದು ಕರೆ\(**call**\) ಯನ್ನು ಮಾಡಿ:

```blocks3
+    when I receive [level-1 v]
+    set [start-x v] to [-183]
+    set [start-y v] to [42]
+    reset-character :: custom
```

```blocks3
+    when I receive [level-2 v]
+    set [start-x v] to [-218]
+    set [start-y v] to [-143]
+    reset-character :: custom
```

--- /task ---

### ಹಂತ 1 ರಿಂದ ಪ್ರಾರಂಭ

ಯಾರಾದರೂ ಆಟವನ್ನು ಪ್ರಾರಂಭಿಸಿದಾಗ, ಅವರು ಆಡುವ ಮೊದಲ ಹಂತವು ಮಟ್ಟ 1 ಎಂದು ನೀವು ಖಚಿತಪಡಿಸಿಕೊಳ್ಳಬೇಕು.

--- task ---

`reset-game`{:class="block3myblocks"} ನ ಸ್ಕ್ರಿಪ್ಟ್ ಗೆ ಹೋಗಿ ಅದರಿಂದ `reset-character`{:class="block3myblocks"} ಗೆ ಇರುವ ಕರೆಯನ್ನು ತೆಗೆದು ಹಾಕಿ. ಅದರ ಸ್ಥಳದಲ್ಲಿ, `min-level`{:class="block3variables"} ಪ್ರಸಾರ ಮಾಡಿ. ಈ ಕಾರ್ಡ್‌ನೊಂದಿಗೆ ನೀವು ಈಗಾಗಲೇ ಸೇರಿಸಿದ ಕೋಡ್, ನಂತರ **Player Character** spriteಗೆ ಸರಿಯಾದ ಆರಂಭಿಕ ನಿರ್ದೇಶಾಂಕಗಳನ್ನು ಹೊಂದಿಸುತ್ತದೆ, ಮತ್ತು `reset-character`{:class="block3myblocks"} ಸಹ ಕರೆ ಮಾಡುತ್ತದೆ.

```blocks3
    define reset-game
    set rotation style [left-right v]
    set [jump-height v] to [15]
    set [gravity v] to [2]
    set [x-speed v] to [1]
    set [y-speed v] to [1]
    set [lives v] to [3]
    set [points v] to [0]
+    broadcast (join [level-](min-level ::variables))
```

--- /task ---

--- collapse ---
---
title: ಆಟವನ್ನು ಮರುಹೊಂದಿಸುವ ವಿರುದ್ಧ ಪ್ಲೇಯರ್ ಅಕ್ಷರವನ್ನು ಮರುಹೊಂದಿಸುವುದು
---

**Player Character** sprite‌ನ ಮುಖ್ಯ ಹಸಿರು ಧ್ವಜ ಸ್ಕ್ರಿಪ್ಟ್‌ನಲ್ಲಿನ ಮೊದಲ ಬ್ಲಾಕ್ `reset-game`{:class="block3myblocks"} **My blocks** ಗೆ ಇರುವ ಕರೆ ಎಂದು ಗಮನಿಸಿ.

ಈ ಬ್ಲಾಕ್ ಹೊಸ ಆಟಕ್ಕಾಗಿ ಎಲ್ಲಾ ವೇರಿಯೇಬಲ್ ಗಳನ್ನು ಹೊಂದಿಸುತ್ತದೆ ಮತ್ತು ನಂತರ `reset-character`{:class="block3myblocks"} **My blocks** ಅನ್ನು ಕರೆಯುತ್ತದೆ. ಇದು ಅಕ್ಷರವನ್ನು ಅದರ ಸರಿಯಾದ ಆರಂಭಿಕ ಸ್ಥಾನದಲ್ಲಿ ಇರಿಸುತ್ತದೆ.

`reset-character`{:class="block3myblocks"} ಹೊಂದಿರುವ ಕೋಡ್ `reset-game`{:class="block3myblocks"} ನಲ್ಲಿ ಇರದೇ, ತನ್ನದೇ ಆದ ಬ್ಲಾಕಿನಲ್ಲಿ ಇರುವುದರಿಂದ, ಆಟವನ್ನು **ಪುನರಾರಂಭಿಸದೇ** ಪಾತ್ರದ ಸ್ಥಳವನ್ನು ಮರುಹೊಂದಿಸಲು ಸಾಧ್ಯವಾಗುತ್ತದೆ.

--- /collapse ---