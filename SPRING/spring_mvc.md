# Spring MVC

## 1. What is Spring MVC?

- 자바에서 웹 어플리케이션을 만들기위해 사용하는 프레임워크.

- Model-View-Controller 디자인패턴을 기반으로 한다.

- Core Spring 프레임워크의 기능을 활용한다.(IoC,DI)

## 2. Components of a Spring MVC Application

- UI 컴포넌트의 레이아웃을 위한 웹 페이지의 집합.

- Spring bean의 집합.

- Spring configuration.

## 3. How Spring MVC Works Behind the Scenes.

![](./common/images/mvc.jpg)

### 3-1. Front Controller

모든것은 브라우저로부터 요청이 들어오면서 시작되고 front controller라는 것을 만나게 된다.

- Front Controller는 DispatcherServlet이라고 알려져 있다. 요청을 시스템 내의 다른 객체나 요소들에게 위임하는 일을 한다.

  - Spring 프레임 워크의 한 부분이다.

  - Spring 개발 팀에 의해 이미 개발되어 있다.

- 우리가 개발해야 할 것

  - Model objects

  - View templates

  - Controller classes

### 3-2. Controller

- 개발자가 작성해야 하는 부분.

- business 로직을 포함한다.

  - 요청을 다룬다.

  - 데이터를 저장하거나 가져온다.

  - 데이터를 model에 위치시킨다.

- 데이터를 포함하고 있는 model을 적절한 view template으로 보낸다.

### 3-3. Model

- 데이터를 포함하고 있다.

- backend 시스템을 통해 데이터를 저장하거나 가져온다.

  - DB, web service, etc...

  - 원한다면 Spring bean을 사용한다.

### 3-4. View Template

- Spring MVC는 유연하다.

  - 다양한 view template을 지원한다.

- 가장 일반적인 것은 JSP + JSTL이다.

- 개발자는 페이지를 만들고 그 페이지를 통해 사용자에게 데이터를 보여준다.

## 4. Spring MVC Configuration

- web.xml에 내용 추가.

1. Spring MVC의 Dispatcher Servlet 구성.

file: web.xml

```xml
<web-app>

    <servlet>
        <servlet-name>dispatcher</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>

        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>/WEB-INF/spring-mvc-demo-servlet.xml</param-value>
        </init-param>

        <load-on-startup>1</load-on-startup>
    </servlet>

</web-app>
```

2. Dispatcher Servlet에 URL 매핑 설정.

file: web.xml

```xml
<web-app>

    <servlet>
        <servlet-name>dispatcher</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        ...
    </servlet>

    <servlet-mapping>
        <servlet-name>dispatcher</servlet-name>
        <url-pattern>/</url-pattern>
    </servlet-mapping>

</web-app>
```

3. Spring component scanning을 위한 부분 추가.

file: spring-mvc-demo-servlet.xml

```xml
<beans>
    <context:component-scan base-package="com.example"/>
</beans>
```

4. conversion, formatting, validation을 위한 부분 추가.

file: spring-mvc-demo-servlet.xml

```xml
<beans>
    <context:component-scan base-package="com.example"/>

    <mvc:annotation-driven/>
</beans>
```

4. Spring MVC View Resolver 구성.

file: spring-mvc-demo-servlet.xml

```xml
<beans>
    <context:component-scan base-package="com.example"/>

    <mvc:annotation-driven/>

    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/view/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
</beans>
```

## 5. Creating a Spring Home Controller and View

1. Controller 클래스 생성. @Controller annotation은 기본적으로 해당 클래스가 Spring MVC controller임을 명시. 또한 @Controller는 @Component를 상속받음. 따라서 scanning을 지원함.

```java
@Controller
public class HomeController{

}
```

2. Controller method 정의.

```java
@Controller
public class HomeController{

    public String showMyPage(){
        ...
    }

}
```

3. Controller method에 Request Mapping 추가.

```java
@Controller
public class HomeController{

    @RequestMapping("/")
    public String showMyPage(){
        ...
    }

}
```

4. View 이름을 반환.

```java
@Controller
public class HomeController{

    @RequestMapping("/")
    public String showMyPage(){
        return "main-menu";
    }

}
```

5. View Page 생성.
   file: /WEB-INF/view/main-menu.jsp

```html
<%@ page contentType="text/html;charset=UTF-8" language="java" %>
<html>
  <head>
    <title>Hello Spring MVC!</title>
  </head>
  <body>
    <h2>Spring MVC Demo - Home Page</h2>
  </body>
</html>
```

## 6. Adding Data to the Spring Model

### 6-1. Spring Model

- Model은 application data를 위한 컨테이너이다.

- Controller에서 Model로 무엇이든 넣을 수 있다. (String, Object, info from DB, etc...)

- View page(JSP)에서 model의 데이터에 접근할 수 있다.

### 6-2. 예시

1. Model을 Controller에 전달.

   Controller method에 Model 파라미터를 추가하고 Model.addAttribute("이름",값) 을 통해 Model에 데이터를 담을 수 있다.

```java
@RequestMapping("processFormVersionTwo")
public String letsShoutDude(HttpServletRequest request, Model model){

    String theName = request.getParameter("studentName");

    theName = theName.toUpperCase();

    String result = "Yo! " + theName;

    model.addAttribute("message",result);

    return "helloworld";
}
```

2. View Template -JSP

   JSP에서 ${}안에 Controller method에서 넘긴 Model의 데이터 이름을 작성하여 접근할 수 있다

```html
<html>
  <body>
    Hello World of Spring!<br />
    ...<br />
    The message: ${message}
  </body>
</html>
```

## 7. Binding Request Params
