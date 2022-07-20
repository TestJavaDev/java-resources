---
layout: default
title: Java interview
nav_order: 8
permalink: /java_interview
has_children: true
---
<div align="center" markdown="1">
Java interview / Java resources / Grokking the interview

{: .fs-6 .fw-300 }
</div>

## Spring

### Spring Core

* [Spring Core in Spring Certification](https://mossgreen.github.io/Spring-Certification-Spring-Core/)
* [Spring изнутри. Этапы инициализации контекста / Хабр](https://habr.com/ru/post/222579/)
* [Injecting Spring Prototype bean into Singleton bean](http://dolszewski.com/spring/accessing-prototype-bean-in-singleton)
* [Spring: @Component versus @Bean](https://stackoverflow.com/questions/10604298/spring-component-versus-bean)
* [Difference between @Bean and @Component annotation in Spring.](https://www.tutorialspoint.com/difference-between-bean-and-component-annotation-in-spring#:~:text=It%20is%20used%20to%20explicitly,detect%20by%20using%20classpath%20scan.&text=We%20should%20use%20%40bean%2C%20if,implementation%20based%20on%20dynamic%20condition.)
* [Circular Dependencies in Spring](https://www.baeldung.com/circular-dependencies-in-spring)
* [Circular dependency in Spring](https://stackoverflow.com/questions/3485347/circular-dependency-in-spring)
* [BeanFactoryPostProcessor and BeanPostProcessor in lifecycle events](https://stackoverflow.com/questions/30455536/beanfactorypostprocessor-and-beanpostprocessor-in-lifecycle-events#:~:text=BeanFactoryPostProcessor%20implementations%20are%20%22called%22%20during,demand%20for%20the%20proptotypes%20one))
* [@PostConstruct annotation and spring lifecycle](https://stackoverflow.com/questions/44681142/postconstruct-annotation-and-spring-lifecycle)
* [Spring под капотом](https://medium.com/@kirill.sereda/spring-%D0%BF%D0%BE%D0%B4-%D0%BA%D0%B0%D0%BF%D0%BE%D1%82%D0%BE%D0%BC-9d92f2bf1a04)

### Spring AOP

* [Spring AOP in Spring Certification](https://mossgreen.github.io/Spring-Certification-Spring-AOP/)
* [Spring AOP. Маленький вопросик с собеседования / Хабр](https://habr.com/ru/post/347752/)

### Spring Data Management

* [Spring Data Management in Spring Certification](https://mossgreen.github.io/Spring-Certification-Spring-Data-Management/)
* [Spring Data – One API To Rule Them All](https://www.infoq.com/articles/spring-data-intro/)
* [Why should you use Unchecked exceptions over Checked exceptions in Java](https://www.javacodegeeks.com/2012/03/why-should-you-use-unchecked-exceptions.html)
* [Why does spring prefer unchecked exceptions?](https://stackoverflow.com/questions/52983402/why-does-spring-prefer-unchecked-exceptions)
* [Spring Transaction Management: @Transactional In-Depth](https://www.marcobehler.com/guides/spring-transaction-management-transactional-in-depth)
* [java - Spring @Transactional - isolation, propagation - Stack Overflow](https://stackoverflow.com/questions/8490852/spring-transactional-isolation-propagation)
* [Spring self injection for transactions](https://stackoverflow.com/questions/43280460/spring-self-injection-for-transactions/43282215)
* [@Transactional on @PostConstruct method](https://stackoverflow.com/questions/17346679/transactional-on-postconstruct-method)
* [What are advantages of using @Transactional(readOnly = true)?](https://stackoverflow.com/questions/44984781/what-are-advantages-of-using-transactionalreadonly-true)
* [Spring transaction and non-transaction methods call each other](https://blog.fearcat.in/a?ID=01700-718e2a5b-5ee2-45ab-8706-9cd87328989e)

### Spring Boot

* [Spring Boot in Spring Professional Certification](https://mossgreen.github.io/Spring-Certification-Spring-Boot/)
* [Introducing spring boot](https://topjava.ru/blog/introducing-spring-boot)
* [Spring Boot DevTools](https://habr.com/ru/post/479382/)
* [Spring Boot Actuator](https://habr.com/ru/company/otus/blog/452624/)
* [Spring Boot Starter](https://java-ru-blog.blogspot.com/2020/02/spring-boot-starters.html)
* [Spring Boot Auto-Configuration](https://habr.com/ru/post/487980/)

### Spring MVC

* [Spring MVC in Spring Professional Certification](https://mossgreen.github.io/Spring-Certification-Spring-MVC/)

### Spring Security

* [Spring Security in Spring Certification](https://mossgreen.github.io/Spring-Certification-Spring-Security/)
* [How Spring Security Filter Chain works](https://stackoverflow.com/questions/41480102/how-spring-security-filter-chain-works)
* [Difference between Role and GrantedAuthority in Spring Security](https://stackoverflow.com/questions/19525380/difference-between-role-and-grantedauthority-in-spring-security)

### Spring REST

* [Spring REST in Spring Certification](https://mossgreen.github.io/Spring-Certification-Spring-REST/)
* [Spring RestTemplate](https://mossgreen.github.io/Spring-RestTemplate/)
* [Spring RestTemplate Vs Jersey Rest Client Vs RestEasy Client](https://stackoverflow.com/questions/32337775/spring-resttemplate-vs-jersey-rest-client-vs-resteasy-client)
* [Declarative REST Client: Feign](https://cloud.spring.io/spring-cloud-static/spring-cloud-openfeign/2.1.5.RELEASE/multi/multi_spring-cloud-feign.html)
* [Spring WebClient vs. RestTemplate](https://www.baeldung.com/spring-webclient-resttemplate)

### Spring Testing

* [Spring Testing in Spring Certification](https://mossgreen.github.io/Spring-Certification-Testing/)
* [How to test Spring transactions](https://stackoverflow.com/questions/53380923/how-to-test-spring-transactions)

### Others

* [Евгений Борисов, Кирилл Толкачев — Boot yourself, Spring is coming](https://www.youtube.com/watch?v=yy43NOreJG4)
* [Микросервисная архитектура, Spring Cloud и Docker / Хабр](https://habr.com/ru/post/280786/)
* [Алексей Нестеров — Spring Cloud в эру Kubernetes - YouTube](https://www.youtube.com/watch?v=vUo3cTE3Y0g&t=2260s)
* [Spring Boot Starter](https://www.youtube.com/watch?v=2_iE7jZWl3U&list=WL&index=4&t=2465s)
* [Стратегии обработки ошибок: Circuit Breaker pattern](https://medium.com/@kirill.sereda/%D1%81%D1%82%D1%80%D0%B0%D1%82%D0%B5%D0%B3%D0%B8%D0%B8-%D0%BE%D0%B1%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%BA%D0%B8-%D0%BE%D1%88%D0%B8%D0%B1%D0%BE%D0%BA-circuit-breaker-pattern-650232944e37)
* [Spring Application Context Events](https://www.baeldung.com/spring-context-events)

## Multithreading

//TODO learn jobs from work project

* [Обзор java.util.concurrent.* / Хабр](https://habr.com/ru/company/luxoft/blog/157273/)
* [Справочник по синхронизаторам java.util.concurrent.*](https://habr.com/ru/post/277669/)

* [Monitor vs Mutex](https://stackoverflow.com/questions/38159668/monitor-vs-mutex)
* [В чем разница между мьютексом, монитором и семафором](https://javarush.ru/groups/posts/2174-v-chem-raznica-mezhdu-mjhjuteksom-monitorom-i-semaforom)
* [Semaphore vs. Monitors - what's the difference?](https://stackoverflow.com/questions/7335950/semaphore-vs-monitors-whats-the-difference)
* [The usage case of counting semaphore](https://stackoverflow.com/questions/26217282/the-usage-case-of-counting-semaphore)
* [What are the practical uses of semaphores?](https://stackoverflow.com/questions/21736741/what-are-the-practical-uses-of-semaphores)

* [How does multithreading work for a java Servlet? - Stack Overflow](https://stackoverflow.com/questions/7701772/how-does-multithreading-work-for-a-java-servlet)
* [Java Memory Model вкратце](http://www.javaspecialist.ru/2011/06/java-memory-model.html)
* [Java Memory Model](https://www.slideshare.net/buzdin/java-jmm2011v8)
* [Синхронизация потоков](http://www.skipy.ru/technics/synchronization.html)

## Message communication
* [point-to-point](www.enterpriseintegrationpatterns.com/PointToPointChannel.html) 
A point-to-point channel delivers a message to exactly one of the consumers that
is reading from the channel. Services use point-to-point channels for the oneto-one interaction styles described earlier. For example, a command message is
often sent over a point-to-point channel.(AWS SQS)
* [publish-subscribe](www.enterpriseintegrationpatterns.com/PublishSubscribeChannel.html)
* [Семантика exactly-once в Apache Kafka / Хабр](https://habr.com/ru/company/badoo/blog/333046/)
* [Handling duplicate SNS deliveries : aws](https://www.reddit.com/r/aws/comments/8u1b1v/handling_duplicate_sns_deliveries/)
* [Николай Алименков — Нужен ли нам JMS в мире современных Java-технологий? - YouTube](https://www.youtube.com/watch?v=ExjPxDxkmFo)
* [Producer Consumer Solution](https://www.geeksforgeeks.org/producer-consumer-solution-using-blockingqueue-in-java-thread/)

* [Implementing the Outbox Pattern](https://dzone.com/articles/implementing-the-outbox-pattern)

## DB

* [Вячеслав Круглов — Как начинающему Java-разработчику подружиться со своей базой данных? - YouTube](https://www.youtube.com/watch?v=dFASbaIG-UU)
* [Всё, что вы не знали о CAP теореме / Хабр](https://habr.com/ru/post/328792/)
* [concurrency - How are locking mechanisms (Pessimistic/Optimistic) related to database transaction isolation levels? - Stack Overflow](https://stackoverflow.com/questions/22646226/how-are-locking-mechanisms-pessimistic-optimistic-related-to-database-transact)
* [database - CAP theorem - Availability and Partition Tolerance - Stack Overflow](https://stackoverflow.com/questions/12346326/cap-theorem-availability-and-partition-tolerance)

## ORM

Hibernate save object - strategies, hibernate events, dirty checking, interceptors, N+1, entity lifecycle
* [Николай Алименков — Сделаем Hibernate снова быстрым - YouTube](https://www.youtube.com/watch?v=b52Qz6qlic0&t=24s)
* [Николай Алименков — Босиком по граблям Hibernate - YouTube](https://www.youtube.com/watch?v=YzOTZTt-PR0&t=136s)

## REST

* [Stateless vs. Stateful](https://medium.com/@ermakovichdmitriy/%D0%BE%D0%BF%D1%80%D0%B5%D0%B4%D0%B5%D0%BB%D0%B5%D0%BD%D0%B8%D1%8F-%D0%BF%D0%BE%D0%BD%D1%8F%D1%82%D0%B8%D0%B9-stateful-%D0%B8-stateless-%D0%B2-%D0%BA%D0%BE%D0%BD%D1%82%D0%B5%D0%BA%D1%81%D1%82%D0%B5-%D0%B2%D0%B5%D0%B1-%D1%81%D0%B5%D1%80%D0%B2%D0%B8%D1%81%D0%BE%D0%B2-%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4-18a910a226a1)
* [Manage sessions](https://stackoverflow.com/questions/3105296/if-rest-applications-are-supposed-to-be-stateless-how-do-you-manage-sessions)
* [Stateful vs Stateless Architecture](https://www.virtasant.com/blog/stateful-vs-stateless-architecture-why-stateless-won)
* [Idempotency in HTTP methods](https://stackoverflow.com/questions/45016234/what-is-idempotency-in-http-methods)

## Elasticsearch

* [Строим продвинутый поиск с ElasticSearch DOU](https://dou.ua/lenta/columns/building-advanced-search-with-elasticsearch/)
* [С чего начинается Elasticsearch / Хабр](https://habr.com/ru/post/489924/)
* [How Elasticsearch Search So Fast](https://medium.com/analytics-vidhya/how-elasticsearch-search-so-fast-248630b70ba4)

## Testing

* [Mock vs. Stub vs. Spy](https://www.javatpoint.com/mock-vs-stub-vs-spy)
* [Mocking vs. Spying](https://stackoverflow.com/questions/12827580/mocking-vs-spying-in-mocking-frameworks)
* [Difference between @Mock and @InjectMocks](https://stackoverflow.com/questions/16467685/difference-between-mock-and-injectmocks)

## Java 8 best practices

* [Николай Алименков — Java 8: Хороший, плохой, злой - YouTube](https://www.youtube.com/watch?v=7Iy1hVEXxsU)
* [xpinjection/java8-misuses: Common misuses of new Java 8 features and other mistakes](https://github.com/xpinjection/java8-misuses)
* [Тагир Валеев — Stream API: рекомендации лучших собаководов - YouTube](https://www.youtube.com/watch?v=vxikpWnnnCU)
* [Лямбда-выражения в Java 8 / Хабр](https://habr.com/ru/post/224593/)
* [Используйте Stream API проще (или не используйте вообще) / Хабр](https://habr.com/ru/post/337350/)
* [Шпаргалка Java программиста 4. Java Stream API / Хабр](https://habr.com/ru/company/luxoft/blog/270383/)
* [7 способов использовать groupingBy в Stream API / Хабр](https://habr.com/ru/post/348536/)
* [Java Stream API: что делает хорошо, а что не очень / Хабр](https://habr.com/ru/company/jugru/blog/307938/)
* [Перевод руководства по Stream API от Benjamin Winterberg / Хабр](https://habr.com/ru/post/437038/)

## Java Core

Metaspace, JVM tuning flags, memory leaks, GC algorithms
* [JVM: краткий курс общей анатомии](https://www.youtube.com/watch?v=-fcj6EL9rc4&list=WL&index=5&t=369s)
* [What is profiling?](https://stackoverflow.com/questions/619898/what-is-profiling)
* [ava Profilers: Why You Need These 3 Different Types](https://stackify.com/java-profilers-3-types/)
* [JVM Tutorial - Java Virtual Machine Architecture Explained for Beginners](https://www.freecodecamp.org/news/jvm-tutorial-java-virtual-machine-architecture-explained-for-beginners/)
* [Understanding JVM Architecture. Understanding JVM architecture Medium](https://medium.com/platform-engineer/understanding-jvm-architecture-22c0ddf09722)
* [Разрешение конфликтов в транзитивных зависимостях — Хороший, Плохой, Злой / Хабр](https://habr.com/ru/company/jugru/blog/191246/)
* [Java собеседование. Коллекции / Хабр](https://habr.com/ru/post/162017/)
* [Разбираемся с hashCode() и equals() / Хабр](https://habr.com/ru/post/168195/)
* [Java Memory Model вкратце](http://www.javaspecialist.ru/2011/06/java-memory-model.html)
* [Overriding vs Overloading](https://java-course.ru/begin/override-overload/)
* [Java Pass-by-reference or Pass-by-value](https://stackoverflow.com/questions/40480/is-java-pass-by-reference-or-pass-by-value)
* [Serialization in Java](https://stackoverflow.com/questions/2232759/what-is-the-purpose-of-serialization-in-java)
* [Association, aggregation and composition](https://stackoverflow.com/questions/885937/what-is-the-difference-between-association-aggregation-and-composition)
* [Aggregation versus Composition](https://stackoverflow.com/questions/734891/aggregation-versus-composition)
* [Аннотации в JAVA](https://habr.com/ru/post/139736/)
