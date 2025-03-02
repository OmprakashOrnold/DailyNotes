Below is a list of **100 Spring Data JPA-related questions and answers** with code examples, starting from simple concepts and gradually increasing in complexity. The questions cover setting up a project, defining entities, working with repositories, querying data, and advanced topics like pagination, auditing, and performance optimization. Each question is answered in simple terms with a practical code example.

---

### **1. Setting Up a Spring Data JPA Project**

#### **Q1: What do you need to add to a Spring Boot project to use Spring Data JPA?**
**Answer**: You need to add the Spring Data JPA starter dependency in your `pom.xml` file. For testing, you can also add an in-memory database like H2.

**Code Example**:
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>
```

#### **Q2: How do you set up a database connection in Spring Boot?**
**Answer**: You configure the database connection in the `application.properties` file with details like URL, username, and password.

**Code Example**:
```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
```

#### **Q3: What does the `spring-boot-starter-data-jpa` dependency do?**
**Answer**: It includes Spring Data JPA, Hibernate (a JPA provider), and other libraries to simplify database operations in a Spring Boot app.

**Code Example**: (Already included in Q1’s `pom.xml`)

#### **Q4: How do you enable JPA repositories in a Spring Boot app?**
**Answer**: Add `@EnableJpaRepositories` to a configuration class, though Spring Boot auto-configures this if you use the starter dependency.

**Code Example**:
```java
import org.springframework.context.annotation.Configuration;
import org.springframework.data.jpa.repository.config.EnableJpaRepositories;

@Configuration
@EnableJpaRepositories(basePackages = "com.example.repository")
public class JpaConfig {
}
```

#### **Q5: What is an in-memory database, and why use it with Spring Data JPA?**
**Answer**: An in-memory database (like H2) stores data in memory instead of disk. It’s great for testing because it’s fast and resets after the app stops.

**Code Example**: (See Q2 for H2 configuration)

---

### **2. Defining Entities**

#### **Q6: How do you create a basic entity in Spring Data JPA?**
**Answer**: Use the `@Entity` annotation on a class and `@Id` for the primary key.

**Code Example**:
```java
import javax.persistence.Entity;
import javax.persistence.Id;

@Entity
public class User {
    @Id
    private Long id;
    private String name;

    // Getters and setters
}
```

#### **Q7: What does the `@Id` annotation do?**
**Answer**: It marks a field as the primary key of an entity.

**Code Example**: (See Q6)

#### **Q8: How do you auto-generate an ID for an entity?**
**Answer**: Use `@GeneratedValue` with a strategy like `IDENTITY` to let the database auto-increment the ID.

**Code Example**:
```java
import javax.persistence.Entity;
import javax.persistence.Id;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;

@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;

    // Getters and setters
}
```

#### **Q9: What is the `@Column` annotation used for?**
**Answer**: It customizes the column name or properties (like length) in the database table.

**Code Example**:
```java
@Entity
public class User {
    @Id
    private Long id;

    @Column(name = "full_name", length = 100)
    private String name;

    // Getters and setters
}
```

#### **Q10: How do you define a OneToOne relationship between entities?**
**Answer**: Use the `@OneToOne` annotation to link two entities where one instance relates to exactly one instance of another.

**Code Example**:
```java
@Entity
public class User {
    @Id
    private Long id;
    private String name;

    @OneToOne
    private Profile profile;

    // Getters and setters
}

@Entity
public class Profile {
    @Id
    private Long id;
    private String bio;

    // Getters and setters
}
```

#### **Q11: How do you define a ManyToOne relationship?**
**Answer**: Use `@ManyToOne` when many instances of one entity relate to one instance of another (e.g., many employees in one department).

**Code Example**:
```java
@Entity
public class Employee {
    @Id
    private Long id;
    private String name;

    @ManyToOne
    private Department department;

    // Getters and setters
}

@Entity
public class Department {
    @Id
    private Long id;
    private String name;

    // Getters and setters
}
```

#### **Q12: How do you define a OneToMany relationship?**
**Answer**: Use `@OneToMany` when one entity instance relates to many instances of another (e.g., one department has many employees).

**Code Example**:
```java
@Entity
public class Department {
    @Id
    private Long id;
    private String name;

    @OneToMany(mappedBy = "department")
    private List<Employee> employees;

