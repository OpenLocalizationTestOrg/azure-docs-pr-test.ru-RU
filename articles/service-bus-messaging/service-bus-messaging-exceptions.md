---
title: "исключения обмена сообщениями Service Bus aaaAzure | Документы Microsoft"
description: "Список исключений обмена сообщениями служебной шины и предлагаемые действия."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3d8526fe-6e47-4119-9f3e-c56d916a98f9
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/06/2017
ms.author: sethm
ms.openlocfilehash: 0a206b7bbc808c1190044c1dfd6ffd47b9d454fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-messaging-exceptions"></a>Исключения обмена сообщениями служебной шины
В этой статье перечислены некоторые исключения, создаваемые Microsoft Azure Service Bus hello интерфейсы API обмена сообщениями. Эта ссылка toochange субъекта, поэтому следите за обновлениями.

## <a name="exception-categories"></a>Категории исключений
Hello API обмена сообщениями создают исключения, которые можно делятся на следующие категории hello, вместе с hello связанные действия может занять tootry toofix их. Обратите внимание, что значение hello и причины исключения могут различаться в зависимости от типа hello сущности обмена сообщениями (очередей и разделов или концентраторов событий).

1. Ошибка в коде пользователя ([System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx)). Общие действия: попробуйте использовать код toofix hello, прежде чем продолжить.
2. Ошибка настройки или конфигурации ([Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception), [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx)). Общее действие: проверьте конфигурацию и измените ее при необходимости.
3. Временные исключения ([Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception), [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception)). Общие действия: повторите операцию hello, или уведомить пользователей.
4. Другие исключения ([System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx), [Microsoft.ServiceBus.Messaging.MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception), [Microsoft.ServiceBus.Messaging.SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception)). Общие действия: тип исключения определенных toohello; см. таблицу toohello в следующем разделе hello. 

## <a name="exception-types"></a>Типы исключений
Hello следующей таблице перечислены типы исключений обмена сообщениями и причины и предлагаемое действие заметки, которые можно предпринять.

