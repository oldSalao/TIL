# Spring Dependency Injection - Annotations

## 1. Auto Wiring

Spring은 주어진 속성과 일치하는 클래스를 찾고 자동으로 의존성 주입을 수행한다. 이를 Auto Wiring이라고 한다.

### 1-1. Autowiring Injection Types

- Constructor Injection

- Setter Injection

- Field Injection

## 2. Constructor Injection

1. 종속 인터페이스,클래스 정의.

```java
public interface FortuneService{
    public String getFortune();
}
```

```java
@Component
public class HappyFortuneService implements FortuneService{
    public String getFortune(){
        return "Today is your lucky day!";
    }
}
```

2. 클래스에 주입을 위한 생성자 작성.

```java
@Component
public class TennisCoach implements Coach{
    private FortuneService fortuneService;

    public TennisCoach(FortuneService fortuneService){
        this.fortuneService = fortuneService;
    }
}
```

3. @Autowired annotation으로 의존성 주입 구성. 아래 예시의 경우에 Spring은 FortuneService 인터페이스를 구현한 클래스를 찾고 의존성 주입을 자동으로 수행한다. 구현체가 여러개일 경우에는 @Qualifier를 사용한다.

```java
@Component
public class TennisCoach implements Coach{
    private FortuneService fortuneService;

    @Autowired
    public TennisCoach(FortuneService fortuneService){
        this.fortuneService = fortuneService;
    }
}
```

## 3. Setter Injection

1. 클래스에 주입을 위한 setter 메소드 작성.

```java
@Component
public class TennisCoach implements Coach{
    private FortuneService fortuneService;

    public TennisCoach(){
    }

    public void setFortuneService(FortuneService fortuneService){
        this.fortuneService = fortuneService;
    }
    ...
}
```

2. @Autowired annotation으로 의존성 주입 구성.

```java
@Component
public class TennisCoach implements Coach{
    private FortuneService fortuneService;

    public TennisCoach(){
    }

    @Autowired
    public void setFortuneService(FortuneService fortuneService){
        this.fortuneService = fortuneService;
    }
    ...
}
```

## 4. Method Injection

의존성 주입은 생성자, setter 뿐만 아니라 Class 내의 모든 Method에 @Autowired로 적용이 가능하다.

```java
@Component
public class TennisCoach implements Coach{
    private FortuneService fortuneService;

    public TennisCoach(){
    }

    @Autowired
    public void doSomeCrazyStuff(FortuneService fortuneService){
        this.fortuneService = fortuneService;
    }
    ...
}
```

## 5. Field Injection

Class에 직접 field value를 세팅하여 의존성을 주입할 수 있다. (private field도 가능.) Java Reflection을 사용하여 수행된다.

@Autowired annotation으로 의존성 주입 구성.

- field에 직접 적용.

- setter method 필요없음.

```java
public class TennisCoach implements Coach{
    @Autowired
    private FortuneService fortuneService;

    public TennisCoach(){
    }
    ...
}
```

## 6. Qualifiers for Dependency Injection

Qualifier annotation은 Autowired annotation을 사용할 때 Spring이 여러개의 구현체 중 특정 구현체를 주입할 수 있도록 하는 annotation이다.

@Qualifier("beanID")

```java
@Component
public class TennisCoach implements Coach{
    @Autowired
    @Qualifier("happyFortuneService")
    private FortuneService fortuneService;
    ...
}
```

생성자에 @Qualified를 적용할때는 아래와 같이 적용한다.

```java
@Component
public class TennisCoach implements Coach {

    private FortuneService fortuneService;

    public TennisCoach() {
        System.out.println(">> TennisCoach: inside default constructor");
    }

    @Autowired
    public TennisCoach(@Qualifier("randomFortuneService") FortuneService theFortuneService) {

        System.out.println(">> TennisCoach: inside constructor using @autowired and @qualifier");

        fortuneService = theFortuneService;
    }

    @Override
    public String getDailyWorkout() {
        return "Practice your backhand volley";
    }

    @Override
    public String getDailyFortune() {
        return fortuneService.getFortune();
    }

}
```

## 7. Inject properties file

1. properties 파일생성.

```properties
foo.email=myeasycoach@luv2code.com
foo.team=Silly Java Coders
```

2. applicationContext.xml에 다음 내용 추가

```xml
<context:property-placeholder location="classpath:sport.properties"/>
```

3. @Value annotation을 사용하여 주입

```java
@Value("${foo.email}")
private String email;

@Value("${foo.team}")
private String team;
```
