---
description: polymorphism
icon: '9'
---

# Polymorphism

## 1️⃣ Polymorphism

### 🤔 다형성이란?

다형성이란 **하나의 인스턴스**가 <mark style="background-color:yellow;">**여러 가지 타입을 가질 수 있는 것**</mark>을 의미한다.\
그렇기 때문에 하나의 타입으로 여러 타입의 인스턴스를 처리할 수 있기도 하고,\
하나의 메소드 호출로 객체별로 각기 다른 방법으로 동작하게 할 수도 있다.\
\
다형성은 <mark style="color:purple;">객체지향 프로그래밍의 3대 특징 ( 캡슐화, 상속, 다형성 ) 중 하나</mark>이며,\
객체지향 프로그래밍의 꽃이라고 불리울 정도로 활용성이 높고 장점이 많다.

### 🩷다형성의 장점

1. 여러 타입의 객체를 하나의 타입으로 관리할 수 있기 때문에 <mark style="background-color:yellow;">**유지보수성**</mark>과 <mark style="background-color:yellow;">**생산성**</mark>이 증가됨
2. 상속을 기반으로 한 기술이기 때문에 _<mark style="color:red;">상속 관계에 있는 모든 객체는 동일한 메세지를 수신</mark>_&#xD560; 수 있다. 이런 _<mark style="color:red;">동일한 메세지를 수신 받아 처리하는 내용을 객체별로 다르게</mark>_ 할 수 있다는 장점을 가지고 있다. (다양한 기능을 사용하는데 있어서 관리해야 할 메세지 종류가 줄어들게 된다.) \
   하나의 호출로 여러 가지 동작을 수행할 수 있다는 측면에서 오버로딩을 다형성으로 보기도 한다. 다형성을 이해하기 쉬운 가장 좋은 예 이기도 하다. 하지만 이 부분은 이견이 많이 존재하기 때문에 다형성을 이해하는데 참고로만 활용하자.
3. <mark style="background-color:yellow;">**확장성**</mark>이 좋은 코드를 작성할 수 있다.
4. <mark style="background-color:yellow;">**결합도를 낮**</mark>춰서 <mark style="background-color:yellow;">**유지보수성을 증가**</mark>시킬 수 있다.



### 1. 동적 바인딩

컴파일 당시에는 해당 타입의 메소드와 연결되어 있다가&#x20;**런타임 당시** <mark style="background-color:yellow;">실제 객체가 가진</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">**오버라이딩된 메소드**</mark><mark style="background-color:yellow;">로 바인딩이 바뀌어 동작</mark>하는 것을 의미.

부모 타입으로 자식 인스턴스 주소값을 저장 했을 때

<pre class="language-java"><code class="lang-java"><strong>Animal a1 = new Rabbit(); // Rabbit은 Animal을 상속 받음
</strong>Animal a2 = new Tiger();  // Tiger은 Animal을 상속 받음

// ❌ 반대로는 안된다.
//        Rabbit r =  new Animal();
//        Tiger t = new Animal();
</code></pre>

Animal 클래스가 가진 메서드는 호출 가능 하지만,

```java
a1.cry(); // ⭕
a2.cry(); // ⭕
```

Animal 클래스보다 더 하위 클래스의 고유 기능은 동작시키지 못한다.

{% code title="❌ 잘못된 예시" %}
```java
a1.jump(); // jump는 Rabbit에서 정의된 메서드 
a2.bite();  // bite는 Tiger에서 정의된 메서드
```
{% endcode %}

### 2. 타입 형변환

#### 클래스 간의 타입 형 변환이 가능하다.

```java
((Rabbit)a1).jump();
((Tiger)a2).bite();
```

{% code title="❌ 런타임 에러!" %}
```java
((Tiger)a1).bite(); // a1은 Rabbit class로 생성했지만, Tiger로 형변환 하고 있다.
```
{% endcode %}

#### instance 연산자 사용

`instance of` 연산자를 이용해 Type을 확인할 수 있다.

```java
System.out.println("instance 확인 =====================");
System.out.println("a1이 Tiger 타입인지 확인 : " + (a1 instanceof Tiger));
System.out.println("a1이 Rabit 타입인지 확인 : " + (a1 instanceof Rabbit));

System.out.println("a1이 Animal 타입인지 확인 : " + (a1 instanceof Animal));
System.out.println("a1이 Object 타입인지 확인 : " + (a1 instanceof Object));
```

#### 업캐스팅과 다운캐스팅

클래스 형변환은 up-casting과 down-casting으로 구분할 수 있다.

up-casting : 상위 타입으로 형변환\
down-casting : 하위 타입으로 형변환

{% code title="✅ 작성여부에 따른 형변환" %}
```java
// 작성 여부에 따라 명시적과 묵시적 두 가지로 구분된다.
Animal animal1 = (Animal) new Rabbit(); // up-casting 명시적 형변환
Animal animal2 = new Rabbit(); // up-casting 묵시적 형변환
        
Rabbit rabbit1 = (Rabbit) animal1; // down-casting 명시적 형변환
//        Rabbit rabbit2 = animal1; // down-casting 묵시적 형변환 안됨
```
{% endcode %}

##
