---
icon: '3'
---

# Method & API

## 1️⃣ 메소드

### 메소드란?

메소드(method)는 어떤 특정 작업을 수행하기 위한 명령문의 집합이라고 할 수 있다.

### 메소드 호출 방법

클래스명 사용할 이름 = new 클래스명(); _<mark style="color:green;">// 객체 생성</mark>_\
사용할이름.메소드명(); _<mark style="color:green;">// 메소드 호출</mark>_

```java
Application1 app1 = new Application1();
app1.methodA();
```

#### 전달인자(argument)와 매개변수(parameter)를 이용한 메소드 호출

```
변수의 종류
*  1. 지역변수
*  2. 매개변수
*  3. 전역변수(필드)
*  4. 클래스(static)변수
```

{% hint style="success" %}
지역변수는 선언한 메소드 블럭 내부에서만 사용이 가능하다. 이것을 지역변수의 스코프라고 한다.\
다른 메소드간 서로 공유해야 하는 값이 존재하는 경우 메소드 호출 시 사용하는 괄호를 이용해서 값을 전달 할 수 있다.\
이 때 전달하는 값을 전달인자라고 부르고,\
메소드 선언부 괄호 안에 전달 인자를 받기 위해 선언하는 변수를 매개변수라고 부른다.
{% endhint %}

#### return

모든 메소드 내부에는 return; 이 존재한다.\
void 메소드의 경우 return;을 명시적으로 작성하지 않아도 마지막줄에 컴파일러가 자동으로 추가를 해준다.\
return은 현재 메소드를 강제 종료하고 호출한 구문으로 다시 돌아가는 명령어이다.

### static 메소드

static 메소드를 호출하는 방법\
클래스명.메소드명();

```java
Application8.sumTwoNumbers(10,20);// 클래스 생성 없이, 바로 클래스. 으로 메소드를 접근할 수 있다.

sumTwoNumbers(20,30);// 동일한 클래스일 때 클래스명 생략 가능
```

### 다른 클래스에서 작성한 메소드 호출하기

#### 1. non-static 메소드

```java
Calculator calc = new Calculator();
int min = calc.minNumberOf(first, second);

System.out.println("두 수 중 최소값은 : " + min);
```

#### 2. static 메소드

다른 클래스에 작성한 static 메소드의 경우 호출할 때 클래스 명을&#x20;반드시 기술해야 한다.

```java
//        int max = maxNumberOf(first,second); // 권장하지 않음
int max = Calculator.maxNumberOf(first,second);
System.out.println("두 수 중 최대값은 : " + max);
```

{% hint style="danger" %}
주의사항\
static 메소드도 non-static 메소드처럼 호출은 가능하다.\
하지만 권장하지 않는다.\
이미 메모리에 로딩되어 있는 static 메소드는 여러 객체가 공유하게 된다.\
그 때 객체로 접근하게 되면 인스턴스가 가진 값으로 공유된 값에 예상치 못하는 동작을\
유발할 수 있기 때문에 사용을 제한해달라는 경고이다.\
시스템이 복잡해질 수록 객체의 상태를 추적하기 어려워 유지보수에 악영향을 준다.
{% endhint %}

## 2️⃣ math

Math 클래스에서 제공하는 static 메소드를 호출할 수 있다.

{% hint style="info" %}
API란?\
Application Programming Interface는 응용프로그램에서 사용할 수 있도록\
운영체제가 프로그래밍 언어가 제공하는 기능을 제어할 수 있도록 만든 인터페이스를 뜻한다.\
쉽게 말해 우리가 구현할 수 없거나 구현하기 번거로운 기능들을 JDK를 설치하면 사용할 수 있도록 제공해놓은&#x20;소스코드(클래스나 인터페이스)들을 의미한다.\
더 쉽게 말해 누가 작성해놓은 소스코드이니 가져다 쓰는 방법을 본다는 말이다.\
모든 코드를 우리가 다 외울 수 없으니 API 문서를 별도로 제공해주고 있다.
{% endhint %}

#### java.lang.Math

Math 클래스는 수학에서 자주 사용하는 상수들과 함수들을 미리 구현해 놓은 클래스이다.\
모든 메소드가 static 메소드로 작성되어 있다.

```java
/* 1. 절대값 출력 *
/* 1-1. 클래스의 full-name을 다 적은 경우 */
System.out.println("-7의 절대값 : " + (java.lang.Math.abs(-7)));

/* 1-2. import를 해서 사용 */
System.out.println(Math.abs(-1.25));

/* 2. 최대값, 최소값 출력 */
System.out.println(Math.min(10,20));
System.out.println(Math.max(20,30));

System.out.println(Math.PI);

/* 3. 난수 출력 */
System.out.println(Math.random());
```

#### 사용자 지정 범위 난수&#x20;

{% hint style="info" %}
난수의 활용

