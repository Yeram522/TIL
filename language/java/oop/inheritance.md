---
icon: '1'
---

# Inheritance

## 1️⃣ extends

### 🤔 상속이란?

상속은 현실 세계의 상속과 비슷한 개념이다.\
<mark style="background-color:yellow;">부모가 가지고 있는 재산(자바에서는 클래스가 가지는 멤버)을</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">**자식이 물려받는**</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">의미</mark>이다.\
클래스 또한 부모클래스와 자식클래스로 역할을 나누어서 부모가 가지는 멤버를 <mark style="background-color:yellow;">자식이 물려받아</mark> <mark style="background-color:yellow;"></mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">**자기의 멤버인 것 처럼**</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">사용</mark>할 수 있도록 만든 기술이다.

### 💡확장(extends)의 개념을 가진다.

하지만 단순 물려받는 개념보다 조금 더 나아간다면\
자바에서의 상속은 **부모클래스의 확장(extends)**&#xC758; 개념을 가진다.\
물려받아서 자신의 것 처럼 사용하는 것 뿐 아니라 _<mark style="color:purple;">추가적인 멤버도 작성이 가능</mark>_&#xD558;다.\
특히 <mark style="color:green;background-color:yellow;">**메소드 재정의(overriding)**</mark>라는 기술을 이용해서 부모가 가진 메소드를 재정의하는 것도 가능하다.

{% hint style="success" %}
**메소드 재정의(overriding)이란** \
<mark style="color:green;">부모가 가지는 메소드 선언부를 그대로 사용</mark>하면서&#x20;자식클래스가 정의한 메소드대로 동작하도록 _<mark style="color:red;">구현 몸체 부분을 새롭게 다시 작성</mark>_&#xD558;는 기술이다.\
<mark style="background-color:yellow;">메소드 재정의를 하면 메소드를</mark> <mark style="color:red;background-color:yellow;">**호출할 시 재정의한 메소드가 우선적으로 동작**</mark><mark style="background-color:yellow;">하게 된다.</mark>
{% endhint %}

### ✅상속의 이점

1.  새로운 클래스를 작성할 시 **기존에 작성한 클래스를 재사용**할 수 있다.

    1-1.   재사용 시 **생산성**을 크게 향상시킬 수 있다. (새롭게 작성하는거보다 빠르다)    \
    1-2.  공통적으로 사용하는 코드가 부모클래스에 존재하면 수정사항이 생길 시 부**모 클래스만 수정해도    &#x20;전체적으로 적용**된다. _<mark style="color:orange;">(유지보수성 증가)</mark>_
2. 클래스간의 **계층 관계가** 형성되며 **다형성**의 문법적인 토대가 된다.

### ✅ 상속의 단점

1. 부모클래스의 기능을 추가/변경할 시 자식클래스가 정상적으로 동작하는지에 대한 예측이 힘들다.   **상속 구조가 복잡해 질 수록 그 영향에 대한 예측이 힘들**며 이런 단점이 유지보수성 증가한다는 장점과는   \
   반대로 유지보수에 악영향을 미친다.
2. 또한 부모클래스의 변경 또한 쉽지 않다. 자식클래스에서 중요하게 사용하는 기능인 경우   &#x20;부모클래스를 변경할 시 자식 클래스에 모두 영향을 줄 수 있다.   &#x20;_역시 유지보수에 악영향을 미친다._
3. 부모클래스에서는 의미있었던 기능이 **자식클래스에서는 무의미**할 수 있다. _(불필요한 기능이 추가됨)_



### 🤔장점과 단점을 고려했을 때...

상속은 재사용이라는 장점만 바라보게 되면 오용의 가능성이 있기 때문에 유지보수에 좋지 않는 코드를 작성할 확률이 높다.\
&#xNAN;_<mark style="color:red;background-color:yellow;">상속은 IS-A 관계로 구분되는 경우에만 사용해야 한다.</mark>_

### 객체 지향 설계 관점에서 바라보는 상속

모든 객체는 자신이 수신한 메세지에 대해 응답을 해야하는 책임을 가지며, 그 **책임의 규모는 적절**해야한다.&#x20;적절한 책임을 가진 객체들이 서로 메시지 수신과 응답을 통해 프로그램이 동작하는 것이 객체지향 프로그램이다.\
적절한 책임을 수행하는 객체 또한 그 객체만 수행할 수 있는 기능이라기 보다 역할의 관점으로 바라봐야 한다.\
역할이란 동일한 동작을 수행하는 것을 정의한 것이며, 대체 가능성을 의미한다.\
<mark style="background-color:yellow;">부모클래스를 추상화 하는 경우에는 역할의 관점으로 바라봐야 한다.</mark>\
그래야 자식클래스로 생성한 객체들이 서로 역할을 수행해가며 유연한 코드를 작성할 수 있게 된다.\
&#xNAN;_<mark style="color:purple;">동일한 역할을 가지는 모든 객체는 동일한 메세지를 수신하기만 하지만,&#x20;객체별로 그 메세지에 응답하는 방식은 서로 다를 수 있다. (다형성)</mark>_

{% code title="👩‍🦳 부모 클래스" %}
```java
package com.ohgiraffers.section01.extend;

public class Car {

    private boolean runningStatus;

    public Car(){
        System.out.println("Car 클래스의 기본 생성자 호출됨...");
    }

    public void run(){

        runningStatus = true;
        System.out.println("자동차가 달립니다.");
    }

    public void soundHorn(){

        if(isRunning()){
            System.out.println("빵! 빵!");
        }else{
            System.out.println("주행중이 아닌 상태에넌 경적을 울릴 수 없습니다.");
        }
    }

    public boolean isRunning(){

        return runningStatus;
    }

    public void stop(){

        runningStatus = false;
        System.out.println("자동차가 멈춥니다.");
    }
}
스
```
{% endcode %}

