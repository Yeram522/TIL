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

## 5. Persistence Context

<figure><img src=".gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

**Persistence Context**는 엔티티를 영구 저장하는 환경으로, 엔티티 매니저를 통해 엔티티를 저장하거나 조회하면 해당 엔티티는 영속성 컨텍스트에 보관되고 관리됩니다.

### 1. 엔티티의 생명주기

```
비영속(new/transient) → 영속(managed) → 준영속(detached) → 삭제(removed)
```

### 2. 1차 캐시 (First Level Cache)

#### 1차 캐시란?

* **영속성 컨텍스트 내부에 있는 캐시**
* Map\<Key, Value> 구조로 되어 있음
* Key: @Id로 매핑한 식별자
* Value: 해당 엔티티 인스턴스

#### 1차 캐시의 동작 방식

```java
java// 엔티티를 영속성 컨텍스트에 저장 (1차 캐시에 저장됨)Member member = new Member();member.setId("member1");member.setUsername("회원1");em.persist(member);// 1차 캐시에서 조회 (SQL 쿼리 실행되지 않음)Member findMember = em.find(Member.class, "member1");
```

#### 1차 캐시의 이점

1. **성능 향상**: 같은 트랜잭션 내에서 동일한 엔티티 조회 시 DB에 접근하지 않음
2. **동일성 보장**: 같은 엔티티에 대해 항상 같은 인스턴스 반환
3. **변경 감지**: 엔티티의 변경사항을 자동으로 감지

#### 1차 캐시 조회 과정

```
1. em.find(Member.class, "member1") 호출2. 1차 캐시에서 엔티티 조회 시도3-1. 있으면: 1차 캐시에서 반환3-2. 없으면: 데이터베이스에서 조회 → 1차 캐시에 저장 → 반환
```

### 3. Flush (플러시)

#### Flush란?

**영속성 컨텍스트의 변경 내용을 데이터베이스에 반영하는 것**

* 영속성 컨텍스트를 비우는 것이 아님
* 변경 사항을 데이터베이스에 동기화하는 과정

#### Flush 동작 과정

1. **변경 감지 (Dirty Checking)**
2. **수정된 엔티티를 쓰기 지연 SQL 저장소에 등록**
3. **쓰기 지연 SQL 저장소의 쿼리를 데이터베이스에 전송**

#### Flush 발생 시점

```java
java// 1. 직접 호출em.flush();// 2. 트랜잭션 커밋 시 자동 호출transaction.commit();// 3. JPQL 쿼리 실행 시 자동 호출List<Member> members = em.createQuery("select m from Member m", Member.class)                        .getResultList();
```

#### Flush 모드 설정

```java
java// AUTO: 커밋이나 쿼리 실행 시 플러시 (기본값)em.setFlushMode(FlushModeType.AUTO);// COMMIT: 커밋할 때만 플러시em.setFlushMode(FlushModeType.COMMIT);
```

### 4. Commit (커밋)

#### Commit이란?

**트랜잭션의 변경 사항을 데이터베이스에 영구적으로 반영하는 것**

#### Commit 과정

```java
javaEntityTransaction transaction = em.getTransaction();transaction.begin(); // 트랜잭션 시작// 엔티티 등록Member member = new Member("member1", "회원1");em.persist(member);// 엔티티 수정member.setUsername("수정된회원1");transaction.commit(); // 트랜잭션 커밋
```

#### Commit 시 내부 동작

1. **Flush 자동 호출**
2. **실제 데이터베이스 트랜잭션 커밋**

## 6. Mapping

### 1. 기본 매핑 어노테이션

#### @Entity와 @Table&#x20;

```java
@Entity
@Table(name="users") // 테이블명 지정
public class User{
    // ...
}
```

#### @ID와 기본키 생성 전략(Strategy)

```java
@Entity
public class User{
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY) //AUTO_INCREMENT
    private Long id;
```

### 2. 컬럼 매핑

#### @Column\`

