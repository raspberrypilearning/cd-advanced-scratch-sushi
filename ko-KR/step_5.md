## 슈퍼 파워 업!

새로운 파워 업 수집 작업을 했으므로 이제는 정말 멋진 작업을 수행 할 시간입니다. 단순히 추가 목숨을 제공하는 대신 잠깐 동안 '비 오는' 파워 업을 만들어 보겠습니다.

이를 위해 새로운 `신호 보내기`{: class = "block3events"} 메시지를 사용할 것입니다.

\--- task \--- 먼저, `react-to-player`{: class = "block3myblocks"} 블록에서 플레이어 캐릭터가 타입 `2` 수집품에 닿았을 때 부분을 메시지 신호 보내기로 변경합니다. `collectable-rain`{:class="block3events"} 신호 보내기를 하십시오.

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

이제 **Collectable** 스프라이트 스크립트 내에`collectable-rain`{: class = "block3events"} 신호가 보내질 때마다 시작되는 새로운 코드를 작성해야 합니다.

\--- task \--- 아래 코드를 **Collectable** 스프라이트에 추가하여 `collectable-rain`{:class="block3events"} 메시지 신호를 받을 수 있도록 하세요.

```blocks3
+    [collectable-rain v] 신호를 받았을 때
+    [collectable-frequency v] 를 [0.000001] 로 설정
+    (1) 초 기다리기
+    [collectable-frequency v] 를 [1] 로 설정
```

\--- /task \---

## \--- collapse \---

## title: 새로운 코드가 하는 일은 무엇입니까?

이 코드는 메시지 신호 받기를 기다렸다가 `collectable-frequency`{: class = "block3variables"} 변수 값을 매우 작은 숫자로 설정 한 다음, 1 초를 기다린 후 다시 `1`로 변경합니다.

`collectable-frequency`{:class="block3variables"} 변수가 어떻게 비 수집품 생성을 가능하게 하는지 살펴 보겠습니다.

**Collectable** 스프라이트의 메인 루프에서 복제본 만드는 코드 부분을 보면, 하나의 복제본과 다음 복제본 사이의 대기 시간이 `collectable-frequency`{:class="block3variables"} 변수 값에 의해 정해지는 것을 알 수 있습니다.

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

`기다리기`{:class="block3control"} 블록을 보면`collectable-frequency`{:class="block3variables"} 변수 값에 따라 설정된 시간 동안 일시 중지 됨을 알 수 있습니다.

만약 `collectable-frequency`{:class="block3variables"} 의 값이 `0.000001`이라면, `기다리기`{:class="block3control"} 블록은 **백만분의 1**초 기다리기가 됩니다. 즉, `..까지 반복하기`{:class="block3control"} 블록이 평소보다 더 많이 실행된다는 것입니다. 결과적으로, 이 코드는 평상시보다 훨씬 ** 많은** 파워 업을 생성하게 됩니다. `collectable-frequency`{:class="block3variables"} 가 다시 `1`로 변경될 때 까지요.

어떤 문제가 생길 수 있을까요? 더 많은 파워 업이 생길 것입니다.…계속해서 잡으면 어떨까요?

\--- /collapse \---