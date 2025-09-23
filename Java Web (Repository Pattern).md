An app needs to communicate with a database most of the time, it happens through **queries (instructions)** that are sent by the app. Those instructions are **CRUD (Create, Read, Update, Delete)**

### Direct SQL Queries (Old way):
Older app devs had to communicate via database by writing SQL queries as strings
**Drawback:**
- Lot of repetition
- Error-prone
- Business logic, database logic were tightly coupled making code harder to maintain

### Repository Pattern (Modern Way):
Use many tools to make communicating with the database easier

**ORM (Object-Relational Mapping)**: Allows to work with objects in code instead of writing raw SQL queries. **IT A CONCEPT NOT A TOOL**
- Example: Instead of writing `SELECT * FROM students` you can call `student_repo.find_all();`

**JPA (Jakarta Persistence API)**: A specification and standard that defines the rules for ORM in java

**Hibernate**: Most popular implementation of **JPA**. Responsible for **mapping (converting)** Java **classes (entities)** to **database tables**.
- Java objects to db rows
- Java class properties to columns

**Spring Data**: Big project that makes working with databases easier in Spring apps. It provides a unified approach to working with many different types of data sources.

**Spring Data JPA**: Subproject of Spring Data, relational db using JPA. It helps to build repositories (data access layers) quickly and easily

##### A repository
- It acts as a translator between the app and the database
- Hides SQL and db-specific details behind method calls
- Decouple business logic from data access

Example of JPA:
```java
public interface CarRepository extends JpaRepository<Car, Long> {
	List<Car> findById (Long id);
}

@GetMapping("/{car_id}")
public Car get_car_by_id (@PathVariable Long car_id) {
	return car_repository.findById(car_id);
}
```

**Benefits**:
- Provides a layer of abstraction
- Centralizes data access logic
- Provides flexible architecture
- Saves time

**Entity**: 
- Represent a real-world object/concept that needs to be stored in the database
- Each instance represent a row
- Each field is a column

#### Mappings

`@Entity`: Defines a class as an entity
`@Id`: Marks the primary key
`@GeneratedValue(strategy = GenerationType.)`: How to generate the primary key (AUTO, IDENTITY, SEQUENCE, TABLE)
`@Column(name = "")`: Maps a field to a db column
`@Table(name = "")`: Specifies the db table which the entity is mapped


```java
@Entity
@Table(name = "cars")
public class Car {
	@Id
	@GeneratedValue(strategy = GenerationType.AUTO)
	private Long id;
	
	@Column(name = "car_brand")
	private String brand;
}
```


### Types of repos
**Generic**:
- Defines common CRUD operations in a single reusable class or interface
- Saves time
```java
public interface CarRepository extends JpaRepository<Car, Long> {
	List<Car> findById (Long id);
}
```

**Non-Generic**: 
- Defines operations for a specific entity in its own repository interface/class
- Flexibility

#### Defining custom queries
`@Query("")`: Explicit query definition (raw sql)
- `@Param`: params that the sql needs 

```java
public interface CarRepository extends JpaRepository<Car, Long> {
	@Query("SELECT e FROM Car e WHERE e.id = :id")
	List<Car> findById (@Param("id") Long id);
}
```

#### H2 vs Traditional db
H2:
- Lightweight
- In-memory
- For testing
Other (MySQL, Postgres, Mongo):
- Need to be hosted
- More complex
- More scalable