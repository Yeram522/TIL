---
icon: '4'
---

# Control Flow

## 1️⃣ if

### if문 표현식

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

## 2️⃣ if-else

### if-else문 표현식

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

## 3️⃣ if-else-if

### if-else-if 표현식

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

## 4️⃣ switch

### switch 표현식

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
