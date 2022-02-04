
### HOMEWORK ANSWERS RELATED TO OBJECT ORIENTED PROGRAMMING CONCEPTS WITH JAVA

---

#### Q1 – Why we need to use OOP ? Some major OOP languages ?

---

Before OOP, we just had primitive data types that store single, simple values and then needed to store many pieces of data. Then the structure and the array came to the stage for this. The array can not store different types of data, but structure can do that. The main issue with structures is that you can not define functions within one.

Then OOP solved this issue with classes and now OOP helps programmers create complex programs by grouping together related data and functions.
 Some major OOP languages are Java, Python, Ruby, Javascript.
 
---


#### Q2 – Interface vs Abstract class ?

---

In order to understand well the difference between interface and abstract class, we need to first understand abstraction. Abstraction means showing only essential details and keeping everything else hidden so that the program is prevented from becoming entangled and complex and can be worked on incrementally.

Interface and Abstract class are both used for abstraction. There are several differences between them below:


| Interface  | Abstract Class   |
|------------|------------------|
| Can be declared with the interface keyword as an optional choice | Have to be declared with an abstract keyword |
| Defines the peripheral abilities (communication) of a class | Defines the identity of a class |
| Helps you to achieve loose coupling | Helps you to define a common interface for its subclasses  |
| Allows you to separate the definition of a method from the inheritance hierarchy | Allows code reusability |
| Designed to support dynamic method resolution at run time | Provides a template for future specific classes |
| Only abstract methods| Abstract and non-abstract methods;with Java 8, also default and static methods, also necessary to have at least one abstract method |
| Can be implemented using the keyword “implements” | Can be extended using the keyword “extends” |
| Use when various implementations share only method signature. Polymorphic hierarchy of value types | Use when various implementations of the same kind share a common behavior |
| Only static and final variables | Final, non-final, static and non-static variables|
| Interface can’t provide the implementation of an abstract class| Abstract class can provide the implementation of the interface|
| Variables declared in a Java interface are by default final | An abstract class may contain non-final variables|
| Can extend another Java interface only | Can extend another Java class and implement multiple Java interfaces|
| Can not have an access modifier,it behaves public by default | Can have an access modifier like public, private, protected|
| Can inherit multiple interfaces but cannot inherit a class |Can inherit a class and multiple interfaces|


---

#### Q3 – Why wee need equals and hashcode ? When to override ?

---

The equals() and hashcode() are the two important methods provided by the Object class for comparing objects. Since the Object class is the parent class for all Java objects, hence all objects inherit the default implementation of these two methods.

Java needs equals() because it is the method through which object equality is tested by examining classes, fields, and other conditions the designer considers to be part of an equality test.
A hashcode is an integer value associated with every object in Java, facilitating the hashing in hash tables.To get this hashcode value for an object, we can use the hashcode() method in Java. It is the means hashcode() method that returns the integer hashcode value of the given object. The purpose of hashCode() is to provide a hash value primarily for use by hash tables; though it can also be used for other purposes. The value returned is based on an object's fields and hash codes of its composite and/or aggregate objects. The method does not take into account the class or type of object.

If the generated hashcode values are equal for both the Objects, after that we compare the both these Objects with reference to their state for that we override equals(Object) method within the class. And if both Objects have the same state according to the equals(Object) method then they are equal otherwise not. And it would be better with regard to performance if different Objects generates different hashcode value.

Within the same JVM, hashCode() can be used as a cheap precursor for equality by testing for a known hash code first and only if the same testing actual equality; provided that the equality test is significantly more expensive than generating a hash code.

The default implementation of equals() method is not enough to satisfy business needs, especially if we're talking about a huge application that considers two objects as equal when some business fact happens. In some business scenarios, developers provide their own implementation in order to force their own equality mechanism regardless the memory addresses.
As per the Java documentation, you should override hashcode() each time you override equals() in order to achieve a fully working equality mechanism — it's not enough to just implement the equals() method.  Overriding equals() alone will result in a violation of the general contract for Object.hashCode(), which will prevent your class from functioning properly in conjunction with all hash-based collections, including HashMap, HashSet, and Hashtable.
Domain-Driven Design can help us decide circumstances when we should leave them be. For entity classes – for objects having an intrinsic identity – the default implementation often makes sense. However, for value objects, we usually prefer equality based on their properties. 


---

#### Q4 – Diamond problem in Java ? How to fix it?

---

