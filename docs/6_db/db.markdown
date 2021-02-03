---
layout: default
title: DB, JDBC, ORM
nav_order: 6
permalink: /db_jdbc_orm
has_children: true
---
<div align="center" markdown="1">
DB, JDBC, ORM / Java resources / Grokking the interview

{: .fs-6 .fw-300 }
</div>

### JDBC
{: .label }

* Intro
  * Install MySQL RDBMS + MySQL Workbench
  * RDBMS vs DB, create database
  * JDBC architecture: JDBC API + JDBC Driver
  * JDBC Driver types, transport types
  * Connector/J: JDBC Driver to MySQL
  * JDBC / SQL versions, SQL dialects
* Connect to database
  * Driver, DriverManager, DataSource
  * Connection
  * JDBC URL
  * Connector/J properties
* Query database
  * DDL and DML (TEXT)
  * Statement
  * Statement.executeUpdate: INSERT, UPDATE, DELETE
  * Get auto-generated keys
  * Statement.executeQuery: SELECT, ResultSet
  * Statement.execute
  * SQLWarning
  * SQLException: errorCode and errorState
  * DAO Pattern
  * Альтернатива DAO: Transaction Script, Active Record, ORM // шаблон DAO (cуть шаблона, generic-предок, рекурсивное объединение)
* ResultSet
  * ResultSet: positioning and transition
  * ResultSet: type
  * ResultSet: concurrency
  * ResultSet: holdability
* Optimizations
  * PreparedStatement = + precompilation — SQL injection
  * Batch update = vectorization
  * Connection pooling
* Transactions
  * Transaction manager
  * ACID properties
  * Transaction boundaries
  * SQLTransientException
  * Savepoints //Connection.commit()/.rollback()/.setAutoCommit(), savepoint
  * Transaction isolation levels
  * MySQL transactions: MyISAM vs InnoDB
  * READ UNCOMMITED, Dirty Read “phenomena”
  * READ COMMITED, NonRepeatable Read “phenomena”
  * REPEATABLE READ, Phantom Read “phenomena”
  * SERIALIZABLE
  
* Local Tx-Manager: by-hands
  * Base realization: ThreadLocal Tx-context
  * @Transactional annotation
  * AOP realization of @Transactional
  * Application server = Tx-context + Auth-context + Thread management
* Distributed Transactions
  * 2PC-protocol
  * javax.jdbc.xa.* — XA-standart realization of 2PC-client
  * Distribured-Tx Manager Architecture
*  Query Meta-Information
  * Database meta-info
  * Table meta-info
  * Row meta-info

### ORM

* Introduction
  * O/R Mismatch
  * JPA vs. Hibernate
  * Logging SQL Statements 
  * Schema Management 
* Connection Management
  * Connection Management and Hibernate Connection Providers
  * Hibernate Connection Lifecycle
  * Connection Monitoring
  * Hibernate Statistics
* Types and Identifiers
  * JPA and Hibernate Types
  * Custom Hibernate Types
  * The hibernate-types project
  * JPA and Hibernate Identifiers
  * Hibernate Identifier Optimizers (e.g. hilo, pooled, pooled-lo)
* Relationships
  * JPA and Hibernate Relationships
  * Equals and Hashcode
  * ManyToOne
  * OneToMany
  * OneToOne
  * ManyToMany
  
* Inheritance
  * JPA Inheritance Basics
  * Single Table Inheritance 
  * Discriminator Column
  * Joined Inheritance
  * TablePerClass Inheritance
* Persistence Context
  * Persistence Context and Flushing Basics
  * Action Queue
  * The AUTO FlushModeType
  * Dirty Checking Mechanism
  * Bytecode Enhancement Dirty Checking
* Batching and Statement Caching
  * Statement Lifecycle and Execution Plans
  * Statement Caching
  * Statement Batching and Cascade Operations
  * Batching Update Operations
  * SQL Injection
* Fetching
  * Direct and Natural id fetching
  * DTO projections vs Entity queries
  * LAZY vs. EAGER
  * Query-time fetching
  * Pagination queries
  
* Transactions and Concurrency Control
  * ACID
  * Phenomena
    * Dirty Write,
    * Dirty Read,
    * Non-Repeatable Read,
    * Phantom Read,
    * Read Skew,
    * Write Skew,
    * Lost Update
  * 2PL (Two-Phase Locking)
  * MVCC (Multi-Version Concurrency Control)
  * Isolation levels and database concurrency control
  * Logical vs. physical clock optimistic locking:
    * OPTIMISTIC,
    * OPTIMISTIC FORCE INCREMENT,
    * PESSIMISTIC FORCE INCREMENT,
    * PESSIMISTIC READ,
    * PESSIMISTIC WRITE
  * Versionless optimistic locking
  * JPA physical and optimistic lock types
  * Skip locked and queuing access
  * Preventing lost updates in long conversations
  
