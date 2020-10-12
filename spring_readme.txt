Day1
=====

Spring Bean configuration
=========================
1.XML
2.Annotations

	@Component
	@Controller
	@Service
	@Repository
	@ComponentScan
	@Configuration


url      method                    mapping                                                                                                      new style
=========================================================================================================
/hello   GET            @RequestMapping(value="/hello",method=RequestMethod.GET)                   @GetMapping("/hello")
/hello   POST          @RequestMapping(value="/hello",method=RequestMethod.POST)                @PostMapping("/hello")
/hello   DELETE       @RequestMapping(value="/hello",method=RequestMethod.DELETE)            @DeleteMapping("/hello")
/hello   PUT            @RequestMapping(value="/hello",method=RequestMethod.PUT)                  @PutMapping("/hello")
/hello   PATCH        @RequestMapping(value="/hello",method=RequestMethod.PATCH)               @PatchMapping("/hello")


@ResponseBody  => Server to Client => Java Object to JSON or XML  => Accept       = application/json 

@RequestBody  => Client to Server =>  JSON or XML Java Object to  => Content-Type = application/json



@Controller
@RestController


http://localhost:8080/spring-web-mvc/hello
http://localhost:8080/spring-web-mvc/hello/welcome
http://localhost:8080/spring-web-mvc/hello/greet



@Controller
@RequestMapping("/hello")
public class HelloController{

@RequestMapping(method=RequestMethod.GET)
public @ResponseBody String hello(){
return "Hello World";
}

@RequestMapping(value="/welcome"method=RequestMethod.GET)
public @ResponseBody String welcome(){
return "Welcome World";
}

@RequestMapping(value="/greet", method=RequestMethod.GET)
public @ResponseBody String greet(){
return "Greett World";
}

}



or @RestController =@Controller + @ResponseBody

@RestController
@RequestMapping("/hello")
public class HelloController{

@RequestMapping(method=RequestMethod.GET)
public  String hello(){
return "Hello World";
}

@RequestMapping(value="/welcome"method=RequestMethod.GET)
public  String welcome(){
return "Welcome World";
}

@RequestMapping(value="/greet", method=RequestMethod.GET)
public String greet(){
return "Greett World";
}

}



Step 1  :create a dynamic web project with tomcat as runtime
=======

Step 2  :add spring jar files in lib directory of dynamic web project
=======

Step 3  :configure Disptcher Servlet in web.xml with some name ex. spring and
=======  It should be loaded and instantinated at the time of starting the web application 
         Internally it search the spting config file with spring-servlet.xml


Step 4 :Create spring configuration file spring-servlet.xml
======



Spring Boot
============
Spring Boot is an open source Java-based framework used to create a micro Service. It is developed by Pivotal Team and is used to build stand-alone and production ready spring applications.


Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run".


We take an opinionated view of the Spring platform and third-party libraries so you can get started with minimum fuss. Most Spring Boot applications need minimal Spring configuration.

Features
=========

Create stand-alone Spring applications

Embed Tomcat, Jetty or Undertow directly (no need to deploy WAR files)

Provide opinionated 'starter' dependencies to simplify your build configuration

Automatically configure Spring and 3rd party libraries whenever possible

Provide production-ready features such as metrics, health checks, and externalized configuration

Absolutely no code generation and no requirement for XML configuration


What You Will build ?
====================
You will build a simple web application with Spring Boot and add some useful services to it.

What You Need
==============

A favorite text editor or IDE

JDK 1.8 or later

Gradle 4+ or Maven 3.2+

You can also import the code straight into your IDE:

Spring Tool Suite (STS)

IntelliJ IDEA


Spring Boot Dependencies
========================

Spring Web WEB
===============
Build web, including RESTful, applications using Spring MVC. Uses Apache Tomcat as the default embedded container.

Spring Boot DevTools DEVELOPER TOOLS
====================================
Provides fast application restarts, LiveReload, and configurations for enhanced development experience.


Spring Boot Actuator OPS
=========================
Supports built in (or custom) endpoints that let you monitor and manage your application - such as application health, metrics, sessions, etc.


To get the JSP responses add below dependency
==============================================

                <dependency>
			<groupId>org.apache.tomcat.embed</groupId>
			<artifactId>tomcat-embed-jasper</artifactId>
		</dependency>
		

Develop a Restful Web API with Spring Boot to perform opeartions on Employee 
=============================================================================

Employee
=========
     private int employeeId;
     private String fname;
     private String lname;
     private double salary;
     private String email;
     private Date doj;
     private String mobile;
     private String pan;
     



http://localhost:8080/spring-boot-ems/employees            :GET     : get all employees
http://localhost:8080/spring-boot-ems/employees/101    :GET     : get     employee with id 101
http://localhost:8080/spring-boot-ems/employees/101    :DELETE  : delete  employee with id 101
http://localhost:8080/spring-boot-ems/employees/101    :PUT     : update  employee with id 101
http://localhost:8080/spring-boot-ems/employees/101    :PATCH   : update  employee with id 101
http://localhost:8080/spring-boot-ems/employees            :POST    : add     employee



DataSource
==========
Collection(Map) 
Txt File
Excel File
RDBMS            -> MySQL,Oracle,DB2,
NOSQL            -> MongoDB
Third party application



Day2
=====

Spring Framework DAO support
============================
JdbcTemplate
HibernateTemplate
JpaTemplate

JmsTemplate
Resttemplate





Spring Boot
===========

CRUDRepository
      |
PagingAndSortingRepository       MongoRepository
      |
JpaRepository	  





Execute schema.sql and data.sql on startup of Spring Boot


An SQL database can be initialized manually and can also be done through code. You can create the table and insert the data into tables using JPA.

Initialise the database using JPA
JPA has feature for DDL(Data definition language: DROP, RENAME, CREATE, ALTER, TRUNCATE) generation, and these can be setup to run on startup against database. This is controlled through two external properties:

 spring.jpa.generate-ddl (boolean)
By default, its value is false. Whether to initialize schema on startup and it is vendor independent.
spring.jpa.hibernate.ddl-auto
It is a Hibernate feature that control the behavior in more fine grained way. It is DDL mode. This is actually a shortcut for the hibernate.hbm2ddl.auto property. Defaults to create-drop when using an embedded database and no schema manager was detected. Otherwise, defaults to none.
Initialize a database using Hibernate
You can set spring.jpa.hibernate.ddl-auto explicitly and standard hibernate properties values are enum: none,validate, update, create, create-drop. Spring boot choose a default value type based on the embedded database. It defaults to create-drop if no schema manager has been detected, and none is all other cases. Available embedded databases in spring boot are hsqldb, h2, and derby. An embedded database is detected by looking at Connection type.

You can create the schema from scratch by setting the ddl-auto properties to create or create-drop along with a file import.sql should be in the root of classpath is executed on startup. This is the Hibernate feature and has nothing to do with Spring framework. It is advisable to do for testing or demos, not in production environment.

