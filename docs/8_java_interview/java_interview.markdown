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

* [Spring изнутри. Этапы инициализации контекста](https://habr.com/ru/post/222579/)
* [Injecting Spring Prototype bean into Singleton bean ](http://dolszewski.com/spring/accessing-prototype-bean-in-singleton)
* [How Does Spring @Transactional Really Work](https://dzone.com/articles/how-does-spring-transactional)
* [java - Spring @Transactional - isolation, propagation](https://stackoverflow.com/questions/8490852/spring-transactional-isolation-propagation)
* [Микросервисная архитектура, Spring Cloud и Docker](https://habr.com/ru/post/280786/)
* [Spring Transaction Management: @Transactional In-Depth](https://www.marcobehler.com/guides/spring-transaction-management-transactional-in-depth)
* [Spring AOP. Маленький вопросик с собеседования](https://habr.com/ru/post/347752/)
* [Алексей Нестеров — Spring Cloud в эру Kubernetes](https://www.youtube.com/watch?v=vUo3cTE3Y0g&t=2260s)
* [Spring Boot Starter](https://www.youtube.com/watch?v=2_iE7jZWl3U&list=WL&index=4&t=2465s)
* [Стратегии обработки ошибок: Circuit Breaker pattern | by Kirill Sereda](https://medium.com/@kirill.sereda/%D1%81%D1%82%D1%80%D0%B0%D1%82%D0%B5%D0%B3%D0%B8%D0%B8-%D0%BE%D0%B1%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%BA%D0%B8-%D0%BE%D1%88%D0%B8%D0%B1%D0%BE%D0%BA-circuit-breaker-pattern-650232944e37)

## Message communication
* [point-to-point](www.enterpriseintegrationpatterns.com/PointToPointChannel.html) 
A point-to-point channel delivers a message to exactly one of the consumers that
is reading from the channel. Services use point-to-point channels for the oneto-one interaction styles described earlier. For example, a command message is
often sent over a point-to-point channel.(AWS SQS)
* [publish-subscribe](www.enterpriseintegrationpatterns.com/PublishSubscribeChannel.html)
* [Семантика exactly-once в Apache Kafka](https://habr.com/ru/company/badoo/blog/333046/)
* [Handling duplicate SNS deliveries : aws](https://www.reddit.com/r/aws/comments/8u1b1v/handling_duplicate_sns_deliveries/)
* [Николай Алименков — Нужен ли нам JMS в мире современных Java-технологий](https://www.youtube.com/watch?v=ExjPxDxkmFo)

## DB

* [Вячеслав Круглов — Как начинающему Java-разработчику подружиться со своей базой данных](https://www.youtube.com/watch?v=dFASbaIG-UU)
* [Всё, что вы не знали о CAP теореме / Хабр](https://habr.com/ru/post/328792/)
* [concurrency - How are locking mechanisms (Pessimistic/Optimistic) related to database transaction isolation levels](https://stackoverflow.com/questions/22646226/how-are-locking-mechanisms-pessimistic-optimistic-related-to-database-transact)
* [database - CAP theorem - Availability and Partition Tolerance](https://stackoverflow.com/questions/12346326/cap-theorem-availability-and-partition-tolerance)

## ORM

Hibernate save object - strategies, hibernate events, dirty checking, interceptors, N+1, entity lifecycle
* [Николай Алименков — Сделаем Hibernate снова быстрым](https://www.youtube.com/watch?v=b52Qz6qlic0&t=24s)
* [Николай Алименков — Босиком по граблям Hibernate](https://www.youtube.com/watch?v=YzOTZTt-PR0&t=136s)

## REST

* [Stateless vs. Stateful](https://medium.com/@ermakovichdmitriy/%D0%BE%D0%BF%D1%80%D0%B5%D0%B4%D0%B5%D0%BB%D0%B5%D0%BD%D0%B8%D1%8F-%D0%BF%D0%BE%D0%BD%D1%8F%D1%82%D0%B8%D0%B9-stateful-%D0%B8-stateless-%D0%B2-%D0%BA%D0%BE%D0%BD%D1%82%D0%B5%D0%BA%D1%81%D1%82%D0%B5-%D0%B2%D0%B5%D0%B1-%D1%81%D0%B5%D1%80%D0%B2%D0%B8%D1%81%D0%BE%D0%B2-%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4-18a910a226a1)
* [Manage sessions](https://stackoverflow.com/questions/3105296/if-rest-applications-are-supposed-to-be-stateless-how-do-you-manage-sessions)
* [Stateful vs Stateless Architecture](https://www.virtasant.com/blog/stateful-vs-stateless-architecture-why-stateless-won)
* [Idempotency in HTTP methods](https://stackoverflow.com/questions/45016234/what-is-idempotency-in-http-methods)

## Elasticsearch

* [Строим продвинутый поиск с ElasticSearch](https://dou.ua/lenta/columns/building-advanced-search-with-elasticsearch/)
* [С чего начинается Elasticsearch](https://habr.com/ru/post/489924/)

## Multithreading

* [How does multithreading work for a java Servlet](https://stackoverflow.com/questions/7701772/how-does-multithreading-work-for-a-java-servlet)
* [Обзор java.util.concurrent](https://habr.com/ru/company/luxoft/blog/157273/)

## Testing

* [Mock vs. Stub vs. Spy](https://www.javatpoint.com/mock-vs-stub-vs-spy)
* [Mocking vs. Spying](https://stackoverflow.com/questions/12827580/mocking-vs-spying-in-mocking-frameworks)
* [Difference between @Mock and @InjectMocks](https://stackoverflow.com/questions/16467685/difference-between-mock-and-injectmocks)

## Java 8 best practices

* [Николай Алименков — Java 8: Хороший, плохой, злой](https://www.youtube.com/watch?v=7Iy1hVEXxsU)
* [xpinjection/java8-misuses: Common misuses of new Java 8 features and other mistakes](https://github.com/xpinjection/java8-misuses)
* [Тагир Валеев — Stream API: рекомендации лучших собаководов](https://www.youtube.com/watch?v=vxikpWnnnCU)
* [Лямбда-выражения в Java 8](https://habr.com/ru/post/224593/)
* [Используйте Stream API проще (или не используйте вообще)](https://habr.com/ru/post/337350/)
* [Шпаргалка Java программиста 4. Java Stream API](https://habr.com/ru/company/luxoft/blog/270383/)
* [7 способов использовать groupingBy в Stream API](https://habr.com/ru/post/348536/)
* [Java Stream API: что делает хорошо, а что не очень](https://habr.com/ru/company/jugru/blog/307938/)
* [Перевод руководства по Stream API от Benjamin Winterberg](https://habr.com/ru/post/437038/)

## Java Core

Metaspace, JVM tuning flags, memory leaks, GC algorithms
* [JVM: краткий курс общей анатомии](https://www.youtube.com/watch?v=-fcj6EL9rc4&list=WL&index=5&t=369s)
* [JVM Tutorial - Java Virtual Machine Architecture Explained for Beginners](https://www.freecodecamp.org/news/jvm-tutorial-java-virtual-machine-architecture-explained-for-beginners/)
* [Understanding JVM Architecture. Understanding JVM architecture](https://medium.com/platform-engineer/understanding-jvm-architecture-22c0ddf09722)
* [Разрешение конфликтов в транзитивных зависимостях — Хороший, Плохой, Злой](https://habr.com/ru/company/jugru/blog/191246/)
* [Java собеседование. Коллекции](https://habr.com/ru/post/162017/)
* [Разбираемся с hashCode и equals](https://habr.com/ru/post/168195/)
* [Java Memory Model](http://www.javaspecialist.ru/2011/06/java-memory-model.html)
* [Overriding vs Overloading](https://java-course.ru/begin/override-overload/)
* [Java Pass by reference or Pass by value](https://stackoverflow.com/questions/40480/is-java-pass-by-reference-or-pass-by-value)
* [Serialization in Java](https://stackoverflow.com/questions/2232759/what-is-the-purpose-of-serialization-in-java)
* [Association, aggregation and composition](https://stackoverflow.com/questions/885937/what-is-the-difference-between-association-aggregation-and-composition)
* [Aggregation versus Composition](https://stackoverflow.com/questions/734891/aggregation-versus-composition)
* [Аннотации в JAVA](https://habr.com/ru/post/139736/)
