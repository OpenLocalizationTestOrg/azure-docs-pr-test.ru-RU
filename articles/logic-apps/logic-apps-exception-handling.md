---
title: "aaaError & обработку исключений - приложения логики Azure | Документы Microsoft"
description: "Сведения об обработке ошибок и исключений в Azure Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: e50ab2f2-1fdc-4d2a-be40-995a6cc5a0d4
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 326a252310c8dfb154e583f91c9421675e448d1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a>Обработка ошибок и исключений в Azure Logic Apps

Приложения логики Azure предоставляет широкие возможности средства и шаблоны toohelp вы убедитесь, что интеграцию надежным и устойчивым к сбоям. Любой архитектуры интеграции создает hello сложность обеспечения tooappropriately убедиться, что дескриптор простоя или проблемы с зависимыми системами. Упрощает логику приложения, обработка ошибок эффективные возможности, предоставляя hello средства, необходимые tooact на исключения и ошибки в рабочих процессах.

## <a name="retry-policies"></a>Политики повтора

Политика повторов — самый простой тип исключения и обработка ошибок hello. Если начального запроса истекло время ожидания или сбой (любой запрос, который приводит 429 или отклик 5xx), эта политика определяет, следует ли повторить действие hello. По умолчанию все действия повторяются 4 дополнительных раза с 20-секундным интервалом. Таким образом, если первый запрос hello получает `500 Internal Server Error` ответа, механизм hello рабочих процессов приостанавливает 20 секунд и попыток hello запрос еще раз. Если после всех попыток hello ответа по-прежнему исключение или ошибка, продолжает hello рабочего процесса и метки hello состояние действия как `Failed`.

Можно настроить политики повтора в hello **входов** для конкретного действия. Например настройкой tootry политики повтора как минимум четыре раза через 1 час. Дополнительные сведения о входных свойствах см. в статье [Workflow actions and triggers for Azure Logic Apps][retryPolicyMSDN] (Действия и триггеры рабочего процесса для Azure Logic Apps).

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

Если нужна вашей tooretry действия HTTP 4 раза и подождите 10 минут между попытками, необходимо использовать hello следующие определения:

```json
"HTTP": 
{
    "inputs": {
        "method": "GET",
        "uri": "http://myAPIendpoint/api/action",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT10M",
            "count": 4
        }
    },
    "runAfter": {},
    "type": "Http"
}
```

Дополнительные сведения о поддерживаемом синтаксисе см. в разделе hello [статьи политики повтора действия рабочего процесса и триггеры][retryPolicyMSDN].

## <a name="catch-failures-with-hello-runafter-property"></a>CATCH сбоев с hello RunAfter свойство

Каждое действие логику приложения объявляет, какие действия необходимо завершить перед запуском hello действия, такие как упорядочение hello действия в рабочем процессе. В определении действия hello, этот порядок называется hello `runAfter` свойство. Это свойство является объект, описывающий, какие действия и действия состояния выполнения действия hello. По умолчанию все действия, добавленные с помощью конструктора логики приложения hello заданы слишком`runAfter` hello предыдущий шаг, если hello ранее `Succeeded`. Тем не менее, можно настроить действия toofire этого значения после выполнения предыдущих действий `Failed`, `Skipped`, или возможный набор из следующих значений. Если требуется tooadd tooa элемент определен раздел служебной шины после определенного действия `Insert_Row` завершается ошибкой, можно использовать следующие hello `runAfter` конфигурации:

```json
"Send_message": {
    "inputs": {
        "body": {
            "ContentData": "@{encodeBase64(body('Insert_Row'))}",
            "ContentType": "{ \"content-type\" : \"application/json\" }"
        },
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/servicebus"
            },
            "connection": {
                "name": "@parameters('$connections')['servicebus']['connectionId']"
            }
        },
        "method": "post",
        "path": "/@{encodeURIComponent('failures')}/messages"
    },
    "runAfter": {
        "Insert_Row": [
            "Failed"
        ]
    }
}
```

