## 레벨 2

이 단계에서는, 버튼을 누르기만 하면 새로운 레벨의 게임을 추가하게 됩니다. 나중에 코드를 수정하여 특정 포인트 점수 또는 그 밖의 다른 항목으로 게임의 레벨을 변경할 수 있습니다. 다음 단계로 이동 나중에 코드를 변경하여 특정 수의 점 또는 다른 것을 필요로하도록 코드를 변경할 수 있습니다.

### 다음 레벨로 이동

\--- task \---

First, create a new sprite as a button by either adding one from the library or drawing your own. I did a bit of both and came up with this:

![The button sprite to switch levels](images/levelButton.png)

\--- /task \---

\--- task \---

Now, the code for this button is clever: it’s designed so that every time you click it it will take you to the next level, no matter how many levels there are.

Add these scripts to your **Button** sprite. You will need to create some variables as you do so.

```blocks3
+    녹색 깃발을 클릭했을 때
+    [max-level v] 를 [2] 로 설정
+    [min-level v] 를 [1] 로 설정
+    [current-level v] 를 [1] 로 설정
```

```blocks3
+    이 스프라이트를 클릭했을 때
+    [current-level v] 를 (1) 로 변경
+    만약 <(current-level) > (max-level ::variables)> 이라면
        [current-level v] 을 (min-level ::variables) 로 설정
    끝
+    [collectable-cleanup v] 신호 보내기
+    (join [level-](current-level)) 신호 보내기
```

\--- /task \---

Can you see how the program will use the variables you created?

+ `max-level`{:class="block3variables"} 최대 레벨 저장
+ `min-level`{:class="block3variables"} 최소 레벨 저장
+ `current-level`{:class="block3variables"} 현재 레벨 저장

These all need to be set by the programmer \(you!\), so if you add a third level, don’t forget to change the value of `max-level`{:class="block3variables"}! `min-level`{:class="block3variables"} will never need to change, of course.

The broadcasts are used to tell the other sprites which level to display, and to clear up the collectables when a new level starts.

### 스프라이트가 반응하도록 하기

#### **수집품** 스프라이트

Now you need to get the other sprites to respond to these broadcasts! Start with the easiest one: clearing all the collectables.

\--- task \---

Add the following code to the **Collectable** sprite scripts to tell all its clones to `hide`{:class="block3vlooks"} when they receive the cleanup broadcast:

```blocks3
+    [collectable-cleanup v] 신호를 받았을 때
+    숨기기
```

\--- /task \---

Since one of the first things any new clone does is show itself, you don't have to worry about unhiding collectables!

#### **Platforms** 스프라이트

Now to switch the **Platforms** sprite. You can design your own new level later if you like, but for now let’s use the one I’ve already included — you’ll see why on the next step!

\--- task \---

Add this code to the **Platforms** sprite:

```blocks3
+    [level-1 v] 신호를 받았을 때
+    모양을 [Level 1 v] 로 바꾸기
+    보이기
```

```blocks3
+    [level-2 v] 신호를 받았을 때
+    모양을 [Level 2 v] 로 바꾸기
+    보이기
```

\--- /task \---

It receives the `joined`{:class="block3operators"} messages of `level-`{:class="block3variables"} and `current-level`{:class="block3variables"} that the **Button** sprite sends out, and responds by changing the **Platforms** costume.

#### **적** 스프라이트

\--- task \---

In the **Enemy** sprite scripts, just make sure the sprite disappears when the player enters level 2, like this:

```blocks3
+ [level-1 v] 신호를 받았을 때
+ 보이기
```

```blocks3
+    [level-2 v] 신호를 받았을 때
+    숨기기
```

\--- /task \---

If you prefer, you can make the enemy move to another platform instead. In that case, you would use a `go to`{:class="block3motion"} block instead of the `show`{:class="block3looks"} and `hide`{:class="block3looks"} blocks.

### 적절한 장소에 나타나는** 플레이어 캐릭터 만들기 ** 

Whenever a new level starts, the **Player Character** sprite needs to go to the right place for that level. To make this happen, you need to change where the sprite gets its coordinates from when it first appears on the Stage. At the moment, there are fixed `x` and `y` values in its code.

\--- task \---

Begin by creating variables for the starting coordinates: `start-x`{:class="block3variables"} and `start-y`{:class="block3variables"}. Then plug them into the `go to`{:class="block3motion"} block in the `reset-character`{:class="block3myblocks"} **My blocks** block instead of the fixed `x` and `y` values:

```blocks3
    reset-character 정의하기
    [can-jump v] 를 [true] 로 설정
    [x-velocity v] 를 [0] 로 설정
    [y-velocity v] 를 [-0] 로 설정
+    x: (start-x) y: (start-y) 로 이동하기
```

\--- /task \---

\--- task \---

Then for each broadcast announcing the start of a level, set the right `start-x`{:class="block3variables"} and `start-y`{:class="block3variables"} coordinates in response, and add a **call** to `reset-character`{:class="block3myblocks"}:

```blocks3
+    [level-1 v] 신호를 받았을 때
+    [start-x v] 를 [-183] 로 정하기
+    [start-y v] 를 [42] 로 정하기
+    reset-character :: custom
```

```blocks3
+    [level-2 v] 신호를 받았을 때
+    [start-x v] 를 [-218] 로 정하기
+    [start-y v] 를 [-143] 로 정하기
+    reset-character :: custom
```

\--- /task \---

### 레벨 1부터 시작

You also need to make sure that every time someone starts the game, the first level they play is level 1.

\--- task \---

Go to the `reset-game`{:class="block3myblocks"} script and remove the call to `reset-character`{:class="block3myblocks"} from it. In its place, broadcast the `min-level`{:class="block3variables"}. The code you've already added with this card will then set up the correct starting coordinates for the **Player Character** sprite, and also call `reset-character`{:class="block3myblocks"}.

```blocks3
    reset-game 정의하기
    rotation style 를 [left-right v] 로 정하기 
    [jump-height v] 를 [15] 로 정하기 
    [gravity v] 를 [2] 로 정하기 
    [x-speed v] 를 [1] 로 정하기 
    [y-speed v] 를 [1] 로 정하기 
    [lives v] 를 [3] 로 정하기 
    [points v] 를 [0] 로 정하기 
+    ([level-] 과 (min-level ::variables) 결합하기) 신호 보내기
```

\--- /task \---

## \--- collapse \---

## title: 플레이어 캐릭터 리셋과 게임 리셋

Notice that the first block in the **Player Character** sprite's main green flag script is a call to the `reset-game`{:class="block3myblocks"} **My blocks** block.

This block sets up all the variables for a new game and then calls the `reset-character`{:class="block3myblocks"} **My blocks** block, which places the character back in its correct starting position.

Having the `reset-character`{:class="block3myblocks"} code in its own block separate from `reset-game`{:class="block3myblocks"} allows you to reset the character to different positions **without** having to reset the whole game.

\--- /collapse \---