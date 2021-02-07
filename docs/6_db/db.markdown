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
  * RDBMS vs DB  [first site](https://stackoverflow.com/questions/18419137/what-is-the-difference-between-dbms-and-rdbms)
  * JDBC Driver types, transport types  [first site](https://proselyte.net/tutorials/jdbc/introduction/) [second site](https://www.tutorialspoint.com/jdbc/jdbc-driver-types.htm) [third site](https://www.progress.com/faqs/datadirect-jdbc-faqs/what-are-the-types-of-jdbc-drivers)
* Connect to database
  * Driver, DriverManager, DataSource  [first site](https://stackoverflow.com/questions/15198319/why-do-we-use-a-datasource-instead-of-a-drivermanager) [second site](http://java-online.ru/jdbc-drivermanager.xhtml) [third site](https://overcoder.net/q/80648/%D0%BF%D0%BE%D1%87%D0%B5%D0%BC%D1%83-%D0%BC%D1%8B-%D0%B8%D1%81%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D1%83%D0%B5%D0%BC-datasource-%D0%B2%D0%BC%D0%B5%D1%81%D1%82%D0%BE-drivermanager)
  * Connection, JDBC URL   [first site](https://proselyte.net/tutorials/jdbc/connection/) [second site](https://www.tutorialspoint.com/jdbc/jdbc-db-connections.htm)
* Query database
  * DDL and DML [first site](https://info-comp.ru/what-is-ddl-dml-dcl-tcl)
  * Statement  [first site](https://proselyte.net/tutorials/jdbc/statements/) [second site](https://www.tutorialspoint.com/jdbc/jdbc-statements.htm)
  * Statement.executeUpdate: INSERT, UPDATE, DELETE  [first site](https://www.codota.com/code/java/methods/java.sql.Statement/executeUpdate)
  * Statement.executeQuery: SELECT, ResultSet  [first site](https://www.codota.com/code/java/methods/java.sql.Statement/executeQuery)
  * Statement.execute  [first site](http://tutorials.jenkov.com/jdbc/statement.html) [second site](https://www.codota.com/code/java/methods/java.sql.Statement/execute)
  * SQLException: errorCode and errorState  [first site](https://docs.microsoft.com/en-us/sql/connect/jdbc/handling-errors?view=sql-server-ver15) [second site](https://www.codota.com/code/java/classes/java.sql.SQLException) [third site](https://www.codota.com/code/java/methods/java.sql.Statement/getWarnings)
* ResultSet
  * ResultSet: (positioning, transition, type, concurrency, holdability)  [first site](https://proselyte.net/tutorials/jdbc/result-set/) [second site](https://stackoverflow.com/questions/55531375/why-is-reading-a-jdbc-resultset-by-position-faster-than-by-name-and-how-much-fas)
* JDBC Optimizations(important)
  * PreparedStatement = + precompilation — SQL injection  [first site](https://stackoverflow.com/questions/23845383/what-does-it-mean-when-i-say-prepared-statement-is-pre-compiled) [second site](https://stackoverflow.com/questions/1582161/how-does-a-preparedstatement-avoid-or-prevent-sql-injection)
  * Batch update = vectorization  [first site](https://www.codejava.net/java-se/jdbc/jdbc-batch-update-examples)  [second site](https://stackoverflow.com/questions/14264953/how-is-jdbc-batch-update-helpful)  [third site](http://tutorials.jenkov.com/jdbc/batchupdate.html)
  * Connection pooling  [first site](https://vladmihalcea.com/the-anatomy-of-connection-pooling/) [second  site](https://stackoverflow.com/questions/2835090/how-to-establish-a-connection-pool-in-jdbc)

### ORM
{: .label }

* Introduction
  * ORM implementations  [Hibernate](https://ru.wikipedia.org/wiki/Hibernate_(библиотека)) [OpenJPA](https://en.wikipedia.org/wiki/Apache_OpenJPA) [EсlipseLink](http://en.wikipedia.org/wiki/EclipseLink) [TopLink](http://en.wikipedia.org/wiki/TopLink)
  * Hibernate VS JDBC  [first site](https://habiletechnologies.com/blog/reasons-to-choose-hibernate-over-jdbc)
  * O/R Mismatch  [first site](https://uk.wikipedia.org/wiki/%D0%9E%D0%B1%27%D1%94%D0%BA%D1%82%D0%BD%D0%BE-%D1%80%D0%B5%D0%BB%D1%8F%D1%86%D1%96%D0%B9%D0%BD%D0%B8%D0%B9_%D1%80%D0%BE%D0%B7%D1%80%D0%B8%D0%B2)
  * JPA vs. Hibernate  [first site](https://dzone.com/articles/what-is-the-difference-between-hibernate-and-sprin-1) [second site]()
  * Schema Management   [first site](https://stackoverflow.com/questions/2585641/hibernate-jpa-db-schema-generation-best-practices) [second site](https://docs.jboss.org/hibernate/orm/5.2/userguide/html_single/chapters/schema/Schema.html)  [Flyway vs. Liquibase](https://habr.com/ru/company/haulmont/blog/440696/)
* Connection Management
  * Hibernate Connection Lifecycle, Open Session In View  [first site](http://java-latte.blogspot.com/2014/10/how-hibernate-works-and-its-architecture-and-Persistence-Lifecycle-of-hibernate.html) [second site](https://stackoverflow.com/questions/1103363/why-is-hibernate-open-session-in-view-considered-a-bad-practice) [third site](https://stackoverflow.com/questions/8724259/spring-hibernate-session-lifecycle)
  * Connection Monitoring  [first site](https://stackoverflow.com/questions/3522051/hibernate-monitoring-solution) [second site](https://vladmihalcea.com/connection-monitoring-jpa-hibernate/)
  * Hibernate Statistics  [first site](https://vladmihalcea.com/hibernate-statistics/)
* Types and Identifiers
  * JPA and Hibernate Types  [first site](https://vladmihalcea.com/a-beginners-guide-to-hibernate-types/) [second site](https://docs.jboss.org/hibernate/stable/core.old/reference/en/html/mapping-types.html)
  * Custom Hibernate Types  [first site](https://vladmihalcea.com/how-to-implement-a-custom-basic-type-using-hibernate-usertype/) [second site](https://stackoverflow.com/questions/35227986/implementing-custom-hibernate-type)
  * JPA and Hibernate Identifiers  [first site](https://vladmihalcea.com/jpa-entity-identifier-sequence/) [second site](https://thorben-janssen.com/jpa-generate-primary-keys/)
  * Hibernate Identifier Optimizers (e.g. hilo, pooled, pooled-lo)  [first site](https://stackoverflow.com/questions/25204019/how-to-use-the-pooled-lo-optimizer-with-hibernate) [second site](https://vladmihalcea.com/hibernate-hidden-gem-the-pooled-lo-optimizer/)
* Relationships
  * JPA and Hibernate Relationships  [first site](https://stackabuse.com/a-guide-to-jpa-with-hibernate-relationship-mapping/) [second site](https://thorben-janssen.com/ultimate-guide-association-mappings-jpa-hibernate/)
  * Equals and Hashcode  [first site](https://stackoverflow.com/questions/1638723/how-should-equals-and-hashcode-be-implemented-when-using-jpa-and-hibernate) [second site](https://vladmihalcea.com/the-best-way-to-implement-equals-hashcode-and-tostring-with-jpa-and-hibernate/) [third site](https://thorben-janssen.com/ultimate-guide-to-implementing-equals-and-hashcode-with-hibernate/)
  * ManyToOne  [first site](https://vladmihalcea.com/manytoone-jpa-hibernate/) [second site](https://qna.habr.com/q/62258)
  * OneToMany  [first site](https://vladmihalcea.com/the-best-way-to-map-a-onetomany-association-with-jpa-and-hibernate/) [second site](https://medium.com/@rajibrath20/the-best-way-to-map-a-onetomany-relationship-with-jpa-and-hibernate-dbbf6dba00d3)
  * OneToOne  [first site](https://vladmihalcea.com/the-best-way-to-map-a-onetoone-relationship-with-jpa-and-hibernate/) [second site](https://stackoverflow.com/questions/21762328/java-hibernate-onetoone-mapping)
  * ManyToMany  [first site](https://thorben-janssen.com/best-practices-for-many-to-many-associations-with-hibernate-and-jpa/) [second site](https://www.baeldung.com/jpa-many-to-many)
  
* Inheritance  [first site](https://habr.com/ru/post/337488/)
  * JPA Inheritance Basics  [first site](https://vladmihalcea.com/the-best-way-to-use-entity-inheritance-with-jpa-and-hibernate/)
  * Single Table Inheritance   [first site](https://vladmihalcea.com/the-best-way-to-map-the-single_table-inheritance-with-jpa-and-hibernate/) [second site](https://stackoverflow.com/questions/63656497/jpa-repository-with-single-table-inheritance-hibernate)
  * Discriminator Column  [first site](https://vladmihalcea.com/the-best-way-to-map-the-discriminatorcolumn-with-jpa-and-hibernate/) [second site](https://stackoverflow.com/questions/16772370/when-to-use-discriminatorvalue-annotation-in-hibernate)
  * Joined Inheritance  [first site](https://habr.com/ru/post/337488/)
  * TablePerClass Inheritance  [first site](https://stackoverflow.com/questions/3557879/hibernate-and-inheritance-table-per-class)
* Persistence Context
  * Persistence Context and Flushing Basics  [first site](https://vladmihalcea.com/a-beginners-guide-to-jpahibernate-flush-strategies/) [second site](https://vladmihalcea.com/hibernate-facts-knowing-flush-operations-order-matters/)
  * The AUTO FlushModeType  [first site](https://stackoverflow.com/questions/18149876/what-to-use-flush-mode-auto-or-commit)
  * Dirty Checking Mechanism  [first site](https://vladmihalcea.com/the-anatomy-of-hibernate-dirty-checking/) [second site](https://vladmihalcea.com/how-to-customize-hibernate-dirty-checking-mechanism/) [third site](https://stackoverflow.com/questions/5268466/how-does-hibernate-detect-dirty-state-of-an-entity-object)
  * Bytecode Enhancement Dirty Checking  [first site](https://vladmihalcea.com/how-to-enable-bytecode-enhancement-dirty-checking-in-hibernate/)
* Batching and Statement Caching
  * Statement Lifecycle and Execution Plans  [first site](https://vladmihalcea.com/execution-plan-sql-server/)
  * Statement Caching  [first site](https://vladmihalcea.com/hibernate-performance-tuning-tips/) [second site](https://stackoverflow.com/questions/17764142/does-hibernate-use-preparedstatement-by-default)
  * Statement Batching and Cascade Operations  [first site](https://vladmihalcea.com/how-to-batch-delete-statements-with-hibernate/) [second site](https://vladmihalcea.com/how-to-optimize-the-merge-operation-using-update-while-batching-with-jpa-and-hibernate/)
  * Batching Update Operations  [first site](https://www.codejava.net/frameworks/hibernate/how-to-execute-batch-insert-update-in-hibernate)
  * SQL Injection  [first site](https://habr.com/ru/company/parallels/blog/272589/)
  * Hibernate Cache  [first site](http://habrahabr.ru/post/135176/) [second site](http://habrahabr.ru/post/136375/) [third site](http://www.tutorialspoint.com/hibernate/hibernate_caching.htm) [fourth site](http://stackoverflow.com/questions/3663979/how-to-use-jpa2s-cacheable-instead-of-hibernates-cache) [fifth site](http://vladmihalcea.com/2015/06/08/how-does-hibernate-query-cache-work/) [sixth](https://www.javacodegeeks.com/2014/06/pitfalls-of-the-hibernate-second-level-query-caches.html)
* Fetching
  * Direct and Natural id fetching  [first site](https://vladmihalcea.com/the-best-way-to-map-a-naturalid-business-key-with-jpa-and-hibernate/)
  * DTO projections vs Entity queries  [first site](https://vladmihalcea.com/the-best-way-to-map-a-projection-query-to-a-dto-with-jpa-and-hibernate/) [second site](https://thorben-janssen.com/entities-dtos-use-projection/)
  * LAZY vs. EAGER  [first site](https://stackoverflow.com/questions/2990799/difference-between-fetchtype-lazy-and-eager-in-java-persistence-api)

### Hibernate flush

-  Ресурсы:
- <a href="https://dou.ua/lenta/articles/hibernate-fetch-types/">Стратегии загрузки коллекций в Hibernate</a>
-  <a href="http://habrahabr.ru/post/265061/">JPA и Hibernate в вопросах и ответах</a>
- [Hibernate — о чем молчат туториалы](https://habr.com/ru/post/416851/)
- [Наследование в Hibernate: выбор стратегии](https://habrahabr.ru/post/337488/)
- [Field vs property access](http://stackoverflow.com/a/6084701/548473)
- <a href="http://stackoverflow.com/questions/1069992/jpa-entitymanager-why-use-persist-over-merge">Merge vs Persist</a>
- <a href="https://developer.jboss.org/wiki/OpenSessionInView">Паттерн "открытие транзакции в фильтре"</a> и <a href="http://stackoverflow.com/questions/1103363/why-is-hibernate-open-session-in-view-considered-a-bad-practice">почему это bad-practice</a>



### DB
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
- <a href="http://www.youtube.com/watch?v=YzOTZTt-PR0">Видео: Николай Алименков — Босиком по граблям Hibernate</a>
- <a href="https://www.youtube.com/watch?v=-EpP0Vo63FM">Hibernate, how the magic is really done?</a>   - [code](https://github.com/xpinjection/hibernate-basics)
- <a href="https://www.youtube.com/watch?v=b52Qz6qlic0">Видео: Николай Алименков — Сделаем Hibernate снова быстрым</a>   - [code](https://github.com/xpinjection/hibernate-performance)
- <a href="https://www.youtube.com/watch?list=PLYj3Bx1JM6Y7BKivc3eZwRUhWwBmbIFXg&v=V-ljsrVy6pE">Hibernate performance tuning (Mikalai Alimenkou /Igor Dmitriev)</a>
- <a href="http://www.youtube.com/watch?v=1KphwODu1gg">Видео: работа в ZK с OpenJPA (в чем Hibernate хуже)</a>








