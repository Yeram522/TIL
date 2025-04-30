---
icon: '5'
---

# Array

## 1️⃣ 배열이란?

동일한 자료형의 묶음(연속된 메모리 공간에 값을 저장하고 사용하기 위한 용도) 이다.\
배열은 heap 영역에 new 연산자를 이용하여 할당한다.

### 💡배열의 사용 이유?

만약 배열을 사용하지 않는다면 변수를 여러 개 사용해야 한다.\
1\. 연속된 메모리 공간으로 관리할 수 없다.( 모든 변수의 이름을 사용자가 관리해야 한다.)\
2\. 반복문을 이용한 연속 처리가 불가능하다.

{% code title="✅ 배열의 선언 및 할당" %}
```java
int[] arr = new int[5];
```
{% endcode %}

_하나의 이름으로 관리되는 <mark style="background-color:yellow;">**연속된 메모리 공간**</mark>이고, 공간마다 찾아갈 수 있는 <mark style="background-color:yellow;">번호(인덱스)를 이용해 접근</mark>한다._

```java
arr[0] = 10;
arr[1] = 20;
arr[2] = 30;
arr[3] = 40;
arr[4] = 50;
```

{% code title="✅ 반복문으로 값 대입" %}
```java
for(int i = 0 , value = 0; i < arr.length; i++){
    arr[i] = value += 10;
}
```
{% endcode %}

### 1. 배열의 선언

```
자료형[] 변수명;
자료형 변수명[]; 로 선언할 수 있다.
```

<pre class="language-java"><code class="lang-java"><strong>//✅ 선언은 stack에 배열의 주소를 보관할 수 있는 공간을 만드는 것
</strong><strong>int[] iarr;
</strong>char carr[];
</code></pre>

### 2. 배열의 할당

선언한 레퍼런스 변수에 배열을 할당하여 대입할 수 있다.\
<mark style="background-color:yellow;">**new**</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">연산자는</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">**heap**</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">영역에 공간을 할당</mark>하고 _발생한 주소값을 반환하는 연산&#xC790;_&#xC774;다.\
발생한 주소를 <mark style="color:red;background-color:yellow;">레퍼런스변수(참조형 변수)</mark><mark style="background-color:yellow;">에 저장하</mark>고 이것을 참조하여 사용하기 때문에 <mark style="background-color:yellow;">**참조자료형**</mark>이라고 한다.

```java
// ✅ 배열을 할당할 때는 반드시 배열의 크기를 지정해 주어야 한다.
//        iarr = new int[];
iarr = new int[5];
carr = new char[10];
```

{% code title="✅ 선언과 할당을 동시에 가능" %}
```java
int[] iarr2 = new int[5];
char[] carr2 = new char[10];
```
{% endcode %}

```java
/* heap 메모리는 이름으로 접근하는 것이 아닌 주소로 접근하는 영역이다.
*  stack에 저장된 주소로 heap에 할당된 배열을 찾아갈 수 있다.
* */
System.out.println("iarr 2 = " + iarr2); // 16진수 주소값 출력
System.out.println("carr 2 = " + carr2);
```

{% hint style="success" %}
**hashcode()** : 일반적으로 객체의 주소값을 10진수로 변환하여 생성한 <mark style="background-color:yellow;">**객체의 고유한 정수값을 반환**</mark>한다.&#x20;_<mark style="color:orange;">동일객체인지 비교할 때 사용할 목적으로 쓰여진다.</mark>_
{% endhint %}

{% hint style="success" %}
**length** : 배열의 길이를 알 수 있는 기능

```java
System.out.println(iarr2.length);
System.out.println(carr2.length);
```
{% endhint %}

{% hint style="success" %}
**NullPointerException** : 아무것도 참조하지 않고 null이라는 특수한 값을 참조하고 있는 경우\
참조연산자를 사용하게 될 때 발생하는 에러이다.

```java
darr = null;
System.out.println(darr.length);
```
{% endhint %}

### 3. 배열에 초기화 되는 자료형별 기본값

```java
값의 형태 별 기본값
*  정수 : 0
*  실수 : 0.0
*  논리 : false
*  문자 : \u0000
*  참조 : null
```

```java
/* 자바에서 지정한 기본값 외의 값으로 초기화를 하고 싶은 경우 블럭을 이용한다.
*  블럭을 사용하는 경우 new를 사용하지 않아도 되며, 값의 갯수만큼 자동으로 크기가 설정된다.
* */
int[] iarr2 = {11,22,33,44,55};

int[] iarr3 = new int[] {11,22,33,44,55};

System.out.println("iarr2 = " + iarr2.length);
System.out.println("iarr2 = " + iarr3.length);
```

## 2️⃣ 다차원 배열

_2차원 이상의 배&#xC5F4;_&#xC744; 의미한다.\
배열의 인덱스마다 또 다른 배열의 주소를 보관하는 배열을 의미한다.\
즉, <mark style="background-color:green;">**2차원 배열은 1차원 배열 여러 개를 하나로 묶어서 관리하는 배열**</mark>을 의미한다.\
더 많은 차원의 배열을 사용할 수 있지만 일반적으로 2차원 배열보다 더 높은 차원의 배열은 사용 빈도가 적다.

### 1. 레퍼런스 변수 선언

```java
/* 1. 배열의 주소를 보관할 레퍼런스 변수 선언(stack) */
int[][] iarr1;
int iarr2[][];
int[] iarr[];
```

### 2. 1차원 배열 생성

