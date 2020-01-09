## 움직이는 플랫폼

나의 레벨 2 버전을 사용하도록 요청한 이유는 레이아웃 중간에 눈에 띄는 갭이 있기 때문입니다. 이 갭을 극복하고 플레이어가 점프하여 탈 수 있는 플랫폼을 만들 것입니다!

![다른 플랫폼이 있는 또 다른 레벨](images/movingPlatforms.png)

먼저 플랫폼 용 스프라이트가 필요합니다.

\--- task \--- 새로운 스프라이트를 생성하고, 이름을 **이동 플랫폼**이라 합니다. 코스튬 탭의 커스터마이징 툴을 사용하여 다른 플랫폼과 유사하게 만듭니다. \(벡터 모드 사용\). \--- /task \---

Now, let's add some code to the sprite.

기본 사항부터 시작하십시오. 끝없는 플랫폼 세트를 화면 위로 이동하려면 일정한 간격으로 플랫폼을 복제해야 합니다. 저는 ` 4`초 간격으로 정했습니다. 또한 레벨 1에 나타나지 않도록 하기 위해, 플랫폼 만들기 용 켜기 / 끄기 스위치가 있어야 합니다. 저는 `create-platforms`{:class="block3variables"} 라는 이름의 새 변수를 추가하였습니다.

\--- task \--- 플랫폼 스프라이트의 복제본을 생성하는 코드를 추가합니다.

아래와 같이 작성합니다:

```blocks3
+    녹색 깃발이 클릭되었을 때
+    숨기기
+    무한 반복
        (4) 초 기다리기
        만약 <(create-platforms ::variables) = [true]> 이라면
            [myself v] 복제하기
        끝
    끝
```

\--- /task \---

\--- task \--- 그런 다음 복제 코드를 추가하십시오.

```blocks3
+    복제되었을 때
+    보이기
+    무한 반복
        만약 <(y position) < [180]> 이라면
            y를 (1)만큼 바꾸기
            (0.02) 초 기다리기
        아니면
            이 복제본 삭제하기
        끝
    끝
```

\--- /task \---

이 코드는 ** 이동 플랫폼 ** 복제본이 화면 상단으로 올라가도록 합니다. 플레이어가 점프할 수 있도록 천천히 움직입니다.

\--- task \--- 이제 레벨을 변경하는 신호 보내기와 `game over`{:class="block3events"} 메시지를 기반으로 플랫폼이 사라지거나 다시 나타나게 만듭니다. 

```blocks3
+    [level-1 v] 신호를 받았을 때
+    [create-platforms v] 를 [false] 로 정하기
+    숨기기

+    [level-2 v] 신호를 받았을 때
+    [create-platforms v] 를 [true] 로 정하기

+    [game over v] 신호를 받았을 때
+    숨기기
+    [create-platforms v] 를 [false] 로 정하기
```

\--- /task \---

이제 실제로 게임을 하려고 하면, **플레이어 캐릭터** 가 플랫폼을 통과합니다.! 왜 그럴까요?

왜냐하면 물리 코드가 플랫폼에 대해 알지 못하기 때문입니다. 빠른 해결책입니다:

\--- task \--- **플레이어 캐릭터** 스프라이트 스크립트에서, 모든 `“Platforms”에 닿았는가?`{:class="block3sensing"} 블록을 `또는`{:class="block3operators"} 연산자를 사용하여 `“Platforms”에 닿았는가?`{:class="block3sensing"} **또는** ` “Moving-Platform”에 닿았는가?`{:class="block3sensing"} 로 바꾸면 됩니다.

** 플레이어 캐릭터** 스프라이트에서 아래와 같은 블록이 보이는 모든 곳을 살펴보십시오.

```blocks3
    <touching [Platforms v] ?>
```

이것으로 교체하십시오:

```blocks3
    <<touching [Platforms v] ?> or <touching [Moving-Platform v] ?>>
```

\--- /task \---