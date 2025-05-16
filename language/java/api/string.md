# String

## String 메서드

### charAt()

해당 문자열의 특정 인덱스에 해당하는 문자를 반환한다.\
인덱스는 0부터 시작하는 숫자 체계를 의미하며,&#x20;

인덱스를 벗어난 정수를 인자로 전달하는 경우에는 _<mark style="color:red;">IndexOutOfBoundsException</mark>_&#xC774; 발생한다.

```java
String str1 = "apple";

for(int i = 0; i < str1.length(); i++){
    System.out.println(str1.charAt(i));
}
```

### compareTo()

인자로 전달된 문자열과 사전 순으로 비교를 하여 <mark style="background-color:yellow;">두 문자열이 같다면</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">**0**</mark><mark style="background-color:yellow;">을 반환</mark>, 인자로 전달된 문자열보다 <mark style="background-color:yellow;">작으면</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">**음수**</mark><mark style="background-color:yellow;">, 크면</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">**양수**</mark>를 반환한다.

단, 이 메소드는 대소문자를 구분하여 비교한다.

```java
String str2 = "java";
String str3 = "java";
String str4 = "JAVA";
String str5 = "oracle";

System.out.println("compareTo() : " + (str2.compareTo(str3))); // 0

System.out.println("compareTo() : " + (str2.compareTo(str4))); // 32
System.out.println("compareTo() : " + (str4.compareTo(str2))); // -32

System.out.println("compareTo() : " + (str2.compareTo(str5))); // -5
System.out.println("compareTo() : " + (str5.compareTo(str2))); // 5
```

### compareToIgnoreCase()

<mark style="background-color:green;">대소문자를</mark> <mark style="background-color:green;"></mark><mark style="background-color:green;">**구분하지 않고**</mark> 비교

```java
System.out.println("CompareToIgnoreCase() : " + (str3.compareToIgnoreCase(str4)));//0
```

### concat()

문자열에 인자로 <mark style="background-color:green;">전달된 문자열을</mark> <mark style="background-color:green;"></mark><mark style="background-color:green;">**합치기**</mark> 해서 새로운 문자열을 반환한다.\
원본 문자열에는 영향을 주지 않는다.

```java
System.out.println("concat() : " + (str2.concat(str5)));// javaoracle
System.out.println(str2); // java
```

### indexOf()

문자열에서 **특정 문자를 탐색**하여 _<mark style="background-color:green;">처음 일치하는</mark>_ <mark style="background-color:green;">**인덱스 위치**</mark><mark style="background-color:green;">를 정수형으로 반환</mark>한다.\
단, _<mark style="color:orange;">일치하는 문자가 없는 경우 -1을 반환</mark>_&#xD55C;다.

```java
String indexOf = "java oracle";
System.out.println(indexOf.indexOf('a')); // 1
System.out.println(indexOf.indexOf('z')); // -1
```

### lastIndexOf()

문자열 탐색을 **뒤에서부터** 하고 <mark style="background-color:green;">처음 일치하는 위치의 인덱스를 반환</mark>한다.\
단, _<mark style="color:orange;">일치하는 문자가 없는 경우 -1을 반환</mark>_&#xD55C;다.

```java
System.out.println(indexOf.lastIndexOf('a'));// 7
System.out.println(indexOf.lastIndexOf('z')); // -1
```

### trim()

문자열의 <mark style="background-color:green;">**앞 뒤**</mark><mark style="background-color:green;">에</mark> <mark style="background-color:green;"></mark><mark style="background-color:green;">**공백을 제거**</mark><mark style="background-color:green;">한 문자열을 반환</mark>한다.

```java
String trimStr = "   java   ";
System.out.println("trimStr : #" + trimStr + "#");// #   java   #
System.out.println("trimStr : #" + trimStr.trim() + "#"); // #java#
// 원본에 영향을 주지 않는다.
System.out.println("trimStr : #" + trimStr + "#");// #   java   ##
```

### toLowerCase()

모든 문자를 <mark style="background-color:green;">**소문자로 변환**</mark> 시킨다.