Initialize a Database
Spring boot automatically create the schema(DDL scripts) of your DataSource and initialize it (DML scripts). It loads the SQL from the standard root classpath locations: schema.sql and data.sql respectively. You can create the schema and initialize it based on the platform. Platform value is of spring.datasource.platform. Now you can create files schema-${platform}.sql and data-${platform}.sql which is processed by Spring Boot. It allows you to choose the database specific scripts if necessary. You can choose the vendor name of database(platform) like hsqldb, h2, oracle, mysql, postgresql, and so on.

In the JPA based app, You should not use both spring.jpa.hibernate.ddl-auto and schema.sql. Make sure to disable spring.jpa.hibernate.ddl-auto if you use schema.sql.

Spring Boot automatically creates the schema of embedded DataSource. You can customize this behaviour using spring.datasource.initialization-mode property. You can always initialize the DataSource regardless of its type setting spring.datasource.initialization-mode=always. The property spring.datasource.initialization-mode supports three values:

always
Always initialize the datasource.
embedded
Only initialize an embedded datasource.
never
Do not initialize the datasource.
By default Spring Boot enables the fail-fast feature of the Spring JDBC initializer. This means application fails to start when scripts causes exception. You can tune that behavior by setting spring.datasource.continue-on-error.

Initialize a Spring Batch Database
In Spring Batch, Spring Boot detect your database type and execute the scripts on startup and it happens by defaults for the embedded database. You can enable it for any database by setting spring.batch.initialize-schema=always. You can also switch off the initialization explicitly by setting spring.batch.initialize-schema=never.

Execute schema.sql and data.sql with Spring Boot
Lets initialize a database with spring boot. Create schema.sql and data.sql files under resources folder. Lets understand with spring boot maven based sample application.


Spring Data JPA SQL
====================
Persist data in SQL stores with Java Persistence API using Spring Data and Hibernate.


 <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
 </dependency>

     
Lombok DEVELOPER TOOLS
=======================

https://www.baeldung.com/lombok-ide


Java annotation library which helps to reduce boilerplate code.
	 
	  	  
	  <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
            <optional>true</optional>
        </dependency>



@Data  =>  @Getter @Setter @RequiredArgsConstructor @ToString @EqualsAndHashCode.

@AllArgsConstructor     :Generate param constructor with all fields

@RequiredArgsConstructor : Generate constructor for nont null fields

@CommonsLog











application.properties

spring.jpa.generate-ddl=false
spring.jpa.hibernate.ddl-auto=none
spring.datasource.url=jdbc:mysql://localhost:3306/test?useSSL=true
spring.datasource.username=root
spring.datasource.password=admin
spring.datasource.initialization-mode=always



You can also create user table through spring boot auto generate script if you set spring.jpa.generate-ddl to true or set spring.jpa.hibernate.ddl-auto to any validate, update, create, create-drop.

You can also run scripts based on platform. Lets suppose you want to run for mysql plateform then create files schema-mysql.sql and data-mysql.sql under resources folder and set property spring.datasource.platform=mysql in application.properties file.




Spring Security SECURITY
==========================
Highly customizable authentication and access-control framework for Spring applications.


       <dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-security</artifactId>
		</dependency>


JAAS (Java Authentication and Authorization)
============================================
200   : OK
404   : NOT FOUND
500   : INTERNAL SERVER ERROR
403   : NOT AUTHORIZED     type=Forbidden, status=403)
401   : NOT AUTHENTICATED  type=Unauthorized, status=401
405   : METHOD NOT ALLOWED


1.Authentication
=================
	1.BASIC     (spring Boot 1.5)
	2.DIGEST
	3.FORM Based (spring Boot 2.x) 
       
           Default username  :user	
           Password          :generated on console	
		   
In memory authentication
========================

=========================================
USERNAME   PASSWORD      ROLE    
==========================================
RAM         RAM          ADMIN
RAHIM       RAHIM        STUDENT
DAVID       DAVID        TEACHER 
		   
		   
RAM   $2a$10$eDADpARaorWqr2/tCLbZ..jTFbeOeDuXvUjmtR9p3dg90ksJ0xHx2
RAHIM $2a$10$12pH61XM.FUqVEmNqecJmOgps0A2uW0JXqJgSYXvUCTgXYtpEDzO.
DAVID $2a$10$Bgoe1PwmoFiskQS2ywAtn.QsIKzjTp/lkgoczhis.ehO2yjjzV85W
		   
		   
		   
		  
/hi    ADMIN,STUDENT,TEACHER
/hello ADMIN
/greet TEACHER
/users ADMIN,TEACHER		  
		  
		   
		   
Default end points
===================
/login 
/logout
2.Authorization



class BankingService{


withdraw(){
BAnkingSecurity bs=new BAnkingSecurity();

if (bs.validate()){
}


}
deposit(){
BAnkingSecurity bs=new BAnkingSecurity();

}

fundTransfer(){
BAnkingSecurity bs=new BAnkingSecurity();

}

}


class BankSecurity{

validate(){

}

}




AOP (Aspect Orineted Programming)
==================================


Concern :Piece Of Code

Business Logic  =           Core Concern   +       Cross Cutting Concern

                           withdraw                  secuirty
                           deposit                   logging 
                           transfer                  scalabilty tx mgmt


AOP is used to separate CCC from CC and attach CCC dynamically in a CC.

Can We Separate CCC from CC using OOP? Yes but it is a static approach


Target  :It is a piece of code that implements Core Concern


Advice  :It is a piece of code that implements Cross Cutting  Concern
                what +when

               before,after, after return,after throwing,around

JoinPoint :
                 It is a well defined point in Core Concern where u want to execute CCC
                Spring supports only method call as a join point

Point Cut  :
                 It is a set of one or more join points

Aspect :advice +point cut  ->what +when+where


Weaving :Mechanism of attaching CCC to CC (Autowinring)




Assignment -Casestudy

Online line shopping application  using Spring Boot   
========================================================
https://o7planning.org/en/10683/create-a-shopping-cart-web-application-with-spring-boot-hibernate

1.Develop UI using JSP 
2.Develop Restful Web API
































































































































































































































































































































































Micro Service with Spring Boot    (12 hours)
============================================

Service (API)

Enterprise  Application
=======================
Colleges
Hotels
Hospital
Banks

Bank => withdraw,deposit,fundTransfer,

C =>
R =>
U =>
D =>


Customer
Bank
Account
Address


Online Shopping Application (Domain Driven Development)
=======================================================
MFG
Insurance 
HEalthCare
Banking
Ecommerce domain


Customer =>login,register
Product  =>CRUD
Payment  =>
Order    =>

PL  SL DAL  DL 
              
SOAP ->WSDL -> Top Down,Bootm up
             wsgen -> JAva ->WSDL
             wsimprt->WSDL  -> Java
			 

Restful Webservice
=================
If you are providing service (CRUD ->Domain Objects) via http urls

GET 
POST
PUT/PATCH
DELETE
			 
			 
Domain Objects (5)
===================
Product =>CRUD

Customer =>CRUD

Order =>CRUD

Payment =>CRUD

User =>CRUD

