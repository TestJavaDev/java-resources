---
layout: default
title: Microservices Core
parent: Microservices
nav_order: 1
permalink: /microservices/core
---
<div align="center" markdown="1">
Microservices Core / Java resources / Grokking the interview

{: .fs-6 .fw-300 }
</div>

## Microservices core 

## Cloud

What exactly is the cloud?
Cloud computing is the delivery of computing and virtualized IT services—databases, networking, software, servers, analytics, and more—through the internet to provide a
flexible, secure, and easy-to-use environment. Cloud computing offers significant advantages in the internal management of a company, such as low initial investment,
ease of use and maintenance, and scalability, among others. The cloud computing models let the user choose the level of control over the
information and services that these provide. These models are known by their acronyms, and are generically referred to as XaaS—an acronym that means anything as a
service. The following lists the most common cloud computing models. 
Differences between these models:
* Infrastructure as a Service (IaaS)—The vendor provides the infrastructure that lets
you access computing resources such as servers, storage, and networks. In this
model, the user is responsible for everything related to the maintenance of the
infrastructure and the scalability of the application.
IaaS platforms include AWS (EC2), Azure Virtual Machines, Google Compute Engine, and Kubernetes.
* Container as a Service (CaaS)—An intermediate model between the IaaS and the
PaaS, it refers to a form of container-based virtualization. Unlike an IaaS model,
where a developer manages the virtual machine to which the service is
deployed, with CaaS, you deploy your microservices in a lightweight, portable
virtual container (such as Docker) to a cloud provider. The cloud provider runs
the virtual server the container is running on, as well as the provider’s comprehensive tools for building, deploying, monitoring, and scaling containers.
CaaS platforms include Google Container Engine (GKE) and Amazon’s Elastic Container Service (ECS).
* Platform as a Service (PaaS)—This model provides a platform and an environment that allow users to focus on the development, execution, and maintenance of the application. The applications can be created with tools that are
provided by the vendor (for example, operating system, database management
systems, technical support, storage, hosting, network, and more). Users do not
need to invest in a physical infrastructure, nor spend time managing it, allowing
them to concentrate exclusively on the development of applications.
PaaS platforms include Google App Engine, Cloud Foundry, Heroku, and
AWS Elastic Beanstalk.
* Function as a Service (FaaS)—Also known as serverless architecture, despite the
name, this architecture doesn’t mean running specific code without a server.
What it means is a way of executing functionalities in the cloud in which the
vendor provides all the required servers. Serverless architecture allows us to
focus only on the development of services without having to worry about scaling
provisioning, and server administration. Instead, we can solely concentrate on
uploading our functions without handling any administration infrastructure.
FaaS platforms include AWS (Lambda), Google Cloud Function, and Azure
functions.
* Software as a Service (SaaS)—Also known as software on demand, this model allows
users to use a specific application without having to deploy or to maintain it. In
most cases, the access is through a web browser. Everything is managed by the service provider: application, data, operating system, virtualization, servers, storage,
and network. The user just hires the service and uses the software.
SaaS platforms include Salesforce, SAP, and Google Business.
![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro1.png)

###  Microservices are more than writing the code

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro2.png)

Writing a robust service includes considering several topics. Let’s walk through the
items show in more detail:
* Right-sized—How you ensure that your microservices are properly sized so that
you don’t have a microservice take on too much responsibility. Remember,
properly sized, a service allows you to make changes to an application quickly
and reduces the overall risk of an outage to the entire application.
* Location transparent—How you manage the physical details of service invocation.
When in a microservice application, multiple service instances can quickly start
and shut down.
* Resilient—How you protect your microservice consumers and the overall integrity of your application by routing around failing services and ensuring that you
take a “fail-fast” approach.
* Repeatable—How you ensure that every new instance of your service brought up
is guaranteed to have the same configuration and codebase as all the other service instances in production.
* Scalable—How you establish a communication that minimizes the direct dependencies between your services and ensures that you can gracefully scale your
microservices. 

### Core microservice development pattern
![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro3.png)

The following patterns show the basics of building a microservice:
* Service granularity—How do you approach decomposing a business domain
down into microservices so that each microservice has the right level of responsibility? Making a service too coarse-grained with responsibilities that overlap
into different business-problems domains makes the service difficult to maintain and change over time. Making the service too fine-grained increases the
overall complexity of the application and turns the service into a “dumb” data
abstraction layer with no logic except for that needed to access the data store.
* Communication protocols—How will developers communicate with your service?
The first step is to define whether you want a synchronous or asynchronous protocol. For synchronous, the most common communication is HTTP-based REST
using XML (Extensible Markup Language), JSON (JavaScript Object Notation),
or a binary protocol such as Thrift to send data back and forth to your microservices. For asynchronous, the most popular protocol is AMQP (Advanced Message
Queuing Protocol) using a one-to-one (queue) or a one-to-many (topic) with
message brokers such as RabbitMQ, Apache Kafka, and Amazon Simple Queue
Service (SQS).
* Interface design—What’s the best way to design the actual service interfaces that
developers are going to use to call your service? How do you structure your services? What are the best practices? Best practices and interface design are covered in the next chapters.
* Configuration management of service—How do you manage the configuration of
your microservice so that it moves between different environments in the
cloud?
* Event processing between services—How do you decouple your microservice using
events so that you minimize hardcoded dependencies between your services
and increase the resiliency of your application

## Microservice routing patterns

