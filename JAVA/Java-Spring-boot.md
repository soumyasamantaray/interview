Here are some common Spring Boot interview questions and answers for candidates with 1+ years of experience.

### Spring Boot Core Concepts

1.  **What is Spring Boot and what are its main advantages?**
    *   **Answer:** Spring Boot is an opinionated framework that makes it easy to create stand-alone, production-grade Spring applications that you can "just run." Its main advantages include:
        *   **Auto-configuration:** Automatically configures your Spring application based on the JARs on its classpath.
        *   **Opinionated defaults:** Provides sensible default configurations, reducing the need for boilerplate setup.
        *   **Embedded servers:** Allows you to embed web servers like Tomcat, Jetty, or Undertow directly into your executable JAR, simplifying deployment.
        *   **Starter dependencies:** Provides a set of convenient `pom.xml` dependencies that you can include to get a specific functionality (e.g., `spring-boot-starter-web` for web applications).
        *   **No XML configuration:** Primarily relies on Java-based configuration and annotations.
        *   **Production-ready features:** Includes tools like Actuator for monitoring and managing applications in production.

2.  **Explain Spring Boot Auto-configuration. How does it work?**
    *   **Answer:** Spring Boot auto-configuration attempts to automatically configure your Spring application based on the JARs that you have added to your classpath. For example, if you have `spring-boot-starter-web` on your classpath, Spring Boot will automatically configure a Tomcat server and Spring MVC.
        It works by looking at the presence of specific classes or beans on the classpath. It then applies a set of default configurations. This process is driven by the `@EnableAutoConfiguration` annotation (which is part of `@SpringBootApplication`). Spring Boot provides many auto-configuration classes (e.g., `DataSourceAutoConfiguration`, `WebMvcAutoConfiguration`), each conditionally applied based on the environment.

3.  **What are Spring Boot Starters? Give an example.**
    *   **Answer:** Spring Boot Starters are a set of convenient dependency descriptors that you can include in your application. They simplify build configuration by providing a curated set of transitive dependencies that are commonly used together for a particular feature.
        **Example:** If you want to build a web application, you just need to add `spring-boot-starter-web` to your `pom.xml` (for Maven) or `build.gradle` (for Gradle). This starter will automatically bring in all necessary dependencies like Spring MVC, Tomcat, Jackson, etc., with compatible versions.

4.  **What is the purpose of the `@SpringBootApplication` annotation?**
    *   **Answer:** The `@SpringBootApplication` annotation is a convenience annotation that combines three commonly used Spring Boot annotations:
        *   `@Configuration`: Tags the class as a source of bean definitions for the application context.
        *   `@EnableAutoConfiguration`: Tells Spring Boot to start adding beans based on classpath settings, other beans, and various property settings.
        *   `@ComponentScan`: Tells Spring to look for other components, configurations, and services in the current package and its sub-packages, allowing them to be discovered and registered as beans.
        It's typically placed on your main application class.

### Dependency Injection and IoC

5.  **Explain Dependency Injection (DI) and Inversion of Control (IoC) in the context of Spring Boot.**
    *   **Answer:**
        *   **Inversion of Control (IoC):** IoC is a design principle where the control of object creation and lifecycle management is transferred from the application code to a container (the Spring IoC container). Instead of your code creating dependent objects, the container creates them and injects them.
        *   **Dependency Injection (DI):** DI is a specific implementation of IoC where the container "injects" dependencies into an object at runtime rather than the object creating or looking up its dependencies. This promotes loose coupling and makes components easier to test and manage. In Spring Boot, you primarily use `@Autowired` to let Spring inject beans into your classes.

