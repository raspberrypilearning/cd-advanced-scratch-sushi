## 게임에서 질 경우

먼저 첫 번째! 플레이어의 목숨이 다 없어진 경우 게임을 끝내는 방법이 필요합니다. 아무 일도 일어나지 않을 때.

플레이어 캐릭터 스프라이트의 `lose`{: 클래스 = "block3myblocks"} **나만의 블록**스크립트가 비어 있는 상태입니다. 이 부분을 채우고 멋진 '게임 오버'화면에 필요한 모든 부분을 설정합니다. 

\--- task \---

First, find the `lose`{:class="block3myblocks"} block and complete it with the following code:

```blocks3
    lose 정의하기
+    멈추기 [이 스프라이트에 있는 다른 스크립트 v]
+    [game over v] 신호 보내기
+    x:(0) y:(0) 으로 이동하기
+    [Game over!] 을 (2) 초 동안 말하기
+    멈추기 [모두 v]
```

\--- /task \---

## \--- collapse \---

## title: 이 코드는 무엇을 합니까?

Whenever the `lose`{:class="block3myblocks"} block runs now, what it does is:

1. **플레이어 캐릭터**에 작용하는 물리 및 기타 게임 스크립트 중지
2. `game over`{: 클래스 = "block3events"} **신호보내기**를 사용하여 다른 스프라이트들에게 게임이 끝났다고 알립니다.
3. **플레이어 캐릭터** 을 무대 중앙으로 이동시키고 게임 종료를 말하게 합니다.
4. 게임의 모든 스크립트를 중지합니다.

\--- /collapse \---

Now you need to make sure all the sprites know what to do when the game is over, and how to reset themselves when the player starts a new game. **Don’t forget that any new sprites you add also might need code for this!**

### 플랫폼과 가장자리 숨기기

\--- task \---

Start with the easiest sprites. The **Platforms** and **Edges** sprites both need code for appearing when the game starts and disappearing when they receive the `game over`{:class="block3events"} broadcast, so add these blocks to each of them:

```blocks3
+ [게임 오버 v] 신호를 받았을 때
+ 숨기기
```

```blocks3
+ 녹색 깃발이 클릭되었을 때
+ 보이기
```

\--- /task \---

### 별 멈추기

Now, if you look at the code for the **Collectable** sprite, you’ll see it works by **cloning** itself. That is, it makes copies of itself that follow the special `when I start as a clone`{:class="block3events"} instructions.

We’ll talk more about what makes clones special when we get to the step about making new and different collectables. For now, what you need to know is that clones can do **almost** everything a normal sprite can, including receiving `broadcast`{:class="block3events"} messages.

Look at how the **Collectable** sprite works. See if you can understand some of its code:

```blocks3
    녹색 깃발이 클릭되었을 때
    숨기기
    [collectable-value v] 을 [1] 로 정하기
    [collectable-speed v] 을 [1] 로 정하기
    [collectable-frequency v] 을 [1] 로 정하기
    [create-collectables v] 을 [true] 로 정하기
    [collectable-type v] 을 [1] 로 정하기
    <not <(create-collectables) = [true]>> 까지 반복하기
        (collectable-frequency) 초 기다리기
        x: (pick random (-240) to (240)) y: (179) 으로 이동하기
        [myself v] 복제하기
    끝
```

1. 먼저 원래의 **Collectable** 스프라이트를 숨김으로 보이지 않게 합니다.
2. 그런 다음 제어 변수를 설정합니다. - 나중에 다시 돌아올 것입니다.
3. `create-collectables`{:class="block3variables"} 변수는 복제본 생성을 위한 on/off 스위칭 변수입니다: 만약 `create-collectables`{:class="block3variables"} 가 `true`라면 클론을 생성하고, 아니라면 아무것도 하지 않습니다.

\--- task \---

Now set up a block for the **Collectable** sprite so that it reacts to the `game over` broadcast:

```blocks3
+ [게임 오버 v] 신호를 받았을 때
+ 숨기기
+ [create-collectables v]를 [false] 로 정하기
```

\--- /task \---

This code is similar to the code controlling the **Platforms** and **Edges** sprites. The only difference is that you’re also setting the `create-collectables`{:class="block3variables"} variable to `false` so that no new clones get created when it's 'Game over'.

Note that you can use the `create-collectables`{:class="block3variables"} variable to pass messages from one part of your code to another!