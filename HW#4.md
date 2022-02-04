### ANSWERS TO WEEK-4 HOMEWORK QUESTIONS

---

#### Q1 - What is JPA ?

---

The *Java Persistence API (JPA)* is a specification for persistence, which may also mean any method through which Java objects overlive their application process. All Java objects do not need to be persisted, but most applications persist key business objects. We can choose which objects must persist, which ones should persist with JPA specification. JPA is not a tool or framework, it describes a collection of principles that can be applied by any tool or framework, like Hibernate.

Relational objects are represented in a tabular format, however object models are represented in an interconnected graph of object format. While storing and retrieving an object model from a relational database, some problems can occur due to the following reasons:
- *Granularity :* Object model has more granularity than relational model.
- *Subtypes :* Subtypes (means inheritance) are not supported by all types of relational databases.
- *Identity :* Like object model, relational model does not expose identity while writing equality.
- *Associations :* Relational models cannot determine multiple relationships while looking into an object domain model.
- *Data navigation :* Data navigation between objects in an object network is different in both models.

As an effective solution to these problems, a programmer follows the *JPA Provider* framework, which allows easy interaction with database instance,  for relational object management. When you use JPA, you create a map from the datastore to your application's data model objects. Instead of defining how objects are saved and retrieved, you define the mapping between objects and your database, then invoke JPA to persist them. If you're using a relational database, much of the actual connection between your application code and the database will then be handled by *Java Database Connectivity API (JDBC )*. It provides annotations for metadata to describe the mapping of objects to the database in a specific form. For JPA annotations, each JPA implementation provides its own engine.

Each JPA implementation, a framework like Hibernate ORM or EclipseLink, codifies object-relational mapping into a library or framework, an **ORM layer**.  Hibernate, which was developed as an alternative to entity beans for persistence,  was originally based on JPA's object-relational mapping (ORM) model. As part of the application architecture, the ORM layer is responsible for managing the conversion of software objects to interact with the tables and columns in a relational database. In Java, the ORM layer converts Java classes and objects and hence, they can be stored and managed in a relational database. By default, the name of the object being persisted becomes the name of the table, and fields become columns. Once the table is set up, each table row corresponds to an object in the application. Object mapping is configurable, but defaults tend to work well. We can say that the ORM layer is an adapter layer; it adapts the language of object graphs to the language of SQL and relational tables. The ORM layer allows object-oriented developers to build software that persists data without ever leaving the object-oriented paradigm.

While JPA was originally intended for use with relational/SQL databases, some JPA implementations have been extended for use with NoSQL datastores. 

Spring Data JPA API provides JpaTemplate class to integrate spring application with JPA. Hence, we don't need to write the before and after code for persisting, updating, deleting or searching object such as creating *Persistence* instance, creating *EntityManagerFactory* instance, creating *EntityTransaction* instance, creating *EntityManager* instance, commiting *EntityTransaction* instance and closing *EntityManager*.


---

#### Q2 - What is the naming convention for finder methods in the Spring data repository interface ?

---

Spring data JPA has its own naming conventions for methods. We can build sophisticated queries just by following these conventions . These conventions are also known as **method name strategies**. These strategies have defined set of keyword to use in method names and based on the formed method name, method performs predefined operations.  

Finder methods should use a special verb, like *get*, *read*, *find*, *query*, *stream*, *count*, followed by the property expressions. For instance, `findByLastName()`.   