The microservice routing patterns deal with how a client application that wants to consume a microservice discovers the location of the service and is routed over to it.
In a cloud-based application, it is possible to have hundreds of microservice instances running. To enforce security and content policies, it is required to abstract the physical IP address of those services and have a single point of entry for the service calls.
How?  The following patterns are going to answer that question:
* Service discovery—With service discovery and its key feature, service registry, you
can make your microservice discoverable so client applications can find them
without having the location of the service hardcoded into their application.
How?. Remember the service discovery is an internal service, not a client-facing service.
Note that in this book, we use Netflix Eureka Service Discovery, but there are
other service registries such as etcd, Consul, and Apache Zookeeper. Also, some
systems do not have an explicit service registry. Instead these use an interservice
communication infrastructure known as a service mesh.
* Service routing—With an API Gateway, you can provide a single entry point for
all of your services so that security policies and routing rules are applied uniformly to multiple services and service instances in your microservices applications. How? With the Spring Cloud API Gateway

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro4.png)

## Microservice client resiliency

Because microservice architectures are highly distributed, you have to be extremely sensitive in how you prevent a problem in a single service (or service instance) from
cascading up and out to the consumers of the service. To this end, we’ll cover four client resiliency patterns:
* Client-side load balancing—How you cache the location of your service instances
on the service so that calls to multiple instances of a microservice are load balanced to all the health instances of that microservice.
* Circuit breaker pattern—How you prevent a client from continuing to call a service that’s failing or suffering performance problems. When a service is running slowly, it consumes resources on the client calling it. You want these
microservice calls to fail fast so that the calling client can quickly respond and
take appropriate action.
* Fallback pattern—When a service call fails, how you provide a “plug-in” mechanism that allows the service client to try to carry out its work through alternative
means other than the microservice being called.
* Bulkhead pattern—Microservice applications use multiple distributed resources
to carry out their work. This pattern refers to how you compartmentalize these
calls so that the misbehavior of one service call doesn’t negatively impact the
rest of the application.

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro5.png)

## Microservice security patterns

To ensure that the microservices are not open to the public, it is important to apply the following security patterns to the architecture in order to ensure that only granted
requests with proper credentials can invoke the services.We can implement these three patterns to build an authentication service that can protect your microservices:
* Authentication—How you determine the service client calling the service is who
they say they are.
* Authorization—How you determine whether the service client calling a microservice is allowed to undertake the action they’re trying to take.
* Credential management and propagation—How you prevent a service client from
constantly having to present their credentials for service calls involved in a transaction. To achieve this, we’ll look at how you can use token-based security standards such as OAuth2 and JSON Web Tokens (JWT) to obtain a token that can
be passed from service call to service call to authenticate and authorize the user

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro6.png)

## Microservice logging and tracing patterns

The downside of a microservice architecture is that it’s much more difficult to debug, trace, and monitor the issues because one simple action can trigger numerous microservice calls within your application. 
Distributed tracing with Spring Cloud Sleuth, Zipkin, and the ELK Stack. For this reason, we’ll look at the following three core logging and tracing patterns to achieve distributed tracing:
* Log correlation—How you tie together all the logs produced between services for a
single user transaction. With this pattern, we’ll look at how to implement a correlation ID, which is a unique identifier that’s carried across all service calls in a transaction and that can be used to tie together log entries produced from each service.
* Log aggregation—With this pattern, we’ll look at how to pull together all of the
logs produced by your microservices (and their individual instances) into a single queryable database across all the services involved and understand the performance characteristics of the services in the transaction.
* Microservice tracing—We’ll explore how to visualize the flow of a client transaction across all the services involved and understand the performance characteristics of the transaction’s services.
![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro7.png)

## Application metrics pattern

The application metrics pattern deals with how the application is going to monitor metrics and warn of possible causes of failure within our applications. This pattern
shows how the metrics service is responsible for getting (scraping), storing, and querying business-related data in order to prevent potential performance issues in our services. This pattern contains the following three main components:
* Metrics—How you create critical information about the health of your application and how to expose those metrics
* Metrics service—Where you can store and query the application metrics
* Metrics visualization suite—Where you can visualize business-related time data for the application and infrastructure
Picture shows how the metrics generated by the microservices are highly dependent on the metrics service and the visualization suite. It would be useless to have metrics that
generate and show infinite information if there is no way to understand and analyze that information. The metrics service can obtain the metrics using the pull or push style:
* With the push style, the service instance invokes a service API exposed by the
metrics service in order to send the application data.
* With the pull style, the metrics service asks or queries a function to fetch the
application data.

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro8.png)

## Microservice build/deployment patterns

One of the core parts of a microservice architecture is that each instance of a microservice should be identical to all its other instances. You can’t allow configuration drift
(something changes on a server after it’s been deployed) to occur because this can
introduce instability in your applications.
 The goal with this pattern is to integrate the configuration of your infrastructure
right into your build/deployment process so that you no longer deploy software artifacts such as Java WAR or EAR files to an already running piece of infrastructure.
Instead, you want to build and compile your microservice and the virtual server image
it’s running on as part of the build process. Then, when your microservice gets
deployed, the entire machine image with the server running on it gets deployed. Figure
1.17 illustrates this process. At the end of the book, we’ll look at how to create your
build/deployment pipeline. Following patterns and topics:
* Build and deployment pipelines—How you create a repeatable build and deployment process that emphasizes one-button builds and deployment to any environment in your organization.
* Infrastructure as code—How you treat the provisioning of your services as code
that can be executed and managed under source control.
* Immutable servers—Once a microservice image is created, how you ensure that
it’s never changed after it has been deployed.
* Phoenix servers—How you ensure that servers that run individual containers get
torn down on a regular basis and re-created from an immutable image. The
longer a server is running, the more opportunity there is for configuration
drift. A configuration drift can occur when ad hoc changes to a system configuration are unrecorded.
Our goal with these patterns and topics is to ruthlessly expose and stamp out configuration drift as quickly as possible before it can hit your upper environments (stage or
production).

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro9.png)

