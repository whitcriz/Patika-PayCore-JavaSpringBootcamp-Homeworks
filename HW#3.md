## PATIKA & PAYCORE JAVA SPRING BOOTCAMP

### ANSWERS TO WEEK-3 HOMEWORK QUESTIONS

---

#### Q1 - SOAP vs Restful ?

---

Application Programming Interfaces (APIs) provide a secure and standardized way for different software to communicate to each other. In other words, an application can extract functionality or data from another piece of software and use it to enhance its own functionality or UX.  The communication method, how we make this communication, depends on how the API was built. The two most common methods are RESTful and SOAP methods.

Simple Object Access Protocol (SOAP) is a standard communication protocol system that uses XML technologies to build APIs and maintained by the World Wide Web Consortium (W3C). SOAP was first designed in order to allow applications running on different operating systems to communicate using different languages and technologies. So, it imposes built-in rules that increase its complexity and overhead, which can lead to longer page load times. However, these standards also offer built-in compliances that can make it preferable for enterprise scenarios. The built-in compliance standards include security, Atomicity, Consistency, Isolation, and Durability (ACID), which is a set of properties for ensuring reliable database transactions. A client can use SOAP APIs to create, retrieve, update or delete records, such as passwords, accounts, leads, and custom objects, from a server.

RESTful APIs follows REST (REpresentational State Transfer) architectural principles that uses a simpler, solitary, consistent and more flexible method for building APIs. In order to understand a RESTful approach, we need to understand REST principles first. REST  is a set of architectural principles attuned to the needs of lightweight web services and mobile applications by defining how to build APIs, which allow data to be communicated between web applications.   Because it's a set of guidelines, it leaves the implementation of these recommendations to developers.

A RESTful application must have these guidelines:
- A client-server architecture composed of clients, servers, and resources.
- Stateless client-server communication, meaning no client content is stored on the server between requests. Information about the session’s state is instead held with the client.
- Cacheable data to eliminate the need for some client-server interactions.
- The central feature that distinguishes the REST architectural style from other network-based styles is a uniform interface between components so that information is transferred in a standardized form instead of specific to an application’s needs.
- A layered system constraint, where client-server interactions can be mediated by hierarchical layers.
- Code on demand, allowing servers to extend the functionality of a client by transferring executable code (though also reducing visibility, making this an optional guideline).


Differences between SOAP and RESTful:

| SOAP | RESTful |
|---------|-----------|
| A type of protocol and consists of an official standard, so very strict. | An architectural style, so more flexible |
| Developing private APIs, especially for large enterprises, since SOAP allows data to be transferred in a decentralized, distributed environment and has lots of web security mechanisms  | Developing public APIs to access data |
| Using an underlying transport protocol other than HTTP: SMTP (Simple Mail Transfer Protocol) or JMS (Java Messaging Service) or TCP or another transport protocol, depending on your application.  | Access web services by using HTTP. |
| Return SOAP messages must be returned as XML documents—a markup language that is both human- and machine-readable.  | Return data in a variety of formats, including XML as well as plain text, HTML, and JSON. |
| Not cacheable by a browser, so it cannot be accessed later without resending to the API. | Cacheable for information that’s not altered and not dynamic because of working with staless operations, thanks to JSON |
| Ideal for internal data transfers and other sensitive tasks, because defines its own security. | Offers better support for browser clients, because inherits security measures from the underlying transport. |
| SOAP web services offer built-in security and transaction compliance that align with many enterprise needs, but that also makes them heavier.  | Lightweight, making them ideal for newer contexts like the Internet of Things (IoT), mobile application development, and serverless computing. |
| Working with stateful operations, so requires more server resources and bandwidth, it’s important if performing repetitive or chained tasks, like bank transfers. | Working with stateless operations, so uses limited server resources and less bandwidth. |
| Offers built-in retry logic to compensate for failed communications.  | Doesn’t have a built-in messaging system. If a communication fails, the client has to deal with it by retrying. There’s also no standard set of rules for REST. This means that both parties (the service and the consumer) need to understand both content and context. |
| Highly extensible through other protocols and technologies. In addition to WS-Security, supports WS-Addressing, WS-Coordination, WS-ReliableMessaging, and others on W3C. | Only support traditional web security mechanisms, such as HTTPS, Secure Socket Layer (SSL). |
| Uses services interfaces to expose the business logic. | Uses URI to expose business logic. |



---

#### Q2 - Difference between acceptance test and functional test ?

---