Math.random()을 이용해 발생한 난수는 0부터 1전까지의 실수 범위의 난수값을 반환한다.\
필요에 따라 정수 형태의 값을 원하는 범위 만큼 발생시켜야 하는 경우들이 존재한다.
{% endhint %}

{% hint style="success" %}
원하는 범위의 난수를 구하는 공식\
`(int) (Math.random * 구하려는 난수의 갯수) + 구하려는 난수의 최소값`
{% endhint %}

```java
/* 1. 0 ~ 9까지의 난수 발생 */
int random1  = (int) (Math.random() * 10);
System.out.println(random1);

/* 2. 1 ~ 10까지의 난수 발생*/
int random2  = (int) (Math.random() * 10) + 1;
System.out.println(random2);
/* 3. 10 ~ 15까지의 난수 발생*/
int random3  = (int) (Math.random() * 6) + 10;
System.out.println(random3);
/* 4. -128 ~ 127까지의 난수 발생*/
int random4  = (int) (Math.random() * 256) - 128;
System.out.println(random4);
```

#### java.util.Random

사용자 지정 범위의 난수를 발생시키는 클래스.

java.util.Randon 클래스의 nextInt() 메소드를 이용한 난수 발생시킬 수 있다.

{% hint style="success" %}
원하는 범위의 난수를 구하는 공식\
random.nextInt(구하려는 난수의 갯수) + 구하려는 난수의 최소값
{% endhint %}

```java
Random random = new Random();

/* 1. 0 ~ 9까지 난수 발생 */
int random1 = random.nextInt(10);
System.out.println("random1 = " + random1);

/* 2. 1 ~ 10까지 난수 발생*/
int random2 = random.nextInt(10) + 1;
System.out.println("random2 = " + random2);
/* 3. 20 ~ 45까지 난수 발생*/
int random3 = random.nextInt(26) + 20;
System.out.println("random3 = " + random3);
/* 2. -128 ~ 127까지 난수 발생*/
int random4 = random.nextInt(256)-128;
System.out.println("random4 = " + random4);
```

## 3️⃣ scanner

java.util.Scanner를 이용한 다양한 자료형 값 입력 받기

### 1. Scanner 객체 생성

```java
//java.util.Scanner sc = new java.util.Scanner(java.lang.System.in);
//java.util.Scanner sc = new java.util.Scanner(System.in);
Scanner sc = new Scanner(System.in);
```

### 2. 자료형별 값 입력 받기

#### 문자열 입력받기

```java
/* nextLine() : 입력받은 값을 문자열로 반환해준다. */
System.out.print("이름을 입력하세요 : ");
String name = sc.nextLine();
System.out.println("입력하신 이름은 " + name + "입니다.");
```

#### 정수형 값 입력받기

```java
/* nextInt() : 입력받은 값을 int형으로 반환한다. */
System.out.print("나이를 입력하세요 : ");
int age = sc.nextInt();
System.out.println("입력하신 나이는 " + age + "입니다.");
```

```java
/* nextLong() : 입력받은 값을 long형으로 반환한다. */
System.out.print("금액을 입력해주세요.");
long money = sc.nextLong();
System.out.println("입력하신 금액은" +money+"원 입니다.");
```

#### 실수형 값 입력 받기

```java
/* nextFloat() : 입력받은 값을 float형으로 반환한다. */
System.out.println("키를 입력해주세요 :");
float height = sc.nextFloat();
System.out.println("입력하신 키는" + height + "cm 입니다.");
```

```java
/* nextDouble() : 입력받은 값을 double형으로 반환한다. */
System.out.print("원하는 실수를 입력하세요 : ");
double number = sc.nextDouble();
System.out.println("입력하신 실수는 " + number + "입니다.");
```

#### 논리형 값 입력 받기

```java
/* nextBoolean() : 입력받은 값을 boolean형으로 반환한다. */
System.out.print("참과 거짓 중에 한 가지를 true or false로 입력해주세요 : ");
boolean isTrue = sc.nextBoolean();
System.out.println("입력하신 논리 값은 : " + isTrue + "입니다.");
```

#### 문자형 값 입력 받기

```java
sc.nextLine();
System.out.println("아무 문자나 입력해주세요 : ");
char ch = sc.nextLine().charAt(5);
System.out.println("입력하신 문자는" + ch + "입니다.");
```

#### nextLine()과 next()

<mark style="background-color:green;">**nextLine()**</mark> : 공백을 포함한 한 줄을 입력을 위한 개행문자 전까지 읽어서 문자열로 반환한다. ( 공백문자 포함 )\
<mark style="background-color:green;">**next()**</mark> : 공백문자나 개행문자 전까지 읽어서 문자열로 반환한다.

```java
Scanner sc = new Scanner(System.in);
/* nextLine */
System.out.print("인사말을 입력해주세요 : ");
String greeting1 = sc.nextLine();

/* next */
System.out.print("인사말을 입력해주세요 : ");
String greeting2 = sc.next();

System.out.println("greeting2 = " + greeting2);
```