### toUpperCase()

모든 문자를 <mark style="background-color:green;">**대문자로 변환**</mark> 시킨다. _원본에는 영향을 주지 않는다._

```java
String caseStr = "JavaOracle";
System.out.println(caseStr.toLowerCase()); // javaoracle
System.out.println(caseStr.toUpperCase()); // JAVAORACLE
System.out.println(caseStr); // JavaOracle
```

### substring()

문자열의 <mark style="background-color:green;">**일부분을 잘라**</mark>내어 새로운 문자열을 반환한다. _원본에 영향을 주지 않는다._

```java
String javaOracle = "javaoracle";

//aor
System.out.println(javaOracle.substring(3,6));// 3번째 index부터 6번째 index 전까지 자른다.

//aoracle
System.out.println(javaOracle.substring(3));// 인자를 하나만 전달도 가능

//javaoracle
System.out.println(javaOracle);// 원본은 변하지 않는다.
```

### replace()

문자열에서 <mark style="background-color:green;">**대체할 문자열로 기존 문자열을 변경**</mark>해서 반환한다. _원본에 영향을 주지 않는다._

```java
System.out.println(javaOracle.replace("java", "python"));// pythonoracle

System.out.println(javaOracle);// javaoracle
```

### length()

문자열의 길이를 <mark style="background-color:green;">**정수형**</mark><mark style="background-color:green;">으로 전환</mark>한다.

```java
System.out.println(javaOracle.length()); // 10
System.out.println("".length()); // 0
```

### isEmpty()

문자열의 길이가 **0**이면 **true** 반환, 아니면 false를 반환\
<mark style="color:red;background-color:yellow;">길이가 0인 문자열은 null과는 다르다.</mark>

```java
System.out.println("".isEmpty()); // 비어있기 때문에 true
System.out.println("abc".isEmpty()); // false
```

## 문자열 객체

### "" 리터럴 형태

동일한 값을 가지는 인스턴스를 **단일 인스턴스로 관리**한다. (singleton)

### new String("문자열")

매번 **새로운 인스턴스를 생성**한다.

```java
String str1 = "java";
String str2 = "java";
String str3 = new String("java");
String str4 = new String("java");

System.out.println(str1 == str2); // true
System.out.println(str2 == str3); // false
System.out.println(str3 == str4); // false
```

{% hint style="success" %}
동일한 문자열은 동일한 hashCode값을 반환하도록 재정의 되어있다.

```java
System.out.println(str1.hashCode()); // 3254818
System.out.println(str2.hashCode()); // 3254818
System.out.println(str3.hashCode()); // 3254818
System.out.println(str4.hashCode()); // 3254818
```
{% endhint %}

<details>

<summary>🤔 Java Heap과 String pool, hashcode</summary>

<figure><img src="../../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

리터럴로 String을 생성하면 java heap의 string pool에 저장 되어 재사용되지만,\
`new` 키워드를 이용해 새로운 인스턴스를 생성하므로 str3과 str4는 별도의 객체로 볼 수 있다.

하지만 hashcode가 전부 같게 나오는 이유는, _hashCode()는 <mark style="color:red;background-color:yellow;">객체의 내용을 기반</mark>으로 해시 **값을 계산**하기 때&#xBB38;_&#xC774;다.

</details>

{% hint style="success" %}
문자열은 불변이라는 특징을 가진다.

```java
str2 += "oracle";

System.out.println(str1 == str2);
```
{% endhint %}

### equeals()

String 클래스의 `equals()` 메소드는 <mark style="color:red;background-color:yellow;">인스턴스 비교가 아닌 문자열 값을 비교</mark>하여 동일한 값을 가지는 경우 true, 다른 값을 가지는 경우 false를 반환하도록 Object의 equals() 메소드를 재정의 해두었다.