| Acceptance Test | Functional Test |
|----------------------|---------------------|
| Validates the software against customer expectations | Validates the functionality of the software |
| Typically a check list of behaviors and expected results that end-users must run through and also the first manual tests on the list. | Mainly a black box type of testing as source code is not considered during the testing process. |
 | Also known as **Beta testing** or **End-user testing** | Also known as **Specification-based testing** as it is completely based on program specifications. |
| This is the last and final step, performed after functional and regression testing. | Functional testing is performed before acceptance testing |
|  Usually done in cooperation with the customer, or by an internal customer proxy (product owner).The various stakeholders involved in this test process include business analyst, QA lead or Test Manager, requirements specialist (if any), and the business or product owner. |  Functional testing is just performed by Software or QA engineer. |
| Most often developed with the business case(s) in mind for finding the answer of the question “does the software work” from the business perspective. | Developed for testing each functionality of the application by providing certain inputs and validating the outputs against the functional requirements.  |
| A validation activity that asks questions like  *did we build the right thing?*,  *Is this what the customer really needs?* | A verification activity that asks questions like *did we build a correctly working product?*, *Does the software meet the business requirements?* |
| Test cases cover the typical scenarios under which we expect the software to be used.   | Test cases cover all the possible scenarios we can think of, even if that scenario is unlikely to exist "in the real world". When doing this type of testing, we aim for maximum code coverage.  |
| Must be conducted in a "production-like" environment, on hardware that is the same as, or close to, what a customer will use. | Can be conducted in any test environment we can grab at the time, it doesn't have to be "production" caliber, so long as it's usable. |
  
 
 With Acceptance testing, we test our application's abilities:
- *Reliability, Availability :* Validated via a stress test.
- *Scalability :* Validated via a load test.
- *Usability :* Validated via an inspection and demonstration to the customer. Is the UI configured to their liking? Did we put the customer branding in all the right places? Do we have all the fields/screens they asked for?
- *Security (or Securability) :* Validated via demonstration. Sometimes a customer will hire an outside firm to do a security audit and/or intrusion testing.
- *Maintainability :* Validated via demonstration of how we will deliver software updates/patches.
- *Configurability :* Validated via demonstration of how the customer can modify the system to suit their needs.


Functional testing consists of unit testing, smoke testing, integration testing, regression testing, etc.
- *Unit tests*
  - Tests individual functions
  - Stubs out all calls made within the function
  - Tests side effects and expected results
  - Good for libraries, helpers, private methods

- *Integration tests*
  - Tests flows
  - Tests side effects and expected results, often HTML, JSON, or XML responses in the case of web apps
  - Makes calls to external services (stubbed or QA services, never to production services)

- *Regression tests*
  - Tests current code against past test cases and environments
  - Tests that changes do not break existing code, or the environment for deploy

- *Smoke tests*
  - Tests calls
  - Tests expected results, often HTML, JSON, or XML responses in the case of web apps
  - Acts as a black box for testing to determine if a release was good from a high level typically


---

#### Q3 - What is Mocking ?

---

The idea of unit testing is that we want to test our code without testing the dependencies. This test allows you to verify that the code being tested works, regardless of it's dependencies. The theory is that if the code I write works as designed and my dependencies work as designed, then they should work together as designed. To achieve unit testing properly, we need mocking. **Mocking** is replacing real objects with the imitating (mock) objects by creating them during test process in order to provide you to be able to test what you write without having to address dependency concerns.  These mock objects will expect a certain method to be called with certain parameters and when that happens, it will return an expected result. 

There are essentially two main types of mock object frameworks, ones that are implemented via proxy and ones that are implemented via class remapping.
- A proxy object is an object that is used to take the place of a real object. In the case of mock objects, a proxy object is used to imitate the real object your code is dependent on. We create a proxy object with the mocking framework, and then set it on the object using either a *setter* or *constructor*. This points out an inherent issue with mocking using proxy objects. It means that we can't create the dependency by calling `new MyObject()` since there is no way to mock that with a proxy object. This is one of the reasons Dependency Injection frameworks like *Spring* have taken off. They allow us to inject your proxy objects without modifying any code.
	
- The second form of mocking is to remap the class file in the class loader. The mocking framework *jmockit* is a framework that currently gives this ability for mock objects. The concept is provided by the new `java.lang.Instrument` class. We tell the class loader to remap the reference to the class file and then, it will load. For example, if we have a class `Dependent` with the corresponding `.class ` file called `Dependent.class` and we want to mock it to use `Mock` instead. By using this type of mock objects, we will actually remap in the *classloader* the reference from `Dependent` to `Mock.class`. We are able to mock objects that are created by using the `new` operator. This remapping approach provides more power than the proxy object approach, however it is also harder and more confusing to get going given the knowledge of classloaders we need to really be able to use all its features.


