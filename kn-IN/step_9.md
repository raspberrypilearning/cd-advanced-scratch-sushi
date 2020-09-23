## ಚಲಿಸುವ ವೇದಿಕೆಗಳು (ಪ್ಲಾಟ್‌ಫಾರ್ಮ್)

ನನ್ನ 2 ನೇ ಹಂತದ ಆವೃತ್ತಿಯನ್ನು ಬಳಸಲು ನಾನು ನಿಮ್ಮನ್ನು ಕೇಳಲು ಕಾರಣ ‌ವಿನ್ಯಾಸದ ಮಧ್ಯದಲ್ಲಿರುವ ಅಂತರ ಎಂದು ನೀವು ಗಮನಿಸಿರಬಹುದು. ಈ ಅಂತರವನ್ನು ಅಂತರದಲ್ಲಿ ಪ್ಲಾಟ್‌ಫಾರ್ಮ್ ಅನ್ನು ನೀವು ರಚಿಸಲಿದ್ದೀರಿ ಮತ್ತು ಆಟಗಾರನು ಜಿಗಿಯಬಹುದು ಮತ್ತು ಸವಾರಿ ಮಾಡಬಹುದು!

![ವಿಭಿನ್ನ ವೇದಿಕೆಗಳನ್ನು ಹೊಂದಿರುವ ಮತ್ತೊಂದು ಹಂತ](images/movingPlatforms.png)

ಮೊದಲಿಗೆ, ಪ್ಲಾಟ್‌ಫಾರ್ಮ್‌ಗಾಗಿ ನಿಮಗೆ sprite ಅಗತ್ಯವಿದೆ.

--- task ---

ಹೊಸ sprite ಅನ್ನು ಸೇರಿಸಿ, ಅದಕ್ಕೆ **Moving-Platform** ಎಂದು ಹೆಸರಿಸಿ, ಮತ್ತು Costumes ಟ್ಯಾಬ್‌ನಲ್ಲಿ ವೇಷಭೂಷಣ ಗ್ರಾಹಕೀಕರಣ ಸಾಧನಗಳನ್ನು ಬಳಸಿ \(vector mode ಬಳಸಿ\) ಇತರ ಪ್ಲ್ಯಾಟ್‌ಫಾರ್ಮ್‌ಗಳಂತೆ ಕಾಣುವಂತೆ ಮಾಡಿ.

--- /task ---

ಈಗ, sprite ಗೆ ಕೆಲವು ಕೋಡ್ ಅನ್ನು ಸೇರಿಸೋಣ.

ಮೂಲಭೂತ ಸಂಗತಿಗಳೊಂದಿಗೆ ಪ್ರಾರಂಭಿಸಿ: ಪರದೆಯ ಮೇಲೆ ಚಲಿಸುವ ಪ್ಲಾಟ್‌ಫಾರ್ಮ್‌ಗಳ ಅಂತ್ಯವಿಲ್ಲದ ಗುಂಪನ್ನು ಮಾಡಲು, ನೀವು ಪ್ಲ್ಯಾಟ್‌ಫಾರ್ಮ್ ಅನ್ನು ನಿಯಮಿತ ಮಧ್ಯಂತರದಲ್ಲಿ ಕ್ಲೋನ್ ಮಾಡಬೇಕಾಗುತ್ತದೆ. ನಾನು interval ಆಗಿ `4` ಸೆಕೆಂಡುಗಳನ್ನು ಆರಿಸಿದೆ. ಪ್ಲ್ಯಾಟ್‌ಫಾರ್ಮ್‌ಗಳನ್ನು ತಯಾರಿಸಲು ಆನ್/ಆಫ್ ಸ್ವಿಚ್ ಇದೆ ಎಂದು ನೀವು ಖಚಿತಪಡಿಸಿಕೊಳ್ಳಬೇಕು, ಇದರಿಂದ ಅವು ಹಂತ 1 ರಲ್ಲಿ ತೋರಿಸುವುದಿಲ್ಲ. ನಾನು `create-platforms`{:class="block3variables"} ಎಂಬ ಹೊಸ ವೇರಿಯೇಬಲ್ ಅನ್ನು ಬಳಸುತ್ತಿದ್ದೇನೆ.

--- task ---

ನಿಮ್ಮ ಪ್ಲಾಟ್‌ಫಾರ್ಮ್ sprite‌ ನ ತದ್ರೂಪುಗಳನ್ನು ರಚಿಸಲು ಕೋಡ್ ಸೇರಿಸಿ.

