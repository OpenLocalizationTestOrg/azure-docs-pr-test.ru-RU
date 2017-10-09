---
title: "aaaCreate секционированные очереди и разделы шины службы Azure | Документы Microsoft"
description: "Описывает, как toopartition Service Bus очереди и разделы с помощью нескольких сообщений является посредником."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a0c7d5a2-4876-42cb-8344-a1fc988746e7
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;hillaryc
ms.openlocfilehash: 6d42556a0714d6a012dc319f662521c8b0bb958b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="partitioned-queues-and-topics"></a>Секционированные очереди и разделы
Azure Service Bus использует несколько сообщений tooprocess брокеры сообщений и несколько сообщений хранит сообщения toostore. Обычная очередь или раздел обрабатываются одним брокером сообщений и сохраняются в одном хранилище сообщений. Шина обслуживания *секций* включить очереди и разделы, или *сущностей обмена сообщениями*, toobe секционированы по нескольким посредникам сообщений и хранилищам сообщений. Это означает, что hello общая пропускная способность секционированной сущности больше не ограничивается hello производительностью одного брокера сообщений или хранилища обмена сообщениями. Кроме того, при возникновении временного сбоя хранилища сообщений секционированная очередь или раздел останутся доступными. Секционированные очереди и разделы могут предоставлять все расширенные функции служебной шины, в том числе поддержку транзакций и сеансов.

Сведения о внутренней организации Service Bus см. в разделе hello [архитектуры Service Bus] [ Service Bus architecture] статьи.

Секционирование включается по умолчанию при создании сущности во всех очередях и разделах на уровне обмена сообщениями "Стандартный" и "Премиум". Сущности уровня обмена сообщениями "Стандартный"можно создать без секционирования, но очереди и разделы в пространстве имен уровня "Премиум" всегда секционируются. Этот параметр невозможно отключить. 

Это не возможные toochange hello вариант на существующей очереди или раздела на уровнях Standard или Premium секционирования, можно задать только hello параметр при создании сущности hello.

## <a name="how-it-works"></a>Принцип работы

Каждая секционированная очередь или раздел состоит из нескольких фрагментов. Фрагменты хранятся в разных хранилищах сообщений и обрабатываются разными посредниками сообщений. При отправке сообщения tooa секционированной очереди или раздела Service Bus назначает tooone сообщение hello hello фрагментов. Выбор Hello случайным образом осуществляется служебной шины или можно указать с помощью ключа секции, hello отправителя.

Когда клиенту tooreceive сообщение из секционированной очереди или из секционированного раздела tooa подписки, Service Bus запрашивает все фрагменты сообщения, затем возвращает первое сообщение hello, полученный из любого hello обмена сообщениями получатель toohello хранилищ. Кэши Service Bus hello другие сообщения и возвращает их при получении дополнительных получать запросы. Получающему клиенту неизвестно о секционировании hello. Здравствуйте поведение клиента секционированной очереди или раздела (например, чтение завершение, откладывание, блокированное письмо, предварительная выборка) поведение идентичные toohello обычной сущности.

При отправке или получении сообщения из секционированной очереди или раздела не возникает никаких дополнительных затрат.

## <a name="enable-partitioning"></a>Включение секционирования

toouse секционированные очереди и разделы с Azure Service Bus использовать hello Azure SDK версии 2.2 или более поздней версии, либо указать `api-version=2013-10` в запросах HTTP.

### <a name="standard"></a>Standard

Стандартный уровень обмена сообщениями hello можно создать очереди Service Bus и разделы с размерами 1, 2, 3, 4 или 5 ГБ (по умолчанию hello составляет 1 ГБ). Секционирование включено, служебная шина создает 16 копий hello сущности (16 секции) для каждого указанного ГБ. Таким образом, при создании очереди, имеет размер в 5 ГБ, с 16 секциями hello максимальный размер очереди становится (5 \* 16) = 80 ГБ. Вы увидите hello максимальный размер секционированной очереди или раздела, просмотрев его запись в hello [портал Azure][Azure portal], в hello **Обзор** колонку для этой сущности.

