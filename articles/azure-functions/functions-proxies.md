---
title: "aaaWork с прокси-серверов в функции Azure | Документы Microsoft"
description: "Общие сведения о том, как toouse функции Azure учетные записи-посредники"
services: functions
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/11/2017
ms.author: mahender
ms.openlocfilehash: 4d94c89e8f8f2d2c771b01bae142bf9a4f3b7f2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a><span data-ttu-id="a16b5-103">Работа с прокси в Функциях Azure (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="a16b5-103">Work with Azure Functions Proxies (preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="a16b5-104">Сейчас доступна предварительная версия прокси Функций Azure.</span><span class="sxs-lookup"><span data-stu-id="a16b5-104">Azure Functions Proxies is currently in preview.</span></span> <span data-ttu-id="a16b5-105">Он распространяется бесплатно, пока в предварительной версии, но стандартные функции выставления счетов применяется tooproxy выполнений.</span><span class="sxs-lookup"><span data-stu-id="a16b5-105">It is free while in preview, but standard Functions billing applies tooproxy executions.</span></span> <span data-ttu-id="a16b5-106">Дополнительные сведения см. на странице [цен на Функции Azure](https://azure.microsoft.com/pricing/details/functions/).</span><span class="sxs-lookup"><span data-stu-id="a16b5-106">For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).</span></span>

<span data-ttu-id="a16b5-107">В этой статье объясняется, как tooconfigure и работать с Azure функции прокси-серверов.</span><span class="sxs-lookup"><span data-stu-id="a16b5-107">This article explains how tooconfigure and work with Azure Functions Proxies.</span></span> <span data-ttu-id="a16b5-108">Эта функция позволяет указать конечные точки в приложении-функции, реализуемые другим ресурсом.</span><span class="sxs-lookup"><span data-stu-id="a16b5-108">With this feature, you can specify endpoints on your function app that are implemented by another resource.</span></span> <span data-ttu-id="a16b5-109">Можно использовать эти учетные записи-посредники toobreak больших API, в нескольких приложениях функции (как архитектура микрослужбу) и сохранить одну область API для клиентов.</span><span class="sxs-lookup"><span data-stu-id="a16b5-109">You can use these proxies toobreak a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <span data-ttu-id="a16b5-110"><a name="enable"></a>Включение прокси-серверов Функций Azure</span><span class="sxs-lookup"><span data-stu-id="a16b5-110"><a name="enable"></a>Enable Azure Functions Proxies</span></span>

<span data-ttu-id="a16b5-111">По умолчанию прокси не включены.</span><span class="sxs-lookup"><span data-stu-id="a16b5-111">Proxies are not enabled by default.</span></span> <span data-ttu-id="a16b5-112">Можно создать учетные записи-посредники hello компонент отключен, но они не будут выполняться.</span><span class="sxs-lookup"><span data-stu-id="a16b5-112">You can create proxies while hello feature is disabled, but they will not execute.</span></span> <span data-ttu-id="a16b5-113">учетные записи-посредники tooenable hello следующие:</span><span class="sxs-lookup"><span data-stu-id="a16b5-113">tooenable proxies, do hello following:</span></span>

1. <span data-ttu-id="a16b5-114">Откройте hello [портал Azure], и затем перейти tooyour функции приложения.</span><span class="sxs-lookup"><span data-stu-id="a16b5-114">Open hello [Azure portal], and then go tooyour function app.</span></span>
2. <span data-ttu-id="a16b5-115">Выберите **Параметры приложения-функции**.</span><span class="sxs-lookup"><span data-stu-id="a16b5-115">Select **Function app settings**.</span></span>
3. <span data-ttu-id="a16b5-116">Коммутатор **включить Azure функции прокси-серверов (Предварительная версия)** слишком**на**.</span><span class="sxs-lookup"><span data-stu-id="a16b5-116">Switch **Enable Azure Functions Proxies (preview)** too**On**.</span></span>

<span data-ttu-id="a16b5-117">Можно также вернуть здесь tooupdate hello прокси-сервера, среда выполнения как становятся доступными новые возможности.</span><span class="sxs-lookup"><span data-stu-id="a16b5-117">You can also return here tooupdate hello proxy runtime as new features become available.</span></span>


## <span data-ttu-id="a16b5-118"><a name="create"></a>Создание прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="a16b5-118"><a name="create"></a>Create a proxy</span></span>

<span data-ttu-id="a16b5-119">В этом разделе показано, как toocreate a прокси-сервера в hello функции портала.</span><span class="sxs-lookup"><span data-stu-id="a16b5-119">This section shows you how toocreate a proxy in hello Functions portal.</span></span>

1. <span data-ttu-id="a16b5-120">Откройте hello [портал Azure], и затем перейти tooyour функции приложения.</span><span class="sxs-lookup"><span data-stu-id="a16b5-120">Open hello [Azure portal], and then go tooyour function app.</span></span>
2. <span data-ttu-id="a16b5-121">Выберите в левой области hello **новый прокси-сервер**.</span><span class="sxs-lookup"><span data-stu-id="a16b5-121">In hello left pane, select **New proxy**.</span></span>
3. <span data-ttu-id="a16b5-122">Задайте имя прокси.</span><span class="sxs-lookup"><span data-stu-id="a16b5-122">Provide a name for your proxy.</span></span>
4. <span data-ttu-id="a16b5-123">Настройте hello конечную точку, которая предоставляется для этой функции приложения, указав hello **шаблон маршрута** и **методы HTTP**.</span><span class="sxs-lookup"><span data-stu-id="a16b5-123">Configure hello endpoint that's exposed on this function app by specifying hello **route template** and **HTTP methods**.</span></span> <span data-ttu-id="a16b5-124">Эти параметры ведут себя соответствующим правила toohello [триггеры HTTP].</span><span class="sxs-lookup"><span data-stu-id="a16b5-124">These parameters behave according toohello rules for [HTTP triggers].</span></span>
5. <span data-ttu-id="a16b5-125">Набор hello **URL-адрес внутреннего** tooanother конечной точки.</span><span class="sxs-lookup"><span data-stu-id="a16b5-125">Set hello **backend URL** tooanother endpoint.</span></span> <span data-ttu-id="a16b5-126">Ею может быть функция в другом приложении-функции или другой API.</span><span class="sxs-lookup"><span data-stu-id="a16b5-126">This endpoint could be a function in another function app, or it could be any other API.</span></span> <span data-ttu-id="a16b5-127">Hello значение не обязательно toobe статический, и он может ссылаться на [параметры приложения] и [параметров из исходного запроса клиента hello].</span><span class="sxs-lookup"><span data-stu-id="a16b5-127">hello value does not need toobe static, and it can reference [application settings] and [parameters from hello original client request].</span></span>
6. <span data-ttu-id="a16b5-128">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a16b5-128">Click **Create**.</span></span>

<span data-ttu-id="a16b5-129">Прокси теперь существует в виде новой конечной точки в приложении-функции.</span><span class="sxs-lookup"><span data-stu-id="a16b5-129">Your proxy now exists as a new endpoint on your function app.</span></span> <span data-ttu-id="a16b5-130">С точки зрения клиента это эквивалент tooan HttpTrigger в функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="a16b5-130">From a client perspective, it is equivalent tooan HttpTrigger in Azure Functions.</span></span> <span data-ttu-id="a16b5-131">Можно опробовать новый прокси-сервера путем копирования hello URL-адрес прокси-сервера и его тестирование с помощью HTTP клиента по вашему выбору.</span><span class="sxs-lookup"><span data-stu-id="a16b5-131">You can try out your new proxy by copying hello Proxy URL and testing it with your favorite HTTP client.</span></span>

## <span data-ttu-id="a16b5-132"><a name="modify-requests-responses"></a>Изменение запросов и ответов</span><span class="sxs-lookup"><span data-stu-id="a16b5-132"><a name="modify-requests-responses"></a>Modify requests and responses</span></span>

<span data-ttu-id="a16b5-133">С помощью функции Azure учетных записей-посредников можно изменить ответы tooand запросов из серверной части hello.</span><span class="sxs-lookup"><span data-stu-id="a16b5-133">With Azure Functions Proxies, you can modify requests tooand responses from hello back end.</span></span> <span data-ttu-id="a16b5-134">При таком преобразовании используются переменные, указанные в разделе [Использование переменных].</span><span class="sxs-lookup"><span data-stu-id="a16b5-134">These transformations can use variables as defined in [Use variables].</span></span>

### <span data-ttu-id="a16b5-135"><a name="modify-backend-request"></a>Измените запрос hello серверной части</span><span class="sxs-lookup"><span data-stu-id="a16b5-135"><a name="modify-backend-request"></a>Modify hello back-end request</span></span>

<span data-ttu-id="a16b5-136">По умолчанию hello серверной части запроса инициализируется как копию исходного запроса hello.</span><span class="sxs-lookup"><span data-stu-id="a16b5-136">By default, hello back-end request is initialized as a copy of hello original request.</span></span> <span data-ttu-id="a16b5-137">В дополнение к этому toosetting hello серверной части URL-адрес, можно сделать метод HTTP toohello изменения, заголовки и параметры строки запроса.</span><span class="sxs-lookup"><span data-stu-id="a16b5-137">In addition toosetting hello back-end URL, you can make changes toohello HTTP method, headers, and query string parameters.</span></span> <span data-ttu-id="a16b5-138">Hello измененные значения могут ссылаться на [параметры приложения] и [параметров из исходного запроса клиента hello].</span><span class="sxs-lookup"><span data-stu-id="a16b5-138">hello modified values can reference [application settings] and [parameters from hello original client request].</span></span>

<span data-ttu-id="a16b5-139">Сейчас на портале не предусмотрена возможность изменения запросов внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="a16b5-139">Currently, there is no portal experience for modifying back-end requests.</span></span> <span data-ttu-id="a16b5-140">toolearn tooapply эту возможность от proxies.json, в статье [Определите объект requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="a16b5-140">toolearn how tooapply this capability from proxies.json, see [Define a requestOverrides object].</span></span>

### <span data-ttu-id="a16b5-141"><a name="modify-response"></a>Изменение ответа hello</span><span class="sxs-lookup"><span data-stu-id="a16b5-141"><a name="modify-response"></a>Modify hello response</span></span>

<span data-ttu-id="a16b5-142">По умолчанию hello ответа клиента инициализируется как копия ответа hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="a16b5-142">By default, hello client response is initialized as a copy of hello back-end response.</span></span> <span data-ttu-id="a16b5-143">Можно сделать код состояния ответа toohello изменения, фразу причины, заголовки и текст.</span><span class="sxs-lookup"><span data-stu-id="a16b5-143">You can make changes toohello response's status code, reason phrase, headers, and body.</span></span> <span data-ttu-id="a16b5-144">Hello измененные значения могут ссылаться на [параметры приложения], [параметров из исходного запроса клиента hello], и [параметров из ответа внутренней hello].</span><span class="sxs-lookup"><span data-stu-id="a16b5-144">hello modified values can reference [application settings], [parameters from hello original client request], and [parameters from hello back-end response].</span></span>

<span data-ttu-id="a16b5-145">Сейчас на портале не предусмотрена возможность изменения ответов.</span><span class="sxs-lookup"><span data-stu-id="a16b5-145">Currently, there is no portal experience for modifying responses.</span></span> <span data-ttu-id="a16b5-146">toolearn tooapply эту возможность от proxies.json, в статье [Определите объект responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="a16b5-146">toolearn how tooapply this capability from proxies.json, see [Define a responseOverrides object].</span></span>

## <span data-ttu-id="a16b5-147"><a name="using-variables"></a>Использование переменных</span><span class="sxs-lookup"><span data-stu-id="a16b5-147"><a name="using-variables"></a>Use variables</span></span>

<span data-ttu-id="a16b5-148">Hello конфигурации для прокси-сервер не обязательно toobe статический.</span><span class="sxs-lookup"><span data-stu-id="a16b5-148">hello configuration for a proxy does not need toobe static.</span></span> <span data-ttu-id="a16b5-149">Можно условия его toouse переменные из hello первоначальный запрос, ответ серверной части hello или параметров приложений.</span><span class="sxs-lookup"><span data-stu-id="a16b5-149">You can condition it toouse variables from hello original request, hello back-end response, or application settings.</span></span>

### <span data-ttu-id="a16b5-150"><a name="request-parameters"></a>Ссылки на параметры запроса</span><span class="sxs-lookup"><span data-stu-id="a16b5-150"><a name="request-parameters"></a>Reference request parameters</span></span>

<span data-ttu-id="a16b5-151">Параметры запроса можно использовать как входные данные свойства URL-адрес внутренней toohello или как часть изменение запросов и ответов.</span><span class="sxs-lookup"><span data-stu-id="a16b5-151">You can use request parameters as inputs toohello back-end URL property or as part of modifying requests and responses.</span></span> <span data-ttu-id="a16b5-152">Некоторые параметры могут быть привязаны из hello шаблон маршрута, который задан в конфигурации hello базовый прокси-сервера, а другие могут поступать из свойства hello входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="a16b5-152">Some parameters can be bound from hello route template that's specified in hello base proxy configuration, and others can come from properties of hello incoming request.</span></span>

#### <a name="route-template-parameters"></a><span data-ttu-id="a16b5-153">Параметры шаблона маршрута</span><span class="sxs-lookup"><span data-stu-id="a16b5-153">Route template parameters</span></span>
<span data-ttu-id="a16b5-154">Параметры, используемые в шаблоне маршрута hello являются доступными toobe ссылаться по имени.</span><span class="sxs-lookup"><span data-stu-id="a16b5-154">Parameters that are used in hello route template are available toobe referenced by name.</span></span> <span data-ttu-id="a16b5-155">имена параметров Hello заключенных в фигурные скобки ({}).</span><span class="sxs-lookup"><span data-stu-id="a16b5-155">hello parameter names are enclosed in braces ({}).</span></span>

<span data-ttu-id="a16b5-156">Например, если прокси-сервер имеет шаблон маршрута, например `/pets/{petId}`, hello серверной части URL-адрес может включать значение hello `{petId}`, как в `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span><span class="sxs-lookup"><span data-stu-id="a16b5-156">For example, if a proxy has a route template, such as `/pets/{petId}`, hello back-end URL can include hello value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span></span> <span data-ttu-id="a16b5-157">Если шаблон маршрута hello завершается в подстановочный знак, таких как `/api/{*restOfPath}`, hello значение `{restOfPath}` представляет собой строку hello оставшиеся сегменты пути hello входящий запрос.</span><span class="sxs-lookup"><span data-stu-id="a16b5-157">If hello route template terminates in a wildcard, such as `/api/{*restOfPath}`, hello value `{restOfPath}` is a string representation of hello remaining path segments from hello incoming request.</span></span>

#### <a name="additional-request-parameters"></a><span data-ttu-id="a16b5-158">Дополнительные параметры запроса</span><span class="sxs-lookup"><span data-stu-id="a16b5-158">Additional request parameters</span></span>
<span data-ttu-id="a16b5-159">Кроме toohello направления параметров шаблона, можно использовать hello последующих значений в значения конфигурации:</span><span class="sxs-lookup"><span data-stu-id="a16b5-159">In addition toohello route template parameters, hello following values can be used in config values:</span></span>

* <span data-ttu-id="a16b5-160">**{request.method}** : hello метод HTTP, используемый в исходном запросе hello.</span><span class="sxs-lookup"><span data-stu-id="a16b5-160">**{request.method}**: hello HTTP method that's used on hello original request.</span></span>
* <span data-ttu-id="a16b5-161">**{request.headers. \<HeaderName\>}**: заголовок, который может быть считано из исходного запроса hello.</span><span class="sxs-lookup"><span data-stu-id="a16b5-161">**{request.headers.\<HeaderName\>}**: A header that can be read from hello original request.</span></span> <span data-ttu-id="a16b5-162">Замените  *\<HeaderName\>*  с именем hello hello заголовка, которые должны tooread.</span><span class="sxs-lookup"><span data-stu-id="a16b5-162">Replace *\<HeaderName\>* with hello name of hello header that you want tooread.</span></span> <span data-ttu-id="a16b5-163">Если заголовок hello не включена в запрос hello, hello значение будет пустая строка hello.</span><span class="sxs-lookup"><span data-stu-id="a16b5-163">If hello header is not included on hello request, hello value will be hello empty string.</span></span>
* <span data-ttu-id="a16b5-164">**{request.querystring. \<Имя_параметра\>}**: параметр строки запроса, могут быть прочитаны из исходного запроса hello.</span><span class="sxs-lookup"><span data-stu-id="a16b5-164">**{request.querystring.\<ParameterName\>}**: A query string parameter that can be read from hello original request.</span></span> <span data-ttu-id="a16b5-165">Замените  *\<Имя_параметра\>*  с именем hello hello параметра, которое следует tooread.</span><span class="sxs-lookup"><span data-stu-id="a16b5-165">Replace *\<ParameterName\>* with hello name of hello parameter that you want tooread.</span></span> <span data-ttu-id="a16b5-166">Если параметр hello не включается в запрос hello, hello значение будет пустая строка hello.</span><span class="sxs-lookup"><span data-stu-id="a16b5-166">If hello parameter is not included on hello request, hello value will be hello empty string.</span></span>

### <span data-ttu-id="a16b5-167"><a name="response-parameters"></a>Ссылки на параметры ответа внутреннего сервера</span><span class="sxs-lookup"><span data-stu-id="a16b5-167"><a name="response-parameters"></a>Reference back-end response parameters</span></span>

<span data-ttu-id="a16b5-168">Параметры ответа можно использовать как часть изменения hello ответа toohello клиента.</span><span class="sxs-lookup"><span data-stu-id="a16b5-168">Response parameters can be used as part of modifying hello response toohello client.</span></span> <span data-ttu-id="a16b5-169">Hello последующих значений можно использовать в значения конфигурации:</span><span class="sxs-lookup"><span data-stu-id="a16b5-169">hello following values can be used in config values:</span></span>

* <span data-ttu-id="a16b5-170">**{backend.response.statusCode}** : hello код состояния HTTP, который возвращается в ответе hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="a16b5-170">**{backend.response.statusCode}**: hello HTTP status code that's returned on hello back-end response.</span></span>
* <span data-ttu-id="a16b5-171">**{backend.response.statusReason}** : фразу причины hello HTTP, возвращаемый в ответе hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="a16b5-171">**{backend.response.statusReason}**: hello HTTP reason phrase that's returned on hello back-end response.</span></span>
* <span data-ttu-id="a16b5-172">**{backend.response.headers. \<HeaderName\>}**: заголовок, который может быть считано из ответа hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="a16b5-172">**{backend.response.headers.\<HeaderName\>}**: A header that can be read from hello back-end response.</span></span> <span data-ttu-id="a16b5-173">Замените  *\<HeaderName\>*  с именем hello заголовка hello требуется tooread.</span><span class="sxs-lookup"><span data-stu-id="a16b5-173">Replace *\<HeaderName\>* with hello name of hello header you want tooread.</span></span> <span data-ttu-id="a16b5-174">Если заголовок hello не включена в запрос hello, hello значение будет пустая строка hello.</span><span class="sxs-lookup"><span data-stu-id="a16b5-174">If hello header is not included on hello request, hello value will be hello empty string.</span></span>

### <span data-ttu-id="a16b5-175"><a name="use-appsettings"></a>Ссылки на параметры приложения</span><span class="sxs-lookup"><span data-stu-id="a16b5-175"><a name="use-appsettings"></a>Reference application settings</span></span>

<span data-ttu-id="a16b5-176">Можно также сослаться на [параметры приложения, определенные для функции приложение hello](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) заключив имя параметра hello в символы процентов (%).</span><span class="sxs-lookup"><span data-stu-id="a16b5-176">You can also reference [application settings defined for hello function app](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding hello setting name with percent signs (%).</span></span>

<span data-ttu-id="a16b5-177">Например, серверной части URL- *https://%ORDER_PROCESSING_HOST%/api/orders* бы «% ORDER_PROCESSING_HOST %» заменено значением hello параметра ORDER_PROCESSING_HOST hello.</span><span class="sxs-lookup"><span data-stu-id="a16b5-177">For example, a back-end URL of *https://%ORDER_PROCESSING_HOST%/api/orders* would have "%ORDER_PROCESSING_HOST%" replaced with hello value of hello ORDER_PROCESSING_HOST setting.</span></span>

> [!TIP] 
> <span data-ttu-id="a16b5-178">Используйте параметры приложения для внутренних узлов при наличии нескольких развертываний или тестовых сред.</span><span class="sxs-lookup"><span data-stu-id="a16b5-178">Use application settings for back-end hosts when you have multiple deployments or test environments.</span></span> <span data-ttu-id="a16b5-179">Таким образом, можно гарантировать, что вы всегда говорите самому началу toohello завершения для этой среды.</span><span class="sxs-lookup"><span data-stu-id="a16b5-179">That way, you can make sure that you are always talking toohello right back end for that environment.</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="a16b5-180">Расширенная конфигурация</span><span class="sxs-lookup"><span data-stu-id="a16b5-180">Advanced configuration</span></span>

<span data-ttu-id="a16b5-181">Hello прокси-серверы, настроенные хранятся в файле proxies.json, который находится в корневом каталоге hello функции каталога приложения.</span><span class="sxs-lookup"><span data-stu-id="a16b5-181">hello proxies that you configure are stored in a proxies.json file, which is located in hello root of a function app directory.</span></span> <span data-ttu-id="a16b5-182">Можно вручную изменить этот файл и развернуть его как часть приложения, при использовании любого hello [методы развертывания](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) , поддерживаемые функции.</span><span class="sxs-lookup"><span data-stu-id="a16b5-182">You can manually edit this file and deploy it as part of your app when you use any of hello [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span></span> <span data-ttu-id="a16b5-183">функция Hello должен быть [включен](#enable) для обработки toobe файл hello.</span><span class="sxs-lookup"><span data-stu-id="a16b5-183">hello feature must be [enabled](#enable) for hello file toobe processed.</span></span> 

> [!TIP] 
> <span data-ttu-id="a16b5-184">Если вы не настроили одним из способов развертывания hello, можно также работать с файлом proxies.json hello hello портала.</span><span class="sxs-lookup"><span data-stu-id="a16b5-184">If you have not set up one of hello deployment methods, you can also work with hello proxies.json file in hello portal.</span></span> <span data-ttu-id="a16b5-185">Последовательно выберите tooyour функции приложения, выберите **возможности платформы**и выберите **редактор службы приложения**.</span><span class="sxs-lookup"><span data-stu-id="a16b5-185">Go tooyour function app, select **Platform features**, and then select **App Service Editor**.</span></span> <span data-ttu-id="a16b5-186">Таким образом, можно просматривать структуру приложения функции hello весь файл и внесите изменения.</span><span class="sxs-lookup"><span data-stu-id="a16b5-186">By doing so, you can view hello entire file structure of your function app and then make changes.</span></span>

<span data-ttu-id="a16b5-187">Файл proxies.json определяется объектом прокси, который состоит из именованных прокси и их определений.</span><span class="sxs-lookup"><span data-stu-id="a16b5-187">Proxies.json is defined by a proxies object, which is composed of named proxies and their definitions.</span></span> <span data-ttu-id="a16b5-188">При необходимости для автозавершения кода можно ссылаться на [схему JSON](http://json.schemastore.org/proxies), если ваш редактор поддерживает такую возможность.</span><span class="sxs-lookup"><span data-stu-id="a16b5-188">Optionally, if your editor supports it, you can reference a [JSON schema](http://json.schemastore.org/proxies) for code completion.</span></span> <span data-ttu-id="a16b5-189">Пример файла может выглядеть hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a16b5-189">An example file might look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>"
        }
    }
}
```

<span data-ttu-id="a16b5-190">Каждый прокси-сервер имеет понятное имя, например *proxy1* в предшествующих пример hello.</span><span class="sxs-lookup"><span data-stu-id="a16b5-190">Each proxy has a friendly name, such as *proxy1* in hello preceding example.</span></span> <span data-ttu-id="a16b5-191">Hello соответствующий объект определения прокси-сервера определяется hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="a16b5-191">hello corresponding proxy definition object is defined by hello following properties:</span></span>

* <span data-ttu-id="a16b5-192">**matchCondition**: требуется — объект, определяющий hello запросы, вызывающие выполнение hello этого прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="a16b5-192">**matchCondition**: Required--an object defining hello requests that trigger hello execution of this proxy.</span></span> <span data-ttu-id="a16b5-193">Он содержит два свойства, используемые совместно с [триггеры HTTP]:</span><span class="sxs-lookup"><span data-stu-id="a16b5-193">It contains two properties that are shared with [HTTP triggers]:</span></span>
    * <span data-ttu-id="a16b5-194">_методы_: массив hello HTTP-методов, которые hello прокси-сервер отвечает на.</span><span class="sxs-lookup"><span data-stu-id="a16b5-194">_methods_: An array of hello HTTP methods that hello proxy responds to.</span></span> <span data-ttu-id="a16b5-195">Если не указан, hello прокси-сервер отвечает tooall HTTP-методов в маршруте hello.</span><span class="sxs-lookup"><span data-stu-id="a16b5-195">If it is not specified, hello proxy responds tooall HTTP methods on hello route.</span></span>
    * <span data-ttu-id="a16b5-196">_маршрут_: требуются определяет шаблон маршрута hello, управление которой запрос URL-адреса прокси-сервер отвечает.</span><span class="sxs-lookup"><span data-stu-id="a16b5-196">_route_: Required--defines hello route template, controlling which request URLs your proxy responds to.</span></span> <span data-ttu-id="a16b5-197">В отличие от триггеров HTTP значение по умолчанию отсутствует.</span><span class="sxs-lookup"><span data-stu-id="a16b5-197">Unlike in HTTP triggers, there is no default value.</span></span>
* <span data-ttu-id="a16b5-198">**backendUri**: hello URL-адрес hello внутренний ресурс toowhich hello запроса должен быть прокси.</span><span class="sxs-lookup"><span data-stu-id="a16b5-198">**backendUri**: hello URL of hello back-end resource toowhich hello request should be proxied.</span></span> <span data-ttu-id="a16b5-199">Это значение можно ссылаться из исходного запроса клиента hello параметры приложения и параметры.</span><span class="sxs-lookup"><span data-stu-id="a16b5-199">This value can reference application settings and parameters from hello original client request.</span></span> <span data-ttu-id="a16b5-200">Если это свойство не включено, Функции Azure вернут ответ HTTP 200 OK.</span><span class="sxs-lookup"><span data-stu-id="a16b5-200">If this property is not included, Azure Functions responds with an HTTP 200 OK.</span></span>
* <span data-ttu-id="a16b5-201">**requestOverrides**: объект, определяющий преобразования toohello серверной части запроса.</span><span class="sxs-lookup"><span data-stu-id="a16b5-201">**requestOverrides**: An object that defines transformations toohello back-end request.</span></span> <span data-ttu-id="a16b5-202">Ознакомьтесь с разделом [Определите объект requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="a16b5-202">See [Define a requestOverrides object].</span></span>
* <span data-ttu-id="a16b5-203">**responseOverrides**: объект, определяющий ответа клиента toohello преобразования.</span><span class="sxs-lookup"><span data-stu-id="a16b5-203">**responseOverrides**: An object that defines transformations toohello client response.</span></span> <span data-ttu-id="a16b5-204">Ознакомьтесь с разделом [Определите объект responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="a16b5-204">See [Define a responseOverrides object].</span></span>

> [!NOTE] 
> <span data-ttu-id="a16b5-205">свойства маршрута Hello Azure функции прокси-серверы не учитывают свойство routePrefix hello конфигурации узла функции hello.</span><span class="sxs-lookup"><span data-stu-id="a16b5-205">hello route property Azure Functions Proxies does not honor hello routePrefix property of hello Functions host configuration.</span></span> <span data-ttu-id="a16b5-206">Если вы хотите tooinclude является префиксом, например /api, он должен включаться в свойстве маршрута hello.</span><span class="sxs-lookup"><span data-stu-id="a16b5-206">If you want tooinclude a prefix such as /api, it must be included in hello route property.</span></span>

### <span data-ttu-id="a16b5-207"><a name="requestOverrides"></a>Определение объекта requestOverrides</span><span class="sxs-lookup"><span data-stu-id="a16b5-207"><a name="requestOverrides"></a>Define a requestOverrides object</span></span>

<span data-ttu-id="a16b5-208">Объект requestOverrides Hello определяет изменения, внесенные toohello запроса при вызове hello внутренний ресурс.</span><span class="sxs-lookup"><span data-stu-id="a16b5-208">hello requestOverrides object defines changes made toohello request when hello back-end resource is called.</span></span> <span data-ttu-id="a16b5-209">Hello объекта определяется hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="a16b5-209">hello object is defined by hello following properties:</span></span>

* <span data-ttu-id="a16b5-210">**backend.Request.Method**: hello метод HTTP, который использовал toocall hello серверной части.</span><span class="sxs-lookup"><span data-stu-id="a16b5-210">**backend.request.method**: hello HTTP method that's used toocall hello back end.</span></span>
* <span data-ttu-id="a16b5-211">**backend.Request.Querystring. \<Имя_параметра\>**: параметр строки запроса, можно задать для hello вызовов toohello серверной части.</span><span class="sxs-lookup"><span data-stu-id="a16b5-211">**backend.request.querystring.\<ParameterName\>**: A query string parameter that can be set for hello call toohello back end.</span></span> <span data-ttu-id="a16b5-212">Замените  *\<Имя_параметра\>*  с именем hello hello параметра, которое следует tooset.</span><span class="sxs-lookup"><span data-stu-id="a16b5-212">Replace *\<ParameterName\>* with hello name of hello parameter that you want tooset.</span></span> <span data-ttu-id="a16b5-213">Если пустая строка hello, параметр hello не включена на hello серверной части запроса.</span><span class="sxs-lookup"><span data-stu-id="a16b5-213">If hello empty string is provided, hello parameter is not included on hello back-end request.</span></span>
* <span data-ttu-id="a16b5-214">**backend.Request.Headers. \<HeaderName\>**: заголовок, который может быть задано для hello вызовов toohello серверной части.</span><span class="sxs-lookup"><span data-stu-id="a16b5-214">**backend.request.headers.\<HeaderName\>**: A header that can be set for hello call toohello back end.</span></span> <span data-ttu-id="a16b5-215">Замените  *\<HeaderName\>*  с именем hello hello заголовка, которые должны tooset.</span><span class="sxs-lookup"><span data-stu-id="a16b5-215">Replace *\<HeaderName\>* with hello name of hello header that you want tooset.</span></span> <span data-ttu-id="a16b5-216">Если указать пустую строку hello hello не колонтитул hello серверной части запроса.</span><span class="sxs-lookup"><span data-stu-id="a16b5-216">If you provide hello empty string, hello header is not included on hello back-end request.</span></span>

<span data-ttu-id="a16b5-217">Значения можно ссылаться из исходного запроса клиента hello параметры приложения и параметры.</span><span class="sxs-lookup"><span data-stu-id="a16b5-217">Values can reference application settings and parameters from hello original client request.</span></span>

<span data-ttu-id="a16b5-218">Пример конфигурации может выглядеть hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a16b5-218">An example configuration might look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "backendUri": "https://<AnotherApp>.azurewebsites.net/api/<FunctionName>",
            "requestOverrides": {
                "backend.request.headers.Accept": "application/xml",
                "backend.request.headers.x-functions-key": "%ANOTHERAPP_API_KEY%"
            }
        }
    }
}
```

### <span data-ttu-id="a16b5-219"><a name="responseOverrides"></a>Определение объекта responseOverrides</span><span class="sxs-lookup"><span data-stu-id="a16b5-219"><a name="responseOverrides"></a>Define a responseOverrides object</span></span>

<span data-ttu-id="a16b5-220">Объект requestOverrides Hello определяет изменения, внесенные toohello ответ, который прошел задней toohello клиента.</span><span class="sxs-lookup"><span data-stu-id="a16b5-220">hello requestOverrides object defines changes that are made toohello response that's passed back toohello client.</span></span> <span data-ttu-id="a16b5-221">Hello объекта определяется hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="a16b5-221">hello object is defined by hello following properties:</span></span>

* <span data-ttu-id="a16b5-222">**response.statusCode**: toobe код состояния hello HTTP вернул toohello клиента.</span><span class="sxs-lookup"><span data-stu-id="a16b5-222">**response.statusCode**: hello HTTP status code toobe returned toohello client.</span></span>
* <span data-ttu-id="a16b5-223">**response.statusReason**: toobe фразу причины hello HTTP вернул toohello клиента.</span><span class="sxs-lookup"><span data-stu-id="a16b5-223">**response.statusReason**: hello HTTP reason phrase toobe returned toohello client.</span></span>
* <span data-ttu-id="a16b5-224">**Response.Body**: hello строковое представление toobe текст hello вернул toohello клиента.</span><span class="sxs-lookup"><span data-stu-id="a16b5-224">**response.body**: hello string representation of hello body toobe returned toohello client.</span></span>
* <span data-ttu-id="a16b5-225">**Response.Headers. \<HeaderName\>**: заголовок, который можно задать для клиента toohello hello ответа.</span><span class="sxs-lookup"><span data-stu-id="a16b5-225">**response.headers.\<HeaderName\>**: A header that can be set for hello response toohello client.</span></span> <span data-ttu-id="a16b5-226">Замените  *\<HeaderName\>*  с именем hello hello заголовка, которые должны tooset.</span><span class="sxs-lookup"><span data-stu-id="a16b5-226">Replace *\<HeaderName\>* with hello name of hello header that you want tooset.</span></span> <span data-ttu-id="a16b5-227">Если указать пустую строку hello hello не колонтитул hello ответа.</span><span class="sxs-lookup"><span data-stu-id="a16b5-227">If you provide hello empty string, hello header is not included on hello response.</span></span>

<span data-ttu-id="a16b5-228">Значения можно ссылаться из ответа внутренней hello параметры приложения, параметры из hello первоначальный запрос клиента и параметры.</span><span class="sxs-lookup"><span data-stu-id="a16b5-228">Values can reference application settings, parameters from hello original client request, and parameters from hello back-end response.</span></span>

<span data-ttu-id="a16b5-229">Пример конфигурации может выглядеть hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="a16b5-229">An example configuration might look like hello following:</span></span>

```json
{
    "$schema": "http://json.schemastore.org/proxies",
    "proxies": {
        "proxy1": {
            "matchCondition": {
                "methods": [ "GET" ],
                "route": "/api/{test}"
            },
            "responseOverrides": {
                "response.body": "Hello, {test}",
                "response.headers.Content-Type": "text/plain"
            }
        }
    }
}
```
> [!NOTE] 
> <span data-ttu-id="a16b5-230">В этом примере текст hello задается значение напрямую, поэтому нет `backendUri` необходимые свойства.</span><span class="sxs-lookup"><span data-stu-id="a16b5-230">In this example, hello body is being set directly, so no `backendUri` property is needed.</span></span> <span data-ttu-id="a16b5-231">Hello примере показано, как можно использовать функции Azure учетных записей-посредников для имитации API-интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="a16b5-231">hello example shows how you might use Azure Functions Proxies for mocking APIs.</span></span>

[портал Azure]: https://portal.azure.com
[триггеры HTTP]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger
[Modify hello back-end request]: #modify-backend-request
[Modify hello response]: #modify-response
[Определите объект requestOverrides]: #requestOverrides
[Определите объект responseOverrides]: #responseOverrides
[параметры приложения]: #use-appsettings
[Использование переменных]: #using-variables
[параметров из исходного запроса клиента hello]: #request-parameters
[параметров из ответа внутренней hello]: #response-parameters