```java
@Entity
public class User {
    @Column(name = "user_name", nullable = false, length = 50)
    private String username;
    
    @Column(unique = true)
    private String email;
    
    @Column(columnDefinition = "TEXT")
    private String description;
}
```

### 3. 연관관계 매핑

#### 일대일(One-to-One)

```java
// 주 테이블에 외래키
@Entity
public class User {
    @OneToOne(cascade = CascadeType.ALL)
    @JoinColumn(name = "profile_id")
    private Profile profile;
}

@Entity
public class Profile {
    @OneToOne(mappedBy = "profile")
    private User user;
}
```

#### 다대일(Many-to-One) / 일대다(One-to-Many)

```java
// 다대일 (외래키를 가진 쪽)
@Entity
public class Order {
    @ManyToOne
    @JoinColumn(name = "user_id")
    private User user;
}

// 일대다 (외래키를 가지지 않은 쪽)
@Entity
public class User {
    @OneToMany(mappedBy = "user", cascade = CascadeType.ALL)
    private List<Order> orders = new ArrayList<>();
}
```

✅ Cascade Type\
`CascadeType.ALL`  : 모든 영속성 연산이 전이된다.

```java
@Entity
public class User {
    @OneToMany(mappedBy = "user", cascade = CascadeType.ALL)
    private List<Order> orders = new ArrayList<>();
}

// 사용 예시
User user = new User();
Order order1 = new Order();
Order order2 = new Order();
user.addOrder(order1); // 연관관계 편의 메서드
user.addOrder(order2);

em.persist(user); // user와 함께 order1, order2도 자동으로 저장됨
em.remove(user);  // user와 함께 order1, order2도 자동으로 삭제됨
```

`CascadeType.PERSIST` : 저장 시에만 전이된다.

```java
@Entity
public class User {
    @OneToMany(mappedBy = "user", cascade = CascadeType.PERSIST)
    private List<Order> orders = new ArrayList<>();
}

User user = new User();
user.addOrder(new Order());

em.persist(user); // order도 함께 저장됨
em.remove(user);  // order는 삭제되지 않음 (PERSIST만 전이)
```

`CascadeType.MERGE` : 병합 시에만 전이된다.

```java
@Entity
public class User {
    @OneToMany(mappedBy = "user", cascade = CascadeType.MERGE)
    private List<Order> orders = new ArrayList<>();
}

// 준영속 상태의 엔티티를 다시 영속 상태로 만들 때
User detachedUser = // ... 준영속 상태의 user
User mergedUser = em.merge(detachedUser); // order들도 함께 병합됨
```

✅ Fetch Type

`FetchType.EAGER`  : 즉시 로딩

엔티티를 조회할 때 연관된 엔티티도 함께 조회한다.

`FetchType.LAZY`  : 지연 로딩

실제 사용될 때까지 로딩을 지연시킨다.



## 7. JPQL(Java Persistence Query Language)&#x20;

### 1. 기본 JPQL - TypedQuery 사용

#### 개념

* JPQL은 JPA에서 제공하는 객체지향 쿼리 언어
* SQL과 유사하지만 엔티티 객체를 대상으로 쿼리를 작성
* TypedQuery는 타입 안전성을 보장하는 쿼리 인터페이스

#### 코드 예시

```java
public String selectSingleMenuByTypedQuery(){
    String jpql = "SELECT m.menuName FROM Section01Menu as m WHERE m.menuCode = 8";
    TypedQuery<String> query = entityManager.createQuery(jpql, String.class);
    String resultMenuName = query.getSingleResult();
    
    return resultMenuName;
}
```

#### 주요 특징

* **TypedQuery**: 반환 타입을 명시하여 컴파일 타임에 타입 체크
* **getSingleResult()**: 정확히 하나의 결과만 반환 (0개 또는 2개 이상이면 예외 발생)
* **getResultList()**: 여러 개의 결과를 List로 반환
* **별칭(alias) 사용**: `Section01Menu as m` - 쿼리 작성을 간편하게 함

***

### 2. 매개변수 바인딩 JPQL

#### 개념

