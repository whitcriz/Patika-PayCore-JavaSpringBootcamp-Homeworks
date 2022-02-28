## Patika & PayCore Java Spring Bootcamp


### Week-5 Homework Questions & Answers

---

#### Q1 - What are Authentication and Authorization ?

---

**Authentication** identifies and verifies who the user or system is by checking the user or system identity. It is used by both server and client. The server uses authentication when someone wants to access the information, and the server needs to know who is accessing the information. The client uses it when he wants to know that it is the same server that it claims to be.

In a typical authentication scheme, the user provides some form of identification that proves their identity. Most commonly, this authentication requirement is a specific username and password combination. The username tells the system who is logging in, while the password proves their identity. If we need more bulletproof strategies rather than this authentication, we can use multiple authentication factors and this may require a code sent to a user's phone or cards or biometric identifier such as retina scans, voice recognition, and fingerprints in addition to a password.  Then the system will check it's authorization to check whether it is allowed to look at the resources been attempted to access. 

After Authentication process, **Authorization** process comes to the stage for checking which resources the user can access and how the user can use these resources. Authorization needs user’s privilege or security levels. User roles and categories help network administrators more easily determine which users should have authorization for specific resources. In some cases, there is no authorization; any user may be use a resource or access a file simply by asking for it. Most of the web pages on the Internet require no authentication or authorization.



---

#### Q2 - What is Hashing in Spring Security ?

---

Storing account passwords as plain text makes our applications vulnerable to attacks like *SQL Injection* . When an attack happens, malicious user would make operations by imitating the users, and because most people use the same password in different platforms which means that other user accounts in different platforms are at risk becaus of our application vulnerability. For these security risks, we need to store passwords as hashed values by generating them in one-way hashing functions, or known hashing algorithms.  **Hashing** is the process of generating a fixed-length result, value from the password by the hashing function. Then we need to store non-reversible hash values in the database. Every time a user tries to authenticate, we compare the hash value to the hash of the password that is typed by the user.  

One-input hashing functions such as *MD5*,*SHA-family* like the most known *SHA-256* of *SHA-2*, are not safe enough to *Rainbow Table* attack. Besides, billions of hash calculations can be performed in a second with modern hardware and so each password individually can be cracked easily. Hence, developers needed an additional random and unique input, also known *salt* values, for the hashing function. We can run through the hash function with the salt and the password input combination and produce a unique hash. We need to store salt with the hash value in the database. During the authentication process, the stored hash value would be compared to the hash of the stored salt and the password that is typed by the user. *Rainbow Tables* are no longer effective with the unique salt value because unique hash values is generated even with the same passwords. Hashing functions uses *salt* and avaliable in Spring Security are *bcrypt*, *PBKDF2*, *scrypt* and *argon2*.

- *bcrypt* is a hashing algorithm that is implemented by `BCryptPasswordEncoder`  and based on Blowfish cipher to hash the passwords. This algorithm can be iteratively applied to passwords in order to offset advances in hardware processing speeds, making it harder to brute-force, so it is deliberately slow. Using *bcrypt* with Spring just needs to start an instance of the `BCryptPasswordEncoder`. We will use  two main methods from the encoder. The *encode* method generates the hash value, and the *matches* method compares a password and a *bcrypt hash* to figure out if the password matches the hashed value.
	
```
// Create an encoder with strength 16
BCryptPasswordEncoder encoder = newBCryptPasswordEncoder(16);
String result = encoder.encode("myPassword");
assertTrue(encoder.matches("myPassword", result));
```
	
- *PBKDF2* is a hashing algorithm that is implemented by `Pbkdf2PasswordEncoder` to hash the passwords. In order to defeat password cracking, PBKDF2 is a deliberately slow algorithm and also  a good choice when FIPS certification is required.
	
```
// Create an encoder with all the defaults
Pbkdf2PasswordEncoder encoder = newPbkdf2PasswordEncoder();
String result = encoder.encode("myPassword");
assertTrue(encoder.matches("myPassword", result));
```
	
