# Spring Configuration with Java Code (no xml)

XML 대신에 Java 코드를 이용해서 Spring 컨테이너를 구성할 수 있다.

## 1. Spring Configuration.

1. Java 클래스를 생성하고 @Configuration annotation을 적용한다.

```java
@Configuration
public class SportConfig{

}
```

2. Component scan을 수행하려면 @ComponentScan annotation을 적용한다.

```java
@Configuration
@ComponentScan("com.example")
public class SportConfig{

}
```

3. 이렇게 만들어진 클래스를 사용한다.

```java
AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(SportConfig.class);
```

4. Spring Container 에서 Bean을 얻는다.

```java
Coach theCoach = context.getBean("tennisCoach",Coach.class);
```

## 2. Defining Spring Beans.

1. Bean을 나타내는 method 정의. 이때 method의 이름은 곧 bean ID가 된다.

```java
@Configuration
public class SportConfig{

    @Bean
    public Coach swimCoach(){
        SwimCoach mySwimCoach = new SwimCoach();

        return mySwimCoach;
    }

}
```

2. Bean 의존성 주입.

```java
@Configuration
public class SportConfig{

    @Bean
    public FortuneService happyFortuneService(){
        return new HappyFortuneService();
    }

    @Bean
    public Coach swimCoach(){
        SwimCoach mySwimCoach = new SwimCoach(happyFortuneService());

        return mySwimCoach;
    }

}
```

3. Java configuration 클래스를 사용.

```java
AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(SportConfig.class);
```

4. Spring Container 에서 Bean을 얻는다.

```java
Coach theCoach = context.getBean("swimCoach",Coach.class);
```

## 2. Injecting Values from Properties File

1. properties 파일 생성

```properties
foo.email=myeasycoach@luv2code.com
foo.team=Awesome Java Coders
```

2. config 클래스에서 properties 파일 로드

```java
@Configuration
@PropertySource("classpath:sport.properties")
public class SprotConfig{
    ...
}
```

3. properties 파일로부터 값을 참조.

```java
public class SwimCoach implements Coach{

    @Value("${foo.email}")
    private String email;

    @Value("${foo.team}")
    private String team;

    ...
}
```
