---
icon: clock-three
---

# Enum

## 1️⃣ IntEnum

정수 열거 패턴이라고도 한다.

1. 정수값만을 저장하고 있는 필드일 뿐이다.

```java
public interface Subjects {

    public static final int JAVA = 0;
    public static final int ORACLE = 1;
    public static final int JDBC = 2;

    public static final int HTML = 0;
    public static final int CSS = 1;
    public static final int JAVASCRIPT = 2;

}
```

2.  이름 출동 방지를 위해 접두어를 써서 구분해야 한다.



    {% code title="❌ 옳지 않은 문법" %}
    ```java
    BACKEND_JAVASCRIPT = 0;
    FRONTEND_JAVASCRIPT = 0;
    ```
    {% endcode %}
3.  문자열로 출력하기 까다롭다.

    ```java
    int num = 0;
    String subjectText = "";

    switch (num){
            case Subjects.JAVA : subjectText = "JAVA" ; break ;
            case Subjects.ORACLE: subjectText = "ORACLE" ; break ;
            case Subjects.JDBC : subjectText = "JDBC" ; break ;
    };

    System.out.println("subjectText = " + subjectText);
    ```
4. 같은 그룹에 속한 상수들을 순회 할 수 없다. (전체 상수의 갯수 확인 불가능 )
5. 타입 안전을 보장 할 수 없다.

```java
printSubject(Subjects.ORACLE);
printSubject(2); // 대충 아무숫자나 넣어도 에러가 발생하지 않음
```

```java
public static void printSubject(int subjectNumber){
    String subject = "";

    switch (subjectNumber){
        case Subjects.JAVA : subject = "JAVA" ; break ;
        case Subjects.ORACLE: subject = "ORACLE" ; break ;
        case Subjects.JDBC : subject = "JDBC" ; break ;
    };

    System.out.println(subject);
}
```

## 2️⃣ EnumType

```java
public enum Subjects {

    JAVA, // 0
    ORACLE, // 1
    JDBC, // 2
    HTML, // 3
    CSS, // 4
    JAVASCRIPT // 5

}
```

1. 열거 타입으로 선언된 인스턴스는 <mark style="background-color:yellow;">**싱글톤으로 관리**</mark>되며 인스턴스가 한 개 임을 보장한다.

```java
Subjects subjects1 = Subjects.JAVA;
Subjects subjects2 = Subjects.HTML;

if(subjects1 == subjects2){
    System.out.println("두 과목은 같은 과목입니다. ");
}else{
    System.out.println("두 과목은 다른 과목입니다. ");
}
```

{% code title="✅단일 인스턴스임을 보장하기에 == 비교가 가능하다." %}
```java
System.out.println(subjects1 == subjects2.JAVA);
```
{% endcode %}

2. 이름 충돌 방지를 위해 접두사를 쓰지 않아도 Enum 타입별로 네임스페이스를 가진다.

```java
public enum Backend { JAVA, ORACLE, JDBC, JAVASCRIPT }
public enum Frontent { HTML, CSS, JAVASCRIPT }
```

3.  toString()을 이용하여 문자열로 변경하기 쉽다.



    ```java
    System.out.println(Subjects.JAVA.toString());
    ```
4.  values()를 이용하여 상수값 배열을 반환하고 이를 이용해 연속처리 할 수 있다.



    ```java
    Subjects[] subjects = Subjects.values();
    for(Subjects s : subjects){
        System.out.println(s);
    }
    ```
5.  타입 안정성이 보장한다.



    ```java
     printSubject(Subjects.HTML);
    //printSubject(2); // Enumtype은 인스턴스이기 때문에 정수를 사용하는 경우 타입불일치로 컴파일 에러 발생

     public static void printSubject(Subjects subject){
            System.out.println(subject.toString());
    }
    ```

## 3️⃣Enum 문법

### 1. Enum은 기본 생성자를 가질 수 있다.

<mark style="background-color:green;">**default**</mark>와 <mark style="background-color:green;">**private**</mark> 접근 제한 사용 가능하지만 <mark style="color:red;">외부에서 호출을 불가능</mark><mark style="background-color:yellow;">( 묵시적으로 private )</mark>\
enum 타입은 <mark style="color:red;background-color:yellow;">고정된 상수들의 집합</mark>으로,\
런타임이 아닌 **컴파일 시에 모든 값이 결정**되어 있어야한다.\
따라서 다른 클래스에서 enum 타입에 접근해 동적으로 생성자를 이용해 어떤 값을 전달해 줄 수 없기 때문이다.\
&#xNAN;_<mark style="color:orange;">단, 생성자를 가질 시 열거형 상수 선언 마지막에 세미콜론을 붙여야 한다.</mark>_

```java
public enum UserRole {

    GUEST,
    CONSUMER,
    PRODUCER,
    ADMIN;

    UserRole(){}

    public String getNameToLowerCase(){
        return this.name().toLowerCase();
    }
}
```

### 2. Enum의 매개변수 있는 생성자

```java
public enum UserRole2 {

    GUEST("게스트"),
    CONSUMER("구매자"),
    PRODUCER("판매자"),
    ADMIN("관리자");

    private final String description;

    /* 이러한 경우 매개변수 있는 생성자가 반드시 필요하다.
    *  enum 상수의 괄호 안에 넣은 값이 해당 생성자쪽으로 전달되며 Enum 인스턴스가 생성되며,
    *  생성된 인스턴스는 싱글톤 객체이다.
    * */

    UserRole2(String description){
        this.description = description;
        System.out.println("descrption : " + description);
    }

    public String getDescription(){
        return description;
    }
}
```