- *scrypt* is  password based hashing function that is implemented by `SCryptPasswordEncoder` to hash the passwords. Due to memory constraints, large scale hardware brute force attacks against scrypt can be extremely expensive. However, we will also need to add a dependency to *Bouncy Castle Core* with the Spring Security. The *Bouncy Castle Crypto* package is a Java implementation of cryptographic algorithms and it is used by Spring for their implementation of the `SCryptPasswordEncoder`.
	
```
// Create an encoder with all the defaults
SCryptPasswordEncoder encoder = newSCryptPasswordEncoder();
String result = encoder.encode("myPassword");
assertTrue(encoder.matches("myPassword", result));
```
	
- *Argon2* hashing algorithm is implemented by `Argon2PasswordEncoder` to hash the passwords. In order to defeat password cracking on custom hardware, *Argon2* is a deliberately slow algorithm that requires large amounts of memory. The current implementation of the `Argon2PasswordEncoder` requires `BouncyCastle`.
	
```
// Create an encoder with all the defaults
Argon2PasswordEncoder encoder = newArgon2PasswordEncoder();
String result = encoder.encode("myPassword");
assertTrue(encoder.matches("myPassword", result));
```
 

The default `PasswordEncoder` was `NoOpPasswordEncoder` that is plain text passwords, before *Spring Security 5.0*. Because the best practice for storing password will change again and it is hard to change easily for many applications using old password encodings, *Spring Security* represents **`DelegatingPasswordEncoder`** for using both modern, even with the current password storage options, and legacy formats and also upgrading the encodings later. We can easily start an instance of `DelegatingPasswordEncoder` using `PasswordEncoderFactories`. The password format is :

`{id}encodedPassword`

`id` identifies `PasswordEncoder` type and `encodedPassword` is the encoded hash value for the selected *PasswordEncoder*. If the *id* cannot be found, the *id* will be null.  Some Spring Security supporting  hashing algorithms password format examples of the same password which is "password" are  :
	
-  When matching this password would delegate to `BCryptPasswordEncoder`:

`{bcrypt}$2a$10$dXJ3SW6G7P50lGmMkkmwe.20cQQubK3.HZWzG3YB1tlRy.fqvM/BG` 

- When matching the password would delegate to `NoOpPasswordEncoder`  :

`{noop}password`

- When matching the password would delegate to `Pbkdf2PasswordEncoder` :

`{pbkdf2}5d923b44a6d129f3ddf3e3c8d29412723dcbde72445e8ef6bf3b508fbf17fa4ed4d6b99ca763d8dc`

- When matching this password format would delegate to `SCryptPasswordEncoder` :

`{scrypt}$e0801$8bWJaSu2IKSn9Z9kM+TPXfOc/9bdYSrN1oD9qfVThWEwdRTnO7re7Ei+fUZRJ68k9lTyuTeUp4of4g24hHnazw==$OAOec05+bXxvuu/1qZ6NUR+xQYvYv7BeL1QxwRpY5Pc= `

- When matching this password would delegate to `StandardPasswordEncoder` :

`{sha256}97cde38028ad898ebc02e690819fa220e88c62e0699403e94fff291cfffaf8410849f27605abcbc0`

The `{id}` and the mapping of the *id* to the `PasswordEncoder` provided in the constructor identifies mathching. By default, the result of invoking `matches(CharSequence, String)` with a password and an id that is not mapped (including a null id) will result in an `IllegalArgumentException`. This default behavior can be customized using 

`DelegatingPasswordEncoder.setDefaultPasswordEncoderForMatches(PasswordEncoder)`



---

#### Q3 - What is Salting and why do we use the process of Salting ?

---

**Salting** is the process of generating random ve unique bytes, also known as salt, and using this salt value addition to the password as input in the hash funtion. Randomly generated salt values need to be  saved and stored with the user's password and during authentication process, the hash of the stored salt and the password that is typed by the user would be compared the hashed password in the database. 