6.  **How do you define and inject a bean in Spring Boot?**
    *   **Answer:**
        *   **Defining a bean:** You can define a bean using several stereotype annotations:
            *   `@Component`: A generic stereotype for any Spring-managed component.
            *   `@Service`: Denotes a class that performs business logic.
            *   `@Repository`: Denotes a class that interacts with a database (often used with Spring Data JPA).
            *   `@Controller` / `@RestController`: Denotes a class that handles web requests.
            Alternatively, for third-party classes or when you need more control, you can use the `@Bean` annotation within a `@Configuration` class.
            ```java
            // Example using @Service
            @Service
            public class MyBusinessService {
                // ...
            }

            // Example using @Bean
            @Configuration
            public class AppConfig {
                @Bean
                public MyThirdPartyService myThirdPartyService() {
                    return new MyThirdPartyService();
                }
            }
            ```
        *   **Injecting a bean:** You inject a bean primarily using the `@Autowired` annotation. Spring will find a matching bean in its application context and inject it.
            ```java
            @Service
            public class AnotherService {
                private final MyBusinessService myBusinessService; // Recommended: constructor injection

                @Autowired
                public AnotherService(MyBusinessService myBusinessService) {
                    this.myBusinessService = myBusinessService;
                }

                // ...
            }
            ```

### RESTful Web Services

7.  **How do you create a RESTful API endpoint in Spring Boot?**
    *   **Answer:** You use the `@RestController` annotation on a class to combine `@Controller` and `@ResponseBody`. This tells Spring that the return value of the methods should be bound directly to the web response body. Then, you use mapping annotations like `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`, or `@RequestMapping` to define the HTTP method and URL path.
        ```java
        @RestController
        @RequestMapping("/api/products")
        public class ProductController {

            @GetMapping("/{id}")
            public Product getProductById(@PathVariable Long id) {
                // Logic to fetch product
                return new Product(id, "Example Product");
            }

            @PostMapping
            public ResponseEntity<Product> createProduct(@RequestBody Product product) {
                // Logic to save product
                return new ResponseEntity<>(product, HttpStatus.CREATED);
            }
        }
        ```

8.  **When would you use `@RequestParam` versus `@PathVariable`?**
    *   **Answer:**
        *   **`@PathVariable`**: Used to extract values from the URI path. It's suitable for identifying a specific resource. For example, in `/users/{id}`, `id` would be a path variable.
            ```java
            @GetMapping("/users/{id}")
            public User getUser(@PathVariable Long id) { // id comes from URI path
                // ...
            }
            ```
        *   **`@RequestParam`**: Used to extract values from the query string parameters of the URL. It's suitable for filtering, sorting, or pagination. For example, in `/products?category=electronics&minPrice=100`.
            ```java
            @GetMapping("/products")
            public List<Product> getProducts(@RequestParam String category,
                                             @RequestParam(required = false) Double minPrice) { // category & minPrice from query params
                // ...
            }
            ```

9.  **How do you handle exceptions in a Spring Boot REST API?**
    *   **Answer:** You can handle exceptions using a combination of `@ControllerAdvice` and `@ExceptionHandler`.
        *   **`@ControllerAdvice`**: A global annotation that allows you to apply exception handling logic across multiple controllers.
        *   **`@ExceptionHandler`**: Placed on a method within a `@Controller` or `@ControllerAdvice` class, it specifies the type of exception it should handle.
        ```java
        @ControllerAdvice
        public class GlobalExceptionHandler {

            @ExceptionHandler(ResourceNotFoundException.class)
            public ResponseEntity<ErrorResponse> handleResourceNotFoundException(ResourceNotFoundException ex) {
                ErrorResponse error = new ErrorResponse(HttpStatus.NOT_FOUND.value(), ex.getMessage());
                return new ResponseEntity<>(error, HttpStatus.NOT_FOUND);
            }

            @ExceptionHandler(MethodArgumentNotValidException.class)
            public ResponseEntity<Map<String, String>> handleValidationExceptions(MethodArgumentNotValidException ex) {
                Map<String, String> errors = new HashMap<>();
                ex.getBindingResult().getAllErrors().forEach((error) -> {
                    String fieldName = ((FieldError) error).getField();
                    String errorMessage = error.getDefaultMessage();
                    errors.put(fieldName, errorMessage);
                });
                return new ResponseEntity<>(errors, HttpStatus.BAD_REQUEST);
            }
        }
        ```

### Data Access

