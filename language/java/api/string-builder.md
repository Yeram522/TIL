# String Builder

## StringBuffer

**스레드 동기화 기능 제공** 함.\
성능면에서는 StringBuilder 보다 느림.

## StringBuilder

**스레드 동기화 기능 제공하지 않음.**\
스레드 동기화 처리를 고려하지 않는 상황에서 StringBuffer보다 성능이 좋음.

```java
StringBuilder sb1 = new StringBuilder("javaoracle");
```

### delete()

시작 인덱스와 종료 인덱스를 이용해서 문자열에서 원하는 부분의 문자열을 제거한다.

### deleteCharAt()&#x20;

문자열 인덱스를 이용해서 문자 하나를 제거한다.\


<mark style="color:orange;">‼️</mark>_<mark style="color:orange;">둘 다 원본에 영향을 미친다.</mark>_

```java
System.out.println("delete() : " + sb1.delete(2,5)); // jaracle
System.out.println("deleteCharAt() : " + sb1.deleteCharAt(0)); // aracle
System.out.println(sb1); // aracle
```

### insert()

인자로 전달된 값을 문자열로 변환 후 지정한 인덱스 위치에 추가한다.

_<mark style="color:orange;">‼️원본에 영향을 미친다.</mark>_

```java
System.out.println("insert() : " + sb1.insert(1,"vao"));//avaoracle
System.out.println("insert() : " + sb1.insert(0, "j"));//javaoracle
System.out.println("insert() : " + sb1.insert(sb1.length(), "jdbc"));//javaoraclejdbc

System.out.println(sb1);//javaoraclejdbc
```

### reverse()

문자열 인덱스 순번을 역순으로 재배열한다.

‼️원본에 영향을 미친다.

```java
System.out.println(sb1.reverse());// cbdjelcaroavaj
System.out.println(sb1);// cbdjelcaroavaj
```
