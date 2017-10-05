---
title: "Обработка ошибок и исключений с помощью Azure Logic Apps | Документация Майкрософт"
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
ms.openlocfilehash: 9af2f71b3d288cc6f4e271d0915545d43a1249bc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="handle-errors-and-exceptions-in-azure-logic-apps"></a><span data-ttu-id="73be9-103">Обработка ошибок и исключений в Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="73be9-103">Handle errors and exceptions in Azure Logic Apps</span></span>

<span data-ttu-id="73be9-104">Azure Logic Apps предоставляет большой набор средств и шаблонов, позволяющих обеспечить надежные и устойчивые к сбоям интеграции.</span><span class="sxs-lookup"><span data-stu-id="73be9-104">Azure Logic Apps provides rich tools and patterns to help you make sure your integrations are robust and resilient against failures.</span></span> <span data-ttu-id="73be9-105">При использовании любой архитектуры интеграции возникают сложности, связанные с соответствующей обработкой простоя или устранением неполадок, вызванных зависимыми системами.</span><span class="sxs-lookup"><span data-stu-id="73be9-105">Any integration architecture poses the challenge of making sure to appropriately handle downtime or issues from dependent systems.</span></span> <span data-ttu-id="73be9-106">Logic Apps существенно упрощает обработку ошибок, предоставляя средства для устранения ошибок и исключений в рабочих процессах.</span><span class="sxs-lookup"><span data-stu-id="73be9-106">Logic Apps makes handling errors a first-class experience, giving you the tools you need to act on exceptions and errors in your workflows.</span></span>

## <a name="retry-policies"></a><span data-ttu-id="73be9-107">Политики повтора</span><span class="sxs-lookup"><span data-stu-id="73be9-107">Retry policies</span></span>

<span data-ttu-id="73be9-108">Самое простое средство обработки ошибок и исключений — политика повтора.</span><span class="sxs-lookup"><span data-stu-id="73be9-108">A retry policy is the most basic type of exception and error handling.</span></span> <span data-ttu-id="73be9-109">Эта политика определяет, следует ли повторить действие, если время ожидания первоначального запроса истекло или он завершился сбоем (любой запрос с ответом 429 или 5xx).</span><span class="sxs-lookup"><span data-stu-id="73be9-109">If an initial request timed out or failed (any request that results in a 429 or 5xx response), this policy defines whether the action should retry.</span></span> <span data-ttu-id="73be9-110">По умолчанию все действия повторяются 4 дополнительных раза с 20-секундным интервалом.</span><span class="sxs-lookup"><span data-stu-id="73be9-110">By default, all actions retry 4 additional times over 20-second intervals.</span></span> <span data-ttu-id="73be9-111">То есть, если для первого запроса вернулся ответ `500 Internal Server Error`, обработчик рабочего процесса отправляет повторный запрос по истечении 20 секунд.</span><span class="sxs-lookup"><span data-stu-id="73be9-111">So if the first request receives a `500 Internal Server Error` response, the workflow engine pauses for 20 seconds, and attempts the request again.</span></span> <span data-ttu-id="73be9-112">Если после всех попыток в ответе по-прежнему возвращается исключение или сбой, выполнение рабочего процесса продолжится, а действие будет помечено как `Failed`.</span><span class="sxs-lookup"><span data-stu-id="73be9-112">If after all retries, the response is still an exception or failure, the workflow continues and marks the action status as `Failed`.</span></span>

