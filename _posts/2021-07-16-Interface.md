---
title: Interface
subtitle: "자바의 인터페이스에 대해 알아보자!"
categories: Java
tags: Study
date: 2021-07-16 00:28:42 +0000
last_modified_at: 2021-07-16 00:28:43 +0000
---
# Interface

> 학습 목표 : 자바의 인터페이스에 대해 알아보자!

## 인터페이스란?

일종의 추상클래스이지만, 추상클래스보다 추상화정도가 더 높아, 
일반 메서드나 멤버변수를 가질 수 없다.  

추상클래스와 상수만으로 구성되어 구현을 강제하는 역할을 한다. 

추상메서드처럼, 인터페이스도 불완전 한 것이므로 그 자체로 객체를 생성해 사용할 수 없다. 

다른 클래스를 작성하는데 도움을 줄 목적으로 작성된다.

### 인터페이스를 사용하는 이유(장점)

1. 개발시간을 단축시킬 수 있다.
2. 표준화가 가능하다.
3. 서로 관계없는 클래스들에게 관계를 맺어 주어 묶어서 관리할 수 있다.

### 인터페이스 정의하는 방법

클래스 작성하는 것과 같고 키워드로 class대신 'interface'를 사용한다. 

접근제어자 public 또는 default를 사용할 수 있다. (생략가능)

