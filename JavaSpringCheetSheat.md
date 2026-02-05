
# Java + Spring Boot Cheat Sheet (Backend Focus)

### Core Java (Must-Know)

**OOP**

* Encapsulation → private fields + public methods
* Inheritance → `extends`
* Polymorphism → method overriding
* Abstraction → interfaces / abstract classes

**Immutability**

* Make class `final`
* Fields `private final`
* No setters
* Defensive copies for mutable objects

**equals & hashCode**

* If `equals()` is true → `hashCode()` must be same
* Critical for `HashMap`, `HashSet`

**Collections**

* `ArrayList` → fast reads, O(1) access
* `LinkedList` → slow traversal, extra memory
* `HashMap` → not thread-safe
* `ConcurrentHashMap` → thread-safe, high performance

**Streams**

* Use for readable transformations
* Avoid in tight performance loops
* Don’t modify collections while streaming

---

### Multithreading & Concurrency

**Thread Safety**

* Prefer immutability
* Avoid shared mutable state
* Use concurrent collections

**synchronized vs Lock**

* `synchronized` → simple, blocking
* `ReentrantLock` → tryLock, timeout, fairness

**volatile**

* Guarantees visibility
* No atomicity
* Good for flags, not counters

**Executors**

```java
ExecutorService pool = Executors.newFixedThreadPool(10);
pool.submit(task);
```

---

### JVM & Memory

**Memory Areas**

* Stack → method calls, local variables
* Heap → objects

  * Young Gen
  * Old Gen
* Metaspace → class metadata

**Garbage Collection**

* Minor GC → Young Gen
* Major GC → Old Gen (expensive)
* Reduce object creation

**Memory Leaks**

* Static collections
* Unremoved listeners
* Caches without eviction

---

### Spring Boot Core

**Why Spring Boot**

* Auto-configuration
* Embedded server
* Opinionated defaults

**Common Annotations**

```java
@SpringBootApplication
@RestController
@Service
@Repository
@Component
@Autowired
```

**Controller**

```java
@GetMapping("/users/{id}")
public User getUser(@PathVariable Long id) {}
```

**Dependency Injection**

* Constructor injection preferred
* Avoid field injection in production

---

### Spring Boot Layers (Clean Architecture)

* Controller → HTTP layer only
* Service → business logic
* Repository → DB access
* Entity → data only (no logic)

**Rule**

> Controllers thin, services fat, entities dumb

---

### JPA / Hibernate

**Entity**

```java
@Entity
class User {
  @Id
  @GeneratedValue
  Long id;
}
```

**Repositories**

```java
Optional<User> findById(Long id);
```

**Important**

* Don’t use `Optional` as entity fields
* Avoid logic in entities
* Use DTOs for APIs

**Lazy vs Eager**

* Default: LAZY
* EAGER causes performance issues

---

### Transactions

```java
@Transactional
public void transfer() {}
```

* Rollback on RuntimeException
* Avoid long-running transactions
* Don’t call transactional methods internally

---

### Exception Handling

**Global Handler**

```java
@RestControllerAdvice
class GlobalExceptionHandler {}
```

**Best Practices**

* Use unchecked exceptions
* Centralized handling
* Clean API error responses

---

### REST API Best Practices

* Use proper HTTP status codes
* DTOs for request/response
* Validation with `@Valid`
* No business logic in controllers

---

### Serialization

* REST → JSON (Jackson)
* Avoid Java serialization for microservices
* Use `serialVersionUID` if needed

---

### Performance Tips

* Prefer `ArrayList` over `LinkedList`
* Avoid `synchronized` in controllers
* Use connection pooling
* Cache wisely (Redis, Caffeine)
* Monitor GC logs

---

### Spring Boot Real-World Rules (Interview Gold)

* No DB calls in constructors
* Use `@PostConstruct` for initialization
* Avoid static state in beans
* Don’t block async threads
* Design for stateless services

---