---

#### Q4 - What is a reasonable code coverage % for unit tests (and why) ?

---

Code coverage is an objective measurement, so once we see our coverage report, there is no ambiguity about whether standards have been met are useful.  It has a clear relationship to how well-tested the code is, which in turn is our best way to increase confidence in its correctness. Code coverage is a measurable approximation of immeasurable qualities we care about.

Following specific cases where having an empirical standard could add value:
- *Satisfying stakeholders :* Providing measurable standards and explaining how they reasonably approximate actual goals is better.
- *Normalize team behavior :* If you are working on a team where multiple people are writing code and tests, there is room for ambiguity for what qualifies as "well-tested." Find a metric you can all agree on and accept it as a reasonable approximation. This is especially (but not exclusively) useful in large teams,  without objective measurements, it is easy for group behavior to become inconsistent, even if everyone is acting in good faith.
- *Keeping yourself on right track :* Even if you're the only developer and only stakeholder for your project, you might have certain qualities in mind for the software. Instead of making ongoing subjective assessments about how well-tested the software is , you can use code coverage as a reasonable approximation, and let machines measure it for you.

We need an approximation to begin with, so any number we pick is going to be inherently approximate.
Some numbers that can be choosen:
- **100% :** We might choose this because you want to be sure everything is tested. This doesn't give us any insight into test quality, but tells us that some test of some quality has touched every statement (or branch, etc.) 
	
- **99% (or 95%) :** Appropriate in cases where we want to convey a level of confidence similar to 100%, but leave ourself some margin to not worry about the occasional hard-to-test corner of code.
	
- **80% :**   The intent here is to show that most of your code is tested. This is appropriate for middle-ground cases where "well-tested" is not a high priority (not want to waste effort on low-value tests), but is enough of a priority that we'd still like to have some standard in place.
	
The role of these standards is to increase confidence in correctness, and *numbers below 80%* aren't particularly confidence-inspiring. 

Correctness is the goal, however code coverage is just information; it may be relevant to other goals. For instance, if we're concerned about maintainability, we probably care about loose coupling, which can be demonstrated by testability, which in turn can be measured (in certain fashions) by code coverage. So our code coverage standard provides an empirical basis for approximating the quality of "maintainability" as well.


---

#### Q5 - HTTP/POST vs HTTP/PUT ?

---

| PUT  |  POST |
|-------|--------|
| Request is made to a particular resource which is the enclosed entity be stored under the supplied URI. If the URI refers to an already existing resource, an update operation will happen and if the URI does not point to an existing resource, then the server can create the resource with that URI. | Requests that a web server accepts the data enclosed in the body of the request message, most likely for storing it. It essentially means that POST request-URI should be of a collection URI. |
| The syntax is  `PUT/article/{article-id}` | The syntax is `POST/articles` |
| Idempotent. So if we send PUT request multiple times, the result will remain the  equivalent to single request modification. | NOT idempotent. So if you send POST request N times, you will end up having N resources with N different URIs created on server. |
| The client decides which URI resource should have | The server decides which URI resource should have. |
| Is called when you have to modify a single resource which is already a part of resources collection. PUT overwrites the resource in its entire resource. We can use PATCH if request updates part of the resource. | Is called when you have to add a child resource under resources collection.   POST is often used when uploading a file or when submitting a completed web form. |
| PUT method response can be cached | POST method responses are not cacheable. |
| Generally, use PUT for UPDATE operations in practice. |  Always use POST for CREATE operations. |
| Works as specific | Works as abstract. |



---

#### Q6 - What are the Safe and Unsafe methods of HTTP ?

---

**Safe HTTP methods** are not expected to change any resource on the server and **Unsafe HTTP methods** are expected to change some resource on the server.  In other words, a method is safe if it leads to a read-only operation. Safe  HTTP methods are  *GET*, *HEAD*, *TRACE* or *OPTIONS*.  Unsafe methods are *PUT*, *DELETE*, *POST* and *PATCH*.

All safe methods are also idempotent, but not all idempotent methods are safe. For example, *PUT* and *DELETE* are both idempotent but unsafe methods.

Even if safe methods have a read-only semantic, servers can alter their state, for instance they can log or keep statistics. By calling a safe method, the client doesn't request any server change itself, and therefore won't create an unnecessary load or burden for the server. Browsers can call safe methods without fearing to cause any harm to the server; this allows them to perform activities like pre-fetching without risk. Web crawlers also rely on calling safe methods.

