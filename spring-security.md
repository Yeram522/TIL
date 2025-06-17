# Spring Security

## Spring Security 개념 정리

### Spring Security란?

Spring Security는 Spring 기반 애플리케이션의 보안을 담당하는 프레임워크입니다. 인증(Authentication)과 인가(Authorization)를 핵심으로 하여 웹 애플리케이션과 메소드 레벨의 보안을 제공합니다.

### 핵심 개념

#### 인증 (Authentication)

사용자가 누구인지 확인하는 과정입니다. 일반적으로 사용자명과 비밀번호를 통해 이루어집니다.

#### 인가 (Authorization)

인증된 사용자가 특정 리소스에 접근할 권한이 있는지 확인하는 과정입니다.

#### 주요 구성요소

**SecurityContext**: 현재 보안 컨텍스트에 대한 정보를 담고 있습니다.

**Authentication**: 사용자의 인증 정보를 나타내는 객체입니다.

**GrantedAuthority**: 사용자에게 부여된 권한을 나타냅니다.

**UserDetails**: 사용자 정보를 담는 인터페이스입니다.

**AuthenticationManager**: 인증을 처리하는 핵심 인터페이스입니다.

### 기본 설정 예시

#### 의존성 추가 (Maven)

```xml
xml<dependency>    <groupId>org.springframework.boot</groupId>    <artifactId>spring-boot-starter-security</artifactId></dependency>
```

#### 기본 보안 설정

```java
java@Configuration@EnableWebSecuritypublic class SecurityConfig {    @Bean    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {        http            .authorizeHttpRequests(authz -> authz                .requestMatchers("/", "/home", "/public/**").permitAll()                .requestMatchers("/admin/**").hasRole("ADMIN")                .anyRequest().authenticated()            )            .formLogin(form -> form                .loginPage("/login")                .defaultSuccessUrl("/dashboard")                .permitAll()            )            .logout(logout -> logout                .logoutSuccessUrl("/")                .permitAll()            );                return http.build();    }    @Bean    public PasswordEncoder passwordEncoder() {        return new BCryptPasswordEncoder();    }}
```

#### 사용자 정의 UserDetailsService

```java
java@Servicepublic class CustomUserDetailsService implements UserDetailsService {        @Autowired    private UserRepository userRepository;        @Override    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {        User user = userRepository.findByUsername(username)            .orElseThrow(() -> new UsernameNotFoundException("User not found: " + username));                return User.builder()            .username(user.getUsername())            .password(user.getPassword())            .authorities(user.getRoles().stream()                .map(role -> new SimpleGrantedAuthority("ROLE_" + role.getName()))                .collect(Collectors.toList()))            .build();    }}
```

#### 컨트롤러에서 보안 적용

```java
java@RestController@RequestMapping("/api")public class ApiController {        @GetMapping("/public")    public String publicEndpoint() {        return "This is a public endpoint";    }        @GetMapping("/user")    @PreAuthorize("hasRole('USER')")    public String userEndpoint() {        return "This requires USER role";    }        @GetMapping("/admin")    @PreAuthorize("hasRole('ADMIN')")    public String adminEndpoint() {        return "This requires ADMIN role";    }        @GetMapping("/current-user")    public String getCurrentUser(Authentication authentication) {        return "Current user: " + authentication.getName();    }}
```

#### JWT 토큰 기반 인증 예시

```java
java@Componentpublic class JwtAuthenticationFilter extends OncePerRequestFilter {        @Autowired    private JwtTokenProvider tokenProvider;        @Autowired    private CustomUserDetailsService userDetailsService;        @Override    protected void doFilterInternal(HttpServletRequest request,                                   HttpServletResponse response,                                   FilterChain filterChain) throws ServletException, IOException {                String token = getTokenFromRequest(request);                if (token != null && tokenProvider.validateToken(token)) {            String username = tokenProvider.getUsernameFromToken(token);            UserDetails userDetails = userDetailsService.loadUserByUsername(username);                        UsernamePasswordAuthenticationToken authentication =                 new UsernamePasswordAuthenticationToken(userDetails, null, userDetails.getAuthorities());                        SecurityContextHolder.getContext().setAuthentication(authentication);        }                filterChain.doFilter(request, response);    }        private String getTokenFromRequest(HttpServletRequest request) {        String bearerToken = request.getHeader("Authorization");        if (bearerToken != null && bearerToken.startsWith("Bearer ")) {            return bearerToken.substring(7);        }        return null;    }}
```

### 메소드 레벨 보안

```java
java@Configuration@EnableGlobalMethodSecurity(prePostEnabled = true)public class MethodSecurityConfig {        @Bean    public MethodSecurityExpressionHandler methodSecurityExpressionHandler() {        DefaultMethodSecurityExpressionHandler handler = new DefaultMethodSecurityExpressionHandler();        return handler;    }}@Servicepublic class DocumentService {        @PreAuthorize("hasRole('ADMIN') or #document.owner == authentication.name")    public void deleteDocument(Document document) {        // 문서 삭제 로직    }        @PostAuthorize("returnObject.owner == authentication.name")    public Document getDocument(Long id) {        return documentRepository.findById(id);    }}
```

### 주요 특징

**필터 체인**: Spring Security는 서블릿 필터 체인을 기반으로 동작합니다.

**다양한 인증 방식 지원**: Form 로그인, HTTP Basic, OAuth2, JWT 등을 지원합니다.

**CSRF 보호**: Cross-Site Request Forgery 공격으로부터 보호합니다.

**세션 관리**: 세션 고정 공격 방어, 동시 세션 제어 등을 제공합니다.

**표현식 기반 접근 제어**: SpEL을 사용한 복잡한 권한 검사가 가능합니다.

Spring Security는 강력하고 유연한 보안 프레임워크로, 복잡한 보안 요구사항도 쉽게 구현할 수 있도록 도와줍니다.
