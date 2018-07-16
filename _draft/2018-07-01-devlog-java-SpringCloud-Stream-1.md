### 비동기기술 Spring Cloud Stream, MQ ( 메세지큐잉 )


**Message Queuing**

시스템간 결합을 최대한 느슨하게 유지한채로 상호 정보 - 데이타, 신호 - 를 주고 받을 수 있는 방식.  
이 기술을 지원하는 라이브러리, 솔루션들을 'Message Broker'로 부름.

대표적인 MQ 라이브러리 - RabbitMq

**MQ 기본개념**

* AMQP(Advanced Message Queuing Protocol) : MQ 표준 프로토콜. 시스템 간 메시지를 교환하기 위해 공개 표준으로 정의한 프로토콜
* Broker : 발행자가 만든 메시지를 구독자가 수신할 수 있도록 저장
* Virtual host : Broker 내의 가상 영역
* Connection : 발생자와 소비자, Broker 사이의 물리적인 연결
* Channel : 발행자와 소비자, Broker 사이의 논리적인 연결, 하나의 Connection 내에 다수의 Channel 설정 가능
* Exchange : 발행한 모든 메시지가 처음 도달하는 지점으로 메시지가 목적지에 도달할 수 있도록 라우팅 규칙 적용, 라우팅 규칙에는 direct, topic, fanout
* Queue : 메시지가 소비되기 전 대기하고 있는 최종 지점으로 Exchange 라우팅 규칙에 의해 단일 메시지가 복사되거나 다수의 큐에 도달할 수 있다
* Binding : Exchange 와 Queue 간의 가상 연결
* 

**참고서적**.  
RabbitMQ 따라잡기-에이콘출판사-


### Spring Cloud Stream

- 메세지가반 마이크로 서비스를 구현하기 위한 프레임워크
- SpringBoot 기반
- Spring Integration이 메세지브로커(Rabbit-MQ)와의 중계를 담당
- `@EnableBinding` 어노테이션 선언으로 메세지브로커에 연결됨.
- `@StreamListener` 선언시 스트림처리를 위한 이벤트 수신
