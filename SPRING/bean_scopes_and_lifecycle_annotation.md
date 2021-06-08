# Bean Scopes and Lifecycle - Annotation

## 1. @Scope Annotation

@Scope annotation을 사용하여 Bean의 Scope를 설정할 수 있다.

```java
@Component
@Scope("prototype")
public class TennisCoach implements Coach{
    ...
}
```

## 2. Bean Lifecycle Method Annotations.

annotation으로 Bean이 생성, 소멸될 때 실행될 custom code를 설정할 수 있다.

1. 생성 또는 소멸 시 호출할 method 정의.

2. annotation 추가 (@PostConstruct,@PreDestroy)

```java
@Component
public class TennisCoach implements Coach{

    @PostConstruct
    public void doMyStartupStuff(){...}
    ...
}
```
