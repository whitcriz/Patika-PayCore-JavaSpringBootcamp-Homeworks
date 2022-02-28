## Patika & Paycore Java Spring Bootcamp 
### Week-6 Homework Answers

---

#### Q1 - What is the difference between manual testing and automated testing ?

---

| Manual Testing | Automated Testing |
|---------------------|-------------------------|
| QA Analyst executes manually | Uses automation tools such as Selenium in order to develop the test scripts and validate the software |
| Not much realiable because of human error possibilities | Reliable because of code and script-based executing. There is no testing Fatigue.|
| Slower than automated testing and uses human resources| Faster even with more test and less human resources |
| Does not necessarily require programming experience and knowledge | Require programming knowledge |
| Allows random testing | not allowed with random testing | 
| Not cost effective for high volume regression. | Not cost effective for low volume regression |
| Less expensive | More expensive with using the automation tools |
| Convenient for Exploratory, Usability and Adhoc Testing, and especially when we want a user-friendly system | Convenient for Regression Testing, Performance Testing, Load Testing and also all highly repeatable functional test cases. |


---

#### Q2 - What does Assert class ?

---

Assert class is a collection of helper classes to test various conditions within unit tests. Assert class provides us several static methods in order to compare the expecting value to the actual value during unit testing. If the expected and actual  are different related to the method condition, then it will throw an AssertionError with the given message in the parameters.


---

#### Q3 - How can be tested 'private' methods ?

---

We can handle testing *private methods* in four ways :

- We can test *private methods* indirectly by testing their effects on the public methods that call these private methods. Testing private methods may be an indication that those methods are moved into another class that assisting/supporting the reusability.
- We can make the method package private with no access modifier and put tests into the same package. This way can be handled with JUnit but it is slightly costly. Also, if we want another code then we can make the method public. 
- We can nest a static class inside the production class being tested which contains the private methods. The nested class has access to the private member of its enclosing class, so it would be able to invoke the private methods directly. The static class itself could be package access, allowing it to be a load part of the white box test. However, if we don’t want the nested class being accessible in our department JAR file, then we need to do extra work to extract it. This may be problematic because quality analysts will make changes in source code.
- We can use reflection that provides a clean separation of test code and production code.  Reflection is an API that is used to examine or modify the behavior of the methods, classes, interfaces at run time.


---

#### Q4 - What is Monolithic Architecture ?

---

Unlike layer-based structure, Monolithic Architecture is like a container that is made of dependent components. We can find all the functionalities of a project exists in a single codebase and so the components are tightly-coupled. Because of thightly-coupled components, it is unscalable and unflexible. Maintanance is quite difficult because this architecture creates very large and complex applications. 


---

#### Q5 - What are the best practices to write a Unit Test Case ?

---

The best practices to write a Unit Test Case should ensure these following properties :
- **Reliable** : Unit tests should fail only if there’s a bug in the system under test. If it doesn't, we cannot trust what the test results are telling us. They should be reproducible and independent from external factors such as the environment or running order.
- **Maintainable and readable** : When production code changes, tests often need to be updated, and possibly debugged as well. It is important to be easy to read and understand the test, for not only whoever wrote it, but also other developers. We should always organize and name your tests for a neat and readable structure.
- **Single-Use Case and fast**  : Good tests validate just one thing, a single use-case. Hence, they could be simpler and more understandable, and this brings us easier maintainability and debugging. When tests verify more than one thing, they can easily become complex and time-consuming to maintain. 
- **Using a minimal number of assertions** :  Focus on validating only what is needed for the use-case you are testing with the assertions.
- **Not doublet of the implementation logic of code** : If we mirror the implementation code in the unit test, then we can not truly test the code and this kind of test can misguide us about the code.
- **Isolated or Self-contained** :  Tests should be runnable on any machine, in any order, without affecting each other. If possible, tests should have no dependencies on environmental factors or global/external state. When tests have these kind of  dependencies, they will be harder to run and usually unstable. Besides this would make harder to debug and fix, and end up costing more time than they save. We can call them *sociable tests*  and they can require more setup, also violate the principles of being isolated and repeatable. Thanks to using mocks in testing, we have more control over the behavior of dependencies and so more testable code paths, especially because of self-contained structure of mocks . For example, we can return custom values or throw exceptions from the mock, in order to cover boundary or error conditions.
- **Automated** : We should run the unit tests in an automated process such as  daily, or every hour, or in a Continuous Integration or Delivery process. The reports need to be accessible to and reviewed by everyone on the team. As a team, we need to determine which metrics we care about, like code coverage, modified code coverage, number of tests being run, performance, etc.
- **Executed Within an Organized Test Practice** : We will need to write unit tests as we write our application code in order to drive the success of our testing at all levels, and make the unit testing process scalable and sustainable. We can also write the tests before the application code, called test-driven development. The crucial thing here is that tests go hand-in-hand with the application code. The tests and application code should even be reviewed together in the code review process. It's also critical for bug fixes. Every bug we fix should have a test that verifies the bug is fixed and this approach ensures that the bug stays fixed in the future.

