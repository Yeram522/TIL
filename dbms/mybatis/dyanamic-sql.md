---
description: 💡동적 쿼리를 작성하는 실습의 과정을 정리한 글이다.
---

# Dyanamic SQL

## 1️⃣ config directory

설정 파일을 모아둔 디렉토리. java 에서는 main의 resources 디렉토리 하위에 위치한다.

<figure><img src="../../.gitbook/assets/image (83).png" alt=""><figcaption></figcaption></figure>

### `connection-info.properties`&#x20;

db와 연결하기 위한 driver, url, username,password가 저장되어있다.

```xml
driver=com.mysql.cj.jdbc.Driver
url=jdbc:mysql://localhost/menudb
username=myiaong
password=myiaong
```

### `mybatis-config.xml`&#x20;

#### XML 선언부

```xml
xml<?xml version="1.0" encoding="UTF-8" ?><!DOCTYPE configuration        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"        "https://mybatis.org/dtd/mybatis-3-config.dtd">
```

* XML 문서의 버전과 인코딩을 지정
* DOCTYPE으로 MyBatis 설정 파일임을 명시하고 DTD(Document Type Definition) 위치를 지정

#### `<configuration>` 태그

MyBatis 설정 파일의 최상위 루트 요소입니다. 모든 설정은 이 태그 안에 포함되어야 합니다.

#### `<properties>` 태그

```xml
xml<properties resource="config/connection-info.properties"/>
```

* **역할**: 외부 properties 파일에서 설정값을 불러옵니다
* **resource 속성**: 클래스패스 기준으로 properties 파일의 경로를 지정
* **목적**: DB 연결 정보 등을 외부 파일로 분리하여 보안성과 유지보수성을 높입니다
* **사용 예**: `${driver}`, `${url}` 등으로 참조 가능

#### `<typeAliases>` 태그

```xml
xml<typeAliases>    <typeAlias type = "com.ohgiraffers.common.SearchCriteria" alias="SearchCriteria"/></typeAliases>
```

* **역할**: 자주 사용하는 클래스의 전체 패키지명을 단축 별명으로 지정
* **type 속성**: 실제 클래스의 전체 경로(FQCN)
* **alias 속성**: 매퍼 파일에서 사용할 별명
* **효과**: `com.ohgiraffers.common.SearchCriteria` 대신 `SearchCriteria`만 사용 가능

#### `<environments>` 태그

```xml
xml<environments default="dev">    <environment id="dev">        <transactionManager type="JDBC"/>        <dataSource type="POOLED">            <property name="driver" value="${driver}"/>            <property name="url" value="${url}"/>            <property name="username" value="${username}"/>            <property name="password" value="${password}"/>        </dataSource>    </environment></environments>
```

#### `<environments>` 속성

* **default 속성**: 기본으로 사용할 환경을 지정 (여기서는 "dev")

#### `<environment>` 태그

* **id 속성**: 환경의 고유 식별자
* **용도**: 개발(dev), 테스트(test), 운영(prod) 등 다양한 환경별 설정 가능

#### `<transactionManager>` 태그

* **type="JDBC"**: JDBC의 기본 트랜잭션 관리 방식 사용
* **다른 옵션**: MANAGED (컨테이너가 트랜잭션 관리)

#### `<dataSource>` 태그

* **type="POOLED"**: 커넥션 풀을 사용하는 데이터소스
* **다른 옵션**:
  * UNPOOLED: 매번 새로운 커넥션 생성
  * JNDI: JNDI를 통한 데이터소스 조회

#### `<property>` 태그들

* **driver**: JDBC 드라이버 클래스명
* **url**: 데이터베이스 연결 URL
* **username**: DB 사용자명
* **password**: DB 비밀번호
* `${}` 문법으로 properties 파일의 값을 참조

### `<mappers>` 태그

```xml
xml<mappers>    <package name = "com.ohgiraffers.section01.xml"/></mappers>
```

* **역할**: SQL 매퍼 파일들의 위치를 지정
* **package 속성**: 지정된 패키지 내의 모든 매퍼 인터페이스를 자동으로 등록
* **다른 방식**:
  * `<mapper resource="경로"/>`: 개별 XML 파일 지정
  * `<mapper class="클래스명"/>`: 개별 인터페이스 지정

이 설정 파일을 통해 MyBatis는 데이터베이스 연결, 트랜잭션 관리, 매퍼 등록 등을 자동으로 처리할 수 있다.



## 2️⃣ Templete

```java
public class Template {

    public static SqlSessionFactory sqlSessionFactory;
    public static SqlSession getSqlSession(){

        if(sqlSessionFactory == null){
            String resource = "config/mybatis-config.xml";
            InputStream inputStream = null;
            try {
                inputStream = Resources.getResourceAsStream(resource);
                sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
            } catch (IOException e) {
                throw new RuntimeException(e);
            }
        }

        return  sqlSessionFactory.openSession(false);
    }
}
```
