---
title: "Концентраторы событий aaaAzure исключения при обмене сообщениями | Документы Microsoft"
description: "Список исключений обмена сообщениями концентраторов событий и предлагаемые действия."
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 2c6273de-0106-47e5-b45d-59040e51f2c5
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 9c164e76612c26607219f08407f689aaab4050a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-messaging-exceptions"></a>Исключения обмена сообщениями концентраторов событий
В этой статье перечислены некоторые hello исключения, создаваемые hello Azure Service Bus обмена сообщениями API-интерфейсы, включающие концентраторов событий. Эта ссылка toochange субъекта, поэтому следите за обновлениями.

## <a name="exception-categories"></a>Категории исключений
Hello API-интерфейсов концентраторы событий создания исключения, которые можно делятся на следующие категории hello, вместе с hello связанные действия могут занять tootry toofix их.

1. Ошибка в коде пользователя: [System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx). Общие действия: попробуйте использовать код toofix hello, прежде чем продолжить.
2. Ошибка настройки или конфигурации: [Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception), [Microsoft.Azure.EventHubs.MessagingEntityNotFoundException](/dotnet/api/microsoft.azure.eventhubs.messagingentitynotfoundexception), [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). Общее действие: проверьте конфигурацию и измените ее при необходимости.
3. Временные исключения: [Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](#serverbusyexception), [Microsoft.Azure.EventHubs.ServerBusyException](#serverbusyexception), [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception). Общие действия: повторите операцию hello, или уведомить пользователей.
4. Другие исключения: [System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](#timeoutexception), [Microsoft.ServiceBus.Messaging.MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception), [Microsoft.ServiceBus.Messaging.SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception). Общие действия: тип исключения определенных toohello; см. таблицу toohello в следующем разделе hello. 

## <a name="exception-types"></a>Типы исключений
Hello следующей таблице перечислены типы исключений обмена сообщениями и причины и предлагаемое действие заметки, которые можно предпринять.

| **Тип исключения** | **Описание, причина, примеры** | **Рекомендуемое действие** | **Примечание к автоматическому или немедленному повтору** |
| --- | --- | --- | --- |
| [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Hello сервер не ответил toohello запросил операцию в hello указанного времени, которая управляется [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout). завершена Hello server hello запрошенную операцию. Это может произойти из-за toonetwork или других задержек. |Проверьте состояние системы hello для обеспечения согласованности и повторите при необходимости.<br /> Ознакомьтесь с разделом [TimeoutException](#timeoutexception). |Повторите попытку могут помочь в некоторых случаях; Добавьте toocode логику повторных попыток. |
| [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Hello указанного пользователя операция не разрешена в hello server или службе. См. сообщение об исключении hello подробные сведения. Например [завершить](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) создает это исключение, если было получено сообщение hello в [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) режим. |Проверка кода hello и документации hello. Убедитесь, что операция является допустимой запросил hello. |Повторная попытка не поможет. |
| [OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Попытка сделать tooinvoke операцию на объекте, который уже закрыт, прервана или удален. В редких случаях hello внешняя транзакция уже удален. |Проверка кода hello и убедитесь, что он не вызывает операции над удаленным объектом. |Повторная попытка не поможет. |
| [UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) объекта не удалось получить маркер, маркер hello является недопустимым или hello маркер не содержит необходимые tooperform hello hello утверждения операции. |Убедитесь, что поставщик маркеров hello создается с правильными значениями hello. Проверьте конфигурацию hello hello служба управления доступом. |Повторите попытку могут помочь в некоторых случаях; Добавьте toocode логику повторных попыток. |
| [ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [ArgumentNullException](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[ArgumentOutOfRangeException](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Один или несколько метод toohello аргументов являются недопустимыми. Hello URI, указанный слишком[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) или [создать](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) содержит путь сегментами. Схема URI Hello указано слишком[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) или [создать](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_Create_System_Collections_Generic_IEnumerable_System_Uri__) является недопустимым. значение свойства Hello не должен превышать 32 КБ. |Проверьте вызывающего кода hello и убедитесь, что hello аргументы заданы правильно. |Повторная попытка не поможет. |
| [Microsoft.ServiceBus.Messaging.MessagingEntityNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagingentitynotfoundexception) <br /> [Microsoft.Azure.EventHubs.MessagingEntityNotFoundException](/dotnet/api/microsoft.azure.eventhubs.messagingentitynotfoundexception) |Сущности, связанной с операцией hello не существует или был удален. |Убедитесь, что существует сущность hello. |Повторная попытка не поможет. |
| [MessageNotFoundException](/dotnet/api/microsoft.servicebus.messaging.messagenotfoundexception) |Попробуйте tooreceive сообщение с номером определенной последовательности. Это сообщение не найдено. |Убедитесь, что уже не было получено сообщение hello. Если сообщение hello было считается недоставленным, проверьте toosee очереди недоставленных сообщений hello. |Повторная попытка не поможет. |
| [MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception) |Клиент не может tooestablish tooEvent подключение концентратора. |Убедитесь, что предоставленный hello имени узла и hello узел доступен. |Повторная попытка может помочь при наличии периодических сбоев подключения. |
| [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) <br /> [Microsoft.Azure.EventHubs.ServerBusyException](/dotnet/api/microsoft.azure.eventhubs.serverbusyexception) |Служба не может tooprocess hello запрос в настоящее время. |Клиент может ожидать в течение заданного времени, затем повторите операцию hello. <br /> Ознакомьтесь с разделом [ServerBusyException](#serverbusyexception). |Клиент может повторить операцию через определенный промежуток времени. Если в результате повтора возникает другое исключение, проверьте поведение повтора этого исключения. |
| [MessageLockLostException](/dotnet/api/microsoft.servicebus.messaging.messagelocklostexception) |Маркер блокировки, связанный с приветственное сообщение уже истек, или маркер блокировки hello не найден. |Удалите сообщение hello. |Повторная попытка не поможет. |
| [SessionLockLostException](/dotnet/api/microsoft.servicebus.messaging.sessionlocklostexception) |Потеряна блокировка, связанная с данным сеансом. | Прервать hello [MessageSession](/dotnet/api/microsoft.servicebus.messaging.messagesession) объекта. |Повторная попытка не поможет. |
| [MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception) |Универсальное исключение, которое может быть создано в следующих случаях hello обмена сообщениями: попытка toocreate [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) используя имя или путь, к которому относится тип tooa другой сущности (например, раздел). Попытка сделать сообщение, toosend, размер которых превышает 256 КБ. Hello сервером или службой произошла ошибка при обработке запроса hello. Сообщение об исключении hello Дополнительные сведения см. Как правило, это временное исключение. |Проверка кода hello и убедитесь, что только сериализуемые объекты используются для текста сообщения hello или использование настраиваемого сериализатора. Документации hello hello поддерживается типы значений свойства hello и только поддерживаемые типы использования. Проверьте hello [IsTransient](/dotnet/api/microsoft.servicebus.messaging.messagingexception#Microsoft_ServiceBus_Messaging_MessagingException_IsTransient) свойство. Если это **true**, можно повторить операцию hello. |Алгоритм поведения не определен и может не помочь. |
| [MessagingEntityAlreadyExistsException](/dotnet/api/microsoft.servicebus.messaging.messagingentityalreadyexistsexception) |Попробуйте toocreate сущность с именем, которое уже используется другой сущности в этом пространстве имен службы. |Удалите существующую сущность hello или выберите другое имя для создания toobe сущности hello. |Повторная попытка не поможет. |
| [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |сущность обмена сообщениями Hello достигнуто максимально допустимое. Это может произойти, если на уровне группы-получатель уже открыт hello максимального числа приемников (который является 5). |Создайте место в сущности hello, прием сообщений от сущности hello или его вложенные очереди. <br /> Ознакомьтесь с разделом [QuotaExceededException](#quotaexceededexception). |Повторных попыток может помочь, если сообщения были удалены в hello это время. |
|  | | | |
| [SessionCannotBeLockedException](/dotnet/api/microsoft.servicebus.messaging.sessioncannotbelockedexception) |Попробуйте tooaccept, сеанса с Идентификатором сеанса, но сеанс hello заблокирован другим клиентом. |Убедитесь, что сеанс hello разблокируется другими клиентами. |Повторных попыток может помочь, если выпустила сеанса hello в промежуточный hello. |
| [TransactionSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.transactionsizeexceededexception) |Слишком много операций являются частью транзакции hello. |Сократите число hello операций, которые являются частью этой транзакции. |Повторная попытка не поможет. |
| [MessagingEntityDisabledException](/dotnet/api/microsoft.servicebus.messaging.messagingentitydisabledexception) |Выполнен запрос на операцию среды выполнения с отключенной сущностью. |Активация сущности hello. |Повторных попыток может помочь, если активирована hello сущности в промежуточный hello. |
| [Microsoft.ServiceBus.Messaging.MessageSizeExceededException](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) <br /> [Microsoft.Azure.EventHubs.MessageSizeExceededException](/dotnet/api/microsoft.azure.eventhubs.messagesizeexceededexception) | Полезные данные сообщения превышает предел hello 256 КБ. Обратите внимание, что этот предел hello 256 КБ — hello общий размер сообщений, который может включать свойства системы и служебных данных .NET. |Уменьшить размер полезных данных сообщения hello hello, а затем повторите операцию hello. |Повторная попытка не поможет. |
| [TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx) |Здравствуйте, внешнюю транзакцию (*Transaction.Current*) является недопустимым. Возможно, она завершена или прервана. Дополнительные сведения можно найти во внутреннем исключении. | |Повторная попытка не поможет. |
| [TransactionInDoubtException](https://msdn.microsoft.com/library/system.transactions.transactionindoubtexception.aspx) |Попытка выполнить операцию в транзакции, которая находится в состоянии, или попытка toocommit hello транзакции и становится hello транзакций под сомнением. |Приложение должно обрабатывать это исключение (как особый случай), как транзакция hello уже были зафиксированы. |- |

## <a name="quotaexceededexception"></a>QuotaExceededException
[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) указывает на превышение квоты для конкретного объекта.

Это может произойти, если на уровне группы-получатель уже открыт hello максимального числа приемников (5).

### <a name="event-hubs"></a>Концентраторы событий
Концентраторы событий имеют ограничение в 20 групп потребителей на один концентратор событий. Появляется при попытке дополнительные toocreate [QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception). 

## <a name="timeoutexception"></a>TimeoutException
Объект [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) указывает инициированную пользователем операцию занимает больше времени, чем операции hello. 

Для концентраторов событий hello времени ожидания должно быть указано как часть строки соединения hello или через [ServiceBusConnectionStringBuilder](/dotnet/api/microsoft.servicebus.servicebusconnectionstringbuilder). само сообщение Hello ошибки могут быть различными, но он всегда содержит значение времени ожидания hello hello текущей операции. 

### <a name="common-causes"></a>Основные причины
Существует две основные причины этой ошибки: неправильная конфигурация или временная ошибка службы.

1. **Неправильная конфигурация** hello время ожидания операции может оказаться слишком маленьким для hello рабочее состояние. значение по умолчанию Hello времени ожидания операции hello в пакет SDK для клиента hello составляет 60 секунд. Проверка toosee, если код имеет значение hello установки toosomething слишком мал. Обратите внимание, это условие hello hello сети и ЦП может повлиять на hello время, необходимое для toocomplete конкретной операции, поэтому не следует задавать время ожидания операции hello tooa очень маленькое значение.
2. **Временная ошибка** иногда hello службы концентраторов событий можно возникают задержки при обработке запросов, например во время периодов с большим трафиком. В таких случаях можно повторите операцию через некоторое время, вплоть до завершения операции hello. Hello же операция по-прежнему не удается после нескольких попыток, обращайтесь hello [состояние узла службы Azure](https://azure.microsoft.com/status/) toosee в случае сбоев любого известной службы.

## <a name="serverbusyexception"></a>ServerBusyException

[Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) или [Microsoft.Azure.EventHubs.ServerBusyException](/dotnet/api/microsoft.azure.eventhubs.serverbusyexception) указывают на то, что сервер перегружен. Для этого исключения есть два соответствующих кода ошибки.

### <a name="error-code-50002"></a>Код ошибки 50002

Эта ошибка может возникать по одной из двух причин:

1. Загрузка Hello не распределена должным образом во всех разделах на hello концентратора событий и один раздел попаданий hello локальной пропускной способности единицы ограничение.
    
    Решение: Пересмотр стратегии распространения hello секциями или попытке [EventHubClient.Send(eventDataWithOutPartitionKey)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) может помочь.

2. приветствия имен концентраторы событий не имеет достаточно единиц производительности (можно проверить hello **метрики** колонки в колонке имен концентраторов событий в hello [портал Azure](https://portal.azure.com) tooconfirm). Обратите внимание, что портал hello представлены сведения о статистических (1 минута), но измерять пропускную способность hello в режиме реального времени — это только оценка.

    Решение: Увеличить пропускную способность hello, может помочь единиц на пространство имен hello. Это можно сделать на портале hello hello **шкалы** колонке колонка имен hello концентраторов событий.

### <a name="error-code-50001"></a>Код ошибки 50001

Эта ошибка не должна возникать часто. Оно происходит, когда контейнер hello выполнение кода для пространства имен не хватает ЦП — загрузить концентраторы событий не более нескольких секунд до hello начинает балансировки.


## <a name="next-steps"></a>Дальнейшие действия
На сайте ссылкам hello, изучите более подробную концентраторов событий:

* [Обзор концентраторов событий](event-hubs-what-is-event-hubs.md)
* [Создание концентратора событий](event-hubs-create.md)
* [Часто задаваемые вопросы о концентраторах событий](event-hubs-faq.md)