Обратите внимание hello `runAfter` свойству toofire Если hello `Insert_Row` действия `Failed`. Действие hello toorun, если действие hello статус `Succeeded`, `Failed`, или `Skipped`, используйте следующий синтаксис:

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> Действия, успешно завершенные после сбоя предыдущего действия, будут помечены как `Succeeded`. Это поведение означает, что если вы успешно перехватывать все ошибки в рабочем процессе hello запустите сам помечен как `Succeeded`.

## <a name="scopes-and-results-tooevaluate-actions"></a>Области и результаты действия tooevaluate

Аналогичные toohow, можно выполнить после отдельных действий, можно также сгруппировать действия внутри [область](../logic-apps/logic-apps-loops-and-scopes.md), что действуют как логическое группирование действий. Области полезны и для организации ваши действия приложений логики, так и для выполнения статистических вычислений на hello состояние области. область Hello сам переходит в состояние после завершения всех действий в области видимости. состояние области Hello определяется с помощью hello такие же условия в сеансе. Если финальное действие hello в ветвь выполнения `Failed` или `Aborted`, находится в состоянии hello `Failed`.

toofire определенные действия на наличие ошибок, возникших внутри области hello, можно использовать `runAfter` с областью, помеченного `Failed`. Если *любой* действия в области hello ошибкой, выполнение после сбоя на область позволяет создавать toocatch отдельную операцию сбоев.

### <a name="getting-hello-context-of-failures-with-results"></a>Получение контекста hello сбоев с результатами

Несмотря на то, что полезно перехват ошибок из области, можно также toohelp контекста понять точно какие действия, которые не удалось выполнить, и все ошибки и коды состояния, которые были возвращены. Hello `@result()` функции рабочего процесса предоставляет контекст для hello результат всех действий в области видимости.

`@result()`принимает один параметр, имя области и возвращает массив всех результатов действий hello из в пределах данной области. Эти объекты действия включают hello же атрибутов в виде hello `@actions()` выводит объекта, включая время начала действия, время окончания действия, состояние действия, входными параметрами действий, идентификаторы корреляции действия и действия. toosend контекста любые действия, которые не удалось выполнить в пределах области, вы могли легко сопоставить `@result()` функционировать с `runAfter`.

Действие tooexecute *для каждого* действия в области, `Failed`, фильтр hello массив tooactions результаты, сбой, вы можете обеспечить `@result()` с  **[массив фильтра](../connectors/connectors-native-query.md)**  действия и  **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**  цикла. Может принимать массив отфильтрованный результирующий hello и выполнить действие для каждой ошибки с помощью hello **ForEach** цикла. Ниже приведен пример, а затем получить подробное описание, который отправляет запрос HTTP POST с hello в тексте ответа каких-либо действий, которые не удалось выполнить в пределах области hello `My_Scope`.

```json
"Filter_array": {
    "inputs": {
        "from": "@result('My_Scope')",
        "where": "@equals(item()['status'], 'Failed')"
    },
    "runAfter": {
        "My_Scope": [
            "Failed"
        ]
    },
    "type": "Query"
},
"For_each": {
    "actions": {
        "Log_Exception": {
            "inputs": {
                "body": "@item()['outputs']['body']",
                "method": "POST",
                "headers": {
                    "x-failed-action-name": "@item()['name']",
                    "x-failed-tracking-id": "@item()['clientTrackingId']"
                },
                "uri": "http://requestb.in/"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "foreach": "@body('Filter_array')",
    "runAfter": {
        "Filter_array": [
            "Succeeded"
        ]
    },
    "type": "Foreach"
}
```

Вот toodescribe Подробное пошаговое руководство, что происходит.

1. результат tooget Привет всем действиям в `My_Scope`, hello **массив фильтра** фильтры действий `@result('My_Scope')`.

