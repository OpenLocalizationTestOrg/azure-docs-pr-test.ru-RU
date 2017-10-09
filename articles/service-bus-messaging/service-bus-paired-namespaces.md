---
title: "пространства имен в паре aaaAzure Service Bus | Документы Microsoft"
description: "Сведения о реализации и затратах для сопряженных пространств имен"
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 2440c8d3-ed2e-47e0-93cf-ab7fbb855d2e
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: sethm
ms.openlocfilehash: 4c44b2b95d2228e1ad8075b52634d88a1593d3b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="paired-namespace-implementation-details-and-cost-implications"></a>Сведения о реализации и финансовых затратах для сопряженных пространств имен
Hello [PairNamespaceAsync] [ PairNamespaceAsync] метод, с помощью [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] экземпляр, выполняет видимые задачи от вашего имени. Так как при использовании функции hello стоимости вопросы, бывает полезно toounderstand тех задач, чтобы ожидать поведения hello, это происходит при. Hello API использует следующие автоматическое поведение от вашего имени hello:

* Создает очереди невыполненной работы.
* Создание [MessageSender] [ MessageSender] объекта говорят tooqueues или разделы.
* Сущности обмена сообщениями становится недоступной, отправляет сообщения проверки связи toohello сущности в toodetect попытки при этой сущности снова становится доступной.
* Дополнительно создается набор «конвейеров сообщений» hello, перемещение сообщения из очередей основной toohello очередей невыполненной работы.
* Согласовывает закрытие или завершение со сбоем hello первичного и вторичного [MessagingFactory] [ MessagingFactory] экземпляров.

На высоком уровне hello функция работает следующим образом: Если hello основная сущность работоспособна, изменения поведения не происходят. Здравствуйте, когда [FailoverInterval] [ FailoverInterval] истекает период и основная сущность hello видит не отправляет успешно после непереходные [MessagingException] [ MessagingException] или [TimeoutException][TimeoutException], происходит следующая поведение hello:

1. Toohello операции отправки основной сущности отключаются, и hello системы связи hello основной сущности, пока не будет успешно доставлено проверки связи.
2. Выбирается произвольная очередь невыполненной работы.
3. [BrokeredMessage] [ BrokeredMessage] объектов, перенаправленных toohello выбрана очередь невыполненной работы.
4. Если происходит сбой toohello операции отправки, выбрана очередь невыполненной работы, эта очередь убирается из ротации hello и новая очередь. Все отправители в hello [MessagingFactory] [ MessagingFactory] экземпляр узнать hello сбоя.

Hello следующие данные описывают последовательность hello. Во-первых hello отправитель отправляет сообщения.

![Сопряженные пространства имен][0]

После сбоя toosend toohello основную очередь hello отправитель начинает отправлять сообщения tooa выбрана случайным образом очередь невыполненной работы. Одновременно он запускает задачу проверки связи.

![Сопряженные пространства имен][1]

На этом этапе сообщения hello все еще находятся в дополнительной очереди hello и не были доставлены toohello основную очередь. После hello основная очередь снова становится работоспособной, по крайней мере один процесс должен быть запущен процесс выкачивания hello. Hello выкачивания доставляет сообщения hello из различных невыполненной работы всех приветствия очереди toohello соответствующие сущности назначения (очереди и разделы).

![Сопряженные пространства имен][2]

Hello оставшейся части этого раздела обсуждаются hello определенные сведения о работе этих частей.

## <a name="creation-of-backlog-queues"></a>Создание очередей невыполненной работы
Hello [SendAvailabilityPairedNamespaceOptions] [ SendAvailabilityPairedNamespaceOptions] объекта, переданного toohello [PairNamespaceAsync] [ PairNamespaceAsync] hello указывает, метод число невыполненной работы по очереди, вы хотите toouse. Каждая очередь невыполненной работы затем создается hello следующие свойства явным образом задать (все остальные значения устанавливаются toohello [QueueDescription] [ QueueDescription] значения по умолчанию):

