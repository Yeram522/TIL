# Exception Handler

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

에러가 발생하면 톰캣이 자동으로 request에 에러 정보를 추가하기 때문에, 우리는 아래처럼 request에서 에러 정보를 받아올 수 있다.

```java
WebServlet("/showErrorPage")
public class ExceptionHandlerServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

        Enumeration<String> attrName = request.getAttributeNames();
        while (attrName.hasMoreElements()){
            System.out.println(attrName.nextElement());
        }

        Integer statusCode = (Integer) request.getAttribute("jakarta.servlet.error.status_code");
        String message = (String) request.getAttribute("jakarta.servlet.error.message");

        System.out.println("statusCode = " + statusCode);
        System.out.println("message = " + message);

        StringBuilder errorPage = new StringBuilder();
        errorPage.append("<!doctype html>\n")
                .append("<html>\n")
                .append("<head>\n")
                .append("</head>\n")
                .append("<body>\n")
                .append("<h1>")
                .append(" - ")
                .append(statusCode)
                .append(message)
                .append("/<h1>")
                .append("</body>\n")
                .append("</html>\n");


        response.setContentType("text/html");

        PrintWriter out = response.getWriter();

        out.print(errorPage);

        out.close();

    }
}
```