## Give it a REST

* Use HTTP/HTTPS as the invocation protocol for the service —An HTTP endpoint
exposes the service, and the HTTP protocol carries data to and from the
service.
* Map the behavior of the service to standard HTTP verbs —REST emphasizes
having services that map their behavior to the HTTP verbs POST, GET, PUT,
and DELETE. These verbs map to the CRUD functions found in most services.
* Use JSON as the serialization format for all data going to and from the
service —This isn’t a hard-and-fast principle for REST-based microservices,
but JSON has become “lingua franca” for serializing data that’s submitted
and returned by a microservice. You can use XML, but many REST-based
applications make use of JavaScript and JSON. JSON is the native format for
serializing and deserializing data consumed by JavaScript-based web front
ends and services.
* Use HTTP status codes to communicate the status of a service call —The HTTP
protocol uses a rich set of status codes to indicate the success or failure of a
service. REST-based services take advantage of these HTTP status codes
and other web-based infrastructures, such as reverse proxies and caches.
These can be integrated with your microservices with relative ease.
HTTP is the language of the web. Using HTTP as the philosophical framework for building your service is key to building services in the cloud.

## Why JSON for microservices?
We can use multiple protocols to send data back and forth between HTTP-based
microservices. But JSON has emerged as the de facto standard for several reasons:
* Compared to other protocols like XML-based SOAP (Simple Object Access Protocol), JSON is extremely lightweight. You can express your data without having
much textual overhead.
* JSON is easily read and consumed by a human being. This is an underrated
quality for choosing a serialization protocol. When a problem arises, it’s critical for developers to look at a chunk of JSON and to quickly process what’s in
it. The simplicity of the protocol makes this incredibly easy to do.
* JSON is the default serialization protocol used in JavaScript. Since the dramatic rise of JavaScript as a programming language and the equally dramatic
rise of Single Page Internet Applications (SPIA) that rely heavily on JavaScript,
JSON has become a natural fit for building REST-based applications, which is
what the front-end web clients use to call services.
* Other mechanisms and protocols, however, are more efficient than JSON for
communicating between services. The Apache Thrift (http://thrift.apache.org)
framework allows you to build multilanguage services that can communicate
with one another using a binary protocol. The Apache Avro protocol
(http://avro.apache.org) is a data serialization protocol that converts data
back and forth to a binary format between client and server calls. If you need
to minimize the size of the data you’re sending across the wire, we recommend you look at these protocols. But it has been our experience that using
straight-up JSON in your microservices works effectively and doesn’t interject
another layer of communication to debug between your service consumers
and service clients.

# Service discovery

In any distributed architecture, we need to find the hostname or IP address of
where a machine is located. This concept has been around since the beginning of
distributed computing and is known formally as “service discovery.” Service discovery can be something as simple as maintaining a property file with the addresses of
all the remote services used by an application, or something as formalized as a Universal Description, Discovery, and Integration (UDDI) repository. Service discovery
is critical to microservice, cloud-based applications for two key reasons:
* Horizontal scaling or scale out—This pattern usually requires adjustments in the
application architecture, such as adding more instances of a service inside a
cloud service and more containers.
* Resiliency—This pattern refers to the ability to absorb the impact of problems
within an architecture or service without affecting the business. Microservice
architectures need to be extremely sensitive to preventing a problem in a single
service (or service instance) from cascading up and out to the consumers of the
service.

There are two main ways to implement service discovery:
* The services and their clients interact directly with the service registry.
* The deployment infrastructure handles service discovery

*[Pattern: Self registration](http://microservices.io/patterns/self-registration.html.) A service instance registers itself with the service registry.
*[Pattern: Client-side discovery](http://microservices.io/patterns/clientside-discovery.html.) A service client retrieves the list of available service instances from the service registry and load balances across them.

## The architecture of service discovery

To begin our discussion around service discovery, we need to understand four concepts.
These general concepts are often shared across all service discovery implementations:
* Service registration—How a service registers with the service discovery agent
* Client lookup of service address—How a service client looks up service information
* Information sharing—How nodes share service information
* Health monitoring—How services communicate their health back to the service discovery agent
The principal objective of service discovery is to have an architecture where our services indicate where they are physically located instead of having to manually configure their location. Figure 6.2 shows how service instances are added and removed,
and how they update the service discovery agent and become available to process user
requests.

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro15.png)

Client-side load balancing caches the location of the services so that the service client doesn’t
need to contact service discovery on every call.
This mechanism uses an algorithm like zone-specific or round-robin to invoke the instances of
the calling services. When we say “round-robin algorithm load balancing,” we are
referring to a way of distributing client requests across several servers. This consists of
forwarding a client request to each of the servers in turn. An advantage of using the
client-side load balancer with Eureka is that when a service instance goes down, it is
removed from the registry. Once that is done, the client-side load balancer updates
itself without manual intervention by establishing constant communication with the
registry service

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro16.png)

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro17.png)

## Applying the platform-provided service discovery patterns 

The deployment platform automatically load balances requests across the three instances of the Order Service. This approach is a combination of two patterns:
* 3rd party registration pattern—Instead of a service registering itself with the service registry, a third party called the registrar, which is typically part of the
deployment platform, handles the registration.
* Server-side discovery pattern—Instead of a client querying the service registry, it
makes a request to a DNS name, which resolves to a request router that queries
the service registry and load balances requests.
The key benefit of platform-provided service discovery is that all aspects of service discovery are entirely handled by the deployment platform. Neither the services nor the
clients contain any service discovery code. Consequently, the service discovery mechanism is readily available to all services and clients regardless of which language or
framework they’re written in.

- [Pattern: 3rd party registration Service instances are automatically registered with the service registry by a third party.](http://microservices.io/patterns/3rd-party-registration.html.)
- [Pattern: Server-side discovery A client makes a request to a router, which is responsible for service discovery.](http://microservices.io/patterns/server-side-discovery.html.)

# When bad things happen: Resiliency patterns

All systems, especially distributed systems, experience failure. How we build our applications to respond to that failure is a critical part of every software developer’s
job. However, when it comes to building resilient systems, most software engineers only take into account the complete failure of a piece of infrastructure or critical 
service. They focus on building redundancy into each layer of their application using
techniques such as clustering key servers, load balancing between services, and segregating infrastructure into multiple locations.
 While these approaches take into account the complete (and often spectacular) loss
of a system component, they address only one small part of building resilient systems.
When a service crashes, it’s easy to detect that it’s no longer there, and the application
can route around it. However, when a service is running slow, detecting that poor performance and routing around it is extremely difficult. Let’s look at some reasons why:
* Service degradation can start out as intermittent and then build momentum. Service
degradation might also occur only in small bursts. The first signs of failure
might be a small group of users complaining about a problem until suddenly,
the application container exhausts its thread pool and collapses completely.
* Calls to remote services are usually synchronous and don’t cut short a long-running call.
The application developer normally calls a service to perform an action and
waits for the service to return. The caller has no concept of a timeout to keep
the service call from hanging.
* Applications are often designed to deal with complete failures of remote resources, not partial degradations. Often, as long as the service has not entirely failed, an application will continue to call a poorly behaving service and won’t fail fast. In this
case, the calling application or service can degrade gracefully or, more likely,
crash because of resource exhaustion. Resource exhaustion is where a limited
resource, such as a thread pool or database connection, maxes out, and the calling client must wait for that resource to become available again.
What’s insidious about problems caused by poorly performing remote services is that
they are not only difficult to detect but can trigger a cascading effect that can ripple
throughout an entire application ecosystem. Without safeguards in place, a single,
poorly performing service can quickly take down multiple applications. Cloud-based,
microservice-based applications are particularly vulnerable to these types of outages
because these applications are composed of a large number of fine-grained, distributed services with different pieces of infrastructure involved in completing a user’s
transaction.

### What are client-side resiliency patterns?

Client-side resiliency software patterns focus on protecting a client of a remote resource (another microservice call or database lookup) from crashing when the
remote resource fails because of errors or poor performance. These patterns allow the client to fail fast and not consume valuable resources, such as database
connections and thread pools. They also prevent the problem of the poorly. performing remote service from spreading “upstream” to consumers of the client.
 
![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro18.png)

## Client-side load balancing

We introduced the client-side load balancing pattern when we
talked about service discovery. Client-side load balancing involves having the client
look up all of a service’s individual instances from a service discovery agent (like Netflix Eureka) and then caching the physical location of said service instances.
 When a service consumer needs to call a service instance, the client-side load balancer returns a location from the pool of service locations it maintains. Because the
 client-side load balancer sits between the service client and the service consumer, the
 load balancer can detect if a service instance is throwing errors or behaving poorly. If
 the client-side load balancer detects a problem, it can remove that service instance
 from the pool of available service locations and prevent any future calls from hitting
 that service instance.
  This is precisely the behavior that the Spring Cloud Load Balancer libraries
 provide out of the box (with no extra configuration). Because we’ve already covered
 client-side load balancing with Spring Cloud Load Balancer.
 
## Circuit breaker

 The circuit breaker pattern is modeled after an electrical circuit breaker. In an electrical system, a circuit breaker detects if there’s too much current flowing through the
 wire. If the circuit breaker detects a problem, it breaks the connection with the rest of
 the electrical system and keeps the system from frying the downstream components.
  With a software circuit breaker, when a remote service is called, the circuit breaker
 monitors the call. If the calls take too long, the circuit breaker intercedes and kills the
 call. The circuit breaker pattern also monitors all calls to a remote resource, and if
 enough calls fail, the circuit breaker implementation will “pop,” failing fast and preventing future calls to the failing remote resource.

## Fallback processing

 With the fallback pattern, when a remote service call fails, rather than generating an
 exception, the service consumer executes an alternative code path and tries to carry
 out the action through another means. This usually involves looking for data from
 another data source or queueing the user’s request for future processing. The user’s
 call is not shown an exception indicating a problem, but they can be notified that
 their request will have to be tried later.
  For instance, let’s suppose you have an e-commerce site that monitors your user’s
 behavior and gives them recommendations for other items they might want to buy.
 Typically, you’d call a microservice to run an analysis of the user’s past behavior and
 return a list of recommendations tailored to that specific user. However, if the preference service fails, your fallback might be to retrieve a more general list of preferences
 that are based on all user purchases, which is much more generalized. And, this data
 might come from a completely different service and data source.
 
## Bulkheads

 The bulkhead pattern is based on a concept from building ships. A ship is divided into
 compartments called bulkheads, which are entirely segregated and watertight. Even if
 the ship’s hull is punctured, one bulkhead keeps the water confined to the area of the
 ship where the puncture occurred and prevents the entire ship from filling with water
 and sinking

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro19.png)
![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro20.png)

## Implementing the bulkhead pattern

In a microservice-based application, we’ll often need to call multiple microservices to
complete a particular task. Without using a bulkhead pattern, the default behavior for
these calls is that these are executed using the same threads that are reserved for handling requests for the entire Java container. In high volumes, performance problems
with one service out of many can result in all of the threads for the Java container
being maxed out and waiting to process work, while new requests for work back up.
The Java container will eventually crash.
 The bulkhead pattern segregates remote resource calls in their own thread pools
so that a single misbehaving service can be contained and not crash the container.
Resilience4j provides two different implementations of the bulkhead pattern. You can
use these implementations to limit the number of concurrent executions:
* Semaphore bulkhead—Uses a semaphore isolation approach, limiting the number
of concurrent requests to the service. Once the limit is reached, it starts rejecting requests.
* Thread pool bulkhead—Uses a bounded queue and a fixed thread pool. This
approach only rejects a request when the pool and the queue are full.
Resilience4j, by default, uses the semaphore bulkhead type. Figure 7.9 illustrates this
type.
 This model works fine if we have a small number of remote resources being
accessed within an application, and the call volumes for the individual services are
(relatively) evenly distributed. The problem is that if we have services with far higher
volumes or longer completion times than other services, we can end up introducing
thread exhaustion into our thread pools because one service ends up dominating all
of the threads in the default thread pool.
![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro21.png)
![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro22.png)

# Service routing

In a distributed architecture like a microservice, there will come a point where we’ll
need to ensure that critical behaviors such as security, logging, and tracking users
across multiple service calls occur. To implement this functionality, we’ll want these
attributes to be consistently enforced across all of our services without the need for
each individual development team to build their own solution. While it’s possible
to use a common library or framework to assist with building these capabilities
directly in an individual service, doing so has these implications:
* It’s challenging to implement these capabilities in each service consistently. Developers are focused on delivering functionality, and in the whirlwind of day-to-day
activity, they can easily forget to implement service logging or tracking unless
they work in a regulated industry where it’s required.
* Pushing the responsibilities to implement cross-cutting concerns like security and logging
down to the individual development teams greatly increases the odds that someone will not
implement them properly or will forget to do them. Cross-cutting concerns refer to
parts or features of the program’s design that are applicable throughout the
application and may affect other parts of the application.
* It’s possible to create a hard dependency across all our services. The more capabilities
we build into a common framework shared across all our services, the more difficult it is to change or add behavior in our common code without having to
recompile and redeploy all our services. Suddenly an upgrade of core capabilities built into a shared library becomes a long migration process.
To solve this problem, we need to abstract these cross-cutting concerns into a service
that can sit independently and act as a filter and router for all the microservice calls in
our architecture. We call this service a gateway. Our service clients no longer directly
call a microservice. Instead, all calls are routed through the service gateway, which acts
as a single Policy Enforcement Point (PEP), and are then routed to a final destination.
  We’ll see how to use Spring Cloud Gateway to implement a service
gateway. Specifically, we’ll look at how to use Spring Cloud Gateway to
* Put all service calls behind a single URL and map those calls using service discovery to their actual service instances
* Inject correlation IDs into every service call flowing through the service gateway
* Inject the correlation ID returned from the HTTP response and send it back to
the client

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro23.png)

The service gateway sits as the gatekeeper for all inbound traffic to microservice calls
within our application. With a service gateway in place, our service clients never
directly call the URL of an individual service, but instead place all calls to the service
gateway.
 Because a service gateway sits between all calls from the client to the individual services, it also acts as a central PEP for service calls. The use of a centralized PEP means
that cross-cutting service concerns can be carried out in a single place without the
individual development teams having to implement those concerns. Examples of
cross-cutting concerns that can be implemented in a service gateway include these:
* Static routing—A service gateway places all service calls behind a single URL and
API route. This simplifies development as we only have to know about one service endpoint for all of our services.
* Dynamic routing—A service gateway can inspect incoming service requests and,
based on the data from the incoming request, perform intelligent routing for
the service caller. For instance, customers participating in a beta program might
have all calls to a service routed to a specific cluster of services that are running
a different version of code from what everyone else is using.
* Authentication and authorization—Because all service calls route through a service gateway, the service gateway is a natural place to check whether the callers
of a service have authenticated themselves.
* Metric collection and logging—A service gateway can be used to collect metrics
and log information as a service call passes through it. You can also use the service gateway to confirm that critical pieces of information are in place for user
requests, thereby ensuring that logging is uniform. This doesn’t mean that you
shouldn’t collect metrics from within your individual services

Isn’t a service gateway a single point of failure and a potential
bottleneck?
When we introduced Eureka, we talked about how centralized
load balancers can be a single point of failure and a bottleneck for your services. A
service gateway, if not implemented correctly, can carry the same risk. Keep the following in mind as you build your service gateway implementation:
* Load balancers are useful when placed in front of individual groups of services.
In this case, a load balancer sitting in front of multiple service gateway
instances is an appropriate design and ensures that your service gateway
implementation can scale as needed. But having a load balancer sitting in front
of all your service instances isn’t a good idea because it becomes a bottleneck.
* Keep any code you write for your service gateway stateless. Don’t store any
information in memory for the service gateway. If you aren’t careful, you can
limit the scalability of the gateway. Then, you will need to ensure that the data
gets replicated across all service gateway instances.
* Keep the code you write for your service gateway light. The service gateway is
the “chokepoint” for your service invocation. Complex code with multiple
database calls can be the source of difficult-to-track performance problems in
the service gateway

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro24.png)

