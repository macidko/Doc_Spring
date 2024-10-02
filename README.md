## İçindekiler
- [Proje İncelemesi ve Açıklamalar](#proje-incelemesi-ve-açıklamalar)
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
```java
@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
@Entity
@Table(name="users")
public class User {
  @Id
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  @Column(name="id")
  private Long id;

  @Column(name="email")
  private String email;

  @Column(name="password")
  private String password;

  @Column(name="name")
  private String name;

  @Column(name="surname")
  private String surname;

  @Column(name="identityno")
  private String identityNo;
}
```

#### Açıklamalar

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

### Product Entity

```java
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
@Entity
@Table(name="products")
public class Product {
  @Id
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  @Column(name="id")
  private int id;

  @Column(name="name")
  private String name;

  @Column(name="price")
  private BigDecimal unitPrice;

  @Column(name="stock")
  private int unitsInStock;

  @ManyToOne
  @JoinColumn(name="categoryid")
  private Category category;
}
```

#### Açıklamalar

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

```java
@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
@Table(name="categories")
@Entity
public class Category {
  @Id
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  @Column(name="id")
  private int id;

  @Column(name="name")
  private String name;

  @OneToMany(mappedBy = "category")
  private List<Product> products;
}
```

#### Açıklamalar

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

```java
public interface ProductRepository extends JpaRepository<Product, Integer> {
  List<Product> findByNameLikeIgnoreCase(String name);
  Optional<Product> findByNameIgnoreCase(String name);

  @Query(value = "Select p from Product p " +
          "inner join p.category " +
          "where p.unitPrice > :unitPrice and lower(p.name) like concat('%', lower(:name), '%')", nativeQuery=false)
  List<Product> findByNameAndUnitPriceGreaterThan(String name, BigDecimal unitPrice);

  @Query(value = "Select * from products p where p.price > :unitPrice and lower(p.name) LIKE concat('%', lower(:name), '%')", nativeQuery=true)
  List<Product> findByNameAndUnitPriceGreaterThanSql(String name, BigDecimal unitPrice);
}
```

#### Açıklamalar

1. `JpaRepository<Product, Integer>`: Bu arayüz, `Product` varlığı için CRUD işlemlerini sağlar.
2. `findByNameLikeIgnoreCase(String name)`: Ürün adını büyük/küçük harf duyarlılığı olmadan arayan metod.
3. `findByNameIgnoreCase(String name)`: Ürün adını büyük/küçük harf duyarlılığı olmadan arayan metod.
4. `@Query`: JPQL sorgusunu tanımlar, belirli bir fiyatın üzerindeki ve adı belirtilen ürünleri arar.
5. `nativeQuery=true`: Native SQL sorgusunu tanımlar, belirli bir fiyatın üzerindeki ve adı belirtilen ürünleri arar.

#### Product Repository Detay

```java
public interface ProductRepository extends JpaRepository<Product, Integer> {
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
  @Query(value = "Select p from Product p " +
          "inner join p.category " +
          "where p.unitPrice > :unitPrice and lower(p.name) like concat('%', lower(:name), '%')", nativeQuery=false)
  List<Product> findByNameAndUnitPriceGreaterThan(String name, BigDecimal unitPrice);
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
  @Query(value = "Select * from products p where p.price > :unitPrice and lower(p.name) LIKE concat('%', lower(:name), '%')", nativeQuery=true)
  List<Product> findByNameAndUnitPriceGreaterThanSql(String name, BigDecimal unitPrice);
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

```java
public interface UserRepository extends JpaRepository<User, Integer> {
  Optional<User> findByEmailIgnoreCase(String email);
}
```

#### Açıklamalar

1. `JpaRepository<User, Integer>`: Bu arayüz, `User` varlığı için CRUD işlemlerini sağlar.
2. `findByEmailIgnoreCase(String email)`: Kullanıcı e-postasını büyük/küçük harf duyarlılığı olmadan arayan metod.

#### UserRepository Detay
Tabii ki! Aşağıda `ProductRepository` arayüzündeki her bir satırı detaylı bir şekilde açıklayacağım. Bu arayüz, Spring Data JPA kullanarak `Product` nesneleri ile veritabanı işlemleri gerçekleştirmek için gereken metodları tanımlar.

### ProductRepository Arayüzü

```java
public interface ProductRepository extends JpaRepository<Product, Integer> {
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
  @Query(value = "Select p from Product p " +
          "inner join p.category " +
          "where p.unitPrice > :unitPrice and lower(p.name) like concat('%', lower(:name), '%')", nativeQuery=false)
  List<Product> findByNameAndUnitPriceGreaterThan(String name, BigDecimal unitPrice);
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
  @Query(value = "Select * from products p where p.price > :unitPrice and lower(p.name) LIKE concat('%', lower(:name), '%')", nativeQuery=true)
  List<Product> findByNameAndUnitPriceGreaterThanSql(String name, BigDecimal unitPrice);
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

### ProductService ve ProductServiceImpl

```java
public interface ProductService {
   ListProductDto getById(int id);
   List<ListProductDto> getAll();
   List<ListProductDto> getByName(String name);
   List<ListProductDto> getByNameAndUnitPrice(String name, BigDecimal unitPrice);
   void add(CreateProductDto createProductDto);
}
```

```java
@Service
@RequiredArgsConstructor
public class ProductServiceImpl implements ProductService {
  private final ProductRepository productRepository;
  private final ProductBusinessRules productBusinessRules;

  @Override
  @Cacheable(value = "product", key = "#id")
  public ListProductDto getById(int id) {
    Product product = productRepository.findById(id).orElseThrow

(() -> new BusinessException("Böyle bir ürün yok"));
    ProductMapper mapper = ProductMapper.INSTANCE;
    return mapper.productDtoFromProduct(product);
  }

  @Override
  @Cacheable(value = "products")
  public List<ListProductDto> getAll() {
    List<Product> products = productRepository.findAll();
    ProductMapper productMapper = ProductMapper.INSTANCE;
    return productMapper.productDtoListFromProductList(products);
  }

  @Override
  public List<ListProductDto> getByName(String name) {
    List<Product> products = productRepository.findByNameLikeIgnoreCase("%"+name+"%");
    ProductMapper productMapper = ProductMapper.INSTANCE;
    return productMapper.productDtoListFromProductList(products);
  }

  @Override
  public List<ListProductDto> getByNameAndUnitPrice(String name, BigDecimal unitPrice) {
    List<Product> products = productRepository.findByNameAndUnitPriceGreaterThan(name, unitPrice);
    ProductMapper productMapper = ProductMapper.INSTANCE;
    return productMapper.productDtoListFromProductList(products);
  }

  @Override
  @CacheEvict(value = "products", allEntries = true)
  public void add(CreateProductDto createProductDto) {
    productBusinessRules.productWithSameNameShouldNotExist(createProductDto.getName());
    Product product = ProductMapper.INSTANCE.productFromCreateDto(createProductDto);
    productRepository.save(product);
  }
}
```

#### Açıklamalar

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
```java
public interface ProductService {
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

#### ProductImpl Detay
```java
@Service
@RequiredArgsConstructor
public class ProductServiceImpl implements ProductService {
```

- `@Service`: Bu sınıfın bir servis bileşeni olduğunu belirtir. Spring, bu sınıfı bileşen taraması ile bulur ve yönetir.
- `@RequiredArgsConstructor`: Lombok kütüphanesi, tüm final alanlar için bir constructor oluşturur. Böylece bağımlılıkları otomatik olarak enjekte eder.
- `public class ProductServiceImpl implements ProductService`: `ProductService` arayüzünü implement eden sınıf. Bu, `ProductService` arayüzünde tanımlanan tüm metodları uygulamak zorundadır.

```java
  private final ProductRepository productRepository;
  private final ProductBusinessRules productBusinessRules;
```

- `private final ProductRepository productRepository;`: Ürün veritabanı işlemlerini gerçekleştirmek için kullanılan repository. Spring tarafından otomatik olarak enjekte edilir.
- `private final ProductBusinessRules productBusinessRules;`: Ürün ile ilgili iş kurallarını kontrol eden bir nesne. Bu, ürün eklenmeden önce belirli kuralların kontrol edilmesini sağlar.

### Metodlar

#### 1. getById

```java
  @Override
  @Cacheable(value = "product", key = "#id") // product.1, product.2
  public ListProductDto getById(int id) {
```

- `@Override`: Bu metodun bir üst sınıf veya arayüzde tanımlı olan bir metodun implementasyonu olduğunu belirtir.
- `@Cacheable(value = "product", key = "#id")`: Bu metod çağrıldığında, sonuçların Redis gibi bir önbellekte saklanmasını sağlar. `value` önbellek adını belirtir; `key` ise önbellek için anahtarı belirtir (bu durumda ürün ID'si).

```java
    Product product = productRepository.findById(id)
        .orElseThrow(() -> new BusinessException("Böyle bir ürün yok"));
```

- `productRepository.findById(id)`: Belirtilen ID'ye sahip ürünü veritabanında arar.
- `.orElseThrow(() -> new BusinessException("Böyle bir ürün yok"))`: Eğer ürün bulunamazsa, bir `BusinessException` fırlatır.

```java
    ProductMapper mapper = ProductMapper.INSTANCE;
    return mapper.productDtoFromProduct(product);
  }
```

- `ProductMapper mapper = ProductMapper.INSTANCE;`: `ProductMapper`'ın singleton örneğini alır. `ProductMapper`, MapStruct kullanarak `Product` ve `ListProductDto` arasında dönüşüm yapar.
- `return mapper.productDtoFromProduct(product);`: Bulunan `Product` nesnesini `ListProductDto` nesnesine dönüştürür ve döner.

#### 2. getAll

```java
  @Override
  @Cacheable(value = "products")
  public List<ListProductDto> getAll() {
```

- `@Cacheable(value = "products")`: Bu metod çağrıldığında, sonuçların önbelleğe alınmasını sağlar. Bu, tüm ürünlerin listelendiği metoddur.

```java
    List<Product> products = productRepository.findAll();
```

- `productRepository.findAll()`: Veritabanındaki tüm ürünleri alır.

```java
    ProductMapper productMapper = ProductMapper.INSTANCE;
    return productMapper.productDtoListFromProductList(products);
  }
```

- `ProductMapper productMapper = ProductMapper.INSTANCE;`: `ProductMapper`'ın singleton örneğini alır.
- `return productMapper.productDtoListFromProductList(products);`: Alınan ürün listesini `ListProductDto` listesine dönüştürür ve döner.

#### 3. getByName

```java
  @Override
  public List<ListProductDto> getByName(String name) {
```

- `public List<ListProductDto> getByName(String name)`: Ürün adını kullanarak ürünleri arayan bir metod.

```java
    List<Product> products = productRepository.findByNameLikeIgnoreCase("%"+name+"%");
```

- `productRepository.findByNameLikeIgnoreCase("%"+name+"%")`: Belirtilen isimle eşleşen ürünleri büyük/küçük harf duyarlılığı olmadan arar. `"%"+name+"%"` ifadesi, isimle eşleşen tüm ürünleri bulmak için kullanılan bir SQL gibi bir `LIKE` ifadesidir.

```java
    ProductMapper productMapper = ProductMapper.INSTANCE;
    return productMapper.productDtoListFromProductList(products);
  }
```

- Alınan ürün listesini `ListProductDto` listesine dönüştürür ve döner.

#### 4. getByNameAndUnitPrice

```java
  @Override
  public List<ListProductDto> getByNameAndUnitPrice(String name, BigDecimal unitPrice) {
```

- `public List<ListProductDto> getByNameAndUnitPrice(String name, BigDecimal unitPrice)`: Ürün adını ve birim fiyatını kullanarak ürünleri arayan bir metod.

```java
    List<Product> products = productRepository.findByNameAndUnitPriceGreaterThan(name, unitPrice);
```

- `productRepository.findByNameAndUnitPriceGreaterThan(name, unitPrice)`: Belirtilen isimle eşleşen ve birim fiyatı belirtilen değerden büyük olan ürünleri bulur.

```java
    ProductMapper productMapper = ProductMapper.INSTANCE;
    return productMapper.productDtoListFromProductList(products);
  }
```

- Alınan ürün listesini `ListProductDto` listesine dönüştürür ve döner.

#### 5. add

```java
  @Override
  @CacheEvict(value = "products", allEntries = true)
  public void add(CreateProductDto createProductDto) {
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
    productRepository.save(product);
  }
```

- `productRepository.save(product)`: Yeni `Product` nesnesini veritabanına kaydeder.

### Özet

- `ProductServiceImpl` sınıfı, ürünlerle ilgili iş mantığını içerir ve `ProductService` arayüzünü implement eder.
- Redis, veri önbellekleme için kullanılır; `@Cacheable` ve `@CacheEvict` anotasyonları ile önbellek yönetimi sağlanır.
- Ürün bilgileri üzerinde CRUD işlemleri gerçekleştirilir, özellikle `getById`, `getAll`, `getByName`, ve `add` metodları, veritabanındaki verileri alır veya günceller.
- `ProductMapper`, DTO'lar ve entity'ler arasında dönüştürme işlemlerini gerçekleştirir.

### UserService ve UserServiceImpl

```java
public interface UserService {
  void create(CreateUserRequest createUserRequest);
  String login(LoginRequest loginRequest);
}
```

```java
@Service
@RequiredArgsConstructor
public class UserServiceImpl implements UserService {
  private final UserRepository userRepository;
  private final PasswordEncoder passwordEncoder;
  private final UserMapper userMapper;
  private final JwtService jwtService;

  @Override
  public void create(CreateUserRequest createUserRequest) {
    User user = userMapper.userFromCreateRequest(createUserRequest);
    userRepository.save(user);
  }

  @Override
  public String login(LoginRequest loginRequest) {
    User user = userRepository
            .findByEmailIgnoreCase(loginRequest.getEmail()).orElseThrow(() -> new BusinessException("E-posta veya şifre hatalı."));

    boolean passwordMatching = passwordEncoder.matches(loginRequest.getPassword(), user.getPassword());
    if (!passwordMatching)
      throw new BusinessException("E-posta veya şifre hatalı.");

    return jwtService.generateToken(user.getEmail());
  }
}
```

#### Açıklamalar

1. `UserService`: Kullanıcılarla ilgili işlevsellikleri tanımlar.
2. `UserServiceImpl`: `UserService` arayüzünün implementasyonunu sağlar.
3. `@Service`: Bu sınıfın bir servis bileşeni olduğunu belirtir.
4. `@RequiredArgsConstructor`: Lombok tarafından tüm final alanlar için bir constructor oluşturur ve bu alanları inject eder.
5. `userRepository.findByEmailIgnoreCase(loginRequest.getEmail()).orElseThrow(() -> new BusinessException("E-posta veya şifre hatalı."))`: Belirtilen e-postaya sahip kullanıcıyı bulamazsa özel bir istisna fırlatır.
6. `passwordEncoder.matches(loginRequest.getPassword(), user.getPassword())`: Kullanıcının şifresini kontrol eder.
7. `jwtService.generateToken(user.getEmail())`: Kullanıcı için bir JWT oluşturur.

### DTO Sınıfları

**LoginRequest**

```java
@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
public class LoginRequest {
  @NotBlank
  private String email;

  @NotBlank
  private String password;
}
```

#### Açıklamalar

1. `@NotBlank`: Alanın boş olamayacağını belirtir.
2. `LoginRequest`: Giriş isteği için veri transfer nesnesi.

**CreateProductDto ve ListProductDto**

```java
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
public class CreateProductDto implements Serializable {
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

```java
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
public class ListProductDto implements Serializable {
  private int id;
  private String name;
  private BigDecimal unitPrice;
}
```

#### Açıklamalar

1. `CreateProductDto`: Ürün oluşturma isteği için veri transfer nesnesi.
2. `ListProductDto`: Ürün listeleme için veri transfer nesnesi.
3. `@NotNull`, `@NotBlank`, `@PositiveOrZero`, `@Positive`: Alanların doğrulanmasını sağlar.

**CreateUserRequest**

```java
@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
public class CreateUserRequest {
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

#### Açıklamalar

1. `CreateUserRequest`: Kullanıcı oluşturma isteği için veri transfer nesnesi.
2. `@NotBlank`: Alanın boş olamayacağını belirtir.
3. `@Size(min = 11, max = 11)`: Alanın uzunluğunu belirtir.

### Mapper Sınıfları

**ProductMapper**

```java
@Mapper
public interface ProductMapper {
  ProductMapper INSTANCE = Mappers.getMapper(ProductMapper.class);

  @Mapping(source = "stock", target = "unitsInStock")
  @Mapping(source = "categoryId", target = "category.id")
  Product productFromCreateDto(CreateProductDto dto);

  ListProductDto productDtoFromProduct(Product product);
  List<ListProductDto> productDtoListFromProductList(List<Product> products);
}
```

#### Açıklamalar

1. `@Mapper`: MapStruct tarafından nesne dönüştürme işlemleri için kullanılır.
2. `@Mapping`: Alanları eşleştirmek için kullanılır.
3. `ProductMapper.INSTANCE`: MapStruct'ın mapper örneği.

**UserMapper**

```java
@Mapper(componentModel = "spring", unmappedTargetPolicy = ReportingPolicy.IGNORE)
public abstract class UserMapper {
  @Autowired
  protected PasswordEncoder passwordEncoder;

  @Mapping(target = "password", source = "password", qualifiedByName = "hashPassword")
  public abstract User userFromCreateRequest(CreateUserRequest request);

  @Named("hashPassword")
  protected String hashPassword(String password) {
    return passwordEncoder.encode(password);
  }
}
```

#### Açıklamalar

1. `componentModel = "spring"`: MapStruct bean'inin Spring konteyner tarafından yönetilmesini sağlar.
2. `qualifiedByName`: Özel bir metot ile alanın dönüştürülmesini sağlar.
3. `@Named("hashPassword")`: `hashPassword` metodunun özel olarak tanımlanmasını sağlar.

### Core (Çekirdek) Konfigürasyon ve Servisler

**RedisConfiguration**

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

#### Açıklamalar

1. `@Configuration`: Bu sınıfın bir konfigürasyon sınıfı olduğunu belirtir.
2. `@Bean`: Bir bean tanımlandığını belirtir.
3. `RedisTemplate`: Redis ile veri alışverişini sağlayan yapı.
4. `CacheManager`: Ön bellek yönetimi için kullanılır.

#### Detay

**SecurityConfig**

```java
@Configuration
public class SecurityConfig {
  @Bean
  public PasswordEncoder passwordEncoder() {
    return new BCryptPasswordEncoder();
  }

  @Bean
  public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    http
            .csrf(AbstractHttpConfigurer::disable)
            .httpBasic(AbstractHttpConfigurer::disable)
            .authorizeHttpRequests(req -> req.anyRequest().permitAll());
    return http.build();
  }
}
```

#### Açıklamalar

1. `@Configuration`: Bu sınıfın bir konfigürasyon sınıfı olduğunu belirtir.
2. `@Bean`: Bir bean tanımlandığını belirtir.
3. `PasswordEncoder`: Şifrelerin hashlenmesi için kullanılır.
4. `SecurityFilterChain`: Uygulamanın güvenlik ayarlarını yapılandırır.


**GlobalExceptionHandler**
```java
@RestControllerAdvice
public class GlobalExceptionHandler {
  @ExceptionHandler({ MethodArgumentNotValidException.class })
  @ResponseStatus(HttpStatus.BAD_REQUEST)
  public Map<String, String> handleValidationException(MethodArgumentNotValidException exception) {
    Map<String, String> errors = new HashMap<>();
    for (FieldError error : exception.getBindingResult().getFieldErrors()) {
      errors.put(error.getField(), error.getDefaultMessage());
    }
    return errors;
  }

  @ExceptionHandler({ BusinessException.class })
  @ResponseStatus(HttpStatus.BAD_REQUEST)
  public BusinessExceptionResponse handleBusinessException(BusinessException exception) {
    return new BusinessExceptionResponse(exception.getMessage());
  }

  @ExceptionHandler({ RuntimeException.class })
  @ResponseStatus(HttpStatus.INTERNAL_SERVER_ERROR)
  public String handleRuntimeException() {
    return "Bilinmedik hata";
  }
}
```


#### Açıklamalar

1. `@RestControllerAdvice`: Uygulama genelinde istisnaları yakalayıp işlemek için kullanılır.
2. `@ExceptionHandler`: Belirli istisnaların işlenmesini sağlar.
3. `handleValidationException`: Geçersiz giriş hatalarını yakalayıp yanıt döner.
4. `handleBusinessException`: Özel iş istisnalarını yakalar ve yanıt döner.
5. `handleRuntimeException`: Genel çalışma zamanı hatalarını yakalar ve yanıt döner.

**BusinessException ve BusinessExceptionResponse**

```java
public class BusinessException extends RuntimeException {
  public BusinessException(String message) {
    super(message);
  }
}

@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
public class BusinessExceptionResponse {
  private String message;
}
```

#### Açıklamalar

1. `BusinessException`: Özel iş istisnalarını tanımlar.
2. `BusinessExceptionResponse`: İş istisnalarına yönelik yanıt nesnesidir.

**JwtService**

```java
@Service
public class JwtService {
  @Value("${jwt.expiration}")
  private Long EXPIRATION;

  @Value("${jwt.secret_key}")
  private String SECRET_KEY;

  public String generateToken(String username) {
    return Jwts.builder()
            .issuedAt(new Date(System.currentTimeMillis()))
            .expiration(new Date(System.currentTimeMillis() + EXPIRATION))
            .subject(username)
            .signWith(getSignKey())
            .compact();
  }

  private Key getSignKey() {
    byte[] keyBytes = Decoders.BASE64.decode(SECRET_KEY);
    return Keys.hmacShaKeyFor(keyBytes);
  }
}
```

#### Açıklamalar

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

