### Spring Boot + API Gateway

서로 다른 네트워크 인터페이스를 받아주는 SW 서버

왜 필요하가? 이전까지는 Only 1 Device.
지금은 Too many devices 심지어 제조사, 플랫폼 모두 다 다름.

- 디바이스별로 요청결과를 다르게 돌려주고
- 디바이스 별로 메시지 프로토콜을 다르게 해서

> 최대한 네트워크 성능향상관련 방법이 필요.

(3rd, Web, Mobile, Cloud, B2B Interfaces) <-> API Gateway <-> Applicaiton Server

![](https://docs.oracle.com/cd/E50612_01/doc.11122/concepts_guide/content/images/concepts/api_server_core_app_oracle.png)

![](http://www.codeproject.com/KB/architecture/simplegateway/Gateway.jpg)

#### Requirements

- 빠른 응답속도
- 유지보수
- at least support 2 protocols
- monitoring, Mgmt
- API version Mgmt.
- Pipelining.

### How?

- Kryo: serialization lib (e.g protobuf, message pack)

https://github.com/EsotericSoftware/kryo

높은 성능 자바 직렬화 라이브러리
Scala, Obj-C, Clojure 지원

- undertow: (NIO based)

> Undertow is a flexible performant web server written in java, providing both blocking and non-blocking API’s based on NIO.

- Spring actuator

관리포인트, 감시의 추상화를 몇줄로 바로.

- Netty

e.g Mina, vert.x


Netty 로 HTTP + TCP 바다고, SpringBoot 로 빈 관리
Undertow 로 JSON return

[Convertion over config, COC](http://en.wikipedia.org/wiki/Convention_over_configuration)

#### Kryo

#### Actuator

- thread dump using web interface
- metrics (e.g memory 이전에는 JMS 클라이언트
- beans, config variables


#### Summary

Boot + Actuator -> 빠르게 개발.
그러나 단점도 있음.

- 빠른 개발을 위한 auto-config 가 확장성 문제로
- 웹 말고, 앱에 대해서 Spring boot 는 괜찮음.
- 간단한 구조는 Google protobuf 가 더 나으나, POJO 가 아님.
- Kryo 는 복잡한 메세지에 대해서 더 빠르고, 다른 언어 직렬화 지원 및 POJO

### Spring Boot + Logging

- Boot: JCL
- SLF4J -> Bogback

#### JCL

JCL -> apache logging.Log, Logger

정석은 (`this.log.isDebugEnabled`) 일때만 로그 JCL 홈페이지에 나와있음.

[JCL](http://commons.apache.org/proper/commons-logging/) 은 로깅 추상화 라이브러리

자바 내부에 있는 것은 JUL

Jac

LOG4J 는 JCL 을 구현.

- JCL 은 클래스 패스에서 LOG4J 구현체 찾아보고
- 없으면 1.4 구동중인지 확인하고
- 아무것도 못찾으면 기본 구현체 사용

JCL 을 꺼리는 이유는

- 자바 클래스로더 기본 동작방식, 서블릿 컨테이너의 클래스 로더 동작방식 등이 맞물려서.

암튼 문제가 있음. 아래 아티클을 참조

#### Class Loader

[Important: Taxonomy of class laoder](http://articles.qos.ch/classloader.html)

[Important2: class loading](http://articles.qos.ch/thinkAgain.html)

[Logging dep in Spring](http://spring.io/blog/2009/12/04/logging-dependencies-in-spring/)


http://www.javaworld.com/article/2077260/learn-java/learn-java-the-basics-of-java-class-loaders.html

http://stackoverflow.com/questions/13269556/strange-behavior-of-class-getresource-and-classloader-getresource-in-executa

http://stackoverflow.com/questions/5650334/java-classloaders-why-search-the-parent-classloader-first

### SLF4J

![](http://image.slidesharecdn.com/slf4jsimpleloggingfacadeforjava-091124024151-phpapp01/95/slf4j-simple-logging-facade-for-java-4-1024.jpg?cb=1259052860)

로깅 라이브러리를 런타임이 아닌 **컴파일 타임** 에 정한다

세가지 모듈을 제공

- Bridging: JCL 엔 없던 것. 레거시를 위함

레거시들은 SLF4J 를 안썼음. 이전엔 직접 로거를 쓰거나, JCL 을 쓰거나
그런 호출을 SLF4J 쪽으로 다시 연결해 주는 것.

JCL 을 호출한 코드를 SLF4J 로 호출하는 쪽으로
-> JCL 용 브릿지를 쓰면 됌 `log4j-over-slf4j.jar`

`slf4j-log4j.jar` 랑 같이쓰면 안됌

즉 브릿지랑 바인더를 같은 종류를 쓰면 안됌. 사이클

따라서 logback 을 호출하고 싶으면, logback 을 제외한
모든 브릿지를 추가하고, 바인더는 logback 만 추가.
그러면 모든 로그 호출은 logback 으로

- API: If 를 감싸지 않아도. 부하가 없는 이유는 Placeholder
- Binding: 구현체로 연결. 어댑터 역할이며,

프레임워크 개발자는 Binding 을 쓰면 안됌. 의존성을 넣더라도 Optional 로추가할것. API만 써야

구현체는 slf4f-log4j-{version}.jar

여러 바인딩을 클래스패스에 두면 warning 이 나옴. 얻어걸린 무언가를 씀
규칙이 있지 않음.

#### Spring Boot Logging

위와 같은 세팅을 Spring Boot Logging 이 해줌

-[SpringBoot How To Logging](http://docs.spring.io/spring-boot/docs/current/reference/html/howto-logging.html)

- [SpringBoot Features: Logging](http://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-logging.html)

- [Netgloo SpringBoot Logging](http://blog.netgloo.com/2014/12/11/logging-in-spring-boot/)

### Reactive Programming

ICFP

Push-poll Functional Reactive Programming
Dynamic Optimization

RxJava, RxScala 의 기본
Rx 의 내부를 까 볼 것. 논문들을 찾아볼 것.

#### Event Stream

a uniform interface for composable events

요즘의 추세는 No DI, No IoC

#### Reactors

Observers without IoC

IoC 를 없애기 위해 중앙 개념을 도입.

[Playing with Reactor](http://tech.kinja.com/playing-with-reactor-626741403)

[SO: Akka or Reactor](http://stackoverflow.com/questions/16595393/akka-or-reactor)

[Github: Reactor](https://github.com/reactor/reactor)

단점은 절차적인 코드가 됌.
이런건 하드웨어 쪽에서 씀. Description Language

나중에 많아지면, 이벤트 구조가 힘듬

self =>


CEP 프레임워크 Esper SQL 로 처리리

CEP 는 Complex Event Processing

[CEP with Akka and Esper or Streams](http://typesafe.com/activator/template/akka-with-esper)

#### Signals

Time-varying values

처음에는 Obserber -> Stream -> 중앙관리 Reactor

그 다음이 Signal

요즘에는 Reactive 프레임워크에 다 들어있음

```scala
val sum = Signal { a() + b() }

observe(sum) { x => println(x) }

val b0 = b.now
val sum1 = Signal { a() + b0 }
val sum2 = Signal { a() + b.now }
```

엑셀에서 셀 바뀌면 자동으로 업데이트 되는 것이 그 예제
스냅샷을 이용해서 시간별로 데이터가 있고

실제로는 어떻게 쓰느냐

#### Imperative data flow

최대의 단점은 mutable data

#### Reactive combinators as imperative data-flow

Signal 이 움직이느냐, Reactor 가 받느냐
Observer 가 마음대로 하느냐

내가 Rx 같은걸 구현하려면, 다시 처음으로 돌아가서 Functional 으로
Partial Function, 즉 구현체를 넘겨주면 해결이 되지 않느냐


[Spark 를 돌려 볼 것!!](https://spark.apache.org/)

#### Router

처리자에 대한 관리가 필요함 Akka 에서는 Remote 등을 지원
다중 사용자에 대한 분산처리하거나,

Imperative event coordination

[마틴 오더스키 논문 찾아볼 것]

옵저버 패턴부터, 옵저버 난립해서
콜백 헬, 그런걸 해결하기 위해

중앙 처리하기 시작하기
그러니까 뮤터블이 생기고,

나중엔 Functional 로 돌아오고

#### Reactive Manifesto

http://www.reactivemanifesto.org/
https://typesafe.com/blog/why_do_we_need_a_reactive_manifesto%3F
https://typesafe.com/blog/reactive-manifesto-20

### Reactive using Rx

gmind7.github.io

김대성

Netty 소켓 개발은 트랜잭션을 보장하지 않음

1) Rx 는 Req, Res 두개의 스레드를 하나의 것처럼 해결 (이벤트))

2) 비동기를 쉽게해결

[Netty] 를 써봐야 겠다.

[Akka] 함수, [RxScala] 함수 테스트코드 짜 볼 것


Debounce

control flow vs data flow

엑셀은 data-flow progrmaming


#### Observable

데이터를 PUSH 하는 역할

Observer 는 그 데이터를 소비

Subscriber

1. 데이터 생성 Observable
2. 구독 계획 subscriber
3. 구독 subscribe

influx time series database

- Create, Combine, Listen

즉 데이터를 어떻게 생성하고, 처리하고, 반응할지를 나타냄.

#### Summary

OOP CACHE RDB -> HADOOP NOSQL FP, RX, FRP
JPA?
