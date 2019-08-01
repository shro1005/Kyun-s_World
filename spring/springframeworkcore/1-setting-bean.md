---
description: Xml 설정 파일을 통한 빈 설정 방법부터 현재 SpringBoot에서 사용하는 빈 설정방법까지
---

# 스프링 프레임워크 핵심기술 1 - 빈 설정방법과 의존성 주입

다양한 빈 설정방법과 의존성 주입 방법에 대해 공부해봤습니다. Spring초창기 부터 현재 Spring Boot에서 사용하는 빈 설정 방법과 의존성 주입방법을 알아보겠습니다.

먼저 스프링부트 프로젝트를 하나 만든 뒤 사용할 `BookService`와 `BookRepository` 클래스를 생성해 줍니다.

### 1. Xml 설정파일을 통해 Bean을 직접 등

초기에는 빈 등록 및 의존성 주입까지 xml을 통해 직접 등록을 했죠. 아래의 코드처럼 `application.xml` 파일에 beans 요소를 통해 빈을 등록할 수 있습니다. 

```markup
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd">
	
	<bean id="bookService" 
		  class="study.spring.springApplicationContext.BookService">  
		 <property name="bookRepository" ref="bookRepository"></property> 
	</bean>
	
	<bean id="bookRepository"
		  class="study.spring.springApplicationContext.BookRepository">
	</bean>
	
</beans>

```

빈 등록에 사용된 bean요소의 경우 해당 빈의 이름인 id와 빈으로 설정할 class\(타입\)를 주어 해당 class를 빈으로 등록합니다. id와 bean 속성은 반드시 설정해줘야 하는 속성들이며, 그 이외에도 scope, autowire 등 다양한 속성을 줄 수 있습니다.  

* id : 빈의 이름, id가 중복되는 빈은 있어선 안된다. 소문자로 시작하는 것이 원칙!
* class : 등록할 클래스 타입을 준다. 
* scope : 해당 빈을 싱글톤으로 만들지 프로토타입으로 만들지 설정할 수 있다.
* autowire : 어떤 autowire모드를 사용할 지 설정할 수 있다. \(보통 default 사용\)

 이 처럼 Bean 을 등록하고, property 요소를 사용하여 다른 빈의 의존성을 부여할 수 있습니다. 

name의 'bookRepository' 경우는 앞서 만든 `BookService` 클래스의 `BookRepository`받는 setter에서 가져온것 이고  ref의  'bookRepository' 경우 등록된 빈의 id를 가져온 것입니다. 이렇게 property를 세팅하여 의존성을 주입할 수 있니다.

```java
public class BookService {
	BookRepository bookRepository;

	public void setBookRepository(BookRepository bookRepository) {
		this.bookRepository = bookRepository;
	}
}
```



### 2. &lt;context:component-scan&gt; 태그를 활용한 빈 등록 

하지만 위와 같이 일일이 빈을 등록과 의존성을 주입하면 굉장히 시간도 오래 걸리며 번거롭고 또 실수가 발생할 수 있죠. 그래서 나온 방식이 `<context:component-scan>` 태그입니다. 

Spring2.5부터 빈으로 등록하고 싶은 클래스에 @Component\(@Service, @Repository, @Configuration \) 어노테이션을 설정하고  &lt;context:component-scan&gt; 태그에서 base-package를 설정해주게 되면 해당 패키지 및 하위 패키지안의 클래스를 스캔하여 어노테이션이 있으면 해당 클래스 빈으로 등록합니다.

또 `@Autowired` 어노테이션을 통해 쉽게 의존성을 주입을 할 수 있죠. `@Autowired` 어노테이션의 경우 생성자, setter, 필드 어느곳에 붙여도 상관 없습니다. 그리고 required를 false로 주면 해당 `BookRepository`가 빈으로 등록되지 않아도 에러가 나지 않게 할 수 도 있습니다.

**BookService.java**

```java
@Service  
public class BookService {
	@Autowired(required = false)
	BookRepository bookRepository;

	public void setBookRepository(BookRepository bookRepository) {
		this.bookRepository = bookRepository;
	}
}
```

**BookRepository.java**

```java
@Repository
public interface BookRepository {

}
```

**application.xml**

```markup
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:context="http://www.springframework.org/schema/context"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context.xsd">

	<context:component-scan base-package = "study.spring.springApplicationContext"></context:component-scan>

</beans>
```

### 3. 클래스를 활용한 빈 등록 \(@configuration\)

하지만 `<context:component-scan>` 태그를 활용한 빈 등록 역시 xml 설정 파일이 필요하죠. 설정 파일을 따로 만들지 않고 java 클래스에서 이런 설정 파일 대신 관리해주는 방법을 알아보죠.

