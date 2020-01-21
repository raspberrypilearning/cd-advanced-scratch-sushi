## 경쟁 추가하기

게임이 작동하면 이제 포인트를 모으고 파워 업에서 특별한 힘을 얻고 잃을 수 있습니다. 우리는 좀 더 나아 갈 수 있습니다. 어쩌면 약간의 경쟁을 추가하는 것이 재미있을 것입니다. 조금 움직이는 캐릭터를 포함하는 것은 어떨까요? 이것은 우리가 여기에서 영감을 얻은 슈퍼 마리오와 같은 전통적인 플랫폼 게임의 적과 비슷합니다.

\--- task \---

First, pick a sprite to add as your enemy. Because our player character is a cat, I chose a dog. There are lots of other sprites you could add though. I also renamed the sprite **Enemy**, just to make things clearer for me.

Resize the sprite to the right size, and place it somewhere appropriate to start. Here’s what mine looks like:

![The dog enemy sprite](images/enemySprite.png)

\--- /task \---

\--- task \---

Write the easiest code first: set up its block for reacting to the `game over`{:class="events"} message to make the enemy disappear when the player loses the game.

```blocks3
+ [게임 오버 v] 신호를 받았을 때
+ 숨기기
```

\--- /task \---

\--- task \---

Now you need to write the code for what the enemy does. Use my code here, but consider adding extra bits! (What if they can teleport around to different platforms? What if there’s a power-up that makes them move faster, or slower?)

```blocks3
+    녹색 깃발이 클릭되었을 때
+    보이기
+    [enemy-move-steps v] 를 [5] 로 정하기
+    회전 방식을 [left-right v] 으로 정하기
+    x: (-25) y: (-9) 로 이동하기
+    무한 반복
        (enemy-move-steps) 만큼 움직이기
        만약 <not <touching [Platforms v] ?>> 이라면
           [enemy-move-steps v] 를 ((enemy-move-steps) * (-1)) 로 정하기
        끝
     끝
```

**Note**: if you just drag the `go to`{:class="block3motion"} block into the sprite panel and don’t change the `x` and `y` values, they’ll be the values for the current location of the **Enemy** sprite!

The code in the `if...then`{:class="block3control"} block will make the sprite turn around when they get to the end of the platform!

\--- /task \---

The next thing you’ll need is for the player to lose a life when their **Player Character** sprite touches the **Enemy** sprite. Also, you need to make sure the sprites **stop** touching really quickly, since otherwise the code that checks for touching will keep running and the player will keep losing lives.

\--- task \---

Here's how I did it, but you can try to improve on this code! I modified the **Player Character** sprite’s main block. Add the new code before the `if`{:class="block3control"} block that checks if you're out of lives.

```blocks3
    녹색 깃발이 클릭되었을 때
    reset-game :: custom
    무한 반복
        main-physics :: custom
        만약 <(y position) < [-179]> 이라면
            숨기기
            reset-character :: custom
            [lives v] 를 (-1) 로 바꾸기
            (0.05) 초 기다리기
            보이기
        끝
+        만약 <touching [Enemy v] ?> 이라면
            숨기기
            x: (-187) y: (42) 로 이동하기
            [lives v] 를 (-1) 로 바꾸기
            (0.5) 초 기다리기
            보이기
+        끝
        만약 <(lives) < [1]> 이라면
            lose :: custom
        끝
    끝
```

\--- /task \---

The new code hides the **Player Character** sprite, moves it back to its starting position, reduces the `lives`{:class="block3variables"} variable by `1`, and after half a second makes the sprite re-appear.