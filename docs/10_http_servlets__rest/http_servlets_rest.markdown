---
layout: default
title: HTTP, Servlets API, REST
nav_order: 10
permalink: /http_servlets_rest
has_children: true
---
<div align="center" markdown="1">
HTTP, Servlets API, REST / Java resources / Grokking the interview

{: .fs-6 .fw-300 }
</div>

- [Что на самом деле происходит, когда пользователь вбивает в браузер адрес google.com](https://habr.com/ru/company/htmlacademy/blog/254825/)

## REST
- [Подборка практик REST](https://gist.github.com/Londeren/838c8a223b92aa4017d3734d663a0ba3)
-  <a href="http://www.infoq.com/articles/springmvc_jsx-rs">JAX-RS vs Spring MVC</a>
- <a href="http://habrahabr.ru/post/144011/">RESTful API для сервера – делаем правильно (Часть 1)</a>
- <a href="http://habrahabr.ru/post/144259/">RESTful API для сервера – делаем правильно (Часть 2)</a>
- <a href="https://www.youtube.com/watch?v=Q84xT4Zd7vs&list=PLoij6udfBncivGZAwS2yQaFGWz4O7oH48">И. Головач. RestAPI</a>
- [value/name в аннотациях @PathVariable и @RequestParam](https://habr.com/ru/post/440214/)
- [15 тривиальных фактов о правильной работе с протоколом HTTP](https://habrahabr.ru/company/yandex/blog/265569/)
- [Идемпотентность API](https://habr.com/ru/company/yandex/blog/442762/)
- <a href="https://medium.com/@mwaysolutions/10-best-practices-for-better-restful-api-cbe81b06f291">10 Best Practices for Better RESTful
- [REST resource hierarchy (если кратко: не рекомендуется)](https://stackoverflow.com/questions/15259843/how-to-structure-rest-resource-hierarchy)
- [15 тривиальных фактов о правильной работе с протоколом HTTP](https://habrahabr.ru/company/yandex/blog/265569/)
- [REST vs SOAP](https://habr.com/ru/post/131343/)
- [REST — это новый SOAP](https://habr.com/ru/company/mailru/blog/345184/)
- [Разработка web API](https://habr.com/ru/post/181988/)
- [REST resource hierarchy](https://stackoverflow.com/questions/20951419/what-are-best-practices-for-rest-nested-resources)
- [Приложение двенадцати факторов — The Twelve-Factor App](https://habr.com/ru/post/258739/#dependencies)
- [RESTful API для сервера – делаем правильно 1](https://habr.com/ru/post/144011/)
- [RESTful API для сервера – делаем правильно 2](https://habr.com/ru/post/144259/)
- [REST API Best Practices](https://habr.com/ru/post/351890/)

....Сети
........IP, TCP, UDP
........telnet, FTP, DNS, SMTP/POP3
....протокол HTTP 1.1
........Methods, status codes, headers
........Persistent connection, pipelining
........Chunked encoding
........Caching, encription, compression
........основы REST
........Архитектура простейшего многопоточного HTTP-сервера на Java
....Servlet API 3.0 (Tomcat)
........шаблон MVC
........HttpServlet, HttpServletRequest, HttpServletResponse
........Dependency Injection / Inversion-of-Control framework (Spring)


 Why use Servlets & JSPs?

What is the HTTP protocol?

HTML is part of the HTTP response

If that’s the response, what’s in the request?

GET is a simple request, POST can send user data

It’s true... you can send a little data with HTTP GET

Anatomy of an HTTP GET request

Anatomy of an HTTP POST request

4. Request and Response: Being a Servlet

Servlets are controlled by the Container

But there’s more to a servlet’s life
Your servlet inherits the lifecycle methods

The Three Big Lifecycle Moments

Each request runs in a separate thread!

In the beginning: loading and initializing
Servlet Initialization: when an object becomes a servlet
But a Servlet’s REAL job is to handle requests. That’s when a servlet’s life has meaning.
Request and Response: the key to everything, and the arguments to service()

The HTTP request Method determines whether doGet() or doPost() runs

Actually, one or more of the other HTTP Methods might make a (brief) appearance on the exam...

The difference between GET and POST

No, it’s not just about the size

The story of the non-idempotent request

POST is not idempotent

What determines whether the browser sends a GET or POST request?
What happens if you do NOT say method=“POST” in your <form>?

POST is NOT the default!

Sending and using a single parameter

Sending and using TWO parameters

Besides parameters, what else can I get from a Request object?

Review: servlet lifecycle and API

Review: HTTP and HttpServletRequest

So that’s the Request... now let’s see the Response

Using the response for I/O

Imagine you want to send a JAR to the client...

Servlet code to download the JAR

Whoa. What’s the deal with content type?

You’ve got two choices for output: characters or bytes

You can set response headers, you can add response headers

But sometimes you just don’t want to deal with the response yourself...

Servlet redirect makes the browser do the work
Using relative URLs in sendRedirect()

A request dispatch does the work on the server side

Redirect vs. Request Dispatch

Review: HttpServletResponse

Coffee Cram: Mock Exam Chapter 4

Coffee Cram: Chapter 4 Answers

5. Attributes and Listeners: Being a Web App

Kim wants to configure his email address in the DD, not hard-code it inside the servlet class

Init Parameters to the rescue

You can’t use servlet init parameters until the servlet is initialized

The servlet init parameters are read only ONCE—when the Container initializes the servlet

Testing your ServletConfig

How can a JSP get servlet init parameters?
What about the way we did it with the beer app? We passed the model info to the JSP using a request attribute...

Setting a request attribute works... but only for the JSP to which you forwarded the request

Context init parameters to the rescue

Remember the difference between servlet init parameters and context init parameters

ServletConfig is one per servlet ServletContext is one per web app

So what else can you do with your ServletContext?

What if you want an app init parameter that’s a database DataSource?
What she really wants is a listener.
She wants a ServletContextListener
Tutorial: a simple ServletContextListener
Making and using a context listener
We need three classes and one DD
Writing the listener class
Writing the attribute class (Dog)
Writing the servlet class
Writing the Deployment Descriptor
Compile and deploy
Try it out
Troubleshooting
The full story...
Listeners: not just for context events...
The eight listeners
The HttpSessionBindingListener

What, exactly, is an attribute?
Attributes are not parameters!
The Three Scopes: Context, Request, and Session
Attribute API
The dark side of attributes...
But then something goes horribly wrong...
Context scope isn’t thread-safe!
The problem in slow motion...
How do we make context attributes thread-safe?
Synchronizing the service method is a spectacularly BAD idea
Synchronizing the service method won’t protect a context attribute!
You don’t need a lock on the servlet... you need the lock on the context!
Are Session attributes thread-safe?
What’s REALLY true about attributes and thread-safety?
Protect session attributes by synchronizing on the HttpSession
SingleThreadModel is designed to protect instance variables
But how does the web container guarantee a servlet gets only one request at a time?
Which is the better STM implementation?
Only Request attributes and local variables are thread-safe!
Request attributes and Request dispatching
RequestDispatcher revealed
What’s wrong with this code?
You’ll get a big, fat IllegalStateException!

Coffee Cram: Mock Exam Chapter 5

Coffee Cram: Chapter 5 Answers

6. Session Management: Conversational state

Kim wants to keep client-specific state across multiple requests

It’s supposed to work like a REAL conversation...

How can he track the client’s answers?

How sessions work

One problem... how does the Container know who the client is?

The client needs a unique session ID

How do the Client and Container exchange Session ID info?
Cookies

The best part: the Container does virtually all the cookie work!

What if I want to know whether the session already existed or was just created?

What if I want ONLY a pre-existing session?

You can do sessions even if the client doesn’t accept cookies, but you have to do a little more work...
URL rewriting: something to fall back on
URL rewriting kicks in ONLY if cookies fail, and ONLY if you tell the response to encode the URL
URL rewriting works with sendRedirect()
Getting rid of sessions
How we want it to work...
The HttpSession interface
Key HttpSession methods
Setting session timeout
Can I use cookies for other things, or are they only for sessions?
Using Cookies with the Servlet API
Simple custom cookie example
Custom cookie example continued...
Key milestones for an HttpSession
Session lifecycle Events

Don’t forget about HttpSessionBindingListener
Session migration
The Beer Web App distributed across two VMs
Session migration in action

HttpSessionActivationListener lets attributes prepare for the big move...
Listener examples
Listener examples
Listener examples
Session-related Listeners
Session-related Event Listeners and Event Objects API overview

Session-related Listeners

Coffee Cram: Mock Exam Chapter 6

Coffee Cram: Chapter 6 Answers

Includes and imports can be messy

Tag Files: like include, only better

But how do you send it parameters?

To a Tag File, you don’t send request parameters, you send tag attributes!

Aren’t tag attributes declared in the TLD?

Tag Files use the attribute directive

When an attribute value is really big

Declaring body-content for a Tag File

Where the Container looks for Tag Files

When you need more than Tag Files... Sometimes you need Java

Making a Simple tag handler

A Simple tag with a body

The Simple tag API

The life of a Simple tag handler

What if the tag body uses an expression?

A tag with dynamic row data: iterating the body

A Simple tag with an attribute

What exactly IS a JspFragment?

SkipPageException: stops processing the page...

SkipPageException shows everything up to the point of the exception

But what happens when the tag is invoked from an included page?

SkipPageException stops only the page that directly invoked the tag

You still have to know about Classic tag handlers

Tag handler API

A very small Classic tag handler

A Classic tag handler with TWO methods

When a tag has a body: comparing Simple vs. Classic

Classic tags have a different lifecycle

The Classic lifecycle depends on return values

IterationTag lets you repeat the body

Default return values from TagSupport

OK, let’s get real...

Our dynamic <select> tag isn’t complete...

We could just add more custom tag attributes...

Son of more tag attributes

The return of the son of more tag attributes

I’m getting sick of these tag attributes!

Our tag handler code using the DynamicAttributes interface

The rest of the tag handler code

OK, there is a little bit of configuration in the TLD

What about Tag Files?

But what if you DO need access to the body contents?

With BodyTag, you get two new methods

With BodyTag, you can buffer the body

What if you have tags that work together?

A Tag can call its Parent Tag

Find out just how deep the nesting goes...

Simple tags can have Classic parents

You can walk up, but you can’t walk down...

Getting info from child to parent

Menu and MenuItem tag handlers

Getting an arbitrary ancestor

Using the PageContext API for tag handlers

Coffee Cram: Mock Exam Chapter 10

Coffee Cram: Chapter 10 Answers

11. Web App Deployment: Deploying your web app

The Joy of Deployment

What goes where in a web app
What she really wants is a WAR file

WAR files

What a deployed WAR file looks like

Making static content and JSPs directly accessible

How servlet mapping REALLY works

Servlet mappings can be “fake”

Subtle issues...

Configuring welcome files in the DD

How the Container chooses a welcome file

Configuring error pages in the DD

Configuring servlet initialization in the DD

Making an XML-compliant JSP: a JSP Document

Memorizing the EJB-related DD tags

Memorizing the JNDI <env-entry> DD tag

Memorizing the <mime-mapping> DD tag

Coffee Crem: Mock Exam Chapter 11

Coffee Crem: Chapter 11 Answers

12. Web App Security: Keep it secret, keep it safe

The Bad Guys are everywhere

And it’s not just the SERVER that gets hurt...

The Big 4 in servlet security

A little security story

How to Authenticate in HTTP World: the beginning of a secure transaction

A slightly closer look at how the Container does Authentication and Authorization

How did the Container do that ?

Keep security out of the code!

Who implements security in a web app?

The Big Jobs in servlet security

Just enough Authentication to discuss Authorization

Authorization Step 1: defining roles

Authorization Step 2: defining resource/method constraints

The <security-constraint> rules for <web-resource-collection> elements

Picky <security-constraint> rules for <auth-constraint> sub-elements

The way <auth-constraint> works

How multiple <security-constraint> elements interact

Dueling <auth-constraint> elements

Alice’s recipe servlet, a story about programmatic security...

Customizing methods: isUserInRole()

The declarative side of programmatic security

Authentication revisited

Implementing Authentication

Form-Based Authentication

Summary of Authentication types

She doesn’t know about J2EE’s “protected transport layer connection”

Securing data in transit: HTTPS to the rescue

How to implement data confidentiality and integrity sparingly and declaratively

Protecting the request data

Coffee Cram: Mock Exam Chapter 12

Coffee Cram: Chapter 12 Answers

13. Filters and Wrappers: The Power of Filters

Enhancing the entire web application

How about some kind of “filter”?

Filters are modular, and configurable in the DD

Three ways filters are like servlets

Building the request tracking filter

A filter’s life cycle

Think of filters as being “stackable”
A conceptual call stack example

Declaring and ordering filters

News Flash: As of version 2.4, filters can be applied to request dispatchers

Compressing output with a response-side filter

Architecture of a response filter

But is it really that simple?

The output has left the building

We can implement our OWN response
She doesn’t know about the servlet Wrapper classes

Wrappers rock

Adding a simple Wrapper to the design

Add an output stream Wrapper

The real compression filter code
“Off the path”

Compression wrapper code

Compression wrapper, helper class code

Coffee Cram: Mock Exam Chapter 13

Coffee Cram: Chapter 13 Answers

14. Patterns and Struts: Enterprise Design Patterns

Web site hardware can get complicated

Web application software can get complicated

Lucky for us, we have J2EE patterns
Common pressures

Performance (and the “ilities”)

Aligning our vernaculars...
Code to interfaces
Separation of Concerns & Cohesion
Hide Complexity

More design principles...
Loose Coupling
Remote Proxy
Increase Declarative Control

Patterns to support remote model components
A Fable: The Beer App Grows

How the Business Team supports the web designers when the MVC components are running on one JVM

How will they handle remote objects?

RMI makes life easy
What we want...
How RMI pulls it off

Just a little more RMI review

Adding RMI and JNDI to the controller

How about a “go-between” object?

The “go-between” is a Business Delegate

Simplify your Business Delegates with the Service Locator

Protecting the web designer’s JSPs from remote model complexity

Compare the local model diagram to this remote model diagram

There’s good news and bad news...

Time for a Transfer Object?
Service Locator and Business Delegate both simplify model components

Business tier patterns: quick review

Our very first pattern revisited... MVC
Where we left off...

MVC in a real web app

Looking at the MVC controller

Improving the MVC controllers
New and (shorter) controller pseudo-code

Designing our fantasy controller

Yes! It’s Struts in a nutshell

Is Struts a container?

How does Front Controller fit in?

Refactoring the Beer app for Struts

The Struts Beer app architecture

A form bean exposed

How an Action object ticks

struts-config.xml: tying it all together

Specifying Struts in the web.xml DD

Install Struts, and Just Run It!

Creating the deployment environment

Patterns review for the SCWCD

Business Delegate

Service Locator

Transfer Object

Intercepting Filter

Model, View, Controller (MVC)

Front Controller

Coffee Cram: Mock Exam Chapter 14

Coffee Cram: Chapter 14 Answers










