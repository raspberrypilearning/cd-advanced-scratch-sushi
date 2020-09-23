## ಆಟವನ್ನು ಕಳೆದುಕೊಳ್ಳುವುದು

ಮೊದಲಿನದಕ್ಕೆ ಆದ್ಯತೆ! ಆಟಗಾರನು ಜೀವ ಕಳೆದುಹೋದಾಗ ಆಟವನ್ನು ಕೊನೆಗೊಳಿಸಲು ನಿಮಗೆ ಒಂದು ಮಾರ್ಗ ಬೇಕು. ಈ ಸಮಯದಲ್ಲಿ ಅದು ಸಂಭವಿಸುವುದಿಲ್ಲ.

ನೀವು `lose`{:class="block3myblocks"} ಎಂಬ **My blocks** ಬ್ಲಾಕ್, **Player Character** sprite ಸ್ಕ್ರಿಪ್ಟ್‌ಗಳಲ್ಲಿ ಖಾಲಿಯಾಗಿರುವುದನ್ನು ಗಮನಿಸಿರಬಹುದು. ನೀವು ಇದನ್ನು ಭರ್ತಿ ಮಾಡಲು ಮತ್ತು ಉತ್ತಮವಾದ 'ಆಟ ಮುಗಿದಿದೆ' ಪರದೆಗೆ ಬೇಕಾದ ಎಲ್ಲಾ ತುಣುಕುಗಳನ್ನು ಹೊಂದಿಸಲಿದ್ದೀರಿ.

--- task ---

ಮೊದಲಿಗೆ, `lose`{:class="block3myblocks"} ಬ್ಲಾಕ್ ಅನ್ನು ಹುಡುಕಿ ಮತ್ತು ಅದನ್ನು ಈ ಕೆಳಗಿನ ಕೋಡ್‌ನೊಂದಿಗೆ ಪೂರ್ಣಗೊಳಿಸಿ:

```blocks3
    define lose
+    stop [other scripts in sprite v] :: control stack
+    broadcast [game over v]
+    go to x:(0) y:(0)
+    say [Game over!] for (2) secs
+    stop [all v]
```

--- /task ---

--- collapse ---
---
title: ಈ ಕೋಡ್ ಏನು ಮಾಡುತ್ತದೆ?
---

`lose`{:class="block3myblocks"} ಬ್ಲಾಕ್ ಚಲಾಯಿಸಿದಾಗ ಏನು ಮಾಡುತದೆ ಅಂದರೆ:

1. **Player Character** ನಲ್ಲಿ ಕಾರ್ಯನಿರ್ವಹಿಸುವ ಫಿಸಿಕ್ಸ್ ಮತ್ತು ಇತರ ಆಟದ ಸ್ಕ್ರಿಪ್ಟ್‌ಗಳನ್ನು ನಿಲ್ಲಿಸಿ
2. `game over`{:class="block3events"} ಎಂಬ ಸಂದೇಶವನ್ನು ಪ್ರಸಾರ ಅಥವಾ **broadcast** ಮಾಡುವ ಮೂಲಕ ಉಳಿದ sprite ಗಳಿಗೆ ಆಟ ಮುಗಿದಿರುವ ಬಗ್ಗೆ ಸೂಚಿಸಿ. ಹೀಗೆ ಮಾಡುವುದರಿಂದ, ಅವುಗಳು ಮಾಡುವ ಕೆಲಸದಲ್ಲಿ ಬದಲಾವಣೆ ಮಾಡಬಹುದು
3. **Player Character** ಅನ್ನು ವೇದಿಕೆಯ ಮಧ್ಯಭಾಗಕ್ಕೆ ಸರಿಸಿ ಆಟ ಮುಗಿದಿದೆ ಎಂದು ಹೇಳುವ ಹಾಗೆ ಮಾಡಿ
4. ಆಟದಲ್ಲಿ ಎಲ್ಲಾ ಸ್ಕ್ರಿಪ್ಟ್‌ಗಳನ್ನು ನಿಲ್ಲಿಸಿ

--- /collapse ---

ಆಟ ಮುಗಿದ ನಂತರ ಏನು ಮಾಡಬೇಕೆಂದು ಮತ್ತು ಆಟಗಾರನು ಹೊಸ ಆಟವನ್ನು ಪ್ರಾರಂಭಿಸಿದಾಗ ತಮ್ಮನ್ನು ಹೇಗೆ ಮರುಹೊಂದಿಸುವುದು ಎಂದು ಎಲ್ಲಾ spritesಗೆ ತಿಳಿದಿದೆಯೆ ಎಂದು ಈಗ ನೀವು ಖಚಿತಪಡಿಸಿಕೊಳ್ಳಬೇಕು. **ನೀವು ಸೇರಿಸುವ ಯಾವುದೇ ಹೊಸ spritesಗೆ ಇದಕ್ಕಾಗಿ ಕೋಡ್ ಅಗತ್ಯವಿರುತ್ತದೆ ಎಂಬುದನ್ನು ಮರೆಯಬೇಡಿ!**

### ವೇದಿಕೆಗಳು ಮತ್ತು ಅಂಚುಗಳನ್ನು ಮರೆಮಾಡಲಾಗುತ್ತಿದೆ

--- task ---

ಸುಲಭವಾದ sprites‌ಗಳೊಂದಿಗೆ ಪ್ರಾರಂಭಿಸಿ. ಆಟ ಪ್ರಾರಂಭವಾದಾಗ **Platforms** ಮತ್ತು **Edges** sprite ಕಾಣಿಸಿಕೊಳ್ಳಲು ಮತ್ತು `game over`{:class="block3events"} ಎಂಬ ಪ್ರಸಾರ ಸಂದೇಶವನ್ನು ಸ್ವೀಕರಿಸಿದಾಗ ಕಣ್ಮರೆಯಾಗಲು ಕೋಡ್ ಗಳ ಅಗತ್ಯವಿದೆ. ಆದ್ದರಿಂದ ಪ್ರತಿಯೊಂದಕ್ಕೂ ಈ ಬ್ಲಾಕ್‌ಗಳನ್ನು ಸೇರಿಸಿ:

```blocks3
+    when I receive [game over  v]
+    hide
```

```blocks3
+    when green flag clicked
+    show
```

--- /task ---

### ನಕ್ಷತ್ರಗಳನ್ನು ನಿಲ್ಲಿಸುವುದು

ಈಗ, ನೀವು **Collectable** sprite ಕೋಡ್ ಅನ್ನು ನೋಡಿದರೆ, ಇದು **cloning** ಮೂಲಕ ಕಾರ್ಯನಿರ್ವಹಿಸುತ್ತದೆ ಎಂದು ನೀವು ಸ್ವತಃ ನೋಡುತ್ತೀರಿ. ಅಂದರೆ, `when I start as a clone`{:class="block3events"} ಎನ್ನುವ ವಿಶೇಷ ನಿರ್ದೇಶವನ್ನು ಸ್ವೀಕರಿಸಿವುವ ಮೂಲಕ, ತದ್ರೂಪಿಗಳನ್ನು ಸೃಷ್ಟಿ ಮಾಡುತ್ತದೆ.

ಹೊಸ ಮತ್ತು ವಿಭಿನ್ನ ಸಂಗ್ರಹಣೆಗಳನ್ನು ಮಾಡುವ ಬಗ್ಗೆ ನಾವು ಹೆಜ್ಜೆ ಹಾಕಿದಾಗ ತದ್ರೂಪಿಗಳ ವಿಶೇಷತೆ ಏನು ಎಂದು ಮಾತಾಡೋಣ. ಸದ್ಯಕ್ಕೆ, ನೀವು ತಿಳಿದುಕೊಳ್ಳಬೇಕಾದ ಅಂಶವೆಂದರೆ ತದ್ರೂಪುಗಳು `broadcast`{:class="block3events"} ಸಂದೇಶಗಳನ್ನು ಸ್ವೀಕರಿಸುವುದನ್ನು ಮಾತ್ರವಲ್ಲದೆ ಸ್ಪ್ರೈಟ್ ಮಾಡುವ **ಬಹುತೇಕ** ಕೆಲಸವನ್ನು ಮಾಡುತದೆ.

ಹೇಗೆ **Collectable** sprite ಕೆಲಸ ಮಾಡುತ್ತದೆ ಎಂಬುದನ್ನು ನೋಡಿ. ಅದರ ಕೆಲವು ಕೋಡ್‌ಗಳನ್ನು ನೀವು ಅರ್ಥಮಾಡಿಕೊಳ್ಳಬಹುದೇ ಎಂದು ನೋಡಿ:

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

1. ಮೊದಲು ಮೂಲ **Collectable** sprite ಅನ್ನು ಮರೆಮಾಚುವ ಮೂಲಕ ಅದೃಶ್ಯ ಮಾಡುತದೆ
2. ನಂತರ ಅದು ನಿಯಂತ್ರಣ ವೇರಿಯೇಬಲ್ ಗಳನ್ನು ಹೊಂದಿಸುತ್ತದೆ - ನಾವು ನಂತರ ಇವುಗಳಿಗೆ ಹಿಂತಿರುಗುತ್ತೇವೆ
3. `create-collectables`{:class="block3variables"} ವೇರಿಯೇಬಲ್ ತದ್ರೂಪಿ ಸೃಷ್ಟಿಸುವ ಆನ್/ಆಫ್ ಸ್ವಿಚ್ ಆಗಿದೆ: `create-collectables`{:class="block3variables"} ರ ಬೆಲೆಯು `true` ಆಗಿದ್ದಲ್ಲಿ ಲೂಪ್ ತದ್ರೂಪಿಗಳನ್ನು ಸೃಷ್ಟಿ ಮಾಡುತ್ತದೆ

--- task ---

ಈಗ `game over` ಪ್ರಸಾರಕ್ಕೆ ಪ್ರತಿಕ್ರಿಯಿಸುವ ಒಂದು **Collectable** sprite ಬ್ಲಾಕ್ ಅನ್ನು ಹೊಂದಿಸಿ:

```blocks3
+    when I receive [game over v]
+    hide
+    set [create-collectables v] to [false]
```

--- /task ---

ಈ ಕೋಡ್, **Platforms** ಮತ್ತು **Edges** sprite ಗಳನ್ನು ನಿಯಂತ್ರಿಸುವ ಕೋಡ್ ಗೆ ಸಮಾನವಾಗಿದೆ. ಒಂದೇ ವ್ಯತ್ಯಾಸವೆಂದರೆ ನೀವು `create-collectables`{:class="block3variables"} ವೇರಿಯೇಬಲ್ ಅನ್ನು `false` ಹೊಂದಿಸಿರುವುದರಿಂದ 'Game over' (ಗೇಮ್ ಓವರ್) ಆಗಿರುವಾಗ ಯಾವುದೇ ಹೊಸ ತದ್ರೂಪುಗಳನ್ನು ರಚಿಸಲಾಗುವುದಿಲ್ಲ.

ನೀವು ಕೋಡ್ ನ ಒಂದು ಭಾಗದಿಂದ ಇನ್ನೊಂದು ಭಾಗಕ್ಕೆ ಸಂದೇಶವನ್ನು ರವಾನಿಸಲು `create-collectables`{:class="block3variables"} ವೇರಿಯೇಬಲ್ ಅನ್ನು ಉಪಯೋಗಿಸಬಹುದು!