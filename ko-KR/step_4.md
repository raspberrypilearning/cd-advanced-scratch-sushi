## 파워 업

현재 수집 할 수 있는 유형은 한 가지뿐입니다. 수집 할 때 1점을 얻는 별. 이 프로젝트에서는 새로운 유형의 수집품을 만들고, 다른 유형의 수집품도 쉽게 추가 할 수 있는 방식으로 수행 할 것입니다. 그런 다음 자신의 파워 업과 보너스를 만들어 실제로 자신의 게임을 직접 만들 수 있습니다!

우리는 이 작업을 이미 `collectable-type`{:class="block3variables"} 변수와 `pick-costume`{:class="block3myblocks"} **나만의 블록** 으로 일부 수행했습니다. 당신은 그것들을 개선할 필요가 있을 것입니다.

지금 수집품이 어떻게 작동하는지 살펴 보겠습니다.

**Collectable** 스프라이트에 대한 스크립트에서 `복제되었을 때`{class = "block3events"} 코드를 찾으세요. 살펴 봐야 할 블록은 별 수집을 위한 포인트를 주는 블록입니다.

```blocks3
    만약 <touching [Player Character v]?> 이라면
        [points v] 를 (collectable-value ::variables) 만큼 바꾸기
        이 복제본 삭제하기
```

그리고 이 코드는 복제본에 대한 모양을 선택합니다:

```blocks3
    pick-costume (collectable-type :: variables) :: custom
```

## \--- collapse \---

## 제목: 모양을 정하는 방법은 무엇입니까?

`pick-costume`{:class = "block3myblocks"} 블록은 `lose` {:class = "block3myblocks"}과 같은 방식으로 동작을 하지만, 추가된 기능이 있습니다: `type`{:class="block3myblocks"} 이라고 하는**입력** 변수를 사용합니다.

```blocks3
    pick-costume (type) 정의하기
    만약 <(type ::variables) = [1]> 이라면
        모양을 [star1 v] 으로 바꾸기
    끝
```

`pick-costume`{:class="block3myblocks"} 블록이 실행될 때 수행되는 작업은 다음과 같습니다.

1. `type`{:class = "block3myblocks"}이 입력 변수입니다.
2. `type`{:class="block3myblocks"} 이 `1`과 같다면, `star1` 모양으로 바꿉니다.

블록을 사용하는 스크립트 부분을 살펴보십시오.

```blocks3
    복제되었을 때
    pick-costume (collectable-type ::variables) :: custom
    보이기
    <(y position) < [-170]> 까지 반복하기
        y 좌표를 (collectable-speed ::variables) 만큼 바꾸기
        만약 <touching [Player Character v]?> 이라면
            [points v] 을 (collectable-value ::variables) 만큼 바꾸기
            이 복제본 삭제하기
```

`collectable-type`{：class = "block3variables"}변수가 `pick-costume`{：class = "block3myblocks"}블록으로 **전달**되는 것을 알 수 있습니다. `pick-costume`{: class = "block3myblocks"} 코드에서 `collectable-type`{: class = "block3variables"}가 입력 변수로 사용됩니다 (`type`{: class = "block3myblocks"}) ).

즉, `collectable-type`{: class = "block3variables"} 값은 스프라이트 복제본의 모양을 결정합니다.

\--- /collapse \---

### 새로운 파워 업을 위한 모양 추가

물론, 지금은 ** Collectable** 스프라이트는 모양이 한 종류밖에 없습니다. 이제 이를 바꾸려고 합니다.

\--- task \--- 새로운 파워 업을 위해 **Collectable** 스프라이트에 새로운 모양을 추가하십시오. 저는 번개 화살을 좋아하지만, 당신이 좋아하는 것을 고르세요. \--- /task \---

\--- task \--- 다음으로, `pick-costume`{:class=block3myblocks} **나만의 블록** 에서 새로운 `type`{:class="block3myblocks"}값을 받을 때마다 새로운 모양으로 바꾸는 블록을 사용합니다.

```blocks3
    pick-costume (type) 정의하기
    만약 <(type ::variable) = [1]> 이라면
        모양을 [star1 v] 으로 바꾸기
    끝
+    만약 <(type ::variable) = [2]> 이라면
+        모양을 [lightning v] 으로 바꾸기
+    끝
```

\--- /task \---

### 파워 업 코드 생성

이제 새로운 수집품이 할 일을 결정해야 합니다! 우리는 플레이어에게 목숨을 추가로 주는 간단한 것으로 시작합니다. 다음 단계에서는 더 멋진 작업을 수행하게 됩니다.

\--- task \--- **나만의 블록** 섹션으로 가서 **블록 만들기를 **클릭하십시오. 새 블록의 이름을 `react-to-player`{:class = "block3myblocks"})로 입력하고 `type`{: class = "block3myblocks"}에 **숫자 입력값 추가하기**를 클릭합니다.

