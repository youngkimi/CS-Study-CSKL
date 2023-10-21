# SPRING DI(Dependency Injection) 🔆

# SPRING AOP

### 1️⃣ 답 : 4번
    - Spring AOP는 자바에서 기본적으로 지원하는 Interface를 이용한 프록시 방식을 통해
    구현하므로, AspectJ 라이브러리에 종속적이지 않다.

### 2️⃣ 답 :
    - before : target 메서드 호출 전(실제 메서드 수행 전)
    - after : target 메서드 호출 이후 (try catch구문의 finally와 같은 시점)
    - after-returning : target 메서드가 정상적으로 동작 후(메서드의 return이 이루어진 이후)
    - after-throwing : target 메서드 실행 시 예외가 발생할 경우
    - around : 적용될 시점을 위에 적은 4가지 시점 중 임의로 정할 수 있다.
    - 참고 사항 : advice 적용 순서
        - around -> before -> after-returning/after-throwing -> after -> around

### 3️⃣ 답 : 4번
    - 설명 : 기본적으로
        - 접근제어자 패키지명.클래스명.메서드명(파라미터 타입) // 이렇게 적는 것이 관례이다
        - 예시 : com.ssafy.ws.model.dao 패키지의 public인 select(int id, String modelName) 메서드를 가져오고 싶다.
            - execution(public com.ssafy.ws.model.dao.select(int, String))

### 4️⃣ 답 :
    - AOP = Aspect Oriendted Programming
    - AOP의 특징 :
        - 관점 지향 프로그래밍을 의미하며, 어떤 로직을 핵심적인 관점과 부가적인 관점으로 나누어보고, 그 관점을 기준으로 각각 모듈화를 하겠다는 프로그래밍 패러다임을 의미한다.
        - 핵심적인 비즈니스 로직의 공통적으로 나타나는 관심사들을 분리하여 모듈화함으로써 중복된 코드를 줄이고 모듈화된 코드를 재사용한다.
        - 핵심기능들이 공통된 요소들을 횡적으로 추출한다는 의미에서 크로스 컷팅(Cross-Cutting)이라고 부르기도 한다.
        - Spring AOP의 경우 프록시 패턴을 기반으로 하여 프록시 객체를 통해 AOP를 구현한다는 특징이 있다.

### 5️⃣ 답 : 2개
    - after은 target메서드의 정상동작 여부에 관계없이, 호출 이후에 반드시 실행된다.
    - after-throwing은 예외클래스의 최상위 클래스인 Throwable을 반환한다. 
        - 참고 : Throwable클래스는 Exception, Error클래스로 나뉜다.

# SPRING MVC

# SPRING Interceptor (1)

### 1️⃣ FrontController라고도 하며 어떤 컨트롤러를 매핑할지 알려주는 것

### 2️⃣ 1. true를 반환하게 되면 요청을 종료하는 것이 아니라, 계속 실행한다.

### 3️⃣ getInitParameter();

### 4️⃣ preHandle(), postHandle(), afterCompletion();

### 5️⃣ 2. Filter가 Interceptor보다 먼저 작동한다.

### 6️⃣ @WebListener

### 7️⃣ 5. Model이 생성되며 반환값은 String과 ModelAndView 객체 모두 가능하다.

### 8️⃣ Filter, Interceptor

### 9️⃣ 요청을 종료하며 그 뒤의 메서드들은 실행하지 않는다.

### 🔟

# SPRING Interceptor (2)

# MyBatis - Dynamic SQL (1)

# MyBatis - Dynamic SQL (2)
