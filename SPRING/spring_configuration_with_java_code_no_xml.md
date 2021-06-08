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
