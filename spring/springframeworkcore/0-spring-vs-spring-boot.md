---
description: Spring Boot가 Spring MVC와 뭐가 다른가
---

# 스프링 프레임워크 핵심기술 0 - Spring Boot 와 Spring MVC 차이

 최근에 스프링 프레임워크 학습을 할때 Spring Boot로 시작해라 라는 말을 많이 듣게 되어 스프링 핵심 기술\(core\)에 앞서 Spring\(Spring MVC\)와 Spring Boot의 차이를 알아보았습니다.

모든 Spring 모듈들의 핵심은 의존성 주입과 IoC\(Inversion of Control\)이라고 할 수 있습니다. 이렇게 의존성 주입과 IoC를 통해 소스변경을 최소화 하며 프로그램을 제어할 수 있습니다. 

그 중에서도 Spring Boot를 사용하면 우린 좀더 쉽게 의존성 주입을 받을 수 있습니다. 우리가 웹 어플리케이션을 개발한다고 가정해 보죠. 가장 먼저 우리는 사용하고 싶은 프레임워크들과 그 프레임워크들의 버전을 선택하고 그것들을 연결할 방법을 찾을 겁니다. 

좀더 자세히 설명해보면, 모든 웹 애플리케이션들이 다음과 비슷한 요구사항들을 갖죠.  Spring MVC, Jackson Databind \(데이터 바인딩 용\), Hibernate-Validator \(Java Validation API 를 이용한 서버사이드 유효성 확인 용\), Log4j \(로깅용\). 우리가 이 코스를 생성하려면 이 모든 프레임워크들이 호환되는 버전을 선택해야 했습니다.



하지만 Spring Boot는 스타터들을 제공합니다. 아래는 Spring Boot에서 언급한 스타터입니다.

> 스타터들은 편리한 종속성 기술자들\(dependency descriptors\)로서 여러분은 이 것을 애플리케이션에 포함시킬 수 있다. 여러분은 모든 스프링과 여러분이 필요로하는 관련 기술을 얻을 수 있는 올인원 쇼핑몰을 얻는 것으로 굳이 샘플코드를 찾아보거나 로드할 종속성 기술자들을 복사/붙여넣기 하지 않아도 된다. 예를들어 여러분이 스프링과 데이터베이스 접근을위한 JPA 를 사용하고 싶다면 여러분의 프로젝트에 spring-boot-starter-data-jpa 종속성을 포함시키고 진행하면 된다.

스타터의 예로 Spring Boot Starter Web 들어봅시다.  
  
웹 애플리케이션을 개발하거 싶어한다면 Spring Boot Start Web 을 선택할 수 있겠죠. Spring Initializer 를 이용해서 Spring Boot Starter Web 을 이용하는 프로젝트를 생성하게 되면 아래의 코드 처럼 자동으로 우리가 Spring Web에서 사용하는 다양한 의존성들을 받게 됩니다.



```markup
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.1.6.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<groupId>study.spring</groupId>
	<artifactId>springApplicationContext</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>deom</name>
	<description>Demo project for Spring Boot</description>

	<properties>
		<java.version>1.8</java.version>
	</properties>

	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId> <!--해당되는 라이브러리에서 의존성들을 보장한다. -->
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>

</project>

```



Spring Boot는 클래스 패스상에 사용가능한 프레임 워크와 이미 있는 환경설정을 바라보며, 어플리케이션을 해당 프레임워크들과 함께 구성하는 기본 환경설정을 제공합니다. 이를 Auto Configuration\(자동 구성\)이라 하며 이를 통해 사용자가 보다 쉽게 개발에 집중할 수 있게 됩니다.



그럼 모든 프로젝트에서 Spring Boot를 사용하는 것이 좋을 까요?

예를 들어 다시 하나의 웹  어플리케이션을 만든다고 가정하죠. 해당 어플리케이션의 규모가 작아 돈을 주고 서버에 WAS 설치하게 된다면 이는 전혀 효과적이라고 할 수 없습니다. 하지만 Spring Boot의 경우 embeded container에서 자기의 어플리케이션을 실행하는 구조로 돼있어 JAVA만 설치해도 어플리케이션을 만들 수 있습니다. 이는 Spring Boot의 또 다른 장점이지만 단점이 될 수 있습니다.

비교적 큰 웹 어플리케이션을 만들 경우 이런 구조로 만드는 것 보단 Spring MVC 형태로 만들어 WAS에 배포하는 것이 효과적입니다. embeded container에서 큰 규모의 어플리케이션을 실행하는 것이 불안정하기도 하며 WAS에서 관리하는 데이터 소스나 메세지 등을 활용할 수 있고, 형상관리에도 유리하죠.

이 처럼 어떤 웹을 개발 하느냐에 따라 Spring Boot 가 더 적합한지, 아니면 Spring MVC가 더 적합한지 나뉜다고 볼 수 있죠.



이렇게 Spring Boot가 기존 Spring\(Spring MVC\)와 어떤 점이 다르고 어떤 장점을 가지는지 알아 봤습니다. 물론 더 많은 차이가 존재하겠지만 뚜렷한 장점들은 저정도인 것으로 보입니다. 장점이 크게 좋아 보이지 않다고 생각하시는 분들이 있을 수 있습니다. 실제로 현업에는 큰 규모의 웹서비스가 필요로 하기 때문에 Spring MVC를 사용하며, 초기 설정이외에는 환경 설정에 큰 메리트가 없다는 이야기도 많습니다. 그럼에도 직접 사용해 보면 굉장히 유용한 모듈이라고 생각합니다.  기회가 된다면 Spring Boot, Spring MVC 둘다 공부하고 사용해 보는것도 좋아보입니다. :D  

 

\(\*\)참고

갑자기 Spring Boot의 embeded Tomcat WAS의 성능이 궁금하여 찾아본 결과 embeded Tomcat \(Spring Boot\)에서 APR을 활성화 한 후에는 외장 Tomcat과 비교하여 성능이 동일하다고 합니다.

[https://stackoverflow.com/questions/40319869/spring-boot-embedded-tomcat-performance](https://stackoverflow.com/questions/40319869/spring-boot-embedded-tomcat-performance)

\(기본적으로 내장 된 Tomcat은 NIO를 실행합니다. NIO와 APR의 성능을 비교할 때 APR은 훨씬 빠릅니다. 하지만 사실 모든 Linux 기반의 tomcat 번들은 tomcat lib 폴더 아래에 APR 라이브러리와 함께 제공되기 때문에 embeded Tomcat에서도 APR을 활성화 할 수 있다고 합니다.\)

또 Spring Boot의 내장 톰켓 설정도 ServletWebServerFactoryAutoConfiguration 등의 Class에서 변경할 수 있으며 아래의 의존성을 부여하면 내장 톰캣의 로그를 출력할 수 있습니다.

```markup
<dependency>
      <groupId>org.apache.logging.log4j</groupId>
      <artifactId>log4j-jul</artifactId>
     </dependency>
```

아래 링크는 내장 톰켓 로그를 Log4j 에 보이도록 하는 방법이 더 자세하게 나와있으니 참고하시기 바랍니다.

[https://stackoverflow.com/questions/48312851/spring-boot-embedded-tomcat-logs](https://stackoverflow.com/questions/48312851/spring-boot-embedded-tomcat-logs) 