[https://gist.github.com/rbfl6418/471d9dc6dbaae447f4f0f1d4fd89ff99](https://gist.github.com/rbfl6418/471d9dc6dbaae447f4f0f1d4fd89ff99)

[참고] 이름은 주로 '~을 할 수 있는'의 의미인 'able'로 끝나는 것들이 많다.

### 인터페이스 멤버(멤버변수,메서드) 제약조건

- 모든 멤버변수는 **`public static final`**(상수) 이어야한다. (제어자 생략가능)
- 모든 메서드는 **`public abstract`**(추상메서드) 이어야한다.(제어자 생략가능)

제어자는 모든 인터페이스 멤버에 예외없이 적용되는 것이기 때문에 생략할 수 있다. 생략한 제어자는 컴파일 시에 컴파일러가 자동적으로 추가해준다. 

JDK 1.8 이전 버전 : 상수  + 추상클래스 이렇게 두가지만 가질 수 있다.

[주의!]  (JDK 1.8 이후부터) static메서드와 default 메서드도 추가할 수 있다.

[https://gist.github.com/rbfl6418/2d7aa45d1a901e16e1469c5da2523fc3](https://gist.github.com/rbfl6418/2d7aa45d1a901e16e1469c5da2523fc3)

---

### 인터페이스 상속(Extends)

![/assets/images/2021/07/16/Interface/Untitled.png](/assets/images/2021/07/16/Interface/Untitled.png)

[https://www.cdn.geeksforgeeks.org/wp-content/uploads/extends.png](https://www.cdn.geeksforgeeks.org/wp-content/uploads/extends.png)

인터페이스는 인터페이스로부터만 상속받을 수 있고, 클래스와 달리 다중상속이 가능하다. 
클래스의 상속과 마찬가지로 조상인터페이스의 멤버(상수, 추상 메서드)를 모두 상속받아 사용할 수 있다. 

[https://gist.github.com/rbfl6418/d23e1ea542b8fdf6693fa538b21ee4bd](https://gist.github.com/rbfl6418/d23e1ea542b8fdf6693fa538b21ee4bd)

[참고] 인터페이스는 클래스와 달리 Object클래스와 같은 최고 조상이 없다.

### 인터페이스 구현하는 방법(Implements)

추상클래스처럼 인터페이스 자체로는 미완성 메서드를 포함하기 때문에 인스턴스를 생성할 수 없다.

그래서 상속을 통해서 정의된 추상메서드를 구현하는 클래스를 작성해야만 인스턴스를 생성할 수 있다. 
구현한다는 의미에서 'implements' 키워드를 사용한다.  

[https://gist.github.com/rbfl6418/2bb93cd4dc91d0c83b3115b36bc925ec](https://gist.github.com/rbfl6418/2bb93cd4dc91d0c83b3115b36bc925ec)

인터페이스의 메서드를 오버라이딩해 준다.

[https://gist.github.com/rbfl6418/2628a2b14545e67f54d760f5b014570e](https://gist.github.com/rbfl6418/2628a2b14545e67f54d760f5b014570e)

[주의!] 

인터페이스에선 컴파일러가 자동으로 메서드 앞에 public붙여주지만 
클래스에서는 public명시하지 않으면 default가 된다. 
오버라이딩 할 때는 조상의 메서드보다 넓은 범위의 접근 제어자를 지정해야하므로 
public → default로 좁은 범위로 제한 하는 것은 컴파일 에러가 발생한다. 

(error : Cannot reduce the visibility of the inherited method from Movable)

 **즉, 인터페이스의 메서드를 받아 구현할 때는 반드시 접근 제어자를 public으로 해야 한다.**

아래와 같이 하나의 클래스에 여러개의 인터페이스를 구현할 수도 있다. 

클래스를 여러개 상속할 때와 달리, 서로 다른 인터페이스에 같은 추상 메서드가 있어도 문제가 없다. 

어차피 아직 구현이 안된 추상 메서드이므로, 같은 메서드를 상속 받아도 한 번만 구현하면 된다.
(구현부 내용이 겹쳐 에러가 날 일이 없다.)

[https://gist.github.com/rbfl6418/9276f7871c55d57703e049079c77ce35](https://gist.github.com/rbfl6418/9276f7871c55d57703e049079c77ce35)

### 인터페이스 레퍼런스(참조)를 통해 구현체를 사용하는 방법  
→ 인터페이스를 이용한 다형성

인스턴스는 불완전한 메서드인 추상메서드를 포함하고 있으므로,  
`인터페이스타입 참조변수명 = new 인터페이스타입();` 과 같이 객체를 생성할 수 없다. 

1. 인터페이스타입 참조변수를 선언하고 인터페이스를 구현한 객체를 참조시켜 
 `인터페이스타입 참조변수명 = new 구현클래스();`  형태로 구현체를 사용하거나
2. 인터페이스를 구현한 클래스타입에 구현한 객체를 참조시켜 
`구현클래스타입 참조변수명 = new 구현클래스();` 형태로 구현체를 사용할 수 있다.

- 다형성 : 하나의 타입에 여러 객체를 대입할 수 있는 성질을 뜻한다.

    [참고] [https://debugdaldal.tistory.com/171](https://debugdaldal.tistory.com/171)

---

**예제1**

![/assets/images/2021/07/16/Interface/Untitled%201.png](/assets/images/2021/07/16/Interface/Untitled%201.png)

예제2 계층구조

[https://gist.github.com/rbfl6418/e13a4626bc3b2fcd175d88579c1970b4](https://gist.github.com/rbfl6418/e13a4626bc3b2fcd175d88579c1970b4)

이처럼 구현 클래스뿐만 아니라 상위 인터페이스, 하위 인터페이스 모두 참조타입으로 사용할 수 있다. 즉, 인터페이스 참조로 다형성을 구현해 클래스들을 사용할 수 있다.

[!주의]

IPhone에는 Calculatable,internet,Phone의 모든 메서드들이 구현되어 있지만, cal은 Calculatable의 메서드인 add()만 사용가능하고 internet은 Internet의 메서드인 connectToInternet()만 사용이 가능하다. 즉, 참조 타입에 따라서 사용할 수 있는 메서드가 달라진다. 

**예제2**

[https://gist.github.com/rbfl6418/a4b87c7b4997a1ae9e9d72beb7200b71](https://gist.github.com/rbfl6418/a4b87c7b4997a1ae9e9d72beb7200b71)

<실행 결과> 

MyClass_01

MyClass_02

---

## 인터페이스의 메서드

### 인터페이스의 기본 메서드(default Method) - 자바8

- (public) `default method`란?

default 키워드를 앞에 붙이고 일반 메소드처럼 구현부{ }가 있어야 한다. 그리고 접근제어자는 항상 public이며, 생략이 가능하다. 

오버라이딩 하지 않아도 컴파일 오류가 발생하지 않는 메소드이다.

default 메소드는 오버라이딩하지 않으면 인터페이스에 구현된 것을 사용하고, 필요하다면 구현 클래스에서 오버라이딩할 수도 있다.

- 디폴트 메서드는 왜 생겼을까?

인터페이스에 새로운 메서드를 추가한다고 할 때, 
이 인터페이스를 구현한 기존의 모든 클래스들은 강제로 새로 추가된 메서드를 구현해야 한다. 

그리고 추가되는 메서드를 사용하지 않는 클래스들까지도 
아무것도 하지 않는 비어있는 실행 블록을 작성해야하는 상황이 올 수도 있다.

이런 상황에 클래스에서 인터페이스 내부의 메소드를 
선택적으로 오버라이딩 해서 사용할 수 있도록 만든 것이 default 메소드이다. 

즉, 디폴트 메서드가 추가되어도 해당 인터페이스를 구현한 모든 클래스들에 하나하나 다 구현하지 않고, 필요한 것을 선택적으로 오버라이딩할 수 있도록 해준다. 

[https://gist.github.com/rbfl6418/cae76123b3cfb0e5be8c90014efd7692](https://gist.github.com/rbfl6418/cae76123b3cfb0e5be8c90014efd7692)

### 인터페이스의 static 메서드 - 자바8

- (public) `static method`

인터페이스의 static 메서드도 클래스의 멤버에 static 키워드를 붙인 것과 같이,  
`인터페이스명.메소드()`  로 사용할 수 있다. 
즉, (new 연산자로)객체를 만들지 않고 접근할 수 있다. 
그리고 역시 접근 제어자는 항상 public이다. (생략가능)

static 메소드는 오버라이딩할 수 없기 때문에  주로 구현부 내용이 바뀌면 안되는 경우 사용한다. 

[참고]

**Q.** Can we override a static method?
**A.** **No,** we cannot override static methods because method overriding is based on dynamic binding at runtime and the static methods are bonded using static binding at compile time. So, we cannot override static methods.

[https://gist.github.com/rbfl6418/fd8ee93f8dcced623c26d1e990198fc4](https://gist.github.com/rbfl6418/fd8ee93f8dcced623c26d1e990198fc4)

결과 : static method!

### 인터페이스의 private 메서드 - 자바9

자바 9에서는인터페이스에서 private 메서드를 사용할 수 있게 되었다.

- private method
- private static method

[https://gist.github.com/rbfl6418/400384561df0eac16bdc25390fc7dcb4](https://gist.github.com/rbfl6418/400384561df0eac16bdc25390fc7dcb4)

---

- 참고

    [https://blog.naver.com/hsm622/222201314752](https://blog.naver.com/hsm622/222201314752)

    [https://www.javatpoint.com/can-we-override-static-method-in-java](https://www.javatpoint.com/can-we-override-static-method-in-java)

    [https://soongjamm.tistory.com/119?category=1062727](https://soongjamm.tistory.com/119?category=1062727)

    [https://woowacourse.github.io/javable/post/2020-10-27-polymorphism/](https://woowacourse.github.io/javable/post/2020-10-27-polymorphism/)

    [https://debugdaldal.tistory.com/171](https://debugdaldal.tistory.com/171)

    자바의 정석