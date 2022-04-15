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
