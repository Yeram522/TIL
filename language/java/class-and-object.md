---
icon: '6'
---

# Class & Object

## 1️⃣ 클래스

{% code title="✅ 사용자 정의 클래스" %}
```java
public class Member {
    String id;
    String pwd;
    String name;
    int age;
    char gender;
    String[] hobby;
}
```
{% endcode %}

&#x20;

### 1. 변수를 이용한 회원 데이터 관리

변수를 이용해서 데이터를 하나씩 저장 할 수 있지만,&#x20;

```java
String id = "user01";
String pwd = "pass01";
String name = "홍길동";
int age = 20;
char gender = '남';
String[] hobby = {"축구","볼링","테니스"};

System.out.println("id = " + id);
System.out.println("pwd = " + pwd);
System.out.println("name = " + name);
System.out.println("age = " + age);
System.out.println("gender = " + gender);

for(int i = 0; i < hobby.length; i++){
    System.out.print(hobby[i]+ " ");
}

System.out.println();
```

### 2. 사용자 정의의 자료형 사용하기

사용자 정의 클래스를 이용하여 자료들을 묶어서 관리할 수 있다.

#### 변수 선언 및 객체 생성

<mark style="color:purple;">`자료형 변수명 = new 클래스명();`</mark> _<mark style="color:green;">// 객체를 생성하는 구문이다.</mark>_\
사용자 정의의 자료형인 클래스를 이용하기 위해서는 <mark style="background-color:purple;">**new 연산자**</mark>로 <mark style="background-color:purple;">**heap 메모리 공간에 할당**</mark>을 해야 한다.\
객체를 생성하게 되면 클래스에 정의한 **필드**와 **메소드** 대로 <mark style="background-color:yellow;">**객체(instance)가 생성**</mark>된다.\
위의 _<mark style="color:red;">회원 정보들을 연속된 메모리 주소에서 사용</mark>_&#xD558;도록 heap에 공간을 다음과 같이 만들 수 있다.

```java
Member member = new Member();
```

#### 생성된 인스턴스의 초기값 확인하기

이렇게 객체를 생성하고 나면 서로 다른 자료형들을 하나의 member라는 이름으로\
관리할 수 있도록 공간을 생성한 것이다.\
&#xNAN;_<mark style="color:red;">heap에 생성되기 때문에 jvm 기본값으로 초기화 된다.</mark>_

