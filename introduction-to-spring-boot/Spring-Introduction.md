# Spring Framework
- Spring is one of the most widely used java EE open-source framework for building enterprise java application.
- Aims to simplify the complex enterprise java application development. 
- The Spring Framework is a collection of sub-frameworks including Spring Core, Spring Web, Spring MVC, Spring ORM, Spring AOP, Spring Security, Spring Data, Spring Batch, Spring Boot, Spring Cloud, Spring Integration, and Spring AMQP, each addressing different aspects of enterprise application development. These modules can be used independently or together to build robust applications.
- One of the major features of the spring framework is the dependency injection. It helps make things simpler by allowing us to develop loosely coupled application.

# Spring boot
- While the spring framework focuses on providing flexibility to you, spring boot aims to shorten the code length and provide you with the easiest way to develop a web application. With annotation configuration and default codes, spring boot shortens the time involve in developing an application.
- It helps create a stand-alone application with less or almost zero-configuration.
- Autoconfiguration is a special feature in spring boot. It automatically configures a class based on that requirement.

# Benefits of Spring Boot over Spring

1. **Dependency Resolution**:
  - **Explanation**: Spring Boot simplifies dependency management by providing a curated set of dependencies for commonly used libraries through "starters". This reduces the need to manually specify compatible versions.
  - **Example**:
    ```xml
    <!-- In a Spring Boot application, adding this starter dependency pulls in all necessary dependencies for a web application -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    ```

2. **Minimum Configuration**:
  - **Explanation**: Spring Boot uses convention over configuration, providing sensible defaults that reduce the need for explicit configuration.
  - **Example**:
    ```java
    // In Spring Boot, you can start a web application with minimal configuration
    @SpringBootApplication
    public class Application {
        public static void main(String[] args) {
            SpringApplication.run(Application.class, args);
        }
    }
    ```

3. **Embedded Server for Testing**:
  - **Explanation**: Spring Boot includes an embedded web server (like Tomcat, Jetty, or Undertow), which allows you to run web applications and tests without needing an external server.
  - **Example**:
    ```java
    // The application can be tested with an embedded server, making integration tests simpler
    @SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
    public class MyWebIntegrationTest {
        @Autowired
        private TestRestTemplate restTemplate;

        @Test
        public void exampleTest() {
            String body = this.restTemplate.getForObject("/", String.class);
            assertThat(body).contains("Hello, World");
        }
    }
    ```

4. **Bean Auto Scan**:
  - **Explanation**: Spring Boot automatically scans for beans and components in the application's base package, reducing the need for explicit configuration.
  - **Example**:
    ```java
    // In Spring Boot, this annotation triggers scanning of components and beans in the specified package
    @SpringBootApplication
    public class Application {
        public static void main(String[] args) {
            SpringApplication.run(Application.class, args);
        }
    }

    @Service
    public class MyService {
        // Automatically discovered and registered as a bean
    }
    ```

5. **Health Metrics**:
  - **Explanation**: Spring Boot provides built-in health checks and metrics for monitoring the state of the application out-of-the-box through the Actuator module.
  - **Example**:
    ```java
    // Adding the Actuator dependency enables health checks and metrics
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>

    // Accessing health metrics
    // http://localhost:8080/actuator/health
    // http://localhost:8080/actuator/metrics
    ```

# Core Features of Spring

1. **Inversion of Control (IoC) Container**:
  - Manages the lifecycle and configuration of application objects using Dependency Injection (DI).
  - Example:
    ```java
    @Component
    public class MyComponent {
        // Spring will automatically inject dependencies
    }
    ```

2. **Aspect-Oriented Programming (AOP)**:
  - Separates cross-cutting concerns like logging, security, and transaction management from the business logic.
  - Example:
    ```java
    @Aspect
    public class LoggingAspect {
        @Before("execution(* com.example.MyService.*(..))")
        public void logBefore(JoinPoint joinPoint) {
            System.out.println("Executing: " + joinPoint.getSignature().getName());
        }
    }
    ```

3. **Data Access**:
  - Simplifies data access using JDBC, ORM tools (like Hibernate), and transaction management.
  - Example:
    ```java
    @Repository
    public class MyRepository {
        @Autowired
        private JdbcTemplate jdbcTemplate;
        // Methods to interact with the database
    }
    ```

4. **Transaction Management**:
  - Provides a consistent programming model for transaction management, whether using local or global transactions.
  - Example:
    ```java
    @Service
    public class MyService {
        @Transactional
        public void performTransaction() {
            // Transactional code
        }
    }
    ```

5. **Spring MVC**:
  - A full-featured web framework for building web applications using the Model-View-Controller design pattern.
  - Example:
    ```java
    @Controller
    public class MyController {
        @GetMapping("/hello")
        public String sayHello(Model model) {
            model.addAttribute("message", "Hello, World");
            return "hello";
        }
    }
    ```

