---
layout: post
title:  "[SpringBoot] SpringBoot 개발환경 구성 - 1"
subtitle:   ""
categories: devlog
tags: java springboot
comments: true
---

SpringBoot로 인해 확실히 기존의  Spring기반 웹어플리케이션 프로젝트를 셋업하는데 좀 더 편하고 빠르게 할 수 있게 된 것 같다.



그 동안 많은 자바개발자들이 localhost로 'Hello, Java!' 를  한번 찍어보기 위해서 
톰캣설치 및 설정등 상당히 준비작업들과 시행착오를 겪어야만 했었는데 SpringBoot가 나오면서 
그런 부분들을 많이 해소해 준것 같다.

이 글은 JetBrain의 IntelliJ IDE기반으로 작성된 글이다.



---

### 프로젝트 생성

우선 IntellJ를 실행하고 `InteliJ IDEA > preference` 항목으로 들어가서 Spring Boot Plug-In 을 설치한다.

![](https://t1.daumcdn.net/cfile/tistory/996A9833598FD7571D)

---

`File -> New -> Project` 를 클릭하면 프로젝트 템플릿을 선택할 수 있는데 SpringBoot Plug-in을 설치했으면 Spring Initializr 항목이 보인다.

![](https://monosnap.com/file/lmMcGe29AtyknnvIjEkePm7yPwjusc.png) 

프로젝트 타입은 편한걸로 선택하면 된다.
본인은 Maven에 익숙하니, Maven Project로 선택했다.

지금은 Embeded된 톰캣으로 Stand-Alone형태로 구동시키기 위한 목적이므로
Packagin Type을 jar로 선택한다.

![](https://monosnap.com/file/X9fsZ1t8aUYdcenlggmGEsRqkpy1AE.png)

war로 선택할 경우, 기존과 같이 외부의 톰캣으로 디플로이 하는 구조로 만들어진다.
물론, 소스의 최종배포의 형태가 서버의 톰캣에 디플로이해야 하는 구조라면  처음부터 War로 만들어서 작업해도 상관없다.

지금 얼마나 빨리, 간편하게 웹어플리케이션을 만들어서 실행할 수 있는가를 확인하기 위함이니
jar로 선택하고, 로컬개발 및 테스트를 하다가  나중에 배포할 경우 war로 변경해서 배포를 할 수도 있다.


이 부분과 War방식의 프로젝트 생성방법도 별도로 포스팅할 예정이다.

![](https://monosnap.com/file/Efx4agk87okbKPQ75kqHMN0HmvbUjj.png)

필요한 라이브러리를 자기 입맛에 맞게 선택한다. 
프로젝트 생성 후 나중에 pom.xml로 별도로 추가할 수 있으니, 꼭 필요한 라이브러만 선택하고 넘어가면 된다.
선택하지 않아도 아무런 문제가 되지 않는다. Web은 선택해주는것이 편하다.
SpringBoot를 이용한  톰캣기반 웹프로젝트가 생성되었다.
SpringBoot를 실행하기전에 만들어진 프로젝트의 구조를 잠시 살펴보자


### 프로젝트 소스 구성

---

![프로젝트 구조](https://monosnap.com/file/4ByYwlR1RZAfSG8fb6QZ5eIXxCCQ3O.png)

- 메인클래스: SpringBootRestDemoApplication
- 프로퍼티파일: application.properties 
- 환경설정파일: pom.xml

스프링부트기반으로 프로젝트를 생성하게 되면
기존의 전통적인 웹어플리케이션 방식에서 필수로 관리되어야 하는 톰캣설정 및 web.xml파일등은 
스프링부트의 내부모듈에 의해서 구동시 자동설정된다. 


### 어플리케이션 실행

---

간단하다. 메인클래스를 Run시키면 SpringBoot 특유의 로고와 함께 로그가 올라오면서 실행된다.
여기서 바로 성공! 하면 좋을텐데.... 아래와 같은 에러가 나면서 어플리케이션 시작이 실패된다. 


Cannot determine embedded database driver class for database type NONE


> If you want an embedded database please put a supported one on the classpath. 
If you have database settings to be loaded from a particular profile you may need to active it (no profiles are currently active).


해석해보면,
데이타베이스 type이 None이라 임베디드된 데이타베이스 드라이버를 결정할 수 없다.

이 에러는 SpringBoot 라이브러리 설정시 JDBC를 선택했을 때 발생한다. 초기에 DB Connection관련 어떠한 라이브러리도
추가하지 않았으면 이 에러는 발생하지 않지만, 우리가 만들려고 하는 어플리케이션은 대부분 DB설정이 필수이기 때문에
이 에러에 대한 원인과 조치방법은 꼭 알아두어야 할 필요가 있다.
  

하나의 임베디드된 데이타베이스를 쓰고 싶다면 클래스패스에 지원되는 드라이버 파일을 넣어라.
profile로부터 로드하기 위한 데이터베이스 세팅을 가지고 있다면, profile을 활성화시켜야 한다.

SpringBoot는 어플리케이션이 시작될때 필요한 기본 설정들을 자동으로 설정하게 되어 있는데 (Auto Configuration)
그 중 DataSource설정이 자동구성 될 때 필요한 Database Type 정보들이 설정되어 있지 않아서 발생하는 문제이다.

프로젝트가 생성될 때  application.properties파일이  자동 생성되었으나 빈 파일로 생성된다.
사용자가 원하는 db를 선택하고 거기에 맞는 드라이버 라이브러리 설치와 jdbc설정을 해야 한다는 의미이다.

이렇게 해결을 할 수도 있으나
당장 jdbc설정이 필요없고 어떤 db를 사용할지 결정도 안된 상태이다.
스프링부트의 Datasource 자동설정을 사용하지 않고, 어플리케이션 독립적인 DataSource구성을 하기 위해서 이럴 경우 해결할 수 있는 방법은 없을까?

아래와 같이 SpringBoot 메인클래스에 Annotation을 추가함으로써
SpringBoot시작시 실행되는 Auto Configuration 작업중 DatatSource 설정부분을 
제외시킬 수 있다.

``` java
@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})
```

**스프링 부트 메인 클래스**
``` java 

// SpringBoot 메인클래스 
package com.springboot.demo;
 
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration;
 
@SpringBootApplication
@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})  // Datasource설정은 자동설정에서 제외 
public class SpringbootRestDemoApplication {
 
 public static void main(String[] args) {
  SpringApplication.run(SpringbootRestDemoApplication.class, args);
 }
}
```

위의 어노테이션을 추가하고 다시 스프링부트를 구동하면, 정상적으로 SpringBoot 어플리케이션이 실행된다.
![](https://monosnap.com/file/pSUSLbRTwARYJ4K4QNpREcMl56k0D1.png) 

> 나중에 기회가 되면 다룰 예정이지만, 스프링부트가 구동될때 출력되는 메세지는 스프릉부트 어플리케이션의 구조와 설정정보등의
아주 중요한 정보들을 담고 있다. 

브라우저를 열고 http://localhost:8080 을 입력하자. 참고로 톰캣의 포트는 기본적으로 8080으로 지정되고
application.properties 파일에서 '변경 가능하다.

구동하면 처음에는 아래의 404 에러 메세지가 만나게 된다.

```
Whitelabel Error Page
This application has no explicit mapping for /error, so you are seeing this as a fallback.

Sun Aug 13 14:34:00 KST 2017
There was an unexpected error (type=Not Found, status=404).
No message available
```

톰캣이 인식해야 하는  index.html 파일이나, index.jsp이 아직 없기 떄문이니
웹 설정관련만 하면 해결되는 문제이다.


### SpringBoot Web Application 설정

---

SpringBoot는 프로젝트가 생성될때  Web 라이브러리를 추가한 경우, 정적인 웹 리소스들은 
src > main > resources > static 아래에서 관리되도록 설정된다. 

즉, `html`, `css`, `js`, `image`등의 정적컨텐츠는 static 폴더 아래에 위치시키면 접근가능하고, 
static이 루트폴더가 된다는 의미이다.

프로젝트를 생성할 당시, 라이브러를 추가할때 Web 라이브러를 추가했다면 static 폴더가 자동으로 만들어지는데, 
선택하지 않았다 하더라도 POM.xml파일에 아래의 Dependency를 추가하고  static폴더를 직접 만들어 주면 된다.

웹서비스가 필요한 어플리케이션인 경우,
스프링부트의 web 기본모듈을 설치하는게 좋고, 본격적으로 U.I가 필요한 화면들이 많이 필요한 경우에는
[Thymeleaf](https://www.thymeleaf.org/)와 같은 Server-Side 기반의 템플릿엔진을 추가해서 쓰도록 하자.


*Web 라이브러리 추가*
``` xml
<dependency>
 <groupid>org.springframework.boot</groupid>
 <artifactid>spring-boot-starter-web</artifactid>
</dependency>
```

static 폴더 아래에 index.html 파일을 간단하게 만들고 
'Hello, SpringBoot!' 를 입력하고 어플리케이션을 재구동한다.

다시 http://localhost:8080 로 접근해 보면 웹페이지가 정상적으로 출력된다.
이제 SpringBoot기반으로 웹어플리이케이션을 개발할 수 있는 기본적인 환경이 구성되었다.


다음 포스트에는
JSP를 사용하기 위한 설정과 Spring MVC기반의 웹어플리케이션 개발관련한 내용을 다루어보도록 하겠다.

---

### [참고문서]

---

- [스프링부트 공식 사이트](https://spring.io/projects/spring-boot)
- [스프링부트 Document](https://docs.spring.io/spring-boot/docs/current/reference/html/common-application-properties.html)