바로 `@configuration` 어노테이션을 사용하면 해당 클래스에서 xml설정 파일을 대신할 수 있습니다.

저는 `ApplicationConfig` 클래스를 만들어 해당 클래스에서 설정을 했습니다. Java 클래스에서 설정을 하더라도 컴포넌트 스캔이 필요하겠죠?  Spring에서 `@ComponentScan` 어노테이션을 통해 이를 해결할 수 있습니다. `basePackageClasses` 에 원하는 클래스를 주게되면 해당 클래스가 있는 패키지부터 하위 패키지의 컴포넌트 어노테이션들을 모두 스캔해서 빈에 등록합니다.

```java
@Configuration
@ComponentScan(basePackageClasses = DeomApplication.class)
public class ApplicationConfig {
	
	@Bean
	public BookRepository bookRepository() {
		return new BookRepository();
	}
	
	@Bean
	public BookService bookService() {
		BookService bookService = new BookService()
		bookService.setBookRepository(bookRepository()
		return bookService;
	}
}
```

어? 2번에서 `BookRepository`, `BookService`에 어노테이션을 줬는데 왜 여기서 `@Bean` 어노테이션을 주는지 의아해 하실 수 있습니다. `@Bean`의 경우 내가 작성하지 않은 클래스를 빈으로 등록하고 싶을 때 해당 클래스를 인스턴스화 하는 메소드에 붙여 사용할 수 있습니다.  따라서 아래처럼 컴포넌트 어노테이션이 없어도 `@Bean`을 통해 정상적으로 등록되죠.

**BookService.java**

```java
public class BookService {
	@Autowired(required = false)
	BookRepository bookRepository;

	public void setBookRepository(BookRepository bookRepository) {
		this.bookRepository = bookRepository;
	}
}
```

**BookRepository.java**

```java
public interface BookRepository {

}
```

자 설정파일이 변경됐으니 AppicationContext에도 변경사항이 생겨야 겠죠? 앞서 설명하지 않았지만 우리가 xml을 통해 설정하게 되면 ClassPathXmlApplicationContext 클래스를 사용해서 설정파일을 받아야합니다. 

하지만 java클래스를 통해 설정을 하고 싶으면 AnnotationConfigApplicationContext 클래스를 사용하시면 됩니다. 아주 간단하죠.

```java
public class DeomApplication {

	public static void main(String[] args) {
		//Xml 설정파일 사용시 - ClassPathXmlApplicationContext 사
		ApplicationContext context = new ClassPathXmlApplicationContext("application.xml");
		
		//java 클래스 설정 사용시 - AnnotationConfigApplicationContext 사
		ApplicationContext context = new AnnotationConfigApplicationContext(AplicationConfig.class);
		
		BookService bookService = (BookService) context.getBean("bookService");
		// 의존성 주입이 됐는지 확인 
		System.out.println(bookService.bookRepository != null); 
	}
}
```

 

### 4. SpringBoot는 어떻게?

그렇다면 우리가 앞으로 사용할 Spring Boot는 어떻게 빈 설정을 하고 의존성을 주입할지가 궁금해 집니다. 3번 방법과 거의 동일 하다고 보시면 됩니다. 직접 만든 클래스에는 `@Component`\(`@Service`, `@Repository`, `@Configuration` \) 어노테이션을 사용하고 다른 클래스를 빈에 등록하고 싶으면 `@Bean` 을 사용하면 되죠. 의존성 주입은 `@Autowired` 를 통해 할 수 있습니다.

다만 변하는 것은 3번의 설정 java클래스인 `ApplicationConfig`를 만들필요가 없다는 것이죠. 우리가 Spring Boot프로젝트를 생성하면 main클래스인 Application을 보면 `@SpringBootApplication` 어노테이션이 있는것을 알 수 있죠. 해당 어노테이션을 보면 다음과 같이 `@ComponentScan` 과 @SpringBootConfiguration이 있는것을 알 수 있고,  그 안에 @Configuration이 있습니다.

즉, 따로 설정 클래스를 만들필요 없이 SpringApplication으로 지정해줄 클래스 자체가 설정 클래스 역할도 하게 되는 것이죠. 또한 

**SpringBootApplication.java**

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(excludeFilters = { @Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
		@Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
public @interface SpringBootApplication {

  ...

}
```

**SpringBootConfiguration.java**

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Configuration
public @interface SpringBootConfiguration {

}
```

이렇게 xml을 통한 빈설정 부터 현재 SpringBoot를 사용함에 있어  빈을 설정하는 방법까지 알아봤습니다. 개발자의 편의를 위해 많이 좋아졌다는게 체감됩니다. 아무 생각없이 사용했던 어노테이션들이 어떤 역할을 하는지 좀더 자세히 알게되어 기쁩니다. 