6. **Integration**:
  - Provides integration with other frameworks and libraries, such as JMS, AMQP, and other enterprise integration patterns.
  - Example:
    ```java
    @JmsListener(destination = "myQueue")
    public void receiveMessage(String message) {
        System.out.println("Received <" + message + ">");
    }
    ```

# Core Features of Spring Boot

1. **Auto-Configuration**:
  - Automatically configures Spring and third-party libraries whenever possible, based on the dependencies present in the classpath.
  - Example:
    ```java
    @SpringBootApplication
    public class Application {
        public static void main(String[] args) {
            SpringApplication.run(Application.class, args);
        }
    }
    ```

2. **Spring Boot Starters**:
  - A set of convenient dependency descriptors to simplify the inclusion of common libraries.
  - Example:
    ```xml
    <!-- Adding Spring Boot Web starter for web application development -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    ```

3. **Embedded Servers**:
  - Includes embedded servers (Tomcat, Jetty, Undertow) to run web applications without needing an external server.
  - Example:
    ```java
    // The application can be started and tested with an embedded server
    @SpringBootApplication
    public class Application {
        public static void main(String[] args) {
            SpringApplication.run(Application.class, args);
        }
    }
    ```

4. **Spring Boot CLI**:
  - Allows you to run and test Spring Boot applications from the command line without needing an IDE.
  - Example:
    ```bash
    spring run myapp.groovy
    ```

5. **Actuator**:
  - Provides production-ready features such as monitoring, metrics, and health checks.
  - Example:
    ```xml
    <!-- Adding Actuator dependency -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
    ```

6. **DevTools**:
  - Includes tools to improve the development experience, such as automatic restart and live reload.
  - Example:
    ```xml
    <!-- Adding DevTools dependency for enhanced development experience -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <scope>runtime</scope>
        <optional>true</optional>
    </dependency>
    ```

## Summary

**Spring Core Features**:
- Inversion of Control (IoC) Container
- Aspect-Oriented Programming (AOP)
- Data Access
- Transaction Management
- Spring MVC
- Integration

**Spring Boot Core Features**:
- Auto-Configuration
- Spring Boot Starters
- Embedded Servers
- Spring Boot CLI
- Actuator
- DevTools

# How Spring Boot work internally?
- Spring does not generate code like a magic or it does not use any XML configuration it use all programmatic configuration which is done by spring boot developers.
- Spring boot developer provide us the jar file and we are just using it
- Where these jar file available?
  - starter POM: while creating spring boot application, we import starter like spring-starter-web, spring-starter-jpa etc it import all jar file required for our application.
  - once starter are added, in META-INF/spring.factories spring developers mention which should be enabled at run time and which should not be.
- | Condition                      | Description                                         |
  |--------------------------------|-----------------------------------------------------|
  | OnBeanCondition                | Checks if a bean is in the Spring factory           |
  | OnClassCondition               | Checks if a class is on the classpath               |
  | OnExpressionCondition          | Evaluates a SpEL expression                         |
  | OnJavaCondition                | Checks the version of Java                          |
  | OnJndiCondition                | Checks if a JNDI branch exists                      |
  | OnPropertyCondition            | Checks if a property exists                         |
  | OnResourceCondition            | Checks if a resource exists                         |
  | OnWebApplicationCondition      | Checks if a WebApplicationContext exists            |


# Spring bean
- An object that is managed by spring Framework in a java application
- Aims to simplify the complex enterprise java application development
- Spring beans can be configured using XML, Java annotations or Java Code.

# Life cycle of spring bean
- The lifecycle of an object means when and how it is born, how it behaves throughout its life and when & how it dies.
- Bean life cycle is managed by the spring container.

# @Configuration
- @Configuration declares class as "full" configuration class
  - Class must be non-final and public
# @Bean
- @Bean declares bean configuration inside configuration class
- Method must be "non-final" and "non-private" (i.e public, protected or package-private)

# Spring Component
- Spring Component contains class-level annotation that marks class a Spring Component(@Component)
- Constructor-dependency injection is automatically done using @Autowired by injecting the constructor parameters(s)
- @Autowired on constructor is optional if there is only one constructor

## Spring sub type
- Spring provide component stereotype to classify classes as Spring Components
- Sub-type are available as refinement for statnd components
- @Component as a general annotation indicating thath the class should be initialized, configured and managaed by the core container.
- @Repository, @Service, @Controller as meta-annotations for @Component that allows to further re-fine components
- Own stereotype annotations can(and should) be defined to support general architecture principle.

# Bean injection or dependency Injection
- constructor injection
- field injection
- configuration methods
- setter method injection

# @Qualifier
- primary
- seconday

# @Primary
 - choosing primiary bean from multiple beans in a class