## Custom filters

The ability to proxy all requests through the gateway lets us simplify our service invocations. But the real power of Spring Cloud Gateway comes into play when we want to
write custom logic that can be applied against all the service calls flowing through the
gateway. Most often, this custom logic is used to enforce a consistent set of application
policies like security, logging, and tracking among all the services.
 The Spring Cloud Gateway allows us to build custom logic using a filter within the
gateway. Remember, a filter allows us to implement a chain of business logic that each
service request passes through as it’s implemented. Spring Cloud Gateway supports
the following two types of filters.This shows how the pre- and post-filters fit
together when processing a service client’s request.
* Pre-filters—A pre-filter is invoked before the actual request is sent to the target
destination. A pre-filter usually carries out the task of making sure that the service has a consistent message format (key HTTP headers are in place, for example) or acts as a gatekeeper to ensure that the user calling the service is
authenticated (they are whom they say they are).
* Post-filters—A post-filter is invoked after the target service, and a response is sent
back to the client. Usually, we implement a post-filter to log the response back
from the target service, handle errors, or audit the response for sensitive
information.

## Securing your microservices

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro25.png)

[Decode JWT access token](https://jwt.io/introduction)

## Propagating the access token

To demonstrate propagating a token between services, we’ll protect our licensing service with Keycloak as well. Remember, the licensing service calls the organization service
to look up information. The question becomes, how do we propagate the token from
one service to another?
 We’re going to set up a simple example where we’ll have the licensing service call
the organization service. If you followed the examples we built in the previous chapters, you’d see that both services are running behind a gateway. Figure 9.26 shows how
an authenticated user’s token will flow through the gateway, the licensing service, and
then down to the organization service.

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro26.png)