2. Здравствуйте, условие для **массив фильтра** любой `@result()` элемент, имеющий состояние равно слишком`Failed`. Это условие фильтрует массив hello со всех результатов действий из `My_Scope` tooan массив с единственным сбой результаты действий.

3. Выполнить **для каждого** действие hello **отфильтрованные массива** выходов. При этом выполняется действие *для каждого* ранее отфильтрованного результата действия, завершившегося сбоем.

    При сбое одного действия в области hello, hello действий в hello `foreach` запустить только один раз. 
    Многие завершившиеся сбоем действия приведут к выполнению только одного действия на сбой.

4. Отправить запрос HTTP POST от hello `foreach` элементов текста ответа или `@item()['outputs']['body']`. Hello `@result()` фигуры элемента является hello же hello `@actions()` формирование и может быть проанализирован hello таким же способом.

5. Включение два пользовательских заголовков с именем неудавшееся действие hello `@item()['name']` hello сбой выполнения клиента, идентификатор отслеживания и `@item()['clientTrackingId']`.

Для справки ниже приведен пример с одним `@result()` элемента, показывающая hello `name`, `body`, и `clientTrackingId` свойства, которые были получены в предыдущем примере hello. Вне цикла `foreach` `@result()` возвращает массив этих объектов.

```json
{
    "name": "Example_Action_That_Failed",
    "inputs": {
        "uri": "https://myfailedaction.azurewebsites.net",
        "method": "POST"
    },
    "outputs": {
        "statusCode": 404,
        "headers": {
            "Date": "Thu, 11 Aug 2016 03:18:18 GMT",
            "Server": "Microsoft-IIS/8.0",
            "X-Powered-By": "ASP.NET",
            "Content-Length": "68",
            "Content-Type": "application/json"
        },
        "body": {
            "code": "ResourceNotFound",
            "message": "/docs/folder-name/resource-name does not exist"
        }
    },
    "startTime": "2016-08-11T03:18:19.7755341Z",
    "endTime": "2016-08-11T03:18:20.2598835Z",
    "trackingId": "bdd82e28-ba2c-4160-a700-e3a8f1a38e22",
    "clientTrackingId": "08587307213861835591296330354",
    "code": "NotFound",
    "status": "Failed"
}
```

tooperform обработка исключений в различных шаблонов, можно использовать выражения hello, показанной ранее. Может выбрать tooexecute одного исключения, обработка действия за пределами области hello, которая принимает весь отфильтрованный массив hello сбоев, а также удалить hello `foreach`. Можно также включить других полезных свойств из hello `@result()` ответа, показанной ранее.

## <a name="azure-diagnostics-and-telemetry"></a>Система диагностики и телеметрия Azure

Hello предыдущих шаблоны — это отличный способ toohandle ошибки и исключения в ходе, но также можно обнаруживать и отвечать tooerrors независимо от выполнения самого hello. 
[Диагностика Azure](../logic-apps/logic-apps-monitor-your-logic-apps.md) предоставляет простой способ toosend всех рабочих процессов события (включая все состояния выполнения и действия) tooan учетную запись хранилища Azure или концентратор событий Azure. tooevaluate выполнения состояния, отслеживать журналы hello и метрики, или публиковать их в любое средство наблюдения предпочитаемые. Один из возможных вариантов — toostream все события hello через концентратор событий Azure в [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/). В Stream Analytics можно написать активные запросы отключить все аномалии, средние значения или сбоя из hello журналы диагностики. Stream Analytics можно легко вывода tooother источники данных, таких как очереди, разделы, SQL, Azure Cosmos DB и Power BI.

## <a name="next-steps"></a>Дальнейшие действия

* [Сценарий обработки исключений и ведения журнала ошибок для приложений логики](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [Примеры использования Logic Apps и распространенные сценарии](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Узнайте, как toocreate автоматизировать развертывания для приложения логики](../logic-apps/logic-apps-create-deploy-template.md)
* [Создание и развертывание приложений логики в Visual Studio](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