Safe methods don't need to serve static files only; a server can generate an answer to a safe method on-the-fly, as long as the generating script guarantees safety: it should not trigger external effects, like triggering an order in an e-commerce Web site. The application on the server is responsible to implement the safe semantic correctly. In particular, an application should not allow *GET* requests to alter its state.



---

#### Q7 - How does HTTP Basic Authentication work ?

---

In the context of a HTTP transaction, basic access authentication is a method for an HTTP user agent to provide a user name and password when making a request. HTTP Basic authentication uses static, standard HTTP headers which means that no handshakes have to be done in anticipation.

Basic-Auth makes is that username/password is passed in the request headers instead of the request body (GET/POST). As such, using basic-auth+https is no less or more secure than a form based authentication over HTTPS. Basic Auth over HTTPS is good, but it's not completely safe.

*HTTP Basic  Authentication* use a four step process to authenticate users.

- First HTTP client makes a request to the web server. Request method can be any method. 
- If web server sees that the requested resource need authentication to access then it sends backs 401 Unauthorized status code along with WWW-Authenticate header. And then client displays a dialog box to take username and password as input. 
- Once the credentials has been entered, the client sends it using the Authorization header. 
- If the credentials are correct then server responds with 200 status code and Authentication-Info header. If client sends wrong credentials in the Authorization request then server again responds with 401 status code. The client is allowed to try again and again.
	

We can look at the authentication headers in depth for Basic authentication.
- **WWW-Authenticate :** This header is assigned to a realm. It is compulsory that this header will contain a realm directive. Realm is displayed in the dialog box. Servers use realm to group different parts of the server(assigns same realm, username and password other resources on the same and deeper level). Browser saves credentials for all realm’s. Whenever browser receives a *WWW-Authenticate* response with a realm already saved, it will automatically send the credentials without the knowledge of user. Browser also sends Authorization request directly to the URLs deeper than a level whose realm and credentials are known. This creates a session among the URls with same realm and also URIs deeper to a saved realm.

`WWW-Authenticate: realm="Videos"`

- **Authorization :** Browser sends the username and password using this header. Username and password are joined together with a colon in between and then encoded using base-64 encoding method. So if the username is “narayanprusty” and the password is “qnimate” than a string “narayanprusty:qnimate” is generated and then encoded using base-64 that results to the string “D08mRvgvbhDsU”. And this final string is sended to the server.

`Authorization: Basic D08mRvgvbhDsU`

- **Authentication-Info :** This header is optional. Some web servers send this header assigned to some information about the session and future authentication requests.

Some organizations use proxy servers to authenticate users before allowing them to access the web server resources. The same mechanism is used by proxies to authenticate users but header and status codes are changed. Changes are:
- *Response status 407 :* 407 response status code is sended instead of 401
- *Proxy-Authenticate :* Proxy-Authenticate is used instead of WWW-Authenticate.
- *Proxy-Authorization :* Proxy-Authorization is used instead of Authorization.
- *Proxy-Authentication-Info :* Proxy-Authentication-Info is used instead of Authentication-Info.



---

#### Q8 - Define RestTemplate in Spring ?

---

RestTemplate is a class which is designed to call REST services inside a Spring application. By the use of RestTemplate class, we can write methods which invoke the API from it to consume the data and for further processing, also we can get data from third party or other application if we have any dependency. We can use the exchange() method to consume the web services for all HTTP methods. RestTemplate is present inside the `spring-boot-starter-web` dependency in Spring Boot. If we want to use it, we can simply *Autowired* its object and use its different methods available to make any type of request from the application. So Spring Container now will take care of all the dependency for us. We can make one method inside which we can write the logic to use RestTemplate to call the endpoint. 

```
@Autowired
private RestTemplate name_of_variable;

```

```
public class Test{
@Autowired
private RestTemplate restTemplate;
}

```

First we have to auto wire the RestTemplate object inside the class we want to make use of RestTemplate, after this we can use the methods to call the API.

```
final HttpEntity<String> request = new HttpEntity<>(json.toString(), your_headers);
ResponseEntity<String> response = this.restTemplate.exchange(your_URL, HttpMethod.POST, your-REQUEST, class_type.class);

```

*RestTemplate* provides higher-level methods for each of the HTTP methods which make it easy to invoke RESTful services.
The names of most of the methods are based on a naming convention:
- the first part in the name indicates the HTTP method being invoked
- the second part in the name indicates returned element.

For example, the method `getForObject()` will perform a GET and return an object.