##  Some closing thoughts on microservice security

While this chapter has introduced you to OpenID, OAuth2, and the Keycloak specification and how you can use Spring Cloud security with Keycloak to implement an
authentication and authorization service, Keycloak is only one piece of the microservice security puzzle. As you shape your microservices for production use, you should
also build your microservice security around the following practices:
* Use HTTPS/Secure Sockets Layer (SSL) for all service communications.
* Use an API gateway for all service calls.
* Provide zones for your services (for example, a public API and private API).
* Limit the attack surface of your microservices by locking down unneeded network ports.
Figure 9.28 shows how these different pieces fit together.

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro27.png)

## Event-driven architecture

##  The case for messaging, EDA(event-driven architecture), and microservices
Why is messaging important in building microservice-based applications? To answer
that question, let’s start with an example. For this, we’ll use the two services that we’ve
used throughout the book: our licensing and organization services.
 Let’s imagine that after these services are deployed to production, we find that the
licensing service calls are taking an exceedingly long time when looking up information from the organization service. When we look at the usage patterns of the organization data, we find that the organization data rarely changes and that most of the
data reads from the organization service are done by the primary key of the organization record. If we could cache the reads for the organization data without having to
incur the cost of accessing a database, we could significantly improve the response
time of the licensing service calls. To implement a caching solution, we need to consider the following three core requirements:
1 Cached data needs to be consistent across all instances of the licensing service. This
means that we can’t cache the data locally within the licensing service because
we want to guarantee that the same organization data is read regardless of the
service instance hitting it.
2 We cannot cache the organization data within the memory of the container hosting the
licensing service. The run-time container hosting our service is often restricted in
size and can obtain data using different access patterns. A local cache can introduce complexity because we have to guarantee our local cache is in sync with all
of the other services in the cluster.
3 When an organization record changes via an update or delete, we want the licensing service to recognize that there has been a state change in the organization service. The
licensing service should then invalidate any cached data it has for that specific
organization and evict it from the cache.

