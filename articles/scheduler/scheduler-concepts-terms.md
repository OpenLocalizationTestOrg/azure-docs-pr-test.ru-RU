---
title: "aaaScheduler сущностей, основные понятия и термины | Документы Microsoft"
description: "Основные понятия, терминология и иерархия сущностей планировщика, включая задания и коллекции заданий.  Подробный пример запланированного задания."
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 3ef16fab-d18a-48ba-8e56-3f3e0a1bcb92
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 73e7de7bfd2937e401aeab05e0e10fa292cf37b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-concepts-terminology--entity-hierarchy"></a>Основные понятия, терминология и иерархия сущностей планировщика
## <a name="scheduler-entity-hierarchy"></a>Иерархия сущностей планировщика
Hello следующей таблице описаны основные ресурсы hello предоставляемые или используемые API планировщика hello.

| Ресурс | Description (Описание) |
| --- | --- |
| **Коллекция заданий** |Коллекция заданий содержит группу заданий и сохраняет параметры, квоты и регулирования, которые являются общими для задания в коллекции hello. Коллекция заданий создается владельцем подписки и объединяет задания по областям использования или границам приложений. Это ограниченное tooone области. Она также позволяет hello принудительного применения квот использования hello tooconstrain всех заданий в этой коллекции. Hello квот входят MaxJobs и MaxRecurrence. |
| **Задание.** |Задание определяет одно повторяющееся действие с простой или сложной стратегией выполнения. К действиям относятся HTTP-запросы, запросы к очереди хранилища, запросы к очереди служебной шины и запросы к разделу служебной шины. |
| **Журнал заданий** |Журнал заданий содержит подробные сведения о выполнении заданий. В нем указывается, было ли задание выполнено, а также все данные ответов. |

## <a name="scheduler-entity-management"></a>Управление сущностями планировщика
На высоком уровне планировщик hello и API управления службами hello предоставляют следующие операции с ресурсами hello hello:

