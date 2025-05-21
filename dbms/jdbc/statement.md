---
icon: '2'
---

# Statement로 데이터 조회하기

## 1️⃣ Statement

`Statement` 는 쿼리문을 저장하고 실행하는 기능을 하는 용도의 인터페이스이다.

```java
import java.sql.Statement;
```

`ResultSet` 는 select 결과 집합을 받아올 용도의 인터페이스이다.

```java
import java.sql.ResultSet;
```

💡 모두 `java.sql` 라이브러리 소속이다!

```java
Statement stmt = null;

ResultSet rset = null;
```

{% code title="✅ connection을 이용해서 statement 인스턴스를 생성해준다." %}
```java
Connection con = getConnection();

stmt = con.createStatement();

// 쿼리문을 .executeQuery 메서드를 이용해 전달 후 결과 얻기.
rset = stmt.executeQuery("SELECT EMP_ID, EMP_NAME FROM EMPLOYEE");

/* next() : ResultSet의 커서 위치를 하나 내리면서 행이 존재하면 true, 존재하지 않으면 false를 반환*/
while (rset.next()){
    System.out.println(rset.getString("EMP_ID") + ", " + rset.getString("EMP_NAME"));
}
```
{% endcode %}

{% code title="✅ String 변수를 이용해 query문 안에 변수를 넣을 수도 있다." %}
```java
String empId = "202";
String query = "SELECT EMP_ID, EMP_NAME FROM EMPLOYEE WHERE EMP_ID = '" + empId + "'";

rset = stmt.executeQuery(query);
```
{% endcode %}

{% code title="✅ Scanner로 입력 받는 예시" %}
```java
stmt = con.createStatement();

Scanner sc = new Scanner(System.in);
System.out.print("조회할 사번을 입력해주세요: ");
String empId = sc.nextLine();
String query = "SELECT EMP_ID, EMP_NAME FROM EMPLOYEE WHERE EMP_ID = '" + empId + "'";

System.out.println("query = " + query);

rset = stmt.executeQuery(query);

if(rset.next()){
    System.out.println(rset.getString("EMP_ID")+ ", " + rset.getString("EMP_NAME"));
}
```
{% endcode %}

### DTO 를 이용해 쿼리 결과를 객체에 넣기

```java
stmt = con.createStatement();
rset = stmt.executeQuery(query);

if(rset.next()){
    selectedEmp = new EmployeeDTO();

    selectedEmp.setEmpId(rset.getString("EMP_ID"));
    selectedEmp.setEmpName(rset.getString("EMP_NAME"));
    selectedEmp.setEmpNo(rset.getString("EMP_NO"));
    selectedEmp.setEmail(rset.getString("EMAIL"));
    selectedEmp.setPhone(rset.getString("PHONE"));
    selectedEmp.setDeptCode(rset.getString("DEPT_CODE"));
    selectedEmp.setJobCode(rset.getString("JOB_CODE"));
    selectedEmp.setSalLevel(rset.getString("SAL_LEVEL"));
    selectedEmp.setSalary(rset.getInt("SALARY"));
    selectedEmp.setBonus(rset.getDouble("BONUS"));
    selectedEmp.setManagerId(rset.getString("MANAGER_ID"));
    selectedEmp.setHireDate(rset.getDate("HIRE_DATE"));
    selectedEmp.setEntDate(rset.getDate("ENT_DATE"));
    selectedEmp.setEntYn(rset.getString("ENT_YN"));
```

## 2️⃣ Prepared Statement

```java
import java.sql.PreparedStatement;
```

prepared Statement는 두 단계로 동작한다.

1. 쿼리 준비(Preparation) : 데이터베이스에 실행할 쿼리 템플릿을 미리 전송하고 SQL 구문을 컴파일해서 준비. SQL 구문과 데이터 값이 분리 되고 쿼리 자체는 미리 컴파일 되기 때문에 효율적으로 처리된다.
2. 바인딩(Binding)과 실행(Execition): 준비된 쿼리에 데이터를 바인딩하고 실행. 바인딩되는 데이터 값은 쿼리 구문에 직접 포함되지 않으므로 SQL Injection 공격 방지 가능!

때문에, Prepared Statement는 반복적으로 실행되는 쿼리에 대해 성능을 최적화하고 보안을 강화할 수 있다. (💡 일회성 쿼리에는 부적합할 수 있다. )

```java
Connection con = getConnection();

PreparedStatement pstmt = null;

ResultSet rset = null;

try {
    pstmt = con.prepareStatement("SELECT EMP_ID, EMP_NAME FROM EMPLOYEE");

    rset = pstmt.executeQuery();

    while (rset.next()){
        System.out.println(rset.getString("EMP_ID") + ", " + rset.getString("EMP_NAME"));
    }

} catch (SQLException e) {
    throw new RuntimeException(e);
} finally {
    close(pstmt);
    close(rset);
    close(con);
}
```

### XML 파일을 이용한 쿼리 전송

XML 파일에 쿼리를 미리 작성하고, 파일에서 해당 쿼리를 불러와 쿼리 구문을 전송할 수 있다.

{% code title="employee-query.xml" %}
```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<!DOCTYPE properties SYSTEM "http://java.sun.com/dtd/properties.dtd">
<properties>
    <entry key="selectEmpByFamilyName">
        SELECT E.*
          FROM EMPLOYEE E
         WHERE E.EMP_NAME LIKE CONCAT(?,'%')
    </entry>
</properties>
```
{% endcode %}

```java
Properties prop = new Properties();

prop.loadFromXML(new FileInputStream("src/main/java/com/ohgiraffers/section02/preparedstatement/employee-query.xml"));

String query = prop.getProperty("selectEmpByFamilyName"); // query key name

System.out.println("query = " + query);

pstmt = con.prepareStatement(query);
pstmt.setString(1, empName); // setString을 이용해 XML에 있는 ?에 차례대로 입력 값을 넣어줄 수 있다.
```