    // Getters and setters
}

@Entity
public class Employee {
    @Id
    private Long id;
    private String name;

    @ManyToOne
    private Department department;

    // Getters and setters
}
```

#### **Q13: How do you define a ManyToMany relationship?**
**Answer**: Use `@ManyToMany` when multiple instances of one entity relate to multiple instances of another, with a join table.

**Code Example**:
```java
@Entity
public class User {
    @Id
    private Long id;
    private String name;

    @ManyToMany
    @JoinTable(name = "user_roles",
               joinColumns = @JoinColumn(name = "user_id"),
               inverseJoinColumns = @JoinColumn(name = "role_id"))
    private Set<Role> roles;

    // Getters and setters
}

@Entity
public class Role {
    @Id
    private Long id;
    private String name;

    // Getters and setters
}
```

#### **Q14: What is the `mappedBy` attribute in relationships?**
**Answer**: It specifies the owning side of a bidirectional relationship, avoiding duplicate columns in the database.

**Code Example**: (See Q12)

#### **Q15: How do you make a field optional in an entity?**
**Answer**: Use `nullable = false` in `@Column` to make a field required, or leave it out (default is nullable).

**Code Example**:
```java
@Entity
public class User {
    @Id
    private Long id;

    @Column(nullable = false)
    private String name;

    // Getters and setters
}
```

---

### **3. Repositories**

#### **Q16: How do you create a repository for an entity?**
**Answer**: Create an interface that extends `JpaRepository` with the entity type and ID type.

**Code Example**:
```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {
}
```

#### **Q17: What basic operations does `JpaRepository` provide?**
**Answer**: It gives you methods like `save`, `findById`, `findAll`, and `deleteById` for free.

**Code Example**:
```java
User user = new User();
user.setName("John");
userRepository.save(user); // Save
Optional<User> found = userRepository.findById(1L); // Find
userRepository.deleteById(1L); // Delete
```

#### **Q18: How do you find an entity by a specific field?**
**Answer**: Define a method in the repository with a naming convention like `findByFieldName`.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByName(String name);
}
```

#### **Q19: How do you find entities with multiple conditions?**
**Answer**: Use `And` or `Or` in the method name to combine conditions.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByNameAndEmail(String name, String email);
}
```

#### **Q20: How do you count entities in a repository?**
**Answer**: Use a method like `countByFieldName` or just `count()`.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    long countByName(String name);
}
```

#### **Q21: How do you delete entities by a field?**
**Answer**: Define a `deleteByFieldName` method in the repository.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    void deleteByName(String name);
}
```

#### **Q22: What is a derived query in Spring Data JPA?**
**Answer**: It’s a query automatically created from a method name, like `findByName`.

**Code Example**: (See Q18)

#### **Q23: How do you use `@Query` to write a custom query?**
**Answer**: Use the `@Query` annotation with JPQL (Java Persistence Query Language) to define a custom query.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    @Query("SELECT u FROM User u WHERE u.name = ?1")
    List<User> findUsersByName(String name);
}
```

#### **Q24: How do you write a native SQL query?**
**Answer**: Use `@Query` with `nativeQuery = true` and write regular SQL.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    @Query(value = "SELECT * FROM user WHERE name = ?1", nativeQuery = true)
    List<User> findUsersByNameNative(String name);
}
```

#### **Q25: What does the `@Param` annotation do in queries?**
**Answer**: It lets you name parameters in a query instead of using `?1`, `?2`, etc.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    @Query("SELECT u FROM User u WHERE u.name = :userName")
    List<User> findUsersByName(@Param("userName") String name);
}
```

---

### **4. Querying Data**

#### **Q26: What is JPQL in Spring Data JPA?**
**Answer**: JPQL is a query language similar to SQL but works with entities and their fields, not database tables.

**Code Example**: (See Q23)

#### **Q27: How do you find the first entity matching a condition?**
**Answer**: Use `findFirstBy` or `findTopBy` in the method name.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    User findFirstByName(String name);
}
```

#### **Q28: How do you limit query results?**
**Answer**: Use `Top` or `First` followed by a number in the method name.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findTop5ByName(String name);
}
```