### Using a synchronous request-response approach to communicate state change

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro28.png)

### Downsides of a messaging architecture

Like any architectural model, a message-based architecture has trade-offs. A messagebased architecture can be complicated and requires the development team to pay
close attention to several key things, including message-handling semantics, message
visibility, and message choreography. Let’s look at these in more detail.

## Message handling semantics

Using messages in a microservice-based application requires more than understanding how to publish and consume messages. It requires that we understand how our
application will behave based on the order in which messages are consumed and what
happens if a message is processed out of order. For example, if we have strict requirements that all orders from a single customer must be processed in the order they are
received, we’ll need to set up and structure our message handling differently than if
every message can be consumed independently of one another.
 It also means that if we’re using messaging to enforce strict state transitions of our
data, we need to think about designing our applications to take into consideration
scenarios where a message throws an exception or an error is processed out of order.
If a message fails, do we retry processing the error or do we let it fail? How do we handle future messages related to that customer if one of the customer’s messages fails?
These are important questions to think through.

## Message visibility

Using messages in our microservices often means a mix of synchronous service calls
and asynchronous service processing. The asynchronous nature of messages means
they might not be received or processed in close proximity to when the message is
published or consumed. Also, having things like correlation IDs for tracking a user’s
transactions across web service invocations and messages is critical to understanding
and debugging what’s going on in our application. A correlation ID is a unique number that’s generated at the start of a user’s transaction and passed along with every service call. It should also be passed along with
every message that’s published and consumed.

## Distributed tracing with Spring Cloud Sleuth and Zipkin

