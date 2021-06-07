# Spring Dependency Injection - XML

## 1. DI?

의존성 주입이라고 한다

    의존성?
    어떤 클래스 A가 다른 클래스 또는 인터페이스B를 이용할 때 A가 B에 의존한다고 한다. 이 경우에서 의존성을 주입한다는 것은 클래스 A가 의존하는 B를 외부에서 전달해준다는 것이다.

## 2. Injection Types

스프링에는 다양한 유형의 injection이 존재한다. 그 중 가장 일반적인 두가지는 아래와 같다.

- Constructor Injection

- Setter Injection

## 3. Process of Constructor Injection

1. 의존성 클래스와 인터페이스 정의

```java
public interface FortuneService {

	public String getFortune();

}
```

```java
public class HappyFortuneService implements FortuneService {

	@Override
	public String getFortune() {
		return "Today is your lucky day!";
	}

}
```

2. 클래스에 Injection을 위한 생성자 정의.

```java
public class BaseballCoach implements Coach {

	// define a private field for the dependency
	private FortuneService fortuneService;

	// define a constructor for dependency injection
	public BaseballCoach(FortuneService theFortuneService) {
		fortuneService = theFortuneService;
	}

    @Override
	public String getDailyWorkout() {
		return "Spend 30 minutes on batting practice";
	}

	@Override
	public String getDailyFortune() {
		// use my fortuneService to get a fortune
		return fortuneService.getFortune();
	}
}
```

3. 스프링 구성 파일에 의존성주입 구성.

```xml
<!--applicationContext.xml -->
<bean class="com.luv2code.springdemo.HappyFortuneService" id="myFortuneService">
</bean>

-<bean class="com.luv2code.springdemo.TrackCoach" id="myCoach">
<!-- set up constructor injection -->
<constructor-arg ref="myFortuneService"/>
</bean>
```

4. 메인 클래스

```js
public class HelloSpringApp {

	public static void main(String[] args) {

		// load the spring configuration file
		ClassPathXmlApplicationContext context =
				new ClassPathXmlApplicationContext("applicationContext.xml");

		// retrieve bean from spring container
		Coach theCoach = context.getBean("myCoach", Coach.class);

		// call methods on the bean
		System.out.println(theCoach.getDailyWorkout());

		// let's call our new method for fortunes
		System.out.println(theCoach.getDailyFortune());

		// close the context
		context.close();
	}

}
```

## 4. Process of Setter Injection

1. Injection을 위한 setter 메소드를 클래스에 정의.

```java
public class CricketCoach implements Coach {

	private FortuneService fortuneService;

	// create a no-arg constructor
	public CricketCoach() {
		System.out.println("CricketCoach: inside no-arg constructor");
	}

	// our setter method
	public void setFortuneService(FortuneService fortuneService) {
		System.out.println("CricketCoach: inside setter method - setFortuneService");
		this.fortuneService = fortuneService;
	}

	@Override
	public String getDailyWorkout() {
		return "Practice fast bowling for 15 minutes";
	}

	@Override
	public String getDailyFortune() {
		return fortuneService.getFortune();
	}

}
```

2. 스프링 구성 파일에 의존성주입 구성.

```xml
<bean class="com.luv2code.springdemo.HappyFortuneService" id="myFortuneService">
</bean>

-<bean class="com.luv2code.springdemo.CricketCoach" id="myCricketCoach">
<!-- set up setter injection -->
<property ref="myFortuneService" name="fortuneService"/>
</bean>
```

3. 메인 클래스

```java
public class SetterDemoApp {

	public static void main(String[] args) {

		// load the spring configuration file
		ClassPathXmlApplicationContext context =
				new ClassPathXmlApplicationContext("applicationContext.xml");

		// retrieve bean from spring container
		CricketCoach theCoach = context.getBean("myCricketCoach", CricketCoach.class);

		// call methods on the bean
		// ... let's come back to this ...
		System.out.println(theCoach.getDailyWorkout());

		System.out.println(theCoach.getDailyFortune());

		// close the context
		context.close();
	}

}
```

