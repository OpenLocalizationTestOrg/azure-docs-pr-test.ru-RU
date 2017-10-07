---
title: "aaaWorkflow действия и триггеры — логика приложения Azure | Документы Microsoft"
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
ms.openlocfilehash: 857927b7d7df3fc9cdc4931ffdb613efde0db9f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="workflow-actions-and-triggers-for-azure-logic-apps"></a><span data-ttu-id="26839-102">Действия и триггеры рабочих процессов в Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="26839-102">Workflow actions and triggers for Azure Logic Apps</span></span>

<span data-ttu-id="26839-103">Приложения логики состоят из триггеров и действий.</span><span class="sxs-lookup"><span data-stu-id="26839-103">Logic apps consist of triggers and actions.</span></span> <span data-ttu-id="26839-104">Существует шесть типов триггеров.</span><span class="sxs-lookup"><span data-stu-id="26839-104">There are six types of triggers.</span></span> <span data-ttu-id="26839-105">У каждого из них свой интерфейс и разное поведение.</span><span class="sxs-lookup"><span data-stu-id="26839-105">Each type has different interface and different behavior.</span></span> <span data-ttu-id="26839-106">Также можно узнать о других сведений, просмотрев сведения hello объекта hello [язык определения рабочих процессов](logic-apps-workflow-definition-language.md).</span><span class="sxs-lookup"><span data-stu-id="26839-106">You can also learn about other details by looking at hello details of hello [Workflow Definition Language](logic-apps-workflow-definition-language.md).</span></span>  
  
<span data-ttu-id="26839-107">Прочитано toolearn Дополнительные сведения о триггеров, действий и использования их toobuild логику приложения tooimprove бизнес-процессов и рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="26839-107">Read on toolearn more about triggers and actions and how you might use them toobuild logic apps tooimprove your business processes and workflows.</span></span>  
  
### <a name="triggers"></a><span data-ttu-id="26839-108">триггеры;</span><span class="sxs-lookup"><span data-stu-id="26839-108">Triggers</span></span>  

<span data-ttu-id="26839-109">Триггер задает hello вызовов, которые можно инициировать запуск рабочего процесса логику приложения.</span><span class="sxs-lookup"><span data-stu-id="26839-109">A trigger specifies hello calls that can initiate a run of your logic app workflow.</span></span> <span data-ttu-id="26839-110">Ниже приведены два разных способа hello tooinitiate выполнения рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="26839-110">Here are hello two different ways tooinitiate a run of your workflow:</span></span>  
  
-   <span data-ttu-id="26839-111">с помощью опрашивающего триггера;</span><span class="sxs-lookup"><span data-stu-id="26839-111">A polling trigger</span></span>  

