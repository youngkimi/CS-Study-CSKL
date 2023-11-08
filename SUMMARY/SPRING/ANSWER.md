# SPRING DI(Dependency Injection) 🔆

### 1️⃣. Spring Framework의 특징 세 가지를 서술하시오.

(1) POJO 방식의 프레임워크<br>
(2) 의존성 주입을 통한 객체 관계 구성<br>
(3) 관점 지향 프로그래밍(AOP)

### 2️⃣. POJO는 무엇의 약자인가?

Plain Old Java Object

### 3️⃣. A객체가 B 객체에 의존하다는 말이 어떤 것을 의미하는가?

객체 A가 어떤 일을 처리하기 위해서 객체 B의 도움을 받아야만 할 때 객체 A가 B 객체에 의존한다고 말한다.

### 4️⃣. 해당 코드에서 문제점을 파악하고 어떤 의존성을 제거해줘야 하는지 서술하시오.

해당 코드는 현재 Person클래스가 Chicken 클래스에 의존성을 갖고 있다. Person클래스 내에서 객체가 생성되고 있기 때문에 객채 생성 의존성을 가지고 있다. 따라서 이를 제거하고 Test클래스에서 Chicken객체를 생성하고 만들어진 Chicken 인스턴스를 활용해서 Person 인스턴스를 만든다면 객체생성 의존성을 제거할 수 있다.

### 5️⃣. A 와 B에 알맞은 단어를 작성하시오.

```
스프링에서 핵심적인 역할을 하는 객체를 ( A )이라고 하며, ( B )는  ( A )의 인스턴스화 조립, 관리의 역할, 사용 소멸에 대한 처리를 담당한다.
```

(A) - Bean <br>
(B) - Container

### 6️⃣. 위의 코드는 해당 Spring Container의 설정파일이다. 아래 코드에서 설정파일로 등록한 Bean을 불러오려고 한다. 자바 코드의 문제점을 파악하고 수정하시오.

```xml
<beans>
	<bean class="com.ssafy.test.Programmer" id="programmer"></bean>
</beans>
```

```java
		ApplicationContext context = new GenericXmlApplicationContext("applicationContext.xml");

        Programmer p = context.getBean("programmer");
```

### 수정 후

```java
		ApplicationContext context = new GenericXmlApplicationContext("applicationContext.xml");

        //첫번째 수정 방법
		Programmer p = (Programmer)context.getBean("programmer");

        //두번째 수정방법
		Programmer p = context.getBean("programmer", Programmer.class);
```

### 7️⃣. Bean에 정의할 수 있는 Scope 4가지를 작성하고, 각각의 Scope가 의미하는 것을 간략히 쓰시오.

(1) singleton : 기본값. 단일 객체 인스턴스<br>
(2) prototype : 빈을 요청할 때 마다 새로운 인스턴스 생성<br>
(3) request : HTTP Request 주기로 bean 인스턴스 생성<br>
(4) session : HTTP Session 주기로 bean 인스턴스 생성

### 8️⃣. bean 등록시에 사용할 수 있는 다양한 속성들이 있다. 이 중에 constructor-arg, property 에 대해 설명하시오.

constructor-arg는 생성자 주입시 활용하는 속성이고, property는 설정자 주입시 활용하는 속성이다.

### 9️⃣. Sonata 객체를 Component scan을 통해 빈 등록하려고 한다. 이때 생성되는 빈의 이름은?

sonata

### 🔟. 아래 상황에서 발생하는 문제점이 무엇인지 설명하고, 해결하기 위한 방법을 아는대로 서술하시오.

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

Food의 구현체가 Chicken, Pizza로 두 가지 있는데 현재 모두 Component 어노테이션으로 빈이 등록된 상태이다. 하지만, Person 클래스에서 설정자 주입을 통해 Food의 의존성을 주입하려고 하는데, 두 가지 구현체 중에서 어떤 빈을 주입해야 하는지 알수 가 없으므로 문제가 생긴다. 따라서 @Qaulifer 어노테이션으로 주입할 빈을 명시해주거나, 주입하고 싶은 구현체에 @Primary어노테이션을 써서 가져올 빈을 명시해주어야 한다.

```java
interface Food {
    String getName();
}

@Component
@Primary //첫번째 방법
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
    //두번째 방법
    public void setFood(@Qaulifier("chicken")Food food){
        this.food = food;
    }
}

```

# SPRING AOP

### 1️⃣ 답 : 4번

    - Spring AOP는 자바에서 기본적으로 지원하는 Interface를 이용한 프록시 방식을 통해
    구현하므로, AspectJ 라이브러리에 종속적이지 않다.

### 2️⃣ 답 :

    - before : target 메서드 호출 전(실제 메서드 수행 전)
    - after : target 메서드 호출 이후 (try catch구문의 finally와 같은 시점)
    - after-returning : target 메서드가 정상적으로 동작 후(메서드의 return이 이루어진 이후)
    - after-throwing : target 메서드 실행 시 예외가 발생할 경우
    - around : 
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
        - 핵심기능들의 공통된 요소들을 횡적으로 추출한다는 의미에서 크로스 컷팅(Cross-Cutting)이라고 부르기도 한다.
        - Spring AOP의 경우 프록시 패턴을 기반으로 하여 프록시 객체를 통해 AOP를 구현한다는 특징이 있다.