ನನ್ನದು ಇಲ್ಲಿಯವರೆಗೆ ಹೇಗೆ ಕಾಣುತ್ತದೆ ಎಂಬುದು ಇಲ್ಲಿದೆ:

```blocks3
+    when green flag clicked
+    hide
+    forever
        wait (4) secs
        if <(create-platforms ::variables) = [true]> then
            create clone of [myself v]
        end
    end
```

--- /task ---

--- task ---

ನಂತರ ತದ್ರೂಪಿ ಕೋಡ್ ಸೇರಿಸಿ:

```blocks3
+    when I start as a clone
+    show
+    forever
        if <(y position) < [180]> then
            change y by (1)
            wait (0.02) secs
        else
            delete this clone
        end
    end
```

--- /task ---

ಈ ಕೋಡ್ **Moving-Platform** ತದ್ರೂಪಿ ಪರದೆಯ ಮೇಲ್ಭಾಗಕ್ಕೆ ಚಲಿಸುವಂತೆ ಮಾಡುತ್ತದೆ, ಆಟಗಾರನು ನಿಧಾನವಾಗಿ ಮತ್ತು ಹೊರಗೆ ಹೋಗಲು ಸಾಕಷ್ಟು ನಿಧಾನಗೊಳಿಸುತ್ತದೆ ಮತ್ತು ನಂತರ ಕಣ್ಮರೆಯಾಗುತ್ತದೆ.

--- task ---

ಈಗ ಹಂತಗಳನ್ನು ಬದಲಾಯಿಸುವ ಪ್ರಸಾರಗಳ ಆಧಾರದ ಮೇಲೆ ವೇದಿಕೆ‌ಗಳು ಕಣ್ಮರೆಯಾಗುವಂತೆ/ಮತ್ತೆ ಗೋಚರಿಸುವಂತೆ ಮಾಡಿ (ಆದ್ದರಿಂದ ಅವುಗಳು ಸ್ಥಳಾವಕಾಶದೊಂದಿಗೆ ಮಾತ್ರ ಮಟ್ಟದಲ್ಲಿರುತ್ತವೆ), ಮತ್ತು `game over`{:class="block3events"} ಸಂದೇಶ.

```blocks3
+    when I receive [level-1 v]
+    set [create-platforms v] to [false]
+    hide

+    when I receive [level-2 v]
+    set [create-platforms v] to [true]

+    when I receive [game over v]
+    hide
+    set [create-platforms v] to [false]
```

--- /task ---

ಈಗ, ನೀವು ನಿಜವಾಗಿಯೂ ಆಟವನ್ನು ಆಡಲು ಪ್ರಯತ್ನಿಸಿದರೆ, **Player Character** ವೇದಿಕೆಯ ಮೂಲಕ ಬೀಳುತ್ತದೆ! ಏಕೆ ಎಂದು ಗೊತ್ತೆ?

ಇದಕ್ಕೆ ಕಾರಣ ಪ್ಲಾಟ್‌ಫಾರ್ಮ್ ಬಗ್ಗೆ ಭೌತಶಾಸ್ತ್ರ ಕೋಡ್‌ಗೆ ತಿಳಿದಿಲ್ಲದಿರುವುದು. ಇದು ನಿಜಕ್ಕೂ ತ್ವರಿತ ಪರಿಹಾರ:

--- task ---

**Player Character** sprite ಸ್ಕ್ರಿಪ್ಟ್‌ನಲ್ಲಿ, ಪ್ರತಿಯೊಂದು `touching “Platforms”`{:class="block3sensing"} ಬ್ಲಾಕ್ ನ ಬದಲು, **ಒಂದೋ** `touching “Platforms”`{:class="block3sensing"} **ಅಥವಾ** `touching “Moving-Platform”`{:class="block3sensing"} ಎಂದು ತೀರ್ಮಾನಿಸುವ `OR`{:class="block3operators"} ಆಪರೇಟರ್ ಅನ್ನು ಉಪಯೋಗಿಸಿ.

**Player Character** spriteನ ಕೋಡ್ ಅನ್ನು ಗಮನಿಸಿದರೆ ಎಲ್ಲೆಲ್ಲೂ ನೀವು ಈ ಕೆಳಗಿನದನ್ನು ನೋಡಬಹುದು:

```blocks3
    <touching [Platforms v] ?>
```

ಇದನ್ನು ಇದರೊಂದಿಗೆ ಬದಲಾಯಿಸಿ:

```blocks3
    <<touching [Platforms v] ?> or <touching [Moving-Platform v] ?>>
```

--- /task ---