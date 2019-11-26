## 레벨 2

이 단계에서는, 버튼을 누르기만 하면 새로운 레벨의 게임을 추가하게 됩니다. 나중에 코드를 수정하여 특정 포인트 점수 또는 그 밖의 다른 항목으로 게임의 레벨을 변경할 수 있습니다. 다음 단계로 이동 나중에 코드를 변경하여 특정 수의 점 또는 다른 것을 필요로하도록 코드를 변경할 수 있습니다.

### 다음 레벨로 이동

\--- task \--- 먼저, 스프라이트 고르기로 추가하거나 또는 직접 그려서 새로운 버튼 스프라이트를 만듭니다. 두 가지 방법을 다 이용하여 다음과 같이 만들었습니다.

![스위치 레벨에 따른 버튼 스프라이트](images/levelButton.png) \--- /task \---

\--- task \--- 이 버튼에 대한 코드는 명확합니다. 클릭 할 때마다 얼마나 많은 레벨이 있더라도 다음 레벨로 이동하도록 합니다.

이 스크립트를 **버튼** 스프라이트에 추가하세요. 그렇게 하려면 일부 변수도 만들어야 합니다.

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

\--- /task \--- 프로그램이 당신이 만든 변수를 어떻게 사용하는지 알 수 있습니까?

+ `max-level`{:class="block3variables"} 최대 레벨 저장
+ `min-level`{:class="block3variables"} 최소 레벨 저장
+ `current-level`{:class="block3variables"} 현재 레벨 저장

이것들은 모두 프로그래머가 설정해야 합니다 (당신!), 세 번째 레벨을 추가하는 경우, `max-level`{:class="block3variables"} 값을 변경하는 것을 잊지 마십시오. 물론 `min-level`{:class="block3variables"} 은 변경할 필요가 없습니다.

신호 보내기는 표시 할 레벨을 다른 스프라이트에 알리고, 새 레벨이 시작될 때 수집품들을 지우는 데 사용됩니다.

### Make the sprites react

#### **Collectable** 스프라이트

이제 다른 스프라이트가 이 신호 보내기에 응답하도록 해야 합니다! 가장 쉬운 것부터 시작하십시오: 모든 수집품 지우기.

\--- task \--- **Collectable** 스프라이트에 다음 코드를 추가합니다. 모든 복제본이 cleanup 신호를 받았을 때 `숨기기`{:class="block3looks"} 를 실행하도록 하세요.

```blocks3
+    [collectable-cleanup v] 신호를 받았을 때
+    숨기기
```

\--- /task \---

새로운 복제본이 가장 먼저 하는 일 중 하나는 스스로를 보이는 것이기 때문에 숨기기 해제에 대해 걱정할 필요가 없습니다!

#### **Platforms** 스프라이트

이제 **Platforms** 스프라이트를 작업하도록 하겠습니다. 원하는 경우 나중에 새 레벨을 디자인 할 수 있지만, 지금은 이미 포함 된 것을 사용합시다. - 다음 단계에서 그 이유를 알 수 있습니다!

\--- task \--- 아래 코드를 **Platforms** 스프라이트에 추가합니다:

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

이는 `level-`{:class="block3variables"} 과 `current-level`{:class="block3variables"} `결합하기`{:class="block3operators"} 신호를 **Button** 스프라이트가 전송합니다. 그리고 **Platforms** 모양이 변경되는 응답을 받습니다.

#### **적** 스프라이트

\--- task \--- **적** 스프라이트 스크립트에서는, 플레이어가 레벨 2에 들어갈 때 스프라이트가 사라지는지 확인합니다. 이렇게 :

```blocks3
+ [level-1 v] 신호를 받았을 때
+ 보이기
```

```blocks3
+    [level-2 v] 신호를 받았을 때
+    숨기기
```

\--- /task \---

원하는 경우 적을 다른 플랫폼으로 이동 시킬 수 있습니다. 이 경우에는`보이기`{:class="block3looks"} 와 `숨기기`{:class="block3looks"} 블록 대신 `이동하기`{:class="block3motion"} 블록을 사용합니다.

### 적절한 장소에 나타나는** 플레이어 캐릭터 만들기 ** 

새로운 레벨이 시작될 때마다, ** 플레이어 캐릭터 ** 스프라이트는 해당 레벨의 올바른 위치로 이동해야 합니다. 이를 위해서는 스프라이트가 스테이지에 처음 나타날 때 좌표를 가져 오는 위치를 변경해야합니다. 현재 고정된 ` x ` 및 ` y ` 값을 코드에 넣습니다.

\--- task \--- 좌표값을 저장하는 변수를 만듭니다: `start-x`{:class="block3variables"} 와 `start-y`{:class="block3variables"}. 그런 다음 **나만의 블록** `reset-character`{:class="block3myblocks"} 안에 있는 `로 이동하기`{:class="block3motion"} 블록을 찾아 `x` 와 `y` 변수 값을 수정합니다:

```blocks3
    reset-character 정의하기
    [can-jump v] 를 [true] 로 설정
    [x-velocity v] 를 [0] 로 설정
    [y-velocity v] 를 [-0] 로 설정
+    x: (start-x) y: (start-y) 로 이동하기
```

\--- /task \---

\--- task \--- 그런 다음, 각 레벨에서 `start-x`{:class="block3variables"} 와 `start-y`{:class="block3variables"} 좌표를 정해주고, `reset-character`{:class="block3myblocks"} 를 **호출** 합니다.

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

누군가 게임을 시작할 때마다 그들이 하는 첫 번째 레벨이 1레벨인지 확인해야 합니다.

\--- task \--- `reset-game`{:class="block3myblocks"} 스크립트에서, `reset-character`{:class="block3myblocks"} 블록을 삭제합니다. 그 자리에, `min-level`{:class="block3variables"} 신호 보내기를 설정합니다. 이 코드는 이미 **플레이어 캐릭터 스프라이트** 에 추가된 적이 있습니다. 그리고 `reset-character`{:class="block3myblocks"}에도 올바른 좌표값을 설정하도록 합니다.

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

**플레이어 캐릭터** 메인 코드의 첫 번째 블록을 보면 초록색 깃발이 클릭되었을 때 `reset-game`{:class="block3myblocks"} **나만의 블록** 을 호출합니다.

이 블록은 새로운 게임에 대한 모든 변수를 설정하고, `reset-character`{:class="block3myblocks"} **나만의 블록** 을 호출 하여 캐릭터를 올바른 시작 위치로 되돌립니다.

`reset-game`{:class="block3myblocks"} 과는 별도로 `reset-character`{:class="block3myblocks"}자체 블록을 가지고 있으면 게임 전체를 리셋 할 필요 없이 캐릭터를 다른 위치로 리셋 할 수 있습니다.

\--- /collapse \---