Billions of hash calculations can be performed in a second with modern hardware and so each password individually can be cracked easily. Just hashing with one input, password, could be vulnerable for the *Rainbow Table* attack. For this attack, passwords are computed once and stored in a lookup table, called *Rainbow Table*, rather than guessing each password everytime. Especially, when different users use the same passwords, we  will have the same hash values. However, with unique and random salt values, every password and salt combination will have different hash values even if the passwords are the same. We use Salting to reduce the effectiveness of *Rainbow Tables*.

Some hashing functions which uses *salting* and avaliable in Spring Security are *bcrypt*, *PBKDF2*, *scrypt** and *argon2*.



---

#### Q4 - What is “intercept-url” pattern ?

---

*<intercept-url> element* identifies the set of URL patterns that our application is interested in and  configures how they should be handled in the application. This element constructs the *FilterInvocationSecurityMetadataSource* bean used by the *FilterSecurityInterceptor*. If we need to access specific URLs such as HTTPS, we need to configure a *ChannelProcessingFilter* with <intercept-url> element. While matching the identified patterns during an incoming request, match is done in the order in which the elements are declared. We can say that the most detailed patterns should come first and the most general should come last.

We can use this element with `<filter-security-metadata-source>` as a parent element if we need to configure just a `FilterChainProxy` rather than using <http> element with extra filter chains. The intercept-url elements used with <filter-security-metadata-source>  should only contain pattern, method and access attributes. Otherwise we will get a configuration error. If we need these extra filter chains and other configurations, we can use `<intercept-url>` with the `<http>` element as parent element.

<intercept-url> element has attributes for configuration :

- `access` : A comma-separated access attributes list of the security configuration attributes (role names etc.) that will be stored in `FilterInvocationSecurityMetadataSource` for the identified URL pattern-method 
	
- `method` : HTTP method that will be used in together with the pattern and servlet path(optional) in order to match an incoming request. If we do not define a method here, any method will match. If the same pattern is identified with and without a method, the method-defined one will be prior to the other one.

- **`pattern`** : Defines the URL path and relies on the `request-matcher` attribute from the parent <http> element. As default, it will be to ant path syntax.

- `request-matcher-ref` : A reference to *RequestMatcher* which determines if the corresponding <intercept-url> is used.

- `requires-channel` :  Can be *"http"* or *"https"* depending on whether a particular URL pattern should be accessed over HTTP or HTTPS respectively. We can also use *"any"* value when we have no preference. A `ChannelProcessingFilter` will be added to the filter stack and its additional dependencies added to the application context, if we define this attribute on any <intercept-url> element. When there is a `<port-mappings>` configuration, it determines the ports used for redirecting to HTTP/HTTPS with the `SecureChannelProcessor` and `InsecureChannelProcessor` beans. 

- `servlet-path` : Only avaliable when *`request-matcher = mvc`*. Used  in combination with the *pattern* and *HTTP method* to match an incoming request. This value is only required in the two circumstances :
  - There are two or more *HttpServlet*'s registered in the `ServletContext` that have mappings starting with `'/'` and are different
  - The pattern starts with the same value of a registered *HttpServlet* path, excluding the default (root) *HttpServlet* ` '/'`


An example of using   **`<intercept-url>` pattern** attribute :

```
<http realm="Contacts Realm"use-expressions="false">
    <intercept-url pattern="/index.jsp"access="IS_AUTHENTICATED_ANONYMOUSLY"/>
    <intercept-url pattern="/login.jsp*"access="IS_AUTHENTICATED_ANONYMOUSLY"/>
    <intercept-url pattern="/admin/*"access="ROLE_ADMIN"/>
    <intercept-url pattern="/secret/*"access="ROLE_SECRET"/>
    <intercept-url pattern="/**"access="ROLE_USER,ROLE_ADMIN,ROLE_SECRET"/>
    <http-basic/>
</http>
```



---

#### Q5 - What do you mean by session management in Spring Security ?

---

A session is a set of HTTP request and response transactions related to the same user. Sessions allow us to establish variables, such as access rights and localization settings, which will apply to each and every interaction a user has with the web application during the session.  With session management, we can identify the user on any subsequent requests as well as apply security access controls, authorized access to the user private data, and increase the usability of the application. There are multiple mechanisms available in HTTP to maintain session state within web applications, such as cookies (standard HTTP header), URL parameters (URL rewriting), URL arguments on GET requests, body arguments on POST requests, such as hidden form fields (HTML forms), or proprietary HTTP headers.