10. **What is Spring Data JPA? How does it simplify data access?**
    *   **Answer:** Spring Data JPA is a sub-project of Spring Data that aims to significantly improve the implementation of data access layers by reducing the amount of boilerplate code required. It provides a set of interfaces and conventions that allow you to define repository interfaces.
        It simplifies data access by:
        *   **Automatic repository implementation:** You define an interface extending `JpaRepository` (or `CrudRepository`, `PagingAndSortingRepository`), and Spring Data JPA automatically provides the implementation for common CRUD (Create, Read, Update, Delete) operations.
        *   **Query methods:** You can define custom queries by simply naming methods according to a specific convention (e.g., `findByLastNameAndFirstName(String lastName, String firstName)`). Spring Data JPA parses the method name and generates the appropriate query.
        *   **Reduced boilerplate:** Eliminates the need to write standard DAO (Data Access Object) implementations.

11. **How do you connect a Spring Boot application to a database?**
    *   **Answer:**
        1.  **Add dependencies:** Include the appropriate JDBC driver and Spring Data JPA starter in your `pom.xml` (e.g., `spring-boot-starter-data-jpa` and `mysql-connector-java` or `postgresql`).
        2.  **Configure `application.properties` (or `application.yml`):** Provide the database connection details.
            ```properties
            spring.datasource.url=jdbc:mysql://localhost:3306/mydatabase
            spring.datasource.username=root
            spring.datasource.password=password
            spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
            spring.jpa.hibernate.ddl-auto=update # or create, create-drop, none
            spring.jpa.show-sql=true
            ```
        3.  **Define JPA entities:** Create classes annotated with `@Entity` to map to database tables.
        4.  **Create repository interfaces:** Extend `JpaRepository` for your entities. Spring Boot will automatically configure a `DataSource` and `EntityManagerFactory`.

### Testing

12. **How do you write unit tests and integration tests in Spring Boot?**
    *   **Answer:**
        *   **Unit Tests:** Focus on testing individual components in isolation, often mocking external dependencies. You'd use standard JUnit and Mockito.
            ```java
            // Example Unit Test (Service layer)
            @ExtendWith(MockitoExtension.class)
            public class ProductServiceTest {

                @Mock
                private ProductRepository productRepository;

                @InjectMocks
                private ProductService productService; // Assuming ProductService uses ProductRepository

                @Test
                void testGetProductById() {
                    Product product = new Product(1L, "Test Product");
                    when(productRepository.findById(1L)).thenReturn(Optional.of(product));

                    Product foundProduct = productService.getProductById(1L);
                    assertEquals("Test Product", foundProduct.getName());
                }
            }
            ```
        *   **Integration Tests:** Test the interaction between multiple components or the entire application context. Spring Boot provides annotations to facilitate this:
            *   `@SpringBootTest`: Loads the full Spring application context. Can be used with `webEnvironment` to simulate a running server.
            *   `@WebMvcTest`: Used for testing Spring MVC controllers. It loads only the web layer components, making tests faster. Mocks out other layers.
            *   `@DataJpaTest`: Used for testing JPA repositories. It configures an in-memory database and loads only JPA-related components.

            ```java
            // Example Integration Test (Controller layer)
            @WebMvcTest(ProductController.class)
            public class ProductControllerIntegrationTest {

                @Autowired
                private MockMvc mockMvc;

                @MockBean // Mocks the service layer, so it doesn't load the full app context
                private ProductService productService;

                @Test
                void testGetProductById() throws Exception {
                    Product product = new Product(1L, "Test Product");
                    when(productService.getProductById(1L)).thenReturn(product);

                    mockMvc.perform(get("/api/products/1")
                                .contentType(MediaType.APPLICATION_JSON))
                            .andExpect(status().isOk())
                            .andExpect(jsonPath("$.name").value("Test Product"));
                }
            }
            ```

### Actuator and Monitoring

13. **What is Spring Boot Actuator? Name a few common endpoints.**
    *   **Answer:** Spring Boot Actuator provides production-ready features to help you monitor and manage your application when it's pushed to production. It exposes operational information about the running application, such as health, metrics, info, and environment properties.
        Common endpoints (accessible via `/actuator/{endpoint-name}`):
        *   `/health`: Shows application health information (e.g., database connection, disk space).
        *   `/info`: Displays arbitrary application information (e.g., version, build info).
        *   `/metrics`: Provides various metrics (e.g., JVM memory, CPU usage, HTTP requests).
        *   `/env`: Shows the current Spring `Environment` properties.
        *   `/beans`: Displays a complete list of all Spring beans in the application.
        *   `/loggers`: Allows inspecting and modifying the log levels of the application at runtime.