In order to understand and solve the diamond problem, we need first to understand  inheritance and multiple inheritance clearly. 

Inheritance is a relation between two classes, the parent and child class. The class which inherits the properties is known as sub class or, child class and the class whose properties are inherited is super class or, parent class. In inheritance a copy of super class members is created in the sub class object. Therefore, using the sub class object you can access the members of the both classes. To define this relation, we use extends keyword.

There are different types of inheritance such as, single, multiple, multi-level, and hybrid inheritance.
As simple inheritance allows a child class to derive properties from one super-class.
Multi-level inheritance allows a child class to inherit properties from a class that can inherit properties from some other classes. Java supports them.

What Java does not allow is multiple inheritance where one class can inherit properties from more than one class. In other words, in multiple inheritance we can have one child class and n number of parent classes. 
This creates a problem when there exist methods with the same name and signature in both the super-class and sub-class. When we call the method, the compiler gets confused and cannot determine which class method to be called and even on calling which class method gets the priority. It is known as the diamond problem.  It is an ambiguity that can rise as a consequence of allowing multiple inheritance.  It is sometimes referred to as the deadly diamond of death. 
Due to these complications and ambiguities, Java does not support multiple inheritance. It creates problems during various operations, for example, constructor chaining and casting. Hence, it will be good to avoid it for making things simple.


The solution to the diamond problem is default methods and interfaces. We can achieve multiple inheritance by using these two things.
Unlike other abstract methods, default methods are the methods of an interface with a default implementation. If you have default method in an interface, it is not mandatory to override (provide body) it in the classes that are already implementing this interface.

The advantage of interfaces is that it can have the same default methods with the same name and signature in two different interfaces. It allows us to implement these two interfaces, from a class. If you do so, you must override the default method from the class explicitly specifying the default method along with its interface name.


---

#### Q5 – Why we need Garbage Collector ? How does it run ?

---

Sometimes, the programmer may forget to destroy useless objects, and the memory allocated to them is not released. The used memory of the system keeps on growing and eventually there is no memory left in the system to allocate. Such applications suffer from "memory leaks". After a certain point, sufficient memory is not available for creation of new objects, and the entire program terminates abnormally due to OutOfMemoryErrors.

In Java, garbage collection happens automatically during the lifetime of a program at regular intervals and does not need to be handled separately. It can also be triggered by calling System.gc(), but the execution is not guaranteed.
This eliminates the need to de-allocate memory and therefore avoids memory leaks.
Java Garbage Collection is the process by which Java programs perform automatic memory management. Java programs compile into bytecode that can be run on a Java Virtual Machine (JVM).
When Java programs run on the JVM, objects are created on the heap, which is a portion of memory dedicated to the program.
Over the lifetime of a Java application, new objects are created and released. Eventually, some objects are no longer needed. You can say that at any point in time, the heap memory consists of two types of objects:

* *Live* - these objects are being used and referenced from somewhere else
* *Dead* - these objects are no longer used or referenced from anywhere
	
The Garbage Collector makes Java memory efficient because it removes these unreferenced objects from heap memory and makes free space for new objects. It involves three phases:

* **Mark objects as alive:** The GC identifies all the live objects in memory by traversing the object graph.When GC visits an object, it marks it as accessible and thus alive. Every object the garbage collector visits is marked as alive. All the objects which are not reachable from GC Roots are garbage and considered as candidates for garbage collection.
* **Sweep dead objects:** We have the memory space which is occupied by live (visited) and dead (unvisited) objects. The sweep phase releases the memory fragments which contain these dead objects.
* **Compact remaining objects in memory:** The dead objects that were removed during the sweep phase may not necessarily be next to each other. So, you can end up having fragmented memory space.Memory can be compacted after the garbage collector deletes the dead objects, so that the remaining objects are in a contiguous block at the start of the heap. The compaction process makes it easier to allocate memory to new objects sequentially.

No matter what implementation of the garbage collector we use, to clean up the memory, a short pause needs to happen. Those pauses are also called stop-the-world events or STW in short. The first step of the Garbage Collection cycle starts when your JVM threads are started and your business code is working. This is where your application code is running. At a certain point in time, an event happens that triggers garbage collection. To clear the memory, application threads have to be stopped. This is where the work of your application stops and the next steps start. The garbage collector marks objects that are no longer used and reclaims the memory. Finally, an optional step of heap resizing may happen if possible. Then the circle starts again, application threads are started. The full cycle of the garbage collection is called the epoch.


