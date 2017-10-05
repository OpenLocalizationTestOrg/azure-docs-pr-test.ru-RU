---
title: "Привязки HTTP и webhook в функциях Azure | Microsoft Azure"
description: "Узнайте, как использовать триггеры и привязки HTTP и webhook в функциях Azure."
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: "функции azure, функции, обработка событий, webhook, динамические вычисления, бессерверная архитектура, HTTP, API, REST"
ms.assetid: 2b12200d-63d8-4ec1-9da8-39831d5a51b1
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/18/2016
ms.author: mahender
ms.openlocfilehash: 71c0d22c4b1824078982b9d1cc76645f947ae603
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a><span data-ttu-id="8eee7-104">Привязки HTTP и webhook в функциях Azure</span><span class="sxs-lookup"><span data-stu-id="8eee7-104">Azure Functions HTTP and webhook bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="8eee7-105">В этой статье объясняется, как настраивать и использовать триггеры и привязки в функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="8eee7-105">This article explains how to configure and work with HTTP triggers and bindings in Azure Functions.</span></span>
<span data-ttu-id="8eee7-106">С их помощью на базе функций Azure можно создавать бессерверные API-интерфейсы и отвечать на вызовы webhook.</span><span class="sxs-lookup"><span data-stu-id="8eee7-106">With these, you can use Azure Functions to build serverless APIs and respond to webhooks.</span></span>