<span data-ttu-id="73be9-113">Политику повтора можно задать во **входных данных** определенного действия.</span><span class="sxs-lookup"><span data-stu-id="73be9-113">You can configure retry policies in the **inputs** for a particular action.</span></span> <span data-ttu-id="73be9-114">Например, вы можете настроить выполнение максимум 4 попыток в течение 1 часа.</span><span class="sxs-lookup"><span data-stu-id="73be9-114">For example, you can configure a retry policy to try as many as 4 times over 1-hour intervals.</span></span> <span data-ttu-id="73be9-115">Дополнительные сведения о входных свойствах см. в статье [Workflow actions and triggers for Azure Logic Apps][retryPolicyMSDN] (Действия и триггеры рабочего процесса для Azure Logic Apps).</span><span class="sxs-lookup"><span data-stu-id="73be9-115">For full details about input properties, see [Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

```json
"retryPolicy" : {
      "type": "<type-of-retry-policy>",
      "interval": <retry-interval>,
      "count": <number-of-retry-attempts>
    }
```

<span data-ttu-id="73be9-116">Если необходимо, чтобы для выполнения HTTP-действия предпринималось 4 попытки с 10-минутным интервалом между ними, задайте следующее определение:</span><span class="sxs-lookup"><span data-stu-id="73be9-116">If you wanted your HTTP action to retry 4 times and wait 10 minutes between each attempt, you would use the following definition:</span></span>

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

<span data-ttu-id="73be9-117">Дополнительные сведения о поддерживаемом синтаксисе см. в разделе о политике повторения в [этой статье][retryPolicyMSDN].</span><span class="sxs-lookup"><span data-stu-id="73be9-117">For more information on supported syntax, see the [retry-policy section in Workflow Actions and Triggers][retryPolicyMSDN].</span></span>

## <a name="catch-failures-with-the-runafter-property"></a><span data-ttu-id="73be9-118">Перехват ошибок с помощью свойства RunAfter</span><span class="sxs-lookup"><span data-stu-id="73be9-118">Catch failures with the RunAfter property</span></span>

<span data-ttu-id="73be9-119">Каждое действие приложения логики объявляет, какие действия должны завершаться перед началом определенного действия (наподобие упорядочения действий рабочего процесса).</span><span class="sxs-lookup"><span data-stu-id="73be9-119">Each logic app action declares which actions must finish before the action starts, like ordering the steps in your workflow.</span></span> <span data-ttu-id="73be9-120">Это упорядочение задается с помощью свойства `runAfter` в определении действия.</span><span class="sxs-lookup"><span data-stu-id="73be9-120">In the action definition, this ordering is known as the `runAfter` property.</span></span> <span data-ttu-id="73be9-121">Данное свойство является объектом, описывающим, какие действия и состояния действий необходимы для выполнения определенного действия.</span><span class="sxs-lookup"><span data-stu-id="73be9-121">This property is an object that describes which actions and action statuses execute the action.</span></span> <span data-ttu-id="73be9-122">По умолчанию все действия, добавленные с помощью конструктора приложений логики, получают свойство `runAfter` предыдущего шага, если он получил состояние `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="73be9-122">By default, all actions added through the Logic App Designer are set to `runAfter` the previous step if the previous step `Succeeded`.</span></span> <span data-ttu-id="73be9-123">Однако это значение можно изменить таким образом, чтобы действия срабатывали, если предыдущие действия получили состояние `Failed`, `Skipped` или оба.</span><span class="sxs-lookup"><span data-stu-id="73be9-123">However, you can customize this value to fire actions when previous actions have `Failed`, `Skipped`, or a possible set of these values.</span></span> <span data-ttu-id="73be9-124">Чтобы добавить элемент в указанный раздел служебной шины после сбоя определенного действия `Insert_Row`, необходимо использовать следующую конфигурацию `runAfter`:</span><span class="sxs-lookup"><span data-stu-id="73be9-124">If you wanted to add an item to a designated Service Bus topic after a specific action `Insert_Row` fails, you could use the following `runAfter` configuration:</span></span>

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

<span data-ttu-id="73be9-125">Обратите внимание, что для свойства `runAfter` настроено срабатывание, если действие `Insert_Row` имеет состояние `Failed`.</span><span class="sxs-lookup"><span data-stu-id="73be9-125">Notice the `runAfter` property is set to fire if the `Insert_Row` action is `Failed`.</span></span> <span data-ttu-id="73be9-126">Чтобы выполнить действие, если состояние действия `Succeeded`, `Failed` или `Skipped`, используйте такой синтаксис:</span><span class="sxs-lookup"><span data-stu-id="73be9-126">To run the action if the action status is `Succeeded`, `Failed`, or `Skipped`, use this syntax:</span></span>

```json
"runAfter": {
        "Insert_Row": [
            "Failed", "Succeeded", "Skipped"
        ]
    }
```

> [!TIP]
> <span data-ttu-id="73be9-127">Действия, успешно завершенные после сбоя предыдущего действия, будут помечены как `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="73be9-127">Actions that run and complete successfully after a preceding action has failed, are marked as `Succeeded`.</span></span> <span data-ttu-id="73be9-128">Таким образом, если перехватить все ошибки в рабочем процессе, само выполнение помечается как `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="73be9-128">This behavior means that if you successfully catch all failures in a workflow, the run itself is marked as `Succeeded`.</span></span>

## <a name="scopes-and-results-to-evaluate-actions"></a><span data-ttu-id="73be9-129">Области и результаты для оценки действий</span><span class="sxs-lookup"><span data-stu-id="73be9-129">Scopes and results to evaluate actions</span></span>

<span data-ttu-id="73be9-130">Точно так же, как можно запускать выполнение после отдельных действий, можно сгруппировать действия внутри [области](../logic-apps/logic-apps-loops-and-scopes.md), которая действует как логическая группа действий.</span><span class="sxs-lookup"><span data-stu-id="73be9-130">Similar to how you can run after individual actions, you can also group actions together inside a [scope](../logic-apps/logic-apps-loops-and-scopes.md), which act as a logical grouping of actions.</span></span> <span data-ttu-id="73be9-131">Области можно эффективно использовать как для организации действий приложения логики, так и для выполнения статистических вычислений на основе состояния области.</span><span class="sxs-lookup"><span data-stu-id="73be9-131">Scopes are useful both for organizing your logic app actions, and for performing aggregate evaluations on the status of a scope.</span></span> <span data-ttu-id="73be9-132">Сама область получает определенное состояние после завершения в ней всех действий.</span><span class="sxs-lookup"><span data-stu-id="73be9-132">The scope itself receives a status after all actions in a scope have finished.</span></span> <span data-ttu-id="73be9-133">Состояние области определяется теми же критериями, которые используются для выполнения.</span><span class="sxs-lookup"><span data-stu-id="73be9-133">The scope status is determined with the same criteria as a run.</span></span> <span data-ttu-id="73be9-134">Если состояние последнего действия в ветви выполнения — `Failed` или `Aborted`, область получит состояние `Failed`.</span><span class="sxs-lookup"><span data-stu-id="73be9-134">If the final action in an execution branch is `Failed` or `Aborted`, the status is `Failed`.</span></span>

<span data-ttu-id="73be9-135">Чтобы запускать определенные действия для обнаружения любых сбоев, произошедших в области, вы можете использовать свойство `runAfter` для области с состоянием `Failed`.</span><span class="sxs-lookup"><span data-stu-id="73be9-135">To fire specific actions for any failures that happened within the scope, you can use `runAfter` with a scope that is marked `Failed`.</span></span> <span data-ttu-id="73be9-136">Исходя из этого, можно создать отдельное действие для перехвата ошибок, в случае если *какое-либо* действие в области завершилось сбоем.</span><span class="sxs-lookup"><span data-stu-id="73be9-136">If *any* actions in the scope fail, running after a scope fails lets you create a single action to catch failures.</span></span>

### <a name="getting-the-context-of-failures-with-results"></a><span data-ttu-id="73be9-137">Получение контекста сбоев в результатах</span><span class="sxs-lookup"><span data-stu-id="73be9-137">Getting the context of failures with results</span></span>

<span data-ttu-id="73be9-138">Хотя перехват ошибок в области очень эффективен, вам также может понадобиться контекст, чтобы понять, какие действия завершились сбоем, и узнать возвращенные ошибки и коды состояния.</span><span class="sxs-lookup"><span data-stu-id="73be9-138">Although catching failures from a scope is useful, you might also want context to help you understand exactly which actions failed, and any errors or status codes that were returned.</span></span> <span data-ttu-id="73be9-139">Функция рабочего процесса `@result()` выводит контекст о результате всех действий в области.</span><span class="sxs-lookup"><span data-stu-id="73be9-139">The `@result()` workflow function provides context about the result of all actions in a scope.</span></span>

<span data-ttu-id="73be9-140">`@result()` принимает один параметр, имя области, и возвращает массив результатов всех действий в этой области.</span><span class="sxs-lookup"><span data-stu-id="73be9-140">`@result()` takes a single parameter, scope name, and returns an array of all the action results from within that scope.</span></span> <span data-ttu-id="73be9-141">Объекты действия включают в себя те же атрибуты, что и объект `@actions()` , в том числе время начала и окончания действия, состояние действия, входные и выходные данные действия, а также идентификаторы корреляции действия.</span><span class="sxs-lookup"><span data-stu-id="73be9-141">These action objects include the same attributes as the `@actions()` object, including action start time, action end time, action status, action inputs, action correlation IDs, and action outputs.</span></span> <span data-ttu-id="73be9-142">Чтобы отправить контекст любых действий, завершившихся сбоем в области, вы можете легко связать функцию `@result()` со свойством `runAfter`.</span><span class="sxs-lookup"><span data-stu-id="73be9-142">To send context of any actions that failed within a scope, you can easily pair an `@result()` function with a `runAfter`.</span></span>

<span data-ttu-id="73be9-143">Чтобы выполнять действие *для каждого* действия в области с состоянием `Failed`, выполните фильтрацию массива результатов по действиям, которые завершились сбоем, что позволит вам связать `@result()` с действием **[Фильтр массива](../connectors/connectors-native-query.md)** и циклом **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)**.</span><span class="sxs-lookup"><span data-stu-id="73be9-143">To execute an action *for each* action in a scope that `Failed`, filter the array of results to actions that failed, you can pair `@result()` with a **[Filter Array](../connectors/connectors-native-query.md)** action and a **[ForEach](../logic-apps/logic-apps-loops-and-scopes.md)** loop.</span></span> <span data-ttu-id="73be9-144">Можно настроить выполнение действия для каждой ошибки в отфильтрованном массиве результатов с помощью цикла **ForEach** .</span><span class="sxs-lookup"><span data-stu-id="73be9-144">You can take the filtered result array and perform an action for each failure using the **ForEach** loop.</span></span> <span data-ttu-id="73be9-145">Ниже представлен пример с подробным описанием под ним. В этом примере отправляется запрос HTTP POST, для которого будут возвращены завершившиеся сбоем действия в области `My_Scope`.</span><span class="sxs-lookup"><span data-stu-id="73be9-145">Here's an example, followed by a detailed explanation, that sends an HTTP POST request with the response body of any actions that failed within the scope `My_Scope`.</span></span>

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

<span data-ttu-id="73be9-146">Подробно рассмотрим приведенный выше пример.</span><span class="sxs-lookup"><span data-stu-id="73be9-146">Here's a detailed walkthrough to describe what happens:</span></span>

1. <span data-ttu-id="73be9-147">Чтобы получить результат всех действий в области `My_Scope`, действие **Фильтр массива** выполняет фильтрацию `@result('My_Scope')`.</span><span class="sxs-lookup"><span data-stu-id="73be9-147">To get the result of all actions within `My_Scope`, the **Filter Array** action filters `@result('My_Scope')`.</span></span>

2. <span data-ttu-id="73be9-148">Условием отбора для действия **Фильтр массива** является любой элемент `@result()` с состоянием `Failed`.</span><span class="sxs-lookup"><span data-stu-id="73be9-148">The condition for **Filter Array** is any `@result()` item that has status equal to `Failed`.</span></span> <span data-ttu-id="73be9-149">Это условие применяет к массиву фильтр для получения массива с результатами действий, завершившихся сбоем, в области `My_Scope`.</span><span class="sxs-lookup"><span data-stu-id="73be9-149">This condition filters the array with all action results from `My_Scope` to an array with only failed action results.</span></span>

3. <span data-ttu-id="73be9-150">Затем выполняется действие **For Each** для данных, полученных в результате выполнения действия **Фильтровать массив**.</span><span class="sxs-lookup"><span data-stu-id="73be9-150">Perform a **For Each** action on the **Filtered Array** outputs.</span></span> <span data-ttu-id="73be9-151">При этом выполняется действие *для каждого* ранее отфильтрованного результата действия, завершившегося сбоем.</span><span class="sxs-lookup"><span data-stu-id="73be9-151">This step performs an action *for each* failed action result that was previously filtered.</span></span>

    <span data-ttu-id="73be9-152">Если определенное действие в области завершилось сбоем, действия в цикле `foreach` выполняются не более одного раза.</span><span class="sxs-lookup"><span data-stu-id="73be9-152">If a single action in the scope failed, the actions in the `foreach` run only once.</span></span> 
    <span data-ttu-id="73be9-153">Многие завершившиеся сбоем действия приведут к выполнению только одного действия на сбой.</span><span class="sxs-lookup"><span data-stu-id="73be9-153">Many failed actions cause one action per failure.</span></span>

4. <span data-ttu-id="73be9-154">Затем отправляется запрос HTTP POST для текста ответа элемента `foreach` или `@item()['outputs']['body']`.</span><span class="sxs-lookup"><span data-stu-id="73be9-154">Send an HTTP POST on the `foreach` item response body, or `@item()['outputs']['body']`.</span></span> <span data-ttu-id="73be9-155">Форматы элемента `@result()` и `@actions()` совпадают, поэтому они могут быть проанализированы одинаковым образом.</span><span class="sxs-lookup"><span data-stu-id="73be9-155">The `@result()` item shape is the same as the `@actions()` shape, and can be parsed the same way.</span></span>

5. <span data-ttu-id="73be9-156">В код выше включены два пользовательских заголовка с именем завершившегося сбоем действия `@item()['name']` и идентификатором отслеживания клиента выполнения со сбоем `@item()['clientTrackingId']`.</span><span class="sxs-lookup"><span data-stu-id="73be9-156">Include two custom headers with the failed action name `@item()['name']` and the failed run client tracking ID `@item()['clientTrackingId']`.</span></span>

<span data-ttu-id="73be9-157">Ниже приведен пример (для справочных целей) отдельного элемента `@result()` с отображением свойств `name`, `body` и `clientTrackingId`, проанализированных в примере выше.</span><span class="sxs-lookup"><span data-stu-id="73be9-157">For reference, here's an example of a single `@result()` item, showing the `name`, `body`, and `clientTrackingId` properties that are parsed in the previous example.</span></span> <span data-ttu-id="73be9-158">Вне цикла `foreach` `@result()` возвращает массив этих объектов.</span><span class="sxs-lookup"><span data-stu-id="73be9-158">Outside of a `foreach`, `@result()` returns an array of these objects.</span></span>

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

<span data-ttu-id="73be9-159">Выражения, представленные выше, можно использовать для выполнения различных шаблонов обработки исключений.</span><span class="sxs-lookup"><span data-stu-id="73be9-159">To perform different exception handling patterns, you can use the expressions shown previously.</span></span> <span data-ttu-id="73be9-160">Вы можете настроить выполнение одного действия обработки исключений вне области, которое принимает весь отфильтрованный массив сбоев, и удалить цикл `foreach`.</span><span class="sxs-lookup"><span data-stu-id="73be9-160">You might choose to execute a single exception handling action outside the scope that accepts the entire filtered array of failures, and remove the `foreach`.</span></span> <span data-ttu-id="73be9-161">Можно также включить другие полезные свойства из ответа `@result()`, приведенного выше.</span><span class="sxs-lookup"><span data-stu-id="73be9-161">You can also include other useful properties from the `@result()` response shown previously.</span></span>

## <a name="azure-diagnostics-and-telemetry"></a><span data-ttu-id="73be9-162">Система диагностики и телеметрия Azure</span><span class="sxs-lookup"><span data-stu-id="73be9-162">Azure Diagnostics and telemetry</span></span>

<span data-ttu-id="73be9-163">Приведенные выше шаблоны — эффективный способ обработки ошибок и исключений в выполнении. Однако можно также обнаруживать отдельные ошибки и реагировать на них независимо от выполнения.</span><span class="sxs-lookup"><span data-stu-id="73be9-163">The previous patterns are great way to handle errors and exceptions within a run, but you can also identify and respond to errors independent of the run itself.</span></span> 
<span data-ttu-id="73be9-164">[Система диагностики Azure](../logic-apps/logic-apps-monitor-your-logic-apps.md) предоставляет простой способ отправки всех событий рабочего процесса (включая все состояния выполнений и действий) в учетную запись хранения Azure или концентратор событий Azure.</span><span class="sxs-lookup"><span data-stu-id="73be9-164">[Azure Diagnostics](../logic-apps/logic-apps-monitor-your-logic-apps.md) provides a simple way to send all workflow events (including all run and action statuses) to an Azure Storage account or an Azure Event Hub.</span></span> <span data-ttu-id="73be9-165">Вы можете отслеживать журналы и метрики или публиковать их в любом средстве мониторинга для оценки состояния выполнения.</span><span class="sxs-lookup"><span data-stu-id="73be9-165">To evaluate run statuses, you can monitor the logs and metrics, or publish them into any monitoring tool you prefer.</span></span> <span data-ttu-id="73be9-166">К примеру, можно направлять поток всех событий через концентратор событий Azure в [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="73be9-166">One potential option is to stream all the events through Azure Event Hub into [Stream Analytics](https://azure.microsoft.com/services/stream-analytics/).</span></span> <span data-ttu-id="73be9-167">В Stream Analytics можно написать активные запросы для получения сведений об отклонении, средних показателей или сбоев из журналов диагностики.</span><span class="sxs-lookup"><span data-stu-id="73be9-167">In Stream Analytics, you can write live queries off any anomalies, averages, or failures from the diagnostic logs.</span></span> <span data-ttu-id="73be9-168">Stream Analytics может выводить данные в другие источники данных, такие как очереди, разделы, SQL, Azure Cosmos DB и Power BI.</span><span class="sxs-lookup"><span data-stu-id="73be9-168">Stream Analytics can easily output to other data sources like queues, topics, SQL, Azure Cosmos DB, and Power BI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73be9-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="73be9-169">Next Steps</span></span>

* [<span data-ttu-id="73be9-170">Сценарий обработки исключений и ведения журнала ошибок для приложений логики</span><span class="sxs-lookup"><span data-stu-id="73be9-170">See how a customer builds error handling with Azure Logic Apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
* [<span data-ttu-id="73be9-171">Примеры использования Logic Apps и распространенные сценарии</span><span class="sxs-lookup"><span data-stu-id="73be9-171">Find more Logic Apps examples and scenarios</span></span>](../logic-apps/logic-apps-examples-and-scenarios.md)
* [<span data-ttu-id="73be9-172">Создание шаблонов для развертывания приложений логики и управления выпусками</span><span class="sxs-lookup"><span data-stu-id="73be9-172">Learn how to create automated deployments for logic apps</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="73be9-173">Создание и развертывание приложений логики в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="73be9-173">Build and deploy logic apps with Visual Studio</span></span>](logic-apps-deploy-from-vs.md)

<!-- References -->
[retryPolicyMSDN]: https://docs.microsoft.com/rest/api/logic/actions-and-triggers#Anchor_9