* Database, Application and Hibernate Caching
  * Database caching
  * Application-level caching
  * Second-level caching
  * Cache synchronization strategies
  * Cache concurrency strategies
    * READ ONLY,
    * NONSTRICT READ WRITE,
    * READ WRITE,
    * TRANSACTIONAL
  * Collection Cache
  * Query Cache


- <a href="https://dou.ua/lenta/articles/hibernate-fetch-types/">Стратегии загрузки коллекций в Hibernate</a>
- <a href="https://en.wikipedia.org/wiki/Entity%E2%80%93relationship_model">Entity</a>- класс (объект Java), который в ORM маппится в таблицу DB.
-  <a href="http://ru.wikipedia.org/wiki/ORM">ORM</a>.
-  <a href="http://habrahabr.ru/post/265061/">JPA и Hibernate в вопросах и ответах</a>
- [Hibernate — о чем молчат туториалы](https://habr.com/ru/post/416851/)
-  <a href="http://docs.jboss.org/hibernate/orm/4.2/devguide/en-US/html/ch11.html">HQL</a>
- [Наследование в Hibernate: выбор стратегии](https://habrahabr.ru/post/337488/)
- [Field vs property access](http://stackoverflow.com/a/6084701/548473)
- <a href="http://www.quizful.net/post/Hibernate-3-introduction-and-writing-hello-world-application">Hibernate: введение и написания Hello world приложения</a>
- [15 reasons why we need to choose Hibernate over JDBC](https://habiletechnologies.com/blog/reasons-to-choose-hibernate-over-jdbc)
-  <a href="http://en.wikibooks.org/wiki/Java_Persistence/Mapping">Mapping: описания модели Hibernate (hbm.xml/annotation)</a>.
-  <a href="https://ru.wikipedia.org/wiki/Hibernate_(библиотека)">Hibernate</a>
- <a href="http://en.wikipedia.org/wiki/TopLink">TopLink</a>
- <a href="http://en.wikipedia.org/wiki/EclipseLink">EсlipseLink</a>, 
- <a href="http://en.wikipedia.org/wiki/Ebean">EBean</a> (<a href="http://www.playframework.com/documentation/2.2.x/JavaEbean">used in Playframework</a>).
- <a href="http://validator.hibernate.org">hibernate-validator</a>
- <a href="https://ru.wikipedia.org/wiki/ORM">ORM</a> это технология связывания БД и объектов приложения, <a href="https://ru.wikipedia.org/wiki/Java_Persistence_API">JPA</a> - это JavaEE спецификация (API) этой технологии.
Реализации JPA - Hibernate, OpenJPA, EclipceLink, но, например, Hibernate может работать по собственному API (без JPA, которая появилась позже). Spring-JDBC, MyBatis, JDBI не реализуют JPA, это обертки к JDBC. Все ORM и JPA также реализованы поверх JDBC.
- <a href="http://stackoverflow.com/questions/8994864/how-would-i-specify-a-hibernate-pattern-annotation-using-a-regular-expression">Validate by RegExp</a>
- <a href="http://stackoverflow.com/questions/13027214">Do not use `CascadeType` for @ManyToOne</a>
- <a href="http://stackoverflow.com/questions/836569">CascadeType meaning</a>
- <a href="https://en.wikibooks.org/wiki/Java_Persistence/ElementCollection">No cascade option on an ElementCollection, the target objects are always persisted, merged, removed with their parent.</a>
- <a href="http://stackoverflow.com/questions/21149660">Create ON DELETE CASCADE: `@OnDelete`</a>
- <a href="http://stackoverflow.com/questions/3087040">Hibernate second level cache and ON DELETE CASCADE in database schema</a>
- [`orphanRemoval=true` vs `CascadeType.REMOVE`](http://stackoverflow.com/a/19645397/548473)
- [JPA `cascade/orphanRemoval` doesn't work with `NamedQuery`](http://stackoverflow.com/questions/7825484/jpa-delete-where-does-not-delete-children-and-throws-an-exception)
-  <a href="http://habrahabr.ru/post/135176/">Уровни кэширования Hibernate</a>
-  <a href="http://habrahabr.ru/post/136375/">Hibernate Cache. Практика</a>
-  <a href="http://www.tutorialspoint.com/hibernate/hibernate_caching.htm">Hibernate - Caching</a>
-  Починка тестов: <a href="http://stackoverflow.com/questions/1603846/hibernate-2nd-level-cache-invalidation-when-another-process-modifies-the-databas">инвалидация кэша Hibernate</a>
-  [Hibernate User Guide: Caching](http://docs.jboss.org/hibernate/orm/5.2/userguide/html_single/Hibernate_User_Guide.html#caching)
-  [Hibernate 5, Ehcache 3.x](https://www.boraji.com/index.php/hibernate-5-jcache-ehcache-3-configuration-example)
-  Ресурсы:
- <a href="https://www.youtube.com/watch?list=PLYj3Bx1JM6Y7BKivc3eZwRUhWwBmbIFXg&v=V-ljsrVy6pE">Hibernate performance tuning (Mikalai Alimenkou /Igor Dmitriev)</a>
-  <a href="http://stackoverflow.com/questions/3663979/how-to-use-jpa2s-cacheable-instead-of-hibernates-cache">JPA2 @Cacheable vs Hibernate @Cache</a>
-  <a href="http://vladmihalcea.com/2015/06/08/how-does-hibernate-query-cache-work/">How does Hibernate Query Cache work</a>
-  <a href="https://www.javacodegeeks.com/2014/06/pitfalls-of-the-hibernate-second-level-query-caches.html">Pitfalls of the Hibernate Second-Level / Query Caches</a>
- <a href="http://articles.javatalks.ru/articles/17">Использование ThreadLocal переменных</a>
- <a href="http://stackoverflow.com/questions/1069992/jpa-entitymanager-why-use-persist-over-merge">Merge vs Persist</a>
- <a href="https://developer.jboss.org/wiki/OpenSessionInView">Паттерн "открытие транзакции в фильтре"</a> и <a href="http://stackoverflow.com/questions/1103363/why-is-hibernate-open-session-in-view-considered-a-bad-practice">почему это bad-practice</a>
- <a href="https://en.wikibooks.org/wiki/Java_Persistence/Identity_and_Sequencing#Sequence_Strategies">Sequence Strategies</a>
- <a href="http://stackoverflow.com/questions/9470442/why-is-the-hibernate-default-generator-for-postgresql-sequencegenerator-not?lq=1">SequenceGenerator/IdentityGenerator in PostgreSql</a>
- <a href="http://stackoverflow.com/questions/7793395">hbm2ddl.auto and autoincrement</a>
- <a href="http://stackoverflow.com/questions/2585641">Hibernate/JPA DB Schema Generation Best Practices</a>


### DB
{: .label }

* Реляционные базы данных (MySQL)
  * Устанавливаем, администрируем
  * Физическая организация данных
  * реляционная алгебра, реляционное исчисление
  * SQL types, CREATE/ALTER/DELETE table
* Логическое проектирование
  * ER-моделирование
  * Нормальные формы, денормализация
  * Целостность данных
  * Транзакции
* Физическое проектирование
  * Индексы
  * Блокировки
* Документно-ориентированные (MongoDB)
  * архитектура и особенности MongoDB
  * работаем с MongoDB на Java
* Key-value хранилища (Riak)
  * архитектура и особенности Riak
  * работаем с Riak на Java
  
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

### Blog
{: .label }

- [Vlad Mihalcea High-Performance Java Persistence Book ](https://vladmihalcea.com/books/high-performance-java-persistence/)
- [The best Tutorials on High-Performance Hibernate](https://vladmihalcea.com/tutorials/hibernate/)

### Video
{: .label }

- <a href="https://www.youtube.com/watch?v=dFASbaIG-UU">Видео: Вячеслав Круглов — Как начинающему Java-разработчику подружиться со своей базой данных?</a>
- <a href="http://www.youtube.com/watch?v=YzOTZTt-PR0">Видео: Николай Алименков — Босиком по граблям Hibernate</a>
- <a href="https://www.youtube.com/watch?v=-EpP0Vo63FM">Hibernate, how the magic is really done?</a>   - [code](https://github.com/xpinjection/hibernate-basics)
- <a href="https://www.youtube.com/watch?v=b52Qz6qlic0">Видео: Николай Алименков — Сделаем Hibernate снова быстрым</a>   - [code](https://github.com/xpinjection/hibernate-performance)
- <a href="https://www.youtube.com/watch?list=PLYj3Bx1JM6Y7BKivc3eZwRUhWwBmbIFXg&v=V-ljsrVy6pE">Hibernate performance tuning (Mikalai Alimenkou /Igor Dmitriev)</a>
- <a href="http://www.youtube.com/watch?v=1KphwODu1gg">Видео: работа в ZK с OpenJPA (в чем Hibernate хуже)</a>