product-service  (.Net Web MVC) =>A Team   8081 ->IIS   =>1 Instance (100 req)
============================================================================
http://localhost:8081/online-shopping/products     =>GET
http://localhost:8081/online-shopping/products/101 =>GET
http://localhost:8081/online-shopping/products/101 =>DELETE
http://localhost:8081/online-shopping/products/101 =>PUT/PATCH
http://localhost:8081/online-shopping/products     =>POST

customer-service  (Java -Spring Boot)  =>B Team =>  8080

===================================================
http://localhost:8080/online-shopping/customers     =>GET
http://localhost:8080/online-shopping/csustomers/101 =>GET
http://localhost:8080/online-shopping/csustomers/101 =>DELETE
http://localhost:8080/online-shopping/customers/101 =>PUT
http://localhost:8080/online-shopping/customers     =>POST

order-service  (Node JS -> Express JS)  => C Team  =>1212
==================================================
http://localhost:3000/online-shopping/orders      =>GET
http://localhost:3000/online-shopping/orders/101 =>GET
http://localhost:3000/online-shopping/orders/101 =>DELETE
http://localhost:3000/online-shopping/orders/101 =>PUT
http://localhost:3000/online-shopping/orders     =>POST



 online-shopping/products                        product-service  ->  8081
 online-shopping/csutomer                        customer-service ->  8080
 online-shopping/order       Eureka Server       order-service    ->  3000
 online-shopping/payment                         payment-service  ->  4444
 online-shoppinng/user                           user-service     ->  5555



Day1
====
1.What is MCA?
================
Microservices - also known as the microservice architecture - is an architectural style that structures an application as a collection of services that are


	1.Highly maintainable and testable
	2.Loosely coupled
	3.Independently deployable
	4.Organized around single business capabilities. 
	  (Single Responsibility Principle)
	  
	
The microservice architecture enables the continuous delivery/deployment of large, complex applications. It also enables an organization to evolve its technology stack.

1.MCA Vs Monolithic

2.Adantages of MCA
	1.Highly maintainable and testable
	2.Loosely coupled
	3.Independently deployable
	4.Organized around single business capabilities.


3.Challanges of MCA
   1.Avaialabilty  
   2.Scaling
   3.Monitoring -logs,loads,heap,memory ->actuator -> Admin Server
   4.Integration 
   
   
   
4.Orchestration and Choreography

5.What is TDD,BDD,DDD,MDD?
6.SOLID Design Principles
7.Design Patterns(creational,Structural,Behavioural)
8.12 Factor Application

What is DDD?
=============
Domain Driven Design is a way of looking at software from top down.
When we are developing a software our focus should not be primarily on technology,It should be primaryly on business or whatever activity we are trying to assist with software,domain
The domain is the business that we are trying to solve/assist with software.
The domain can be any business domain

Aviation domain
Railway domain
Banking domain
Insurance domain
Manufacturing domain
Ecommerce domain


Specifically we approach that by trying to develop the models of that domain and make our software confirmed to that.

What DDD gives us?
===================
Strategic Design Tool
Tactical Design Tools


Service
Project
Layers(Service/Data Access Layer,Controller)
Modules
Design Patterns
OOP
Classes
Objects
Exe/Jar/war/ear


Why We should go for DDD?

1.	To improve your craft
2.	As a software developer you want to grow
3.	You want to take a responsibility
4.	You want to design things from scratch


It’s not a customers job what they want (Steve Jobs)
What problems this customer is going to face in the future
If you want to give any new feature it should go from your side

Your architecture might be fabulous but it’s the end user ultimately who decides whether your system is fabulous or not.


A system that doesn’t solve the business needs is of no use to any one, no matter how pretty it looks or how well architected it’s infrastructure.


##########
What is the difference between Orchestration and Choreography in Microservices architecture?
################ 
In Orchestration, we rely on a central system to control and call various Microservices to complete a task.

In Choreography, each Microservice works like a State Machine and reacts based on the input from other parts. 

Orchestration is a tightly coupled approach for integrating Microservices.
But Choreography introduces loose coupling. Also, Choreography based systems are more flexible and easy to change than Orchestration based systems.

Orchestration is often done by synchronous calls. But choreography is done by asynchronous calls. The synchronous calls are much simpler compared to asynchronous communication. 




                                             withdraw(source,amount)
fundTransfer(source,desitnation,amount)
                                             deposit(desination,amount)




S-Single Responsibilty Principle

           
		   void addEmployee(Employee e){
		   //add
		    }



O-Open Close Principle 


       Shape

Rect    Circle 	   

          class PaintBrush{
		  
		  
		  drawShape(Shape s){
		  s.draw();
		  }
		  
		   	  
		  
		  }

  
		  
		  
		  
		  

L-Liscovs Substituion Principle
I-Interface segration principle

interface Flyable{
void fly();
}

interface Drivable{
void drive();
}


              Vehicle 

Bus    Truck    Bike 	 implements Drivable
Aeroplane    Helicapter   implement Flyable,Drivable		  
			  





D-Dependency Injection

          interface EmployeeInterface{
           Collection<Employee> getEmployeeList()
		  }



=========================
The Twelve Factors
==========================
          This is best practices to develop spring cloud native applications

I. Codebase
One codebase tracked in revision control, many deploys
II. Dependencies
Explicitly declare and isolate dependencies
III. Config
Store config in the environment
IV. Backing services
Treat backing services as attached resources
V. Build, release, run
Strictly separate build and run stages
VI. Processes
Execute the app as one or more stateless processes
VII. Port binding
Export services via port binding
VIII. Concurrency
Scale out via the process model
IX. Disposability
Maximize robustness with fast startup and graceful shutdown
X. Dev/prod parity
Keep development, staging, and production as similar as possible
XI. Logs
Treat logs as event streams
XII. Admin processes
Run admin/management tasks as one-off processes



Spring Cloud Config Server
===========================
Spring Cloud Config provides server and client-side support for externalized configuration in a distributed system. With the Config Server you have a central place to manage external properties for applications across all environments. The concepts on both client and server map identically to the Spring Environment and PropertySource abstractions, so they fit very well with Spring applications, but can be used with any application running in any language. As an application moves through the deployment pipeline from dev to test and into production you can manage the configuration between those environments and be certain that applications have everything they need to run when they migrate. The default implementation of the server storage backend uses git so it easily supports labelled versions of configuration environments, as well as being accessible to a wide range of tooling for managing the content. It is easy to add alternative implementations and plug them in with Spring configuration.


In Local File system
======================

By default cloud config server loads the properites file from config folder

In Git
======
By default cloud config server loads the properites file from git  repository

To make it to locaal fs

spring.profiles.active=native



@EnableConfigServer
@SpringBootApplication
public class ConfigServerApplication {

	public static void main(String[] args) {
		SpringApplication.run(ConfigServerApplication.class, args);
	}

}


Spring Cloud Config Client
===========================
A Spring Boot application can take immediate advantage of the Spring Config Server (or other external property sources provided by the application developer). It also picks up some additional useful features related to Environment change events.


7.1 Config First Bootstrap
===================================
The default behavior for any application that has the Spring Cloud Config Client on the classpath is as follows: When a config client starts, it binds to the Config Server (through the spring.cloud.config.uri bootstrap configuration property) and initializes Spring Environment with remote property sources.