### <a name="premium"></a>Premium

В пространстве имен уровня Premium можно создать очереди Service Bus и разделы с размерами 1, 2, 3, 4, 5, 10, 20, 40 или 80 ГБ (по умолчанию hello составляет 1 ГБ). Если секционирование включено по умолчанию, служебная шина создает две секции на каждую сущность. Вы увидите hello максимальный размер секционированной очереди или раздела, просмотрев его запись в hello [портал Azure][Azure portal], в hello **Обзор** колонку для этой сущности.

Дополнительные сведения о секционировании в уровня обмена сообщениями Premium hello см. в разделе [Service Bus Premium и стандартного уровней обмена сообщениями](service-bus-premium-messaging.md). 

### <a name="create-a-partitioned-entity"></a>Создание секционированной сущности

Существует несколько способов toocreate секционированной очереди или раздела. При создании hello очереди или раздела из приложения можно включить секционирование hello очередь или раздел, соответственно, параметр hello [QueueDescription.EnablePartitioning] [ QueueDescription.EnablePartitioning] или [TopicDescription.EnablePartitioning] [ TopicDescription.EnablePartitioning] свойство слишком**true**. Эти свойства должны задаваться в очередь hello hello времени или создания раздела. Как уже говорилось ранее, это невозможно, toochange на эти свойства существующей очереди или раздела. Например:

