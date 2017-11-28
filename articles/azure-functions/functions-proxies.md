---
title: "Работа с прокси в Функциях Azure | Документация Майкрософт"
description: "Общие сведения об использовании прокси Функций Azure"
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
ms.openlocfilehash: 102e54627a8fee721d3ed85e86a8009e706bb5b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="work-with-azure-functions-proxies-preview"></a><span data-ttu-id="b8d1f-103">Работа с прокси в Функциях Azure (предварительная версия)</span><span class="sxs-lookup"><span data-stu-id="b8d1f-103">Work with Azure Functions Proxies (preview)</span></span>

> [!NOTE] 
> <span data-ttu-id="b8d1f-104">Сейчас доступна предварительная версия прокси Функций Azure.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-104">Azure Functions Proxies is currently in preview.</span></span> <span data-ttu-id="b8d1f-105">Предварительная версия предоставляется бесплатно, но на выполнение прокси распространяется стандартная тарификация Функций.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-105">It is free while in preview, but standard Functions billing applies to proxy executions.</span></span> <span data-ttu-id="b8d1f-106">Дополнительные сведения см. на странице [цен на Функции Azure](https://azure.microsoft.com/pricing/details/functions/).</span><span class="sxs-lookup"><span data-stu-id="b8d1f-106">For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).</span></span>

<span data-ttu-id="b8d1f-107">В этой статье описано, как настроить прокси Функций Azure и работать с ними.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-107">This article explains how to configure and work with Azure Functions Proxies.</span></span> <span data-ttu-id="b8d1f-108">Эта функция позволяет указать конечные точки в приложении-функции, реализуемые другим ресурсом.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-108">With this feature, you can specify endpoints on your function app that are implemented by another resource.</span></span> <span data-ttu-id="b8d1f-109">Эти прокси можно использовать для разбиения большого API-интерфейса на несколько приложений-функций (как в архитектуре микрослужб), сохраняя при этом единую область API для клиентов.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-109">You can use these proxies to break a large API into multiple function apps (as in a microservice architecture), while still presenting a single API surface for clients.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]


## <span data-ttu-id="b8d1f-110"><a name="enable"></a>Включение прокси-серверов Функций Azure</span><span class="sxs-lookup"><span data-stu-id="b8d1f-110"><a name="enable"></a>Enable Azure Functions Proxies</span></span>

<span data-ttu-id="b8d1f-111">По умолчанию прокси не включены.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-111">Proxies are not enabled by default.</span></span> <span data-ttu-id="b8d1f-112">Вы можете создавать прокси, когда функция отключена, но они не будут выполняться.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-112">You can create proxies while the feature is disabled, but they will not execute.</span></span> <span data-ttu-id="b8d1f-113">Чтобы включить прокси-серверы, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="b8d1f-113">To enable proxies, do the following:</span></span>

1. <span data-ttu-id="b8d1f-114">Откройте [портал Azure] и перейдите к своему приложению-функции.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-114">Open the [Azure portal], and then go to your function app.</span></span>
2. <span data-ttu-id="b8d1f-115">Выберите **Параметры приложения-функции**.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-115">Select **Function app settings**.</span></span>
3. <span data-ttu-id="b8d1f-116">Включите **параметр** **Включить прокси-серверы для функций Azure (предварительная версия)**.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-116">Switch **Enable Azure Functions Proxies (preview)** to **On**.</span></span>

<span data-ttu-id="b8d1f-117">Вы можете также возвращаться сюда для обновления среды выполнения прокси по мере появления новых функций.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-117">You can also return here to update the proxy runtime as new features become available.</span></span>


## <span data-ttu-id="b8d1f-118"><a name="create"></a>Создание прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="b8d1f-118"><a name="create"></a>Create a proxy</span></span>

<span data-ttu-id="b8d1f-119">В этом разделе показано, как создать прокси-сервер на портале Функций.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-119">This section shows you how to create a proxy in the Functions portal.</span></span>

1. <span data-ttu-id="b8d1f-120">Откройте [портал Azure] и перейдите к своему приложению-функции.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-120">Open the [Azure portal], and then go to your function app.</span></span>
2. <span data-ttu-id="b8d1f-121">В левой области выберите **Создать прокси-сервер**.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-121">In the left pane, select **New proxy**.</span></span>
3. <span data-ttu-id="b8d1f-122">Задайте имя прокси.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-122">Provide a name for your proxy.</span></span>
4. <span data-ttu-id="b8d1f-123">Настройте конечную точку в этом приложении-функции, указав **шаблон маршрута** и **методы HTTP**.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-123">Configure the endpoint that's exposed on this function app by specifying the **route template** and **HTTP methods**.</span></span> <span data-ttu-id="b8d1f-124">Поведение этих параметров соответствует правилам для [триггеров HTTP].</span><span class="sxs-lookup"><span data-stu-id="b8d1f-124">These parameters behave according to the rules for [HTTP triggers].</span></span>
5. <span data-ttu-id="b8d1f-125">Задайте **URL-адрес внутреннего сервера** для другой конечной точки.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-125">Set the **backend URL** to another endpoint.</span></span> <span data-ttu-id="b8d1f-126">Ею может быть функция в другом приложении-функции или другой API.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-126">This endpoint could be a function in another function app, or it could be any other API.</span></span> <span data-ttu-id="b8d1f-127">Значение не обязательно должно быть статическим и может ссылаться на [параметры приложения] и [параметры исходного запроса клиента].</span><span class="sxs-lookup"><span data-stu-id="b8d1f-127">The value does not need to be static, and it can reference [application settings] and [parameters from the original client request].</span></span>
6. <span data-ttu-id="b8d1f-128">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-128">Click **Create**.</span></span>

<span data-ttu-id="b8d1f-129">Прокси теперь существует в виде новой конечной точки в приложении-функции.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-129">Your proxy now exists as a new endpoint on your function app.</span></span> <span data-ttu-id="b8d1f-130">С точки зрения клиента это аналогично HttpTrigger в Функциях Azure.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-130">From a client perspective, it is equivalent to an HttpTrigger in Azure Functions.</span></span> <span data-ttu-id="b8d1f-131">Можно испытать новый прокси, скопировав URL-адрес прокси и протестировав его с помощью избранного клиента HTTP.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-131">You can try out your new proxy by copying the Proxy URL and testing it with your favorite HTTP client.</span></span>

## <span data-ttu-id="b8d1f-132"><a name="modify-requests-responses"></a>Изменение запросов и ответов</span><span class="sxs-lookup"><span data-stu-id="b8d1f-132"><a name="modify-requests-responses"></a>Modify requests and responses</span></span>

<span data-ttu-id="b8d1f-133">Прокси-серверы для Функций Azure позволяют изменять запросы и ответы из внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-133">With Azure Functions Proxies, you can modify requests to and responses from the back end.</span></span> <span data-ttu-id="b8d1f-134">При таком преобразовании используются переменные, указанные в разделе [Использование переменных].</span><span class="sxs-lookup"><span data-stu-id="b8d1f-134">These transformations can use variables as defined in [Use variables].</span></span>

### <span data-ttu-id="b8d1f-135"><a name="modify-backend-request"></a>Изменение запроса внутреннего сервера</span><span class="sxs-lookup"><span data-stu-id="b8d1f-135"><a name="modify-backend-request"></a>Modify the back-end request</span></span>

<span data-ttu-id="b8d1f-136">По умолчанию запрос внутреннего сервера инициализируется в качестве копии исходного запроса.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-136">By default, the back-end request is initialized as a copy of the original request.</span></span> <span data-ttu-id="b8d1f-137">Кроме настройки URL-адреса внутреннего сервера вы также можете изменить метод, заголовки и параметры строки запроса HTTP.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-137">In addition to setting the back-end URL, you can make changes to the HTTP method, headers, and query string parameters.</span></span> <span data-ttu-id="b8d1f-138">Измененные значения могут ссылаться на [параметры приложения] и [параметры исходного запроса клиента].</span><span class="sxs-lookup"><span data-stu-id="b8d1f-138">The modified values can reference [application settings] and [parameters from the original client request].</span></span>

<span data-ttu-id="b8d1f-139">Сейчас на портале не предусмотрена возможность изменения запросов внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-139">Currently, there is no portal experience for modifying back-end requests.</span></span> <span data-ttu-id="b8d1f-140">Чтобы узнать, как использовать эту возможность в файле proxies.json, ознакомьтесь с разделом [Определение объекта requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="b8d1f-140">To learn how to apply this capability from proxies.json, see [Define a requestOverrides object].</span></span>

### <span data-ttu-id="b8d1f-141"><a name="modify-response"></a>Изменение ответа</span><span class="sxs-lookup"><span data-stu-id="b8d1f-141"><a name="modify-response"></a>Modify the response</span></span>

<span data-ttu-id="b8d1f-142">По умолчанию ответ клиента инициализируется в качестве копии ответа внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-142">By default, the client response is initialized as a copy of the back-end response.</span></span> <span data-ttu-id="b8d1f-143">Вы можете изменить код состояния, описание, заголовки и текст ответа.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-143">You can make changes to the response's status code, reason phrase, headers, and body.</span></span> <span data-ttu-id="b8d1f-144">Измененные значения могут ссылаться на [параметры приложения], [параметры исходного запроса клиента] и [параметры ответа внутреннего сервера].</span><span class="sxs-lookup"><span data-stu-id="b8d1f-144">The modified values can reference [application settings], [parameters from the original client request], and [parameters from the back-end response].</span></span>

<span data-ttu-id="b8d1f-145">Сейчас на портале не предусмотрена возможность изменения ответов.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-145">Currently, there is no portal experience for modifying responses.</span></span> <span data-ttu-id="b8d1f-146">Чтобы узнать, как использовать эту возможность в файле proxies.json, ознакомьтесь с разделом [Определение объекта responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="b8d1f-146">To learn how to apply this capability from proxies.json, see [Define a responseOverrides object].</span></span>

## <span data-ttu-id="b8d1f-147"><a name="using-variables"></a>Использование переменных</span><span class="sxs-lookup"><span data-stu-id="b8d1f-147"><a name="using-variables"></a>Use variables</span></span>

<span data-ttu-id="b8d1f-148">Использовать статическую конфигурацию для прокси-сервера необязательно.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-148">The configuration for a proxy does not need to be static.</span></span> <span data-ttu-id="b8d1f-149">Вы можете настроить для него использование переменных из исходного запроса, ответа внутреннего сервера или параметров приложения.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-149">You can condition it to use variables from the original request, the back-end response, or application settings.</span></span>

### <span data-ttu-id="b8d1f-150"><a name="request-parameters"></a>Ссылки на параметры запроса</span><span class="sxs-lookup"><span data-stu-id="b8d1f-150"><a name="request-parameters"></a>Reference request parameters</span></span>

<span data-ttu-id="b8d1f-151">Параметры запроса можно использовать в качестве входных данных для свойства URL-адреса внутреннего сервера или в рамках изменения запросов и ответов.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-151">You can use request parameters as inputs to the back-end URL property or as part of modifying requests and responses.</span></span> <span data-ttu-id="b8d1f-152">Некоторые параметры могут быть связаны с шаблоном маршрута, указанным в основной конфигурации прокси-сервера, тогда как другие задаются в соответствии со свойствами входящих запросов.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-152">Some parameters can be bound from the route template that's specified in the base proxy configuration, and others can come from properties of the incoming request.</span></span>

#### <a name="route-template-parameters"></a><span data-ttu-id="b8d1f-153">Параметры шаблона маршрута</span><span class="sxs-lookup"><span data-stu-id="b8d1f-153">Route template parameters</span></span>
<span data-ttu-id="b8d1f-154">Параметры, используемые в шаблоне маршрута, указываются по именам,</span><span class="sxs-lookup"><span data-stu-id="b8d1f-154">Parameters that are used in the route template are available to be referenced by name.</span></span> <span data-ttu-id="b8d1f-155">которые заключаются в фигурные скобки — {}.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-155">The parameter names are enclosed in braces ({}).</span></span>

<span data-ttu-id="b8d1f-156">Например, если прокси-сервер использует шаблон маршрута, подобный `/pets/{petId}`, URL-адрес внутреннего сервера может содержать значение `{petId}`, как в `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-156">For example, if a proxy has a route template, such as `/pets/{petId}`, the back-end URL can include the value of `{petId}`, as in `https://<AnotherApp>.azurewebsites.net/api/pets/{petId}`.</span></span> <span data-ttu-id="b8d1f-157">Если шаблон маршрута заканчивается подстановочным знаком, например `/api/{*restOfPath}`, значение `{restOfPath}` будет строковым представлением остальных сегментов пути входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-157">If the route template terminates in a wildcard, such as `/api/{*restOfPath}`, the value `{restOfPath}` is a string representation of the remaining path segments from the incoming request.</span></span>

#### <a name="additional-request-parameters"></a><span data-ttu-id="b8d1f-158">Дополнительные параметры запроса</span><span class="sxs-lookup"><span data-stu-id="b8d1f-158">Additional request parameters</span></span>
<span data-ttu-id="b8d1f-159">В дополнение к параметрам шаблона маршрута вы можете использовать следующие значения конфигурации:</span><span class="sxs-lookup"><span data-stu-id="b8d1f-159">In addition to the route template parameters, the following values can be used in config values:</span></span>

* <span data-ttu-id="b8d1f-160">**{request.method}.** Метод HTTP, используемый в исходном запросе.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-160">**{request.method}**: The HTTP method that's used on the original request.</span></span>
* <span data-ttu-id="b8d1f-161">**{request.headers.\<имя_заголовка\>}.** Заголовок, который можно считать из исходного запроса.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-161">**{request.headers.\<HeaderName\>}**: A header that can be read from the original request.</span></span> <span data-ttu-id="b8d1f-162">Замените *\<имя_заголовка\>* именем заголовка, который вы собираетесь считать.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-162">Replace *\<HeaderName\>* with the name of the header that you want to read.</span></span> <span data-ttu-id="b8d1f-163">Если заголовок не включен в запрос, в качестве значения будет отображаться пустая строка.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-163">If the header is not included on the request, the value will be the empty string.</span></span>
* <span data-ttu-id="b8d1f-164">**{request.querystring.\<имя_параметра\>}.** Параметр строки запроса, который можно считать из исходного запроса.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-164">**{request.querystring.\<ParameterName\>}**: A query string parameter that can be read from the original request.</span></span> <span data-ttu-id="b8d1f-165">Замените *\<имя_параметра\>* именем параметра, который вы собираетесь считать.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-165">Replace *\<ParameterName\>* with the name of the parameter that you want to read.</span></span> <span data-ttu-id="b8d1f-166">Если параметр не включен в запрос, в качестве значения будет отображаться пустая строка.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-166">If the parameter is not included on the request, the value will be the empty string.</span></span>

### <span data-ttu-id="b8d1f-167"><a name="response-parameters"></a>Ссылки на параметры ответа внутреннего сервера</span><span class="sxs-lookup"><span data-stu-id="b8d1f-167"><a name="response-parameters"></a>Reference back-end response parameters</span></span>

<span data-ttu-id="b8d1f-168">Параметры ответа можно использовать при изменении ответов для клиента.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-168">Response parameters can be used as part of modifying the response to the client.</span></span> <span data-ttu-id="b8d1f-169">Следующие значения можно использовать в качестве значений конфигурации:</span><span class="sxs-lookup"><span data-stu-id="b8d1f-169">The following values can be used in config values:</span></span>

* <span data-ttu-id="b8d1f-170">**{backend.response.statusCode}.** Код состояния HTTP, возвращаемый для ответа внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-170">**{backend.response.statusCode}**: The HTTP status code that's returned on the back-end response.</span></span>
* <span data-ttu-id="b8d1f-171">**{backend.response.statusReason}.** Код состояния HTTP, возвращаемый для ответа внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-171">**{backend.response.statusReason}**: The HTTP reason phrase that's returned on the back-end response.</span></span>
* <span data-ttu-id="b8d1f-172">**{backend.response.headers.\<имя_заголовка\>}.** Заголовок, который можно считать из ответа внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-172">**{backend.response.headers.\<HeaderName\>}**: A header that can be read from the back-end response.</span></span> <span data-ttu-id="b8d1f-173">Замените *\<имя_заголовка\>* именем заголовка, который вы собираетесь считать.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-173">Replace *\<HeaderName\>* with the name of the header you want to read.</span></span> <span data-ttu-id="b8d1f-174">Если заголовок не включен в запрос, в качестве значения будет отображаться пустая строка.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-174">If the header is not included on the request, the value will be the empty string.</span></span>

### <span data-ttu-id="b8d1f-175"><a name="use-appsettings"></a>Ссылки на параметры приложения</span><span class="sxs-lookup"><span data-stu-id="b8d1f-175"><a name="use-appsettings"></a>Reference application settings</span></span>

<span data-ttu-id="b8d1f-176">Вы также можете ссылаться на [параметры приложения, определенные для приложения-функции](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop), поставив знаки процента (%) перед именем параметра и после него.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-176">You can also reference [application settings defined for the function app](https://docs.microsoft.com/azure/azure-functions/functions-how-to-use-azure-function-app-settings#develop) by surrounding the setting name with percent signs (%).</span></span>

<span data-ttu-id="b8d1f-177">Например, в URL-адресе внутреннего сервера *https://%ORDER_PROCESSING_HOST%/api/orders* %ORDER_PROCESSING_HOST% будет заменено значением параметра ORDER_PROCESSING_HOST.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-177">For example, a back-end URL of *https://%ORDER_PROCESSING_HOST%/api/orders* would have "%ORDER_PROCESSING_HOST%" replaced with the value of the ORDER_PROCESSING_HOST setting.</span></span>

> [!TIP] 
> <span data-ttu-id="b8d1f-178">Используйте параметры приложения для внутренних узлов при наличии нескольких развертываний или тестовых сред.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-178">Use application settings for back-end hosts when you have multiple deployments or test environments.</span></span> <span data-ttu-id="b8d1f-179">Таким образом, вы будете всегда обращаться к правильному внутреннему серверу в этой среде.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-179">That way, you can make sure that you are always talking to the right back end for that environment.</span></span>

## <a name="advanced-configuration"></a><span data-ttu-id="b8d1f-180">Расширенная конфигурация</span><span class="sxs-lookup"><span data-stu-id="b8d1f-180">Advanced configuration</span></span>

<span data-ttu-id="b8d1f-181">Настроенные прокси хранятся в файле proxies.json, расположенном в корневом каталоге приложения-функции.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-181">The proxies that you configure are stored in a proxies.json file, which is located in the root of a function app directory.</span></span> <span data-ttu-id="b8d1f-182">Вы можете вручную изменить этот файл и развернуть его как часть приложения, используя любой из [методов развертывания](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment), поддерживаемых Функциями.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-182">You can manually edit this file and deploy it as part of your app when you use any of the [deployment methods](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment) that Functions supports.</span></span> <span data-ttu-id="b8d1f-183">Для обработки файла функция должна быть [включена](#enable).</span><span class="sxs-lookup"><span data-stu-id="b8d1f-183">The feature must be [enabled](#enable) for the file to be processed.</span></span> 

> [!TIP] 
> <span data-ttu-id="b8d1f-184">Вы также можете работать с файлом proxies.json на портале, если вы не настроили ни один из методов развертывания.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-184">If you have not set up one of the deployment methods, you can also work with the proxies.json file in the portal.</span></span> <span data-ttu-id="b8d1f-185">Перейдите к приложению-функции и выберите **Функции платформы**, а затем — **Редактор службы приложений**.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-185">Go to your function app, select **Platform features**, and then select **App Service Editor**.</span></span> <span data-ttu-id="b8d1f-186">Так вы сможете просмотреть всю структуру файла приложения-функции и внести изменения.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-186">By doing so, you can view the entire file structure of your function app and then make changes.</span></span>

<span data-ttu-id="b8d1f-187">Файл proxies.json определяется объектом прокси, который состоит из именованных прокси и их определений.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-187">Proxies.json is defined by a proxies object, which is composed of named proxies and their definitions.</span></span> <span data-ttu-id="b8d1f-188">При необходимости для автозавершения кода можно ссылаться на [схему JSON](http://json.schemastore.org/proxies), если ваш редактор поддерживает такую возможность.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-188">Optionally, if your editor supports it, you can reference a [JSON schema](http://json.schemastore.org/proxies) for code completion.</span></span> <span data-ttu-id="b8d1f-189">Например, файл может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b8d1f-189">An example file might look like the following:</span></span>

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

<span data-ttu-id="b8d1f-190">Каждый прокси имеет понятное имя, как например *proxy1* в предыдущем примере.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-190">Each proxy has a friendly name, such as *proxy1* in the preceding example.</span></span> <span data-ttu-id="b8d1f-191">Соответствующий объект определения прокси определяется следующими свойствами:</span><span class="sxs-lookup"><span data-stu-id="b8d1f-191">The corresponding proxy definition object is defined by the following properties:</span></span>

* <span data-ttu-id="b8d1f-192">**matchCondition** (обязательное) — объект, который определяет запросы, активирующие выполнение этого прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-192">**matchCondition**: Required--an object defining the requests that trigger the execution of this proxy.</span></span> <span data-ttu-id="b8d1f-193">Он содержит два свойства, используемые совместно с [триггеров HTTP]:</span><span class="sxs-lookup"><span data-stu-id="b8d1f-193">It contains two properties that are shared with [HTTP triggers]:</span></span>
    * <span data-ttu-id="b8d1f-194">_methods_ — массив методов HTTP, на которые отвечает прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-194">_methods_: An array of the HTTP methods that the proxy responds to.</span></span> <span data-ttu-id="b8d1f-195">Если свойство не указано, прокси-сервер будет отвечать на все методы HTTP в маршруте.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-195">If it is not specified, the proxy responds to all HTTP methods on the route.</span></span>
    * <span data-ttu-id="b8d1f-196">_route_ (обязательное) — шаблон маршрута, определяющий URL-адреса запросов, на которые будет отвечать прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-196">_route_: Required--defines the route template, controlling which request URLs your proxy responds to.</span></span> <span data-ttu-id="b8d1f-197">В отличие от триггеров HTTP значение по умолчанию отсутствует.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-197">Unlike in HTTP triggers, there is no default value.</span></span>
* <span data-ttu-id="b8d1f-198">**backendUri** — URL-адрес внутреннего ресурса, к которому должен быть отправлен запрос.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-198">**backendUri**: The URL of the back-end resource to which the request should be proxied.</span></span> <span data-ttu-id="b8d1f-199">Это значение может ссылаться на параметры приложения и параметры исходного запроса клиента.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-199">This value can reference application settings and parameters from the original client request.</span></span> <span data-ttu-id="b8d1f-200">Если это свойство не включено, Функции Azure вернут ответ HTTP 200 OK.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-200">If this property is not included, Azure Functions responds with an HTTP 200 OK.</span></span>
* <span data-ttu-id="b8d1f-201">**requestOverrides.** Объект, определяющий преобразование запросов внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-201">**requestOverrides**: An object that defines transformations to the back-end request.</span></span> <span data-ttu-id="b8d1f-202">Ознакомьтесь с разделом [Определение объекта requestOverrides].</span><span class="sxs-lookup"><span data-stu-id="b8d1f-202">See [Define a requestOverrides object].</span></span>
* <span data-ttu-id="b8d1f-203">**responseOverrides.** Объект, определяющий преобразование ответа клиента.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-203">**responseOverrides**: An object that defines transformations to the client response.</span></span> <span data-ttu-id="b8d1f-204">Ознакомьтесь с разделом [Определение объекта responseOverrides].</span><span class="sxs-lookup"><span data-stu-id="b8d1f-204">See [Define a responseOverrides object].</span></span>

> [!NOTE] 
> <span data-ttu-id="b8d1f-205">Свойство route прокси-сервера Функций Azure не учитывает свойство routePrefix конфигурации узла Функций.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-205">The route property Azure Functions Proxies does not honor the routePrefix property of the Functions host configuration.</span></span> <span data-ttu-id="b8d1f-206">Если вы хотите включить префикс, например /api, он должен быть включен в свойство route.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-206">If you want to include a prefix such as /api, it must be included in the route property.</span></span>

### <span data-ttu-id="b8d1f-207"><a name="requestOverrides"></a>Определение объекта requestOverrides</span><span class="sxs-lookup"><span data-stu-id="b8d1f-207"><a name="requestOverrides"></a>Define a requestOverrides object</span></span>

<span data-ttu-id="b8d1f-208">Объект requestOverrides определяет изменения, внесенные в запрос во время вызова внутреннего ресурса.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-208">The requestOverrides object defines changes made to the request when the back-end resource is called.</span></span> <span data-ttu-id="b8d1f-209">Объект определяется следующими свойствами:</span><span class="sxs-lookup"><span data-stu-id="b8d1f-209">The object is defined by the following properties:</span></span>

* <span data-ttu-id="b8d1f-210">**backend.request.method.** Метод HTTP, используемый для вызова внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-210">**backend.request.method**: The HTTP method that's used to call the back end.</span></span>
* <span data-ttu-id="b8d1f-211">**backend.request.querystring.\<имя_параметра\>.** Параметр строки запроса, который можно задать для вызова внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-211">**backend.request.querystring.\<ParameterName\>**: A query string parameter that can be set for the call to the back end.</span></span> <span data-ttu-id="b8d1f-212">Замените *\<имя_параметра\>* именем параметра, который вы собираетесь задать.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-212">Replace *\<ParameterName\>* with the name of the parameter that you want to set.</span></span> <span data-ttu-id="b8d1f-213">Если указана пустая строка, параметр не включается в запрос внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-213">If the empty string is provided, the parameter is not included on the back-end request.</span></span>
* <span data-ttu-id="b8d1f-214">**backend.request.headers.\<имя_заголовка\>.** Заголовок, который можно задать для вызова внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-214">**backend.request.headers.\<HeaderName\>**: A header that can be set for the call to the back end.</span></span> <span data-ttu-id="b8d1f-215">Замените *\<имя_заголовка\>* именем заголовка, который вы собираетесь задать.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-215">Replace *\<HeaderName\>* with the name of the header that you want to set.</span></span> <span data-ttu-id="b8d1f-216">Если указана пустая строка, заголовок не включается в запрос внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-216">If you provide the empty string, the header is not included on the back-end request.</span></span>

<span data-ttu-id="b8d1f-217">Значения могут ссылаться на параметры приложения и параметры исходного запроса клиента.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-217">Values can reference application settings and parameters from the original client request.</span></span>

<span data-ttu-id="b8d1f-218">Пример конфигурации может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b8d1f-218">An example configuration might look like the following:</span></span>

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

### <span data-ttu-id="b8d1f-219"><a name="responseOverrides"></a>Определение объекта responseOverrides</span><span class="sxs-lookup"><span data-stu-id="b8d1f-219"><a name="responseOverrides"></a>Define a responseOverrides object</span></span>

<span data-ttu-id="b8d1f-220">Объект requestOverrides определяет изменения, внесенные в ответ, который передается обратно к клиенту.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-220">The requestOverrides object defines changes that are made to the response that's passed back to the client.</span></span> <span data-ttu-id="b8d1f-221">Объект определяется следующими свойствами:</span><span class="sxs-lookup"><span data-stu-id="b8d1f-221">The object is defined by the following properties:</span></span>

* <span data-ttu-id="b8d1f-222">**response.statusCode.** Код состояния HTTP, который будет возвращен клиенту.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-222">**response.statusCode**: The HTTP status code to be returned to the client.</span></span>
* <span data-ttu-id="b8d1f-223">**response.statusReason.** Описание HTTP, которое будет возвращено клиенту.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-223">**response.statusReason**: The HTTP reason phrase to be returned to the client.</span></span>
* <span data-ttu-id="b8d1f-224">**response.body.** Строковое представление текста, который будет возвращен клиенту.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-224">**response.body**: The string representation of the body to be returned to the client.</span></span>
* <span data-ttu-id="b8d1f-225">**response.headers.\<имя_заголовка\>.** Заголовок, который можно задать для ответа клиенту.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-225">**response.headers.\<HeaderName\>**: A header that can be set for the response to the client.</span></span> <span data-ttu-id="b8d1f-226">Замените *\<имя_заголовка\>* именем заголовка, который вы собираетесь задать.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-226">Replace *\<HeaderName\>* with the name of the header that you want to set.</span></span> <span data-ttu-id="b8d1f-227">Если указана пустая строка, заголовок не включается в ответ.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-227">If you provide the empty string, the header is not included on the response.</span></span>

<span data-ttu-id="b8d1f-228">Значения могут ссылаться на параметры приложения, параметры исходного запроса клиента и параметры ответа внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-228">Values can reference application settings, parameters from the original client request, and parameters from the back-end response.</span></span>

<span data-ttu-id="b8d1f-229">Пример конфигурации может выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b8d1f-229">An example configuration might look like the following:</span></span>

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
> <span data-ttu-id="b8d1f-230">В этом примере текст задается напрямую, поэтому задавать свойство `backendUri` не требуется.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-230">In this example, the body is being set directly, so no `backendUri` property is needed.</span></span> <span data-ttu-id="b8d1f-231">В примере показано, как можно использовать прокси-серверы Функций Azure для имитации API.</span><span class="sxs-lookup"><span data-stu-id="b8d1f-231">The example shows how you might use Azure Functions Proxies for mocking APIs.</span></span>

<span data-ttu-id="b8d1f-232">[портал Azure]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="b8d1f-232">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="b8d1f-233">[триггеров HTTP]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger</span><span class="sxs-lookup"><span data-stu-id="b8d1f-233">[HTTP triggers]: https://docs.microsoft.com/azure/azure-functions/functions-bindings-http-webhook#http-trigger</span></span>
[Modify the back-end request]: #modify-backend-request
[Modify the response]: #modify-response
<span data-ttu-id="b8d1f-234">[Определение объекта requestOverrides]: #requestOverrides</span><span class="sxs-lookup"><span data-stu-id="b8d1f-234">[Define a requestOverrides object]: #requestOverrides</span></span>
<span data-ttu-id="b8d1f-235">[Определение объекта responseOverrides]: #responseOverrides</span><span class="sxs-lookup"><span data-stu-id="b8d1f-235">[Define a responseOverrides object]: #responseOverrides</span></span>
<span data-ttu-id="b8d1f-236">[параметры приложения]: #use-appsettings</span><span class="sxs-lookup"><span data-stu-id="b8d1f-236">[application settings]: #use-appsettings</span></span>
<span data-ttu-id="b8d1f-237">[Использование переменных]: #using-variables</span><span class="sxs-lookup"><span data-stu-id="b8d1f-237">[Use variables]: #using-variables</span></span>
<span data-ttu-id="b8d1f-238">[параметры исходного запроса клиента]: #request-parameters</span><span class="sxs-lookup"><span data-stu-id="b8d1f-238">[parameters from the original client request]: #request-parameters</span></span>
<span data-ttu-id="b8d1f-239">[параметры ответа внутреннего сервера]: #response-parameters</span><span class="sxs-lookup"><span data-stu-id="b8d1f-239">[parameters from the back-end response]: #response-parameters</span></span>
