---
description: polymorphism
icon: '2'
---

# Polymorphism

## 1️⃣ 다형성

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

## 2️⃣ 추상 클래스와 추상 메소드

### 추상 클래스

추상 메소드를 0개 이상 포함하는 클래스를 추상 클래스라고 한다.\
1\. 추상클래스는 **클래스 선언부**에 <mark style="background-color:yellow;">**abstract**</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">키워드</mark>를 명시해야 한다.\
2\. <mark style="color:red;">추상클래스로는 인스턴스를 생성할 수 없다.</mark>\
3\. 추상클래스를 사용하려면 <mark style="background-color:yellow;">추상클래스를 상속받은 하위 클래스를 이용해서 인스턴스를 생성</mark>해야한다.&#x20;이 때, 추상 클래스는 상위 타입으로 사용될 수 있으며, **다형성을 이용**할 수 있다.

추상 클래스에 작성한 추상메소드는 <mark style="background-color:yellow;">반드시 후손이</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">**오버라이딩**</mark><mark style="background-color:yellow;">해서 작성</mark>해야 하며,&#x20;후손 클래스들의 메소드들의 <mark style="color:purple;">공통 인터페이스로의 역할</mark>을 수행할 수 있다.\
추상 클래스에 작성한 메소드를 호출하게 되면 실제 후손 타입의 인스턴스가 가지는 메소드는&#x20;다형성이 적용되어 _<mark style="color:orange;">동적바인딩에 의한 다양한 응답</mark>_&#xC744; 할 수 있다.

### 추상 메소드

메소드의 선언부만 있고 구현부가 없는 메소드를 추상메소드라고 한다.\
추상메소드의 경우 반드시 <mark style="background-color:yellow;">**abstract**</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">키워드</mark>를 메소드 헤드에 작성해야 한다.\
`ex) public abstract void method()`

```
// ❌ 추상 클래스는 인스턴스 생성 불가능!
//        Product product = new Product();

// 추상 클래스를 상속받은 하위 클래스는 인스턴스 생성 가능~!
SmartPhone smartPhone = new SmartPhone();

System.out.println(smartPhone instanceof SmartPhone);
System.out.println(smartPhone instanceof Product);

Product product = new SmartPhone();

product.abstMethod();

product.nonStaticMethod();

product.staticMethod();
```

### 추상 클래스를 쓰는 이유

추상클래스의 추상메소드는 <mark style="color:red;background-color:yellow;">오버라이딩에 대한 강제성이 부여</mark>된다.\
따라서 여러 클래스들을 그룹화 하여&#x20;필수 기능을 정의하여 강제성을 부여해 개발 시 <mark style="color:purple;">일관된 인터페이스를 제공</mark>할 수 있다.\
하지만 다른 클래스를 상속 받고 있는 클래스를 작성할 시에는 추상클래스를 추가로 상속받을 수 없다.\
그래서 추상클래스보다 더 강제성이 강한 인터페이스(interface)라는 매커니즘을 제공하고 있다.

## 3️⃣ 인터페이스

### 인터페이스의 사용 목적

1. 추상클래스와 비슷하게 필요한 기능을 공통화 해서 강제성을 부여할 목적으로 사용한다.
2. 자바의 단일상속의 단점을 극복할 수 있다.( 다중 상속 )

{% code title="❌ 인스턴스 생성 불가능!" %}
```java
InterProduct interProduct = new InterProduct();
```
{% endcode %}

```java
InterProduct interProduct = new Product();

interProduct.nonStaticMethod();
interProduct.abstMethod();

interProduct.defaultMethod();

/* 인터페이스명.메소드명() ; */
InterProduct.staticMethod();

System.out.println(InterProduct.MAX_NUM);
System.out.println(InterProduct.MIN_NUM);
```

### 인터페이스&#x20;

#### 1. 인터페이스는 <mark style="color:red;">상수 필드만 작성이 가능하</mark>다.

public static final 제어자 조합 상수 필드라고 부른다.&#x20;반드시 <mark style="background-color:yellow;">**선언과 동시에 초기**</mark>화 해줘야 한다.

```java
public static final int MAX_NUM = 100;
```

{% code title="✅묵시적 public static final" %}
```java
/* 모든 필드는 무시적으로 public static final 이다.*/
int MIN_NUM = 10;
```
{% endcode %}

2.  인터페이스는 <mark style="color:red;">생성자를 가질 수 없다</mark>.



    <pre class="language-java" data-title="❌ 불가능한 예시"><code class="lang-java"><strong>public InterProduct(){};
    </strong></code></pre>
3.  인터페이스는 <mark style="color:red;">구현부가 있는 non-static 메소드를 가질 수 없다.</mark>



    {% code title="⭕ 가능한 예시" %}
    ```java
    public abstract void nonStaticMethod(); // 구현부가 없는 추상화 함수이므로 가능능
    ```
    {% endcode %}



    {% code title="❌ 불가능한 예시" %}
    ```java
    public void nonStaticMethod(){}
    ```
    {% endcode %}
4.  인터페이스 안에 작성한 메소드는 <mark style="background-color:yellow;">묵시적으로</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">**public abstract**</mark><mark style="background-color:yellow;">의 의미</mark>를 가진다.(다른 접근제한자 사용 불가)\
    따라서 인터페이스의 메소드를 오버라이딩 해야하는 경우    &#x20;<mark style="color:red;">반드시 접근제한자를 public으로 해야 오버라이딩이 가능</mark>하다.

    ```java
    void abstMethod();
    ```
5.  <mark style="background-color:yellow;">**static 메소드**</mark>는 작성이 가능하다.



    ```javascript
    public static void staticMethod(){
        System.out.println("InterProduct 클래스의 staticMethod 호출됨...");
    }
    ```
6.  <mark style="background-color:yellow;">**default 키워드**</mark>를 사용하면 n<mark style="color:red;">on-static 메소드도 작성 가능</mark>하다.



    ```java
    public default void defaultMethod(){

    }
    ```

### 인터페이스 구현부

클래스에서 인터페이스를 상속 받을 때에는 <mark style="background-color:yellow;">**implements 키워드**</mark>를 사용한다.\
인터페이스는 <mark style="color:red;">여러 개를 상속  받을 수 있으며</mark>,\
extends로 다른 클래스를 상속 받는 경우에도 그것과 별개로 인터페이스도 추가 상속이 가능해진다.\
단, extends 키워드를 앞에 작성하고 implements를 뒤에 작성한다.

```java
@Override
public void nonStaticMethod() {

    System.out.println("InterProduct의 nonStaticMethod 오버라이딩한 메소드 호출됨...");

}

@Override
public void abstMethod() {

    System.out.println("InterProduct의 abstMethod 오버라이딩한 메소드 호출됨...");

}
```

{% code title="❌ static 오버라이딩 불가" %}
```java
@Override
public static void staticMethod(){}
```
{% endcode %}

{% code title="❌ default는 인터페이스에서만 가능" %}
```java
@Override
public default void defaultMethod(){}
```
{% endcode %}

{% code title="⭕ default 없이 오버라이딩 가능" %}
```java
@Override
public void defaultMethod(){

    System.out.println("Product 클래스의 defaultMethod 호출됨...");
}
```
{% endcode %}