```csharp
// Create partitioned topic
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

Кроме того, можно создать секционированной очереди или раздела в hello [портал Azure] [ Azure portal] или в Visual Studio. При создании очереди или раздела на портале hello hello **включить секционирование** параметр в hello очередь или раздел **создать** колонке включен по умолчанию. Можно только отключить этот параметр в стандартном уровне сущности; в hello секционирование уровня Premium всегда включен. В Visual Studio щелкните hello **включить секционирование** флажок в hello **новую очередь** или **новый раздел** диалоговое окно.

## <a name="use-of-partition-keys"></a>Использование ключей секции
Когда сообщение помещается в секционированные очередь или раздел, Service Bus проверяет hello наличие ключа секционирования. Если найден, он выбирает hello фрагмент на основе такого ключа. Если не удается найти ключ раздела, он выбирает hello фрагмент на основе внутреннего алгоритма.

### <a name="using-a-partition-key"></a>Использование ключа секции
Некоторые сценарии, такие как сеансы или транзакции, требуется toobe сообщений, хранимых в определенных фрагментах. Эти сценарии необходимо использовать hello ключ раздела. Все сообщения, используйте hello, одинаковым ключом секции назначаются toohello же фрагмента. Если hello фрагмент временно недоступен, Service Bus возвращает ошибку.

В зависимости от сценария hello в качестве ключа секционирования используются различные свойства сообщения:

**SessionId**: Если в сообщении имеется hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] свойство задано, то Service Bus использует это свойство в качестве ключа секции hello. Таким образом, все сообщения, которые принадлежат toohello того же сеанса, обрабатываются hello же посредником сообщения. Благодаря этому сообщения tooguarantee Service Bus, порядок и согласованность состояний сеанса hello.

**PartitionKey**: Если в сообщении имеется hello [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] свойство, но не hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] свойство задано, то Service Bus использует hello [PartitionKey] [ PartitionKey] свойство в качестве ключа секции hello. Если сообщение hello имеет оба hello [SessionId] [ SessionId] и hello [PartitionKey] [ PartitionKey] набором свойств, оба свойства должны совпадать. Если hello [PartitionKey] [ PartitionKey] свойству tooa отличается от hello [SessionId] [ SessionId] свойство Service Bus возвращает недопустимый исключение, вызванное операции. Hello [PartitionKey] [ PartitionKey] свойство должно использоваться, если отправитель посылает транзактные сообщения вне сеанса. Hello ключ секционирования гарантирует, что все сообщения, отправленные в транзакции обрабатываются hello же брокера обмена сообщениями.

**Код (ID)**: Если hello очередь или раздел имеют hello [QueueDescription.RequiresDuplicateDetection] [ QueueDescription.RequiresDuplicateDetection] значение свойства слишком**true** и hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] или [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] свойства не заданы, то hello [BrokeredMessage.MessageId] [ BrokeredMessage.MessageId] служит в качестве ключа секции hello. (Обратите внимание, что hello библиотек Microsoft .NET и AMQP автоматически назначают идентификатор сообщения, если не делает отправляющее приложение hello). В этом случае все копии одного сообщения обрабатываются hello hello одним посредником сообщения. Это позволяет toodetect Service Bus и удалить дублирующие сообщения. Если hello [QueueDescription.RequiresDuplicateDetection] [ QueueDescription.RequiresDuplicateDetection] свойство не задано слишком**true**, Service Bus не учитывает hello [MessageId] [ MessageId] свойство в качестве ключа секции.

### <a name="not-using-a-partition-key"></a>Неиспользование ключа секции
В отсутствие hello ключа секционирования Service Bus распределяет сообщения фрагментами hello циклического перебора tooall hello секционированной очереди или раздела. Если hello выбранный фрагмент недоступен, Service Bus назначает hello сообщение tooa другой фрагмент. В этом случае hello операция отправки завершается успешно, несмотря hello Временная недоступность хранилища обмена сообщениями. Тем не менее не произойдет hello гарантированное упорядочивание, предоставляет ключ раздела.

Подробное обсуждение hello компромисс между доступностью (нет ключа секции) и согласованности (с помощью ключа секции) см. в разделе [в этой статье](../event-hubs/event-hubs-availability-and-consistency.md). Эти сведения относятся одинаково toopartitioned сущностей служебной шины и разделов концентраторов событий.

toogive службы шины сообщение hello tooenqueue достаточное количество времени в другом фрагменте hello [MessagingFactorySettings.OperationTimeout] [ MessagingFactorySettings.OperationTimeout] значения, указанного в hello клиента, который отправляет сообщение hello должно быть больше 15 секунд. Рекомендуется установить hello [OperationTimeout] [ OperationTimeout] свойство toohello значение по умолчанию 60 секунд.

Обратите внимание, что ключ раздела «прикрепляет» определенному фрагменту tooa сообщение. Если хранилище сообщений hello, этим фрагментом недоступно, Service Bus возвращает ошибку. В отсутствие hello ключа секционирования Service Bus можно выбрать другой фрагмент и hello операция выполнена успешно. Поэтому рекомендуется не указывать ключ раздела, если он не является обязательным.

## <a name="advanced-topics-use-transactions-with-partitioned-entities"></a>Дополнительные разделы: использование транзакций и секционированных сущностей
Сообщения, отправленные в рамках транзакции, должны указать ключ секции. Это может быть одним из hello следующие свойства: [BrokeredMessage.SessionId][BrokeredMessage.SessionId], [BrokeredMessage.PartitionKey][BrokeredMessage.PartitionKey], или [ BrokeredMessage.MessageId][BrokeredMessage.MessageId]. Все сообщения, отправленные в рамках одной транзакции необходимо указать hello hello же ключ секционирования. При попытке toosend сообщение без ключа секции в пределах транзакции, Service Bus возвращает исключение Недопустимая операция. При попытке toosend Здравствуйте, несколько сообщений в рамках одной транзакции, имеют различные ключи разделов, Service Bus возвращает исключение Недопустимая операция. Например:

```csharp
CommittableTransaction committableTransaction = new CommittableTransaction();
using (TransactionScope ts = new TransactionScope(committableTransaction))
{
    BrokeredMessage msg = new BrokeredMessage("This is a message");
    msg.PartitionKey = "myPartitionKey";
    messageSender.Send(msg); 
    ts.Complete();
}
committableTransaction.Commit();
```

Если заданы свойства hello, которые выступают в качестве ключа секции, Service Bus ПИН-кодов hello tooa фрагмент сообщения. Это происходит независимо от того, используется ли транзакция. Рекомендуется не указывать ключ секции, если в этом нет необходимости.

## <a name="using-sessions-with-partitioned-entities"></a>Использование сеансов и секционированных сущностей
toosend с поддержкой сеансов раздела tooa транзакционного сообщения или очереди, сообщение hello должно иметь hello [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] набор свойств. Если hello [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] также задается свойство, оно должно быть идентичными toohello [SessionId] [ SessionId] свойство. Если они различаются, служебная шина возвращает исключение недопустимой операции.

В отличие от обычных очередей (несекционированного) или разделы нет возможности toouse toosend одной транзакции несколько сеансов toodifferent сообщений. Если же попытаться это сделать, служебная шина возвращает исключение недопустимой операции. Например:

```csharp
CommittableTransaction committableTransaction = new CommittableTransaction();
using (TransactionScope ts = new TransactionScope(committableTransaction))
{
    BrokeredMessage msg = new BrokeredMessage("This is a message");
    msg.SessionId = "mySession";
    messageSender.Send(msg); 
    ts.Complete();
}
committableTransaction.Commit();
```

## <a name="automatic-message-forwarding-with-partitioned-entities"></a>Автоматическая переадресация сообщений для секционированных сущностей
Служебная шина поддерживает автоматическую переадресацию сообщений в секционированные сущности, из них или между ними. hello задать автоматическую отправку, сообщений tooenable [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] свойство hello исходной очереди или подписки. Если сообщение hello указывает ключ раздела ([SessionId][SessionId], [PartitionKey][PartitionKey], или [MessageId] [ MessageId]), этот ключ секции используется для конечной сущности hello.

## <a name="considerations-and-guidelines"></a>Рекомендации и советы
* **Высокий уровень согласованности функции**: если сущность использует функции, такие как сеансы, обнаружение повторяющихся сообщений или явное управление ключ секционирования, то hello операций обмена сообщениями всегда являются фрагментами перенаправленное toospecific. Если любой из фрагментов hello столкнуться с высоким трафиком или hello базовое хранилище находится в неработоспособном состоянии, эти операции завершатся ошибкой и доступности снижается. В целом hello согласованности по-прежнему гораздо выше, чем несекционированного сущности; только часть трафика, возникают проблемы, как противоположность tooall hello трафика. Дополнительные сведения см. в этом [обсуждении доступности и целостности](../event-hubs/event-hubs-availability-and-consistency.md).
* **Управление**: операции, такие как Create, Update и Delete, которые необходимо выполнить на всех фрагментов hello объекта hello. Если какой-либо из фрагментов находится в неработоспособном состоянии, это может привести к сбою этих операций. Для операции Get hello сведения о таких, как количество сообщений должны быть собраны из всех фрагментов. Если любой фрагмент неработоспособен, состояние доступности hello сущности отображается как limited.
* **Недостаточно сценарии сообщение корпоративных**: для таких сценариев, особенно при использовании протокола hello HTTP, может иметь tooperform несколько операций получения в порядке tooobtain все сообщения hello. Для получения запросов обслуживающего hello выполняет инструкция receive на все фрагменты hello и кэширует все hello ответов, полученных. Последующие приема запроса hello одного соединения бы выиграть от этого кэширования и получения задержки будет ниже. Тем не менее при наличии нескольких подключений или использовании протокола HTTP для каждого запроса устанавливается новое подключение. Таким образом, нет никакой гарантии, что она окажется на hello того же узла. Если все существующие сообщения блокируются и кэширования данных в другой интерфейс hello получать возвращает **null**. Когда в конечном итоге срок действия сообщений истекает, их снова можно получать. Рекомендуется выполнить проверку активности HTTP.
* **Обзор и Просмотр сообщения**: [PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) не всегда возвращают hello количество сообщений, определенных в hello [MessageCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MessageCount) свойство. На это есть две причины. Одна из причин — что hello агрегированных размер hello коллекция сообщений превышает максимальный размер hello 256 КБ. Еще одна причина: Если hello очередь или раздел имеют hello [свойство параметр EnablePartitioning](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning) значение слишком**true**, секции не может иметь достаточного количества сообщений toocomplete hello запрошено количество сообщений. Как правило, если приложению требуется tooreceive определенное число сообщений, он должен вызывать [PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) несколько раз он получает это количество сообщений, или пока не дополнительные toopeek сообщений. Дополнительные сведения, включая примеры кода, см. в разделах [QueueClient.PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) или [SubscriptionClient.PeekBatch](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient#Microsoft_ServiceBus_Messaging_SubscriptionClient_PeekBatch_System_Int32_).

## <a name="latest-added-features"></a>Новые функции
* Теперь для секционированных сущностей поддерживаются операции добавления и удаления правила. В отличие от несекционированных сущностей эти операции не поддерживаются при выполнении транзакций. 
* AMQP теперь поддерживается для отправки и получения сообщений tooand от секционированную сущность.
* AMQP теперь поддерживается для следующих операций hello: [отправки пакета](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_BrokeredMessage__), [получения пакета](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_ReceiveBatch_System_Int32_), [Receive порядковом номере](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_Receive_System_Int64_), [Показать](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_Peek), [ Обновить блокировки](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_RenewMessageLock_System_Guid_), [запланировать сообщение](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_ScheduleMessageAsync_Microsoft_ServiceBus_Messaging_BrokeredMessage_System_DateTimeOffset_), [запланированные сообщения отмены](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_CancelScheduledMessageAsync_System_Int64_), [добавить правило](/dotnet/api/microsoft.servicebus.messaging.ruledescription), [удалить правило](/dotnet/api/microsoft.servicebus.messaging.ruledescription), [Блокировки обновления сеанса](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_RenewLock), [состояние сеанса набор](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_SetState_System_IO_Stream_), [состояние сеанса Get](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_GetState), и [перечислить сеансы](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_GetMessageSessionsAsync).

## <a name="partitioned-entities-limitations"></a>Ограничения секционированных сущностей
В настоящее время Service Bus налагает следующие ограничения на секционированные очереди и разделы hello:

* Секционированные очереди и разделы не поддерживают отправку сообщений, которые принадлежат toodifferent сеансы в одной транзакции.
* Service Bus в настоящее время позволяет too100 секционированных очередей или разделов на пространство имен. Каждая секционированная очередь или раздел учитывается при подсчете квоты hello 10 000 объектов на пространство имен (tooPremium уровня не применяется).

## <a name="next-steps"></a>Дальнейшие действия
См. обсуждение hello [поддержка AMQP 1.0 Service Bus секционированные очереди и разделы] [ AMQP 1.0 support for Service Bus partitioned queues and topics] toolearn Дополнительные общие сведения о секционировании сущностей обмена сообщениями. 

[Service Bus architecture]: service-bus-architecture.md
[Azure portal]: https://portal.azure.com
[QueueDescription.EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning
[TopicDescription.EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.topicdescription#Microsoft_ServiceBus_Messaging_TopicDescription_EnablePartitioning
[BrokeredMessage.SessionId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId
[BrokeredMessage.PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_PartitionKey
[SessionId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId
[PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_PartitionKey
[QueueDescription.RequiresDuplicateDetection]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_RequiresDuplicateDetection
[BrokeredMessage.MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[MessagingFactorySettings.OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[AMQP 1.0 support for Service Bus partitioned queues and topics]: service-bus-partitioned-queues-and-topics-amqp-overview.md