-   <span data-ttu-id="26839-112">Триггер push - по вызывающему Привет [API REST службы рабочего процесса](https://docs.microsoft.com/rest/api/logic/workflows)</span><span class="sxs-lookup"><span data-stu-id="26839-112">A push trigger - by calling hello [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows)</span></span>  
  
<span data-ttu-id="26839-113">Все триггеры содержат следующие элементы верхнего уровня:</span><span class="sxs-lookup"><span data-stu-id="26839-113">All triggers contain these top-level elements:</span></span>  
  
```json
"<name-of-the-trigger>" : {
    "type": "<type-of-trigger>",
    "inputs": { <settings-for-the-call> },
    "recurrence": {  
        "frequency": "Second|Minute|Hour|Week|Month|Year",
        "interval": "<recurrence interval in units of frequency>"
    },
    "conditions": [ <array-of-required-conditions > ],
    "splitOn" : "<property toocreate runs for>",
    "operationOptions": "<operation options on hello trigger>"
}
```

### <a name="trigger-types-and-their-inputs"></a><span data-ttu-id="26839-114">Типы триггеров и их входные данные</span><span class="sxs-lookup"><span data-stu-id="26839-114">Trigger types and their inputs</span></span>  

<span data-ttu-id="26839-115">Можно использовать такие типы триггеров:</span><span class="sxs-lookup"><span data-stu-id="26839-115">You can use these types of triggers:</span></span>
  
-   <span data-ttu-id="26839-116">**Запрос** \- делает приложение hello логику конечную точку для вас toocall</span><span class="sxs-lookup"><span data-stu-id="26839-116">**Request** \- Makes hello logic app an endpoint for you toocall</span></span>  
  
-   <span data-ttu-id="26839-117">**Триггер повторения** (recurrence) — активируется на основе определенного расписания.</span><span class="sxs-lookup"><span data-stu-id="26839-117">**Recurrence** \- Fires based on a defined schedule</span></span>  
  
-   <span data-ttu-id="26839-118">**HTTP-триггер** — опрашивает конечную веб-точку HTTP.</span><span class="sxs-lookup"><span data-stu-id="26839-118">**HTTP** \- Polls an HTTP web endpoint.</span></span> <span data-ttu-id="26839-119">Hello HTTP конечной точки должны соответствовать определенным контрактом запускающее tooa \- либо с помощью 202\-асинхронный шаблон, или, возвращая массив</span><span class="sxs-lookup"><span data-stu-id="26839-119">hello HTTP endpoint must conform tooa specific triggering contract \- either by using a 202\-async pattern, or by returning an array</span></span>  
  
-   <span data-ttu-id="26839-120">**ApiConnection** \- активировать опросы как hello HTTP, однако она использует преимущества hello [API-интерфейсы, управляемая корпорацией Майкрософт](https://docs.microsoft.com/azure/connectors/apis-list)</span><span class="sxs-lookup"><span data-stu-id="26839-120">**ApiConnection** \- Polls like hello HTTP trigger, however, it takes advantage of hello [Microsoft-managed APIs](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>  
  
-   <span data-ttu-id="26839-121">**HTTPWebhook** \- открывает конечной точки, аналогичные toohello триггер запуска вручную, однако он также вызывает tooa указан URL-адрес tooregister и отмены регистрации</span><span class="sxs-lookup"><span data-stu-id="26839-121">**HTTPWebhook** \- Opens an endpoint, similar toohello Manual trigger, however, it also calls out tooa specified URL tooregister and unregister</span></span>  
  
-   <span data-ttu-id="26839-122">**ApiConnectionWebhook** \- работает как hello HTTPWebhook триггер, используя преимущества hello API-интерфейсы, управляемая корпорацией Майкрософт</span><span class="sxs-lookup"><span data-stu-id="26839-122">**ApiConnectionWebhook** \- Operates like hello HTTPWebhook trigger by taking advantage of hello Microsoft-managed APIs</span></span>       
    <span data-ttu-id="26839-123">Каждый тип триггера имеет разный набор **входных данных**, определяющий его поведение.</span><span class="sxs-lookup"><span data-stu-id="26839-123">Each trigger type has a different set of **inputs** that defines its behavior.</span></span>  
  
## <a name="request-trigger"></a><span data-ttu-id="26839-124">Триггер запросов</span><span class="sxs-lookup"><span data-stu-id="26839-124">Request trigger</span></span>  

<span data-ttu-id="26839-125">Этот триггер служит в качестве конечной точки, которые можно вызвать через HTTP-запроса tooinvoke логику приложения.</span><span class="sxs-lookup"><span data-stu-id="26839-125">This trigger serves as an endpoint that you call via an HTTP Request tooinvoke your logic app.</span></span> <span data-ttu-id="26839-126">Триггер запроса выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="26839-126">A request trigger looks like this example:</span></span>  
  
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

<span data-ttu-id="26839-127">Имеется также необязательное свойство, которое называется **schema**.</span><span class="sxs-lookup"><span data-stu-id="26839-127">There is also an optional property called **schema**:</span></span>  
  
|<span data-ttu-id="26839-128">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="26839-128">Element name</span></span>|<span data-ttu-id="26839-129">Обязательно</span><span class="sxs-lookup"><span data-stu-id="26839-129">Required</span></span>|<span data-ttu-id="26839-130">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-130">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="26839-131">schema</span><span class="sxs-lookup"><span data-stu-id="26839-131">schema</span></span>|<span data-ttu-id="26839-132">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-132">No</span></span>|<span data-ttu-id="26839-133">Схема JSON, которая проверяет hello входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="26839-133">A JSON schema that validates hello incoming request.</span></span> <span data-ttu-id="26839-134">Это полезно для помогает знать, какие свойства tooreference действия последующих рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="26839-134">Useful for helping subsequent workflow steps know which properties tooreference.</span></span>|

<span data-ttu-id="26839-135">tooinvoke этой конечной точки требуется toocall hello *listCallbackUrl* API.</span><span class="sxs-lookup"><span data-stu-id="26839-135">tooinvoke this endpoint, you need toocall hello *listCallbackUrl* API.</span></span> <span data-ttu-id="26839-136">См. сведения в статье [Рабочие процессы](https://docs.microsoft.com/rest/api/logic/workflows).</span><span class="sxs-lookup"><span data-stu-id="26839-136">See [Workflow Service REST API](https://docs.microsoft.com/rest/api/logic/workflows).</span></span>  
  
## <a name="recurrence-trigger"></a><span data-ttu-id="26839-137">Триггер повторения</span><span class="sxs-lookup"><span data-stu-id="26839-137">Recurrence trigger</span></span>  

<span data-ttu-id="26839-138">Триггер recurrence — это триггер, который выполняется на основе заданного расписания.</span><span class="sxs-lookup"><span data-stu-id="26839-138">A Recurrence trigger is one that runs based on a defined schedule.</span></span> <span data-ttu-id="26839-139">Такой триггер может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="26839-139">Such a trigger might look like this example:</span></span>  

```json
"dailyReport" : {
    "type": "recurrence",
    "recurrence": {
        "frequency": "Day",
        "interval": "1"
    }
}
```

<span data-ttu-id="26839-140">Как видите, это простой способ toorun рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="26839-140">As you can see, it is a simple way toorun a workflow.</span></span>  
  
|<span data-ttu-id="26839-141">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="26839-141">Element name</span></span>|<span data-ttu-id="26839-142">Обязательно</span><span class="sxs-lookup"><span data-stu-id="26839-142">Required</span></span>|<span data-ttu-id="26839-143">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-143">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="26839-144">frequency</span><span class="sxs-lookup"><span data-stu-id="26839-144">frequency</span></span>|<span data-ttu-id="26839-145">Да</span><span class="sxs-lookup"><span data-stu-id="26839-145">Yes</span></span>|<span data-ttu-id="26839-146">Как часто hello триггер выполняет.</span><span class="sxs-lookup"><span data-stu-id="26839-146">How often hello trigger executes.</span></span> <span data-ttu-id="26839-147">Используйте только одно из этих значений: Second, Minute, Hour, Day, Week, Month или Year.</span><span class="sxs-lookup"><span data-stu-id="26839-147">Use only one of these possible values: second, minute, hour, day, week, month, or year</span></span>|  
|<span data-ttu-id="26839-148">interval</span><span class="sxs-lookup"><span data-stu-id="26839-148">interval</span></span>|<span data-ttu-id="26839-149">Да</span><span class="sxs-lookup"><span data-stu-id="26839-149">Yes</span></span>|<span data-ttu-id="26839-150">Интервал hello заданных частоту повторения hello</span><span class="sxs-lookup"><span data-stu-id="26839-150">Interval of hello given frequency for hello recurrence</span></span>|  
|<span data-ttu-id="26839-151">startTime</span><span class="sxs-lookup"><span data-stu-id="26839-151">startTime</span></span>|<span data-ttu-id="26839-152">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-152">No</span></span>|<span data-ttu-id="26839-153">Используется, если для свойства startTime указано значение без смещения от UTC.</span><span class="sxs-lookup"><span data-stu-id="26839-153">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
|<span data-ttu-id="26839-154">timeZone</span><span class="sxs-lookup"><span data-stu-id="26839-154">timeZone</span></span>|<span data-ttu-id="26839-155">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-155">no</span></span>|<span data-ttu-id="26839-156">Используется, если для свойства startTime указано значение без смещения от UTC.</span><span class="sxs-lookup"><span data-stu-id="26839-156">If a startTime is provided without a UTC offset, this timeZone is used.</span></span>|  
  
<span data-ttu-id="26839-157">Можно также запланировать триггеров toostart, выполняющихся в определенный момент в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="26839-157">You can also schedule a trigger toostart executing at some point in hello future.</span></span> <span data-ttu-id="26839-158">Например если требуется toostart еженедельную отчета каждый понедельник можно запланировать hello логику приложения toostart каждый понедельник, создав hello, следующий триггер:</span><span class="sxs-lookup"><span data-stu-id="26839-158">For example, if you want toostart a weekly report every Monday you can schedule hello logic app toostart every Monday by creating hello following trigger:</span></span>  

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

## <a name="http-trigger"></a><span data-ttu-id="26839-159">Триггер HTTP</span><span class="sxs-lookup"><span data-stu-id="26839-159">HTTP trigger</span></span>  

<span data-ttu-id="26839-160">Триггеры HTTP опроса указанной конечной точкой и проверьте наличие toodetermine ответа hello hello рабочего процесса должны быть выполнены.</span><span class="sxs-lookup"><span data-stu-id="26839-160">HTTP triggers poll a specified endpoint and check hello response toodetermine whether hello workflow should be executed.</span></span> <span data-ttu-id="26839-161">Hello объекта входных данных принимает набор hello tooconstruct необходимые параметры вызов HTTP:</span><span class="sxs-lookup"><span data-stu-id="26839-161">hello inputs object takes hello set of parameters required tooconstruct an HTTP call:</span></span>  
  
|<span data-ttu-id="26839-162">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="26839-162">Element name</span></span>|<span data-ttu-id="26839-163">Обязательно</span><span class="sxs-lookup"><span data-stu-id="26839-163">Required</span></span>|<span data-ttu-id="26839-164">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-164">Description</span></span>|<span data-ttu-id="26839-165">Тип</span><span class="sxs-lookup"><span data-stu-id="26839-165">Type</span></span>|  
|----------------|------------|---------------|--------|  
|<span data-ttu-id="26839-166">метод</span><span class="sxs-lookup"><span data-stu-id="26839-166">method</span></span>|<span data-ttu-id="26839-167">Да</span><span class="sxs-lookup"><span data-stu-id="26839-167">yes</span></span>|<span data-ttu-id="26839-168">Может принимать одно из hello следующие методы HTTP: GET, POST, PUT, DELETE, HEAD или ИСПРАВЛЕНИЯ</span><span class="sxs-lookup"><span data-stu-id="26839-168">Can be one of hello following HTTP methods: GET, POST, PUT, DELETE, PATCH, or HEAD</span></span>|<span data-ttu-id="26839-169">Строка</span><span class="sxs-lookup"><span data-stu-id="26839-169">String</span></span>|  
|<span data-ttu-id="26839-170">uri</span><span class="sxs-lookup"><span data-stu-id="26839-170">uri</span></span>|<span data-ttu-id="26839-171">Да</span><span class="sxs-lookup"><span data-stu-id="26839-171">yes</span></span>|<span data-ttu-id="26839-172">Здравствуйте, конечная точка http или https, вызывается.</span><span class="sxs-lookup"><span data-stu-id="26839-172">hello http or https endpoint that is called.</span></span> <span data-ttu-id="26839-173">Не более 2 КБ.</span><span class="sxs-lookup"><span data-stu-id="26839-173">Maximum of 2 kilobytes.</span></span>|<span data-ttu-id="26839-174">string</span><span class="sxs-lookup"><span data-stu-id="26839-174">String</span></span>|  
|<span data-ttu-id="26839-175">Запросы</span><span class="sxs-lookup"><span data-stu-id="26839-175">queries</span></span>|<span data-ttu-id="26839-176">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-176">No</span></span>|<span data-ttu-id="26839-177">Объект, представляющий URL-адрес hello запроса параметров tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="26839-177">An object representing hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="26839-178">Например `"queries" : { "api-version": "2015-02-01" }` добавляет `?api-version=2015-02-01` toohello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="26839-178">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|<span data-ttu-id="26839-179">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-179">Object</span></span>|  
|<span data-ttu-id="26839-180">headers</span><span class="sxs-lookup"><span data-stu-id="26839-180">headers</span></span>|<span data-ttu-id="26839-181">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-181">No</span></span>|<span data-ttu-id="26839-182">Объект, представляющий каждый заголовков hello, отправляет запрос toohello.</span><span class="sxs-lookup"><span data-stu-id="26839-182">An object representing each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="26839-183">Например tooset hello язык и тип запроса в:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="26839-183">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|<span data-ttu-id="26839-184">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-184">Object</span></span>|  
|<span data-ttu-id="26839-185">текст</span><span class="sxs-lookup"><span data-stu-id="26839-185">body</span></span>|<span data-ttu-id="26839-186">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-186">No</span></span>|<span data-ttu-id="26839-187">Объект, представляющий полезные данные hello, отсылаемые toohello конечной точки.</span><span class="sxs-lookup"><span data-stu-id="26839-187">An object representing hello payload that is sent toohello endpoint.</span></span>|<span data-ttu-id="26839-188">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-188">Object</span></span>|  
|<span data-ttu-id="26839-189">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="26839-189">retryPolicy</span></span>|<span data-ttu-id="26839-190">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-190">No</span></span>|<span data-ttu-id="26839-191">Объект, позволяющий настраивать поведение повтора hello 4xx или 5xx ошибок.</span><span class="sxs-lookup"><span data-stu-id="26839-191">An object that lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|<span data-ttu-id="26839-192">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-192">Object</span></span>|  
|<span data-ttu-id="26839-193">authentication</span><span class="sxs-lookup"><span data-stu-id="26839-193">authentication</span></span>|<span data-ttu-id="26839-194">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-194">No</span></span>|<span data-ttu-id="26839-195">Представляет метод hello, который hello запроса должен пройти проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="26839-195">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="26839-196">Дополнительные сведения см. в статье [Исходящая проверка подлинности планировщика](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="26839-196">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="26839-197">Помимо планировщика, имеется еще одно поддерживаемое свойство: `authority`. По умолчанию его значение равно `https://login.windows.net`, если не указано другое. Также можно использовать другое значение, например `https://login.windows\-ppe.net`.</span><span class="sxs-lookup"><span data-stu-id="26839-197">Beyond scheduler, there is one more supported property: `authority` By default, this value is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|<span data-ttu-id="26839-198">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-198">Object</span></span>|  
  
<span data-ttu-id="26839-199">триггер Hello HTTP необходимо tooconform hello HTTP API с toowork конкретному шаблону в логике приложения.</span><span class="sxs-lookup"><span data-stu-id="26839-199">hello HTTP trigger requires hello HTTP API tooconform with a specific pattern toowork well with your logic app.</span></span> <span data-ttu-id="26839-200">Он требует hello следующие поля:</span><span class="sxs-lookup"><span data-stu-id="26839-200">It requires hello following fields:</span></span>  
  
|<span data-ttu-id="26839-201">Ответ</span><span class="sxs-lookup"><span data-stu-id="26839-201">Response</span></span>|<span data-ttu-id="26839-202">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-202">Description</span></span>|  
|------------|---------------|  
|<span data-ttu-id="26839-203">Код состояния</span><span class="sxs-lookup"><span data-stu-id="26839-203">Status code</span></span>|<span data-ttu-id="26839-204">Код состояния 200 \(ОК\) toocause запуска.</span><span class="sxs-lookup"><span data-stu-id="26839-204">Status code 200 \(OK\) toocause a run.</span></span> <span data-ttu-id="26839-205">Другие коды состояния не вызывают запуск.</span><span class="sxs-lookup"><span data-stu-id="26839-205">Any other status code doesn't cause a run.</span></span>|  
|<span data-ttu-id="26839-206">Заголовок Retry\-After</span><span class="sxs-lookup"><span data-stu-id="26839-206">Retry\-after header</span></span>|<span data-ttu-id="26839-207">Число секунд, пока приложение hello логику снова опрашивает hello конечной точки.</span><span class="sxs-lookup"><span data-stu-id="26839-207">Number of seconds until hello logic app polls hello endpoint again.</span></span>|  
|<span data-ttu-id="26839-208">Заголовок Location</span><span class="sxs-lookup"><span data-stu-id="26839-208">Location header</span></span>|<span data-ttu-id="26839-209">Hello toocall URL-адрес в следующем интервале опроса hello.</span><span class="sxs-lookup"><span data-stu-id="26839-209">hello URL toocall on hello next polling interval.</span></span> <span data-ttu-id="26839-210">Если не указан, используется hello исходный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="26839-210">If not specified, hello original URL is used.</span></span>|  
  
<span data-ttu-id="26839-211">Ниже приведены некоторые примеры различных поведений для различных типов запросов.</span><span class="sxs-lookup"><span data-stu-id="26839-211">Here are some examples of different behaviors for different types of requests:</span></span>  
  
|<span data-ttu-id="26839-212">Код ответа</span><span class="sxs-lookup"><span data-stu-id="26839-212">Response code</span></span>|<span data-ttu-id="26839-213">Retry\-After</span><span class="sxs-lookup"><span data-stu-id="26839-213">Retry\-After</span></span>|<span data-ttu-id="26839-214">Поведение</span><span class="sxs-lookup"><span data-stu-id="26839-214">Behavior</span></span>|  
|-----------------|----------------|------------|  
|<span data-ttu-id="26839-215">200</span><span class="sxs-lookup"><span data-stu-id="26839-215">200</span></span>|<span data-ttu-id="26839-216">\(Нет\)</span><span class="sxs-lookup"><span data-stu-id="26839-216">\(none\)</span></span>|<span data-ttu-id="26839-217">Не допустимый триггер, повторите попытку\-After используется engine требуется, в противном случае hello никогда не опрашивает hello следующего запроса.</span><span class="sxs-lookup"><span data-stu-id="26839-217">Not a valid trigger, Retry\-After is required, or else hello engine never polls for hello next request.</span></span>|  
|<span data-ttu-id="26839-218">202</span><span class="sxs-lookup"><span data-stu-id="26839-218">202</span></span>|<span data-ttu-id="26839-219">60</span><span class="sxs-lookup"><span data-stu-id="26839-219">60</span></span>|<span data-ttu-id="26839-220">Не вызывать hello рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="26839-220">Do not trigger hello workflow.</span></span> <span data-ttu-id="26839-221">Hello при следующей попытке происходит через одну минуту.</span><span class="sxs-lookup"><span data-stu-id="26839-221">hello next attempt happens in one minute.</span></span>|  
|<span data-ttu-id="26839-222">200</span><span class="sxs-lookup"><span data-stu-id="26839-222">200</span></span>|<span data-ttu-id="26839-223">10</span><span class="sxs-lookup"><span data-stu-id="26839-223">10</span></span>|<span data-ttu-id="26839-224">Запуск рабочего процесса hello и еще раз проверить больше содержимого в течение 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="26839-224">Run hello workflow, and check again for more content in 10 seconds.</span></span>|  
|<span data-ttu-id="26839-225">400</span><span class="sxs-lookup"><span data-stu-id="26839-225">400</span></span>|<span data-ttu-id="26839-226">\(Нет\)</span><span class="sxs-lookup"><span data-stu-id="26839-226">\(none\)</span></span>|<span data-ttu-id="26839-227">Ошибочный запрос, не запускайте hello рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="26839-227">Bad request, do not run hello workflow.</span></span> <span data-ttu-id="26839-228">При наличии не **политика повтора** определено, то используется политика по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="26839-228">If there is no **Retry Policy** defined, then hello default policy is used.</span></span> <span data-ttu-id="26839-229">После достижения hello число повторных попыток hello триггер больше не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="26839-229">After hello number of retries has been reached, hello trigger is no longer valid.</span></span>|  
|<span data-ttu-id="26839-230">500</span><span class="sxs-lookup"><span data-stu-id="26839-230">500</span></span>|<span data-ttu-id="26839-231">\(Нет\)</span><span class="sxs-lookup"><span data-stu-id="26839-231">\(none\)</span></span>|<span data-ttu-id="26839-232">Ошибка сервера, не запускайте hello рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="26839-232">Server error, do not run hello workflow.</span></span>  <span data-ttu-id="26839-233">При наличии не **политика повтора** определено, то используется политика по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="26839-233">If there is no **Retry Policy** defined, then hello default policy is used.</span></span> <span data-ttu-id="26839-234">После достижения hello число повторных попыток hello триггер больше не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="26839-234">After hello number of retries has been reached, hello trigger is no longer valid.</span></span>|  
  
<span data-ttu-id="26839-235">выходы Hello триггера HTTP будет выглядеть как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="26839-235">hello outputs of an HTTP trigger look like this example:</span></span>  
  
|<span data-ttu-id="26839-236">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="26839-236">Element name</span></span>|<span data-ttu-id="26839-237">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-237">Description</span></span>|<span data-ttu-id="26839-238">Тип</span><span class="sxs-lookup"><span data-stu-id="26839-238">Type</span></span>|  
|----------------|---------------|--------|  
|<span data-ttu-id="26839-239">headers</span><span class="sxs-lookup"><span data-stu-id="26839-239">headers</span></span>|<span data-ttu-id="26839-240">заголовки HTTP-ответа hello Hello.</span><span class="sxs-lookup"><span data-stu-id="26839-240">hello headers of hello http response.</span></span>|<span data-ttu-id="26839-241">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-241">Object</span></span>|  
|<span data-ttu-id="26839-242">текст</span><span class="sxs-lookup"><span data-stu-id="26839-242">body</span></span>|<span data-ttu-id="26839-243">текст Hello hello HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="26839-243">hello body of hello http response.</span></span>|<span data-ttu-id="26839-244">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-244">Object</span></span>|  
  
## <a name="api-connection-trigger"></a><span data-ttu-id="26839-245">Триггер подключения API</span><span class="sxs-lookup"><span data-stu-id="26839-245">API Connection trigger</span></span>  

<span data-ttu-id="26839-246">триггер подключения Hello API — аналогичные триггера toohello HTTP в своей функциональности.</span><span class="sxs-lookup"><span data-stu-id="26839-246">hello API connection trigger is similar toohello HTTP trigger in its basic functionality.</span></span> <span data-ttu-id="26839-247">Однако параметры hello для идентификации действия hello отличаются.</span><span class="sxs-lookup"><span data-stu-id="26839-247">However, hello parameters for identifying hello action are different.</span></span> <span data-ttu-id="26839-248">Пример:</span><span class="sxs-lookup"><span data-stu-id="26839-248">Here is an example:</span></span>  
  
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

|<span data-ttu-id="26839-249">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="26839-249">Element name</span></span>|<span data-ttu-id="26839-250">Обязательно</span><span class="sxs-lookup"><span data-stu-id="26839-250">Required</span></span>|<span data-ttu-id="26839-251">Тип</span><span class="sxs-lookup"><span data-stu-id="26839-251">Type</span></span>|<span data-ttu-id="26839-252">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-252">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="26839-253">host</span><span class="sxs-lookup"><span data-stu-id="26839-253">host</span></span>|<span data-ttu-id="26839-254">Да</span><span class="sxs-lookup"><span data-stu-id="26839-254">Yes</span></span>||<span data-ttu-id="26839-255">Hello ApiApp размещается шлюза и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="26839-255">hello ApiApp hosted gateway and id.</span></span>|  
|<span data-ttu-id="26839-256">метод</span><span class="sxs-lookup"><span data-stu-id="26839-256">method</span></span>|<span data-ttu-id="26839-257">Да</span><span class="sxs-lookup"><span data-stu-id="26839-257">Yes</span></span>|<span data-ttu-id="26839-258">Строка</span><span class="sxs-lookup"><span data-stu-id="26839-258">String</span></span>|<span data-ttu-id="26839-259">Может принимать одно из hello следующие методы HTTP: **получить**, **POST**, **ПОМЕСТИТЬ**, **удаление**, **PATCH**, или  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="26839-259">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="26839-260">Запросы</span><span class="sxs-lookup"><span data-stu-id="26839-260">queries</span></span>|<span data-ttu-id="26839-261">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-261">No</span></span>|<span data-ttu-id="26839-262">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-262">Object</span></span>|<span data-ttu-id="26839-263">Представляет hello запроса параметров toobe добавлен toohello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="26839-263">Represents hello query parameters toobe added toohello URL.</span></span> <span data-ttu-id="26839-264">Например `"queries" : { "api-version": "2015-02-01" }` добавляет `?api-version=2015-02-01` toohello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="26839-264">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="26839-265">headers</span><span class="sxs-lookup"><span data-stu-id="26839-265">headers</span></span>|<span data-ttu-id="26839-266">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-266">No</span></span>|<span data-ttu-id="26839-267">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-267">Object</span></span>|<span data-ttu-id="26839-268">Представляет каждый заголовков hello, отправляет запрос toohello.</span><span class="sxs-lookup"><span data-stu-id="26839-268">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="26839-269">Например tooset hello язык и тип запроса в:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="26839-269">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="26839-270">текст</span><span class="sxs-lookup"><span data-stu-id="26839-270">body</span></span>|<span data-ttu-id="26839-271">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-271">No</span></span>|<span data-ttu-id="26839-272">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-272">Object</span></span>|<span data-ttu-id="26839-273">Представляет полезные данные hello, отправляемое toohello конечной точки.</span><span class="sxs-lookup"><span data-stu-id="26839-273">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="26839-274">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="26839-274">retryPolicy</span></span>|<span data-ttu-id="26839-275">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-275">No</span></span>|<span data-ttu-id="26839-276">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-276">Object</span></span>|<span data-ttu-id="26839-277">Позволяет toocustomize характер повторения hello 4xx или 5xx ошибок.</span><span class="sxs-lookup"><span data-stu-id="26839-277">Allows you toocustomize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="26839-278">authentication</span><span class="sxs-lookup"><span data-stu-id="26839-278">authentication</span></span>|<span data-ttu-id="26839-279">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-279">No</span></span>|<span data-ttu-id="26839-280">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-280">Object</span></span>|<span data-ttu-id="26839-281">Представляет метод hello, который hello запроса должен пройти проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="26839-281">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="26839-282">Дополнительные сведения см. в статье [Исходящая проверка подлинности планировщика](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="26839-282">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication)</span></span>|  
  
<span data-ttu-id="26839-283">являются следующие свойства Hello для узла.</span><span class="sxs-lookup"><span data-stu-id="26839-283">hello properties for host are:</span></span>  
  
|<span data-ttu-id="26839-284">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="26839-284">Element name</span></span>|<span data-ttu-id="26839-285">Обязательно</span><span class="sxs-lookup"><span data-stu-id="26839-285">Required</span></span>|<span data-ttu-id="26839-286">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-286">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="26839-287">api runtimeUrl</span><span class="sxs-lookup"><span data-stu-id="26839-287">api runtimeUrl</span></span>|<span data-ttu-id="26839-288">Да</span><span class="sxs-lookup"><span data-stu-id="26839-288">Yes</span></span>|<span data-ttu-id="26839-289">Конечная точка Hello hello управляемый API.</span><span class="sxs-lookup"><span data-stu-id="26839-289">hello endpoint of hello managed API.</span></span>|  
|<span data-ttu-id="26839-290">connection name</span><span class="sxs-lookup"><span data-stu-id="26839-290">connection name</span></span>||<span data-ttu-id="26839-291">Должен быть вызван ссылочного параметра tooa `$connection` и hello имя подключения hello управляемых API, которое hello использует рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="26839-291">Must be a reference tooa parameter called `$connection` and is hello name of hello managed API connection that hello workflow uses.</span></span>|
  
<span data-ttu-id="26839-292">результаты Hello триггера API подключения являются:</span><span class="sxs-lookup"><span data-stu-id="26839-292">hello outputs of an API connection trigger are:</span></span>
  
|<span data-ttu-id="26839-293">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="26839-293">Element name</span></span>|<span data-ttu-id="26839-294">Тип</span><span class="sxs-lookup"><span data-stu-id="26839-294">Type</span></span>|<span data-ttu-id="26839-295">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-295">Description</span></span>|  
|----------------|--------|---------------|  
|<span data-ttu-id="26839-296">headers</span><span class="sxs-lookup"><span data-stu-id="26839-296">headers</span></span>|<span data-ttu-id="26839-297">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-297">Object</span></span>|<span data-ttu-id="26839-298">заголовки HTTP-ответа hello Hello.</span><span class="sxs-lookup"><span data-stu-id="26839-298">hello headers of hello http response.</span></span>|  
|<span data-ttu-id="26839-299">текст</span><span class="sxs-lookup"><span data-stu-id="26839-299">body</span></span>|<span data-ttu-id="26839-300">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-300">Object</span></span>|<span data-ttu-id="26839-301">текст Hello hello HTTP-ответа.</span><span class="sxs-lookup"><span data-stu-id="26839-301">hello body of hello http response.</span></span>|  
  
## <a name="httpwebhook-trigger"></a><span data-ttu-id="26839-302">Триггер httpWebhook</span><span class="sxs-lookup"><span data-stu-id="26839-302">HTTPWebhook trigger</span></span>  

<span data-ttu-id="26839-303">Hello HTTPWebhook триггер открывает конечную точку, аналогичные toohello триггер запуска вручную, но hello HTTPWebhook триггер также вызова tooa указан URL-адрес tooregister и отменять регистрацию.</span><span class="sxs-lookup"><span data-stu-id="26839-303">hello HTTPWebhook trigger opens an endpoint, similar toohello manual trigger, but hello HTTPWebhook trigger also calls out tooa specified URL tooregister and unregister.</span></span> <span data-ttu-id="26839-304">Триггер httpWebhook может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="26839-304">Here's an example of what an HTTPWebhook trigger might look like:</span></span>  

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

<span data-ttu-id="26839-305">Многие из этих разделов являются необязательными, и поведение hello hello веб-перехватчика зависит от того, какие разделы предоставленные или опущен.</span><span class="sxs-lookup"><span data-stu-id="26839-305">Many of these sections are optional, and hello behavior of hello Webhook depends on which sections are provided or omitted.</span></span>  
<span data-ttu-id="26839-306">свойства веб-перехватчика Hello выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="26839-306">hello properties of a Webhook are as follows:</span></span>  
  
|<span data-ttu-id="26839-307">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="26839-307">Element name</span></span>|<span data-ttu-id="26839-308">Обязательно</span><span class="sxs-lookup"><span data-stu-id="26839-308">Required</span></span>|<span data-ttu-id="26839-309">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-309">Description</span></span>|  
|----------------|------------|---------------|  
|<span data-ttu-id="26839-310">subscribe</span><span class="sxs-lookup"><span data-stu-id="26839-310">subscribe</span></span>|<span data-ttu-id="26839-311">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-311">No</span></span>|<span data-ttu-id="26839-312">Здравствуйте, исходящий запрос, который вызывается, когда триггер hello создается и выполняет hello первоначальной регистрации.</span><span class="sxs-lookup"><span data-stu-id="26839-312">hello outgoing request that is called when hello trigger is created and performs hello initial registration.</span></span>|  
|<span data-ttu-id="26839-313">unsubscribe</span><span class="sxs-lookup"><span data-stu-id="26839-313">unsubscribe</span></span>|<span data-ttu-id="26839-314">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-314">No</span></span>|<span data-ttu-id="26839-315">Здравствуйте, исходящего сообщения запроса, при удалении триггера hello.</span><span class="sxs-lookup"><span data-stu-id="26839-315">hello outgoing request when hello trigger is deleted.</span></span>|  
  
-   <span data-ttu-id="26839-316">**Подписка** hello исходящего вызова, от которого поступил прослушивания tooevents toostart.</span><span class="sxs-lookup"><span data-stu-id="26839-316">**Subscribe** is hello outgoing call that's made toostart listening tooevents.</span></span> <span data-ttu-id="26839-317">Этот вызов начинается с hello выполните одинаковый набор параметров, которые hello обычные действия HTTP.</span><span class="sxs-lookup"><span data-stu-id="26839-317">This call starts with hello same set of parameters that hello normal HTTP actions do.</span></span> <span data-ttu-id="26839-318">Исходящих вызове любой hello время изменения рабочего процесса каким-либо образом, например, каждый раз, когда учетные данные hello учитываются или триггер hello входных параметров изменений.</span><span class="sxs-lookup"><span data-stu-id="26839-318">This outgoing call is made any time hello workflow changes in any way, for example, whenever hello credentials are rolled, or hello trigger's input parameters change.</span></span>
  
    <span data-ttu-id="26839-319">toosupport этот вызов, новые функции: `@listCallbackUrl()`.</span><span class="sxs-lookup"><span data-stu-id="26839-319">toosupport this call, there is a new function: `@listCallbackUrl()`.</span></span> <span data-ttu-id="26839-320">Эта функция возвращает уникальный URL-адрес для конкретного триггера в этом рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="26839-320">This function returns a unique URL for this specific trigger in this workflow.</span></span> <span data-ttu-id="26839-321">Он представляет уникальный идентификатор hello hello конечные точки, использующие hello службы REST.</span><span class="sxs-lookup"><span data-stu-id="26839-321">It represents hello unique identifier for hello endpoints that use hello Service REST.</span></span>  
  
-   <span data-ttu-id="26839-322">**unsubscribe** вызывается, когда операция делает этот триггер недействительным, например в результате таких действий:</span><span class="sxs-lookup"><span data-stu-id="26839-322">**Unsubscribe** is called when an operation renders this trigger invalid, including:</span></span>  
  
    -   <span data-ttu-id="26839-323">Удаление или отключение триггера hello</span><span class="sxs-lookup"><span data-stu-id="26839-323">Deleting or disabling hello trigger</span></span>  
  
    -   <span data-ttu-id="26839-324">Удаление или отключение hello рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="26839-324">Deleting or disabling hello workflow</span></span>  
  
    -   <span data-ttu-id="26839-325">Удаление или отключение подписки hello</span><span class="sxs-lookup"><span data-stu-id="26839-325">Deleting or disabling hello subscription</span></span>  
  
    <span data-ttu-id="26839-326">приложения логики Hello автоматически вызывает hello действие отмены подписки.</span><span class="sxs-lookup"><span data-stu-id="26839-326">hello logic app automatically calls hello unsubscribe action.</span></span> <span data-ttu-id="26839-327">Параметры Hello, функция toothis hello таким же как триггер hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="26839-327">hello parameters toothis function are hello same as hello HTTP trigger.</span></span>  
  
    <span data-ttu-id="26839-328">Hello выходы триггера HTTPWebhook hello представляют Привет содержимое hello входящего запроса:</span><span class="sxs-lookup"><span data-stu-id="26839-328">hello outputs of hello HTTPWebhook trigger are hello contents of hello incoming request:</span></span>  
  
|<span data-ttu-id="26839-329">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="26839-329">Element name</span></span>|<span data-ttu-id="26839-330">Тип</span><span class="sxs-lookup"><span data-stu-id="26839-330">Type</span></span>|<span data-ttu-id="26839-331">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-331">Description</span></span>|  
|-----------------|--------|---------------|  
|<span data-ttu-id="26839-332">headers</span><span class="sxs-lookup"><span data-stu-id="26839-332">headers</span></span>|<span data-ttu-id="26839-333">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-333">Object</span></span>|<span data-ttu-id="26839-334">заголовки Hello hello HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="26839-334">hello headers of hello http request.</span></span>|  
|<span data-ttu-id="26839-335">текст</span><span class="sxs-lookup"><span data-stu-id="26839-335">body</span></span>|<span data-ttu-id="26839-336">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-336">Object</span></span>|<span data-ttu-id="26839-337">текст Hello hello HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="26839-337">hello body of hello http request.</span></span>|  

<span data-ttu-id="26839-338">Ограничения на действия веб-перехватчик может быть указано в hello так же, как [ограничения асинхронный HTTP](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="26839-338">Limits on a webhook action can be specified in hello same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  

## <a name="conditions"></a><span data-ttu-id="26839-339">Условия</span><span class="sxs-lookup"><span data-stu-id="26839-339">Conditions</span></span>  

<span data-ttu-id="26839-340">Для любого триггера можно использовать один или несколько условий toodetermine ли должен выполняться рабочий процесс hello, или нет.</span><span class="sxs-lookup"><span data-stu-id="26839-340">For any trigger, you can use one or more conditions toodetermine whether hello workflow should run or not.</span></span> <span data-ttu-id="26839-341">Например:</span><span class="sxs-lookup"><span data-stu-id="26839-341">For example:</span></span>  

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

<span data-ttu-id="26839-342">В этом случае hello только триггеры отчета во время рабочего процесса hello `sendReports` параметр имеет значение tootrue.</span><span class="sxs-lookup"><span data-stu-id="26839-342">In this case, hello report only triggers while hello workflow's `sendReports` parameter is set tootrue.</span></span> <span data-ttu-id="26839-343">Наконец условий может ссылаться на код состояния hello hello триггера.</span><span class="sxs-lookup"><span data-stu-id="26839-343">Finally, conditions may reference hello status code of hello trigger.</span></span> <span data-ttu-id="26839-344">Например, можно настроить так, чтобы рабочий процесс запускался только в том случае, если веб-сайт возвращает код состояния 500:</span><span class="sxs-lookup"><span data-stu-id="26839-344">For example, you could kick off a workflow only when your website returns a status code 500, as follows:</span></span>
  
```  
"conditions": [  
        {  
          "expression": "@equals(triggers().code, 'InternalServerError')"  
        }  
      ]  
```  
  
> [!NOTE]  
> <span data-ttu-id="26839-345">Когда любое выражение ссылается на код состояния hello триггера hello \(каким-либо образом\), поведение по умолчанию hello \(триггер только на 200 \(ОК\) \) заменяется.</span><span class="sxs-lookup"><span data-stu-id="26839-345">When any expression references hello status code of hello trigger \(in any way\), hello default behavior \(trigger only on 200 \(OK\)\) is replaced.</span></span> <span data-ttu-id="26839-346">Например, если требуется tootrigger на код состояния 200 и код состояния 201 имеется tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` как условие.</span><span class="sxs-lookup"><span data-stu-id="26839-346">For example, if you want tootrigger on both status code 200 and status code 201, you have tooinclude: `@or(equals(triggers().code, 200),equals(triggers().code,201))` as your condition.</span></span>  
  
## <a name="start-multiple-runs-for-a-request"></a><span data-ttu-id="26839-347">Запуск нескольких выполнений запроса</span><span class="sxs-lookup"><span data-stu-id="26839-347">Start multiple runs for a request</span></span>

<span data-ttu-id="26839-348">tookick отключение нескольких тестовых запусков для отдельного запроса `splitOn` может быть полезным, например, при необходимости toopoll конечную точку, которая может иметь несколько новых элементов между интервалами опроса.</span><span class="sxs-lookup"><span data-stu-id="26839-348">tookick off multiple runs for a single request, `splitOn` is useful, for example, when you want toopoll an endpoint that can have multiple new items between polling intervals.</span></span>
  
<span data-ttu-id="26839-349">С `splitOn`, можно указать свойство hello внутри hello полезные данные ответа, содержащий hello массив элементов, каждый из которых требуется toouse toostart выполнения триггера hello.</span><span class="sxs-lookup"><span data-stu-id="26839-349">With `splitOn`, you specify hello property inside hello response payload that contains hello array of items, each of which you want toouse toostart a run of hello trigger.</span></span> <span data-ttu-id="26839-350">Например предположим, что у вас есть API, который возвращает hello следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="26839-350">For example, imagine you have an API that returns hello following response:</span></span>  
  
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
  
<span data-ttu-id="26839-351">Логика приложения требуется только содержимое строк hello, можно создать триггер как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="26839-351">Your logic app only needs hello Rows content, so you can construct your trigger like this example:</span></span>  
  
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
  
<span data-ttu-id="26839-352">Затем в hello определения рабочего процесса, `@triggerBody().name` возвращает `mycoolrow` для первого запуска hello и `another row` hello второго тестового запуска.</span><span class="sxs-lookup"><span data-stu-id="26839-352">Then, in hello workflow definition, `@triggerBody().name` returns `mycoolrow` for hello first run, and `another row` for hello second run.</span></span> <span data-ttu-id="26839-353">Hello вид триггера выходные данные как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="26839-353">hello trigger outputs look like this example:</span></span>  
  
```json
{
    "body" : {
        "id" : 938109381,
        "name" : "another row"
    }
}
```

<span data-ttu-id="26839-354">Таким образом, если вы используете `SplitOn`, не удалось получить свойства hello, которые находятся за пределами массива hello в этом случае hello `Status` поля.</span><span class="sxs-lookup"><span data-stu-id="26839-354">So if you use `SplitOn`, you can't get hello properties that are outside hello array, in this case, hello `Status` field.</span></span>  
  
> [!NOTE]  
> <span data-ttu-id="26839-355">В этом примере мы используем hello `?` tooavoid сбой, если hello может toobe оператор `Rows` свойство отсутствует.</span><span class="sxs-lookup"><span data-stu-id="26839-355">In this example, we use hello `?` operator toobe able tooavoid a failure if hello `Rows` property is not present.</span></span> 
  
## <a name="single-run-instance"></a><span data-ttu-id="26839-356">Экземпляр однократного выполнения</span><span class="sxs-lookup"><span data-stu-id="26839-356">Single run instance</span></span>

<span data-ttu-id="26839-357">Вы можете настроить триггеры, если завершены все активные запуски пожар tooonly свойство повторения.</span><span class="sxs-lookup"><span data-stu-id="26839-357">You can configure triggers that have a recurrence property tooonly fire if all active runs have completed.</span></span> <span data-ttu-id="26839-358">В случае запланированного повторения при выполняющегося теста триггер hello пропускает и ждет, пока hello Далее повторения запланированного интервала toocheck еще раз.</span><span class="sxs-lookup"><span data-stu-id="26839-358">If a scheduled recurrence occurs while there is an in-progress run, hello trigger skips and waits until hello next scheduled recurrence interval toocheck again.</span></span>

<span data-ttu-id="26839-359">Этот параметр через параметры hello операции:</span><span class="sxs-lookup"><span data-stu-id="26839-359">You can configure this setting through hello operation options:</span></span>

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

## <a name="types-and-inputs"></a><span data-ttu-id="26839-360">Типы и входные данные</span><span class="sxs-lookup"><span data-stu-id="26839-360">Types and inputs</span></span>  

<span data-ttu-id="26839-361">Существует много типов действий, каждое из которых имеет уникальное поведение.</span><span class="sxs-lookup"><span data-stu-id="26839-361">There are many types of actions, each with unique behavior.</span></span> <span data-ttu-id="26839-362">Действия коллекций могут содержать множество вложенных действий.</span><span class="sxs-lookup"><span data-stu-id="26839-362">Collection actions may contain many other actions within itself.</span></span>

### <a name="standard-actions"></a><span data-ttu-id="26839-363">Стандартные действия</span><span class="sxs-lookup"><span data-stu-id="26839-363">Standard actions</span></span>  

-   <span data-ttu-id="26839-364">**http** — это действие вызывает конечную веб-точку HTTP.</span><span class="sxs-lookup"><span data-stu-id="26839-364">**HTTP** This action calls an HTTP web endpoint.</span></span>  
  
-   <span data-ttu-id="26839-365">**ApiConnection** \- это действие ведет себя как hello действия HTTP, но использует hello API-интерфейсы, управляемая корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="26839-365">**ApiConnection** \- This action behaves like hello HTTP action, but uses hello Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="26839-366">**ApiConnectionWebhook** \- как HTTPWebhook, но hello использует API-интерфейсы, управляемая корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="26839-366">**ApiConnectionWebhook** \- Like HTTPWebhook, but uses hello Microsoft-managed APIs.</span></span>  
  
-   <span data-ttu-id="26839-367">**response** — это действие определяет ответ для входящего вызова.</span><span class="sxs-lookup"><span data-stu-id="26839-367">**Response** \- This action defines a response for an incoming call.</span></span>  
  
-   <span data-ttu-id="26839-368">**wait** — это простое действие ожидает фиксированное количество времени или до определенного времени.</span><span class="sxs-lookup"><span data-stu-id="26839-368">**Wait** \- This simple action waits a fixed amount of time or until a specific time.</span></span>  
  
-   <span data-ttu-id="26839-369">**workflow** — это действие представляет вложенный рабочий процесс.</span><span class="sxs-lookup"><span data-stu-id="26839-369">**Workflow** \- This action represents a nested workflow.</span></span>  

-   <span data-ttu-id="26839-370">**Function** \- — это действие представляет функцию Azure.</span><span class="sxs-lookup"><span data-stu-id="26839-370">**Function** \- This action represents an Azure Function.</span></span>

### <a name="collection-actions"></a><span data-ttu-id="26839-371">Действия коллекций</span><span class="sxs-lookup"><span data-stu-id="26839-371">Collection actions</span></span>

-   <span data-ttu-id="26839-372">**scope** — это действие является логическим объединением других действий.</span><span class="sxs-lookup"><span data-stu-id="26839-372">**Scope** \- This action is a logical grouping of other actions.</span></span>

-   <span data-ttu-id="26839-373">**Условие** \- это действие, вычисляет выражение и выполняет соответствующую ветвь результат hello.</span><span class="sxs-lookup"><span data-stu-id="26839-373">**Condition** \- This action evaluates an expression and executes hello corresponding result branch.</span></span>

-   <span data-ttu-id="26839-374">**foreach** — это циклическое действие выполняет итерацию по массиву и внутренние действия для каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="26839-374">**ForEach** \- This looping action iterates through an array and performs inner actions for each item.</span></span>

-   <span data-ttu-id="26839-375">**Пока** \- этого цикла действия выполняет внутреннее действий, пока условие приводит tootrue.</span><span class="sxs-lookup"><span data-stu-id="26839-375">**Until** \- This looping action executes inner actions until a condition results tootrue.</span></span>
  
<span data-ttu-id="26839-376">Каждый тип действия имеет разный набор **входных данных**, определяющих его поведение.</span><span class="sxs-lookup"><span data-stu-id="26839-376">Each type of action has a different set of **inputs** that define an action's behavior.</span></span>  
  
## <a name="http-action"></a><span data-ttu-id="26839-377">Действие HTTP</span><span class="sxs-lookup"><span data-stu-id="26839-377">HTTP action</span></span>  

<span data-ttu-id="26839-378">Действия HTTP вызова заданной конечной точки и проверьте наличие toodetermine hello ответ должен выполняться рабочий процесс hello.</span><span class="sxs-lookup"><span data-stu-id="26839-378">HTTP actions call a specified endpoint and check hello response toodetermine whether hello workflow should run.</span></span> <span data-ttu-id="26839-379">Hello **входов** объект принимает набор hello вызовов hello HTTP tooconstruct необходимые параметры:</span><span class="sxs-lookup"><span data-stu-id="26839-379">hello **inputs** object takes hello set of parameters required tooconstruct hello HTTP call:</span></span>  
  
|<span data-ttu-id="26839-380">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="26839-380">Element name</span></span>|<span data-ttu-id="26839-381">Обязательно</span><span class="sxs-lookup"><span data-stu-id="26839-381">Required</span></span>|<span data-ttu-id="26839-382">Тип</span><span class="sxs-lookup"><span data-stu-id="26839-382">Type</span></span>|<span data-ttu-id="26839-383">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-383">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="26839-384">метод</span><span class="sxs-lookup"><span data-stu-id="26839-384">method</span></span>|<span data-ttu-id="26839-385">Да</span><span class="sxs-lookup"><span data-stu-id="26839-385">Yes</span></span>|<span data-ttu-id="26839-386">Строка</span><span class="sxs-lookup"><span data-stu-id="26839-386">String</span></span>|<span data-ttu-id="26839-387">Может принимать одно из hello следующие методы HTTP: **получить**, **POST**, **ПОМЕСТИТЬ**, **удаление**, **PATCH**, или  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="26839-387">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="26839-388">uri</span><span class="sxs-lookup"><span data-stu-id="26839-388">uri</span></span>|<span data-ttu-id="26839-389">Да</span><span class="sxs-lookup"><span data-stu-id="26839-389">Yes</span></span>|<span data-ttu-id="26839-390">Строка</span><span class="sxs-lookup"><span data-stu-id="26839-390">String</span></span>|<span data-ttu-id="26839-391">Здравствуйте, конечная точка http или https, вызывается.</span><span class="sxs-lookup"><span data-stu-id="26839-391">hello http or https endpoint that is called.</span></span> <span data-ttu-id="26839-392">Не более 2 КБ.</span><span class="sxs-lookup"><span data-stu-id="26839-392">Maximum length is 2 kilobytes.</span></span>|  
|<span data-ttu-id="26839-393">Запросы</span><span class="sxs-lookup"><span data-stu-id="26839-393">queries</span></span>|<span data-ttu-id="26839-394">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-394">No</span></span>|<span data-ttu-id="26839-395">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-395">Object</span></span>|<span data-ttu-id="26839-396">Представляет URL-адрес hello запроса параметров tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="26839-396">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="26839-397">Например `"queries" : { "api-version": "2015-02-01" }` добавляет `?api-version=2015-02-01` toohello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="26839-397">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="26839-398">headers</span><span class="sxs-lookup"><span data-stu-id="26839-398">headers</span></span>|<span data-ttu-id="26839-399">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-399">No</span></span>|<span data-ttu-id="26839-400">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-400">Object</span></span>|<span data-ttu-id="26839-401">Представляет каждый заголовков hello, отправляет запрос toohello.</span><span class="sxs-lookup"><span data-stu-id="26839-401">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="26839-402">Например tooset hello язык и тип запроса в:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="26839-402">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="26839-403">текст</span><span class="sxs-lookup"><span data-stu-id="26839-403">body</span></span>|<span data-ttu-id="26839-404">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-404">No</span></span>|<span data-ttu-id="26839-405">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-405">Object</span></span>|<span data-ttu-id="26839-406">Представляет полезные данные hello, отправляемое toohello конечной точки.</span><span class="sxs-lookup"><span data-stu-id="26839-406">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="26839-407">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="26839-407">retryPolicy</span></span>|<span data-ttu-id="26839-408">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-408">No</span></span>|<span data-ttu-id="26839-409">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-409">Object</span></span>|<span data-ttu-id="26839-410">Позволяет настраивать поведение повтора hello 4xx или 5xx ошибок.</span><span class="sxs-lookup"><span data-stu-id="26839-410">Lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="26839-411">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="26839-411">operationsOptions</span></span>|<span data-ttu-id="26839-412">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-412">No</span></span>|<span data-ttu-id="26839-413">Строка</span><span class="sxs-lookup"><span data-stu-id="26839-413">String</span></span>|<span data-ttu-id="26839-414">Определяет набор hello toooverride специальные поведения.</span><span class="sxs-lookup"><span data-stu-id="26839-414">Defines hello set of special behaviors toooverride.</span></span>|  
|<span data-ttu-id="26839-415">authentication</span><span class="sxs-lookup"><span data-stu-id="26839-415">authentication</span></span>|<span data-ttu-id="26839-416">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-416">No</span></span>|<span data-ttu-id="26839-417">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-417">Object</span></span>|<span data-ttu-id="26839-418">Представляет метод hello, который hello запроса должен пройти проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="26839-418">Represents hello method that hello request should be authenticated.</span></span> <span data-ttu-id="26839-419">Дополнительные сведения см. в статье [Исходящая проверка подлинности планировщика](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span><span class="sxs-lookup"><span data-stu-id="26839-419">For details on this object, see [Scheduler Outbound Authentication](https://docs.microsoft.com/azure/scheduler/scheduler-outbound-authentication).</span></span> <span data-ttu-id="26839-420">Помимо планировщика, имеется еще одно поддерживаемое свойство: `authority`.</span><span class="sxs-lookup"><span data-stu-id="26839-420">Beyond scheduler, there is one more supported property: `authority`.</span></span> <span data-ttu-id="26839-421">По умолчанию его значение равно `https://login.windows.net`, если не указано другое. Также можно использовать другое значение, например `https://login.windows\-ppe.net`.</span><span class="sxs-lookup"><span data-stu-id="26839-421">By default, this is `https://login.windows.net` when not specified, but you can use a different audience like `https://login.windows\-ppe.net`</span></span>|  
  
<span data-ttu-id="26839-422">Действия HTTP и \(действия API подключения\) поддерживают политики повтора.</span><span class="sxs-lookup"><span data-stu-id="26839-422">HTTP actions \(and API Connection\) actions support retry policies.</span></span> <span data-ttu-id="26839-423">Политику повтора применяет toointermittent сбои, характеризуется как код состояния HTTP коды 408 429 и 5xx в исключения при подключении tooany сложения.</span><span class="sxs-lookup"><span data-stu-id="26839-423">A retry policy applies toointermittent failures, characterized as HTTP status codes 408, 429, and 5xx, in addition tooany connectivity exceptions.</span></span> <span data-ttu-id="26839-424">Эта политика описываются с помощью hello *retryPolicy* объекта, определенного как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="26839-424">This policy is described using hello *retryPolicy* object defined as shown here:</span></span>
  
```json
"retryPolicy" : {
    "type": "<type-of-retry-policy>",
    "interval": <retry-interval>,
    "count": <number-of-retry-attempts>
}
```
  
<span data-ttu-id="26839-425">Интервал повтора Hello указывается в формате ISO 8601 hello.</span><span class="sxs-lookup"><span data-stu-id="26839-425">hello retry interval is specified in hello ISO 8601 format.</span></span> <span data-ttu-id="26839-426">Этот интервал имеет по умолчанию и минимальное значение 20 секунд, а hello максимальное значение составляет один час.</span><span class="sxs-lookup"><span data-stu-id="26839-426">This interval has a default and minimum value of 20 seconds, while hello maximum value is one hour.</span></span> <span data-ttu-id="26839-427">Hello по умолчанию и максимальное число повторных попыток составляет четыре часа.</span><span class="sxs-lookup"><span data-stu-id="26839-427">hello default and maximum retry count is four hours.</span></span> <span data-ttu-id="26839-428">Если не указано определение политики "Повторить" hello, `fixed` стратегия используется со значениями счетчика и интервала повторных попыток по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="26839-428">If hello retry policy definition is not specified, a `fixed` strategy is used with default retry count and interval values.</span></span> <span data-ttu-id="26839-429">политика повтора toodisable hello, задайте для него тип слишком`None`.</span><span class="sxs-lookup"><span data-stu-id="26839-429">toodisable hello retry policy, set its type too`None`.</span></span>  
  
<span data-ttu-id="26839-430">Например hello следующее действие повторных попыток извлечение последние новости hello два раза, если временной ошибкой для всех трех выполнений, с 30-секундная задержка между попытками:</span><span class="sxs-lookup"><span data-stu-id="26839-430">For example, hello following action retries fetching hello latest news two times, if there are intermittent failures, for a total of three executions, with a 30-second delay between each attempt:</span></span>  
  
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
### <a name="asynchronous-patterns"></a><span data-ttu-id="26839-431">Модель асинхронных операций</span><span class="sxs-lookup"><span data-stu-id="26839-431">Asynchronous patterns</span></span>

<span data-ttu-id="26839-432">По умолчанию все действия на основе HTTP поддерживают hello шаблон Стандартная асинхронной операции.</span><span class="sxs-lookup"><span data-stu-id="26839-432">By default, all HTTP-based actions support hello standard asynchronous operation pattern.</span></span> <span data-ttu-id="26839-433">Поэтому если удаленный сервер hello указывает этот запрос hello принимается для обработки с 202 \(принято\) ответа, hello Logic Apps ядра отслеживает опроса hello URL-адрес, указанный в заголовок расположения hello ответа до достижения терминала состояние \(не является\-ответа 202\).</span><span class="sxs-lookup"><span data-stu-id="26839-433">So if hello remote server indicates that hello request is accepted for processing with a 202 \(Accepted\) response, hello Logic Apps engine keeps polling hello URL specified in hello response's location header until reaching a terminal state \(a non\-202 response\).</span></span>  
  
<span data-ttu-id="26839-434">toodisable hello работы в асинхронном режиме описанные, заданные ранее `DisableAsyncPattern` параметр во входных параметрах действие hello.</span><span class="sxs-lookup"><span data-stu-id="26839-434">toodisable hello asynchronous behavior previously described, set a `DisableAsyncPattern` option in hello action inputs.</span></span> <span data-ttu-id="26839-435">В этом случае hello выходные данные действия hello зависит от первоначального hello 202 ответа от сервера hello.</span><span class="sxs-lookup"><span data-stu-id="26839-435">In this case, hello output of hello action is based on hello initial 202 response from hello server.</span></span>  
  
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

#### <a name="asynchronous-limits"></a><span data-ttu-id="26839-436">Ограничения асинхронных операций</span><span class="sxs-lookup"><span data-stu-id="26839-436">Asynchronous Limits</span></span>

<span data-ttu-id="26839-437">Асинхронная модель может быть ограничена его длительность tooa определенного интервала времени.</span><span class="sxs-lookup"><span data-stu-id="26839-437">An asynchronous pattern can be limited in its duration tooa specific time interval.</span></span>  <span data-ttu-id="26839-438">Если hello прошествии времени без достижения конечного состояния, помечается состояние hello действие hello `Cancelled` с кодом `ActionTimedOut`.</span><span class="sxs-lookup"><span data-stu-id="26839-438">If hello time interval elapses without reaching a terminal state, hello status of hello action will be marked `Cancelled` with a code of `ActionTimedOut`.</span></span>  <span data-ttu-id="26839-439">время ожидания Hello предел задается в формате ISO 8601.</span><span class="sxs-lookup"><span data-stu-id="26839-439">hello limit timeout is specified in ISO 8601 format.</span></span>  <span data-ttu-id="26839-440">Ограничения могут быть заданы с hello, используя синтаксис:</span><span class="sxs-lookup"><span data-stu-id="26839-440">Limits can be specified with hello following syntax:</span></span>

``` json
"<action-name>": {
    "type": "workflow|webhook|http|apiconnectionwebhook|apiconnection",
    "inputs": { },
    "limit": {
        "timeout": "PT10S"
    }
}
```
  
## <a name="api-connection"></a><span data-ttu-id="26839-441">API подключения</span><span class="sxs-lookup"><span data-stu-id="26839-441">API Connection</span></span>  

<span data-ttu-id="26839-442">API подключения — это действие, которое ссылается на соединитель, управляемый Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="26839-442">API Connection is an action that references a Microsoft-managed connector.</span></span>
<span data-ttu-id="26839-443">Это действие требует допустимое соединение tooa ссылки и сведения об hello API и параметров, необходимых.</span><span class="sxs-lookup"><span data-stu-id="26839-443">This action requires a reference tooa valid connection, and information on hello API and parameters required.</span></span>

|<span data-ttu-id="26839-444">Имя элемента</span><span class="sxs-lookup"><span data-stu-id="26839-444">Element name</span></span>|<span data-ttu-id="26839-445">Обязательно</span><span class="sxs-lookup"><span data-stu-id="26839-445">Required</span></span>|<span data-ttu-id="26839-446">Тип</span><span class="sxs-lookup"><span data-stu-id="26839-446">Type</span></span>|<span data-ttu-id="26839-447">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-447">Description</span></span>|  
|----------------|------------|--------|---------------|  
|<span data-ttu-id="26839-448">host</span><span class="sxs-lookup"><span data-stu-id="26839-448">host</span></span>|<span data-ttu-id="26839-449">Да</span><span class="sxs-lookup"><span data-stu-id="26839-449">Yes</span></span>|<span data-ttu-id="26839-450">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-450">Object</span></span>|<span data-ttu-id="26839-451">Представляет hello соединителя сведения, такие как hello runtimeUrl и ссылка toohello объект подключения</span><span class="sxs-lookup"><span data-stu-id="26839-451">Represents hello connector information such as hello runtimeUrl and reference toohello connection object</span></span>|
|<span data-ttu-id="26839-452">метод</span><span class="sxs-lookup"><span data-stu-id="26839-452">method</span></span>|<span data-ttu-id="26839-453">Да</span><span class="sxs-lookup"><span data-stu-id="26839-453">Yes</span></span>|<span data-ttu-id="26839-454">Строка</span><span class="sxs-lookup"><span data-stu-id="26839-454">String</span></span>|<span data-ttu-id="26839-455">Может принимать одно из hello следующие методы HTTP: **получить**, **POST**, **ПОМЕСТИТЬ**, **удаление**, **PATCH**, или  **HEAD**</span><span class="sxs-lookup"><span data-stu-id="26839-455">Can be one of hello following HTTP methods: **GET**, **POST**, **PUT**, **DELETE**, **PATCH**, or **HEAD**</span></span>|  
|<span data-ttu-id="26839-456">path</span><span class="sxs-lookup"><span data-stu-id="26839-456">path</span></span>|<span data-ttu-id="26839-457">Да</span><span class="sxs-lookup"><span data-stu-id="26839-457">Yes</span></span>|<span data-ttu-id="26839-458">Строка</span><span class="sxs-lookup"><span data-stu-id="26839-458">String</span></span>|<span data-ttu-id="26839-459">путь Hello hello API-операции.</span><span class="sxs-lookup"><span data-stu-id="26839-459">hello path of hello API operation.</span></span>|  
|<span data-ttu-id="26839-460">Запросы</span><span class="sxs-lookup"><span data-stu-id="26839-460">queries</span></span>|<span data-ttu-id="26839-461">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-461">No</span></span>|<span data-ttu-id="26839-462">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-462">Object</span></span>|<span data-ttu-id="26839-463">Представляет URL-адрес hello запроса параметров tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="26839-463">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="26839-464">Например `"queries" : { "api-version": "2015-02-01" }` добавляет `?api-version=2015-02-01` toohello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="26839-464">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="26839-465">headers</span><span class="sxs-lookup"><span data-stu-id="26839-465">headers</span></span>|<span data-ttu-id="26839-466">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-466">No</span></span>|<span data-ttu-id="26839-467">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-467">Object</span></span>|<span data-ttu-id="26839-468">Представляет каждый заголовков hello, отправляет запрос toohello.</span><span class="sxs-lookup"><span data-stu-id="26839-468">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="26839-469">Например tooset hello язык и тип запроса в:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="26839-469">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="26839-470">текст</span><span class="sxs-lookup"><span data-stu-id="26839-470">body</span></span>|<span data-ttu-id="26839-471">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-471">No</span></span>|<span data-ttu-id="26839-472">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-472">Object</span></span>|<span data-ttu-id="26839-473">Представляет полезные данные hello, отправляемое toohello конечной точки.</span><span class="sxs-lookup"><span data-stu-id="26839-473">Represents hello payload that is sent toohello endpoint.</span></span>|  
|<span data-ttu-id="26839-474">retryPolicy</span><span class="sxs-lookup"><span data-stu-id="26839-474">retryPolicy</span></span>|<span data-ttu-id="26839-475">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-475">No</span></span>|<span data-ttu-id="26839-476">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-476">Object</span></span>|<span data-ttu-id="26839-477">Позволяет настраивать поведение повтора hello 4xx или 5xx ошибок.</span><span class="sxs-lookup"><span data-stu-id="26839-477">Lets you customize hello retry behavior for 4xx or 5xx errors.</span></span>|  
|<span data-ttu-id="26839-478">operationsOptions</span><span class="sxs-lookup"><span data-stu-id="26839-478">operationsOptions</span></span>|<span data-ttu-id="26839-479">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-479">No</span></span>|<span data-ttu-id="26839-480">Строка</span><span class="sxs-lookup"><span data-stu-id="26839-480">String</span></span>|<span data-ttu-id="26839-481">Определяет набор hello toooverride специальные поведения.</span><span class="sxs-lookup"><span data-stu-id="26839-481">Defines hello set of special behaviors toooverride.</span></span>|  

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

## <a name="api-connection-webhook-action"></a><span data-ttu-id="26839-482">Действие webhook API подключения</span><span class="sxs-lookup"><span data-stu-id="26839-482">API Connection webhook action</span></span>

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

<span data-ttu-id="26839-483">Ограничения на действия веб-перехватчик может быть указано в hello так же, как [ограничения асинхронный HTTP](#asynchronous-limits).</span><span class="sxs-lookup"><span data-stu-id="26839-483">Limits on a webhook action can be specified in hello same manner as [HTTP Asynchronous Limits](#asynchronous-limits).</span></span>
  
## <a name="response-action"></a><span data-ttu-id="26839-484">Действие ответа</span><span class="sxs-lookup"><span data-stu-id="26839-484">Response action</span></span>  

<span data-ttu-id="26839-485">Этот тип действия содержит полезные данные ответа hello из HTTP-запроса и включает statusCode, тело и заголовки:</span><span class="sxs-lookup"><span data-stu-id="26839-485">This action type contains hello entire response payload from an HTTP request and includes a statusCode, body, and headers:</span></span>  
  
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
  
<span data-ttu-id="26839-486">Hello ответное действие имеет специальные ограничения, которые неприменимы tooother действия.</span><span class="sxs-lookup"><span data-stu-id="26839-486">hello response action has special restrictions that don't apply tooother actions.</span></span> <span data-ttu-id="26839-487">В частности:</span><span class="sxs-lookup"><span data-stu-id="26839-487">Specifically:</span></span>  
  
-   <span data-ttu-id="26839-488">Ответные меры не может быть параллельной в определении, поскольку toohello входящего запроса детерминированным ответа является обязательным.</span><span class="sxs-lookup"><span data-stu-id="26839-488">Response actions cannot be parallel in a definition because a deterministic response toohello incoming request is required.</span></span>  
  
-   <span data-ttu-id="26839-489">Ответное действие при достижении после hello входящий запрос после получения действие hello считается сбой \(конфликт\), и в результате выполнения hello `Failed`.</span><span class="sxs-lookup"><span data-stu-id="26839-489">If a response action is reached after hello incoming request has received a response, hello action is considered failed \(conflict\), and as a result, hello run is `Failed`.</span></span>  
  
-   <span data-ttu-id="26839-490">Рабочий процесс с действиями ответа не может содержать `splitOn` в своем триггере, так как один вызов запускает несколько выполнений.</span><span class="sxs-lookup"><span data-stu-id="26839-490">A workflow with Response actions cannot have `splitOn` in its trigger because one call causes many runs.</span></span> <span data-ttu-id="26839-491">В результате это должны проверяться, когда поток hello PUT и причина неверный запрос.</span><span class="sxs-lookup"><span data-stu-id="26839-491">As a result, this should be validated when hello flow is PUT and cause a Bad Request.</span></span>  
  
## <a name="wait-action"></a><span data-ttu-id="26839-492">Действие wait</span><span class="sxs-lookup"><span data-stu-id="26839-492">Wait action</span></span>  

<span data-ttu-id="26839-493">Hello `wait` действие приостанавливает выполнение рабочего процесса в течение указанного интервала hello.</span><span class="sxs-lookup"><span data-stu-id="26839-493">hello `wait` action suspends workflow execution for hello specified interval.</span></span> <span data-ttu-id="26839-494">Например, toowait 15 минут можно использовать этот фрагмент кода:</span><span class="sxs-lookup"><span data-stu-id="26839-494">For example, toowait 15 minutes, you can use this snippet:</span></span>  
  
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
  
<span data-ttu-id="26839-495">Кроме того, toowait до определенный момент времени, можно использовать в этом примере:</span><span class="sxs-lookup"><span data-stu-id="26839-495">Alternatively, toowait until a specific moment in time, you can use this example:</span></span>  
  
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
> <span data-ttu-id="26839-496">Длительность ожидания Hello можно задать либо с помощью hello **интервал** объекта или hello **до** объекта, но не оба.</span><span class="sxs-lookup"><span data-stu-id="26839-496">hello wait duration can be either specified using hello **interval** object or hello **until** object, but not both.</span></span>  
  
|<span data-ttu-id="26839-497">Имя</span><span class="sxs-lookup"><span data-stu-id="26839-497">Name</span></span>|<span data-ttu-id="26839-498">Обязательно</span><span class="sxs-lookup"><span data-stu-id="26839-498">Required</span></span>|<span data-ttu-id="26839-499">Тип</span><span class="sxs-lookup"><span data-stu-id="26839-499">Type</span></span>|<span data-ttu-id="26839-500">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-500">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="26839-501">interval</span><span class="sxs-lookup"><span data-stu-id="26839-501">interval</span></span>|<span data-ttu-id="26839-502">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-502">No</span></span>|<span data-ttu-id="26839-503">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-503">Object</span></span>|<span data-ttu-id="26839-504">длительность, в зависимости от времени ожидания Hello.</span><span class="sxs-lookup"><span data-stu-id="26839-504">hello wait duration based on amount of time.</span></span>|  
|<span data-ttu-id="26839-505">interval unit</span><span class="sxs-lookup"><span data-stu-id="26839-505">interval unit</span></span>|<span data-ttu-id="26839-506">Да</span><span class="sxs-lookup"><span data-stu-id="26839-506">Yes</span></span>|<span data-ttu-id="26839-507">Строка</span><span class="sxs-lookup"><span data-stu-id="26839-507">String</span></span>|<span data-ttu-id="26839-508">Одна из таких единиц времени: second, minute, hour, day, week, month, year.</span><span class="sxs-lookup"><span data-stu-id="26839-508">One of these intervals: second, minute, hour, day, week, month, year.</span></span>|  
|<span data-ttu-id="26839-509">interval count</span><span class="sxs-lookup"><span data-stu-id="26839-509">interval count</span></span>|<span data-ttu-id="26839-510">Да</span><span class="sxs-lookup"><span data-stu-id="26839-510">Yes</span></span>|<span data-ttu-id="26839-511">Строка</span><span class="sxs-lookup"><span data-stu-id="26839-511">String</span></span>|<span data-ttu-id="26839-512">Длительность основании hello данных внутренних единицах измерения.</span><span class="sxs-lookup"><span data-stu-id="26839-512">Duration based on hello given internal unit.</span></span>|  
|<span data-ttu-id="26839-513">until</span><span class="sxs-lookup"><span data-stu-id="26839-513">until</span></span>|<span data-ttu-id="26839-514">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-514">No</span></span>|<span data-ttu-id="26839-515">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-515">Object</span></span>|<span data-ttu-id="26839-516">длительность, основано на точке на времени ожидания Hello.</span><span class="sxs-lookup"><span data-stu-id="26839-516">hello wait duration based on a point in time.</span></span>|  
|<span data-ttu-id="26839-517">until timestamp</span><span class="sxs-lookup"><span data-stu-id="26839-517">until timestamp</span></span>|<span data-ttu-id="26839-518">Да</span><span class="sxs-lookup"><span data-stu-id="26839-518">Yes</span></span>|<span data-ttu-id="26839-519">Строка</span><span class="sxs-lookup"><span data-stu-id="26839-519">String</span></span>|<span data-ttu-id="26839-520">Строка &#124; hello моменту времени в формате UTC, когда hello ожидания истечения срока действия.</span><span class="sxs-lookup"><span data-stu-id="26839-520">String&#124;hello point in time in UTC when hello wait expires.</span></span>|  

## <a name="query-action"></a><span data-ttu-id="26839-521">Действие запроса</span><span class="sxs-lookup"><span data-stu-id="26839-521">Query action</span></span>

<span data-ttu-id="26839-522">Hello `query` действие позволяет фильтровать массив на основе условия.</span><span class="sxs-lookup"><span data-stu-id="26839-522">hello `query` action lets you filter an array based on a condition.</span></span> <span data-ttu-id="26839-523">Например номера tooselect больше 2, можно использовать:</span><span class="sxs-lookup"><span data-stu-id="26839-523">For example, tooselect numbers greater than 2, you can use:</span></span>

```json
"FilterNumbers" : {
    "type": "query",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "where": "@greater(item(), 2)"
    }
}
```

<span data-ttu-id="26839-524">Здравствуйте, выходные данные hello `query` действие — массив, содержащий элементы из входного массива hello, удовлетворяющие условию hello.</span><span class="sxs-lookup"><span data-stu-id="26839-524">hello output from hello `query` action is an array that has elements from hello input array that satisfy hello condition.</span></span>

> [!NOTE]
> <span data-ttu-id="26839-525">Если значения не удовлетворяют hello `where` условия, hello результат — пустой массив.</span><span class="sxs-lookup"><span data-stu-id="26839-525">If no values satisfy hello `where` condition, hello result is an empty array.</span></span>

|<span data-ttu-id="26839-526">Имя</span><span class="sxs-lookup"><span data-stu-id="26839-526">Name</span></span>|<span data-ttu-id="26839-527">Обязательно</span><span class="sxs-lookup"><span data-stu-id="26839-527">Required</span></span>|<span data-ttu-id="26839-528">Тип</span><span class="sxs-lookup"><span data-stu-id="26839-528">Type</span></span>|<span data-ttu-id="26839-529">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-529">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="26839-530">from</span><span class="sxs-lookup"><span data-stu-id="26839-530">from</span></span>|<span data-ttu-id="26839-531">Да</span><span class="sxs-lookup"><span data-stu-id="26839-531">Yes</span></span>|<span data-ttu-id="26839-532">Массив,</span><span class="sxs-lookup"><span data-stu-id="26839-532">Array</span></span>|<span data-ttu-id="26839-533">Hello исходного массива.</span><span class="sxs-lookup"><span data-stu-id="26839-533">hello source array.</span></span>|
|<span data-ttu-id="26839-534">где:</span><span class="sxs-lookup"><span data-stu-id="26839-534">where</span></span>|<span data-ttu-id="26839-535">Да</span><span class="sxs-lookup"><span data-stu-id="26839-535">Yes</span></span>|<span data-ttu-id="26839-536">Строка</span><span class="sxs-lookup"><span data-stu-id="26839-536">String</span></span>|<span data-ttu-id="26839-537">Hello условие tooapply tooeach элемент hello исходного массива.</span><span class="sxs-lookup"><span data-stu-id="26839-537">hello condition tooapply tooeach element of hello source array.</span></span>|

## <a name="select-action"></a><span data-ttu-id="26839-538">Выбор действия</span><span class="sxs-lookup"><span data-stu-id="26839-538">Select action</span></span>

<span data-ttu-id="26839-539">Hello `select` действие позволяет проект в новое значение каждого элемента массива.</span><span class="sxs-lookup"><span data-stu-id="26839-539">hello `select` action lets you project each element of an array into a new value.</span></span>
<span data-ttu-id="26839-540">Например, tooconvert массив чисел в массив объектов, можно использовать:</span><span class="sxs-lookup"><span data-stu-id="26839-540">For example, tooconvert an array of numbers into an array of objects, you can use:</span></span>

```json
"SelectNumbers" : {
    "type": "select",
    "inputs": {
        "from": [ 1, 3, 0, 5, 4, 2 ],
        "select": { "number": "@item()" }
    }
}
```

<span data-ttu-id="26839-541">Здравствуйте, выходные данные hello `select` действие — массив, содержащий hello того же количества элементов как hello входного массива, при этом каждый элемент, преобразованные в определенный по hello `select` свойство.</span><span class="sxs-lookup"><span data-stu-id="26839-541">hello output of hello `select` action is an array that has hello same cardinality as hello input array, with each element transformed as defined by hello `select` property.</span></span> <span data-ttu-id="26839-542">Если входные данные hello пустой массив, hello выводится также пустой массив.</span><span class="sxs-lookup"><span data-stu-id="26839-542">If hello input is an empty array, hello output is also an empty array.</span></span>

|<span data-ttu-id="26839-543">Имя</span><span class="sxs-lookup"><span data-stu-id="26839-543">Name</span></span>|<span data-ttu-id="26839-544">Обязательно</span><span class="sxs-lookup"><span data-stu-id="26839-544">Required</span></span>|<span data-ttu-id="26839-545">Тип</span><span class="sxs-lookup"><span data-stu-id="26839-545">Type</span></span>|<span data-ttu-id="26839-546">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-546">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="26839-547">from</span><span class="sxs-lookup"><span data-stu-id="26839-547">from</span></span>|<span data-ttu-id="26839-548">Да</span><span class="sxs-lookup"><span data-stu-id="26839-548">Yes</span></span>|<span data-ttu-id="26839-549">Массив,</span><span class="sxs-lookup"><span data-stu-id="26839-549">Array</span></span>|<span data-ttu-id="26839-550">Hello исходного массива.</span><span class="sxs-lookup"><span data-stu-id="26839-550">hello source array.</span></span>|
|<span data-ttu-id="26839-551">select</span><span class="sxs-lookup"><span data-stu-id="26839-551">select</span></span>|<span data-ttu-id="26839-552">Да</span><span class="sxs-lookup"><span data-stu-id="26839-552">Yes</span></span>|<span data-ttu-id="26839-553">Любой</span><span class="sxs-lookup"><span data-stu-id="26839-553">Any</span></span>|<span data-ttu-id="26839-554">Hello проекции tooapply tooeach элемент hello исходного массива.</span><span class="sxs-lookup"><span data-stu-id="26839-554">hello projection tooapply tooeach element of hello source array.</span></span>|

## <a name="terminate-action"></a><span data-ttu-id="26839-555">Действие terminate</span><span class="sxs-lookup"><span data-stu-id="26839-555">Terminate action</span></span>

<span data-ttu-id="26839-556">Действие прерывания Hello останавливает выполнение hello рабочего процесса, прерывание каких-либо незавершенных действий и пропускает все оставшиеся действия.</span><span class="sxs-lookup"><span data-stu-id="26839-556">hello Terminate action stops execution of hello workflow run, aborting any in-flight actions, and skipping any remaining actions.</span></span> <span data-ttu-id="26839-557">Например, tooterminate выполнения со статусом **сбой**, можно использовать следующий фрагмент кода hello:</span><span class="sxs-lookup"><span data-stu-id="26839-557">For example, tooterminate a run with status **Failed**, you can use hello following snippet:</span></span>

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
> <span data-ttu-id="26839-558">Действия уже выполнены не подвержены hello завершить действие.</span><span class="sxs-lookup"><span data-stu-id="26839-558">Actions already completed are not affected by hello terminate action.</span></span>

|<span data-ttu-id="26839-559">Имя</span><span class="sxs-lookup"><span data-stu-id="26839-559">Name</span></span>|<span data-ttu-id="26839-560">Обязательно</span><span class="sxs-lookup"><span data-stu-id="26839-560">Required</span></span>|<span data-ttu-id="26839-561">Тип</span><span class="sxs-lookup"><span data-stu-id="26839-561">Type</span></span>|<span data-ttu-id="26839-562">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-562">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="26839-563">runStatus</span><span class="sxs-lookup"><span data-stu-id="26839-563">runStatus</span></span>|<span data-ttu-id="26839-564">Да</span><span class="sxs-lookup"><span data-stu-id="26839-564">Yes</span></span>|<span data-ttu-id="26839-565">Строка</span><span class="sxs-lookup"><span data-stu-id="26839-565">String</span></span>|<span data-ttu-id="26839-566">целевой объект Hello состояние выполнения.</span><span class="sxs-lookup"><span data-stu-id="26839-566">hello target run status.</span></span> <span data-ttu-id="26839-567">**Failed** или **Cancelled**.</span><span class="sxs-lookup"><span data-stu-id="26839-567">Either **Failed** or **Cancelled**.</span></span>|
|<span data-ttu-id="26839-568">runError</span><span class="sxs-lookup"><span data-stu-id="26839-568">runError</span></span>|<span data-ttu-id="26839-569">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-569">No</span></span>|<span data-ttu-id="26839-570">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-570">Object</span></span>|<span data-ttu-id="26839-571">сведения об ошибке Hello.</span><span class="sxs-lookup"><span data-stu-id="26839-571">hello error details.</span></span> <span data-ttu-id="26839-572">Если поддерживается только **runStatus** задано слишком**сбой**.</span><span class="sxs-lookup"><span data-stu-id="26839-572">Only supported when **runStatus** is set too**Failed**.</span></span>|
|<span data-ttu-id="26839-573">runError code</span><span class="sxs-lookup"><span data-stu-id="26839-573">runError code</span></span>|<span data-ttu-id="26839-574">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-574">No</span></span>|<span data-ttu-id="26839-575">Строка</span><span class="sxs-lookup"><span data-stu-id="26839-575">String</span></span>|<span data-ttu-id="26839-576">Здравствуйте, запустите код ошибки.</span><span class="sxs-lookup"><span data-stu-id="26839-576">hello run error code.</span></span>|
|<span data-ttu-id="26839-577">runError message</span><span class="sxs-lookup"><span data-stu-id="26839-577">runError message</span></span>|<span data-ttu-id="26839-578">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-578">No</span></span>|<span data-ttu-id="26839-579">Строка</span><span class="sxs-lookup"><span data-stu-id="26839-579">String</span></span>|<span data-ttu-id="26839-580">Здравствуйте, запустите сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="26839-580">hello run error message.</span></span>|

## <a name="compose-action"></a><span data-ttu-id="26839-581">Действие compose</span><span class="sxs-lookup"><span data-stu-id="26839-581">Compose action</span></span>

<span data-ttu-id="26839-582">Создать действие Hello дает возможность создавать произвольный объект.</span><span class="sxs-lookup"><span data-stu-id="26839-582">hello Compose action lets you construct an arbitrary object.</span></span> <span data-ttu-id="26839-583">выходные данные Hello hello составления действие является результатом вычисления входами hello.</span><span class="sxs-lookup"><span data-stu-id="26839-583">hello output of hello compose action is hello result of evaluating its inputs.</span></span> <span data-ttu-id="26839-584">Например, можно использовать hello составления выходов toomerge действие из нескольких действий:</span><span class="sxs-lookup"><span data-stu-id="26839-584">For example, you can use hello compose action toomerge outputs of multiple actions:</span></span>

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
> <span data-ttu-id="26839-585">Hello **составление** действие может быть используется tooconstruct выходные данные, включая объекты, массивы и любого другого типа, изначально поддерживаемых логики приложения, как XML и двоичный файл.</span><span class="sxs-lookup"><span data-stu-id="26839-585">hello **Compose** action can be used tooconstruct any output, including objects, arrays, and any other type natively supported by logic apps like XML and binary.</span></span>

## <a name="table-action"></a><span data-ttu-id="26839-586">Действие таблицы</span><span class="sxs-lookup"><span data-stu-id="26839-586">Table action</span></span>

<span data-ttu-id="26839-587">Hello `table` позволяет tooconvert массив элементов в **CSV** или **HTML** таблицы.</span><span class="sxs-lookup"><span data-stu-id="26839-587">hello `table` allows you tooconvert an array of items into a **CSV** or **HTML** table.</span></span>

<span data-ttu-id="26839-588">Предположим, что @triggerBody() выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="26839-588">Suppose @triggerBody() is</span></span>

```json
[{
  "id": 0,
  "name": "apples"
},{
  "id": 1, 
  "name": "oranges"
}]
```

<span data-ttu-id="26839-589">И позволяют определить как действие hello</span><span class="sxs-lookup"><span data-stu-id="26839-589">And let hello action be defined as</span></span>

```json
"ConvertToTable" : {
    "type": "table",
    "inputs": {
        "from": "@triggerBody()",
        "format": "html"
    }
}
```

<span data-ttu-id="26839-590">Hello выше приведет к получению</span><span class="sxs-lookup"><span data-stu-id="26839-590">hello above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="26839-591">id</span><span class="sxs-lookup"><span data-stu-id="26839-591">id</span></span></th><th><span data-ttu-id="26839-592">name</span><span class="sxs-lookup"><span data-stu-id="26839-592">name</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="26839-593">0</span><span class="sxs-lookup"><span data-stu-id="26839-593">0</span></span></td><td><span data-ttu-id="26839-594">apples</span><span class="sxs-lookup"><span data-stu-id="26839-594">apples</span></span></td></tr><tr><td><span data-ttu-id="26839-595">1</span><span class="sxs-lookup"><span data-stu-id="26839-595">1</span></span></td><td><span data-ttu-id="26839-596">oranges</span><span class="sxs-lookup"><span data-stu-id="26839-596">oranges</span></span></td></tr></tbody></table><span data-ttu-id="26839-597">"</span><span class="sxs-lookup"><span data-stu-id="26839-597">"</span></span>

<span data-ttu-id="26839-598">В таблице hello toocustomize заказа можно задать столбцы hello явным образом.</span><span class="sxs-lookup"><span data-stu-id="26839-598">In order toocustomize hello table, you can specify hello columns explicitly.</span></span> <span data-ttu-id="26839-599">Например:</span><span class="sxs-lookup"><span data-stu-id="26839-599">For example:</span></span>

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

<span data-ttu-id="26839-600">Hello выше приведет к получению</span><span class="sxs-lookup"><span data-stu-id="26839-600">hello above would produce</span></span>

<table><thead><tr><th><span data-ttu-id="26839-601">Код результата</span><span class="sxs-lookup"><span data-stu-id="26839-601">produce id</span></span></th><th><span data-ttu-id="26839-602">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-602">description</span></span></th></tr></thead><tbody><tr><td><span data-ttu-id="26839-603">0</span><span class="sxs-lookup"><span data-stu-id="26839-603">0</span></span></td><td><span data-ttu-id="26839-604">fresh apples</span><span class="sxs-lookup"><span data-stu-id="26839-604">fresh apples</span></span></td></tr><tr><td><span data-ttu-id="26839-605">1</span><span class="sxs-lookup"><span data-stu-id="26839-605">1</span></span></td><td><span data-ttu-id="26839-606">fresh oranges</span><span class="sxs-lookup"><span data-stu-id="26839-606">fresh oranges</span></span></td></tr></tbody></table><span data-ttu-id="26839-607">"</span><span class="sxs-lookup"><span data-stu-id="26839-607">"</span></span>

<span data-ttu-id="26839-608">Если hello `from` значение свойства — пустой массив, hello результатом является пустая таблица.</span><span class="sxs-lookup"><span data-stu-id="26839-608">If hello `from` property value is an empty array, hello output is an empty table.</span></span>

|<span data-ttu-id="26839-609">Имя</span><span class="sxs-lookup"><span data-stu-id="26839-609">Name</span></span>|<span data-ttu-id="26839-610">Обязательно</span><span class="sxs-lookup"><span data-stu-id="26839-610">Required</span></span>|<span data-ttu-id="26839-611">Тип</span><span class="sxs-lookup"><span data-stu-id="26839-611">Type</span></span>|<span data-ttu-id="26839-612">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-612">Description</span></span>|
|--------|------------|--------|---------------|
|<span data-ttu-id="26839-613">from</span><span class="sxs-lookup"><span data-stu-id="26839-613">from</span></span>|<span data-ttu-id="26839-614">Да</span><span class="sxs-lookup"><span data-stu-id="26839-614">Yes</span></span>|<span data-ttu-id="26839-615">Массив,</span><span class="sxs-lookup"><span data-stu-id="26839-615">Array</span></span>|<span data-ttu-id="26839-616">Hello исходного массива.</span><span class="sxs-lookup"><span data-stu-id="26839-616">hello source array.</span></span>|
|<span data-ttu-id="26839-617">свойства</span><span class="sxs-lookup"><span data-stu-id="26839-617">format</span></span>|<span data-ttu-id="26839-618">Да</span><span class="sxs-lookup"><span data-stu-id="26839-618">Yes</span></span>|<span data-ttu-id="26839-619">Строка</span><span class="sxs-lookup"><span data-stu-id="26839-619">String</span></span>|<span data-ttu-id="26839-620">Здравствуйте, формат, либо **CSV** или **HTML**.</span><span class="sxs-lookup"><span data-stu-id="26839-620">hello format, either **CSV** or **HTML**.</span></span>|
|<span data-ttu-id="26839-621">columns</span><span class="sxs-lookup"><span data-stu-id="26839-621">columns</span></span>|<span data-ttu-id="26839-622">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-622">No</span></span>|<span data-ttu-id="26839-623">Массив,</span><span class="sxs-lookup"><span data-stu-id="26839-623">Array</span></span>|<span data-ttu-id="26839-624">столбцы Hello.</span><span class="sxs-lookup"><span data-stu-id="26839-624">hello columns.</span></span> <span data-ttu-id="26839-625">Позволяет toooverride фигуры по умолчанию hello hello таблицы.</span><span class="sxs-lookup"><span data-stu-id="26839-625">Allows toooverride hello default shape of hello table.</span></span>|
|<span data-ttu-id="26839-626">column header</span><span class="sxs-lookup"><span data-stu-id="26839-626">column header</span></span>|<span data-ttu-id="26839-627">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-627">No</span></span>|<span data-ttu-id="26839-628">Строка</span><span class="sxs-lookup"><span data-stu-id="26839-628">String</span></span>|<span data-ttu-id="26839-629">заголовок столбца hello Hello.</span><span class="sxs-lookup"><span data-stu-id="26839-629">hello header of hello column.</span></span>|
|<span data-ttu-id="26839-630">column value</span><span class="sxs-lookup"><span data-stu-id="26839-630">column value</span></span>|<span data-ttu-id="26839-631">Да</span><span class="sxs-lookup"><span data-stu-id="26839-631">Yes</span></span>|<span data-ttu-id="26839-632">Строка</span><span class="sxs-lookup"><span data-stu-id="26839-632">String</span></span>|<span data-ttu-id="26839-633">значение столбца hello Hello.</span><span class="sxs-lookup"><span data-stu-id="26839-633">hello value of hello column.</span></span>|

## <a name="workflow-action"></a><span data-ttu-id="26839-634">Действие workflow</span><span class="sxs-lookup"><span data-stu-id="26839-634">Workflow action</span></span>   

|<span data-ttu-id="26839-635">Имя</span><span class="sxs-lookup"><span data-stu-id="26839-635">Name</span></span>|<span data-ttu-id="26839-636">Обязательно</span><span class="sxs-lookup"><span data-stu-id="26839-636">Required</span></span>|<span data-ttu-id="26839-637">Тип</span><span class="sxs-lookup"><span data-stu-id="26839-637">Type</span></span>|<span data-ttu-id="26839-638">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-638">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="26839-639">host id</span><span class="sxs-lookup"><span data-stu-id="26839-639">host id</span></span>|<span data-ttu-id="26839-640">Да</span><span class="sxs-lookup"><span data-stu-id="26839-640">Yes</span></span>|<span data-ttu-id="26839-641">Строка</span><span class="sxs-lookup"><span data-stu-id="26839-641">String</span></span>|<span data-ttu-id="26839-642">Идентификатор ресурса Hello hello рабочего процесса, которые должны toocall.</span><span class="sxs-lookup"><span data-stu-id="26839-642">hello resource ID of hello workflow that you want toocall.</span></span>|  
|<span data-ttu-id="26839-643">host triggerName</span><span class="sxs-lookup"><span data-stu-id="26839-643">host triggerName</span></span>|<span data-ttu-id="26839-644">Да</span><span class="sxs-lookup"><span data-stu-id="26839-644">Yes</span></span>|<span data-ttu-id="26839-645">Строка</span><span class="sxs-lookup"><span data-stu-id="26839-645">String</span></span>|<span data-ttu-id="26839-646">Имя триггера hello, что требуется tooinvoke Hello.</span><span class="sxs-lookup"><span data-stu-id="26839-646">hello name of hello trigger that you want tooinvoke.</span></span>|  
|<span data-ttu-id="26839-647">Запросы</span><span class="sxs-lookup"><span data-stu-id="26839-647">queries</span></span>|<span data-ttu-id="26839-648">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-648">No</span></span>|<span data-ttu-id="26839-649">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-649">Object</span></span>|<span data-ttu-id="26839-650">Представляет URL-адрес hello запроса параметров tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="26839-650">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="26839-651">Например `"queries" : { "api-version": "2015-02-01" }` добавляет `?api-version=2015-02-01` toohello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="26839-651">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="26839-652">headers</span><span class="sxs-lookup"><span data-stu-id="26839-652">headers</span></span>|<span data-ttu-id="26839-653">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-653">No</span></span>|<span data-ttu-id="26839-654">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-654">Object</span></span>|<span data-ttu-id="26839-655">Представляет каждый заголовков hello, отправляет запрос toohello.</span><span class="sxs-lookup"><span data-stu-id="26839-655">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="26839-656">Например tooset hello язык и тип запроса в:`"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span><span class="sxs-lookup"><span data-stu-id="26839-656">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us",  "Content-Type": "application/json" }`</span></span>|  
|<span data-ttu-id="26839-657">текст</span><span class="sxs-lookup"><span data-stu-id="26839-657">body</span></span>|<span data-ttu-id="26839-658">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-658">No</span></span>|<span data-ttu-id="26839-659">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-659">Object</span></span>|<span data-ttu-id="26839-660">Представляет hello полезные данные, отправленные toohello конечной точки.</span><span class="sxs-lookup"><span data-stu-id="26839-660">Represents hello payload sent toohello endpoint.</span></span>|  
  
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
  
<span data-ttu-id="26839-661">Проверку доступа, внесенные в рабочий процесс hello \(точнее, триггер hello\), то есть вы должны получить доступ к toohello рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="26839-661">An access check is made on hello workflow \(more specifically, hello trigger\), meaning you need access toohello workflow.</span></span>  
  
<span data-ttu-id="26839-662">Выводит Hello из hello `workflow` действия основаны на определенный hello `response` действия в рабочем процессе дочерних hello.</span><span class="sxs-lookup"><span data-stu-id="26839-662">hello outputs from hello `workflow` action are based on what you defined in hello `response` action in hello child workflow.</span></span> <span data-ttu-id="26839-663">Если вы не определили любой `response` действие, а затем выходы hello пусты.</span><span class="sxs-lookup"><span data-stu-id="26839-663">If you have not defined any `response` action, then hello outputs are empty.</span></span>  

## <a name="function-action"></a><span data-ttu-id="26839-664">Действие функции</span><span class="sxs-lookup"><span data-stu-id="26839-664">Function action</span></span>   

|<span data-ttu-id="26839-665">Имя</span><span class="sxs-lookup"><span data-stu-id="26839-665">Name</span></span>|<span data-ttu-id="26839-666">Обязательно</span><span class="sxs-lookup"><span data-stu-id="26839-666">Required</span></span>|<span data-ttu-id="26839-667">Тип</span><span class="sxs-lookup"><span data-stu-id="26839-667">Type</span></span>|<span data-ttu-id="26839-668">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-668">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="26839-669">ИД функции</span><span class="sxs-lookup"><span data-stu-id="26839-669">function id</span></span>|<span data-ttu-id="26839-670">Да</span><span class="sxs-lookup"><span data-stu-id="26839-670">Yes</span></span>|<span data-ttu-id="26839-671">Строка</span><span class="sxs-lookup"><span data-stu-id="26839-671">String</span></span>|<span data-ttu-id="26839-672">Идентификатор ресурса, которые должны tooinvoke функции hello Hello.</span><span class="sxs-lookup"><span data-stu-id="26839-672">hello resource ID of hello function that you want tooinvoke.</span></span>|  
|<span data-ttu-id="26839-673">метод</span><span class="sxs-lookup"><span data-stu-id="26839-673">method</span></span>|<span data-ttu-id="26839-674">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-674">No</span></span>|<span data-ttu-id="26839-675">Строка</span><span class="sxs-lookup"><span data-stu-id="26839-675">String</span></span>|<span data-ttu-id="26839-676">метод HTTP Hello используется tooinvoke функции hello.</span><span class="sxs-lookup"><span data-stu-id="26839-676">hello HTTP method used tooinvoke hello function.</span></span> <span data-ttu-id="26839-677">Если не указан, по умолчанию используется `POST`.</span><span class="sxs-lookup"><span data-stu-id="26839-677">By default, it is `POST` when not specified.</span></span>|  
|<span data-ttu-id="26839-678">Запросы</span><span class="sxs-lookup"><span data-stu-id="26839-678">queries</span></span>|<span data-ttu-id="26839-679">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-679">No</span></span>|<span data-ttu-id="26839-680">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-680">Object</span></span>|<span data-ttu-id="26839-681">Представляет URL-адрес hello запроса параметров tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="26839-681">Represents hello query parameters tooadd toohello URL.</span></span> <span data-ttu-id="26839-682">Например `"queries" : { "api-version": "2015-02-01" }` добавляет `?api-version=2015-02-01` toohello URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="26839-682">For example, `"queries" : { "api-version": "2015-02-01" }` adds `?api-version=2015-02-01` toohello URL.</span></span>|  
|<span data-ttu-id="26839-683">headers</span><span class="sxs-lookup"><span data-stu-id="26839-683">headers</span></span>|<span data-ttu-id="26839-684">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-684">No</span></span>|<span data-ttu-id="26839-685">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-685">Object</span></span>|<span data-ttu-id="26839-686">Представляет каждый заголовков hello, отправляет запрос toohello.</span><span class="sxs-lookup"><span data-stu-id="26839-686">Represents each of hello headers that is sent toohello request.</span></span> <span data-ttu-id="26839-687">Например, tooset hello язык и тип запроса в: `"headers" : { "Accept-Language": "en-us" }`.</span><span class="sxs-lookup"><span data-stu-id="26839-687">For example, tooset hello language and type on a request: `"headers" : { "Accept-Language": "en-us" }`.</span></span>|  
|<span data-ttu-id="26839-688">текст</span><span class="sxs-lookup"><span data-stu-id="26839-688">body</span></span>|<span data-ttu-id="26839-689">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-689">No</span></span>|<span data-ttu-id="26839-690">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-690">Object</span></span>|<span data-ttu-id="26839-691">Представляет hello полезные данные, отправленные toohello конечной точки.</span><span class="sxs-lookup"><span data-stu-id="26839-691">Represents hello payload sent toohello endpoint.</span></span>|  

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

<span data-ttu-id="26839-692">При сохранении логику приложения hello, мы выполняет ряд проверок на hello ссылка на функцию:</span><span class="sxs-lookup"><span data-stu-id="26839-692">When you save hello logic app, we perform some checks on hello referenced function:</span></span>
-   <span data-ttu-id="26839-693">Требуется функция toohello toohave доступа.</span><span class="sxs-lookup"><span data-stu-id="26839-693">You need toohave access toohello function.</span></span>
-   <span data-ttu-id="26839-694">Допускается только стандартный триггер HTTP или универсальный триггер webhook в формате JSON.</span><span class="sxs-lookup"><span data-stu-id="26839-694">Only standard HTTP trigger or generic JSON webhook trigger is allowed.</span></span>
-   <span data-ttu-id="26839-695">В ней не должен быть определен какой-либо маршрут.</span><span class="sxs-lookup"><span data-stu-id="26839-695">It should not have any route defined.</span></span>
-   <span data-ttu-id="26839-696">Допускаются только авторизация с помощью функции и анонимная авторизация.</span><span class="sxs-lookup"><span data-stu-id="26839-696">Only "function" and "anonymous" authorization level is allowed.</span></span>

<span data-ttu-id="26839-697">URL-адрес триггера Hello извлекается, кэшируются и используются во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="26839-697">hello trigger URL is retrieved, cached, and used at runtime.</span></span> <span data-ttu-id="26839-698">Поэтому если любая операция делает недействительными кэшированные hello URL-адрес, действие hello завершается ошибкой во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="26839-698">So if any operation invalidates hello cached URL, hello action fails at runtime.</span></span> <span data-ttu-id="26839-699">toowork возникновения этой проблемы, сохранения hello логику приложения еще раз, что будет привести tooretrieve логику приложения и кэшировать URL-адрес триггера hello еще раз.</span><span class="sxs-lookup"><span data-stu-id="26839-699">toowork around this, save hello logic app again, which will cause logic app tooretrieve and cache hello trigger URL again.</span></span>

## <a name="collection-actions-scopes-and-loops"></a><span data-ttu-id="26839-700">Действия коллекций (области и циклы)</span><span class="sxs-lookup"><span data-stu-id="26839-700">Collection actions (scopes and loops)</span></span>

<span data-ttu-id="26839-701">Действия некоторых типов могут содержать вложенные действия.</span><span class="sxs-lookup"><span data-stu-id="26839-701">Some action types can contain actions within themselves.</span></span> <span data-ttu-id="26839-702">Ссылка действия в пределах коллекции можно ссылаться непосредственно за пределами коллекции hello.</span><span class="sxs-lookup"><span data-stu-id="26839-702">Reference actions within a collection can be referenced directly outside of hello collection.</span></span> <span data-ttu-id="26839-703">Если вы определили `http` в области, `@body('http')` действительно в любой точке рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="26839-703">If you defined `http` in a scope, `@body('http')` is still valid anywhere in a workflow.</span></span> <span data-ttu-id="26839-704">Действия в пределах коллекции могут `runAfter` Здравствуйте, другие действия в одной коллекции.</span><span class="sxs-lookup"><span data-stu-id="26839-704">Actions within a collection can `runAfter` only other actions within hello same collection.</span></span>

## <a name="scope-action"></a><span data-ttu-id="26839-705">Действие scope</span><span class="sxs-lookup"><span data-stu-id="26839-705">Scope action</span></span>

<span data-ttu-id="26839-706">Hello `scope` действие позволяет логически группы действий в рабочем процессе.</span><span class="sxs-lookup"><span data-stu-id="26839-706">hello `scope` action lets you logically group actions in a workflow.</span></span>

|<span data-ttu-id="26839-707">Имя</span><span class="sxs-lookup"><span data-stu-id="26839-707">Name</span></span>|<span data-ttu-id="26839-708">Обязательно</span><span class="sxs-lookup"><span data-stu-id="26839-708">Required</span></span>|<span data-ttu-id="26839-709">Тип</span><span class="sxs-lookup"><span data-stu-id="26839-709">Type</span></span>|<span data-ttu-id="26839-710">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-710">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="26839-711">actions</span><span class="sxs-lookup"><span data-stu-id="26839-711">actions</span></span>|<span data-ttu-id="26839-712">Да</span><span class="sxs-lookup"><span data-stu-id="26839-712">Yes</span></span>|<span data-ttu-id="26839-713">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-713">Object</span></span>|<span data-ttu-id="26839-714">Tooexecute внутреннего действия в пределах области hello</span><span class="sxs-lookup"><span data-stu-id="26839-714">Inner actions tooexecute within hello scope</span></span>|

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

## <a name="foreach-action"></a><span data-ttu-id="26839-715">Действие foreach</span><span class="sxs-lookup"><span data-stu-id="26839-715">ForEach action</span></span>

<span data-ttu-id="26839-716">Это циклическое действие выполняет итерацию по массиву и внутренние действия для каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="26839-716">This looping action iterates through an array and performs inner actions for each item.</span></span> <span data-ttu-id="26839-717">По умолчанию hello цикл выполняется в параллельном режиме (20 выполнений параллельно одновременно).</span><span class="sxs-lookup"><span data-stu-id="26839-717">By default, hello foreach loop executes in parallel (20 executions in parallel at a time).</span></span> <span data-ttu-id="26839-718">Можно задать выполнение правила с помощью hello `operationOptions` параметра.</span><span class="sxs-lookup"><span data-stu-id="26839-718">You can set execution rules using hello `operationOptions` parameter.</span></span>

|<span data-ttu-id="26839-719">Имя</span><span class="sxs-lookup"><span data-stu-id="26839-719">Name</span></span>|<span data-ttu-id="26839-720">Обязательно</span><span class="sxs-lookup"><span data-stu-id="26839-720">Required</span></span>|<span data-ttu-id="26839-721">Тип</span><span class="sxs-lookup"><span data-stu-id="26839-721">Type</span></span>|<span data-ttu-id="26839-722">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-722">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="26839-723">actions</span><span class="sxs-lookup"><span data-stu-id="26839-723">actions</span></span>|<span data-ttu-id="26839-724">Да</span><span class="sxs-lookup"><span data-stu-id="26839-724">Yes</span></span>|<span data-ttu-id="26839-725">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-725">Object</span></span>|<span data-ttu-id="26839-726">Tooexecute внутреннего действия в цикле hello</span><span class="sxs-lookup"><span data-stu-id="26839-726">Inner actions tooexecute within hello loop</span></span>|
|<span data-ttu-id="26839-727">foreach</span><span class="sxs-lookup"><span data-stu-id="26839-727">foreach</span></span>|<span data-ttu-id="26839-728">Да</span><span class="sxs-lookup"><span data-stu-id="26839-728">Yes</span></span>|<span data-ttu-id="26839-729">string</span><span class="sxs-lookup"><span data-stu-id="26839-729">string</span></span>|<span data-ttu-id="26839-730">Hello tooiterate массива по</span><span class="sxs-lookup"><span data-stu-id="26839-730">hello array tooiterate over</span></span>|
|<span data-ttu-id="26839-731">operationOptions</span><span class="sxs-lookup"><span data-stu-id="26839-731">operationOptions</span></span>|<span data-ttu-id="26839-732">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-732">no</span></span>|<span data-ttu-id="26839-733">строка</span><span class="sxs-lookup"><span data-stu-id="26839-733">string</span></span>|<span data-ttu-id="26839-734">Любые параметры операции для определения поведения.</span><span class="sxs-lookup"><span data-stu-id="26839-734">Any operation options for behavior.</span></span> <span data-ttu-id="26839-735">В настоящее время поддерживает только `sequential` tooexecute итераций последовательно (поведение по умолчанию — параллельных)</span><span class="sxs-lookup"><span data-stu-id="26839-735">Currently only supports `sequential` tooexecute iterations sequentially (default behavior is parallel)</span></span>|

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

## <a name="until-action"></a><span data-ttu-id="26839-736">Действие Until</span><span class="sxs-lookup"><span data-stu-id="26839-736">Until action</span></span>

<span data-ttu-id="26839-737">Это действие цикла выполняет внутреннее действия, пока приводит tootrue.</span><span class="sxs-lookup"><span data-stu-id="26839-737">This looping action executes inner actions until a condition results tootrue.</span></span>

|<span data-ttu-id="26839-738">Имя</span><span class="sxs-lookup"><span data-stu-id="26839-738">Name</span></span>|<span data-ttu-id="26839-739">Обязательно</span><span class="sxs-lookup"><span data-stu-id="26839-739">Required</span></span>|<span data-ttu-id="26839-740">Тип</span><span class="sxs-lookup"><span data-stu-id="26839-740">Type</span></span>|<span data-ttu-id="26839-741">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-741">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="26839-742">actions</span><span class="sxs-lookup"><span data-stu-id="26839-742">actions</span></span>|<span data-ttu-id="26839-743">Да</span><span class="sxs-lookup"><span data-stu-id="26839-743">Yes</span></span>|<span data-ttu-id="26839-744">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-744">Object</span></span>|<span data-ttu-id="26839-745">Tooexecute внутреннего действия в цикле hello</span><span class="sxs-lookup"><span data-stu-id="26839-745">Inner actions tooexecute within hello loop</span></span>|
|<span data-ttu-id="26839-746">expression</span><span class="sxs-lookup"><span data-stu-id="26839-746">expression</span></span>|<span data-ttu-id="26839-747">Да</span><span class="sxs-lookup"><span data-stu-id="26839-747">Yes</span></span>|<span data-ttu-id="26839-748">string</span><span class="sxs-lookup"><span data-stu-id="26839-748">string</span></span>|<span data-ttu-id="26839-749">tooevaluate выражение Hello после каждой итерации</span><span class="sxs-lookup"><span data-stu-id="26839-749">hello expression tooevaluate after each iteration</span></span>|
|<span data-ttu-id="26839-750">limit</span><span class="sxs-lookup"><span data-stu-id="26839-750">limit</span></span>|<span data-ttu-id="26839-751">Да</span><span class="sxs-lookup"><span data-stu-id="26839-751">yes</span></span>|<span data-ttu-id="26839-752">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-752">Object</span></span>|<span data-ttu-id="26839-753">должен быть определен Hello ограничения для hello цикл - по крайней мере один нижний предел</span><span class="sxs-lookup"><span data-stu-id="26839-753">hello limits for hello loop - at least one limit must be defined</span></span>|
|<span data-ttu-id="26839-754">count</span><span class="sxs-lookup"><span data-stu-id="26839-754">count</span></span>|<span data-ttu-id="26839-755">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-755">no</span></span>|<span data-ttu-id="26839-756">int</span><span class="sxs-lookup"><span data-stu-id="26839-756">int</span></span>|<span data-ttu-id="26839-757">Hello ограничение toohello числа итераций, которые могут быть выполнены</span><span class="sxs-lookup"><span data-stu-id="26839-757">hello limit toohello number of iterations that can be performed</span></span>|
|<span data-ttu-id="26839-758">timeout</span><span class="sxs-lookup"><span data-stu-id="26839-758">timeout</span></span>|<span data-ttu-id="26839-759">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-759">no</span></span>|<span data-ttu-id="26839-760">string</span><span class="sxs-lookup"><span data-stu-id="26839-760">string</span></span>|<span data-ttu-id="26839-761">Здравствуйте, как долго следует цикла время ожидания.</span><span class="sxs-lookup"><span data-stu-id="26839-761">hello timeout for how long it should loop.</span></span>  <span data-ttu-id="26839-762">(в формате ISO 8601).</span><span class="sxs-lookup"><span data-stu-id="26839-762">ISO 8601 format</span></span>|


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

## <a name="conditions---if-action"></a><span data-ttu-id="26839-763">Условия. Действие If</span><span class="sxs-lookup"><span data-stu-id="26839-763">Conditions - If Action</span></span>

<span data-ttu-id="26839-764">Hello `If` действия позволяет вычислить условие и выполнение ветви, в зависимости от того, является ли выражение hello имеет слишком`true`.</span><span class="sxs-lookup"><span data-stu-id="26839-764">hello `If` action lets you evaluate a condition and execute a branch based on whether hello expression evaluates too`true`.</span></span>

|<span data-ttu-id="26839-765">Имя</span><span class="sxs-lookup"><span data-stu-id="26839-765">Name</span></span>|<span data-ttu-id="26839-766">Обязательно</span><span class="sxs-lookup"><span data-stu-id="26839-766">Required</span></span>|<span data-ttu-id="26839-767">Тип</span><span class="sxs-lookup"><span data-stu-id="26839-767">Type</span></span>|<span data-ttu-id="26839-768">Описание</span><span class="sxs-lookup"><span data-stu-id="26839-768">Description</span></span>|  
|--------|------------|--------|---------------|  
|<span data-ttu-id="26839-769">actions</span><span class="sxs-lookup"><span data-stu-id="26839-769">actions</span></span>|<span data-ttu-id="26839-770">Да</span><span class="sxs-lookup"><span data-stu-id="26839-770">Yes</span></span>|<span data-ttu-id="26839-771">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-771">Object</span></span>|<span data-ttu-id="26839-772">Tooexecute внутреннего действия, когда выражение имеет слишком`true`</span><span class="sxs-lookup"><span data-stu-id="26839-772">Inner actions tooexecute when expression evaluates too`true`</span></span>|
|<span data-ttu-id="26839-773">expression</span><span class="sxs-lookup"><span data-stu-id="26839-773">expression</span></span>|<span data-ttu-id="26839-774">Да</span><span class="sxs-lookup"><span data-stu-id="26839-774">Yes</span></span>|<span data-ttu-id="26839-775">string</span><span class="sxs-lookup"><span data-stu-id="26839-775">string</span></span>|<span data-ttu-id="26839-776">выражение tooevaluate Hello</span><span class="sxs-lookup"><span data-stu-id="26839-776">hello expression tooevaluate</span></span>|
|<span data-ttu-id="26839-777">else</span><span class="sxs-lookup"><span data-stu-id="26839-777">else</span></span>|<span data-ttu-id="26839-778">Нет</span><span class="sxs-lookup"><span data-stu-id="26839-778">no</span></span>|<span data-ttu-id="26839-779">Объект</span><span class="sxs-lookup"><span data-stu-id="26839-779">Object</span></span>|<span data-ttu-id="26839-780">Tooexecute внутреннего действия, когда выражение имеет слишком`false`</span><span class="sxs-lookup"><span data-stu-id="26839-780">Inner actions tooexecute when expression evaluates too`false`</span></span>|
  
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
  
<span data-ttu-id="26839-781">Hello следующей таблице приведены примеры того, как условия можно использовать выражения в действии:</span><span class="sxs-lookup"><span data-stu-id="26839-781">hello following table shows examples of how conditions can use expressions in an action:</span></span>  
  
|<span data-ttu-id="26839-782">Значение JSON</span><span class="sxs-lookup"><span data-stu-id="26839-782">JSON value</span></span>|<span data-ttu-id="26839-783">Результат</span><span class="sxs-lookup"><span data-stu-id="26839-783">Result</span></span>|  
|--------------|----------|  
|`"expression": "@parameters('hasSpecialAction')"`|<span data-ttu-id="26839-784">Любое значение, которое будет возвращаться tootrue вызывает toopass этого условия.</span><span class="sxs-lookup"><span data-stu-id="26839-784">Any value that would evaluate tootrue causes this condition toopass.</span></span> <span data-ttu-id="26839-785">Поддерживаются только логические выражения.</span><span class="sxs-lookup"><span data-stu-id="26839-785">Only Boolean expressions are supported.</span></span> <span data-ttu-id="26839-786">tooconvert других типов tooBoolean, используйте функции `empty`, `equals`.</span><span class="sxs-lookup"><span data-stu-id="26839-786">tooconvert other types tooBoolean, use functions `empty`, `equals`.</span></span>|  
|`"expression": "@greater(actions('act1').output.value, parameters('threshold'))"`|<span data-ttu-id="26839-787">Поддерживаются функции сравнения.</span><span class="sxs-lookup"><span data-stu-id="26839-787">Comparison functions are supported.</span></span> <span data-ttu-id="26839-788">Здесь пример hello действие hello только выполняется, когда выходные данные hello act1 превышает пороговое значение hello.</span><span class="sxs-lookup"><span data-stu-id="26839-788">For hello example here, hello action only executes when hello output of act1 is greater than hello threshold.</span></span>|  
|`"expression": "@or(greater(actions('act1').output.value, parameters('threshold')), less(actions('act1').output.value, 100))"`|<span data-ttu-id="26839-789">Функции логики, также поддерживаемые toocreate вложенных выражений типа Boolean.</span><span class="sxs-lookup"><span data-stu-id="26839-789">Logic functions are also supported toocreate nested Boolean expressions.</span></span> <span data-ttu-id="26839-790">В этом случае hello действие выполняется, когда выходные данные hello act1 выше порогового значения hello или ниже 100.</span><span class="sxs-lookup"><span data-stu-id="26839-790">In this case, hello action executes when hello output of act1 is above hello threshold or below 100.</span></span>|  
|`"expression": "@equals(length(actions('act1').outputs.errors), 0))"`|<span data-ttu-id="26839-791">Функции toocheck массива можно использовать, если массив имеет какие-либо элементы.</span><span class="sxs-lookup"><span data-stu-id="26839-791">You can use array functions toocheck if an array has any items.</span></span> <span data-ttu-id="26839-792">В этом случае hello действие выполняется, когда hello ошибки массив является пустым.</span><span class="sxs-lookup"><span data-stu-id="26839-792">In this case, hello action executes when hello errors array is empty.</span></span>| 
|`"expression": "parameters('hasSpecialAction')"`|<span data-ttu-id="26839-793">Ошибка является недопустимым условием, поскольку для условия требуется @.</span><span class="sxs-lookup"><span data-stu-id="26839-793">Error - not a valid condition because @ is required for conditions.</span></span>|  
  
<span data-ttu-id="26839-794">Если условие не выполняется успешно, условие hello помечается как `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="26839-794">If a condition evaluates successfully, hello condition is marked as `Succeeded`.</span></span> <span data-ttu-id="26839-795">Действия в пределах либо hello `actions` или `else` объектов оценки слишком`Succeeded` при выполнении и успешно выполнен, `Failed` при выполнении и сбой, или `Skipped` при выполнении этой ветви не.</span><span class="sxs-lookup"><span data-stu-id="26839-795">Actions within either hello `actions` or `else` objects evaluate too`Succeeded` when executed and succeeded, `Failed` when executed and failed, or `Skipped` when that branch is not executed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26839-796">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="26839-796">Next steps</span></span>

[<span data-ttu-id="26839-797">REST API службы рабочих процессов</span><span class="sxs-lookup"><span data-stu-id="26839-797">Workflow Service REST API</span></span>](https://docs.microsoft.com/rest/api/logic/workflows)