The net result of this behavior is that all client applications that want to consume the Config Server need a bootstrap.yml (or an environment variable) with the server address set in spring.cloud.config.uri (it defaults to "http://localhost:8888").


bootstrap.properties
=====================
spring.application.name=config-client
spring.cloud.config.uri=http://localhost:9090/cloud-server
spring.profiles.active=dev



Admin Server
==============
Monitoring your application by using Spring Boot Actuator Endpoint is slightly difficult. Because, if you have ‘n’ number of applications, every application has separate actuator endpoints, thus making monitoring difficult. Spring Boot Admin Server is an application used to manage and monitor your Microservice application.

To handle such situations, CodeCentric Team provides a Spring Boot Admin UI to manage and monitor all your Spring Boot application Actuator endpoints at one place.

For building a Spring Boot Admin Server we need to add the below dependencies in your build configuration file.

Maven users can add the below dependencies in your pom.xml file -

<dependency>
   <groupId>de.codecentric</groupId>
   <artifactId>spring-boot-admin-server</artifactId>
</dependency>
<dependency>
   <groupId>de.codecentric</groupId>
   <artifactId>spring-boot-admin-server-ui</artifactId>
</dependency>


package com.tutorialspoint.adminserver;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import de.codecentric.boot.admin.config.EnableAdminServer;

@SpringBootApplication
@EnableAdminServer
public class AdminserverApplication {   
   public static void main(String[] args) {
      SpringApplication.run(AdminserverApplication.class, args);
   }
}


Spring Boot Admin Client
========================
For monitoring and managing your microservice application via Spring Boot Admin Server, you should add the Spring Boot Admin starter client dependency and point out the Admin Server URI into the application properties file.

Note - For monitoring an application, you should enable the Spring Boot Actuator Endpoints for your Microservice application.

First, add the following Spring Boot Admin starter client dependency and Spring Boot starter actuator dependency in your build configuration file.

Maven users can add the following dependencies in your pom.xml file -

<dependency>
   <groupId>de.codecentric</groupId>
   <artifactId>spring-boot-admin-starter-client</artifactId>
</dependency>

<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>



Now, add the Spring Boot Admin Server URL into your application properties file.

For properties file users, add the following properties in the application.properties file.

server.port=1111
spring.application.name=hello-service
spring.boot.admin.client.url=http://localhost:9090

management.endpoints.web.exposure.include=*
management.endpoints.jmx.exposure.include=*

                                                 web.xml

http://localhost:8080/my-app/hello1   
http://localhost:8080/my-app/hello2
http://localhost:8080/my-app/hello3





Service Oriented Architecture
==============================

Service Provider (hello-service,greet-service,welcome-service)/hello,/welcome,/greet

Service Consumer ->

Service Registry ->(register the services in service registry)

Eureka Server
==============

Eureka Server is an application that holds the information about all client-service applications. Every Micro service will register into the Eureka server and Eureka server knows all the client applications running on each port and IP address. Eureka Server is also known as Discovery Server.

In this chapter, we will learn in detail about How to build a Eureka server.

Building a Eureka Server

Eureka Server comes with the bundle of Spring Cloud. For this, we need to develop the Eureka server and run it on the default port 8761.


After downloading the project in main Spring Boot Application class file, we need to add @EnableEurekaServer annotation. The @EnableEurekaServer annotation is used to make your Spring Boot application acts as a Eureka Server.

The code for main Spring Boot application class file is as shown below -

package com.tutorialspoint.eurekaserver;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.eureka.server.EnableEurekaServer;

@SpringBootApplication
@EnableEurekaServer
public class EurekaserverApplication {
   public static void main(String[] args) {
      SpringApplication.run(EurekaserverApplication.class, args);
   }
}
Make sure Spring cloud Eureka server dependency is added in your build configuration file.

The code for Maven user dependency is shown below -

<dependency>
<groupId>org.springframework.cloud</groupId>
   <artifactId>spring-cloud-starter-eureka-server</artifactId>
</dependency>


Service Registration with Eureka
===================================

To register the Spring Boot Micro service application into the Eureka Server. Before registering the application, please make sure Eureka Server is running on the port 8761 or first build the Eureka Server and run it. For further information on building the Eureka server, you can refer to the previous chapter.

First, you need to add the following dependencies in our build configuration file to register the microservice with the Eureka server.

Maven users can add the following dependencies into the pom.xml file -
        
		
    	<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
		</dependency>
	

Now, we need to add the @EnableEurekaClient annotation in the main Spring Boot application class file. The @EnableEurekaClient annotation makes your Spring Boot application act as a Eureka client.

The main Spring Boot application is as given below -

@SpringBootApplication
@EnableEurekaClient
public class EurekaclientApplication {
   public static void main(String[] args) {
      SpringApplication.run(EurekaclientApplication.class, args);
   }
}

To register the Spring Boot application into Eureka Server we need to add the following configuration in our application.properties file or application.yml file and specify the Eureka Server URL in our configuration.


spring.application.name=customer-service
server.port=1111

eureka.client.register-with-eureka=true
eureka.client.fetchRegistry=true
eureka.client.serviceUrl.defaultZone=http://localhost:8761/eureka
eureka.client.serviceUrl.healthcheck.enabled=true



management.endpoints.web.exposure.include=*


Zuul Proxy
===========

Spring Cloud has created an embedded Zuul proxy to ease the development of a common use case where a UI application wants to make proxy calls to one or more back end services. This feature is useful for a user interface to proxy to the back end services it requires, avoiding the need to manage CORS and authentication concerns independently for all the back ends.

To enable it, annotate a Spring Boot main class with @EnableZuulProxy. Doing so causes local calls to be forwarded to the appropriate service. By convention, a service with an ID of users receives requests from the proxy located at /users (with the prefix stripped). The proxy uses Ribbon to locate an instance to which to forward through discovery. All requests are executed in a hystrix command, so failures appear in Hystrix metrics. Once the circuit is open, the proxy does not try to contact the service.



eureka-server    :http://localhost:8761 (service registry)
customer-service :http://localhost:1111 
product-service  :http://localhost:2222

api-gateway      :http://localhost:8181

Server Side Load balncing


      A->B->C->D->E

day4
=====
Most developers face difficulty of tracing logs if any issue occurred. This can be solved by Spring Cloud Sleuth and ZipKin server for Spring Boot application.

Spring Cloud Sleuth
Spring cloud Sleuth logs are printed in the following format -

[application-name,traceid,spanid,zipkin-export]

Where,

Application-name = Name of the application

Traceid = each request and response traceid is same when calling same service or one service to another service.

Spanid = Span Id is printed along with Trace Id. Span Id is different every request and response calling one service to another service.

Zipkin-export = By default it is false. If it is true, logs will be exported to the Zipkin server.

Now, add the Spring Cloud Starter Sleuth dependency in your build configuration file as follows -

Maven users can add the following dependency in your pom.xml file -

<dependency>
   <groupId>org.springframework.cloud</groupId>
   <artifactId>spring-cloud-starter-sleuth</artifactId>
</dependency>