| Путь | [основное пространство имен]/x-servicebus-transfer/[индекс], где [индекс] — это значение в диапазоне [0, BacklogQueueCount) |
| --- | --- |
| MaxSizeInMegabytes |5120 |
| MaxDeliveryCount |int.MaxValue |
| DefaultMessageTimeToLive |TimeSpan.MaxValue |
| AutoDeleteOnIdle |TimeSpan.MaxValue |
| LockDuration |1 минута |
| EnableDeadLetteringOnMessageExpiration |Да |
| EnableBatchedOperations |Да |

Например, первая очередь невыполненной работы hello создается для пространства имен **contoso** называется `contoso/x-servicebus-transfer/0`.

При создании очереди hello, hello код сначала проверяет toosee, если такая очередь существует. Если очередь hello не существует, создается очередь hello. Код Hello не Очистка очередей невыполненной работы «дополнительному». В частности, если hello приложения с hello основного пространства имен **contoso** запрашивает пять очередей невыполненной работы, но очередь невыполненной работы по пути hello `contoso/x-servicebus-transfer/7` существует, эта дополнительная очередь по-прежнему присутствует, но не используется. Hello система явно разрешает tooexist дополнительная очереди, не будет использоваться. Владелец пространства имен hello ответственного за очистку всех неиспользуемых и нежелательных невыполненной работы очередей. Hello причину принятия этого решения является, Service Bus не знает, чего предназначены все очереди hello в пространстве имен. Кроме того Если очередь с заданным именем hello существует, но не соответствует hello предполагается, что [QueueDescription][QueueDescription], то причины не свой собственный изменение стандартного поведения hello. Гарантии не предоставляются для очередей невыполненной работы toohello изменения в коде. Убедитесь, что tootest изменения тщательно.

## <a name="custom-messagesender"></a>Пользовательский объект MessageSender
При отправке, все сообщения проходят через внутренний [MessageSender] [ MessageSender] объекта, который работает нормально, когда все работает и перенаправляет toohello очередей невыполненной работы, когда вещей «прервать.» При возникновении ошибки, которая не является временной, запускается таймер. После [TimeSpan] [ TimeSpan] период, состоящий из hello [FailoverInterval] [ FailoverInterval] значение свойства, во время которого нет успешно отправленных сообщений , запускается отработка отказа hello. На этом этапе hello выполняются следующие действия для каждой сущности.

* Выполняется задача проверки связи каждого [PingPrimaryInterval] [ PingPrimaryInterval] toocheck при наличии hello сущности. После успешного завершения этой задачи весь клиентский код, использующий hello entity немедленно начинает отправлять новые сообщения toohello основного пространства имен.
* Будущие запросы toosend toothat же сущность от любых других отправителей приведут hello [BrokeredMessage] [ BrokeredMessage] , отправляемых toobe изменить toosit в очередь невыполненной работы hello. Hello модификация удаляет некоторые свойства от hello [BrokeredMessage] [ BrokeredMessage] объекта и сохраняет их в другом месте. Hello следующие свойства удаляются и добавляются под новыми псевдонимами, позволяя Service Bus и hello сообщения SDK tooprocess одинаково:

| Старое имя свойства | Новое имя свойства |
| --- | --- |
| SessionId |x-ms-sessionid |
| TimeToLive |x-ms-timetolive |
| ScheduledEnqueueTimeUtc |x-ms-path |

Hello исходный путь назначения также сохраняется в приветственное сообщение как свойство с именем x-ms-path. Такой подход позволяет сообщениям для многих toocoexist сущности в одной очереди невыполненной работы. Hello свойства преобразуются обратно процессом выкачивания hello.

пользовательские Hello [MessageSender] [ MessageSender] объекта может столкнуться с проблемами при сообщений приближается hello 256 КБ и запускается отработка отказа. пользовательские Hello [MessageSender] [ MessageSender] объект хранит сообщения для всех очередей и разделов в очередях невыполненной работы hello вместе. Этот объект смешивает сообщения из нескольких источников вместе в очередях невыполненной работы hello. toohandle балансировку нагрузки между большое количество клиентов, которые не знают каждого других, hello SDK случайным образом выбирает одну очередь невыполненной работы для каждого [QueueClient] [ QueueClient] или [TopicClient] [ TopicClient] создается в коде.

