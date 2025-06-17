# JPA

## 1. JPA(Java Persistence API)란?

* 자바 진영의 ORM(Object Relational Mapping)  기술 표준으로 ORM 기술을 사용하기 위한 표준 인터페이스의 모음

{% hint style="info" %}
**\[ORM] Object relational mapping** \
객체관계 매핑. 자바 플랫폼 SE와 EE를 사용하는 응용프로그램\
에서 객체는 객체 지향적으로 설계하고 관계형 데이터베이스는 관계형 데이터베이스의 패러다임대로 설\
계할 수 있도록 중간에서 매핑을 해주는 기술을 말한다.
{% endhint %}

## 2. JPA 특징

* 영속성 컨텍스트가 엔티티를 생명주기를 통해 관리한다.
* native SQL을 통해 직접 SQL을 해당 DB에 맞게 작성할 수 있다.
* DBMS별로 dialect를 제공한다.

<figure><img src=".gitbook/assets/image (88).png" alt=""><figcaption></figcaption></figure>

## 3. JPA 사용 이유

### 장점

* 객체지향과 관계지향이라는 서로 다른 패러다임 불일치를 해소 -> SQL 중심이 아닌 객체지향 패러다임 중심의 개발 가능
* 개발자가 SQL을 작성해주지 않아도 SQL문을 작성해줘서 생산성 향상
* SQL을 수정할 필요가 없으므로 필드 변경시 자동으로 SQL이 수정되므로 유지보수 굳
* DB의 종류에 따라 SQL문이 있는데 JPA는 이를 자동으로 작성해준다.
* 캐시를 활용한 성능 최적화로 트랜잭션을 처리하는 시간이 단축된다.

### 단점

* 복잡한 SQL을 작성하기에는 적합하지 않다.
* JPA를 제대로 이해하지 못하고 작성시 성능 저하가 발생할 수 있다.



### MYBatis와 JPA

* Mybatis는 SQL Mapper로 SQL Mapping을 사용하는 영속성(DB저장) 프레임워크.
* JPA는 ORM 기술

## 4. JPA 원리

Java 애플리케이션과 JDBC 사이에서 동작하며 내부적으로 JDBC API를 활용.

<figure><img src=".gitbook/assets/image (90).png" alt=""><figcaption></figcaption></figure>

JPA는 엔티티를 저장하는 환경인 영속성 컨텍스트(Persistence Context)를 통해 엔티티를 보관하고&#x20;관리한다.

### 엔티티의 영속성 컨텍스트(Persistence Context)에서의 생명주기

<figure><img src=".gitbook/assets/image (91).png" alt=""><figcaption></figcaption></figure>

* 엔티티 매니저가 엔티티를 저장하는 공간으로 엔티티를 보관하고 관리한다.
* 엔티티 매니저가 생성될 때 하나의 영속성 컨텍스트가 만들어 진다.