![블록의 이름을 입력하십시오.](images/powerupMakeName.png)

**확인**을 클릭하세요. \--- /task \---

\--- task \--- `react-to-player`{:class="block3myblocks"} 블록을 **나만의 블록** 으로 만들고 `type`{:class= "block3myblocks"} 값에 따라 포인트나 플레이어의 목숨을 늘릴 수 있습니다.

```blocks3
+    react-to-player (type) 정의하기
+    만약 <(type ::variable) = [1]> 이라면
+       [points v] 을 (collectable-value ::variables) 만큼 바꾸기
+    끝
+    만약 <(type ::variable) = [2]> 이라면
+        [lives v] 을 [1] 만큼 바꾸기
+    끝
```

\--- /task \---

\--- task \--- `복제되었을 때`{:class="block3events"} 코드 부분을 업데이트하세요. 포인트 값을 증가하는 블록 대신에 `collectable-type`{:class="block3variables"}을 ** 전달** 받은 `react-to-player`{:class="block3myblocks"}블록을 **호출**하는 코드로 바꿔줍니다.

```blocks3
+    만약 <touching [Player Character v] ?> 이라면
+        react-to-player (collectable-type ::variables) :: custom
+        이 복제본 삭제하기
+    끝
```

\--- /task \---

이 새로운 `react-to-player`{: class = "block3myblocks"} **나만의 블록** 을 사용함으로써, 여전히 별은 포인트를 추가하고, 당신이 만든 새로운 파워 업은 목숨을 추가합니다.

### 다른 수집품이 무작위로 나타나게 하기 위한 `collectable-type`{: class = "block3variables"} 사용하기

지금 당신은 각 수집품들로 어떤 유형의 게임을 만들어야 할지 궁금할 것입니다.

`collectable-type`{: class = "block3variables"}의 값을 설정하여 이 작업을 수행 할 수 있습니다. 이 변수는 숫자입니다. 앞에서 보았듯이, `pick-costume`{class = "block3myblocks"})과 `react-to-player`{: class = "block3myblocks"에서 수집품의 모양, 규칙 등 을 정하는 데 사용되었습니다.

## \--- collapse \---

## title: 복제본에서 변수 작업

**Collectable** 스프라이트의 각 복제본에 대해 `collectable-type`{:class="block3variables"} 변수 값을 다르게 설정 할 수 있습니다.

**Collectable** 스프라이트가 복제될 때 `collectable-type`{: class = "block3variables"}에 저장되는 값을 사용하여 **Collectable** 스프라이트의 새 복제본을 만드는 것으로 생각하세요.

`collectable-type`{: class = "block3variables"}의 값을 변경하면 스테이지의 모든 수집품들이 같은 유형으로 바뀌게 되는지 궁금할 것입니다. 그런 일은 일어나지 않습니다. 왜냐하면 복제하기를 특별하게 만드는 이유 중 하나는 시작하는 변수의 값을 변경할 수 없기 때문입니다. 스프라이트 복제본은 효과적으로 **일정한 값**을 갖습니다. 즉, `collectable-type`{:class="block3variables"}의 값을 변경할 때 이미 게임에 있는 **Collectable** 스프라이트 복제본에는 영향을 미치지 않습니다. \--- /collapse \---

당신이 만드는 각각의 새로운 복제본에 대해 `collectable-type`{:class="block3variables"}을 `1` 또는 `2` 로 설정하려고 합니다. 게임을 재미있게 유지하려면 숫자를 무작위로 선택하여 매번 난수로 수집 할 수 있도록 하십시오.

\--- task \--- **Collectable** 스프라이트의 녹색 깃발을 클릭했을 때 블록 내용 중 `..까지 반복하기`{:class="block3control"}를 찾아 아래와 같이 `만약 이라면 ... 아니면`{:class=" block3control "} 코드를 추가하세요.

```blocks3
    <not <(create-collectables ::variables) = [true]>> 까지 반복
+        만약 <[50] = (pick random (1) to (50))> 이라면
+            [collectable-type v] 를 [2] 로 설정
+        아니면
+           [collectable-type v] 를 [1] 로 설정
+        끝
       (collectable-frequency ::variables) 까지 기다리기
        x: ((-240) 부터 (240) 사이의 난수) y: (179) 로 이동
        [myself v] 복제하기
```

\--- /task \---

이 코드는 `collectable-type`{:class="block3variables"}을 `2`로 설정할 수 있는 기회가 1 부터 50 중에서 한번만 주어집니다. 결국, 플레이어에게 목숨 추가 기회를 너무 자주 주지 않으려고 합니다. 그렇지 않으면 게임이 너무 쉬울 것입니다.

이제 별 대신 표시되는 새로운 유형의 수집품이 있습니다. 포인트가 아니라 추가 목숨을 주는 것입니다.