---
icon: '1'
---

# JAVA에서 DB 연결하기

## 1️⃣ Connection과 DriverManager로 연결법

JAVA의 `java.sql` 패키지를 이용해 데이터베이스와 연동할 수 있다.

`java.sql` 패키지는 `Connection` 과 `DriverManager` 을 제공한다.

DriverManager class 에서는 `getConnection` 메서드를 지원하여, 데이터베이스 서버 주소, Id, password를 통해 데이터베이스에 연결시킨다.

```java
@CallerSensitive
public static Connection getConnection(String url,
    String user, String password) throws SQLException {
    java.util.Properties info = new java.util.Properties();

    if (user != null) {
        info.put("user", user);
    }
    if (password != null) {
        info.put("password", password);
    }

    return (getConnection(url, info, Reflection.getCallerClass()));
}
```

그리고, 반환 값으로 Connection 객체를 받음으로써, 잘 연결 되었는지 확인할 수 있다.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

{% code title="✅ 드라이버 등록" %}
```java
Class.forName("com.mysql.cj.jdbc.Driver");
```
{% endcode %}

`Class.forName()` 메서드를 이용해서 드라이버를 등록하는데, 아래 그림에 보이는 위치의 드라이버의 경로를 입력해서 등록할 수 있다.

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

드라이버 등록을 한 후에, `DriverManager` 은 우리가 지정한 데이터베이스와    자바를 연결시키는데, 해당 드라이버를 build.gradle의 의존성에 추가해주어야지 `Class.getName()` 함수로 드라이버를 등록한 후 연결할 수 있다.

실제로 의존성에 추가해주면,  위의   폴더 그림과 같이 외부 라이브러리에 사용할 데베 파일이 들어간 것을 볼 수 있다.

{% code title="✅ DriverManager를 이용해 Connection 생성" %}
```java
Connection con = null;
con = DriverManager.getConnection("jdbc:mysql://localhost/employeedb", "ohgiraffers", "ohgiraffers");
```
{% endcode %}



위에서 설명한 대로 실제 JAVA  코드를 작성하면 다음과 같다.

```java
package com.ohgiraffers.section01.connection;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class Application1 {

    public static void main(String[] args) {

        /* ✅ DB 접속을 위한 Connection Instance 생성 */
        Connection con = null;

        /* ✅ 사용할 Driver 등록 */
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");

            /* ✅ DriverManager를 이용해 Connection 생성 */
            con = DriverManager.getConnection("jdbc:mysql://localhost/employeedb", "ohgiraffers", "ohgiraffers");

            System.out.println("con = " + con);

        } catch (ClassNotFoundException e) {
            throw new RuntimeException(e);
        } catch (SQLException e) {
            throw new RuntimeException(e);
        } finally {
            if(con!= null){
                try {
                    con.close();
                } catch (SQLException e) {
                    throw new RuntimeException(e);
                }
            }
        }

    }
}
```

## 2️⃣ Properties 객체를 이용한 연결

데이터 베이스를 연결할 때마다, `url` , `id` , `pwd` 를 계속 입력하는것은 가시성도 좋지 않고 오타로 인한  오류가 발생할 가능성이 높다.

```java
DriverManager.getConnection("jdbc:mysql://localhost/employeedb", "ohgiraffers", "ohgiraffers");
```

`.properties` 파일을 불러와, `Properties` 객체에 담아 안정적으로  입력 값을 다룰 수 있다.

### properties 확장자

`.properties` 확장자를 가진 파일은 `key` = `value` 의 형태로 데이터를 저장한다. 우리는 아까의 입력 데이터들을 다음과 같이 properties 파일에 저장할 수 있다.

{% code title="connection-info.properties" %}
```properties
driver = com.mysql.cj.jdbc.Driver
url = jdbc:mysql://localhost/employeedb
user = ohgiraffers
password = ohgiraffers
```
{% endcode %}

이렇게 저장한 파일은 JAVA 에서는 `FileReader` 객체를 이용해 불러올 수 있다.

```java
Properties prop = new Properties(); // Properties 인스턴스 생성

// Exception 오류 처리는 코드에 포함하지 않음!
prop.load(new FileReader("src/main/java/com/ohgiraffers/config/connection-info.properties"));
```

{% code title="✅ proerties 파일에서 불러온 키:값은 Properties 객체에 저장되고, get 메서드를 통해 불러올 수 있다." %}
```java
String driver = prop.getProperty("driver");
String url = prop.getProperty("url");
String user = prop.getProperty("user");
String password = prop.getProperty("password");
```
{% endcode %}

이후에는 Properties 객체에서 불러온 값들을 사용해 드라이버를 연결할 수 있다.

```java
Class.forName(driver);

con = DriverManager.getConnection(url, user, password);
```



## 3️⃣ Templete을 이용한 연결

위와 같은 일련의 과정들을 템플릿화 시켜서 메서드를 이용해 간단한 코드로 데이터베이스를 연결시킬 수 있다.

{% code title="✅ File을 읽어 데베 계정정보를  Properties로 변환한뒤, 데이터베이스 연결 수립 " %}
```java
// class JDBCTemplate
public static Connection getConnection(){
    Connection con = null;

    Properties prop = new Properties();

    try {
        prop.load(new FileReader("src/main/java/com/ohgiraffers/config/connection-info.properties"));

        String driver = prop.getProperty("driver");
        String url = prop.getProperty("url");

        Class.forName(driver);

        con = DriverManager.getConnection(url, prop);

    } catch (IOException e) {
        throw new RuntimeException(e);
    } catch (ClassNotFoundException e) {
        throw new RuntimeException(e);
    } catch (SQLException e) {
        throw new RuntimeException(e);
    }

    return con;
}
```
{% endcode %}

{% code title="✅ null 혹은 아직 닫히지 않았다면 Connection을 닫아주는 메서드" %}
```java
public static void close(Connection con){
        try {
            if(con != null && !con.isClosed()){
                con.close();
            }
        } catch (SQLException e) {
            throw new RuntimeException(e);
        }
    }
```
{% endcode %}



그 결과 main에서는 간단한 호출만으로 데이터베이스와의 연결, 연결 끊기를 할 수 있다.

```java
package com.ohgiraffers.section02.template;

import java.sql.Connection;

import static com.ohgiraffers.section02.template.JDBCTemplate.close;
import static com.ohgiraffers.section02.template.JDBCTemplate.getConnection;


public class Application {

    public static void main(String[] args) {

        Connection con = getConnection();
        System.out.println("con = " + con);
        close(con);
    }
}
```
