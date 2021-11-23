---
layout: default
title: Database
nav_order: 9
permalink: /db
has_children: true
---
<div align="center" markdown="1">
Database / Java resources / Grokking the interview

{: .fs-6 .fw-300 }
</div>

### Database
{: .label }

* Transactions and Concurrency Control
  * ACID  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Phenomena  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * Dirty Write,  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * Dirty Read,  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * Non-Repeatable Read,  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * Phantom Read,  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * Read Skew,  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * Write Skew,  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * Lost Update  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * 2PL (Two-Phase Locking)  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * MVCC (Multi-Version Concurrency Control)  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Isolation levels and database concurrency control  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Logical vs. physical clock optimistic locking:  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * OPTIMISTIC,  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * OPTIMISTIC FORCE INCREMENT,  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * PESSIMISTIC FORCE INCREMENT,  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * PESSIMISTIC READ,  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
    * PESSIMISTIC WRITE  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Versionless optimistic locking  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * JPA physical and optimistic lock types  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Skip locked and queuing access  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  * Preventing lost updates in long conversations  [first site]() [second site]() [third site]() [fourth site]() [fifth site]()
  
* Database, Application and Hibernate Caching  
  * Database caching  [first site](https://stackoverflow.com/questions/12227752/what-is-a-database-cache-and-how-does-one-use-it) [second site](https://blog.bluzelle.com/things-you-should-know-about-database-caching-2e8451656c2d)
  * Application-level caching  [first site](https://dzone.com/articles/introducing-amp-assimilating-caching-quick-read-fo) [second site](https://vladmihalcea.com/things-to-consider-before-jumping-to-enterprise-caching/)
  * Cache synchronization strategies  [first site](https://vladmihalcea.com/a-beginners-guide-to-cache-synchronization-strategies/) [second site](https://stackoverflow.com/questions/40759479/how-to-keep-the-cache-in-sync-with-the-database)
  * Cache concurrency strategies  [first site](https://habr.com/ru/post/268747/)  [second side](https://stackoverflow.com/questions/1837651/hibernate-cache-strategy)
    * READ ONLY,  [first site](https://vladmihalcea.com/how-does-hibernate-read_only-cacheconcurrencystrategy-work/)
    * NONSTRICT READ WRITE,  [first site](https://vladmihalcea.com/how-does-hibernate-read_write-cacheconcurrencystrategy-work/) [second site](https://stackoverflow.com/questions/8662609/hibernate-l2-cache-read-write-or-transactional-cache-concurrency-strategy-on-cl)
    * READ WRITE,  [first site](https://stackoverflow.com/questions/1837651/hibernate-cache-strategy)
    * TRANSACTIONAL  [first site](https://vladmihalcea.com/how-does-hibernate-transactional-cacheconcurrencystrategy-work/)
  * Collection Cache  [first site](https://stackoverflow.com/questions/14080735/hibernate-collection-cache-how-to-use)
  * Query Cache  [first site](https://vladmihalcea.com/hibernate-query-cache-n-plus-1-issue/)

- <a href="https://docs.google.com/document/d/1ul1jH7sccyQVqpjItdFo_OQI9YxJV3V5hxqI7xa-YPM">DB Migration rules</a>
- [Опыт 1440 миграций баз данных](https://habr.com/company/wrike/blog/414441/)
-  [BoneCP to be deprecated ](https://stackoverflow.com/a/1662916/548473)
-  Выбор реализации пула коннектов: <a href="https://commons.apache.org/proper/commons-dbcp/">Commons Database Connection Pooling</a>, <a href="https://github.com/brettwooldridge/HikariCP">HikariCP</a>
-  <a href="https://habrahabr.ru/post/269023/">Самый быстрый пул соединений на java (читаем комменты)</a>
-  <a href="http://blog.ippon.fr/2013/03/13/improving-the-performance-of-the-spring-petclinic-sample-application-part-3-of-5">Tomcat pool</a>
- [Оптимизация запросов. Основы EXPLAIN в PostgreSQL](https://habrahabr.ru/post/203320/)
- [Оптимизация запросов. Часть 2](https://habrahabr.ru/post/203386/)
- [Оптимизация запросов. Часть 3](https://habrahabr.ru/post/203484/)
- [Документация Postgres: индексы](https://postgrespro.ru/docs/postgresql/9.6/indexes.html)
- [Стратегии работы с транзакциями, pаспространенные ошибки](https://www.ibm.com/developerworks/ru/library/j-ts1/index.html)
- <a href="https://ru.wikipedia.org/wiki/Транзакция_(информатика)">wiki Транзакция</a>
- <a href="https://jira.spring.io/browse/DATAJPA-601">readOnly и Propagation.SUPPORTS</a>
- <a href="http://www.ibm.com/developerworks/ru/library/j-ts1/">Стратегии работы с транзакциями: Распространенные ошибки</a>
- <a href="http://habrahabr.ru/post/208400/">Принципы работы СУБД. MVCC</a>
- <a href="https://ru.wikipedia.org/wiki/MVCC">MVCC</a>
- <a href="http://ru.wikipedia.org/wiki/Транзакция_(информатика)">Транзакция. ACID. Уровни изоляции транзакций.</a>
- <a href="https://www.ibm.com/developerworks/ru/library/j-ts2/">Стратегии работы с транзакциями</a>
- [DB-Engines Ranking](http://db-engines.com/en/ranking)
- [Реляционная СУБД](https://ru.wikipedia.org/wiki/Реляционная_СУБД) (wiki)
- [Введение в базы данных](http://www.codenet.ru/progr/vbasic/vb_db/1.php)
- [Реляционные базы vs NoSQL](http://habrahabr.ru/post/103021). SQL. Денормализация. PK, FK, Cascade
- [PostgreSQL: надёжность](https://ru.wikipedia.org/wiki/PostgreSQL#Качество_исходного_кода)
- [Работа с базами данных из IDEA](https://habrahabr.ru/company/JetBrains/blog/204064)
- [IDEA Database tools](https://www.jetbrains.com/datagrip/features)
- [Как работает реляционная БД](https://habrahabr.ru/company/mailru/blog/266811)
- [SQL ключи во всех подробностях](https://habrahabr.ru/company/oleg-bunin/blog/348172)
- [Книги по postgreSQL](https://postgrespro.ru/education/books)
- [Интерактивная обучалка по postgreSQL](https://www.pgexercises.com/)
- <a href="http://ru.wikipedia.org/wiki/Транзакция_(информатика)">Транзакция. ACID.</a> <a href="https://ru.wikipedia.org/wiki/Уровень_изолированности_транзакций">Уровни изоляции транзакций.</a>
- <a href="http://www.osp.ru/pcworld/2009/07/9708191/">Уровни изоляции транзакций в SQL</a>
- <a href="https://habr.com/ru/post/120003/">БД Oracle для программиста</a>

### Database Performance Tuning
{: .label }

*  Common Performance Problems and Their Solutions
*  Database-related problems;
*  JVM performance problems;
*  Application specific performance problems;
*  Network-related problems.

### Blog
{: .label }

- [Vlad Mihalcea High-Performance Java Persistence Book ](https://vladmihalcea.com/books/high-performance-java-persistence/)
- [The best Tutorials on High-Performance Hibernate](https://vladmihalcea.com/tutorials/hibernate/)

### Video
{: .label }

- <a href="https://www.youtube.com/watch?v=dFASbaIG-UU">Видео: Вячеслав Круглов — Как начинающему Java-разработчику подружиться со своей базой данных?</a>








