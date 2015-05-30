
[IO, Boot](https://blog.codecentric.de/en/2013/09/spring-one-wrap-up-spring-boot-spring-io/)
[Batch, Hadoop, YARN, XS](https://blog.codecentric.de/en/2013/09/spring-one-wrap-up-spring-batch-spring-hadoop-and-spring-xd/)

![](http://spring.io/img/platform-stack.png)

### Spring IO

The Spring IO platform is splitted into two groups: IO Foundation and IO Execution.

**IO Foundation** contains all the different Spring projects, and **IO Execution** projects are *Spring Boot* and *Spring XD* which are using those foundational libraries, combining them.

### Spring Boot

Spring Boot offers a fast way to build applications. It looks at your classpath and at beans you have configured, makes reasonable assumptions about what you're missing, and adds it. With Spring Boot you can focus more on business features and less on infrastructures.

Note: Spring Boot doesn’t generate code or make edits to your files. Instead, when you start up your application, Spring Boot dynamically wires up beans and settings and applies them to your application context.

### Spring Batch

[See JSR-352, Batch Applications for the Java Platform](https://jcp.org/en/jsr/detail?id=352)

> If you haven’t heard of it by now: there’s the JSR-352 standardizing batch application development in Java SE and EE. Spring Batch was deeply involved in bringing the JSR forward, so it’s not a surprise to hear that Spring Batch 3.0 will be fully compliant with the spec. And yes, even the read-process-write cycles that differ between the current implementation of Spring Batch and the spec will be optionally adapted. You’ll have the choice in the future to either do read-process-read-process-bulkwrite (JSR-352 style) or read-read-process-process-bulkwrite (classic Spring Batch style).

Spring Batch is a lightweight, comprehensive batch framework designed to enable the development of robust batch applications vital for the daily operations of enterprise systems.

- Transaction Mgmt
- Chunk based processing
- Declarative I/O
- Start / Stop / Restart
- Retry / Skip
- Web based admin interface

### Spring Integration

[Important: Spring Integration Overview](http://docs.spring.io/spring-integration/reference/html/overview.html)  
[Enterprise Integration Patterns](http://www.eaipatterns.com/)

**Spring Integration** extends the spring programming model to support the well-known Enterprise Integration Patterns.

Spring Integration enables lightweight messaging system within Spring-based applications and support integration with external systems via declarative adapters.

Spring Integrations' primary goal is provide a simple model for building enterprise integration solutions while maintaining the separation of concerns that is essential for producing maintainable, testable code.

#### Background

One of the key themes of the Spring Framework is **inversion of control**. In its broadest sense, this means that the framework handle responsibilities on behalf of the components that are managed with in context. The components themselves are simplified since they are relieved of those responsibilities. For example, **dependency injection** relieves the components of the responsibility of locating or creating their dependencies. Likewise **AOP** relieves business components of generic cross-cutting concerns by modularizing them into reusable aspects. In each case, the end result is a system that is **easier to test, understand, maintain, and extend**.

Spring Integration is motivated by these same goals and principles. It extends the Spring programming model into the messaging domain and builds upon Spring's existing enterprise integration support to provide an even higher level of abstraction. It support message-driven architectures where inversion of control applies to runtime concerns, such as **when** certain business logic should execute and **where** the response should be sent.

It supports routing and transformation of messages so that different transports and different data formats can be integrated without impacting testability. In other words, the messaging and integration concerns are handled by the framework, so business components are further isolated from the infrastructure and developers are relieved of complex integration responsibilities.


### Spring XD

![](http://projects.spring.io/spring-xd/img/spring-xd-unified-platform-for-big-data.png)

Spring XD is a unified, distributed, and extensible system for data ingestion, real time analytics, batch processing, and data export.
