# SPRING DI(Dependency Injection) 🔆

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

#### 6. 위의 코드는 해당 Spring Container의 설정파일이다. 아래 코드에서 설정파일로 등록한 Bean을 불러오려고 한다. 자바 코드의 문제점을 파악하고 수정하시오.🔆

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

#### 1️⃣ Spring AOP에 대한 설명으로 옳지 않은 것은?🔆
    1. Spring AOP를 통해 실제 기능이 구현된 Target 객체를 호출하려고 하면, Target 객체가 호출되지 않는다.
    2. Spring AOP에서 Join Point는 일반적으로 메서드 실행시점이다.
    3. Spring AOP는 인터페이스를 구현한 클래스가 아닌 경우에는 CGLIB 프록시를 통해서 구현할 수 있다.
    4. Spring AOP를 구현하기 위해서는 AspectJ 라이브러리를 사용하여야 한다.
    5. Spring AOP는 일반적으로 런타임 시에 위빙을 수행한다.
    6. Spring AOP에서 Bean으로 등록된 객체는 항상 Proxy 객체가 된다.

#### 2️⃣ Spring AOP에서 Advice 타입은 5가지가 존재한다. 5가지의 Advice 타입을 쓰고, 각 타입이 어느 시점에서 적용되는지 작성하시오.🔆

#### 3️⃣ com.xyz.service package 또는 그 하위 패키지에 선언된 모든 메서드를 실행하는 PointCut Expression으로 알맞은 것은?🔆🔆
    1. execution(public * *(..))
    2. execution(* set*(..))
    3. execution(* com.xyz.service.*.*(..))
    4. execution(* com.xyz.service..*.*(..))
    5. within(com.xyz.service.*)
    6. execution(* com.xyz.service.MovieService.*(..))

#### 4️⃣ AOP(관점 지향 프로그래밍)가 어떤 영어 단어의 약어인지 쓰고, AOP의 특징에 대해 서술하시오.

#### 5️⃣ 다음은 Spring AOP의 Advice 타입에 관한 설명이다. 옳지 않은 것의 개수를 구하시오.
    - after : target메서드 정상 동작 이후에 실행된다.
    - after returning : 타입이 target메서드의 반환형과 같아야 한다.
    - after throwing : 에러가 발생하면 수행되는 메서드이므로 타입은 Exception이여야 한다.
    - around : target메서드의 실행 시점, 방법, 여부를 모두 결정할 수 있으므로 다른 advice 타입들을 모두 대체할 수 있다.


# SPRING MVC

#### 1️⃣ 스프링 MVC란, (A), (B), (C)의 약자로 (D)를 기반으로 어플리케이션을 개발할 때 사용하는 디자인 패턴이다. A, B, C, D의 알맞은 말은?

#### 2️⃣ 스프링 MVC의 동작 과정을 순서대로 쓰시오.
```
a. 클라이언트 요청이 들어오면 DispatcherServlet이 받는다.
b. DispatcherServlet은 Controller에 요청을 전달
c. DispatcherServlet은 View가 만들어낸 결과를 응답
d. 결과(요청처리를 위한 data, 결과를 보여줄 view의 이름)를 ModelAndView에 담아 반환
e. HandlerMapping이 어떤 Controller가 요청을 처리할지 결정한다.
f. Controller는 요청을 처리한다.
g. 결과를 처리할 View에 ModelAndView를 전달
h. ViewResolver에 의해서 실제 결과를 처리할 View를 결정하고 반환
```

#### 3️⃣ MVC 설정에 대해 옳바르지 않은 것은?
1. Controller는 Annotation 방식으로 bean을 등록하기 위해서 component-scan을 설정한다.
2. ViewResolver는 servlet-context.xml에 설정해야한다.
3. root-context.xml에는 Service, DAO 등의 bean을 포함한다.
4. handler mapping은 별도의 등록없이 사용가능하다.
5. 정답없음