*Available methods for executing GET APIs* are:

`getForObject(url, classType)` – retrieve a representation by doing a GET on the URL. The response (if any) is  returned directly without attached to given class type.

`getForEntity(url, responseType)` – executes a GET request and returns an object of `ResponseEntity` class that contains both the status code and the resource as an object.

`exchange(url, httpMethod, requestEntity, responseType)` – execute the specified RequestEntity and return the response as ResponseEntity containing both the HTTP status code and the resource as an object.

`execute(url, httpMethod, requestCallback, responseExtractor)` – execute the httpMethod to the given URI template, preparing the request with the RequestCallback, and reading the response with a ResponseExtractor.

*Available methods for consuming POST APIs* are:

`postForObject(url, request, classType)` – creates the given object using HTTP POST method and returns the representation found in the response as given class type.  and returns an entity. ???

`postForEntity(url, request, responseType)` – POSTs the given object to the URL, and returns the response as ResponseEntity.

`postForLocation(url, request, responseType)` – POSTs the given object to the URL, and returns the value of the Location header. returns the location of the newly created resource. ???

`exchange(url, requestEntity, responseType)`

`execute(url, httpMethod, requestCallback, responseExtractor)`

*Other available methods* are:

`put(url, request)` – Updates a resource for a given URL using the HTTP PUT method.

`delete(url)` – deletes the resource at the specified URL using the HTTP DELETE method.

`headForHeaders()` : executes a HEAD request and returns all HTTP headers for the specified URL.

`optionsForAllow()` : executes an OPTIONS request and uses the Allow header to return the HTTP methods that are allowed under the specified URL.




---

#### Q9 - What is idempotant and which HTTP methods are idempotant ?

---

When we design the REST APIs, we must realize that the API consumers can make mistakes. Consumers can write the client code in such a way that there can be duplicate requests coming to the API. These duplicate requests may be unintentional as well as intentional sometimes (foe example, due to timeout or network issues). Non-idempotent operations can cause significant unintended side-effects by creating additional resources or changing them unexpectedly. When a business relies on the accuracy of its data, non-idempotency posts a significant risk.  We have to make our APIs fault-tolerant in such a way that the duplicate requests do not leave the system unstable.

