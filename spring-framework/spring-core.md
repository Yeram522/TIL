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
