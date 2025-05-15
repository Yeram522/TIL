---
icon: clock-eleven
---

# Exception

컴퓨터 프로그램이 동작하는 도중에 예상치 못한 사태가 발생하여&#x20;실행중인 프로그램이 영향을 받는 것을 오류(Error)와 예외(Exception) 두 가지로 구분할 수 있다.

#### 오류(Error)

시스템 상에서 프로그램에 심각한 문제를 발생하여 실행중인 프로그램이 종료되는 것을 말한다.

#### 예외(Exception)

오류와 마찬가지로 실행중인 프로그램을 비정상적으로 종료시키지만&#x20;발생할 수 있는 상황을 미리 예측하고 처리할 수 있는 미약한 오류를 말한다.\
개발자는 이러한 예외에 대해 예외처리를 통해 예외 상황을 적절히 처리하여 코드의 흐름을 컨트롤 할 수 있다.

## Exception

```java
throw new 예외클래스명();
```

{% code title="✅ Exception을 클래스 내에서 throw하면서 상위 클래스에도 책임을 위임하기 때문에 메소드 헤드에 throws 구문 추가" %}
```java
public class ExceptionTest {

    public void checkEnoughMoney(int price, int money) throws Exception {
        System.out.println("가지고 있는 돈은 " + money + "원 입니다.");

        if(money >= price){
            System.out.println("상품을 구입하기 위한 금액이 충분합니다.");
        }else{
            /* 강제로 예외를 발생
            * 예외 발생 시키고 메소드 헤드에 throws 구문 추가한다.
            * 예외를 발생시킨 쪽에서는 thorws로 예외에 대한 책임을 위임해서
            * 해당 예외에 대한 처리를 강제화한다.
            * */
            throw new Exception();
        }

        System.out.println("즐거운 쇼핑 되세요~");
    }
    
}
```
{% endcode %}

```java
public static void main(String[] args) throws Exception {
    ExceptionTest et = new ExceptionTest();
    et.checkEnoughMoney(10000, 50000); // checkEnoughMoney에서 예외를 발생시키고 있기 때문에 상위 메서드에서도 exception을 받을 수 있게 추가해줘야한다. -> throws 위임!
    et.checkEnoughMoney(50000, 10000);
}
```

## Unexception

{% code title="✅ Exception을 상속받은 클래스의 상속 예시" %}
```java
public class NegativeException extends Exception{

    public NegativeException(String message){
        super(message);
    }


public class MoneyNegativeException extends NegativeException{

    public MoneyNegativeException(String message) {
        super(message);
    }
    
}
```
{% endcode %}

{% code title="✅ 사용자 정의 exception 사용 예시" %}
```java
public class Application1 {

    public static void main(String[] args) {

        /* comment. 사용자 정의와 에외클래스 정의 후 발생한 사용자 정의의 예외를 처리할 수 있다. */

        ExceptionTest et = new ExceptionTest();


        try {
//            et.checkEnoughMoney(50000, 30000);
            et.checkEnoughMoney(-50000, 50000);
        } catch (Exception e) {
            e.printStackTrace();
        }


    }
}
```
{% endcode %}

Exception을 throw하는 메소드를 호출하는 경우에는, 상위 메서드에 Exception을 위임하거나 try-catch 블럭을 통해 해결할 수 있다.

#### multi-catch

multi-catch 블럭으로 동일한 레벨의 다른 타입의 예외를 하나의 catch 블럭으로 처리할 수 있다.

```java
ExceptionTest et = new ExceptionTest();

try {
    et.checkEnoughMoney(20000,30000);
} catch (NotEnoughMoneyException e) {
    // 예외 클래스명, 예외발생 위치, 예외 메세지 등을 stack 호출 역순으로
    // 빨간색 글씨를 이용해서 로그 형태로 출력해주는 기능
    e.printStackTrace();
}catch (PriceNegativeException |MoneyNegativeException e){

    // 발생한 예외 클래스 이름
    System.out.println(e.getClass());
    System.out.println(e.getMessage());
}finally {
    /*예외 발생 여부와 관계 없이 실행할 내용*/
    System.out.println("finally 블럭의 내용이 동작함");
}

System.out.println("프로그램을 종료합니다.");
```

## Override

```java
package com.ohgiraffers.section03.override;

import java.io.IOException;

public class SuperClass {
    public void method() throws IOException{

    }
}
```

`public class SubClass extends SuperClass`  클래스에서 아래의 메서드를 오버라이딩 했을 때의 여러가지 상황을 알아보도록 한다.

{% code title="✅ 예외 없이 오버라이딩 가능" %}
```java
@Override
public void method(){} 
```
{% endcode %}

하위 메서드는 상위 메서드의 예외 반환에 영향 받지 않는다.

{% code title="✅같은 예외를 던져주는 구문으로 오버라이딩 해야한다." %}
```java
@Override
public void method() throws IOException{}
```
{% endcode %}

{% code title="❌ 부모의 예외처리 클래스보다 상위의 예외로는 후손클래스에서 오버라이딩 불가능" %}
```java
@Override
public void method() throws Exception{}
```
{% endcode %}

{% code title="✅부모의 예외처리 클래스보다 더 하위에 있는 예외( 즉, 더 구체적인 예외상황)인 경우 오버라이딩 가능" %}
```java
@Override
public void method() throws FileNotFoundException{}
```
{% endcode %}
