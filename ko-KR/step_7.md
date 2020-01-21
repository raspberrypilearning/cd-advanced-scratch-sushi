## 경쟁 추가하기

게임이 작동하면 이제 포인트를 모으고 파워 업에서 특별한 힘을 얻고 잃을 수 있습니다. 우리는 좀 더 나아 갈 수 있습니다. 어쩌면 약간의 경쟁을 추가하는 것이 재미있을 것입니다. 조금 움직이는 캐릭터를 포함하는 것은 어떨까요? 이것은 우리가 여기에서 영감을 얻은 슈퍼 마리오와 같은 전통적인 플랫폼 게임의 적과 비슷합니다.

\--- task \--- 먼저, 스프라이트를 선택하여 적으로 추가하십시오. 우리의 플레이어는 고양이이기 때문에 강아지를 선택했습니다. 추가 할 수 있는 다른 스프라이트도 많이 있습니다. 그리고 스프라이트의 이름을 **적**이라 바꾸어 적임을 분명히 하세요.

스프라이트의 크기를 조정하고 시작하기에 적절한 위치에 배치하십시오. 다음과 같이 만들 수 있습니다:

![적 스프라이트, 강아지](images/enemySprite.png) \--- /task \---

\--- task \--- 가장 쉬운 코드부터 써 봅시다. 플레이어가 게임에서 질 때 적을 사라지게 하는 `game over`{:class="events"} 신호에 반응하는 블록을 작성하십시오. 

```blocks3
+ [게임 오버 v] 신호를 받았을 때
+ 숨기기
```

\--- /task \---

\--- task \--- 이제 적의 행동에 대한 코드를 작성해야 합니다. 여기에 있는 코드를 사용하십시오, 하지만 추가 할 부분도 고려해보세요! (다른 플랫폼으로 순간 이동 할 수 있다면 어떨까요? 더 빠르게 혹은 더 느리게 움직이게 하는 파워 업이 있다면 어떨까요?)

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

**참고**: `..로 이동하기`{:class="block3motion"} 블록을 스크립트 영역에 드래그하고 `x` 와 `y` 값을 변경하지 마세요. 이 값은 **적** 스프라이트의 현재 위치를 나타냅니다!

`만약...이라면`{:class="block3control"} 블록의 코드는 스프라이트가 플랫폼 끝에 도달하면 돌아가게 합니다. \--- /task \---

다음으로 필요한 것은 **플레이어 캐릭터** 스프라이트가 **적** 스프라이트에 닿았을 때 플레이어의 목숨이 줄어들게 하는 것입니다. 또한 스프라이트가 닿았을 때 실제로 빨리 **멈추는지** 확인해야 합니다. 그렇지 않으면 닿았는지를 확인하는 코드가 계속 실행되고 플레이어는 계속 목숨이 줄어들기 때문입니다.

\--- task \--- 아래와 같이 코드를 작성해 보았습니다. 이 코드를 개선할 수 도 있을 것입니다. **플레이어 캐릭터** 스프라이트의 메인 블록을 수정합니다. 목숨이 없는지 확인하는 `만약 `{:class="block3control"}블록 앞에 이 코드를 추가합니다.

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

새 코드는 **플레이어 캐릭터** 스프라이트를 숨기고, 시작 위치로 다시 이동하며 `lives`{:class="block3variables"} 변수를 `1`씩 줄입니다. 그리고 0.5초 후 스프라이트가 다시 보이도록 합니다.