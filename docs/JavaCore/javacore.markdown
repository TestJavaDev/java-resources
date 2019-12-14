---
layout: default
title: JavaCore
nav_order: 1
permalink: /javacore
has_children: true
---
<div align="center" markdown="1">
JavaCore / Java resources / Articles

{: .fs-6 .fw-300 }
</div>

- <a href="https://habrahabr.ru/post/283290/">Сравнение EE и Spring в комментариях</a>
- [The Top 20 Most Popular Java Libraries](https://dzone.com/articles/the-top-100-java-libraries-in-2016-after-analyzing)
- [Guava Wiki](https://github.com/google/guava/wiki)
  - [Apache Commons](https://commons.apache.org/)
  - [Spring Boot cache providers](http://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-caching.html#_supported_cache_providers)
- [Release 21.0: Java 8!](https://github.com/google/guava/wiki/Release21)
- [118 слайдов от Егора Чернышева](https://www.slideshare.net/echernyshev/guava-41982734)








- [Java](http://ru.wikipedia.org/wiki/Java), [JVM](http://ru.wikipedia.org/wiki/Виртуальная_машина_Java), [JIT-компиляция](http://ru.wikipedia.org/wiki/JIT) (wiki)
- [Что такое Java? История создания](http://www.intuit.ru/studies/courses/16/16/lecture/27105)
- [Что такое JDK? Введение в средства разработки Java](https://topjava.ru/blog/what-is-the-jdk)
- [Что такое JRE? Введение в среду выполнения Java](https://topjava.ru/blog/what-is-the-jre)
- [Programming languages TIOBE Index](http://www.tiobe.com/index.php/content/paperinfo/tpci/index.html)

![jvm](https://cloud.githubusercontent.com/assets/18701152/15219296/e6c67e86-186b-11e6-986f-651a87deec6c.png)

- [ME](http://ru.wikipedia.org/wiki/Java_Platform,_Micro_Edition), [SE](https://ru.wikipedia.org/wiki/Java_Platform,_Standard_Edition), [EE](http://ru.wikipedia.org/wiki/Java_Platform,_Enterprise_Edition) (wiki)
- [Java Microbenchmark JMH](http://openjdk.java.net/projects/code-tools/jmh/)
- [Oracle Java8 Home](http://docs.oracle.com/javase/8/docs/index.html)
- <a href="http://www.intuit.ru/studies/courses/16/16/info">Интуит. Программирование на Java</a>
- <a href="http://ggenikus.github.io/blog/2014/05/04/gc">Основы Java garbage collection</a>
- <a href="https://habrahabr.ru/post/134102/">Размер Java объектов</a>
- <a href="http://www.quizful.net/post/java-reflection-api">Введение в Java Reflection API</a>
- <a href="https://habrahabr.ru/users/tarzan82/topics/">Структуры данных в картинках</a>
- <a href="https://habrahabr.ru/company/luxoft/blog/157273/">Обзор java.util.concurrent.*</a>
- <a href="http://www.skipy.ru/technics/synchronization.html">Синхронизация потоков</a>
- <a href="http://java67.blogspot.ru/2014/08/difference-between-string-literal-and-new-String-object-Java.html">String literal pool</a>
- <a href="https://habrahabr.ru/post/132241/">Маленькие хитрости Java</a>
-  <a href="https://github.com/winterbe/java8-tutorial">A Guide to Java 8</a>
- [Implementing equals() and hashCode()](https://access.redhat.com/documentation/en-us/jboss_enterprise_application_platform/4.3/html/hibernate_reference_guide/persistent_classes-implementing_equals_and_hashcode)

- Оптимально использовать уникальные бизнес-поля, но обычно таких нет, и чаще всего используются PK с ограничением, что он может быть `null` у новых объектов, и нельзя объекты сравнивать через `equals() and hashCode()` в бизнес-логике (например, тестах).

- [equals() and hashcode() when using JPA and Hibernate](https://stackoverflow.com/questions/1638723)
- [Методы класса String, появившиеся в Java 11](https://topjava.ru/blog/java-11-string-api-additions)
- [Модификатор static](http://www.intuit.ru/studies/courses/16/16/lecture/27119)
- [10 заметок о модификаторе static в Java](http://info.javarush.ru/translation/2014/04/15/10-заметок-о-модификаторе-Static-в-Java.html)
- [Класс Object. Контракт equals/hashCode](http://www.intuit.ru/studies/courses/16/16/lecture/27129?page=1)
- [Абстрактные классы](https://www.youtube.com/watch?v=ZjiFL2Yo2fw) (youtube)
- [Интерфейсы](http://www.intuit.ru/studies/courses/16/16/lecture/27119?page=3)
- [Полиморфизм](http://www.intuit.ru/studies/courses/16/16/lecture/27119?page=4)
- [Отличия абстрактного класса от интерфейса](https://ru.stackoverflow.com/questions/235352/Отличия-абстрактного-класса-от-интерфейса-abstract-class-and-interface)
- [Что такое полиморфизм?](https://github.com/ichimax/Core-Java-Interview-Questions/blob/master/Questions/1.%20OOP.md#%D0%A7%D1%82%D0%BE-%D1%82%D0%B0%D0%BA%D0%BE%D0%B5-%D0%BF%D0%BE%D0%BB%D0%B8%D0%BC%D0%BE%D1%80%D1%84%D0%B8%D0%B7%D0%BC)
- [Ключевое слово static](https://www.youtube.com/watch?v=GZzVfeY7yEM) (youtube)
- [Интерфейсы, абстрактные классы, полиморфизм](https://www.youtube.com/watch?v=7NMFk2oj1-c&index=4&list=PLkKunJj_bZefB1_hhS68092rbF4HFtKjW) (youtube)
- [Разбираемся с hashCode() и equals()](https://habrahabr.ru/post/168195/)
- [Строки в Java](https://urvanov.ru/2016/04/20/java-8-строки/)
- [Кодировка в Java](http://www.skipy.ru/technics/encodings.html)
- [Ошибки при использовании строк](http://www.skipy.ru/technics/strings.html)
- [Обработка строк в Java](https://habrahabr.ru/post/260767/)
- [StringBuilder vs StringBuffer](https://stackoverflow.com/questions/355089/difference-between-stringbuilder-and-stringbuffer?rq=1)
- [String vs StringBuffer vs StringBuilder](https://www.journaldev.com/538/string-vs-stringbuffer-vs-stringbuilder)
- [String literal pool](http://java67.blogspot.ru/2014/08/difference-between-string-literal-and-new-String-object-Java.html)
- [Java 8 аннотации](https://urvanov.ru/2016/03/30/java-8-аннотации/)
- [Reflection для начинающих](https://youtu.be/XJQuBXWADZg) (youtube)
- [Руководство по Java Reflection API](http://javadevblog.com/polnoe-rukovodstvo-po-java-reflection-api-refleksiya-na-primerah.html)
- [Java Reflection Example Tutorial](https://www.journaldev.com/1789/java-reflection-example-tutorial)
- [The Reflection API](https://docs.oracle.com/javase/tutorial/reflect/)
- [What is reflection and why is it useful?](https://stackoverflow.com/questions/37628/what-is-reflection-and-why-is-it-useful) В нашем проекте Reflection используют JUnit и будут использовать библиотеки работы с XML и JSON
 - [Фреймворк для модульного тестирования JUnit](http://junit.org/)
 - [Тестирование с помощью JUnit (Test Case)](http://www.javenue.info/post/19)
 - [Тестирование кода Java с помощью фреймворка JUnit](https://www.youtube.com/watch?v=z9jEVLCF5_w) (youtube)
 - [Исключения (Exceptions)](http://proglang.su/java/exceptions)
 - [Статья про исключения](http://developer.alexanderklimov.ru/android/java/exception.php)
 - Про исключения также можно почитать в книге Джошуа Блоха - ["Java. Эффективное программирование"](https://www.ozon.ru/context/detail/id/21724143/)
 - [Конструктор](http://info.javarush.ru/javarush_articles/2015/12/04/Конструкторы-классов-Java-JDK-1-5-.html)
 - [Ключевые слова: this, super](http://info.javarush.ru/grishin/2015/03/31/Разница-между-ключевыми-словами-this-и-super-в-Java.html)
 - [Exceptions](https://docs.oracle.com/javase/tutorial/essential/exceptions/)
 - [Checked vs unchecked exception explanation](https://stackoverflow.com/questions/6115896/java-checked-vs-unchecked-exception-explanation)

### Java data types

 - [Типы данных](http://www.intuit.ru/studies/courses/16/16/lecture/27111)
 - [Классы-обертки](http://www.intuit.ru/studies/courses/16/16/lecture/27129?page=2)
 - [Java types](https://youtu.be/JmplWN-FdMQ) (youtube)
 - [Модификаторы доступа](https://www.youtube.com/watch?v=e14xUIUc6y0) (youtube)
 - [Пакеты](https://youtu.be/a6KGNASOtK8) (youtube)
 - [Packages](https://docs.oracle.com/javase/tutorial/java/package/index.html)
 - [Primitive data types](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html)
 - [What is a NullPointerException, and how do I fix it?](https://stackoverflow.com/questions/218384/what-is-a-nullpointerexception-and-how-do-i-fix-it)
 - [Why should one use Objects.requireNonNull()?](https://stackoverflow.com/questions/45632920/why-should-one-use-objects-requirenonnull)
 - [Инициализация и загрузка классов](https://www.youtube.com/watch?v=TdvnGw_KcFY) (youtube)

### Classloader
- <a href="https://habrahabr.ru/post/103830/">Загрузка классов в Java</a>
- <a href="https://tomcat.apache.org/tomcat-8.0-doc/class-loader-howto.html">Apache Tomcat Class Loader</a>
- <a href="https://tomcat.apache.org/tomcat-8.0-doc/class-loader-howto.html">Class Loader HOW-TO</a>
- Библиотеки vs Frameworks и Tomcat Common Lib. <a href="https://habrahabr.ru/post/222443/">Memory Leaks</a>. 
- <a href="https://www.youtube.com/watch?v=sSmQ6W-ovZE">Никита Сальников-Тарновский — Утечки памяти</a>

### Java Collections

- [Контейнеры/коллекции](http://en.wikipedia.org/wiki/Java_collections_framework)
- [List, Set, Map, Queue, Iterator, ListIterator](http://www.intuit.ru/studies/courses/16/16/lecture/27131?page=2)
- [Структуры данных в картинках](http://habrahabr.ru/users/tarzan82/topics/)
- [Внутренняя работа HashMap в Java](https://habr.com/post/421179/)
- [Инициализация полей в Java](http://www.quizful.net/post/java-fields-initialization)
- [Java собеседование по коллекциям](http://habrahabr.ru/post/162017/)
- [Часто задаваемые на собеседованиях вопросы по классам коллекциям в Java](http://info.javarush.ru/translation/2013/10/08/Часто-задаваемые-на-собеседованиях-вопросы-по-классам-коллекциям-в-Java-Часть-2-.html#1)
- [Собеседование по Java — коллекции](http://javastudy.ru/interview/collections/)
- [Коллекции в Java (стандартные, guava, apache, trove, gs-collections и другие)](https://habr.com/ru/company/luxoft/blog/256877/)
- [Collection.toArray(new T[0]) or Collection.toArray(new T[size]), that's the question](https://shipilev.net/blog/2016/arrays-wisdom-ancients)
- [Автоупаковка и распаковка в Java](https://habrahabr.ru/post/329498/)
- [Преобразования Integer и int](https://habrahabr.ru/post/104231/)
- [Класс-обертка](https://www.youtube.com/watch?v=T99Dpp29jrU) (youtube)
- [Autoboxing and Unboxing](https://docs.oracle.com/javase/tutorial/java/data/autoboxing.html)
- [Why do we use autoboxing and unboxing in Java?](https://stackoverflow.com/questions/27647407/why-do-we-use-autoboxing-and-unboxing-in-java)
- [Паттерн проектирования Итератор](https://refactoring.guru/ru/design-patterns/iterator/java/example)
- [Iterator / Iterable](http://www.javenue.info/post/101)
- [Iterator in Java](https://www.journaldev.com/13460/java-iterator)
- <a href="http://stackoverflow.com/questions/1132507/java-array-thread-safety">Java array thread-safety</a>

### Java Nested and Inner Class
- [Вложенные классы в Java](https://habrahabr.ru/post/342090/) 
- [Вложенные, внутренние, локальные и анонимные классы](http://pr0java.blogspot.ru/2015/08/1.html)
- [Локальные и анонимные классы](http://easy-code.ru/lesson/local-anonymous-nested-classes-java). 
- [Интерфейсы Comparable и Comparator](https://metanit.com/java/tutorial/5.6.php)
- [Анонимные классы в Java](https://www.youtube.com/watch?v=P3uicghNPLg) (youtube)
- [Nested (static) классы в Java](https://www.youtube.com/watch?v=svOwVvSWeus) (youtube)
- [Inner (non-static) классы в Java](https://www.youtube.com/watch?v=LflAy_LOwwQ) (youtube)
- [Вложенные, внутренние, локальные и анонимные классы [eng]](https://docs.oracle.com/javase/tutorial/java/javaOO/nested.html)
- [Дженерики (Java, обучающая статья)](http://www.quizful.net/post/java-generics-tutorial)
- [Обобщения (Generic)](http://developer.alexanderklimov.ru/android/java/generic.php)
- [Ограничения](http://docs.oracle.com/javase/tutorial/java/generics/restrictions.html)
- [Java Generics Example Tutorial](https://www.journaldev.com/1663/java-generics-example-method-class-interface)
- [Одиночка (шаблон проектирования)](https://ru.wikipedia.org/wiki/Одиночка_(шаблон_проектирования))
- [Перечисляемые типы (enum) в Java](http://easy-code.ru/lesson/enum-types-java)

### Logging

- [Log4J (Apache logging)](https://logging.apache.org/)
- [Java Logging API - Tutorial](http://www.vogella.com/tutorials/Logging/article.html)
- [Логирование в Java / quick start](https://habrahabr.ru/post/130195/)
- [Ведение лога приложения](http://skipy.ru/useful/logging.html)
- [Java Logging: история кошмара](http://habrahabr.ru/post/113145/)

### IO

 - <a href="http://www.intuit.ru/studies/courses/16/16/lecture/27133?page=4#sect23">File. Работа с файловой системой.</a>
 - Работа с ресурсами. <a href="https://habrahabr.ru/post/178405/">Правильно освобождаем ресурсы в Java</a>
 - <a href="http://info.javarush.ru/translation/2013/08/19/Java-7-try-with-resources.html">Java 7 try-with-resources</a>
- <a href="http://www.intuit.ru/studies/courses/16/16/lecture/27133">Пакет java.io</a>
- <a href="http://ru.wikipedia.org/wiki/Декоратор_(шаблон_проектирования)">Паттерн Декоратор</a>.
- <a href="http://www.intuit.ru/studies/courses/16/16/lecture/27133?page=4">Классы Reader и Writer.</a>
 <a href="http://www.intuit.ru/studies/courses/16/16/lecture/27133?page=3">Сериализация объектов (serialization)</a>
- Реализация Storage используя <a href="https://habrahabr.ru/post/60317/">сериализацию</a>.
- Сериализация: [1](https://www.youtube.com/watch?v=dBcqizwOWLg), [2](https://www.youtube.com/watch?v=nr4_JRKCGBU) (youtube)

### XML

- <a href="http://www.duct-tape-architect.ru/?p=315">XML формат и технологии</a>
- Wiki: <a href="https://ru.wikipedia.org/wiki/XML">XML</a>, <a href="https://ru.wikipedia.org/wiki/XSL">XSL</a> , <a href="https://ru.wikipedia.org/wiki/Document_Object_Model">DOM</a>, <a href="https://ru.wikipedia.org/wiki/SAX">SAX</a>, <a href="https://en.wikipedia.org/wiki/StAX">StAX</a>, <a href="https://ru.wikipedia.org/wiki/Java_Architecture_for_XML_Binding">JAXB</a>
- <a href="http://www.vogella.com/tutorials/JavaXML/article.html">Работа с XML в Java</a>. Реализация хранения в XML. 
- <a href="http://genberm.narod.ru/xml/lections/xml/introduction.html">История создания</a>. <a href="http://www.duct-tape-architect.ru/?p=315">XML формат и технологии</a>, <a href="https://ru.wikipedia.org/wiki/XML">XML</a>
- <a href="http://stackoverflow.com/questions/33746/xml-attribute-vs-xml-element#33757">Attribute vs Element</a>. 
- <a href="http://genberm.narod.ru/xml/schema/schema0/2.7.html">sequence/ choice/ all/ group</a>. <a href="https://docstore.mik.ua/orelly/xml/schema/ch09_01.htm">Define referring to Another XML Element</a>
- <a href="http://genberm.narod.ru/xml/lections.html">Лекции по XML</a>
- <a href="http://www.vogella.com/tutorials/JavaXML/article.html">Работа с XML в Java</a>.
- <a href="https://ru.wikipedia.org/wiki/Document_Object_Model">DOM</a>, <a href="https://ru.wikipedia.org/wiki/SAX">SAX</a>
- <a href="http://www.ibm.com/developerworks/ru/library/x-jaxp/">JAXP: вспомогательный слой над SAX и DOM API</a>
- <a href="https://ru.wikipedia.org/wiki/Java_Architecture_for_XML_Binding">JAXB</a>, <a href="https://ru.wikipedia.org/wiki/JAXP">JAXP</a>, <a href="https://ru.wikipedia.org/wiki/Xerces">Xerces</a>, <a href="https://ru.wikipedia.org/wiki/Xalan">Xalan</a>
- <a href="https://www.ibm.com/developerworks/ru/library/x-javaxmlvalidapi/">Валидации XML</a>

### Структура памяти: куча, стек, permanent/metaspace
- <a href="https://www.slideshare.net/solit/jvm-16948708">JVM изнутри - оптимизация и профилирование</a>.
- <a href="http://stackoverflow.com/questions/79923/what-and-where-are-the-stack-and-heap#24171266">Stack and Heap</a>
- <a href="http://habrahabr.ru/post/117274/">Из каких частей состоит память java процесса</a>.
- <a href="http://www.javaspecialist.ru/2011/04/permanent.html">Permanent область памяти</a>
- <a href="http://www.javaspecialist.ru/2011/04/java-thread-stack.html">Java thread stack </a>
- <a href="http://habrahabr.ru/post/134102/">Размер Java объектов</a>

### Ленивая инициализация Singleton
- <a href="https://habrahabr.ru/post/27108/">Реализация Singleton в JAVA</a>
- <a href="https://ru.wikipedia.org/wiki/Double_checked_locking">Double checked locking</a>
- <a href="https://en.wikipedia.org/wiki/Initialization-on-demand_holder_idiom">Initialization-on-demand holder idiom</a>
- <a href="https://tproger.ru/translations/singleton-pitfalls/">Подводные камни Singleton</a>

### Multithreading

![Закон Мура](https://www.karlrupp.net/wp-content/uploads/2015/06/40-years-processor-trend.png)
- <a href="https://ru.wikipedia.org/wiki/Закон_Мура">Закон Мура</a>
- <a href="https://ru.wikipedia.org/wiki/Закон_Амдала">Закон Амдала</a>
- [Фундаментальный поворот к параллелизму в программировании](https://habrahabr.ru/post/145432/)
- <a href="https://ru.wikipedia.org/wiki/Параллелизм_в_Java">Параллелизм в Java</a>
- <a href="https://habrahabr.ru/post/27108/">Реализация Singleton в JAVA</a>
- <a href="https://ru.wikipedia.org/wiki/Double_checked_locking">Double checked locking</a>
-  <a href="http://www.javaspecialist.ru/2011/06/java-memory-model.html">Java Memory Model</a>. final, volatile
- <a href="https://en.wikipedia.org/wiki/Initialization-on-demand_holder_idiom">Initialization-on-demand holder idiom</a>
- <a href="https://ru.wikipedia.org/wiki/Параллелизм_в_Java">Параллелизм в Java</a>
- <a href="https://ru.wikipedia.org/wiki/Монитор_(синхронизация)">Монитор (синхронизация)</a>
- <a href="https://en.wikipedia.org/wiki/Compare-and-swap">Compare-and-swap</a>
- <a href="http://www.javaspecialist.ru/2011/06/java-memory-model.html">Java Memory Model</a>
- <a href="http://www.skipy.ru/technics/synchronization.html">Синхронизация потоков</a>
- <a href="https://habrahabr.ru/company/luxoft/blog/157273">Обзор java.util.concurrent.*</a>
- <a href="https://habrahabr.ru/post/132884/">Как работает ConcurrentHashMap</a>
- <a href="https://habrahabr.ru/post/277669/"> Справочник по синхронизаторам java.util.concurrent.*</a>
- <a href="http://articles.javatalks.ru/articles/17">Использование ThreadLocal переменных</a>
- <a href="https://www.youtube.com/watch?v=8piqauDj2yo">Николай Алименков — Прикладная многопоточность</a>
- <a href="http://stackoverflow.com/questions/20163056/in-java-can-thread-switching-happen-in-the-synchronized-block">Can thread switching happen in the synchronized block?</a>
- Алексей Владыкин, <a href="https://www.youtube.com/watch?v=zxZ0BXlTys0&list=PLlb7e2G7aSpRSBWi5jbGjIe-v_CjRO_Ug">Основы многопоточность в Java</a>
- Виталий Чибриков, <a href="https://www.youtube.com/watch?v=dLDhB6SRXzw&list=PLrCZzMib1e9qkzxEuU_huxtSAxrW1t9NZ">Java. Многопоточность</a>
- Computer Science Center, курс <a href="https://compscicenter.ru/courses/hp-course/2016-spring">Параллельное программирование</a>
- Юрий Ткач, курс <a href="https://www.youtube.com/playlist?list=PL6jg6AGdCNaXo06LjCBmRao-qJdf38oKp">Advanced Java - Concurrency</a>
- Головач, курс <a href="https://www.youtube.com/playlist?list=PLoij6udfBncgVRq487Me6yQa1kqtxobZS">Java Multithreading</a>

### Concurrency
- <a href="http://habrahabr.ru/company/luxoft/blog/157273/">Обзор java.util.concurrent.*</a></li>
- <a href="https://en.wikipedia.org/wiki/Compare-and-swap">Compare-and-swap</a>
- <a href="https://habrahabr.ru/post/277669/"> Справочник по синхронизаторам java.util.concurrent.*</a>
- <a href="http://articles.javatalks.ru/articles/17">Использование ThreadLocal переменных</a>

## Потоки. Синхронизация
-  <a href="http://www.intuit.ru/studies/courses/16/16/lecture/27127">Потоки выполнения. Синхронизация.</a>
-  <a href="http://www.intuit.ru/studies/courses/16/16/lecture/27127?page=4">Методы wait(), notify(), notifyAll() класса Object</a>



### OOP

 - [Объектно-ориентированное программирование](https://ru.wikipedia.org/wiki/Объектно-ориентированное_программирование) (wiki)
 - [Объектно-ориентированное программирование (перевод статьи)](http://info.javarush.ru/translation/2016/01/28/Объектно-ориентированное-программирование-перевод-статьи-.html)
- [Основы Объектно-Ориентированного Программирования (ООП)](https://github.com/ichimax/Core-Java-Interview-Questions/blob/master/Questions/1.%20OOP.md)
- [Наследование, агрегация, композиция, ассоциация](https://ru.wikipedia.org/wiki/Диаграмма_классов#Взаимосвязи) (wiki)
- [Типы отношений между классами](http://www.intuit.ru/studies/courses/16/16/lecture/27107?page=4)
- [Достоинства / Недостатки ООП](http://www.intuit.ru/studies/courses/16/16/lecture/27107?page=5)
- [Зачем нам ООП и что это такое?](https://habrahabr.ru/post/148015/)
- [Николай Алименков — Парадигмы ООП](https://www.youtube.com/watch?v=G6LJkWwZGuc) (youtube)
- [Object-Oriented Programming Concepts](https://docs.oracle.com/javase/tutorial/java/concepts/index.html)
- [Classes and Objects](https://docs.oracle.com/javase/tutorial/java/javaOO/index.html)

### Java Memory Model

 - [Что такое Heap и Stack память в Java?](https://javadevblog.com/chto-takoe-heap-i-stack-pamyat-v-java.html)
 - [Стек](https://ru.wikipedia.org/wiki/Стек) (wiki)
 - [От Java-кода к Java-куче](https://www.ibm.com/developerworks/ru/library/j-codetoheap/index.html)
 - [Java Heap Space vs Stack – Memory Allocation in Java](https://www.journaldev.com/4098/java-heap-space-vs-stack-memory)
 - [Основы Java garbage collection](https://youtu.be/3TROgt7ncMo?t=51) (youtube)
 - [Из каких частей состоит память java процесса](http://habrahabr.ru/post/117274/)
 - [Permanent область памяти](http://www.javaspecialist.ru/2011/04/permanent.html)
 - [Java thread stack](http://www.javaspecialist.ru/2011/04/java-thread-stack.html)
 - [Размер Java объектов](http://habrahabr.ru/post/134102/)
 - [JVM - краткий курс общей анатомии](https://www.youtube.com/watch?v=-fcj6EL9rc4) (youtube)
 - [What and where are the stack and heap?](http://stackoverflow.com/questions/79923/what-and-where-are-the-stack-and-heap#24171266)
 - [The Java Virtual Machine Specification Java SE 8 Edition](https://docs.oracle.com/javase/specs/jvms/se8/jvms8.pdf)