The microservices architecture is a powerful design paradigm for breaking down
complex monolithic software systems into smaller, more manageable pieces. These
pieces can be built and deployed independently of each other; however, this flexibility comes at a price—complexity. 
Because microservices are distributed by nature, trying to debug where a problem
occurs can be maddening. The distributed nature of the services means that we need
to trace one or more transactions across multiple services, physical machines, and different data stores, and then try to piece together what exactly is going on. This chapter lays out several techniques and technologies for using distributed debugging. In
this chapter, we look at the following:
* Using correlation IDs to link together transactions across multiple services
* Aggregating log data from various services into a single searchable source
* Visualizing the flow of a user transaction across multiple services to understand
each part of the transaction’s performance characteristics
* Analyzing, searching, and visualizing log data in real time using the ELK stack
To accomplish this, we will use the following technologies:
* Spring Cloud Sleuth (https://cloud.spring.io/spring-cloud-sleuth/reference/
html/)—The Spring Cloud Sleuth project instruments our incoming HTTP
requests with trace IDs (aka correlation IDs). It does this by adding filters and
interacting with other Spring components to let the generated correlation IDs
pass through to all the system calls.
* Zipkin (https://zipkin.io/)—Zipkin is an open source data-visualization tool
that shows the flow of a transaction across multiple services. Zipkin allows us to
break a transaction down into its component pieces and visually identify where
there might be performance hotspots.
* ELK stack (https://www.elastic.co/what-is/elk-stack)—The ELK stack combines
three open source tools—Elasticsearch, Logstash, and Kibana—that allow us to
analyze, search, and visualize logs in real time.
– Elasticsearch is a distributed analytics engine for all types of data (structured
and non-structured, numeric, text-based, and so on).
– Logstash is a server-side data processing pipeline that allows us to add and
ingest data from multiple sources simultaneously and transform it before it is
indexed in Elasticsearch.
– Kibana is the visualization and data management tool for Elasticsearch. It
provides charts, maps, and real-time histograms. 

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro33.png)

## Deploying your microservices

### The architecture of a build/deployment pipeline

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro34.png)
Figure 12.1 should look somewhat familiar because it’s based on the general build/
deployment pattern used for implementing continuous integration (CI):
1 A developer commits their code to the source code repository.
2 A build tool monitors the source control repository for changes and kicks off a
build when a change is detected.
3 During the build, the application’s unit and integration tests are run, and if
everything passes, a deployable software artifact is created (a JAR, WAR, or
EAR).
4 This JAR, WAR, or EAR might then be deployed to an application server running on another server (usually a development server).

A similar process is followed by the build/deployment pipeline until the code is ready to
be deployed. We’re going to tack continuous delivery (CD) onto the build/deployment
process shown in figure 12.1 with the following steps:
1 A developer commits their service code to a source repository.
2 A build/deploy engine monitors the source code repository for changes. If
code is committed, the build/deploy engine checks out the code and runs the
build scripts.
3 After the build scripts compile the code and run its unit and integration tests,
the service is then compiled to an executable artifact. Because our microservices were built using Spring Boot, our build process creates an executable JAR
file that contains both the service code and a self-contained Tomcat server.
Note that the next step is where our build/deploy pipeline begins to deviate
from a traditional Java CI build process.
4 After the executable JAR is built, we “bake” a machine image with our microservice deployed to it. This baking process creates a virtual machine image or container (Docker) and installs our service onto it.
When the virtual machine image starts, our service also starts and is ready to
begin taking requests. Unlike a traditional CI build process, where you might
deploy the compiled JAR or WAR to an application server that’s independently
(and often with a separate team) managed from the application, with the
CI/CD process, we deploy the microservice, the run-time engine for the service,
and the machine image all as one codependent unit managed by the development team that wrote the software.
5 Before we officially deploy to a new environment, the machine image starts,
and a series of platform tests are run against the image for the environment to
determine if everything is proceeding correctly. If the platform tests pass, the
machine image is promoted to the new environment and made available for
use.
6 The promotion of the service to the new environment involves starting up the
exact machine image that was used in the lower environment. This is the secret
sauce of the whole process. The entire machine image is deployed.

The build/deploy process is built on four core patterns. These patterns have emerged
from the collective experience of development teams building microservice and
cloud-based applications. These patterns include
* Continuous integration/continuous delivery (CI/CD)—With CI/CD, your application code isn’t only built and tested when it is committed and deployed. The
deployment of your code should go something like this: if the code passes its
unit, integration, and platform tests, it’s immediately promoted to the next
environment. The only stopping point in most organizations is the push to
production.
* Infrastructure as code—The final software artifact that’s pushed to development
and beyond is a machine image. The machine image with your microservice
installed in it is provisioned immediately after your microservice’s source code
is compiled and tested. The provisioning of the machine image occurs through
a series of scripts that run with each build. No human hands should ever touch
the server after it’s built. The provisioning scripts should be kept under source
control and managed like any other piece of code.
* Immutable server—Once a server image is built, the server’s configuration and
microservice are never touched after the provisioning process. This guarantees
that your environment won’t suffer from “configuration drift,” where a developer or system administrator made “one small change” that later caused an outage. If a change needs to be made, change the provisioning scripts for the
server and kick off a new build.

## The DevOps story: Building for the rigors of runtime