---

#### Q6 – Java ‘static’ keyword usage ?

---

In Java, if we want to access class members, we must first create an instance of the class. But there will be situations where we want to access class members without creating any instances. If we want to access class members without creating an instance of the class, we need to declare the class members static. When a member is declared static, it can be accessed before any objects of its class are created, and without reference to any object.

The static keyword in Java is mainly used for memory management. It is used to share the same variable or method of a given class. The users can apply static keywords with variables, methods, blocks, and nested classes. The static keyword belongs to the class than an instance of the class. The static keyword is used for a constant variable or a method that is the same for every instance of a class.


The static keyword is a non-access modifier in Java that is applicable for the following: 
1. Blocks
2. Variables
3. Methods
4. Classes and Interfaces

**Static blocks:** If you need to do the computation in order to initialize your static variables, you can declare a static block that gets executed exactly once, when the class is first loaded. Besides, we cannot use a non-static variable in a static block.

**Static variables:** When a variable is declared as static, then a single copy of the variable is created and shared among all objects at the class level. Static variables are, essentially, global variables. All instances of the class share the same static variable. 
You should use the static variable for the property that is common to all objects. 


Important points for static variables:
* We can create static variables at the class level only. 
* Static block and static variables are executed in the order they are presented in a program.

**Static methods:** When a method is declared with the static keyword, it is known as the static method. The most common example of a static method is the main( ) method. 
Methods declared as static have several restrictions: 
* The static method can’t use a non-static variable or non-static method directly. They can only directly call other static methods and  access static data.
* They cannot refer to this or super in any way.
* We can’t override the static members in a derived class.
	
**Static Classes and Interfaces:**
Static classes and interfaces are a type of nested class and interface in Java. Java uses the concept of nested class; i.e., a class defined under another class. The class in which the nested class is defined is the outer class. We cannot declare a top-level class and interface with a static modifier but can declare nested classes and interfaces as static. Such types of classes are called Nested static classes.
 
Nested static class doesn’t need a reference of Outer class. In this case, a static class cannot access non-static members of the Outer class. 

As the inner class is capable of accessing all the members of the outer class, without using a reference to the outside class thus it makes it more concise and simple.

As a summary, static keyword is important when the same value is used in the program again and again. It will not have any impact on objects, and if the variable is static, then its value will be the same for all objects irrespective of the object. 


---

#### Q7 – Immutability means ? Where, How and Why to use it ?

---

Immutability briefly refers to unchangable or unalterable structure. The fundamental idea behind immutability is that if we want to change a data-structure, we need to create a new copy of it with the changes, instead of mutating the original data-structure.
Mutating data-structures can create unexpected side-effects, and we must check against them. With immutability, we can keep our data structures predictable and side-effect free, and easier to reason with.
Data-structures shouldn’t be modifiable after being initialized. To change/mutate a data-structure, we must create a new variable containing the changed value. We can safely use any immutable data-structure without side-effects, even in parallel/concurrent environments, without uncertain results or issues due to unsynchronized access, or changes to out-of-scope state.

Functional languages support immutability by design. When using an object-oriented language, objects that accesses data structures (respectively) have to be designed explicitly to provide protection against unwanted modification.
Immutable objects offer a number of advantages for building reliable applications. As we don’t need to write defensive or protective code to keep application state consistent, our code can be simpler, more concise, and less error-prone than when we define immutable objects.

An immutable object is an object whose state cannot be modified after it is created. 
For example, primitive objects , all legacy classes, Wrapper class, String class, etc. 

We can make our own data structures immutable, either manually, or by using a library like Immutables. But it’s still an implementation detail, not a language feature like in other programming languages.
Every field of an immutable data-structure has to be immutable. And every field of the types of it has to be immutable, too. With a single mutable type, maybe even deeply nested, all the benefits of being immutable will be destroyed.

Some of the key benefits of immutable objects are:
- Simple to construct, test, and use
- Thread safety and have no synchronization issues
- Atomicity of failure : if an immutable object throws an exception, it's never left in an undesirable or indeterminate state
- Absence of hidden side-effects
- Protection against null reference errors
- Ease of caching
- Prevention of identity mutation
- Avoidance of temporal coupling between methods
- Support for referential transparency
- Protection from instantiating logically-invalid objects
- Protection from inadvertent corruption of existing objects
- Always having the same Hash code, so they can be used as the keys in a HashMap (or similar). If the hash code of an element in a hash table was to change, the table entry would then effectively be lost, since attempts to find it in the table would end up looking in the wrong place. This is the main reason that String objects are immutable - they are frequently used as HashMap keys.


