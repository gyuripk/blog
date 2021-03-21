---
layout: single
title: "가비지 컬렉터를 알아보자!"
category: Java
---


> 학습 목표 : 가비지 컬렉터의 역할과 동작방식을 이해해보자!

---

## GC란?

JVM의 Heap영역에서 사용하지 않는 객체를 삭제하는 프로세스를 말한다.

자바는 managed Language로써, 사용자 대신 JVM안에 있는 Garbage Collector가 메모리를 자동으로 관리해주는 언어다.

- 탄생 배경 : 개발자가 사용한 모든 메모리를 직접 삭제하고, 관리하는 번거로움을 줄여주기 위해 만들어졌다.
- 역할 : JVM안에 있는 기능 중 하나로써 Heap영역의 메모리를 특정 로직에 의해 관리해주는 역할을 한다

---

## GC의 수거대상 : reachability
GC는 객체가 수거의 대상인지 판별하기 위해 reachability라는 개념을 사용한다.

- Reachable : 참조되고 있는 객체
- Unreachable : 참조되지 않고 있는 객체 → GC의 수거 대상이 된다.

아래 그림과 같이 객체들은 참조 사슬을 이루는데, 유요한 참조 여부를 파악하려면 '항상 유효한 최초의 참조'가 있어야한다. 이를 객체 참조의 Root Set이라고 한다.

- GC roots가 되는 조건
    1. stack 영역에 있는 지역변수, 메서드의 파라미터 등등
    2. method영역에 있는 변수들, static 데이터들 (ClassLoader에 의해 로드된 것들)
    3. JNI(Java Native Interface)에 의해 생성된 객체들

![GC%20Garbage%20Collection%200692e2d6ffe34899b0d3e338d1465e4c/Untitled.png](/assets/images/2021/03/20/Untitled.png)

![GC%20Garbage%20Collection%200692e2d6ffe34899b0d3e338d1465e4c/Untitled%201.png](/assets/images/2021/03/20/Untitled%201.png)

---

## GC의 동작 방식

1. mark & sweep (compact)

     필요한 것을 mark하고 나머지 것들은 sweep해서 제거하는 방식이다. (알고리즘에 따라 compact까지 한싸이클로 동작한다.)

    ![GC%20Garbage%20Collection%200692e2d6ffe34899b0d3e338d1465e4c/Untitled%202.png](/assets/images/2021/03/20/Untitled%202.png)

    - mark : GC root로부터 모든 변수를 스캔하며 참조된 것들을 체크해둔다. (식별과정)

    ![GC%20Garbage%20Collection%200692e2d6ffe34899b0d3e338d1465e4c/Untitled%203.png](/assets/images/2021/03/20/Untitled%203.png)

    - sweep : 마크되지 않은 unreachable한 객체를 heap영역에서 제거한다.

    ![GC%20Garbage%20Collection%200692e2d6ffe34899b0d3e338d1465e4c/Untitled%204.png](/assets/images/2021/03/20/Untitled%204.png)

    - compact : sweep후에 흩어져있는 객체들을 heap의 시작주소로 모아서 메모리의 단편화를 막아준다. (메모리가 할당된 부분과 그렇지 않은 부분을 구분해놓는다)
2. reference counting (참조 카운팅)

     한 요소가 다른 요소에게 참조 되는 횟수를 세어서 더이상 참조되지 않는 것들을 제거하는 방식이다.

---

## Heap의 Generation Structure

![GC%20Garbage%20Collection%200692e2d6ffe34899b0d3e338d1465e4c/Untitled%205.png](/assets/images/2021/03/20/Untitled%205.png)

![GC%20Garbage%20Collection%200692e2d6ffe34899b0d3e338d1465e4c/Untitled%206.png](/assets/images/2021/03/20/Untitled%206.png)

- Young Generation : 새로 만들어진 객체들이 저장되는 곳
- Old Generation : Young Generation에서 오랫동안 살아남은 객체들이 저장되는 곳
- Permanent Generation : 가비지 컬렉션 시에 필요한 클레스와 메서드의 요약정보를 담고있는 영역

---

## GC의 과정

1. 새로운 객체가 만들어지면 → Eden 영역에 할당된다.(survivor 영역은 둘다 빈 상태로 시작한다)

    ![GC%20Garbage%20Collection%200692e2d6ffe34899b0d3e338d1465e4c/bb.png](/assets/images/2021/03/20/bb.png)

2. Eden영역이 다 채워지면  → minor GC가 발생되어 → Eden영역이 청소된다. (Unreferenced 객체들 제거)
3. Eden에서 살아남은 객체들(Referenced) → age가 +1되며 servivor영역에 할당된다.

    ![GC%20Garbage%20Collection%200692e2d6ffe34899b0d3e338d1465e4c/Untitled%207.png](/assets/images/2021/03/20/Untitled%207.png)

4. 이후에 다시 Eden영역이 차면 → minor GC가 발생되어 → 객체가 있는 Eden과  Survivor영역이 청소된다. 
5. 마찬가지로, 살아남은 객체들은 → age가 +1되며 다른 servivor영역에 할당된다.

    ![GC%20Garbage%20Collection%200692e2d6ffe34899b0d3e338d1465e4c/Untitled%208.png](/assets/images/2021/03/20/Untitled%208.png)

    ![GC%20Garbage%20Collection%200692e2d6ffe34899b0d3e338d1465e4c/Untitled%209.png](/assets/images/2021/03/20/Untitled%209.png)

6. 1~5번이 반복되어 객체의 age가 특정 숫자 이상이되면(여기에선 8) → Old Generation영역에 할당된다. (Tenured)

    ![GC%20Garbage%20Collection%200692e2d6ffe34899b0d3e338d1465e4c/Untitled%2010.png](/assets/images/2021/03/20/Untitled%2010.png)

    - Promotion : Young Generation에서 살아남은 객체들이 Old Generation영역으로 할당되는 것

    ![GC%20Garbage%20Collection%200692e2d6ffe34899b0d3e338d1465e4c/Untitled%2011.png](/assets/images/2021/03/20/Untitled%2011.png)

7. 이런 과정들이 반복되어 Old 영역도 다 채워지면 → major GC가 발생하여 → Old영역의 Unreferenced된 객체를 삭제한다.

---

## Stop The World

GC를 실행하기 위해 JVM이 애플리케이션 실행을 멈추는 것을 의미한다.

→ GC를 실행하는 Thread외의 모든 Thread가 작업을 중단한다.

GC의 종류에 따라서 Stop The World가 발생하는 시간이 다르다.

---

## GC의 종류

- Serial GC
- Parallel GC
- Parallel Old GC
- CMS GC(Concurrent Mark Sweep)
- G1 GC(Garbage First)
