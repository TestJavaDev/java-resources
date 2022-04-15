---
layout: default
title: Core Microservices
parent: Microservices
nav_order: 1
permalink: /microservices/core
---
<div align="center" markdown="1">
Core Microservices / Java resources / Grokking the interview

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





### Deploying your microservices

Unit tests vs. integration tests vs. platform tests
Figure 12.1 exposes several types of testing (unit, integration, and platform) during
the building and deployment of a service. Three types of testing are typical in this type
of a pipeline:
Unit tests—These are run immediately before the compilation of the service
code, but before deployment to an environment. The tests are designed to
run in complete isolation, with each unit test being small and narrow in focus.
A unit test should have no dependencies on third-party infrastructure databases, services, and so on. Usually, a unit test scope encompasses the testing of a single method or function.
 Integration tests—These are run immediately after packaging the service
code. They are designed to test an entire workflow, code path, and stub or to
mock primary services or components that would need to be called with thirdparty services. During integration testing, you might be running an in-memory
database to hold data, mocking out third-party service calls, and so on. With
integration tests, third-party dependencies are mocked or stubbed so that
any requests that would invoke a remote service are also mocked or stubbed.
The calls never leave the build server.
 Platform tests—These are run right before a service is deployed to an environment. These tests typically test an entire business flow and also call all the
third-party dependencies that would normally be called in a production system. Platform tests are running live in a particular environment and don’t
involve any mocked-out services. This type of test is run to determine integration problems with third-party services that would typically not be detected
when a third-party service is stubbed out during an integration test.
If you are interested in diving into more detail on how to create unit, integration, and
platform tests, we highly recommend Testing Java Microservices (Manning, 2018) by
Alex Soto Bueno, Andy Gumbrecht, and Jason Porter.

The build/deploy process is built on four core patterns. These patterns have emerged
from the collective experience of development teams building microservice and
cloud-based applications. These patterns include
 Continuous integration/continuous delivery (CI/CD)—With CI/CD, your application code isn’t only built and tested when it is committed and deployed. The
deployment of your code should go something like this: if the code passes its
unit, integration, and platform tests, it’s immediately promoted to the next
environment. The only stopping point in most organizations is the push to
production.
 Infrastructure as code—The final software artifact that’s pushed to development
and beyond is a machine image. The machine image with your microservice
installed in it is provisioned immediately after your microservice’s source code
is compiled and tested. The provisioning of the machine image occurs through
a series of scripts that run with each build. No human hands should ever touch
the server after it’s built. The provisioning scripts should be kept under source
control and managed like any other piece of code.
 Immutable server—Once a server image is built, the server’s configuration and
microservice are never touched after the provisioning process. This guarantees
that your environment won’t suffer from “configuration drift,” where a developer or system administrator made “one small change” that later caused an outage. If a change needs to be made, change the provisioning scripts for the
server and kick off a new build

## Creating our build/deploy pipeline



## Integrating Docker with our microservices





Handling partial failure using the Circuit breaker pattern
In a distributed system, whenever a service makes a synchronous request to another
service, there is an ever-present risk of partial failure. Because the client and the service are separate processes, a service may not be able to respond in a timely way to a
client’s request. The service could be down because of a failure or for maintenance.
Or the service might be overloaded and responding extremely slowly to requests.
Pattern: Circuit breaker
An RPI proxy that immediately rejects invocations for a timeout period after the number of consecutive failures exceeds a specified threshold. See http://microservices
.io/patterns/reliability/circuit-breaker.html.

DEVELOPING ROBUST RPI PROXIES
Whenever one service synchronously invokes another service, it should protect itself
using the approach described by Netflix (http://techblog.netflix.com/2012/02/faulttolerance-in-high-volume.html)
