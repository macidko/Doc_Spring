

## İçindekiler
- [Proje İncelemesi ve Açıklamalar](#proje-incelemesi-ve-açıklamalar)
  - [User Entity](#user-entity)
    - [Açıklama](#user-entity-açıklama)
  - [Product Entity](#product-entity)
    - [Açıklama](#product-entity-açıklama)
  - [Category Entity](#category-entity)
    - [Açıklama](#category-entity-açıklama)
  - [Product Repository](#productrepository)
    - [Açıklama](#product-repository-açıklama)
    - [Detay](#product-repository-detay)
  - [User Repository](#userrepository)
    - [Açıklama](#userrepository-açıklama)
    - [Detay](#userrepository-detay)
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
### ProductsController Açıklama

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

### AuthController Açıklama

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

### UsersController Açıklama

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

### Özet

`UsersController`, kullanıcı ile ilgili HTTP isteklerini yöneten bir denetleyici sınıfıdır. `userService` aracılığıyla kullanıcı işlemleri ile ilgili işlevselliği sağlar. Spring’in REST mimarisine uygun şekilde tasarlanmıştır.

### DTO Sınıfları

**LoginRequest**

```java @Getter @Setter @AllArgsConstructor @NoArgsConstructor public class LoginRequest {    
 @NotBlank private String email;    
@NotBlank private String password;}   
```   
#### LoginRequest Açıklama

1. `@NotBlank`: Alanın boş olamayacağını belirtir.
2. `LoginRequest`: Giriş isteği için veri transfer nesnesi.

**CreateProductDto ve ListProductDto**

```java @Getter @Setter @NoArgsConstructor @AllArgsConstructor public class CreateProductDto implements Serializable {    
 @NotNull @NotBlank private String name;    
 @NotNull @PositiveOrZero private int stock;    
 @NotNull private BigDecimal unitPrice;    
@NotNull @Positive private int categoryId;}   
```   
```java @Getter @Setter @NoArgsConstructor @AllArgsConstructor public class ListProductDto implements Serializable {    
private int id; private String name; private BigDecimal unitPrice;}   
```   
#### CreateProductDto ve ListProductDto Açıklama

1. `CreateProductDto`: Ürün oluşturma isteği için veri transfer nesnesi.
2. `ListProductDto`: Ürün listeleme için veri transfer nesnesi.
3. `@NotNull`, `@NotBlank`, `@PositiveOrZero`, `@Positive`: Alanların doğrulanmasını sağlar.

**CreateUserRequest**

```java @Getter @Setter @AllArgsConstructor @NoArgsConstructor public class CreateUserRequest {    
 @NotBlank private String email;    
 @NotBlank private String password;    
 @NotBlank private String name;    
 @NotBlank private String surname;    
@NotBlank @Size(min = 11, max = 11) private String identityNo;}   
```   
#### CreateUserRequest Açıklama

1. `CreateUserRequest`: Kullanıcı oluşturma isteği için veri transfer nesnesi.
2. `@NotBlank`: Alanın boş olamayacağını belirtir.
3. `@Size(min = 11, max = 11)`: Alanın uzunluğunu belirtir.

### Mapper Sınıfları

**ProductMapper**

```java @Mapper public interface ProductMapper {    
 ProductMapper INSTANCE = Mappers.getMapper(ProductMapper.class);    
 @Mapping(source = "stock", target = "unitsInStock") @Mapping(source = "categoryId", target = "category.id") Product productFromCreateDto(CreateProductDto dto);    
ListProductDto productDtoFromProduct(Product product); List<ListProductDto> productDtoListFromProductList(List<Product> products);}   
```   
#### ProductMapper Açıklama

1. `@Mapper`: MapStruct tarafından nesne dönüştürme işlemleri için kullanılır.
2. `@Mapping`: Alanları eşleştirmek için kullanılır.
3. `ProductMapper.INSTANCE`: MapStruct'ın mapper örneği.

**UserMapper**

```java @Mapper(componentModel = "spring", unmappedTargetPolicy = ReportingPolicy.IGNORE) public abstract class UserMapper {    
 @Autowired protected PasswordEncoder passwordEncoder;    
 @Mapping(target = "password", source = "password", qualifiedByName = "hashPassword") public abstract User userFromCreateRequest(CreateUserRequest request);    
@Named("hashPassword") protected String hashPassword(String password) { return passwordEncoder.encode(password); }}   
```   
#### UserMapper Açıklama

1. `componentModel = "spring"`: MapStruct bean'inin Spring konteyner tarafından yönetilmesini sağlar.
2. `qualifiedByName`: Özel bir metot ile alanın dönüştürülmesini sağlar.
3. `@Named("hashPassword")`: `hashPassword` metodunun özel olarak tanımlanmasını sağlar.

### Core (Çekirdek) Konfigürasyon ve Servisler

**RedisConfiguration**

```java @Configuration public class RedisConfiguration {    
 @Bean public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory connectionFactory) { RedisTemplate<String, Object> template = new RedisTemplate<>(); template.setConnectionFactory(connectionFactory); template.setKeySerializer(new StringRedisSerializer()); template.setValueSerializer(new GenericJackson2JsonRedisSerializer()); template.setHashKeySerializer(new StringRedisSerializer()); template.setHashValueSerializer(new GenericJackson2JsonRedisSerializer()); return template; }    
@Bean public CacheManager cacheManager(RedisConnectionFactory redisConnectionFactory) { RedisCacheConfiguration configuration = RedisCacheConfiguration .defaultCacheConfig() .entryTtl(Duration.ofMinutes(30)); return RedisCacheManager.builder(redisConnectionFactory).cacheDefaults(configuration).build(); }}   
```   
#### RedisConfiguration Açıklama

1. `@Configuration`: Bu sınıfın bir konfigürasyon sınıfı olduğunu belirtir.
2. `@Bean`: Bir bean tanımlandığını belirtir.
3. `RedisTemplate`: Redis ile veri alışverişini sağlayan yapı.
4. `CacheManager`: Ön bellek yönetimi için kullanılır.

#### Detay

**SecurityConfig**

```java @Configuration public class SecurityConfig {    
 @Bean public PasswordEncoder passwordEncoder() { return new BCryptPasswordEncoder(); }    
@Bean public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception { http .csrf(AbstractHttpConfigurer::disable) .httpBasic(AbstractHttpConfigurer::disable) .authorizeHttpRequests(req -> req.anyRequest().permitAll()); return http.build(); }}   
```   
#### SecurityConfig Açıklama

1. `@Configuration`: Bu sınıfın bir konfigürasyon sınıfı olduğunu belirtir.
2. `@Bean`: Bir bean tanımlandığını belirtir.
3. `PasswordEncoder`: Şifrelerin hashlenmesi için kullanılır.
4. `SecurityFilterChain`: Uygulamanın güvenlik ayarlarını yapılandırır.


**GlobalExceptionHandler**
```java @RestControllerAdvice public class GlobalExceptionHandler {    
 @ExceptionHandler({ MethodArgumentNotValidException.class }) @ResponseStatus(HttpStatus.BAD_REQUEST) public Map<String, String> handleValidationException(MethodArgumentNotValidException exception) { Map<String, String> errors = new HashMap<>(); for (FieldError error : exception.getBindingResult().getFieldErrors()) { errors.put(error.getField(), error.getDefaultMessage()); } return errors; }    
 @ExceptionHandler({ BusinessException.class }) @ResponseStatus(HttpStatus.BAD_REQUEST) public BusinessExceptionResponse handleBusinessException(BusinessException exception) { return new BusinessExceptionResponse(exception.getMessage()); }    
@ExceptionHandler({ RuntimeException.class }) @ResponseStatus(HttpStatus.INTERNAL_SERVER_ERROR) public String handleRuntimeException() { return "Bilinmedik hata"; }}   
```   

#### GlobalExceptionHandler Açıklama

1. `@RestControllerAdvice`: Uygulama genelinde istisnaları yakalayıp işlemek için kullanılır.
2. `@ExceptionHandler`: Belirli istisnaların işlenmesini sağlar.
3. `handleValidationException`: Geçersiz giriş hatalarını yakalayıp yanıt döner.
4. `handleBusinessException`: Özel iş istisnalarını yakalar ve yanıt döner.
5. `handleRuntimeException`: Genel çalışma zamanı hatalarını yakalar ve yanıt döner.

**BusinessException ve BusinessExceptionResponse**

```java public class BusinessException extends RuntimeException {    
 public BusinessException(String message) { super(message); }}    
 @Getter @Setter @NoArgsConstructor @AllArgsConstructor public class BusinessExceptionResponse {    
private String message;}   
```   
#### BusinessException ve BusinessExceptionResponse Açıklama

1. `BusinessException`: Özel iş istisnalarını tanımlar.
2. `BusinessExceptionResponse`: İş istisnalarına yönelik yanıt nesnesidir.

**JwtService**

```java @Service public class JwtService {    
 @Value("${jwt.expiration}") private Long EXPIRATION;    
 @Value("${jwt.secret_key}") private String SECRET_KEY;    
 public String generateToken(String username) { return Jwts.builder() .issuedAt(new Date(System.currentTimeMillis())) .expiration(new Date(System.currentTimeMillis() + EXPIRATION)) .subject(username) .signWith(getSignKey()) .compact(); }    
private Key getSignKey() { byte[] keyBytes = Decoders.BASE64.decode(SECRET_KEY); return Keys.hmacShaKeyFor(keyBytes); }}   
```   
#### JwtService Açıklama

1. `@Service`: Bu sınıfın bir servis bileşeni olduğunu belirtir.
2. `@Value`: Konfigürasyon dosyasından değerleri okur.
3. `generateToken`: Kullanıcı adı ile bir JWT oluşturur.
4. `getSignKey`: JWT imzalarken kullanılacak anahtarı döner.

### 3. İlişkiler

- **User ve UserRepository**: `User` entity sınıfı, `UserRepository` aracılığıyla veritabanı işlemlerini gerçekleştirir.
- **Product ve ProductRepository**: `Product` entity sınıfı, `ProductRepository` aracılığıyla veritabanı işlemlerini gerçekleştirir.
- **Category ve Product**: `Category` entity sınıfı, birden fazla ürüne sahip olabilir (`OneToMany`), her ürün bir kategoriye aittir (`ManyToOne`).
- **UserService ve UserServiceImpl**: Kullanıcı işlemlerini yönetir.
- **ProductService ve ProductServiceImpl**: Ürün işlemlerini yönetir.
- **UserMapper ve UserServiceImpl**: `CreateUserRequest` nesnesini `User` nesnesine dönüştürmek için kullanılır.
- **ProductMapper ve ProductServiceImpl**: Ürün DTO'larını ve entity'lerini dönüştürmek için kullanılır.

### 4. Yapılar

#### Redis

Redis, hızlı veri erişimi ve önbellekleme amacıyla kullanılır. `RedisConfiguration` sınıfı, RedisTemplate ve CacheManager bean'lerini tanımlar.

#### JWT

JWT (JSON Web Token), kullanıcıların kimlik doğrulaması için kullanılır. `JwtService` sınıfı, token oluşturma ve imzalama işlemlerini gerçekleştirir.

#### Exception Handler

`GlobalExceptionHandler` sınıfı, uygulama genelinde oluşan istisnaları yakalayıp işlemek için kullanılır. Özel iş kuralları hataları için `BusinessException` sınıfı tanımlanmıştır.

#### Validation

DTO sınıflarında kullanılan `@NotBlank`, `@NotNull`, `@PositiveOrZero`, `@Size` gibi doğrulama anotasyonları, alanların doğrulanmasını sağlar.

#### Annotations

- **@Entity, @Table, @Id, @GeneratedValue, @Column**: JPA entity sınıfları için kullanılır.
- **@Getter, @Setter, @AllArgsConstructor, @NoArgsConstructor**: Lombok kütüphanesi ile otomatik metod oluşturma.
- **@Mapper, @Mapping**: MapStruct ile nesne dönüştürme işlemleri.
- **@Service, @Configuration, @RestControllerAdvice, @Bean**: Spring bileşenleri ve konfigürasyonları.
- **@ExceptionHandler**: Özel istisna işleyicileri.

#### MapStruct

MapStruct, DTO ve entity sınıfları arasında dönüştürme işlemlerini kolaylaştırır. `ProductMapper` ve `UserMapper` sınıfları bu amaçla kullanılır.

### Sonuç

Proje, kullanıcı ve ürün yönetimi işlemlerini Spring Boot ve çeşitli kütüphaneler kullanarak gerçekleştirmektedir. Projenin genel akışını, sınıflar arası ilişkileri ve kullanılan yapıların işlevlerini detaylı bir şekilde açıklamış olduk. Eğer daha spesifik bir sorunuz veya anlamadığınız bir kısım varsa, lütfen belirtin.
    
---   
## Lombok

Lombok, Java uygulamalarında boilerplate (tekrarlayan) kodları azaltmak için kullanılan bir kütüphanedir. Lombok, sınıf tanımlarına anotasyonlar ekleyerek getter ve setter metodları, `toString()`, `equals()`, `hashCode()`, yapıcı metodlar gibi yaygın olarak kullanılan kodları otomatik olarak oluşturur.

### Lombok Anotasyonları

- **@Getter ve @Setter**: Alanlar için getter ve setter metodlarını oluşturur.

```java
import lombok.Getter;
import lombok.Setter;

public class Person {
    @Getter @Setter private String name;
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

Request-Response yapısı, web uygulamalarında istemci ve sunucu arasındaki iletişimi yönetir. Spring, bu süreçleri kolaylaştırır ve esnek bir yapı sunar.

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
        return new ResponseEntity<>("An error occurred: " + ex.getMessage(),
            HttpStatus.INTERNAL_SERVER_ERROR);
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
        return new ResponseEntity<>("Custom error: " + ex.getMessage(),
            HttpStatus.BAD_REQUEST);
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