## İçindekiler
- [Lombok](#lombok)
- [MapStruct](#mapstruct)
- [Spring IoC (Inversion of Control)](#spring-ioc-inversion-of-control)
- [Spring Controller](#spring-controller)
- [SpringBoot (Genel)](#springboot-genel)
- [Request-Response](#request-response)
- [Mapping](#mapping)
- [Validations](#validations)
- [Global Exceptions](#global-exceptions)
- [Business Rules](#business-rules)
- [JDBC-JPA](#jdbc-jpa)
- [application.properties - yaml](#applicationproperties---yaml)
- [Derived Method Naming, JPQL, Native SQL](#derived-method-naming-jpql-native-sql)
- [Redis](#redis)
- [MicroService](#microservice)
- [Monolith vs MicroService](#monolith-vs-microservice)
- [SQL](#sql)

---

## Lombok

Lombok, Java uygulamalarında boilerplate (tekrarlayan) kodları azaltmak için kullanılan bir kütüphanedir. Lombok, sınıf tanımlarına anotasyonlar ekleyerek getter ve setter metodları, `toString()`, `equals()`, `hashCode()`, yapıcı metodlar gibi yaygın olarak kullanılan kodları otomatik olarak oluşturur.

### Lombok Anotasyonları

- **@Getter ve @Setter**: Alanlar için getter ve setter metodlarını oluşturur.
  
  ```java
  import lombok.Getter;
  import lombok.Setter;

  public class Person {
      @Getter @Setter
      private String name;
      private int age;
  }
  ```

- **@ToString**: Sınıf için `toString()` metodunu oluşturur.

  ```java
  import lombok.ToString;

  @ToString
  public class Person {
      private String name;
      private int age;
  }
  ```

- **@EqualsAndHashCode**: Sınıf için `equals()` ve `hashCode()` metodlarını oluşturur.

  ```java
  import lombok.EqualsAndHashCode;

  @EqualsAndHashCode
  public class Person {
      private String name;
      private int age;
  }
  ```

- **@AllArgsConstructor ve @NoArgsConstructor**: Tüm alanlar için yapıcı metod ve parametresiz yapıcı metod oluşturur.

  ```java
  import lombok.AllArgsConstructor;
  import lombok.NoArgsConstructor;

  @AllArgsConstructor
  @NoArgsConstructor
  public class Person {
      private String name;
      private int age;
  }
  ```

### Sonuç

Lombok, tekrarlayan kodları azaltarak geliştiricilerin daha temiz ve bakımı kolay kod yazmasını sağlar.

---

## MapStruct

MapStruct, Java nesneleri arasında tür güvenli ve yüksek performanslı dönüşümler gerçekleştiren bir araçtır. Özellikle DTO (Data Transfer Object) ve entity dönüşümlerinde sıkça kullanılır.

### Kullanımı

- **Maven Bağımlılıkları**:

  ```xml
  <dependency>
      <groupId>org.mapstruct</groupId>
      <artifactId>mapstruct</artifactId>
      <version>1.4.2.Final</version>
  </dependency>
  <dependency>
      <groupId>org.mapstruct</groupId>
      <artifactId>mapstruct-processor</artifactId>
      <version>1.4.2.Final</version>
  </dependency>
  ```

- **DTO ve Entity Dönüşümü**:

  ```java
  @Mapper
  public interface CarMapper {
      CarMapper INSTANCE = Mappers.getMapper(CarMapper.class);

      @Mapping(source = "numberOfSeats", target = "seatCount")
      CarDto carToCarDto(Car car);
  }
  ```

### Sonuç

MapStruct, manuel dönüşüm kodları yazmayı ortadan kaldırır ve dönüşüm işlemlerini basit ve verimli hale getirir.

---

## Spring IoC (Inversion of Control)

Spring IoC, nesnelerin oluşturulması, yönetilmesi ve bağımlılıklarının sağlanması işlemlerini merkezi bir yerden yönetmek için kullanılan bir prensiptir.

### IoC ve DI (Dependency Injection)

- **IoC Container**: Nesnelerin yaşam döngüsünü ve bağımlılıklarını yönetir.
- **Dependency Injection**: Nesnelerin ihtiyaç duyduğu bağımlılıkları dışarıdan sağlar.

### Örnek Kullanım

- **Bean Tanımı**:

  ```java
  @Configuration
  public class AppConfig {
      @Bean
      public MyService myService() {
          return new MyServiceImpl();
      }
  }
  ```

- **Bean Kullanımı**:

  ```java
  @Service
  public class MyServiceConsumer {
      private final MyService myService;

      @Autowired
      public MyServiceConsumer(MyService myService) {
          this.myService = myService;
      }
  }
  ```

### Sonuç

Spring IoC, uygulamalarda bağımlılık yönetimini ve nesne oluşturma süreçlerini basitleştirir ve merkezi bir şekilde yönetir.

---

## Spring Controller

Spring Controller'lar, HTTP isteklerini karşılamak ve uygun yanıtları döndürmek için kullanılır. MVC (Model-View-Controller) yapısının bir parçasıdır.

### Örnek Kullanım

- **Basit Bir Controller**:

  ```java
  @RestController
  @RequestMapping("/api")
  public class MyController {

      @GetMapping("/hello")
      public String sayHello() {
          return "Hello, World!";
      }
  }
  ```

- **PathVariable ve RequestParam Kullanımı**:

  ```java
  @GetMapping("/greet/{name}")
  public String greet(@PathVariable String name) {
      return "Hello, " + name;
  }

  @GetMapping("/greet")
  public String greetWithRequestParam(@RequestParam String name) {
      return "Hello, " + name;
  }
  ```

### Sonuç

Spring Controller'lar, web uygulamalarında kullanıcı etkileşimlerini yönetmek için kritik öneme sahiptir. MVC yapısı sayesinde uygulamaların bakımı ve genişletilmesi kolaylaşır.

---

## SpringBoot (Genel)

Spring Boot, Spring Framework üzerine inşa edilmiş, mikro hizmet mimarisine uygun, hızlı ve kolay bir şekilde üretim düzeyinde uygulamalar geliştirmeyi sağlayan bir araçtır.

### Özellikleri

- **Hızlı Başlangıç**: Spring Boot, minimum konfigürasyonla projelere hızlı bir başlangıç yapmanızı sağlar.
- **Yerleşik Sunucu**: Yerleşik Tomcat, Jetty veya Undertow sunucuları ile gelir.
- **Otomatik Konfigürasyon**: Sık kullanılan kütüphaneler ve Spring modülleri için otomatik konfigürasyon sağlar.
- **Bağımlılık Yönetimi**: Spring Boot Starter'lar ile bağımlılık yönetimi ve versiyon uyumluluğu sağlar.

### Örnek Kullanım

1. **Spring Boot Projesi Oluşturma**:

   ```bash
   spring init --dependencies=web my-project
   cd my-project
   ```

2. **Ana Uygulama Sınıfı**:

   ```java
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;

   @SpringBootApplication
   public class MyApplication {
       public static void main(String[] args) {
           SpringApplication.run(MyApplication.class, args);
       }
   }
   ```

3. **Basit Bir REST Controller**:

   ```java
   import org.springframework.web.bind.annotation.GetMapping;
   import org.springframework.web.bind.annotation.RestController;

   @RestController
   public class HelloController {
       @GetMapping("/hello")
       public String hello() {
           return "Hello, World!";
       }
   }
   ```

### Sonuç

Spring Boot, mikro hizmet mimarisi ve modern uygulama geliştirme ihtiyaçlarını karşılayan güçlü bir araçtır. Hızlı başlangıç, otomatik konfigürasyon ve yerleşik sunucular gibi özellikleriyle geliştiricilerin işini büyük ölçüde kolaylaştırır.

---

## Request-Response

Spring uygulamalarında, HTTP istekleri (request) ve yanıtları (response) nasıl işlenir.

### Request Handling

- **HTTP GET İstekleri**:

  ```java
  @RestController
  public class MyController {
      @GetMapping("/api/data")
      public String getData() {
          return "Data";
      }
  }
  ```

- **HTTP POST İstekleri**:

  ```java
  @RestController
  public class MyController {
      @PostMapping("/api/data")
      public ResponseEntity<String> postData(@RequestBody String data) {
          return ResponseEntity.ok("Received: " + data);
      }
  }
  ```

### Response Handling

- **Yanıt Döndürme**:

  ```java
  @RestController
  public class MyController {
      @GetMapping("/api/data")
      public ResponseEntity<String> getData() {
          return new ResponseEntity<>("Data", HttpStatus.OK);
      }
  }
  ```

### Sonuç

Request-Response yapısı, web uygulamalarında istemci

ve sunucu arasındaki iletişimi yönetir. Spring, bu süreçleri kolaylaştırır ve esnek bir yapı sunar.

---

## Mapping

Spring uygulamalarında veri transferi ve iş kuralları için DTO'lar ve entity'ler arasında nasıl dönüşüm yapılır.

### DTO ve Entity Dönüşümü

- **Entity**:

  ```java
  public class User {
      private Long id;
      private String name;
      private String email;
  }
  ```

- **DTO**:

  ```java
  public class UserDTO {
      private Long id;
      private String name;
  }
  ```

- **Mapper**:

  ```java
  public class UserMapper {
      public UserDTO toDTO(User user) {
          UserDTO dto = new UserDTO();
          dto.setId(user.getId());
          dto.setName(user.getName());
          return dto;
      }

      public User toEntity(UserDTO dto) {
          User user = new User();
          user.setId(dto.getId());
          user.setName(dto.getName());
          return user;
      }
  }
  ```

### Sonuç

Mapping, veri transferi ve iş kuralları için önemlidir. DTO ve entity dönüşümleri, veri güvenliği ve iş kurallarının uygulanması açısından kritik öneme sahiptir.

---

## Validations

Spring uygulamalarında veri doğrulama işlemleri nasıl gerçekleştirilir.

### Anotasyonlar ile Doğrulama

- **Entity**:

  ```java
  import javax.validation.constraints.NotEmpty;

  public class User {
      @NotEmpty(message = "Name cannot be empty")
      private String name;
      private String email;
  }
  ```

- **Controller**:

  ```java
  @RestController
  public class UserController {
      @PostMapping("/users")
      public ResponseEntity<String> createUser(@Valid @RequestBody User user) {
          return ResponseEntity.ok("User is valid");
      }
  }
  ```

### Custom Validator

- **Custom Annotation**:

  ```java
  @Target({ ElementType.FIELD })
  @Retention(RetentionPolicy.RUNTIME)
  @Constraint(validatedBy = CustomValidator.class)
  public @interface CustomConstraint {
      String message() default "Invalid value";
      Class<?>[] groups() default {};
      Class<? extends Payload>[] payload() default {};
  }
  ```

- **Validator**:

  ```java
  public class CustomValidator implements ConstraintValidator<CustomConstraint, String> {
      @Override
      public boolean isValid(String value, ConstraintValidatorContext context) {
          return value != null && value.startsWith("A");
      }
  }
  ```

### Sonuç

Validations, veri bütünlüğünü ve iş kurallarının uygulanmasını sağlar. Spring, basit ve gelişmiş doğrulama mekanizmaları sunar.

---

## Global Exceptions

Spring uygulamalarında global exception handling nasıl gerçekleştirilir.

### @ControllerAdvice ile Global Exception Handling

- **Global Exception Handler**:

  ```java
  @ControllerAdvice
  public class GlobalExceptionHandler {
      @ExceptionHandler(value = { Exception.class })
      public ResponseEntity<Object> handleException(Exception ex) {
          return new ResponseEntity<>("An error occurred: " + ex.getMessage(), HttpStatus.INTERNAL_SERVER_ERROR);
      }
  }
  ```

### Özel Exception Sınıfları

- **Custom Exception**:

  ```java
  public class CustomException extends RuntimeException {
      public CustomException(String message) {
          super(message);
      }
  }
  ```

- **Exception Handler**:

  ```java
  @ControllerAdvice
  public class CustomExceptionHandler {
      @ExceptionHandler(value = { CustomException.class })
      public ResponseEntity<Object> handleCustomException(CustomException ex) {
          return new ResponseEntity<>("Custom error: " + ex.getMessage(), HttpStatus.BAD_REQUEST);
      }
  }
  ```

### Sonuç

Global exceptions, uygulama genelinde tutarlı ve merkezi bir hata yönetimi sağlar. Spring, bu süreci kolaylaştıran güçlü araçlar sunar.

---

## Business Rules

Spring uygulamalarında iş kuralları nasıl uygulanır.

### Service Katmanı ile İş Kuralları

- **Service**:

  ```java
  @Service
  public class UserService {
      public void createUser(User user) {
          if (user.getName().isEmpty()) {
              throw new CustomException("Name cannot be empty");
          }
          // İş kuralları uygulanır
      }
  }
  ```

### AOP (Aspect-Oriented Programming) ile İş Kuralları

- **Aspect**:

  ```java
  @Aspect
  @Component
  public class LoggingAspect {
      @Before("execution(* com.example.service.UserService.*(..))")
      public void logBefore(JoinPoint joinPoint) {
          System.out.println("Before method: " + joinPoint.getSignature().getName());
      }
  }
  ```

### Sonuç

Business rules, uygulamanın iş mantığını ve veri bütünlüğünü sağlar. Service katmanı ve AOP, bu kuralların uygulanmasını kolaylaştırır.

---

## JDBC-JPA

Spring uygulamalarında veri erişimi için JDBC ve JPA nasıl kullanılır.

### JDBC

- **JdbcTemplate Kullanımı**:

  ```java
  @Service
  public class UserService {
      @Autowired
      private JdbcTemplate jdbcTemplate;

      public List<User> findAll() {
          return jdbcTemplate.query("SELECT * FROM users", new UserRowMapper());
      }
  }

  public class UserRowMapper implements RowMapper<User> {
      @Override
      public User mapRow(ResultSet rs, int rowNum) throws SQLException {
          User user = new User();
          user.setId(rs.getLong("id"));
          user.setName(rs.getString("name"));
          user.setEmail(rs.getString("email"));
          return user;
      }
  }
  ```

### JPA

- **Entity Tanımı**:

  ```java
  @Entity
  public class User {
      @Id
      @GeneratedValue(strategy = GenerationType.IDENTITY)
      private Long id;
      private String name;
      private String email;
  }
  ```

- **Repository Kullanımı**:

  ```java
  @Repository
  public interface UserRepository extends JpaRepository<User, Long> {
  }
  ```

- **Service Kullanımı**:

  ```java
  @Service
  public class UserService {
      @Autowired
      private UserRepository userRepository;

      public List<User> findAll() {
          return userRepository.findAll();
      }
  }
  ```

### Sonuç

JDBC ve JPA, veri erişiminde farklı ihtiyaçlara cevap veren güçlü araçlardır. Spring, bu araçlarla entegrasyonu kolaylaştırır ve esneklik sağlar.

---

## application.properties - yaml

Spring Boot uygulamalarında konfigürasyon ayarları için `application.properties` ve `application.yml` dosyaları nasıl kullanılır.

### application.properties

- **Örnek Konfigürasyon**:

  ```properties
  server.port=8080
  spring.datasource.url=jdbc:mysql://localhost:3306/mydb
  spring.datasource.username=root
  spring.datasource.password=secret
  ```

### application.yml

- **Örnek Konfigürasyon**:

  ```yaml
  server:
    port: 8080

  spring:
    datasource:
      url: jdbc:mysql://localhost:3306/mydb
      username: root
      password: secret
  ```

### Sonuç

`application.properties` ve `application.yml`, Spring Boot uygulamalarında konfigürasyon yönetimini esnek ve okunabilir hale getirir.

---

## Derived Method Naming, JPQL, Native SQL

Spring Data JPA'da türetilmiş metod isimlendirme, JPQL ve native SQL sorguları nasıl kullanılır.

### Derived Method Naming

- **Repository**:

  ```java
  @Repository
  public interface UserRepository extends JpaRepository<User, Long> {
      List<User> findByName(String name);
      List<User> findByEmail(String email);
  }
  ```

### JPQL

- **Örnek JPQL Sorgusu**:

  ```java
  @Query("SELECT u FROM User u WHERE u.email = ?1")
  List<User> findByEmail(String email);
  ```

### Native SQL

- **Örnek Native SQL Sorgusu**:

  ```java
  @Query(value = "SELECT * FROM users WHERE email = ?1", nativeQuery = true)
  List<User> findByEmailNative(String email);
  ```

### Sonuç

Spring Data JPA, veri sorgulama işlemlerini kolaylaştıran türetilmiş metod isimlendirme, JPQL ve native SQL desteği sunar.

---

## Redis

Redis, in-memory (bellek içi) bir veri tabanı olup, yüksek performanslı veri depolama ve erişim sağlar.

### Redis Kullanımı

- **Bağlantı Konfigürasyonu**:

  ```properties
  spring.redis.host=localhost
  spring.redis.port=6379
  ```

- **RedisTemplate Kullanımı**:

  ```java
  @Service
  public class RedisService {
      @Autowired
      private RedisTemplate<String, Object> redisTemplate;

      public void save(String key, Object value) {
          redisTemplate.opsForValue().set(key, value);
      }

      public Object find(String key) {
          return redisTemplate.opsForValue().get(key);
      }
  }
  ```

### Sonuç

Redis, yüksek hızlı veri erişimi ve önbellekleme için güçlü bir araçtır. Spring, Redis ile entegrasyonu kolaylaştırır ve esneklik sağlar.

---



## MicroService

Mikro hizmetler, büyük ve karmaşık uygulamaların daha küçük, bağımsız ve yönetilebilir parçalara bölünmesini sağlayan bir mimari yaklaşımdır.

### Mikro Hizmetlerin Özellikleri

- **Bağımsız Dağıtım**: Her bir hizmet bağımsız olarak dağıtılabilir ve yönetilebilir.
- **Tek Sorumluluk İlkesi**: Her bir hizmet belirli bir işlevi yerine getirir.
- **Teknoloji Bağımsızlığı**: Her bir hizmet farklı teknolojilerle geliştirilebilir.

### Örnek Mikro Hizmet Yapısı

- **Kullanıcı Hizmeti**:

  ```java
  @RestController
  @RequestMapping("/users")
  public class UserController {
      @GetMapping("/{id}")
      public User getUserById(@PathVariable Long id) {
          // Kullanıcıyı veritabanından al
      }
  }
  ```

- **Sipariş Hizmeti**:

  ```java
  @RestController
  @RequestMapping("/orders")
  public class OrderController {
      @GetMapping("/{id}")
      public Order getOrderById(@PathVariable Long id) {
          // Siparişi veritabanından al
      }
  }
  ```

### Sonuç

Mikro hizmetler, büyük ölçekli ve karmaşık uygulamaların yönetimini ve bakımını kolaylaştırır. Bağımsız dağıtım ve teknoloji bağımsızlığı gibi özellikleriyle esneklik sağlar.

---

## Monolith vs MicroService

Monolitik ve mikro hizmet mimarileri arasındaki farklar ve her birinin avantajları ve dezavantajları.

### Monolitik Mimari

- **Avantajları**:
  - Basitlik: Tek bir kod tabanı ve dağıtım birimi.
  - Performans: Aynı bellek alanında çalıştıkları için düşük gecikme.

- **Dezavantajları**:
  - Esneklik: Değişiklik yapmak tüm uygulamayı etkiler.
  - Ölçeklenebilirlik: Belli bir noktadan sonra ölçeklendirmek zorlaşır.

### Mikro Hizmet Mimari

- **Avantajları**:
  - Bağımsız Dağıtım: Her hizmet bağımsız olarak dağıtılabilir.
  - Ölçeklenebilirlik: Her hizmet bağımsız olarak ölçeklenebilir.
  - Teknoloji Çeşitliliği: Her hizmet farklı teknolojilerle geliştirilebilir.

- **Dezavantajları**:
  - Karmaşıklık: Dağıtık sistemlerin yönetimi daha zordur.
  - Performans: Hizmetler arası iletişim gecikmelere neden olabilir.

### Sonuç

Monolitik ve mikro hizmet mimarileri, farklı ihtiyaçlara ve koşullara göre avantaj ve dezavantajlara sahiptir. Uygulama gereksinimlerine göre doğru mimari seçilmelidir.

---

## SQL

SQL, ilişkisel veri tabanları ile etkileşim kurmak için kullanılan bir sorgulama dilidir.

### Temel SQL Komutları

- **SELECT**:

  ```sql
  SELECT * FROM users;
  ```

- **INSERT**:

  ```sql
  INSERT INTO users (name, email) VALUES ('John Doe', 'john@example.com');
  ```

- **UPDATE**:

  ```sql
  UPDATE users SET email = 'john.doe@example.com' WHERE name = 'John Doe';
  ```

- **DELETE**:

  ```sql
  DELETE FROM users WHERE name = 'John Doe';
  ```

### İlişkisel Veri Tabanı Yönetim Sistemleri (RDBMS)

- **MySQL**: Açık kaynaklı ve yaygın olarak kullanılan bir RDBMS.
- **PostgreSQL**: İleri seviye özelliklere sahip açık kaynaklı bir RDBMS.
- **Oracle**: Kurumsal düzeyde özellikler sunan bir RDBMS.

### Sonuç

SQL, ilişkisel veri tabanları ile veri yönetimi ve sorgulama için temel bir araçtır. Temel SQL komutları ve RDBMS'ler, veri tabanı yönetimini ve etkileşimini sağlar.

---
