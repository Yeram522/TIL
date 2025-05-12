---
icon: '9'
---

# Generics

## 1. Generic

사전적 의미 : 일반적인

자바에서 제네릭이란 <mark style="background-color:green;">데이터의 타입을 일반화한다는 의미</mark>를 가진다.\
제네릭은 클래스나 메소드에서 **사용할 내부 데이터 타입**을 <mark style="background-color:yellow;">**컴파일 시에 지정**</mark>하는 방법을 말한다.

\
컴파일 시에 미리 타입 검사를 시행하게 되면 클래스나 메소드 내부에서 사용되는 사용되는 <mark style="background-color:yellow;">**객체의 타입의 안정성**</mark><mark style="background-color:yellow;">을</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">**높일 수 있**</mark><mark style="background-color:yellow;">으며</mark>, 반환값에 대한 타입 변환 및 타입 검사에 들어가는 코드 생략이 가능해진다.

#### ✅ 제네릭 프로그래밍

데이터의 형식에 의존하지 않고 하나의 값이 여러 다른 데이터 타입들을 가질 수 있는 기술에&#x20;중점을 두어 <mark style="color:red;">재사용성을 높일 수 있는</mark> 프로그래밍 방식이다.

```java
public class GenericTest<T> {

    private T value;

    public void setValue(T value){
        this.value = value;
    }

    public T getValue(){
        return this.value;
    }
}
```

```java
GenericTest<Integer> gt1 = new GenericTest<Integer>(); // 뒤에는 type 생략 가능

gt1.setValue(Integer.valueOf(10));
System.out.println(gt1.getValue()); // 10
System.out.println(gt1.getValue() instanceof Integer); // true

GenericTest<String> gt2 = new GenericTest<>();

gt2.setValue("홍길동"); 
System.out.println(gt2.getValue()); // 홍길동
System.out.println(gt2.getValue() instanceof String); // true

GenericTest<Double> gt3 = new GenericTest<>();

gt3.setValue(0.5);
System.out.println(gt3.getValue()); // 0.5
System.out.println(gt3.getValue() instanceof Double); // true
```

## 2. extends

extends 키워드를 이용하여 특정 타입만 사용하도록 제네릭 범위를 제한할 수 있다.

{% code title="✅Rabbit을 extends 한 RabbitFarm" %}
```java
public class RabbitFarm <T extends Rabbit>{

    private T animal;

    public RabbitFarm(){}

    public RabbitFarm(T animal){
        this.animal = animal;
    }

    public void setAnimal(T animal) {
        this.animal = animal;
    }

    public T getAnimal(){
        return animal;
    }
}
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (80).png" alt=""><figcaption></figcaption></figure>

{% code title="✅ Rabbit의 상위 클래스로는 생성할 수 없지만, Rabbit을 상속받은 클래스로는 생성이 가능하다." %}
```java
//        RabbitFarm<Animal> farm1 = new RabbiFarm();

//        RabbitFarm<Mammal> farm2 = new RabbitFarm();

//        RabbitFarm<Snake> farm3 = new RabbitFarm();

RabbitFarm<Rabbit> farm4 = new RabbitFarm();
RabbitFarm<Bunny> farm5 = new RabbitFarm();
RabbitFarm<DrunkenBunny> farm6 = new RabbitFarm();

//        farm4.setAnimal(new Snake());
```
{% endcode %}

{% code title="✅ 사용 예시" %}
```java
farm4.setAnimal(new Rabbit());
((Rabbit) farm4.getAnimal()).cry();
(farm4.getAnimal()).cry();

farm5.setAnimal(new Bunny());
((Bunny) farm4.getAnimal()).cry();
(farm5.getAnimal()).cry();

farm6.setAnimal(new DrunkenBunny());
((DrunkenBunny) farm4.getAnimal()).cry();
(farm4.getAnimal()).cry();
```
{% endcode %}

### 와일드 카드

제네릭 클래스 타입의 객체를 **메소드의 매개변수로 받을 때**,&#x20;그 객체의 <mark style="color:red;">타입 변수를 제한</mark>할 수 있다.

```
<?> : 제한 없음
<? extends Type> : 와일드카드의 상한 제한
<? super Type> : 와일드카드의 하한 제한
```

```java
package com.ohgiraffers.section02.extend;

public class WildCardFarm {
    /* 매개변수로 전달받는 토끼농장을 구현할 때 사용한 타입변수에 대해 제한할 수 있다. */

    public void anyType(RabbitFarm<?> farm){
        farm.getAnimal().cry();
    }

    /* Bunny이거나 그 후손 타입으로 만들어진 토끼농장만 매개변수로 사용 가능 */
    public void extendsType(RabbitFarm<? extends Bunny> farm){
        farm.getAnimal().cry();
    }

    /* Bunny이거나 그 부모 타입으로 만들어진 토끼농장만 매개변수로 사용 가능*/
    public void superType(RabbitFarm<? super Bunny> farm){
        farm.getAnimal().cry();
    }
}
```

```java
WildCardFarm wildCardFarm = new WildCardFarm();

//    wildCardFarm.anyType(new RabbitFarm<Mammal>(new Mammal()));

wildCardFarm.anyType(new RabbitFarm<Rabbit>(new Rabbit()));
wildCardFarm.anyType(new RabbitFarm<Bunny>(new Bunny()));
wildCardFarm.anyType(new RabbitFarm<DrunkenBunny>(new DrunkenBunny()));
```