- **Zero-tolerance policy for failing tests** : Test failures should indicate real issues, so we need to address these issues right away, before they waste QA's time, or worse, they get into the released product. The longer it takes to address failures, the more time and money those failures will ultimately cost your organization. So we need to run tests during refactoring, run tests right before you commit code, and should not let a task be considered "done" until the tests are passing too.

- **Up-to-date** : We need to refactor the unit tests by keeping them up to date when the application changes, otherwise they will lose their value. Especially if they are failing, failing tests are costing time and money to investigate each time they fail. 



---

#### Q6 - Why does JUnit only report the first failure in a single test ?

---

Reporting multiple failures on a single test indicates mostly that the test does too much and it is too big for a unit test. These indications are not compatible with the best practices of writing unit test case. Long tests are a design smell and indicate the likelihood of a design problem. So, Junit is designed to work best with small tests. It executes each test within a separate instance of the test class and reports failure on each test. Hence, failure in one test does not affect the execution of the other tests. We generally want exactly one test to fail for any given bug, if we can manage it.


---

#### Q7 - What are the benefits and drawbacks of Microservices ?

---

| Benefits | Drawbacks |
|------------|---------------|
| High scalability because of indepently scalable structure | More complicated architecture |
| Independently deployable | Communication between services can be complex. |
| More team autonomy which means that specific microservices can be assigned to specific development teams, which allows them to focus solely on one service or feature. Each team can work autonomously without worrying what’s going on with the rest of the app. | Prepaid costs can be higher because we need sufficient hosting infrastructure with security and maintenance support, and also skilled development teams who understand and manage all the services. |
| Reduced downtime through fault isolation and so a more stable system. | More challenging debugging which means each microservice having its own set of logs, so tracing the source of the problem can be difficult. |
| Possibility of working many teams at once in different parts of the network | Required security is more difficult because communication here takes place over the network, not in memory |
| Highly flexible for changes especially provide faster future implementation | A quite high complex infrastructure to allow for the proper operations of the distributed system architecture |
| Possibility to replace small parts of the system in case of crucial problems with these small parts | Making general, core changes are difficult | 
| Easy to integrate with new systems and external sources via API | Hard to ensure the transactionality because of complex and multiple services structure|
| Less dependence of the company on the service provider | Needed awareness of the possibility of delay because of the possibility of failing of network calls |



---

#### Q8 - What is the role of actuator in spring boot ?

---

Actuators can generate a large amount of motion from a small change. The Actuator in Spring Boot provides production ready features, such as health, auditing, and metric REST or JMX endpoints, to help you monitor and manage your application via actuator endpoints. Actuator endpoints let you monitor and interact with your application. Spring Boot includes a number of built-in endpoints and lets us add our own. 
Some built-in endpoints :
*`/health` endpoint* : Basic application health information. 
*`/env` endpoint* : The list of Environment variables used in the application
*`/metrics` endpoint* : The application metrics such as memory used, memory usable, threads, classes, system uptime
*`/beans` endpoint* : Spring beans and its types, scopes and dependency


Each individual endpoint can be enabled or disabled and exposed over *HTTP* or *JMX* which makes them remotely accessible. An endpoint is considered to be available when it is both enabled and exposed. The built-in endpoints are auto-configured only when they are available. Most applications choose exposure over *HTTP*, where the ID of the endpoint and a prefix of `/actuator` is mapped to a *URL*. For instance, by default, the health endpoint is mapped to `/actuator/health`. By default, all endpoints except for `shutdown` are enabled. If we prefer to disable all the default endpoints :

`management.endpoints.enabled-by-default=false`

Then, we can enable the endpoint whatever we want :

`management.endpoint.info.enabled=true`

However, disabled endpoints are removed entirely from the application context. So, if we want to change only the technologies over which an endpoint is exposed, we can use  the `include`  and `exclude` properties instead . Spring Boot endpoints have default exposures for *Web* and *JMX*. We can change these default exposures by using the technology-specific `include` and `exclude` properties.

The include property lists the *ID*s of the endpoints that are exposed. The exclude property lists the IDs of the endpoints that should not be exposed. The exclude property takes priority over the include property. You can configure both the include and the exclude properties with a list of endpoint IDs. If we want to stop exposing all endpoints over JMX and only expose the health and info endpoints, we can use the following property :

`management.endpoints.jmx.exposure.include=health,info`

`*` is used to select all endpoints. When we want to expose everything over HTTP except the `env` and `beans` endpoints, we use the following properties : 

```
management.endpoints.web.exposure.include=*
management.endpoints.web.exposure.exclude=env,beans
``` 

As a side note, iIf we want to implement our own strategy for when endpoints are exposed, we can register an `EndpointFilter` bean. 

The actuator endpoints that require a POST (shutdown and loggers endpoints), a PUT, or a DELETE get a 403 (forbidden) error when the default security configuration is in use because of CSRF protection. Disabling CSRF protection completely should be a choice only if you are creating a service that is used by non-browser clients. 



---

#### Q9 - What are the challenges that one has to face while using Microservices ?

---

The challenges that we could face while using Microservices are :