```java
/* 2. 여러 개의 1차원 배열의 주소를 관리하는 배열을 생성(heap) */
//        iarr1 = new int[][];
//        iarr1 = new int[][4]; // 주소를 묶어서 관리할 배열의 크기를 지정하지 않으면 에러 발생
iarr1 = new int[3][];
```

### 3. 각 인덱스에서 관리하는 배열 할당

```java
/* 3. 각 인덱스에서 관리하는 배열을 할당(heap)하여 주소를 보관하는 배열에 저장 */
iarr1[0] = new int[5];
iarr1[1] = new int[5];
iarr1[2] = new int[5];
```

{% hint style="success" %}
앞 부분은 주소를 관리하는 배열의 크기, 뒷 부분은 각 인덱스 할당하는 배열의 길이

```java
iarr2 = new int[3][5];
```
{% endhint %}

### 4. 배열 접근 및 사용

```java
// 0번째 인덱스의 배열 값 출력
for(int i = 0; i < iarr1[0].length; i++){
    System.out.print(iarr1[0][i] + " ");
}
System.out.println();

// 0번째 인덱스의 배열 값 출력
for(int i = 0; i < iarr1[1].length; i++){
    System.out.print(iarr1[1][i] + " ");
}
System.out.println();

// 0번째 인덱스의 배열 값 출력
for(int i = 0; i < iarr1[2].length; i++){
    System.out.print(iarr1[2][i] + " ");
}
System.out.println();
```

## 3️⃣ 깊은 복사 VS 얕은 복사

배열의 복사에는 두 가지 종류가 있다.

<mark style="background-color:green;">**얕은 복사**</mark> : stack의 주소값만 복사

<mark style="background-color:green;">**깊은 복사**</mark> : heap의 배열에 저장된 값 복사

### 1. 얕은 복사(shallow copy)

{% hint style="warning" %}
**얕은 복사**는 <mark style="background-color:yellow;">stack에 저장되어 있는</mark> <mark style="color:red;background-color:yellow;">배열의 주소값만 복사</mark><mark style="background-color:yellow;">한다는 것</mark>이다.\
따라서 _두 개의 레퍼런스 변수는 동일한 배열의 주소값을 가지고 있다_.\
하나의 레퍼런스 변수에 저장된 주소값을 가지고 배열의 내용을 수정(값 변경)을 하게 되면\
&#xNAN;_<mark style="color:red;background-color:yellow;">다른 레퍼런스 변수로 배열에 접근했을 떄도 동일한 배열을 가리키고 있기 때문에 원본 값이 변경된다.</mark>_
{% endhint %}

```java
int[] originArr = {1,2,3,4,5};

int[] copyArr = originArr; // 얕은 복사
System.out.println(originArr.hashCode());
System.out.println(copyArr.hashCode());

for(int i = 0; i < originArr.length; i ++){
    System.out.print(originArr[i] + " ");
}

System.out.println();

for(int i = 0; i < copyArr.length; i++){
    System.out.print(copyArr[i] + " ");
}
System.out.println();

copyArr[0] = 99;

for(int i = 0; i < originArr.length; i ++){
    System.out.print(originArr[i] + " ");
}

System.out.println();

for(int i = 0; i < copyArr.length; i++){
    System.out.print(copyArr[i] + " ");
}
System.out.println();
```

### 2. 얕은 복사의 활용

주로 <mark style="background-color:green;">**메소드 호출 시 인자로 사용하는 경우**</mark>와&#x20;<mark style="background-color:green;">리턴값으로 동일한 배열을 리턴해주고 싶은 경우</mark> 사용한다.

#### 인자와 매개변수로 활용

다른 메소드에서 동일한 배열을 사용하고 싶은 경우 얕은 복사를 이용한다.

```java
print(names);
```

#### 리턴 값으로 활용

```java
String[] animals = getAnimals();

System.out.println("리턴 받은 animals hashcode : " + animals.hashCode());

print(animals);
```

### 3. 깊은 복사

{% hint style="warning" %}
**깊은 복사**는 <mark style="color:red;background-color:yellow;">heap에 생성된 배열이 가지고 있는 값을&#x20;또 다른 배열에 복사</mark><mark style="background-color:yellow;">를 해 놓은 것</mark>이다.\
서로 같은 값을 가지고 있지만, 두 배열은 서로 다른 배열이기에&#x20;하나의 _<mark style="color:red;">배열에 변경을 하더라도 다른 배열에는 영향을 주지 않는다.</mark>_
{% endhint %}

#### 깊은 복사를 하는 법

1.  for 문을 이용한 동일한 인덱스의 값을 복사



    ```java
    int[] copyArr1 = new int[10];

    for(int i = 0; i < originArr.length; i ++){
        copyArr1[i] = originArr[i];
    }

    print(copyArr1);
    ```
2.  Object의 `clone()` 을 이용한 복사



    동일한 길이, 동일한 값을 가지는 배열이 생성되어 복사되며, 다른 주소를 가지고 있다.

    ```java
    int[] copyArr2 = originArr.clone();

    print(copyArr2); 
    ```
3.  System의 `arraycopy()` 를 이용한 복사



    ```java
    int[] copyArr3 = new int[10];

    /*✅ 원본배열, 복사를 시작할 인덱스, 복사본 배열, 복사를 시작할 인덱스, 복사할 길이 */
    System.arraycopy(originArr, 0, copyArr3,3, originArr.length);

    print(copyArr3); // 복사한 만큼의 값은 같지만 길이도 다르고 주소도 다르다.
    ```
4.  Array의 `copyOf()` 를 이용한 복사



    ```java
    int[] copyArr4 = Arrays.copyOf(originArr, 7);

    print(copyArr4);
    ```
