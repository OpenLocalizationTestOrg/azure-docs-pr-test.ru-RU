---
title: "Действия и триггеры рабочих процессов в Azure Logic Apps | Документация Майкрософт"
description: 
services: logic-apps
author: MandiOhlinger
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 86a53bb3-01ba-4e83-89b7-c9a7074cb159
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/17/2016
ms.author: LADocs; mandia
ms.openlocfilehash: bd3f1d225b974ebde889738bb435825658d1e1e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a><span data-ttu-id="94a18-102">Действия и триггеры рабочих процессов в Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="94a18-102">Workflow actions and triggers for Azure Logic Apps</span></span>

<span data-ttu-id="94a18-103">Приложения логики состоят из триггеров и действий.</span><span class="sxs-lookup"><span data-stu-id="94a18-103">Logic apps consist of triggers and actions.</span></span> <span data-ttu-id="94a18-104">Существует шесть типов триггеров.</span><span class="sxs-lookup"><span data-stu-id="94a18-104">There are six types of triggers.</span></span> <span data-ttu-id="94a18-105">У каждого из них свой интерфейс и разное поведение.</span><span class="sxs-lookup"><span data-stu-id="94a18-105">Each type has different interface and different behavior.</span></span> <span data-ttu-id="94a18-106">Подробные сведения см. в статье [Схема языка определения рабочих процессов в Azure Logic Apps](logic-apps-workflow-definition-language.md).</span><span class="sxs-lookup"><span data-stu-id="94a18-106">You can also learn about other details by looking at the details of the [Workflow Definition Language](logic-apps-workflow-definition-language.md).</span></span>  
  
<span data-ttu-id="94a18-107">Здесь вы узнаете о триггерах и действиях, а также об их использовании при создании приложений логики для оптимизации бизнес-процессов и рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="94a18-107">Read on to learn more about triggers and actions and how you might use them to build logic apps to improve your business processes and workflows.</span></span>  
  
### <a name="triggers"></a><span data-ttu-id="94a18-108">триггеры;</span><span class="sxs-lookup"><span data-stu-id="94a18-108">Triggers</span></span>  

<span data-ttu-id="94a18-109">Триггер указывает вызовы, которые могут инициировать запуск рабочего процесса приложения логики.</span><span class="sxs-lookup"><span data-stu-id="94a18-109">A trigger specifies the calls that can initiate a run of your logic app workflow.</span></span> <span data-ttu-id="94a18-110">Ниже приведены два разных способа инициировать запуск рабочего процесса:</span><span class="sxs-lookup"><span data-stu-id="94a18-110">Here are the two different ways to initiate a run of your workflow:</span></span>  
  
-   <span data-ttu-id="94a18-111">с помощью опрашивающего триггера;</span><span class="sxs-lookup"><span data-stu-id="94a18-111">A polling trigger</span></span>  