With **session management in Spring Security**, we manage *detecting timeouts*, *concurrent session control*, *session fixation attack protection*, *`SessionManagementFilter`* ,*`SessionAuthenticationStrategy`*  and *querying the `SessionRegistry` for currently authenticated users and their sessions*.

When creating our session, we can define how Spring Security will interact with the session :
- `always` : A session will always be created if one doesn't already exist.
- `ifRequired` *default*: A session will be created only if required.
- `never` : The framework will never create a session itself, but it will use one if it already exists.
- `stateless` : No session will be created or used by Spring Security.

This defining only controls what *Spring Security* does, not the entire application. 

`<http  create-session = "ifRequired">…</http>`

Java configuration:

```
@Override
Protected void configure (HttpSecurity http) throws Exception {
    http.sessionManagement()
           .sessionCreationPolicy(SessionCreationPolicy.IF_REQUIRED)
}
```

The application won't create any session with the *stateless* option and will effectively skip parts of the Spring Security filter chain, mainly the session-related parts such as `HttpSessionSecurityContextRepository`, `SessionManagementFilter` and `RequestCacheFilter`. With this option, cookies are not used, and so each and every request needs to be re-authenticated. This stateless architecture plays well with *REST API*s and also work well with authentication mechanisms such as Basic and Digest Authentication.

Before the *Authentication* process, Spring Security will run  `SecurityContextPersistenceFilter`  as a filter which stores the *Security Context* between requests according to the strategy which is by default `HttpSessionSecurityContextRepository`  that uses the *HTTP Session* as storage. For *stateless create-session* option, this strategy will be replaced with `NullSecurityContextRepository` strategy and no session will be created or used to keep the context.


- **Detecting and Managing Timeout** :  After the session has timed out, if the user sends a request with an *expired session id* or   a session id that is not expired but entirely invalid , they will be redirected to a configurable URL :

   ```
   http.sessionManagement() 
       .expiredUrl("/sessionExpired.html") 
       .invalidSessionUrl("/invalidSession.html");
   ```
   
   If the user logs out and then logs back in without closing the browser, the session cookie is not cleared when you invalidate the session and will be resubmitted even if the user has logged out. Then it may falsely report an error. We may be able to explicitly delete the `JSESSIONID` cookie on logging out :

   ```
   @Override
   Protected void configure (HttpSecurity http) throws Exception {
       http
           .logout(logout -> logout
               .deleteCookies("JSESSIONID")
            );
   }
   ```

   Spring Session supports  to configure Spring session timeout value using `spring.session.timeout`, but if that's not defined, the autoconfiguration will consider the Session timeout value of the embedded server can be configured using :

   `server.servlet.session.timeout=15m`

   The default duration unit is *second* if we do not specify it. The session is considered invalid after this period of time. Tomcat only supports minute precision for session timeout, with a minimum of one minute. 