While DevOps is a rich and emerging IT field, for the DevOps engineer, the design of
the microservice is all about managing the service after it goes into production. Writing the code is often the easy part. Keeping it running is the hard part. We’ll start our
microservice development effort with four principles and build on these later in the
book:
* A microservice should be self-contained. It should also be independently deployable
with multiple instances of the service being started up and torn down with a single software artifact.
* A microservice should be configurable. When a service instance starts up, it should
read the data it needs to configure itself from a central location or have its configuration information passed on as environment variables. No human intervention should be required to configure the service.
* A microservice instance needs to be transparent to the client. The client should never
know the exact location of a service. Instead, a microservice client should talk
to a service discovery agent. That allows the application to locate an instance of
a microservice without having to know its physical location.
* A microservice should communicate its health. This is a critical part of your cloud
architecture. Microservice instances will fail, and discovery agents need to route
around bad service instances. In this book, we’ll use Spring Boot Actuator to
display the health of each microservice.
These four principles expose the paradox that can exist with microservice development. Microservices are smaller in size and scope, but their use introduces more moving parts in an application because microservices are distributed and run
independently of each other in their own containers. This introduces a high degree of
coordination and more opportunities for failure points in the application.
 From a DevOps perspective, you must address the operational needs of a microservice up front and translate these four principles into a standard set of lifecycle events
that occur every time a microservice is built and deployed to an environment. The
four principles can be mapped to the following operational lifecycles. Figure 3.9
shows how these four steps fit together.
* Service assembly—How you package and deploy your service to guarantee repeatability and consistency so that the same service code and run time are deployed
exactly the same way.
* Service bootstrapping—How you separate your application and environmentspecific configuration code from the run-time code so that you can start and
deploy a microservice instance quickly in any environment without human
intervention.
* Service registration/discovery—When a new microservice instance is deployed,
how you make the new service instance discoverable by other application
clients.
* Service monitoring—In a microservice environment, it’s common for multiple
instances of the same service to be running due to high availability needs. From
a DevOps perspective, you need to monitor microservice instances and ensure
that any faults are routed around failing service instances, and that these are
taken down. 

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro10.png)

## Service assembly: Packaging and deploying your microservices

From a DevOps perspective, one of the key concepts behind a microservice architecture is that multiple instances of a microservice can be deployed quickly in response
to a changed application environment (for example, a sudden influx of user requests,
problems within the infrastructure, and so on). To accomplish this, a microservice
needs to be packaged and installable as a single artifact with all of its dependencies
defined within it. These dependencies must also include the run-time engine (for
example, an HTTP server or application container) that hosts the microservice.
 The process of consistently building, packaging, and deploying is the service
assembly (step 1 in figure 3.9). Figure 3.10 shows additional details about this step.
![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro11.png)

## Service bootstrapping: Managing configuration of your microservices

Service bootstrapping (step 2 in figure 3.9) occurs when the microservice first starts
and needs to load its application configuration information. Figure 3.11 provides
more context for the bootstrapping process.

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro12.png)

As any application developer knows, there will be times when you need to make the
run-time behavior of the application configurable. Usually this involves reading your
application configuration data from a property file deployed with the application or
reading the data out of a data store like a relational database.
 Microservices often run into the same type of configuration requirements. The difference is that in a microservice application running in the cloud, you might have
hundreds or even thousands of microservice instances running. Further complicating
this is that the services might be spread across the globe. With a high number of geographically dispersed services, it becomes unfeasible to redeploy your services to pick
up new configuration data. Storing the data in a data store external to the service
solves this problem. But microservices in the cloud offer a set of unique challenges:
* Configuration data tends to be simple in structure and is usually read frequently and written infrequently. Relational databases are overkill in this situation because they’re designed to manage much more complicated data models
than a simple set of key-value pairs.
* Because the data is accessed on a regular basis but changes infrequently, the
data must be readable with a low level of latency.
* The data store has to be highly available and close to the services reading the
data. A configuration data store can’t go down completely because it would
become a single point of failure for your application.

## Service registration and discovery: How clients communicate with your microservices

From a microservice consumer perspective, a microservice should be location-transparent
because in a cloud-based environment, servers are ephemeral. Ephemeral means that the
servers that a service is hosted on usually have shorter lives than a service running in a corporate data center. Cloud-based services can be started and torn down quickly with an
entirely new IP address assigned to the server on which the services are running.
 By insisting that services are treated as short-lived disposable objects, microservice
architectures can achieve a high degree of scalability and availability by having multiple instances of a service running. Service demand and resiliency can be managed as
quickly as the situation warrants. Each service has a unique and impermanent IP
address assigned to it. The downside to ephemeral services is that with services constantly coming up and down, managing a large pool of these services manually or by
hand is an invitation to an outage.
 A microservice instance needs to register itself with a third-party agent. This registration process is called service discovery (see step 3 in figure 3.9, then see figure 3.12
for details on this process). When a microservice instance registers with a service discovery agent, it tells the discovery agent two things: the physical IP address (or domain
address of the service instance) and a logical name that an application can use to look
up the service. Certain service discovery agents also require a URL sent back to the
registering service, which can be used by the service discovery agent to perform health
checks. The service client then communicates with the discovery agent to look up the
service’s location.

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro13.png)

## Communicating a microservice’s health

A service discovery agent doesn’t act only as a traffic cop that guides the client to the
location of the service. In a cloud-based microservice application, you’ll often have
multiple instances of a running service. Sooner or later, one of those service instances
will fail. The service discovery agent monitors the health of each service instance registered with it and removes any failing service instances from its routing tables to ensure
that clients aren’t sent a service instance that has failed.
 After a microservice comes up, the service discovery agent will continue to monitor
and ping the health check interface to ensure that that service is available. This is step
4 in figure 3.9; figure 3.13 provides context for this step. 

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro14.png)