---

#### Q8 – Composition and Aggregation means and differences ?

---

An object is a real-time entry, and objects have relationships between them both in programming or real life. Objects are related to each other using more than one relationship, such as Aggregation, Composition and Association.

Association is a relation between two separate classes which establishes through their Objects. Association can be one-to-one, one-to-many, many-to-one, many-to-many. In Object-Oriented programming, an Object communicates to another object to use functionality and services provided by that object. Composition and Aggregation are the two forms of association. 

**Aggregation:**
It is a special form of Association where it is a unidirectional association i.e. a one-way relationship. For example, a department can have students but vice versa is not possible and thus unidirectional in nature.
Java Aggregation allows only one-to-one relationships. Code reuse is best achieved by aggregation.  

**Composition:**
It is a restricted form of Aggregation in which two entities are highly dependent on each other unlike the aggregation. 
Composition in Java represents a one-to-many relationship.  

| Aggregation |	Composition |
|-------------|-------------|
| Implies a relationship where the child can survive independently of the parent which means ending one entity will not affect the other entity. | Implies a relationship where the child cannot exist independent of the parent which means two entities are tightly coupled or highly dependent on each other. |
| For example, Bank and Employee, delete the Bank and the Employee still exist.	| Example: Human and heart, heart don’t exist separate to a Human |
| Has-A relationship | Strong kind of Has-A or belong-to relationship, because the containing object owns it. |
|Weak Association |	Strong Association |


---

#### Q9 – Cohesion and Coupling means and differences ?

---

In object oriented design, **Coupling** refers to the degree of direct knowledge that one element has of another. In other words, the degree of dependency, connection between the components is called coupling. If the dependency is more, then it is considered as tight coupling. In general, tight coupling means the two classes often change together. In other words, if A knows more than it should about the way in which B was implemented, then A and B are tightly coupled.And if the dependency is less, then it is called loose coupling.In simple words, loose coupling means they are mostly independent. If the only knowledge that class A has about class B, is what class B has exposed through its interface, then class A and class B are said to be loosely coupled.

Tight coupling has several disadvantages:
- Without affecting remaining components, we cannot modify any component. Hence, enhancement becomes difficult.
- It suppresses reusability because of too much dependency.
- It reduces maintainability of the application.
- Tight coupling is not good at the test-ability. But loose coupling improves the test ability.
- Tight coupling does not provide the concept of interface. But loose coupling helps us follow the GOF principle of program to interfaces, not implementations.
- In Tight coupling, it is not easy to swap the codes between two classes. But it’s much easier to swap other pieces of code/modules/objects/components in loose coupling.

A good application designing is creating an application with loosely coupled classes by following encapsulation, i.e. by declaring data members of a class with the private access modifier, which disallows other classes to directly access these data members, and forcing them to call the public getter, setter methods to access these private data members.

**Cohesion** is the Object Oriented principle most closely associated with making sure that a class is designed with a single, specific, well-focused purpose.  A class created with high cohesion is targeted towards a single specific purpose, rather than performing many different purposes. The more focused a class is, the cohesiveness of that class is more.

When a class is designed to do many different tasks rather than focus on a single specialized task, this class is said to be a "low cohesive" class. Low cohesive classes are said to be badly designed, as it requires a lot of work at creating, maintaining and updating them.

High cohesion has following several advantages:
- Without affecting any components, we can modify any component. Hence, enhancement becomes easy.
- It promotes reusability of the code.
- It improves maintainability of the application.

 
| Coupling | Cohesion |
|----------|----------|
| Relationships between modules	| Relationship within the module |
| The relative independence between the modules	| The module's relative functional strength |
| Inter-Module Binding | Intra-Module Binding |
| While creating, you should aim for low coupling, i.e., dependency among modules should be less | While creating, you should aim for high cohesion, i.e., a cohesive component/ module focuses on a single function (i.e., single-mindedness) with little interaction with other modules of the system |
| In coupling, modules are linked to the other modules | In cohesion, the module focuses on a single thing |


---

#### Q10 - Heap and Stack means and differences ?

---

**Heap Area:** All the objects and their corresponding instance variables are stored here. This is the run-time data area from which memory for all class instances and arrays is allocated.
The heap is created on the virtual machine start-up, and there is only one heap area per JVM.

