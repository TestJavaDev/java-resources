---
layout: default
title: WebProfile
parent: JavaEE
# nav_order: 1
permalink: /javaee/webprofile
---
<div align="center" markdown="1">
JavaEE / Java resources / Articles

{: .fs-6 .fw-300 }
</div>

- <a href="https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol/">HTTP</a>
- <a href="https://stackoverflow.com/tags/servlets/info/">Servlets</a>
- <a href="https://stackoverflow.com/tags/jsp/info/">JSP (JavaServer Pages)</a>
- <a href="https://stackoverflow.com/tags/jsf/info/">JSF (JavaServer Faces)</a>
- <a href="https://stackoverflow.com/tags/jstl/info/">JSTL</a>
- <a href="https://jaxenter.com/introducing-the-java-ee-web-profile-103275.html/">Introducing the Java EE Web Profile</a>
- <a href="http://java-course.ru/student/book1/servlet/">Сервлеты</a>
- <a href="https://stackoverflow.com/questions/2349633/doget-and-dopost-in-servlets/">doGet and doPost in Servlets</a>
- <a href="https://stackoverflow.com/questions/2095397/what-is-the-difference-between-jsf-servlet-and-jsp/">What is the difference between JSF, Servlet and JSP?</a>
- <a href="https://stackoverflow.com/questions/3106452/how-do-servlets-work-instantiation-sessions-shared-variables-and-multithreadi/">Servlets: Instantiation, sessions, shared variables and multithreading</a>
- <a href="https://devcolibri.com/как-создать-servlet-полное-руководство/">Руководство: как создать servlet</a>
- <a href="http://java-course.ru/student/book1/servlet/">Интернет-приложения на JAVA</a>
  - <a href="http://java-course.ru/student/book1/jsp/">JSP</a>
  - [Как создать Servlet? Полное руководство](https://devcolibri.com/как-создать-servlet-полное-руководство)
  - [JSTL для написания JSP страниц](https://devcolibri.com/jstl-для-написания-jsp-страниц/)
  - <a href="http://javatutor.net/articles/jstl-patterns-for-developing-web-application-1">JSTL: Шаблоны для разработки веб-приложений в java</a>
-  <a href="https://ru.wikipedia.org/wiki/HTTP_cookie">HTTP cookie</a></h3>
-  <a href="http://stackoverflow.com/questions/595872/under-what-conditions-is-a-jsessionid-created">Under what conditions is a JSESSIONID created?</a>
-  <a href="http://halyph.blogspot.ru/2014/08/how-to-disable-tomcat-session.html">Tomcat Session Serialization</a>

Для хранения сосотяния сессии (например корзины покупателя) в Servlet API есть механизм хранения объектов сессии (грубо- мультимапмапа, которая достается из хранилища по ключу). При создании сессии на стороне сервера (через `request.getSession`) создается кука `JSESSIONID`, которая передается между клиентом и сервером и является ключом в хранилище объектов сессий.
<a href="http://javatutor.net/books/tiej/servlets#_Toc39472970">Обработка сессий с помощью сервлетов</a>

- [Tomcat 7 Async Processing](http://stackoverflow.com/questions/7287244/tomcat-7-async-processing)
- [Async in Servlet 3.0 vs NIO in Servlet 3.1](http://stackoverflow.com/questions/39802643/java-async-in-servlet-3-0-vs-nio-in-servlet-3-1)
- [AsyncContext.start in Servlet 3.0](https://stackoverflow.com/questions/10073392/whats-the-purpose-of-asynccontext-start-in-servlet-3-0)
- [The Limited Usefulness of AsyncContext.start()](https://dzone.com/articles/limited-usefulness)