- **Concurrent Session Control** :  The implementation of concurrency control uses a specialized version of `SessionAuthenticationStrategy`, called `ConcurrentSessionControlAuthenticationStrategy`. With Spring Security 3, the user is first authenticated by the `AuthenticationManager` and after they are successfully authenticated, a session is created and the check is made whether they are allowed to have another session open or not. For enabling the concurrent session-control support, we need to define first a listener  in order to keep Spring Security updated about session lifecycle events. We can do it by adding a listener to `web.xml` :
	
	```
	<listener>
		<listener-class>
		org.springframework.security.web.session.HttpSessionEventPublisher
		</listener-class>
	</listener>
	```
	
	Or we can define it as a *Bean* :
	
    ```
    @Bean
    Public HttpSessionEventPublisher httpSessionEventPublisher() {
        return new HttpSessionEventPublisher();
    }
    ```
	
	Moreover, we need to add the `ConcurrentSessionFilter` to our `FilterChainProxy`. This filter requires two constructor arguments, one is `sessionRegistry`,generally points to an instance of `SessionRegistryImpl`, and the other is `sessionInformationExpiredStrategy` , defines the strategy to apply when a session has expired. 
	
	Adding the listener to `web.xml` causes an `ApplicationEvent` to be published to the Spring `ApplicationContext` every time a `HttpSession` commences or ends. It is crucial because it notifies the `SessionRegistryImpl`  when a session ends. Otherwise, a user will never be able to log back in again once they have exceeded their session allowance, even if they log out of another session or it times out.
	
	We need to use `sessionManagement` method in order to allow multiple concurrent sessions for the same user :

    ```
    @Override
    Protected void configure(HttpSecurity http) throws Exception {
        http
              .sessionManagement( session -> session
                  .maximumSessions(2)
               );
    }
    ```

    Or we can allow one session and in this condition, a second login will make the first session invalidated. Therefore, we can choose not to allow a second login while controlling the session maximum number :

    ```
    @Override 
    Protected void configure ( HttpSecurity http ) throws Exception  { 
          http 
                .sessionManagement ( session -> session 
                      .maximumSessions(1) 
                      .maxSessionsPreventsLogin(true) 
                );
    }
    ```

- **Session Fixation Attack Protection** :  A malicious user can create a session by accessing a site and induce another user to log in with the same session for example by sending the user a link containing the session identifier as a parameter. This attack is called  *session fixation attack*. Spring Security protects against session fixation attack automatically  by configuring what happens to an existing session when the user tries to authenticate again by allowing us to choose the following options  using the `session-fixation-protection` attribute on `<session-management>` :
  - `none` : The original session will be maintained and do not provide any protection for this attack.
  - `newSession` : Will be created a new and *clean* session, only Spring Security- related attributes will be copied related to the previous session.
  - `migrateSession` :  Will be created a new session by copying all the previous session attributes to the new session.
  - `changeSessionId` : Will use the *session fixation protection* provided by the Servlet container that is `HttpServletRequest#changeSessionId()`, instead of creating a new session. This option is the default in Servlet 3.1 and newer containers and will throw an exception if we specify this option in the older containers.
	
  A `SessionFixationProtectionEvent` will be published in the application context when session fixation protection happens. Besides, if we use `changeSessionId` option,this protection will also notify any `javax.servlet.http.HttpSessionIdListeners`. So we need to use caution if our code listens for both events. 


- **`SessionManagementFilter`** : This mechanism will check the contents of `SecurityContextRepository` comparing the current contents of `SecurityContextHolder` and determine whether a user has been  authenticated during the current request by a non-interactive authentication mechanism, such as pre-authentication or remember-me.
	After comparing, if the repository has a security context, the filter does not do anything. 
	
	Otherwise, the filter will check if the *thread-local SecurityContext* has a (non-anonymous) Authentication object. If it finds this object, the filter guess the user has been authenticated by a previous filter in the stack and will call the configured `SessionAuthenticationStrategy`. 
	
	If the filter does not find the object that means the user is not currently authenticated, then the filter check whether an invalid session ID has been requested (maybe because of a timeout) and will call the configured `InvalidSessionStrategy`, if there is one. The most common approach is just to redirect to a fixed URL and this is encapsulated in the standard implementation `SimpleRedirectInvalidSessionStrategy`.  This approach is also used when configuring an invalid session URL through the namespace.

- **`SessionAuthenticationStrategy`** : It is used by both `SessionManagementFilter` and `AbstractAuthenticationProcessingFilter`.  For example, using a customized form-login class will create a need to inject it into both of these.
	
- **Querying the SessionRegistry for currently authenticated users and their sessions** :   As A useful side effect, setting up concurrency-control, either through the namespace or using plain beans provides us with a reference to the `SessionRegistry` which we can use directly within your application. We can set the `maximumSession` property to -1 to allow unlimited sessions. While using the namespace, we can set an alias for the internally-created `SessionRegistry` using the `session-registry-alias` attribute, providing a reference which we can inject into our own beans. The `getAllPrincipals()` method supplies us with a list of the currently authenticated users and we can list a user’s sessions by calling the `getAllSessions(Object principal, boolean includeExpiredSessions)` method, which returns a list of `SessionInformation` objects. Besides, we can expire a user’s session by calling `expireNow()` on a `SessionInformation` instance. After expiring a user's session with this method, when the user returns to the application, they will be prevented from proceeding. 