### Configuration and Profiles

14. **How do you externalize configuration in Spring Boot?**
    *   **Answer:** Spring Boot allows externalizing configuration so you can work with the same application code in different environments. It loads properties from various sources in a specific order. Common ways include:
        *   **`application.properties` or `application.yml` files:** These are the default locations for configuration.
        *   **Profile-specific files:** `application-{profile}.properties` (e.g., `application-dev.properties`, `application-prod.properties`).
        *   **Command-line arguments:** Properties can be passed as command-line arguments (e.g., `java -jar myapp.jar --server.port=8081`).
        *   **Environment variables:** Properties can be mapped from environment variables.
        *   **System properties:** Using `-D` flags (e.g., `java -Dserver.port=8082 -jar myapp.jar`).
        *   **Spring Cloud Config Server:** For more advanced, centralized configuration management across microservices.

15. **Explain Spring Boot Profiles. How are they used?**
    *   **Answer:** Spring Profiles provide a way to segregate parts of your application configuration and make them available only in certain environments. This allows you to have different configurations (e.g., database connections, logging levels, external service URLs) for development, testing, and production environments without changing the code.
        **How they are used:**
        *   **Defining profiles:** You define properties in `application-{profile}.properties` or `application-{profile}.yml` files.
        *   **Activating profiles:** You can activate a profile using:
            *   `spring.profiles.active` property in `application.properties`.
            *   Command-line argument: `--spring.profiles.active=dev`.
            *   Environment variable: `SPRING_PROFILES_ACTIVE=prod`.
            *   Programmatically using `SpringApplication.setAdditionalProfiles()`.
        *   **Conditional bean creation:** Use `@Profile("dev")` or `@Profile("!prod")` on `@Component` or `@Configuration` classes/methods to conditionally register beans based on the active profile.

### Other Important Concepts

16. **What is the difference between `@Component`, `@Service`, `@Repository`, and `@Controller`?**
    *   **Answer:** These are stereotype annotations that are specializations of `@Component`. They are primarily used for semantic clarity, better organization, and enabling specific features:
        *   `@Component`: A generic stereotype for any Spring-managed component. It's the base annotation.
        *   `@Service`: Indicates that an annotated class is a "Service". Typically, it holds business logic. It's a specialization of `@Component` for the service layer.
        *   `@Repository`: Indicates that an annotated class is a "Repository". It's a specialization of `@Component` that also enables Spring's exception translation for data access exceptions (e.g., converting JDBC-specific exceptions to Spring's `DataAccessException` hierarchy).
        *   `@Controller`: Indicates that an annotated class is a "Controller" in the MVC pattern. It's used to handle web requests and return views.
        *   `@RestController`: A convenience annotation that combines `@Controller` and `@ResponseBody`. It's used for building RESTful web services, as it automatically serializes the return value directly into the HTTP response body.

17. **What is Lombok and how is it used in Spring Boot projects?**
    *   **Answer:** Project Lombok is a Java library that automatically plugs into your build process and "lomboks" away boilerplate code. It generates code at compile time, reducing verbosity and improving readability.
        In Spring Boot projects, it's commonly used to:
        *   Generate getters and setters (`@Getter`, `@Setter`).
        *   Generate constructors (`@NoArgsConstructor`, `@AllArgsConstructor`, `@RequiredArgsConstructor`).
        *   Generate `equals()`, `hashCode()`, and `toString()` methods (`@Data`, `@EqualsAndHashCode`, `@ToString`).
        *   Simplify logging (`@Slf4j`, `@Log4j2`).
        *   Create immutable classes (`@Value`).
        **Example:**
        ```java
        import lombok.Data;

        @Data // Generates getters, setters, equals, hashCode, toString
        public class User {
            private Long id;
            private String name;
            private String email;
        }
        ```