* 동적으로 값을 전달받아 쿼리를 실행하는 방식
* SQL Injection 공격을 방지하고 쿼리 재사용성을 높임
* 위치 기반 매개변수(?1, ?2, ...)와 이름 기반 매개변수(:paramName) 지원

#### 코드 예시

```java
public List<Menu> selectMenuBybindingPosition(String menuName){
    String jpql = "SELECT m FROM Section02Menu m WHERE m.menuName = ?1";
    List<Menu> resultMenuList = entityManager.createQuery(jpql, Menu.class)
            .setParameter(1, menuName)
            .getResultList();
    return resultMenuList;
}
```

#### 주요 특징

* **위치 기반 매개변수**: `?1`, `?2` 순서대로 번호 매김
* **setParameter()**: 매개변수 값을 바인딩
* **메소드 체이닝**: 여러 메소드를 연속으로 호출 가능
* **타입 안전성**: Menu.class로 반환 타입 명시

#### SQL Injection 방지

**SQL Injection**은 악의적인 사용자가 입력값을 통해 SQL 쿼리를 조작하여 데이터베이스를 공격하는 기법입니다.

**위험한 방식 (문자열 연결)**

```java
// 절대 사용하면 안 되는 방식!
String jpql = "SELECT m FROM Menu m WHERE m.menuName = '" + menuName + "'";
// 만약 menuName = "'; DROP TABLE Menu; --" 라면?
// 실제 쿼리: SELECT m FROM Menu m WHERE m.menuName = ''; DROP TABLE Menu; --'
```

**안전한 방식 (매개변수 바인딩)**

```java
// 안전한 방식
String jpql = "SELECT m FROM Menu m WHERE m.menuName = ?1";
query.setParameter(1, menuName); // JPA가 자동으로 이스케이프 처리
```

**매개변수 바인딩의 보안 장점:**

* JPA가 자동으로 특수문자를 이스케이프 처리
* 사용자 입력값이 쿼리 구조를 변경할 수 없음
* PreparedStatement 사용으로 SQL 파싱 최적화

#### 이름 기반 매개변수 예시

```java
// 이름 기반 매개변수 사용법
String jpql = "SELECT m FROM Menu m WHERE m.menuName = :menuName";
List<Menu> results = entityManager.createQuery(jpql, Menu.class)
        .setParameter("menuName", menuName)
        .getResultList();
```

***

### 3. Projection (프로젝션)

#### 개념

**Projection**은 SELECT 절에서 조회할 대상을 지정하는 것을 의미합니다. 전체 엔티티가 아닌 필요한 데이터만 선택적으로 조회할 수 있는 기능입니다.

#### Projection의 4가지 종류

**1. 스칼라 프로젝션 (Scalar Projection)**

**개념**: 기본 데이터 타입(String, Integer, Long 등)을 직접 조회

```java
// 단일 컬럼 조회
"SELECT m.menuName FROM Menu m"

// 여러 컬럼 조회 (Object[] 반환)
"SELECT m.menuName, m.menuPrice FROM Menu m"
TypedQuery<Object[]> query = em.createQuery(jpql, Object[].class);
```

**특징**:

* 가장 빠른 성능 (필요한 컬럼만 조회)
* 영속성 컨텍스트 관리 대상 아님
* 단순한 데이터 조회에 적합

**2. 엔티티 프로젝션 (Entity Projection)**

**개념**: JPA 엔티티 객체 전체를 조회

```java
"SELECT m FROM Menu m"
TypedQuery<Menu> query = em.createQuery(jpql, Menu.class);
```

**특징**:

* 모든 컬럼을 조회 (성능상 불리할 수 있음)
* 영속성 컨텍스트에서 관리됨 (변경 감지, 지연 로딩 등 가능)
* CRUD 작업이 필요한 경우에 사용

**3. 임베디드 타입 프로젝션 (Embedded Type Projection)**

**개념**: @Embeddable로 정의된 값 타입 객체를 조회

```java
@Embeddable
public class Address {
    private String city;
    private String street;
    private String zipcode;
}

// 임베디드 타입 조회
"SELECT m.address FROM Member m"
```