- **Design-related challenges** :  They can be determining each microservice’s size, optimal boundaries and connection points between each microservice and the framework to integrate services. 
Designing microservices requires creating them within a bounded context. Therefore, each microservice should clarify, encapsulate, and define a specific responsibility. To do this for each responsibility/function, developers usually use a data-centric view when modeling a domain. This approach raises its own challenge which is without logic, the data is nonsensical.

- **Security-related challenges** : Setting up access controls and administering secured authentication to individual services can be challenging, because data is distributed and maintaining the confidentiality and integrity of user data could be very difficult. Increased attack surface vulnerability can be very challenging too. When deploying microservices across multi-cloud environments, there is higher risk, besides loss of control and visibility of application components, resulting in more vulnerable points. Moreover, it becomes extremely hard to test for vulnerabilities since each microservice communicates with others through different infrastructure layers.

- **Testing and monitoring-related challenges** :  Interdependencies between services should be closely monitored. Any downtime of service due to service outages, service upgrades, etc., can all have cascading downstream effects. Due to the standalone nature of each microservice, every dependent service needs to be determined and confirmed before testing. One transaction can easily space across multiple services, and, as a result, any issue in one area can lead to a problem elsewhere. 

  Given the standalone nature of each microservice, we have to test individual services independently. Moreover, development teams also have to factor in integrating services and their interdependencies in test plans. When dealing with a microservices environment, there can be various reasons for a runtime failure, such as the microservice itself, its container, or even the network interconnecting the various services. Any failure would result in complex intermediate states, which would be difficult to recover from in most cases. 

- **Operational complexities-related challenges** : 

  - Traditional forms of monitoring may not work properly, for example with  a scenario where a request from the user interface traverses multiple services before getting to the one that can fulfill its request. With this scenario, the result of this traversal is a convoluted path of services, and without the appropriate monitoring tools, identifying the underlying cause of an issue is very tricky or often even impossible.
  - Although the scalability of microservices is often considered as an advantage, successfully scaling  microservice-based applications is challenging.
  - Optimizing and scaling require more complex coordination. In a typical microservices framework, an application is broken down to smaller-independent services that are hosted and deployed across separate servers. This architecture requires coordinating individual components, which is another challenge particularly when you experience a sudden spike in application usage.
  - Every service is needed to be fault tolerance. Businesses need their microservices to be resilient enough to withstand internal and external failures. In a microservices-based application, one component failing can affect the entire system. Therefore, the framework you use should consider fault tolerance for every service to ensure a design that prevents failure of an entire application in the event of an individual service downtime.

- **Communication-relates challenges** : We have to configure infrastructure layers that enable resource sharing across services in order to achieve the effective communication between the microservices like they are miniature standalone applications deployed independently. Otherwise, a poor configuration may lead to *Increased latency* and *Reduced speed of calls across different services*. Then we can have a non-optimized application with a slow response time.
- **Network Management** 
- **Maintanence of Microservices** 
- **Debugging issues**
- **Achieving Data Consistency**


---

#### Q10 - How independent microservices communicate with each other?

---

Microservices communicate with the help of an Application Programming Interface (APIs). For each microservice to interact with other microservices properly, there are two possible techniques, *Synchronous* and *Asynchronous*.
	
In the *synchronous communication protocol*, the user sends an request and waits for a response from the service. It is kind of delaying as the processor waits for the response without doing any other tasks. An example of this communication protocol is *HTTP (HyperText Transfer Protocol)*. In this protocol, the client requests the service directly via the HTTP rules. The client typically gets the response instantly with either success or error. The CPU gets blocked till the service sends the response to the designated requests. If, for any reason, the delay is much longer, it will affect the overall performance of the applications as the CPU sits and cannot do other vital tasks. That is, it can continue doing its job only when it receives the HTTP server reply. We can solve this issue with two ways by :
- Adding a circuit breaker to every service request, such as the *Rest Template*.
- Binding the HTTP-based interaction synchronous with the HTTP-based interaction asynchronous. 
	
In the *asynchronous communication protocol*, the client sends a request. But as opposed to the synchronous communication protocol, it doesn’t stop its task while waiting for a response from the service. It keeps continuing to do its designated work as it should have been doing, without affecting its performance or any functionalities. Hence, it has no delay as there is no blocking in letting the processor do any other tasks. An example of an asynchronous communication protocol is *AMQP (Advanced Message QueuingProtocol)*, which is supported by many operating systems and cloud providers.     Unlike HTTP, there is no direct communication between the services as it doesn’t directly send the request. Instead, it pushes the message via a *message broker* and just waits for acknowledgment that the message has been received by the broker. Generally, a message broker is used to manage and process the texts sent by the sender. The message broker takes all the liability and assurance to deliver the message to the designated place. As an important note, the interaction is always asynchronous where a message broker is used.  
An asynchronous messaging system may be implemented in a *one-to-one(queue)* or *one-to-many (topic)* mode. The most popular message brokers are *RabbitMQ* and *Apache Kafka*. An interesting framework which provides mechanisms for building message-driven microservices based on those brokers is *Spring Cloud Stream*.


---

#### Q11 - What do you mean by Domain driven design ?

---

