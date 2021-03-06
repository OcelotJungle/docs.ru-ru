---
title: Взаимодействие между службами
description: Узнайте, как встроенные микрослужбы облака взаимодействуют с другими внутренними микрослужбами.
author: robvet
ms.date: 09/09/2019
ms.openlocfilehash: 556617a9e2df5a4d9ff9adb9d19e714ca94930ea
ms.sourcegitcommit: 957c49696eaf048c284ef8f9f8ffeb562357ad95
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/07/2020
ms.locfileid: "82895498"
---
# <a name="service-to-service-communication"></a>Взаимодействие между службами

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

Перемещаясь с клиентского клиента, мы теперь подключаемся к внутренним микрослужбам.

При создании собственного облачного приложения необходимо учитывать, как серверные службы взаимодействуют друг с другом. В идеале, чем меньше взаимодействие между службами, тем лучше. Тем не менее, не всегда возможно, что серверные службы часто зависят друг от друга, чтобы выполнить операцию.

Существует несколько широко принятых подходов к реализации взаимодействия между службами. *Тип взаимодействия* взаимодействия часто определяет наилучший подход.

Рассмотрим следующие типы взаимодействия:

- *Запрос* . когда вызывающей микрослужбе требуется ответ от вызываемой микрослужбы, например "Эй, дайте мне сведения о покупателе для данного идентификатора клиента".

- *Команда* — когда вызывающей микрослужбе требуется другая микрослужба для выполнения действия, но не требуется ответ, например «Эй, просто поставьте этот заказ».

- *Событие* — когда микрослужба, называемая издателем, вызывает событие, которое изменилось или произошло действие. Другие микрослужбы, называемые подписчиками, могут реагировать на событие соответствующим образом. Издатель и подписчики не знают друг о друга.

Системы микрослужб обычно используют сочетание этих типов взаимодействия при выполнении операций, требующих взаимодействия между службами. Давайте подробно рассмотрим каждую из них и то, как их можно реализовать.

## <a name="queries"></a>Запросы

Во многих случаях одной микрослужбе может потребоваться выполнить *запрос* к другой, что требует немедленного реагирования на выполнение операции. Микрослужбе корзины покупок может потребоваться информация о продукте и цена для добавления товара в корзину. Существует ряд подходов к реализации операций запросов.

### <a name="requestresponse-messaging"></a>Обмен сообщениями с запросами и ответами

Одним из вариантов реализации этого сценария является вызов микрослужбы на внутреннем сервере для выполнения прямых HTTP-запросов к микрослужбам, которые необходимо запросить, как показано на рис. 4-8.

![Прямой обмен данными по протоколу HTTP](./media/direct-http-communication.png)

**Рис. 4-8**. Прямой обмен данными по протоколу HTTP

Хотя прямые вызовы HTTP между микрослужбами относительно просты для реализации, следует соблюдать осторожность, чтобы не усложнять эту методику. Для начала эти вызовы всегда *синхронны* и будут блокировать операцию до тех пор, пока не будет возвращен результат или не истечет время ожидания запроса. Что делать, когда автономные, независимые службы, могут развиваться независимо друг от друга и развертывать их часто, теперь становятся взаимосвязанными друг с другом. При увеличении взаимосвязей между микрослужбами их архитектурные преимущества уменьшаются.

Асинхронный запрос, выполняющий один прямой вызов HTTP к другой микрослужбе, может быть приемлемым для некоторых систем. Однако не рекомендуется делать вызовы с большими объемами, которые вызывают прямые вызовы HTTP к нескольким микрослужбам. Они могут увеличить задержку и негативно сказаться на производительности, масштабируемости и доступности системы. Еще хуже, длинная последовательность прямого обмена данными по протоколу HTTP может привести к серьезным и сложным цепочкам синхронных вызовов микрослужб, показанных на рисунке 4-9:

![Сцепление HTTP-запросов](./media/chaining-http-queries.png)