{% code title="👼 자식 클래스" %}
```java
package com.ohgiraffers.section01.extend;

public class FireCar extends Car{

    public FireCar(){

        /* 모든 생성자에는 맨 첫 줄에 super()를 컴파일러가 자동 추가한다.
        *  부모의 기본 생성자를 호출하는 구문이다.
        *  해당 생성자가 호출 될 시 가장 먼저 Car 클래스 호출 내용이 출력될 것이다.
        *  명시적, 묵시적 전부 사용 가능하다.
        * */
        super();

        System.out.println("FireCar 클래스의 기본 생성자 호출됨..");
    }

    /* @Override 어노테이션
    *  오버라이딩 성립 요건을 체크하여 성립되지 않는 경우 컴파일에러를 발생시킨다.
    *  오버라이딩 하는 메소드는 기본적으로 부모 메소드 선언 내용을 그대로 작성해야 한다.
    * */

    @Override
    public void soundHorn(){

        if(isRunning()){
            System.out.println("빠아아아아아앙!!!!!!!!!!!!!!!!!!!");
        }else {
            System.out.println("소방차가 앞으로 갈 수 없습니다. 비키세요~~~");
        }
    }

    public void sprayWater(){
        System.out.println("불난 곳을 발견했습니다. 물을 뿌립니다 ========================>>");

    }

}스
```
{% endcode %}

## 2️⃣ super 키워드

### super

자식클래스를 이용해서 객체를 생성할 때 부모생성자를 호출하여 부모클래스의 인스턴스도 함께 생성하게 된다.\
이 때 <mark style="color:red;background-color:yellow;">생성한 부모의 인스턴스 주소를 보관하는 레퍼런스 변수</mark>로&#x20;자식 클래스 내의 모든 생성자와 메소드 내에서 **선언하지 않고도 사용할 수 있는** 레퍼런스 변수이다.

```java
@Override
public String getInformation(){
    return super.getInformation()
            + "Computer ["
            + "cpu=" + this.cpu
            + ", hdd=" + this.hdd
            + ", ram=" + this.ram
            + ", operationSystem" + this.operationSystem
            + "]";
}
```

### super()

**부모 생성자를 호출하는 구문**으로 <mark style="color:red;">인자와 매개변수의 타입, 순서, 갯수가 일치하는</mark>\ <mark style="color:red;">부모의 생성자를 호출</mark>하게 된다.\
this()가 해당 클래스 내의 다른 생성자를 호출하는 구문이라면,&#x20;super()는 <mark style="color:red;background-color:yellow;">부모클래스가 가지는 private 생성자를 제외한 나머지 생성자를&#x20;호출할 수 있도록 한 구문</mark>이다.

```java
/* 부모의 필드도 모두 초기화하는 생성자 */
public Computer(String code, String brand, String name,int price, Date manufacturingDate, String cpu, int hdd, int ram, String operationSystem) {

    /* 부모가 가진 필드를 초기화 할 값 전달 */
    super(code, brand, name,price, manufacturingDate);

    /* 나머지 필드를 초기화 */
    this.cpu = cpu;
    this.hdd = hdd;
    this.ram = ram;
    this.operationSystem = operationSystem;

    System.out.println("Computer 클래스의 부모 필드를 초기화하는 생성자 호출함..");
}
```

## 3️⃣ Overriding

### 오버라이딩 성립 요건

1.  메소드의 이름이 동일해야 한다.

    {% code title="❌메소드 이름 변경 에러" %}
    ```java
    @Override
    public void method2(int num){}
    ```
    {% endcode %}


2.  메소드의 리턴 타입이 동일해야 한다.

    {% code title="❌ 메소드 리턴타입 변경 에러" %}
    ```
    @Override
    public int method(int num){}
    ```
    {% endcode %}


3.  매개변수의 타입, 갯수, 순서가 동일해야 한다.

    ```java
    @Override
    public void method(String num){}
    ```


4.  private 메소드는 접근이 불가능하기 때문에 오버라이딩이 불가능하다.

    ```java
    @Override
    public void method(int num){}
    ```


5.  final 키워드가 사용된 메소드는 오버라이딩이 불가능하다.

    ```java
    @Override
    private void privateMethod(){}
    ```


6.  접근제한자는 부모 메소드와 같거나 더 넓은 범위여야 한다.

    ```java
    @Override
    public final void finalMethod(){}
    ```


7.  예외처리는 같은 예외이거나 더 구체적(하위)인 예외를 처리해야 한다.



    ```java
    @Override
    public void protectedMethod(){} // 더 넓은 범위로도 가능
    ```



    ```java
    @Override
    protected void protectedMethod(){} // 같은 범위로 가능
    ```



    <pre class="language-java"><code class="lang-java"><strong>@Override
    </strong>void protectedMethod(){} 
    // 더 좁은 범위로는 불가능
    </code></pre>

```
public 접근 제한자: 단어 뜻 그대로 외부 클래스가 자유롭게 사용할 수 있도록 합니다.
protected 접근 제한자: 같은 패키지 또는 자식 클래스에서 사용할 수 있도록 합니다.
private 접근 제한자: 단어 뜻 그대로 개인적인 것이라 외부에서 사용될 수 없도록 합니다.
default 접근 제한자 : 같은 패키지에 소속된 클래스에서만 사용할 수 있도록 합니다.
```

<figure><img src="../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
