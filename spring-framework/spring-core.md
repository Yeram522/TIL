# Spring Core

## 1️⃣ IoC(Inversion of Control)

**IoC = 제어의 역전**이라는 뜻. 쉽게 말하면 "누가 객체를 만들고 관리하느냐"의 주도권이 바뀐 것이다.

#### 기존 방식 (개발자가 제어)

```java
public class BookService {    
    private BookDAO bookDAO;        
    
    public BookService() {        
        // 개발자가 직접 객체 생성과 의존성을 제어        
        this.bookDAO = new BookDAOImpl();    
    }
    
}
```

#### IoC 방식 (컨테이너가 제어)

```java
@Service
public class BookService {
    @Autowired
    private BookDAO bookDAO; // Spring 컨테이너가 객체 생성과 주입을 제어
}
```

### IoC 컨테이너란?

IoC 컨테이너는 \*\*"객체들의 생명주기와 의존성을 관리해주는 관리자"\*\*라고 생각하면 됨.

#### 컨테이너가 하는 일들:

1. **객체 생성** (빈 생성)
2. **의존성 주입** (DI - Dependency Injection)
3. **생명주기 관리** (초기화, 소멸)
4. **설정 관리**

### 구체적인 동작 과정

#### 1. 빈 등록 단계

```java
// Spring이 이런 어노테이션들을 스캔해서 빈으로 등록
@Repository
public class BookDAOImpl implements BookDAO { ... }

@Service  
public class BookService { 
    @Autowired
    private BookDAO bookDAO;
}

@Controller
public class BookController {
    @Autowired 
    private BookService bookService;
}
```

**컨테이너 내부 상황:**

```
IoC Container
├── bookDAOImpl (BookDAO 타입)
├── bookService (BookService 타입)  
└── bookController (BookController 타입)
```

#### 2. 의존성 해결 단계

```java
// Spring 컨테이너가 내부적으로 하는 일 (의사코드)
public class SpringContainer {
    private Map<String, Object> beans = new HashMap<>();
    
    public void createBeans() {
        // 1. 객체들 생성
        BookDAOImpl bookDAO = new BookDAOImpl();
        BookService bookService = new BookService();
        BookController bookController = new BookController();
        
        // 2. 의존성 주입
        bookService.setBookDAO(bookDAO);        // @Autowired 처리
        bookController.setBookService(bookService); // @Autowired 처리
        
        // 3. 컨테이너에 보관
        beans.put("bookDAOImpl", bookDAO);
        beans.put("bookService", bookService);  
        beans.put("bookController", bookController);
    }
}
```

### 실제 예시로 이해하기

#### 전통적인 방식 (No IoC)

```java
public class BookController {
    private BookService bookService;
    
    public BookController() {
        // 내가 직접 다 만들어야 함
        BookDAO bookDAO = new BookDAOImpl();
        this.bookService = new BookService(bookDAO);
    }
    
    public String getBooks() {
        return bookService.selectAllBooks();
    }
}
```

**문제점:**

* `BookController`가 `BookService`, `BookDAO`의 생성 방법을 다 알아야 함
* 의존성이 복잡해질수록 생성자가 지저분해짐
* 테스트하기 어려움

#### IoC 컨테이너 방식

```java
@Controller
public class BookController {
    @Autowired
    private BookService bookService; // 컨테이너가 알아서 주입
    
    public String getBooks() {
        return bookService.selectAllBooks();
    }
}
```

**장점:**

* `BookController`는 자신의 역할(웹 요청 처리)에만 집중
* 객체 생성과 의존성 관리는 컨테이너가 담당
* 테스트할 때 쉽게 Mock 객체 주입 가능

### Spring IoC 컨테이너의 종류

#### 1. BeanFactory

```java
// 가장 기본적인 컨테이너 (잘 직접 사용하지 않음)
BeanFactory factory = new XmlBeanFactory(new FileSystemResource("beans.xml"));
BookService service = (BookService) factory.getBean("bookService");
```

