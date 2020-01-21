## 슈퍼 파워 업!

새로운 파워 업 수집 작업을 했으므로 이제는 정말 멋진 작업을 수행 할 시간입니다. 단순히 추가 목숨을 제공하는 대신 잠깐 동안 '비 오는' 파워 업을 만들어 보겠습니다.

이를 위해 새로운 `신호 보내기`{: class = "block3events"} 메시지를 사용할 것입니다.

\--- task \---

First, change the `react-to-player`{:class="block3myblocks"} block to broadcast a message when the player character touches a type `2` collectable. Call the message `collectable-rain`{:class="block3events"}.

```blocks3
    react-to-player (type) 정의하기
    만약 <(type ::variable) = [1]> 이라면
       [points v] 를 (collectable-value ::variables) 로 변경하기
    끝
    만약 <(type ::variable) = [2]> 이라면
-        [lives v] 를 [1] 로 변경하기   
+        신호 보내기 [collectable-rain v]
    끝
```

\--- /task \---

Now you need to create a new piece of code inside the **Collectable** sprite scripts that will start whenever the `collectable-rain`{:class="block3events"} message is broadcast.

\--- task \---

Add this code for the **Collectable** sprite to make it listen out for the `collectable-rain`{:class="block3events"} broadcast.

```blocks3
+    [collectable-rain v] 신호를 받았을 때
+    [collectable-frequency v] 를 [0.000001] 로 설정
+    (1) 초 기다리기
+    [collectable-frequency v] 를 [1] 로 설정
```

\--- /task \---

## \--- collapse \---

## title: 새로운 코드가 하는 일은 무엇입니까?

This piece of code waits to receive a broadcast, and responds by setting the `collectable-frequency`{:class="block3variables"} variable to a very small number, then waiting for one second, and then changing the variable back to `1`.

Let's look at how the `collectable-frequency`{:class="block3variables"} variable is used to find out why this makes it rain collectables.

In the main game loop, the part of the code that makes **Collectable** sprite clones gets told by the `collectable-frequency`{:class="block3variables"} variable how long to wait between making one clone and the next:

```blocks3
    <not <(create-collectables ::variables) = [true]>> 까지 반복
        만약 < [50] = (pick random (1) to (50))> 이라면
           [collectable-type v] 를 [2] 로 설정
        아니면
            [collectable-type v] 를 [1] 로 설정
        끝
        (collectable-frequency ::variables) 초 기다리기
        x: ((-240) 부터 (240) 사이의 난수) y:(179) 로 이동
        [myself v] 복제하기
    끝
```

You can see that the `wait`{:class="block3control"} block here pauses the code for the length of time set by `collectable-frequency`{:class="block3variables"}.

If the value of `collectable-frequency`{:class="block3variables"} is `0.000001`, the `wait`{:class="block3control"} block only pauses for **one millionth** of a second, meaning that the `repeat until`{:class="block3control"} loop will run many more times than normal. As a result, the code is going to create **a lot** more power-ups than it normally would, until `collectable-frequency`{:class="block3variables"} is changed back `1`.

Can you think of any problems that might cause? There’ll be a lot more power-ups…what if you kept catching them?

\--- /collapse \---