| **Тип исключения** | **Описание, причина, примеры** | **Рекомендуемое действие** | **Примечание к автоматическому или немедленному повтору** |
| --- | --- | --- | --- |
| [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Hello сервер не ответил toohello запросил операцию в hello указанного времени, которая управляется [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout). завершена Hello server hello запрошенную операцию. Это может произойти из-за toonetwork или других задержек. |Проверьте состояние системы hello для обеспечения согласованности и повторите при необходимости. Ознакомьтесь с разделом [Исключения времени ожидания](#timeoutexception). |Повторите попытку могут помочь в некоторых случаях; Добавьте toocode логику повторных попыток. |
| [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Hello указанного пользователя операция не разрешена в hello server или службе. См. сообщение об исключении hello подробные сведения. Например [завершить](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) создаст это исключение, если было получено сообщение hello в [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) режим. |Проверка кода hello и документации hello. Убедитесь, что операция является допустимой запросил hello. |Повторная попытка не поможет. |
| [OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Попытка сделать tooinvoke операцию на объекте, который уже закрыт, прервана или удален. В редких случаях hello внешняя транзакция уже удален. |Проверка кода hello и убедитесь, что он не вызывает операции над удаленным объектом. |Повторная попытка не поможет. |
| [UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) объекта не удалось получить маркер, маркер hello является недопустимым или hello маркер не содержит необходимые tooperform hello hello утверждения операции. |Убедитесь, что поставщик маркеров hello создается с правильными значениями hello. Проверьте конфигурацию hello hello служба управления доступом. |Повторите попытку могут помочь в некоторых случаях; Добавьте toocode логику повторных попыток. |
| [ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [ArgumentNullException](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[ArgumentOutOfRangeException](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Один или несколько метод toohello аргументов являются недопустимыми.<br /> Hello URI, указанный слишком[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) или [создать](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) содержит путь сегментами.<br /> Схема URI Hello указано слишком[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) или [создать](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) является недопустимым. <br />значение свойства Hello не должен превышать 32 КБ. |Проверьте вызывающего кода hello и убедитесь, что hello аргументы заданы правильно. |Повторная попытка не поможет. |
| [MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception) |Сущности, связанной с операцией hello не существует или был удален. |Убедитесь, что существует сущность hello. |Повторная попытка не поможет. |
| [MessageNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagenotfoundexception) |Попробуйте tooreceive сообщение с номером определенной последовательности. Это сообщение не найдено. |Убедитесь, что уже не было получено сообщение hello. Если сообщение hello было считается недоставленным, проверьте toosee очереди недоставленных сообщений hello. |Повторная попытка не поможет. |
| [MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception) |Клиент не может tooestablish tooService соединений шины. |Убедитесь, что предоставленный hello имени узла и hello узел доступен. |Повторная попытка может помочь при наличии периодических сбоев подключения. |
| [ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) |Служба не может tooprocess hello запрос в настоящее время. |Клиент может ожидать в течение заданного времени, затем повторите операцию hello. |Клиент может повторить операцию через определенный промежуток времени. Если в результате повтора возникает другое исключение, проверьте поведение повтора этого исключения. |
| [MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception) |Маркер блокировки, связанный с приветственное сообщение уже истек, или маркер блокировки hello не найден. |Удалите сообщение hello. |Повторная попытка не поможет. |
| [SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception) |Потеряна блокировка, связанная с данным сеансом. |Прервать hello [MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession) объекта. |Повторная попытка не поможет. |
| [MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception) |Универсальное исключение, которое может быть создано в следующих случаях hello обмена сообщениями:<br /> Попытка toocreate [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) используя имя или путь, к которому относится тип tooa другой сущности (например, раздел).<br />  Попытка сделать сообщение, toosend, размер которых превышает 256 КБ. Hello сервером или службой произошла ошибка при обработке запроса hello. Сообщение об исключении hello Дополнительные сведения см. Как правило, это временное исключение. |Проверка кода hello и убедитесь, что только сериализуемые объекты используются для текста сообщения hello или использование настраиваемого сериализатора. Документации hello hello поддерживается типы значений свойства hello и только поддерживаемые типы использования. Проверьте hello [IsTransient](/dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient) свойство. Если это **true**, можно повторить операцию hello. |Алгоритм поведения не определен и может не помочь. |
| [MessagingEntityAlreadyExistsException](/dotnet/api/microsoft.servicebus.messaging.messagingentityalreadyexistsexception) |Попробуйте toocreate сущность с именем, которое уже используется другой сущности в этом пространстве имен службы. |Удалите существующую сущность hello или выберите другое имя для создания toobe сущности hello. |Повторная попытка не поможет. |
| [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |Hello сущности обмена сообщениями был достигнут максимальный допустимый размер или превышено максимальное число подключений tooa имен hello. |Создайте место в сущности hello, прием сообщений от сущности hello или его вложенные очереди. Ознакомьтесь с разделом [Исключение QuotaExceededException](#quotaexceededexception). |Повторных попыток может помочь, если сообщения были удалены в hello это время. |
| [RuleActionException](/dotnet/api/microsoft.servicebus.messaging.ruleactionexception) |Service Bus возвращает это исключение при попытке toocreate действие недопустимое правило. Service Bus присоединяет это сообщение считается недоставленным tooa исключение при возникновении ошибки во время обработки hello действие правила по этому сообщению. |Проверьте действие hello правила для определения правильности. |Повторная попытка не поможет. |
| [FilterException](/dotnet/api/microsoft.servicebus.messaging.filterexception) |Service Bus возвращает это исключение при попытке toocreate недопустимый фильтр. Service Bus присоединяет это сообщение считается недоставленным tooa исключение, если произошла ошибка при обработке фильтра hello для сообщения. |Фильтр hello проверку правильности. |Повторная попытка не поможет. |
| [SessionCannotBeLockedException](/dotnet/api/microsoft.servicebus.messaging.sessioncannotbelockedexception) |Попробуйте tooaccept, сеанса с Идентификатором сеанса, но сеанс hello заблокирован другим клиентом. |Убедитесь, что сеанс hello разблокируется другими клиентами. |Повторных попыток может помочь, если выпустила сеанса hello в промежуточный hello. |
| [TransactionSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.transactionsizeexceededexception) |Слишком много операций являются частью транзакции hello. |Сократите число hello операций, которые являются частью этой транзакции. |Повторная попытка не поможет. |
| [MessagingEntityDisabledException](/dotnet/api/microsoft.servicebus.messaging.messagingentitydisabledexception) |Выполнен запрос на операцию среды выполнения с отключенной сущностью. |Активация сущности hello. |Повторных попыток может помочь, если активирована hello сущности в промежуточный hello. |
| [NoMatchingSubscriptionException](/dotnet/api/microsoft.servicebus.messaging.nomatchingsubscriptionexception) |Service Bus возвращает это исключение при отправке сообщения раздела tooa, предварительная фильтрация включена, и ни один из фильтров hello соответствует. |Убедитесь, что соответствует по меньшей мере один фильтр. |Повторная попытка не поможет. |
| [MessageSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) |Полезные данные сообщения превышает 256 КБ hello. Обратите внимание, что этот предел hello 256 КБ — hello общий размер сообщений, который может включать свойства системы и служебных данных .NET. |Уменьшить размер полезных данных сообщения hello hello, а затем повторите операцию hello. |Повторная попытка не поможет. |
| [TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx) |Здравствуйте, внешнюю транзакцию (*Transaction.Current*) является недопустимым. Возможно, она завершена или прервана. Дополнительные сведения можно найти во внутреннем исключении. | |Повторная попытка не поможет. |
| [TransactionInDoubtException](https://msdn.microsoft.com/library/system.transactions.transactionindoubtexception.aspx) |Попытка выполнить операцию в транзакции, которая находится в состоянии, или попытка toocommit hello транзакции и становится hello транзакций под сомнением. |Приложение должно обрабатывать это исключение (как особый случай), как транзакция hello уже были зафиксированы. |- |

## <a name="quotaexceededexception"></a>QuotaExceededException
[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) указывает на превышение квоты для конкретного объекта.

### <a name="queues-and-topics"></a>Очереди и разделы
Для очередей и разделов часто это hello размер очереди hello. свойства сообщения Hello ошибок будет содержать подробные сведения, как следующий пример hello:

```
Microsoft.ServiceBus.Messaging.QuotaExceededException
Message: hello maximum entity size has been reached or exceeded for Topic: ‘xxx-xxx-xxx’. 
    Size of entity in bytes:1073742326, Max entity size in bytes:
1073741824..TrackingId:xxxxxxxxxxxxxxxxxxxxxxxxxx, TimeStamp:3/15/2013 7:50:18 AM
```

приветственное сообщение подтверждает, что эту статью hello Превышен предельный размер case 1 ГБ (hello предельный размер по умолчанию). 

### <a name="namespaces"></a>Пространства имен

Для пространств имен [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) можно указать, что приложение превысил максимальное количество подключений tooa имен hello. Например:

```
Microsoft.ServiceBus.Messaging.QuotaExceededException: ConnectionsQuotaExceeded for namespace xxx.
<tracking-id-guid>_G12 ---> 
System.ServiceModel.FaultException`1[System.ServiceModel.ExceptionDetail]: 
ConnectionsQuotaExceeded for namespace xxx.
```

#### <a name="common-causes"></a>Основные причины
Существуют две распространенные причины этой ошибки: hello очереди недоставленных сообщений и сбою получателей сообщений.

1. **Очередь недоставленных сообщений** читатель произошел сбой toocomplete сообщений и сообщений hello возвращаются toohello очереди или раздела, когда заканчивается срок действия блокировки hello. Это может произойти, если hello чтения встречает исключение, которое позволяет избежать вызова [BrokeredMessage.Complete](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.brokeredmessage.complete.aspx). После 10 попыток считывания сообщения, он перемещает toohello очередь недоставленных сообщений по умолчанию. Это поведение управляется hello [QueueDescription.MaxDeliveryCount](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queuedescription.maxdeliverycount.aspx) свойство и значение по умолчанию 10. Как сообщения накапливаться в очереди недоставленных сообщений hello, занимаемое ими пространство.
   
    проблема tooresolve hello, чтения и полным hello сообщения из очереди недоставленных сообщений hello, как вы, как и из любой другой очереди. Hello [QueueClient](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queueclient.aspx) класс даже содержит [FormatDeadLetterPath](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queueclient.formatdeadletterpath.aspx) путь к очереди недоставленных сообщений hello метод toohelp формат.
2. **Остановить получателя** приемником остановлена получение сообщений из очереди или подписки. Здравствуйте, tooidentify способом это toolook в hello [QueueDescription.MessageCountDetails](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.queuedescription.messagecountdetails.aspx) свойство, которое показывает полный подразделение hello сообщений hello. Если hello [ActiveMessageCount](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.messagecountdetails.activemessagecount.aspx) свойство большими или очень растущей, а затем быстрое время записываемого не во время чтения сообщений hello.

### <a name="event-hubs"></a>Концентраторы событий
Концентраторы событий имеют ограничение в 20 групп потребителей на один концентратор событий. Появляется при попытке дополнительные toocreate [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception). 

## <a name="timeoutexception"></a>TimeoutException
Объект [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) указывает инициированную пользователем операцию занимает больше времени, чем операции hello. 

Следует проверить значение hello hello [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit) свойство как попадание это ограничение также может привести к [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx).

### <a name="queues-and-topics"></a>Очереди и разделы
Для очередей и разделов, указано время ожидания hello в hello [MessagingFactorySettings.OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout) свойства, как часть строки соединения hello или через [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). само сообщение Hello ошибки могут быть различными, но он всегда содержит значение времени ожидания hello hello текущей операции. 

### <a name="event-hubs"></a>Концентраторы событий
Для концентраторов событий hello времени ожидания должно быть указано как часть строки соединения hello или через [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). само сообщение Hello ошибки могут быть различными, но он всегда содержит значение времени ожидания hello hello текущей операции. 

### <a name="common-causes"></a>Основные причины
Существует две основные причины этой ошибки: неправильная конфигурация или временная ошибка службы.

1. **Неправильная конфигурация** hello время ожидания операции может оказаться слишком маленьким для hello рабочее состояние. значение по умолчанию Hello времени ожидания операции hello в пакет SDK для клиента hello составляет 60 секунд. Проверка toosee, если код имеет значение hello установки toosomething слишком мал. Обратите внимание, это условие hello hello сети и ЦП может повлиять на hello время, необходимое для toocomplete конкретной операции, поэтому не следует задавать время ожидания операции hello tooa очень маленькое значение.
2. **Временная ошибка** иногда hello службы шины обслуживания можно возникают задержки при обработке запросов, например во время периодов с большим трафиком. В таких случаях можно повторите операцию через некоторое время, вплоть до завершения операции hello. Hello же операция по-прежнему не удается после нескольких попыток, обращайтесь hello [состояние узла службы Azure](https://azure.microsoft.com/status/) toosee в случае сбоев любого известной службы.

## <a name="next-steps"></a>Дальнейшие действия

Hello полный Справочник по API .NET служебной шины, в разделе hello [Справочник по Azure .NET API](/dotnet/api/overview/azure/servicebus).

Дополнительные сведения о toolearn [Service Bus](https://azure.microsoft.com/services/service-bus/), см. следующие разделы hello.

* [Основные сведения об обмене сообщениями через служебную шину](service-bus-messaging-overview.md)
* [Базовая информация о служебной шине](service-bus-fundamentals-hybrid-solutions.md)
* [Архитектура служебной шины](service-bus-architecture.md)

