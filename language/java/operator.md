---
icon: '2'
---

# Operator

## 1️⃣ 산술 연산자

산술연산자는 주로 사칙연산과 관련된 연산자로 가장 기본적이면서도 많이 사용되는 연산자이다.\
연산의 실행이 가능하기 위해 필요한 값이나 변수가 두 개인 이항 연산자로 분류되며\
피연산자들의 연산 방향은 왼쪽에서 오른쪽이다.

### 산술 연산자의 우선순위

수학의 개념과 유사하게 곱하기와 나누기 연산이 더하기와 빼기 연산보다 우선적으로 동작한다.\
우선순위가 같은 경우 연산자의 결합 방향에 의해 실행 순서가 결정된다.

```java
int num1 = 20;
int num2 = 7;

System.out.println(num1 + num2);
System.out.println(num1 - num2);
System.out.println(num1 * num2);
System.out.println(num1 / num2);
System.out.println(num1 % num2);
```



## 2️⃣ 대입 연산자

`=` : 왼쪽의 피연산자에 오른쪽의 피연산자를 대입함\
`+=` : 왼쪽의 피연산자에 오른쪽의 피연산자를 더한 결과를 왼쪽의 피연산자에 대입함.\
`-=` : 왼쪽의 피연산자에 오른쪽의 피연산자를 뺀 결과를 왼쪽의 피연산자에 대입함\
`*=` : 왼쪽의 피연산자에 오른쪽의 피연산자를 곱한 결과를 왼쪽의 피연산자에 대입함.\
`/=` : 왼쪽의 피연산자에 오른쪽의 피연산자를 나눈 결과를 왼쪽의 피연산자에 대입함.\
`%=` : 왼쪽의 피연산자에 오른쪽의 피연산자를 나눈 나머지 결과를 왼쪽의 피연산자에 대입함.



## 3️⃣ 증감 연산자

{% hint style="info" %}
증감 연산자

피연산자의 앞 or 뒤에 사용이 가능하다.\
&#x20;`++` : 1 증가의 의미\
&#x20;`--` : 1 감소의 의미
{% endhint %}

### 1. 증감 연산자를 단항으로만 사용

```java
int num = 20;

num++; // 1 증가

++num; // 1 증가

num--; // 1 감소

--num; // 1 감소
```

### 2. 증감 연산자를 다른 연산자와 함께 사용

{% hint style="danger" %}
주의사항

다른 연산자와 함께 사용할 때 증감 연산자의 의미\
`++var` : 피연산자의 값을 먼저 1을 증가시킨 후 다른 연산을 진행함.\
`var++` : 다른 연산을 먼저 진행하고 난 뒤 마지막에 피연산자의 값을 1 증가시킴\
`--var` : 피연산자의 값을 먼저 1을 감소시킨 후 다른 연산을 진행함.\
`var--` : 다른 연산을 먼저 진행하고 난 뒤 마지막에 피연산자의 값을 1 감소시킴
{% endhint %}

```java
int firstNum = 20;

int result1 = firstNum++ * 3;

System.out.println("result1 = " + result1);
System.out.println("firstNum = " + firstNum);

int secondNum = 20;

int result2 = ++secondNum * 3;

System.out.println("result2 = " + result2);
System.out.println("secondNum = " + secondNum);
```



## 3️⃣ 비교 연산자

비교연산자는 피연산자 사이에서 상대적인 크기를 판단해서 참 혹은 거짓을 반환하는 연산자이다.\
연산자 중 참 혹은 거짓을 반환하는 연산자는 삼항연산자의 조건이나 조건문의 조건절에 많이 사용된다.

`==` : 왼쪽의 피연산자와 오른쪽의 피연산자가 같으면 true 다르면 false를 반환\
`!=` : 왼쪽의 피연산자와 오른쪽의 피연산자가 다르면 true 같으면 false를 반환\
`>` : 왼쪽의 피연산자가 오른쪽의 피연산자보다 크면 true 작으면 false를 반환\
`>=` : 왼쪽의 피연산자가 오른쪽의 피연산자보다 크거나 같으면 true 아니면 false를 반환.\
`<` : 왼쪽의 피연산자가 오른쪽의 피연산자보다 작으면 true 크면 false를 반환\
`<=` : 왼쪽의 피연산자가 오른쪽의 피연산자보다 작거나 같으면 true 아니면 false를 반환.

### 숫자값 비교 - 전수 비교

```java
int inum1 = 10;
int inum2 = 20;

System.out.println(inum1 == inum2);
System.out.println(inum1 != inum2);
System.out.println(inum1 > inum2);
System.out.println(inum1 >= inum2);
System.out.println(inum1 < inum2);
System.out.println(inum1 <= inum2);
```