The Heap-memory allocation is further divided into three categories and these three categories help us to prioritize the data(Objects) to be stored in the Heap-memory or in the Garbage collection.
1. *Young Generation:*  It’s the portion of the memory where all the new data(objects) are made to allocate the space and whenever this memory is completely filled then the rest of the data is stored in Garbage collection.
2. *Old or Tenured Generation:*  This is the part of Heap-memory that contains the older data objects that are not in frequent use or not in use at all are placed.
3. *Permanent Generation:*  This is the portion of Heap-memory that contains the JVM’s metadata for the runtime classes and application methods.

**Stack Area:**

Whenever a new thread is created in the JVM, a separate runtime stack is also created at the same time. All local variables, method calls, and partial results are stored in the stack area.

For every method call, one entry is made in the stack memory which is called the Stack Frame. When the method call is complete, the Stack Frame is destroyed.

The Stack Frame is divided into three sub-parts:
1. *Local Variables –* Each frame contains an array of variables known as its local variables. All local variables and their values are stored here. The length of this array is determined at compile-time.
2. *Operand Stack –* Each frame contains a last-in-first-out (LIFO) stack known as its operand stack. This acts as a runtime workspace to perform any intermediate operations. The maximum depth of this stack is determined at compile-time.
3. *Frame Data –* All symbols corresponding to the method are stored here. This also stores the catch block information in case of exceptions.

| Heap	| Stack |
|-------|-------|
| Heap-memory is accessible or exists as long as the whole application(or java program) runs | It’s a temporary memory allocation scheme where the data members are accessible only if the method( ) that contained them is currently is running |
| This memory allocation scheme is different from the Stack-space allocation, here no automatic de-allocation feature is provided. We need to use a Garbage collector to remove the old unused objects in order to use the memory efficiently	| It allocates or de-allocates the memory automatically as soon as the corresponding method completes its execution. |
| We receive the corresponding error message if Heap-space is entirely full,  java. lang.OutOfMemoryError by JVM	| We receive the corresponding error Java. lang. StackOverFlowError by JVM, If the stack memory is filled completely |
| Since the Method and Heap areas share the same memory for multiple threads, the data stored here is not thread safe.	| Since the Stack Area is not shared and can only be access by owner thread, it is inherently thread safe |
| The processing time(Accessing time) of this memory is quite slow as compared to Stack-memory	| Memory allocation and de-allocation is faster as compared to Heap-memory allocation |
Size of Heap-memory is quite larger as compared to the Stack-memory	| Stack-memory has less storage space as compared to Heap-memory |


---

#### Q11 – Exception means ? Type of Exceptions ?

---

An exception (or exceptional event) is an unwanted or unexpected event, which occurs during the execution of a program i.e at run time, that disrupts the normal flow of the program’s instructions. When an exception occurs, the normal flow of the program is disrupted and the program/Application terminates abnormally, which is not recommended, therefore, these exceptions are to be handled. Exception indicates conditions that a reasonable application might try to catch.

All exception classes are subtypes of the java.lang.Exception class. The exception class is a subclass of the Throwable class. The Exception class has two main subclasses: IOException class and RuntimeException Class.
 

Other than the exception class there is another subclass called Error which is derived from the Throwable class.
Errors are abnormal conditions that happen in case of severe failures, these are not handled by the Java programs. Errors are generated to indicate errors generated by the runtime environment. Example: JVM is out of memory. Normally, programs cannot recover from errors.


An exception can occur for many different reasons. Following are some scenarios where an exception occurs.
- A user has entered an invalid data.
- A file that needs to be opened cannot be found.
- A network connection has been lost in the middle of communications or the JVM has run out of memory.

Some of these exceptions are caused by user error, others by programmer error, and others by physical resources that have failed in some manner.

Java defines several types of exceptions that relate to its various class libraries. Java also allows users to define their own exceptions. 