What is Distributed Tracing?
=============================
Distributed Tracing is crucial for troubleshooting and understanding microservices. It is very useful when we need to track the request passing through multiple microservices. Distributed Tracing can be used to measure the performance of the microservices. 

It is easy to identify which microservice is failed or having performance issues whenever there are multiple service calls within a single request.

In this article, you will see how to implement Zipkin Server for Distributed Tracing.

To achieve this, you need to create Zipkin Server application and add these three dependencies in POM.xml.


 <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-zipkin</artifactId>
  </dependency>
	

<dependency>
  <groupId>io.zipkin.java</groupId>
  <artifactId>zipkin-server</artifactId>
</dependency>

<!-- https://mvnrepository.com/artifact/io.zipkin.java/zipkin-autoconfigure-ui -->
<dependency>
   <groupId>io.zipkin.java</groupId>
   <artifactId>zipkin-autoconfigure-ui</artifactId>
</dependency>


Internally it has 4 modules –

Collector – Once any component sends the trace data arrives to Zipkin collector daemon, it is validated, stored, and indexed for lookups by the Zipkin collector.

Storage – This module store and index the lookup data in backend. Cassandra, ElasticSearch and MySQL are supported.

Search – This module provides a simple JSON API for finding and retrieving traces stored in backend. The primary consumer of this API is the Web UI.

Web UI – A very nice UI interface for viewing traces.

=======
Zipkin is very efficient tool for distributed tracing in microservices ecosystem. Distributed tracing, in general, is latency measurement of each component in a distributed transaction where multiple microservices are invoked to serve a single business usecase. Let’s say from our application, we have to call 4 different services/components for a transaction. Here with distributed tracing enabled, we can measure which component took how much time.

This is useful during debugging when lots of underlying systems are involved and the application becomes slow in any particular situation. In such case, we first need to identify see which underlying service is actually slow. Once the slow service is identified, we can work to fix that issue. Distributed tracing helps in identifying that slow component among in the ecosystem.


Sleuth
========
Sleuth is a tool from Spring cloud family. It is used to generate the trace id, span id and add these information to the service calls in the headers and MDC, so that It can be used by tools like Zipkin and ELK etc. to store, index and process log files. As it is from spring cloud family, once added to the CLASSPATH, it automatically integrated to the common communication channels like –

requests made with the RestTemplate etc.
requests that pass through a Netflix Zuul microproxy
HTTP headers received at Spring MVC controllers
requests over messaging technologies like Apache Kafka or RabbitMQ etc.
Using Sleuth is very easy. We just need to add it’s started pom in the spring boot project. It will add the Sleuth to project and so in its runtime.



Registering Client Application With Zipkin Server

 <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-zipkin</artifactId>
  </dependency>
	

application.properties	

spring.zipkin.base-url=http://localhost:9041


day8
=====
zipkin-server       (zipkin-server,zipkin-autoconfigure-ui,spring-cloud-starter-zipkin)  9041
product-service =>(sleuth,spring-cloud-starter-zipkin)  2222
customer-service=>(sleuth,spring-cloud-starter-zipkin)  1111
greeting-service=>(sleuth,spring-cloud-starter-zipkin)  8484


17-May-2019
============

JMS (Java Messaging Service) :To develop a java application to send and recevie messages in synchronus and asynchronus way 


Types of commmuncation
=======================
1.synchronus => Sender and receiver should be online (Phone calling)
2.asynchronus => Sender / receiver need not be online (SMS,Whatsapp,Email)


MOM (Message Oriented Middlware) (JBoss,Oracle Weblogic,Active MQ,Rabbit MQ,IBM Websphere,MQ Series)

Apache Kafka =>Producing messages =>Producer and Consumer


1.Point to Point (One to One) =>Queue 
  
  One message will have one consumer only
  
2.Publisher to Subscriber (One to Many) =>Topic

   One message will have one/more consumer 
  

1.JMS in memory Active MQ
    Producer ->
	   JMSTemplate->
	               ->Queue
      	                   =>Consumer1
						   =>Consumer2
			   
			 
      

2.JMS  stand alone Active MQ

To start Active MQ
c:\apache-activemq-5.15.8\bin>activemq start 

Active MQ Web Console  :http://localhost:8161/
  username :admin
  password :admin
    
  
  
  
  
  
  
  
  
  
  

  
 Apache Kafka
=============
Apache Kafka is an open-source stream-processing software platform developed by LinkedIn and donated to the Apache Software Foundation, written in Scala and Java. The project aims to provide a unified, high-throughput, low-latency platform for handling real-time data feeds.


Apache Kafka is a community distributed event streaming platform capable of handling trillions of events a day. Initially conceived as a messaging queue, Kafka is based on an abstraction of a distributed commit log.



1. Producer 
==========
 An application that sends the messages(data or record ) to kafka Server


Message :
                  1.Small to medium sized piece of data
                  2.It may have some meaning or some schema for us but for apache kafka It is simple array of bytes.



2. Consumer
                An application which reads the data from Kafka Server.


                Producer1                             Consumer1
				                 Kafka Server
                Producer2 			                  Consumer2	

3. Broker
                   It is a Kafka Server.
                   It's a just meaningful name given to kafka server
                   Kafka Server acts as a broker between Producer and Consumer
                   Producer and Consumer don't interact directly
                   They use Kafka Server as a agent or broker to exchange the messages
        
4. Cluster
            A group of computers sharing the workload for common purpose.
            Kafka is a distrubuted system. so Cluster as same meaning as kafka.


5. Topic

                 Topic is a arbitary name for kafka stream


6. Partitions
                     The data stored in a topic is huge or it is beyond storage capacity of a single computer.
                      In this case Broker may have challange to store this data.
                      One of the solution is to break that data in to 2 or more parts and distrubute it to a multiple computers.
                      Kafka is a distrubuted system that runs on cluster of computers.
                      Kafka can break the topic in partitions and store one partition on one computer.  
                      But how many partitions?
                      How kafka will decide that whether it has do 100 or 10 partiotions.
                      Kafka will no take any decision. We have to take this decision.
                      


7. Offset
                      It is a sequence no of a message in a partition.This number will be assigned to message as soon as message arrives.
                      This sequence will not change .it is immutable.Kafka stores the message in a sequence in which they arrives.The offset
                       starts from zero.offsets are local to the partitions and not local to gloabal.
					   
		

 Topic     
         partition1     m-0,m-1,m-2
		 partition2     m-0,m-1,m-2
		 
		 
		 
		 
					   
					   

                         Global uniqueue idenetifier of a message.
                                      Topic Name ->Partition Number->Offset =>using these three thins you can locate a message.
 

8. Consumer groups
                        A group of consumers acting as a single logical unit.

                       Partioning and consumer group  is a tool for scalability.

                       Maximum no of consumers in a group is total no of partitions in a topic.      

                       Kafka doesn't allow more than 2 consumers to read data from one partition of the topic simultaneously.
                       This restriction is necessary of double reading of records. 




Apache ZooKeeper is an effort to develop and maintain an open-source server which enables highly reliable distributed coordination.


What is ZooKeeper?

