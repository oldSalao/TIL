# Spring Inversion of Control

## 1. IoC 란?

번역하면 "제어의 역전"이라고 한다. 스프링에서 객체의 생성과 관리에 대한 제어권이 개발자가 아닌 컨테이너에게 역전되는 것을 뜻한다.

## 2. Spring Container

- 스프링 컨테이너의 주요 기능

  - 객체를 생성하고 관리한다.

  - 객체의 의존성을 주입한다.

- 스프링 컨테이너를 구성하는 방법.

  - XML configuration file (Legacy)

  - Java Annotations

  - Java Source Code

- IoC Process

  1.  Spring beans 구성.

            Spring beans?

            Spring beans란 단순히 Java 객체이다.
            Spring Container에 의해 Java 객체가 생성될 때, Spring은 이를 Spring beans라 칭한다.
            Spring beans는 Java 객체와 마찬가지로 일반적인 Java 클래스로부터 생성된다.

  2.  Spring Container 생성.

  3.  Spring Container로부터 beans 얻기.

## 3. Spring Inversion of Control - XML Configuration

1. Spring beans 구성.

```xml
<!--applicationContext.xml -->
<beans>
    <bean id="myCoach"
        class="com.example.springdemo.BaseballCoach">
    </bean>
</beans>
```

2. Spring Container 생성.

Spring Container는 일반적으로 ApplicationContext라고 한다. (ClassPathXmlApplicationContext, AnnotationConfigApplicationContext, GenericWebApplicationContext 등..)

```java
// Spring Container 생성.
ClassPathXmlApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
```

3. Spring Container로부터 beans 얻기.

```java
// Spring Container로부터 beans 얻기.
// Coach는 인터페이스
// getBean의 두번째 인자로 인터페이스 클래스를 전달함으로써 Spring은 해당 클래스 타입으로 객체를 캐스팅 해준다.
// 인자로 클래스를 전달하지 않으면 반환형은 Object임.
Coach theCoach = context.getBean("myCoach",Coach.class);
```

## 4. Spring Inversion of Control - Java Annotations

Spring은 특수한 annotation이 추가된 class를 스캔하고 자동으로 컨테이너에 Bean을 등록한다. 규모에 따라 장황해질 수 있는 xml 파일을 사용하는 방식에 비해 간편하다고 할 수 있다.

### 4-1. Java Annotations?

- Java class들에 추가되는 특별한 라벨/마커

- class에 대한 meta-data를 제공

- 런타임 또는 컴파일타임에 처리된다.

### 4-2. Development Process

1. Spring config 파일에서 컴포넌트 스캐닝을 활성화.

```xml
<beans ...>
<context:component-scan base-package="com.example"/>
</beans>
```

2. class에 @Component annotation을 추가.

```java
// @Component("bean ID")
@Component("thatSillyCoach")
public class TennisCoach implements Coach{

  @Override
  public String getDailyWorkout(){
    return "Practice your backhand volley";
  }

}
```

3. Spring 컨테이너에서 Bean을 회수.

```java
Coach theCoach = context.getBean("thatSillyCoach",Coach.class);
```

### 4-3. Default Component Names

Default bean id는 앞글자가 소문자로 변경된 class 이름이다.
