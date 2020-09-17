## ಸೂಪರ್ ಪವರ್-ಅಪ್ಗಳು!

ಈಗ ನೀವು ಹೊಸ ಪವರ್-ಅಪ್ ಸಂಗ್ರಹಿಸಬಹುದಾದ ಕೆಲಸವನ್ನು ಹೊಂದಿದ್ದೀರಿ, ಅದು ನಿಜವಾಗಿಯೂ ಚೆನ್ನಾಗಿ ಏನನ್ನಾದರೂ ಮಾಡುವ ಸಮಯ: ಹೆಚ್ಚುವರಿ ಜೀವನವನ್ನು ನೀಡುವ ಬದಲು ಕೆಲವು ಸೆಕೆಂಡುಗಳ ಕಾಲ ಅದನ್ನು ಪವರ್-ಅಪ್‌ಗಳ 'ಮಳೆ'ಯನ್ನಾಗಿ ಮಾಡೋಣ.

ಇದಕ್ಕಾಗಿ, ನೀವು ಇನ್ನೊಂದು `broadcast`{:class="block3events"} ಸಂದೇಶವನ್ನು ಬಳಸಲಿದ್ದೀರಿ.

\--- task \---

ಮೊದಲಿಗೆ, ಆಟಗಾರ ಪಾತ್ರವು `2` ಸಂಗ್ರಹಿಸಬಹುದಾದ ಪ್ರಕಾರವನ್ನು ಮುಟ್ಟಿದಾಗ ಸಂದೇಶವನ್ನು ಪ್ರಸಾರ ಮಾಡಲು `react-to-player`{:class="block3myblocks"} ಬ್ಲಾಕ್ ಅನ್ನು ಬದಲಾಯಿಸಿ. `collectable-rain`{:class="block3events"} ಸಂದೇಶವನ್ನು ಕರೆಯಿರಿ.

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

`collectable-rain`{:class="block3events"} ಸಂದೇಶ ಪ್ರಸಾರ ಮಾಡಿದಾಗ ಶುರುವಾಗುವಂಥಹ ಕೋಡ್ ಅನ್ನು, ಈಗ ನೀವು **Collectable** sprite ಸ್ಕ್ರಿಪ್ಟ್‌ನ ಒಳಗೆ ಸೇರಿಸಬೇಕು.

\--- task \---

`collectable-rain`{:class="block3events"} ಪ್ರಸಾರವನ್ನು ಆಲಿಸುವಂತೆ ಮಾಡಲು **Collectable** spriteಗಾಗಿ ಈ ಕೋಡ್ ಅನ್ನು ಸೇರಿಸಿ.

```blocks3
+    when I receive [collectable-rain v]
+    set [collectable-frequency v] to [0.000001]
+    wait (1) secs
+    set [collectable-frequency v] to [1]
```

\--- /task \---

## \--- collapse \---

## title: ಈ ಹೊಸ ಕೋಡ್ ಏನು ಮಾಡುತ್ತದೆ?

ಈ ಕೋಡ್ ತುಣುಕು ಪ್ರಸಾರವನ್ನು ಸ್ವೀಕರಿಸಲು ಕಾಯುತ್ತದೆ ಮತ್ತು `collectable-frequency`{:class="block3variables"} ವೇರಿಯೇಬಲ್ ಅನ್ನು ಬಹಳ ಕಡಿಮೆ ಸಂಖ್ಯೆಗೆ ಹೊಂದಿಸುವ ಮೂಲಕ ಸ್ಪಂದಿಸುತ್ತದೆ, ನಂತರ ಒಂದು ಸೆಕೆಂಡ್ ಕಾಯುತ್ತದೆ, ತದನಂತರ ಪುನಃ `1` ಗೆ ಬದಲಾಯಿಸುತ್ತದೆ.

`collectable-frequency`{:class="block3variables"} ವೇರಿಯೇಬಲ್ ಅನ್ನು ಇದು ಸಂಗ್ರಹಯೋಗ್ಯ ಮಳೆಯಾಗಲು ಕಾರಣವೇನೆಂದು ಕಂಡುಹಿಡಿಯಲು ಹೇಗೆ ಬಳಸಲಾಗುತ್ತದೆ ಎಂಬುದನ್ನು ನೋಡೋಣ.

ಮುಖ್ಯ ಆಟದ ‌ಲೂಪ್ ನಲ್ಲಿ, **Collectable** sprite ತದ್ರೂಪಿಗಳನ್ನು ಸೃಷ್ಟಿಸುವ ಕೋಡ್‌ನ ಭಾಗಕ್ಕೆ, `collectable-frequency`{:class="block3variables"} ವೇರಿಯೇಬಲ್, ಎರಡು ತದ್ರೂಪಿಗಳನ್ನು ಸೃಷ್ಟಿಸುವ ನಡುವೆ ಎಷ್ಟು ಸಮಯದ ಅಂತರ ಇರಬೇಕೆಂದು ಸೂಚಿಸುತ್ತದೆ:

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

`wait`{:class="block3control"} ಬ್ಲಾಕ್ ಇಲ್ಲಿ `collectable-frequency`{:class="block3variables"} ನಿಗದಿಪಡಿಸಿದ ಸಮಯ ತನಕ ವಿರಾಮ ಹೊಂದುವಂತೆ ಮಾಡುತ್ತದೆ.

`collectable-frequency`{:class="block3variables"} ನ ಮೌಲ್ಯ `<code>0.000001` ಆಗಿದ್ದರೆ, `wait`{:class="block3control"} ಬ್ಲಾಕ್, ಸೆಕೆಂಡಿನ **ದಶಲಕ್ಷ** ಒಂದು ಭಾಗದ ವರೆಗೆ ಮಾತ್ರ ವಿರಾಮ ನೀಡುತ್ತದೆ. ಇದರರ್ಥ <0>repeat until</code>{:class="block3control"} ಲೂಪ್ ನಿರೀಕ್ಷೆಗಿಂತ ಹಲವು ಪಟ್ಟು ಹೆಚ್ಚು ಸಮಯ ಓಡುತ್ತದೆ. ಪರಿಣಾಮವಾಗಿ ಕೋಡ್, `collectable-frequency`{:class="block3variables"} ನ ಬೆಲೆ `1` ಆಗುವ ವರೆಗೆ ಸಾಧಾರಣಕ್ಕಿಂತ ತುಂಬ ಹೆಚ್ಚು ಪವರ್-ಅಪ್ ಗಳನ್ನು ಸೃಷ್ಟಿಸುತ್ತದೆ.

ನೀವು ಇದರಿಂದ ಉಂಟಾಗುವ ಯಾವುದೇ ಸಮಸ್ಯೆಗಳ ಬಗ್ಗೆ ಯೋಚಿಸಬಹುದೇ? ಇನ್ನೂ ಹೆಚ್ಚಿನ ಪವರ್-ಅಪ್‌ಗಳು ಇರುತ್ತವೆ…ನೀವು ಅವುಗಳನ್ನು ಹಿಡಿಯುತ್ತಿದ್ದರೆ ಏನು?

\--- /collapse \---