ZooKeeper is used for managing and coordinating Kafka broker. ZooKeeper service is mainly used to notify producer and consumer about the presence of any new broker in the Kafka system or failure of the broker in the Kafka system. As per the notification received by the Zookeeper regarding presence or failure of the broker then pro-ducer and consumer takes decision and starts coordinating their task with some other broker.

 
Apache Kafka Download  :
===================
https://kafka.apache.org/downloads  =>binary 


To start Zookeeper
==================
c:\kafka_2.12-2.2.0\bin\windows>zookeeper-server-start.bat ..\..\config\zookeeper.properties


To start a Kafka Server
============================
c:\kafka_2.12-2.2.0\bin\windows>kafka-server-start.bat ..\..\config\server.properties


To create a topic
==============

C:\kafka_2.11-2.1.0\bin\windows>kafka-topics.bat --zookeeper localhost:2181 --create --topic MyFirstTopic --partitions 2 --replication-factor 1

Created topic "MyFirstTopic".

C:\kafka_2.11-2.1.0\bin\windows>


To start a Console Producer
==============================

C:\kafka_2.11-2.1.0\bin\windows>kafka-console-producer.bat --broker-list localhost:9092 --topic MyFirstTopic
>

To start a Console Consumer
==============================
C:\kafka_2.11-2.1.0\bin\windows>kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic MyFirstTopic


Client Side Load balancing (Clustering)  and  
============================================================


customer-service=>product-service=>order-service=>payment-service


restfull api =>
            RestTemplate 


			
Hystrix
			













 
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
Spring Boot Security
=====================
JAAS (Java Authentication and Authorization Service)

1.Basic (Spring Boot1.x by default uses Basic Authentication)
2.Digest
3.Form  (Spring Boot2.x by default uses Form based Authentication)

<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-security</artifactId>
</dependency>

A)In Memory
B)Database Authentication (users,roles)
C)OAuth2 





Spring Cloud Netflix: Load Balancer with Ribbon/Feign
=========================================================

You can use Spring Cloud Netflix to provide client-side load balancing in calls to another microservice.

The idea in this post is to show some concepts about load balancing, Ribbon and Feign, and step by step process for working with Ribbon and Feign.

Load Balancing
===============

Load Balancing automatically distributes incoming application traffic between two or more computers. It enables you to achieve fault tolerance in your applications, seamlessly providing the required amount of load balancing capacity needed to route application traffic. Load balancing aims to optimize resource use, maximize throughput, minimize response time, and avoid overload of any single resource. Using multiple components with load balancing instead of a single component may increase reliability and availability through redundancy.


===
Ribbon: Load Balancer Without Eureka 
====================================

Ribbon is a client-side load balancer, which gives you a lot of control over the behavior of HTTP and TCP clients. Ribbon's Client component offers a good set of configuration options such as connection timeouts, retries, retry algorithm (exponential, bounded back off) etc. Ribbon comes built in with a pluggable and customizable Load Balancing component. 

Some of the load balancing strategies offered are listed below:

Simple Round Robin LB
Weighted Response Time LB
Zone Aware Round Robin LB
Random LB


Client-Side Load Balancing
==========================

An approach to load balancing is to deliver a list of server IPs to the client, and then to have client randomly select the IP from the list on each connection. It has been claimed that client-side random load balancing tends to provide better load distribution than round-robin DNS. With this approach, the method of delivery of lists of IPs to the client can vary, and may be implemented as a DNS list (delivered to all the clients without any round-robin), or via hardcoding it to the list. If a "smart client" is used, detecting that randomly selected server is down and connecting randomly again, it also provides fault tolerance.

Ribbon provides the following features:
=======================================
Load balancing
Fault tolerance
Multiple protocols (HTTP, TCP, UDP) support in an asynchronous and reactive model
Caching and batching



Enabling Ribbon
================
Add Ribbon Dependency to pom.xml

    <dependency>
      <groupId>org.springframework.cloud</groupId>
      <artifactId>spring-cloud-starter-netflix-ribbon</artifactId>
    </dependency>

Fault Tolerance with Hystrix
=============================
Microservices must be extremely reliable because they depend on each other. The microservice architecture contains a large number of small microservices. These microservices communicate with each other in order to fulfill their requirements.

The instances of microservices may go up and down frequently. As the number of interactions between microservices increases, the chances of failure of the microservice also increases in the system.

Fault Tolerance
===============
Consider a scenario in which six microservices are communicating with each other. The microservice-5 becomes down at some point, and all the other microservices are directly or indirectly depend on it, so all other services also go down.



Fault tolerance can be achieved with the help of a circuit breaker. It is a pattern that wraps requests to external services and detects when they fail. If a failure is detected, the circuit breaker opens. All the subsequent requests immediately return an error instead of making requests to the unhealthy service. It monitors and detects the service which is down and misbehaves with other services. It rejects calls until it becomes healthy again.

Hystrix
Hystrix is a library that controls the interaction between microservices to provide latency and fault tolerance. Additionally, it makes sense to modify the UI to let the user know that something might not have worked as expected or would take more time.


Fallback method
================

The fallback method is a method that invokes when a fault occurs. Hystrix allows us to define a fallback method for each service method. Here one question arises that if the method throws an exception, what should be returned to the consumer?

So answer is that if method() fails, the method fallbackmethod() is called. The fallback method returns the hardcoded message instance.


Hystrix =>Circuit Broker

While the circuit is open, Hystrix redirects calls to the method, and they're passed on to our specified fallback method. Spring Cloud Netflix Hystrix looks for any method annotated with the @HystrixCommand annotation, and wraps that method in a proxy connected to a circuit breaker so that Hystrix can monitor it.

Netflix has created a library called Hystrix that implements the circuit breaker pattern. In a microservice architecture, it is common to have multiple layers of service calls,



Hystrix is a library that controls the interaction between microservices to provide latency and fault tolerance. Additionally, it makes sense to modify the UI to let the user know that something might not have worked as expected or would take more time.






Assignment
==========
https://github.com/cassiomolin/microservices-springboot






Pivotal Cloud Foundry (PAAS)
=====================
Pivotal Cloud Foundry, also known as PCF, is a distribution of the open-source Cloud Foundry platform that includes additional features and services that expand the capabilities of Cloud Foundry and make it easier to use.



Cloud Foundry is an open source, multi-cloud application platform as a service (PaaS) governed by the Cloud Foundry Foundation, a 501(c)(6) organization.[1]

The software was originally developed by VMware, transferred to Pivotal Software (a joint venture by EMC, VMware and General Electric) but brought back into VMware at the end of 2019 with VMware's take over of Pivotal.


Register on PCF
=================
https://account.run.pivotal.io/z/uaa/sign-up


To Login
=========
https://login.run.pivotal.io/login









Install CF cli tool
=======================
https://github.com/cloudfoundry/cli#downloads



PCF Login
=========


C:\Users\PRADEEP>cf login -o pradeepch82-org -s development
API endpoint: https://api.run.pivotal.io

Email: dharmendrapradeep@gmail.com

Password:
Authenticating...
OK

Targeted org pradeepch82-org

Targeted space development


API endpoint:   https://api.run.pivotal.io (API version: 3.82.0)
User:           dharmendrapradeep@gmail.com
Org:            pradeepch82-org
Space:          development



