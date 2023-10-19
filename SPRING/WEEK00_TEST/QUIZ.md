# SPRING DI

#### 1. Spring Framework의 특징 세 가지를 서술하시오.

#### 2. POJO는 무엇의 약자인가?

#### 3. A객체가 B 객체에 의존하다는 말이 어떤 것을 의미하는가?

#### 4. 해당 코드에서 문제점을 파악하고 어떤 의존성을 제거해줘야 하는지 서술하시오.

```java
class Chicken{
	public String getName() {
		return "치킨";
	}
}

class Person{
    private Chicken food;

    public Person(){
        food = new Chicken();
    }

    public void eat(){
        System.out.println(food.getName() + "을 먹습니다");
    }
}

//메인 클래스
public class Test{
    public static void main(String[] args){

    	Person p = new Person();
    	p.eat();
    }
}
```

#### 5. A 와 B에 알맞은 단어를 작성하시오.

```
스프링에서 핵심적인 역할을 하는 객체를 ( A )이라고 하며, ( B )는  ( A )의 인스턴스화 조립, 관리의 역할, 사용 소멸에 대한 처리를 담당한다.
```

#### 6. 위의 코드는 해당 Spring Container의 설정파일이다. 아래 코드에서 설정파일로 등록한 Bean을 불러오려고 한다. 자바 코드의 문제점을 파악하고 수정하시오.

```xml
<beans>
	<bean class="com.ssafy.test.Programmer" id="programmer"></bean>
</beans>
```

```java
		ApplicationContext context = new GenericXmlApplicationContext("applicationContext.xml");

        Programmer p = context.getBean("programmer");
```

#### 7. Bean에 정의할 수 있는 Scope 4가지를 작성하고, 각각의 Scope가 의미하는 것을 간략히 쓰시오.

#### 8. bean 등록시에 사용할 수 있는 다양한 속성들이 있다. 이 중에 constructor-arg, property 에 대해 설명하시오.

#### 9. Sonata 객체를 Component scan을 통해 빈 등록하려고 한다. 이때 생성되는 빈의 이름은?

```java
@Component
public class Sonata implements Car {
    ...
}
```

#### 10. 아래 상황에서 발생하는 문제점이 무엇인지 설명하고, 해결하기 위한 방법을 아는대로 서술하시오.

```java
interface Food {
    String getName();
}

@Component
class Chicken implements Food{
	public String getName() {
		return "치킨";
	}
}
@Component
class Pizza implements Food{
	public String getName() {
		return "피자";
	}

}


class Person {
    Food food
    public Person(){}

    @Autowired
    public void setFood(Food food){
        this.food = food;
    }
}

```

# SPRING AOP

# SPRING MVC

# SPRING Interceptor (1)

### 1️⃣ Dispatcher Servlet의 역할은 ?

### 2️⃣ Interceptor에 대해서 옳지 않은 것은 ?

1. preHandle()은 Controller 실행 이전에 호출되며, true를 반환하게 되면 요청을 종료한다.
2. postHandle()은 ModelAndView 객체가 인자로 포함되어 있다.
3. afterCompletion()은 Exception으로 전달되며, 기본은 null이다.
4. afterCompletion()은 뷰가 클라이언트에서 응답을 전송한 뒤 실행된다.
5. 인터셉터는 요청을 처리하는 과정에서 요청을 가로채서 처리하는 것을 의미한다.

### 3️⃣ Listener를 web.xml에 등록했을 때, 인자의 parameter 값을 가져오는 메서드는 ?

### 4️⃣ Interceptor의 주요 메서드 3가지는 ?

### 5️⃣ Filter와 Interceptor에 대한 설명으로 올바르지 않은 것은 ?

1. Filter는 FilterChain을 통해 연쇄적으로 동작 가능하다.
2. Interceptor가 Filter 보다 먼저 작동한다.
3. 사용자의 요청이 Servlet에 전달되기 전에 Filter를 거친다.
4. 로그인, 권한 체크, 로그 처리 등 비즈니스 로직 시작 전 수행하는데 사용하는 것은 Interceptor이다.
5. Filter는 요청과 응답 데이터를 필터링하여 제어, 변경하는 역할을 한다.

### 6️⃣ Listener를 사용하기 위한 Annotation은 ?

Spring에서 Listener를 사용하는 방법에는 Annotation으로 등록하는 것과, Web.xml에 등록하는 두 가지 방법이 있다.

이때 사용하는 Annotation은 ?

### 7️⃣ MVC 요청 흐름에 대한 설명으로 옳지 않은 것은 ?

1. 핸들러 매핑을 통해 어떤 컨트롤러를 매핑할지 알 수 있다.
2. Dispatcher Servlet은 Front Controller라고도 부른다.
3. Handler Adapter를 실행하면, 컨트롤러가 실행되며 Service 로직이 돌아간다.
4. DAO는 데이터베이스와 소통하며, 데이터베이스 친화적인 메서드들을 동작시킨다.
5. Model이 생성되며 반환값은 String만 가능하다.

### 8️⃣ 아래 빈칸에 들어갈 단어는 ?

<빈칸> → DispatcherServlet → <빈칸> → Controller

### 9️⃣ 아래 상황에서 어떤 결과가 나타나는지 서술하시오.

```java
public class TestInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        log.info("⭐️ Interceptor - preHandle : 인터셉터 시작");
        return false;
    }
}
```

### 🔟 servlet-context에 선언해야 하는 것을 모두 선택하세요.

1. Service
2. view resolver
3. intercepter
4. DAO
5. Mybatis

# SPRING Interceptor (2)

# MyBatis - Dynamic SQL (1)

# MyBatis - Dynamic SQL (2)