#### **Q29: How do you use `LIKE` in a query method?**
**Answer**: Add `Like` to the method name to match patterns.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByNameLike(String pattern);
}
```

#### **Q30: How do you ignore case in a query?**
**Answer**: Add `IgnoreCase` to the method name.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByNameIgnoreCase(String name);
}
```

#### **Q31: How do you order query results?**
**Answer**: Add `OrderBy` with the field name and `Asc` or `Desc`.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByNameOrderByIdAsc(String name);
}
```

#### **Q32: How do you query with `IS NULL`?**
**Answer**: Use `IsNull` in the method name.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByEmailIsNull();
}
```

#### **Q33: How do you query with `NOT NULL`?**
**Answer**: Use `IsNotNull` in the method name.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByEmailIsNotNull();
}
```

#### **Q34: How do you use `IN` in a query method?**
**Answer**: Use `In` in the method name with a list parameter.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByNameIn(List<String> names);
}
```

#### **Q35: How do you combine multiple conditions with `@Query`?**
**Answer**: Use `AND` or `OR` in the JPQL query.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    @Query("SELECT u FROM User u WHERE u.name = ?1 AND u.email = ?2")
    User findByNameAndEmail(String name, String email);
}
```

---

### **5. Advanced Topics**

#### **Q36: How do you paginate query results?**
**Answer**: Use `Pageable` as a parameter and return a `Page` object.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    Page<User> findByName(String name, Pageable pageable);
}

// Usage
Page<User> users = userRepository.findByName("John", PageRequest.of(0, 10));
```

#### **Q37: How do you sort query results with pagination?**
**Answer**: Pass a `Sort` object to `PageRequest`.

**Code Example**:
```java
Page<User> users = userRepository.findAll(PageRequest.of(0, 10, Sort.by("name").ascending()));
```

#### **Q38: What is a `Slice` in Spring Data JPA?**
**Answer**: A `Slice` is like a `Page` but doesn’t include the total count of pages, making it faster for large datasets.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    Slice<User> findByName(String name, Pageable pageable);
}
```

#### **Q39: How do you enable auditing in Spring Data JPA?**
**Answer**: Use `@EnableJpaAuditing` and add auditing annotations like `@CreatedDate` to your entity.

**Code Example**:
```java
@Configuration
@EnableJpaAuditing
public class JpaConfig {
}

@Entity
public class User {
    @Id
    private Long id;
    private String name;

    @CreatedDate
    private LocalDateTime createdDate;

    // Getters and setters
}
```

#### **Q40: How do you track who modified an entity?**
**Answer**: Add `@CreatedBy` or `@LastModifiedBy` and provide an `AuditorAware` implementation.

**Code Example**:
```java
@Entity
public class User {
    @Id
    private Long id;

    @CreatedBy
    private String createdBy;

    @LastModifiedBy
    private String lastModifiedBy;

    // Getters and setters
}

@Component
public class AuditorAwareImpl implements AuditorAware<String> {
    @Override
    public Optional<String> getCurrentAuditor() {
        return Optional.of("admin"); // Replace with real user logic
    }
}
```

#### **Q41: What is a transaction in Spring Data JPA?**
**Answer**: A transaction groups database operations so they either all succeed or all fail.

**Code Example**:
```java
@Service
public class UserService {
    @Autowired
    private UserRepository userRepository;

    @Transactional
    public void updateUser(Long id, String name) {
        User user = userRepository.findById(id).orElseThrow();
        user.setName(name);
        userRepository.save(user);
    }
}
```

#### **Q42: How do you make a transaction read-only?**
**Answer**: Use `@Transactional(readOnly = true)` for queries that don’t modify data.

**Code Example**:
```java
@Transactional(readOnly = true)
public List<User> getAllUsers() {
    return userRepository.findAll();
}
```

#### **Q43: What is optimistic locking in Spring Data JPA?**
**Answer**: It uses a `@Version` field to detect conflicts when multiple users update the same entity.

**Code Example**:
```java
@Entity
public class User {
    @Id
    private Long id;
    private String name;

    @Version
    private Integer version;

    // Getters and setters
}
```

#### **Q44: How do you use pessimistic locking?**
**Answer**: Use `@Lock` with a lock mode like `PESSIMISTIC_WRITE` in a query.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    @Lock(LockModeType.PESSIMISTIC_WRITE)
    @Query("SELECT u FROM User u WHERE u.id = ?1")
    User findByIdForUpdate(Long id);
}
```