---

#### Q6 - 	Why we need Exception Handling ?

---

They are two type of *Exception*; *compile time* (*Checked Exception*) and *Runtime* ( *Unchecked Exception*).
Sometimes when there are certain situation which goes beyond the compiler, the machine does understands what to do with *exception handling*. For example, if there is no money in an ATM and we try to withdraw money as an exception, an exception must be thrown to tell that insufficient money in the ATM. Another example is that  while running an application user won’t expect something `FileNotFoundException`, so we can handle the exception by giving a proper message like `The file that you are looking for is not found`.

The flow of the application can be maintained even after runtime errors if we handle exceptions. When we have an exception in the middle of our program and we could not handle that exception, our program will stop to be executed at that point and could not continue to work. 

If we handle exceptions just in each of the method, our code will be a mess and hard to read. We can throw the exceptions at root level where the activity is triggered and handle every exception at one level. Then we can handle these exceptions at one level only more easily. Especially if we are making a large project, there will be lots of exceptions that can be occur. *Exception handling* will help us to organize these exceptions properly, write much clean and so understandable code and handle all exceptions automatically by giving us more time and less problems to deal with.

Moreover, we need *exception handling* for logging purposes.


---

#### Q7 - Explain what is AuthenticationManager in Spring security ?

---

`AuthenticationManager`  allows us to plug in other authentication schemes. It specifies how the authentication is performed by *Spring Security Filters*.  The returned `Authentication` is then set on the `SecurityContextHolder`  by  *Spring Security Filters* which called the `AuthenticationManager`. Although the implementation of `AuthenticationManager` could be anything, the most used implementation is `ProviderManager`.

We can set the `SecurityContextHolder` directly and are not required to use an `AuthenticationManager`, if we are not integrating with *Spring Security Filters* . 


---

#### Q8 - What is Spring Security Filter Chain ?

---

`SecurityFilterChain` is like a container for  *Spring Security Filters* which should be called for related request and used by `FilterChainProxy`  to specify it. Spring Security maintains a filter chain internally where each of the filters has a particular responsibility and filters are added or removed from the configuration depending on which services are required. The ordering of the filters is crucial as there are dependencies between them. This allows providing a totally separate configuration for different slices of your application. Even if we have lots of filters, `FilterChainProxy` lets us add a single entry to `web.xml` and deal entirely with the application context file for managing our web security beans. It is wired using a `DelegatingFilterProxy`, but with the `filter-name` set to the bean name “filterChainProxy”. The filter chain is then declared in the application context with the same bean name. 

 Each `SecurityFilterChain` can be unique and configured in isolation. In fact, a `SecurityFilterChain` might have zero *security Filters* if the application wants Spring Security to ignore certain requests. The *Security Filters* in `SecurityFilterChain` are typically *Beans*, but they are registered with `FilterChainProxy` instead of `DelegatingFilterProxy`. The `FilterChainProxy` contains information about the different security filter chains and it delegates the task to the chain based on the URI’s mapping or using the `RequestMatcher` interface.`FilterChainProxy` can not be executed directly, just it is started by `DelegatingFilterProxy` filter.

The `DelegatingFilterProxy`  is a filter which provides a connection between Servlet container’s life-cycle (`web.xml`) and Spring’s Application Context  and  delegates the work to the spring bean to start the security flow.  Servlet container does not have any information about the Spring’s application context, but spring security needs security filters to execute the task. Since `DelegatingFilterProxy`  is a servlet filter, the application server register it as a normal filter in the context.


---

#### Q9 - What are the differences between OAuth2 and  JWT ?

---

The OAuth 2.0 specification defines a delegation protocol that provides clients with secure access to the user resources on a service provider. Such an approach prevents the user from the necessity to enter his password out of the service provider: the whole process is curtailed to clicking the «I agree to provide access to ...» button. The idea is that having one secure account, the user can use it for identity verification on other services, without disclosing his password.