**Рис. 4-9**. Сцепление HTTP-запросов

Вы наверняка можете представить риск в структуре, показанной на предыдущем изображении. Что происходит при сбое \#шага 3? Или \#8 завершается ошибкой? Как выполнить восстановление? Что если шаг \#6 замедлится из-за того, что базовая служба занята? Как продолжить? Даже если все работает правильно, подумайте о задержке этого вызова, которая является суммой задержки каждого шага.

Большая степень связывания в предыдущем образе предполагает, что службы не были оптимально смоделированы. Он направляет бы команду повторно посетить свой проект.

### <a name="materialized-view-pattern"></a>Шаблон материализованного представления

Распространенным вариантом для удаления связи микрослужб является [шаблон материализованных представлений](https://docs.microsoft.com/azure/architecture/patterns/materialized-view). В этом шаблоне микрослужба хранится собственная локальная денормализованная копия данных, принадлежащих другим службам. Вместо микрослужбы покупательской корзины, которая запрашивает Каталог продуктов и микрослужбы ценообразования, она сохраняет собственную локальную копию этих данных. Этот шаблон устраняет ненужную связь и повышает надежность и время ответа. Вся операция выполняется внутри одного процесса. Мы рассмотрим этот шаблон и другие проблемы с данными в главе 5.

### <a name="service-aggregator-pattern"></a>Шаблон агрегатора служб

Другой вариант для устранения межсерверной связи между микрослужбами — [микрослужба агрегатора](https://devblogs.microsoft.com/cesardelatorre/designing-and-implementing-api-gateways-with-ocelot-in-a-microservices-and-container-based-architecture/), как показано на рисунке 4-10.

![Служба агрегатора](./media/aggregator-service.png)

**Рис. 4-10**. Микрослужба агрегатора

Шаблон изолирует операцию, которая вызывает несколько серверных микрослужб, путем централизации ее логики в специализированной микрослужбе.  На предыдущем рисунке микрослужба агрегатора для извлечения фиолетового цвета управляет рабочим процессом для операции извлечения. Он включает вызовы нескольких серверных микрослужб в упорядоченном порядке. Данные из рабочего процесса объединяются и возвращаются вызывающему. Несмотря на то, что он по-прежнему реализует прямые вызовы HTTP, микрослужба агрегатора сокращает прямые зависимости между внутренними микрослужбами.

### <a name="requestreply-pattern"></a>Шаблон "запрос-ответ"

Другой подход к разделению синхронных HTTP-сообщений — это шаблон типа " [запрос-ответ](https://www.enterpriseintegrationpatterns.com/patterns/messaging/RequestReply.html)", который использует связь с очередями. Связь с помощью очереди всегда является односторонним каналом с тем, что производитель отправляет сообщение и получает его потребитель. При использовании этого шаблона реализуются как очередь запросов, так и очередь ответов, показанные на рисунке 4-11.

![Шаблон "запрос-ответ"](./media/request-reply-pattern.png)

**Рис. 4-11**. Шаблон "запрос-ответ"

В этом случае производитель сообщения создает сообщение на основе запроса, которое содержит уникальный идентификатор корреляции и помещает его в очередь запросов. Служба, использующая службу, выводит сообщения из очереди, обрабатывает их и помещает ответ в очередь ответов с тем же ИДЕНТИФИКАТОРом корреляции. Служба Producer выводит сообщение из очереди, сопоставляет его с ИДЕНТИФИКАТОРом корреляции и возобновляет обработку. Мы подробно рассмотрим очереди в следующем разделе.

## <a name="commands"></a>Команды

Другим типом взаимодействия является *команда*. Микрослужбе может потребоваться другая микрослужба для выполнения действия. Микрослужбе заказа может потребоваться микрослужба доставки для создания отгрузки для утвержденного заказа. На рис. 4-12 одна микрослужба, называемая производителем, отправляет сообщение другой микрослужбе, потребителю, что делает что-то.

![Взаимодействие команд с очередью](./media/command-interaction-with-queue.png)

**Рис. 4-12**. Взаимодействие команд с очередью

Чаще всего производителю не требуется ответ, и он может *запустить и забыть* сообщение. Если требуется ответ, потребитель отправляет отдельное сообщение обратно в Producer на другом канале. Командное сообщение лучше отсылается асинхронно с помощью очереди сообщений. поддерживается облегченным посредником сообщений. На предыдущей схеме Обратите внимание на то, как очередь разделяет и отделяет обе службы.

Очередь сообщений — это промежуточная конструкция, с помощью которой производитель и потребитель проходят сообщение. Очереди реализуют асинхронный шаблон обмена сообщениями типа "точка — точка". Производитель знает, где должна быть отправлена команда, и правильно ли они перенаправляются. Очередь гарантирует, что сообщение обрабатывается только одним из экземпляров потребителя, которые считываются из канала. В этом сценарии либо производитель, либо служба-потребитель могут масштабироваться без влияния на другую. Кроме того, технологии могут быть разными на разных сторонах, то есть у нас может быть микрослужба Java, вызывающая микрослужбу [Golang](https://golang.org) .

В главе 1 мы говорили о *резервных службах*. Резервные службы — это вспомогательные ресурсы, от которых зависят облачные системы. Очереди сообщений являются резервными службами. Облако Azure поддерживает два типа очередей сообщений, которые могут использоваться облачными системами для реализации обмена сообщениями с помощью команд: очереди службы хранилища Azure и очереди служебной шины Azure.

### <a name="azure-storage-queues"></a>Очереди службы хранилища Azure

Очереди службы хранилища Azure предлагают простую инфраструктуру очередей, которая является быстрой, доступной и поддерживается учетными записями хранения Azure.

[Очереди службы хранилища Azure](https://docs.microsoft.com/azure/storage/queues/storage-queues-introduction) — это механизм очередей на основе RESTful с надежной и устойчивой системой обмена сообщениями. Они обеспечивают минимальный набор функций, но представляют собой недорогие и хранят миллионы сообщений. Их емкость составляет до 500 ТБ. Размер одного сообщения может доставлять до 64 КБ.

Доступ к сообщениям можно получить из любой точки мира через вызовы с проверкой подлинности с помощью HTTP или HTTPS. Очереди службы хранилища могут масштабироваться до большого количества параллельных клиентов, чтобы справиться с нагрузками на трафик.

С другой стороны, существуют ограничения службы:

- Порядок сообщений не гарантируется.

- Сообщение может храниться только в течение семи дней, прежде чем оно будет автоматически удалено.

- Поддержка управления состоянием, обнаружения повторяющихся данных или транзакций недоступна.

На рис. 4-13 показана иерархия очереди службы хранилища Azure.

![Иерархия очередей хранилища](./media/storage-queue-hierarchy.png)

**Рис. 4-13**. Иерархия очередей хранилища

На предыдущем рисунке обратите внимание, как очереди хранилища хранят свои сообщения в базовой учетной записи хранения Azure.

Для разработчиков Корпорация Майкрософт предоставляет несколько клиентских и серверных библиотек для обработки очереди хранилища. Поддерживаются большинство основных платформ, включая .NET, Java, JavaScript, Ruby, Python и Go. Разработчики никогда не должны обмениваться данными напрямую с этими библиотеками. Это обеспечит тесное связывание кода микрослужбы с служба очередей службы хранилища Azure. Рекомендуется изолировать сведения о реализации API. Познакомьтесь с уровнем взаимодействий или промежуточным API, который предоставляет универсальные операции и инкапсулирует конкретную библиотеку. Эта слабая связь позволяет переключать одну службу очереди на другую без внесения изменений в код службы магистрали.

Очереди службы хранилища Azure — это экономичный вариант для реализации обмена сообщениями в собственных облачных приложениях. Особенно если размер очереди превысит 80 ГБ, а простой набор функций приемлем. Вы платите только за хранение сообщений; нет фиксированной почасовой оплаты.

### <a name="azure-service-bus-queues"></a>Очереди служебной шины Azure

Для более сложных требований к обмену сообщениями рекомендуется использовать очереди служебной шины Azure.

В рамках надежной инфраструктуры сообщений [служебная шина Azure](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-messaging-overview) поддерживает *модель обмена сообщениями через брокер*. Сообщения надежно хранятся в брокере (очереди) до получения потребителем. Очередь гарантирует доставку сообщений по принципу "первым поступил/первым обслужен" (FIFO), учитывающую порядок добавления сообщений в очередь.

Размер сообщения может быть намного больше, до 256 КБ. Сообщения сохраняются в очереди в течение неограниченного периода времени. Служебная шина поддерживает не только вызовы на основе HTTP, но и обеспечивает полную поддержку [протокола AMQP](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-amqp-overview). AMQP — это открытый стандарт для поставщиков, поддерживающих двоичный протокол и более высокий уровень надежности.

Служебная шина предоставляет широкий набор функций, включая [поддержку транзакций](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-transactions) и [функцию обнаружения дубликатов](https://docs.microsoft.com/azure/service-bus-messaging/duplicate-detection). Очередь гарантирует "не более одной доставки" на каждое сообщение. Оно автоматически удаляет сообщение, которое уже было отправлено. Если производитель сомнительен, он может повторно отправить то же сообщение, а служебная шина гарантирует, что будет обработана только одна копия. Обнаружение дубликатов освобождает вас от необходимости создавать дополнительные коммуникации по инфраструктуре.

Два других корпоративных компонента — это секционирование и сеансы. Обычная очередь служебной шины обрабатывается одним посредником сообщений и хранится в одном хранилище сообщений. Однако [секционирование служебной шины](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-partitioning) распределяет очередь между несколькими брокерами сообщений и хранилищами сообщений. Общая пропускная способность больше не ограничивается производительностью одного брокера сообщений или хранилища сообщений. Временное отключение хранилища сообщений не приводит к недоступности секционированной очереди.

[Сеансы служебной шины](https://codingcanvas.com/azure-service-bus-sessions/) предоставляют возможность группирования сообщений, связанных с группировкой. Представьте себе сценарий рабочего процесса, в котором сообщения должны обрабатываться вместе, а операция завершилась в конце. Чтобы воспользоваться преимуществами, необходимо явно включить сеансы для очереди, а каждое связанное с ним сообщение должно содержать один и тот же идентификатор сеанса.

Однако существуют некоторые важные предостережения: размер очередей служебной шины ограничен 80 ГБ, что намного меньше, чем доступно из очередей хранилища. Кроме того, очереди служебной шины имеют базовую стоимость и плату за операцию.

На рис. 4-14 показано высокоуровневая архитектура очереди служебной шины.

![Очередь служебной шины](./media/service-bus-queue.png)

**Рис. 4-14**. Очередь служебной шины

На предыдущем рисунке обратите внимание на связь «точка-точка». Два экземпляра одного поставщика постановку сообщения в одну очередь служебной шины. Каждое сообщение потребляется только одним из трех экземпляров потребителей справа. Далее мы обсудим, как реализовать обмен сообщениями, когда разным потребителям может быть интересно одно и то же сообщение.

## <a name="events"></a>События

Очередь сообщений — это эффективный способ реализации взаимодействия, когда производитель может асинхронно отправить сообщение потребителю. Но что происходит, когда *много различных потребителей* интересуют одно и то же сообщение? Выделенная очередь сообщений для каждого потребителя не масштабируется хорошо, а управление становится затруднительным.

Для решения этой ситуации мы перейдем к третьему типу взаимодействия сообщений, *событию*. Одна микрослужба объявляет о том, что произошло действие. Другие микрослужбы, если интересно, реагируют на действие или событие.

Процесс обработки событий состоит из двух этапов. Для данного изменения состояния микрослужба публикует событие в брокере сообщений, делая его доступным для любой другой заинтересованной микрослужбы. Заинтересованная микрослужба получает уведомление от подписки на событие в брокере сообщений. Для реализации [взаимодействия на основе событий](https://docs.microsoft.com/dotnet/standard/microservices-architecture/multi-container-microservice-net-applications/integration-event-based-microservice-communications)используется шаблон [публикации или подписки](https://docs.microsoft.com/azure/architecture/patterns/publisher-subscriber) .

На рис. 4-15 показана микрослужба корзины покупок, публикующая событие с двумя другими микрослужбами, подписавшими на нее.

![Обмен сообщениями на основе событий](./media/event-driven-messaging.png)

**Рис. 4-15**. Обмен сообщениями на основе событий

Обратите внимание на компонент *шины событий* , расположенный в середине коммуникационного канала. Это пользовательский класс, который инкапсулирует брокер сообщений и отделяет его от базового приложения. Микрослужбы упорядочивания и инвентаризации независимо работают с событиями, не зная друг друга, а микрослужбой корзины покупок. Когда зарегистрированное событие публикуется в шине событий, оно работает над ним.

С помощью событий мы перейдем от технологии очередей к *разделам*. [Раздел](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions) похож на очередь, но поддерживает шаблон обмена сообщениями «один ко многим». Одна микрослужба публикует сообщение. При наличии нескольких подписок микрослужб можно принять это сообщение и выполнить действия. На рис. 4-16 показана архитектура раздела.

![Архитектура раздела](./media/topic-architecture.png)

**Рис. 4-16**. Архитектура раздела

На предыдущем рисунке издатели отправляют сообщения в раздел. В итоге подписчики получают сообщения из подписок. В середине раздел пересылает сообщения в подписки на основе набора *правил*, показанных в темно-синем прямоугольнике. Правила действуют в качестве фильтра, который перенаправляет определенные сообщения в подписку. Здесь событие "CreateOrder" будет отправлено в подписку \#1 и подписку \#3, но не в подписку \#2. В подписку \#2 и подписку \#3 будет отправлено событие "ордеркомплетед".

Облако Azure поддерживает два разных тематических служб: разделы служебной шины Azure и Azure EventGrid.

### <a name="azure-service-bus-topics"></a>Разделы служебной шины Azure

В основе той же надежной модели брокера сообщений для очередей служебной шины Azure входят разделы служебной [шины Azure](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions). Раздел может получать сообщения от нескольких независимых издателей и отправлять сообщения до 2 000 подписчиков. Подписки можно динамически добавлять или удалять во время выполнения без остановки системы или повторного создания раздела.

Многие расширенные возможности очередей служебной шины Azure также доступны для разделов, в том числе для [поиска повторяющихся](https://docs.microsoft.com/azure/service-bus-messaging/duplicate-detection) сообщений и [поддержки транзакций](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-transactions). По умолчанию разделы служебной шины обрабатываются одним посредником сообщений и хранятся в одном хранилище сообщений. Однако [секционирование служебной шины](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-partitioning) масштабирует раздел, распределяя его между несколькими брокерами сообщений и хранилищами сообщений.

[Запланированная доставка сообщений](https://docs.microsoft.com/azure/service-bus-messaging/message-sequencing) помечает сообщение с заданным временем для обработки. Это сообщение не будет отображаться в разделе до этого времени. [Период отсрочки сообщения](https://docs.microsoft.com/azure/service-bus-messaging/message-deferral) позволяет отложить получение сообщения на более позднее время. Оба они часто используются в сценариях обработки рабочих процессов, где операции обрабатываются в определенном порядке. Обработку полученных сообщений можно отложить до завершения предыдущей работы.

Разделы служебной шины — это надежная и проверенная технология, позволяющая обеспечить взаимодействие публикации и подписки в собственных системах в облаке.

### <a name="azure-event-grid"></a>Сетка событий Azure

Хотя служебная шина Azure — это проверенный брокер сообщений с полным набором корпоративных функций, служба " [Сетка событий Azure](https://docs.microsoft.com/azure/event-grid/overview) " — это новый ребенок в блоке.

На первый взгляд, сетка событий может выглядеть как просто другая система обмена сообщениями на основе разделов. Однако во многих отношениях он отличается. С учетом рабочих нагрузок, управляемых событиями, она обеспечивает обработку событий в реальном времени, глубокую интеграцию с Azure и инфраструктуру «открытый платформенный-все» в бессерверной инфраструктуре. Он предназначен для современных облачных и бессерверных приложений.

Как централизованная *Объединительная плата для событий*или канал, служба "Сетка событий" реагирует на события в ресурсах Azure и из собственных служб.

Уведомления о событиях публикуются в разделе сетки событий, который, в свою очередь, направляет каждое событие в подписку. Подписчики сопоставляются с подписками и используют события. Как и служебная шина, служба "Сетка событий" поддерживает *модель фильтрованного подписчика* , в которой подписка задает правило для событий, которые он хочет получить. Служба "Сетка событий" обеспечивает высокую пропускную способность с гарантией 10 000 000 событий в секунду, обеспечивающей доставку практически в реальном времени, намного больше, чем может создать служебная шина Azure.

Очень полезное место для службы "Сетка событий" — это глубокая интеграция в структуру инфраструктуры Azure. Ресурс Azure, например Cosmos DB, может публиковать встроенные события непосредственно в других заинтересованных ресурсах Azure без необходимости создавать пользовательский код. Служба "Сетка событий" может публиковать события из подписки Azure, группы ресурсов или службы, предоставляя разработчикам точный контроль над жизненным циклом облачных ресурсов. Однако служба "Сетка событий" не ограничена в Azure. Это открытая платформа, которая может использовать пользовательские HTTP-события, опубликованные из приложений или сторонних служб, и перенаправлять события внешним подписчикам.

При публикации и подписке на собственные события из ресурсов Azure не требуется писать код. С помощью простой конфигурации можно интегрировать события из одного ресурса Azure в другой, используя встроенные коммуникации для разделов и подписок. На рис. 4-17 показана структура сетки событий.

![Таблица событий Анатомия](./media/event-grid-anatomy.png)

**Рис. 4-17**. Таблица событий Анатомия

Основным различием между EventGrid и служебной шиной является основной *шаблон обмена сообщениями*.

Служебная шина реализует устаревшую *модель извлечения* в стиле, в которой подчиненный подписчик активно опрашивает подписку на раздел на предмет новых сообщений. На самом переуровне этот подход дает подписчику полный контроль над темпом обработки сообщений. Он определяет, когда и сколько сообщений должны обрабатываться в любое заданное время. Непрочитанные сообщения остаются в подписке до обработки. Серьезным недостатком является задержка между временем создания события и операцией опроса, которая извлекает это сообщение подписчику для обработки. Кроме того, затраты на постоянный опрос для следующего события потребляют ресурсы и деньги.

Однако EventGrid отличается. Он реализует *модель отправки* , в которой события отправляются в евенсандлерс как полученные, что обеспечивает доставку событий почти в реальном времени. Это также сокращает затраты, так как служба активируется только в том случае, когда требуется использовать событие — не постоянно, как при опросе. С другой стороны, обработчик событий должен обрабатывать входящую нагрузку и предоставлять механизмы регулирования, чтобы защитить себя от чрезмерного увеличения. Многие службы Azure, использующие эти события, такие как функции Azure и Logic Apps, обеспечивают автоматическое Автомасштабирование для обработки повышенных нагрузок.  

Служба "Сетка событий" является полностью управляемой облачной службой. Он динамически масштабируется на основе трафика и оплачивается только для фактического использования, а не предварительно приобретенной емкости. Первые 100 000 операций в месяц — это операции, которые определяются как исходящие события (входящие уведомления о событиях), попытки доставки подписки, вызовы управления и фильтрация по субъекту. Благодаря 99,99% доступности EventGrid гарантирует доставку события в течение 24-часового периода, используя встроенные функции повтора для неудачной доставки. Недоставленные сообщения можно переместить в очередь недоставленных сообщений для разрешения.  В отличие от служебной шины Azure, служба "Сетка событий" настроена на высокую производительность и не поддерживает такие функции, как упорядоченные сообщения, транзакции и сеансы.

### <a name="streaming-messages-in-the-azure-cloud"></a>Потоковая передача сообщений в облаке Azure

Служебная шина Azure и служба "Сетка событий" обеспечивают отличную поддержку для приложений, которые предоставляют отдельные дискретные события, такие как новый документ, в Cosmos DB. Но что делать, если ваша облачная система должна обработать *поток связанных событий*? [Потоки событий](https://docs.microsoft.com/archive/msdn-magazine/2015/february/microsoft-azure-the-rise-of-event-stream-oriented-systems) более сложны. Обычно они упорядочены по времени, взаимосвязаны и должны обрабатываться как группа.

[Концентратор событий Azure](https://azure.microsoft.com/services/event-hubs/) — это платформа потоковой передачи данных и служба приема событий, которая собирает, преобразует и хранит события. Она настроена для сбора данных потоковой передачи, таких как уведомления о непрерывных событиях, созданные из контекста телеметрии. Служба обладает высокой степенью масштабируемости и может хранить и [обрабатывать миллионы событий в секунду](https://docs.microsoft.com/azure/event-hubs/event-hubs-about). Как показано на рисунке 4-18, это часто первая дверца для конвейера событий, которая разсопряжена с приемом потока от потребления событий.

![концентратору событий Azure](./media/azure-event-hub.png)

**Рис. 4-18**. концентратору событий Azure

Концентратор событий поддерживает низкую задержку и настраиваемое хранение времени. В отличие от очередей и разделов, концентраторы событий сохраняют данные событий после их считывания потребителем. Эта функция позволяет другим службам аналитики данных, как внутренним, так и внешним, воспроизводить данные для дальнейшего анализа. События, хранящиеся в концентраторе событий, удаляются только по истечении срока хранения, который по умолчанию является одним днем, но настраивается.

Концентратор событий поддерживает общие протоколы публикации событий, включая HTTPS и AMQP. Он также поддерживает Kafka 1,0. [Существующие приложения Kafka могут взаимодействовать с концентратором событий](https://docs.microsoft.com/azure/event-hubs/event-hubs-for-kafka-ecosystem-overview) с помощью протокола Kafka, предоставляющего альтернативу управлению крупными кластерами Kafka. Многие облачные системы с открытым исходным кодом включают Kafka.

Концентраторы событий реализуют потоковую передачу сообщений через [модель секционированных потребителей](https://docs.microsoft.com/azure/event-hubs/event-hubs-features) , в которой каждый потребитель считывает только определенное подмножество или секцию потока сообщений. Это позволяет получить непревзойденные преимущества горизонтального масштабирования для обработки событий и другие ориентированные на работу с потоками функции, недоступные в очередях и разделах. Секция — это упорядоченная последовательность событий, хранящаяся в концентраторе событий. По мере поступления новых событий они добавляются в конец этой последовательности.На рис. 4-19 показано секционирование в концентраторе событий.

![Секционирование концентратора событий](./media/event-hub-partitioning.png)

**Рис. 4-19**. Секционирование концентратора событий

Вместо того чтобы считывать данные из одного и того же ресурса, каждая группа потребителей считывает данные из подмножества или секции потока сообщений.

Для облачных приложений, которые должны выполнять потоковую передачу большого количества событий, концентратор событий Azure может быть надежным и доступным решением.

>[!div class="step-by-step"]
>[Назад](front-end-communication.md)
>[Вперед](grpc.md)
