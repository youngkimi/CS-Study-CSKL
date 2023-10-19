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


# SPRING Interceptor (2)


# MyBatis - Dynamic SQL (1)


# MyBatis - Dynamic SQL (2)