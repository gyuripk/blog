---
title: Java Package
subtitle: "자바의 패기지에대해 이해해보자!"
categories: Java
tags: Study
date: 2021-07-15 23:36:59 +0000
last_modified_at: 2021-07-15 23:36:59 +0000
---
# Java Package

> 학습목표 : 자바의 패키지에대해서 이해해보자!

## package 키워드

### package란?

클래스의 묶음으로 물리적인 하나의 디렉토리이다. 

클래스나 인터페이스의 소스파일(.java)의 첫 번째 문장에 한 번만 선언해주면 된다. 

### package를 사용하는 이유

1. 같은 이름의 클래스를 선언할 때 구분할 수 있다.
2. 관련된 클래스들끼리 그룹단위로 묶어서 효율적으로 관리하기 위함이다. 

### 패키지 이름을 정하는 규칙

- 영문 소문자를 사용한다.
- 점(.)을 구분자로 계층구조를 구성한다.
- 자바 예약어는 사용하지 않는다.

### 참고

- java로 시작하면 자바에서 기본적으로 제공하는 패키지이다.
- javax로 시작하면 자바에서 기본적으로 제공하는 확장 패키지이다.
- org로 시작하면 비영리 단체에서 만든 패키지이다.
- com으로 시작하면 기업에서 만든 패키지이다.
- 패키지를 선언하지 않는 경우, 클래스는 default 패키지에 생성된다. (디폴트 패키지의 경우 package 키우드를 사용하지 않는다.)


## import 키워드

### import란?

다른 패키지에 있는 클래스를 가져다 사용하고 싶을 때 쓰는 키워드로 '패키지명'을 생략할 수 있다. 

결국, 코드를 간결히 하기위해서 사용하는 키워드이다. 

{% gist rbfl6418/02fd4e4143e7a693fc67f6ddbc23df9e %}

### static import문

static import문을 사용해 static멤버를 호출할 때 '클래스 이름'을 생략할 수 있다. 

{% gist rbfl6418/84263c1c6007d9a40869ae04890bb8e2 %}

---

## ClassPath란?

JVM에 의해 프로그램이 실행될 때 사용할 클래스 파일(.class)들을 찾는 경로로, JVM과 컴파일러에서 사용하는 파라미터다.


## CLASSPATH 환경변수

명령 프롬프트에서 컴파일하고 실행하려면 환경변수를 설정해야 한다. 환경변수를 잘못 설정해 놓으면 JVM에서 .class파일을 찾지 못해 프로그램을 실행하지 못한다.


## -classpath 옵션

java 명령어로 실행할 때, -classpath나 -cp 옵션으로 클래스패스를 지정할 수도 있다.


## 제어자(modifier)

### 제어자란?

클래스, 변수, 메서드의 선언부에 쓰이며 부가적인 의미를 준다.

크게 접근 제어자와 그 외의 제어자로 나눌 수 있다. 

### 접근 제어자 (access modifier)

클래스나 클래스의 맴버(변수, 메소드)에 사용되어, 외부에서 접근하지 못하도록 제한하는 역할을 한다.

- 접근 제어자가 사용될 수 있는 곳 - 클래스, 멤버변수, 메서드, 생성자(private-싱글톤패턴)

![/assets/images/2021/07/15/Java-Package/Untitled.png](/assets/images/2021/07/15/Java-Package/Untitled.png)

- 클래스의 접근 제어자

    접근 범위 : public , (default)

- 클래스 맴버(멤버변수, 메서드)에 대한 접근 제어자

    접근 범위 : private < (default) < protected < public 순으로 더 많은 접근을 허용한다.

    1. private : 같은 클래스 내에서만 접근이 가능하다.

    2. default : 같은 패키지 내에서만 접근이 가능하다.

    3. protected 같은 패키지 내에서, 그리고 다른 패키지의 자손 클래스에서 접근 가능하다.

    4. public : 접근 제한이 전혀 없다.

![/assets/images/2021/07/15/Java-Package/Untitled%201.png](/assets/images/2021/07/15/Java-Package/Untitled%201.png)

![/assets/images/2021/07/15/Java-Package/Untitled%202.png](/assets/images/2021/07/15/Java-Package/Untitled%202.png)

### 접근 제어자를 사용하는 이유

- 외부로부터 데이터를 보호하기 위해 → 캡슐화(데이터 감추기)
- 외부에는 불필요한, 내부적으로만 사용되는 부분을 감추기 위해 → 복잡성 줄인다.

즉, 사용자가 접근하면 안되거나 접근 할 필요가 없는 맴버에 대한 접근을 규제하기 위함이다. 

멤버변수에 직접 접근하여 값을 변경하는 문제를 막기위해 일반적으로 속성은 private나 protected로 제한하고, 메소드는 public으로 선언한다. 

---

- 참고

    [https://csw7432.tistory.com/entry/Java-접근제어자-Access-Modifier](https://csw7432.tistory.com/entry/Java-%EC%A0%91%EA%B7%BC%EC%A0%9C%EC%96%B4%EC%9E%90-Access-Modifier)

    [https://blog.naver.com/hsm622/220979792342](https://blog.naver.com/hsm622/220979792342)

    [https://soongjamm.tistory.com/118?category=1062727](https://soongjamm.tistory.com/118?category=1062727)