JWT tokens are JSON encoded data structures contains information about issuer, subject (claims), expiration time etc. It is signed for tamper proof and authenticity and it is  supported by all devices.


| JWT | OAuth2 |
|-------|------------|
|  Just a token format | An authorization protocol that can use JWT as a token |
|  Defines a compact and self-contained mechanism for transmitting data between parties in a way that can be verified and trusted because it is digitally signed. |  quite flexible mechanism, each service requires its own implementation. |
| Contains all important information about an entity, meaning that no database queries are necessary and the session doesn’t need to be saved on the server. | Even getting minimal user information can force us making additional requests in the process of user verification |
| Good choice for implementing stateless authentication mechanisms |  just for authorization, client software can be authorized to access the resources on-behalf of end user using access token.|
|  Can be encrypted to protect the token information using symmetric or asymmetric approach, so more secure with digital signature | When a token is stolen, an attacker gains access to the secure data for a while. |
| Authentication with JWT token can not log out actually, as we don't have an *Authentication Server* that keeps track of tokens. | We can do real log out you must go with OAuth2. | 



---

#### Q10 - What is method security and why do we need it ?

---

Method security is an approach that adds support for securing methods mostly through annotations on Spring Security beans via <method-security>  element. Methods can be secured by the use of annotations (defined at the interface or class level) or by defining a set of pointcuts. We also need to explicitly enable method security by putting the `@EnableGlobalMethodSecurity` annotation on your `ApplicationContextConfiguration`. 

```
@Configuration
@EnableGlobalMethodSecurity(
   prePostEnabled=true, // (1)
   securedEnabled=true, // (2)
   jsr250Enabled=true) // (3)
Public class YourSecurityConfig  extends WebSecurityConfigurerAdapter{
}
```

`<method-security>` has attributes :

- `pre-post-enabled`  : Enables Spring Security’s *pre* and *post* invocation annotations (`@PreFilter`, `@PreAuthorize`, `@PostFilter`, `@PostAuthorize`) for this application context. The default value is "true".

- `secured-enabled` : Enables Spring Security’s `@Secured` annotation for this application context. The default value is "false".

- `jsr250-enabled` : Enables JSR-250 authorization annotations (`@RolesAllowed`, `@PermitAll`, `@DenyAll`) for this application context. The default value is "false".

- `proxy-target-class` : If true, class based proxying will be used instead of interface based proxying. The default value is "false".

`@Secured` and `@RolesAllowed` take in an authority/role string as value. `@PreAuthorize` and `@PostAuthorize` contain not only authorities/roles, but also any valid SpEL expression. If we try and access a protected method with an insufficient authority/role, these annotations will raise an `AccessDeniedException`.

With method security, we could secure our service layer  for example  by restricting which roles are able to execute a particular method  and hence test it using dedicated method-level security test support.


---

#### Q11 - What Proxy means and how and where can be used ?

---

Proxy  is a structural pattern that provides a substitute or placeholder for another object in order to control creation and access to the original object. This placeholder object is called *proxy object*. The proxy pattern allows us to perform some logic either before or after invoking the original object. It is mostly used for postponing the cost of instantiating of an object ( especially an expensive to create object) until it is actually needed by clients.

Spring creates a new caching proxy class by adding `@Cacheable` annotation. This class will be responsible of adding *Caching* behavior and will be used for dependency injection.

As an example of proxy, we can consider a report viewer application that generates and displays sales reports. When the application starts, it displays a UI where users can specify the format and amount of data to display in a report. Users can also specify the type of report to generate, such as a daily sales report, a complex sales forecast report for the next quarter, and on. The application has a report generator object, a resource consuming (expensive) object that gathers report data from various sources, analyzes them, formats them, and sends it to the UI for display. In the report viewer application, it is not necessary to create the report generator object when the application loads. We want the UI to be light and start up quickly. It’s only when a user clicks on the Generate Report button on the UI we will need to instantiate the report generator object and ask it to create the report. 