#### **Q45: What are projections in Spring Data JPA?**
**Answer**: Projections let you fetch only specific fields instead of the whole entity.

**Code Example**:
```java
public interface UserProjection {
    String getName();
    String getEmail();
}

public interface UserRepository extends JpaRepository<User, Long> {
    UserProjection findById(Long id);
}
```

#### **Q46: How do you use DTOs instead of entities?**
**Answer**: Use a constructor expression in `@Query` to map results to a DTO.

**Code Example**:
```java
public class UserDTO {
    private String name;
    private String email;

    public UserDTO(String name, String email) {
        this.name = name;
        this.email = email;
    }

    // Getters
}

public interface UserRepository extends JpaRepository<User, Long> {
    @Query("SELECT new com.example.UserDTO(u.name, u.email) FROM User u WHERE u.id = ?1")
    UserDTO findUserDTOById(Long id);
}
```

#### **Q47: What are Specifications in Spring Data JPA?**
**Answer**: Specifications let you build dynamic queries based on conditions.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long>, JpaSpecificationExecutor<User> {
}

public class UserSpecifications {
    public static Specification<User> hasName(String name) {
        return (root, query, cb) -> cb.equal(root.get("name"), name);
    }
}

// Usage
List<User> users = userRepository.findAll(UserSpecifications.hasName("John"));
```

#### **Q48: How do you combine multiple Specifications?**
**Answer**: Use `and()` or `or()` to chain Specifications.

**Code Example**:
```java
List<User> users = userRepository.findAll(
    Specification.where(UserSpecifications.hasName("John"))
                 .and(UserSpecifications.hasEmail("john@example.com"))
);
```

#### **Q49: What is an Entity Graph?**
**Answer**: An Entity Graph tells JPA which related data to fetch eagerly.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    @EntityGraph(attributePaths = {"roles"})
    User findById(Long id);
}
```

#### **Q50: How do you use `FETCH` in a JPQL query?**
**Answer**: Use `JOIN FETCH` to eagerly load related data.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    @Query("SELECT u FROM User u JOIN FETCH u.roles WHERE u.id = ?1")
    User findUserWithRoles(Long id);
}
```

---

### **6. Best Practices and Performance**

#### **Q51: What is the N+1 query problem?**
**Answer**: It happens when JPA runs one query for an entity and then N more queries for its related data.

**Code Example**: (See Q50 for a solution with `JOIN FETCH`)

#### **Q52: How do you enable lazy loading?**
**Answer**: Use `fetch = FetchType.LAZY` on relationships (it’s the default for `@OneToMany` and `@ManyToMany`).

**Code Example**:
```java
@OneToMany(fetch = FetchType.LAZY)
private List<Employee> employees;
```

#### **Q53: How do you enable eager loading?**
**Answer**: Use `fetch = FetchType.EAGER` on relationships.

**Code Example**:
```java
@ManyToOne(fetch = FetchType.EAGER)
private Department department;
```

#### **Q54: How do you enable caching in Spring Data JPA?**
**Answer**: Use `@EnableCaching` and `@Cacheable` on repository methods.

**Code Example**:
```java
@Configuration
@EnableCaching
public class CacheConfig {
}

public interface UserRepository extends JpaRepository<User, Long> {
    @Cacheable("users")
    User findById(Long id);
}
```

#### **Q55: How do you evict cache entries?**
**Answer**: Use `@CacheEvict` to remove items from the cache.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    @CacheEvict(value = "users", key = "#user.id")
    User save(User user);
}
```

#### **Q56: How do you check SQL queries generated by JPA?**
**Answer**: Set `spring.jpa.show-sql=true` in `application.properties`.

**Code Example**:
```properties
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
```

#### **Q57: How do you use batch inserts?**
**Answer**: Set `spring.jpa.properties.hibernate.jdbc.batch_size` in properties.

**Code Example**:
```properties
spring.jpa.properties.hibernate.jdbc.batch_size=50
```

