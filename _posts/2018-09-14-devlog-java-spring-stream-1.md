---
layout: post
title:  "[Java/Spring] Spring Cloud Stream의 이해 - 1"
subtitle:   ""
categories: devlog
tags: java spring springboot spring-cloud-stream messagebroker
comments: true
---

## 비동기기술,   MQ ( 메세지큐잉 ), Spring Cloud Stream



### **비동기 방식**

- 좋은 블로그: http://homoefficio.github.io/2017/02/19/Blocking-NonBlocking-Synchronous-Asynchronous/index.html



### **Message Queuing**

시스템간 결합을 최대한 느슨하게 유지한 채로 상호 정보 - 데이타, 신호 - 를 주고 받을 수 있는 방식.  
이 기술을 지원하는 라이브러리, 솔루션들을 'Message Broker'로 부름.

대표적인 MQ 라이브러리 

- RabbitMq, Apache Kafka, Amazon SQS, SNS, AmazonMq(ActiveMq)



### **MQ 기본개념**

* 프로토콜 
  - AMQP, STOMP, MTQQ, TCP/IP
* Connection : 발생자와 소비자, Broker 사이의 물리적인 연결
* Channel - 외부에서 메세지 브로커를 통해 메세지를 주고받을 수 있는 채널, 논리적인 연결고리 (발행시스템과 구독시스템은  채널을 통해 Queue에 접근 )
* Exchange - 메세지의 라우팅 규칙(교환자), 실제 메세지를 담는 Queue와 바인딩 됨.
* Queue - 메세지의 최종 목적지 



### 대표적인 메세지브로커 (external message broker)

- Rabbit MQ
  - 가장 범용적이고, 널리 사용되는 오픈소스 메세지 브로커 (35,000개 이상)
  - 강력한 메세지 라우팅 기능, Queue의 다양한 옵션 설정
  - Supports [multiple messaging protocols](https://www.rabbitmq.com/protocols.html), [message queuing](https://www.rabbitmq.com/tutorials/tutorial-two-python.html), [delivery acknowledgement](https://www.rabbitmq.com/reliability.html), [flexible routing to queues](https://www.rabbitmq.com/tutorials/tutorial-four-python.html), [multiple exchange type](https://www.rabbitmq.com/tutorials/amqp-concepts.html).(direct, topic, )
- Amazon SQS / SNS 
  - 메세지 브로커를 설정할 필요없는 단순 대기열(queue)과 주제(topic) 서비스
  - 단순히 Queue용도로만 사용할 경우 적절한 대안이 될 수 있음. 메세지 라우팅 기능, 채널 그룹핑기능 없음.
  - 관련문서: [https://www.baeldung.com/aws-queues-java](https://www.baeldung.com/aws-queues-java)
- Amazon MQ (Apache MQ)
  - Apache ActiveMQ 기반의 클라우드 기반 메세지 브로커
  - 표준 프로토콜 모두 지원 ( 향후 ApacheMQ뿐만이 아니라 다른 Third-Party 추가될 가능성 )
  - 브로커의 생성, 이중화(Active-Standby), 모니터링(CloudWatch)를 AWS기반에서 간단하게 구성할 수 있음 (매우 매력적인 장점)
  - 레퍼런스 문서: [https://docs.aws.amazon.com/ko_kr/amazon-mq/latest/developer-guide/welcome.html](https://docs.aws.amazon.com/ko_kr/amazon-mq/latest/developer-guide/welcome.html)
- Apache Kafka 
  - 범용 메세지 브로커중에서는 가장 뛰어난 성능
  - 통신프로토콜이 TCP/IP방식임
  - 메세지 전송보장



> RabbitMQ. Kafka 와 AmazonMq와의 가장 큰 차이점은 
>
> - RabbitMQ. Kafkas는 spring-cloud-stream에서 제공하는 단순화돤 공통 어노테이션을 통해 구현.
> - AmazonMq는 spring-cloud-stream 기반의 바인딩 및 Pub/Sub 구현이 안됨. JMS 방식으로 바인딩 및 메세지교환처리 구현. 즉, 사용하는 어노테이션이 틀림. (추가될 가능성은 있음)
> - 예제를 통해 확인이 가능




### Spring Cloud Stream

- 메세지가반 마이크로 서비스간 연결과 정보 교환 위한 프레임워크

- Spring Integration이 메세지브로커(RabbitMQ, Kafka)와의 중계를 담당

  - 연계에 필요한 추상화 인터페이스 제공

    - `@EnableBinding` 어노테이션 선언으로 메세지브로커에 연결됨.
    - `@StreamListener` 선언시 스트림처리를 위한 이벤트 수신
    - `Source`, `Input` 인터페이스를 통해 큐/토픽과 쉽게 연결



    ##### 주요 인터페이스 

    > - **Sink:** Identifies the contract for the message consumer by providing the destination from which the message is consumed.
    > - **Source:** Identifies the contract for the message producer by providing the destination to which the produced message is sent.
    > - **Processor:** Encapsulates both the sink and the source contracts by exposing two destinations that allow consumption and production of messages.

    ![spring cloud stream](https://zuminternet.github.io/images/portal/post/2017-7-11-spring_cloud_stream_rabbitmq_01/20170610_sourcesink.png)



- Springboot 기반으로 간편하고 직관적인 어노테이션으로 빠른 개발이 가능
- 개발자는 메세지브로커의 커넥션, 설정등에 신경쓰지 않고 비즈니스 로직에 집중할 수 있음



![Spring Cloud Stream overview](https://cloud.spring.io/spring-cloud-stream/img/SCSt-overview.png)



#### 왜 메세지 기반 (Messaga-Driven) 기술이 필요한가?

- 느슨한 결합이 가능하므로 분산시스템, 마이크로서비스간 협업 관계에 있어 상호 의존성을 배제 할 수 있다.
- 상대시스템의 성능, 서버 상태에 전혀 영향을 받지 않는다.
- 서로 시스템 정보를 몰라도 메세지 브로커 시스템간 메세지 교환-상호간 정보 교환-이 가능하다.
- API 방식의 경우, 목적지 시스템의 성능과 서버의 상태에 직접적인 영향을 받기 때문에 예외처리, FallBack처리가 필수
- 상대 시스템은 서로 독립적으로 인스턴스를 증가 감소할 수 있다.
- 상호 정보 교환을 하는 시스템들은 서로가 어디에 위치하는지 (Endpoint가 어디인지), 어떤 기술기반인지 관심을 가질 필요가 없다. 알지 못한다. 오로지 메세지 전송(Pub) 과 수신(Sub)에만 관심을 가지면 된다.