**특징**:

* 복합키 용도가 아닌 **값 타입 집합**을 표현
* 주소, 좌표, 기간 등 관련된 데이터를 하나로 묶어 재사용
* 영속성 컨텍스트 관리 대상 아님 (값 타입이므로)

**4. 생성자 프로젝션 (Constructor Projection)**

**개념**: new 명령어를 사용해 DTO 객체를 생성하며 조회

```java
// DTO 클래스
public class MenuDTO {
    private String menuName;
    private int menuPrice;
    
    public MenuDTO(String menuName, int menuPrice) {
        this.menuName = menuName;
        this.menuPrice = menuPrice;
    }
}

// JPQL에서 생성자 프로젝션 사용
"SELECT new com.example.MenuDTO(m.menuName, m.menuPrice) FROM Menu m"
```

#### 코드 예시

```java
@Transactional
public List<Menu> singleEntityProjection(){
    List<Menu> menuList = projectionRepository.singleEntityProjection();
    
    // 영속성 컨텍스트에 관리되는 엔티티이므로 변경 감지 가능
    menuList.get(0).setMenuName("맛있는 삼겹살");
    
    return menuList;
}
```

#### 주요 특징

* **엔티티 프로젝션**: 조회된 엔티티는 영속성 컨텍스트에 의해 관리됨
* **변경 감지**: @Transactional 하에서 엔티티 변경 시 자동으로 UPDATE 쿼리 실행
* **성능 최적화**: 필요한 컬럼만 조회하여 네트워크 비용과 메모리 사용량 절약

#### 생성자 프로젝션을 사용하는 이유

**DTO 사용의 장점**

1. **성능 최적화**: 필요한 데이터만 조회하여 네트워크 비용과 메모리 사용량 절약
2. **보안**: 민감한 정보를 제외하고 필요한 데이터만 노출
3. **계층 분리**: 엔티티는 영속성 계층에서만 사용, DTO는 프레젠테이션 계층에서 사용
4. **API 응답 최적화**: JSON 응답 시 불필요한 데이터 제외

**실무 활용 예시**

```java
// 사용자 목록 조회 API - 비밀번호 등 민감 정보 제외
"SELECT new com.example.UserDTO(u.id, u.username, u.email) FROM User u"

// 대시보드용 통계 데이터
"SELECT new com.example.SalesDTO(s.date, s.totalAmount, s.orderCount) FROM Sales s"

// 검색 결과용 간단한 정보
"SELECT new com.example.ProductSummaryDTO(p.name, p.price, p.thumbnailUrl) FROM Product p"
```

**4가지 프로젝션 비교표**

| 프로젝션 타입  | 반환 타입           | 영속성 컨텍스트 관리 | 성능  | 사용 용도            |
| -------- | --------------- | ----------- | --- | ---------------- |
| **스칼라**  | 기본 타입/Object\[] | ❌           | ⭐⭐⭐ | 단순 데이터 조회, 통계    |
| **엔티티**  | 엔티티 객체          | ✅           | ⭐   | CRUD 작업, 비즈니스 로직 |
| **임베디드** | @Embeddable 객체  | ❌           | ⭐⭐  | 값 타입 집합 조회       |
| **생성자**  | DTO 객체          | ❌           | ⭐⭐⭐ | API 응답, 화면 표시용   |

#### 임베디드 타입 상세 설명

임베디드 타입은 **복합키 용도가 아닌** 관련된 속성들을 하나의 값 타입으로 묶어서 재사용하는 목적입니다.

```java
@Entity
public class Member {
    @Id
    private Long id;
    
    @Embedded
    private Address homeAddress;  // 집 주소
    
    @Embedded
    private Address workAddress;  // 직장 주소
}

@Embeddable
public class Address {
    private String city;
    private String street;
    private String zipcode;
    
    // 비즈니스 로직도 포함 가능
    public String getFullAddress() {
        return city + " " + street + " " + zipcode;
    }
}
```