There are some types of proxy :
- **Virtual proxy** : Creates expensive objects on demand. For instance,  we can create a proxy *with the same interface* as the real report generator object. The UI keeps interacting with the proxy. It is only when the UI asks the proxy to generate a report, the proxy will instantiate the real report generator object. 

- **Protection proxy** : Controls access to the real object. As an example, in the report viewer application, a report generator object generates sensitive reports that a protection proxy allows access to only users with the Manager role.

- **Remote proxy** : Represents an object running on a remote JVM. Java RMI and Jini used to create distributed applications in Java uses remote proxies, which are called *stubs*. 

- **Smart reference proxy** : Performs additional actions on the real object, such as maintaining reference counts to a real object so that the real object can be freed when no more references exist. It can also load and cache a persistent object in memory when first referenced or lock a real object to ensure that no other objects can change it.


---

#### Q12 - What is Wrapper Class and where can be used ?

---

Wrapper class provides us an exchange mechanism between primitive types and objects. When we create an object to a wrapper class, it contains a field that we can store primitive data type values.  A Wrapper class isencapsulates primitive data types via their objects. 

|Primitive Data Type | Wrapper Class |
|---------------------------|--------------------|
| char | Character |
| byte | Byte |
|short | Short |
|int | Integer |
| long | Long |
| float | Float |
| double | Double |
| boolean | Boolean |

*Autoboxing* and *unboxing* feature convert primitives into objects and objects into primitives automatically. The automatic conversion of primitive into an object is known as *autoboxing* and the opposite direction of conversion is known as *unboxing*.

We use wrapper class when :
- We need to change the value in method. Java supports only call by value. So, if we pass a primitive value, it will not change the original value. But, if we convert the primitive value in an object, it will change the original value.

- We need to convert the objects into streams to perform the serialization. If we have a primitive value, we can convert it in objects through the wrapper classes.
- We need Java synchronization that works only with objects in *Multithreading*.
- We need the classes in `java.util package` which handles only objects and hence wrapper classes help in this  case.
- We need data structures in the Collection framework, such as *ArrayList*, *LinkedList*,  *HashSet*, *LinkedHashSet*, *TreeSet*, *PriorityQueue*, *ArrayDeque* and *Vector*, that store only objects (reference types) and not primitive types.


---

#### Q13 - What is SSL ? What is TLS ? What is the difference ? How can we use them ?

---

SSL (*Secure Sockets Layer*) is a cryptographic protocol that facilities secure, encrypted connections on the Internet. The most well-known use of SSL is web browsers connecting to websites, where SSL is used on top of HTTP to create a HTTPS connection. 

TLS (*Transport Layer Security*)  is also a cryptographic protocols that encrypt data and authenticate a connection when transporting data on the Internet. TLS is  just a newer and upgraded version of SSL. It fixes some security vulnerabilities in the earlier SSL protocols.

How they establish secure connections is the main difference between them. They both do it through a process called “the handshake”. Handshake is how the server and the client authenticate each other before finally creating an encrypted connection. The SSL handshake involves using a port to make what is known as an explicit connection. However, TLS handshake connects via a protocol, which is known as an implicit connection. The process of both handshakes is determined by *cipher suites*. *Cipher suites* are algorithms that outline the sequence of steps that must be performed in order to execute a cryptographic function. TLS-supported cipher suites are faster and more secure than SSL-supported cipher suites.  

We use them by installing the digital certificate on our server so that web browsers can connect with our site via HTTPS. All modern SSL certificates should work by doing this via the TLS protocol.


---

#### Q14 - Why do you need the intercept-url ?

---

Most web applications using Spring Security only have a couple of intercept-urls because they only have very basic security requirements. We need to have unauthenticated access to the login and login-error screens and usually some aspect of the public site, so that can be a few URL patterns. Then there's often an admin section, and then everything else is `ROLE_USER`.
If we need more roles, we should associate them with top level URL path components. Although it's not required, it makes it easier to be sure that resources are appropriately protected. We need the *intercept-url* to create these top level URL path components easily.