#### **Q58: How do you handle large datasets efficiently?**
**Answer**: Use `Stream` or `Slice` instead of fetching all at once.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    Stream<User> findAllByName(String name);
}
```

#### **Q59: How do you prevent SQL injection in Spring Data JPA?**
**Answer**: Use parameterized queries (default in JPQL and derived queries).

**Code Example**: (See Q23)

#### **Q60: How do you use indexes to improve performance?**
**Answer**: Add `@Index` to your entity fields.

**Code Example**:
```java
@Entity
@Table(indexes = @Index(name = "idx_name", columnList = "name"))
public class User {
    @Id
    private Long id;
    private String name;

    // Getters and setters
}
```

#### **Q61: How do you handle soft deletes?**
**Answer**: Add a `deleted` flag and filter with `@Where`.

**Code Example**:
```java
@Entity
@Where(clause = "deleted = false")
public class User {
    @Id
    private Long id;
    private String name;
    private boolean deleted;

    // Getters and setters
}
```

#### **Q62: How do you update an entity without loading it?**
**Answer**: Use a modifying `@Query` with `@Modifying`.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    @Modifying
    @Query("UPDATE User u SET u.name = ?2 WHERE u.id = ?1")
    int updateName(Long id, String name);
}
```

#### **Q63: How do you bulk delete entities?**
**Answer**: Use `@Modifying` with a delete query.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    @Modifying
    @Query("DELETE FROM User u WHERE u.name = ?1")
    int deleteByName(String name);
}
```

#### **Q64: What is the `@EntityListeners` annotation?**
**Answer**: It lets you define callback listeners for entity lifecycle events.

**Code Example**:
```java
@Entity
@EntityListeners(AuditingEntityListener.class)
public class User {
    @Id
    private Long id;
    private String name;

    // Getters and setters
}
```

#### **Q65: How do you validate entity data?**
**Answer**: Use Bean Validation annotations like `@NotNull`.

**Code Example**:
```java
@Entity
public class User {
    @Id
    private Long id;

    @NotNull
    private String name;

    // Getters and setters
}
```

#### **Q66: How do you handle database migrations with JPA?**
**Answer**: Use Flyway or Liquibase with Spring Boot (not directly a JPA feature).

**Code Example**:
```xml
<dependency>
    <groupId>org.flywaydb</groupId>
    <artifactId>flyway-core</artifactId>
</dependency>
```

#### **Q67: How do you map an enum in an entity?**
**Answer**: Use `@Enumerated` with `EnumType.STRING` or `ORDINAL`.

**Code Example**:
```java
@Entity
public class User {
    @Id
    private Long id;

    @Enumerated(EnumType.STRING)
    private Status status;

    // Getters and setters
}

public enum Status {
    ACTIVE, INACTIVE
}
```

#### **Q68: How do you map a date field?**
**Answer**: Use `@Temporal` (JPA 1) or Java 8 time API (like `LocalDateTime`).

**Code Example**:
```java
@Entity
public class User {
    @Id
    private Long id;

    private LocalDateTime createdAt;

    // Getters and setters
}
```

#### **Q69: How do you handle composite keys?**
**Answer**: Use `@Embeddable` and `@EmbeddedId`.

**Code Example**:
```java
@Embeddable
public class UserKey implements Serializable {
    private String username;
    private String email;

    // Getters, setters, equals, hashCode
}

@Entity
public class User {
    @EmbeddedId
    private UserKey id;
    private String name;

    // Getters and setters
}
```

#### **Q70: How do you map inheritance in JPA?**
**Answer**: Use `@Inheritance` with a strategy like `TABLE_PER_CLASS`.

**Code Example**:
```java
@Entity
@Inheritance(strategy = InheritanceType.TABLE_PER_CLASS)
public abstract class Person {
    @Id
    private Long id;
    private String name;

    // Getters and setters
}

@Entity
public class Employee extends Person {
    private String department;

    // Getters and setters
}
```

---

### **7. Miscellaneous**

#### **Q71: What is the difference between `CrudRepository` and `JpaRepository`?**
**Answer**: `JpaRepository` extends `CrudRepository` and adds JPA-specific methods like `flush()` and `deleteAllInBatch()`.

**Code Example**:
```java
public interface UserRepository extends CrudRepository<User, Long> {
}
```

#### **Q72: How do you use `existsBy` in a repository?**
**Answer**: Use `existsByFieldName` to check if an entity exists.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    boolean existsByName(String name);
}
```