**임베디드 타입의 장점:**

* 코드 재사용성 향상
* 응집도 높은 객체 설계
* 의미 있는 메소드 추가 가능
* 데이터베이스 테이블 구조는 그대로 유지

***

### 4. Paging (페이징)

#### 개념

대용량 데이터를 효율적으로 조회하기 위해 결과를 나누어 가져오는 기법입니다. 전체 데이터를 한 번에 로드하지 않고 필요한 만큼만 조회하여 메모리 사용량과 응답 시간을 최적화합니다.

#### 코드 예시

```java
public List<Menu> usingPagingAPI(int offset, int limit){
    String jpql = "SELECT m FROM Section04Menu m ORDER BY m.menuCode DESC";
    List<Menu> pagingMenuList = entityManager.createQuery(jpql, Menu.class)
            .setFirstResult(offset)  // 조회를 시작할 위치(0부터 시작)
            .setMaxResults(limit)    // 조회할 데이터의 개수
            .getResultList();
    
    return pagingMenuList;
}
```

#### 주요 특징

* **setFirstResult(offset)**: 조회 시작 위치 설정 (0-based index)
* **setMaxResults(limit)**: 최대 조회할 레코드 수 제한
* **ORDER BY**: 페이징 시 정렬 기준 필수 (일관된 결과를 위해)
* **성능 최적화**: 데이터베이스 레벨에서 LIMIT/OFFSET 쿼리로 변환

#### 페이징 계산 예시

```java
// 페이지 번호로 offset 계산
int pageNumber = 2;  // 2페이지
int pageSize = 10;   // 페이지당 10개
int offset = (pageNumber - 1) * pageSize;  // offset = 10

// 실제 사용
List<Menu> page2Menus = usingPagingAPI(offset, pageSize);
```

#### 실무 활용 팁

* **총 개수 조회**: 페이징과 함께 전체 데이터 개수도 조회하여 총 페이지 수 계산
* **인덱스 활용**: ORDER BY 절에 사용되는 컬럼에 인덱스 생성 권장
* **Spring Data JPA**: Pageable 인터페이스로 더 편리한 페이징 지원



### 5. Group Functuon(그룹 함수)

```java
public Long otherWithNoResult(int categoryCode){
    String jpql = "SELECT SUM(m.menuPrice) FROM Section05Menu m WHERE m.categoryCode = :categoryCode";
    /* COUNT 외의 다른 그룹함수는 결과 값이 없을 경우 Null이 반환되기 때문에 기본 자료형으로 다를 경우 문제가 생긴다.
     *  Long과 같이 Wrapper 클래스 자료형으로 다루어주어야 한다. */
    Long sumOfMenu = entityManager.createQuery(jpql, Long.class)
            .setParameter("categoryCode", categoryCode)
            .getSingleResult();
    return sumOfMenu;
}
```



### 6. Join

```java
public List<Menu> selectByInnerJoin(){
        String jpql = "SELECT m FROM Section06Menu m JOIN m.category c";
        List<Menu> menuList = entityManager.createQuery(jpql, Menu.class).getResultList();

        return menuList;
    }

    public List<Object[]> selectByOuterJoin(){
        String jpql = "SELECT m.menuName , c.categoryName FROM Section06Menu m RIGHT JOIN m.category c" +
                " ORDER BY m.category.categoryCode";

        List<Object[]> menuList = entityManager.createQuery(jpql).getResultList();
        return menuList;
    }

    public List<Menu> selectByFetchJoin(){
        /* FETCH : JPQL 에서 성능 최적화를 위해 제공하는 기능으로 연과 된 엔티티나 컬렉션을 한번에 조회한다.
        *  지연 로딩이 아닌 즉시 로등을 수행한다. */
        String jpql = "SELECT m FROM Section06Menu m JOIN FETCH m.category c";

        List<Menu> menuList = entityManager.createQuery(jpql, Menu.class).getResultList();
        return menuList;
    }

    public List<Object[]> selectByCollectionJoin(){
        String jpql = "SELECT m.menuName , c.categoryName FROM Section06Category c RIGHT JOIN c.menuList m" +
                " ORDER BY m.category.categoryCode";

        List<Object[]> categoryList = entityManager.createQuery(jpql).getResultList();
        return categoryList;
    }
```

