# Response

### 서블릿의 역할

1. 요청 받기 - HTTP method GET/POST 요청에 따라 parameter로 전달받은 데이터를 꺼내올 수 있다.
2. 비즈니스 로직 처리 - DB 접속과 CRUD에 대한 로직처리
3. 응답 하기- 문자열로 동적인 웹(HTML 태그) 페이지를 만들고 스트림을 이용해 내보낸다.



사용자 브라우저에 응답하기 위해서는 `HttpServletResponse`의 `getWriter()` method로 `PrintWriter` 인스턴스를 반환받는다.

```java
PrintWriter out = response.getWriter();
```

\
PrintWriter는 BufferedWriter와 형제격인 클래스이지만\
더 많은 형태의 생성자를 제공하고 있는 범용성으로 인해 더 많이 사용된다.



{% code title="문자열을 이용해 사용자에게 내보낼 페이지를 작성" %}
```java
StringBuilder responseBuilder = new StringBuilder();
responseBuilder.append("<!doctype html>\n")
        .append("<html>\n")
        .append("<head>\n")
        .append("</head>\n")
        .append("<body>\n")
        .append("<h1>안녕 servlet response</h1>\n")
        .append("</body>\n")
        .append("</html>\n");
```
{% endcode %}



{% code title="응답을 위한 content-type을 text/html로 지정" %}
```java
response.setContentType("text/html");
```
{% endcode %}



