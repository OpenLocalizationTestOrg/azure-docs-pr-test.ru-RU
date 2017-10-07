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
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a><span data-ttu-id="1ba19-103">Обработка ошибок и исключений в Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="1ba19-103">Handle errors and exceptions in Azure Logic Apps</span></span>

<span data-ttu-id="1ba19-104">Приложения логики Azure предоставляет широкие возможности средства и шаблоны toohelp вы убедитесь, что интеграцию надежным и устойчивым к сбоям.</span><span class="sxs-lookup"><span data-stu-id="1ba19-104">Azure Logic Apps provides rich tools and patterns toohelp you make sure your integrations are robust and resilient against failures.</span></span> <span data-ttu-id="1ba19-105">Любой архитектуры интеграции создает hello сложность обеспечения tooappropriately убедиться, что дескриптор простоя или проблемы с зависимыми системами.</span><span class="sxs-lookup"><span data-stu-id="1ba19-105">Any integration architecture poses hello challenge of making sure tooappropriately handle downtime or issues from dependent systems.</span></span> <span data-ttu-id="1ba19-106">Упрощает логику приложения, обработка ошибок эффективные возможности, предоставляя hello средства, необходимые tooact на исключения и ошибки в рабочих процессах.</span><span class="sxs-lookup"><span data-stu-id="1ba19-106">Logic Apps makes handling errors a first-class experience, giving you hello tools you need tooact on exceptions and errors in your workflows.</span></span>

## <a name="retry-policies"></a><span data-ttu-id="1ba19-107">Политики повтора</span><span class="sxs-lookup"><span data-stu-id="1ba19-107">Retry policies</span></span>

<span data-ttu-id="1ba19-108">Политика повторов — самый простой тип исключения и обработка ошибок hello.</span><span class="sxs-lookup"><span data-stu-id="1ba19-108">A retry policy is hello most basic type of exception and error handling.</span></span> <span data-ttu-id="1ba19-109">Если начального запроса истекло время ожидания или сбой (любой запрос, который приводит 429 или отклик 5xx), эта политика определяет, следует ли повторить действие hello.</span><span class="sxs-lookup"><span data-stu-id="1ba19-109">If an initial request timed out or failed (any request that results in a 429 or 5xx response), this policy defines whether hello action should retry.</span></span> <span data-ttu-id="1ba19-110">По умолчанию все действия повторяются 4 дополнительных раза с 20-секундным интервалом.</span><span class="sxs-lookup"><span data-stu-id="1ba19-110">By default, all actions retry 4 additional times over 20-second intervals.</span></span> <span data-ttu-id="1ba19-111">Таким образом, если первый запрос hello получает `500 Internal Server Error` ответа, механизм hello рабочих процессов приостанавливает 20 секунд и попыток hello запрос еще раз.</span><span class="sxs-lookup"><span data-stu-id="1ba19-111">So if hello first request receives a `500 Internal Server Error` response, hello workflow engine pauses for 20 seconds, and attempts hello request again.</span></span> <span data-ttu-id="1ba19-112">Если после всех попыток hello ответа по-прежнему исключение или ошибка, продолжает hello рабочего процесса и метки hello состояние действия как `Failed`.</span><span class="sxs-lookup"><span data-stu-id="1ba19-112">If after all retries, hello response is still an exception or failure, hello workflow continues and marks hello action status as `Failed`.</span></span>