#### **Q73: How do you handle unique constraints?**
**Answer**: Use `@Column(unique = true)`.

**Code Example**:
```java
@Entity
public class User {
    @Id
    private Long id;

    @Column(unique = true)
    private String email;

    // Getters and setters
}
```

#### **Q74: How do you map a collection of basic types?**
**Answer**: Use `@ElementCollection`.

**Code Example**:
```java
@Entity
public class User {
    @Id
    private Long id;

    @ElementCollection
    private List<String> hobbies;

    // Getters and setters
}
```

#### **Q75: How do you use `@PostLoad` in an entity?**
**Answer**: Add a method with `@PostLoad` to run logic after an entity is loaded.

**Code Example**:
```java
@Entity
public class User {
    @Id
    private Long id;
    private String name;

    @PostLoad
    public void onLoad() {
        System.out.println("User loaded: " + name);
    }
}
```

#### **Q76: How do you disable automatic schema generation?**
**Answer**: Set `spring.jpa.hibernate.ddl-auto=none`.

**Code Example**:
```properties
spring.jpa.hibernate.ddl-auto=none
```

#### **Q77: How do you use a custom ID generator?**
**Answer**: Implement `IdentifierGenerator` and use `@GenericGenerator`.

**Code Example**:
```java
@Entity
public class User {
    @Id
    @GenericGenerator(name = "customGen", strategy = "com.example.CustomIdGenerator")
    @GeneratedValue(generator = "customGen")
    private String id;

    // Getters and setters
}
```

#### **Q78: How do you handle exceptions in Spring Data JPA?**
**Answer**: Catch exceptions like `DataIntegrityViolationException` in your service layer.

**Code Example**:
```java
try {
    userRepository.save(user);
} catch (DataIntegrityViolationException e) {
    // Handle duplicate entry or constraint violation
}
```

#### **Q79: How do you use `findBy` with nested properties?**
**Answer**: Use dot notation in the method name.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByDepartmentName(String deptName);
}
```

#### **Q80: How do you use `DISTINCT` in a query?**
**Answer**: Add `Distinct` to the method name or use it in `@Query`.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<String> findDistinctNameBy();
}
```

#### **Q81: How do you use `BETWEEN` in a query?**
**Answer**: Use `Between` in the method name.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByIdBetween(Long start, Long end);
}
```

#### **Q82: How do you use `LESS THAN` in a query?**
**Answer**: Use `LessThan` in the method name.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByIdLessThan(Long maxId);
}
```

#### **Q83: How do you use `GREATER THAN` in a query?**
**Answer**: Use `GreaterThan` in the method name.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByIdGreaterThan(Long minId);
}
```

#### **Q84: How do you use `STARTING WITH` in a query?**
**Answer**: Use `StartingWith` in the method name.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByNameStartingWith(String prefix);
}
```

#### **Q85: How do you use `ENDING WITH` in a query?**
**Answer**: Use `EndingWith` in the method name.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByNameEndingWith(String suffix);
}
```

#### **Q86: How do you use `CONTAINING` in a query?**
**Answer**: Use `Containing` in the method name.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByNameContaining(String substring);
}
```

#### **Q87: How do you use `TRUE` or `FALSE` in a query?**
**Answer**: Use `IsTrue` or `IsFalse` in the method name.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByActiveIsTrue();
}
```

#### **Q88: How do you use custom repository implementations?**
**Answer**: Create an interface and its implementation, then extend it in the main repository.

**Code Example**:
```java
public interface CustomUserRepository {
    void customMethod();
}

public class CustomUserRepositoryImpl implements CustomUserRepository {
    public void customMethod() {
        // Custom logic
    }
}

public interface UserRepository extends JpaRepository<User, Long>, CustomUserRepository {
}
```

#### **Q89: How do you use Spring Data JPA with multiple databases?**
**Answer**: Configure multiple `DataSource`s and repositories for each database.

**Code Example**:
```java
@Configuration
public class JpaConfig {
    @Bean
    @ConfigurationProperties(prefix = "spring.datasource.first")
    public DataSource firstDataSource() {
        return DataSourceBuilder.create().build();
    }