### 숫자값 비교 - 실수 비교

```java
double dnum1 = 10.0;
double dnum2 = 20.0;

System.out.println(dnum1 == dnum2);
System.out.println(dnum1 != dnum2);
System.out.println(dnum1 > dnum2);
System.out.println(dnum1 >= dnum2);
System.out.println(dnum1 < dnum2);
System.out.println(dnum1 <= dnum2);
```

### 문자값 비교

```java
char ch1 = 'a';
char ch2 = 'A';

System.out.println(ch1 == ch2);
System.out.println(ch1 != ch2);
System.out.println(ch1 > ch2);
System.out.println(ch1 >= ch2);
System.out.println(ch1 < ch2);
System.out.println(ch1 <= ch2);
```

### 논리값 비교

```java
boolean bool1 = true;
boolean bool2 = false;

System.out.println(bool1 = bool2);
System.out.println(bool1 != bool2);
//        System.out.println(bool1 > bool2); // 대소 비교 불가능
```



### 문자열값 비교

```java
String str1 = "java";
String str2 = "java";

System.out.println(str1 == str2);
System.out.println(str1 != str2);
//        System.out.println(str1 > str2); // 대소 비교 불가능
```

## 4️⃣ 논리 연산자

### 논리연산자의 종류

#### &#xD;1\. 논리 연결 연산자 :&#x20;

두 개의 피연산자르 가지는 이항 연산자이며, 연산자의 결합 방향은 왼쪽에서 오른쪽이다.&#x20;두 개의 논리식을 판단하여 참과 거짓을 판단한다.\
**1-1.&#x20;**<mark style="background-color:purple;">**&&(논리 AND) 연산자**</mark> : 두 개의 논리식 모두 참 일 경우 참을 반환, 둘 중 한개라도 거짓인 경우 거짓을 반환한다.\
**1-2.&#x20;**<mark style="background-color:purple;">**||(논리 OR) 연산자**</mark> : 두 개의 논리식 중 둘 중 하나라도 참 일 경우 참을 반환, 둘 다 모두 거짓일 경우 거짓을 반환한다.

```java
System.out.println(true && true);
System.out.println(true && false);
System.out.println(false && true);
System.out.println(false && false);

System.out.println(true || true);
System.out.println(true || false);
System.out.println(false || true);
System.out.println(false || false);

System.out.println(!true);
System.out.println(!false);
```

#### 2. 논리식에 논리연산자 활용

피연산자가 하나인 단항연산자로, 피연산자의 결합 방향을 왼쪽에서 오른쪽이다.\
**2-1.&#x20;**<mark style="background-color:purple;">**!(논리 NOT) 연산자**</mark> : 논리식의 결과가 참이면 거짓을, 거짓이면 참을 반환한다.

```java
int a = 10;
int b = 20;
int c = 30;
int d = 40;

System.out.println(a < b && c < d);
System.out.println(a < b && c > d);
System.out.println(a > b && c < d);
System.out.println(a > b && c > d);

System.out.println(a < b || c < d);
System.out.println(a < b || c > d);
System.out.println(a > b || c < d);
System.out.println(a > b || c > d);
```

## 5️⃣ 삼항 연산자

자바에서 유일하게 피연산자 항목이 3개인 연산자이다.\
⭐<mark style="background-color:yellow;">항목이 3개</mark>이다 : `(조건식) ? 참일 때 사용할 값 : 거짓일때 사용할 값`\
&#xNAN;_<mark style="color:red;">조건식은 반드시 결과가 true 또는 false 가 나오게끔 작성해야 한다.</mark>_





### 1. 삼항 연산자 단독 사용

```java
int num1 = 10;
int num2 = -10;

String result1 = (num1 > 0)?"양수다":"양수가 아니다";
String result2 = (num2 > 0)?"양수다":"양수가 아니다";

System.out.println("result1 = " + result1);
System.out.println("result2 = " + result2);
```

### 2. 삼항 연산자 중첩 사용

```java
int num3 = 5;
int num4 = 0;
int num5 = -5;

String result3 = (num3 > 0 )? "양수다" : (num3 == 0)? "0이다": "음수다";
String result4 = (num4 > 0 )? "양수다" : (num4 == 0)? "0이다": "음수다";
String result5 = (num5 > 0 )? "양수다" : (num5 == 0)? "0이다": "음수다";
System.out.println("result3 = " + result3);
System.out.println("result4 = " + result4);
System.out.println("result5 = " + result5);
```