-   <span data-ttu-id="94a18-112">с помощью извещающего триггера путем вызова [REST API службы рабочих процессов](https://docs.microsoft.com/rest/api/logic/workflows).</span><span class="sxs-lookup"><span data-stu-id="94a18-112">A push trigger - by calling the [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span></span>  
  
<span data-ttu-id="94a18-113">Все триггеры содержат следующие элементы верхнего уровня:</span><span class="sxs-lookup"><span data-stu-id="94a18-113">All triggers contain these top-level elements:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property to create runs for>",
    "operationOptions": "<operation options on the trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a><span data-ttu-id="94a18-114">Типы триггеров и их входные данные</span><span class="sxs-lookup"><span data-stu-id="94a18-114">Trigger types and their inputs</span></span>  

<span data-ttu-id="94a18-115">Можно использовать такие типы триггеров:</span><span class="sxs-lookup"><span data-stu-id="94a18-115">You can use these types of triggers:</span></span>
  
-   <span data-ttu-id="94a18-116">**Триггер запросов** (request) — делает приложение логики конечной точкой для вызова.</span><span class="sxs-lookup"><span data-stu-id="94a18-116">**Request** \- Makes the logic app an endpoint for you to call</span></span>  
  
-   <span data-ttu-id="94a18-117">**Триггер повторения** (recurrence) — активируется на основе определенного расписания.</span><span class="sxs-lookup"><span data-stu-id="94a18-117">**Recurrence** \- Fires based on a defined schedule</span></span>  
  
-   <span data-ttu-id="94a18-118">**HTTP-триггер** — опрашивает конечную веб-точку HTTP.</span><span class="sxs-lookup"><span data-stu-id="94a18-118">**HTTP** \- Polls an HTTP web endpoint.</span></span> <span data-ttu-id="94a18-119">Конечная точка HTTP должна соответствовать определенному условию триггера — используя шаблон асинхронных операций  202 или возвращая массив.</span><span class="sxs-lookup"><span data-stu-id="94a18-119">The HTTP endpoint must conform to a specific triggering contract \- either by using a 202\-async pattern, or by returning an array</span></span>  
  
-   <span data-ttu-id="94a18-120">**ApiConnection** — выполняет опрос как триггер HTTP, но использует преимущества [интерфейсов API, управляемых Майкрософт](https://docs.microsoft.com/azure/connectors/apis-list).</span><span class="sxs-lookup"><span data-stu-id="94a18-120">**ApiConnection** \- Polls like the HTTP trigger, however, it takes advantage of the [Microsoft-managed APIs](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>  
  
-   <span data-ttu-id="94a18-121">**httpWebhook** — открывает конечную точку аналогично триггеру запуска вручную, но также вызывает указанный URL-адрес для регистрации и отмены регистрации.</span><span class="sxs-lookup"><span data-stu-id="94a18-121">**HTTPWebhook** \- Opens an endpoint, similar to the Manual trigger, however, it also calls out to a specified URL to register and unregister</span></span>  
  
-   <span data-ttu-id="94a18-122">**apiconnectionwebhook** — работает как триггер httpWebhook, используя преимущества интерфейсов API, управляемых Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="94a18-122">**ApiConnectionWebhook** \- Operates like the HTTPWebhook trigger by taking advantage of the Microsoft-managed APIs</span></span>       
    <span data-ttu-id="94a18-123">Каждый тип триггера имеет разный набор **входных данных**, определяющий его поведение.</span><span class="sxs-lookup"><span data-stu-id="94a18-123">Each trigger type has a different set of **inputs** that defines its behavior.</span></span>  
  
## <a name="request-trigger"></a><span data-ttu-id="94a18-124">Триггер запросов</span><span class="sxs-lookup"><span data-stu-id="94a18-124">Request trigger</span></span>  

<span data-ttu-id="94a18-125">Этот триггер служит в качестве конечной точки, которая вызывается с помощью HTTP-запроса для вызова приложения логики.</span><span class="sxs-lookup"><span data-stu-id="94a18-125">This trigger serves as an endpoint that you call via an HTTP Request to invoke your logic app.</span></span> <span data-ttu-id="94a18-126">Триггер запроса выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="94a18-126">A request trigger looks like this example:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type" : "request",
    "kind": "http",
    "inputs" : {
        "schema" : {
            "properties" : {
                "myInputProperty1" : { "type" : "string" },
                "myInputProperty2" : { "type" : "number" }
            },
        "required" : [ "myInputProperty1" ],
        "type" : "object"
        }
    }
} 
```

<span data-ttu-id="94a18-127">Имеется также необязательное свойство, которое называется **schema**.</span><span class="sxs-lookup"><span data-stu-id="94a18-127">There is also an optional property called **schema**:</span></span>  
  
|<span data-ttu-id="94a18-128">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="94a18-128">Element name</span></span>|<span data-ttu-id="94a18-129">Обязательно</span><span class="sxs-lookup"><span data-stu-id="94a18-129">Required</span></span>|<span data-ttu-id="94a18-130">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-130">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="94a18-131">schema</span><span class="sxs-lookup"><span data-stu-id="94a18-131">schema</span></span>|<span data-ttu-id="94a18-132">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-132">No</span></span>|<span data-ttu-id="94a18-133">Схема JSON, которая проверяет входящий запрос.</span><span class="sxs-lookup"><span data-stu-id="94a18-133">A JSON schema that validates the incoming request.</span></span> <span data-ttu-id="94a18-134">Используется, чтобы указать, на какие свойства ссылаться последующим действиям рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="94a18-134">Useful for helping subsequent workflow steps know which properties to reference.</span></span>|

<span data-ttu-id="94a18-135">Для вызова этой конечной точки необходимо вызвать API *listCallbackUrl*.</span><span class="sxs-lookup"><span data-stu-id="94a18-135">To invoke this endpoint, you need to call the *listCallbackUrl* API.</span></span> <span data-ttu-id="94a18-136">См. сведения в статье [Рабочие процессы](https://docs.microsoft.com/rest/api/logic/workflows).</span><span class="sxs-lookup"><span data-stu-id="94a18-136">See [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows).</span></span>  
  
## <a name="recurrence-trigger"></a><span data-ttu-id="94a18-137">Триггер повторения</span><span class="sxs-lookup"><span data-stu-id="94a18-137">Recurrence trigger</span></span>  

<span data-ttu-id="94a18-138">Триггер recurrence — это триггер, который выполняется на основе заданного расписания.</span><span class="sxs-lookup"><span data-stu-id="94a18-138">A Recurrence trigger is one that runs based on a defined schedule.</span></span> <span data-ttu-id="94a18-139">Такой триггер может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="94a18-139">Such a trigger might look like this example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="94a18-140">Как видно, это простой способ запуска рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="94a18-140">As you can see, it is a simple way to run a workflow.</span></span>  
  
|<span data-ttu-id="94a18-141">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="94a18-141">Element name</span></span>|<span data-ttu-id="94a18-142">Обязательно</span><span class="sxs-lookup"><span data-stu-id="94a18-142">Required</span></span>|<span data-ttu-id="94a18-143">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-143">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="94a18-144">frequency</span><span class="sxs-lookup"><span data-stu-id="94a18-144">frequency</span></span>|<span data-ttu-id="94a18-145">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-145">Yes</span></span>|<span data-ttu-id="94a18-146">Частота выполнения триггера.</span><span class="sxs-lookup"><span data-stu-id="94a18-146">How often the trigger executes.</span></span> <span data-ttu-id="94a18-147">Используйте только одно из этих значений: Second, Minute, Hour, Day, Week, Month или Year.</span><span class="sxs-lookup"><span data-stu-id="94a18-147">Use only one of these possible values: second, minute, hour, day, week, month, or year</span></span>|  
|<span data-ttu-id="94a18-148">interval</span><span class="sxs-lookup"><span data-stu-id="94a18-148">interval</span></span>|<span data-ttu-id="94a18-149">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-149">Yes</span></span>|<span data-ttu-id="94a18-150">Интервал повторения в указанной единице времени</span><span class="sxs-lookup"><span data-stu-id="94a18-150">Interval of the given frequency for the recurrence</span></span>|  
|<span data-ttu-id="94a18-151">startTime</span><span class="sxs-lookup"><span data-stu-id="94a18-151">startTime</span></span>|<span data-ttu-id="94a18-152">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-152">No</span></span>|<span data-ttu-id="94a18-153">Используется, если для свойства startTime указано значение без смещения от UTC.</span><span class="sxs-lookup"><span data-stu-id="94a18-153">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
|<span data-ttu-id="94a18-154">timeZone</span><span class="sxs-lookup"><span data-stu-id="94a18-154">timeZone</span></span>|<span data-ttu-id="94a18-155">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-155">no</span></span>|<span data-ttu-id="94a18-156">Используется, если для свойства startTime указано значение без смещения от UTC.</span><span class="sxs-lookup"><span data-stu-id="94a18-156">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
  
<span data-ttu-id="94a18-157">Вы также можете запланировать запуск триггера в определенный момент времени в будущем.</span><span class="sxs-lookup"><span data-stu-id="94a18-157">You can also schedule a trigger to start executing at some point in the future.</span></span> <span data-ttu-id="94a18-158">Например, если вы хотите, чтобы еженедельный отчет запускался каждый понедельник, можно запланировать запуск приложения логики каждый понедельник, создав следующий триггер:</span><span class="sxs-lookup"><span data-stu-id="94a18-158">For example, if you want to start a weekly report every Monday you can schedule the logic app to start every Monday by creating the following trigger:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Week",
        "interval": "1",
        "startTime" : "2015-06-22T00:00:00Z"
    }
}
```

## <a name="http-trigger"></a><span data-ttu-id="94a18-159">Триггер HTTP</span><span class="sxs-lookup"><span data-stu-id="94a18-159">HTTP trigger</span></span>  

<span data-ttu-id="94a18-160">Триггеры HTTP опрашивают указанную конечную точку и проверяют ответ, чтобы определить, следует ли запускать рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="94a18-160">HTTP triggers poll a specified endpoint and check the response to determine whether the workflow should be executed.</span></span> <span data-ttu-id="94a18-161">Объект входных данных принимает набор параметров, необходимый для создания HTTP-вызова:</span><span class="sxs-lookup"><span data-stu-id="94a18-161">The inputs object takes the set of parameters required to construct an HTTP call:</span></span>  
  
|<span data-ttu-id="94a18-162">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="94a18-162">Element name</span></span>|<span data-ttu-id="94a18-163">Обязательно</span><span class="sxs-lookup"><span data-stu-id="94a18-163">Required</span></span>|<span data-ttu-id="94a18-164">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-164">Description</span></span>|<span data-ttu-id="94a18-165">Тип</span><span class="sxs-lookup"><span data-stu-id="94a18-165">Type</span></span>|  
|----------------|------------|---------------|--------|  
|<span data-ttu-id="94a18-166">метод</span><span class="sxs-lookup"><span data-stu-id="94a18-166">method</span></span>|<span data-ttu-id="94a18-167">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-167">yes</span></span>|<span data-ttu-id="94a18-168">Это может быть один из следующих методов HTTP: GET, POST, PUT, DELETE, HEAD или PATCH.</span><span class="sxs-lookup"><span data-stu-id="94a18-168">Can be one of the following HTTP methods: GET, POST, PUT, DELETE, PATCH, or HEAD</span></span>|<span data-ttu-id="94a18-169">Строка</span><span class="sxs-lookup"><span data-stu-id="94a18-169">String</span></span>|  
|<span data-ttu-id="94a18-170">uri</span><span class="sxs-lookup"><span data-stu-id="94a18-170">uri</span></span>|<span data-ttu-id="94a18-171">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-171">yes</span></span>|<span data-ttu-id="94a18-172">Вызываемая конечная точка HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="94a18-172">The http or https endpoint that is called.</span></span> <span data-ttu-id="94a18-173">Не более 2 КБ.</span><span class="sxs-lookup"><span data-stu-id="94a18-173">Maximum of 2 kilobytes.</span></span>|<span data-ttu-id="94a18-174">string</span><span class="sxs-lookup"><span data-stu-id="94a18-174">String</span></span>|  
|<span data-ttu-id="94a18-175">Запросы</span><span class="sxs-lookup"><span data-stu-id="94a18-175">queries</span></span>|<span data-ttu-id="94a18-176">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-176">No</span></span>|<span data-ttu-id="94a18-177">Объект, представляющий параметры запроса для добавления к URL-адресу.</span><span class="sxs-lookup"><span data-stu-id="94a18-177">An object representing the query parameters to add to the URL.</span></span> <span data-ttu-id="94a18-178">Например, `"queries" : { "api-version": "2015-02-01" }` добавляет `?api-version=2015-02-01` в URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="94a18-178">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|<span data-ttu-id="94a18-179">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-179">Object</span></span>|  
|<span data-ttu-id="94a18-180">headers</span><span class="sxs-lookup"><span data-stu-id="94a18-180">headers</span></span>|<span data-ttu-id="94a18-181">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-181">No</span></span>|<span data-ttu-id="94a18-182">Объект, представляющий все заголовки, которые отправляются в запрос.</span><span class="sxs-lookup"><span data-stu-id="94a18-182">An object representing each of the headers that is sent to the request.</span></span> <span data-ttu-id="94a18-183">Например, чтобы задать язык и тип запроса: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="94a18-183">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|<span data-ttu-id="94a18-184">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-184">Object</span></span>|  
|<span data-ttu-id="94a18-185">текст</span><span class="sxs-lookup"><span data-stu-id="94a18-185">body</span></span>|<span data-ttu-id="94a18-186">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-186">No</span></span>|<span data-ttu-id="94a18-187">Объект, представляющий полезные данные, отправляемые конечной точке.</span><span class="sxs-lookup"><span data-stu-id="94a18-187">An object representing the payload that is sent to the endpoint.</span></span>|<span data-ttu-id="94a18-188">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-188">Object</span></span>|  
|<span data-ttu-id="94a18-189">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="94a18-189">retryPolicy</span></span>|<span data-ttu-id="94a18-190">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-190">No</span></span>|<span data-ttu-id="94a18-191">Объект, который позволяет настроить поведение повтора при возникновении ошибок 4xx или 5xx.</span><span class="sxs-lookup"><span data-stu-id="94a18-191">An object that lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|<span data-ttu-id="94a18-192">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-192">Object</span></span>|  
|<span data-ttu-id="94a18-193">authentication</span><span class="sxs-lookup"><span data-stu-id="94a18-193">authentication</span></span>|<span data-ttu-id="94a18-194">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-194">No</span></span>|<span data-ttu-id="94a18-195">Представляет метод для проверки подлинности запроса.</span><span class="sxs-lookup"><span data-stu-id="94a18-195">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="94a18-196">Дополнительные сведения см. в статье [Исходящая проверка подлинности планировщика](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="94a18-196">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="94a18-197">Помимо планировщика, имеется еще одно поддерживаемое свойство: `authority`. По умолчанию его значение равно `https://login.windows.net`, если не указано другое. Также можно использовать другое значение, например `https://login.windows\-ppe.net`.</span><span class="sxs-lookup"><span data-stu-id="94a18-197">Beyond scheduler, there is one more supported property: `authority` By default, this value is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|<span data-ttu-id="94a18-198">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-198">Object</span></span>|  
  
<span data-ttu-id="94a18-199">Для эффективной работы с приложением логики триггеру HTTP требуется, чтобы HTTP API соответствовал определенному шаблону.</span><span class="sxs-lookup"><span data-stu-id="94a18-199">The HTTP trigger requires the HTTP API to conform with a specific pattern to work well with your logic app.</span></span> <span data-ttu-id="94a18-200">Необходимы следующие поля:</span><span class="sxs-lookup"><span data-stu-id="94a18-200">It requires the following fields:</span></span>  
  
|<span data-ttu-id="94a18-201">Ответ</span><span class="sxs-lookup"><span data-stu-id="94a18-201">Response</span></span>|<span data-ttu-id="94a18-202">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-202">Description</span></span>|  
|------------|---------------|  
|<span data-ttu-id="94a18-203">Код состояния</span><span class="sxs-lookup"><span data-stu-id="94a18-203">Status code</span></span>|<span data-ttu-id="94a18-204">Код состояния 200 \(ОК\) инициирует запуск.</span><span class="sxs-lookup"><span data-stu-id="94a18-204">Status code 200 \(OK\) to cause a run.</span></span> <span data-ttu-id="94a18-205">Другие коды состояния не вызывают запуск.</span><span class="sxs-lookup"><span data-stu-id="94a18-205">Any other status code doesn't cause a run.</span></span>|  
|<span data-ttu-id="94a18-206">Заголовок Retry\-After</span><span class="sxs-lookup"><span data-stu-id="94a18-206">Retry\-after header</span></span>|<span data-ttu-id="94a18-207">Количество секунд перед повторным опросом конечной точки приложением логики.</span><span class="sxs-lookup"><span data-stu-id="94a18-207">Number of seconds until the logic app polls the endpoint again.</span></span>|  
|<span data-ttu-id="94a18-208">Заголовок Location</span><span class="sxs-lookup"><span data-stu-id="94a18-208">Location header</span></span>|<span data-ttu-id="94a18-209">URL-адрес для вызова во время следующего интервала опроса.</span><span class="sxs-lookup"><span data-stu-id="94a18-209">The URL to call on the next polling interval.</span></span> <span data-ttu-id="94a18-210">Если не указан, используется исходный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="94a18-210">If not specified, the original URL is used.</span></span>|  
  
<span data-ttu-id="94a18-211">Ниже приведены некоторые примеры различных поведений для различных типов запросов.</span><span class="sxs-lookup"><span data-stu-id="94a18-211">Here are some examples of different behaviors for different types of requests:</span></span>  
  
|<span data-ttu-id="94a18-212">Код ответа</span><span class="sxs-lookup"><span data-stu-id="94a18-212">Response code</span></span>|<span data-ttu-id="94a18-213">Retry\-After</span><span class="sxs-lookup"><span data-stu-id="94a18-213">Retry\-After</span></span>|<span data-ttu-id="94a18-214">Поведение</span><span class="sxs-lookup"><span data-stu-id="94a18-214">Behavior</span></span>|  
|-----------------|----------------|------------|  
|<span data-ttu-id="94a18-215">200</span><span class="sxs-lookup"><span data-stu-id="94a18-215">200</span></span>|<span data-ttu-id="94a18-216">\(Нет\)</span><span class="sxs-lookup"><span data-stu-id="94a18-216">\(none\)</span></span>|<span data-ttu-id="94a18-217">Недопустимый триггер. Необходимо указать заголовок Retry\-After. В противном случае обработчик не будет выполнять опрос при следующем запросе.</span><span class="sxs-lookup"><span data-stu-id="94a18-217">Not a valid trigger, Retry\-After is required, or else the engine never polls for the next request.</span></span>|  
|<span data-ttu-id="94a18-218">202</span><span class="sxs-lookup"><span data-stu-id="94a18-218">202</span></span>|<span data-ttu-id="94a18-219">60</span><span class="sxs-lookup"><span data-stu-id="94a18-219">60</span></span>|<span data-ttu-id="94a18-220">Рабочий процесс не запускается.</span><span class="sxs-lookup"><span data-stu-id="94a18-220">Do not trigger the workflow.</span></span> <span data-ttu-id="94a18-221">Следующая попытка произойдет через одну минуту.</span><span class="sxs-lookup"><span data-stu-id="94a18-221">The next attempt happens in one minute.</span></span>|  
|<span data-ttu-id="94a18-222">200</span><span class="sxs-lookup"><span data-stu-id="94a18-222">200</span></span>|<span data-ttu-id="94a18-223">10</span><span class="sxs-lookup"><span data-stu-id="94a18-223">10</span></span>|<span data-ttu-id="94a18-224">Рабочий процесс запускается, и через 10 секунд проверяется наличие дополнительного содержимого.</span><span class="sxs-lookup"><span data-stu-id="94a18-224">Run the workflow, and check again for more content in 10 seconds.</span></span>|  
|<span data-ttu-id="94a18-225">400</span><span class="sxs-lookup"><span data-stu-id="94a18-225">400</span></span>|<span data-ttu-id="94a18-226">\(Нет\)</span><span class="sxs-lookup"><span data-stu-id="94a18-226">\(none\)</span></span>|<span data-ttu-id="94a18-227">Недопустимый запрос, рабочий процесс не запускается.</span><span class="sxs-lookup"><span data-stu-id="94a18-227">Bad request, do not run the workflow.</span></span> <span data-ttu-id="94a18-228">Если **политика повтора** не задана, используется политика по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="94a18-228">If there is no **Retry Policy** defined, then the default policy is used.</span></span> <span data-ttu-id="94a18-229">По достижении определенного количества повторных попыток триггер перестает быть допустимым.</span><span class="sxs-lookup"><span data-stu-id="94a18-229">After the number of retries has been reached, the trigger is no longer valid.</span></span>|  
|<span data-ttu-id="94a18-230">500</span><span class="sxs-lookup"><span data-stu-id="94a18-230">500</span></span>|<span data-ttu-id="94a18-231">\(Нет\)</span><span class="sxs-lookup"><span data-stu-id="94a18-231">\(none\)</span></span>|<span data-ttu-id="94a18-232">Ошибка сервера. Рабочий процесс не запускается.</span><span class="sxs-lookup"><span data-stu-id="94a18-232">Server error, do not run the workflow.</span></span>  <span data-ttu-id="94a18-233">Если **политика повтора** не задана, используется политика по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="94a18-233">If there is no **Retry Policy** defined, then the default policy is used.</span></span> <span data-ttu-id="94a18-234">По достижении определенного количества повторных попыток триггер перестает быть допустимым.</span><span class="sxs-lookup"><span data-stu-id="94a18-234">After the number of retries has been reached, the trigger is no longer valid.</span></span>|  
  
<span data-ttu-id="94a18-235">Выходные данные триггера HTTP выглядят, как приведено ниже.</span><span class="sxs-lookup"><span data-stu-id="94a18-235">The outputs of an HTTP trigger look like this example:</span></span>  
  
|<span data-ttu-id="94a18-236">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="94a18-236">Element name</span></span>|<span data-ttu-id="94a18-237">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-237">Description</span></span>|<span data-ttu-id="94a18-238">Тип</span><span class="sxs-lookup"><span data-stu-id="94a18-238">Type</span></span>|  
|----------------|---------------|--------|  
|<span data-ttu-id="94a18-239">headers</span><span class="sxs-lookup"><span data-stu-id="94a18-239">headers</span></span>|<span data-ttu-id="94a18-240">Заголовки HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="94a18-240">The headers of the http response.</span></span>|<span data-ttu-id="94a18-241">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-241">Object</span></span>|  
|<span data-ttu-id="94a18-242">текст</span><span class="sxs-lookup"><span data-stu-id="94a18-242">body</span></span>|<span data-ttu-id="94a18-243">Текст HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="94a18-243">The body of the http response.</span></span>|<span data-ttu-id="94a18-244">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-244">Object</span></span>|  
  
## <a name="api-connection-trigger"></a><span data-ttu-id="94a18-245">Триггер подключения API</span><span class="sxs-lookup"><span data-stu-id="94a18-245">API Connection trigger</span></span>  

<span data-ttu-id="94a18-246">Триггер подключения API по своей функциональности аналогичен триггеру HTTP.</span><span class="sxs-lookup"><span data-stu-id="94a18-246">The API connection trigger is similar to the HTTP trigger in its basic functionality.</span></span> <span data-ttu-id="94a18-247">Однако параметры для определения действия различаются.</span><span class="sxs-lookup"><span data-stu-id="94a18-247">However, the parameters for identifying the action are different.</span></span> <span data-ttu-id="94a18-248">Пример:</span><span class="sxs-lookup"><span data-stu-id="94a18-248">Here is an example:</span></span>  
  
```json
"dailyReport" : {
    "type": "ApiConnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://myarticles.example.com/"
            },
        }
        "connection": {
            "name": "@parameters('$connections')['myconnection'].name"
        }
    },  
    "method": "POST",
    "body": {
        "category": "awesomest"
    }
}
```

|<span data-ttu-id="94a18-249">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="94a18-249">Element name</span></span>|<span data-ttu-id="94a18-250">Обязательно</span><span class="sxs-lookup"><span data-stu-id="94a18-250">Required</span></span>|<span data-ttu-id="94a18-251">Тип</span><span class="sxs-lookup"><span data-stu-id="94a18-251">Type</span></span>|<span data-ttu-id="94a18-252">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-252">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="94a18-253">host</span><span class="sxs-lookup"><span data-stu-id="94a18-253">host</span></span>|<span data-ttu-id="94a18-254">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-254">Yes</span></span>||<span data-ttu-id="94a18-255">Шлюз, где размещено приложение API, и его идентификатор.</span><span class="sxs-lookup"><span data-stu-id="94a18-255">The ApiApp hosted gateway and id.</span></span>|  
|<span data-ttu-id="94a18-256">метод</span><span class="sxs-lookup"><span data-stu-id="94a18-256">method</span></span>|<span data-ttu-id="94a18-257">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-257">Yes</span></span>|<span data-ttu-id="94a18-258">Строка</span><span class="sxs-lookup"><span data-stu-id="94a18-258">String</span></span>|<span data-ttu-id="94a18-259">Это может быть один из следующих методов HTTP: **GET**, **POST**, **PUT**, **DELETE**, **HEAD** или **PATCH**.</span><span class="sxs-lookup"><span data-stu-id="94a18-259">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="94a18-260">Запросы</span><span class="sxs-lookup"><span data-stu-id="94a18-260">queries</span></span>|<span data-ttu-id="94a18-261">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-261">No</span></span>|<span data-ttu-id="94a18-262">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-262">Object</span></span>|<span data-ttu-id="94a18-263">Представляет параметры запроса для добавления в URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="94a18-263">Represents the query parameters to be added to the URL.</span></span> <span data-ttu-id="94a18-264">Например, `"queries" : { "api-version": "2015-02-01" }` добавляет `?api-version=2015-02-01` в URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="94a18-264">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="94a18-265">headers</span><span class="sxs-lookup"><span data-stu-id="94a18-265">headers</span></span>|<span data-ttu-id="94a18-266">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-266">No</span></span>|<span data-ttu-id="94a18-267">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-267">Object</span></span>|<span data-ttu-id="94a18-268">Представляет все заголовки, которые отправляются в запрос.</span><span class="sxs-lookup"><span data-stu-id="94a18-268">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="94a18-269">Например, чтобы задать язык и тип запроса: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="94a18-269">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="94a18-270">текст</span><span class="sxs-lookup"><span data-stu-id="94a18-270">body</span></span>|<span data-ttu-id="94a18-271">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-271">No</span></span>|<span data-ttu-id="94a18-272">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-272">Object</span></span>|<span data-ttu-id="94a18-273">Представляет полезные данные, отправляемые конечной точке.</span><span class="sxs-lookup"><span data-stu-id="94a18-273">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="94a18-274">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="94a18-274">retryPolicy</span></span>|<span data-ttu-id="94a18-275">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-275">No</span></span>|<span data-ttu-id="94a18-276">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-276">Object</span></span>|<span data-ttu-id="94a18-277">Позволяет настроить поведение повтора при возникновении ошибок 4xx или 5xx.</span><span class="sxs-lookup"><span data-stu-id="94a18-277">Allows you to customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="94a18-278">authentication</span><span class="sxs-lookup"><span data-stu-id="94a18-278">authentication</span></span>|<span data-ttu-id="94a18-279">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-279">No</span></span>|<span data-ttu-id="94a18-280">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-280">Object</span></span>|<span data-ttu-id="94a18-281">Представляет метод для проверки подлинности запроса.</span><span class="sxs-lookup"><span data-stu-id="94a18-281">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="94a18-282">Дополнительные сведения см. в статье [Исходящая проверка подлинности планировщика](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="94a18-282">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span></span>|  
  
<span data-ttu-id="94a18-283">Ниже приведены свойства узла.</span><span class="sxs-lookup"><span data-stu-id="94a18-283">The properties for host are:</span></span>  
  
|<span data-ttu-id="94a18-284">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="94a18-284">Element name</span></span>|<span data-ttu-id="94a18-285">Обязательно</span><span class="sxs-lookup"><span data-stu-id="94a18-285">Required</span></span>|<span data-ttu-id="94a18-286">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-286">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="94a18-287">api runtimeUrl</span><span class="sxs-lookup"><span data-stu-id="94a18-287">api runtimeUrl</span></span>|<span data-ttu-id="94a18-288">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-288">Yes</span></span>|<span data-ttu-id="94a18-289">Конечная точка управляемого API.</span><span class="sxs-lookup"><span data-stu-id="94a18-289">The endpoint of the managed API.</span></span>|  
|<span data-ttu-id="94a18-290">connection name</span><span class="sxs-lookup"><span data-stu-id="94a18-290">connection name</span></span>||<span data-ttu-id="94a18-291">Должно быть ссылкой на параметр с именем `$connection` и представлять имя подключения управляемого API, которое использует рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="94a18-291">Must be a reference to a parameter called `$connection` and is the name of the managed API connection that the workflow uses.</span></span>|
  
<span data-ttu-id="94a18-292">Выходные данные триггера подключения API:</span><span class="sxs-lookup"><span data-stu-id="94a18-292">The outputs of an API connection trigger are:</span></span>
  
|<span data-ttu-id="94a18-293">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="94a18-293">Element name</span></span>|<span data-ttu-id="94a18-294">Тип</span><span class="sxs-lookup"><span data-stu-id="94a18-294">Type</span></span>|<span data-ttu-id="94a18-295">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-295">Description</span></span>|  
|----------------|--------|---------------|  
|<span data-ttu-id="94a18-296">headers</span><span class="sxs-lookup"><span data-stu-id="94a18-296">headers</span></span>|<span data-ttu-id="94a18-297">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-297">Object</span></span>|<span data-ttu-id="94a18-298">Заголовки HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="94a18-298">The headers of the http response.</span></span>|  
|<span data-ttu-id="94a18-299">текст</span><span class="sxs-lookup"><span data-stu-id="94a18-299">body</span></span>|<span data-ttu-id="94a18-300">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-300">Object</span></span>|<span data-ttu-id="94a18-301">Текст HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="94a18-301">The body of the http response.</span></span>|  
  
## <a name="httpwebhook-trigger"></a><span data-ttu-id="94a18-302">Триггер httpWebhook</span><span class="sxs-lookup"><span data-stu-id="94a18-302">HTTPWebhook trigger</span></span>  

<span data-ttu-id="94a18-303">Триггер httpWebhook открывает конечную точку аналогично триггеру запуска вручную, но также вызывает указанный URL-адрес для регистрации и отмены регистрации.</span><span class="sxs-lookup"><span data-stu-id="94a18-303">The HTTPWebhook trigger opens an endpoint, similar to the manual trigger, but the HTTPWebhook trigger also calls out to a specified URL to register and unregister.</span></span> <span data-ttu-id="94a18-304">Триггер httpWebhook может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="94a18-304">Here's an example of what an HTTPWebhook trigger might look like:</span></span>  

```json
"myappspottrigger": {
    "type": "httpWebhook",
    "inputs": {
        "subscribe": {
            "method": "POST",
            "uri": "https://pubsubhubbub.appspot.com/subscribe",
            "headers": { },
            "body": {
                "hub.callback": "@{listCallbackUrl()}",
                "hub.mode": "subscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "authentication": { },
            "retryPolicy": { }
        },
        "unsubscribe": {
            "url": "https://pubsubhubbub.appspot.com/subscribe",
            "body": {
                "hub.callback": "@{workflow().endpoint}@{listCallbackUrl()}",
                "hub.mode": "unsubscribe",
                "hub.topic": "https://pubsubhubbub.appspot.com/articleCategories/technology"
            },
            "method": "POST",
            "authentication": { }
        }
    },
    "conditions": [ ]
    }
```

<span data-ttu-id="94a18-305">Многие из этих разделов являются необязательными, и поведение объекта webhook зависит от того, какие разделы предоставлены или опущены.</span><span class="sxs-lookup"><span data-stu-id="94a18-305">Many of these sections are optional, and the behavior of the Webhook depends on which sections are provided or omitted.</span></span>  
<span data-ttu-id="94a18-306">Ниже приведены свойства объекта webhook.</span><span class="sxs-lookup"><span data-stu-id="94a18-306">The properties of a Webhook are as follows:</span></span>  
  
|<span data-ttu-id="94a18-307">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="94a18-307">Element name</span></span>|<span data-ttu-id="94a18-308">Обязательно</span><span class="sxs-lookup"><span data-stu-id="94a18-308">Required</span></span>|<span data-ttu-id="94a18-309">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-309">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="94a18-310">subscribe</span><span class="sxs-lookup"><span data-stu-id="94a18-310">subscribe</span></span>|<span data-ttu-id="94a18-311">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-311">No</span></span>|<span data-ttu-id="94a18-312">Исходящий запрос, который вызывается, когда триггер создается, и выполняет первоначальную регистрацию.</span><span class="sxs-lookup"><span data-stu-id="94a18-312">The outgoing request that is called when the trigger is created and performs the initial registration.</span></span>|  
|<span data-ttu-id="94a18-313">unsubscribe</span><span class="sxs-lookup"><span data-stu-id="94a18-313">unsubscribe</span></span>|<span data-ttu-id="94a18-314">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-314">No</span></span>|<span data-ttu-id="94a18-315">Исходящий запрос при удалении триггера.</span><span class="sxs-lookup"><span data-stu-id="94a18-315">The outgoing request when the trigger is deleted.</span></span>|  
  
-   <span data-ttu-id="94a18-316">**subscribe** является исходящим вызовом для начала прослушивания событий.</span><span class="sxs-lookup"><span data-stu-id="94a18-316">**Subscribe** is the outgoing call that's made to start listening to events.</span></span> <span data-ttu-id="94a18-317">Этот вызов запускается с тем же набором параметров, что и обычные действия HTTP.</span><span class="sxs-lookup"><span data-stu-id="94a18-317">This call starts with the same set of parameters that the normal HTTP actions do.</span></span> <span data-ttu-id="94a18-318">Этот исходящий вызов выполняется при любом изменении рабочего процесса, например когда происходит отзыв учетных данных или изменяются входные параметры триггера.</span><span class="sxs-lookup"><span data-stu-id="94a18-318">This outgoing call is made any time the workflow changes in any way, for example, whenever the credentials are rolled, or the trigger's input parameters change.</span></span>
  
    <span data-ttu-id="94a18-319">Для поддержки этого вызова используется новая функция: `@listCallbackUrl()`.</span><span class="sxs-lookup"><span data-stu-id="94a18-319">To support this call, there is a new function: `@listCallbackUrl()`.</span></span> <span data-ttu-id="94a18-320">Эта функция возвращает уникальный URL-адрес для конкретного триггера в этом рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="94a18-320">This function returns a unique URL for this specific trigger in this workflow.</span></span> <span data-ttu-id="94a18-321">Это уникальный идентификатор для конечных точек, использующих REST для службы.</span><span class="sxs-lookup"><span data-stu-id="94a18-321">It represents the unique identifier for the endpoints that use the Service REST.</span></span>  
  
-   <span data-ttu-id="94a18-322">**unsubscribe** вызывается, когда операция делает этот триггер недействительным, например в результате таких действий:</span><span class="sxs-lookup"><span data-stu-id="94a18-322">**Unsubscribe** is called when an operation renders this trigger invalid, including:</span></span>  
  
    -   <span data-ttu-id="94a18-323">удаление или отключение триггера;</span><span class="sxs-lookup"><span data-stu-id="94a18-323">Deleting or disabling the trigger</span></span>  
  
    -   <span data-ttu-id="94a18-324">удаление или отключение рабочего процесса;</span><span class="sxs-lookup"><span data-stu-id="94a18-324">Deleting or disabling the workflow</span></span>  
  
    -   <span data-ttu-id="94a18-325">удаление или отключение подписки.</span><span class="sxs-lookup"><span data-stu-id="94a18-325">Deleting or disabling the subscription</span></span>  
  
    <span data-ttu-id="94a18-326">Приложение логики автоматически вызывает действие отмены подписки.</span><span class="sxs-lookup"><span data-stu-id="94a18-326">The logic app automatically calls the unsubscribe action.</span></span> <span data-ttu-id="94a18-327">Параметры этой функции совпадают с параметрами триггера HTTP.</span><span class="sxs-lookup"><span data-stu-id="94a18-327">The parameters to this function are the same as the HTTP trigger.</span></span>  
  
    <span data-ttu-id="94a18-328">Выходные данные триггера httpWebhook представляют собой содержимое входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="94a18-328">The outputs of the HTTPWebhook trigger are the contents of the incoming request:</span></span>  
  
|<span data-ttu-id="94a18-329">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="94a18-329">Element name</span></span>|<span data-ttu-id="94a18-330">Тип</span><span class="sxs-lookup"><span data-stu-id="94a18-330">Type</span></span>|<span data-ttu-id="94a18-331">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-331">Description</span></span>|  
|-----------------|--------|---------------|  
|<span data-ttu-id="94a18-332">headers</span><span class="sxs-lookup"><span data-stu-id="94a18-332">headers</span></span>|<span data-ttu-id="94a18-333">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-333">Object</span></span>|<span data-ttu-id="94a18-334">Заголовки HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="94a18-334">The headers of the http request.</span></span>|  
|<span data-ttu-id="94a18-335">текст</span><span class="sxs-lookup"><span data-stu-id="94a18-335">body</span></span>|<span data-ttu-id="94a18-336">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-336">Object</span></span>|<span data-ttu-id="94a18-337">Текст HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="94a18-337">The body of the http request.</span></span>|  

<span data-ttu-id="94a18-338">Ограничения для действий webhook можно указать так же, как [ограничения для асинхронной модели HTTP](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="94a18-338">Limits on a webhook action can be specified in the same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  

## <a name="conditions"></a><span data-ttu-id="94a18-339">Условия</span><span class="sxs-lookup"><span data-stu-id="94a18-339">Conditions</span></span>  

<span data-ttu-id="94a18-340">Для любого триггера можно задать одно или несколько условий, определяющих, должен ли выполняться рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="94a18-340">For any trigger, you can use one or more conditions to determine whether the workflow should run or not.</span></span> <span data-ttu-id="94a18-341">Например:</span><span class="sxs-lookup"><span data-stu-id="94a18-341">For example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "conditions": [ {
        "expression": "@parameters('sendReports')"
    } ],
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="94a18-342">В этом случае отчет запускается, если для параметра рабочего процесса `sendReports` установлено значение true.</span><span class="sxs-lookup"><span data-stu-id="94a18-342">In this case, the report only triggers while the workflow's `sendReports` parameter is set to true.</span></span> <span data-ttu-id="94a18-343">Условия могут ссылаться на код состояния триггера.</span><span class="sxs-lookup"><span data-stu-id="94a18-343">Finally, conditions may reference the status code of the trigger.</span></span> <span data-ttu-id="94a18-344">Например, можно настроить так, чтобы рабочий процесс запускался только в том случае, если веб-сайт возвращает код состояния 500:</span><span class="sxs-lookup"><span data-stu-id="94a18-344">For example, you could kick off a workflow only when your website returns a status code 500, as follows:</span></span>
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> <span data-ttu-id="94a18-345">Если любое выражение ссылается на код состояния триггера \(каким-либо образом\), поведение по умолчанию \(запускать только при возникновении кода состояния 200 \(ОК\)\) изменяется.</span><span class="sxs-lookup"><span data-stu-id="94a18-345">When any expression references the status code of the trigger \(in any way\), the default behavior \(trigger only on 200 \(OK\)\) is replaced.</span></span> <span data-ttu-id="94a18-346">Например, если требуется запуск при возникновении кода состояния 200 и 201, необходимо включить `@or(equals(triggers().code, 200),equals(triggers().code,201))` в качестве условия.</span><span class="sxs-lookup"><span data-stu-id="94a18-346">For example, if you want to trigger on both status code 200 and status code 201, you have to include: `@or(equals(triggers().code, 200),equals(triggers().code,201))` as your condition.</span></span>  
  
## <a name="start-multiple-runs-for-a-request"></a><span data-ttu-id="94a18-347">Запуск нескольких выполнений запроса</span><span class="sxs-lookup"><span data-stu-id="94a18-347">Start multiple runs for a request</span></span>

<span data-ttu-id="94a18-348">Для запуска нескольких выполнений одного запроса можно использовать `splitOn`. Например, при необходимости опросить конечную точку, которая может получить несколько новых элементов между интервалами опроса.</span><span class="sxs-lookup"><span data-stu-id="94a18-348">To kick off multiple runs for a single request, `splitOn` is useful, for example, when you want to poll an endpoint that can have multiple new items between polling intervals.</span></span>
  
<span data-ttu-id="94a18-349">Используя `splitOn`, можно указать свойство в полезных данных ответа, содержащих массив элементов, каждый из которых необходим для запуска триггера.</span><span class="sxs-lookup"><span data-stu-id="94a18-349">With `splitOn`, you specify the property inside the response payload that contains the array of items, each of which you want to use to start a run of the trigger.</span></span> <span data-ttu-id="94a18-350">Представьте, что у вас есть API, который возвращает следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="94a18-350">For example, imagine you have an API that returns the following response:</span></span>  
  
```json
{
    "Status" : "success",
    "Rows" : [
        {  
            "id" : 938109380,
            "name" : "mycoolrow"
        },
        {
            "id" : 938109381,
            "name" : "another row"
        }
    ]
}
```
  
<span data-ttu-id="94a18-351">Приложению логики необходимо только содержимое строк, поэтому можно создать триггер, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="94a18-351">Your logic app only needs the Rows content, so you can construct your trigger like this example:</span></span>  
  
```json
"mysplitter" : {
    "type" : "http",
    "recurrence": {
        "frequency": "Minute",
        "interval": "1"
    },
    "intputs" : {
        "uri" : "https://mydomain.com/myAPI",
        "method" : "GET"
    },
    "splitOn" : "@triggerBody()?.Rows"
}
```
  
<span data-ttu-id="94a18-352">Затем в определении рабочего процесса `@triggerBody().name` возвращает `mycoolrow` для первого выполнения и `another row` для второго.</span><span class="sxs-lookup"><span data-stu-id="94a18-352">Then, in the workflow definition, `@triggerBody().name` returns `mycoolrow` for the first run, and `another row` for the second run.</span></span> <span data-ttu-id="94a18-353">Выходные данные триггера выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="94a18-353">The trigger outputs look like this example:</span></span>  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

<span data-ttu-id="94a18-354">Если используется `SplitOn`, невозможно получить свойства, которые находятся за пределами массива, в данном случае поле `Status`.</span><span class="sxs-lookup"><span data-stu-id="94a18-354">So if you use `SplitOn`, you can't get the properties that are outside the array, in this case, the `Status` field.</span></span>  
  
> [!NOTE]  
> <span data-ttu-id="94a18-355">В этом примере используется оператор `?`, чтобы избежать ошибок, если отсутствует свойство `Rows`.</span><span class="sxs-lookup"><span data-stu-id="94a18-355">In this example, we use the `?` operator to be able to avoid a failure if the `Rows` property is not present.</span></span> 
  
## <a name="single-run-instance"></a><span data-ttu-id="94a18-356">Экземпляр однократного выполнения</span><span class="sxs-lookup"><span data-stu-id="94a18-356">Single run instance</span></span>

<span data-ttu-id="94a18-357">Для триггеров можно настроить так, чтобы свойство повторения срабатывало, только если завершены все активные выполнения.</span><span class="sxs-lookup"><span data-stu-id="94a18-357">You can configure triggers that have a recurrence property to only fire if all active runs have completed.</span></span> <span data-ttu-id="94a18-358">Если запланированное повторение случается во время уже происходящего выполнения, триггер не срабатывает и ожидает следующего запланированного интервала повторения, чтобы сделать повторную проверку.</span><span class="sxs-lookup"><span data-stu-id="94a18-358">If a scheduled recurrence occurs while there is an in-progress run, the trigger skips and waits until the next scheduled recurrence interval to check again.</span></span>

<span data-ttu-id="94a18-359">Этот параметр можно настроить с помощью параметров операции:</span><span class="sxs-lookup"><span data-stu-id="94a18-359">You can configure this setting through the operation options:</span></span>

```json
"triggers": {
    "mytrigger": {
        "type": "http",
        "inputs": { ... },
        "recurrence": { ... },
        "operationOptions": "singleInstance"
    }
}
```

## <a name="types-and-inputs"></a><span data-ttu-id="94a18-360">Типы и входные данные</span><span class="sxs-lookup"><span data-stu-id="94a18-360">Types and inputs</span></span>  

<span data-ttu-id="94a18-361">Существует много типов действий, каждое из которых имеет уникальное поведение.</span><span class="sxs-lookup"><span data-stu-id="94a18-361">There are many types of actions, each with unique behavior.</span></span> <span data-ttu-id="94a18-362">Действия коллекций могут содержать множество вложенных действий.</span><span class="sxs-lookup"><span data-stu-id="94a18-362">Collection actions may contain many other actions within itself.</span></span>

### <a name="standard-actions"></a><span data-ttu-id="94a18-363">Стандартные действия</span><span class="sxs-lookup"><span data-stu-id="94a18-363">Standard actions</span></span>  

-   <span data-ttu-id="94a18-364">**http** — это действие вызывает конечную веб-точку HTTP.</span><span class="sxs-lookup"><span data-stu-id="94a18-364">**HTTP** This action calls an HTTP web endpoint.</span></span>  
  
-   <span data-ttu-id="94a18-365">**apiConnection** — это действие ведет себя как действие HTTP, но использует интерфейсы API, управляемые Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="94a18-365">**ApiConnection** \- This action behaves like the HTTP action, but uses the Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="94a18-366">**apiConnectionWebhook** — аналогично httpWebhook, но использует интерфейсы API, управляемые Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="94a18-366">**ApiConnectionWebhook** \- Like HTTPWebhook, but uses the Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="94a18-367">**response** — это действие определяет ответ для входящего вызова.</span><span class="sxs-lookup"><span data-stu-id="94a18-367">**Response** \- This action defines a response for an incoming call.</span></span>  
  
-   <span data-ttu-id="94a18-368">**wait** — это простое действие ожидает фиксированное количество времени или до определенного времени.</span><span class="sxs-lookup"><span data-stu-id="94a18-368">**Wait** \- This simple action waits a fixed amount of time or until a specific time.</span></span>  
  
-   <span data-ttu-id="94a18-369">**workflow** — это действие представляет вложенный рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="94a18-369">**Workflow** \- This action represents a nested workflow.</span></span>  

-   <span data-ttu-id="94a18-370">**Function** \- — это действие представляет функцию Azure.</span><span class="sxs-lookup"><span data-stu-id="94a18-370">**Function** \- This action represents an Azure Function.</span></span>

### <a name="collection-actions"></a><span data-ttu-id="94a18-371">Действия коллекций</span><span class="sxs-lookup"><span data-stu-id="94a18-371">Collection actions</span></span>

-   <span data-ttu-id="94a18-372">**scope** — это действие является логическим объединением других действий.</span><span class="sxs-lookup"><span data-stu-id="94a18-372">**Scope** \- This action is a logical grouping of other actions.</span></span>

-   <span data-ttu-id="94a18-373">**condition** — это действие вычисляет выражение и выполняет соответствующую ветвь результатов.</span><span class="sxs-lookup"><span data-stu-id="94a18-373">**Condition** \- This action evaluates an expression and executes the corresponding result branch.</span></span>

-   <span data-ttu-id="94a18-374">**foreach** — это циклическое действие выполняет итерацию по массиву и внутренние действия для каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="94a18-374">**ForEach** \- This looping action iterates through an array and performs inner actions for each item.</span></span>

-   <span data-ttu-id="94a18-375">**Until** — это циклическое действие выполняет внутренние действия, пока для условия не возвращается значение true.</span><span class="sxs-lookup"><span data-stu-id="94a18-375">**Until** \- This looping action executes inner actions until a condition results to true.</span></span>
  
<span data-ttu-id="94a18-376">Каждый тип действия имеет разный набор **входных данных**, определяющих его поведение.</span><span class="sxs-lookup"><span data-stu-id="94a18-376">Each type of action has a different set of **inputs** that define an action's behavior.</span></span>  
  
## <a name="http-action"></a><span data-ttu-id="94a18-377">Действие HTTP</span><span class="sxs-lookup"><span data-stu-id="94a18-377">HTTP action</span></span>  

<span data-ttu-id="94a18-378">Действия HTTP вызывают указанную конечную точку и проверяют ответ, чтобы определить, следует ли запускать рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="94a18-378">HTTP actions call a specified endpoint and check the response to determine whether the workflow should run.</span></span> <span data-ttu-id="94a18-379">Объект **входных данных** принимает набор параметров, необходимых для создания HTTP-вызова:</span><span class="sxs-lookup"><span data-stu-id="94a18-379">The **inputs** object takes the set of parameters required to construct the HTTP call:</span></span>  
  
|<span data-ttu-id="94a18-380">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="94a18-380">Element name</span></span>|<span data-ttu-id="94a18-381">Обязательно</span><span class="sxs-lookup"><span data-stu-id="94a18-381">Required</span></span>|<span data-ttu-id="94a18-382">Тип</span><span class="sxs-lookup"><span data-stu-id="94a18-382">Type</span></span>|<span data-ttu-id="94a18-383">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-383">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="94a18-384">метод</span><span class="sxs-lookup"><span data-stu-id="94a18-384">method</span></span>|<span data-ttu-id="94a18-385">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-385">Yes</span></span>|<span data-ttu-id="94a18-386">Строка</span><span class="sxs-lookup"><span data-stu-id="94a18-386">String</span></span>|<span data-ttu-id="94a18-387">Это может быть один из следующих методов HTTP: **GET**, **POST**, **PUT**, **DELETE**, **HEAD** или **PATCH**.</span><span class="sxs-lookup"><span data-stu-id="94a18-387">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="94a18-388">uri</span><span class="sxs-lookup"><span data-stu-id="94a18-388">uri</span></span>|<span data-ttu-id="94a18-389">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-389">Yes</span></span>|<span data-ttu-id="94a18-390">Строка</span><span class="sxs-lookup"><span data-stu-id="94a18-390">String</span></span>|<span data-ttu-id="94a18-391">Вызываемая конечная точка HTTP или HTTPS.</span><span class="sxs-lookup"><span data-stu-id="94a18-391">The http or https endpoint that is called.</span></span> <span data-ttu-id="94a18-392">Не более 2 КБ.</span><span class="sxs-lookup"><span data-stu-id="94a18-392">Maximum length is 2 kilobytes.</span></span>|  
|<span data-ttu-id="94a18-393">Запросы</span><span class="sxs-lookup"><span data-stu-id="94a18-393">queries</span></span>|<span data-ttu-id="94a18-394">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-394">No</span></span>|<span data-ttu-id="94a18-395">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-395">Object</span></span>|<span data-ttu-id="94a18-396">Представляет параметры запроса для добавления в URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="94a18-396">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="94a18-397">Например, `"queries" : { "api-version": "2015-02-01" }` добавляет `?api-version=2015-02-01` в URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="94a18-397">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="94a18-398">headers</span><span class="sxs-lookup"><span data-stu-id="94a18-398">headers</span></span>|<span data-ttu-id="94a18-399">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-399">No</span></span>|<span data-ttu-id="94a18-400">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-400">Object</span></span>|<span data-ttu-id="94a18-401">Представляет все заголовки, которые отправляются в запрос.</span><span class="sxs-lookup"><span data-stu-id="94a18-401">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="94a18-402">Например, чтобы задать язык и тип запроса: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="94a18-402">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="94a18-403">текст</span><span class="sxs-lookup"><span data-stu-id="94a18-403">body</span></span>|<span data-ttu-id="94a18-404">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-404">No</span></span>|<span data-ttu-id="94a18-405">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-405">Object</span></span>|<span data-ttu-id="94a18-406">Представляет полезные данные, отправляемые конечной точке.</span><span class="sxs-lookup"><span data-stu-id="94a18-406">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="94a18-407">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="94a18-407">retryPolicy</span></span>|<span data-ttu-id="94a18-408">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-408">No</span></span>|<span data-ttu-id="94a18-409">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-409">Object</span></span>|<span data-ttu-id="94a18-410">Позволяет настроить поведение повтора при возникновении ошибок 4xx или 5xx.</span><span class="sxs-lookup"><span data-stu-id="94a18-410">Lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="94a18-411">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="94a18-411">operationsOptions</span></span>|<span data-ttu-id="94a18-412">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-412">No</span></span>|<span data-ttu-id="94a18-413">string</span><span class="sxs-lookup"><span data-stu-id="94a18-413">String</span></span>|<span data-ttu-id="94a18-414">Определяет набор особого поведения для переопределения.</span><span class="sxs-lookup"><span data-stu-id="94a18-414">Defines the set of special behaviors to override.</span></span>|  
|<span data-ttu-id="94a18-415">authentication</span><span class="sxs-lookup"><span data-stu-id="94a18-415">authentication</span></span>|<span data-ttu-id="94a18-416">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-416">No</span></span>|<span data-ttu-id="94a18-417">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-417">Object</span></span>|<span data-ttu-id="94a18-418">Представляет метод для проверки подлинности запроса.</span><span class="sxs-lookup"><span data-stu-id="94a18-418">Represents the method that the request should be authenticated.</span></span> <span data-ttu-id="94a18-419">Дополнительные сведения см. в статье [Исходящая проверка подлинности планировщика](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="94a18-419">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="94a18-420">Помимо планировщика, имеется еще одно поддерживаемое свойство: `authority`.</span><span class="sxs-lookup"><span data-stu-id="94a18-420">Beyond scheduler, there is one more supported property: `authority`.</span></span> <span data-ttu-id="94a18-421">По умолчанию его значение равно `https://login.windows.net`, если не указано другое. Также можно использовать другое значение, например `https://login.windows\-ppe.net`.</span><span class="sxs-lookup"><span data-stu-id="94a18-421">By default, this is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|  
  
<span data-ttu-id="94a18-422">Действия HTTP и \(действия API подключения\) поддерживают политики повтора.</span><span class="sxs-lookup"><span data-stu-id="94a18-422">HTTP actions \(and API Connection\) actions support retry policies.</span></span> <span data-ttu-id="94a18-423">Помимо исключений при подключении, политика повтора применяется к периодическим сбоям, классифицируемым как коды состояния HTTP 408, 429 и 5xx.</span><span class="sxs-lookup"><span data-stu-id="94a18-423">A retry policy applies to intermittent failures, characterized as HTTP status codes 408, 429, and 5xx, in addition to any connectivity exceptions.</span></span> <span data-ttu-id="94a18-424">Эта политика описывается с помощью объекта *retryPolicy*, определенного, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="94a18-424">This policy is described using the *retryPolicy* object defined as shown here:</span></span>
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
<span data-ttu-id="94a18-425">Интервал повторных попыток указывается в формате ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="94a18-425">The retry interval is specified in the ISO 8601 format.</span></span> <span data-ttu-id="94a18-426">Минимальное значение по умолчанию для этого интервала составляет 20 секунд, а максимальное — один час.</span><span class="sxs-lookup"><span data-stu-id="94a18-426">This interval has a default and minimum value of 20 seconds, while the maximum value is one hour.</span></span> <span data-ttu-id="94a18-427">Максимальное число повторных попыток по умолчанию составляет четыре часа.</span><span class="sxs-lookup"><span data-stu-id="94a18-427">The default and maximum retry count is four hours.</span></span> <span data-ttu-id="94a18-428">Если определение политики повтора не указано, используется стратегия `fixed` со значениями числа и интервала повтора по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="94a18-428">If the retry policy definition is not specified, a `fixed` strategy is used with default retry count and interval values.</span></span> <span data-ttu-id="94a18-429">Чтобы отключить политику повтора, задайте для нее тип `None`.</span><span class="sxs-lookup"><span data-stu-id="94a18-429">To disable the retry policy, set its type to `None`.</span></span>  
  
<span data-ttu-id="94a18-430">Например, при возникновении временных сбоев следующее действие от двух до трех раз пытается получить последние новости с 30-секундной задержкой между попытками.</span><span class="sxs-lookup"><span data-stu-id="94a18-430">For example, the following action retries fetching the latest news two times, if there are intermittent failures, for a total of three executions, with a 30-second delay between each attempt:</span></span>  
  
```json
"latestNews" : {
    "type": "http",
    "inputs": {
        "method": "GET",
        "uri": "https://mynews.example.com/latest",
        "retryPolicy" : {
            "type": "fixed",
            "interval": "PT30S",
            "count": 2
        }
    }
}
```
### <a name="asynchronous-patterns"></a><span data-ttu-id="94a18-431">Модель асинхронных операций</span><span class="sxs-lookup"><span data-stu-id="94a18-431">Asynchronous patterns</span></span>

<span data-ttu-id="94a18-432">По умолчанию все действия на основе HTTP поддерживают стандартную модель асинхронных операций.</span><span class="sxs-lookup"><span data-stu-id="94a18-432">By default, all HTTP-based actions support the standard asynchronous operation pattern.</span></span> <span data-ttu-id="94a18-433">Таким образом, если удаленный сервер указывает, что запрос принят для обработки с ответом 202 \(Accepted\), ядро приложений логики продолжает опрашивать URL-адрес, указанный в заголовке расположения ответа, пока не получит конечного ответа, отличного \(от ответа 202\).</span><span class="sxs-lookup"><span data-stu-id="94a18-433">So if the remote server indicates that the request is accepted for processing with a 202 \(Accepted\) response, the Logic Apps engine keeps polling the URL specified in the response's location header until reaching a terminal state \(a non\-202 response\).</span></span>  
  
<span data-ttu-id="94a18-434">Чтобы отключить асинхронное поведение, установите параметр `DisableAsyncPattern` во входных данных действия.</span><span class="sxs-lookup"><span data-stu-id="94a18-434">To disable the asynchronous behavior previously described, set a `DisableAsyncPattern` option in the action inputs.</span></span> <span data-ttu-id="94a18-435">В таком случае входные данные действия будут основаны на первоначальном ответе 202 от сервера.</span><span class="sxs-lookup"><span data-stu-id="94a18-435">In this case, the output of the action is based on the initial 202 response from the server.</span></span>  
  
```json
"invokeLongRunningOperation" : {
    "type": "http",
    "inputs": {
        "method": "POST",
        "uri": "https://host.example.com/resources"
    },
    "operationOptions": "DisableAsyncPattern"
}
```

#### <a name="asynchronous-limits"></a><span data-ttu-id="94a18-436">Ограничения асинхронных операций</span><span class="sxs-lookup"><span data-stu-id="94a18-436">Asynchronous Limits</span></span>

<span data-ttu-id="94a18-437">Действие модели асинхронных операций можно ограничить, задав определенный период времени.</span><span class="sxs-lookup"><span data-stu-id="94a18-437">An asynchronous pattern can be limited in its duration to a specific time interval.</span></span>  <span data-ttu-id="94a18-438">Если интервал времени истекает без достижения конечного состояния, состояние действия будет помечено как `Cancelled` с помощью кода `ActionTimedOut`.</span><span class="sxs-lookup"><span data-stu-id="94a18-438">If the time interval elapses without reaching a terminal state, the status of the action will be marked `Cancelled` with a code of `ActionTimedOut`.</span></span>  <span data-ttu-id="94a18-439">Ограничение времени ожидания указывается в формате ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="94a18-439">The limit timeout is specified in ISO 8601 format.</span></span>  <span data-ttu-id="94a18-440">Ограничения можно задать с помощью следующего синтаксиса:</span><span class="sxs-lookup"><span data-stu-id="94a18-440">Limits can be specified with the following syntax:</span></span>

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a><span data-ttu-id="94a18-441">API подключения</span><span class="sxs-lookup"><span data-stu-id="94a18-441">API Connection</span></span>  

<span data-ttu-id="94a18-442">API подключения — это действие, которое ссылается на соединитель, управляемый Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="94a18-442">API Connection is an action that references a Microsoft-managed connector.</span></span>
<span data-ttu-id="94a18-443">Для этого действия требуется ссылка на допустимое подключение и сведения об API и необходимых параметрах.</span><span class="sxs-lookup"><span data-stu-id="94a18-443">This action requires a reference to a valid connection, and information on the API and parameters required.</span></span>

|<span data-ttu-id="94a18-444">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="94a18-444">Element name</span></span>|<span data-ttu-id="94a18-445">Обязательно</span><span class="sxs-lookup"><span data-stu-id="94a18-445">Required</span></span>|<span data-ttu-id="94a18-446">Тип</span><span class="sxs-lookup"><span data-stu-id="94a18-446">Type</span></span>|<span data-ttu-id="94a18-447">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-447">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="94a18-448">host</span><span class="sxs-lookup"><span data-stu-id="94a18-448">host</span></span>|<span data-ttu-id="94a18-449">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-449">Yes</span></span>|<span data-ttu-id="94a18-450">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-450">Object</span></span>|<span data-ttu-id="94a18-451">Представляет сведения о соединителе, например runtimeUrl, и ссылку на объект подключения.</span><span class="sxs-lookup"><span data-stu-id="94a18-451">Represents the connector information such as the runtimeUrl and reference to the connection object</span></span>|
|<span data-ttu-id="94a18-452">метод</span><span class="sxs-lookup"><span data-stu-id="94a18-452">method</span></span>|<span data-ttu-id="94a18-453">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-453">Yes</span></span>|<span data-ttu-id="94a18-454">Строка</span><span class="sxs-lookup"><span data-stu-id="94a18-454">String</span></span>|<span data-ttu-id="94a18-455">Это может быть один из следующих методов HTTP: **GET**, **POST**, **PUT**, **DELETE**, **HEAD** или **PATCH**.</span><span class="sxs-lookup"><span data-stu-id="94a18-455">Can be one of the following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="94a18-456">path</span><span class="sxs-lookup"><span data-stu-id="94a18-456">path</span></span>|<span data-ttu-id="94a18-457">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-457">Yes</span></span>|<span data-ttu-id="94a18-458">Строка</span><span class="sxs-lookup"><span data-stu-id="94a18-458">String</span></span>|<span data-ttu-id="94a18-459">Путь к операции API.</span><span class="sxs-lookup"><span data-stu-id="94a18-459">The path of the API operation.</span></span>|  
|<span data-ttu-id="94a18-460">Запросы</span><span class="sxs-lookup"><span data-stu-id="94a18-460">queries</span></span>|<span data-ttu-id="94a18-461">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-461">No</span></span>|<span data-ttu-id="94a18-462">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-462">Object</span></span>|<span data-ttu-id="94a18-463">Представляет параметры запроса для добавления в URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="94a18-463">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="94a18-464">Например, `"queries" : { "api-version": "2015-02-01" }` добавляет `?api-version=2015-02-01` в URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="94a18-464">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="94a18-465">headers</span><span class="sxs-lookup"><span data-stu-id="94a18-465">headers</span></span>|<span data-ttu-id="94a18-466">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-466">No</span></span>|<span data-ttu-id="94a18-467">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-467">Object</span></span>|<span data-ttu-id="94a18-468">Представляет все заголовки, которые отправляются в запрос.</span><span class="sxs-lookup"><span data-stu-id="94a18-468">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="94a18-469">Например, чтобы задать язык и тип запроса: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="94a18-469">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="94a18-470">текст</span><span class="sxs-lookup"><span data-stu-id="94a18-470">body</span></span>|<span data-ttu-id="94a18-471">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-471">No</span></span>|<span data-ttu-id="94a18-472">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-472">Object</span></span>|<span data-ttu-id="94a18-473">Представляет полезные данные, отправляемые конечной точке.</span><span class="sxs-lookup"><span data-stu-id="94a18-473">Represents the payload that is sent to the endpoint.</span></span>|  
|<span data-ttu-id="94a18-474">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="94a18-474">retryPolicy</span></span>|<span data-ttu-id="94a18-475">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-475">No</span></span>|<span data-ttu-id="94a18-476">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-476">Object</span></span>|<span data-ttu-id="94a18-477">Позволяет настроить поведение повтора при возникновении ошибок 4xx или 5xx.</span><span class="sxs-lookup"><span data-stu-id="94a18-477">Lets you customize the retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="94a18-478">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="94a18-478">operationsOptions</span></span>|<span data-ttu-id="94a18-479">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-479">No</span></span>|<span data-ttu-id="94a18-480">string</span><span class="sxs-lookup"><span data-stu-id="94a18-480">String</span></span>|<span data-ttu-id="94a18-481">Определяет набор особого поведения для переопределения.</span><span class="sxs-lookup"><span data-stu-id="94a18-481">Defines the set of special behaviors to override.</span></span>|  

```json
"Send_Email": {
    "type": "apiconnection",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "method": "post",
        "body": {
            "Subject": "New Tweet from @{triggerBody()['TweetedBy']}",
            "Body": "@{triggerBody()['TweetText']}",
            "To": "me@example.com"
        },
        "path": "/Mail"
    },
    "runAfter": {}
    }
```

## <a name="api-connection-webhook-action"></a><span data-ttu-id="94a18-482">Действие webhook API подключения</span><span class="sxs-lookup"><span data-stu-id="94a18-482">API Connection webhook action</span></span>

```json
"Send_approval_email": {
    "type": "apiconnectionwebhook",
    "inputs": {
        "host": {
            "api": {
                "runtimeUrl": "https://logic-apis-df.azure-apim.net/apim/office365"
            },
            "connection": {
                "name": "@parameters('$connections')['office365']['connectionId']"
            }
        },
        "body": {
            "Message": {
                "Subject": "Approval Request",
                "Options": "Approve, Reject",
                "Importance": "Normal",
                "To": "me@email.com"
            }
        },
        "path": "/approvalmail",
        "authentication": "@parameters('$authentication')"
    },
    "runAfter": {}
}
```

<span data-ttu-id="94a18-483">Ограничения для действий webhook можно указать так же, как [ограничения для асинхронной модели HTTP](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="94a18-483">Limits on a webhook action can be specified in the same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  
## <a name="response-action"></a><span data-ttu-id="94a18-484">Действие ответа</span><span class="sxs-lookup"><span data-stu-id="94a18-484">Response action</span></span>  

<span data-ttu-id="94a18-485">Этот тип действия содержит все полезные данные ответа из HTTP-запроса и содержит код состояния, текст и заголовки:</span><span class="sxs-lookup"><span data-stu-id="94a18-485">This action type contains the entire response payload from an HTTP request and includes a statusCode, body, and headers:</span></span>  
  
```json
"myresponse" : {
    "type" : "response",
    "inputs" : {
        "statusCode" : 200,
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        },
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        }
    },
    "runAfter": {}
}
```
  
<span data-ttu-id="94a18-486">Действие ответа имеет специальные ограничения, которые не применяются к другим действиям.</span><span class="sxs-lookup"><span data-stu-id="94a18-486">The response action has special restrictions that don't apply to other actions.</span></span> <span data-ttu-id="94a18-487">В частности:</span><span class="sxs-lookup"><span data-stu-id="94a18-487">Specifically:</span></span>  
  
-   <span data-ttu-id="94a18-488">Действия ответов не могут быть параллельными в определении, так как требуется детерминированный ответ на входящий запрос.</span><span class="sxs-lookup"><span data-stu-id="94a18-488">Response actions cannot be parallel in a definition because a deterministic response to the incoming request is required.</span></span>  
  
-   <span data-ttu-id="94a18-489">Если действие ответа получено после получения ответа входящим запросом, действие считается неудачным \(конфликт\) и, как результат, получает состояние `Failed`.</span><span class="sxs-lookup"><span data-stu-id="94a18-489">If a response action is reached after the incoming request has received a response, the action is considered failed \(conflict\), and as a result, the run is `Failed`.</span></span>  
  
-   <span data-ttu-id="94a18-490">Рабочий процесс с действиями ответа не может содержать `splitOn` в своем триггере, так как один вызов запускает несколько выполнений.</span><span class="sxs-lookup"><span data-stu-id="94a18-490">A workflow with Response actions cannot have `splitOn` in its trigger because one call causes many runs.</span></span> <span data-ttu-id="94a18-491">Поэтому это нужно проверить, когда поток использует метод PUT и получает ошибку запроса.</span><span class="sxs-lookup"><span data-stu-id="94a18-491">As a result, this should be validated when the flow is PUT and cause a Bad Request.</span></span>  
  
## <a name="wait-action"></a><span data-ttu-id="94a18-492">Действие wait</span><span class="sxs-lookup"><span data-stu-id="94a18-492">Wait action</span></span>  

<span data-ttu-id="94a18-493">Действие `wait` приостанавливает выполнение рабочего процесса на указанный период времени.</span><span class="sxs-lookup"><span data-stu-id="94a18-493">The `wait` action suspends workflow execution for the specified interval.</span></span> <span data-ttu-id="94a18-494">Например, чтобы ожидать 15 минут, можно использовать следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="94a18-494">For example, to wait 15 minutes, you can use this snippet:</span></span>  
  
```json
"waitForFifteenMinutes" : {
    "type": "wait",
    "inputs": {
        "interval": {
            "unit" : "minute",
            "count" : 15
        }
    }
}
```  
  
<span data-ttu-id="94a18-495">Кроме того, чтобы задать ожидание до определенного момента времени, можно использовать такой пример:</span><span class="sxs-lookup"><span data-stu-id="94a18-495">Alternatively, to wait until a specific moment in time, you can use this example:</span></span>  
  
```json
"waitUntilOctober" : {
    "type": "wait",
    "inputs": {
        "until": {
            "timestamp" : "2016-10-01T00:00:00Z"
        }
    }
}
```
  
> [!NOTE]  
> <span data-ttu-id="94a18-496">Длительность ожидания можно задать только с помощью одного из объектов — **interval** или **until**.</span><span class="sxs-lookup"><span data-stu-id="94a18-496">The wait duration can be either specified using the **interval** object or the **until** object, but not both.</span></span>  
  
|<span data-ttu-id="94a18-497">Имя</span><span class="sxs-lookup"><span data-stu-id="94a18-497">Name</span></span>|<span data-ttu-id="94a18-498">Обязательно</span><span class="sxs-lookup"><span data-stu-id="94a18-498">Required</span></span>|<span data-ttu-id="94a18-499">Тип</span><span class="sxs-lookup"><span data-stu-id="94a18-499">Type</span></span>|<span data-ttu-id="94a18-500">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-500">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="94a18-501">interval</span><span class="sxs-lookup"><span data-stu-id="94a18-501">interval</span></span>|<span data-ttu-id="94a18-502">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-502">No</span></span>|<span data-ttu-id="94a18-503">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-503">Object</span></span>|<span data-ttu-id="94a18-504">Длительность ожидания зависит от количества времени.</span><span class="sxs-lookup"><span data-stu-id="94a18-504">The wait duration based on amount of time.</span></span>|  
|<span data-ttu-id="94a18-505">interval unit</span><span class="sxs-lookup"><span data-stu-id="94a18-505">interval unit</span></span>|<span data-ttu-id="94a18-506">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-506">Yes</span></span>|<span data-ttu-id="94a18-507">Строка</span><span class="sxs-lookup"><span data-stu-id="94a18-507">String</span></span>|<span data-ttu-id="94a18-508">Одна из таких единиц времени: second, minute, hour, day, week, month, year.</span><span class="sxs-lookup"><span data-stu-id="94a18-508">One of these intervals: second, minute, hour, day, week, month, year.</span></span>|  
|<span data-ttu-id="94a18-509">interval count</span><span class="sxs-lookup"><span data-stu-id="94a18-509">interval count</span></span>|<span data-ttu-id="94a18-510">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-510">Yes</span></span>|<span data-ttu-id="94a18-511">Строка</span><span class="sxs-lookup"><span data-stu-id="94a18-511">String</span></span>|<span data-ttu-id="94a18-512">Длительность на основе заданной внутренней единицы измерения.</span><span class="sxs-lookup"><span data-stu-id="94a18-512">Duration based on the given internal unit.</span></span>|  
|<span data-ttu-id="94a18-513">until</span><span class="sxs-lookup"><span data-stu-id="94a18-513">until</span></span>|<span data-ttu-id="94a18-514">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-514">No</span></span>|<span data-ttu-id="94a18-515">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-515">Object</span></span>|<span data-ttu-id="94a18-516">Длительность ожидания на основе точки на момент времени.</span><span class="sxs-lookup"><span data-stu-id="94a18-516">The wait duration based on a point in time.</span></span>|  
|<span data-ttu-id="94a18-517">until timestamp</span><span class="sxs-lookup"><span data-stu-id="94a18-517">until timestamp</span></span>|<span data-ttu-id="94a18-518">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-518">Yes</span></span>|<span data-ttu-id="94a18-519">string</span><span class="sxs-lookup"><span data-stu-id="94a18-519">String</span></span>|<span data-ttu-id="94a18-520">Точка во времени в формате UTC, когда истекает время ожидания.</span><span class="sxs-lookup"><span data-stu-id="94a18-520">String&#124;The point in time in UTC when the wait expires.</span></span>|  

## <a name="query-action"></a><span data-ttu-id="94a18-521">Действие запроса</span><span class="sxs-lookup"><span data-stu-id="94a18-521">Query action</span></span>

<span data-ttu-id="94a18-522">Действие `query` позволяет фильтровать массив на основе условия.</span><span class="sxs-lookup"><span data-stu-id="94a18-522">The `query` action lets you filter an array based on a condition.</span></span> <span data-ttu-id="94a18-523">Например, чтобы выбрать числа больше 2, можно использовать:</span><span class="sxs-lookup"><span data-stu-id="94a18-523">For example, to select numbers greater than 2, you can use:</span></span>

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

<span data-ttu-id="94a18-524">Выходные данные действия `query` представлены в виде массива, содержащего элементы из массива входных данных, которые соответствуют условию.</span><span class="sxs-lookup"><span data-stu-id="94a18-524">The output from the `query` action is an array that has elements from the input array that satisfy the condition.</span></span>

> [!NOTE]
> <span data-ttu-id="94a18-525">Если значений, соответствующих условию `where`, нет, результатом будет пустой массив.</span><span class="sxs-lookup"><span data-stu-id="94a18-525">If no values satisfy the `where` condition, the result is an empty array.</span></span>

|<span data-ttu-id="94a18-526">Имя</span><span class="sxs-lookup"><span data-stu-id="94a18-526">Name</span></span>|<span data-ttu-id="94a18-527">Обязательно</span><span class="sxs-lookup"><span data-stu-id="94a18-527">Required</span></span>|<span data-ttu-id="94a18-528">Тип</span><span class="sxs-lookup"><span data-stu-id="94a18-528">Type</span></span>|<span data-ttu-id="94a18-529">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-529">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="94a18-530">from</span><span class="sxs-lookup"><span data-stu-id="94a18-530">from</span></span>|<span data-ttu-id="94a18-531">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-531">Yes</span></span>|<span data-ttu-id="94a18-532">Массив,</span><span class="sxs-lookup"><span data-stu-id="94a18-532">Array</span></span>|<span data-ttu-id="94a18-533">Исходный массив.</span><span class="sxs-lookup"><span data-stu-id="94a18-533">The source array.</span></span>|
|<span data-ttu-id="94a18-534">где:</span><span class="sxs-lookup"><span data-stu-id="94a18-534">where</span></span>|<span data-ttu-id="94a18-535">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-535">Yes</span></span>|<span data-ttu-id="94a18-536">Строка</span><span class="sxs-lookup"><span data-stu-id="94a18-536">String</span></span>|<span data-ttu-id="94a18-537">Условие, применяемое к каждому элементу исходного массива.</span><span class="sxs-lookup"><span data-stu-id="94a18-537">The condition to apply to each element of the source array.</span></span>|

## <a name="select-action"></a><span data-ttu-id="94a18-538">Выбор действия</span><span class="sxs-lookup"><span data-stu-id="94a18-538">Select action</span></span>

<span data-ttu-id="94a18-539">Действие `select` позволяет проецировать каждый элемент массива на новое значение.</span><span class="sxs-lookup"><span data-stu-id="94a18-539">The `select` action lets you project each element of an array into a new value.</span></span>
<span data-ttu-id="94a18-540">Например, чтобы преобразовать массив чисел в массив объектов, можно использовать следующую команду:</span><span class="sxs-lookup"><span data-stu-id="94a18-540">For example, to convert an array of numbers into an array of objects, you can use:</span></span>

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

<span data-ttu-id="94a18-541">Выходные данные действия `select` — это массив с таким же количеством элементов, как и во входном массиве. При этом каждый его элемент преобразован так, как предписывает свойство `select`.</span><span class="sxs-lookup"><span data-stu-id="94a18-541">The output of the `select` action is an array that has the same cardinality as the input array, with each element transformed as defined by the `select` property.</span></span> <span data-ttu-id="94a18-542">Если вход — это пустой массив, выходные данные также будут пустым массивом.</span><span class="sxs-lookup"><span data-stu-id="94a18-542">If the input is an empty array, the output is also an empty array.</span></span>

|<span data-ttu-id="94a18-543">Имя</span><span class="sxs-lookup"><span data-stu-id="94a18-543">Name</span></span>|<span data-ttu-id="94a18-544">Обязательно</span><span class="sxs-lookup"><span data-stu-id="94a18-544">Required</span></span>|<span data-ttu-id="94a18-545">Тип</span><span class="sxs-lookup"><span data-stu-id="94a18-545">Type</span></span>|<span data-ttu-id="94a18-546">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-546">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="94a18-547">from</span><span class="sxs-lookup"><span data-stu-id="94a18-547">from</span></span>|<span data-ttu-id="94a18-548">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-548">Yes</span></span>|<span data-ttu-id="94a18-549">Массив,</span><span class="sxs-lookup"><span data-stu-id="94a18-549">Array</span></span>|<span data-ttu-id="94a18-550">Исходный массив.</span><span class="sxs-lookup"><span data-stu-id="94a18-550">The source array.</span></span>|
|<span data-ttu-id="94a18-551">select</span><span class="sxs-lookup"><span data-stu-id="94a18-551">select</span></span>|<span data-ttu-id="94a18-552">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-552">Yes</span></span>|<span data-ttu-id="94a18-553">Любой</span><span class="sxs-lookup"><span data-stu-id="94a18-553">Any</span></span>|<span data-ttu-id="94a18-554">Проекция, применяемая к каждому элементу исходного массива.</span><span class="sxs-lookup"><span data-stu-id="94a18-554">The projection to apply to each element of the source array.</span></span>|

## <a name="terminate-action"></a><span data-ttu-id="94a18-555">Действие terminate</span><span class="sxs-lookup"><span data-stu-id="94a18-555">Terminate action</span></span>

<span data-ttu-id="94a18-556">Действие terminate останавливает выполнение рабочего процесса, прерывая активные действия и пропуская все оставшиеся действия.</span><span class="sxs-lookup"><span data-stu-id="94a18-556">The Terminate action stops execution of the workflow run, aborting any in-flight actions, and skipping any remaining actions.</span></span> <span data-ttu-id="94a18-557">Например, для прерывания выполнения с состоянием **Failed** можно использовать следующий фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="94a18-557">For example, to terminate a run with status **Failed**, you can use the following snippet:</span></span>

```json
"HandleUnexpectedResponse" : {
    "type": "terminate",
    "inputs": {
        "runStatus" : "failed",
        "runError": {
            "code": "UnexpectedResponse",
            "message": "Received an unexpected response.",
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="94a18-558">Действие прерывания не распространяется на уже выполненные действия.</span><span class="sxs-lookup"><span data-stu-id="94a18-558">Actions already completed are not affected by the terminate action.</span></span>

|<span data-ttu-id="94a18-559">Имя</span><span class="sxs-lookup"><span data-stu-id="94a18-559">Name</span></span>|<span data-ttu-id="94a18-560">Обязательно</span><span class="sxs-lookup"><span data-stu-id="94a18-560">Required</span></span>|<span data-ttu-id="94a18-561">Тип</span><span class="sxs-lookup"><span data-stu-id="94a18-561">Type</span></span>|<span data-ttu-id="94a18-562">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-562">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="94a18-563">runStatus</span><span class="sxs-lookup"><span data-stu-id="94a18-563">runStatus</span></span>|<span data-ttu-id="94a18-564">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-564">Yes</span></span>|<span data-ttu-id="94a18-565">string</span><span class="sxs-lookup"><span data-stu-id="94a18-565">String</span></span>|<span data-ttu-id="94a18-566">Состояние выполнения объекта:</span><span class="sxs-lookup"><span data-stu-id="94a18-566">The target run status.</span></span> <span data-ttu-id="94a18-567">**Failed** или **Cancelled**.</span><span class="sxs-lookup"><span data-stu-id="94a18-567">Either **Failed** or **Cancelled**.</span></span>|
|<span data-ttu-id="94a18-568">runError</span><span class="sxs-lookup"><span data-stu-id="94a18-568">runError</span></span>|<span data-ttu-id="94a18-569">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-569">No</span></span>|<span data-ttu-id="94a18-570">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-570">Object</span></span>|<span data-ttu-id="94a18-571">Сведения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="94a18-571">The error details.</span></span> <span data-ttu-id="94a18-572">Поддерживается, только если **runStatus** имеет значение **Failed**.</span><span class="sxs-lookup"><span data-stu-id="94a18-572">Only supported when **runStatus** is set to **Failed**.</span></span>|
|<span data-ttu-id="94a18-573">runError code</span><span class="sxs-lookup"><span data-stu-id="94a18-573">runError code</span></span>|<span data-ttu-id="94a18-574">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-574">No</span></span>|<span data-ttu-id="94a18-575">Строка</span><span class="sxs-lookup"><span data-stu-id="94a18-575">String</span></span>|<span data-ttu-id="94a18-576">Код ошибки выполнения.</span><span class="sxs-lookup"><span data-stu-id="94a18-576">The run error code.</span></span>|
|<span data-ttu-id="94a18-577">runError message</span><span class="sxs-lookup"><span data-stu-id="94a18-577">runError message</span></span>|<span data-ttu-id="94a18-578">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-578">No</span></span>|<span data-ttu-id="94a18-579">Строка</span><span class="sxs-lookup"><span data-stu-id="94a18-579">String</span></span>|<span data-ttu-id="94a18-580">Сообщение об ошибке выполнения.</span><span class="sxs-lookup"><span data-stu-id="94a18-580">The run error message.</span></span>|

## <a name="compose-action"></a><span data-ttu-id="94a18-581">Действие compose</span><span class="sxs-lookup"><span data-stu-id="94a18-581">Compose action</span></span>

<span data-ttu-id="94a18-582">Действие compose позволяет создать произвольный объект.</span><span class="sxs-lookup"><span data-stu-id="94a18-582">The Compose action lets you construct an arbitrary object.</span></span> <span data-ttu-id="94a18-583">Выходные данные действия compose являются результатом вычисления входных данных.</span><span class="sxs-lookup"><span data-stu-id="94a18-583">The output of the compose action is the result of evaluating its inputs.</span></span> <span data-ttu-id="94a18-584">Например, это действие можно использовать для объединения выходных данных нескольких действий:</span><span class="sxs-lookup"><span data-stu-id="94a18-584">For example, you can use the compose action to merge outputs of multiple actions:</span></span>

```json
"composeUserRecord" : {
    "type": "compose",
    "inputs": {
        "firstName": "@actions('getUser').firstName",
        "alias": "@actions('getUser').alias",
        "thumbnailLink": "@actions('lookupThumbnail').url"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="94a18-585">Действие **compose** может использоваться для создания выходных данных, включая объекты, массивы и любой другой тип, изначально поддерживаемый приложениями логики (XML и двоичный тип).</span><span class="sxs-lookup"><span data-stu-id="94a18-585">The **Compose** action can be used to construct any output, including objects, arrays, and any other type natively supported by logic apps like XML and binary.</span></span>

## <a name="table-action"></a><span data-ttu-id="94a18-586">Действие таблицы</span><span class="sxs-lookup"><span data-stu-id="94a18-586">Table action</span></span>

<span data-ttu-id="94a18-587">Позволяет `table` преобразовать массив элементов в таблицу **CSV** или **HTML**.</span><span class="sxs-lookup"><span data-stu-id="94a18-587">The `table` allows you to convert an array of items into a **CSV** or **HTML** table.</span></span>

<span data-ttu-id="94a18-588">Предположим, что @triggerBody() выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="94a18-588">Suppose @triggerBody() is</span></span>

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

<span data-ttu-id="94a18-589">Пускай действие определено так:</span><span class="sxs-lookup"><span data-stu-id="94a18-589">And let the action be defined as</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

<span data-ttu-id="94a18-590">Результат для указанного выше кода будет следующим:</span><span class="sxs-lookup"><span data-stu-id="94a18-590">The above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="94a18-591">id</span><span class="sxs-lookup"><span data-stu-id="94a18-591">id</span></span></th><th><span data-ttu-id="94a18-592">name</span><span class="sxs-lookup"><span data-stu-id="94a18-592">name</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="94a18-593">0</span><span class="sxs-lookup"><span data-stu-id="94a18-593">0</span></span></td><td><span data-ttu-id="94a18-594">apples</span><span class="sxs-lookup"><span data-stu-id="94a18-594">apples</span></span></td></tr><tr><td><span data-ttu-id="94a18-595">1</span><span class="sxs-lookup"><span data-stu-id="94a18-595">1</span></span></td><td><span data-ttu-id="94a18-596">oranges</span><span class="sxs-lookup"><span data-stu-id="94a18-596">oranges</span></span></td></tr></tbody></table><span data-ttu-id="94a18-597">"</span><span class="sxs-lookup"><span data-stu-id="94a18-597">"</span></span>

<span data-ttu-id="94a18-598">Чтобы настроить таблицу, можно явно указать столбцы.</span><span class="sxs-lookup"><span data-stu-id="94a18-598">In order to customize the table, you can specify the columns explicitly.</span></span> <span data-ttu-id="94a18-599">Например:</span><span class="sxs-lookup"><span data-stu-id="94a18-599">For example:</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html",
        "columns": [{
          "header": "produce id",
          "value": "@item().id"
        },{
          "header": "description",
          "value": "@concat('fresh ', item().name)"
        }]
    }
}
```

<span data-ttu-id="94a18-600">Результат для указанного выше кода будет следующим:</span><span class="sxs-lookup"><span data-stu-id="94a18-600">The above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="94a18-601">Код результата</span><span class="sxs-lookup"><span data-stu-id="94a18-601">produce id</span></span></th><th><span data-ttu-id="94a18-602">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-602">description</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="94a18-603">0</span><span class="sxs-lookup"><span data-stu-id="94a18-603">0</span></span></td><td><span data-ttu-id="94a18-604">fresh apples</span><span class="sxs-lookup"><span data-stu-id="94a18-604">fresh apples</span></span></td></tr><tr><td><span data-ttu-id="94a18-605">1</span><span class="sxs-lookup"><span data-stu-id="94a18-605">1</span></span></td><td><span data-ttu-id="94a18-606">fresh oranges</span><span class="sxs-lookup"><span data-stu-id="94a18-606">fresh oranges</span></span></td></tr></tbody></table><span data-ttu-id="94a18-607">"</span><span class="sxs-lookup"><span data-stu-id="94a18-607">"</span></span>

<span data-ttu-id="94a18-608">Если значение свойства `from` — это пустой массив, выходные данные будут пустой таблицей.</span><span class="sxs-lookup"><span data-stu-id="94a18-608">If the `from` property value is an empty array, the output is an empty table.</span></span>

|<span data-ttu-id="94a18-609">Имя</span><span class="sxs-lookup"><span data-stu-id="94a18-609">Name</span></span>|<span data-ttu-id="94a18-610">Обязательно</span><span class="sxs-lookup"><span data-stu-id="94a18-610">Required</span></span>|<span data-ttu-id="94a18-611">Тип</span><span class="sxs-lookup"><span data-stu-id="94a18-611">Type</span></span>|<span data-ttu-id="94a18-612">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-612">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="94a18-613">from</span><span class="sxs-lookup"><span data-stu-id="94a18-613">from</span></span>|<span data-ttu-id="94a18-614">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-614">Yes</span></span>|<span data-ttu-id="94a18-615">Массив,</span><span class="sxs-lookup"><span data-stu-id="94a18-615">Array</span></span>|<span data-ttu-id="94a18-616">Исходный массив.</span><span class="sxs-lookup"><span data-stu-id="94a18-616">The source array.</span></span>|
|<span data-ttu-id="94a18-617">свойства</span><span class="sxs-lookup"><span data-stu-id="94a18-617">format</span></span>|<span data-ttu-id="94a18-618">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-618">Yes</span></span>|<span data-ttu-id="94a18-619">Строка</span><span class="sxs-lookup"><span data-stu-id="94a18-619">String</span></span>|<span data-ttu-id="94a18-620">Формат (**CSV** или **HTML**).</span><span class="sxs-lookup"><span data-stu-id="94a18-620">The format, either **CSV** or **HTML**.</span></span>|
|<span data-ttu-id="94a18-621">columns</span><span class="sxs-lookup"><span data-stu-id="94a18-621">columns</span></span>|<span data-ttu-id="94a18-622">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-622">No</span></span>|<span data-ttu-id="94a18-623">Массив,</span><span class="sxs-lookup"><span data-stu-id="94a18-623">Array</span></span>|<span data-ttu-id="94a18-624">Столбцы.</span><span class="sxs-lookup"><span data-stu-id="94a18-624">The columns.</span></span> <span data-ttu-id="94a18-625">Позволяет переопределить стандартную форму таблицы.</span><span class="sxs-lookup"><span data-stu-id="94a18-625">Allows to override the default shape of the table.</span></span>|
|<span data-ttu-id="94a18-626">column header</span><span class="sxs-lookup"><span data-stu-id="94a18-626">column header</span></span>|<span data-ttu-id="94a18-627">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-627">No</span></span>|<span data-ttu-id="94a18-628">string</span><span class="sxs-lookup"><span data-stu-id="94a18-628">String</span></span>|<span data-ttu-id="94a18-629">Заголовок столбца.</span><span class="sxs-lookup"><span data-stu-id="94a18-629">The header of the column.</span></span>|
|<span data-ttu-id="94a18-630">column value</span><span class="sxs-lookup"><span data-stu-id="94a18-630">column value</span></span>|<span data-ttu-id="94a18-631">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-631">Yes</span></span>|<span data-ttu-id="94a18-632">Строка</span><span class="sxs-lookup"><span data-stu-id="94a18-632">String</span></span>|<span data-ttu-id="94a18-633">Значение столбца.</span><span class="sxs-lookup"><span data-stu-id="94a18-633">The value of the column.</span></span>|

## <a name="workflow-action"></a><span data-ttu-id="94a18-634">Действие workflow</span><span class="sxs-lookup"><span data-stu-id="94a18-634">Workflow action</span></span>   

|<span data-ttu-id="94a18-635">Имя</span><span class="sxs-lookup"><span data-stu-id="94a18-635">Name</span></span>|<span data-ttu-id="94a18-636">Обязательно</span><span class="sxs-lookup"><span data-stu-id="94a18-636">Required</span></span>|<span data-ttu-id="94a18-637">Тип</span><span class="sxs-lookup"><span data-stu-id="94a18-637">Type</span></span>|<span data-ttu-id="94a18-638">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-638">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="94a18-639">host id</span><span class="sxs-lookup"><span data-stu-id="94a18-639">host id</span></span>|<span data-ttu-id="94a18-640">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-640">Yes</span></span>|<span data-ttu-id="94a18-641">string</span><span class="sxs-lookup"><span data-stu-id="94a18-641">String</span></span>|<span data-ttu-id="94a18-642">Идентификатор ресурса рабочего процесса, который требуется вызвать.</span><span class="sxs-lookup"><span data-stu-id="94a18-642">The resource ID of the workflow that you want to call.</span></span>|  
|<span data-ttu-id="94a18-643">host triggerName</span><span class="sxs-lookup"><span data-stu-id="94a18-643">host triggerName</span></span>|<span data-ttu-id="94a18-644">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-644">Yes</span></span>|<span data-ttu-id="94a18-645">string</span><span class="sxs-lookup"><span data-stu-id="94a18-645">String</span></span>|<span data-ttu-id="94a18-646">Имя триггера, который необходимо вызвать.</span><span class="sxs-lookup"><span data-stu-id="94a18-646">The name of the trigger that you want to invoke.</span></span>|  
|<span data-ttu-id="94a18-647">Запросы</span><span class="sxs-lookup"><span data-stu-id="94a18-647">queries</span></span>|<span data-ttu-id="94a18-648">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-648">No</span></span>|<span data-ttu-id="94a18-649">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-649">Object</span></span>|<span data-ttu-id="94a18-650">Представляет параметры запроса для добавления в URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="94a18-650">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="94a18-651">Например, `"queries" : { "api-version": "2015-02-01" }` добавляет `?api-version=2015-02-01` в URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="94a18-651">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="94a18-652">headers</span><span class="sxs-lookup"><span data-stu-id="94a18-652">headers</span></span>|<span data-ttu-id="94a18-653">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-653">No</span></span>|<span data-ttu-id="94a18-654">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-654">Object</span></span>|<span data-ttu-id="94a18-655">Представляет все заголовки, которые отправляются в запрос.</span><span class="sxs-lookup"><span data-stu-id="94a18-655">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="94a18-656">Например, чтобы задать язык и тип запроса: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="94a18-656">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="94a18-657">текст</span><span class="sxs-lookup"><span data-stu-id="94a18-657">body</span></span>|<span data-ttu-id="94a18-658">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-658">No</span></span>|<span data-ttu-id="94a18-659">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-659">Object</span></span>|<span data-ttu-id="94a18-660">Представляет полезные данные, отправляемые конечной точке.</span><span class="sxs-lookup"><span data-stu-id="94a18-660">Represents the payload sent to the endpoint.</span></span>|  
  
```json
"mynestedwf" : {
    "type" : "workflow",
    "inputs" : {
        "host" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName " : "mytrigger001"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()",
            "Content-type" : "application/json"
        },
        "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
    }
```
  
<span data-ttu-id="94a18-661">Проверка доступа выполняется в рабочем процессе, \(точнее в триггере\). Это означает, что требуется доступ к рабочему процессу.</span><span class="sxs-lookup"><span data-stu-id="94a18-661">An access check is made on the workflow \(more specifically, the trigger\), meaning you need access to the workflow.</span></span>  
  
<span data-ttu-id="94a18-662">Выходные данные действия `workflow` основаны на заданном в действии `response` в дочернем рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="94a18-662">The outputs from the `workflow` action are based on what you defined in the `response` action in the child workflow.</span></span> <span data-ttu-id="94a18-663">Если действие `response` не задано, выходные данные будут пустыми.</span><span class="sxs-lookup"><span data-stu-id="94a18-663">If you have not defined any `response` action, then the outputs are empty.</span></span>  

## <a name="function-action"></a><span data-ttu-id="94a18-664">Действие функции</span><span class="sxs-lookup"><span data-stu-id="94a18-664">Function action</span></span>   

|<span data-ttu-id="94a18-665">Имя</span><span class="sxs-lookup"><span data-stu-id="94a18-665">Name</span></span>|<span data-ttu-id="94a18-666">Обязательно</span><span class="sxs-lookup"><span data-stu-id="94a18-666">Required</span></span>|<span data-ttu-id="94a18-667">Тип</span><span class="sxs-lookup"><span data-stu-id="94a18-667">Type</span></span>|<span data-ttu-id="94a18-668">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-668">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="94a18-669">ИД функции</span><span class="sxs-lookup"><span data-stu-id="94a18-669">function id</span></span>|<span data-ttu-id="94a18-670">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-670">Yes</span></span>|<span data-ttu-id="94a18-671">string</span><span class="sxs-lookup"><span data-stu-id="94a18-671">String</span></span>|<span data-ttu-id="94a18-672">Идентификатор ресурса функции, которую требуется вызвать.</span><span class="sxs-lookup"><span data-stu-id="94a18-672">The resource ID of the function that you want to invoke.</span></span>|  
|<span data-ttu-id="94a18-673">метод</span><span class="sxs-lookup"><span data-stu-id="94a18-673">method</span></span>|<span data-ttu-id="94a18-674">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-674">No</span></span>|<span data-ttu-id="94a18-675">Строка</span><span class="sxs-lookup"><span data-stu-id="94a18-675">String</span></span>|<span data-ttu-id="94a18-676">Метод HTTP, используемый для вызова функции.</span><span class="sxs-lookup"><span data-stu-id="94a18-676">The HTTP method used to invoke the function.</span></span> <span data-ttu-id="94a18-677">Если не указан, по умолчанию используется `POST`.</span><span class="sxs-lookup"><span data-stu-id="94a18-677">By default, it is `POST` when not specified.</span></span>|  
|<span data-ttu-id="94a18-678">Запросы</span><span class="sxs-lookup"><span data-stu-id="94a18-678">queries</span></span>|<span data-ttu-id="94a18-679">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-679">No</span></span>|<span data-ttu-id="94a18-680">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-680">Object</span></span>|<span data-ttu-id="94a18-681">Представляет параметры запроса для добавления в URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="94a18-681">Represents the query parameters to add to the URL.</span></span> <span data-ttu-id="94a18-682">Например, `"queries" : { "api-version": "2015-02-01" }` добавляет `?api-version=2015-02-01` в URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="94a18-682">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` to the URL.</span></span>|  
|<span data-ttu-id="94a18-683">headers</span><span class="sxs-lookup"><span data-stu-id="94a18-683">headers</span></span>|<span data-ttu-id="94a18-684">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-684">No</span></span>|<span data-ttu-id="94a18-685">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-685">Object</span></span>|<span data-ttu-id="94a18-686">Представляет все заголовки, которые отправляются в запрос.</span><span class="sxs-lookup"><span data-stu-id="94a18-686">Represents each of the headers that is sent to the request.</span></span> <span data-ttu-id="94a18-687">Например, чтобы задать язык и тип запроса: `"headers" : { "Accept-Language": "en-us" }`.</span><span class="sxs-lookup"><span data-stu-id="94a18-687">For example, to set the language and type on a request: `"headers" : { "Accept-Language": "en-us" }`.</span></span>|  
|<span data-ttu-id="94a18-688">текст</span><span class="sxs-lookup"><span data-stu-id="94a18-688">body</span></span>|<span data-ttu-id="94a18-689">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-689">No</span></span>|<span data-ttu-id="94a18-690">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-690">Object</span></span>|<span data-ttu-id="94a18-691">Представляет полезные данные, отправляемые конечной точке.</span><span class="sxs-lookup"><span data-stu-id="94a18-691">Represents the payload sent to the endpoint.</span></span>|  

```json
"myfunc" : {
    "type" : "Function",
    "inputs" : {
        "function" : {
            "id" : "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Web/sites/myfuncapp/functions/myfunc"
        },
        "queries" : {
            "extrafield" : "specialValue"
        },  
        "headers" : {
            "x-ms-date" : "@utcnow()"
        },
        "method" : "POST",
    "body" : {
            "contentFieldOne" : "value100",
            "anotherField" : 10.001
        }
    },
    "runAfter": {}
}
```

<span data-ttu-id="94a18-692">При сохранении приложения логики мы выполняем ряд проверок указанной функции.</span><span class="sxs-lookup"><span data-stu-id="94a18-692">When you save the logic app, we perform some checks on the referenced function:</span></span>
-   <span data-ttu-id="94a18-693">У вас должен быть доступ к функции.</span><span class="sxs-lookup"><span data-stu-id="94a18-693">You need to have access to the function.</span></span>
-   <span data-ttu-id="94a18-694">Допускается только стандартный триггер HTTP или универсальный триггер webhook в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="94a18-694">Only standard HTTP trigger or generic JSON webhook trigger is allowed.</span></span>
-   <span data-ttu-id="94a18-695">В ней не должен быть определен какой-либо маршрут.</span><span class="sxs-lookup"><span data-stu-id="94a18-695">It should not have any route defined.</span></span>
-   <span data-ttu-id="94a18-696">Допускаются только авторизация с помощью функции и анонимная авторизация.</span><span class="sxs-lookup"><span data-stu-id="94a18-696">Only "function" and "anonymous" authorization level is allowed.</span></span>

<span data-ttu-id="94a18-697">URL-адрес триггера извлекается, помещается в кэш и используется во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="94a18-697">The trigger URL is retrieved, cached, and used at runtime.</span></span> <span data-ttu-id="94a18-698">Поэтому, если какая-либо операция делает недействительным кэшированный URL-адрес, то во время выполнения действие заканчивается сбоем.</span><span class="sxs-lookup"><span data-stu-id="94a18-698">So if any operation invalidates the cached URL, the action fails at runtime.</span></span> <span data-ttu-id="94a18-699">Чтобы обойти это, еще раз сохраните приложение логики. При этом приложение логики повторно получит и поместит в кэш URL-адрес триггера.</span><span class="sxs-lookup"><span data-stu-id="94a18-699">To work around this, save the logic app again, which will cause logic app to retrieve and cache the trigger URL again.</span></span>

## <a name="collection-actions-scopes-and-loops"></a><span data-ttu-id="94a18-700">Действия коллекций (области и циклы)</span><span class="sxs-lookup"><span data-stu-id="94a18-700">Collection actions (scopes and loops)</span></span>

<span data-ttu-id="94a18-701">Действия некоторых типов могут содержать вложенные действия.</span><span class="sxs-lookup"><span data-stu-id="94a18-701">Some action types can contain actions within themselves.</span></span> <span data-ttu-id="94a18-702">На действия ссылок в коллекции можно ссылаться непосредственно за пределами коллекции.</span><span class="sxs-lookup"><span data-stu-id="94a18-702">Reference actions within a collection can be referenced directly outside of the collection.</span></span> <span data-ttu-id="94a18-703">Если вы определили `http` в области, `@body('http')` действительно в любой точке рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="94a18-703">If you defined `http` in a scope, `@body('http')` is still valid anywhere in a workflow.</span></span> <span data-ttu-id="94a18-704">Действия в коллекции могут выполнять (`runAfter`) только после других действий в этой коллекции.</span><span class="sxs-lookup"><span data-stu-id="94a18-704">Actions within a collection can `runAfter` only other actions within the same collection.</span></span>

## <a name="scope-action"></a><span data-ttu-id="94a18-705">Действие scope</span><span class="sxs-lookup"><span data-stu-id="94a18-705">Scope action</span></span>

<span data-ttu-id="94a18-706">Действие `scope` позволяет логически группировать действия в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="94a18-706">The `scope` action lets you logically group actions in a workflow.</span></span>

|<span data-ttu-id="94a18-707">Имя</span><span class="sxs-lookup"><span data-stu-id="94a18-707">Name</span></span>|<span data-ttu-id="94a18-708">Обязательно</span><span class="sxs-lookup"><span data-stu-id="94a18-708">Required</span></span>|<span data-ttu-id="94a18-709">Тип</span><span class="sxs-lookup"><span data-stu-id="94a18-709">Type</span></span>|<span data-ttu-id="94a18-710">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-710">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="94a18-711">actions</span><span class="sxs-lookup"><span data-stu-id="94a18-711">actions</span></span>|<span data-ttu-id="94a18-712">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-712">Yes</span></span>|<span data-ttu-id="94a18-713">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-713">Object</span></span>|<span data-ttu-id="94a18-714">Внутренние действия, выполняемые в области.</span><span class="sxs-lookup"><span data-stu-id="94a18-714">Inner actions to execute within the scope</span></span>|

```json
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```

## <a name="foreach-action"></a><span data-ttu-id="94a18-715">Действие foreach</span><span class="sxs-lookup"><span data-stu-id="94a18-715">ForEach action</span></span>

<span data-ttu-id="94a18-716">Это циклическое действие выполняет итерацию по массиву и внутренние действия для каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="94a18-716">This looping action iterates through an array and performs inner actions for each item.</span></span> <span data-ttu-id="94a18-717">По умолчанию цикл ForEach выполняется параллельно (20 параллельных выполнений одновременно).</span><span class="sxs-lookup"><span data-stu-id="94a18-717">By default, the foreach loop executes in parallel (20 executions in parallel at a time).</span></span> <span data-ttu-id="94a18-718">Правила выполнения можно задать с помощью параметра `operationOptions`.</span><span class="sxs-lookup"><span data-stu-id="94a18-718">You can set execution rules using the `operationOptions` parameter.</span></span>

|<span data-ttu-id="94a18-719">Имя</span><span class="sxs-lookup"><span data-stu-id="94a18-719">Name</span></span>|<span data-ttu-id="94a18-720">Обязательно</span><span class="sxs-lookup"><span data-stu-id="94a18-720">Required</span></span>|<span data-ttu-id="94a18-721">Тип</span><span class="sxs-lookup"><span data-stu-id="94a18-721">Type</span></span>|<span data-ttu-id="94a18-722">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-722">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="94a18-723">actions</span><span class="sxs-lookup"><span data-stu-id="94a18-723">actions</span></span>|<span data-ttu-id="94a18-724">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-724">Yes</span></span>|<span data-ttu-id="94a18-725">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-725">Object</span></span>|<span data-ttu-id="94a18-726">Внутренние действия, выполняемые в цикле.</span><span class="sxs-lookup"><span data-stu-id="94a18-726">Inner actions to execute within the loop</span></span>|
|<span data-ttu-id="94a18-727">foreach</span><span class="sxs-lookup"><span data-stu-id="94a18-727">foreach</span></span>|<span data-ttu-id="94a18-728">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-728">Yes</span></span>|<span data-ttu-id="94a18-729">строка</span><span class="sxs-lookup"><span data-stu-id="94a18-729">string</span></span>|<span data-ttu-id="94a18-730">Массив для итерации.</span><span class="sxs-lookup"><span data-stu-id="94a18-730">The array to iterate over</span></span>|
|<span data-ttu-id="94a18-731">operationOptions</span><span class="sxs-lookup"><span data-stu-id="94a18-731">operationOptions</span></span>|<span data-ttu-id="94a18-732">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-732">no</span></span>|<span data-ttu-id="94a18-733">строка</span><span class="sxs-lookup"><span data-stu-id="94a18-733">string</span></span>|<span data-ttu-id="94a18-734">Любые параметры операции для определения поведения.</span><span class="sxs-lookup"><span data-stu-id="94a18-734">Any operation options for behavior.</span></span> <span data-ttu-id="94a18-735">В данный момент поддерживается только `sequential` для последовательного выполнения итераций (поведение по умолчанию — параллельное выполнение).</span><span class="sxs-lookup"><span data-stu-id="94a18-735">Currently only supports `sequential` to execute iterations sequentially (default behavior is parallel)</span></span>|

```json
"forEach_email": {
    "type": "foreach",
    "foreach": "@body('email_filter')",
    "actions": {
        "send_email": {
            "type": "ApiConnection",
            "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                }
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                }
            }
        }
    },
    "runAfter":{
        "email_filter": [ "Succeeded" ]
    }
}
```

## <a name="until-action"></a><span data-ttu-id="94a18-736">Действие Until</span><span class="sxs-lookup"><span data-stu-id="94a18-736">Until action</span></span>

<span data-ttu-id="94a18-737">Это циклическое действие выполняет внутренние действия, пока для условия не возвращается значение true.</span><span class="sxs-lookup"><span data-stu-id="94a18-737">This looping action executes inner actions until a condition results to true.</span></span>

|<span data-ttu-id="94a18-738">Имя</span><span class="sxs-lookup"><span data-stu-id="94a18-738">Name</span></span>|<span data-ttu-id="94a18-739">Обязательно</span><span class="sxs-lookup"><span data-stu-id="94a18-739">Required</span></span>|<span data-ttu-id="94a18-740">Тип</span><span class="sxs-lookup"><span data-stu-id="94a18-740">Type</span></span>|<span data-ttu-id="94a18-741">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-741">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="94a18-742">actions</span><span class="sxs-lookup"><span data-stu-id="94a18-742">actions</span></span>|<span data-ttu-id="94a18-743">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-743">Yes</span></span>|<span data-ttu-id="94a18-744">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-744">Object</span></span>|<span data-ttu-id="94a18-745">Внутренние действия, выполняемые в цикле.</span><span class="sxs-lookup"><span data-stu-id="94a18-745">Inner actions to execute within the loop</span></span>|
|<span data-ttu-id="94a18-746">expression</span><span class="sxs-lookup"><span data-stu-id="94a18-746">expression</span></span>|<span data-ttu-id="94a18-747">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-747">Yes</span></span>|<span data-ttu-id="94a18-748">string</span><span class="sxs-lookup"><span data-stu-id="94a18-748">string</span></span>|<span data-ttu-id="94a18-749">Выражение, вычисляемое после каждой итерации.</span><span class="sxs-lookup"><span data-stu-id="94a18-749">The expression to evaluate after each iteration</span></span>|
|<span data-ttu-id="94a18-750">limit</span><span class="sxs-lookup"><span data-stu-id="94a18-750">limit</span></span>|<span data-ttu-id="94a18-751">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-751">yes</span></span>|<span data-ttu-id="94a18-752">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-752">Object</span></span>|<span data-ttu-id="94a18-753">Для цикла должно быть определено по крайней мере одно ограничение.</span><span class="sxs-lookup"><span data-stu-id="94a18-753">The limits for the loop - at least one limit must be defined</span></span>|
|<span data-ttu-id="94a18-754">count</span><span class="sxs-lookup"><span data-stu-id="94a18-754">count</span></span>|<span data-ttu-id="94a18-755">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-755">no</span></span>|<span data-ttu-id="94a18-756">int</span><span class="sxs-lookup"><span data-stu-id="94a18-756">int</span></span>|<span data-ttu-id="94a18-757">Ограничение на число итераций, которые могут быть выполнены.</span><span class="sxs-lookup"><span data-stu-id="94a18-757">The limit to the number of iterations that can be performed</span></span>|
|<span data-ttu-id="94a18-758">timeout</span><span class="sxs-lookup"><span data-stu-id="94a18-758">timeout</span></span>|<span data-ttu-id="94a18-759">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-759">no</span></span>|<span data-ttu-id="94a18-760">строка</span><span class="sxs-lookup"><span data-stu-id="94a18-760">string</span></span>|<span data-ttu-id="94a18-761">Время ожидания выполнения цикла</span><span class="sxs-lookup"><span data-stu-id="94a18-761">The timeout for how long it should loop.</span></span>  <span data-ttu-id="94a18-762">(в формате ISO 8601).</span><span class="sxs-lookup"><span data-stu-id="94a18-762">ISO 8601 format</span></span>|


```json
 "Until_succeeded": {
    "actions": {
        "Http": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "expression": "@equals(outputs('Http')['statusCode', 200)",
    "limit": {
        "count": 1000,
        "timeout": "PT1H"
    },
    "runAfter": {},
    "type": "Until"
}
```

## <a name="conditions---if-action"></a><span data-ttu-id="94a18-763">Условия. Действие If</span><span class="sxs-lookup"><span data-stu-id="94a18-763">Conditions - If Action</span></span>

<span data-ttu-id="94a18-764">Действие `If` позволяет вычислить условие и выполнить ветвь в зависимости от того, получает ли выражение значение `true`.</span><span class="sxs-lookup"><span data-stu-id="94a18-764">The `If` action lets you evaluate a condition and execute a branch based on whether the expression evaluates to `true`.</span></span>

|<span data-ttu-id="94a18-765">Имя</span><span class="sxs-lookup"><span data-stu-id="94a18-765">Name</span></span>|<span data-ttu-id="94a18-766">Обязательно</span><span class="sxs-lookup"><span data-stu-id="94a18-766">Required</span></span>|<span data-ttu-id="94a18-767">Тип</span><span class="sxs-lookup"><span data-stu-id="94a18-767">Type</span></span>|<span data-ttu-id="94a18-768">Описание</span><span class="sxs-lookup"><span data-stu-id="94a18-768">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="94a18-769">actions</span><span class="sxs-lookup"><span data-stu-id="94a18-769">actions</span></span>|<span data-ttu-id="94a18-770">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-770">Yes</span></span>|<span data-ttu-id="94a18-771">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-771">Object</span></span>|<span data-ttu-id="94a18-772">Внутренние действия, выполняемые, когда выражение получает значение `true`.</span><span class="sxs-lookup"><span data-stu-id="94a18-772">Inner actions to execute when expression evaluates to `true`</span></span>|
|<span data-ttu-id="94a18-773">expression</span><span class="sxs-lookup"><span data-stu-id="94a18-773">expression</span></span>|<span data-ttu-id="94a18-774">Да</span><span class="sxs-lookup"><span data-stu-id="94a18-774">Yes</span></span>|<span data-ttu-id="94a18-775">строка</span><span class="sxs-lookup"><span data-stu-id="94a18-775">string</span></span>|<span data-ttu-id="94a18-776">Выражение для вычисления.</span><span class="sxs-lookup"><span data-stu-id="94a18-776">The expression to evaluate</span></span>|
|<span data-ttu-id="94a18-777">else</span><span class="sxs-lookup"><span data-stu-id="94a18-777">else</span></span>|<span data-ttu-id="94a18-778">Нет</span><span class="sxs-lookup"><span data-stu-id="94a18-778">no</span></span>|<span data-ttu-id="94a18-779">Объект</span><span class="sxs-lookup"><span data-stu-id="94a18-779">Object</span></span>|<span data-ttu-id="94a18-780">Внутренние действия, выполняемые, когда выражение получает значение `false`.</span><span class="sxs-lookup"><span data-stu-id="94a18-780">Inner actions to execute when expression evaluates to `false`</span></span>|
  
```json
"My_condition": {
    "actions": {
        "If_true": {
            "inputs": {
                "method": "GET",
                "uri": "http://myurl"
            },
            "runAfter": {},
            "type": "Http"
        }
    },
    "else": {
        "actions": {
            "if_false": {
                "inputs": {
                    "method": "GET",
                    "uri": "http://myurl"
                },
                "runAfter": {},
                "type": "Http"
            }
        }
    },
    "expression": "@equals(triggerBody(), json(true))",
    "runAfter": {},
    "type": "If"
}
```  
  
<span data-ttu-id="94a18-781">Ниже приведены примеры, как условия могут использовать выражения в действии.</span><span class="sxs-lookup"><span data-stu-id="94a18-781">The following table shows examples of how conditions can use expressions in an action:</span></span>  
  
|<span data-ttu-id="94a18-782">Значение JSON</span><span class="sxs-lookup"><span data-stu-id="94a18-782">JSON value</span></span>|<span data-ttu-id="94a18-783">Результат</span><span class="sxs-lookup"><span data-stu-id="94a18-783">Result</span></span>|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|<span data-ttu-id="94a18-784">Условие выполняется при наличии какого-либо значения, которое возвращает значение true для выражения.</span><span class="sxs-lookup"><span data-stu-id="94a18-784">Any value that would evaluate to true causes this condition to pass.</span></span> <span data-ttu-id="94a18-785">Поддерживаются только логические выражения.</span><span class="sxs-lookup"><span data-stu-id="94a18-785">Only Boolean expressions are supported.</span></span> <span data-ttu-id="94a18-786">Для преобразования других типов в логическое значение используются функции `empty` и `equals`.</span><span class="sxs-lookup"><span data-stu-id="94a18-786">To convert other types to Boolean, use functions `empty`, `equals`.</span></span>|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|<span data-ttu-id="94a18-787">Поддерживаются функции сравнения.</span><span class="sxs-lookup"><span data-stu-id="94a18-787">Comparison functions are supported.</span></span> <span data-ttu-id="94a18-788">В этом примере действие выполняется, только если выходные данные act1 превышают пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="94a18-788">For the example here, the action only executes when the output of act1 is greater than the threshold.</span></span>|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|<span data-ttu-id="94a18-789">Функции логики позволяют создавать вложенные логические выражения.</span><span class="sxs-lookup"><span data-stu-id="94a18-789">Logic functions are also supported to create nested Boolean expressions.</span></span> <span data-ttu-id="94a18-790">В этом случае действие выполняется, если выходные данные act1 выше порогового значения или меньше 100.</span><span class="sxs-lookup"><span data-stu-id="94a18-790">In this case, the action executes when the output of act1 is above the threshold or below 100.</span></span>|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|<span data-ttu-id="94a18-791">Чтобы проверить, содержит ли массив элементы, можно использовать функции массива.</span><span class="sxs-lookup"><span data-stu-id="94a18-791">You can use array functions to check if an array has any items.</span></span> <span data-ttu-id="94a18-792">В этом случае действие выполняется, если массив ошибок пустой.</span><span class="sxs-lookup"><span data-stu-id="94a18-792">In this case, the action executes when the errors array is empty.</span></span>| 
|`"expression": "parameters('hasSpecialAction')"`|<span data-ttu-id="94a18-793">Ошибка является недопустимым условием, поскольку для условия требуется @.</span><span class="sxs-lookup"><span data-stu-id="94a18-793">Error - not a valid condition because @ is required for conditions.</span></span>|  
  
<span data-ttu-id="94a18-794">Если условие выполняется успешно, оно помечается как `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="94a18-794">If a condition evaluates successfully, the condition is marked as `Succeeded`.</span></span> <span data-ttu-id="94a18-795">Действия в объектах `actions` или `else` помечаются как `Succeeded` при успешном выполнении, `Failed` при выполнении с ошибкой или `Skipped`, если эта ветвь не выполняется.</span><span class="sxs-lookup"><span data-stu-id="94a18-795">Actions within either the `actions` or `else` objects evaluate to `Succeeded` when executed and succeeded, `Failed` when executed and failed, or `Skipped` when that branch is not executed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94a18-796">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="94a18-796">Next steps</span></span>

[<span data-ttu-id="94a18-797">REST API службы рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="94a18-797">Workflow Service REST API</span></span>](https://docs.microsoft.com/rest/api/logic/workflows)