<span data-ttu-id="1ba19-113">Можно настроить политики повтора в hello **входов** для конкретного действия.</span><span class="sxs-lookup"><span data-stu-id="1ba19-113">You can configure retry policies in hello **inputs** for a particular action.</span></span> <span data-ttu-id="1ba19-114">Например настройкой tootry политики повтора как минимум четыре раза через 1 час.</span><span class="sxs-lookup"><span data-stu-id="1ba19-114">For example, you can configure a retry policy tootry as many as 4 times over 1-hour intervals.</span></span> <span data-ttu-id="1ba19-115">Дополнительные сведения о входных свойствах см. в статье [Workflow actions and triggers for Azure Logic Apps][retryPolicyMSDN] (Действия и триггеры рабочего процесса для Azure Logic Apps).</span><span class="sxs-lookup"><span data-stu-id="1ba19-115">For full details about input properties, see [Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

<span data-ttu-id="1ba19-116">Если нужна вашей tooretry действия HTTP 4 раза и подождите 10 минут между попытками, необходимо использовать hello следующие определения:</span><span class="sxs-lookup"><span data-stu-id="1ba19-116">If you wanted your HTTP action tooretry 4 times and wait 10 minutes between each attempt, you would use hello following definition:</span></span>

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

<span data-ttu-id="1ba19-117">Дополнительные сведения о поддерживаемом синтаксисе см. в разделе hello [статьи политики повтора действия рабочего процесса и триггеры][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="1ba19-117">For more information on supported syntax, see hello [retry-policy section in Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

## <a name="catch-failures-with-hello-runafter-property"></a><span data-ttu-id="1ba19-118">CATCH сбоев с hello RunAfter свойство</span><span class="sxs-lookup"><span data-stu-id="1ba19-118">Catch failures with hello RunAfter property</span></span>

<span data-ttu-id="1ba19-119">Каждое действие логику приложения объявляет, какие действия необходимо завершить перед запуском hello действия, такие как упорядочение hello действия в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="1ba19-119">Each logic app action declares which actions must finish before hello action starts, like ordering hello steps in your workflow.</span></span> <span data-ttu-id="1ba19-120">В определении действия hello, этот порядок называется hello `runAfter` свойство.</span><span class="sxs-lookup"><span data-stu-id="1ba19-120">In hello action definition, this ordering is known as hello `runAfter` property.</span></span> <span data-ttu-id="1ba19-121">Это свойство является объект, описывающий, какие действия и действия состояния выполнения действия hello.</span><span class="sxs-lookup"><span data-stu-id="1ba19-121">This property is an object that describes which actions and action statuses execute hello action.</span></span> <span data-ttu-id="1ba19-122">По умолчанию все действия, добавленные с помощью конструктора логики приложения hello заданы слишком`runAfter` hello предыдущий шаг, если hello ранее `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="1ba19-122">By default, all actions added through hello Logic App Designer are set too`runAfter` hello previous step if hello previous step `Succeeded`.</span></span> <span data-ttu-id="1ba19-123">Тем не менее, можно настроить действия toofire этого значения после выполнения предыдущих действий `Failed`, `Skipped`, или возможный набор из следующих значений.</span><span class="sxs-lookup"><span data-stu-id="1ba19-123">However, you can customize this value toofire actions when previous actions have `Failed`, `Skipped`, or a possible set of these values.</span></span> <span data-ttu-id="1ba19-124">Если требуется tooadd tooa элемент определен раздел служебной шины после определенного действия `Insert_Row` завершается ошибкой, можно использовать следующие hello `runAfter` конфигурации:</span><span class="sxs-lookup"><span data-stu-id="1ba19-124">If you wanted tooadd an item tooa designated Service Bus topic after a specific action `Insert_Row` fails, you could use hello following `runAfter` configuration:</span></span>

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

<span data-ttu-id="1ba19-125">Обратите внимание hello `runAfter` свойству toofire Если hello `Insert_Row` действия `Failed`.</span><span class="sxs-lookup"><span data-stu-id="1ba19-125">Notice hello `runAfter` property is set toofire if hello `Insert_Row` action is `Failed`.</span></span> <span data-ttu-id="1ba19-126">Действие hello toorun, если действие hello статус `Succeeded`, `Failed`, или `Skipped`, используйте следующий синтаксис:</span><span class="sxs-lookup"><span data-stu-id="1ba19-126">toorun hello action if hello action status is `Succeeded`, `Failed`, or `Skipped`, use this syntax:</span></span>

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> <span data-ttu-id="1ba19-127">Действия, успешно завершенные после сбоя предыдущего действия, будут помечены как `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="1ba19-127">Actions that run and complete successfully after a preceding action has failed, are marked as `Succeeded`.</span></span> <span data-ttu-id="1ba19-128">Это поведение означает, что если вы успешно перехватывать все ошибки в рабочем процессе hello запустите сам помечен как `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="1ba19-128">This behavior means that if you successfully catch all failures in a workflow, hello run itself is marked as `Succeeded`.</span></span>

## <a name="scopes-and-results-tooevaluate-actions"></a><span data-ttu-id="1ba19-129">Области и результаты действия tooevaluate</span><span class="sxs-lookup"><span data-stu-id="1ba19-129">Scopes and results tooevaluate actions</span></span>

<span data-ttu-id="1ba19-130">Аналогичные toohow, можно выполнить после отдельных действий, можно также сгруппировать действия внутри [область](../logic-apps/logic-apps-loops-and-scopes.md), что действуют как логическое группирование действий.</span><span class="sxs-lookup"><span data-stu-id="1ba19-130">Similar toohow you can run after individual actions, you can also group actions together inside a [scope](../logic-apps/logic-apps-loops-and-scopes.md), which act as a logical grouping of actions.</span></span> <span data-ttu-id="1ba19-131">Области полезны и для организации ваши действия приложений логики, так и для выполнения статистических вычислений на hello состояние области.</span><span class="sxs-lookup"><span data-stu-id="1ba19-131">Scopes are useful both for organizing your logic app actions, and for performing aggregate evaluations on hello status of a scope.</span></span> <span data-ttu-id="1ba19-132">область Hello сам переходит в состояние после завершения всех действий в области видимости.</span><span class="sxs-lookup"><span data-stu-id="1ba19-132">hello scope itself receives a status after all actions in a scope have finished.</span></span> <span data-ttu-id="1ba19-133">состояние области Hello определяется с помощью hello такие же условия в сеансе.</span><span class="sxs-lookup"><span data-stu-id="1ba19-133">hello scope status is determined with hello same criteria as a run.</span></span> <span data-ttu-id="1ba19-134">Если финальное действие hello в ветвь выполнения `Failed` или `Aborted`, находится в состоянии hello `Failed`.</span><span class="sxs-lookup"><span data-stu-id="1ba19-134">If hello final action in an execution branch is `Failed` or `Aborted`, hello status is `Failed`.</span></span>

<span data-ttu-id="1ba19-135">toofire определенные действия на наличие ошибок, возникших внутри области hello, можно использовать `runAfter` с областью, помеченного `Failed`.</span><span class="sxs-lookup"><span data-stu-id="1ba19-135">toofire specific actions for any failures that happened within hello scope, you can use `runAfter` with a scope that is marked `Failed`.</span></span> <span data-ttu-id="1ba19-136">Если *любой* действия в области hello ошибкой, выполнение после сбоя на область позволяет создавать toocatch отдельную операцию сбоев.</span><span class="sxs-lookup"><span data-stu-id="1ba19-136">If *any* actions in hello scope fail, running after a scope fails lets you create a single action toocatch failures.</span></span>

### <a name="getting-hello-context-of-failures-with-results"></a><span data-ttu-id="1ba19-137">Получение контекста hello сбоев с результатами</span><span class="sxs-lookup"><span data-stu-id="1ba19-137">Getting hello context of failures with results</span></span>

<span data-ttu-id="1ba19-138">Несмотря на то, что полезно перехват ошибок из области, можно также toohelp контекста понять точно какие действия, которые не удалось выполнить, и все ошибки и коды состояния, которые были возвращены.</span><span class="sxs-lookup"><span data-stu-id="1ba19-138">Although catching failures from a scope is useful, you might also want context toohelp you understand exactly which actions failed, and any errors or status codes that were returned.</span></span> <span data-ttu-id="1ba19-139">Hello `@result()` функции рабочего процесса предоставляет контекст для hello результат всех действий в области видимости.</span><span class="sxs-lookup"><span data-stu-id="1ba19-139">hello `@result()` workflow function provides context about hello result of all actions in a scope.</span></span>

<span data-ttu-id="1ba19-140">`@result()`принимает один параметр, имя области и возвращает массив всех результатов действий hello из в пределах данной области.</span><span class="sxs-lookup"><span data-stu-id="1ba19-140">`@result()` takes a single parameter, scope name, and returns an array of all hello action results from within that scope.</span></span> <span data-ttu-id="1ba19-141">Эти объекты действия включают hello же атрибутов в виде hello `@actions()` выводит объекта, включая время начала действия, время окончания действия, состояние действия, входными параметрами действий, идентификаторы корреляции действия и действия.</span><span class="sxs-lookup"><span data-stu-id="1ba19-141">These action objects include hello same attributes as hello `@actions()` object, including action start time, action end time, action status, action inputs, action correlation IDs, and action outputs.</span></span> <span data-ttu-id="1ba19-142">toosend контекста любые действия, которые не удалось выполнить в пределах области, вы могли легко сопоставить `@result()` функционировать с `runAfter`.</span><span class="sxs-lookup"><span data-stu-id="1ba19-142">toosend context of any actions that failed within a scope, you can easily pair an `@result()` function with a `runAfter`.</span></span>

<span data-ttu-id="1ba19-143">Действие tooexecute *для каждого* действия в области, `Failed`, фильтр hello массив tooactions результаты, сбой, вы можете обеспечить `@result()` с  **[массив фильтра](../connectors/connectors-native-query.md)**  действия и  **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**  цикла.</span><span class="sxs-lookup"><span data-stu-id="1ba19-143">tooexecute an action *for each* action in a scope that `Failed`, filter hello array of results tooactions that failed, you can pair `@result()` with a **[Filter Array](../connectors/connectors-native-query.md)** action and a **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)** loop.</span></span> <span data-ttu-id="1ba19-144">Может принимать массив отфильтрованный результирующий hello и выполнить действие для каждой ошибки с помощью hello **ForEach** цикла.</span><span class="sxs-lookup"><span data-stu-id="1ba19-144">You can take hello filtered result array and perform an action for each failure using hello **ForEach** loop.</span></span> <span data-ttu-id="1ba19-145">Ниже приведен пример, а затем получить подробное описание, который отправляет запрос HTTP POST с hello в тексте ответа каких-либо действий, которые не удалось выполнить в пределах области hello `My_Scope`.</span><span class="sxs-lookup"><span data-stu-id="1ba19-145">Here's an example, followed by a detailed explanation, that sends an HTTP POST request with hello response body of any actions that failed within hello scope `My_Scope`.</span></span>

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

<span data-ttu-id="1ba19-146">Вот toodescribe Подробное пошаговое руководство, что происходит.</span><span class="sxs-lookup"><span data-stu-id="1ba19-146">Here's a detailed walkthrough toodescribe what happens:</span></span>

1. <span data-ttu-id="1ba19-147">результат tooget Привет всем действиям в `My_Scope`, hello **массив фильтра** фильтры действий `@result('My_Scope')`.</span><span class="sxs-lookup"><span data-stu-id="1ba19-147">tooget hello result of all actions within `My_Scope`, hello **Filter Array** action filters `@result('My_Scope')`.</span></span>

2. <span data-ttu-id="1ba19-148">Здравствуйте, условие для **массив фильтра** любой `@result()` элемент, имеющий состояние равно слишком`Failed`.</span><span class="sxs-lookup"><span data-stu-id="1ba19-148">hello condition for **Filter Array** is any `@result()` item that has status equal too`Failed`.</span></span> <span data-ttu-id="1ba19-149">Это условие фильтрует массив hello со всех результатов действий из `My_Scope` tooan массив с единственным сбой результаты действий.</span><span class="sxs-lookup"><span data-stu-id="1ba19-149">This condition filters hello array with all action results from `My_Scope` tooan array with only failed action results.</span></span>

3. <span data-ttu-id="1ba19-150">Выполнить **для каждого** действие hello **отфильтрованные массива** выходов.</span><span class="sxs-lookup"><span data-stu-id="1ba19-150">Perform a **For Each** action on hello **Filtered Array** outputs.</span></span> <span data-ttu-id="1ba19-151">При этом выполняется действие *для каждого* ранее отфильтрованного результата действия, завершившегося сбоем.</span><span class="sxs-lookup"><span data-stu-id="1ba19-151">This step performs an action *for each* failed action result that was previously filtered.</span></span>

    <span data-ttu-id="1ba19-152">При сбое одного действия в области hello, hello действий в hello `foreach` запустить только один раз.</span><span class="sxs-lookup"><span data-stu-id="1ba19-152">If a single action in hello scope failed, hello actions in hello `foreach` run only once.</span></span> 
    <span data-ttu-id="1ba19-153">Многие завершившиеся сбоем действия приведут к выполнению только одного действия на сбой.</span><span class="sxs-lookup"><span data-stu-id="1ba19-153">Many failed actions cause one action per failure.</span></span>

4. <span data-ttu-id="1ba19-154">Отправить запрос HTTP POST от hello `foreach` элементов текста ответа или `@item()['outputs']['body']`.</span><span class="sxs-lookup"><span data-stu-id="1ba19-154">Send an HTTP POST on hello `foreach` item response body, or `@item()['outputs']['body']`.</span></span> <span data-ttu-id="1ba19-155">Hello `@result()` фигуры элемента является hello же hello `@actions()` формирование и может быть проанализирован hello таким же способом.</span><span class="sxs-lookup"><span data-stu-id="1ba19-155">hello `@result()` item shape is hello same as hello `@actions()` shape, and can be parsed hello same way.</span></span>

5. <span data-ttu-id="1ba19-156">Включение два пользовательских заголовков с именем неудавшееся действие hello `@item()['name']` hello сбой выполнения клиента, идентификатор отслеживания и `@item()['clientTrackingId']`.</span><span class="sxs-lookup"><span data-stu-id="1ba19-156">Include two custom headers with hello failed action name `@item()['name']` and hello failed run client tracking ID `@item()['clientTrackingId']`.</span></span>

<span data-ttu-id="1ba19-157">Для справки ниже приведен пример с одним `@result()` элемента, показывающая hello `name`, `body`, и `clientTrackingId` свойства, которые были получены в предыдущем примере hello.</span><span class="sxs-lookup"><span data-stu-id="1ba19-157">For reference, here's an example of a single `@result()` item, showing hello `name`, `body`, and `clientTrackingId` properties that are parsed in hello previous example.</span></span> <span data-ttu-id="1ba19-158">Вне цикла `foreach` `@result()` возвращает массив этих объектов.</span><span class="sxs-lookup"><span data-stu-id="1ba19-158">Outside of a `foreach`, `@result()` returns an array of these objects.</span></span>

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

<span data-ttu-id="1ba19-159">tooperform обработка исключений в различных шаблонов, можно использовать выражения hello, показанной ранее.</span><span class="sxs-lookup"><span data-stu-id="1ba19-159">tooperform different exception handling patterns, you can use hello expressions shown previously.</span></span> <span data-ttu-id="1ba19-160">Может выбрать tooexecute одного исключения, обработка действия за пределами области hello, которая принимает весь отфильтрованный массив hello сбоев, а также удалить hello `foreach`.</span><span class="sxs-lookup"><span data-stu-id="1ba19-160">You might choose tooexecute a single exception handling action outside hello scope that accepts hello entire filtered array of failures, and remove hello `foreach`.</span></span> <span data-ttu-id="1ba19-161">Можно также включить других полезных свойств из hello `@result()` ответа, показанной ранее.</span><span class="sxs-lookup"><span data-stu-id="1ba19-161">You can also include other useful properties from hello `@result()` response shown previously.</span></span>

## <a name="azure-diagnostics-and-telemetry"></a><span data-ttu-id="1ba19-162">Система диагностики и телеметрия Azure</span><span class="sxs-lookup"><span data-stu-id="1ba19-162">Azure Diagnostics and telemetry</span></span>

<span data-ttu-id="1ba19-163">Hello предыдущих шаблоны — это отличный способ toohandle ошибки и исключения в ходе, но также можно обнаруживать и отвечать tooerrors независимо от выполнения самого hello.</span><span class="sxs-lookup"><span data-stu-id="1ba19-163">hello previous patterns are great way toohandle errors and exceptions within a run, but you can also identify and respond tooerrors independent of hello run itself.</span></span> 
<span data-ttu-id="1ba19-164">[Диагностика Azure](../logic-apps/logic-apps-monitor-your-logic-apps.md) предоставляет простой способ toosend всех рабочих процессов события (включая все состояния выполнения и действия) tooan учетную запись хранилища Azure или концентратор событий Azure.</span><span class="sxs-lookup"><span data-stu-id="1ba19-164">[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) provides a simple way toosend all workflow events (including all run and action statuses) tooan Azure Storage account or an Azure Event Hub.</span></span> <span data-ttu-id="1ba19-165">tooevaluate выполнения состояния, отслеживать журналы hello и метрики, или публиковать их в любое средство наблюдения предпочитаемые.</span><span class="sxs-lookup"><span data-stu-id="1ba19-165">tooevaluate run statuses, you can monitor hello logs and metrics, or publish them into any monitoring tool you prefer.</span></span> <span data-ttu-id="1ba19-166">Один из возможных вариантов — toostream все события hello через концентратор событий Azure в [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="1ba19-166">One potential option is toostream all hello events through Azure Event Hub into [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> <span data-ttu-id="1ba19-167">В Stream Analytics можно написать активные запросы отключить все аномалии, средние значения или сбоя из hello журналы диагностики.</span><span class="sxs-lookup"><span data-stu-id="1ba19-167">In Stream Analytics, you can write live queries off any anomalies, averages, or failures from hello diagnostic logs.</span></span> <span data-ttu-id="1ba19-168">Stream Analytics можно легко вывода tooother источники данных, таких как очереди, разделы, SQL, Azure Cosmos DB и Power BI.</span><span class="sxs-lookup"><span data-stu-id="1ba19-168">Stream Analytics can easily output tooother data sources like queues, topics, SQL, Azure Cosmos DB, and Power BI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ba19-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1ba19-169">Next Steps</span></span>

* [<span data-ttu-id="1ba19-170">Сценарий обработки исключений и ведения журнала ошибок для приложений логики</span><span class="sxs-lookup"><span data-stu-id="1ba19-170">See how a customer builds error handling with Azure Logic Apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [<span data-ttu-id="1ba19-171">Примеры использования Logic Apps и распространенные сценарии</span><span class="sxs-lookup"><span data-stu-id="1ba19-171">Find more Logic Apps examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="1ba19-172">Узнайте, как toocreate автоматизировать развертывания для приложения логики</span><span class="sxs-lookup"><span data-stu-id="1ba19-172">Learn how toocreate automated deployments for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="1ba19-173">Создание и развертывание приложений логики в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ba19-173">Build and deploy logic apps with Visual Studio</span></span>](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