cf commands
==============

cf version 6.51.0+2acd15650.2020-04-07, Cloud Foundry command line tool
Usage: cf [global options] command [arguments...] [command options]

Before getting started:
  config    login,l      target,t
  help,h    logout,lo

Application lifecycle:
  apps,a        run-task,rt    events
  push,p        logs           set-env,se
  start,st      ssh            create-app-manifest
  stop,sp       app            delete,d
  restart,rs    env,e
  restage,rg    scale

Services integration:
  marketplace,m        create-user-provided-service,cups
  services,s           update-user-provided-service,uups
  create-service,cs    create-service-key,csk
  update-service       delete-service-key,dsk
  delete-service,ds    service-keys,sk
  service              service-key
  bind-service,bs      bind-route-service,brs
  unbind-service,us    unbind-route-service,urs

Route and domain management:
  routes,r        delete-route    create-domain
  domains         map-route
  create-route    unmap-route

Space management:
  spaces         create-space    set-space-role
  space-users    delete-space    unset-space-role

Org management:
  orgs,o       set-org-role
  org-users    unset-org-role

CLI plugin management:
  plugins           add-plugin-repo      repo-plugins
  install-plugin    list-plugin-repos

Commands offered by installed plugins:

Global options:
  --help, -h                         Show help
  -v                                 Print API request diagnostics to stdout







https://springboot-ems-app.cfapps.io/semployees




cf push tea-app --docker-image pradeepch82/tea:1.1 --docker-username pradeepch82
 
 
 
 PCF
 ===
Q: What is Pivotal Cloud Foundry?
A: Cloud Foundry is an open source cloud computing platform originally developed in-house at VMware. It is a platform (PaaS) for cloud native application, it helps developer to just focus on code rather worrying about platform they use and their configurations.

Q: What are the advantages of Pivotal Cloud Foundry(PCF)?
A: The advantages of using Pivotal Cloud Foundry(PCF) are as follows-
Fast application development and deployment.
Highly scalable and available architecture.
DevOps-friendly workflows.
Reduced chance of human error.
Multi-tenant compute efficiencies.

Q: What is Cloud Foundry BuildPack?
A: Buildpacks provide framework and runtime support for apps. Buildpacks typically examine your apps to determine what dependencies to download and how to configure the apps to communicate with bound services. When you push an app, Cloud Foundry automatically detects an appropriate buildpack for it. This buildpack is used to compile or prepare your app for launch.

Q: What is CLI? How to use it?
A: The Cloud Foundry (cf) command line interface (CLI) provides a set of commands for managing your apps. We will need to download and install this interface for our windows machine.
Download the CF Windows installer. It will prompt for the download. Save the zip file distribution.
After successfully unzip operation, double click on the CF CLI executable.


To list all of the cf commands and associated help information, use cf help. Use cf command_name -h to view detailed help information for a particular command.


cf commands
==============

cf version 6.51.0+2acd15650.2020-04-07, Cloud Foundry command line tool

Usage: cf [global options] command [arguments...] [command options]

Before getting started:
  config    login,l      target,t
  help,h    logout,lo

Application lifecycle:
  apps,a        run-task,rt    events
  push,p        logs           set-env,se
  start,st      ssh            create-app-manifest
  stop,sp       app            delete,d
  restart,rs    env,e
  restage,rg    scale

Services integration:
  marketplace,m        create-user-provided-service,cups
  services,s           update-user-provided-service,uups
  create-service,cs    create-service-key,csk
  update-service       delete-service-key,dsk
  delete-service,ds    service-keys,sk
  service              service-key
  bind-service,bs      bind-route-service,brs
  unbind-service,us    unbind-route-service,urs

Route and domain management:
  routes,r        delete-route    create-domain
  domains         map-route
  create-route    unmap-route

Space management:
  spaces         create-space    set-space-role
  space-users    delete-space    unset-space-role

Org management:
  orgs,o       set-org-role
  org-users    unset-org-role

CLI plugin management:
  plugins           add-plugin-repo      repo-plugins
  install-plugin    list-plugin-repos

Commands offered by installed plugins:

Global options:
  --help, -h                         Show help
  -v                                 Print API request diagnostics to stdout





https://github.com/pradeepch82/cicd-jenkins-example


cf push coffee-app --docker-image pradeepch82/coffee:1.1 --docker-username pradeepch82










Pivotal Cloud Foundry(PCF) Interview Questions.
Ad by Valueimpression
In this post we will look at Pivotal Cloud Foundry (PCF) questions. Examples are provided with explanation.


Q: What is Pivotal Cloud Foundry?
A: Cloud Foundry is an open source cloud computing platform originally developed in-house at VMware. It is a platform (PaaS) for cloud native application, it helps developer to just focus on code rather worrying about platform they use and their configurations.

Q: What are the advantages of Pivotal Cloud Foundry(PCF)?
A: The advantages of using Pivotal Cloud Foundry(PCF) are as follows-
Fast application development and deployment.
Highly scalable and available architecture.
DevOps-friendly workflows.
Reduced chance of human error.
Multi-tenant compute efficiencies.


Q: What is Cloud Foundry BuildPack?
A: Buildpacks provide framework and runtime support for apps. Buildpacks typically examine your apps to determine what dependencies to download and how to configure the apps to communicate with bound services. When you push an app, Cloud Foundry automatically detects an appropriate buildpack for it. This buildpack is used to compile or prepare your app for launch.

Q: What is CLI? How to use it?
A: The Cloud Foundry (cf) command line interface (CLI) provides a set of commands for managing your apps. We will need to download and install this interface for our windows machine.
Download the CF Windows installer. It will prompt for the download. Save the zip file distribution.
After successfully unzip operation, double click on the CF CLI executable. Install this executable-
CF CLI executable

To list all of the cf commands and associated help information, use cf help. Use cf command_name -h to view detailed help information for a particular command.
CF CLI help

Q: How to deploy Spring Boot Application to PCF?
A: Deploying Spring Boot Application to PCF

Q: How to deploy Spring Boot + MySQL Application to PCF?
A: Pivotal Cloud Foundry Tutorial - Deploying Spring Boot + MySQL Application to PCF

Q: How to deploy Spring Boot + RabbitMQ Application to PCF?
A: Pivotal Cloud Foundry Tutorial - Deploying Spring Boot + RabbitMQ Application to PCF

Q: What are various Roles and associated permissions in PCF?
A:
Role	Permissions

Admin	An admin user has permissions on all orgs and spaces

Admin Read-Only	This role has read-only access to all Cloud Controller API resources.
Global Auditor	This role has read-only access to all Cloud Controller API resources except for secrets such as environment variables.

Org Managers	managers or other users who need to administer the org
Org Auditors	view but cannot edit user information and org quota usage information

Org Billing Managers	create and manage billing account and payment information

Org Users	Can view the list of other org users and their roles. When an Org Manager gives a person an 

Org or Space role, that person automatically receives Org User status in that Org

Space Managers	Managers or other users who administer a space within an org

Space Developers	Application developers or other users who manage applications and services in a space

Space Auditors	View but cannot edit the space

