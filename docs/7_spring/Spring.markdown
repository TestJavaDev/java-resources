---
layout: default
title: Spring
nav_order: 7
permalink: /spring
has_children: true
---
<div align="center" markdown="1">
Spring / Java resources / Grokking the interview

{: .fs-6 .fw-300 }
</div>

- <a href="https://habr.com/ru/post/350682/">Spring interview questions</a>
- <a href="https://www.baeldung.com/spring-boot-interview-questions">Spring Boot Interview Questions</a>
- <a href="https://stackoverflow.com/questions/1061717/what-exactly-is-spring-framework-for">What exactly is Spring framework for</a>
- <a href="https://habr.com/ru/post/535816/">Мониторинг и профилирование Spring Boot приложения</a>

- <a href="https://martinfowler.com/articles/injection.html">Inversion of Control Containers and the Dependency Injection pattern</a>
- <a href="https://martinfowler.com/bliki/InversionOfControl.html">InversionOfControl</a>

### Spring Core

-  <a href="http://habrahabr.ru/post/222579/">Spring изнутри. Этапы инициализации контекста.</a>
-  <a href="https://ru.wikipedia.org/wiki/Инверсия_управления">Инверсия управления.</a>
-  <a href="https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#mvc-servlet-context-hierarchy">Spring Web MVC Tutorial</a>
-  <a href="http://habrahabr.ru/post/131993/">IoC, DI, IoC-контейнер — Просто о простом</a>
-  <a href="https://www.ibm.com/developerworks/ru/library/ws-springjava/index.html">Управление bean-компонентами Spring при конфигурировании на основе Java</a>
-  <a href="https://habr.com/ru/post/334448/">Обратная сторона Spring</a>
-  <a href="http://stackoverflow.com/questions/6827752/whats-the-difference-between-component-repository-service-annotations-in">Difference between @Component, @Repository & @Service annotations in Spring</a>
-  <a href="http://www.mkyong.com/spring/spring-auto-scanning-components/">Spring Auto Scanning Components</a>
-  <a href="http://www.seostella.com/ru/article/2012/02/12/ispolzovanie-annotacii-autowired-v-spring-3.html">Использование аннотации @Autowired</a>
-  <a href="https://docs.spring.io/spring/docs/current/spring-framework-reference/html/beans.html">Introduction to the Spring IoC container and beans</a>
- [Подготовка к Spring Professional Certification. Контейнер, IoC, бины](https://habr.com/ru/post/470305/)
-  <a href="http://it.vaclav.kiev.ua/2010/12/25/spring-framework-for-begginers-part-7/">Constructor против Setter Injection </a>
-  <a href="https://spring.io/guides">Getting Started</a>
-  <a href="https://docs.spring.io/spring/docs/current/spring-framework-reference/">Spring Framework Reference Documentation</a>
-  <a href="https://github.com/spring-projects">Spring на GitHub</a>
-  <a href="https://dzone.com/refcardz/spring-annotations">Spring Annotations</a>
-  <a href="http://www.mkyong.com/spring/spring-autowiring-qualifier-example/"> имя бина через @Qualifier</a>
- [Перевод "Field Dependency Injection Considered Harmful"](https://habrahabr.ru/post/334636/)
- [Field vs Constructor vs Setter DI](http://stackoverflow.com/questions/39890849/what-exactly-is-field-injection-and-how-to-avoid-it)
- [Юрий Ткач: Spring Framework - The Basics](https://www.youtube.com/playlist?list=PL6jg6AGdCNaWF-sUH2QDudBRXo54zuN1t)
- [Евгений Борисов — Spring-потрошитель, часть 1](https://www.youtube.com/watch?v=BmBr5diz8WA)
- [Евгений Борисов — Spring-потрошитель, часть 2](https://www.youtube.com/watch?v=cou_qomYLNU)
- [Mapping Entity->DTO: Controller or Service?](http://stackoverflow.com/questions/31644131)

### Spring Boot

- [Spring Boot the Ripper (Evgeny Borisov and Kirill Tolkachev)](https://www.youtube.com/watch?v=zEdHFXr9D9Y)
- [Введение в Spring Boot: создание простого REST API на Java](https://habr.com/ru/post/435144/)
- [Understanding Spring Boot](https://geowarin.com/understanding-spring-boot/)
- [В чем различие между Spring Framework и Spring Boot](https://ru.stackoverflow.com/questions/318146/%D0%92-%D1%87%D0%B5%D0%BC-%D1%80%D0%B0%D0%B7%D0%BB%D0%B8%D1%87%D0%B8%D0%B5-%D0%BC%D0%B5%D0%B6%D0%B4%D1%83-spring-framework-%D0%B8-spring-boot)
- [Использование аннотации @SpringBootApplication](https://java-ru-blog.blogspot.com/2020/02/annotation-springbootapplication.html)

### Spring Data

-  <a class="anchor" id="datajpa"></a><a href="http://projects.spring.io/spring-data-jpa/">Spring Data JPA</a>
-  <a href="https://habrahabr.ru/post/232381/#datajpa">Делегирование (в конце статьи)</a>
-  <a href="https://spring.io/blog/2011/02/10/getting-started-with-spring-data-jpa">Getting started with Spring Data JPA</a>
-  <a href="http://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.query-methods.query-creation">Query methods</a>
-  <a href="http://jeeconf.com/archive/jeeconf-2013/materials/spring-data/">Spring Data – новый взгляд на persistence (JeeConf)</a>
-  <a href="https://www.youtube.com/watch?v=nwM7A4TwU3M">Евгений Борисов — Spring Data? Да, та!</a>
-  <a href="https://github.com/spring-projects?query=spring-data">Github repositories</a>
-  <a href="http://www.petrikainulainen.net/spring-data-jpa-tutorial">Spring Data JPA Tutorial</a>
-  <a href="https://blog.42.nl/articles/spring-data-jpa-with-querydsl-repositories-made-easy/">Spring Data JPA with QueryDSL</a>
-  [SpEL support in Spring Data JPA @Query](https://spring.io/blog/2014/07/15/spel-support-in-spring-data-jpa-query-definitions)
-  <a href="http://habrahabr.ru/post/113945/">Кэширование в Spring Framework</a>
- [Транзакции в Spring Framework](https://medium.com/@kirill.sereda/%D1%82%D1%80%D0%B0%D0%BD%D0%B7%D0%B0%D0%BA%D1%86%D0%B8%D0%B8-%D0%B2-spring-framework-a7ec509df6d2)
- <a href="https://dzone.com/articles/how-does-spring-transactional">How does Spring @Transactional Really Work</a>
- <a href="https://www.ibm.com/developerworks/ru/library/j-ts1/">Стратегии работы с транзакциями: распространенные ошибки</a>
- <a href="http://stackoverflow.com/questions/8490852/spring-transactional-isolation-propagation">Spring @Transactional - isolation, propagation</a>
-  <a href="https://docs.spring.io/spring/docs/current/spring-framework-reference/integration.html#cache">Spring cache Abstraction</a>
-  <a href="http://habrahabr.ru/post/25140/">Распределённая система кэша ehcache</a>
-  <a href="http://stackoverflow.com/questions/10013288/another-unnamed-cachemanager-already-exists-in-the-same-vm-ehcache-2-5">один кэш на JVM</a>
- <a href="http://docs.spring.io/spring-framework/docs/4.0.x/spring-framework-reference/html/transaction.html">Spring Framework transaction management</a>
- <a href="http://www.baeldung.com/persistence-with-spring-series/">Spring Persistence Tutorial</a>
- <a href="http://www.tutorialspoint.com/spring/spring_transaction_management.htm">Spring Transaction Management</a>

### Spring MVC

- <a class="anchor" id="mvc"></a><a href="https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html#mvc">Spring Web MVC</a>
- [ContextLoaderListener vs DispatcherServlet](https://howtodoinjava.com/spring-mvc/contextloaderlistener-vs-dispatcherservlet/)
-  <a href="http://design-pattern.ru/patterns/front-controller.html">Паттерн Front Controller</a>
-  <a href="https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html#mvc-servlet-context-hierarchy">Иерархия контекстов в Spring Web MVC</a>
-  <a href="http://www.tutorialspoint.com/spring/spring_web_mvc_framework.htm">Сценарий обработки запроса</a>. <a href="http://www.studytrails.com/frameworks/spring/spring-mvc.jsp">HandlerMappings</a>
-  <a href="https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html#mvc-viewresolver">View Resolution</a>: прячем jsp под WEB-INF.
-  HandlerMapping: <a href="http://www.mkyong.com/spring-mvc/spring-mvc-simpleurlhandlermapping-example/">SimpleUrlHandlerMapping</a>, <a href="http://www.mkyong.com/spring-mvc/spring-mvc-beannameurlhandlermapping-example/">BeanNameUrlHandlerMapping</a>
-  <a href="https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html#mvc-caching-static-resources">Маппинг ресурсов.</a>
-  Ресурсы:
-  <a href="http://www.mkyong.com/spring-mvc/spring-mvc-hello-world-example/">Spring MVC hello world</a>
-  <a href="https://docs.spring.io/spring/docs/current/spring-framework-reference/web.html#mvc-servlet-special-bean-types">Special bean types in the WebApplicationContext</a>

### Spring Security

-  <a href="http://projects.spring.io/spring-security/">Spring Security</a>
-  <a href="https://ru.wikipedia.org/wiki/Протокол_AAA">Протокол AAA</a>
-  <a href="https://ru.wikipedia.org/wiki/Аутентификация_в_Интернете">Методы аутентификации</a>.
-  <a href="https://en.wikipedia.org/wiki/Basic_access_authentication">Basic access authentication</a>
-  <a href="http://articles.javatalks.ru/articles/17">Использование ThreadLocal</a>
-  <a href="http://www.baeldung.com/security-spring">Security with Spring</a>
-  <a class="anchor" id="csrf"></a><a href="https://ru.wikipedia.org/wiki/Межсайтовая_подделка_запроса">Межсайтовая подделка запроса (CSRF)</a>
-  <a href="https://docs.spring.io/spring-security/site/docs/current/reference/html/web-app-security.html#csrf-using">Using Spring Security CSRF Protection</a>
-  <a href="https://docs.spring.io/spring-security/site/docs/current/reference/html/web-app-security.html#csrf-include-csrf-token-ajax">Ajax and JSON Requests</a>
-  <a href="http://blog.jdriven.com/2014/10/stateless-spring-security-part-1-stateless-csrf-protection/">Stateless CSRF protection</a>
-  <a href="http://habrahabr.ru/post/264641/">Spring Security 4 + CSRF</a>
-  <a href="http://stackoverflow.com/questions/11008469/are-json-web-services-vulnerable-to-csrf-attacks">Are JSON web services vulnerable to CSRF attacks</a>
-  <a href="https://ru.wikipedia.org/wiki/Правило_ограничения_домена">Правило ограничения домена (SOP)</a>
-  <a href="https://ru.wikipedia.org/wiki/Cross-origin_resource_sharing">Cross-origin resource sharing (C

