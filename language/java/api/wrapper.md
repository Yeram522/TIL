# Wrapper

<table><thead><tr><th width="125.33331298828125">기본 타입</th><th width="141.99996948242188">레퍼 클래스</th></tr></thead><tbody><tr><td>byte</td><td>Byte</td></tr><tr><td>short</td><td>Short</td></tr><tr><td>int</td><td>Integer</td></tr><tr><td>long</td><td>Long</td></tr><tr><td>float</td><td>Float</td></tr><tr><td>double</td><td>Double</td></tr><tr><td>char</td><td>Character</td></tr><tr><td>boolean</td><td>Boolean</td></tr></tbody></table>

## 박싱(Boxing) 언박싱(unBoxing)

기본타입을 래퍼클래스의 인스턴스로 인스턴스화 하는 것을 박싱(Boxing)이라고 하며,\
래퍼클래스 타입의 인스턴스를 기본 타입으로 변경하는 것을 언박싱(UnBoxing)이라고 한다.

```java
int intValue = 20;
Integer boxingNumber1 = Integer.valueOf(intValue); // 박싱

int unBoxingNumber1 = boxingNumber1.intValue(); // 언박싱
```

### 오토 박싱과 오토 언박싱

```java
Integer boxingNumber2 = intValue;

int unBoxingNumber2 = boxingNumber2;
```

## Pharsing

문자열(String)값을 기본자료형 값으로 변경하는 것을 pharsing이라고 한다.

```java
byte b = Byte.parseByte("1");
short s = Short.parseShort("2");
int i = Integer.parseInt("4");
long l = Long.parseLong("8L"); // 8L은 안됨
float f = Float.parseFloat("4.0");// 4.0f는 됨!
double d = Double.parseDouble("8.0");
boolean b1 = Boolean.parseBoolean("true");

// ‼️ character는 parsing 기능을 제공하지 않는다.
char c = "abc".charAt(0);
```

## 기본 자료형 to 문자열

### valueOf()

기본자료형 값을 Warpper 클래스 타입으로 변환시키는 메소드

### toString()

필드 값을 문자열로 반환하는 메소드

```java
String b = Byte.valueOf((byte)1).toString();
String s = Short.valueOf((short)2).toString();
String i = Integer.valueOf(4).toString();
String l = Long.valueOf(8L).toString();
String f = Double.valueOf(8.0).toString();
String bl = Boolean.valueOf(true).toString();
String c = Character.valueOf('a').toString();

// String 클래스의 valueOf
String str = String.valueOf(10);

String str2 = 123 + "";
```

## java.time

`java.time.zone` : 시간대에 관련된 기능 제공

```
LocalTime, LocalDate, LocalDateTime, ZonedDateTime 클래스들이 있다.
```

```java
LocalTime timeNow = LocalTime.now();
System.out.println(timeNow);

LocalTime timeOf = LocalTime.of(18, 30, 0);
System.out.println(timeOf);

LocalDate dateNow = LocalDate.now();
System.out.println(dateNow);
LocalDate dateOf = LocalDate.of(2023,1,19);
System.out.println(dateOf);

LocalDateTime dateTimeNow = LocalDateTime.now();
System.out.println(dateTimeNow);

LocalDateTime dateTimeOf = LocalDateTime.of(dateNow, timeNow);
System.out.println(dateTimeOf);

ZonedDateTime zonedDateTimeNow = ZonedDateTime.now();
System.out.println(zonedDateTimeNow);

ZonedDateTime zonedDateTime = ZonedDateTime.of(dateOf, timeOf, ZoneId.of("Asia/Seoul"));
System.out.println(zonedDateTime);
```

{% code title="✅ 날짜 비교 연산자 이용 예시" %}
```java
LocalDate localDate = LocalDate.now();
LocalDateTime localDateTime = LocalDateTime.now();
ZonedDateTime zonedDateTime = ZonedDateTime.now();

LocalDate past = LocalDate.of(2020, 11, 11);
LocalDateTime future = LocalDateTime.of(2025, 12, 25,12,0,0);
ZonedDateTime now = ZonedDateTime.now();

System.out.println(localDate.isAfter(past));
System.out.println(localDateTime.isBefore(future));
System.out.println(zonedDateTime.isEqual(now));
```
{% endcode %}