#### 2. ApplicationContext (주로 사용)

```java
// 더 많은 기능을 제공하는 컨테이너
ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
// 또는 어노테이션 기반
ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);

BookService service = context.getBean(BookService.class);
```

### 컨테이너 설정 방법

#### 1. XML 설정

```xml
<!-- applicationContext.xml -->
<beans>
    <bean id="bookDAO" class="com.example.BookDAOImpl"/>
    <bean id="bookService" class="com.example.BookService">
        <property name="bookDAO" ref="bookDAO"/>
    </bean>
</beans>
```

#### 2. Java 설정 (현재 주류)

```java
@Configuration
public class AppConfig {
    
    @Bean
    public BookDAO bookDAO() {
        return new BookDAOImpl();
    }
    
    @Bean  
    public BookService bookService() {
        return new BookService(bookDAO());
    }
}
```

#### 3. 어노테이션 설정 (가장 편함)

```java
@ComponentScan("com.example") // 이 패키지 하위를 스캔
@Configuration
public class AppConfig {
    // @Service, @Repository, @Controller 어노테이션을 자동으로 찾아 빈 등록
}
```

### 컨테이너의 생명주기

```java
public class MyService {
    
    @PostConstruct  // 빈 생성 후 초기화
    public void init() {
        System.out.println("MyService 초기화됨");
    }
    
    @PreDestroy     // 빈 소멸 전 정리작업
    public void cleanup() {
        System.out.println("MyService 정리됨");
    }
}
```

## 2️⃣ Annotation 방식

### Annotation 종류 정리

<table><thead><tr><th width="148">어노테이션</th><th>역할</th><th>비고</th></tr></thead><tbody><tr><td><code>@Configuration</code></td><td>해당 클래스가 설정파일이 되고, 빈을 생성하는 클래스임을 표기</td><td></td></tr><tr><td><code>@Bean</code></td><td>해당 메소드의 반환 값을 스프링 컨테이너에 빈으로 등록</td><td>이름을 별도로 지정하지 않으면 메소드 이름을 bean의 id로 자동 인식(<code>@Bean("myName")</code> 또는 <code>@Bean(name="myName")</code>)의 형식으로 설정 가능</td></tr><tr><td><code>@ComponentScan</code></td><td>basePackage로 설정 된 하위 경로에 특정 어노테이션을 가지고 있는 클래스를 bean으로 등록하는 기능</td><td><p></p><ul><li>basePackage를 설정하지 않으면 기본적으로 설정 파일과 동일한 패키지에 있는 bean만 탐색</li></ul><ul><li>@Component 어노테이션이 작성 된 클래스를 인식으로 bean으로 등록</li><li>특수 목적에 따라 세부 기능을 제공하는 @Controller, @Service, @Repository, @Cofiguration 등을 사용</li></ul></td></tr><tr><td><code>@Service</code></td><td></td><td></td></tr><tr><td><code>@Autowired</code></td><td></td><td></td></tr></tbody></table>

## 3️⃣ Dependency Injection(의존성 주입)

### 1. Field 주입

```java
@Service("bookServiceField")
public class BookService {

    /* BookDAO 타입의 빈 객체를 이 프로퍼티에 자동으로 주입해준다.*/
    @Autowired
    private BookDAO bookDAO;

    public List<BookDTO> selectAllBooks(){
        return bookDAO.selectBookList();
    }

    public BookDTO searchBookBySequence(int sequnce){
        return bookDAO.selectOneBook(sequnce);
    }
}
```

{% code title="✅ main 메서드에서 scan 기능을 통해 context를 가져오고, getBean을 이용해 BookService를 가져오므로써, BookService의 멤버변수인 BookDAO를 @Autowired 어노테이션을 통해 BookDAO 빈 객체를 자동 주입 시켜준다." %}
```java
ApplicationContext context =
        /* 컴포넌트 스캔기능을 활성화시키는 또 다른 방법이다.*/
        new AnnotationConfigApplicationContext("com.ohgiraffers.section01");

BookService bookService = context.getBean("bookServiceField", BookService.class);
```
{% endcode %}