#### 4️⃣ 다음 코드의 실행 결과로 알맞은 것은?
url 정보
```
~/test?id=&pw=2
```
```
@GetMapping("test")
public String test1(Model model, @RequestParam(value="myid")Stirng id, String pw){
    model.addAttribute("id", id);
    model.addAttribute("pw", pw);
    return "test";
}
```
test.jsp
```
${id}
${pw}
```
1. 2
2. &nbsp; 2
3. null 2
4. 에러 발생

#### 5️⃣ 다음 코드의 실행 결과로 알맞은 것은?
url 정보
```
~/test?id=&pw=2
```
```
@GetMapping("test")
public String test1(Model model, Stirng id, String pw){
    model.addAttribute("id", id);
    model.addAttribute("pw", pw);
    return "test";
}
```
test.jsp
```
${id}
${pw}
```
1. 2
2. &nbsp; 2
3. null 2
4. 에러 발생

#### 6️⃣ 다음 중 root-context.xml에 설정해야 하는 것을 모두 고르시오.
1. HandlerMapping
2. viewResolver
3. Service
4. Controller
5. Repositories

#### 7️⃣ 3개의 @RequestMapping 방식의 차이점을 쓰시오.
- @RequestMapping("test")
- @RequestMapping(value="test", method = RequestMethod.GET)
- @RequestMapping(value="test", method = RequestMethod.POST)

#### 8️⃣ <a>태그를 눌렀을때 Controller에서 test1으로 forward하는 코드를 작성하시오.
```
<a href=test></a>
```
```
@_________
public String test(){
    return ______;
}
```

#### 9️⃣ <a>태그를 눌렀을때 Controller에서 test1으로 redirect하는 코드를 작성하시오.
```
<a href=test></a>
```
```
@_________
public String test(){
    return ______;
}
```

#### 🔟 Spring MVC에서 Controller란?

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

### 1. MyFilter와 MyFilter2는 순서대로 Mapping되어있다. 출력 순서는?

```java
public class MyFilter implements Filter {
    public MyFilter() {}

    public void init(FilterConfig fConfig) throws ServletException {}
	public void destroy() {}

	public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
		System.out.println("A");
		chain.doFilter(request, response);
		System.out.println("B");
	}
}

public class MyFilter2 implements Filter {
    public MyFilter2() {}

    public void init(FilterConfig fConfig) throws ServletException {}
	public void destroy() {}

	public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) throws IOException, ServletException {
		System.out.println("C");
		chain.doFilter(request, response);
		System.out.println("D");
	}
}
```

### 2. doFilter 내에서 다음 필터가 존재하면 다음 필터를 호출하고 존재하지 않는다면 서블릿을 호출할 수 있게 해주는 것은?

### 3. AInterceptor와 같은 형식으로 B,C 인터셉터가 있고 각 메서드에 아래와 같은 형식으로 들어있다. 출력 순서는?
System.out.println("A : preHandle");<br>
System.out.println("B : preHandle");<br>
System.out.println("C : preHandle");<br>
```java
public class AInterceptor implements HandlerInterceptor{
	@Override
	public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
		System.out.println("A : preHandle");
		return true;
	}
	
	@Override
	public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
		System.out.println("A : postHandle");
	}
	
	@Override
	public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
		System.out.println("A : afterCompletion");
	}
}
```
### 4. 인터셉터의 preHandle에서 false를 반환했다. 다음 동작으로 옳은 것?<br>
    a. Controller 실행<br>
    b. postHandle 호출<br>
    c. afterCompletion 호출<br>
    d. 요청 종료<br>

### 5. Controller에서 예외 발생 시 다음 동작 옳은 것?<br>
    a. 요청 종료<br>
    b. afterCompletion 호출<br>
    c. postHandle 호출<br>
    d. preHandle 호출<br>

### 6. 요청의 흐름이 다음과 같을 때 filter의 위치는?<br>
    a 디스패처서블릿 b 인터셉터 c 컨트롤러 d 뷰<br>

### 7. 인터셉터의 설정을 "/regist" 처리할 때 빈 칸 채우기
    ```xml
    <interceptors>
		<interceptor>
			<_______ path="_______"/>
			<beans:ref bean="confirm"/>
		</interceptor>
	</interceptors>
    
    ```