Property expressions are usually property traversals combined with operators that can be concatenated.  *By* indicates the start of the actual criteria.  We can combine property expressions with *AND* and *OR*.  We can use several comparison keywords like *Between*, *LessThan*, *GreaterThan*, *Like* etc. As a default, this keyword is *Equals*. The method parser supports setting an *IgnoreCase* flag for individual properties, for example,`findByLastnameIgnoreCase(…))` or for all properties of a type that support ignoring case (usually Strings, for example, `findByLastnameAndFirstnameAllIgnoreCase(…))`.  We can apply static ordering by appending an *OrderBy* clause to the query method that references a property and by providing a sorting direction (*Asc or Desc*).


The following table shows some supported  keywords inside method names :

| Keyword | Sample |
|---------|--------|
| And | findByLastnameAndFirstname |
| Or | findByLastnameOrFirstname |
| Is , Equals | findByFirstname , findByFirstnameIs ,findByFirstnameEquals |
| Between | findByStartDateBetween |
| LessThan | findByAgeLessThan |
| LessThanEqual | findByAgeLessThanEqual |
| GreaterThan | findByAgeGreaterThan |
| GreaterThanEqual | findByAgeGreaterThanEqual |
| After | findByStartDateAfter |
| Before | findByStartDateBefore |
| IsNull | findByAgeIsNull |
| IsNotNull,NotNull | findByAge(Is)NotNull |
| Like | findByFirstnameLike |
| NotLike | findByFirstnameNotLike |
| StartingWith | findByFirstnameStartingWith |
| EndingWith | findByFirstnameEndingWith |
| Containing | findByFirstnameContaining |
| OrderBy | findByAgeOrderByLastnameDesc |
| Not | findByLastnameNot |
| In | findByAgeIn(Collection`<Age>` ages) |
| NotIn | findByAgeNotIn(Collection`<Age>` ages) |
| True | findByActiveTrue() |
| False | findByActiveFalse() |
| IgnoreCase | findByFirstnameIgnoreCase |



---

#### Q3 - What is PagingAndSortingRepository ?

---

Pagination allows the users to see a small portion of data at a time (a page), and sorting allows the users to view the data in a more organized way. Both paging and sorting help the users consume information more easily and conveniently. Paging and sorting is mostly required when we are displaying domain data in tabular format in UI. Pagination consist of two fields – page size and page number. Sorting is done on a single of multiple fields in the table.

Our repository interface must extend the `PagingAndSortingRepository` interface in order to use paging and sorting APIs provided by Spring Data JPA. **`PagingAndSortingRepository`** is an extension of the `CrudRepository` to provide additional methods to retrieve entities using the pagination and sorting abstraction. It provides two methods :
- `Page findAll(Pageable pageable)` – returns a Page of entities meeting the paging restriction provided in the Pageable object.
- `Iterable findAll(Sort sort)` – returns all entities sorted by the given options. No paging is applied here.

Once we extend `PagingAndSortingRepository`, we can add our own methods that take *Pageable* and *Sort* as parameters.

`JpaRepository` interface extends the `PagingAndSortingRepository` interface, so if your repository interface is of type `JpaRepository`, you don’t have to make a change to it.



---

#### Q4 -  Differentiate between findById() and getOne() ?

---

Both `findById()` and `getOne()` methods are used to retrieve an object from underlying datastore. But the underlying mechanism for retrieving records is different for both these methods.  Differences between them :

| `findById()` | `getOne()` |
|----------------|---------------|
| Available in `CrudRepository` | Available in `JpaRepository` |
| EAGER loaded operation | Lazy loaded operation that avoids database roundtrip from the JVM as it never hits the database until the properties of returned proxy object are actually accessed. |
| Will actually hit the database and return the real object mapping to a row in the database | Does not even hit the database, so in order to be sure about the effective loading of the entity, invoking a method on it is required. |
| Returns null if actual object corresponding to given Id does not exist | Will throw an exception called `EntityNotFoundException` if the actual object does not exist during access invocation |
| Returns one Optional (a value that may or may not exist) Object | Returns a reference to an entity with the given identifier  |
| An additional round-trip to database is required | Better performance |
| Object is eagerly loaded so all attributes can be accessed | Useful only when access to properties of object is not required |
| Relies on  `EntityManager.find()` | Relies on `EntityManager.getReference()` |


---

#### Q5 - What is @Query used for ?

---

Spring Data provides many ways to define a query that we can execute. One of these is the `@Query` annotation.

- **Select Query :** We can annotate a method with the **`@Query`** annotation — its value attribute contains the JPQL or SQL to execute - *for defining SQL to execute for a Spring Data repository method*.  The `@Query` annotation takes precedence over named queries, which are annotated with `@NamedQuery` or defined in an `orm.xml` file. It's better to place a query definition just above the method inside the repository rather than inside our domain model as named queries. The repository is responsible for persistence, so it's a better place to store these definitions.   
   - *JPQL :* By default, the query definition uses JPQL.  A simple repository method that returns active User entities from the database:
	```
	@Query("SELECT u FROM User u WHERE u.status = 1")
    Collection<User> findAllActiveUsers();
	```
   -  *Native :* We can use also *native SQL* to define our query. All we have to do is set the value of the `nativeQuery` attribute to true and define the native SQL query in the value attribute of the annotation:
	```
	@Query(
	    value = "SELECT * FROM USERS u WHERE u.status = 1", 
	    nativeQuery = true)
      Collection<User> findAllActiveUsersNative();
	```
	
- **Define Order in a Query :** We can pass an additional parameter of type *Sort* to a Spring Data method declaration that has the `@Query` annotation. It'll be translated into the *ORDER BY* clause that gets passed to the database.
   -  *Sorting for JPA Provided and Derived Methods  :* For the methods we get out of the box such as `findAll(Sort)` or the ones that are generated by parsing method signatures, we can only use object properties to define our sort :
	  
     `userRepository.findAll(Sort.by(Sort.Direction.ASC, "name"));`

   -  *JPQL :* When we use JPQL for a query definition, then Spring Data can handle sorting without any problem — all we have to do is add a method parameter of type Sort:
	```
     @Query(value = "SELECT u FROM User u")
     List<User> findAllUsers(Sort sort);
   ```
	We can call this method and pass a Sort parameter, which will order the result by the name property of the User object:
	  
      `userRepository.findAllUsers(Sort.by("name"));`

	Because we used the `@Query` annotation, we can use the same method to get the sorted list of Users by the length of their names:
	
      `userRepository.findAllUsers(JpaSort.unsafe("LENGTH(name)"));`

	It's crucial that we use `JpaSort.unsafe()` to create a *Sort* object instance.
   -  *Native :*  When the `@Query` annotation uses native SQL, then it's not possible to define a Sort.

- **Pagination :** It allows us to return just a subset of a whole result in a Page. This is useful, for example, when navigating through several pages of data on a web page. Pagination also minimizes the amount of data sent from server to client. By sending smaller pieces of data, we can generally see an improvement in performance.
   -  *JPQL  :*  Using pagination in the JPQL query definition is straightforward:
	    ```
	    @Query(value = "SELECT u FROM User u ORDER BY id")
        Page<User> findAllUsersWithPagination(Pageable    pageable);
	    ```
	    We can pass a `PageRequest` parameter to get a page of data.
   -  *Native  :*  We can enable pagination for native queries by declaring an additional attribute `countQuery`. This defines the SQL to execute to count the number of rows in the whole result:
	```
	@Query(
        value = "SELECT * FROM Users ORDER BY id", 
        countQuery = "SELECT count(*) FROM Users", 
        nativeQuery = true)
      Page<User> findAllUsersWithPagination(Pageable pageable);
	```
	
- **Indexed Query Parameters :** It is one of two possible ways that we can pass method parameters to our query. 
   -  *JPQL :*  For indexed parameters in JPQL, Spring Data will pass method parameters to the query in the same order they appear in the method declaration.
	```
    @Query("SELECT u FROM User u WHERE u.status = ?1") 
    User findUserByStatus(Integer status); 
    
    @Query("SELECT u FROM User u WHERE u.status = ?1 and u.name = ?2") 
    User findUserByStatusAndName(Integer status, String name);
	```
	For the above queries, the `status` method parameter will be assigned to the query parameter with index 1, and the `name `method parameter will be assigned to the query parameter with index 2.
   -  *Native :*  Indexed parameters for the native queries work exactly in the same way as for JPQL:
	```
	@Query(
         value = "SELECT * FROM Users u WHERE u.status = ?1", 
         nativeQuery = true)
      User findUserByStatusNative(Integer status);
	```
- **Named Parameters :**  We can also pass method parameters to the query using named parameters. We define these using the `@Param` annotation inside our repository method declaration. Each parameter annotated with `@Param` must have a value string matching the corresponding JPQL or SQL query parameter name. A query with named parameters is easier to read and is less error-prone in case the query needs to be refactored.
   - *JPQL :*  We use the `@Param` annotation in the method declaration to match parameters defined by name in JPQL with parameters from the method declaration:
	```
	 @Query("SELECT u FROM User u WHERE u.status = :status and u.name = :name")
     User findUserByStatusAndNameNamedParams(
        @Param("status")Integer status, 
        @Param("name")String name);
	```
   - *Native :*  There is no difference in how we pass a parameter via the name to the query in comparison to JPQL — we use the `@Param` annotation:
	```
	 @Query(value = "SELECT * FROM Users u WHERE u.status = :status and u.name = :name", 
         nativeQuery = true)
     User findUserByStatusAndNameNamedParamsNative(
         @Param("status")Integer status, @Param("name")String name);
	```
	
- **Collection Parameter :**  The case when the where clause of our JPQL or SQL query contains the *IN (or NOT IN)* keyword:
	`SELECTu FROMUseru WHEREu.name IN:names`
	
  In this case, we can define a query method that takes `Collection` as a parameter:
	```
	@Query(value = "SELECT u FROM User u WHERE u.name IN :names")
      List<User> findUserByNameList(@Param("names")Collection<String> names);
	```
	As the parameter is a `Collection`, it can be used with *List*, *HashSet*, etc.
	
- **Update Queries with `@Modifying` :**  We can use the `@Query` annotation to modify the state of the database by also adding the `@Modifying` annotation to the repository method.
   - *JPQL :* The repository method that modifies the data has two differences in comparison to the select query — it has the `@Modifying` annotation and, of course, the JPQL query uses update instead of select:
	
    ```
	@Modifying
    @Query("update User u set u.status = :status where u.name = :name")
    int updateUserSetStatusForName(@Param("status")Integer status, 
      @Param("name")String name);
	```
	The return value defines how many rows the execution of the query updated. Both indexed and named parameters can be used inside update queries.
   - *Native :*  We can modify the state of the database also with a native query. We just need to add the `@Modifying`  annotation:
	```
	 @Modifying
     @Query(value = "update Users u set u.status = ? where u.name = ?", 
          nativeQuery = true)
     int updateUserSetStatusForNameNative(Integer status, String name);
	```



---

#### Q6 - What is lazy loading in hibernate ?

---

Lazy loading, also known as *dynamic function loading*, is a fetching technique used for all the entities in *Hibernate*. It decides whether to load a child class object while loading the parent class object. When we use association mapping in Hibernate, it is required to define the fetching technique. The main purpose of lazy loading is to fetch the needed objects from the database.

Hibernate supports inheritance which means records with parent child relationship. Consider the situation when one parent have multiple child records. Now, Hibernate can use lazy loading, which means it will load only the required classes, not all classes.  It prevents a huge load since the entity is loaded only once when necessary.  Lazy loading improves performance by avoiding unnecessary computation and reduce memory requirements.
 
The simplest way that Hibernate can apply lazy load behavior upon the entities and associations is by providing a proxy implementation of them. Hibernate intercepts calls to the entity by substituting a proxy for it derived from the entity’s class. Where the requested information is missing, it will be loaded from the database before control is ceded to the parent entity’s implementation.

Lazy loading can be used with all types of Hibernate mapping, i.e., one-to-one, one-to-many, many-to-one, and many-to-many.

To enable Lazy loading, we use the following annotation parameter:

`fetch= FetchType.LAZY`

Following code is the syntax of lazy loading:

`@OneToOne(fetch= FetchType.LAZY)`




---

#### Q7 - What is SQL injection attack ? Is Hibernate open to SQL injection attack ?

---

SQL injection is a common attack vector that allows users with malicious SQL code to access hidden information by manipulating the backend of databases. SQL injection refers to the act of someone inserting a MySQL statement to be run on your database without your knowledge. Injection usually occurs when you ask a user for input, like their name, and instead of a name they give you a MySQL statement that you will unknowingly run on your database. This data may include sensitive business information, private customer details, or user lists. A successful SQL injection can result in deletion of entire databases, unauthorized use of sensitive data, and unintended granting of administrative rights to a database.

Normal:    ` ” SELECT * FROM student WHERE studentName= ‘sweety'” `
Injection: ` “SELECT * FROM student WHERE studentName= ” +studentName `

A successful malicious SQL statement could give an attacker administrator access to a database, allowing them to select data such as employee ID/password combinations or customer records, and delete, modify, or data dump anything in the database they choose. The right SQL injection attack can actually allow access to a hosting machine’s operating system and other network resources, depending on the nature of the SQL database.

Hibernate relieves us from creating hand-coded SQL statements, but they won't prevent us from writing vulnerable code. Hibernate allows the use of “native SQL” and defines a proprietary query language, named, HQL the former is prone to SQL Injection and the later is prone to HQL injection. Because we're using unvalidated input to create a JPA query, Hibernate is open to SQL Injection attack too.

For Hibernate, we can prevent SQL injection with parameter binding. There are two ways to parameter binding :
1. **Named parameters binding :** The most common and user friendly way. It use colon followed by a parameter name (:example) to define a named parameter.
   - The `setParameter`  is smart enough to discover the parameter data type for you.

   ```
    String hql = "from Student student where student.rollNumber= :rollNumber";
    Query query = session.createQuery(hql);
    query.setParameter("rollNumber", "3");
    List result = query.list();
    ```

    - `setString` can be used to tell Hibernate this parameter date type is String.

    ```
     String hql = "from Student student where student.studentName= :studentName";
     Query query = session.createQuery(hql);
     query.setString("studentName", "Sweety Rajput");
     List result = query.list();
    ```

   - The object can be passed into the parameter binding. Hibernate will automatic check the object’s properties and match with the colon parameter.

    ```
     Student student= new Student();
     student.setCourse("MCA");
     String hql = "from Student student where student.course= :course";
     Query query = session.createQuery(hql);
     query .setProperties(student);
     List result = query.list();
    ```

2. **Positional parameters binding :**  It’s use question mark (?) to define a named parameter, and you have to set your parameter according to the position sequence. 

    ```
     String hql = "from Student student where student.course= ? and student.studentName = ?";
     Query query = session.createQuery(hql);
     query.setString(0, "MCA");
     query.setParameter(1, "Dinesh Rajput")
     List result = query.list();
    ```


---

#### Q8 - What is criteria API in hibernate ?

---

While working with Hibernate Query Language (HQL), we manually prepare the HQL queries for reading the data from database. For the better performance, it is always recommended to write a query as tuned query. In the case of HQL, we need to prepare the tuned queries. Hibernate will only translate HQL into SQL and then executes it, but it will not tune the queries. For HQL, the responsibility of tuning the queries depends on the developer. Instead of writing the HQL queries and tuning them explicitly, we can use **Hibernate Criteria API**.

In the Hibernate Criteria API, there is no need to create a query. Instead, hibernate itself will prepare a tuned query. So that we can get better performance with criteria while reading the data from the database.
Query tuning is required only while selecting the data, so *Hibernate Criteria API* is for select operations only. Criteria API allows us to build up a  query criteria object programmatically where you can apply filtration rules and logical conditions. Hibernate Criteria is an interface, a simplified API for retrieving entities. We can obtain a reference of Criteria interface by calling the`createCriteria()` method on the session by passing the object of a pojo class. This method can be used to create a *Criteria* object that returns instances of the persistence and object class when your application executes a criteria query.

`Criteria criteria = session.createCriteria(Employee.class);`

 Here is a basic example of a criteria query is one, which will simply return every object that corresponds to the Employee class.

```
Criteria cr = session.createCriteria(Employee.class);
List results = cr.list();
```

We can use `add()` method available for Criteria object to add restriction for a criteria query. This is the example to add a restriction to return the records with salary is equal to 2000 −

```
Criteria cr = session.createCriteria(Employee.class);
cr.add(Restrictions.eq("salary", 2000));
List results = cr.list();
```


---

#### Q9 - What Is Erlang? Why Is It Required For Rabbitmq ?

---

**Erlang** is a general-purpose, concurrent and functional programming language and also garbage-collected runtime system. Erlang has built-in support for  distribution, fault tolerance, eager evaluation, single assignment and dynamic typing. It has also immutable data and pattern matching.

OTP (Open Telecom Platform) is a large collection of libraries for Erlang which consists of the Erlang runtime system, several ready-to-use components (OTP) mainly written in Erlang, and a set of design principles for Erlang programs. Most projects using *Erlang* are actually using *Erlang/OTP*,  they are used interchangeably with eachother even if one is the language and the other is the collection of libraries. OTP is also open source.

The Erlang runtime system is designed for systems that are:
- Distributed
- Fault-tolerant
- Soft real-time
- Highly avaliable, non-stop applications
- Hot swapping, where code can be changed without stopping the system.

Erlang applications are built of very lightweight Erlang processes in the Erlang runtime system. Erlang processes can be seen as "living" objects (OOP), with data encapsulation and message passing, but capable of changing behavior during runtime. The Erlang runtime system provides strict process isolation between Erlang processes (this includes data and garbage collection, separated individually by each Erlang process) and transparent communication between processes on different Erlang nodes (on different hosts).

Erlang OTP is a technology tailored for building stabe, reliable, fault tolerant and highly scalable systems which possess native capabilities of handling very large numbers of concurrent operations, such as is the case with RabbitMQ.

The RabbitMQ server, which is written in Erlang programming language, is built on the *Erlang/OTP framework* for clustering and failover. Client libraries to interface with the broker are available for all major programming languages. We need to first install Erlang before installing RabbitMQ, because RabbitMQ is built on Erlang.


---

#### Q10 - What is the JPQL ?

---

 *Java Persistence Query Language (JPQL)* defined in JPA specification is an onject-oriented query language which performs several database operations especially on persistent entities  in a relational database. JPQL is developed based on SQL syntax by using the entity object model. A JPQL query can get and return objects more than field values from tables. We can say that the main aim of JPA is to convert JPQL into SQL. Even though this is established based on SQL syntax, the database won’t be affected directly.

JPQL is an extension of *Entity JavaBeans Query Language (EJBQL)*, adding some important features to it: -
	Performing join operations.
	Updating and deleting data in a bulk.
	Performing aggregate function with sorting and grouping clauses.
	Single and multiple value result types.
	
JPQL has significant features to consider:
- A platform-independent query language.
- Simple and robust.
- Possible to  use with any type of database such as MySQL, Oracle.
- Queries can be declared statically into metadata or can also be dynamically built in code.

JPQL syntax is very similar to the syntax of SQL. SQL works directly against relational database tables, records and fields, whereas JPQL works with Java classes and instances. There are several clauses used by JPQL similar to SQL, They are:
- *SELECT :* Retrieves data or information.
- *UPDATE :* Updates data.
- *DELETE :* Deletes data.

`EntityManager.createQuery()` API will support for querying language. 


---

#### Q11 - What are the steps to persist an entity object ?

---


1. Create an *entity manager factory* object. The `EntityManagerFactory` interface present in `java.persistence` package is used to provide an entity manager.
	
	`EntityManagerFactory emf=Persistence.createEntityManagerFactory("Employee_details");`  
	
2. Get an *entity manager* from the factory.
	
	`EntityManager em=emf.createEntityManager();`  
	
3. Initialize an entity manager.
	
	`em.getTransaction().begin(); `
	
4. Persist the data into the relational database.
	
	`em.persist(e1);` 
	
5. Close the transaction
	
	`em.getTransaction().commit();`  
	
6. Finally, release the factory resources.
	
	```
	emf.close();  
	    em.close();  
	```


---

#### Q12 - What are the different types of entity mapping ?

---

- **One-to-one mapping :**  It represents a single-valued association where an instance of one entity is associated with an instance of another entity. In this type of association, one instance of source entity can be mapped with at most one instance of the target entity. For instance, a person can have only one passport, and a passport is assigned to a single person.
	
- **One-To-Many mapping :**  This type of mapping comes into the category of collection-valued association where an entity is associated with a collection of other entities. In this type of association, the instance of one entity can be mapped with any number of instances of another entity.  For example, a Person instance can have more than one Bank Account instance but a bank account instance can have at most one person instance as account holder.
	There are some employees who manage more than one team while there is only one manager to manage a team”.

- **Many-to-one mapping :**  This mapping type represents a single-valued association where a collection of entities can be associated with the similar entity. In the relational database, more than one row of an entity can refer to the same row of another entity. It is related to a one-to-many mapping but the difference is due to perspective. As an example, any number of credit cards can belong to a customer and there might be some customers who do not have any credit card, but every credit card in a system has to be associated with an employee(like total participation). While a single credit card can not belong to multiple customers.
	
	
- **Many-to-many mapping :**   The Many-To-Many mapping represents a collection-valued association where any number of entities can be associated with a collection of other entities. In the relational database, more than one row of one entity can refer to more than one row of another entity. A person can have more than one skills. More than one person can attain a skill. A customer can buy any number of products and a product can be bought by many customers. 



---

#### Q13 - What are the properties of an entity ?

---

An entity is an application-defined object in Java Persistence Library, so the properties of an entity that application-defined object must have: -
- **Persistability :**  An object is called persistent if it is stored in the database and can be accessed anytime.
- **Persistent Identity :**  In Java, each entity is unique and represents an object identity. Similarly, when the object identity is stored in a database, then it is represented as persistence identity. This object identity is the same with the primary key in the database.
- **Transactionality :**  Entity can perform various operations such as create, delete, update. Each operation makes some changes in the database. It ensures that whatever changes made in the database either be succeed or failed atomically.
- **Granularity :**  Entities should not be primitives, primitive wrappers or built-in objects with single dimensional state.



---

#### Q14 - Difference between CrudRepository and JpaRepository in Spring Data JPA?

---

CrudRepository and JPA repository both are the interface of the Spring Data Repository Library. Spring Data Repository reduces the boilerplate code by providing some predefined finders to access the data layer for various persistence layers. Important differences between them :

| CrudRepository | JpaRepository |
|----------------|---------------|
| The base interface and acts as a marker interface that extends *Spring Data `Repository` interface* | Extends `PagingAndSortingRepository` that extends `CrudRepository` |
| Provides methods for *CRUD* operations. For example, `save()`, `saveAll()`, `findById()`, `findAll()`, etc. | Provides the full API of `CrudRepository` and `PagingAndSortingRepository`. For instance,  `flush()`, `saveAndFlush()`, `saveAllAndFlush()`, `deleteInBatch()`, etc along with the methods that are available in `CrudRepository`. |
| Does not provide methods for implementing pagination and sorting. | Provides all the methods for which are useful for implementing pagination and sorting, because of extension the `PagingAndSortingRepository`. We can also add new methods using named or native queries based on business requirements. |
| The `saveAll(Iterable<S> entities)`  method of *CrudRepository* returns *Iterable*. | The `saveAll(Iterable<S> entities)`  method of *JpaRepository* returns *List*. |

 A simple example of `CrudRepository` usage : 

```
@Repository
public interface BookDAO extends CrudRepository {
   Book Event findById(@Param("id") Integer id);
}
```   

 A simple example of `JpaRepository` usage: 

```
@Repository
public interface BookDAO extends JpaRepository {
   Book findByAuthor(@Param("id") Integer id);
}
``` 


---


 




 


 



