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

Java Core
Serialization, 
Impl HTTP cashing on the server/client side
Method signature, all references are the same size, static variable, ( numeric promotion rules )
Method declaration, passing data among methods, 
THis mean that a copy of the variable is made and the method receives that copy
pass by value   pass by reference
overriding a method
overloaded method will use a differente signature than an overriden method
hiding static method
final methods cannot be ovveriden
default methods - backward compatibility
checked unchecked expetions
has a relationship

( Blocked queue)
composition, aggregation, is-a, has-a
Zookeeper
Metaspace, JVM tuning flags, memory leaks, GC algorithms
JDBC statement - prepared statement- callable statement
Hibernate save object - strategies, hibernate events, dirty checking, interceptors, N+1, entity lifecycle
Cronjoba Bintime (Spy Mock) proxy-transactional денормалізація 2 методи транзакція Select N+1 RDS
Синхронна і Асинхроннна комунікація Stage по CI/CD
плюси і мінуси асинхронної комунікації
Retention annotations 
Proxy Маршрутизація JWT Cookfiles
Statefull OWASP Життєвий цикл бінів  скоуп бінів рівні ізоляції  PostProces | Inject prototype в Singleton 
Proxy Pattern Strategy  



* [xpinjection/java8-misuses: Common misuses of new Java 8 features and other mistakes](https://github.com/xpinjection/java8-misuses)
* [Николай Алименков — Java 8: Хороший, плохой, злой - YouTube](https://www.youtube.com/watch?v=7Iy1hVEXxsU)
* [Тагир Валеев — Stream API: рекомендации лучших собаководов - YouTube](https://www.youtube.com/watch?v=vxikpWnnnCU)
* [Лямбда-выражения в Java 8 / Хабр](https://habr.com/ru/post/224593/)
* [Используйте Stream API проще (или не используйте вообще) / Хабр](https://habr.com/ru/post/337350/)
* [Шпаргалка Java программиста 4. Java Stream API / Хабр](https://habr.com/ru/company/luxoft/blog/270383/)
* [7 способов использовать groupingBy в Stream API / Хабр](https://habr.com/ru/post/348536/)
* [Java Stream API: что делает хорошо, а что не очень / Хабр](https://habr.com/ru/company/jugru/blog/307938/)
* [Перевод руководства по Stream API от Benjamin Winterberg / Хабр](https://habr.com/ru/post/437038/)
* [JVM Tutorial - Java Virtual Machine Architecture Explained for Beginners](https://www.freecodecamp.org/news/jvm-tutorial-java-virtual-machine-architecture-explained-for-beginners/)
* [Understanding JVM Architecture. Understanding JVM architecture and how… | by Thilina Ashen Gamage | Platform Engineer | Medium](https://medium.com/platform-engineer/understanding-jvm-architecture-22c0ddf09722)
* [Разрешение конфликтов в транзитивных зависимостях — Хороший, Плохой, Злой / Хабр](https://habr.com/ru/company/jugru/blog/191246/)
* [Java собеседование. Коллекции / Хабр](https://habr.com/ru/post/162017/)
* [Разбираемся с hashCode() и equals() / Хабр](https://habr.com/ru/post/168195/)
* [Java Memory Model вкратце | Java Specialist](http://www.javaspecialist.ru/2011/06/java-memory-model.html)

* [Spring изнутри. Этапы инициализации контекста / Хабр](https://habr.com/ru/post/222579/)
* [Injecting Spring Prototype bean into Singleton bean | Dev in Web](http://dolszewski.com/spring/accessing-prototype-bean-in-singleton)
* [How Does Spring @Transactional Really Work? - DZone Integration](https://dzone.com/articles/how-does-spring-transactional)
* [java - Spring @Transactional - isolation, propagation - Stack Overflow](https://stackoverflow.com/questions/8490852/spring-transactional-isolation-propagation)
* [Микросервисная архитектура, Spring Cloud и Docker / Хабр](https://habr.com/ru/post/280786/)
* [Spring Transaction Management: @Transactional In-Depth](https://www.marcobehler.com/guides/spring-transaction-management-transactional-in-depth)
* [Spring AOP. Маленький вопросик с собеседования / Хабр](https://habr.com/ru/post/347752/)
* [Семантика exactly-once в Apache Kafka / Хабр](https://habr.com/ru/company/badoo/blog/333046/)
* [Handling duplicate SNS deliveries : aws](https://www.reddit.com/r/aws/comments/8u1b1v/handling_duplicate_sns_deliveries/)
* [Николай Алименков — Сделаем Hibernate снова быстрым - YouTube](https://www.youtube.com/watch?v=b52Qz6qlic0&t=24s)
* [Николай Алименков — Босиком по граблям Hibernate - YouTube](https://www.youtube.com/watch?v=YzOTZTt-PR0&t=136s)
* [Вячеслав Круглов — Как начинающему Java-разработчику подружиться со своей базой данных? - YouTube](https://www.youtube.com/watch?v=dFASbaIG-UU)
* [Николай Алименков — Нужен ли нам JMS в мире современных Java-технологий? - YouTube](https://www.youtube.com/watch?v=ExjPxDxkmFo)
* [Строим продвинутый поиск с ElasticSearch | DOU](https://dou.ua/lenta/columns/building-advanced-search-with-elasticsearch/)
* [Алексей Нестеров — Spring Cloud в эру Kubernetes - YouTube](https://www.youtube.com/watch?v=vUo3cTE3Y0g&t=2260s)
* [С чего начинается Elasticsearch / Хабр](https://habr.com/ru/post/489924/)
* [How does multithreading work for a java Servlet? - Stack Overflow](https://stackoverflow.com/questions/7701772/how-does-multithreading-work-for-a-java-servlet)
* [concurrency - How are locking mechanisms (Pessimistic/Optimistic) related to database transaction isolation levels? - Stack Overflow](https://stackoverflow.com/questions/22646226/how-are-locking-mechanisms-pessimistic-optimistic-related-to-database-transact)
* [database - CAP theorem - Availability and Partition Tolerance - Stack Overflow](https://stackoverflow.com/questions/12346326/cap-theorem-availability-and-partition-tolerance)
* [Обзор java.util.concurrent.* / Хабр](https://habr.com/ru/company/luxoft/blog/157273/)
* [Всё, что вы не знали о CAP теореме / Хабр](https://habr.com/ru/post/328792/)
* [Стратегии обработки ошибок: Circuit Breaker pattern | by Kirill Sereda | Medium](https://medium.com/@kirill.sereda/%D1%81%D1%82%D1%80%D0%B0%D1%82%D0%B5%D0%B3%D0%B8%D0%B8-%D0%BE%D0%B1%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%BA%D0%B8-%D0%BE%D1%88%D0%B8%D0%B1%D0%BE%D0%BA-circuit-breaker-pattern-650232944e37)