### 8. 인터셉터 설정 시 메인페이지("/")와 로그인페이지("/login")는 로그인을 하지 않아도 접속이 가능할 때 빈 칸 채우기
    ```xml
    	<interceptor>
			<mapping path="/*"/>
			<_______________ path="/login"/>
			<_______________ path="/"/>
			<beans:ref bean="confirm"/>
		</interceptor>
    
    ```

### 9. Listener 시작 메서드<br>
    a. contextStarted
    b. contextBegin
    c. contextInitialized
    d. contextRun

### 10. 인터셉터에서 afterCompletion() 메서드의 용도 서술

---

# MyBatis - Dynamic SQL (1)


### 1️⃣. MyBatis에서 동적 쿼리를 사용할 때, ${}와 #{}의 차이에 대해 서술하시오.

### 2️⃣. MyBatis를 사용하기 위한 sqlSessionFactory를 등록하려고 한다. 해당 빈 칸을 작성하시오.

```
<!-- MyBatis를 사용하기 위한 sqlSessionFactory를 등록한다. -->
	<bean id="sqlSessionFactory" 
		class="org.mybatis.spring.SqlSessionFactoryBean">
		<property name="dataSource" ref="dataSource"/>
		<!--mapper.xml 파일의 경로를 ant 표현식의 상태로 사용 -->
		<property name="____________" value="classpath*:mappers/**/*.xml"/>
		<!-- mapper에서 사용할 DTO들의 기본 패키지를 등록 -->
		<property name="____________" value="com.ssafy.ws.model.dto"/>
	</bean>
```

### 3️⃣ JDBC를 사용하지 않고 MyBatis를 사용하였을 때 장점을 2가지 이상 서술하시오.

### 4️⃣. 다음 중 SqlSession에 대한 설명으로 옳지 않은 것을 모두 고르시오.

1. mapper.xml에 등록된 SQL의 실행이나 트랙잭션을 관리하는 인터페이스이다.
2. Spring 프로젝트의 DTO에 직접 접근하여 쿼리를 수행한다.
3. Thread-safe 하지 않으므로 thread를 매번 필요에 따라 생성한다.
4. MyBatis 설정파일을 읽고 SqlSessionFactoryBuilder에 의해 생성된다.
5. SqlSession은 Mapping File에서 실행할 SQL을 찾아서 실행한다.

### 5️⃣. MyBatis에서 SQL 쿼리와 자바 객체 간의 매핑을 설정하는 파일은 무엇인가?

1. mybatis-config.xml
2. applicationContext.xml
3. mapper.xml
4. pom.xml
5. servlet-context.xml



### 6️⃣. 사용자 이름(name)을 바탕으로 검색하여 조회하려고 한다. 해당 빈칸을 작성하시오.

```
<select id="searchByName "___________="string"
		__________="User">
		SELECT *
		FROM users WHERE ____________________________
	</select>
```

### 7️⃣. MyBatis에서 동적 쿼리를 작성할 때 if, choose, when, otherwise 태그를 어떻게 활용하는지 설명하고, 각 태그의 역할에 대해 서술해주세요.

### 8️⃣. MyBatis의 DB Access 순서에 대해 알맞게 정렬하시오.

(5) 애플리케이션이 SqlSessionFactoryBuilder를 위해 SqlSessionFactory를 빌드하도록 요청<br>
(2) SqlSessionFactoryBuilder는 SqlSessionFactory를 생성하기 위해 MyBatis 설정 파일을 읽음<br>
(7) SqlSessionFactoryBuilder는 MyBatis 설정 파일의 정의에 따라 SqlSessionFactory를 생성<br>
(1) 클라이언트의 애플리케이션에 대한 요청<br>
(5) 애플리케이션은 SqlSessionFactoryBuilder를 사용하여 빌드된 SqlSessioFactory에서 SqlSession을 가져옴<br>
(9) SqlSessionFactory는 SqlSession 생성하고 이를 애플리케이션에 반환<br>
(4) 애플리케이션이 SqlSession에서 Mapper Interface 구현 개체를 가져옴<br>
(6) 애플리케이션에서 Mapper Interface의 메소드를 호출<br>
(3) Mapper Interfcae의 구현 개체가 SqlSession메소드를 호출하고 SQL 실행 요청<br>
(8) SqlSession은 Mapping File에서 실행할 SQL을 찾아서 실행