### 5️⃣ 답 : 2개

    - after은 target메서드의 정상동작 여부에 관계없이, 호출 이후에 반드시 실행된다.
    - after-throwing은 예외클래스의 최상위 클래스인 Throwable을 반환한다.
        - 참고 : Throwable클래스는 Exception, Error클래스로 나뉜다.

# SPRING MVC

### 1️⃣ A : Model B : View C : Controller D : Servlet API

### 2️⃣ a, e, b, f, d, h, g, c

### 3️⃣ 5

### 4️⃣ 4

### 5️⃣ 1

### 6️⃣ 3, 5

### 7️⃣

1. 요청을 GET과 POST방식으로 둘다 받을 수 있음
2. GET요청만 받을 수 있음
3. POST요청만 받을 수 있음

### 8️⃣

```
@GetMapping("test")
public String test(){
    return "test1";
}
```

### 9️⃣

```
@GetMapping("test")
public String test(){
    return "redirect:test1";
}
```

### 🔟

1. 모델과 뷰를 연결하는 역할을 수행
2. 사용자에게 데이터를 가져오고 수정하고 제공

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

### 🔟 Interceptor, View Resolver

# SPRING Interceptor (2)

### 1️⃣ A C D B

### 2️⃣ FilterChain

### 3️⃣ A:preHandle, B:preHandle, C:preHandle, C:postHandle, B:postHandle, A:postHandle, C:afterCompletion, B:afterCompletion, A:afterCompletion

### 4️⃣ d

### 5️⃣ b

### 6️⃣ a

### 7️⃣ mapping, /regist

### 8️⃣ exclude-mapping

### 9️⃣ c

### 🔟 Controller에서 발생한 예외 혹은 실행 시간 같은 것들을 기록하는 등의 후처리로 주로 사용

# MyBatis - Dynamic SQL (1)

### 1️⃣. MyBatis에서 동적 쿼리를 사용할 때, ${}와 #{}의 차이에 대해 서술하시오.

#{}은 '' 콜른이 와서 String 형태로 들어온다. 예를들어 {user_id}의 user_id 값이 abc라면 쿼리문에는 USER_ID = 'abc'의 형태가 된다.
<br>
${}은 파라매터가 바로 출력되기 때문에 쿼리 주입을 예방할 수 없어 보안 측면에서 불리하다.
따라서 사용자의 입력을 전달할 때는 사용하지 않는 편이다.

### 2️⃣. MyBatis를 사용하기 위한 sqlSessionFactory를 등록하려고 한다. 해당 빈 칸을 작성하시오.

mapperLocations, typeAliaesPackage

### 3️⃣ JDBC를 사용하지 않고 MyBatis를 사용하였을 때 장점을 2가지 이상 서술하시오.

1. 자동으로 Connection close()기능
2. MyBatis 내부적으로 PreparedStatement 처리
3. #{prop}와 같이 속성을 지정하면 내부적으로 자동 처리
4. 리턴 타입을 지정하는 경우 자동으로 객체 생성 및 ResultSet 처리

### 4️⃣. 다음 중 SqlSession에 대한 설명으로 옳지 않은 것을 모두 고르시오.

2번 DTO가 아닌 DAO에 접근한다. <br>
4번 SqlSessionFactoryBuilder가 아닌 SqlSessionFactory에 의해 생성된다.

### 5️⃣. MyBatis에서 SQL 쿼리와 자바 객체 간의 매핑을 설정하는 파일은 무엇인가?

3번 (mapper.xml)

### 6️⃣. 사용자 이름(name)을 바탕으로 검색하여 조회하려고 한다. 해당 빈칸을 작성하시오.

```
<select id="searchByName "typeParameter="string"
		resultParameter="User">
		SELECT *
		FROM users WHERE name LIKE
		CONCAT('%',#{name},'%')
	</select>
```

### 7️⃣. MyBatis에서 동적 쿼리를 작성할 때 if, choose, when, otherwise 태그를 어떻게 활용하는지 설명하고, 각 태그의 역할에 대해 서술해주세요.

if, 조건문이 true가 되었을 때 포함된 SQL을 사용하고자 할 때 작성한다. <br>
choose는 Java의 'switch-case와 비슷하며 when 요소의 여러 조건 중 하나일 때 실행되거나 모두 아닐 경우 otherwise에 의해 실행된다.

### 8️⃣. MyBatis의 DB Access 순서에 대해 알맞게 정렬하시오.

(5) - (2) - (7) - (1) - (5) - (9) - (4) - (6) - (3) - (8)

### 9️⃣. 동적쿼리의 trim에서 사용되는 prefix, prefixOverrides의 차이에 대해 서술하시오.