Q: What is difference between IaaS vs PaaS?

A:PaaS, or solution stack, offers a more comprehensive approach to the cost effective application deployment need of today's developers. This service provides the necessary hardware architecture and software framework needed to put an application into service, without having to own, manage and upkeep all the required resources.
IaaS, in comparison to the PaaS, provides equipment for operations, networking, data storage and hardware with the use of the internet, so that the subscriber is no longer confronted with location and purchase costs.


On-premises IT infrastructure is like owning a car. We have to take full responsibility for its upkeep. If needs to use latest car we will need to buy new one then.

IaaS is like renting a car. When you rent a car, we choose which ever car we want and then drive to our destination ourselves.If we need latest car we then rent another car

PaaS is like taking a taxi. We dont need to drive it. We just tell the driver the destination and he drives us around while we relax


Q: What are types of cloud computing?
Ans:

Iaas (Infrastructure as a Service)
Replacement for physical hardware
Provides virtual hardware , OS, Network

Amazon Web Services (AWS), RackSpace, Microsoft Azure, VMware vCloudAir

PaaS (Platform as a Service)
More than a raw machine with OS
Provides ready-made Platform for running apps

CloudFoundry, Heroku, Google App Engine, Amazon Elastic Beanstalk
SaaS (Software as a Service)
Complete Software Application
SaleForce.com, Google Apps etc





the next right thing...
Home
Spring
Java
Front-end
Cloud
Interview Questions
Know Us


















Cloud Foundry - Ultimate Guide to PCF Interview Questions (2020)
PCF - Cloud Foundry Interview Questions

 
Cloud Foundry Interview Questions
In this article, we explore the Cloud Foundry Interview Questions & Answers for Experienced or Freshers. we are trying to share experience and learning to helps you advance your career as Cloud Foundry Developer.

Cloud platform like platform as a service (PaaS) gaining lots of importance in today's world, and many reputed companies has a growing its usage day over day. At TechGeekNext, Pivotal Cloud Foundry is one of our key focus area of our site, we provide number of technology article around Cloud Foundry.

Q: What is the Cloud Foundry?
Q: What do you understand by "The Cloud"?
Q: What are types of cloud computing?
Q: Why Cloud Foundry?
Q: What are the components in Cloud Foundry and Cloud Foundry Architecture?
Q: How to deploy Spring Boot + MySQL Application to Cloud Foundry (PCF)?
Q: How to deploy Spring Boot + RabbitMQ Application to Cloud Foundry (PCF)?
Q: What is difference between restart and restage in Cloud Foundry (PCF)?
Q: What is stagging in Cloud Foundry?
Q: What is droplet in Cloud Foundry?
Q: What is Cloud Foundry log aggregator and it's architecture?
Q: What is UAA in Cloud Foundry (PCF)?
Q: What are the features of UAA in Cloud Foundry (PCF)?
Q: What are the steps to deploy application in Iaas and PaaS (Cloud Foundry - PCF)
Q: What is cloud foundry VCAP?
Q: What is Manifests?
Q: What is Organization, Spaces, and Domains?
Q: What is Services?
Q: What is CLI utility and how to use?
Q: What are some basic command in CF?
Q: In how many ways we can use Pivotal Cloud Foundry?
Q: How memory allocation happens?
Q: Can we use third party log mangers in Cloud Foundry (PCF)?
Q: What is a Buildpack?
Q: How Cloud Foundry different from AWS?
Q: What is Cloud Foundry container?
Q: Is Cloud Foundry a container?
Q: What is the Cloud Foundry?
Ans:
Cloud Foundry is an open source cloud computing platform originally developed in-house at VMware. It is a platform (PaaS) for cloud native application, it helps developer to just focus on code rather worrying about platform they use and their configurations.
Q: What do you understand by "The Cloud"?
Ans:
Distributed applications accessible over network.
Resource on Demand : On-demand cloud computing allow provide resources on an "as needed" basis to client, rather than all at once. Advantages are Efficient Resources Management, Reduced Costs etc.
Can run in-house (private cloud) as well.
Hardware and Software sold as commodity
Inherently Virtualized : Because of this feature, there are many benefits like Cost reduction, Clean up the environment.,Uptime increase,Faster provisioning, Easier backup.

Q: What are types of cloud computing?
Ans:
Iaas (Infrastructure as a Service)
Replacement for physical hardware
Provides virtual hardware , OS, Network
Amazon Web Services (AWS), RackSpace, Microsoft Azure, VMware vCloudAir
PaaS (Platform as a Service)
More than a raw machine with OS
Provides ready-made Platform for running apps
CloudFoundry, Heroku, Google App Engine, Amazon Elastic Beanstalk
SaaS (Software as a Service)
Complete Software Application
SaleForce.com, Google Apps etc.
Cloud Foundry Architecture

Q: Why Cloud Foundry?
Open Source : Reduce vendor lock
Public OR Private
Language Independence - Via Buildpacks
Wide growing range of services

Q: What do you understand by "The Cloud"?
Ans:
Distributed applications accessible over network.
Resource on Demand : On-demand cloud computing allow provide resources on an "as needed" basis to client, rather than all at once. Advantages are Efficient Resources Management, Reduced Costs etc.
Can run in-house (private cloud) as well.
Hardware and Software sold as commodity
Inherently Virtualized : Because of this feature, there are many benefits like Cost reduction, Clean up the environment.,Uptime increase,Faster provisioning, Easier backup.



Q: What is RabbitMQ?

RabbitMQ is also known as message queueing technology or message broker. It's an open source message broker. Simply stated: it is program that determines queues and which applications connect to send messages or messages. Any kind of information can be given in a message.




PCF components
==============
Routing
=======
Router

The router routes incoming traffic to the appropriate component, either a Cloud Controller component or a hosted application running on a Diego Cell.

The router periodically queries the Diego Bulletin Board System (BBS) to determine which cells and containers each application currently runs on. Using this information, the router recomputes new routing tables based on the IP addresses of each cell virtual machine (VM) and the host-side port numbers for the cell’s containers.


App Lifecycle
================

Cloud Controller and Diego Brain
The Cloud Controller (CC) directs the deployment of applications. To push an app to CF, you target the Cloud Controller. The Cloud Controller then directs the Diego Brain through the CC-Bridge components to coordinate individual Diego cells to stage and run applications.

The Cloud Controller also maintain records of orgs, spaces, user roles, services, and more.

nsync, BBS, and Cell Reps
To keep applications available, cloud deployments must constantly monitor their states and reconcile them with their expected states, starting and stopping processes as required.


The nsync, BBS, and Cell Rep components work together along a chain to keep apps running. At one end is the user. At the other end are the instances of applications running on widely-distributed VMs, which may crash or become unavailable.

Here is how the components work together:

nsync receives a message from the Cloud Controller when the user scales an app. It writes the number of instances into a DesiredLRP structure in the Diego BBS database.
BBS uses its convergence process to monitor the DesiredLRP and ActualLRP values. It launches or kills application instances as appropriate to ensure the ActualLRP count matches the DesiredLRP count.
Cell Rep monitors the containers and provides the ActualLRP value.
























 
 




