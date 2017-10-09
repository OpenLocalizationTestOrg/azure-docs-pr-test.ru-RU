---
title: "aaaAzure ретрансляции исключения и как tooresolve их | Документы Microsoft"
description: "Получить список исключений ретрансляции Azure и предлагаются действия может занять toohelp устраните их."
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5f9dd02c-cce0-43b3-8eb8-744f0c27f38c
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: de417c8e9e43407ef355fd44f6170cf2cdc46d6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-relay-exceptions"></a>Исключения ретранслятора Azure

В этой статье перечислены некоторые исключения, которые могут быть вызваны hello API-интерфейсов Azure ретрансляции. Эта ссылка toochange субъекта, поэтому следите за обновлениями.

## <a name="exception-categories"></a>Категории исключений

API-интерфейсы ретрансляции Hello создавать исключения, которые могут относиться к hello следующие категории. Кроме того, содержатся предлагаемые действия, которые можно предпринять toohelp resolve hello исключения.

*   **Ошибка в коде пользователя.** [System.ArgumentException](https://msdn.microsoft.com/library/system.argumentexception.aspx), [System.InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx), [System.OperationCanceledException](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx), [System.Runtime.Serialization.SerializationException](https://msdn.microsoft.com/library/system.runtime.serialization.serializationexception.aspx). 

    **Общие действия**: попробуйте использовать код hello toofix перед продолжением работы.
*   **Ошибка настройки или конфигурации.** [System.UnauthorizedAccessException](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx). 

    **Общее действие.** Проверьте конфигурацию При необходимости измените конфигурацию hello.
*   **Временные исключения.** [Microsoft.ServiceBus.Messaging.MessagingException](/dotnet/api/microsoft.servicebus.messaging.messagingexception), [Microsoft.ServiceBus.Messaging.ServerBusyException](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception), [Microsoft.ServiceBus.Messaging.MessagingCommunicationException](/dotnet/api/microsoft.servicebus.messaging.messagingcommunicationexception). 

    **Общие действия**: повторите операцию hello, или уведомить пользователей.
*   **Другие исключения.** [System.Transactions.TransactionException](https://msdn.microsoft.com/library/system.transactions.transactionexception.aspx), [System.TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx). 

    **Общие действия**: toohello конкретного типа исключения. См. таблицу hello в следующем разделе hello. 

## <a name="exception-types"></a>Типы исключений

Hello следующей таблице перечислены типы сообщений исключений и их причины. Также замечает, предлагаемые действия может занять toohelp resolve hello исключения.

| **Тип исключения** | **Описание** | **Рекомендуемое действие** | **Примечание к автоматическому или немедленному повтору** |
| --- | --- | --- | --- |
| [Время ожидания](https://msdn.microsoft.com/library/system.timeoutexception.aspx) |Hello сервер не ответил toohello запросил операцию в hello указанного времени, которая управляется [OperationTimeout](/dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout). Здравствуйте, сервер может завершенного hello запрошенную операцию. Это может произойти из-за toonetwork или других задержек. |Проверьте hello состояния системы для обеспечения согласованности и повторите попытку, при необходимости. Ознакомьтесь с разделом [TimeoutException](#timeoutexception). |Повторите попытку могут помочь в некоторых случаях; Добавьте toocode логику повторных попыток. |
| [Недопустимая операция](https://msdn.microsoft.com/library/system.invalidoperationexception.aspx) |Hello указанного пользователя операция не разрешена в hello server или службе. См. сообщение об исключении hello подробные сведения. |Проверка кода hello и документации hello. Убедитесь, что операция является допустимой запросил, hello. |Повторная попытка не поможет. |
| [Операция отменена](https://msdn.microsoft.com/library/system.operationcanceledexception.aspx) |Попытка сделать tooinvoke операцию на объекте, который уже закрыт, прервана или удален. В редких случаях hello внешняя транзакция уже удален. |Проверка кода hello и убедитесь, что он не вызывает операции над удаленным объектом. |Повторная попытка не поможет. |
| [Несанкционированный доступ](https://msdn.microsoft.com/library/system.unauthorizedaccessexception.aspx) |Hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) объекта не удалось получить маркер, маркер hello является недопустимым или hello маркер не содержит необходимые tooperform hello hello утверждения операции. |Убедитесь, что поставщик маркеров, hello создается с правильными значениями hello. Проверьте конфигурацию hello hello служба управления доступом. |Повторите попытку могут помочь в некоторых случаях; Добавьте toocode логику повторных попыток. |
| [Исключение аргумента](https://msdn.microsoft.com/library/system.argumentexception.aspx)<br /> [Аргумент Null](https://msdn.microsoft.com/library/system.argumentnullexception.aspx)<br />[Аргумент вне допустимого диапазона](https://msdn.microsoft.com/library/system.argumentoutofrangeexception.aspx) |Один или несколько из следующих hello произошла:<br />Один или несколько метод toohello аргументов являются недопустимыми.<br /> Hello URI, указанный слишком[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) или [создать](/dotnet/api/microsoft.servicebus.messaging.messagingfactory.create) содержит один или несколько сегментов пути.<br />Схема URI Hello указано слишком[NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) или [создать](/dotnet/api/microsoft.servicebus.messaging.messagingfactory.create) является недопустимым. <br />значение свойства Hello не должен превышать 32 КБ. |Проверьте вызывающего кода hello и убедитесь, что hello аргументы заданы правильно. |Повторная попытка не поможет. |
| [Сервер занят](/dotnet/api/microsoft.servicebus.messaging.serverbusyexception) |Служба не может tooprocess hello запрос в настоящее время. |Hello клиент может ожидать в течение заданного времени, а затем повторить операцию hello. |Hello клиент может повторить попытку через заданный интервал. Если повторить результаты, в другое исключение, проверьте hello повтора поведение этого исключения. |
| [Превышена квота](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) |сущность обмена сообщениями Hello достигнуто максимально допустимое. |Создайте место в сущности hello, прием сообщений от сущности hello или его вложенные очереди. Ознакомьтесь с разделом [Исключение QuotaExceededException](#quotaexceededexception). |Повторных попыток может помочь, если сообщения были удалены в hello это время. |
| [Превышен размер сообщения](/dotnet/api/microsoft.servicebus.messaging.messagesizeexceededexception) |Полезные данные сообщения превышает 256 КБ hello. Обратите внимание, что этот предел hello 256 КБ — hello общий размер сообщений. Hello общий размер сообщений может включать свойства системы и служебных данных Microsoft .NET. |Уменьшить размер полезных данных сообщения hello hello, а затем повторите операцию hello. |Повторная попытка не поможет. |

## <a name="quotaexceededexception"></a>QuotaExceededException

[QuotaExceededException](/dotnet/api/microsoft.servicebus.messaging.quotaexceededexception) указывает на превышение квоты для конкретного объекта.

Для ретрансляции, это исключение служит оболочкой hello [System.ServiceModel.QuotaExceededException](https://msdn.microsoft.com/library/system.servicemodel.quotaexceededexception.aspx), указывающая, что hello максимальное число прослушивателей было превышено для этой конечной точки. Это указано в hello **MaximumListenersPerEndpoint** значение hello сообщение об исключении.

## <a name="timeoutexception"></a>TimeoutException
Объект [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx) указывает инициированную пользователем операцию занимает больше времени, чем операции hello. 

Проверьте значение hello hello [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit) свойство. Достижение этого ограничения также может породить исключение [TimeoutException](https://msdn.microsoft.com/library/system.timeoutexception.aspx).

Для ретранслятора исключения времени ожидания могут отображаться при первом открытии подключения отправителя ретрансляции. Существует две основные причины этого исключения:

*   Hello [OpenTimeout](https://msdn.microsoft.com/library/wcf.opentimeout.aspx) значение может быть слишком мал (даже при долей секунды).
* Прослушиватель ретрансляции в локальной среде может не отвечать (или его могут возникнуть проблемы правила брандмауэра, которые мешают прослушиватели перестает принимать новые клиентские соединения) и hello [OpenTimeout](https://msdn.microsoft.com/library/wcf.opentimeout.aspx) значение составляет менее около 20 секунд.

Пример:

```
'System.TimeoutException’: hello operation did not complete within hello allotted timeout of 00:00:10.
hello time allotted toothis operation may have been a portion of a longer timeout.
```

### <a name="common-causes"></a>Основные причины
Существует две основные причины этой ошибки.

*   **Неправильная конфигурация**
    
    время ожидания операции Hello может оказаться слишком маленьким для hello рабочее состояние. значение по умолчанию Hello времени ожидания операции hello в пакет SDK для клиента hello составляет 60 секунд. Проверьте наличие toosee hello в коде значение toosomething слишком мал. Обратите внимание, условия использования и hello ЦП hello сети может повлиять на hello время, необходимое для toocomplete операции. Рекомендуется не tooset hello операции ожидания tooa очень маленькое значение.
*   **Временная ошибка службы**

    В некоторых случаях hello служба ретрансляции могут возникнуть задержки при обработке запросов. Например, это может произойти в период интенсивной нагрузки сети. В этом случае повторите операцию через некоторое время, пока не будет выполнена операция hello. Если hello одной операции продолжается toofail после нескольких попыток, проверьте hello [состояние узла службы Azure](https://azure.microsoft.com/status/) toosee Если известны сбои в работе службы.

## <a name="next-steps"></a>Дальнейшие действия
* [Часто задаваемые вопросы о ретрансляторе Azure](relay-faq.md)
* [Создание пространства имен ретранслятора с помощью портала Azure](relay-create-namespace-portal.md)
* [Приступая к работе с гибридными подключениями к ретранслятору](relay-hybrid-connections-dotnet-get-started.md)
* [Приступая к работе с гибридными подключениями к ретранслятору](relay-hybrid-connections-node-get-started.md)