## 5. Injecting Literal Values

1. Injection을 위한 setter 메소드를 클래스에 정의.

```java
public class CricketCoach implements Coach {

	private FortuneService fortuneService;

	// add new fields for emailAddress and team
	private String emailAddress;
	private String team;


	// create a no-arg constructor
	public CricketCoach() {
		System.out.println("CricketCoach: inside no-arg constructor");
	}

	public String getEmailAddress() {
		return emailAddress;
	}

	public void setEmailAddress(String emailAddress) {
		System.out.println("CricketCoach: inside setter method - setEmailAddress");
		this.emailAddress = emailAddress;
	}

	public String getTeam() {
		return team;
	}

	public void setTeam(String team) {
		System.out.println("CricketCoach: inside setter method - setTeam");
		this.team = team;
	}

	// our setter method
	public void setFortuneService(FortuneService fortuneService) {
		System.out.println("CricketCoach: inside setter method - setFortuneService");
		this.fortuneService = fortuneService;
	}

	@Override
	public String getDailyWorkout() {
		return "Practice fast bowling for 15 minutes";
	}

	@Override
	public String getDailyFortune() {
		return fortuneService.getFortune();
	}

}
```

2. 스프링 구성 파일에 의존성주입 구성.

```xml
<bean class="com.luv2code.springdemo.CricketCoach" id="myCricketCoach">
<!-- set up setter injection -->
<property ref="myFortuneService" name="fortuneService"/>
<!-- inject literal values -->
<property name="emailAddress" value="thebestcoach@luv2code.com"/>
<property name="team" value="Sunrisers Hyderabad"/>
</bean>
```

3. 메인 클래스

```js
public class SetterDemoApp {

	public static void main(String[] args) {

		// load the spring configuration file
		ClassPathXmlApplicationContext context =
				new ClassPathXmlApplicationContext("applicationContext.xml");

		// retrieve bean from spring container
		CricketCoach theCoach = context.getBean("myCricketCoach", CricketCoach.class);

		// call methods on the bean
		// ... let's come back to this ...
		System.out.println(theCoach.getDailyWorkout());

		System.out.println(theCoach.getDailyFortune());

		// call our new methods to get the literal values
		System.out.println(theCoach.getEmailAddress());

		System.out.println(theCoach.getTeam());

		// close the context
		context.close();
	}

}
```

## 6. Injecting Values from Properties File

1. name과 value로 이루어진 Properties 파일 생성.

```text
(파일명 : sport.properties)
foo.email=myeasycoach@luv2code.com
foo.team=Royal Challengers Bangalore
```

2. 스프링 구성 파일에서 Properties 파일을 로드.

```xml
<context:property-placeholder location="classpath:sport.properties"/>

<bean class="com.luv2code.springdemo.CricketCoach" id="myCricketCoach">
<!-- set up setter injection -->
<property ref="myFortuneService" name="fortuneService"/>
<!-- inject literal values -->
<property name="emailAddress" value="${foo.email}"/>
<property name="team" value="${foo.team}"/>
</bean>
```

3. 메인 클래스

```java
public class SetterDemoApp {

	public static void main(String[] args) {

		// load the spring configuration file
		ClassPathXmlApplicationContext context =
				new ClassPathXmlApplicationContext("applicationContext.xml");

		// retrieve bean from spring container
		CricketCoach theCoach = context.getBean("myCricketCoach", CricketCoach.class);

		// call methods on the bean
		// ... let's come back to this ...
		System.out.println(theCoach.getDailyWorkout());

		System.out.println(theCoach.getDailyFortune());

		// call our new methods to get the literal values
		System.out.println(theCoach.getEmailAddress());

		System.out.println(theCoach.getTeam());

		// close the context
		context.close();
	}

}
```