An idempotent HTTP method is a method that can be invoked many times without the different outcomes. The result should always be the same. Idempotency essentially means that the result of a successfully performed request is independent of the number of times it is executed. While idempotent operations produce the same result on the server (no side effects), the response itself may not be the same (e.g. a resource's state may change between requests).

If we follow the REST principles in designing our APIs, we will have automatically idempotent REST APIs for *GET*, *PUT*, *DELETE*, *HEAD*, *OPTIONS*, and *TRACE* methods. Only *POST API*s will not be idempotent.

There is an issue with *DELETE*. The issue is, if successful would normally return a 200 (OK) or 204 (No Content), will often return a 404 (Not Found) on subsequent calls, unless the service is configured to "mark" resources for deletion without actually deleting them. However, when the service actually deletes the resource, the next call will not find the resource to delete it and return a 404. However, the state on the server is the same after each *DELETE* call, but the response is different.



---

#### Q10 - What is DNS Spoofing ? How to prevent ?

---

DNS (Domain Name Service) Spoofing is the process of poisoning entries on a DNS server to redirect a targeted user to a malicious website under attacker control. The DNS attack typically happens in a public Wi-Fi environment but can occur in any situation where the attacker can poison ARP (Address Resolution Protocol) tables and force targeted user devices into using the attacker-controlled machine as the server for a specific website. It’s the first step in a sophisticated phishing attack on public Wi-Fi, and it can also trick users into installing malware on their devices or divulge sensitive information.

Any user that accesses the internet from public Wi-Fi is vulnerable to DNS spoofing. To protect from DNS spoofing, internet providers can use *DNSSEC (DNS security)*. When a domain owner sets up DNS entries, DNSSEC adds a cryptographic signature to the entries required by resolvers before they accept DNS lookups as authentic.
Standard DNS is not encrypted, and it’s not programmed to ensure that changes and resolved lookups are from legitimate servers and users. DNSSEC adds a signature component to the process that verifies updates and ensures that DNS spoofing is blocked. DNSSEC has gained more popularity recently as DNS spoofing threatens to breach user data privacy across any public Wi-Fi.


We can also use encryption to protect against DNS spoofing. Encryption methods generally offer two key advantages:
- Data is protected from unauthorized access by third parties
- It ensures the authenticity of the communicating party
	
The last point is critical in the fight against DNS spoofing. If an attacker tries to pretend to be a legitimate host, this will result in a certificate error on the user side and the spoofing attempt will be detected.

- **Using transport encryption :** For a basic level of security, you should secure as many connections as possible using the common transport encryption method. Preferably, websites should be accessed in the browser using HTTPS. The popular browser add-on *HTTPS Everywhere* secures connections to websites that transfer content over both HTTP and HTTPS. You should also make sure that the connections configured in your email client (e.g. IMAP, POP3, and SMTP connections) use secure protocols such as TLS and SSL.
Since the malicious host does not have the security certificate that the real host would have, the browser and email client will send an alert when a connection is established. This gives you a chance to terminate the connection and implement additional security measures.
- **Encrypting DNS traffic :** While transport encryption secures your data transfer, the connection to the DNS server is still vulnerable and is considered to be the weakest link. However, there are dedicated solutions for DNS request encryption on the user side. The most notable of these are *DNSCrypt, DNS over HTTPS (DoH), and DNS over TLS (DoT)*. These technologies all provide protection against dangerous man-in-the-middle attacks. However, not one of these three solutions comes pre-integrated with any standard operating systems in a way that is suitable for the mass market. Furthermore, the DNS server must also support the respective security technology for DNS encryption to work.

- **Using a virtual private network :** In addition to transport encryption and securing the DNS server connection, using a *Virtual Private Network (VPN)* can also help to protect against DNS spoofing. When using a VPN, all connections are routed through an encrypted tunnel. However, you should keep in mind that the IP address of a DNS server can still be stored in most VPN programs. If this is a malicious address, the VPN’s protection against DNS spoofing will be rendered ineffective.
- **Using a public DNS resolver network :** One of the most effective security measures you can take against DNS spoofing is using a public DNS resolver. The setup is simple enough for practically any user to be able to configure their own device to use. All you have to do is change the DNS server entered on your system. Using a public DNS resolver provides also the following advantages: 
  - *High-speed DNS responses :* Large DNS resolver networks operate dozens of servers around the world. Thanks to Anycast routing, the physically closest server is always used for name resolution which is reflected in the short response times.
 
  -	*High level of data protection and anonymity :* Many internet service providers sell their customers’ data that is generated by DNS traffic. These popular public resolvers generally store little to no user data, offering a high level of data protection and anonymity.
  -	*Does not enforce censorship measures :* State censorship regulations are only valid within national borders. Internet service providers usually operate within their customers’ country of residence and are required to enforce state censorship. However, a resolver network based abroad can offer its services worldwide without having to consider state-mandated censorship.
  - *Supports modern security standards :* Large public DNS resolver networks specialize in responding to DNS requests. They are often trailblazers in using modern security standards, such as DNSSEC, DoH, DoT, and DNSCrypt.
  - *Blocks malicious domains :* Using a public DNS resolver network can also help protect against malware and phishing, as these keep blacklists of known malicious domains. Attempting to access these domains will result in the user being redirected to a warning page.


---

#### Q11 - What is content negotiation ?

---

The REST resources can have multiple presentations, mostly because there may be different clients expecting different representations. Asking for a suitable presentation by a client is referred to as **content negotiation**.
HTTP has provisions for several mechanisms for *content negotiation* — the process of selecting the best representation for a given response when there are multiple representations available.

If the selection of the best representation for a response is made by an algorithm located at the server, it is called **server-driven negotiation**. If that selection is made at the agent or client-side, it is called **agent-driven negotiation**.

Practically, we will not find much usage of server-side negotiations because, in that way, we have to make a lot of assumptions about the client’s expectations, like the client context or how the client will use the resource representation, which are almost impossible to determine. Also, the server-driven negotiation makes the server-side code more complex, unnecessarily. Hence, most REST API implementations rely on agent-driven content negotiations. Agent-driven content negotiation depends on the usage of HTTP request headers or resource URI patterns. At server side, an incoming request may have an entity attached to it. To determine it’s type, server uses the HTTP request header `Content-Type`. Some common examples of content types are `text/plain`, `application/xml`, `text/html`, `application/json`, `image/gif`, and `image/jpeg`.



---

#### Q12 - What is statelessness in RESTful Web Services ?

---

In RESTful Web Services, each request from the client to the server must contain all of the necessary information to understand the request. The server cannot take advantage of any stored context on the server.The application’s session state is therefore kept entirely on the client. The client is responsible for storing and handling the session related information on its own side and also sending any state information to the server whenever it is needed. There should not be any session affinity or sticky session between the client and the server.

This restriction related to the server that can not store any state about the client session on the server-side  is called **Statelessness**. In other words, every HTTP request happens in complete isolation.  To enable clients to access these stateless APIs, it is necessary that servers also should include every piece of information that the client may need to create/maintain the state on its side. For becoming stateless, servers can not store even authentication/authorization details of the client. Client provides authentication credentials with each request.
Thus each request MUST be stand alone and should not be affected by the previous conversation that happened with the same client in past.

It is important to understand the between the application state and the resource state. Both are completely different things:
- *Application state* is server-side data that servers store to identify incoming client requests, their previous interaction details, and current context information.
- *Resource state* is the current state of a resource on a server at any point in time – and it has nothing to do with the interaction between client and server. It is what we get as a response from the server as the API response. We refer to it as resource representation.

REST statelessness means being free from the application state.

There are some very noticeable advantages of having REST APIs stateless.
- Statelessness helps in scaling the APIs to millions of concurrent users by deploying it to multiple servers. Any server can handle any request because there is no session related dependency.
- Being stateless makes REST APIs less complex – by removing all server-side state synchronization logic.
- A stateless API is easily cacheable. Specific softwares can decide whether or not to cache the result of an HTTP request just by looking at that one request. There’s no nagging uncertainty that state from a previous request might affect the cacheability of this one. It improves the performance of applications.
- The server never loses track of “where” each client is in the application because the client sends all necessary information with each request.


---

#### Q13 - What is CSRF attack? How to prevent ?

---

When a malicious site or program causes a user's browser to perform an unwanted action on a trusted site after the user is authenticated, it is called **Cross Site Request Forgery ( CSRF )**. Any malicious action is limited to the capability of the website to which the user is authenticated. CSRF is also known as **XSRF, Sea Surf, Session Riding, Hostile Linking, One-Click Attack**.

In order for an attacker to carry out a CSRF attack, several things need to be true:
- There is an action in the application which an attacker wants to take – like changing a password, transferring funds, and so on.	
- There are not unpredictable request parameters – the attacker can guess (or knows) all of the parameters which the application expects to see from this type of request.
- The action can be carried out by HTTP request(s) and it relies only on cookies in order to verify that the request is coming from the user.

CSRF can impact web applications which use cookies, browser authentication, or client side certificates to authenticate users. Essentially it can occur in any case where the application automatically appends a users' credentials or identity to a request.

A CSRF attack can either leverage a GET request or a POST request (though a POST request is more complicated and is thus uncommon). Either one needs to start with an attacker tricking a victim into loading or submitting the information to a web application. This can take place in a number of ways – for example via a phishing link. Alternatively, similar to XSS (Cross-site scripting), CSRF can be a stored vulnerability. Stored CSRF occurs when an attacker stores the attack in a field which accepts HTML such as an IMG or IFRAME tag. This would mean that anyone who views the page could be impacted.  The exploit can be disguised as an ordinary link or hidden in an image tag.

For example, as an *ordinary link* on a webpage :

` <a href=“malicious link”>Unsubscribe here</a>`

as an *image tag* :

 `<img src=“malicious link” width=“0” height=“0” border=“0”>`

For instance, Rose might login to her online banking portal while checking her email. Then, she may click a link in a phishing email (like a link-shortening site) which would include a request for Jane's bank to transfer money to an account the attacker controls. Since she is already authenticated by her bank, they automatically carry out the transaction, believing that because it is being requested by Rose's browser that she has authorized it.

Some defense mechanism against CSRF Attacks:

- **Choose Your Frameworks Carefully :** Use frameworks which have built in protections against CSRF, like .NET. Correct configuration is key. If the framework you're using doesn't have protection, you can add protection with Anti-CSRF Tokens.

- **Use Anti-CSRF Tokens :** Tokens (also known as synchronizer token patterns) are a server-side protection where the server provides a user's browser with a unique, randomly generated token and checks each request to see if the browser sends it back before carrying out a request. This token is sent via a hidden field and should be a non-predictable, random number which expires after a short time and cannot be reused. Depending on the sensitivity of the page, different tokens can be used for each request, or simply for different forms. The tokens should be compared in a safe way (such as by comparing hashes) and should not be sent in an HTTP get request so they are not a part of the URL and cannot leak via the Referrer header.

- **Use the SameSite Flag in Cookies :** The `SameSite` flag marks a cookie so it can only be sent for requests which originate from the same domain. Essentially if www.Abank.com wants to make a request to www.Abank.com/updatepassword, it's allowed to. But if www.maliciousdomain.com wants to make a request to www.Abank.com/updatepassword, it can't send the session cookie and therefore cannot carry out the attack. Most browsers now support this flag, but not all. It should be part of a comprehensive defense strategy.

- **Involve the User in the Transaction :** For sensitive actions such as money transfers or password changes, require the user to take action (such as *CAPTCHA*, one-time tokens, or re-authentication).

- **Verify the origin with standard headers** Determine where the request originates and where it's targeted to ensure they match
	
- **Use a custom request header** Hence, without the header the site will not accept the request.
	
- **Double submit cookies** Essentially a second, randomly generated and unknown – to the attacker – parameter which an attacker has to submit with a request in order for it to be successful.



---

#### Q14 - What are the core components of the HTTP request and HTTP response ?

---

An **HTTP request** has 3 core components :
1. **A request line :** In the request line we place the *HTTP method* to be used, the *URI* of the request and the *HTTP protocol Version* to be used.  
	
     `HTTP-METHOD  URI  HTTP-Version`

  - *HTTP methods* or *Verb* indicate what kind of action our client wants to perform, whether he wants to read a resource, or if he wants to send information to the API, etc. 
  - The *URI (Uniform Resource Identifier)* refers to the address where the resource is located. 
  -  *HTTP protocol* or *HTTP Version* refers to which HTTP protocol will be used, this is because there are      several versions of the HTTP protocol.
           
  An example of a request line:

     `GET /api/authors HTTP/1.1`

2. **Request Header :** It indicates where the headers of the request are located.Headers are *metadata* that are sent as key-value pairs in the request to provide information about the request. Each header is specified with a name, then two points, and then followed by the value of that header. For example, the header can be  client ( or browser) type, format supported by client, format of message body, cache settings etc.
  An example of a header:
	
	`Host: en.wikipedia.org`
	
	The name of the header is Host, and its value is en.wikipedia.org. The Host header indicates the domain of the server.
	
	There may be multiple headers in the header of the request. 
	
	An example with its request line and header:
	```
	GET /api/autores HTTP/1.1
	Host: en.wikipedia.org
	Cache-Control: no-cache
	```
	
	The first line is the request line, below this is the header of the request, which is composed of several individual headers, host and cache-control in our case. The Host and Cache-Control headers are standard headers, which already have a well-defined purpose. 
	
	We are also free to use our own custom headers. When we need to express our metadata of our request, we can use custom headers. All we need to do is send them in the header of the HTTP request.
	
	
3. **A Request body**, *which is optional :* This shows where we put additional information that we are going to send to the server. In the body of the request we are free to place virtually whatever we want. From the username and password of a person trying to login to our system, to the answers of a complex form of a survey. The body is quite important, because it represents, in many cases, the content per se that one wants to transmit. 
	
	GET requests do not use a body, because one does not tend to send many complex data when reading information. In the case of the POST method, we usually use the body of the request to place what we want to send.
	
	An example of a request body:
	
	`Hello`
	
	The body of the request is to send virtually anything we want, from a simple greeting, to a little more structured information.
	
An HTTP request with its three core components:

```
POST /api/authors HTTP/1.1
Host: myWebApi.com
Content-Type: application/json
Cache-Control: no-cache

{
  "Name": "Felipe Gavilán",
  "Age": 999
}
```
	
A blank line is the separation between the HTTP header and the body.



An **HTTP Response** has 3 core components: 

1. **Status Line :** It contains three important components 
   - *HTTP Version :* The HTTP version number shows the HTTP specification to which the server has tried to make the response message comply. 
   - *HTTP Response Code :* This indicates Server status for the requested resource. It is a 3 digit number that shows the conclusion of the Request. For example,  404 means resource not found and 200 means response is ok.
   - *Reason-Phrase :* Also known as *Status Text* as it summarizes the Status Code in human-readable form.

2. **Response Header :**  The Response Header contains the information, *metadata*, as key-value pairs about the content that is being returned in response together with data about the Server that sent it.  This information helps the Client/Browser in deciding in what way the response data would be used. The most popular response headers are Content-Length, Content-Type, Date, Server, Set-Cookie etc.  The Server can send as many headers as needed. Every header is sent as a key-value pair separated by a colon ( : ).  

3. **Body (Optional) :**   In case of a successful response, Resource representation is used to serve the Client/User with the resource asked for in the request. Although the body is optional, it is one of the most fundamental parts of the communication between the Client and Server and is sent most of the time. The body carries the data and can be in one of the many formats such as json, html, image, etc. which is accordingly specified in the headers. 


---


 

