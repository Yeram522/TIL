---
icon: '4'
---

# Control Flow

## 1️⃣ Conditional

### 1. if문 표현식

```
if(조건식) {
    조건식이 true일 때 실행할 명령문;
}
```

<mark style="background-color:purple;">**조건식**</mark> : true or false가 나오는 연산식을 조건식이라고 한다.\
if문은 조건식의 결과 값이 참(true) { } 안에 있는 코드를 실행하고,\
조건식의 결과 값이 거짓(false)이면 { } 안에 있는 코드를 무시하고 넘어감

{% code title="✅ 단일 if문" %}
```java
Scanner sc = new Scanner(System.in);

System.out.print("숫자를 한 개 입력하세요 : ");
int num = sc.nextInt();

if(num % 2 == 0){
        System.out.println("입력하신 숫자는 짝수입니다.");
}

System.out.println("프로그램을 종료합니다.");
```
{% endcode %}

{% code title="✅ 중첩 if문" %}
```java
Scanner sc = new Scanner(System.in);

System.out.print("숫자 한 개를 입력하세요 : ");
int num = sc.nextInt();

if(num > 0){
    if(num % 2 == 0){
        System.out.println("입력하신 숫자는 양수이면서 짝수입니다.");
    }
}

System.out.println("프로그램을 종료합니다.");
```
{% endcode %}

### 2. if-else문

```
if(조건식) {
      조건식이 true 일 떄 실행할 명령문;
} else{
      조건식 false 일 때 실행할 명령문;
}
```

```java
Scanner sc = new Scanner(System.in);
System.out.print("정수 한 개를 입력하세요 : ");
int num = sc.nextInt();

if(num % 2 != 0){
    System.out.println("입력하신 숫자는 홀수입니다.");
} else{
    System.out.println("입력하신 숫자는 짝수입니다.");
}

System.out.println("프로그램을 종료합니다.");
```

### 3. if-else-if

```
if(조건식1){
   조건식1이 true일 떄 실행할 명령문;
} else if(조건식2){
   조건식1이 false이고 조건식2가 true일 때 실행할 명령문;
} else{
    위의 조건 2개가 모두 거짓인 경우 실행할 명령문;
}
```

```java
Scanner sc = new Scanner(System.in);
System.out.print("학생의 이름을 입력하세요 : ");
String name = sc.nextLine();
System.out.print("학생의 점수를 입력하세요 : ");
int point = sc.nextInt();

String grade = "";
if(point >= 90){

    grade = "A";

    if(point >= 95){
        grade += "+";
    }
} else if (point >= 80) {
    grade = "B";

    if(point >= 85){
        grade += "+";
    }
}else if (point >= 70) {
    grade = "C";

    if(point >= 75){
        grade += "+";
    }
}else if (point >= 60) {
    grade = "D";

    if(point >= 65){
        grade += "+";
    }
} else{
    grade = "F";
}

System.out.println(name + "학생의 점수는" + point + "이고, 등급은" + grade + "입니다.");
System.out.println("프로그램을 종료합니다.");
```

### 4. switch

```
switch(비교할 변수){
  case 비교값1 : 비교값1과 일치하는 경우 실행할 구문; break;
  case 비교값2 : 비교값2과 일치하는 경우 실행할 구문; break;
  default : case에 모두 해당하지 않는 경우 실행할 구문; break;
}
```

```java
Scanner sc = new Scanner(System.in);
System.out.print("첫 번째 정수 입력 :");
int first = sc.nextInt();
System.out.print("두 번째 정수 입력 :");
int second = sc.nextInt();
System.out.print("연산 기호 입력(+, -, *, /, %) : ");
char op = sc.next().charAt(0);

int result = 0;

switch (op){
    case '+':
        result = first + second;
        break;
    case '-':
        result = first - second;
        break;
    case '*':
        result = first * second;
        break;
    case '/':
        result = first / second;
        break;
    case '%':
        result = first % second;
        break;

        // 산술연산 외에 다른 문자에 대한 처리는 생략하였음
}
System.out.println(first + " " + op + " " + second + " = " + result);
```

## 2️⃣ looping

### 1. for

```
for(초기식; 조건식; 증감식){
         조건을 만족하는 경우 수행할 구문(반복할 구문);
}
```

```java
/* 1부터 10까지 1씩 증가시키면서 i값을 출력하는 기본 반복문 */
for(int i = 1; i <= 10; i++){
    System.out.println(i);
}
```

#### 중첩 for문

```java
for(int dan = 2; dan < 10; dan ++){
    for(int su = 1; su < 10; su++){
        System.out.println(dan + "*" + su + "=" + (dan*su));
    }
}
```

### 2. while

<pre><code>초기식;
while(조건식){
  조건을 만족하는 경우 수행할 구문(반복할 구문);
<strong>  증감식;
</strong>}
</code></pre>

```java
/* 1부터 10까지 1씩 증가시키면서 i값 출력해보자 */
int i = 1;
while (i <= 10){
    System.out.println(i);
    i++;
}
```

#### 중첩 while 문

```java
int dan = 2;
while(dan<10){
    int su = 1;
    while(su < 10){
        System.out.println(dan + "*" +su + " = " + (dan*su));
        su++;
    }
    System.out.println();
    su++;
}
```

### 3. do while

```
초기식;
do{
    1회차에는 무조건 실행하고, 이후에는 조건식을 확인하여 조건을 만족하는 경우 수행할 구문(반복할 수분)
} while(조건식);
```

```java
do{
    System.out.println("최초 한 번 동작함...?");
}while(false);
```



## 3️⃣branching

### 1. break

break는 반복문 내에서 사용한다.\
해당 반복문을 빠져 나올 때 사용하며, 반복문의 조건문 판단 결과와  상관없이\
반복문을 빠져나올 떄 사용한다.\
일반적으로 if(조건식) {break;} 처럼 사용된다.\
단, switch문은 반복문이 아니지만 예외적으로 사용된다.

```java
/* break를 이용하여 무한루프를 활용한 1 ~ 100 합계 구하기 */
int sum = 0;
int i = 1;
while(true){
    sum += i;

    if(i == 100){
        break;
    }

    i++;
}
```

### 2. continue

continue문은 반복문 내에서 사용한다.\
해당 반복문의 반복 회차를 중간에 멈추고, 다시 증감식으로 넘어가게 해준다.\
일반적으로 if(조건식) { continue; } 처럼 사용된다.\
보통 반복문 내에서 특정 조건에 대한 예외를 처리하고자 할 때 자주 사용된다.

```java
/* 1부터 100 사이의 4의 배수이면서 5의 배수인 값 출력 */
for(int i = 1; i <= 100; i++){

    if(i % 4 == 0 && i % 5 == 0){

        System.out.println("i = " + i);
    }else{
        continue;
    }
}
```