    @Bean
    public LocalContainerEntityManagerFactoryBean firstEntityManagerFactory() {
        // Configure for first database
    }
}
```

#### **Q90: How do you test a Spring Data JPA repository?**
**Answer**: Use `@DataJpaTest` and an in-memory database.

**Code Example**:
```java
@DataJpaTest
public class UserRepositoryTest {
    @Autowired
    private UserRepository userRepository;

    @Test
    public void testFindByName() {
        User user = new User();
        user.setName("John");
        userRepository.save(user);
        assertEquals(1, userRepository.findByName("John").size());
    }
}
```

#### **Q91: How do you use `Tuple` for custom queries?**
**Answer**: Return `Tuple` from a `@Query` for flexible result mapping.

**Code Example**:
```java
public interface UserRepository extends JpaRepository<User, Long> {
    @Query("SELECT u.name, u.email FROM User u WHERE u.id = ?1")
    Tuple findNameAndEmailById(Long id);
}
```

#### **Q92: How do you use `Criteria API` with Spring Data JPA?**
**Answer**: Use `CriteriaBuilder` manually (less common with Spring Data).

**Code Example**:
```java
CriteriaBuilder cb = entityManager.getCriteriaBuilder();
CriteriaQuery<User> cq = cb.createQuery(User.class);
Root<User> root = cq.from(User.class);
cq.select(root).where(cb.equal(root.get("name"), "John"));
List<User> users = entityManager.createQuery(cq).getResultList();
```

#### **Q93: How do you handle versioning of entities?**
**Answer**: Use `@Version` for optimistic locking (see Q43).

#### **Q94: How do you map a JSON column?**
**Answer**: Use `@Type` with a custom Hibernate type or a library like Jackson.

**Code Example**:
```java
@Entity
public class User {
    @Id
    private Long id;

    @Column(columnDefinition = "json")
    private String metadata;

    // Getters and setters
}
```

#### **Q95: How do you use `@NamedQuery`?**
**Answer**: Define a query on the entity with `@NamedQuery`.

**Code Example**:
```java
@Entity
@NamedQuery(name = "User.findByName", query = "SELECT u FROM User u WHERE u.name = ?1")
public class User {
    @Id
    private Long id;
    private String name;

    // Getters and setters
}
```

#### **Q96: How do you use `@NamedNativeQuery`?**
**Answer**: Define a native SQL query on the entity.

**Code Example**:
```java
@Entity
@NamedNativeQuery(name = "User.findByNameNative", query = "SELECT * FROM user WHERE name = ?1")
public class User {
    @Id
    private Long id;
    private String name;

    // Getters and setters
}
```

#### **Q97: How do you handle relationships with cascading?**
**Answer**: Use `cascade = CascadeType.ALL` to propagate operations.

**Code Example**:
```java
@Entity
public class User {
    @Id
    private Long id;

    @OneToMany(cascade = CascadeType.ALL)
    private List<Role> roles;

    // Getters and setters
}
```

#### **Q98: How do you use `@PrePersist` and `@PreUpdate`?**
**Answer**: Add methods with these annotations for pre-save logic.

**Code Example**:
```java
@Entity
public class User {
    @Id
    private Long id;
    private String name;
    private LocalDateTime updatedAt;

    @PrePersist
    public void prePersist() {
        updatedAt = LocalDateTime.now();
    }

    @PreUpdate
    public void preUpdate() {
        updatedAt = LocalDateTime.now();
    }
}
```

#### **Q99: How do you use `EntityManager` directly?**
**Answer**: Inject `EntityManager` for manual JPA operations.

**Code Example**:
```java
@Service
public class UserService {
    @PersistenceContext
    private EntityManager entityManager;

    public User findUser(Long id) {
        return entityManager.find(User.class, id);
    }
}
```

#### **Q100: How do you integrate Spring Data JPA with Spring Security?**
**Answer**: Use the authenticated user in `AuditorAware` for auditing.

**Code Example**:
```java
@Component
public class SpringSecurityAuditorAware implements AuditorAware<String> {
    @Override
    public Optional<String> getCurrentAuditor() {
        return Optional.ofNullable(SecurityContextHolder.getContext().getAuthentication())
                       .map(Authentication::getName);
    }
}
```

---

This list starts with basic setup and entity creation, moves through repository usage and querying, and ends with advanced topics like auditing, performance, and integration. Each answer is concise, and the code examples are practical and easy to follow!
