# 💡SPRING DI 

## DI(Dependency Injection) 의존성 주입

A 객체가 어떤 일을 처리하기 위해서 B 객체의 도움을 받아야 한다면 A가 B에 의존한다.

### 🔍 의존관계 역전

- 객체 생성 의존성 제거
- 타입 의존성 제거

의존관계 역전이란, 객체에 존재하는 의존관계들을 제거하고, 그 의존관계를 객체 외부로 넘기는 것을 말한다.

### 🔍 의존성 주입

```java
public class Person {
    
    private Food food;

    // 1. 생성자에 food를 주입한다
    public  Person(Food food){
        this.food = food;
    }

    //2. 설정자에 food를 주입한다.
    public setFood(Food food){
        this.food = food;
    }

    public void eat(){
        System.out.println(food.name() + "을 먹는다");
    }
}
```

### 🔍 Spring IoC Container(Spring Inversion of Control Container)

- Bean : 스프링에서 핵심적인 역할을 하는 객체
- Container : Bean의 인스턴스화 조립, 관리, 사용 소멸에 대한 처리 담당


### 🔍 스프링 설정 정보
설정 정보를 작성하는 방법은 총 3가지
```
(1) XML방식
(2) Annotation방식 
(3) Java 방식
```

### 🔍 bean 직접 등록 예시

#### (1) 빈등록
```xml
<bean class="com.ssafy.test.Person" id = "person"/>
```
#### (2) 생성자 주입
```xml
<bean class="com.ssafy.test.Chicken" id = "chicken"/>
<bean class="com.ssafy.test.Person" id = "person">
    <constructor-arg ref="chicken"/>
</bean>
```
#### (3) 설정자 주입
**name** : setter와 매핑(setFood -> food)

**ref** : 참조할 Bean의 id
```xml
<bean class="com.ssafy.test.Pizza" id = "pizza"/>
<bean class="com.ssafy.test.Person" id = "person">
    <property name="food" ref="pizza"/>
</bean>
```

### 🔍 Annotation으로 의존성 주입
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

class Person{

    //1. 필드주입
    @Autowired
    @Qaulifier("beanName")
    private Food food;

    //2. 생성자 주입
    @Autowired
    public Person(@Qualifier("beanName")Food food){
    	this.food = food;
    }
    
    //3. 설정자 주입
    @Autowired
    public void setFood(@Qaulifier("beanName")Food food) {
    	this.food = food;
    }

    public void eat(){
        System.out.println(food.getName() + "을(를) 먹습니다");
    }
}

```

### 🔍 Bean Scope
```Bean 범위를 정의해서 객체의 범위를 제어할 수 있다.```

(1) singleton : 기본값. 단일 객체 인스턴스

(2) prototype : 빈을 요청할 때 마다 새로운 인스턴스 생성

(3) request : HTTP Request 주기로 bean 인스턴스 생성

(4) session : HTTP Session 주기로 bean 인스턴스 생성

# SPRING AOP


# SPRING MVC


# SPRING Interceptor (1)


# SPRING Interceptor (2)


# MyBatis - Dynamic SQL (1)


# MyBatis - Dynamic SQL (2)