---
title: "привязки функции HTTP и веб-перехватчика aaaAzure | Документы Microsoft"
description: "Понять, каким образом toouse HTTP и веб-перехватчика триггеры и привязки в функциях Azure."
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
ms.openlocfilehash: c23b7a1443d492ed78c595e97d1d778a7ab12416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a><span data-ttu-id="0f12d-104">Привязки HTTP и webhook в функциях Azure</span><span class="sxs-lookup"><span data-stu-id="0f12d-104">Azure Functions HTTP and webhook bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="0f12d-105">В этой статье объясняется, как триггеры tooconfigure и работа с HTTP и привязками в функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="0f12d-105">This article explains how tooconfigure and work with HTTP triggers and bindings in Azure Functions.</span></span>
<span data-ttu-id="0f12d-106">С этими можно использовать функции Azure toobuild без сервера API-интерфейсов и отправки ответа toowebhooks.</span><span class="sxs-lookup"><span data-stu-id="0f12d-106">With these, you can use Azure Functions toobuild serverless APIs and respond toowebhooks.</span></span>

<span data-ttu-id="0f12d-107">Функции Azure предоставляет следующие привязки hello:</span><span class="sxs-lookup"><span data-stu-id="0f12d-107">Azure Functions provides hello following bindings:</span></span>
- <span data-ttu-id="0f12d-108">[Триггер HTTP](#httptrigger) позволяет вызвать функцию с помощью HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="0f12d-108">An [HTTP trigger](#httptrigger) lets you invoke a function with an HTTP request.</span></span> <span data-ttu-id="0f12d-109">Это может быть слишком настраиваемые toorespond[веб-перехватчиков](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="0f12d-109">This can be customized toorespond too[webhooks](#hooktrigger).</span></span>
- <span data-ttu-id="0f12d-110">[Привязка для вывода HTTP](#output) позволяет toorespond toohello запроса.</span><span class="sxs-lookup"><span data-stu-id="0f12d-110">An [HTTP output binding](#output) allows you toorespond toohello request.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a><span data-ttu-id="0f12d-111">Триггер HTTP</span><span class="sxs-lookup"><span data-stu-id="0f12d-111">HTTP trigger</span></span>
<span data-ttu-id="0f12d-112">функция будет выполняться в триггер HTTP Hello в ответ tooan HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="0f12d-112">hello HTTP trigger will execute your function in response tooan HTTP request.</span></span> <span data-ttu-id="0f12d-113">Его можно настраивать определенный URL-адрес toorespond tooa или набор методов HTTP.</span><span class="sxs-lookup"><span data-stu-id="0f12d-113">You can customize it toorespond tooa particular URL or set of HTTP methods.</span></span> <span data-ttu-id="0f12d-114">Триггер HTTP также может быть настроенный toorespond toowebhooks.</span><span class="sxs-lookup"><span data-stu-id="0f12d-114">An HTTP trigger can also be configured toorespond toowebhooks.</span></span> 

<span data-ttu-id="0f12d-115">Если с помощью портала функции hello, можно также начинается немедленно с помощью готового шаблона.</span><span class="sxs-lookup"><span data-stu-id="0f12d-115">If using hello Functions portal, you can also get started right away using a pre-made template.</span></span> <span data-ttu-id="0f12d-116">Выберите **новая функция** и выберите команду «Веб-перехватчиков & API» hello **сценарий** раскрывающегося списка.</span><span class="sxs-lookup"><span data-stu-id="0f12d-116">Select **New function** and choose "API & Webhooks" from hello **Scenario** dropdown.</span></span> <span data-ttu-id="0f12d-117">Выберите один из шаблонов hello и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="0f12d-117">Select one of hello templates and click **Create**.</span></span>

<span data-ttu-id="0f12d-118">По умолчанию триггер HTTP будет отвечать toohello запрос с кодом состояния HTTP 200 OK и пустой текст.</span><span class="sxs-lookup"><span data-stu-id="0f12d-118">By default, an HTTP trigger will respond toohello request with an HTTP 200 OK status code and an empty body.</span></span> <span data-ttu-id="0f12d-119">toomodify ответ hello, настройте [привязка для вывода HTTP](#output)</span><span class="sxs-lookup"><span data-stu-id="0f12d-119">toomodify hello response, configure an [HTTP output binding](#output)</span></span>

### <a name="configuring-an-http-trigger"></a><span data-ttu-id="0f12d-120">Настройка триггера HTTP</span><span class="sxs-lookup"><span data-stu-id="0f12d-120">Configuring an HTTP trigger</span></span>
<span data-ttu-id="0f12d-121">Определен триггер HTTP, включая JSON объект аналогичные toohello, выполнив в hello `bindings` массив function.json:</span><span class="sxs-lookup"><span data-stu-id="0f12d-121">An HTTP trigger is defined by including a JSON object similar toohello following in hello `bindings` array of function.json:</span></span>

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
<span data-ttu-id="0f12d-122">Привязка Hello поддерживает hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="0f12d-122">hello binding supports hello following properties:</span></span>

* <span data-ttu-id="0f12d-123">**имя** : требуется "-" hello переменной имя, используемое в коде функция для запроса hello или текст запроса.</span><span class="sxs-lookup"><span data-stu-id="0f12d-123">**name** : Required - hello variable name used in function code for hello request or request body.</span></span> <span data-ttu-id="0f12d-124">См. раздел [Использование триггера HTTP в коде программы](#httptriggerusage).</span><span class="sxs-lookup"><span data-stu-id="0f12d-124">See [Working with an HTTP trigger from code](#httptriggerusage).</span></span>
* <span data-ttu-id="0f12d-125">**Тип** : требуется — должен быть задан слишком «httpTrigger».</span><span class="sxs-lookup"><span data-stu-id="0f12d-125">**type** : Required - must be set too"httpTrigger".</span></span>
* <span data-ttu-id="0f12d-126">**Направление** : требуется - должно быть задано слишком «in».</span><span class="sxs-lookup"><span data-stu-id="0f12d-126">**direction** : Required - must be set too"in".</span></span>
* <span data-ttu-id="0f12d-127">_authLevel_ : Определяет, какие ключи, должны toobe есть в запросе hello в функции hello tooinvoke заказа.</span><span class="sxs-lookup"><span data-stu-id="0f12d-127">_authLevel_ : This determines what keys, if any, need toobe present on hello request in order tooinvoke hello function.</span></span> <span data-ttu-id="0f12d-128">См. раздел [Работа с ключами](#keys) далее в этой статье.</span><span class="sxs-lookup"><span data-stu-id="0f12d-128">See [Working with keys](#keys) below.</span></span> <span data-ttu-id="0f12d-129">Hello значение может быть одним из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="0f12d-129">hello value can be one of hello following:</span></span>
    * <span data-ttu-id="0f12d-130">_anonymous_: ключи API не требуются.</span><span class="sxs-lookup"><span data-stu-id="0f12d-130">_anonymous_: No API key is required.</span></span>
    * <span data-ttu-id="0f12d-131">_function_: требуется ключ API для конкретной функции.</span><span class="sxs-lookup"><span data-stu-id="0f12d-131">_function_: A function-specific API key is required.</span></span> <span data-ttu-id="0f12d-132">Это значение по умолчанию hello, если не указан.</span><span class="sxs-lookup"><span data-stu-id="0f12d-132">This is hello default value if none is provided.</span></span>
    * <span data-ttu-id="0f12d-133">_Администратор_ : hello главный ключ не требуется.</span><span class="sxs-lookup"><span data-stu-id="0f12d-133">_admin_ : hello master key is required.</span></span>
* <span data-ttu-id="0f12d-134">**методы** : это массив будет отвечать функции hello toowhich методы hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="0f12d-134">**methods** : This is an array of hello HTTP methods toowhich hello function will respond.</span></span> <span data-ttu-id="0f12d-135">Если не указано, функция hello ответит tooall HTTP-методов.</span><span class="sxs-lookup"><span data-stu-id="0f12d-135">If not specified, hello function will respond tooall HTTP methods.</span></span> <span data-ttu-id="0f12d-136">В разделе [Настройка конечной точки hello HTTP](#url).</span><span class="sxs-lookup"><span data-stu-id="0f12d-136">See [Customizing hello HTTP endpoint](#url).</span></span>
* <span data-ttu-id="0f12d-137">**маршрут** : Определяет шаблон маршрута hello, управление toowhich URL-адресов будет отвечать функции запроса.</span><span class="sxs-lookup"><span data-stu-id="0f12d-137">**route** : This defines hello route template, controlling toowhich request URLs your function will respond.</span></span> <span data-ttu-id="0f12d-138">Hello значение по умолчанию, если не указан — `<functionname>`.</span><span class="sxs-lookup"><span data-stu-id="0f12d-138">hello default value if none is provided is `<functionname>`.</span></span> <span data-ttu-id="0f12d-139">В разделе [Настройка конечной точки hello HTTP](#url).</span><span class="sxs-lookup"><span data-stu-id="0f12d-139">See [Customizing hello HTTP endpoint](#url).</span></span>
* <span data-ttu-id="0f12d-140">**webHookType** : Это настраивает tooact триггер hello HTTP в качестве веб-перехватчика получателем для указанного поставщика hello.</span><span class="sxs-lookup"><span data-stu-id="0f12d-140">**webHookType** : This configures hello HTTP trigger tooact as a webhook reciever for hello specified provider.</span></span> <span data-ttu-id="0f12d-141">Hello _методы_ свойство не должно быть установлено, если вы выбрали это.</span><span class="sxs-lookup"><span data-stu-id="0f12d-141">hello _methods_ property should not be set if this is chosen.</span></span> <span data-ttu-id="0f12d-142">В разделе [toowebhooks отвечает](#hooktrigger).</span><span class="sxs-lookup"><span data-stu-id="0f12d-142">See [Responding toowebhooks](#hooktrigger).</span></span> <span data-ttu-id="0f12d-143">Hello значение может быть одним из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="0f12d-143">hello value can be one of hello following:</span></span>
    * <span data-ttu-id="0f12d-144">_genericJson_: конечная точка webhook общего назначения без логики для конкретного поставщика.</span><span class="sxs-lookup"><span data-stu-id="0f12d-144">_genericJson_ : A general purpose webhook endpoint without logic for a specific provider.</span></span>
    * <span data-ttu-id="0f12d-145">_github_ : функции hello ответит tooGitHub веб-привязок.</span><span class="sxs-lookup"><span data-stu-id="0f12d-145">_github_ : hello function will respond tooGitHub webhooks.</span></span> <span data-ttu-id="0f12d-146">Hello _authLevel_ свойство не должно быть установлено, если вы выбрали это.</span><span class="sxs-lookup"><span data-stu-id="0f12d-146">hello _authLevel_ property should not be set if this is chosen.</span></span>
    * <span data-ttu-id="0f12d-147">_резерв_ : функции hello ответит tooSlack веб-привязок.</span><span class="sxs-lookup"><span data-stu-id="0f12d-147">_slack_ : hello function will respond tooSlack webhooks.</span></span> <span data-ttu-id="0f12d-148">Hello _authLevel_ свойство не должно быть установлено, если вы выбрали это.</span><span class="sxs-lookup"><span data-stu-id="0f12d-148">hello _authLevel_ property should not be set if this is chosen.</span></span>

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a><span data-ttu-id="0f12d-149">Использование триггера HTTP в коде программы</span><span class="sxs-lookup"><span data-stu-id="0f12d-149">Working with an HTTP trigger from code</span></span>
<span data-ttu-id="0f12d-150">Для функции C# и F #, можно объявить тип входного toobe ваш триггер hello либо `HttpRequestMessage` или пользовательского типа.</span><span class="sxs-lookup"><span data-stu-id="0f12d-150">For C# and F# functions, you can declare hello type of your trigger input toobe either `HttpRequestMessage` or a custom type.</span></span> <span data-ttu-id="0f12d-151">При выборе `HttpRequestMessage`, а затем получите объект запроса toohello полный доступ.</span><span class="sxs-lookup"><span data-stu-id="0f12d-151">If you choose `HttpRequestMessage`, then you will get full access toohello request object.</span></span> <span data-ttu-id="0f12d-152">Для пользовательского типа (например, POCO) функции попытается текст запроса hello tooparse как свойства объекта JSON toopopulate hello.</span><span class="sxs-lookup"><span data-stu-id="0f12d-152">For a custom type (such as a POCO), Functions will attempt tooparse hello request body as JSON toopopulate hello object properties.</span></span>

<span data-ttu-id="0f12d-153">Для функций, Node.js среда выполнения функции hello предоставляет текст hello запроса вместо hello объекта запроса.</span><span class="sxs-lookup"><span data-stu-id="0f12d-153">For Node.js functions, hello Functions runtime provides hello request body instead of hello request object.</span></span>

<span data-ttu-id="0f12d-154">В разделе [Образцы триггеров HTTP](#httptriggersample) приводятся примеры использования.</span><span class="sxs-lookup"><span data-stu-id="0f12d-154">See [HTTP trigger samples](#httptriggersample) for example usages.</span></span>


<a name="output"></a>
## <a name="http-response-output-binding"></a><span data-ttu-id="0f12d-155">Привязка для вывода HTTP-ответа</span><span class="sxs-lookup"><span data-stu-id="0f12d-155">HTTP response output binding</span></span>
<span data-ttu-id="0f12d-156">Используйте hello HTTP выходные данные привязки toorespond toohello HTTP отправитель запроса.</span><span class="sxs-lookup"><span data-stu-id="0f12d-156">Use hello HTTP output binding toorespond toohello HTTP request sender.</span></span> <span data-ttu-id="0f12d-157">Эта привязка требует триггер HTTP и позволяет toocustomize hello ответа, связанного с запрос hello триггера.</span><span class="sxs-lookup"><span data-stu-id="0f12d-157">This binding requires an HTTP trigger and allows you toocustomize hello response associated with hello trigger's request.</span></span> <span data-ttu-id="0f12d-158">Если привязка для вывода HTTP отсутствует, триггер HTTP возвращает ответ HTTP "200 ОК" с пустым текстом.</span><span class="sxs-lookup"><span data-stu-id="0f12d-158">If an HTTP output binding is not provided, an HTTP trigger will return HTTP 200 OK with an empty body.</span></span> 

### <a name="configuring-an-http-output-binding"></a><span data-ttu-id="0f12d-159">Настройка привязки для вывода HTTP</span><span class="sxs-lookup"><span data-stu-id="0f12d-159">Configuring an HTTP output binding</span></span>
<span data-ttu-id="0f12d-160">выходные данные Hello HTTP, включая JSON объект аналогичные toohello, выполнив в hello определена привязка `bindings` массив function.json:</span><span class="sxs-lookup"><span data-stu-id="0f12d-160">hello HTTP output binding is defined by including a JSON object similar toohello following in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
<span data-ttu-id="0f12d-161">Привязка Hello содержит hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="0f12d-161">hello binding contains hello following properties:</span></span>

* <span data-ttu-id="0f12d-162">**имя** : требуется — имя переменной, используемые в коде функция в ответе hello "hello".</span><span class="sxs-lookup"><span data-stu-id="0f12d-162">**name** : Required - hello variable name used in function code for hello response.</span></span> <span data-ttu-id="0f12d-163">См. раздел [Работа с привязкой для вывода HTTP в коде программы](#outputusage).</span><span class="sxs-lookup"><span data-stu-id="0f12d-163">See [Working with an HTTP output binding from code](#outputusage).</span></span>
* <span data-ttu-id="0f12d-164">**Тип** : требуется — должен быть задан слишком «http».</span><span class="sxs-lookup"><span data-stu-id="0f12d-164">**type** : Required - must be set too"http".</span></span>
* <span data-ttu-id="0f12d-165">**Направление** : требуется - должно быть задано слишком «out».</span><span class="sxs-lookup"><span data-stu-id="0f12d-165">**direction** : Required - must be set too"out".</span></span>

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a><span data-ttu-id="0f12d-166">Работа с привязкой для вывода HTTP в коде программы</span><span class="sxs-lookup"><span data-stu-id="0f12d-166">Working with an HTTP output binding from code</span></span>
<span data-ttu-id="0f12d-167">Можно использовать hello выходной параметр (например, «res») toorespond toohello http или веб-перехватчика вызывающего объекта.</span><span class="sxs-lookup"><span data-stu-id="0f12d-167">You can use hello output parameter (e.g., "res") toorespond toohello http or webhook caller.</span></span> <span data-ttu-id="0f12d-168">Кроме того, можно использовать стандартные `Request.CreateResponse()` (C#) или `context.res` (Node.JS) шаблон tooreturn ответ пользователя.</span><span class="sxs-lookup"><span data-stu-id="0f12d-168">Alternatively, you can use the standard `Request.CreateResponse()` (C#) or `context.res` (Node.JS) pattern tooreturn your response.</span></span> <span data-ttu-id="0f12d-169">Примеры как toouse hello последний метод см. в разделе [образцы триггер HTTP](#httptriggersample) и [образцы триггер веб-перехватчика](#hooktriggersample).</span><span class="sxs-lookup"><span data-stu-id="0f12d-169">For examples on how toouse hello latter method, see [HTTP trigger samples](#httptriggersample) and [Webhook trigger samples](#hooktriggersample).</span></span>


<a name="hooktrigger"></a>
## <a name="responding-toowebhooks"></a><span data-ttu-id="0f12d-170">Отвечать на запросы toowebhooks</span><span class="sxs-lookup"><span data-stu-id="0f12d-170">Responding toowebhooks</span></span>
<span data-ttu-id="0f12d-171">Триггер HTTP с hello _webHookType_ свойство будет иметь настроенное toorespond слишком[веб-перехватчиков](https://en.wikipedia.org/wiki/Webhook).</span><span class="sxs-lookup"><span data-stu-id="0f12d-171">An HTTP trigger with hello _webHookType_ property will be configured toorespond too[webhooks](https://en.wikipedia.org/wiki/Webhook).</span></span> <span data-ttu-id="0f12d-172">Основная конфигурация Hello использует параметр «genericJson» hello.</span><span class="sxs-lookup"><span data-stu-id="0f12d-172">hello basic configuration uses hello "genericJson" setting.</span></span> <span data-ttu-id="0f12d-173">Это ограничивает запросы tooonly их с помощью HTTP POST и с hello `application/json` тип содержимого.</span><span class="sxs-lookup"><span data-stu-id="0f12d-173">This restricts requests tooonly those using HTTP POST and with hello `application/json` content type.</span></span>

<span data-ttu-id="0f12d-174">Hello триггер Кроме того можно специально настроенные tooa конкретного веб-перехватчика поставщика (например, [GitHub](https://developer.github.com/webhooks/) и [Slack](https://api.slack.com/outgoing-webhooks)).</span><span class="sxs-lookup"><span data-stu-id="0f12d-174">hello trigger can additionally be tailored tooa specific webhook provider (e.g., [GitHub](https://developer.github.com/webhooks/) and [Slack](https://api.slack.com/outgoing-webhooks)).</span></span> <span data-ttu-id="0f12d-175">Если указан поставщик, среда выполнения функции hello заняться hello поставщика логику проверки для вас.</span><span class="sxs-lookup"><span data-stu-id="0f12d-175">If a provider is specified, hello Functions runtime can take care of hello provider's validation logic for you.</span></span>  

### <a name="configuring-github-as-a-webhook-provider"></a><span data-ttu-id="0f12d-176">Настройка GitHub в качестве поставщика webhook</span><span class="sxs-lookup"><span data-stu-id="0f12d-176">Configuring GitHub as a webhook provider</span></span>
<span data-ttu-id="0f12d-177">веб-привязок tooGitHub toorespond, сначала создайте функции с триггером HTTP и задайте hello _webHookType_ свойство слишком «github».</span><span class="sxs-lookup"><span data-stu-id="0f12d-177">toorespond tooGitHub webhooks, first create your function with an HTTP Trigger, and set hello _webHookType_ property too"github".</span></span> <span data-ttu-id="0f12d-178">Затем скопируйте его [URL-адрес](#url) и [ключ API](#keys) в репозиторий GitHub, используя страницу **Добавить веб-перехватчик**.</span><span class="sxs-lookup"><span data-stu-id="0f12d-178">Then copy its [URL](#url) and [API key](#keys) into your GitHub repository's **Add webhook** page.</span></span> <span data-ttu-id="0f12d-179">Дополнительные сведения см. в разделе документации GitHub [о создании webhook](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="0f12d-179">See GitHub's [Creating Webhooks](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentation for more.</span></span>

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a><span data-ttu-id="0f12d-180">Настройка Slack в качестве поставщика webhook</span><span class="sxs-lookup"><span data-stu-id="0f12d-180">Configuring Slack as a webhook provider</span></span>
<span data-ttu-id="0f12d-181">Резерв Hello веб-перехватчика создается маркер вместо позволяет указать, поэтому необходимо настроить ключ конкретными функциями с маркером hello из Slack.</span><span class="sxs-lookup"><span data-stu-id="0f12d-181">hello Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with hello token from Slack.</span></span> <span data-ttu-id="0f12d-182">См. раздел [Работа с ключами](#keys).</span><span class="sxs-lookup"><span data-stu-id="0f12d-182">See [Working with keys](#keys).</span></span>

<a name="url"></a>
## <a name="customizing-hello-http-endpoint"></a><span data-ttu-id="0f12d-183">Настройка конечной точки HTTP hello</span><span class="sxs-lookup"><span data-stu-id="0f12d-183">Customizing hello HTTP endpoint</span></span>
<span data-ttu-id="0f12d-184">По умолчанию при создании функции для триггера HTTP или веб-перехватчика, функции hello адресуемые с маршрутом hello формы:</span><span class="sxs-lookup"><span data-stu-id="0f12d-184">By default when you create a function for an HTTP trigger, or WebHook, hello function is addressable with a route of hello form:</span></span>

    http://<yourapp>.azurewebsites.net/api/<funcname> 

<span data-ttu-id="0f12d-185">Вы можете настроить этот маршрут, используя необязательный hello `route` свойство в триггере hello HTTP входных привязки.</span><span class="sxs-lookup"><span data-stu-id="0f12d-185">You can customize this route using hello optional `route` property on hello HTTP trigger's input binding.</span></span> <span data-ttu-id="0f12d-186">Пример: hello следующие *function.json* файл определяет `route` свойство для триггера HTTP:</span><span class="sxs-lookup"><span data-stu-id="0f12d-186">As an example, hello following *function.json* file defines a `route` property for an HTTP trigger:</span></span>

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

<span data-ttu-id="0f12d-187">Используя эту конфигурацию, функции hello теперь адресуемый с hello следующий маршрут вместо hello исходный маршрут.</span><span class="sxs-lookup"><span data-stu-id="0f12d-187">Using this configuration, hello function is now addressable with hello following route instead of hello original route.</span></span>

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

<span data-ttu-id="0f12d-188">Это позволяет коду функции hello toosupport двух параметров в адрес hello, «категория» и «id».</span><span class="sxs-lookup"><span data-stu-id="0f12d-188">This allows hello function code toosupport two parameters in hello address, "category" and "id".</span></span> <span data-ttu-id="0f12d-189">Для параметров можно использовать любое [ограничение маршрута веб-API](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints).</span><span class="sxs-lookup"><span data-stu-id="0f12d-189">You can use any [Web API Route Constraint](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) with your parameters.</span></span> <span data-ttu-id="0f12d-190">Здравствуйте, следующие функции кода C# используются оба параметра.</span><span class="sxs-lookup"><span data-stu-id="0f12d-190">hello following C# function code makes use of both parameters.</span></span>

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

<span data-ttu-id="0f12d-191">Ниже приведен код toouse Node.js функции hello такими же параметрами маршрута.</span><span class="sxs-lookup"><span data-stu-id="0f12d-191">Here is Node.js function code toouse hello same route parameters.</span></span>

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

<span data-ttu-id="0f12d-192">По умолчанию все маршруты функций начинаются с префикса *api*.</span><span class="sxs-lookup"><span data-stu-id="0f12d-192">By default, all function routes are prefixed with *api*.</span></span> <span data-ttu-id="0f12d-193">Также можно настроить или удалить с помощью hello префикс hello `http.routePrefix` свойство в вашей *host.json* файла.</span><span class="sxs-lookup"><span data-stu-id="0f12d-193">You can also customize or remove hello prefix using hello `http.routePrefix` property in your *host.json* file.</span></span> <span data-ttu-id="0f12d-194">Hello следующий пример удаляет hello *api* префикс маршрута, используя пустую строку для префикса hello в hello *host.json* файла.</span><span class="sxs-lookup"><span data-stu-id="0f12d-194">hello following example removes hello *api* route prefix by using an empty string for hello prefix in hello *host.json* file.</span></span>

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

<span data-ttu-id="0f12d-195">Подробные сведения о том, как tooupdate hello *host.json* файл функции, см. в разделе [как tooupdate функция файлов приложения](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="0f12d-195">For detailed information on how tooupdate hello *host.json* file for your function, See, [How tooupdate function app files](functions-reference.md#fileupdate).</span></span> 

<span data-ttu-id="0f12d-196">Дополнительные сведения о других свойствах, которые можно настроить в файле *host.json*, см. в [справочнике по host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="0f12d-196">For information on other properties you can configure in your *host.json* file, see [host.json reference](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>


<a name="keys"></a>
## <a name="working-with-keys"></a><span data-ttu-id="0f12d-197">Работа с ключами</span><span class="sxs-lookup"><span data-stu-id="0f12d-197">Working with keys</span></span>
<span data-ttu-id="0f12d-198">Триггеры HTTP могут использовать ключи для повышения безопасности.</span><span class="sxs-lookup"><span data-stu-id="0f12d-198">HttpTriggers can leverage keys for added security.</span></span> <span data-ttu-id="0f12d-199">Стандартная HttpTrigger можно использовать как ключ API требует hello ключа toobe есть в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="0f12d-199">A standard HttpTrigger can use these as an API key, requiring hello key toobe present on hello request.</span></span> <span data-ttu-id="0f12d-200">Веб-привязок можно использовать ключи tooauthorize запросы различными способами, в зависимости от того, какой поставщик hello поддерживает.</span><span class="sxs-lookup"><span data-stu-id="0f12d-200">Webhooks can use keys tooauthorize requests in a variety of ways, depending on what hello provider supports.</span></span>

<span data-ttu-id="0f12d-201">Ключи хранятся в Azure в составе приложения-функции в зашифрованном виде.</span><span class="sxs-lookup"><span data-stu-id="0f12d-201">Keys are stored as part of your function app in Azure and are encrypted at rest.</span></span> <span data-ttu-id="0f12d-202">tooview ключей необходимо создать новые или toonew значения ключей данных наката, перейдите tooone функций hello портале и выберите «Управление».</span><span class="sxs-lookup"><span data-stu-id="0f12d-202">tooview your keys, create new ones, or roll keys toonew values, navigate tooone of your functions within hello portal and select "Manage."</span></span> 

<span data-ttu-id="0f12d-203">Существует два типа ключей.</span><span class="sxs-lookup"><span data-stu-id="0f12d-203">There are two types of keys:</span></span>
- <span data-ttu-id="0f12d-204">**Ключи узла**: эти ключи являются общими для всех функций в приложение функции hello.</span><span class="sxs-lookup"><span data-stu-id="0f12d-204">**Host keys**: These keys are shared by all functions within hello function app.</span></span> <span data-ttu-id="0f12d-205">Если используется как ключ API, они позволяют функция tooany доступ в приложении функции hello.</span><span class="sxs-lookup"><span data-stu-id="0f12d-205">When used as an API key, these allow access tooany function within hello function app.</span></span>
- <span data-ttu-id="0f12d-206">**Функциональные клавиши**: эти ключи применяются только toohello определенные функции в которых они определены.</span><span class="sxs-lookup"><span data-stu-id="0f12d-206">**Function keys**: These keys apply only toohello specific functions under which they are defined.</span></span> <span data-ttu-id="0f12d-207">При использовании в качестве ключа API, эти только разрешить toothat функции доступа.</span><span class="sxs-lookup"><span data-stu-id="0f12d-207">When used as an API key, these only allow access toothat function.</span></span>

<span data-ttu-id="0f12d-208">Каждый ключ имеет имя для ссылки и отсутствует ключ по умолчанию (с именем «default») на уровне функций и узла hello.</span><span class="sxs-lookup"><span data-stu-id="0f12d-208">Each key is named for reference, and there is a default key (named "default") at hello function and host level.</span></span> <span data-ttu-id="0f12d-209">Hello **главный ключ** ключ узла по умолчанию с именем «_master», определенное для каждой функции приложения и не может быть отменено.</span><span class="sxs-lookup"><span data-stu-id="0f12d-209">hello **master key** is a default host key named "_master" that is defined for each function app and cannot be revoked.</span></span> <span data-ttu-id="0f12d-210">Он предоставляет административный доступ toohello API среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="0f12d-210">It provides administrative access toohello runtime APIs.</span></span> <span data-ttu-id="0f12d-211">С помощью `"authLevel": "admin"` в hello привязки JSON потребует этого ключа toobe, представленные в запросе hello; ошибка авторизации приведет к любой другой ключ.</span><span class="sxs-lookup"><span data-stu-id="0f12d-211">Using `"authLevel": "admin"` in hello binding JSON will require this key toobe presented on hello request; any other key will result in a authorization failure.</span></span>

> [!NOTE]
> <span data-ttu-id="0f12d-212">Из-за toohello повышенные разрешения, предоставляемые hello главный ключ базы данных не следует предоставлять этот ключ третьим лицам или распространять его в собственные клиентские приложения.</span><span class="sxs-lookup"><span data-stu-id="0f12d-212">Due toohello elevated permissions granted by hello master key, you should not share this key with third parties or distribute it in native client applications.</span></span> <span data-ttu-id="0f12d-213">Соблюдайте осторожность при выборе уровень авторизации администратора hello.</span><span class="sxs-lookup"><span data-stu-id="0f12d-213">Exercise caution when choosing hello admin authorization level.</span></span>
> 
> 

### <a name="api-key-authorization"></a><span data-ttu-id="0f12d-214">Проверка подлинности с помощью ключа API</span><span class="sxs-lookup"><span data-stu-id="0f12d-214">API key authorization</span></span>
<span data-ttu-id="0f12d-215">По умолчанию HttpTrigger требуется ключ API в HTTP-запросе hello.</span><span class="sxs-lookup"><span data-stu-id="0f12d-215">By default, an HttpTrigger requires an API key in hello HTTP request.</span></span> <span data-ttu-id="0f12d-216">Поэтому HTTP-запрос обычно выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0f12d-216">So your HTTP request normally looks like this:</span></span>

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

<span data-ttu-id="0f12d-217">Hello ключ может быть включено в переменную строки запроса с именем `code`, как описано выше, или он может быть включено в `x-functions-key` заголовка HTTP.</span><span class="sxs-lookup"><span data-stu-id="0f12d-217">hello key can be included in a query string variable named `code`, as above, or it can be included in an `x-functions-key` HTTP header.</span></span> <span data-ttu-id="0f12d-218">значение Hello hello ключа может быть любого сочетания клавиш, определенные для функции hello или ключ любого узла.</span><span class="sxs-lookup"><span data-stu-id="0f12d-218">hello value of hello key can be any function key defined for hello function, or any host key.</span></span>

<span data-ttu-id="0f12d-219">Можно выбрать запросы tooallow без ключей или указать, что hello основного ключа необходимо использовать, изменив hello `authLevel` свойство в hello привязки JSON (см. [триггер HTTP](#httptrigger)).</span><span class="sxs-lookup"><span data-stu-id="0f12d-219">You can choose tooallow requests without keys or specify that hello master key must be used by changing hello `authLevel` property in hello binding JSON (see [HTTP trigger](#httptrigger)).</span></span>

### <a name="keys-and-webhooks"></a><span data-ttu-id="0f12d-220">Ключи и вызовы webhook</span><span class="sxs-lookup"><span data-stu-id="0f12d-220">Keys and webhooks</span></span>
<span data-ttu-id="0f12d-221">Авторизация веб-перехватчика обрабатывается компонентом получателем hello веб-перехватчика, часть hello HttpTrigger и механизм hello варьируется в зависимости от типа веб-перехватчика hello.</span><span class="sxs-lookup"><span data-stu-id="0f12d-221">Webhook authorization is handled by hello webhook reciever component, part of hello HttpTrigger, and hello mechanism varies based on hello webhook type.</span></span> <span data-ttu-id="0f12d-222">Но каждый из этих механизмов использует ключи.</span><span class="sxs-lookup"><span data-stu-id="0f12d-222">Each mechanism does, however rely on a key.</span></span> <span data-ttu-id="0f12d-223">По умолчанию будет использоваться hello функциональную клавишу с именем «default».</span><span class="sxs-lookup"><span data-stu-id="0f12d-223">By default, hello function key named "default" will be used.</span></span> <span data-ttu-id="0f12d-224">Если вы хотите toouse другой ключ, необходимо будет tooconfigure hello веб-перехватчика toosend hello имя ключа для поставщика с запросом hello в одном из следующих способов hello:</span><span class="sxs-lookup"><span data-stu-id="0f12d-224">If you wish toouse a different key, you will need tooconfigure hello webhook provider toosend hello key name with hello request in one of hello following ways:</span></span>

- <span data-ttu-id="0f12d-225">**Строка запроса**: hello Поставщик передает имя ключа hello в hello `clientid` параметр строки запроса (например, `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span><span class="sxs-lookup"><span data-stu-id="0f12d-225">**Query string**: hello provider passes hello key name in hello `clientid` query string parameter (e.g., `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).</span></span>
- <span data-ttu-id="0f12d-226">**Заголовок запроса**: hello Поставщик передает имя ключа hello в hello `x-functions-clientid` заголовок.</span><span class="sxs-lookup"><span data-stu-id="0f12d-226">**Request header**: hello provider passes hello key name in hello `x-functions-clientid` header.</span></span>

> [!NOTE]
> <span data-ttu-id="0f12d-227">Ключи функций имеют приоритет над ключами узла.</span><span class="sxs-lookup"><span data-stu-id="0f12d-227">Function keys take precedence over host keys.</span></span> <span data-ttu-id="0f12d-228">Если два ключа определены с точно такое же имя, hello hello функция ключ будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="0f12d-228">If two keys are defined with hello same name, hello function key will be used.</span></span>
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a><span data-ttu-id="0f12d-229">Образцы триггеров HTTP</span><span class="sxs-lookup"><span data-stu-id="0f12d-229">HTTP trigger samples</span></span>
<span data-ttu-id="0f12d-230">Предположим, что имеется следующий триггер HTTP в hello hello `bindings` массив function.json:</span><span class="sxs-lookup"><span data-stu-id="0f12d-230">Suppose you have hello following HTTP trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

<span data-ttu-id="0f12d-231">См. Образец hello конкретного языка, выполняющий поиск `name` параметр в строку запроса hello или текста hello hello HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="0f12d-231">See hello language-specific sample that looks for a `name` parameter either in hello query string or hello body of hello HTTP request.</span></span>

* [<span data-ttu-id="0f12d-232">C#</span><span class="sxs-lookup"><span data-stu-id="0f12d-232">C#</span></span>](#httptriggercsharp)
* [<span data-ttu-id="0f12d-233">F#</span><span class="sxs-lookup"><span data-stu-id="0f12d-233">F#</span></span>](#httptriggerfsharp)
* [<span data-ttu-id="0f12d-234">Node.js</span><span class="sxs-lookup"><span data-stu-id="0f12d-234">Node.js</span></span>](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a><span data-ttu-id="0f12d-235">Пример триггера HTTP на языке C#</span><span class="sxs-lookup"><span data-stu-id="0f12d-235">HTTP trigger sample in C#</span></span> #
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

    // Set name tooquery string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

<span data-ttu-id="0f12d-236">Можно также привязать tooa POCO вместо `HttpRequestMessage`.</span><span class="sxs-lookup"><span data-stu-id="0f12d-236">You can also bind tooa POCO instead of `HttpRequestMessage`.</span></span> <span data-ttu-id="0f12d-237">Это будет структура из текста hello запроса hello, интерпретировать как JSON.</span><span class="sxs-lookup"><span data-stu-id="0f12d-237">This will be hydrated from hello body of hello request, parsed as JSON.</span></span> <span data-ttu-id="0f12d-238">Аналогичным образом тип может быть передан вывода ответа toohello HTTP привязки, и это будет возвращаться в виде текста ответа hello, с кодом состояния 200.</span><span class="sxs-lookup"><span data-stu-id="0f12d-238">Similarly, a type can be passed toohello HTTP response output binding, and this will be returned as hello response body, with a 200 status code.</span></span>
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
### <a name="http-trigger-sample-in-f"></a><span data-ttu-id="0f12d-239">Пример триггера HTTP на языке F#</span><span class="sxs-lookup"><span data-stu-id="0f12d-239">HTTP trigger sample in F#</span></span> #
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
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
    } |> Async.StartAsTask
```

<span data-ttu-id="0f12d-240">Требуется `project.json` файла, который использует NuGet tooreference hello `FSharp.Interop.Dynamic` и `Dynamitey` сборки следующим образом:</span><span class="sxs-lookup"><span data-stu-id="0f12d-240">You need a `project.json` file that uses NuGet tooreference hello `FSharp.Interop.Dynamic` and `Dynamitey` assemblies, like this:</span></span>

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

<span data-ttu-id="0f12d-241">Это будет использовать NuGet toofetch зависимостей и будет ссылаться на них в скрипте.</span><span class="sxs-lookup"><span data-stu-id="0f12d-241">This will use NuGet toofetch your dependencies and will reference them in your script.</span></span>

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a><span data-ttu-id="0f12d-242">Пример триггера HTTP для Node.js</span><span class="sxs-lookup"><span data-stu-id="0f12d-242">HTTP trigger sample in Node.JS</span></span>
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults too200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a><span data-ttu-id="0f12d-243">Примеры вызовов webhook</span><span class="sxs-lookup"><span data-stu-id="0f12d-243">Webhook samples</span></span>
<span data-ttu-id="0f12d-244">Предположим, что имеется следующая веб-перехватчика триггера в hello hello `bindings` массив function.json:</span><span class="sxs-lookup"><span data-stu-id="0f12d-244">Suppose you have hello following webhook trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

<span data-ttu-id="0f12d-245">См. Образец hello конкретного языка, зарегистрировавший GitHub проблема комментарии.</span><span class="sxs-lookup"><span data-stu-id="0f12d-245">See hello language-specific sample that logs GitHub issue comments.</span></span>

* [<span data-ttu-id="0f12d-246">C#</span><span class="sxs-lookup"><span data-stu-id="0f12d-246">C#</span></span>](#hooktriggercsharp)
* [<span data-ttu-id="0f12d-247">F#</span><span class="sxs-lookup"><span data-stu-id="0f12d-247">F#</span></span>](#hooktriggerfsharp)
* [<span data-ttu-id="0f12d-248">Node.js</span><span class="sxs-lookup"><span data-stu-id="0f12d-248">Node.js</span></span>](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a><span data-ttu-id="0f12d-249">Пример веб-перехватчика на языке C#</span><span class="sxs-lookup"><span data-stu-id="0f12d-249">Webhook sample in C#</span></span> #
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

### <a name="webhook-sample-in-f"></a><span data-ttu-id="0f12d-250">Пример веб-перехватчика на языке F#</span><span class="sxs-lookup"><span data-stu-id="0f12d-250">Webhook sample in F#</span></span> #
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

### <a name="webhook-sample-in-nodejs"></a><span data-ttu-id="0f12d-251">Пример webhook для Node.js</span><span class="sxs-lookup"><span data-stu-id="0f12d-251">Webhook sample in Node.JS</span></span>
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a><span data-ttu-id="0f12d-252">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0f12d-252">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

