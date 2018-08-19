---
layout: post
title:  "[Java/Spring] Spring 진영의 주요 Tech Trend  - 1"
subtitle:   ""
categories: devlog
tags: java, spring, spring framework, spring boot, spring cloud, spring cloud dataflow
comments: true
---



어떤 언어이든 이제는 기술의 화두가 간결함, 빠른적용, 분산, 그리고 분산의 연결, 클라우드 플랫폼을 지향하고 있다. 현재 Spring 진영의 핵심 기술 축- Tech Trend-도 역시 이런 기조에 맞춰 아래와 같이 크게 3가지 영역으로 진화 중인 것 같다.

1. Spring Boot
2. Spring Cloud
3. Spring Cloud DataFlow



![image-20180819161115647](https://t1.daumcdn.net/cfile/tistory/992D88395B791BC803)



### 1. Spring Boot 

Buid Anything - 어떤 것이든 빌드한다. 

> Spring Boot is designed to get you up and running as quickly as possible, with minimal upfront configuration of Spring. Spring Boot takes an opinionated view of building production ready applications.

지금 자바 개발자들에게는 없어서는 안될 필수 기술요소로 자리잡아 가고 있는 중이다. 아니, 이미 자리를 잡았다고 봐야 할 것 같다.   xml의 지옥(?)에서 벗어날 수 있는데 안 쓸 이유가 없다. 자바도 이제 타 서버사이드 언어에 빠르고 쉽게 서비스 배포가 가능한 환경을 가질 수 있게 되었다. 그 밖에도 전통적인 자바기반의 개발환경에 익숙해져 있던 개발자들에게는 정말 필요한 기능과 편리함을 제공해주는 라이브러리들의 총집합체라 할 수 있다.

- Build anything - REST API, WebSocket, Web, Streaming, Tasks, and more
- Simplified Security
- Rich support for SQL and NoSQL
- Embedded runtime support - Tomcat, Jetty, and Undertow
- Developer productivity tools such as live reload and auto restart
- Curated dependencies that just work
- Production-ready features such as tracing, metrics and health status

위의 특징들은 굳이 설명을 하지 않아도, 우리 Java개발자들이 현재 Spring Boot를 쓰면서 충분히 누리고 있는 편리한 기능들이다.

벌써 2.0 버전이 나왔고, 기술적으로 굉장히 큰 변화가 생겼다. 앞으로 자바진영의 메인 스트림 버전은 Spring Framework 5 + Sprin Boot 2.0 이 될 것이고 JDK1.9기반의  Runtime 환경을 염두 해 두고 계속 발전될 것이다.



![](https://spring.io/img/homepage/diagram-boot-reactor.svg)



새로 출시된 스프링 프레임워크 5의 가장 중요한 키워드는 두 개일것 같다.

- Reactive
- Non-Blocking

기존의 Spirng Framework의 주요 기술 스펙이었던. Spring MVC, JPA, Servlet API들과 완전히 결을 달리하는 스펙들이 나왔고그 스펙들을 대표할 키워드가 `Reactive`,`WebFlux`,`Stream`,`Non-blocking` 으로 보인다. 아무래도 전통적인 웹기반의 기술들을 벗어난 새로운 기술들이 대거 도입, 적용된게 아닐까 추측해 본다.

이 주제에 대해서 별도 포스트로 다뤄 볼 예정이다.



### 2. Spring Cloud

Coordinate Anything: Distributed Systems simplified - 어떤 것이든 통합(조정)한다. 그 과정을 통해 단순화(간소화) 시킨다.

> Built directly on Spring Boot's innovative approach to enterprise Java, Spring Cloud simplifies distributed, microservice-style architecture by implementing proven patterns to bring resilience, reliability, and coordination to your microservices.

스프링부트의 엔터프라이즈 자바에 대한 혁신적인 접근방식을 기반으로 구현된 스프링 클라우드는, 마이크로서비스에 대한 검증된, 탄력적이고 안정적이며, 조정기능을 제공하는 검증된 패턴을 구현함으로써 분산된 마이크로서비스 아키텍쳐를 단순화(간소화)한다. 

![](https://spring.io/img/homepage/diagram-distributed-systems.svg)

스프링 클라우드의 핵심은 마이크로서비스이다.

스프링 클라우드는 마이크로서비스 기반의 분산된 시스템을 통합하고 관리해주는 라이브러리들이 집합이다. 즉, 클라우드 플랫폼 기반에서 마이크로서비스를 구축하기 위해서 필요한 기술들이라 할 수 있겠다. 아래는 스프링 클라우드에 포함된 메인 컴포넌트들이다.

Release train contents:

| Component                 | Edgware.SR4    | Finchley.SR1  | Finchley.BUILD-SNAPSHOT |
| ------------------------- | -------------- | ------------- | ----------------------- |
| spring-cloud-aws          | 1.2.3.RELEASE  | 2.0.0.RELEASE | 2.0.1.BUILD-SNAPSHOT    |
| spring-cloud-bus          | 1.3.3.RELEASE  | 2.0.0.RELEASE | 2.0.1.BUILD-SNAPSHOT    |
| spring-cloud-cli          | 1.4.1.RELEASE  | 2.0.0.RELEASE | 2.0.1.BUILD-SNAPSHOT    |
| spring-cloud-commons      | 1.3.4.RELEASE  | 2.0.1.RELEASE | 2.0.2.BUILD-SNAPSHOT    |
| spring-cloud-contract     | 1.2.5.RELEASE  | 2.0.1.RELEASE | 2.0.2.BUILD-SNAPSHOT    |
| spring-cloud-config       | 1.4.4.RELEASE  | 2.0.1.RELEASE | 2.0.2.BUILD-SNAPSHOT    |
| spring-cloud-netflix      | 1.4.5.RELEASE  | 2.0.1.RELEASE | 2.0.2.BUILD-SNAPSHOT    |
| spring-cloud-security     | 1.2.3.RELEASE  | 2.0.0.RELEASE | 2.0.1.BUILD-SNAPSHOT    |
| spring-cloud-cloudfoundry | 1.1.2.RELEASE  | 2.0.0.RELEASE | 2.0.1.BUILD-SNAPSHOT    |
| spring-cloud-consul       | 1.3.4.RELEASE  | 2.0.1.RELEASE | 2.0.2.BUILD-SNAPSHOT    |
| spring-cloud-sleuth       | 1.3.4.RELEASE  | 2.0.1.RELEASE | 2.0.2.BUILD-SNAPSHOT    |
| spring-cloud-stream       | Ditmars.SR4    | Elmhurst.SR1  | Elmhurst.BUILD-SNAPSHOT |
| spring-cloud-zookeeper    | 1.2.2.RELEASE  | 2.0.0.RELEASE | 2.0.1.BUILD-SNAPSHOT    |
| spring-boot               | 1.5.14.RELEASE | 2.0.4.RELEASE | 2.0.4.BUILD-SNAPSHOT    |
| spring-cloud-task         | 1.2.3.RELEASE  | 2.0.0.RELEASE | 2.0.1.BUILD-SNAPSHOT    |
| spring-cloud-vault        | 1.1.1.RELEASE  | 2.0.1.RELEASE | 2.0.2.BUILD-SNAPSHOT    |
| spring-cloud-gateway      | 1.0.2.RELEASE  | 2.0.1.RELEASE | 2.0.2.BUILD-SNAPSHOT    |
| spring-cloud-openfeign    |                | 2.0.1.RELEASE | 2.0.2.BUILD-SNAPSHOT    |
| spring-cloud-function     | 1.0.0.RELEASE  | 1.0.0.RELEASE | 1.0.1.BUILD-SNAPSHOT    |

주요한 컴포넌트들만 간단히 살펴보면,

- **Spring Cloud Config**

  Centralized external configuration management backed by a git repository. The configuration resources map directly to Spring `Environment` but could be used by non-Spring applications if desired.

- **Spring Cloud Netflix**

  Integration with various Netflix OSS components (Eureka, Hystrix, Zuul, Archaius, etc.).

- **Spring Cloud Stream**

  A lightweight event-driven microservices framework to quickly build applications that can connect to external systems. Simple declarative model to send and receive messages using Apache Kafka or RabbitMQ between Spring Boot apps.

- **Spring Cloud for Amazon Web Services**

  Easy integration with hosted Amazon Web Services. It offers a convenient way to interact with AWS provided services using well-known Spring idioms and APIs, such as the messaging or caching API. Developers can build their application around the hosted services without having to care about infrastructure or maintenance.

- **Spring Cloud Gateway**

  Spring Cloud Gateway is an intelligent and programmable router based on Project Reactor.

- **Spring Cloud Stream**

  A lightweight event-driven microservices framework to quickly build applications that can connect to external systems. Simple declarative model to send and receive messages using Apache Kafka or RabbitMQ between Spring Boot apps.

  

스프링 클라우드 기반의 프로젝트를 생성하기 위해서는 기본적으로 아래의 라이브러리를 추가하면 된다.(Maven 기준)

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.0.1.RELEASE</version>
</parent>
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-dependencies</artifactId>
            <version>Finchley.SR1</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
<dependencies>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-config</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
    </dependency>
</dependencies>
```



### 3. Spring Cloud DataFlow

Connect Anything - 어떤 것이든 연결한다.

> Connect the Enterprise to the Internet of Anything-mobile devices, sensors, wearables, automobiles, and more. Spring Cloud Data Flow provides a unified service for creating composable data microservices that address streaming and ETL-based data processing patterns.

Spring Cloud Data Flow를 통해 모바일 장치, 웨어러블, 자동차등 어떤 디바이스든지 엔터프라이즈 환경과 연결할 수 있다.
Spring Cloud Data Flow는 스트리밍 및 ETL(Extract, Translate, Load)기반의 데이타 프로세싱 패턴을 어드레스하는 마이크로서비스들의 구성가능한 데이타를 생성하기 위한 통합된 서비스를 제공한다.

요약하자면, 마이크로 서비스간의 데이타 연결, 흐름을 통일된 서비스의 형태로 제공하는 기술이라고 정의 할 수 있다.

전통적으로, 엔터프라이즈 시장에서의 시스템간의 데이타의 연결은 EAI, ESB등의 고비용 솔루션을 기반으로 한 접근방법이 유일하였는데 도입 후 지속적인 관리와 고도화을 위한 기술축적을 하지 못하고 솔루션에 의지 할 수 밖에 없다는 큰 취약점을 가지고 있었다. Spring Cloud DataFlow는 그런 전통적인 EAI, ESB 솔루션을 대체할 수 있는 충분한 스펙을 담고 있다. Spring Framework가 결국 Java의 EJB를 대체할 수 있었듯이...

현재는, 또 앞으로 계속 서비스들-또는 서비스들의 집합체인 시스템들-은 마이크로화 되고, 더 잘게 쪼개진 도메인으로 분화 될 수 밖에 없는 환경에서 그런 수많은 서비스들간의 연계, 연결, 관리가 더 효율적이고 집약적인 방식으로 제공되어야 할 필요성이 생겼고  Spring Cloud DataFlow는 그런 요구를 충족시켜주기 위해서 나온 기술들이라 할 수 있겠다.

> Spring Cloud Data Flow makes it easy to build and orchestrate cloud-native data pipelines for use cases such as data ingest, real-time analytics, and data import/export. Spring Cloud Data Flow makes it simple to connect systems by providing out of the box connectors for the most common integration scenarios.

Spring Cloud Data Flow는  데이타 수집, 실시간 분석, 데이타 임포트/익스포트와 같은 유즈케이스들을 처리하기 위해 클라우드기반의 데이타 파이프라인을 쉽게 빌드할 수 있게 해 주고, 그런 파이프라인들을 조정,통제(오케스트레이션) 할 수 있다. 물론, 메세지 브로커와 연계한 비동기 방식의 데이타 처리도 지원해 준다.

Spring Cloud DataFlow의 주요 기능이다.

- Supports processing data in real-time streams and batch
- Ingest, transform, analyze & store data
- Connectors for FTP, RDBMS, Cassandra, RabbitMQ, GemFire, Redis, and much more
- Supports modern messaging middleware - Kafka and RabbitMQ
- Spring Flo visual designer for pipelines
- Operational dashboard - metrics, health checks, and remote management
- Supported platforms: Cloud Foundry, Kubernetes, Apache YARN, Apache Mesos

개인적으로 가장 관심있는 분야중 하나이며, 백앤드 분야에서 필수적인 기술요소들이 가득 들어있는 영역이라 하겠다. 특히 메세징기반의 미들웨어를 연결하고 비동기 방식으로 데이타를 주고받을 수 있는 라이브러리들은 직접 업무시스템에 적용할 예정이다.

이 영역에 포함된 라이브러리 중 백앤드 데이타 처리에  많이 사용되고 있는 Spring-Batch 이다.



지금까지  Spring진영의  세 가지 큰 기술축인 Spring Boot, Spring Cloud, Spring Cloud DataFlow에 대해서 개략적이고, 개념중심으로 알아 보았는데, 앞으로 각 영역에 대해서 세부적인 내용과 코드중심으로 살펴볼 예정이다.

------

### 참고자료

- [spring.io](https://spring.io/)
- [Reactive Streams Specification](http://www.reactive-streams.org/)
- [ WebFlux Reference Documentation](https://docs.spring.io/spring/docs/current/spring-framework-reference/web-reactive.html#spring-webflux)
- [ Spring Boot Reference Manual](https://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/)
- [ Spring Cloud Reference Manual](https://cloud.spring.io/spring-cloud-static/current/)
  - Getting Started Guides 
    - [ Config](https://spring.io/guides/gs/centralized-configuration/)
    - [ Registry](https://spring.io/guides/gs/service-registration-and-discovery/)
    - [ Breakers](https://spring.io/guides/gs/circuit-breaker/)
    - [ Load Balancing](https://spring.io/guides/gs/client-side-load-balancing/)
    - [ Routing](https://spring.io/guides/gs/routing-and-filtering/)
- [ Getting Started Guide](https://spring.io/guides/gs/spring-boot/)
- [ Spring Cloud Data Flow Reference Manual](https://docs.spring.io/spring-cloud-dataflow/docs/current/reference/htmlsingle/#getting-started)