***

## 8. Native Query

### 1. Native Query 란?

SQL 쿼리를 그대로 사용하는 것을 말한다. 이를 사용하면 ORM의 기능을 이용하면서도 SQL 쿼리도 활용할 수 있어서 더욱 강력한 데이터베이스 접근이 가능하다. 따라서 복잡한 쿼리를 작성할 때나, 특정 데이터베이스에서만 사용 가능한 기능을 사용해야할 때 등에 Native query를 사용한다.

### 2. Native Query의 API 3가지

#### 결과 타입 정의

`public Query createNativeQuery(String sqlString, Class resultClass)`

사용자 정의 타입으로 결과 타입을 정의 했을 때, 모든 칼럼값을 매핑하는 경우에만 타입을 특정할 수 있다. 일부 칼럼만 조회할 경우에는 Object\[]또는 스칼라 값을 별도로 담을 클래스를 정의해야한다.

```java
public Menu nativeQueryByResultType(int menuCode) {
 String query
 = "SELECT" +
 " menu_code, menu_name, menu_price, category_code, orderable_status"
 " FROM tbl_menu" +
 " WHERE menu_code = ?";
 Query nativeQuery
 = manager.createNativeQuery(query, Menu.class)
 .setParameter(1, menuCode);
 return (Menu) nativeQuery.getSingleResult();
}
```

#### 결과 타입을 정의할 수 없을 때

`public Query createNativeQuery(String sqlString)`

엔티티의 일부 컬럼만 조회할 경우 결과 타입을 특정할 수 없으므로 Object\[] 타입을 사용한다.

```java
public List<Object[]> nativeQueryByNoResultType() {
 String query = "SELECT menu_name, menu_price FROM tbl_menu";
 return manager.createNativeQuery(query).getResultList();
}
```

#### 결과 매핑 사용

`public Query createNativeQuery(String sqlString, String resultsetMapping)`

다른 엔터티와 함께 조회하고 싶을 때는 `@SqlResultSetMapping` 어노테이션을 이용해 네이티브 쿼리의 결과를 매핑할 수 있다.

```java
@SqlResultSetMappings(
value=
 {
 /* 자동 엔티티 매핑 : @Column으로 매핑 설정이 되어 있는 경우 사용 */
@SqlResultSetMapping(
// 결과 매핑 이름
name = "categoryCountAutoMapping",
// @EntityResult를 사용해서 엔티티를 결과로 매핑
entities = {@EntityResult(entityClass = Category.class)},
// @ColumnResult를 사용해서 컬럼을 결과로 매핑
columns = {@ColumnResult(name = "menu_count")}
)
}
)
```

```java
public List<Object[]> nativeQueryByAutoMapping() {
 String query
 = "SELECT a.category_code, a.category_name, a.ref_category_code," +
 " COALESCE(v.menu_count, 0) menu_count" +
 " FROM tbl_category a" +
 " LEFT JOIN (SELECT COUNT(*) AS menu_count, b.category_code" +
 " FROM tbl_menu b" +
 " GROUP BY b.category_code) v ON (a.category_code = v.category_code)" +
 " ORDER BY 1";
  Query nativeQuery
 = manager.createNativeQuery(query, "categoryCountAutoMapping");
 return nativeQuery.getResultList();
}
```

```java
@DisplayName("자동 결과 매핑을 사용한 Native Query 조회 테스트")
@Test
public void testNativeQueryByAutoMapping() {
 //given
 //when
 List<Object[]> categoryList
 = nativeQueryRepository.nativeQueryByAutoMapping();
 //then
 Assertions.assertNotNull(categoryList);
 categoryList.forEach(
 row -> {
 for(Object col : row) {
 System.out.print(col + "/");
 }
 System.out.println();
 }
 );
}
```