| Функция | Описание и URI-адрес |
| --- | --- |
| **Управление коллекциями заданий** |GET, PUT и DELETE поддержку для создания и изменения коллекций заданий и заданий hello, содержащийся в ней. Коллекция заданий — это контейнер для заданий и сопоставляет tooquotas и общих настроек. В качестве примеров квот (которые подробно описаны ниже) можно привести максимальное число заданий и наименьший интервал повторения. <p>PUT и DELETE: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</p><p>GET: `https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}`</p> |
| **Управление заданиями** |Поддержка запросов GET, PUT, POST, PATCH и DELETE для создания и изменения облачных заданий. Все задания должны принадлежать tooa коллекции заданий, которая уже существует, то есть нет неявного создания. <p>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}`</p> |
| **Управление журналами заданий** |Поддержка запроса GET для извлечения журнала заданий за последние 60 дней с указанием времени и результатов выполнения. Добавляет поддержку строкового параметра запроса для фильтрации результатов по состоянию и статусу. <P>`https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Scheduler/jobCollections/{jobCollectionName}/jobs/{jobName}/history`</p> |

## <a name="job-types"></a>Типы заданий
Существует несколько типов заданий: задания HTTP (включая задания HTTPS, поддерживающие протокол SSL), задания очереди хранилища, задания очереди служебной шины и задания раздела служебной шины. Задания HTTP применяются, если у вас есть конечная точка существующей рабочей нагрузки или службы. Можно использовать очереди заданий toopost сообщения toostorage очереди хранилища, поэтому эти задания лучше подходят для рабочих нагрузок, использующих очереди хранилища. Аналогичным образом задания служебной шины идеально подходят для рабочих нагрузок, использующих очереди и разделы служебной шины.

## <a name="hello-job-entity-in-detail"></a>сущность «задание» Hello подробно
На базовом уровне запланированное задание состоит из нескольких частей.

* Hello tooperform действие при запуске задания таймера hello  
* Задание hello toorun hello (необязательно)  
* (Необязательно) Когда и как часто toorepeat hello задания  
* (Необязательно) Toofire действия при сбое основного действия hello  

Внутренне запланированное задание также содержит системные данные, такие как hello следующее запланированное время выполнения.

После кода Hello предоставляет подробный пример запланированного задания. Подробности см. в следующих разделах.

    {
        "startTime": "2012-08-04T00:00Z",               // optional
        "action":
        {
            "type": "http",
            "retryPolicy": { "retryType":"none" },
            "request":
            {
                "uri": "http://contoso.com/foo",        // required
                "method": "PUT",                        // required
                "body": "Posting from a timer",         // optional
                "headers":                              // optional

                {
                    "Content-Type": "application/json"
                },
            },
           "errorAction":
           {
               "type": "http",
               "request":
               {
                   "uri": "http://contoso.com/notifyError",
                   "method": "POST",
               },
           },
        },
        "recurrence":                                   // optional
        {
            "frequency": "week",                        // can be "year" "month" "day" "week" "minute"
            "interval": 1,                              // optional, how often toofire (default too1)
            "schedule":                                 // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]
            },
            "count": 10,                                 // optional (default toorecur infinitely)
            "endTime": "2012-11-04",                     // optional (default toorecur infinitely)
        },
        "state": "disabled",                           // enabled or disabled
        "status":                                       // controlled by Scheduler service
        {
            "lastExecutionTime": "2007-03-01T13:00:00Z",
            "nextExecutionTime": "2007-03-01T14:00:00Z ",
            "executionCount": 3,
                                                "failureCount": 0,
                                                "faultedCount": 0
        },
    }

По результатам hello образец запланированное задание выше, определение задания состоит из нескольких частей:

* Время начала (startTime).  
* Действие (action), которое включает действие ошибки (errorAction).
* Повторение (recurrence).  
* Состояние (state).  
* Статус (status).  
* Политика повтора (retryPolicy).  

Рассмотрим каждую часть подробно.

## <a name="starttime"></a>startTime
Hello «startTime» время начала hello и позволяет hello вызывающего объекта toospecify сети hello в смещение часового пояса [формата ISO 8601](http://en.wikipedia.org/wiki/ISO_8601).

## <a name="action-and-erroraction"></a>action и errorAction
Действие «Hello» — hello действие, вызываемое при каждом выполнении и описывает тип вызова службы. Действие Hello является то, что будет выполняться по hello указано расписание. Планировщик поддерживает действия, связанные с HTTP, очередью хранилища, разделом служебной шины и очередью служебной шины.

Действие Hello в приведенном выше примере hello является действие HTTP. Ниже приведен пример с действием очереди хранилища.

    {
            "type": "storageQueue",
            "queueMessage":
            {
                "storageAccount": "myStorageAccount",  // required
                "queueName": "myqueue",                // required
                "sasToken": "TOKEN",                   // required
                "message":                             // required
                    "My message body",
            },
    }

Ниже приведен пример действия раздела служебной шины.

  "action": { "type": "serviceBusTopic", "serviceBusTopicMessage": { "topicPath": "t1",  
      "namespace": "mySBNamespace", "transportType": "netMessaging", // Может быть netMessaging или AMQP "authentication": { "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Сообщение", "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, }

Ниже приведен пример действия очереди служебной шины.

  "action": { "serviceBusQueueMessage": { "queueName": "q1",  
      "namespace": "mySBNamespace", "transportType": "netMessaging", // Может быть netMessaging или AMQP "authentication": {  
        "sasKeyName": "QPolicy", "type": "sharedAccessKey" }, "message": "Сообщение",  
      "brokeredMessageProperties": {}, "customMessageProperties": { "appname": "FromScheduler" } }, "type": "serviceBusQueue" }

Hello «errorAction» — обработчик ошибок hello, вызывается при сбое основного действия hello действие hello. Можно использовать этот переменной toocall конечную точку обработки ошибок или отправить уведомления пользователям. Это можно использовать для достижения этого hello вторичной конечной точки в случае hello основной недоступен (например, в случае аварии на узле конечной точки hello hello) или может использоваться для уведомления конечную точку обработки ошибок. Так же, как hello главное действие действие при возникновении ошибки hello может быть простая или составная логика, основанная на других действиях. как toocreate маркер SAS см. слишком toolearn[Создание и использование подписи общего доступа](https://msdn.microsoft.com/library/azure/jj721951.aspx).

## <a name="recurrence"></a>recurrence
Параметр recurrence состоит из нескольких частей.

* Частота (frequency): минута, час, день, неделя, месяц или год.  
* Интервал: Интервал hello, заданных частоту повторения hello  
* Предписанное расписание: укажите минуты, часы, дни недели, месяцы и дни месяца для повторения hello  
* Количество (count): число повторений.  
* Время окончания: никакие задания не будет выполняться после hello указано время окончания  

Задание повторяется, если его определение JSON включает объект повторения. Если указаны count и endTime учитывается hello правилу выполнения, которая должна выполняться первой.

## <a name="state"></a>state
состояние Hello hello задания является одним из четырех значений: включено, отключено, завершена или произошел сбой. Можно ПОМЕСТИТЬ или исправление для задания, так как tooupdate их toohello включен или отключенном состоянии. Если задание завершено или произошел сбой, то есть конечное состояние, которое не может быть обновлен (но hello задания по-прежнему может быть удалено). Пример свойства состояния hello выглядит следующим образом:

        "state": "disabled", // enabled, disabled, completed, or faulted
Завершенные и неисправные задания удаляются через 60 дней.

## <a name="status"></a>status
После запуска задания планировщика будут возвращены сведения о текущем состоянии hello hello задания. Этот объект не может задаваться пользователем hello — он задается системой hello. Тем не менее он включен в hello объекта задания (а не отдельным связанным ресурсом), чтобы один легко получить hello состояния задания.

Состояние задания содержит время hello hello предыдущего выполнения (если таковые имеются), hello время следующего запланированного выполнения hello (для выполняющихся заданий) и число выполнений hello hello задания.

## <a name="retrypolicy"></a>retryPolicy
При сбое задания планировщика это возможных toospecify toodetermine политики повтора, повторяется ли и каким образом действие hello. Это определяется hello **тип повторов** объект — установлено слишком**нет** Если нет политики повтора, как показано выше. Задайте для него слишком**фиксированной** при наличии политики повтора.

tooset политику повтора можно указать два дополнительных параметра: интервал повтора (**retryInterval**) и hello число повторных попыток (**retryCount**).

Интервал повтора Hello, указанный с hello **retryInterval** , является hello интервал между повторными попытками. Значение по умолчанию составляет 30 секунд, минимальное настраиваемое значение — 15 секунд, а максимальное — 18 месяцев. Для заданий в бесплатных коллекциях минимальное настраиваемое значение составляет 1 час.  Он определен в формате ISO 8601 hello. Аналогичным образом, заданное значение hello hello число повторных попыток с hello **retryCount** объекта; это hello количество попыток. Значение по умолчанию равно 4, а максимальное значение — 20\. Оба **retryInterval** и **retryCount** являются необязательными. Они получают их значения по умолчанию, если **тип повторов** задано слишком**фиксированной** и значения не указаны явным образом.

## <a name="see-also"></a>См. также
 [Что такое планировщик?](scheduler-intro.md)

 [Начало работы с планировщиком в hello портал Azure](scheduler-get-started-portal.md)

 [Планы и выставление счетов в планировщике Azure](scheduler-plans-billing.md)

 [Как планирует комплексного toobuild и дополнительно повторения с планировщиком Azure](scheduler-advanced-complexity.md)

 [Справочник по API REST планировщика Azure](https://msdn.microsoft.com/library/mt629143)

 [Справочник по командлетам PowerShell планировщика Azure](scheduler-powershell-reference.md)

 [Высокая доступность и надежность планировщика Azure](scheduler-high-availability-reliability.md)

 [Ограничения, значения по умолчанию и коды ошибок планировщика Azure](scheduler-limits-defaults-errors.md)

 [Исходящая аутентификация планировщика Azure](scheduler-outbound-authentication.md)