prefix: 접두어를 붙여주는 기능<br>
prefixOverrides: trim태그 내부 실행될 쿼리문 가장 앞의 단어가 속성값에 설쟁해둔 문자와 동일할 경우 문자를 지움.

### 🔟. 아래 상황에서 발생하는 문제점이 무엇인지 설명하고, 해결하기 위한 방법을 아는대로 서술하시오.

사용자로부터 입력된 데이터가 직접 SQL 쿼리에 삽입되고 있으며, 이러한 데이터는 충분한 검증 없이 그대로 사용되기 때문에 SQL Injection 공격에 취약한 상태를 만들어준다. 따라서 해커가 악의적인 입력을 제공하여 데이터베이스를 침입하거나 손상시킬 수 있음.

# MyBatis - Dynamic SQL (2)

1️. Mapper.xml에 파라미터 표기 시 `#{}` 을 이용하는 것과 `${}` 을 이용하는 것의 차이는 무엇인가? <br>
`#{}` 는 parameter에 \"\" 을 붙여준다. `${}` 는 parameter 내용 자체를 가져온다. ${} 사용 시 SQL 주입 공격에 취약해진다. <br> 2. DB에서 받아온 칼럼 명이 프로퍼티 명과 다른 경우에 어떻게 처리해야 하는가? <br>
resultMap을 이용하거나 as 를 사용하여 Dao로 전달하기 전에 칼럼 명을 프로퍼티 명으로 변환해주어야 한다.<br> 3. title이라는 조건이 주어지는지 여부를 확인하고, 주어진다면 해당 title을 포함하는 블로그를 검색하고 싶다. 알맞은 동적 쿼리를 작성하시오.<br>

```java
select id="findActiveBlogWithTitleLike"
     resultType="Blog">
  SELECT * FROM BLOG
  WHERE state = ‘ACTIVE’
  <if test="title != null">
    AND title like #{title}
  </if>
</select>
```

4. 다음을 보고 Database의 정확한 속성명들과 User 클래스의 정확한 프로퍼티명을 유추하시오.
   DB : column_id, user_name, hashed_password
   User : id, username, password

5. typeAliases에 대해 옳지 않은 것은? <br>

- typeAliases는 자바 타입에 대한 짧은 이름이다. <br>
- **아래 코드로 domain에서 빈을 검색할 때, 애노테이션이 없으면 등록되지 않는다.** <<<
  <typeAliases>
  <package name="domain.blog"/>
  </typeAliases> <br>

- 공통 자바 타입을 위한 여러 내장 타입 별칭은 대소문자를 구별하지 않는다. <br>
- @Alias 애노테이션을 사용한다면 애노테이션에서 지정한 값이 별칭으로 사용될 것이다.

6. 데이터 무결성이 뭐임
   - 데이터베이스 내의 정확성, 일관성을 지키는 것.
   - 갱신 이상, 삭제 이상, 삽입 이상 등으로 인해 깨질 수 있다.
7. com.ssafy.model.dao.BoardDao에 위치한 인터페이스를 구현체 없이 매퍼와 연결하고 싶다. 빈칸 채워주세요.<br>

```java
<mapper namespace="com.ssafy.model.dao.BoardDao">
    <select id="getUser" resultType="User">
        SELECT * FROM users
    </select>
</mapper>
```

8. 프로젝트의 규모가 커져서 현수는 xml 방식으로 Bean을 등록하는 것이 너무 힘들다. 대신 어떠한 방식을 사용할 수 있는지와, 이때 사용해야 하는 어노테이션들을 작성하시오.<br>
   Java Configuration 파일로 작성. @Configuration @Bean
9. CRUD 중 Transaction 처리가 필요한 기능과 필요하지 않은 기능은 무엇인가? 이유도 설명해주세요.

```
   Read는 불필요. Transaction 처리는 데이터 삽입, 수정, 삭제(CUD) 등에 필요한 기능이다. (물론 Read에도 필요한 경우가 있음)
```

10. SearchCondition은 key (검색 기준), orderBy (정렬 기준), orderByDir(정렬방향) 의 프로퍼티를 가진다. key와 orderBy는 none 값과 DB 내 컬럼명을 속성으로 가진다. orderByDir는 내림차순("DESC"), 오름차순("ASC")을 속성으로 가진다. key나 orderBy가 none이 아닐 때 검색 기준을 포함하는지 검색하고 정렬 기준으로 정렬하는 동적 쿼리 함 짜보셈. 참고로 Board의 프로퍼티명은 id, writer, content, title, viewCnt. DB 내 board의 속성 명은 board_id, writer, content, title, view_cnt로 작성되어 있다.

```java
<select id="search" resultType="Board" parameterType="SearchCondition>
    Select board_id as id, writer, content, title, view_cnt as viewCnt
    FROM borad
    <if test="key != null">
    WHERE ${key} LIKE concat('%', #{word}, '%')
  </if>
  <if test="orderBy != null">
    ORDER BY ${orderBy} ${orderByDir}
  </if>
</select>
```
