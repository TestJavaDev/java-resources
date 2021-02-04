---
layout: default
title: Network, Servlets API, REST
nav_order: 10
permalink: /http_servlets_rest
has_children: true
---
<div align="center" markdown="1">
Network, Servlets API, REST / Java resources / Grokking the interview

{: .fs-6 .fw-300 }
</div>

- [Что на самом деле происходит, когда пользователь вбивает в браузер адрес google.com](https://habr.com/ru/company/htmlacademy/blog/254825/)

### REST
{: .label }

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

### Java Networking – TCP/UDP Sockets
{: .label }

* OSI Model
  * OSI Layer 1 - The Physical Layer
  * OSI Layer 2 - The Data Link Layer
  * OSI Layer 3 - The Network Layer
  * OSI Layer 4 – The Transport Layer
  * OSI Layer 5 – The Session Layer
  * OSI Layer 6 – The Presentation Layer
  * OSI Layer 7 – The Application Layer
* TCP/IP Model
  * TCP/IP Layer 1 - The Link Layer
  * TCP/IP Layer 2 - The Internet Layer
  * TCP/IP Layer 3 - The Transport Layer
  * TCP/IP Layer 4 – The Application Layer 
* The TCP Protocol
  * TCP 3-Way Handshake
  * TCP 4-Way Disconnect
  * TCP Header Format
  * Socket Programming
  * The ServerSocket Class
  * EchoServer and EchoClient
  * Multiple clients EchoServer2
* Working with Thread Pools
  * Thread Pooling Client-Server
  * Cached Thread Pool
* A Template for TCP Server
  * An Upload Client-Server Program
  * A Chat Client-Server Program
  * Remote Procedure Call through Proxy
* Java NIO
  * Streams
  * Input and Output
  * NIO Channel vs. Stream
  * Stream Oriented vs. Buffer Oriented
* Java NIO core components
  * Channels
  * Buffers
  * Selectors
* Java Networking: TCP/UDP Sockets
  * The UDP Protocol
  * UDP Limitations
  * UDP Header Format
  * Application Layer Protocols to Use UDP
* Datagram Sockets, Datagram Packets
  * The DatagramSocket Class
  * The DatagramPacket Class
  * EchoUdpServer and EchoUdpClient
  * Predefined Socket Connection
  * UDP Chat
  * Multicast Receiver and Sender
* HTTP
  * Methods, status codes, headers (GET VS POST Idempotent)
  * Persistent connection, pipelining
  * Chunked encoding
  * Caching, encription, compression
  * основы REST
  * Архитектура простейшего многопоточного HTTP-сервера на Java
  
* Network
  * IP, TCP, UDP
  * telnet, FTP, DNS, SMTP/POP3
 

Руководство по Servlets
1. Введение
2. Жизненный цикл сервлетов
3. Пример приложения
4. HTTP коды
5. Запрос клиента
6. Ответ сервера
7. Заполнение форм
8. Исключения
9. Фильтры
10. Сессии
11. Работа с cookie
12. Работа с БД
13. Работа с датой и временем
14. Автоматическое обновление
15. Перенаправление
16. Счётчик посещение страницы
17. Интернационализация
18. Загрузка файлов
19. Отправка email

<a href="https://stackoverflow.com/questions/3106452/how-do-servlets-work-instantiation-sessions-shared-variables-and-multithreadi">How do servlets work? Instantiation, sessions, shared variables and multithreading</a>
<a href="https://mkyong.com/servlet/what-is-listener-servletcontextlistener-example/">ServletContextListener Example</a>
<a href="https://docs.oracle.com/javaee/6/tutorial/doc/bnafi.html">The Java EE 6 Tutorial</a>











