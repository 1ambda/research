
### @SpringBootApplication

- @ComponentScan
- @Configuration
- @EnableAutoConfiguraiton

[@SpringBootApplication](http://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/#getting-started-first-application-auto-configuration)

### @EnableAutoConfiguration

The second class-level annotation is @EnableAutoConfiguration. This annotation tells Spring Boot to “guess” how you will want to configure Spring, based on the jar dependencies that you have added. Since spring-boot-starter-web added Tomcat and Spring MVC, the auto-configuration will assume that you are developing a web application and setup Spring accordingly.

Spring Boot auto-configuration attempts to automatically configure your Spring application based on the jar dependencies that you have added. For example, If HSQLDB is on your classpath, and you have not manually configured any database connection beans, then we will auto-configure an in-memory database.


### @Configuration

[Link](http://stackoverflow.com/questions/24014919/understanding-spring-configuration-class-usage)

Migrating XML to `@Configuration`

```java

@Configuration
public class MyApplicationContext {

  @Bean(name = "someBean")
  public SomeClass getSomeClass() {
    return new SomeClassImpl(someInterestingProperty); // We still need to inject someInterestingProperty
  }

  @Bean(name = "anotherBean")
  pubic AnotherClass getAnotherClass() {
    return new AnotherClassImpl(getSomeClass(), beanFromSomewhereElse); // We still need to inject beanFromSomewhereElse
  }
}

@ImportResource("another-application-context.xml")
@Configuration
public class MyApplicationContext {
  ...  
}

@Import(OtherConfiguration.class)
@Configuration
public class MyApplicationContext {
  ...
}
```

```xml
<beans ...>
    <context:component-scan base-package="my.base.package"/>
    ... other configuration ...
</beans>
```

```java
@Configuration
@ComponentScan(basePackages = "my.base.package")
public class RootConfig {
    ... other configuration ...
}
```

### @Component vs @Bean

[@Component](http://docs.spring.io/spring/docs/3.1.x/javadoc-api/org/springframework/stereotype/Component.html)
[@Bean](http://docs.spring.io/spring/docs/3.1.x/javadoc-api/org/springframework/context/annotation/Bean.html)
[SO: Difference between @Bean and @Component](http://stackoverflow.com/questions/10604298/spring-component-versus-bean)
[Component@ vs @Bean](http://zezutom.blogspot.kr/2014/02/spring-series-part-5-component-vs-bean.html)
[@Component vs @Bean]()

- `@Component` indicates that an annotated **class** is a "component". Such classes are considered as candidates for auto-detection when using annotation-based configuration and classpath scanning

- `@Bean` indicates that a **method** produces a bean to be managed by the Spring Container. The names and semantics of the attributes to this annotation are intentionally similar to those of the <bean/> element in the Spring XML schema.

and

- `@Component`

### @ComponentScan

```xml
<context:component-scan/>
```

### Gradle Plugin

```gradle

buildscript {
    repositories {
	    mavenCentral()
    }
    dependencies {
        classpath 'org.springframework.boot:spring-boot-gradle-plugin:1.2.2.RELEASE'
    }
}

apply plugin: org.springframework.boot.gradle.SpringBootPlugin

```

use `gradle bootRun`. This task is added whenever you import the srping boot plugin.


### Hot-Swap

[SpringLoaded](https://github.com/spring-projects/spring-loaded)
[Gradle Setting](http://docs.spring.io/spring-boot/docs/current/reference/html/howto-hotswapping.html)


### Jar Manifest Issue

[SO: BootRepackage](http://stackoverflow.com/questions/24695701/no-main-manifest-attribute-when-trying-to-execute-fat-jar)
