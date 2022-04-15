---
layout: default
title: Microservices patterns
parent: Microservices
nav_order: 2
permalink: /microservices/paterns
---
<div align="center" markdown="1">
Microservices patterns/ Java resources / Grokking the interview

{: .fs-6 .fw-300 }
</div>

## Service discovery

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

-[Pattern: Self registration A service instance registers itself with the service registry.](http://microservices.io/patterns/self-registration.html.)
-[Pattern: Client-side discoveryA service client retrieves the list of available service instances from the service registry and load balances across them.](http://microservices.io/patterns/clientside-discovery.html.)

### The architecture of service discovery

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
![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro16.png)
![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro17.png)

#### Applying the platform-provided service discovery patterns 

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

## When bad things happen: Resiliency patterns

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

#### Client-side load balancing
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
#### Circuit breaker
 The circuit breaker pattern is modeled after an electrical circuit breaker. In an electrical system, a circuit breaker detects if there’s too much current flowing through the
 wire. If the circuit breaker detects a problem, it breaks the connection with the rest of
 the electrical system and keeps the system from frying the downstream components.
  With a software circuit breaker, when a remote service is called, the circuit breaker
 monitors the call. If the calls take too long, the circuit breaker intercedes and kills the
 call. The circuit breaker pattern also monitors all calls to a remote resource, and if
 enough calls fail, the circuit breaker implementation will “pop,” failing fast and preventing future calls to the failing remote resource.
#### Fallback processing
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
#### Bulkheads
 The bulkhead pattern is based on a concept from building ships. A ship is divided into
 compartments called bulkheads, which are entirely segregated and watertight. Even if
 the ship’s hull is punctured, one bulkhead keeps the water confined to the area of the
 ship where the puncture occurred and prevents the entire ship from filling with water
 and sinking

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro19.png)
![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro20.png)

### Implementing the bulkhead pattern
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

## Service routing

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

---- Wait—isn’t a service gateway a single point of failure and a potential
bottleneck?
Earlier in chapter 6, when we introduced Eureka, we talked about how centralized
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

#### Custom filters
The ability to proxy all requests through the gateway lets us simplify our service invocations. But the real power of Spring Cloud Gateway comes into play when we want to
write custom logic that can be applied against all the service calls flowing through the
gateway. Most often, this custom logic is used to enforce a consistent set of application
policies like security, logging, and tracking among all the services.
 The Spring Cloud Gateway allows us to build custom logic using a filter within the
gateway. Remember, a filter allows us to implement a chain of business logic that each
service request passes through as it’s implemented. Spring Cloud Gateway supports
the following two types of filters. Figure 8.10 shows how the pre- and post-filters fit
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

Decode JWT access token

### Propagating the access token
To demonstrate propagating a token between services, we’ll protect our licensing service with Keycloak as well. Remember, the licensing service calls the organization service
to look up information. The question becomes, how do we propagate the token from
one service to another?
 We’re going to set up a simple example where we’ll have the licensing service call
the organization service. If you followed the examples we built in the previous chapters, you’d see that both services are running behind a gateway. Figure 9.26 shows how
an authenticated user’s token will flow through the gateway, the licensing service, and
then down to the organization service.
![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro26.png)

###  Some closing thoughts on microservice security
While this chapter has introduced you to OpenID, OAuth2, and the Keycloak specification and how you can use Spring Cloud security with Keycloak to implement an
authentication and authorization service, Keycloak is only one piece of the microservice security puzzle. As you shape your microservices for production use, you should
also build your microservice security around the following practices:
* Use HTTPS/Secure Sockets Layer (SSL) for all service communications.
* Use an API gateway for all service calls.
* Provide zones for your services (for example, a public API and private API).
* Limit the attack surface of your microservices by locking down unneeded network ports.
Figure 9.28 shows how these different pieces fit together. Each of the bulleted items in
the list maps to the numbers in figure 9.28. We’ll examine each of the topic areas enumerated in the previous list and in the figure in more detail throughout the next sections.
![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro27.png)

## Event-driven architecture
###  The case for messaging, EDA(event-driven architecture), and microservices
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
MESSAGE-HANDLING SEMANTICS
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
MESSAGE VISIBILITY
Using messages in our microservices often means a mix of synchronous service calls
and asynchronous service processing. The asynchronous nature of messages means
they might not be received or processed in close proximity to when the message is
published or consumed. Also, having things like correlation IDs for tracking a user’s
transactions across web service invocations and messages is critical to understanding
and debugging what’s going on in our application. As you may remember from chapter 8, a correlation ID is a unique number that’s generated at the start of a user’s transaction and passed along with every service call. It should also be passed along with
every message that’s published and consumed.
MESSAGE CHOREOGRAPHY
As alluded to in the section on message visibility, a message-based application makes it
more difficult to reason through its business logic because its code is no longer processed in a linear fashion with a simple block request-response model. Instead, debugging message-based applications can involve wading through the logs of several
different services, where user transactions can be executed out of order and at different times.

### Introducing Spring Cloud Stream
![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro29.png)
![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro30.png)
![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro31.png)
![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro32.png)

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

---- On immutability and the rise of the Phoenix Server
With the concept of immutable servers, we should always be guaranteed that a
server’s configuration matches precisely with what the machine image for the server
says it does. A server should have the option to be killed and restarted from the
machine image without any changes in the service or microservice behavior. This killing and resurrection of a new server was termed “Phoenix Server” by Martin Fowler
because, when the old server is killed, the new server should rise from the ashes.
For more information, see the following link:
 http://martinfowler.com/bliki/PhoenixServer.html
The Phoenix Server pattern has two fundamental benefits. First, it exposes and drives
configuration drift from your environment. If you’re constantly tearing down and setting up new servers, you’re more likely to expose configuration drift early. This is a
tremendous help in ensuring consistency.
Second, the Phoenix Server pattern helps to improve resiliency by allowing you to find
situations where a server or service isn’t cleanly recoverable after it’s killed and
restarted. Remember, in a microservices architecture, your services should be stateless, and the death of a server should be a minor blip. Randomly killing and restarting
servers quickly exposes situations where you have a state in your services or infrastructure. It’s better to find these situations and dependencies early in your deployment pipeline than when you’re on the phone with an angry customer or company.


### Managing transactions with sagas

Using the Saga pattern to maintain data consistency
Sagas are mechanisms to maintain data consistency in a microservice architecture
without having to use distributed transactions. You define a saga for each system command that needs to update data in multiple services. A saga is a sequence of local
transactions. Each local transaction updates data within a single service using the
familiar ACID transaction frameworks and libraries mentioned earlier

Pattern: Saga
Maintain data consistency across services using a sequence of local transactions
that are coordinated using asynchronous messaging. See http://microservices.io/
patterns/data/saga.html.


Coordinating sagas
A saga’s implementation consists of logic that coordinates the steps of the saga.
When a saga is initiated by system command, the coordination logic must select and
tell the first saga participant to execute a local transaction. Once that transaction
completes, the saga’s sequencing coordination selects and invokes the next saga
participant. This process continues until the saga has executed all the steps. If any
local transaction fails, the saga must execute the compensating transactions in
reverse order. There are a couple of different ways to structure a saga’s coordination logic:
 Choreography—Distribute the decision making and sequencing among the saga
participants. They primarily communicate by exchanging events.
Orchestration—Centralize a saga’s coordination logic in a saga orchestrator class.
A saga orchestrator sends command messages to saga participants telling them
which operations to perform.

BENEFITS AND DRAWBACKS OF CHOREOGRAPHY-BASED SAGAS
Choreography-based sagas have several benefits:
 Simplicity—Services publish events when they create, update, or delete business
objects.
 Loose coupling —The participants subscribe to events and don’t have direct knowledge of each other.
And there are some drawbacks:
 More difficult to understand—Unlike with orchestration, there isn’t a single place
in the code that defines the saga. Instead, choreography distributes the implementation of the saga among the services. Consequently, it’s sometimes difficult
for a developer to understand how a given saga works.
 Cyclic dependencies between the services—The saga participants subscribe to each
other’s events, which often creates cyclic dependencies. For example, if you
carefully examine figure 4.4, you’ll see that there are cyclic dependencies, such
as Order Service  Accounting Service  Order Service. Although this isn’t
necessarily a problem, cyclic dependencies are considered a design smell.
 Risk of tight coupling—Each saga participant needs to subscribe to all events that
affect them. For example, Accounting Service must subscribe to all events that
cause the consumer’s credit card to be charged or refunded. As a result, there’s
a risk that it would need to be updated in lockstep with the order lifecycle
implemented by Order Service.
Choreography can work well for simple sagas, but because of these drawbacks it’s
often better for more complex sagas to use orchestration. Let’s look at how orchestration works

Orchestration-based sagas
Orchestration is another way to implement sagas. When using orchestration, you
define an orchestrator class whose sole responsibility is to tell the saga participants
what to do. The saga orchestrator communicates with the participants using command/
async reply-style interaction. To execute a saga step, it sends a command message to a
participant telling it what operation to perform. After the saga participant has performed the operation, it sends a reply message to the orchestrator. The orchestrator
then processes the message and determines which saga step to perform next.

BENEFITS AND DRAWBACKS OF ORCHESTRATION-BASED SAGAS
Orchestration-based sagas have several benefits:
 Simpler dependencies—One benefit of orchestration is that it doesn’t introduce
cyclic dependencies. The saga orchestrator invokes the saga participants, but
the participants don’t invoke the orchestrator. As a result, the orchestrator
depends on the participants but not vice versa, and so there are no cyclic
dependencies.
 Less coupling—Each service implements an API that is invoked by the orchestrator, so it does not need to know about the events published by the saga
participants.
 Improves separation of concerns and simplifies the business logic—The saga coordination logic is localized in the saga orchestrator. The domain objects are simpler
and have no knowledge of the sagas that they participate in. For example, when
using orchestration, the Order class has no knowledge of any of the sagas, so it
has a simpler state machine model. During the execution of the Create Order
Saga, it transitions directly from the APPROVAL_PENDING state to the APPROVED
state. The Order class doesn’t have any intermediate states corresponding to the
steps of the saga. As a result, the business is much simpler.
Orchestration also has a drawback: the risk of centralizing too much business logic in
the orchestrator. This results in a design where the smart orchestrator tells the dumb
services what operations to do. Fortunately, you can avoid this problem by designing
orchestrators that are solely responsible for sequencing and don’t contain any other
business logic.
 I recommend using orchestration for all but the simplest sagas. Implementing the
coordination logic for your sagas is just one of the design problems you need to solve.
Another, which is perhaps the biggest challenge that you’ll face when using sagas, is
handling the lack of isolation. Let’s take a look at that problem and how to solve it


The challenge with using sagas is that they lack the isolation property of ACID
transactions. That’s because the updates made by each of a saga’s local transactions
are immediately visible to other sagas once that transaction commits. This behavior
can cause two problems. First, other sagas can change the data accessed by the saga
while it’s executing. And other sagas can read its data before the saga has completed
its updates, and consequently can be exposed to inconsistent data. You can, in fact,
consider a saga to be ACD:
 Atomicity—The saga implementation ensures that all transactions are executed
or all changes are undone.
 Consistency—Referential integrity within a service is handled by local databases.
Referential integrity across services is handled by the services.
 Durability—Handled by local databases.

THE STRUCTURE OF A SAGA
The countermeasures paper mentioned in the last section defines a useful model for
the structure of a saga. In this model, shown in figure 4.8, a saga consists of three types
of transactions:
 Compensatable transactions—Transactions that can potentially be rolled back using
a compensating transaction.
 Pivot transaction—The go/no-go point in a saga. If the pivot transaction commits, the saga will run until completion. A pivot transaction can be a transaction
that’s neither compensatable nor retriable. Alternatively, it can be the last compensatable transaction or the first retriable transaction
- Retriable transactions—Transactions that follow the pivot transaction and are guaranteed to succeed.

### Designing business logic in a microservice architecture

The Aggregate pattern structures a service’s business logic as a collection of
aggregates. An aggregate is a cluster of objects that can be treated as a unit. There are
two reasons why aggregates are useful when developing business logic in a microservice architecture:
 Aggregates avoid any possibility of object references spanning service boundaries, because an inter-aggregate reference is a primary key value rather than an
object reference.
 Because a transaction can only create or update a single aggregate, aggregates
fit the constraints of the microservices transaction model.
As a result, an ACID transaction is guaranteed to be within a single service

About Domain-driven design
DDD, which is described in the book Domain-Driven Design by Eric Evans (AddisonWesley Professional, 2003), is a refinement of OOD and is an approach for developing
complex business logic. I introduced DDD in chapter 2 when discussing the usefulness of DDD subdomains when decomposing an application into services. When using
DDD, each service has its own domain model, which avoids the problems of a single,
application-wide domain model. Subdomains and the associated concept of Bounded
Context are two of the strategic DDD patterns.
 DDD also has some tactical patterns that are building blocks for domain models.
Each pattern is a role that a class plays in a domain model and defines the characteristics of the class. The building blocks that have been widely adopted by developers
include the following:
 Entity—An object that has a persistent identity. Two entities whose attributes
have the same values are still different objects. In a Java EE application, classes
that are persisted using JPA @Entity are usually DDD entities.
 Value object—An object that is a collection of values. Two value objects whose
attributes have the same values can be used interchangeably. An example of a
value object is a Money class, which consists of a currency and an amount.
 Factory—An object or method that implements object creation logic that’s too
complex to be done directly by a constructor. It can also hide the concrete
classes that are instantiated. A factory might be implemented as a static method
of a class.
 Repository—An object that provides access to persistent entities and encapsulates the mechanism for accessing the database.
 Service—An object that implements business logic that doesn’t belong in an
entity or a value object

These building blocks are used by many developers. Some are supported by frameworks such as JPA and the Spring framework. There is one more building block that
has been generally ignored (myself included!) except by DDD purists: aggregates. As
it turns out, aggregates are an extremely useful concept when developing microservices. Let’s first look at some subtle problems with classic OOD that are solved by
using aggregates. 


Aggregates have explicit boundaries
An aggregate is a cluster of domain objects within a boundary that can be treated as a
unit. It consists of a root entity and possibly one or more other entities and value
objects. Many business objects are modeled as aggregates. For example, in chapter 2
we created a rough domain model by analyzing the nouns used in the requirements
and by domain experts. Many of these nouns, such as Order, Consumer, and Restaurant, are aggregates

Pattern: Aggregate
Organize a domain model as a collection of aggregates, each of which is a graph of
objects that can be treated as a unit.

Aggregate rules
RULE #1: REFERENCE ONLY THE AGGREGATE ROOT
RULE #2: INTER-AGGREGATE REFERENCES MUST USE PRIMARY KEYS
RULE #3: ONE TRANSACTION CREATES OR UPDATES ONE AGGREGATE

### Developing business logic with event sourcing

Developing business logic using event sourcing
Event sourcing is a different way of structuring the business logic and persisting aggregates. It persists an aggregate as a sequence of events. Each event represents a state
change of the aggregate. An application recreates the current state of an aggregate by
replaying the events

Pattern: Event sourcing
Persist an aggregate as a sequence of domain events that represent state changes.
See http://microservices.io/patterns/data/event-sourcing.html.

Event sourcing has several important benefits. For example, it preserves the history of
aggregates, which is valuable for auditing and regulatory purposes. And it reliably
publishes domain events, which is particularly useful in a microservice architecture.
Event sourcing also has drawbacks. It involves a learning curve, because it’s a different
way to write your business logic

Idempotent message processing
Services often consume messages from other applications or other services. A service
might, for example, consume domain events published by aggregates or command
messages sent by a saga orchestrator. As described in chapter 3, an important issue
when developing a message consumer is ensuring that it’s idempotent, because a message broker might deliver the same message multiple times.
 A message consumer is idempotent if it can safely be invoked with the same message multiple times. The Eventuate Tram framework, for example, implements idempotent message handling by detecting and discarding duplicate messages. It records
the ids of processed messages in a PROCESSED_MESSAGES table as part of the local
ACID transaction used by the business logic to create or update aggregates. If the ID
of a message is in the PROCESSED_MESSAGES table, it’s a duplicate and can be discarded. Event sourcing-based business logic must implement an equivalent mechanism. How this is done depends on whether the event store uses an RDBMS or a
NoSQL database.
IDEMPOTENT MESSAGE PROCESSING WITH AN RDBMS-BASED EVENT STORE
If an application uses an RDBMS-based event store, it can use an identical approach to
detect and discard duplicates messages. It inserts the message ID into the PROCESSED
_MESSAGES table as part of the transaction that inserts events into the EVENTS table.
IDEMPOTENT MESSAGE PROCESSING WHEN USING A NOSQL-BASED EVENT STORE
A NoSQL-based event store, which has a limited transaction model, must use a different
mechanism to implement idempotent message handling. A message consumer must
somehow atomically persist events and record the message ID. Fortunately, there’s a
simple solution. A message consumer stores the message’s ID in the events that are
generated while processing it. It detects duplicates by verifying that none of an aggregate’s events contains the message ID.
 One challenge with using this approach is that processing a message might not
generate any events. The lack of events means there’s no record of a message having
been processed. A subsequent redelivery and reprocessing of the same message might
result in incorrect behavior. For example, consider the following scenario:
1 Message A is processed but doesn’t update an aggregate.
2 Message B is processed, and the message consumer updates the aggregate.
3 Message A is redelivered, and because there’s no record of it having been processed, the message consumer updates the aggregate.
4 Message B is processed again….
In this scenario, the redelivery of events results in a different and possibly erroneous
outcome.
 One way to avoid this problem is to always publish an event. If an aggregate doesn’t
emit an event, an application saves a pseudo event solely to record the message ID.
Event consumers must ignore these pseudo events.

Benefits of event sourcing
Event sourcing has both benefits and drawbacks. The benefits include the following:
 Reliably publishes domain events
 Preserves the history of aggregates
 Mostly avoids the O/R impedance mismatch problem
 Provides developers with a time machine
Let’s examine each benefit in more detail.
RELIABLY PUBLISHES DOMAIN EVENTS
A major benefit of event sourcing is that it reliably publishes events whenever the state
of an aggregate changes. That’s a good foundation for an event-driven microservice
architecture. Also, because each event can store the identity of the user who made the
change, event sourcing provides an audit log that’s guaranteed to be accurate. The
stream of events can be used for a variety of other purposes, including notifying users,
application integration, analytics, and monitoring.
PRESERVES THE HISTORY OF AGGREGATES
Another benefit of event sourcing is that it stores the entire history of each aggregate.
You can easily implement temporal queries that retrieve the past state of an aggregate.
To determine the state of an aggregate at a given point in time, you fold the events
that occurred up until that point. It’s straightforward, for example, to calculate the
available credit of a customer at some point in the past.
MOSTLY AVOIDS THE O/R IMPEDANCE MISMATCH PROBLEM
Event sourcing persists events rather than aggregating them. Events typically have a
simple, easily serializable structure. As mentioned earlier, a service can snapshot a
complex aggregate by serializing a memento of its state, which adds a level of indirection between an aggregate and its serialized representation.
PROVIDES DEVELOPERS WITH A TIME MACHINE
Event sourcing stores a history of everything that’s happened in the lifetime of an
application. Imagine that the FTGO developers need to implement a new requirement to customers who added an item to their shopping cart and then removed it. A
traditional application wouldn’t preserve this information, so could only market to
customers who add and remove items after the feature is implemented. In contrast, an
event sourcing-based application can immediately market to customers who have done
this in the past. It’s as if event sourcing provides developers with a time machine for
traveling to the past and implementing unanticipated requirements.

Using sagas and event sourcing together
Imagine you’ve implemented one or more services using event sourcing. You’ve probably written services similar to the one shown in listing 6.4. But if you’ve read chapter 4,
you know that services often need to initiate and participate in sagas, sequences of
local transactions used to maintain data consistency across services. For example,
Order Service uses a saga to validate an Order. Kitchen Service, Consumer Service,
and Accounting Service participate in that saga. Consequently, you must integrate
sagas and event sourcing-based business logic.
 Event sourcing makes it easy to use choreography-based sagas. The participants
exchange the domain events emitted by their aggregates. Each participant’s aggregates handle events by processing commands and emitting new events. You need to
write the aggregates and the event handler classes, which update the aggregates.
 But integrating event sourcing-based business logic with orchestration-based sagas
can be more challenging. That’s because the event store’s concept of a transaction
might be quite limited. When using some event stores, an application can only create
or update a single aggregate and publish the resulting event(s). But each step of a
saga consists of several actions that must be performed atomically:
 Saga creation—A service that initiates a saga must atomically create or update an
aggregate and create the saga orchestrator. For example, Order Service’s
createOrder() method must create an Order aggregate and a CreateOrderSaga.
 Saga orchestration—A saga orchestrator must atomically consume replies, update
its state, and send command messages.
 Saga participants—Saga participants, such as Kitchen Service and Order Service,
must atomically consume messages, detect and discard duplicates, create or
update aggregates, and send reply messages.
Because of this mismatch between these requirements and the transactional capabilities of an event store, integrating orchestration-based sagas and event sourcing potentially creates some interesting challenges.
 A key factor in determining the ease of integrating event sourcing and orchestrationbased sagas is whether the event store uses an RDBMS or a NoSQL database. The
Eventuate Tram saga framework described in chapter 4 and the underlying Tram messaging framework described in chapter 3 rely on flexible ACID transactions provided
by the RDBMS. The saga orchestrator and the saga participants use ACID transactions
to atomically update their databases and exchange messages. If the application uses
an RDBMS-based event store, such as Eventuate Local, then it can cheat and invoke the
Eventuate Tram saga framework and update the event store within an ACID transaction. But if the event store uses a NoSQL database, which can’t participate in the same
transaction as the Eventuate Tram saga framework, it will have to take a different
approach.
 Let’s take a closer look at some of the different scenarios and issues you’ll need to
address:
 Implementing choreography-based sagas
 Creating an orchestration-based saga
 Implementing an event sourcing-based saga participant
 Implementing saga orchestrators using event sourcing
We’ll begin by looking at how to implement choreography-based sagas using event
sourcing.

Summary
 Event sourcing persists an aggregate as a sequence of events. Each event represents either the creation of the aggregate or a state change. An application
recreates the state of an aggregate by replaying events. Event sourcing preserves
the history of a domain object, provides an accurate audit log, and reliably publishes domain events.
 Snapshots improve performance by reducing the number of events that must
be replayed.
 Events are stored in an event store, a hybrid of a database and a message broker.
When a service saves an event in an event store, it delivers the event to subscribers.
 Eventuate Local is an open source event store based on MySQL and Apache
Kafka. Developers use the Eventuate client framework to write aggregates and
event handlers.
 One challenge with using event sourcing is handling the evolution of events. An
application potentially must handle multiple event versions when replaying
events. A good solution is to use upcasting, which upgrades events to the latest
version when they’re loaded from the event store.
 Deleting data in an event sourcing application is tricky. An application must use
techniques such as encryption and pseudonymization in order to comply with
regulations like the European Union’s GDPR that requires an application to
erase an individual’s data.
Event sourcing is a simple way to implement choreography-based sagas. Services have event handlers that listen to the events published by event sourcingbased aggregates.
 Event sourcing is a good way to implement saga orchestrators. As a result, you
can write applications that exclusively use an event store.


### Implementing queries in a microservice architecture

There are two different patterns for implementing query operations in a microservice architecture:
 The API composition pattern—This is the simplest approach and should be used
whenever possible. It works by making clients of the services that own the data
responsible for invoking the services and combining the results.
 The Command query responsibility segregation (CQRS) pattern—This is more powerful than the API composition pattern, but it’s also more complex. It maintains
one or more view databases whose sole purpose is to support queries.

Pattern: API composition
Implement a query that retrieves data from several services by querying each service
via its API and combining the results. See http://microservices.io/patterns/data/apicomposition.html.

API composition design issues
When using this pattern, you have to address a couple of design issues:
 Deciding which component in your architecture is the query operation’s API
composer
 How to write efficient aggregation logic

## Using the CQRS pattern
   Many enterprise applications use an RDBMS as the transactional system of record and
   a text search database, such as Elasticsearch or Solr, for text search queries. Some
   applications keep the databases synchronized by writing to both simultaneously. Others periodically copy data from the RDBMS to the text search engine. Applications
   with this architecture leverage the strengths of multiple databases: the transactional
   properties of the RDBMS and the querying capabilities of the text database.
   Pattern: Command query responsibility segregation
   Implement a query that needs data from several services by using events to maintain
   a read-only view that replicates data from the services. See http://microservices
   .io/patterns/data/cqrs.html.
   
CQRS is a generalization of this kind of architecture. It maintains one or more view
databases—not just text search databases—that implement one or more of the application’s queries. To understand why this is useful, we’ll look at some queries that can’t
be efficiently implemented using the API composition pattern. I’ll explain how CQRS
works and then talk about the benefits and drawbacks of CQRS. Let’s take a look at
when you need to use CQRS.

CQRS SEPARATES COMMANDS FROM QUERIES

### External API patterns

 One approach to API design is for clients to invoke the services directly. On the
surface, this sounds quite straightforward—after all, that’s how clients invoke the API
of a monolithic application. But this approach is rarely used in a microservice architecture because of the following drawbacks:
 The fine-grained service APIs require clients to make multiple requests to
retrieve the data they need, which is inefficient and can result in a poor user
experience.
 The lack of encapsulation caused by clients knowing about each service and its
API makes it difficult to change the architecture and the APIs.
 Services might use IPC mechanisms that aren’t convenient or practical for clients to use, especially those clients outside the firewall.

The API gateway pattern
As you’ve just seen, there are numerous drawbacks with services accessing services
directly. It’s often not practical for a client to perform API composition over the internet. The lack of encapsulation makes it difficult for developers to change service
decomposition and APIs. Services sometimes use communication protocols that
aren’t suitable outside the firewall. Consequently, a much better approach is to use an
API gateway.

Pattern: API gateway
Implement a service that’s the entry point into the microservices-based application
from external API clients. See http://microservices.io/patterns/apigateway.html.

An API gateway is a service that’s the entry point into the application from the outside
world. It’s responsible for request routing, API composition, and other functions,
such as authentication. This section covers the API gateway pattern. I discuss its benefits and drawbacks and describe various design issues you must address when developing an API gateway.

IMPLEMENTING EDGE FUNCTIONS
Although an API gateway’s primary responsibilities are API routing and composition,
it may also implement what are known as edge functions. An edge function is, as the
name suggests, a request-processing function implemented at the edge of an application. Examples of edge functions that an application might implement include the
following:
 Authentication—Verifying the identity of the client making the request.
 Authorization—Verifying that the client is authorized to perform that particular
operation.
 Rate limiting —Limiting how many requests per second from either a specific client and/or from all clients.
 Caching—Cache responses to reduce the number of requests made to the services.
 Metrics collection—Collect metrics on API usage for billing analytics purposes.
 Request logging—Log requests.
There are three different places in your application where you could implement these
edge functions. First, you can implement them in the backend services. This might
make sense for some functions, such as caching, metrics collection, and possibly authorization. But it’s generally more secure if the application authenticates requests on the
edge before they reach the services.

The solution is to have an API gateway for each client, the so-called Backends for frontends (BFF) pattern, which was pioneered by Phil Calçado (http://philcalcado.com/)
and his colleagues at SoundCloud. As figure 8.7 shows, each API module becomes its
own standalone API gateway that’s developed and operated by a single client team.
Pattern: Backends for frontends
Implement a separate API gateway for each type of client. See http://microservices
.io/patterns/apigateway.html.

 Benefits and drawbacks of an API gateway
As you might expect, the API gateway pattern has both benefits and drawbacks.
BENEFITS OF AN API GATEWAY
A major benefit of using an API gateway is that it encapsulates internal structure of the
application. Rather than having to invoke specific services, clients talk to the gateway.
The API gateway provides each client with a client-specific API, which reduces the
number of round-trips between the client and application. It also simplifies the client
code.
DRAWBACKS OF AN API GATEWAY
The API gateway pattern also has some drawbacks. It is yet another highly available
component that must be developed, deployed, and managed. There’s also a risk that
the API gateway becomes a development bottleneck. Developers must update the API
gateway in order to expose their services’s API. It’s important that the process for
updating the API gateway be as lightweight as possible. Otherwise, developers will be
forced to wait in line in order to update the gateway. Despite these drawbacks, though,
for most real-world applications, it makes sense to use an API gateway. If necessary,
you can use the Backends for frontends pattern to enable the teams to develop and
deploy their APIs independently. 

API gateway design issues
Now that we’ve looked at the API gateway pattern and its benefits and drawbacks, let’s
examine various API gateway design issues. There are several issues to consider when
designing an API gateway:
 Performance and scalability
 Writing maintainable code by using reactive programming abstractions
 Handling partial failure
 Being a good citizen in the application’s architecture

Implementing an API gateway
Let’s now look at how to implement an API gateway. As mentioned earlier, the responsibilities of an API gateway are as follows:
 Request routing—Routes requests to services using criteria such as HTTP request
method and path. The API gateway must route using the HTTP request method
when the application has one or more CQRS query services. As discussed in
chapter 7, in such an architecture commands and queries are handled by separate services.
 API composition—Implements a GET REST endpoint using the API composition
pattern, described in chapter 7. The request handler combines the results of
invoking multiple services.
 Edge functions—Most notable among these is authentication.
 Protocol translation—Translates between client-friendly protocols and the clientunfriendly protocols used by services.
 Being a good citizen in the application’s architecture.
There are a couple of different ways to implement an API gateway:
 Using an off-the-shelf API gateway product/service—This option requires little or no
development but is the least flexible. For example, an off-the-shelf API gateway
typically does not support API composition
 Developing your own API gateway using either an API gateway framework or a web framework as the starting point—This is the most flexible approach, though it requires
some development effort.

Schema-driven API technologies
The two most popular graph-based API technologies are GraphQL (http://graphql.org)
and Netflix Falcor (http://netflix.github.io/falcor/). Netflix Falcor models server-side
data as a virtual JSON object graph. The Falcor client retrieves data from a Falcor
server by executing a query that retrieves properties of that JSON object. The client
can also update properties. In the Falcor server, the properties of the object graph
are mapped to backend data sources, such as services with REST APIs. The server
handles a request to set or get properties by invoking one or more backend data
sources.
GraphQL, developed by Facebook and released in 2015, is another popular graphbased API technology. It models the server-side data as a graph of objects that have
fields and references to other objects. The object graph is mapped to backend data
sources. GraphQL clients can execute queries that retrieve data and mutations that
create and update data. Unlike Netflix Falcor, which is an implementation, GraphQL
is a standard, with clients and servers available for a variety of languages, including
NodeJS, Java, and Scala.
Apollo GraphQL is a popular JavaScript/NodeJS implementation (www.apollographql
.com). It’s a platform that includes a GraphQL server and client. Apollo GraphQL
implements some powerful extensions to the GraphQL specification, such as subscriptions that push changed data to the client.

### Testing microservices

THE DIFFERENT TYPES OF TESTS
There are many different types of tests. Some tests, such as performance tests and
usability tests, verify that the application satisfies its quality of service requirements. In
this chapter, I focus on automated tests that verify the functional aspects of the application or service. I describe how to write four different types of tests:
 Unit tests—Test a small part of a service, such as a class.
 Integration tests—Verify that a service can interact with infrastructure services
such as databases and other application services.
 Component tests—Acceptance tests for an individual service.
 End-to-end tests—Acceptance tests for the entire application.

TESTING USING MOCKS AND STUBS

CONSUMER-DRIVEN CONTRACT TESTING

Pattern: Consumer-driven contract test
Verify that a service meets the expectations of its clients See http://microservices.io/patterns/testing/service-integration-contract-test.html.

Consumer-driven contract tests typically use testing by example. The interaction
between a consumer and provider is defined by a set of examples, known as contracts.
Each contract consists of example messages that are exchanged during one interaction
For instance, a contract for a REST API consists of an example HTTP request and
response. On the surface, it may seem better to define the interaction using schemas
written using, for example, OpenAPI or JSON schema. But it turns out schemas aren’t
that useful when writing tests. A test can validate the response using the schema but it
still needs to invoke the provider with an example request.
 What’s more, consumer tests also need example responses. That’s because even
though the focus of consumer-driven contract testing is to test a provider, contracts
are also used to verify that the consumer conforms to the contract. For instance, a
consumer-side contract test for a REST client uses the contract to configure an HTTP
stub service that verifies that the HTTP request matches the contract’s request and
sends back the contract’s HTTP response. Testing both sides of interaction ensures
that the consumer and provider agree on the API. Later on we’ll look at examples of
how to write this kind of testing, but first let’s see how to write consumer contract tests
using Spring Cloud Contract

Pattern: Consumer-side contract test
Verify that the client of a service can communicate with the service. See https://
microservices.io/patterns/testing/consumer-side-contract-test.html. 


The example deployment pipeline shown in figure 9.9 consists of the following
stages:
 Pre-commit tests stage—Runs the unit tests. This is executed by the developer
before committing their changes.
 Commit tests stage—Compiles the service, runs the unit tests, and performs static
code analysis.
 Integration tests stage—Runs the integration tests.
 Component tests stage—Runs the component tests for the service.
 Deploy stage—Deploys the service into production.

The contracts are used to test both the consumer and the provider, which ensures
that they agree on the API. They’re used in slightly different ways depending on
whether you’re testing the consumer or the provider:
 Consumer-side tests—These are tests for the consumer’s adapter. They use the
contracts to configure stubs that simulate the provider, enabling you to write
integration tests for a consumer that don’t require a running provider.
 Provider-side tests—These are tests for the provider’s adapter. They use the contracts to test the adapters using mocks for the adapters’s dependencies.

Developing component tests
So far, we’ve looked at how to test individual classes and clusters of classes. But imagine that we now want to verify that Order Service works as expected. In other words,
we want to write the service’s acceptance tests, which treat it as a black box and verify
its behavior through its API. One approach is to write what are essentially end-to-end
tests and deploy Order Service and all of its transitive dependencies. As you should
know by now, that’s a slow, brittle, and expensive way to test a service.

Pattern: Service component test
Test a service in isolation. See http://microservices.io/patterns/testing/servicecomponent-test.html.

### Developing production-ready services

## Developing secure services

An application developer is primarily responsible for implementing four different
aspects of security:
 Authentication—Verifying the identity of the application or human (a.k.a. the
principal) that’s attempting to access the application. For example, an application typically verifies a principal’s credentials, such as a user ID and password or
an application’s API key and secret.
 Authorization—Verifying that the principal is allowed to perform the requested
operation on the specified data. Applications often use a combination of rolebased security and access control lists (ACLs). Role-based security assigns each
user one or more roles that grant them permission to invoke particular operations. ACLs grant users or roles permission to perform an operation on a particular business object, or aggregate.
 Auditing—Tracking the operations that a principal performs in order to detect
security issues, help customer support, and enforce compliance.
 Secure interprocess communication—Ideally, all communication in and out of services should be over Transport Layer Security (TLS). Interservice communication may even need to use authentication.

## security in a traditional monolithic application

Using a security framework
Implementing authentication and authorization correctly is challenging. It’s best to
use a proven security framework. Which framework to use depends on your application’s technology stack. Some popular frameworks include the following:
 Spring Security (https://projects.spring.io/spring-security/)—A popular framework for Java applications. It’s a sophisticated framework that handles authentication and authorization.
 Apache Shiro (https://shiro.apache.org)—Another Java framework.
 Passport (http://www.passportjs.org)—A popular security framework for NodeJS
applications that’s focused on authentication.

## Security in a microservice architecture

One challenge with implementing security in a microservices application is that we
can’t just copy the design from a monolithic application. That’s because two aspects of
the monolithic application’s security architecture are nonstarters for a microservice
architecture:
 In-memory security context—Using an in-memory security context, such as a threadlocal, to pass around user identity. Services can’t share memory, so they can’t
use an in-memory security context, such as a thread-local, to pass around the user identity. In a microservice architecture, we need a different mechanism for
                                                                              passing user identity from one service to another.
                                                                               Centralized session —Because an in-memory security context doesn’t make sense,
                                                                              neither does an in-memory session. In theory, multiple services could access a
                                                                              database-based session, except that it would violate the principle of loose coupling. We need a different session mechanism in a microservice architecture.
                                                                              
HANDLING AUTHENTICATION IN THE API GATEWAY

There are a couple of different ways to handle authentication. One option is for the
individual services to authenticate the user. The problem with this approach is that it
permits unauthenticated requests to enter the internal network. It relies on every
development team correctly implementing security in all of their services. As a result,
there’s a significant risk of an application containing security vulnerabilities.
 Another problem with implementing authentication in the services is that different clients authenticate in different ways. Pure API clients supply credentials with
each request using, for example, basic authentication. Other clients might first log in
and then supply a session token with each request. We want to avoid requiring services
to handle a diverse set of authentication mechanisms.
 A better approach is for the API gateway to authenticate a request before forwarding it to the services. Centralizing API authentication in the API gateway has the
advantage that there’s only one place to get right. As a result, there’s a much smaller
chance of a security vulnerability. Another benefit is that only the API gateway has to
deal with the various different authentication mechanisms. It hides this complexity
from the services.
 Figure 11.3 shows how this approach works. Clients authenticate with the API gateway. API clients include credentials in each request. Login-based clients POST the
user’s credentials to the API gateway’s authentication and receive a session token.
Once the API gateway has authenticated a request, it invokes one or more services.

Pattern: Access token
The API gateway passes a token containing information about the user, such as their
identity and their roles, to the services that it invokes. See http://microservices.io/
patterns/security/access-token.html.

The sequence of events for API clients is as follows:
1 A client makes a request containing credentials.
2 The API gateway authenticates the credentials, creates a security token, and
passes that to the service or services.
The sequence of events for login-based clients is as follows:
1 A client makes a login request containing credentials.
2 The API gateway returns a security token.
3 The client includes the security token in requests that invoke operations.
4 The API gateway validates the security token and forwards it to the service or
services.

The key concepts in OAuth 2.0 are the following:
Authorization Server—Provides an API for authenticating users and obtaining an access token and a refresh token. Spring OAuth is a great example of a
framework for building an OAuth 2.0 authorization server.
 Access Token—A token that grants access to a Resource Server. The format of
the access token is implementation dependent. But some implementations,
such as Spring OAuth, use JWTs.
 Refresh Token—A long-lived yet revocable token that a Client uses to obtain a
new AccessToken.
 Resource Server—A service that uses an access token to authorize access. In a
microservice architecture, the services are resource servers.
 Client—A client that wants to access a Resource Server. In a microservice
architecture, API Gateway is the OAuth 2.0 client.

Pattern: Externalized configuration
Supply configuration property values, such as database credentials and network
location, to a service at runtime. See http://microservices.io/patterns/externalizedconfiguration.html.

An externalized configuration mechanism provides the configuration property values
to a service instance at runtime. There are two main approaches:
 Push model—The deployment infrastructure passes the configuration properties
to the service instance using, for example, operating system environment variables or a configuration file.
 Pull model—The service instance reads its configuration properties from a configuration server.

Using a configuration server has several benefits:
 Centralized configuration—All the configuration properties are stored in one
place, which makes them easier to manage. What’s more, in order to eliminate
duplicate configuration properties, some implementations let you define global
defaults, which can be overridden on a per-service basis.
 Transparent decryption of sensitive data—Encrypting sensitive data such as database
credentials is a security best practice. One challenge of using encryption, though,
is that usually the service instance needs to decrypt them, which means it needs
the encryption keys. Some configuration server implementations automatically
decrypt properties before returning them to the service.
 Dynamic reconfiguration—A service could potentially detect updated property values by, for example, polling, and reconfigure itself.

patterns to design observable services:
 Health check API—Expose an endpoint that returns the health of the service.
 Log aggregation—Log service activity and write logs into a centralized logging
server, which provides searching and alerting.
Distributed tracing—Assign each external request a unique ID and trace requests
as they flow between services.
 Exception tracking—Report exceptions to an exception tracking service, which
de-duplicates exceptions, alerts developers, and tracks the resolution of each
exception.
 Application metrics—Services maintain metrics, such as counters and gauges, and
expose them to a metrics server.
 Audit logging—Log user actions.

## Using the Health check API pattern

Sometimes a service may be running but unable to handle requests. For instance, a
newly started service instance may not be ready to accept requests. The FTGO Consumer Service, for example, takes around 10 seconds to initialize the messaging and
database adapters. It would be pointless for the deployment infrastructure to route
HTTP requests to a service instance until it’s ready to process them.
 Also, a service instance can fail without terminating. For example, a bug might
cause an instance of Consumer Service to run out of database connections and
be unable to access the database. The deployment infrastructure shouldn’t route
requests to a service instance that has failed yet is still running. And, if the service
instance does not recover, the deployment infrastructure must terminate it and create
a new instance.

Pattern: Health check API
A service exposes a health check API endpoint, such as GET /health, which returns
the health of the service. See http://microservices.io/patterns/observability/healthcheck-api.html.

## Applying the Log aggregation pattern

Logs are a valuable troubleshooting tool. If you want to know what’s wrong with your
application, a good place to start is the log files. But using logs in a microservice architecture is challenging. For example, imagine you’re debugging a problem with the
getOrderDetails() query. As described in chapter 8, the FTGO application implements this query using API composition. As a result, the log entries you need are scattered across the log files of the API gateway and several services, including Order
Service and Kitchen Service.
Pattern: Log aggregation
Aggregate the logs of all services in a centralized database that supports searching
and alerting. See http://microservices.io/patterns/observability/application-logging
.html

THE LOG AGGREGATION INFRASTRUCTURE
The logging infrastructure is responsible for aggregating the logs, storing them, and
enabling the user to search them. One popular logging infrastructure is the ELK
stack. ELK consists of three open source products:
 Elasticsearch—A text search-oriented NoSQL database that’s used as the logging
server
 Logstash—A log pipeline that aggregates the service logs and writes them to
Elasticsearch
 Kibana—A visualization tool for Elasticsearch
Other open source log pipelines include Fluentd and Apache Flume. Examples of logging servers include cloud services, such as AWS CloudWatch Logs, as well as numerous
commercial offerings. Log aggregation is a useful debugging tool in a microservice
architecture.

## Using the Distributed tracing pattern

Pattern: Distributed tracing
Assign each external request a unique ID and record how it flows through the system
from one service to the next in a centralized server that provides visualization and
analysis. See http://microservices.io/patterns/observability/distributed-tracing.html.

## Using the Exception tracking pattern

A service should rarely log an exception, and when it does, it’s important that you
identify the root cause. The exception might be a symptom of a failure or a programming bug. The traditional way to view exceptions is to look in the logs. You might even
configure the logging server to alert you if an exception appears in the log file. There
are, however, several problems with this approach:
 Log files are oriented around single-line log entries, whereas exceptions consist
of multiple lines.
 There’s no mechanism to track the resolution of exceptions that occur in log
files. You would have to manually copy/paste the exception into an issue tracker.
 There are likely to be duplicate exceptions, but there’s no automatic mechanism to treat them as one.

Pattern: Exception tracking
Services report exceptions to a central service that de-duplicates exceptions, generates alerts, and manages the resolution of exceptions. See http://microservices.io/
patterns/observability/audit-logging.html.

Exception tracking services
There are several exception tracking services. Some, such as Honeybadger (www
.honeybadger.io), are purely cloud-based. Others, such as Sentry.io (https://sentry.io/
welcome/), also have an open source version that you can deploy on your own infrastructure. These services receive exceptions from your application and generate alerts.
They provide a console for viewing exceptions and managing their resolution. An exception tracking service typically provides client libraries in a variety of languages.

## Applying the Audit logging pattern

The purpose of audit logging is to record each user’s actions. An audit log is typically
used to help customer support, ensure compliance, and detect suspicious behavior.
Each audit log entry records the identity of the user, the action they performed, and
the business object(s). An application usually stores the audit log in a database table.

Pattern: Audit logging
Record user actions in a database in order to help customer support, ensure compliance, and detect suspicious behavior. See http://microservices.io/patterns/
observability/audit-logging.html.

There are a few different ways to implement audit logging:
 Add audit logging code to the business logic.
 Use aspect-oriented programming (AOP).
 Use event sourcing.

ADD AUDIT LOGGING CODE TO THE BUSINESS LOGIC
The first and most straightforward option is to sprinkle audit logging code throughout your service’s business logic. Each service method, for example, can create an
audit log entry and save it in the database. The drawback with this approach is that it
intertwines auditing logging code and business logic, which reduces maintainability.
The other drawback is that it’s potentially error prone, because it relies on the developer writing audit logging code.
USE ASPECT-ORIENTED PROGRAMMING
The second option is to use AOP. You can use an AOP framework, such as Spring
AOP, to define advice that automatically intercepts each service method call and persists an audit log entry. This is a much more reliable approach, because it automatically records every service method invocation. The main drawback of using AOP is
that the advice only has access to the method name and its arguments, so it might be
challenging to determine the business object being acted upon and generate a businessoriented audit log entry.
USE EVENT SOURCING
The third and final option is to implement your business logic using event sourcing.
As mentioned in chapter 6, event sourcing automatically provides an audit log for create and update operations. You need to record the identity of the user in each event.
One limitation with using event sourcing, though, is that it doesn’t record queries. If
your service must create log entries for queries, then you’ll have to use one of the
other options as well. 

## Developing services using the Microservice chassis pattern

Pattern: Microservice chassis
Build services on a framework or collection of frameworks that handle cross-cutting
concerns, such as exception tracking, logging, health checks, externalized configuration, and distributed tracing. See http://microservices.io/patterns/microservicechassis.html.

## From microservice chassis to service mesh

A microservice chassis is a good way to implement various cross-cutting concerns, such
as circuit breakers. But one obstacle to using a microservice chassis is that you need
one for each programming language you use. For example, Spring Boot and Spring
Cloud are useful if you’re a Java/Spring developer, but they aren’t any help if you
want to write a NodeJS-based service.

Pattern: Service mesh
Route all network traffic in and out of services through a networking layer that implements various concerns, including circuit breakers, distributed tracing, service discovery, load balancing, and rule-based traffic routing. See http://microservices.io/
patterns/deployment/service-mesh.html.

### Deploying microservices

A production environment must implement four key capabilities:
 Service management interface—Enables developers to create, update, and configure services. Ideally, this interface is a REST API invoked by command-line and
GUI deployment tools.
 Runtime service management—Attempts to ensure that the desired number of service instances is running at all times. If a service instance crashes or is somehow
unable to handle requests, the production environment must restart it. If a
machine crashes, the production environment must restart those service instances
on a different machine.
 Monitoring—Provides developers with insight into what their services are doing,
including log files and metrics. If there are problems, the production environment must alert the developers. Chapter 11 describes monitoring, also called
observability.
 Request routing—Routes requests from users to the services.

## Deploying services using the Language-specific packaging format pattern  

Pattern: Language-specific packaging format
Deploy a language-specific package into production. See http://microservices.io/
patterns/deployment/language-specific-packaging.html.

## Deploying services using the Service as a virtual machine pattern

Once again, imagine you want to deploy the FTGO Restaurant Service, except this
time it’s on AWS EC2. One option would be to create and configure an EC2 instance
and copy onto it the executable or WAR file. Although you would get some benefit
from using the cloud, this approach suffers from the drawbacks described in the preceding section. A better, more modern approach is to package the service as an Amazon Machine Image (AMI), as shown in figure 12.6. Each service instance is an EC2
instance created from that AMI. The EC2 instances would typically be managed by an
AWS Auto Scaling group, which attempts to ensure that the desired number of
healthy instances is always running.
   
Pattern: Deploy a service as a VM
Deploy services packaged as VM images into production. Each service instance is a
VM. See http://microservices.io/patterns/deployment/service-per-vm.html.

The benefits of deploying services as VMs
The Service as a virtual machine pattern has a number of benefits:
 The VM image encapsulates the technology stack.
 Isolated service instances.
 Uses mature cloud infrastructure.

THE VM IMAGE ENCAPSULATES THE TECHNOLOGY STACK
An important benefit of this pattern is that the VM image contains the service and all
of its dependencies. It eliminates the error-prone requirement to correctly install and
set up the software that a service needs in order to run. Once a service has been packaged as a virtual machine, it becomes a black box that encapsulates your service’s technology stack. The VM image can be deployed anywhere without modification. The API
for deploying the service becomes the VM management API. Deployment becomes
much simpler and more reliable.
SERVICE INSTANCES ARE ISOLATED
A major benefit of virtual machines is that each service instance runs in complete isolation. That, after all, is one of the main goals of virtual machine technology. Each virtual machine has a fixed amount of CPU and memory and can’t steal resources from
other services.
USES MATURE CLOUD INFRASTRUCTURE
Another benefit of deploying your microservices as virtual machines is that you can
leverage mature, highly automated cloud infrastructure. Public clouds such as AWS
attempt to schedule VMs on physical machines in a way that avoids overloading the
machine. They also provide valuable features such as load balancing of traffic across
VMs and autoscaling. 

The Service as a VM pattern also has some drawbacks:
 Less-efficient resource utilization
 Relatively slow deployments
 System administration overhead

LESS-EFFICIENT RESOURCE UTILIZATION
Each service instance has the overhead of an entire virtual machine, including its
operating system. Moreover, a typical public IaaS virtual machine offers a limited set
of VM sizes, so the VM will probably be underutilized. This is less likely to be a problem for Java-based services because they’re relatively heavyweight. But this pattern
might be an inefficient way of deploying lightweight NodeJS and GoLang services.
RELATIVELY SLOW DEPLOYMENTS
Building a VM image typically takes some number of minutes because of the size of
the VM. There are lots of bits to be moved over the network. Also, instantiating a VM
from a VM image is time consuming because of, once again, the amount of data that
must be moved over the network. The operating system running inside the VM also
takes some time to boot, though slow is a relative term. This process, which perhaps
takes minutes, is much faster than the traditional deployment process. But it’s much
slower than the more lightweight deployment patterns you’ll read about soon.
SYSTEM ADMINISTRATION OVERHEAD
You’re responsible for patching the operation system and runtime. System administration may seem inevitable when deploying software, but later in section 12.5, I describe
serverless deployment, which eliminates this kind of system administration.

##  Deploying services using the Service as a container pattern

Containers are a more modern and lightweight deployment mechanism. They’re an
operating-system-level virtualization mechanism. A container, as figure 12.7 shows,
consists of usually one but sometimes multiple processes running in a sandbox, which
isolates it from other containers. A container running a Java service, for example,
would typically consist of the JVM process.
 From the perspective of a process running in a container, it’s as if it’s running on
its own machine. It typically has its own IP address, which eliminates port conflicts. All
Java processes can, for example, listen on port 8080. Each container also has its own
root filesystem. The container runtime uses operating system mechanisms to isolate
the containers from each other. The most popular example of a container runtime is
Docker, although there are others, such as Solaris Zones.

Pattern: Deploy a service as a container
Deploy services packaged as container images into production. Each service instance
is a container. See http://microservices.io/patterns/deployment/service-per-container
.html.

## 2 Benefits of deploying services as containers
   Deploying services as containers has several benefits. First, containers have many of
   the benefits of virtual machines:
    Encapsulation of the technology stack in which the API for managing your services becomes the container API.
    Service instances are isolated.
    Service instances’s resources are constrained
   
## Deploying the FTGO application with Kubernetes

Kubernetes is a Docker orchestration framework. A Docker orchestration framework treats
a set of machines running Docker as a pool of resources. You tell the Docker orchestration framework to run N instances of your service, and it handles the rest. Figure 12.9
shows the architecture of a Docker orchestration framework.
 A Docker orchestration framework, such as Kubernetes , has three main functions:
 Resource management—Treats a cluster of machines as a pool of CPU, memory,
and storage volumes, turning the collection of machines into a single machine.
 Scheduling—Selects the machine to run your container. By default, scheduling
considers the resource requirements of the container and each node’s available
resources. It might also implement affinity, which colocates containers on the
same node, and anti-affinity, which places containers on different nodes.
 Service management—Implements the concept of named and versioned services
that map directly to services in the microservice architecture. The orchestration
framework ensures that the desired number of healthy instances is running at
all times. It load balances requests across them. The orchestration framework
performs rolling upgrades of services and lets you roll back to an old version.

KUBERNETES ARCHITECTURE
Kubernetes runs on a cluster of machines. Figure 12.10 shows the architecture of a
Kubernetes cluster. Each machine in a Kubernetes cluster is either a master or a node.
A typical cluster has a small number of masters—perhaps just one—and many nodes.
A master machine is responsible for managing the cluster. A node is a worker than runs
one or more pods. A pod is Kubernetes’s unit of deployment and consists of a set of
containers.
 A master runs several components, including the following:
 API server—The REST API for deploying and managing services, used by the
kubectl command-line interface, for example.
 Etcd—A key-value NoSQL database that stores the cluster data.
Scheduler—Selects a node to run a pod.
 Controller manager—Runs the controllers, which ensure that the state of the cluster matches the intended state. For example, one type of controller known as a
replication controller ensures that the desired number of instances of a service
are running by starting and terminating instances.
A node runs several components, including the following:
 Kubelet—Creates and manages the pods running on the node
 Kube-proxy—Manages networking, including load balancing across pods
 Pods—The application services

KEY KUBERNETES CONCEPTS
As mentioned in the introduction to this section, Kubernetes is quite complex. But it’s
possible to use Kubernetes productively once you master a few key concepts, called
objects. Kubernetes defines many types of objects. From a developer’s perspective, the
most important objects are the following:
 Pod—A pod is the basic unit of deployment in Kubernetes. It consists of one or
more containers that share an IP address and storage volumes. The pod for a
service instance often consists of a single container, such as a container running
the JVM. But in some scenarios a pod contains one or more sidecar containers,
which implement supporting functions. For example, an NGINX server could
have a sidecar that periodically does a git pull to download the latest version
of the website. A pod is ephemeral, because either the pod’s containers or the
node it’s running on might crash.
 Deployment—A declarative specification of a pod. A deployment is a controller
that ensures that the desired number of instances of the pod (service instances)
are running at all times. It supports versioning with rolling upgrades and rollbacks. Later in section 12.4.2, you’ll see that each service in a microservice
architecture is a Kubernetes deployment.
 Service—Provides clients of an application service with a static/stable network
location. It’s a form of infrastructure-provided service discovery, described in
chapter 3. A service has an IP address and a DNS name that resolves to that IP
address and load balances TCP and UDP traffic across one or more pods. The
IP address and a DNS name are only accessible within the Kubernetes. Later, I
describe how to configure services that are accessible from outside the cluster.
 ConfigMap—A named collection of name-value pairs that defines the externalized configuration for one or more application services (see chapter 11 for an
overview of externalized configuration). The definition of a pod’s container
can reference a ConfigMap to define the container’s environment variables. It
can also use a ConfigMap to create configuration files inside the container. You
can store sensitive information, such as passwords, in a form of ConfigMap
called a Secret

## Zero-downtime deployments

## Deploying services using the Serverless deployment pattern

Pattern: Serverless deployment
Deploy services using a serverless deployment mechanism provided by a public cloud.
See http://microservices.io/patterns/deployment/serverless-deployment.html.

Benefits of using lambda functions
Deploying services using lambda functions has several benefits:
 Integrated with many AWS services—It’s remarkably straightforward to write lambdas that consume events generated by AWS services, such as DynamoDB and
Kinesis, and handle HTTP requests via the AWS API Gateway.
 Eliminates many system administration tasks—You’re no longer responsible for lowlevel system administration. There are no operating systems or runtimes to
patch. As a result, you can focus on developing your application.
 Elasticity—AWS Lambda runs as many instances of your application as are needed
to handle the load. You don’t have the challenge of predicting needed capacity or
run the risk of underprovisioning or overprovisioning VMs or containers.
 Usage-based pricing—Unlike a typical IaaS cloud, which charges by the minute or
hour for a VM or container even when it’s idle, AWS Lambda only charges you
for the resources that are consumed while processing each request. 



## The DevOps story: Building for the rigors of runtime

While DevOps is a rich and emerging IT field, for the DevOps engineer, the design of
the microservice is all about managing the service after it goes into production. Writing the code is often the easy part. Keeping it running is the hard part. We’ll start our
microservice development effort with four principles and build on these later in the
book:
 A microservice should be self-contained. It should also be independently deployable
with multiple instances of the service being started up and torn down with a single software artifact.
 A microservice should be configurable. When a service instance starts up, it should
read the data it needs to configure itself from a central location or have its configuration information passed on as environment variables. No human intervention should be required to configure the service.
 A microservice instance needs to be transparent to the client. The client should never
know the exact location of a service. Instead, a microservice client should talk
to a service discovery agent. That allows the application to locate an instance of
a microservice without having to know its physical location.
 A microservice should communicate its health. This is a critical part of your cloud
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
 Service assembly—How you package and deploy your service to guarantee repeatability and consistency so that the same service code and run time are deployed
exactly the same way.
 Service bootstrapping—How you separate your application and environmentspecific configuration code from the run-time code so that you can start and
deploy a microservice instance quickly in any environment without human
intervention.
 Service registration/discovery—When a new microservice instance is deployed,
how you make the new service instance discoverable by other application
clients.
 Service monitoring—In a microservice environment, it’s common for multiple
instances of the same service to be running due to high availability needs. From
a DevOps perspective, you need to monitor microservice instances and ensure
that any faults are routed around failing service instances, and that these are
taken down. 

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro10.png)

#### Service assembly: Packaging and deploying your microservices

From a DevOps perspective, one of the key concepts behind a microservice architecture is that multiple instances of a microservice can be deployed quickly in response
to a changed application environment (for example, a sudden influx of user requests,
problems within the infrastructure, and so on). To accomplish this, a microservice
needs to be packaged and installable as a single artifact with all of its dependencies
defined within it. These dependencies must also include the run-time engine (for
example, an HTTP server or application container) that hosts the microservice.
 The process of consistently building, packaging, and deploying is the service
assembly (step 1 in figure 3.9). Figure 3.10 shows additional details about this step.
![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro11.png)

#### Service bootstrapping: Managing configuration of your microservices

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
 Configuration data tends to be simple in structure and is usually read frequently and written infrequently. Relational databases are overkill in this situation because they’re designed to manage much more complicated data models
than a simple set of key-value pairs.
 Because the data is accessed on a regular basis but changes infrequently, the
data must be readable with a low level of latency.
 The data store has to be highly available and close to the services reading the
data. A configuration data store can’t go down completely because it would
become a single point of failure for your application.
In chapter 5, we’ll show how to manage your microservice application configuration
data using things like a simple key-value data store. 

#### Service registration and discovery: How clients communicate with your microservices
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

#### Communicating a microservice’s health

A service discovery agent doesn’t act only as a traffic cop that guides the client to the
location of the service. In a cloud-based microservice application, you’ll often have
multiple instances of a running service. Sooner or later, one of those service instances
will fail. The service discovery agent monitors the health of each service instance registered with it and removes any failing service instances from its routing tables to ensure
that clients aren’t sent a service instance that has failed.
 After a microservice comes up, the service discovery agent will continue to monitor
and ping the health check interface to ensure that that service is available. This is step
4 in figure 3.9; figure 3.13 provides context for this step. 

![micro](https://raw.githubusercontent.com/JavaLvivDev/prog-resources/master/resources/micro/micro14.png)














List of Patterns
Application architecture patterns
Monolithic architecture (40)
Microservice architecture (40)
Decomposition patterns
Decompose by business capability (51)
Decompose by subdomain (54)
Messaging style patterns
Messaging (85)
Remote procedure invocation (72)
Reliable communications patterns
Circuit breaker (78)
Service discovery patterns
3rd party registration (85)
Client-side discovery (83)
Self-registration (82)
Server-side discovery (85)
Transactional messaging patterns
Polling publisher (98)
Transaction log tailing (99)
Transactional outbox (98)
Data consistency patterns
Saga (114)
Business logic design patterns
Aggregate (150)
Domain event (160)
Domain model (150)
Event sourcing (184)
Transaction script (149)
Querying patterns
API composition (223)
Command query responsibility segregation
(228)
External API patterns
API gateway (259)
Backends for frontends (265)
Testing patterns
Consumer-driven contract test (302)
Consumer-side contract test (303)
Service component test (335)
Security patterns
Access token (354)
Cross-cutting concerns patterns
Externalized configuration (361)
Microservice chassis (379)
Observability patterns
Application metrics (373)
Audit logging (377)
Distributed tracing (370)
Exception tracking (376)
Health check API (366)
Log aggregation (368)
Deployment patterns
Deploy a service as a container (393)
Deploy a service as a VM (390)
Language-specific packaging format (387)
Service mesh (380)
Serverless deployment (416)
Sidecar (410)
Refactoring to microservices patterns
Anti-corruption layer (447)
Strangler application (432)