### 2. Constructor 주입

{% code title="✅ @Service를 이용해 scanner가 스캔할 수 있도록 등록." %}
```java
@Service("bookServiceConstructor")
public class BookService {
    /* ...생략...*/
}
```
{% endcode %}

{% code title="✅ 생성자 쪽에 @autowired 어노테이션을 붙여서 생성자 주입을 받을 수 있게 함." %}
```java
private final BookDAO bookDAO;

@Autowired
public BookService(BookDAO bookDAO){
    this.bookDAO = bookDAO;
}
```
{% endcode %}

{% hint style="warning" %}
생성자가 하나만 있으면 @AutoWired 어노테이션을 생략해도, 생성자 주입을 받을 수 있다. 하지만 생성자가 여러개 있으면 어노테이션 없이 생성자 주입을 받을 수 없다.
{% endhint %}

#### 😀 생성자 주입의 장점

* 객체가 생성 될 때 모든 의존성이 주입 되므로 의존성을 보장 할 수 있다.
  * 순환 참조 에 대해 필드 주입/세터 주입은 메소드 실행 시점에 오류가 발생한다.
  * 생성자 주입은 어플리케이션 실행 시점에 오류가 발생한다.
* 객체의 불변성을 보장할 수 있다.
  * 필드에 'final' 사용 가능하고 객체 생성 이후 의존성을 변경할 수 없어 안정성이 보장된다.
* 코드 가독성이 좋다
  * 해당 객체가 어떤 의존성을 가지고 있는지 명확히 알 수 있다.

### &#x20;3. Setter 주입

😒setter은 final을 사용할 수 없다. ( 불변성을 보장할 수 없기 때문! )

```java
@Service("bookServiceSetter")
public class BookService {

    /* setter은 final을 사용할 수 없다ㅠ 불변성 보장 ❌*/
    private BookDAO bookDAO;

    /* BookDAO 타입의 빈 객체를 setter에 자동으로 주입해준다. */
    @Autowired
    public void setBookDAO(BookDAO bookDAO){
        this.bookDAO = bookDAO;
    }

    public List<BookDTO> selectAllBooks(){

        return bookDAO.selectBookList();
    }

    public BookDTO searchBookBySequence(int sequence){

        return bookDAO.selectOneBook(sequence);
    }
}
```

### 4️⃣ Annotation

{% code title="✅ @Component 어노테이션으로 클래스를 bean으로 등록할 수 있다." %}
```java
@Component
public class Charmander implements Pokemon {

    @Override
    public void attack() {
        System.out.println("파이리 불꽃 공격 🔥🔥");
    }
}
```
{% endcode %}

따라서 Service class에서도 직접 객체를 생성하지 않아도 되서 의존성을 줄일 수 있다.

```java

@Service("pokemonServicePrimary")
public class PokemonService {

    private Pokemon pokemon;

    @Autowired
    public PokemonService(Pokemon pokemon){ 
        this.pokemon = pokemon;
    }


    public void pokemonAttack(){
        pokemon.attack();
    }
}
```

#### @Primary

같은 interface를 구현한 클래스 여러개가 bean에 등록되어 있다면, Spring은 어떤 구현체를 주입할 지 알 수 없다. 따라서 `@Primary`  어노테이션을 사용해서 우선적으로 어떤 구현체를 주입할지 결정 할 수 있다.

`@Primary` 어노테이션을 사용하지 않는다면, 아래와 같은 오류를 볼 수 있다.

```java
Caused by: org.springframework.beans.factory.NoUniqueBeanDefinitionException: No qualifying bean of type 'com.ohgiraffers.section02.common.Pokemon' available: expected single matching bean but found 3: charmander,pikachu,squirtle
```