### 9️⃣. 동적쿼리의 trim에서 사용되는 prefix, prefixOverrides의 차이에 대해 서술하시오.

### 🔟. 아래 상황에서 발생하는 문제점이 무엇인지 설명하고, 해결하기 위한 방법을 아는대로 서술하시오.

```
SELECT
    member_id,
    name,
    city,
    street,
    zipcode
FROM
    member_table
WHERE 1=1
    <if test="member_id != null and member_id != ''">
    	and member_id = #{member_id}
    </if>
    <if test="name != null and name != ''">
    	and name = #{name}
    </if>
```


# MyBatis - Dynamic SQL (2)
#### 1️. Mapper.xml에 파라미터 표기 시 #{} 을 이용하는 것과 ${} 을 이용하는 것의 차이는 무엇인가?

#### 2. DB에서 받아온 칼럼 명이 프로퍼티 명과 다른 경우에 어떻게 처리해야 하는가?

#### 3. title이라는 조건이 주어지는지 여부를 확인하고, 주어진다면 해당 title을 포함하는 블로그를 검색하고 싶다. 알맞은 동적 쿼리를 작성하시오.
```
select id="findActiveBlogWithTitleLike"
     resultType="Blog">
  SELECT * FROM BLOG
  WHERE state = ‘ACTIVE’
  _____________________
  _____________________
  _____________________
</select>
```

#### 4. 다음을 보고 Database의 정확한 속성명들과 User 클래스의 정확한 프로퍼티명을 유추하시오.
```
<resultMap id="userResultMap" type="User">
  <id property="id" column="user_id" />
  <result property="username" column="user_name"/>
  <result property="password" column="hashed_password"/>
</resultMap>
```

#### 5. typeAliases에 대해 옳지 않은 것은?
1. typeAliases는 자바 타입에 대한 짧은 이름이다.
2. 아래 코드로 domain에서 빈을 검색할 때, 애노테이션이 없으면 등록되지 않는다.
```
<typeAliases>
  <package name="domain.blog"/>
</typeAliases>
```
3. 공통 자바 타입을 위한 여러 내장 타입 별칭은 대소문자를 구별하지 않는다.
4. @Alias 애노테이션을 사용한다면 애노테이션에서 지정한 값이 별칭으로 사용될 것이다. 

#### 6. 데이터 무결성이 뭐임


#### 7. com.ssafy.model.dao.BoardDao에 위치한 인터페이스를 구현체 없이 매퍼와 연결하고 싶다. 빈칸 채워주세요.
``` xml
<mapper __________________________________>
    <select id="getUser" resultType="User">
        SELECT * FROM users
    </select>
</mapper>

```

#### 8. 프로젝트의 규모가 커져서 현수는 xml 방식으로 Bean을 등록하는 것이 너무 힘들다. 대신 어떠한 방식을 사용할 수 있는지와, 이때 사용해야 하는 어노테이션들을 작성하시오.

#### 9.  CRUD 중 Transaction 처리가 필요한 기능과 필요하지 않은 기능은 무엇인가? 이유도 설명해주세요.

#### 10. SearchCondition은 key (검색 기준), orderBy (정렬 기준), orderByDir(정렬방향) 의 프로퍼티를 가진다. key와 orderBy는 none 값과 DB 내 컬럼명을 속성으로 가진다. orderByDir는 내림차순("DESC"), 오름차순("ASC")을 속성으로 가진다. key나 orderBy가 none이 아닐 때 검색 기준을 포함하는지 검색하고 정렬 기준으로 정렬하는 동적 쿼리 함 짜보셈. 참고로 Board의 프로퍼티명은 id, writer, content, title, viewCnt. DB 내 board의 속성 명은 board_id, writer, content, title, view_cnt로 작성되어 있다. 


``` xml
<select id="search" resultType="Board" parameterType="SearchCondition>
   
</select>
```