<span data-ttu-id="8eee7-107">Функции Azure предоставляют следующие привязки.</span><span class="sxs-lookup"><span data-stu-id="8eee7-107">Azure Functions provides the following bindings:</span></span>
- <span data-ttu-id="8eee7-108">[Триггер HTTP](#httptrigger) позволяет вызвать функцию с помощью HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="8eee7-108">An [HTTP trigger](#httptrigger) lets you invoke a function with an HTTP request.</span></span> <span data-ttu-id="8eee7-109">Его можно настроить для ответа на [webhook](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="8eee7-109">This can be customized to respond to [webhooks](#hooktrigger).</span></span>
- <span data-ttu-id="8eee7-110">[Привязка для вывода HTTP](#output) дает возможность возвращать ответ на запрос.</span><span class="sxs-lookup"><span data-stu-id="8eee7-110">An [HTTP output binding](#output) allows you to respond to the request.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a><span data-ttu-id="8eee7-111">Триггер HTTP</span><span class="sxs-lookup"><span data-stu-id="8eee7-111">HTTP trigger</span></span>
<span data-ttu-id="8eee7-112">Триггер HTTP выполняет выбранную функцию в ответ на запрос HTTP.</span><span class="sxs-lookup"><span data-stu-id="8eee7-112">The HTTP trigger will execute your function in response to an HTTP request.</span></span> <span data-ttu-id="8eee7-113">Его можно настроить для ответа на определенный URL-адрес или набор методов HTTP.</span><span class="sxs-lookup"><span data-stu-id="8eee7-113">You can customize it to respond to a particular URL or set of HTTP methods.</span></span> <span data-ttu-id="8eee7-114">Триггер HTTP также можно настроить для ответа на вызовы webhook.</span><span class="sxs-lookup"><span data-stu-id="8eee7-114">An HTTP trigger can also be configured to respond to webhooks.</span></span> 

<span data-ttu-id="8eee7-115">Если вы используете портал функций, вы сможете быстро начать работу с помощью готового шаблона.</span><span class="sxs-lookup"><span data-stu-id="8eee7-115">If using the Functions portal, you can also get started right away using a pre-made template.</span></span> <span data-ttu-id="8eee7-116">Щелкните **Новая функция**, а затем выберите "API и Webhook" из раскрывающегося списка **Сценарий**.</span><span class="sxs-lookup"><span data-stu-id="8eee7-116">Select **New function** and choose "API & Webhooks" from the **Scenario** dropdown.</span></span> <span data-ttu-id="8eee7-117">Выберите один из шаблонов и нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8eee7-117">Select one of the templates and click **Create**.</span></span>

<span data-ttu-id="8eee7-118">По умолчанию триггер HTTP возвращает на запрос ответ с кодом состояния HTTP "200 ОК" и пустым текстом.</span><span class="sxs-lookup"><span data-stu-id="8eee7-118">By default, an HTTP trigger will respond to the request with an HTTP 200 OK status code and an empty body.</span></span> <span data-ttu-id="8eee7-119">Чтобы изменить ответ, настройте [привязку для вывода HTTP](#output).</span><span class="sxs-lookup"><span data-stu-id="8eee7-119">To modify the response, configure an [HTTP output binding](#output)</span></span>

### <a name="configuring-an-http-trigger"></a><span data-ttu-id="8eee7-120">Настройка триггера HTTP</span><span class="sxs-lookup"><span data-stu-id="8eee7-120">Configuring an HTTP trigger</span></span>
<span data-ttu-id="8eee7-121">Чтобы определить триггер HTTP, поместите объект JSON примерно следующего вида в массив `bindings` файла function.json.</span><span class="sxs-lookup"><span data-stu-id="8eee7-121">An HTTP trigger is defined by including a JSON object similar to the following in the `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function",
    "methods": [ "get" ],
    "route": "values/{id}"
},
```
<span data-ttu-id="8eee7-122">Привязка поддерживает следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="8eee7-122">The binding supports the following properties:</span></span>

* <span data-ttu-id="8eee7-123">**name** (обязательное) — имя переменной, из которой в коде функции можно получить запрос или текст запроса.</span><span class="sxs-lookup"><span data-stu-id="8eee7-123">**name** : Required - the variable name used in function code for the request or request body.</span></span> <span data-ttu-id="8eee7-124">См. раздел [Использование триггера HTTP в коде программы](#httptriggerusage).</span><span class="sxs-lookup"><span data-stu-id="8eee7-124">See [Working with an HTTP trigger from code](#httptriggerusage).</span></span>
* <span data-ttu-id="8eee7-125">**type** (обязательное) —для этого свойства необходимо задать значение httpTrigger.</span><span class="sxs-lookup"><span data-stu-id="8eee7-125">**type** : Required - must be set to "httpTrigger".</span></span>
* <span data-ttu-id="8eee7-126">**direction** (обязательное) — для этого свойства нужно задать значение in.</span><span class="sxs-lookup"><span data-stu-id="8eee7-126">**direction** : Required - must be set to "in".</span></span>
* <span data-ttu-id="8eee7-127">_authLevel_ — определяет, какие ключи (если они требуются) должны присутствовать в запросе, чтобы вызвать функцию.</span><span class="sxs-lookup"><span data-stu-id="8eee7-127">_authLevel_ : This determines what keys, if any, need to be present on the request in order to invoke the function.</span></span> <span data-ttu-id="8eee7-128">См. раздел [Работа с ключами](#keys) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="8eee7-128">See [Working with keys](#keys) below.</span></span> <span data-ttu-id="8eee7-129">Принимается одно из следующих значений:</span><span class="sxs-lookup"><span data-stu-id="8eee7-129">The value can be one of the following:</span></span>
    * <span data-ttu-id="8eee7-130">_anonymous_: ключи API не требуются.</span><span class="sxs-lookup"><span data-stu-id="8eee7-130">_anonymous_: No API key is required.</span></span>
    * <span data-ttu-id="8eee7-131">_function_: требуется ключ API для конкретной функции.</span><span class="sxs-lookup"><span data-stu-id="8eee7-131">_function_: A function-specific API key is required.</span></span> <span data-ttu-id="8eee7-132">Это значение используется по умолчанию, если не указано иное.</span><span class="sxs-lookup"><span data-stu-id="8eee7-132">This is the default value if none is provided.</span></span>
    * <span data-ttu-id="8eee7-133">_admin_: требуется главный ключ.</span><span class="sxs-lookup"><span data-stu-id="8eee7-133">_admin_ : The master key is required.</span></span>
* <span data-ttu-id="8eee7-134">**methods** — это массив методов HTTP, на которые будет отвечать функция.</span><span class="sxs-lookup"><span data-stu-id="8eee7-134">**methods** : This is an array of the HTTP methods to which the function will respond.</span></span> <span data-ttu-id="8eee7-135">Если свойство не указано, функция будет отвечать на все методы HTTP.</span><span class="sxs-lookup"><span data-stu-id="8eee7-135">If not specified, the function will respond to all HTTP methods.</span></span> <span data-ttu-id="8eee7-136">См. раздел [Настройка конечной точки HTTP](#url).</span><span class="sxs-lookup"><span data-stu-id="8eee7-136">See [Customizing the HTTP endpoint](#url).</span></span>
* <span data-ttu-id="8eee7-137">**route** — это шаблон маршрута, который определяет URL-адреса запросов, на которые будет отвечать функция.</span><span class="sxs-lookup"><span data-stu-id="8eee7-137">**route** : This defines the route template, controlling to which request URLs your function will respond.</span></span> <span data-ttu-id="8eee7-138">Если значение не указано, по умолчанию используется `<functionname>`.</span><span class="sxs-lookup"><span data-stu-id="8eee7-138">The default value if none is provided is `<functionname>`.</span></span> <span data-ttu-id="8eee7-139">См. раздел [Настройка конечной точки HTTP](#url).</span><span class="sxs-lookup"><span data-stu-id="8eee7-139">See [Customizing the HTTP endpoint](#url).</span></span>
* <span data-ttu-id="8eee7-140">**webHookType** — указывает, что триггер HTTP должен работать как получатель webhook для указанного поставщика.</span><span class="sxs-lookup"><span data-stu-id="8eee7-140">**webHookType** : This configures the HTTP trigger to act as a webhook reciever for the specified provider.</span></span> <span data-ttu-id="8eee7-141">Если выбран такой вариант, свойство _methods_ задавать не следует.</span><span class="sxs-lookup"><span data-stu-id="8eee7-141">The _methods_ property should not be set if this is chosen.</span></span> <span data-ttu-id="8eee7-142">См. раздел [Ответ на вызовы webhook](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="8eee7-142">See [Responding to webhooks](#hooktrigger).</span></span> <span data-ttu-id="8eee7-143">Принимается одно из следующих значений:</span><span class="sxs-lookup"><span data-stu-id="8eee7-143">The value can be one of the following:</span></span>
    * <span data-ttu-id="8eee7-144">_genericJson_: конечная точка webhook общего назначения без логики для конкретного поставщика.</span><span class="sxs-lookup"><span data-stu-id="8eee7-144">_genericJson_ : A general purpose webhook endpoint without logic for a specific provider.</span></span>
    * <span data-ttu-id="8eee7-145">_github_: функция будет отвечать на вызовы webhook GitHub.</span><span class="sxs-lookup"><span data-stu-id="8eee7-145">_github_ : The function will respond to GitHub webhooks.</span></span> <span data-ttu-id="8eee7-146">Если выбран такой вариант, свойство _authLevel_ задавать не следует.</span><span class="sxs-lookup"><span data-stu-id="8eee7-146">The _authLevel_ property should not be set if this is chosen.</span></span>
    * <span data-ttu-id="8eee7-147">_slack_: функция будет отвечать на вызовы webhook Slack.</span><span class="sxs-lookup"><span data-stu-id="8eee7-147">_slack_ : The function will respond to Slack webhooks.</span></span> <span data-ttu-id="8eee7-148">Если выбран такой вариант, свойство _authLevel_ задавать не следует.</span><span class="sxs-lookup"><span data-stu-id="8eee7-148">The _authLevel_ property should not be set if this is chosen.</span></span>

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a><span data-ttu-id="8eee7-149">Использование триггера HTTP в коде программы</span><span class="sxs-lookup"><span data-stu-id="8eee7-149">Working with an HTTP trigger from code</span></span>
<span data-ttu-id="8eee7-150">Для функций на языках C# и F# можно объявить для входных данных триггера тип `HttpRequestMessage` или пользовательский тип.</span><span class="sxs-lookup"><span data-stu-id="8eee7-150">For C# and F# functions, you can declare the type of your trigger input to be either `HttpRequestMessage` or a custom type.</span></span> <span data-ttu-id="8eee7-151">Если вы выберете `HttpRequestMessage`, то получите полный доступ к объекту запроса.</span><span class="sxs-lookup"><span data-stu-id="8eee7-151">If you choose `HttpRequestMessage`, then you will get full access to the request object.</span></span> <span data-ttu-id="8eee7-152">Для пользовательского типа (например, POCO) функции попытаются выполнить синтаксический анализ текста запроса как объекта JSON и заполнить свойства объекта.</span><span class="sxs-lookup"><span data-stu-id="8eee7-152">For a custom type (such as a POCO), Functions will attempt to parse the request body as JSON to populate the object properties.</span></span>

<span data-ttu-id="8eee7-153">Для функций Node.js среда выполнения Функций предоставляет текст запроса, а не объект запроса.</span><span class="sxs-lookup"><span data-stu-id="8eee7-153">For Node.js functions, the Functions runtime provides the request body instead of the request object.</span></span>

<span data-ttu-id="8eee7-154">В разделе [Образцы триггеров HTTP](#httptriggersample) приводятся примеры использования.</span><span class="sxs-lookup"><span data-stu-id="8eee7-154">See [HTTP trigger samples](#httptriggersample) for example usages.</span></span>


<a name="output"></a>
## <a name="http-response-output-binding"></a><span data-ttu-id="8eee7-155">Привязка для вывода HTTP-ответа</span><span class="sxs-lookup"><span data-stu-id="8eee7-155">HTTP response output binding</span></span>
<span data-ttu-id="8eee7-156">Привязка для вывода HTTP используется для ответа отправителю запроса HTTP.</span><span class="sxs-lookup"><span data-stu-id="8eee7-156">Use the HTTP output binding to respond to the HTTP request sender.</span></span> <span data-ttu-id="8eee7-157">Эта привязка требует наличия триггера HTTP и позволяет настроить ответ, возвращаемый на запрос этого триггера.</span><span class="sxs-lookup"><span data-stu-id="8eee7-157">This binding requires an HTTP trigger and allows you to customize the response associated with the trigger's request.</span></span> <span data-ttu-id="8eee7-158">Если привязка для вывода HTTP отсутствует, триггер HTTP возвращает ответ HTTP "200 ОК" с пустым текстом.</span><span class="sxs-lookup"><span data-stu-id="8eee7-158">If an HTTP output binding is not provided, an HTTP trigger will return HTTP 200 OK with an empty body.</span></span> 

### <a name="configuring-an-http-output-binding"></a><span data-ttu-id="8eee7-159">Настройка привязки для вывода HTTP</span><span class="sxs-lookup"><span data-stu-id="8eee7-159">Configuring an HTTP output binding</span></span>
<span data-ttu-id="8eee7-160">Чтобы определить привязку для вывода HTTP, поместите объект JSON примерно следующего вида в массив `bindings` файла function.json.</span><span class="sxs-lookup"><span data-stu-id="8eee7-160">The HTTP output binding is defined by including a JSON object similar to the following in the `bindings` array of function.json:</span></span>

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
<span data-ttu-id="8eee7-161">Привязка содержит следующие свойства.</span><span class="sxs-lookup"><span data-stu-id="8eee7-161">The binding contains the following properties:</span></span>

* <span data-ttu-id="8eee7-162">**name** (обязательное) — имя переменной, используемое в коде функции для ответа.</span><span class="sxs-lookup"><span data-stu-id="8eee7-162">**name** : Required - the variable name used in function code for the response.</span></span> <span data-ttu-id="8eee7-163">См. раздел [Работа с привязкой для вывода HTTP в коде программы](#outputusage).</span><span class="sxs-lookup"><span data-stu-id="8eee7-163">See [Working with an HTTP output binding from code](#outputusage).</span></span>
* <span data-ttu-id="8eee7-164">**type** (обязательное) —для этого свойства нужно задать значение http.</span><span class="sxs-lookup"><span data-stu-id="8eee7-164">**type** : Required - must be set to "http".</span></span>
* <span data-ttu-id="8eee7-165">**direction** (обязательное) — для этого свойства нужно задать значение out.</span><span class="sxs-lookup"><span data-stu-id="8eee7-165">**direction** : Required - must be set to "out".</span></span>

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a><span data-ttu-id="8eee7-166">Работа с привязкой для вывода HTTP в коде программы</span><span class="sxs-lookup"><span data-stu-id="8eee7-166">Working with an HTTP output binding from code</span></span>
<span data-ttu-id="8eee7-167">Используйте выходной параметр (например, res) для ответа отправителю запроса http или webhook.</span><span class="sxs-lookup"><span data-stu-id="8eee7-167">You can use the output parameter (e.g., "res") to respond to the http or webhook caller.</span></span> <span data-ttu-id="8eee7-168">Кроме того, для передачи ответа можно использовать стандартные методы `Request.CreateResponse()` (в C#) или `context.res` (в Node.JS).</span><span class="sxs-lookup"><span data-stu-id="8eee7-168">Alternatively, you can use the standard `Request.CreateResponse()` (C#) or `context.res` (Node.JS) pattern to return your response.</span></span> <span data-ttu-id="8eee7-169">Примеры использования альтернативных методов см. в разделах с [образцами триггеров HTTP](#httptriggersample) и [webhook](#hooktriggersample).</span><span class="sxs-lookup"><span data-stu-id="8eee7-169">For examples on how to use the latter method, see [HTTP trigger samples](#httptriggersample) and [Webhook trigger samples](#hooktriggersample).</span></span>


<a name="hooktrigger"></a>
## <a name="responding-to-webhooks"></a><span data-ttu-id="8eee7-170">Ответ на вызовы webhook</span><span class="sxs-lookup"><span data-stu-id="8eee7-170">Responding to webhooks</span></span>
<span data-ttu-id="8eee7-171">Триггер HTTP с заданным свойством _webHookType_ будет отвечать на вызовы [webhook](https://en.wikipedia.org/wiki/Webhook).</span><span class="sxs-lookup"><span data-stu-id="8eee7-171">An HTTP trigger with the _webHookType_ property will be configured to respond to [webhooks](https://en.wikipedia.org/wiki/Webhook).</span></span> <span data-ttu-id="8eee7-172">В стандартной конфигурации используется параметр genericJson.</span><span class="sxs-lookup"><span data-stu-id="8eee7-172">The basic configuration uses the "genericJson" setting.</span></span> <span data-ttu-id="8eee7-173">Он определяет, что принимаются только запросы HTTP POST с содержимым типа `application/json`.</span><span class="sxs-lookup"><span data-stu-id="8eee7-173">This restricts requests to only those using HTTP POST and with the `application/json` content type.</span></span>

<span data-ttu-id="8eee7-174">Кроме того, триггер можно адаптировать для определенного поставщика webhook (например, [GitHub](https://developer.github.com/webhooks/) или [Slack](https://api.slack.com/outgoing-webhooks)).</span><span class="sxs-lookup"><span data-stu-id="8eee7-174">The trigger can additionally be tailored to a specific webhook provider (e.g., [GitHub](https://developer.github.com/webhooks/) and [Slack](https://api.slack.com/outgoing-webhooks)).</span></span> <span data-ttu-id="8eee7-175">Если указан поставщик, среда выполнения функций автоматически выполнит логику проверки поставщика.</span><span class="sxs-lookup"><span data-stu-id="8eee7-175">If a provider is specified, the Functions runtime can take care of the provider's validation logic for you.</span></span>  

### <a name="configuring-github-as-a-webhook-provider"></a><span data-ttu-id="8eee7-176">Настройка GitHub в качестве поставщика webhook</span><span class="sxs-lookup"><span data-stu-id="8eee7-176">Configuring GitHub as a webhook provider</span></span>
<span data-ttu-id="8eee7-177">Чтобы настроить ответ на вызовы webhook GitHub, прежде всего создайте функцию с триггером HTTP, для которого свойство _webHookType_ будет иметь значение github.</span><span class="sxs-lookup"><span data-stu-id="8eee7-177">To respond to GitHub webhooks, first create your function with an HTTP Trigger, and set the _webHookType_ property to "github".</span></span> <span data-ttu-id="8eee7-178">Затем скопируйте его [URL-адрес](#url) и [ключ API](#keys) в репозиторий GitHub, используя страницу **Добавить веб-перехватчик**.</span><span class="sxs-lookup"><span data-stu-id="8eee7-178">Then copy its [URL](#url) and [API key](#keys) into your GitHub repository's **Add webhook** page.</span></span> <span data-ttu-id="8eee7-179">Дополнительные сведения см. в разделе документации GitHub [о создании webhook](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="8eee7-179">See GitHub's [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentation for more.</span></span>

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a><span data-ttu-id="8eee7-180">Настройка Slack в качестве поставщика webhook</span><span class="sxs-lookup"><span data-stu-id="8eee7-180">Configuring Slack as a webhook provider</span></span>
<span data-ttu-id="8eee7-181">Webhook Slack создает маркер автоматически и не позволяет вам задать его, поэтому необходимо настроить ключ для конкретной функции с использованием маркера, предоставленного Slack.</span><span class="sxs-lookup"><span data-stu-id="8eee7-181">The Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with the token from Slack.</span></span> <span data-ttu-id="8eee7-182">См. раздел [Работа с ключами](#keys).</span><span class="sxs-lookup"><span data-stu-id="8eee7-182">See [Working with keys](#keys).</span></span>

<a name="url"></a>
## <a name="customizing-the-http-endpoint"></a><span data-ttu-id="8eee7-183">Настройка конечной точки HTTP</span><span class="sxs-lookup"><span data-stu-id="8eee7-183">Customizing the HTTP endpoint</span></span>
<span data-ttu-id="8eee7-184">По умолчанию при создании функции для триггера HTTP или WebHook маршрут для ее адресации имеет следующий вид.</span><span class="sxs-lookup"><span data-stu-id="8eee7-184">By default when you create a function for an HTTP trigger, or WebHook, the function is addressable with a route of the form:</span></span>

    http://<yourapp>.azurewebsites.net/api/<funcname> 

<span data-ttu-id="8eee7-185">Этот маршрут можно настроить с помощью дополнительного свойства `route` привязки для вывода триггера HTTP.</span><span class="sxs-lookup"><span data-stu-id="8eee7-185">You can customize this route using the optional `route` property on the HTTP trigger's input binding.</span></span> <span data-ttu-id="8eee7-186">Например, приведенный ниже файл *function.json* определяет свойство `route` для триггера HTTP.</span><span class="sxs-lookup"><span data-stu-id="8eee7-186">As an example, the following *function.json* file defines a `route` property for an HTTP trigger:</span></span>

```json
    {
      "bindings": [
        {
          "type": "httpTrigger",
          "name": "req",
          "direction": "in",
          "methods": [ "get" ],
          "route": "products/{category:alpha}/{id:int?}"
        },
        {
          "type": "http",
          "name": "res",
          "direction": "out"
        }
      ]
    }
```

<span data-ttu-id="8eee7-187">При такой конфигурации функция доступна по приведенному ниже маршруту вместо исходного.</span><span class="sxs-lookup"><span data-stu-id="8eee7-187">Using this configuration, the function is now addressable with the following route instead of the original route.</span></span>

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

<span data-ttu-id="8eee7-188">Это позволяет использовать в коде функции два параметра, передаваемых в адресе, — category и id.</span><span class="sxs-lookup"><span data-stu-id="8eee7-188">This allows the function code to support two parameters in the address, "category" and "id".</span></span> <span data-ttu-id="8eee7-189">Для параметров можно использовать любое [ограничение маршрута веб-API](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints).</span><span class="sxs-lookup"><span data-stu-id="8eee7-189">You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span></span> <span data-ttu-id="8eee7-190">Приведенный ниже код функции C# используют оба параметра.</span><span class="sxs-lookup"><span data-stu-id="8eee7-190">The following C# function code makes use of both parameters.</span></span>

```csharp
    public static Task<HttpResponseMessage> Run(HttpRequestMessage req, string category, int? id, 
                                                    TraceWriter log)
    {
        if (id == null)
           return  req.CreateResponse(HttpStatusCode.OK, $"All {category} items were requested.");
        else
           return  req.CreateResponse(HttpStatusCode.OK, $"{category} item with id = {id} has been requested.");
    }
```

<span data-ttu-id="8eee7-191">Ниже приведен код функции Node.js, использующей те же параметры маршрута.</span><span class="sxs-lookup"><span data-stu-id="8eee7-191">Here is Node.js function code to use the same route parameters.</span></span>

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults to 200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

<span data-ttu-id="8eee7-192">По умолчанию все маршруты функций начинаются с префикса *api*.</span><span class="sxs-lookup"><span data-stu-id="8eee7-192">By default, all function routes are prefixed with *api*.</span></span> <span data-ttu-id="8eee7-193">Вы можете настроить или удалить этот префикс с помощью свойства `http.routePrefix` в файле *host.json*.</span><span class="sxs-lookup"><span data-stu-id="8eee7-193">You can also customize or remove the prefix using the `http.routePrefix` property in your *host.json* file.</span></span> <span data-ttu-id="8eee7-194">В следующем примере префикс маршрута *api* удаляется. Он заменяется пустой строкой в файле *host.json*.</span><span class="sxs-lookup"><span data-stu-id="8eee7-194">The following example removes the *api* route prefix by using an empty string for the prefix in the *host.json* file.</span></span>

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

<span data-ttu-id="8eee7-195">Дополнительные сведения о способах обновления файла *host.json* для функции см. в разделе [Как обновить файлы приложения-функции](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="8eee7-195">For detailed information on how to update the *host.json* file for your function, See, [How to update function app files](functions-reference.md#fileupdate).</span></span> 

<span data-ttu-id="8eee7-196">Дополнительные сведения о других свойствах, которые можно настроить в файле *host.json*, см. в [справочнике по host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="8eee7-196">For information on other properties you can configure in your *host.json* file, see [host.json reference](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>


<a name="keys"></a>
## <a name="working-with-keys"></a><span data-ttu-id="8eee7-197">Работа с ключами</span><span class="sxs-lookup"><span data-stu-id="8eee7-197">Working with keys</span></span>
<span data-ttu-id="8eee7-198">Триггеры HTTP могут использовать ключи для повышения безопасности.</span><span class="sxs-lookup"><span data-stu-id="8eee7-198">HttpTriggers can leverage keys for added security.</span></span> <span data-ttu-id="8eee7-199">Стандартный триггер HTTP может использовать их в качестве ключа API, то есть требовать наличия ключа в запросе.</span><span class="sxs-lookup"><span data-stu-id="8eee7-199">A standard HttpTrigger can use these as an API key, requiring the key to be present on the request.</span></span> <span data-ttu-id="8eee7-200">Вызовы webhook могут использовать ключи для проверки подлинности запросов различными способами, в зависимости от поддерживаемых поставщиком технологий.</span><span class="sxs-lookup"><span data-stu-id="8eee7-200">Webhooks can use keys to authorize requests in a variety of ways, depending on what the provider supports.</span></span>

<span data-ttu-id="8eee7-201">Ключи хранятся в Azure в составе приложения-функции в зашифрованном виде.</span><span class="sxs-lookup"><span data-stu-id="8eee7-201">Keys are stored as part of your function app in Azure and are encrypted at rest.</span></span> <span data-ttu-id="8eee7-202">Чтобы просмотреть ключи, создать новые или сменить значения ключей, откройте на портале нужную функцию и выберите "Управление".</span><span class="sxs-lookup"><span data-stu-id="8eee7-202">To view your keys, create new ones, or roll keys to new values, navigate to one of your functions within the portal and select "Manage."</span></span> 

<span data-ttu-id="8eee7-203">Существует два типа ключей.</span><span class="sxs-lookup"><span data-stu-id="8eee7-203">There are two types of keys:</span></span>
- <span data-ttu-id="8eee7-204">**Ключи узла**, которые являются общими для всех функций в приложении-функции.</span><span class="sxs-lookup"><span data-stu-id="8eee7-204">**Host keys**: These keys are shared by all functions within the function app.</span></span> <span data-ttu-id="8eee7-205">Если такой ключ используется в качестве ключа API, он предоставляет доступ к любой функции в приложении-функции.</span><span class="sxs-lookup"><span data-stu-id="8eee7-205">When used as an API key, these allow access to any function within the function app.</span></span>
- <span data-ttu-id="8eee7-206">**Ключи функции**, которые применяются только для конкретных функций, в которых они определены.</span><span class="sxs-lookup"><span data-stu-id="8eee7-206">**Function keys**: These keys apply only to the specific functions under which they are defined.</span></span> <span data-ttu-id="8eee7-207">Если такой ключ используется в качестве ключа API, он предоставляет доступ только к определенной функции.</span><span class="sxs-lookup"><span data-stu-id="8eee7-207">When used as an API key, these only allow access to that function.</span></span>

<span data-ttu-id="8eee7-208">Каждый ключ имеет имя для удобства использования, а один из ключей (с именем default) используется как ключ по умолчанию на уровне узла и функции.</span><span class="sxs-lookup"><span data-stu-id="8eee7-208">Each key is named for reference, and there is a default key (named "default") at the function and host level.</span></span> <span data-ttu-id="8eee7-209">**Главный ключ** — это ключ узла по умолчанию (с именем _master). Он определяется для каждого приложения-функции и не может быть отозван.</span><span class="sxs-lookup"><span data-stu-id="8eee7-209">The **master key** is a default host key named "_master" that is defined for each function app and cannot be revoked.</span></span> <span data-ttu-id="8eee7-210">Он предоставляет административный доступ к API-интерфейсам среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="8eee7-210">It provides administrative access to the runtime APIs.</span></span> <span data-ttu-id="8eee7-211">Если в объекте JSON для привязки указать параметр `"authLevel": "admin"`, этот ключ должен обязательно присутствовать в запросе. Передача любого другого ключа приведет к ошибке проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="8eee7-211">Using `"authLevel": "admin"` in the binding JSON will require this key to be presented on the request; any other key will result in a authorization failure.</span></span>

> [!NOTE]
> <span data-ttu-id="8eee7-212">Главный ключ предоставляет высокий уровень разрешений, поэтому никогда не передавайте этот ключ третьим лицам и не включайте его в состав клиентских приложений.</span><span class="sxs-lookup"><span data-stu-id="8eee7-212">Due to the elevated permissions granted by the master key, you should not share this key with third parties or distribute it in native client applications.</span></span> <span data-ttu-id="8eee7-213">Соблюдайте осторожность при выборе уровня проверки подлинности для администратора.</span><span class="sxs-lookup"><span data-stu-id="8eee7-213">Exercise caution when choosing the admin authorization level.</span></span>
> 
> 

### <a name="api-key-authorization"></a><span data-ttu-id="8eee7-214">Проверка подлинности с помощью ключа API</span><span class="sxs-lookup"><span data-stu-id="8eee7-214">API key authorization</span></span>
<span data-ttu-id="8eee7-215">По умолчанию триггер HTTP требует наличия ключа API в HTTP-запросе.</span><span class="sxs-lookup"><span data-stu-id="8eee7-215">By default, an HttpTrigger requires an API key in the HTTP request.</span></span> <span data-ttu-id="8eee7-216">Поэтому HTTP-запрос обычно выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="8eee7-216">So your HTTP request normally looks like this:</span></span>

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

<span data-ttu-id="8eee7-217">Ключ можно передать в переменной строки запроса с именем `code`, как показано выше, или в заголовке HTTP `x-functions-key`.</span><span class="sxs-lookup"><span data-stu-id="8eee7-217">The key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span></span> <span data-ttu-id="8eee7-218">Значением ключа может быть любой ключ функции, определенный для запрашиваемой функции, или любой ключ узла.</span><span class="sxs-lookup"><span data-stu-id="8eee7-218">The value of the key can be any function key defined for the function, or any host key.</span></span>

<span data-ttu-id="8eee7-219">Вы можете разрешить передачу запросов без ключей или потребовать, чтобы всегда использовался главный ключ, изменив значение свойства `authLevel` в объекте JSON для привязки (см. раздел [Триггер HTTP](#httptrigger)).</span><span class="sxs-lookup"><span data-stu-id="8eee7-219">You can choose to allow requests without keys or specify that the master key must be used by changing the `authLevel` property in the binding JSON (see [HTTP trigger](#httptrigger)).</span></span>

### <a name="keys-and-webhooks"></a><span data-ttu-id="8eee7-220">Ключи и вызовы webhook</span><span class="sxs-lookup"><span data-stu-id="8eee7-220">Keys and webhooks</span></span>
<span data-ttu-id="8eee7-221">Авторизация webhook обрабатывается компонентом получателя webhook, который входит в состав триггера HTTP. Механизм обработки различается в зависимости от типа webhook.</span><span class="sxs-lookup"><span data-stu-id="8eee7-221">Webhook authorization is handled by the webhook reciever component, part of the HttpTrigger, and the mechanism varies based on the webhook type.</span></span> <span data-ttu-id="8eee7-222">Но каждый из этих механизмов использует ключи.</span><span class="sxs-lookup"><span data-stu-id="8eee7-222">Each mechanism does, however rely on a key.</span></span> <span data-ttu-id="8eee7-223">По умолчанию используется ключ функции с именем default.</span><span class="sxs-lookup"><span data-stu-id="8eee7-223">By default, the function key named "default" will be used.</span></span> <span data-ttu-id="8eee7-224">Если вы хотите использовать другой ключ, необходимо настроить поставщик webhook так, чтобы он отправлял имя ключа в составе запроса одним из следующих способов.</span><span class="sxs-lookup"><span data-stu-id="8eee7-224">If you wish to use a different key, you will need to configure the webhook provider to send the key name with the request in one of the following ways:</span></span>

- <span data-ttu-id="8eee7-225">**В строке запроса**: поставщик передает имя ключа в параметре `clientid` строки запроса (например, `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span><span class="sxs-lookup"><span data-stu-id="8eee7-225">**Query string**: The provider passes the key name in the `clientid` query string parameter (e.g., `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span></span>
- <span data-ttu-id="8eee7-226">**В заголовке запроса**: поставщик передает имя ключа в заголовке `x-functions-clientid`.</span><span class="sxs-lookup"><span data-stu-id="8eee7-226">**Request header**: The provider passes the key name in the `x-functions-clientid` header.</span></span>

> [!NOTE]
> <span data-ttu-id="8eee7-227">Ключи функций имеют приоритет над ключами узла.</span><span class="sxs-lookup"><span data-stu-id="8eee7-227">Function keys take precedence over host keys.</span></span> <span data-ttu-id="8eee7-228">Если определены два ключа с одним именем, будет использоваться ключ функции.</span><span class="sxs-lookup"><span data-stu-id="8eee7-228">If two keys are defined with the same name, the function key will be used.</span></span>
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a><span data-ttu-id="8eee7-229">Образцы триггеров HTTP</span><span class="sxs-lookup"><span data-stu-id="8eee7-229">HTTP trigger samples</span></span>
<span data-ttu-id="8eee7-230">Предположим, что вы определили следующий триггер HTTP в массиве `bindings` файла function.json:</span><span class="sxs-lookup"><span data-stu-id="8eee7-230">Suppose you have the following HTTP trigger in the `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

<span data-ttu-id="8eee7-231">Выберите пример для конкретного языка, который выполняет поиск параметра `name` в строке запроса или в тексте HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="8eee7-231">See the language-specific sample that looks for a `name` parameter either in the query string or the body of the HTTP request.</span></span>

* [<span data-ttu-id="8eee7-232">C#</span><span class="sxs-lookup"><span data-stu-id="8eee7-232">C#</span></span>](#httptriggercsharp)
* [<span data-ttu-id="8eee7-233">F#</span><span class="sxs-lookup"><span data-stu-id="8eee7-233">F#</span></span>](#httptriggerfsharp)
* [<span data-ttu-id="8eee7-234">Node.js</span><span class="sxs-lookup"><span data-stu-id="8eee7-234">Node.js</span></span>](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a><span data-ttu-id="8eee7-235">Пример триггера HTTP на языке C#</span><span class="sxs-lookup"><span data-stu-id="8eee7-235">HTTP trigger sample in C#</span></span> #
```csharp
using System.Net;
using System.Threading.Tasks;

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
{
    log.Info($"C# HTTP trigger function processed a request. RequestUri={req.RequestUri}");

    // parse query parameter
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    // Get request body
    dynamic data = await req.Content.ReadAsAsync<object>();

    // Set name to query string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on the query string or in the request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

<span data-ttu-id="8eee7-236">Также можно выполнить привязку к POCO вместо `HttpRequestMessage`.</span><span class="sxs-lookup"><span data-stu-id="8eee7-236">You can also bind to a POCO instead of `HttpRequestMessage`.</span></span> <span data-ttu-id="8eee7-237">Будет выполнена расконсервация из тела запроса, интерпретированного как JSON.</span><span class="sxs-lookup"><span data-stu-id="8eee7-237">This will be hydrated from the body of the request, parsed as JSON.</span></span> <span data-ttu-id="8eee7-238">Аналогичным образом тип можно передать в привязку вывода ответа HTTP; результатом будет тело ответа с кодом состояния 200.</span><span class="sxs-lookup"><span data-stu-id="8eee7-238">Similarly, a type can be passed to the HTTP response output binding, and this will be returned as the response body, with a 200 status code.</span></span>
```csharp
using System.Net;
using System.Threading.Tasks;

public static string Run(CustomObject req, TraceWriter log)
{
    return "Hello " + req?.name;
}

public class CustomObject {
     public String name {get; set;}
}
}
```

<a name="httptriggerfsharp"></a>
### <a name="http-trigger-sample-in-f"></a><span data-ttu-id="8eee7-239">Пример триггера HTTP на языке F#</span><span class="sxs-lookup"><span data-stu-id="8eee7-239">HTTP trigger sample in F#</span></span> #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic

let Run(req: HttpRequestMessage) =
    async {
        let q =
            req.GetQueryNameValuePairs()
                |> Seq.tryFind (fun kv -> kv.Key = "name")
        match q with
        | Some kv ->
            return req.CreateResponse(HttpStatusCode.OK, "Hello " + kv.Value)
        | None ->
            let! data = Async.AwaitTask(req.Content.ReadAsAsync<obj>())
            try
                return req.CreateResponse(HttpStatusCode.OK, "Hello " + data?name)
            with e ->
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on the query string or in the request body")
    } |> Async.StartAsTask
```

<span data-ttu-id="8eee7-240">Вам потребуется файл `project.json`, который использует NuGet для ссылки на сборки `FSharp.Interop.Dynamic` и `Dynamitey`, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="8eee7-240">You need a `project.json` file that uses NuGet to reference the `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, like this:</span></span>

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

<span data-ttu-id="8eee7-241">С помощью NuGet файл извлекает зависимости и создает на них ссылки в сценарии.</span><span class="sxs-lookup"><span data-stu-id="8eee7-241">This will use NuGet to fetch your dependencies and will reference them in your script.</span></span>

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a><span data-ttu-id="8eee7-242">Пример триггера HTTP для Node.js</span><span class="sxs-lookup"><span data-stu-id="8eee7-242">HTTP trigger sample in Node.JS</span></span>
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults to 200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on the query string or in the request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a><span data-ttu-id="8eee7-243">Примеры вызовов webhook</span><span class="sxs-lookup"><span data-stu-id="8eee7-243">Webhook samples</span></span>
<span data-ttu-id="8eee7-244">Предположим, что вы определили следующий триггер webhook в массиве `bindings` файла function.json:</span><span class="sxs-lookup"><span data-stu-id="8eee7-244">Suppose you have the following webhook trigger in the `bindings` array of function.json:</span></span>

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

<span data-ttu-id="8eee7-245">Выберите пример для конкретного языка, который регистрирует комментарии о проблемах на GitHub.</span><span class="sxs-lookup"><span data-stu-id="8eee7-245">See the language-specific sample that logs GitHub issue comments.</span></span>

* [<span data-ttu-id="8eee7-246">C#</span><span class="sxs-lookup"><span data-stu-id="8eee7-246">C#</span></span>](#hooktriggercsharp)
* [<span data-ttu-id="8eee7-247">F#</span><span class="sxs-lookup"><span data-stu-id="8eee7-247">F#</span></span>](#hooktriggerfsharp)
* [<span data-ttu-id="8eee7-248">Node.js</span><span class="sxs-lookup"><span data-stu-id="8eee7-248">Node.js</span></span>](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a><span data-ttu-id="8eee7-249">Пример веб-перехватчика на языке C#</span><span class="sxs-lookup"><span data-stu-id="8eee7-249">Webhook sample in C#</span></span> #
```csharp
#r "Newtonsoft.Json"

using System;
using System.Net;
using System.Threading.Tasks;
using Newtonsoft.Json;

public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
{
    string jsonContent = await req.Content.ReadAsStringAsync();
    dynamic data = JsonConvert.DeserializeObject(jsonContent);

    log.Info($"WebHook was triggered! Comment: {data.comment.body}");

    return req.CreateResponse(HttpStatusCode.OK, new {
        body = $"New GitHub comment: {data.comment.body}"
    });
}
```

<a name="hooktriggerfsharp"></a>

### <a name="webhook-sample-in-f"></a><span data-ttu-id="8eee7-250">Пример веб-перехватчика на языке F#</span><span class="sxs-lookup"><span data-stu-id="8eee7-250">Webhook sample in F#</span></span> #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Response = {
    body: string
}

let Run(req: HttpRequestMessage, log: TraceWriter) =
    async {
        let! content = req.Content.ReadAsStringAsync() |> Async.AwaitTask
        let data = content |> JsonConvert.DeserializeObject
        log.Info(sprintf "GitHub WebHook triggered! %s" data?comment?body)
        return req.CreateResponse(
            HttpStatusCode.OK,
            { body = sprintf "New GitHub comment: %s" data?comment?body })
    } |> Async.StartAsTask
```

<a name="hooktriggernodejs"></a>

### <a name="webhook-sample-in-nodejs"></a><span data-ttu-id="8eee7-251">Пример webhook для Node.js</span><span class="sxs-lookup"><span data-stu-id="8eee7-251">Webhook sample in Node.JS</span></span>
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a><span data-ttu-id="8eee7-252">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8eee7-252">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

