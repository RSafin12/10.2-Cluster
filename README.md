10.2 Кластеризация - Роман Сафин 

### Задание 1.

В чем различие между SMP и MPP системами?

SMP(Symmetric Multiprocessing) сильно связанные
Это архитектура при которой к общей высокоскоростной шине подключены несколько процессоров и устройства I/O. Все процессоры имеют равные права на память и общую адресацию, поэтому архитектура называется симметричной.
Из положительных моментов выделяют 
- простота программирования через использование потоков
- относительно простая конструкция 
- относительно невысокая цена 
Однако есть существенный минус, это проблемы с масштабируемостью, из-за чего такие системы не стали сильно популярными. Проблема эта связана с тем, что у общей шины есть пределы скорости. 

Примером таких систем думаю можно считать многопроцессорные серверы типа Intel Xeon E5-2620 или более современные решения на Intel Silver/Gold. 

MPP(Massive Parallel Proctssing) слабо связанные
В данном случае система состоит из отдельных нод, с отдельным CPU, RAM, и другие узлы, такие как сетевые адаптеры и диски. И так как память в этом случае разделена, то доступ к ней имеет только процессор, который находится на этой ноде. 

Ну и так как каждый процессор работает только со своей памятью, то не возникает проблем с масштабированием такого кластера. 

Однако такое решение проигрывает в скорости, посколько нет общей шины передачи данных. Ну и каждый проц ограничен только своей паматью. 

Есть мнение, что поддерживать такие системы дороже

---

### Задание 2.

В чем отличие сильно связанных и слабо связанных систем?
Сильносвязанная система состоит из нескольких однородных процессоров и общей памяти. Примеры, NUMA и SMP системы. 
Я также  нашел другое название таких систем, тесносвязанные системы. В таких системах несколько процессоов подключены на уровне шины. Ранее приведенный пример с Xeon E5-2620 отражает принцип реализации, 2 процессора на одной мат. плате разделяют общую память. 

Слабосвязанная система также называемая кластером это по факту несколько ПК или серверов которые соединены очень высокоскростной сетью, например, Gbps или оптоволкном. Они решают какую-то общую задачу, например, это может быть отказоустойчивый кластер или вычислетильный кластер. 

---

### Задание 3.

Какие преимущества отличают кластерные системы от обычных серверов?

Сам по себе современный 2-х процессорный сервер, например решения на Xeon Gold или AMD Epyc,  на рынке это дорогое удовольстие. К тому же процессорные ресурсы в таком случае трудно масштабировать в случае увеличения нагрузки. 
Кластерные системы в этом отношении проще, можно по факту использовать любое доступное железо. Собирать кластер из обычных ПК это конечно перебор, но собрать кластер из серверов "попроще" это вполне решение. Это дешевле и проще масштабируется с аппаратной точки зрения. То есть если по каким то причинам одна из нод кластера "устала", то ее можно заменить новой по-мощнее. Можно расширять как сам кластер, так и его отдельные ноды. Ну и отказоустойчивость такого решения намного лучше, т.к. ноды автономны. 
В многопроцессорном сервере такой фокус провернуть труднее и намного дороже.


---

### Задание 4.

Приведите примеры типов современных кластерных систем?
1. Отказоустойчивые кластеры 
2. Кластеры с балансировкой нагрузки
3. Вычислительные 
4. Системы распределенных вычислений 


---

### Задание 5.

Где использует сервис Kafka, rabitMQ?

Kafka, rabitMQ - это брокеры сообщений, т.е. посредники отвечающие за прием и отправку сервисных сообщений между разными микросервисами. Они решают похожие задачи, но при этом имеют различия, оба инструмента хорошо масштабируются и надежны. Самое ключевое отличие в модели отправки сообщений, rabitMQ push-ит сообщения подписчикам  до тех пор пока они его не получат, после это сообщение удаляется. Kafka же применяет pull-модель, когда потребители сообщений сами отправляют запрос на получение сообщения. 

RabbitMQ имеет более гибкую маршрутизацию сообщений, можно настроить сложную логику отправки с гарантией доставки сообщений. Также в преимущества можно записать работу с стандартизированными протоколами, т.е. при необходимости можно будет сменить брокера сообщений. RabbitMQ обычно применяется для взаимодействия микросервисов. 

Kafka хранит сообщения в очереди в строгой последовательности - топике. Потребители подписывают на определеннные топики, что позволяет работать с большим кол-вом подписчиков. Kafka чаще всего используется в стриминговых сервисах, потоковой передаче данных благодаря своей высокой скорости и производительности. Kafka отлично масштабируется путем добавления новых узлов. 