필드에 접근하기 위해서는 <mark style="color:purple;">`래퍼런스변수명.필드명`</mark>으로 접근한다.\
<mark style="color:purple;">`'.'`</mark>은 참조연산자라고 하는데, _<mark style="color:green;">레퍼런스 변수가 참고하고 있는 주소로 접근한다는 의미를 가진다.</mark>_\
<mark style="background-color:yellow;">**각 공간은 필드명으로 접근**</mark>한다.(_배열은 인덱스로 접근, 객체는 필드명으로 접&#xADFC;_&#xD55C;다. )

```java
System.out.println(member.id);
System.out.println(member.pwd);
System.out.println(member.name);
System.out.println(member.age);
System.out.println(member.gender);
System.out.println(member.hobby);
```

#### 필드에 접근해서 변수 사용하듯이 사용하기

```java
member.id = "user01";
member.pwd = "pass01";
member.name = "홍길동";
member.age = 20;
member.gender = '남';
member.hobby = new String[] {"축구","볼링","테니스"};


System.out.println(member.id);
System.out.println(member.pwd);
System.out.println(member.name);
System.out.println(member.age);
System.out.println(member.gender);

for(int i = 0; i < member.hobby.length; i++){
    System.out.print(member.hobby[i] + " ");
}
```

## 2️⃣ 캡슐화(encapsulation)

### 1. 캡슐화의 필요성

#### \[ 1 ] 필드에 올바르지 않은 값이 들어가도 통제가 불가능하다.

```java
Monster monster2 = new Monster();
monster2.name = "드라큘라";
monster2.hp = -200; /* hp는 음수가 될 수 없지만, 직접 필드에 접근해
 값을 수정하게 되는 경우 통제 할 수 없다.*/

Monster monster3 = new Monster();
monster3.name = "뿌꾸";
monster3.setHp(-200);
```

```java
public class Monster {
    String name;
    int hp;

    // set 함수를 통해 예방할 수 있지만, 여전히 직접 접근이 가능하다.
    public void setHp(int hp){
        if(hp > 0){
            System.out.println("양수값이 입력되어 몬스터의 체력을 입력한 값으로 변경합니다.");
            this.hp = hp;
        }else{
            System.out.println("0보다 작거나 같은 값이 입력되어 몬스터의 체력을 0으로 변경합니다.");
        }
    }
}
```

#### \[ 2 ] 사용자 지정 클래스의 일부를 수정 했을 때, 해당 필드를 사용하는 모든 코드를 전부 수정해야하는 부담이 생긴다.&#x20;

이는 유지보수에 악영향을 미친다!

<figure><img src="../../.gitbook/assets/image (79).png" alt=""><figcaption><p>String name을 kind로만 바꿨을 뿐이지만 고쳐야 할 것이 많이 생겼다.</p></figcaption></figure>

### 2. 캡슐화의 역할

#### \[ 1 ]  setter, getter 메서드

set,get 메서드를통해 필드 값을 직접 접근하여 읽기/쓰기 하는 것을 대신할 수 있다.

{% code title="✅ 사용자 지정 클래스" %}
```java
public class Monster {

    String name;
    int hp;

    public void setInfo(String name){
        this.name = name;
    }

    public void setHp(int hp){
        if(hp > 0){
            this.hp = hp;
        }else{
            this.hp = 0;
        }
    }
    public  String getInfo(){

        return "몬스터의 이름은" + this.name + "이고, 체력은" + this.hp + "입니다.";
    }
}
```
{% endcode %}

```java
Monster monster1 = new Monster();
monster1.setInfo("드라큘라");
monster1.setHp(200);

Monster monster2 = new Monster();
monster1.setInfo("프랑캔슈타인");
monster1.setHp(200);

Monster monster3 = new Monster();
monster1.setInfo("늑대인간");
monster1.setHp(-300);
```

잘못 된 값으로 필드 값을 지정 해 줄 경우, set 메서드가 동작하여 잘 못된 값이 들어가지 않도록 한다.

#### \[ 2 ] 접근 제한자

하지만 set,get 함수를 사용하지 않고도 `.` 참조연산자를 이용해 여전히 필드 값을 직접 바꿀 수 있다.&#x20;

이를 막기 위해서, 접근 제한자를 이용해 직접 필드에 접근할 수 없도록 강제화 할 수 있다.

<mark style="background-color:yellow;">💡</mark>  <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">**접근제한자**</mark>

클래스 혹은 클래스의 멤버 참조연산자로 접근할 수 있는 <mark style="color:purple;">범위를 제한하기 위한 키워드</mark>

<table><thead><tr><th width="99.66665649414062">종류</th><th>역할</th></tr></thead><tbody><tr><td><strong>public</strong></td><td>모든 패키지에 접근 혀용</td></tr><tr><td><strong>protected</strong></td><td>동알 패키지에 접근 혀용. 단, 상속관계에 있는 경우 다른 패키지에서도 접근 가능</td></tr><tr><td><strong>default</strong></td><td>동일 패키지에서만 접근 혀용. ( 작성하지 않는 것이 default )</td></tr><tr><td><strong>private</strong></td><td>해당 클래스 내부에서만 접근 허용</td></tr></tbody></table>

위의 4가지 접근제한자는 클래스의 멤버(필드, 메소드)에 모두 사용 가능하다.\
✨ _<mark style="color:red;background-color:yellow;">단, 클래스 선언 시 사용하는 접근제한자는 public과 default만 사용 가능하다.</mark>_

{% code title="메서드 통해서만 값 변경 가능" %}
```java
// 멤버변수는 private
private String kinds;
private  int hp;

public void setKinds(String kinds){
    this.kinds = kinds;
}

// 메서드는 public
public  void setHp(int hp){
    if(hp > 0){
        this.hp = hp;
    }else{
        this.hp = 0;
    }
}

public String getInfo(){
    return "몬스터의 종류는 " + this.kinds + "이고, 체력은" + this.hp + "입니다.";
}
```
{% endcode %}

## 3️⃣ 추상화(abstraction)

객체를 설계하기 위해서는 복잡한 현실세계를 그대로 반영하기에는 너무 방대하고 복잡하기 때문에&#x20;_<mark style="color:purple;">현실 세계를 프로그램의 목적에 맞게 단순화하는 추상화라는 기법을 적용하게 된다.</mark>_

### 🤔 추상화란?

공통된 부분을 추출하고, 공통되지 않은 부분을 제거한다는 의미를 가지며, 추상화의 목적은 <mark style="background-color:yellow;">**유연성**</mark>을 확보하기 위함이다.\
유연성 확보는 여러 곳에 적용될 수 있는 유연한 객체를 의미하며, 즉 _<mark style="color:red;">재사용성이 높아질 수 있게 한다는 의미</mark>_&#xC774;다.\
객체의 재사용성이 증가하면 중복 작성되는 코드를 줄일 수 있으며, <mark style="background-color:green;">오류 발생 가능성을 감소시키고 유지보수성을 증가시킨다.</mark>



### ✏️추상화 기법을 활용한 객체 설계

#### 프로그램 개요

집사가 길냥이를 키우는 프로그램

#### 시스템 요구사항

```
/*  시스템 요구사항
* 1. 집사는 고양이에게 츄르 주기, 사료 주기, 놀아주기, 씻기기, 꼬리만지기 를 할 수 있다.
* 2. 고양이는 츄르 먹기, 사료 먹기, 놀기, 씻을 때 화내기?를 할 수 있다.
* 3. 츄르,사료를 먹거나 놀아주면 기분지수가 증가하고, 씻거나 꼬리를 만지면 기분지수가 감소한다.
* 3. 집사는 츄르를 5개 갖고 있고, 츄르가 동나면 사러나가야한다. 사료 또한 마찬가지이다.
* 4. 츄르와 사료가 없다면 집사는 고양이에게 츄르와 사료를 줄 수 없다.
* 5. 고양이의 기분이 나빠져서 기분지수가 음수가되면 고양이는 집을 나가버린다.
* 6. 고양이의 기분지수가 50이하라면 고양이를 씻길 수 없다.
* 7. 기분지수가 100이 되면 시스템은 종료하고 고양이는 당신을 좋아합니다로 마무리..
* */
```

#### 프로그램 설계하기

```
/* 프로그램 설계하기
* 1. 필요한 객체 도출
* - 플레이어(사용자), 집사, 고양이
*
* 2. 객체간 상호작용
* - 집사가 수신할 수 있는 메세지
* 1. 츄르를 고양이에게 주기
* 2. 사료를 고양이에게 주기
* 3. 고양이 놀아주기
* 4. 고양이 씻기기
* 5. 고양이 꼬리 만지기
* 6. 마트 다녀오기
*
* - 고양이가 수신할 수 있는 메세지
* 1. 츄르 먹고 기분지수 20 상승
* 2. 밥 먹구 기분지수 10 상승
* 3. 놀고 기분지수 15 상승
* 4. 씻김 당하고 기분지수 -20하락
* 5. 꼬리만집 당하고 기분지수 -10 하락
* 6. 집사가 마트가면 기분지수 -5 하락
* */
```

<details>

<summary>✏️ 실습 결과물</summary>

{% code title="CatParent" %}
```java
package com.ohgiraffers.practice.homecat;

public class CatParent {
    private final Cat cat = new Cat();
    private int churr;
    private int food;

    public CatParent(){
        this.churr = 3;
        this.food = 3;
    }
    public void giveChurr(){
        if(churr <= 0){
            System.out.println("츄르가 없습니다. 마트가서 사옵시다!");
        }
        cat.eatChurr();
    }

    public void giveFood(){
        if(food <= 0){
            System.out.println("사료가 없습니다. 마트가서 사옵시다!");
        }
        cat.eatFood();
    }

    public void showerCat(){
        cat.shower();
    }

    public void playCat(){
        cat.play();
    }

    public void touchCatTail(){
        cat.decreaseEmoRate(10, "꼬리를 만져서");
    }

    public void goMart(){
        cat.decreaseEmoRate(5, "마트를 가서");

        churr = 3;
        food = 3;
    }

    public boolean checkCatEmo(){
        cat.checkLike();

        if(cat.getemoRate() >= 100 || cat.getemoRate() < 0){
            return false;
        }

        return  true;
    }


```
{% endcode %}

{% code title="Cat.java" %}
```java
package com.ohgiraffers.practice.homecat;

public class Cat {
    private int emoRate;

    public Cat(){
        this.emoRate = 50;
    }

    public void eatChurr(){
        emoRate += 20;
        System.out.println("[system] 고양이가 츄르를 먹습니다!");

        printemoRate();
    }

    public void eatFood(){
        emoRate += 10;

        System.out.println("[system] 고양이가 밥을 먹습니다!");

        printemoRate();
    }

    public void play(){
        emoRate += 15;

        System.out.println("[system] 고양이가 쥐잡기 게임을 즐거워합니다!");

        printemoRate();
    }

    public void shower(){
        emoRate -= 20;

        System.out.println("[system] 고양이가 씻김 당하고 있습니다..");

        printemoRate();

    }

    public void decreaseEmoRate(int decrease,String action){
        this.emoRate -= decrease;
        System.out.println("[system] 고양이가 기분이 안좋아졌습니다....");
        printemoRate();

    }


    public void checkLike(){
        if(emoRate < 0){
            System.out.println("[system] 고양이가 집을 나갔습니다....");

        }else if(emoRate >= 100){
            System.out.println("[system] 고양이가 행복해 합니다~");

        }
    }

    public int getemoRate(){
        return emoRate;
    }

    private void printemoRate(){
        System.out.println("[system] 현재 고양이의 상태 = " + this.emoRate);
    }

}
```
{% endcode %}

{% code title="Application" %}
```java
CatParent catParent = new CatParent();

Scanner sc = new Scanner(System.in);

while (catParent.checkCatEmo()){
    System.out.println("========== 길냥이 키우기 프로그램 ==========");
    System.out.println("1. 츄르 주기");
    System.out.println("2. 밥 주기");
    System.out.println("3. 샤워 시키기");
    System.out.println("4. 놀아주기");
    System.out.println("5. 꼬리 만지기");
    System.out.println("9. 프로그램 종료");
    System.out.print("메뉴 선택 :");
    int no = sc.nextInt();


    switch (no){
        case 1: catParent.giveChurr(); break;
        case 2: catParent.giveFood();break;
        case 3: catParent.showerCat(); break;
        case 4: catParent.playCat(); break;
        case 5: catParent.touchCatTail(); break;
        case 6: catParent.goMart(); break;
        case 9:
            System.out.println("프로그램을 종료합니다.");break;
        default:
            System.out.println("잘못된 번호를 선택하셨습니다. "); break;
    }

    if(no == 9){
        break;
    }


```
{% endcode %}

</details>

## 4️⃣ DTO(Data Tranfer Object)

_캡슐화의 원칙에는 일부 어&#xAE0B;_&#xB098;긴 하지만 다른 목적을 가진 클래스와 객체를 추상화 하는 기법이 있다.\
<mark style="background-color:green;">**행위 위주가 아닌 데이터를 하나로 뭉치기 쉬운 객체(Data Transfer Object)**</mark>의 경우이다.\
이러한 객체를 설계할 때는 행위가 아닌 _<mark style="color:red;">데이터가 위주</mark>_&#xC774;며, <mark style="background-color:yellow;">캡슐화의 원칙을 준수</mark>하여\
<mark style="background-color:yellow;">모든 필드를 private로 직접 접근을 막</mark>고, 각 <mark style="background-color:yellow;">필드값을 변경하거나 반환하는 메소드를 세트로 미리 작성</mark>해둔다.\
어떤것을 쓸 줄 모르니 미리 다 준비해두는 종합선물세트 같은 개념이다.\
&#xNAN;_<mark style="color:purple;">private 필드와 필드값을 수정하는 설정자(setter), 필드에 접근하는 접근자(getter)들로 구성된다.</mark>_\
<mark style="color:green;">// 주로 계층간 데이터를 주고 받을 목적으로 사용한다.</mark>

### 1. 필드 구성하기

취급하려고 하는 정보를 고려해서 필드를 우선 작성  해 볼수있다.\
주로 화면(UI) 혹은 데이터베이스 테이블을 기준으로 한다.\
&#xNAN;_<mark style="color:purple;">객체가 가지는 속성(필드))를 추출하는 과정 또한 추상화라고 볼 수 있다.</mark>_

<mark style="color:red;background-color:yellow;">DTO클래스를 만들기 위해서는</mark> <mark style="color:red;background-color:yellow;"></mark><mark style="color:red;background-color:yellow;">**모든 필드**</mark><mark style="color:red;background-color:yellow;">를</mark> <mark style="color:red;background-color:yellow;"></mark><mark style="color:red;background-color:yellow;">**private**</mark><mark style="color:red;background-color:yellow;">로 만들어야한다.</mark>

{% code title="✅ Member DTO field" %}
```java
private int number;
private String name;
private int age;
private char gender;
private double height;
private double weight;
private boolean isActivated; // 회원탈퇴여부(활성화 여부)
```
{% endcode %}

이렇게 필드만 만들고 나면 <mark style="color:orange;">**private로 접근이 제한**</mark>되었기 때문에 _<mark style="color:orange;">각 영역에 접근을 할 수 없다.</mark>_\


<mark style="color:red;background-color:yellow;">public으로 접근을 허용하는 설정자/접근자를 이용</mark>해 필드에 <mark style="background-color:yellow;">**간접적으로 접근**</mark>할 수 있도록  해야한다.

### 2. 설정자/접근자 구성하기

설정자(setter)/접근자(getter)의 경우 실무에서 암묵적으로 통용되는 작성 규칙이 존재한다.

#### 설정자(setter)작성 규칙

필드값을 변경할 묵적의 매개변수를 변경하려는 필드와 같은 자료형으로 선언하고\
호출 당시 전달되는 매개변수의 값을 이용하여 필드의 값을 변경한다.

{% code title="⭐ [표현식 ]" %}
```java
public void set필드명(매개변수){
   필드 = 매개변수;
 }
```
{% endcode %}

{% code title="⭐[ 작성 예시 ]" %}
```java
public void setName(String name){
     this.name = name;
   }
```
{% endcode %}

#### 접근자(getter)작성 규칙

필드의 값을 반환받을 목적의 메소드 집합을 의미한다.\
각 접근자는 하나의 필드에만 접근하도록 한다.\
필드에 접근해서 기록된 값을 return을 이용하여 반환하며, 이 때 반환타입은 반환하려는 값의 자료형과 일치시킨다.

{% code title="⭐ [표현식]" %}
```java
public 반환형 get필드명(){
      return 반환값;
 }
```
{% endcode %}

{% code title="⭐ [작성 예시]" %}
```java
public void getName(){
      return this.name;
}
```
{% endcode %}

{% code title="✅ 예시 몇개만..!" %}
```java
public void setNumber(int number){
    this.number = number;
}

public void setName(String name){
    this.name = name;
}

public  void setAge(int age){
    this.age = age;
}

/*boolean의 접근자는 get으로 시작하지 않고 is로 시작하는 것이 일반적인 관례이다.*/
public boolean isActivated(){
    return isActivated;
}
```
{% endcode %}

## 5️⃣ 생성자

### 🤔  생성자란?

인스턴스를 생성할 때 초기 수행할 명령이 있는 경우 미리 작성해두고, _<mark style="color:purple;">인스턴스를 생성할 때 호출</mark>_&#xB41C;다.

\
생성자 함수에 <mark style="color:green;">매개변수가 없는 생성자</mark>를 <mark style="background-color:green;">**기본생성자(default constructor**</mark>)라고 하며,&#x20;기본생성자는 <mark style="color:red;background-color:yellow;">compiler에 의해 자동으로 추가</mark>되기 때문에 지금까지 명시적으로 작성하지 않고 사용할 수 있었다.\
&#xNAN;_&#xAE30;본생성자를 이용해 인스턴스를 생&#xC131;_&#xD558;게 되면 자바에서는 _자료형별 초기값을 이용해 필드를 초기화_ 한다.

{% code title="✅ 기본 생성자 호출" %}
```java
User user1 = new User();
System.out.println(user1.getInfomation());
```
{% endcode %}

\
필드의 초기값을 사용자가 원하는대로 설정하고 싶을 경우 <mark style="color:red;background-color:yellow;">생성자의 호출 시 인자로 값을 전달하여 호출</mark>할 수 있다.&#x20;이러한 <mark style="color:green;">인자를 받아 필드를 초기화</mark> 할 목적의 생성자를 <mark style="background-color:green;">**매개변수 있는 생성자**</mark>라고 한다.

{% code title="✅ 매개변수 있는 생성자 호출" %}
```java
// 일부만 초기화 되므로,
// 아래 생성자로 인해 초기화 되지 않은 값을 접근하려고 하면
// 오류가 날 수 있다.
User user2 = new User("user01", "pass01", "홍길동");
System.out.println(user2.getInfomation());
```
{% endcode %}

‼️하지만 _<mark style="color:red;">매개변수 있는 생성자가 한 개라도 존재하는 경우 compiler 기본 생성자를 자동으로 추가해주지 않는다.</mark>_\
✨ 매개변수 있는 생성자는 주로 <mark style="background-color:yellow;">**인스턴스 생성 시점**</mark><mark style="background-color:yellow;">에</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">**필드의 값**</mark><mark style="background-color:yellow;">을 사용자가</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">**원하는 대로 초기화**</mark> <mark style="background-color:yellow;"></mark><mark style="background-color:yellow;">할 목적으로 사용</mark>한다.

{% code title="✅ 모든 필드 초기화 생성자 호출" %}
```java
User user3 = new User("user02", "pass02", "이순신", new java.util.Date()); // java.util.Date를 통해서 현재 날짜로 초기화.
System.out.println(user3.getInfomation());
```
{% endcode %}

### 1. 생성자의 작성 위치

작성 위치는 문법상으로는 **클래스 내부**에 작성하면 되지만,\
통상적으로 **필드 선언부와 메소드 선언부 사이**에 작성하는 것이 관례이다.

### 2. 생성자의 사용 목적

1. <mark style="color:purple;">**인스턴스 생성 시점**</mark>에 수행할 명령이 있는 경우 사용한다.
2. 매개변수 있는 생성자의 경우 매개변수로 전달받은 값으로 **필드를 초기화** 하며 **인스턴스를 생성할 목적**으로 주로 사용된다.
3. 작성한 생성자 외에는 인스턴스를 생성하는 방법을 제공하지 않는다는 의미를 가진다.
4. 따라서, _<mark style="color:purple;">인스턴스를 생성하는 방법을 제한하기 위한 용도</mark>_&#xB85C; 사용할 수도 있다. <mark style="background-color:green;">(초기값 전달 강제화)</mark>

### 3. 생성자 작성 방법

{% code title="⭐ 표현식" %}
```java
접근제한자 클래스명(매개변수){
    인스턴스 생성 시점에 수행할 명령 기술(주로 필드를 초기화)
    this.필드명 = 매개변수; //설정자(setter) 여러 개의 기능을 한 번의 호출로 수행할 수 있다.
}
```
{% endcode %}

### 4. 생성자 작성 시 주의할 점

1. 생성자 메소드는 반드시 <mark style="color:red;background-color:yellow;">클래스의 이름과 동일</mark>해야 한다. (대/소문자까지 같아야함)
2. 생성자 메소드는 <mark style="color:red;background-color:yellow;">반환형을 작성하지 않는다</mark>. ( 작성하는 경우 생성자가 아닌 메소드로 인식한다. )

### 5. 생성자 사용예시

{% code title="1️⃣ 기본 생성자" %}
```java
public User(){
    /* 수행할 내용이 아무 것도 존재하지 않는다. */
    System.out.println("User 클래스의 기본 생성자 호출함...");
}

// 동일한 이름의 생성자 혹은 메소드를 한 클래스 안에서 작성하는 것은 불가능하다.
// public User(){자
```
{% endcode %}

{% code title="2️⃣ 매개변수 있는 생성자" %}
```java
/* 초기화할 필드가 여러개 인 경우, 초기화 하고 싶은 필드의 갯수별로 생성자를 여러 개 준비해둘 수 있다. */
/* id, pwd, name의 초기화를 담당할 생성자 */
public User(String id, String pwd, String name){

    /*  매개변수 있는 생성자의 주 목적은 인스턴스 생성 시점에 매개변수로 전달 받은 값을 이용해서 필드를 초기화한다. */
    this.id = id;
    this.pwd = pwd;
    this.name = name;

    System.out.println("User 클래스의 id, pwd, name을 초기화하는 생성자 호출함...");
}
```
{% endcode %}

{% code title="3️⃣ 모든 필드 초기화 생성자" %}
```java
public User(String id, String pwd, String name, java.util.Date enrollDate){

        /* 매개변수로 전달 받은 값을 이용해 모든 필드를 초기화한다. */
        /* 3-1. 각 필드에 접근하여 초기화 */
//        this.id = id;
//        this.pwd = pwd;
//        this.name = name;
//        this.enrollDate = enrollDate;

        /* 3-2. 사전에 작성되어 있는 다른 생성자 함수를 이용하여 초기화 */
        /* this() : 동일 클래스 내에 작성한 다른 생성자 메소드를 호출하는 구문이다.
        *           가장 첫 줄에 선언해야 한다.
        * */
        this(id, pwd, name); // 미리 작성한 세 개의 필드를 초기화하는 생성자로 매개변수로 받은 값을 전달
        this.enrollDate = enrollDate;

        System.out.println("User 클래스의 모든 필드를 초기화하는 생성자 호출함...");
    }
```
{% endcode %}



### 💡  생성자를 이용한 초기화 VS 설정자를 위한 초기화

#### 생성자를 이용한 초기화

**장점** : setter 메소드를 여러 번 호출해서 사용하지 않고 단 <mark style="color:red;">한번의 호출로 인스턴스를 생성 및 초기화</mark> 할 수 있다.\
**단점** : 필드를 초기화할 _<mark style="color:red;">매개변수의 갯수를 경우의 수 별로 모두 만들어둬야 한다.</mark>_\
호출 시 인자가 많아지는 경우 어떠한 값이 어떤 필드를 의미하는지 한 눈으로 보기 힘들다.

```java
UserDTO user1 = new UserDTO("ohgiraffers", "ohgiraffers","ohgiraffers", new java.util.Date());
System.out.println(user1.getInformation());
```

#### 설정자를 이용한 초기화

**장점** : 필드를 초기화하는 <mark style="color:red;">각각의 값들이 어떤 필드를 초기화하는지 명확하게 볼 수 있다.</mark>\
**단점** : 하나의 인스턴스를 생성할 때 <mark style="color:red;">한 번의 호출로 끝나지 않는다.</mark>

```java
UserDTO user2 = new UserDTO();
user2.setId("ohgiraffers");
user2.setPwd("ohgiraffers");
user2.setName("ohgiraffers");
user2.setEnrollDate(new java.util.Date());

System.out.println(user2.getEnrollDate());
```

## 6️⃣ 오버로딩

매개변수 부분의 타입, 갯수, 순서를 다르게 작성하면 서로 다른 메소드나 생성자로 인식하기 때문에&#x20;<mark style="background-color:yellow;">**동일한 이름의 생성자나 메소드를 여러 개 작성할 수 있는 것**</mark>을 오버로딩 이라고 한다.

#### 오버로딩의 사용 이유

_<mark style="color:orange;">매개변수의 종류 별로 메소드 내용을 다르게 작성 해야 하는 경우</mark>_&#xB4E4;이 종종 있다.\
이 때, 동일한 기능의 메소드를 매개변수에 따라 다르게 이름을 정의하면 복잡하고 관리하기가 매우 어렵다.\
따라서 <mark style="color:purple;">동일한 이름으로 다양한 종류의 매개변수에 따라 처리</mark>해야하는 여러 메소드를 동일한 이름으로 관리하기 위해\
사용하는 기술을 오버로딩이라고 한다.

#### 오버로딩의 조건

동일한 이름을 가진 메소드의 파라미터 선언부에 <mark style="color:green;background-color:green;">매개변수의 타입, 갯수, 순서를 다르게 작성</mark>하여&#x20;한 클래스 내에 동일한 이름의 메소드를 여러 게 작성할 수 있도록 한다.&#x20;<mark style="color:red;">**메소드의 시그니쳐**</mark><mark style="color:red;">가 다르면 다른 메소드로 인식</mark>하기 때문이다.\
즉, <mark style="background-color:yellow;">**시그니쳐 중 메소드 이름은 동일**</mark>해야 하기 때문에 파라미터 선언부가 다르게 작성되어야 오버로딩이 성립되다.

```java
 public void test() {}

//    public void test() {} /* 메소드의 시그니처가 동일하기 때문에 에러가 난다.*/
//    private void test() {} /* 접근 제한자는 메소드의 시그니처에 해당하지 않는다. */

//    public int test(){ return 0;} /* 반환형 또한 메소드 시그니처에 해당하지 않는다.*/

    public void test(int num){}
//    public void test(int num2){} /* 매개변수 이름은, 메소드 시그니처에 영향을 주지 않는다.*/

    public void test(int num1, int num2){} /* 매개변수 갯수에 따라 오버로딩이 성립*/

    public void test(int num1, String name){} /* 매개 변수 타입*/

    public void test(String name , int num1){} /* 매개 변수 순서 */
```

## 7️⃣ 매개변수

#### 매개변수(parameter)로 사용 가능한 자료형

1. 기본자료형
2. 기본자료형 배열
3. 클래스자료형
4. 클래스자료형 배열
5. 가변인자

#### 가변인자

`(자료형)...(매개변수명)` 을 이용해서 같은 자료형을 개수가 정해지지 않은 배열 형태를 매개변수를 사용할 수 있다.

```java
public void testVariableLengthArrayParameter(String name, String...hobby){
    System.out.println("이름 : " + name);
    System.out.println("취미의 갯수 : " + hobby.length);
    System.out.println("취미 : ");
    for(int i = 0; i < hobby.length; i ++){
        System.out.println(hobby[i] + " ");
    }
    System.out.println();
}
```

## 8️⃣ final

final은 종단의 의미를 가지는 키워드이다.

final 키워드를 사용할 수 있는 위치는 다양한 편이며 의미가 약간은 다르지만, 결국 <mark style="background-color:yellow;">**변경 불가의 의미**</mark>이다.

\
1\. **지역변수** : 초기화 이후 값 변경 불가\
2\. **매개변수** : 호출시 전달한 인자 변경 불가\
3\. **전역변수** : 인스턴스 생성 후 초기화 이후에 값 변경 불가\
4\. **클래스(static) 변수** : 프로그램 start 이후 값 변경 불가\
5\. **non-static 메소드** : 메소드 재작성(overriding) 불가\
6\. **static 메소드** : 메소드 재작성(overriding) 불가\
7\. **클래스** : 상속 불가



### 1. non-static field에 final 사용

{% code title="❌ 잘못된 사용" %}
```java
private final int nonStaticNum;
```
{% endcode %}

{% hint style="info" %}
final은 변경 불가의 의미를 가진다.\
따라서 초기 인스턴스가 생성되고 나면 기본값 0이 필드에 들어가게 되는데,\
그 초기화 이후 값을 변경할 수 없기 때문에 선언하면서 바로 초기화를 해주어야한다.
{% endhint %}

#### 💡<mark style="color:green;">해결하는 방법!</mark>

```
/* 1-1. 선언과 동시에 초기화 한다. */
private final int NON_STATIC_NUM = 1;

/* 1-2. 생성자를 이용해서 초기화 한다. */
private final  String NON_STATIC_NAME;

// 생성자를 이용해 필드를 초기화.
public FinalFieldTest(String nonStaticName){
    this.NON_STATIC_NAME = nonStaticName;
}
```

### 2. static field에 final 사용

static에도 자바에서 지정한 기본값이 초기에 대입되기 때문에&#x20;final 키워드 사용 시 초기화를 하지 않으면 에러가 발생한다.

```java
//    private static final int STATIC_NUM; // 자동으로 0으로 초기화됨
private static final int STATIC_NUM = 1; .// 선언과 함께 초기화 ⭕
```

#### ‼️<mark style="color:red;">생성자를 이용한 초기화는 불가능하다.</mark>

생성자는 인스턴스가 생성되는 시점에 호출이 되기 때문에 그 전에는 초기화가 일어나지 못한다.\
하지만 static은 프로그램이 start될 때 할당되기 때문에 초기화가 되지 않은 상태로 선언된 것과\
동일하여 기본값으로 초기화 된 후 값을 변경하지 못하기 때문에 에러가 발생한다.

```java
private static final double STATIC_DOUBLE;

//    public FinalFieldTest(double staticDouble){
//        FinalFieldTest.STATIC_DOUBLE = staticDouble;
//    }
```

## 9️⃣Singleton

### 🤔 싱글톤 패턴이란?

애플리케이션이 시작될 때 어떤 클래스가 최초 한 번만 메모리에 할당하고&#x20;그 메모리에 인스턴스를 만들어서 하나의 인스턴스를 공유해서 사용하며&#x20;메모리 낭비를 방지할 수 있게 함(매번 인스턴스 생성 하지 않음)

#### 장점

1. 첫 번째 이용 시에는 인스턴스를 생성해야 하므로 속도 차이가 나지 않지만   &#x20;두 번째 이용 시에는 인스턴스 생성 시간 없이 사용할 수 있다.
2. 인스턴스가 절대적으로 한 개만 존재하는 것을 보증할 수 있다.

#### 단점

1. 싱글톤 인스턴스가 너무 많은 일을 하거나 많은 데이터를 공유하면 결합도가 높아진다.
2. 동시성 문제를 고려해서 설계해야 하기 때문에 난이도가 있다.



### 싱글톤 구현 방법

#### 1. 이른 초기화 구현

```java
package com.ohgiraffers.section06.singleton;

public class EagerSingleton {

    private static EagerSingleton eager = new EagerSingleton();

    private EagerSingleton() {}

    public static EagerSingleton getInstance() {
        return eager;
    }
}
```

```java
EagerSingleton eager = new EagerSingleton(); // 생성자를 private으로 막았기 때문에 사용할 수 없다.

EagerSingleton eager1 = EagerSingleton.getInstance();
EagerSingleton eager2 = EagerSingleton.getInstance();

System.out.println(eager1.hashCode());
System.out.println(eager2.hashCode());
```

#### 2. 게으른 초기화 구현

```java
package com.ohgiraffers.section06.singleton;

public class LazySingleton {

    private static LazySingleton lazy;

    private LazySingleton() {}

    public static LazySingleton getInstance(){

        /* 인스턴스를 생성한 적이 없는 경우 인스턴스를 생성해서 반환하고
        *  생성한 인스턴스가 있는 경우 만들어둔 인스턴스를 반환한다. */
        if(lazy == null){
            lazy = new LazySingleton();
        }

        return lazy;
    }
}
```

```java
LazySingleton lazy1 = LazySingleton.getInstance();
LazySingleton lazy2 = LazySingleton.getInstance();

System.out.println(lazy1.hashCode());
System.out.println(lazy2.hashCode());
```

## 🔟 Static

정적 메모리 영역에 프로그램이 start 될 때 할당을 하는 키워드

<mark style="color:red;">**인스턴스를 생성하지 않고**</mark>도 <mark style="background-color:green;">사용할 클래스의 멤버(필드, 메소드)에 지정</mark>할 수 있다.\
여러 인스턴스가 공유해서 사용할 목적의 공간이다.\
하지만 static 키워드의 남발은 유지보스와 추적이 힘든 코드를 작성하는 피해야할 방식이다.\
명확한 목적이 존재하지 않는 이상 static 키워드 사용은 자제하자.\
의도적으로 static 키워드를 사용하는 대표적인 예는 singleton 객체를 생성할 때 이다.

### 1. static 키워드를 필드에서 사용

```java
package com.ohgiraffers.section06.statickeyword;

public class StaticFieldTest {

    private int nonStaticCount;

    private static int staticCount;

    public StaticFieldTest() {}

    public int getNonStaticCount(){
        return nonStaticCount;
    }

    /* statkc 필드에 접근하기 위해서는 클래스명.필드명으로 접근한다.*/
    public int getStaticCount(){
        return StaticFieldTest.staticCount;
    }

    /* 필드 값을 1씩 증가시키기 위한 메소드 */
    public void increaseNonStaticCount(){
        nonStaticCount ++;
    }

    public void increaseStaticCount(){
        StaticFieldTest.staticCount++;
    }
}
```

{% code title="✅ static 키워드를 필드에서 사용" %}
```java
StaticFieldTest sft1 = new StaticFieldTest();

System.out.println(sft1.getNonStaticCount());
System.out.println(sft1.getStaticCount());

sft1.increaseNonStaticCount();
sft1.increaseStaticCount();

System.out.println(sft1.getNonStaticCount());
System.out.println(sft1.getStaticCount());

StaticFieldTest sft2 = new StaticFieldTest();

System.out.println(sft2.getNonStaticCount());
System.out.println(sft2.getStaticCount()); // 값 유지
```
{% endcode %}

인스턴스 변수의 경우에는 sft1, sft2 두 개의 인스턴스가 서로 값을 공유하지 못하고&#x20;인스턴스를 생성할때마다 0으로 초기화 되었다.\
하지만 _<mark style="color:red;background-color:yellow;">static 필드의 경우에는 클래스 변수 자체가 프로그램을 종료할 때 까지 유지되고&#x20;있기 때문에 값을 유지하고 있다.</mark>_\
따라서 여러 개의 인스턴스가 같은 공간을 공유할 목적으로 필드에 static 키워드를 사용한다.

### 2. static 메소드 확인

```java
package com.ohgiraffers.section06.statickeyword;

public class StaticMethodTest {
    private int count;

    public void nonStaticMethod(){
        this.count ++;

        System.out.println("nonStaticMethod 호출됨...");
    }

    public static void staticMethod(){
//        this.count ++ ; // 인스턴스를 만들고 사용하는 메소드가 아니기 때문에 this는 사용할 수 없다.

        System.out.println("staticMethod 호출됨...");
    }

}
```

{% code title="✅ non-static 메소드 호출" %}
```java
StaticMethodTest smt = new StaticMethodTest();
smt.nonStaticMethod();
```
{% endcode %}

static method는 정적 영역에 두고 인스턴스를 생성하지 않고 호출할 목적으로&#x20;만들기 때문에 static 메소드를 호출하는 방식으로 호출해야 한다.

{% code title="❌ 권장하지 않음!" %}
```java
smt.staticMethod(); // 권장하지 않음
```
{% endcode %}

{% code title="✅ static 메소드 호출" %}
```java
StaticMethodTest.staticMethod(); // 권장함
```
{% endcode %}

## 11.  변수의 종류

### 필드

클래스 영역에 작성하는 변수를 뜻함.

필드 == 멤버변수(클래스가 가지는 멤버라는 의미) == 전역 변수(클래스 전역에서 사용할 수 있는 변수라는 의미)

### 인스턴스 변수

non-static field\
인스턴스 생성 시점에 사용 가능한 변수라는 의미

```java
private int globalNum;
```



### 클래스 변수

static field(정적 필드)\
정적(클래스) 영역에 생성되는 변수라는 의미

```java
private static int staticNum;
```

### 지역 변수

메소드 영역에서 작성하는 변수를 지역변수라고 한다.\
메소드의 괄호 안에 선언하는 변수를 매개변수라고 한다.\
매개변수도 일종의 지역변수로 생각하면 된다.\
<mark style="color:red;background-color:yellow;">지역변수와 매개변수 모두 호출 시 stack을 할당받아 stack에 생성된다.</mark>

```java
public void tesMethod(int num){ // 메소드 영역의 시작
        int localNum;

        System.out.println(num);

//        System.out.println(localNum); // 반드시 초기화가 되어야 사용할 수 있다.
        System.out.println(globalNum);
        System.out.println(staticNum);
    }
```

```java
public void testMethod2(){
// localNum은 다른 메소드 영역에 있기 때문에 사용할 수 없다.
//        System.out.println(localNum);

        System.out.println(globalNum);
        System.out.println(staticNum);
 }
```

## 12. 초기화 블럭

복잡한 초기화를 수행할 수 있는 블럭을 제공하며, 인스턴스 초기화 블럭과 정적 초기화 블럭으로 구분된다.

1\. 인스턴스 초기화 블럭

: 인스턴스가 생성되는 시점에 생성자 호출 이전에 먼저 실행이 된다.\
인스턴스를 호출하는 시점마다 호출이 된다.\
인스턴스 변수를 초기화하며 정적필드에는 실행시점마다 값을 덮어쓴다.



```
{
  초기화 내용 작성
}
```

\
2\. 정적 초기화 블럭

: 클래스가 로드 될 때 한 번 동작한다.\
정적 필드를 초기화하며, 인스턴스변수는 초기화하지 못한다.

```
static {
  초기화 내용 작성
}
```

### 1. 필드를 초기화 하지 않은 경우

JVM이 정한 기본값으로 객체가 생성된다.

```java
private String name;
private int price;
private static String brand;
```

### 2. 명시적 초기화

```java
private String name = "갤럭시";
private  int price = 10000000;
private static String brand = "삼송";
```

### 3. 인스턴스 초기화 블럭

<pre class="language-java"><code class="lang-java">{
<strong>        name = "사이언";
</strong>        price = 900000;
        brand = "사과";
        System.out.println("인스턴스 초기화 블럭 동작함..");
}

static {
/* static 초기화 블럭에서는 non-static 필드를 초기화하지 못한다. */
//        name = "아이펀";
//        pricc  = 1000000;
        brand = "헬지";
        System.out.println("정적 초기화 블럭 동작함..");
}

public Product() {}
</code></pre>

### 4. 매개변수 있는 생성자

위에서 초기화된 값을 다 무시하고 생성자에 작성한 초기화 내용으로 인스턴스를 초기화시킨다.

```java
public Product(String name, int price, String brand){
    this.name = name;
    this.price = price;
    Product.brand = brand;
    System.out.println("매개변수 있는 생성자 호출됨..");
}

public String getInformation(){

    return "Product [name=" + this.name + ", price=" + this.price  + ", brand=" + Product.brand + "]";
}
```



