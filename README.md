

## İçindekiler
- [ENTITY](#entity)
  - [User Entity](#user-entity)
    - [Açıklama](#user-entity-açıklama)
  - [Product Entity](#product-entity)
    - [Açıklama](#product-entity-açıklama)
  - [Category Entity](#category-entity)
    - [Açıklama](#category-entity-açıklama)
---
- [REPOSITORY](#repository)
  - [Product Repository](#productrepository)
    - [Açıklama](#product-repository-açıklama)
    - [Detay](#product-repository-detay)
  - [User Repository](#userrepository)
    - [Açıklama](#userrepository-açıklama)
    - [Detay](#userrepository-detay)
---
- [SERVICE](#service)
  - [Product Service ve Product Service Implementation](#productservice-ve-productserviceimpl)
    - [Açıklama](#productservice-ve-productserviceimpl-açıklama)
    - [Product Service Detay](#productservice-detay)
    - [Product Service Impl Detay](#productserviceimpl-detay)
  - [AuthService ve AuthServiceImpl](#authservice-ve-authserviceimpl)
    - [Açıklama](#authservice-ve-authserviceimpl-açıklama)
    - [AuthService Detay](#authservice-detay)
    - [AuthServiceImpl Detay](#authserviceimpl-detay)
  - [User Service ve UserServiceImpl](#userservice-ve-userserviceimpl)
    - [Açıklama](#userservice-ve-userserviceimpl-açıklama)
    - [User Service Detay](#userservice-detay)
    - [User Service Impl Detay](#userserviceimpl-detay)
---
- [CONTROLLER](#controller)
  - [Auth Controller](#authcontroller)
    - [Auth Controller Açıklama](#authcontroller-açıklama)
    - [Auth Controller Detay](#authcontroller-detay)
  - [User Controller](#userscontroller)
    - [User Controller Açıklama](#userscontroller-açıklama)
    - [Auth Controller Detay](#userscontroller-detay)
  - [Product Controller](#productscontroller)
    - [Products Controller Açıklama](#productscontroller-açıklama)
    - [Products Controller Detay](#productscontroller-detay)
---
- [CORE](#core)
  - [RedisConfiguration](#redisconfiguration)
    - [Redis Configuration Açıklama](#redisconfiguration-açıklamala)
    - [Redis Configuration Detay](#redisconfiguration-detaylar)
  - [SecurityConfig](#securityconfig)
    - [SecurityConfig Açıklama](#securityconfig-açıklama)
    - [SecurityConfig Detay](#securityconfig-detay)
  - [JwtFilter](#jwtfilter)
    - [JwtFilter Açıklama](#jwtfilter-açıklama)
    - [JwtFilter Detay](#jwtfilter-detay)
  - [JwtService](#jwtservice)
    - [JwtService Açıklama](#jwtservice-açıklama)
    - [JwtService Detay](#jwtservice-detay)
---
- [DTOs](#dtos)
  - [LoginRequest](#loginrequest)
  - [CreateProductDto](#createproductdto)
  - [ListProductDto](#listproductdto)
  - [CreateUserRequest](#createuserrequest)
---
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
## Proje İncelemesi ve Açıklamalar

## ENTITY

### User Entity

```java @Getter @Setter @AllArgsConstructor @NoArgsConstructor @Entity @Table(name="users") public class User implements UserDetails {    
 @Id @GeneratedValue(strategy = GenerationType.IDENTITY) @Column(name="id") private Long id;    
 @Column(name="email") private String email;    
 @Column(name="password") private String password;    
 @Column(name="name") private String name;    
 @Column(name="surname") private String surname;    
 @Column(name="identityno") private String identityNo;    
 @Override public Collection<? extends GrantedAuthority> getAuthorities() { // roller return null; }    
@Override public String getUsername() { return email; }}   
```   
#### User Entity Açıklama

1. `@Getter`: Lombok tarafından bu sınıftaki tüm alanlar için getter metodları oluşturulur.
2. `@Setter`: Lombok tarafından bu sınıftaki tüm alanlar için setter metodları oluşturulur.
3. `@AllArgsConstructor`: Tüm alanları parametre olarak alan bir constructor oluşturur.
4. `@NoArgsConstructor`: Parametresiz bir constructor oluşturur.
5. `@Entity`: Bu sınıfın bir JPA entity (varlık) sınıfı olduğunu belirtir.
6. `@Table(name="users")`: Bu varlığın veritabanındaki `users` tablosuna karşılık geldiğini belirtir.
7. `@Id`: Bu alanın birincil anahtar olduğunu belirtir.
8. `@GeneratedValue(strategy = GenerationType.IDENTITY)`: Birincil anahtarın otomatik olarak veritabanı tarafından oluşturulacağını belirtir.
9. `@Column(name="id")`: `id` alanının veritabanındaki `id` sütununa karşılık geldiğini belirtir.
10. `@Column(name="email")`: `email` alanının veritabanındaki `email` sütununa karşılık geldiğini belirtir.
11. `@Column(name="password")`: `password` alanının veritabanındaki `password` sütununa karşılık geldiğini belirtir.
12. `@Column(name="name")`: `name` alanının veritabanındaki `name` sütununa karşılık geldiğini belirtir.
13. `@Column(name="surname")`: `surname` alanının veritabanındaki `surname` sütununa karşılık geldiğini belirtir.
14. `@Column(name="identityno")`: `identityNo` alanının veritabanındaki `identityno` sütununa karşılık geldiğini belirtir.
15. `implements UserDetails`: Bu sınıfın Spring Security'den `UserDetails` arayüzünü uyguladığını belirtir. Bu, kullanıcıya ait güvenlik bilgilerini sağlamaya yönelik metodların tanımlandığı anlamına gelir.
16. `getAuthorities()`: Kullanıcının yetkilerini (rollerini) döndüren metod. Şu anda `null` döndürüyor.
17. `getUsername()`: Kullanıcının kullanıcı adını döndüren metod. Bu örnekte, `email` alanı kullanıcı adı olarak kullanılıyor.

### Product Entity

```java @Getter @Setter @NoArgsConstructor @AllArgsConstructor @Entity @Table(name="products") public class Product {    
 @Id @GeneratedValue(strategy = GenerationType.IDENTITY) @Column(name="id") private int id;    
 @Column(name="name") private String name;    
 @Column(name="price") private BigDecimal unitPrice;    
 @Column(name="stock") private int unitsInStock;    
@ManyToOne @JoinColumn(name="categoryid") private Category category;}   
```   
#### Product Entity Açıklama

1. `@Getter`: Lombok tarafından bu sınıftaki tüm alanlar için getter metodları oluşturulur.
2. `@Setter`: Lombok tarafından bu sınıftaki tüm alanlar için setter metodları oluşturulur.
3. `@NoArgsConstructor`: Parametresiz bir constructor oluşturur.
4. `@AllArgsConstructor`: Tüm alanları parametre olarak alan bir constructor oluşturur.
5. `@Entity`: Bu sınıfın bir JPA entity (varlık) sınıfı olduğunu belirtir.
6. `@Table(name="products")`: Bu varlığın veritabanındaki `products` tablosuna karşılık geldiğini belirtir.
7. `@Id`: Bu alanın birincil anahtar olduğunu belirtir.
8. `@GeneratedValue(strategy = GenerationType.IDENTITY)`: Birincil anahtarın otomatik olarak veritabanı tarafından oluşturulacağını belirtir.
9. `@Column(name="id")`: `id` alanının veritabanındaki `id` sütununa karşılık geldiğini belirtir.
10. `@Column(name="name")`: `name` alanının veritabanındaki `name` sütununa karşılık geldiğini belirtir.
11. `@Column(name="price")`: `unitPrice` alanının veritabanındaki `price` sütununa karşılık geldiğini belirtir.
12. `@Column(name="stock")`: `unitsInStock` alanının veritabanındaki `stock` sütununa karşılık geldiğini belirtir.
13. `@ManyToOne`: Bu alanın birçok ürünün tek bir kategoriye ait olduğunu belirtir.
14. `@JoinColumn(name="categoryid")`: Bu alanın `categoryid` sütunu ile ilişkili olduğunu belirtir.

### Category Entity

```java @Getter @Setter @AllArgsConstructor @NoArgsConstructor @Table(name="categories") @Entity public class Category {    
 @Id @GeneratedValue(strategy = GenerationType.IDENTITY) @Column(name="id") private int id;    
 @Column(name="name") private String name;    
@OneToMany(mappedBy = "category") private List<Product> products;}   
```   
#### Category Entity Açıklama

1. `@Getter`: Lombok tarafından bu sınıftaki tüm alanlar için getter metodları oluşturulur.
2. `@Setter`: Lombok tarafından bu sınıftaki tüm alanlar için setter metodları oluşturulur.
3. `@AllArgsConstructor`: Tüm alanları parametre olarak alan bir constructor oluşturur.
4. `@NoArgsConstructor`: Parametresiz bir constructor oluşturur.
5. `@Entity`: Bu sınıfın bir JPA entity (varlık) sınıfı olduğunu belirtir.
6. `@Table(name="categories")`: Bu varlığın veritabanındaki `categories` tablosuna karşılık geldiğini belirtir.
7. `@Id`: Bu alanın birincil anahtar olduğunu belirtir.
8. `@GeneratedValue(strategy = GenerationType.IDENTITY)`: Birincil anahtarın otomatik olarak veritabanı tarafından oluşturulacağını belirtir.
9. `@Column(name="id")`: `id` alanının veritabanındaki `id` sütununa karşılık geldiğini belirtir.
10. `@Column(name="name")`: `name` alanının veritabanındaki `name` sütununa karşılık geldiğini belirtir.
11. `@OneToMany(mappedBy = "category")`: Bu alanın birçok ürünün tek bir kategoriye ait olduğunu belirtir ve `Product` sınıfındaki `category` alanı ile ilişkilidir.

## REPOSITORY

### ProductRepository

```java public interface ProductRepository extends JpaRepository<Product, Integer> {    
 List<Product> findByNameLikeIgnoreCase(String name); Optional<Product> findByNameIgnoreCase(String name);    
 @Query(value = "Select p from Product p " + "inner join p.category " + "where p.unitPrice > :unitPrice and lower(p.name) like concat('%', lower(:name), '%')", nativeQuery=false) List<Product> findByNameAndUnitPriceGreaterThan(String name, BigDecimal unitPrice);    
@Query(value = "Select * from products p where p.price > :unitPrice and lower(p.name) LIKE concat('%', lower(:name), '%')", nativeQuery=true) List<Product> findByNameAndUnitPriceGreaterThanSql(String name, BigDecimal unitPrice);}   
```   
#### Product Repository Açıklama

1. `JpaRepository<Product, Integer>`: Bu arayüz, `Product` varlığı için CRUD işlemlerini sağlar.
2. `findByNameLikeIgnoreCase(String name)`: Ürün adını büyük/küçük harf duyarlılığı olmadan arayan metod.
3. `findByNameIgnoreCase(String name)`: Ürün adını büyük/küçük harf duyarlılığı olmadan arayan metod.
4. `@Query`: JPQL sorgusunu tanımlar, belirli bir fiyatın üzerindeki ve adı belirtilen ürünleri arar.
5. `nativeQuery=true`: Native SQL sorgusunu tanımlar, belirli bir fiyatın üzerindeki ve adı belirtilen ürünleri arar.

#### Product Repository Detay

```java public interface ProductRepository extends JpaRepository<Product, Integer> {   
```   
- **public interface ProductRepository**: `ProductRepository` adında bir arayüz tanımlar. `public` erişim belirleyicisi, bu arayüzün diğer paketlerden de erişilebileceğini belirtir.
- **extends JpaRepository<Product, Integer>**: Bu arayüz, Spring Data JPA'nın sağladığı `JpaRepository` arayüzünden türetilmiştir. Bu, `Product` nesneleri için temel CRUD (Create, Read, Update, Delete) işlemlerini sağlar. `Integer` tipi, `Product` nesnesinin birincil anahtarının veri türüdür.

### 1. findByNameLikeIgnoreCase Metodu

```java    
List<Product> findByNameLikeIgnoreCase(String name);   
```   
- **List<Product> findByNameLikeIgnoreCase(String name)**: Bu metod, ürün adının belirtilen `name` ile eşleşenlerini arar ve döner.
  - **List<Product>**: Bu metod, eşleşen ürünlerin bir listesini döner.
  - **findByNameLikeIgnoreCase**: Method adı, Spring Data JPA'nın sorgu oluşturma yeteneğinden yararlanır. `Like` ifadesi, SQL'deki `LIKE` anahtar kelimesine karşılık gelir ve büyük/küçük harf duyarlılığı olmaksızın arama yapar.
  - **String name**: Ürün adını aramak için kullanılan parametredir.

### 2. findByNameIgnoreCase Metodu

```java    
Optional<Product> findByNameIgnoreCase(String name);   
```   
- **Optional<Product> findByNameIgnoreCase(String name)**: Bu metod, belirtilen `name` ile tam olarak eşleşen bir ürünü arar ve döner.
  - **Optional<Product>**: Bu metod, ürün bulunduğunda bir `Product` nesnesi döner; eğer ürün bulunamazsa, `Optional.empty()` döner. Bu, null kontrolü yapmadan güvenli bir şekilde ürünün var olup olmadığını kontrol etmeyi sağlar.
  - **findByNameIgnoreCase**: Method adı, büyük/küçük harf duyarlılığı olmaksızın tam eşleşme araması yapar.
  - **String name**: Ürün adını aramak için kullanılan parametredir.

### 3. findByNameAndUnitPriceGreaterThan Metodu

```java    
@Query(value = "Select p from Product p " + "inner join p.category " + "where p.unitPrice > :unitPrice and lower(p.name) like concat('%', lower(:name), '%')", nativeQuery=false) List<Product> findByNameAndUnitPriceGreaterThan(String name, BigDecimal unitPrice);   
```   
- **@Query**: Bu anotasyon, metodun özel bir JPQL (Java Persistence Query Language) sorgusu kullanarak çalışacağını belirtir.
- **value = "Select p from Product p ...**: JPQL sorgusu.
  - `inner join p.category`: Ürünlerin kategorileri ile ilişkili olduğunu belirtir.
  - `where p.unitPrice > :unitPrice`: Belirtilen `unitPrice` değerinden büyük olan ürünleri bulur.
  - `lower(p.name) like concat('%', lower(:name), '%')`: Ürün adının belirli bir isimle eşleşip eşleşmediğini kontrol eder, büyük/küçük harf duyarlılığı olmadan.
  - `:unitPrice` ve `:name`: Metod parametreleri ile bağlanır.
- **List<Product>**: Bu metod, sorguya uyan ürünlerin bir listesini döner.

### 4. findByNameAndUnitPriceGreaterThanSql Metodu

```java    
@Query(value = "Select * from products p where p.price > :unitPrice and lower(p.name) LIKE concat('%', lower(:name), '%')", nativeQuery=true) List<Product> findByNameAndUnitPriceGreaterThanSql(String name, BigDecimal unitPrice);   
```   
- **@Query**: Bu anotasyon, metodun özel bir SQL sorgusu kullanarak çalışacağını belirtir.
- **value = "Select * from products p ...**: Native SQL sorgusu.
  - `where p.price > :unitPrice`: Belirtilen `unitPrice` değerinden büyük olan ürünleri bulur.
  - `lower(p.name) LIKE concat('%', lower(:name), '%')`: Ürün adının belirli bir isimle eşleşip eşleşmediğini kontrol eder, büyük/küçük harf duyarlılığı olmadan.
- **nativeQuery=true**: Bu sorgunun native SQL olduğunu belirtir.
- **List<Product>**: Bu metod, sorguya uyan ürünlerin bir listesini döner.

### Özet

`ProductRepository`, `Product` varlığı ile ilgili veritabanı işlemlerini gerçekleştirmek için gereken metodları tanımlar. İçinde:
- Ürün adını büyük/küçük harf duyarlılığı olmadan arama yapan ve döndüren metodlar.
- Ürün adını ve fiyatı kullanarak ürünleri sorgulayan özel JPQL ve native SQL sorguları ile veritabanında arama yapan metodlar bulunur.

Bu arayüz, uygulamanın veri erişim katmanında önemli bir rol oynar ve ürünlerle ilgili veritabanı işlemlerini kolaylaştırır.
### UserRepository

```java public interface UserRepository extends JpaRepository<User, Integer> {    
Optional<User> findByEmailIgnoreCase(String email);}   
```   
#### UserRepository Açıklama

1. `JpaRepository<User, Integer>`: Bu arayüz, `User` varlığı için CRUD işlemlerini sağlar.
2. `findByEmailIgnoreCase(String email)`: Kullanıcı e-postasını büyük/küçük harf duyarlılığı olmadan arayan metod.

#### UserRepository Detay
```java public interface UserRepository extends JpaRepository<User, Integer> {   
```   
- **public interface UserRepository**: `UserRepository` adında bir arayüz tanımlar. `public` erişim belirleyicisi, bu arayüzün diğer paketlerden de erişilebileceğini belirtir. Bu arayüz, kullanıcı ile ilgili veritabanı işlemlerini gerçekleştirmek için kullanılan bir yapı sağlar.
- **extends JpaRepository<User, Integer>**:
  - `JpaRepository<User, Integer>`: Spring Data JPA'nın sağladığı bir arayüzdür. `JpaRepository`, temel CRUD (Create, Read, Update, Delete) işlemleri için gerekli metodları otomatik olarak sağlar.
  - `User`: Bu repository'nin yönetiminde bulunan varlık sınıfıdır.
  - `Integer`: `User` varlığının birincil anahtarının veri türüdür. Bu durumda kullanıcı ID'si `Integer` türünde olacak.

### 1. findByEmailIgnoreCase Metodu

```java    
Optional<User> findByEmailIgnoreCase(String email);   
```   
- **Optional<User> findByEmailIgnoreCase(String email)**: Bu metod, belirtilen `email` ile eşleşen bir kullanıcıyı arar.
  - **Optional<User>**: Bu metod, kullanıcı bulunduğunda bir `User` nesnesi döner; eğer kullanıcı bulunamazsa, `Optional.empty()` döner. Bu, null kontrolü yapmadan güvenli bir şekilde kullanıcı nesnesinin var olup olmadığını kontrol etmeyi sağlar.
  - **findByEmailIgnoreCase**: Metod adı, Spring Data JPA'nın sorgu oluşturma yeteneğinden yararlanarak, kullanıcı e-postasını büyük/küçük harf duyarlılığı olmadan aramak için kullanılır. Burada "findBy" ifadesi, "email" alanına göre sorgulama yapılacağını belirtir. "IgnoreCase" ise, büyük/küçük harf duyarsız bir eşleşme sağlamak için kullanılır.
  - **String email**: Arama yapmak için kullanılan parametredir. Bu parametre, veritabanındaki kullanıcıların e-posta adreslerini karşılaştırmak için kullanılır.

### Özet

`UserRepository`, `User` varlığı ile ilgili veritabanı işlemlerini gerçekleştirmek için gerekli metodları tanımlar. İçinde:
- Kullanıcı e-postasına göre kullanıcıyı arayan ve döndüren bir metod bulunur. Bu metod, büyük/küçük harf duyarlılığı olmadan çalışır ve kullanıcı nesnesini güvenli bir şekilde döndürür.

Bu arayüz, uygulamanın veri erişim katmanında önemli bir rol oynar ve kullanıcılarla ilgili veritabanı işlemlerini kolaylaştırır.

## SERVICE

### ProductService ve ProductServiceImpl

```java public interface ProductService {    
ListProductDto getById(int id); List<ListProductDto> getAll(); List<ListProductDto> getByName(String name); List<ListProductDto> getByNameAndUnitPrice(String name, BigDecimal unitPrice); void add(CreateProductDto createProductDto);}   
```   
```java @Service @RequiredArgsConstructor public class ProductServiceImpl implements ProductService {    
 private final ProductRepository productRepository; private final ProductBusinessRules productBusinessRules;    
@Override @Cacheable(value = "product", key = "#id") public ListProductDto getById(int id) { Product product = productRepository.findById(id).orElseThrow (() -> new BusinessException("Böyle bir ürün yok"));    
 ProductMapper mapper = ProductMapper.INSTANCE; return mapper.productDtoFromProduct(product); }    
 @Override @Cacheable(value = "products") public List<ListProductDto> getAll() { List<Product> products = productRepository.findAll(); ProductMapper productMapper = ProductMapper.INSTANCE; return productMapper.productDtoListFromProductList(products); }    
 @Override public List<ListProductDto> getByName(String name) { List<Product> products = productRepository.findByNameLikeIgnoreCase("%"+name+"%"); ProductMapper productMapper = ProductMapper.INSTANCE; return productMapper.productDtoListFromProductList(products); }    
 @Override public List<ListProductDto> getByNameAndUnitPrice(String name, BigDecimal unitPrice) { List<Product> products = productRepository.findByNameAndUnitPriceGreaterThan(name, unitPrice); ProductMapper productMapper = ProductMapper.INSTANCE; return productMapper.productDtoListFromProductList(products); }    
@Override @CacheEvict(value = "products", allEntries = true) public void add(CreateProductDto createProductDto) { productBusinessRules.productWithSameNameShouldNotExist(createProductDto.getName()); Product product = ProductMapper.INSTANCE.productFromCreateDto(createProductDto); productRepository.save(product); }}   
```   
#### ProductService ve ProductServiceImpl Açıklama

1. `ProductService`: Ürünlerle ilgili işlevsellikleri tanımlar.
2. `ProductServiceImpl`: `ProductService` arayüzünün implementasyonunu sağlar.
3. `@Service`: Bu sınıfın bir servis bileşeni olduğunu belirtir.
4. `@RequiredArgsConstructor`: Lombok tarafından tüm final alanlar için bir constructor oluşturur ve bu alanları inject eder.
5. `productRepository.findById(id).orElseThrow(() -> new BusinessException("Böyle bir ürün yok"))`: Belirtilen id'ye sahip ürünü bulamazsa özel bir istisna fırlatır.
6. `ProductMapper.INSTANCE`: MapStruct kullanarak varlıkları DTO'lara dönüştürür.
7. `@Cacheable`: Sonuçların önbelleğe alınmasını sağlar.
8. `@CacheEvict`: Belirli bir önbellek girişini veya tüm girişleri temizler.
9. `productBusinessRules.productWithSameNameShouldNotExist(createProductDto.getName())`: Aynı ada sahip ürünlerin var olup olmadığını kontrol eden iş kuralı.

#### ProductService Detay
```java public interface ProductService {   
```   
- **public interface ProductService**: `ProductService` adında bir arayüz tanımlar. `public` erişim belirleyicisi, bu arayüzün diğer paketlerden de erişilebileceğini belirtir. Arayüz, bir sınıfın uygulaması gereken metodları tanımlar, ancak bu metodların kendisini değil, sadece imzalarını içerir.

#### 1. getById Metodu

```java    
ListProductDto getById(int id);   
```   
- **ListProductDto getById(int id)**: Bu metod, belirli bir ürünün ID'sini alır ve o ürüne karşılık gelen `ListProductDto` nesnesini döner.
  - **int id**: Parametre olarak alınan ürün ID'sidir.
  - **ListProductDto**: Ürün bilgilerini taşıyan bir veri transfer nesnesidir (DTO). Bu nesne, ürünle ilgili bilgileri içerir ve istemciye iletilmek üzere tasarlanmıştır.

#### 2. getAll Metodu

```java    
List<ListProductDto> getAll();   
```   
- **List<ListProductDto> getAll()**: Bu metod, tüm ürünleri döndürür.
  - **List<ListProductDto>**: Tüm ürünlerin `ListProductDto` türünde bir listesini döner. Bu liste, sistemdeki mevcut tüm ürünlerin bilgilerini içerir.

#### 3. getByName Metodu

```java    
List<ListProductDto> getByName(String name);   
```   
- **List<ListProductDto> getByName(String name)**: Bu metod, belirli bir ürün adını alır ve o adla eşleşen ürünleri döner.
  - **String name**: Parametre olarak alınan ürün adıdır. Bu ad ile eşleşen ürünler aratılacaktır.
  - **List<ListProductDto>**: Ürün adıyla eşleşen tüm `ListProductDto` nesnelerinin listesini döner.

#### 4. getByNameAndUnitPrice Metodu

```java    
List<ListProductDto> getByNameAndUnitPrice(String name, BigDecimal unitPrice);   
```   
- **List<ListProductDto> getByNameAndUnitPrice(String name, BigDecimal unitPrice)**: Bu metod, belirli bir ürün adı ve birim fiyatı alır ve bu kriterlere uyan ürünleri döner.
  - **String name**: Ürün adı parametresi.
  - **BigDecimal unitPrice**: Ürün birim fiyatı parametresi. Bu fiyattan yüksek olan ürünler aranacaktır.
  - **List<ListProductDto>**: Bu kriterlere uyan ürünlerin `ListProductDto` nesnelerinin listesini döner.

#### 5. add Metodu

```java    
void add(CreateProductDto createProductDto);   
```   
- **void add(CreateProductDto createProductDto)**: Bu metod, yeni bir ürün eklemek için kullanılır.
  - **CreateProductDto createProductDto**: Yeni bir ürün oluşturmak için gerekli bilgileri içeren veri transfer nesnesidir. Bu nesne, ürünün adı, stok durumu, fiyatı ve kategorisi gibi bilgileri içerir.
  - **void**: Bu metod herhangi bir değer döndürmez. Yeni ürünü eklemek için gerekli işlemleri gerçekleştirir.

### Özet

`ProductService` arayüzü, ürünlerle ilgili işlevleri tanımlar. İçinde, belirli bir ID ile ürün alma, tüm ürünleri listeleme, ürün adına göre arama yapma, ürün adı ve birim fiyatına göre arama yapma ve yeni bir ürün ekleme gibi metodlar yer alır. Bu arayüz, uygulamanızın servis katmanında ürün yönetimi ile ilgili işlevselliği sağlamak için kullanılacaktır.

Bu arayüzü implement eden sınıflar, bu metodların nasıl çalışacağını tanımlamakla sorumludur.

#### ProductServiceImpl Detay
```java @Service @RequiredArgsConstructor public class ProductServiceImpl implements ProductService {   
```   
- `@Service`: Bu sınıfın bir servis bileşeni olduğunu belirtir. Spring, bu sınıfı bileşen taraması ile bulur ve yönetir.
- `@RequiredArgsConstructor`: Lombok kütüphanesi, tüm final alanlar için bir constructor oluşturur. Böylece bağımlılıkları otomatik olarak enjekte eder.
- `public class ProductServiceImpl implements ProductService`: `ProductService` arayüzünü implement eden sınıf. Bu, `ProductService` arayüzünde tanımlanan tüm metodları uygulamak zorundadır.

```java    
private final ProductRepository productRepository; private final ProductBusinessRules productBusinessRules;   
```   
- `private final ProductRepository productRepository;`: Ürün veritabanı işlemlerini gerçekleştirmek için kullanılan repository. Spring tarafından otomatik olarak enjekte edilir.
- `private final ProductBusinessRules productBusinessRules;`: Ürün ile ilgili iş kurallarını kontrol eden bir nesne. Bu, ürün eklenmeden önce belirli kuralların kontrol edilmesini sağlar.

### Metodlar

#### 1. getById

```java    
@Override @Cacheable(value = "product", key = "#id") // product.1, product.2 public ListProductDto getById(int id) {   
```   
- `@Override`: Bu metodun bir üst sınıf veya arayüzde tanımlı olan bir metodun implementasyonu olduğunu belirtir.
- `@Cacheable(value = "product", key = "#id")`: Bu metod çağrıldığında, sonuçların Redis gibi bir önbellekte saklanmasını sağlar. `value` önbellek adını belirtir; `key` ise önbellek için anahtarı belirtir (bu durumda ürün ID'si).

```java    
Product product = productRepository.findById(id) .orElseThrow(() -> new BusinessException("Böyle bir ürün yok"));   
```   
- `productRepository.findById(id)`: Belirtilen ID'ye sahip ürünü veritabanında arar.
- `.orElseThrow(() -> new BusinessException("Böyle bir ürün yok"))`: Eğer ürün bulunamazsa, bir `BusinessException` fırlatır.

```java    
ProductMapper mapper = ProductMapper.INSTANCE; return mapper.productDtoFromProduct(product); }   
```   
- `ProductMapper mapper = ProductMapper.INSTANCE;`: `ProductMapper`'ın singleton örneğini alır. `ProductMapper`, MapStruct kullanarak `Product` ve `ListProductDto` arasında dönüşüm yapar.
- `return mapper.productDtoFromProduct(product);`: Bulunan `Product` nesnesini `ListProductDto` nesnesine dönüştürür ve döner.

#### 2. getAll

```java    
@Override @Cacheable(value = "products") public List<ListProductDto> getAll() {   
```   
- `@Cacheable(value = "products")`: Bu metod çağrıldığında, sonuçların önbelleğe alınmasını sağlar. Bu, tüm ürünlerin listelendiği metoddur.

```java    
List<Product> products = productRepository.findAll();   
```   
- `productRepository.findAll()`: Veritabanındaki tüm ürünleri alır.

```java    
ProductMapper productMapper = ProductMapper.INSTANCE; return productMapper.productDtoListFromProductList(products); }   
```   
- `ProductMapper productMapper = ProductMapper.INSTANCE;`: `ProductMapper`'ın singleton örneğini alır.
- `return productMapper.productDtoListFromProductList(products);`: Alınan ürün listesini `ListProductDto` listesine dönüştürür ve döner.

#### 3. getByName

```java    
@Override public List<ListProductDto> getByName(String name) {   
```   
- `public List<ListProductDto> getByName(String name)`: Ürün adını kullanarak ürünleri arayan bir metod.

```java    
List<Product> products = productRepository.findByNameLikeIgnoreCase("%"+name+"%");   
```   
- `productRepository.findByNameLikeIgnoreCase("%"+name+"%")`: Belirtilen isimle eşleşen ürünleri büyük/küçük harf duyarlılığı olmadan arar. `"%"+name+"%"` ifadesi, isimle eşleşen tüm ürünleri bulmak için kullanılan bir SQL gibi bir `LIKE` ifadesidir.

```java    
ProductMapper productMapper = ProductMapper.INSTANCE; return productMapper.productDtoListFromProductList(products); }   
```   
- Alınan ürün listesini `ListProductDto` listesine dönüştürür ve döner.

#### 4. getByNameAndUnitPrice

```java    
@Override public List<ListProductDto> getByNameAndUnitPrice(String name, BigDecimal unitPrice) {   
```   
- `public List<ListProductDto> getByNameAndUnitPrice(String name, BigDecimal unitPrice)`: Ürün adını ve birim fiyatını kullanarak ürünleri arayan bir metod.

```java    
List<Product> products = productRepository.findByNameAndUnitPriceGreaterThan(name, unitPrice);   
```   
- `productRepository.findByNameAndUnitPriceGreaterThan(name, unitPrice)`: Belirtilen isimle eşleşen ve birim fiyatı belirtilen değerden büyük olan ürünleri bulur.

```java    
ProductMapper productMapper = ProductMapper.INSTANCE; return productMapper.productDtoListFromProductList(products); }   
```   
- Alınan ürün listesini `ListProductDto` listesine dönüştürür ve döner.

#### 5. add

```java    
@Override @CacheEvict(value = "products", allEntries = true) public void add(CreateProductDto createProductDto) {   
```   
- `@CacheEvict(value = "products", allEntries = true)`: Bu metod çağrıldığında, önbellekten "products" anahtarına sahip tüm girişleri temizler. Yeni bir ürün eklendiğinde önbelleğin güncellenmesi için kullanılır.

```java    
productBusinessRules.productWithSameNameShouldNotExist(createProductDto.getName());   
```   
- `productBusinessRules.productWithSameNameShouldNotExist(createProductDto.getName())`: Yeni eklenmek istenen ürün adının zaten mevcut olup olmadığını kontrol eden iş kuralı.

```java    
Product product = ProductMapper.INSTANCE.productFromCreateDto(createProductDto);   
```   
- `ProductMapper.INSTANCE.productFromCreateDto(createProductDto)`: `CreateProductDto` nesnesini bir `Product` nesnesine dönüştürür.

```java    
productRepository.save(product); }   
```   
- `productRepository.save(product)`: Yeni `Product` nesnesini veritabanına kaydeder.

### Özet

- `ProductServiceImpl` sınıfı, ürünlerle ilgili iş mantığını içerir ve `ProductService` arayüzünü implement eder.
- Redis, veri önbellekleme için kullanılır; `@Cacheable` ve `@CacheEvict` anotasyonları ile önbellek yönetimi sağlanır.
- Ürün bilgileri üzerinde CRUD işlemleri gerçekleştirilir, özellikle `getById`, `getAll`, `getByName`, ve `add` metodları, veritabanındaki verileri alır veya günceller.
- `ProductMapper`, DTO'lar ve entity'ler arasında dönüştürme işlemlerini gerçekleştirir.
### AuthService ve AuthServiceImpl

```java  
public interface AuthService {  
 String login(LoginRequest loginRequest); String register(CreateUserRequest createUserRequest);}  
```  

```java  
@Service  
@RequiredArgsConstructor  
public class AuthServiceImpl implements AuthService {  
 private final PasswordEncoder passwordEncoder; private final JwtService jwtService; private final UserService userService; private final UserMapper userMapper;  
 @Override public String login(LoginRequest loginRequest) { UserDetails user = userService.loadUserByUsername(loginRequest.getEmail()); boolean passwordMatching = passwordEncoder.matches(loginRequest.getPassword(), user.getPassword()); if(!passwordMatching) throw new BusinessException("E-posta veya şifre hatalı.");  
 // ... JWT ÜRET return jwtService.generateToken(user.getUsername()); }  
 @Override public String register(CreateUserRequest createUserRequest) { User userToAdd = userMapper.userFromCreateRequest(createUserRequest); User user = userService.create(userToAdd); return jwtService.generateToken(user.getUsername()); }}  
```  

#### AuthService ve AuthServiceImpl Açıklama

1. **AuthService**: Kimlik doğrulama işlevlerini tanımlayan arayüz.
2. **AuthServiceImpl**: `AuthService` arayüzünü implement eden sınıf, kimlik doğrulama işlevlerinin gerçek implementasyonlarını içerir.
3. `@Service`: Bu sınıfın bir servis bileşeni olduğunu belirtir.
4. `@RequiredArgsConstructor`: Lombok tarafından tüm final alanlar için bir constructor oluşturur ve bu alanları inject eder.

### AuthService Detay
```java  
public interface AuthService {  
```  

- **public interface AuthService**: Kimlik doğrulama işlemleri için metodları tanımlayan bir arayüz. `public` erişim belirleyicisi, bu arayüzün diğer paketlerden de erişilebileceğini belirtir.

#### 1. login Metodu

```java  
 String login(LoginRequest loginRequest);  
```  

- **String login(LoginRequest loginRequest)**: Bu metod, bir kullanıcı giriş isteğini alır ve başarılı bir giriş sonrası JWT token'ı döner.
  - **LoginRequest loginRequest**: Parametre olarak alınan giriş isteği nesnesidir.
  - **String**: Başarılı giriş sonrası JWT token'ı döner.

#### 2. register Metodu

```java  
 String register(CreateUserRequest createUserRequest);  
```  

- **String register(CreateUserRequest createUserRequest)**: Bu metod, bir kullanıcı kayıt isteğini alır ve başarılı bir kayıt sonrası JWT token'ı döner.
  - **CreateUserRequest createUserRequest**: Parametre olarak alınan kullanıcı kayıt isteği nesnesidir.
  - **String**: Başarılı kayıt sonrası JWT token'ı döner.

### AuthServiceImpl Detay
```java  
@Service  
@RequiredArgsConstructor  
public class AuthServiceImpl implements AuthService {  
```  

- **@Service**: Bu sınıfın bir servis bileşeni olduğunu belirtir. Spring, bu sınıfı bileşen taraması ile bulur ve yönetir.
- **@RequiredArgsConstructor**: Lombok kütüphanesi, tüm final alanlar için bir constructor oluşturur. Böylece bağımlılıkları otomatik olarak enjekte eder.
- **public class AuthServiceImpl implements AuthService**: `AuthService` arayüzünü implement eden sınıf. Bu, `AuthService` arayüzünde tanımlanan tüm metodları uygulamak zorundadır.

```java  
 private final PasswordEncoder passwordEncoder; private final JwtService jwtService; private final UserService userService; private final UserMapper userMapper;  
```  

- **private final PasswordEncoder passwordEncoder**: Şifreleri şifrelemek ve karşılaştırmak için kullanılan bileşen.
- **private final JwtService jwtService**: JWT token oluşturma ve yönetimi için kullanılan servis.
- **private final UserService userService**: Kullanıcı servis bileşeni.
- **private final UserMapper userMapper**: Kullanıcı veri dönüşümleri için kullanılan bileşen.

### Metodlar

#### 1. login

```java  
 @Override public String login(LoginRequest loginRequest) {  
```  

- **@Override**: Bu metodun bir üst sınıf veya arayüzde tanımlı olan bir metodun implementasyonu olduğunu belirtir.
- **String login(LoginRequest loginRequest)**: Bu metod, bir kullanıcı giriş isteğini alır ve başarılı bir giriş sonrası JWT token'ı döner.
  - **LoginRequest loginRequest**: Parametre olarak alınan giriş isteği nesnesidir.

```java  
 UserDetails user = userService.loadUserByUsername(loginRequest.getEmail()); boolean passwordMatching = passwordEncoder.matches(loginRequest.getPassword(), user.getPassword()); if (!passwordMatching) throw new BusinessException("E-posta veya şifre hatalı.");  
```  

- **UserDetails user = userService.loadUserByUsername(loginRequest.getEmail())**: Kullanıcının e-posta adresine göre kullanıcı detaylarını yükler.
- **boolean passwordMatching = passwordEncoder.matches(loginRequest.getPassword(), user.getPassword())**: Girilen şifre ile kaydedilmiş şifreyi karşılaştırır.
- **if (!passwordMatching) throw new BusinessException("E-posta veya şifre hatalı.")**: Şifreler eşleşmezse özel bir iş istisnası fırlatır.

```java  
 return jwtService.generateToken(user.getUsername()); }  
```  

- **return jwtService.generateToken(user.getUsername())**: Kullanıcı adını kullanarak JWT token'ı oluşturur ve döner.

#### 2. register

```java  
 @Override public String register(CreateUserRequest createUserRequest) {  
```  

- **@Override**: Bu metodun bir üst sınıf veya arayüzde tanımlı olan bir metodun implementasyonu olduğunu belirtir.
- **String register(CreateUserRequest createUserRequest)**: Bu metod, bir kullanıcı kayıt isteğini alır ve başarılı bir kayıt sonrası JWT token'ı döner.
  - **CreateUserRequest createUserRequest**: Parametre olarak alınan kullanıcı kayıt isteği nesnesidir.

```java  
 User userToAdd = userMapper.userFromCreateRequest(createUserRequest); User user = userService.create(userToAdd); return jwtService.generateToken(user.getUsername()); }  
```  

- **User userToAdd = userMapper.userFromCreateRequest(createUserRequest)**: Kullanıcı kayıt isteğinden kullanıcı nesnesi oluşturur.
- **User user = userService.create(userToAdd)**: Yeni kullanıcıyı veritabanına kaydeder.
- **return jwtService.generateToken(user.getUsername())**: Kullanıcı adını kullanarak JWT token'ı oluşturur ve döner.

### Özet

- `AuthService` arayüzü, kimlik doğrulama işlemleri için metodları tanımlar.
- `AuthServiceImpl` sınıfı, bu metodların gerçek implementasyonlarını içerir.
- `login` metodu, kullanıcı giriş isteğini alır ve başarılı bir giriş sonrası JWT token'ı döner.
- `register` metodu, kullanıcı kayıt isteğini alır ve başarılı bir kayıt sonrası JWT token'ı döner.
- Kullanıcı bilgileri üzerinde kimlik doğrulama işlemleri gerçekleştirilir, özellikle `login` ve `register` metodları, veritabanındaki verileri doğrular veya günceller.
### UserService ve UserServiceImpl

```java public interface UserService extends UserDetailsService {    
User create(User user);}   
```   
```java @Service @RequiredArgsConstructor public class UserServiceImpl implements UserService {    
 private final UserRepository userRepository;    
 @Override public User create(User user) { userRepository.save(user); return user; }    
@Override public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException { return userRepository.findByEmailIgnoreCase(username) .orElseThrow(() -> new UsernameNotFoundException("")); }}   
```   
#### UserService ve UserServiceImpl Açıklama

1. `UserService`: Kullanıcılarla ilgili işlevsellikleri tanımlar ve `UserDetailsService` arayüzünü genişletir.
2. `UserServiceImpl`: `UserService` arayüzünün implementasyonunu sağlar.
3. `@Service`: Bu sınıfın bir servis bileşeni olduğunu belirtir.
4. `@RequiredArgsConstructor`: Lombok tarafından tüm final alanlar için bir constructor oluşturur ve bu alanları inject eder.
5. `userRepository.findByEmailIgnoreCase(username).orElseThrow(() -> new UsernameNotFoundException(""))`: Belirtilen kullanıcı adıyla kullanıcıyı bulamazsa özel bir istisna fırlatır.
6. `userRepository.save(user)`: Kullanıcıyı veritabanına kaydeder.

#### UserService Detay
```java public interface UserService extends UserDetailsService {   
```   
- **public interface UserService extends UserDetailsService**: `UserService` adında bir arayüz tanımlar ve `UserDetailsService` arayüzünü genişletir. `public` erişim belirleyicisi, bu arayüzün diğer paketlerden de erişilebileceğini belirtir. Arayüz, bir sınıfın uygulaması gereken metodları tanımlar, ancak bu metodların kendisini değil, sadece imzalarını içerir.

#### 1. create Metodu

```java    
User create(User user);   
```   
- **User create(User user)**: Bu metod, bir kullanıcı nesnesi alır ve onu veritabanına kaydeder.
  - **User user**: Parametre olarak alınan kullanıcı nesnesidir.
  - **User**: Veritabanına kaydedilen kullanıcı nesnesini döner.

### Özet

`UserService` arayüzü, kullanıcılarla ilgili işlevleri tanımlar. İçinde, kullanıcı oluşturma ve kullanıcı adıyla kullanıcı detaylarını yükleme gibi metodlar yer alır. Bu arayüz, uygulamanızın servis katmanında kullanıcı yönetimi ile ilgili işlevselliği sağlamak için kullanılacaktır.

Bu arayüzü implement eden sınıflar, bu metodların nasıl çalışacağını tanımlamakla sorumludur.

#### UserServiceImpl Detay
```java @Service @RequiredArgsConstructor public class UserServiceImpl implements UserService {   
```   
- `@Service`: Bu sınıfın bir servis bileşeni olduğunu belirtir. Spring, bu sınıfı bileşen taraması ile bulur ve yönetir.
- `@RequiredArgsConstructor`: Lombok kütüphanesi, tüm final alanlar için bir constructor oluşturur. Böylece bağımlılıkları otomatik olarak enjekte eder.
- `public class UserServiceImpl implements UserService`: `UserService` arayüzünü implement eden sınıf. Bu, `UserService` arayüzünde tanımlanan tüm metodları uygulamak zorundadır.

```java    
private final UserRepository userRepository;   
```   
- `private final UserRepository userRepository;`: Kullanıcı veritabanı işlemlerini gerçekleştirmek için kullanılan repository. Spring tarafından otomatik olarak enjekte edilir.

### Metodlar

#### 1. create

```java    
@Override public User create(User user) {   
```   
- `@Override`: Bu metodun bir üst sınıf veya arayüzde tanımlı olan bir metodun implementasyonu olduğunu belirtir.
- **User create(User user)**: Bu metod, bir kullanıcı nesnesi alır ve onu veritabanına kaydeder.
  - **User user**: Parametre olarak alınan kullanıcı nesnesidir.

```java    
userRepository.save(user);   
```   
- `userRepository.save(user);`: Kullanıcı nesnesini veritabanına kaydeder.

```java    
return user; }   
```   
- `return user;`: Kaydedilen kullanıcı nesnesini döner.

#### 2. loadUserByUsername

```java    
@Override public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {   
```   
- `@Override`: Bu metodun bir üst sınıf veya arayüzde tanımlı olan bir metodun implementasyonu olduğunu belirtir.
- **UserDetails loadUserByUsername(String username) throws UsernameNotFoundException**: Bu metod, belirli bir kullanıcı adını alır ve o kullanıcıya ait kullanıcı detaylarını döner.
  - **String username**: Parametre olarak alınan kullanıcı adıdır.
  - **throws UsernameNotFoundException**: Kullanıcı adı bulunamazsa bu istisna fırlatılır.

```java    
return userRepository.findByEmailIgnoreCase(username) .orElseThrow(() -> new UsernameNotFoundException("")); }   
```   
- `userRepository.findByEmailIgnoreCase(username).orElseThrow(() -> new UsernameNotFoundException(""))`: Belirtilen kullanıcı adıyla kullanıcıyı bulamazsa özel bir istisna fırlatır ve kullanıcı detaylarını döner.

### Özet

- `UserServiceImpl` sınıfı, kullanıcılarla ilgili iş mantığını içerir ve `UserService` arayüzünü implement eder.
- Kullanıcı oluşturma ve kullanıcı adıyla kullanıcı detaylarını yükleme işlemleri gerçekleştirilir.
- Kullanıcı bilgileri üzerinde CRUD işlemleri gerçekleştirilir, özellikle `create` ve `loadUserByUsername` metodları, veritabanındaki verileri alır veya günceller.

## CONTROLLER

### ProductsController

```java  
@RestController  
@RequestMapping("/api/v1/products")  
@RequiredArgsConstructor  
public class ProductsController {  
    private final ProductService productService;  

    @GetMapping()  
    public ResponseEntity<List<ListProductDto>> getAll() {  
        return ResponseEntity.ok(productService.getAll());  
    }  

    @PostMapping  
    public ResponseEntity<Void> add(@RequestBody @Valid CreateProductDto createProductDto) {  
        productService.add(createProductDto);  
        return new ResponseEntity<Void>(HttpStatus.CREATED);  
    }  

    @GetMapping("{name}")  
    public ResponseEntity<List<ListProductDto>> getByName(@PathVariable String name) {  
        return ResponseEntity.ok(productService.getByName(name));  
    }  

    @GetMapping("name-price")  
    public ResponseEntity<List<ListProductDto>> getByNameAndPrice(@RequestParam String name, @RequestParam BigDecimal unitPrice) {  
        return ResponseEntity.ok(productService.getByNameAndUnitPrice(name, unitPrice));  
    }  

    @GetMapping("id")  
    public ResponseEntity<ListProductDto> getById(@RequestParam int id) {  
        return ResponseEntity.ok(productService.getById(id));  
    }  
}  
```

#### ProductsController Açıklama

1. `ProductsController`: Ürünlerle ilgili HTTP isteklerini işleyen denetleyici sınıfıdır.
2. `@RestController`: Bu sınıfın bir RESTful web hizmeti denetleyicisi olduğunu belirtir.
3. `@RequestMapping("/api/v1/products")`: Bu denetleyiciye gelen tüm isteklerin `/api/v1/products` yolunu kullanacağını belirtir.
4. `@RequiredArgsConstructor`: Lombok tarafından tüm final alanlar için bir constructor oluşturur ve bu alanları inject eder.
5. `private final ProductService productService;`: Ürünlerle ilgili iş mantığını yöneten servis nesnesi. Spring tarafından otomatik olarak enjekte edilir.

#### ProductsController Detay

#### Metodlar

1. **getAll**

```java  
@GetMapping()  
public ResponseEntity<List<ListProductDto>> getAll() {  
    return ResponseEntity.ok(productService.getAll());  
}  
```

- **getAll**: Tüm ürünleri listeleyen bir HTTP GET metodudur.
  - `ResponseEntity.ok(productService.getAll())`: Servisten gelen tüm ürün listesini HTTP 200 OK ile döner.

2. **add**

```java  
@PostMapping  
public ResponseEntity<Void> add(@RequestBody @Valid CreateProductDto createProductDto) {  
    productService.add(createProductDto);  
    return new ResponseEntity<Void>(HttpStatus.CREATED);  
}  
```

- **add**: Yeni bir ürün eklemek için kullanılan bir HTTP POST metodudur.
  - `@RequestBody @Valid CreateProductDto createProductDto`: İstemciden gelen istek gövdesini `CreateProductDto` nesnesine dönüştürür ve doğrulama yapar.
  - `productService.add(createProductDto)`: Servis aracılığıyla yeni ürünü ekler.
  - `return new ResponseEntity<Void>(HttpStatus.CREATED)`: HTTP 201 Created yanıtı döner.

3. **getByName**

```java  
@GetMapping("{name}")  
public ResponseEntity<List<ListProductDto>> getByName(@PathVariable String name) {  
    return ResponseEntity.ok(productService.getByName(name));  
}  
```

- **getByName**: Belirli bir adı alarak o adla eşleşen ürünleri dönen bir HTTP GET metodudur.
  - `@PathVariable String name`: URL yolundan ürün adını alır.
  - `ResponseEntity.ok(productService.getByName(name))`: Servisten gelen adıyla eşleşen ürünleri HTTP 200 OK ile döner.

4. **getByNameAndPrice**

```java  
@GetMapping("name-price")  
public ResponseEntity<List<ListProductDto>> getByNameAndPrice(@RequestParam String name, @RequestParam BigDecimal unitPrice) {  
    return ResponseEntity.ok(productService.getByNameAndUnitPrice(name, unitPrice));  
}  
```

- **getByNameAndPrice**: Belirli bir adı ve birim fiyatı alarak eşleşen ürünleri dönen bir HTTP GET metodudur.
  - `@RequestParam String name`: URL sorgu parametrelerinden ürün adını alır.
  - `@RequestParam BigDecimal unitPrice`: URL sorgu parametrelerinden ürün birim fiyatını alır.
  - `ResponseEntity.ok(productService.getByNameAndUnitPrice(name, unitPrice))`: Servisten gelen sonuçları HTTP 200 OK ile döner.

5. **getById**

```java  
@GetMapping("id")  
public ResponseEntity<ListProductDto> getById(@RequestParam int id) {  
    return ResponseEntity.ok(productService.getById(id));  
}  
```

- **getById**: Belirli bir ID ile ürün bilgilerini dönen bir HTTP GET metodudur.
  - `@RequestParam int id`: URL sorgu parametrelerinden ürün ID'sini alır.
  - `ResponseEntity.ok(productService.getById(id))`: Servisten gelen ürünü HTTP 200 OK ile döner.

### Özet

`ProductsController`, ürünlerle ilgili CRUD işlemlerini gerçekleştiren HTTP isteklerini yöneten bir denetleyici sınıfıdır. `getAll`, `add`, `getByName`, `getByNameAndPrice`, ve `getById` metodları ile ürün verilerine erişim ve manipülasyon sağlar. Spring’in REST mimarisine uygun şekilde tasarlanmıştır.

### AuthController

```java  
@RestController  
@RequestMapping("api/v1/auth")  
@RequiredArgsConstructor  
public class AuthController {  
    private final AuthService authService;  

    @PostMapping("login")  
    public ResponseEntity<String> login(@RequestBody LoginRequest loginRequest){  
        return ResponseEntity.ok(authService.login(loginRequest));  
    }  

    @PostMapping("register")  
    public ResponseEntity<String> register(@RequestBody CreateUserRequest createUserRequest){  
        return ResponseEntity.ok(authService.register(createUserRequest));  
    }  
}  
```

#### AuthController Açıklama

1. `AuthController`: Kullanıcı kimlik doğrulama işlemleri ile ilgili HTTP isteklerini işleyen denetleyici sınıfıdır.
2. `@RestController`: Bu sınıfın bir RESTful web hizmeti denetleyicisi olduğunu belirtir.
3. `@RequestMapping("api/v1/auth")`: Bu denetleyiciye gelen tüm isteklerin `api/v1/auth` yolunu kullanacağını belirtir.
4. `@RequiredArgsConstructor`: Lombok tarafından tüm final alanlar için bir constructor oluşturur ve bu alanları inject eder.
5. `private final AuthService authService;`: Kimlik doğrulama işlemlerini yöneten servis nesnesi. Spring tarafından otomatik olarak enjekte edilir.

#### AuthController Detay

#### Metodlar

1. **login**

```java  
@PostMapping("login")  
public ResponseEntity<String> login(@RequestBody LoginRequest loginRequest){  
    return ResponseEntity.ok(authService.login(loginRequest));  
}  
```

- **login**: Kullanıcı giriş işlemi için kullanılan bir HTTP POST metodudur.
  - `@RequestBody LoginRequest loginRequest`: İstemciden gelen istek gövdesini `LoginRequest` nesnesine dönüştürür.
  - `return ResponseEntity.ok(authService.login(loginRequest))`: `authService` üzerinden giriş işlemini gerçekleştirir ve HTTP 200 OK ile sonucu döner.

2. **register**

```java  
@PostMapping("register")  
public ResponseEntity<String> register(@RequestBody CreateUserRequest createUserRequest){  
    return ResponseEntity.ok(authService.register(createUserRequest));  
}  
```

- **register**: Yeni bir kullanıcı kaydı işlemi için kullanılan bir HTTP POST metodudur.
  - `@RequestBody CreateUserRequest createUserRequest`: İstemciden gelen istek gövdesini `CreateUserRequest` nesnesine dönüştürür.
  - `return ResponseEntity.ok(authService.register(createUserRequest))`: `authService` üzerinden kullanıcı kaydını gerçekleştirir ve HTTP 200 OK ile sonucu döner.

### Özet

`AuthController`, kullanıcı kimlik doğrulama işlemlerini gerçekleştiren HTTP isteklerini yöneten bir denetleyici sınıfıdır. `login` ve `register` metodları ile kullanıcı girişi ve kaydı için gerekli işlevselliği sağlar. Spring’in REST mimarisine uygun şekilde tasarlanmıştır.

### UsersController

```java  
@RestController  
@RequestMapping("api/v1/users")  
@RequiredArgsConstructor  
public class UsersController {  
    private final UserService userService;  
}  
```

#### UsersController Açıklama

1. **UsersController**: Kullanıcı ile ilgili HTTP isteklerini işleyen denetleyici sınıfıdır.
2. **@RestController**: Bu sınıfın bir RESTful web hizmeti denetleyicisi olduğunu belirtir.
3. **@RequestMapping("api/v1/users")**: Bu denetleyiciye gelen tüm isteklerin `api/v1/users` yolunu kullanacağını belirtir.
4. **@RequiredArgsConstructor**: Lombok tarafından tüm final alanlar için bir constructor oluşturur ve bu alanları inject eder.
5. **private final UserService userService;**: Kullanıcı işlemlerini yöneten servis nesnesi. Spring tarafından otomatik olarak enjekte edilir.

#### UsersController Detay

### Özet

`UsersController`, kullanıcı ile ilgili HTTP isteklerini yöneten bir denetleyici sınıfıdır. `userService` aracılığıyla kullanıcı işlemleri ile ilgili işlevselliği sağlar. Spring’in REST mimarisine uygun şekilde tasarlanmıştır.

## CORE

### GlobalExceptionHandler
### GlobalExceptionHandler Açıklama
### GlobalExceptionHandler Detay

### RedisConfiguration

```java
@Configuration
public class RedisConfiguration {

  @Bean
  public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory connectionFactory) {
    RedisTemplate<String, Object> template = new RedisTemplate<>();
    template.setConnectionFactory(connectionFactory);
    template.setKeySerializer(new StringRedisSerializer());
    template.setValueSerializer(new GenericJackson2JsonRedisSerializer());
    template.setHashKeySerializer(new StringRedisSerializer());
    template.setHashValueSerializer(new GenericJackson2JsonRedisSerializer());
    return template;
  }

  @Bean
  public CacheManager cacheManager(RedisConnectionFactory redisConnectionFactory) {
    RedisCacheConfiguration configuration = RedisCacheConfiguration
            .defaultCacheConfig()
            .entryTtl(Duration.ofMinutes(30));
    return RedisCacheManager.builder(redisConnectionFactory).cacheDefaults(configuration).build();
  }
}
```

### RedisConfiguration Açıklamala

- **@Configuration**: Bu sınıfın bir konfigürasyon sınıfı olduğunu belirtir.
- **@Bean**: Metodun bir Spring bean döndürdüğünü belirtir.
- **RedisTemplate**: Redis işlemleri için kullanılır.
- **RedisConnectionFactory**: Redis bağlantı fabrikası.
- **StringRedisSerializer**: Redis anahtarlarını serileştirmek için kullanılır.
- **GenericJackson2JsonRedisSerializer**: Redis değerlerini serileştirmek için kullanılır.
- **CacheManager**: Spring cache yönetimini sağlar.
- **RedisCacheConfiguration**: Redis cache konfigürasyonu.
- **Duration**: Süreyi temsil eden sınıf.

### RedisConfiguration Detaylar

1. **Class Level Annotations**:
  - `@Configuration`: Bu sınıfın Spring konfigürasyon dosyası olduğunu belirtir.

2. **Methods**:
  - **redisTemplate()**:
    ```java
    @Bean
    public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory connectionFactory) {
      RedisTemplate<String, Object> template = new RedisTemplate<>();
      template.setConnectionFactory(connectionFactory);
      template.setKeySerializer(new StringRedisSerializer());
      template.setValueSerializer(new GenericJackson2JsonRedisSerializer());
      template.setHashKeySerializer(new StringRedisSerializer());
      template.setHashValueSerializer(new GenericJackson2JsonRedisSerializer());
      return template;
    }
    ```
    - `@Bean`: Metodun Spring tarafından yönetilen bir bean olduğunu belirtir.
    - `RedisTemplate<String, Object> template = new RedisTemplate<>();`: RedisTemplate nesnesi oluşturur.
    - `template.setConnectionFactory(connectionFactory);`: Redis bağlantı fabrikasını ayarlar.
    - `template.setKeySerializer(new StringRedisSerializer());`: Anahtarları String olarak serileştirir.
    - `template.setValueSerializer(new GenericJackson2JsonRedisSerializer());`: Değerleri JSON formatında serileştirir.
    - `template.setHashKeySerializer(new StringRedisSerializer());`: Hash anahtarlarını String olarak serileştirir.
    - `template.setHashValueSerializer(new GenericJackson2JsonRedisSerializer());`: Hash değerlerini JSON formatında serileştirir.
    - `return template;`: RedisTemplate nesnesini döner.

  - **cacheManager()**:
    ```java
    @Bean
    public CacheManager cacheManager(RedisConnectionFactory redisConnectionFactory) {
      RedisCacheConfiguration configuration = RedisCacheConfiguration
              .defaultCacheConfig()
              .entryTtl(Duration.ofMinutes(30));
      return RedisCacheManager.builder(redisConnectionFactory).cacheDefaults(configuration).build();
    }
    ```
    - `@Bean`: Metodun Spring tarafından yönetilen bir bean olduğunu belirtir.
    - `RedisCacheConfiguration configuration = RedisCacheConfiguration.defaultCacheConfig().entryTtl(Duration.ofMinutes(30));`: Varsayılan cache konfigürasyonunu oluşturur ve 30 dakika süre belirler.
    - `return RedisCacheManager.builder(redisConnectionFactory).cacheDefaults(configuration).build();`: RedisCacheManager nesnesini oluşturur ve döner.

---

### SecurityConfig

```java
@Configuration
@RequiredArgsConstructor
public class SecurityConfig {

  private final UserService userService;
  private final JwtFilter jwtFilter;
  
  @Bean
  public PasswordEncoder passwordEncoder() {
    return new BCryptPasswordEncoder();
  }

  @Bean
  public AuthenticationProvider authenticationProvider() {
    DaoAuthenticationProvider provider = new DaoAuthenticationProvider();
    provider.setPasswordEncoder(passwordEncoder());
    provider.setUserDetailsService(userService);
    return provider;
  }

  @Bean
  public AuthenticationManager authenticationManager(AuthenticationConfiguration config) throws Exception {
    return config.getAuthenticationManager();
  }

  @Bean
  public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    http
      .csrf(AbstractHttpConfigurer::disable)
      .httpBasic(AbstractHttpConfigurer::disable)
      .authorizeHttpRequests(req -> req
        .requestMatchers(HttpMethod.POST, "/api/v1/products/**").authenticated()
        .anyRequest().permitAll()
      )
      .addFilterBefore(jwtFilter, UsernamePasswordAuthenticationFilter.class);
    return http.build();
  }
}
```

### SecurityConfig Açıklama

- **@Configuration**: Bu sınıfın bir konfigürasyon sınıfı olduğunu belirtir.
- **@RequiredArgsConstructor**: Lombok tarafından, final alanlar için bir constructor oluşturur ve bu alanları inject eder.
- **@Bean**: Metodun bir Spring bean döndürdüğünü belirtir.
- **PasswordEncoder**: Şifreleme işlemleri için kullanılır.
- **BCryptPasswordEncoder**: Şifreleri BCrypt algoritmasıyla şifrelemek için kullanılır.
- **AuthenticationProvider**: Kullanıcı doğrulaması için kullanılır.
- **DaoAuthenticationProvider**: Kullanıcı detaylarını ve şifrelerini doğrulayan sağlayıcı.
- **AuthenticationManager**: AuthenticationManager konfigürasyonunu sağlar.
- **HttpSecurity**: HTTP güvenlik konfigürasyonunu sağlar.
- **csrf(AbstractHttpConfigurer::disable)**: CSRF korumasını devre dışı bırakır.
- **httpBasic(AbstractHttpConfigurer::disable)**: HTTP Basic Authentication'ı devre dışı bırakır.
- **authorizeHttpRequests**: HTTP isteklerinin yetkilendirilmesi için kullanılır.
- **requestMatchers**: Belirli URL desenlerine sahip istekleri eşleştirir.
- **addFilterBefore**: Belirtilen filtreyi başka bir filtrenin öncesinde ekler.
- **UsernamePasswordAuthenticationFilter**: Kullanıcı adı ve şifre ile kimlik doğrulama işlemlerini gerçekleştirir.

### SecurityConfig Detay

1. **Class Level Annotations**:
  - `@Configuration`: Bu sınıfın Spring konfigürasyon dosyası olduğunu belirtir.
  - `@RequiredArgsConstructor`: Lombok tarafından oluşturulan bir constructor ile final alanların inject edilmesini sağlar.

2. **Fields**:
  - `private final UserService userService;`: Kullanıcı servisi. Kullanıcı verilerini yönetir.
  - `private final JwtFilter jwtFilter;`: JWT filtrelemesi. JWT tokenleri doğrular.

3. **Methods**:
  - **passwordEncoder()**:
    ```java
    @Bean
    public PasswordEncoder passwordEncoder() {
      return new BCryptPasswordEncoder();
    }
    ```
    - `@Bean`: Metodun Spring tarafından yönetilen bir bean olduğunu belirtir.
    - `BCryptPasswordEncoder`: Şifreleri BCrypt algoritmasıyla şifrelemek için kullanılır.

  - **authenticationProvider()**:
    ```java
    @Bean
    public AuthenticationProvider authenticationProvider() {
      DaoAuthenticationProvider provider = new DaoAuthenticationProvider();
      provider.setPasswordEncoder(passwordEncoder());
      provider.setUserDetailsService(userService);
      return provider;
    }
    ```
    - `DaoAuthenticationProvider provider`: Kullanıcı detaylarını ve şifrelerini doğrulayan sağlayıcı.
    - `provider.setPasswordEncoder(passwordEncoder());`: Şifreleme sağlayıcısını ayarlar.
    - `provider.setUserDetailsService(userService);`: Kullanıcı servisini ayarlar.
    - `return provider;`: Sağlayıcıyı döndürür.

  - **authenticationManager()**:
    ```java
    @Bean
    public AuthenticationManager authenticationManager(AuthenticationConfiguration config) throws Exception {
      return config.getAuthenticationManager();
    }
    ```
    - `AuthenticationManager`: AuthenticationManager konfigürasyonunu sağlar.
    - `return config.getAuthenticationManager();`: Konfigürasyon dosyasından AuthenticationManager'ı döner.

  - **securityFilterChain()**:
    ```java
    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
      http
        .csrf(AbstractHttpConfigurer::disable)
        .httpBasic(AbstractHttpConfigurer::disable)
        .authorizeHttpRequests(req -> req
          .requestMatchers(HttpMethod.POST, "/api/v1/products/**").authenticated()
          .anyRequest().permitAll()
        )
        .addFilterBefore(jwtFilter, UsernamePasswordAuthenticationFilter.class);
      return http.build();
    }
    ```
    - `csrf(AbstractHttpConfigurer::disable)`: CSRF korumasını devre dışı bırakır.
    - `httpBasic(AbstractHttpConfigurer::disable)`: HTTP Basic Authentication'ı devre dışı bırakır.
    - `authorizeHttpRequests(req -> req.anyRequest().permitAll())`: Tüm isteklerin yetkilendirilmesini sağlar.
    - `requestMatchers(HttpMethod.POST, "/api/v1/products/**").authenticated()`: Belirtilen URL desenlerine sahip isteklerin doğrulanmasını sağlar.
    - `addFilterBefore(jwtFilter, UsernamePasswordAuthenticationFilter.class)`: JWT filtresini, UsernamePasswordAuthenticationFilter'dan önce ekler.
    - `return http.build();`: HttpSecurity nesnesini oluşturur ve döner.

---

### JwtFilter

```java
@Component
@RequiredArgsConstructor
public class JwtFilter extends OncePerRequestFilter {

  private final JwtService jwtService;

  @Override
  protected void doFilterInternal(HttpServletRequest request,
                                  HttpServletResponse response,
                                  FilterChain filterChain) throws ServletException, IOException {
    String jwtHeader = request.getHeader("Authorization");

    if(jwtHeader != null)
    {
      // JWT'i doğrula
      String jwt = jwtHeader.substring(7); // bearer abc

      Boolean isTokenValid = jwtService.validateToken(jwt);

      if(isTokenValid)
      {
         // Spring Security'e giriş yapıldığını haber ver.

        // TODO: roller
        // - Spring Security Boilerplate
        UsernamePasswordAuthenticationToken token = new
                UsernamePasswordAuthenticationToken(jwtService.extractUsername(jwt), null, null);

        token.setDetails(new WebAuthenticationDetailsSource().buildDetails(request));
        SecurityContextHolder.getContext().setAuthentication(token);
        // -
      }
    }

    filterChain.doFilter(request,response); // görevi sonraki zincir halkasına aktar.
  }
}
```

### JwtFilter Açıklama

- **@Component**: Bu sınıfın bir Spring bileşeni olduğunu belirtir.
- **@RequiredArgsConstructor**: Lombok tarafından, final alanlar için bir constructor oluşturur ve bu alanları inject eder.
- **OncePerRequestFilter**: Her istek için bir defa çalışacak olan bir filtre sağlar.
- **HttpServletRequest**: HTTP isteği ile ilgili bilgileri temsil eder.
- **HttpServletResponse**: HTTP yanıtı ile ilgili bilgileri temsil eder.
- **FilterChain**: Filtreler arasında geçiş yapmak için kullanılır.
- **validateToken()**: JWT'nin geçerliliğini kontrol eder.
- **UsernamePasswordAuthenticationToken**: Kullanıcı adı ve şifre ile kimlik doğrulama işlemlerini gerçekleştiren bir token.
- **SecurityContextHolder**: Güvenlik bağlamını tutar ve yönetir.

### JwtFilter Detay

1. **Class Level Annotations**:
  - `@Component`: Bu sınıfın Spring bileşeni olduğunu belirtir.
  - `@RequiredArgsConstructor`: Lombok tarafından oluşturulan bir constructor ile final alanların inject edilmesini sağlar.

2. **Fields**:
  - `private final JwtService jwtService;`: JWT işlemleri için gerekli olan servis. JWT tokenlerini doğrulamak için kullanılır.

3. **Methods**:
  - **doFilterInternal()**:
    ```java
    @Override
    protected void doFilterInternal(HttpServletRequest request,
                                    HttpServletResponse response,
                                    FilterChain filterChain) throws ServletException, IOException {
    ```
    - `protected void doFilterInternal(...)`: Bu metod, istek ve yanıt üzerinde işlem yapar. Her istek için bir defa çağrılır.

  - **Authorization Header**:
    ```java
    String jwtHeader = request.getHeader("Authorization");
    ```
    - `request.getHeader("Authorization")`: İstekten "Authorization" başlığını alır. JWT tokeni bu başlıkta taşınır.

  - **Token Extraction**:
    ```java
    if(jwtHeader != null) {
      String jwt = jwtHeader.substring(7); // bearer abc
    ```
    - `jwtHeader.substring(7)`: "Bearer " kelimesinden sonraki kısmı alır. Bu durumda JWT tokenini elde eder.

  - **Token Validation**:
    ```java
    Boolean isTokenValid = jwtService.validateToken(jwt);
    ```
    - `jwtService.validateToken(jwt)`: JWT'nin geçerliliğini kontrol eder. Eğer geçerliyse `true`, değilse `false` döner.

  - **Setting Authentication**:
    ```java
    if(isTokenValid) {
      UsernamePasswordAuthenticationToken token = new
              UsernamePasswordAuthenticationToken(jwtService.extractUsername(jwt), null, null);
    ```
    - `UsernamePasswordAuthenticationToken`: Geçerli token için bir kimlik doğrulama tokeni oluşturur. JWT'den kullanıcı adını çıkararak ayarlar.

  - **Details Setting**:
    ```java
    token.setDetails(new WebAuthenticationDetailsSource().buildDetails(request));
    ```
    - `setDetails(...)`: İstekle ilgili detayları ayarlar.

  - **Security Context Update**:
    ```java
    SecurityContextHolder.getContext().setAuthentication(token);
    ```
    - `SecurityContextHolder.getContext().setAuthentication(token)`: Güvenlik bağlamını günceller ve kullanıcıyı doğrular.

  - **Chain Filter**:
    ```java
    filterChain.doFilter(request,response);
    ```
    - `filterChain.doFilter(...)`: İsteği bir sonraki filtreye veya hedefe aktarır.

---

### JwtService

```java
@Service
public class JwtService
{
  @Value("${jwt.expiration}")
  private Long EXPIRATION;

  @Value("${jwt.secret_key}")
  private String SECRET_KEY;

  public String generateToken(String userName) {
    return Jwts
            .builder()
            .issuedAt(new Date(System.currentTimeMillis()))
            .expiration(new Date(System.currentTimeMillis() + EXPIRATION))
            .subject(userName)
            .signWith(getSignKey())
            .compact();
  }

  public Boolean validateToken(String token)
  {
    try {
      return getClaimsFromToken(token).getExpiration().after(new Date());
    }
    catch(Exception e)
    {
      return false;
    }
  }

  public String extractUsername(String token)
  {
    return getClaimsFromToken(token).getSubject();
  }

  private Claims getClaimsFromToken(String token)
  {
    SecretKey key = (SecretKey) getSignKey();
    return Jwts
            .parser()
            .verifyWith(key)
            .build()
            .parseSignedClaims(token)
            .getPayload();
  }

  private Key getSignKey() {
    byte[] keyBytes = Decoders.BASE64URL.decode(SECRET_KEY);
    return Keys.hmacShaKeyFor(keyBytes);
  }
}
```

### JwtService Açıklama

- **@Service**: Bu sınıfın bir servis bileşeni olduğunu belirtir.
- **@Value**: Uygulama ayarlarından değerleri almak için kullanılır.
- **Jwts**: JWT (JSON Web Token) oluşturmak ve doğrulamak için kullanılan bir sınıf.
- **Claims**: JWT içindeki yükleri temsil eder.
- **SecretKey**: JWT imzalarken kullanılan gizli anahtar.
- **Key**: Anahtar türündeki nesneleri temsil eder.
- **Date**: Tarih ve saat ile ilgili işlemleri yönetmek için kullanılır.

### JwtService Detay

1. **Class Level Annotations**:
  - `@Service`: Bu sınıfın Spring servis bileşeni olduğunu belirtir.

2. **Fields**:
  - `@Value("${jwt.expiration}")`: Uygulama ayarlarından JWT'nin geçerlilik süresini alır.
  - `@Value("${jwt.secret_key}")`: Uygulama ayarlarından JWT imzalamak için kullanılan gizli anahtarı alır.

3. **Methods**:
  - **generateToken()**:
    ```java
    public String generateToken(String userName) {
      return Jwts
              .builder()
              .issuedAt(new Date(System.currentTimeMillis()))
              .expiration(new Date(System.currentTimeMillis() + EXPIRATION))
              .subject(userName)
              .signWith(getSignKey())
              .compact();
    }
    ```
    - `Jwts.builder()`: Yeni bir JWT oluşturmak için bir builder döner.
    - `issuedAt(...)`: Tokenin oluşturulma zamanını ayarlar.
    - `expiration(...)`: Tokenin geçerlilik süresini ayarlar.
    - `subject(userName)`: Tokenin konu bilgisi olarak kullanıcı adını ayarlar.
    - `signWith(getSignKey())`: Tokeni imzalamak için gizli anahtarı kullanır.
    - `compact()`: Tokeni oluşturur ve döner.

  - **validateToken()**:
    ```java
    public Boolean validateToken(String token)
    {
      try {
        return getClaimsFromToken(token).getExpiration().after(new Date());
      }
      catch(Exception e)
      {
        return false;
      }
    }
    ```
    - `getClaimsFromToken(token)`: Tokenin yüklerini alır ve geçerliliğini kontrol eder.
    - `getExpiration().after(new Date())`: Tokenin geçerlilik süresinin geçerli olup olmadığını kontrol eder.

  - **extractUsername()**:
    ```java
    public String extractUsername(String token)
    {
      return getClaimsFromToken(token).getSubject();
    }
    ```
    - `getClaimsFromToken(token).getSubject()`: Tokenin konu bilgisini (kullanıcı adını) döner.

  - **getClaimsFromToken()**:
    ```java
    private Claims getClaimsFromToken(String token)
    {
      SecretKey key = (SecretKey) getSignKey();
      return Jwts
              .parser()
              .verifyWith(key)
              .build()
              .parseSignedClaims(token)
              .getPayload();
    }
    ```
    - `getSignKey()`: JWT'nin imzalanmasında kullanılan anahtarı alır.
    - `Jwts.parser()`: Tokeni analiz etmek için bir parser döner.
    - `parseSignedClaims(token)`: İmzalı tokeni çözümleyerek yükleri döner.

  - **getSignKey()**:
    ```java
    private Key getSignKey() {
      byte[] keyBytes = Decoders.BASE64URL.decode(SECRET_KEY);
      return Keys.hmacShaKeyFor(keyBytes);
    }
    ```
    - `Decoders.BASE64URL.decode(SECRET_KEY)`: Gizli anahtarı Base64 formatında çözümleyerek byte dizisine çevirir.
    - `Keys.hmacShaKeyFor(keyBytes)`: HMAC SHA algoritması için bir anahtar oluşturur.

---

### Açıklamalar

- **@Component**: Bu sınıfın bir Spring bileşeni olduğunu belirtir.
- **@RequiredArgsConstructor**: Lombok tarafından, final alanlar için bir constructor oluşturur ve bu alanları inject eder.
- **OncePerRequestFilter**: Her istek için bir defa çalışacak olan bir filtre sağlar.
- **HttpServletRequest**: HTTP isteği ile ilgili bilgileri temsil eder.
- **HttpServletResponse**: HTTP yanıtı ile ilgili bilgileri temsil eder.
- **FilterChain**: Filtreler arasında geçiş yapmak için kullanılır.
- **validateToken()**: JWT'nin geçerliliğini kontrol eder.
- **UsernamePasswordAuthenticationToken**: Kullanıcı adı ve şifre ile kimlik doğrulama işlemlerini gerçekleştiren bir token.
- **SecurityContextHolder**: Güvenlik bağlamını tutar ve yönetir.

### Detaylar

1. **Class Level Annotations**:
  - `@Component`: Bu sınıfın Spring bileşeni olduğunu belirtir.
  - `@RequiredArgsConstructor`: Lombok tarafından oluşturulan bir constructor ile final alanların inject edilmesini sağlar.

2. **Fields**:
  - `private final JwtService jwtService;`: JWT işlemleri için gerekli olan servis. JWT tokenlerini doğrulamak için kullanılır.

3. **Methods**:
  - **doFilterInternal()**:
    ```java
    @Override
    protected void doFilterInternal(HttpServletRequest request,
                                    HttpServletResponse response,
                                    FilterChain filterChain) throws ServletException, IOException {
    ```
    - `protected void doFilterInternal(...)`: Bu metod, istek ve yanıt üzerinde işlem yapar. Her istek için bir defa çağrılır.

  - **Authorization Header**:
    ```java
    String jwtHeader = request.getHeader("Authorization");
    ```
    - `request.getHeader("Authorization")`: İstekten "Authorization" başlığını alır. JWT tokeni bu başlıkta taşınır.

  - **Token Extraction**:
    ```java
    if(jwtHeader != null) {
      String jwt = jwtHeader.substring(7); // bearer abc
    ```
    - `jwtHeader.substring(7)`: "Bearer " kelimesinden sonraki kısmı alır. Bu durumda JWT tokenini elde eder.

  - **Token Validation**:
    ```java
    Boolean isTokenValid = jwtService.validateToken(jwt);
    ```
    - `jwtService.validateToken(jwt)`: JWT'nin geçerliliğini kontrol eder. Eğer geçerliyse `true`, değilse `false` döner.

  - **Setting Authentication**:
    ```java
    if(isTokenValid) {
      UsernamePasswordAuthenticationToken token = new
              UsernamePasswordAuthenticationToken(jwtService.extractUsername(jwt), null, null);
    ```
    - `UsernamePasswordAuthenticationToken`: Geçerli token için bir kimlik doğrulama tokeni oluşturur. JWT'den kullanıcı adını çıkararak ayarlar.

  - **Details Setting**:
    ```java
    token.setDetails(new WebAuthenticationDetailsSource().buildDetails(request));
    ```
    - `setDetails(...)`: İstekle ilgili detayları ayarlar.

  - **Security Context Update**:
    ```java
    SecurityContextHolder.getContext().setAuthentication(token);
    ```
    - `SecurityContextHolder.getContext().setAuthentication(token)`: Güvenlik bağlamını günceller ve kullanıcıyı doğrular.

  - **Chain Filter**:
    ```java
    filterChain.doFilter(request,response);
    ```
    - `filterChain.doFilter(...)`: İsteği bir sonraki filtreye veya hedefe aktarır.

---

### DTOs

#### LoginRequest

```java
@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
public class LoginRequest
{
  @NotBlank
  private String email;

  @NotBlank
  private String password;
}
```

#### LoginRequest Açıklamala

- **@Getter**: Tüm alanlar için getter metodları oluşturur.
- **@Setter**: Tüm alanlar için setter metodları oluşturur.
- **@AllArgsConstructor**: Tüm alanları içeren bir constructor oluşturur.
- **@NoArgsConstructor**: Parametresiz bir constructor oluşturur.
- **@NotBlank**: Alanın boş olmamasını sağlar.

---

#### CreateProductDto

```java
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
public class CreateProductDto implements Serializable
{
  @NotNull
  @NotBlank
  private String name;

  @NotNull
  @PositiveOrZero
  private int stock;

  @NotNull
  private BigDecimal unitPrice;

  @NotNull
  @Positive
  private int categoryId;
}
```

#### CreateProductDto  Açıklamala

- **Serializable**: Bu sınıfın serileştirilmesine izin verir.
- **@NotNull**: Alanın null olmamasını sağlar.
- **@NotBlank**: Alanın boş olmamasını sağlar.
- **@PositiveOrZero**: Alanın sıfır veya pozitif olmasını sağlar.
- **@Positive**: Alanın pozitif olmasını sağlar.

---

#### ListProductDto

```java
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
public class ListProductDto implements Serializable
{
  private int id;
  private String name;
  private BigDecimal unitPrice;
}
```

#### ListProductDto Açıklamala

- **Serializable**: Bu sınıfın serileştirilmesine izin verir.
- **@Getter**: Tüm alanlar için getter metodları oluşturur.
- **@Setter**: Tüm alanlar için setter metodları oluşturur.
- **@NoArgsConstructor**: Parametresiz bir constructor oluşturur.
- **@AllArgsConstructor**: Tüm alanları içeren bir constructor oluşturur.

---

#### CreateUserRequest

```java
@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
public class CreateUserRequest
{
  @NotBlank
  private String email;

  @NotBlank
  private String password;

  @NotBlank
  private String name;

  @NotBlank
  private String surname;

  @NotBlank
  @Size(min = 11, max = 11)
  private String identityNo;
}
```

#### CreateUserRequest Açıklamala

- **@NotBlank**: Alanın boş olmamasını sağlar.
- **@Size**: Alanın uzunluğunu belirler (bu durumda tam 11 karakter olmalıdır).
- **@Getter**: Tüm alanlar için getter metodları oluşturur.
- **@Setter**: Tüm alanlar için setter metodları oluşturur.
- **@AllArgsConstructor**: Tüm alanları içeren bir constructor oluşturur.
- **@NoArgsConstructor**: Parametresiz bir constructor oluşturur.

---