- **Built-in exceptions** are the exceptions which are available in Java libraries. These exceptions are able to define the error situation so that we can understand the reason of getting this error. It can be categorized into two broad categories, i.e., checked exceptions and unchecked exceptions.
	    
  - **Checked exceptions :** A checked exception is an exception that is checked (notified) by the compiler at compilation-time, these are also called as compile time exceptions. The compiler ensures whether the programmer handles the exception or not. The programmer should have to handle the exception; otherwise, the system has shown a compilation error.
	
     - *ClassNotFoundException :* This Exception is raised when we try to access a class whose definition is not found
	 - *FileNotFoundException :* This Exception is raised when a file is not accessible or does not open.
	 - *InterruptedException :* It is thrown when a thread is waiting, sleeping, or doing some processing, and it is interrupted.
	 - *IOException :* It is thrown when an input-output operation failed or interrupted
	 - *NoSuchFieldException :* It is thrown when a class does not contain the field (or variable) specified
	 - *NoSuchMethodException :* It is thrown when accessing a method which is not found.
	
	
  - **Unchecked exceptions :** An unchecked exception is an exception that occurs at the time of execution. These are also called as Runtime Exceptions. These include programming bugs, such as logic errors or improper use of an API. Runtime exceptions are ignored at the time of compilation. Usually, it occurs when the user provides bad data during the interaction with the program.
	      
	 - *NullPointerException :*  This exception is raised when referring to the members of a null object. Null represents nothing
	 - *ArithmeticException :* It is thrown when an exceptional condition has occurred in an arithmetic operation.
	 - *ArrayIndexOutOfBoundsException :* It is thrown to indicate that an array has been accessed with an illegal index. The index is either negative or greater than or equal to the size of the array.
	 - *RuntimeException :* This represents any exception which occurs during runtime.
	 - *NumberFormatException :* This exception is raised when a method could not convert a string into a numeric format.
	 - *StringIndexOutOfBoundsException :* It is thrown by String class methods to indicate that an index is either negative or greater than the size of the string
	

- **User-Defined Exceptions :** Sometimes, the built-in exceptions in Java are not able to describe a certain situation. In such cases, user can also create exceptions which are called ‘user-defined Exceptions’. 
For the creation of user-defined Exception, the user should create an exception class as a subclass of Exception class. Since all the exceptions are subclasses of Exception class, the user should also make his class a subclass of it. We can write a default constructor in his own exception class.
We can throw our own exception on a particular condition using the throw keyword. For creating a user-defined exception, we should have basic knowledge of the try-catch block and throw keyword.


---

#### Q12 – How to summarize ‘clean code’ as short as possible ?

---

We can summarize the clean code as organized, standardized, tidy, systematic, easily readable and free of unnecessary code.

A programmer who wants to write clean code should follow the Japanese 5S principles, that are:
- Seiri : **Organization :** knowing where things are, using approaches such as suitable naming
- Seiton : **Tidiness and Systematize :** a piece of code should be where you expect to find it, and if not, you should re-factor to get it there
- Seiso :  **Cleaning :**  keep the workplace free of waste, unnecessary code, get rid of  littering your code with comments and commented-out code lines that capture history or wishes of the future
- Seiketsu : **Standardization :** having a consistent coding style and set of practices within the group
- Shutsuke : **Self-discipline :** having the discipline to follow the practices and to frequently reflect on one’s work and be willing to change.


---

#### Q13 - What is the method of hiding in Java ?

---


Method hiding may happen in any hierarchy structure in java. When super class and the sub class contains same methods including parameters, and if they are static and, when called, the super class method is hidden by the method of the sub class. This mechanism is known as method hiding. It happens because static methods are resolved at compile time.

The same behavior involving the instance methods is called method overriding.  Hiding doesn't work like overriding, because static methods are not polymorphic. Overriding occurs only with instance methods. It supports late binding, so which method will be called is determined at runtime. On the other hand, method hiding works with static ones. Therefore it's determined at compile time.


---

#### Q14 - What is the difference between abstraction and polymorphism in Java ?

---


|Abstraction	| Polymorphism |
|---------------|--------------|
|Means  information hiding. Usually what is hidden is the representation of a data structure	| Means reuse with different types |
| Allows a programmer to design software better by thinking in general terms rather than specific terms 	| Allows a programmer to defer choosing the code you want to execute at runtime |
|Is implemented using abstract class and interface in Java	| Is supported by overloading and overriding in Java. Though overloading is also known as compile-time Polymorphism, method overriding is the real one because it allows a code to behave differently at different runtime conditions, which is known as exhibiting polymorphic behavior. |
| Provides a generalization, a concept much needed for the software to be reusable and customizable.	| Provides an applicable version of abstraction |
| Example: I implement sets, but I don't tell you whether a set is represented as a list, a balanced binary tree, or an unbalanced binary tree. Done right, I can change representation without breaking your code. |	So with an alike set example; you could create sets of Social Security numbers, sets of full names, or sets of fruitbats, all using the same code. |

