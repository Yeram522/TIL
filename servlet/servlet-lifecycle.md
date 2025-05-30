# Servlet LifeCycle

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

### init

최초 서블릿 요청 시에 동작하는 메소드로 최초 요청시에만 실행하고 두번째 요청부터는 호출하지 않는다.

### destroy

컨테이너가 종료될 때 호출되는 메소드 이며 주로 자원을 반납하는 용도로 사용된다.

### service

최초 요청 시에는 init() 이후에 동작하고, 두번쨰 요청부터는 init() 호출 없이 바로 service()를 호출한다.
