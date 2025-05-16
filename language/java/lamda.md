---
icon: clock
---

# Lamda

## 1️⃣ 람다식(lamda)

메소드를 하나의 식(expression)으로 표현한것이다.\
메소드를 람다식으로 표현하면 메소드 이름이 없는 익명함수라고 할 수 있다.\
수학 : f(x,y) = x \* y\
→ 람다식 : (x,y) -> x + y

### 장점 < 단순함 >

람다식을 활용하면 컬렉션에 연계하여 데이터를 쉽게 조작할 수 있으며, 불필요한 반복되는 코드도 제거 할 수 있다.\
💡 최근에는 적극적으로 활용하는 추세이다.

### 람다 표현식

#### 매개변수가 없는 경우

`() ⇒ {...}`

#### 매개변수가 있는 경우

`( 매개변수, ... ) -> { ... }`

람다식에서 매개변수의 타입은 추론이 가능하기 때문에 명시적으로 작성하지 않아도 된다.\
또한, 매개변수가 한 개만 존재하는 경우 ()를 생략할 수 있으며,\
실행문이 한 줄인 경우 {}는 생략 가능하다.



### 인터페이스에 정의된 추상메소드 활용법

#### 1. 인터페이스에 상속받은 클래스를 정의하여 기능을 완성 후 사용.

```java
public class CalculatorImpl implements Calculator {

    @Override
    public int sumTwoNumber(int a, int b) {
        return 0;
    }
}
```

#### 2. 익명클래스를 활용하여 메소드 재정의 후 사용하는 방법

```java
Calculator c2 = new Calculator(){
    @Override
    public int sumTwoNumber(int a, int b){
        return a+ b;
    }
};
```

#### 3. 람다식을 활용하는 방법

```java
Calculator c3 = (x,y) -> x+y;
```

### 람다식 활용을 위한 내부 인터페이스 관리 기법

```java
public interface OuterCalculator {

    @FunctionalInterface
    public interface Sum{
        int sumTwoNumber(int a, int b);
    }

    @FunctionalInterface
    public interface Minus{
        int minusTwoNumber(int a, int b);
    }

    @FunctionalInterface
    public interface Multiple{
        int multiplyTwoNumber(int a, int b);
    }

    @FunctionalInterface
    public interface Divide{
        int divideTwoNumber(int a, int b);
    }
}
```

#### @FunctionalInterface

인터페이스 내부에 하나의 추상메소드가 선언된 인터페이스만 람다식의 타깃이 될 수 있고 이러한 인터페이스를 함수적 인터페이스(functional interface)라고 한다.

해당 조건을 만족하는지 컴파일 시점에 체크해주는 기능이 @FunctionalInterface 어노테이션이다.

## 2️⃣ Functional Interface