## <a name="pings"></a>Проверка связи
Сообщение ping — это пустой [BrokeredMessage] [ BrokeredMessage] с его [ContentType] [ ContentType] свойство tooapplication/vnd.ms-servicebus-ping и [TimeToLive] [ TimeToLive] значение равно 1 секунде. Проверка связи имеет одну особенность в Service Bus: hello сервер никогда не доставляет сообщение проверки связи, когда любой вызывающий объект запрашивает [BrokeredMessage][BrokeredMessage]. Таким образом, никогда не toolearn как tooreceive и пропускать эти сообщения. Каждой сущности (уникальной очереди или раздела) на [MessagingFactory] [ MessagingFactory] экземпляр на одного клиента выполняется проверка связи, когда они считаются toobe недоступна. По умолчанию это происходит один раз в минуту. Сообщения проверки связи, считаются toobe регулярных сообщений Service Bus и может привести к расходам на полосу пропускания и сообщения. Как только hello клиенты обнаруживают, что система hello доступна, остановите сообщений hello.

## <a name="hello-syphon"></a>процесс выкачивания Hello
Процесс выкачивания hello должен активно выполнять по крайней мере один исполняемый файл в приложение hello. процесс выкачивания Hello выполняет long опроса получения, которая длится 15 минут. Когда все сущности доступны и имеется 10 очередей невыполненной работы, Здравствуйте, приложения, в котором hello процесс выкачивания вызывает hello получать операции 40 раз в час, 960 раз в день и 28 800 раз в 30 дней. Когда hello выкачивания активно перемещает сообщения из основной очереди hello невыполненной работы toohello, каждое сообщение вносятся hello, следуя расходов (на всех этапах взимается Стандартная плата за размер сообщения и пропускной способности):

1. Отправьте toohello невыполненной работы.
2. Получать от hello невыполненной работы.
3. Отправьте toohello первичной.
4. Получает от основного hello.

## <a name="closefault-behavior"></a>Поведение при закрытии или сбое
В приложении, на котором размещен процесс выкачивания hello, один раз hello первичный или вторичный [MessagingFactory] [ MessagingFactory] завершает работу с ошибкой или закрыт без его партнер ошибкой или закрывает и hello процесс выкачивания обнаруживает это состояние , процесс выкачивания hello действует. Если другие hello [MessagingFactory] [ MessagingFactory] не закрывается в течение 5 секунд hello выкачивания завершит со сбоем по-прежнему открытую hello [MessagingFactory] [ MessagingFactory] .

## <a name="next-steps"></a>Дальнейшие действия
Подробное описание асинхронного обмена сообщениями в служебной шине см. в статье [Шаблоны асинхронного обмена сообщениями и высокий уровень доступности][Asynchronous messaging patterns and high availability]. 

[PairNamespaceAsync]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_PairNamespaceAsync_Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_
[SendAvailabilityPairedNamespaceOptions]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions
[MessageSender]: /dotnet/api/microsoft.servicebus.messaging.messagesender
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[FailoverInterval]: /dotnet/api/microsoft.servicebus.messaging.pairednamespaceoptions#Microsoft_ServiceBus_Messaging_PairedNamespaceOptions_FailoverInterval
[MessagingException]: /dotnet/api/microsoft.servicebus.messaging.messagingexception
[TimeoutException]: https://msdn.microsoft.com/library/azure/system.timeoutexception.aspx
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[TimeSpan]: https://msdn.microsoft.com/library/azure/system.timespan.aspx
[PingPrimaryInterval]: /dotnet/api/microsoft.servicebus.messaging.sendavailabilitypairednamespaceoptions#Microsoft_ServiceBus_Messaging_SendAvailabilityPairedNamespaceOptions_PingPrimaryInterval
[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[TopicClient]: /dotnet/api/microsoft.servicebus.messaging.topicclient
[ContentType]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_ContentType
[TimeToLive]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive
[Asynchronous messaging patterns and high availability]: service-bus-async-messaging.md
[0]: ./media/service-bus-paired-namespaces/IC673405.png
[1]: ./media/service-bus-paired-namespaces/IC673406.png
[2]: ./media/service-bus-paired-namespaces/IC673407.png