따라서 문자열 인스턴스 생성 방식과 상관 없이 <mark style="background-color:green;">동일한 문자열인지를 비교하기 위해</mark> <mark style="background-color:green;"></mark><mark style="background-color:green;">`==`</mark> <mark style="background-color:green;"></mark><mark style="background-color:green;">연산 대신</mark> <mark style="background-color:green;"></mark><mark style="background-color:green;">`equals()`</mark> <mark style="background-color:green;"></mark><mark style="background-color:green;">메소드를 사용해야 한다.</mark>

```java
System.out.println(str1.equals(str3));
System.out.println(str1.equals(str4));
```

## 문자열 분리

문자열을 특정 구분자로 하여 분리한 문자열을 반환하는 기능을 함.

### split()

정규 표현식을 이용해 문자열을 분리한다.\
정규 표현식을 이용하기 때문에 속도가 느리다는 단점을 가진다.

```java
String emp1 = "100/홍길동/서울/영업부"; // 모든 값 존재함
String emp2 = "200/유관순//총무부"; // 주소 없음
String emp3 = "300/이순신/경기도"; // 부서 없음

String[] empArr1 = emp1.split("/");
/*
100
홍길동
서울
영업부
*/
String[] empArr2 = emp2.split("/");
/*
200
유관순

총무부
*/
String[] empArr3 = emp3.split("/");
/*
300
이순신
경기도
*/
```

### StringTokenizer

문자열의 모든 문자들을 구분자로 하여 문자열을 구분한다.\
split()보다 속도면에서 더 빠르다.

```java
StringTokenizer st1 = new StringTokenizer(emp1, "/");
StringTokenizer str2 = new StringTokenizer(emp2, "/");
StringTokenizer str3 = new StringTokenizer(emp3, "/");

while (st1.hasMoreElements()){
    System.out.println(st1.nextToken());
}
/*
100
홍길동
서울
영업부
*/

while (str2.hasMoreTokens()){
    System.out.println(str2.nextToken());
}
/*
200
유관순
총무부
*/

while (str3.hasMoreTokens()){
    System.out.println(str3.nextToken());
}
/*
300
이순신
경기도
*/
```

{% hint style="success" %}
s**plit() VS StringTokenizer**

#### split() 메서드의 특징

* 연속된 구분자 사이에 문자열이 없을 경우, 빈 문자열을 토큰으로 취급합니다.
* 각 구분자를 개별적으로 처리합니다.



#### StringTokenizer의 특징

* 연속된 구분자 사이에 문자열이 없을 경우, 빈 문자열을 토큰으로 취급하지 않습니다.
* 즉, 구분자가 연속으로 나타나면 하나의 구분자로 취급합니다.
{% endhint %}

## escape 문자

문자열 내에서 사용하는 문자 중 특수문자를 표현하거나 특수기능을 사용할 때 사용하는 문자이다.

<table><thead><tr><th width="142.6666717529297">이스케이프 문자</th><th width="185.9999542236328">의미</th></tr></thead><tbody><tr><td>\n</td><td>개행(줄바꿈)</td></tr><tr><td>\t</td><td>탭</td></tr><tr><td>\'</td><td>작은따옴표</td></tr><tr><td>\"</td><td>큰따옴표</td></tr><tr><td>\\</td><td>역슬래쉬 표시</td></tr></tbody></table>

```
System.out.println("안녕하세요.\n저는 홍길동입니다.");
System.out.println("안녕하세요.\t저는 홍길동입니다.");
System.out.println("안녕하세요. 저는 '홍길동' 입니다.");
//        System.out.println('''); // ❌
System.out.println('\'');
//        System.out.println("안녕하세요. 저는 "홍길동" 입니다."); // ❌
System.out.println("안녕하세요. 저는 \"홍길동\" 입니다.");
System.out.println("안녕하세요. 저는 \\홍길동\\ 입니다.");
```

{% hint style="info" %}
split 시 이스케이프 문자를 사용해야 하는 특수문자도 존재한다.\


* 이스케이프 문자 사용 안하는 특수문자
  * \~ \` ! @ # % & - \_ = ; : ' \ " , < > /&#x20;
* 이스케이프 문자를 사용하는 특수문자(\\)
  * $ ^ \* ( ) + | { } \[ ] . ?
{% endhint %}
