---
title: "Политики в службе управления API Azure | Документация Майкрософт"
description: "Сведения о политиках, доступных для использования в службе управления API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 1cc460cb-8e67-41aa-bc76-bbafc1892798
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 485dc3a87a81dc67f5144596a30d498293d6b76a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-policies"></a><span data-ttu-id="4246a-103">Политики управления API</span><span class="sxs-lookup"><span data-stu-id="4246a-103">API Management policies</span></span>
<span data-ttu-id="4246a-104">В этом разделе рассматриваются приведенные ниже политики управления API.</span><span class="sxs-lookup"><span data-stu-id="4246a-104">This section provides a reference for the following API Management policies.</span></span> <span data-ttu-id="4246a-105">Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в управлении API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="4246a-105">For information on adding and configuring policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
  
 <span data-ttu-id="4246a-106">Политики представляют собой одну из эффективных функций системы, позволяющих издателю изменять поведение интерфейса API путем его настройки.</span><span class="sxs-lookup"><span data-stu-id="4246a-106">Policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="4246a-107">Политика — это коллекция операторов, которые выполняются последовательно по запросу интерфейса API или при получении из него ответа.</span><span class="sxs-lookup"><span data-stu-id="4246a-107">Policies are a collection of Statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="4246a-108">К часто используемым операторам относятся преобразование формата из XML в JSON, а также ограничение скорости вызовов, позволяющее ограничивать количество входящих вызовов от разработчика.</span><span class="sxs-lookup"><span data-stu-id="4246a-108">Popular Statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer.</span></span> <span data-ttu-id="4246a-109">Также существует много готовых политик.</span><span class="sxs-lookup"><span data-stu-id="4246a-109">Many more policies are available out of the box.</span></span>  
  
 <span data-ttu-id="4246a-110">Выражения политики можно использовать в качестве значений атрибутов или текстовых значений в любой политике управления API, если в ней не указано иное.</span><span class="sxs-lookup"><span data-stu-id="4246a-110">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="4246a-111">Некоторые политики (включая [управление последовательностью](api-management-advanced-policies.md#choose) и [настройку переменной](api-management-advanced-policies.md#set-variable)) основаны на выражениях политики.</span><span class="sxs-lookup"><span data-stu-id="4246a-111">Some policies such as the [Control flow](api-management-advanced-policies.md#choose) and [Set variable](api-management-advanced-policies.md#set-variable) policies are based on policy expressions.</span></span> <span data-ttu-id="4246a-112">Дополнительную информацию см. в документации по [расширенным политикам](api-management-advanced-policies.md#AdvancedPolicies) и [выражениям политики](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="4246a-112">For more information, see [Advanced policies](api-management-advanced-policies.md#AdvancedPolicies) and [Policy expressions](api-management-policy-expressions.md).</span></span>  
  
##  <span data-ttu-id="4246a-113"><a name="ProxyPolicies"></a> Политики</span><span class="sxs-lookup"><span data-stu-id="4246a-113"><a name="ProxyPolicies"></a> Policies</span></span>  
  
-   [<span data-ttu-id="4246a-114">Политики ограничения доступа</span><span class="sxs-lookup"><span data-stu-id="4246a-114">Access restriction policies</span></span>](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   <span data-ttu-id="4246a-115">[Проверка заголовка HTTP](api-management-access-restriction-policies.md#CheckHTTPHeader) – обеспечивает принудительный ввод заголовка HTTP и/или его значения.</span><span class="sxs-lookup"><span data-stu-id="4246a-115">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
    -   <span data-ttu-id="4246a-116">[Ограничение частоты вызовов по подписке](api-management-access-restriction-policies.md#LimitCallRate) — предотвращает пики использования API, ограничивая частоту вызовов для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="4246a-116">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="4246a-117">[Ограничение частоты вызовов по ключу](api-management-access-restriction-policies.md#LimitCallRateByKey) — предотвращает пики использования API, ограничивая частоту вызовов по ключу.</span><span class="sxs-lookup"><span data-stu-id="4246a-117">[Limit call rate by key](api-management-access-restriction-policies.md#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="4246a-118">[Ограничение IP-адресов вызывающих объектов](api-management-access-restriction-policies.md#RestrictCallerIPs) – фильтрует (разрешает или запрещает) вызовы с конкретных IP-адресов и/или диапазонов адресов.</span><span class="sxs-lookup"><span data-stu-id="4246a-118">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
    -   <span data-ttu-id="4246a-119">[Задание квоты использования по подписке](api-management-access-restriction-policies.md#SetUsageQuota) — позволяет принудительно устанавливать возобновляемую или действующую в течение срока службы квоту на число вызовов и (или) квоту пропускной способности для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="4246a-119">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="4246a-120">[Задание квоты использования по ключу](api-management-access-restriction-policies.md#SetUsageQuotaByKey) — позволяет принудительно устанавливать возобновляемую или действующую в течение срока службы квоту на число вызовов и (или) квоту пропускной способности для каждого ключа.</span><span class="sxs-lookup"><span data-stu-id="4246a-120">[Set usage quota by key](api-management-access-restriction-policies.md#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="4246a-121">[Проверка JWT](api-management-access-restriction-policies.md#ValidateJWT) – обеспечивает принудительное задание и проверку JWT, извлеченного из заданного заголовка HTTP или параметра запроса.</span><span class="sxs-lookup"><span data-stu-id="4246a-121">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
-   [<span data-ttu-id="4246a-122">Расширенные политики</span><span class="sxs-lookup"><span data-stu-id="4246a-122">Advanced policies</span></span>](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   <span data-ttu-id="4246a-123">[Поток управления](api-management-advanced-policies.md#choose) — условно применяет правила политики на основе вычисления логических выражений.</span><span class="sxs-lookup"><span data-stu-id="4246a-123">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on the evaluation of Boolean expressions.</span></span>  
  
    -   <span data-ttu-id="4246a-124">[Перенаправляющий запрос](api-management-advanced-policies.md#ForwardRequest) — перенаправляет запрос в серверную службу.</span><span class="sxs-lookup"><span data-stu-id="4246a-124">[Forward request](api-management-advanced-policies.md#ForwardRequest) - Forwards the request to the backend service.</span></span>  
  
    -   <span data-ttu-id="4246a-125">[Регистрация в концентраторе событий](api-management-advanced-policies.md#log-to-eventhub) — отправляет сообщения в определенном формате объекту, который указан средством ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="4246a-125">[Log to Event Hub](api-management-advanced-policies.md#log-to-eventhub) - Sends messages in the specified format to a message target defined by a Logger entity.</span></span>  
  
    -   <span data-ttu-id="4246a-126">[Повторить](api-management-advanced-policies.md#Retry) — повторяет выполнение инструкций встраиваемой политики, если не выполнено условие и до тех пор пока оно не будет выполнено.</span><span class="sxs-lookup"><span data-stu-id="4246a-126">[Retry](api-management-advanced-policies.md#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="4246a-127">Выполнение будет повторяться через определенные промежутки времени и до указанного количества повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="4246a-127">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>  
  
    -   <span data-ttu-id="4246a-128">[Возврат ответа](api-management-advanced-policies.md#ReturnResponse) — прекращает выполнение конвейера и возвращает указанный ответ непосредственно вызывающему объекту.</span><span class="sxs-lookup"><span data-stu-id="4246a-128">[Return response](api-management-advanced-policies.md#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span>  
  
    -   <span data-ttu-id="4246a-129">[Отправка одностороннего запроса](api-management-advanced-policies.md#SendOneWayRequest) — отправляет запрос на указанный URL-адрес и не ожидает ответа.</span><span class="sxs-lookup"><span data-stu-id="4246a-129">[Send one way request](api-management-advanced-policies.md#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>  
  
    -   <span data-ttu-id="4246a-130">[Отправка запроса](api-management-advanced-policies.md#SendRequest) — отправляет запрос на указанный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="4246a-130">[Send request](api-management-advanced-policies.md#SendRequest) - Sends a request to the specified URL.</span></span>  
  
    -   <span data-ttu-id="4246a-131">[Задание переменной](api-management-advanced-policies.md#set-variable) — сохраняет значение в именованной переменной контекста для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="4246a-131">[Set variable](api-management-advanced-policies.md#set-variable) - Persist a value in a named context variable for later access.</span></span>  
  
    -   <span data-ttu-id="4246a-132">[Установка метода запроса](api-management-advanced-policies.md#SetRequestMethod) — позволяет изменить метод HTTP для запроса.</span><span class="sxs-lookup"><span data-stu-id="4246a-132">[Set request method](api-management-advanced-policies.md#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>  
  
    -   <span data-ttu-id="4246a-133">[Установка кода состояния](api-management-advanced-policies.md#SetStatus) — меняет код состояния HTTP на указанное значение.</span><span class="sxs-lookup"><span data-stu-id="4246a-133">[Set status code](api-management-advanced-policies.md#SetStatus) - Changes the HTTP status code to the specified value.</span></span>  
  
    -   <span data-ttu-id="4246a-134">[Трассировка](api-management-advanced-policies.md#Trace) — добавляет строку в выходные данные [инспектора API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/).</span><span class="sxs-lookup"><span data-stu-id="4246a-134">[Trace](api-management-advanced-policies.md#Trace) - Adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
    -   <span data-ttu-id="4246a-135">[Ожидание](api-management-advanced-policies.md#Wait) — ожидает завершения вложенных политик [запроса отправки](api-management-advanced-policies.md#SendRequest), [получения значения из кэша](api-management-caching-policies.md#GetFromCacheByKey) или [управления потоком](api-management-advanced-policies.md#choose) перед продолжением.</span><span class="sxs-lookup"><span data-stu-id="4246a-135">[Wait](api-management-advanced-policies.md#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies to complete before proceeding.</span></span>  
  
-   [<span data-ttu-id="4246a-136">Политики аутентификации</span><span class="sxs-lookup"><span data-stu-id="4246a-136">Authentication policies</span></span>](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   <span data-ttu-id="4246a-137">[Обычная проверка подлинности](api-management-authentication-policies.md#Basic) – обычная проверка подлинности внутренней службы.</span><span class="sxs-lookup"><span data-stu-id="4246a-137">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
    -   <span data-ttu-id="4246a-138">[Аутентификация с помощью сертификата клиента](api-management-authentication-policies.md#ClientCertificate) – аутентификация внутренней службы с помощью сертификатов клиентов.</span><span class="sxs-lookup"><span data-stu-id="4246a-138">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
-   [<span data-ttu-id="4246a-139">Политики кэширования</span><span class="sxs-lookup"><span data-stu-id="4246a-139">Caching policies</span></span>](api-management-caching-policies.md#CachingPolicies)  
  
    -   <span data-ttu-id="4246a-140">[Получение из кэша](api-management-caching-policies.md#GetFromCache) – выполнение операции поиска в кэше и возврат допустимого кэшированного ответа при его наличии.</span><span class="sxs-lookup"><span data-stu-id="4246a-140">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached response when available.</span></span>  
  
    -   <span data-ttu-id="4246a-141">[Сохранение в кэше](api-management-caching-policies.md#StoreToCache) – помещение в кэш ответа в соответствии с заданной конфигурацией управления кэшем.</span><span class="sxs-lookup"><span data-stu-id="4246a-141">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches response according to the specified cache control configuration.</span></span>  
  
    -   <span data-ttu-id="4246a-142">[Получение значения из кэша](api-management-caching-policies.md#GetFromCacheByKey) — получение кэшированного элемента по ключу.</span><span class="sxs-lookup"><span data-stu-id="4246a-142">[Get value from cache](api-management-caching-policies.md#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="4246a-143">[Сохранение значения в кэше](api-management-caching-policies.md#StoreToCacheByKey) — сохранение элемента в кэше по ключу.</span><span class="sxs-lookup"><span data-stu-id="4246a-143">[Store value in cache](api-management-caching-policies.md#StoreToCacheByKey) - Store an item in the cache by key.</span></span>  
  
    -   <span data-ttu-id="4246a-144">[Удалить значение из кэша](api-management-caching-policies.md#RemoveCacheByKey) — удаление элемента в кэше по ключу.</span><span class="sxs-lookup"><span data-stu-id="4246a-144">[Remove value from cache](api-management-caching-policies.md#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>  
  
-   [<span data-ttu-id="4246a-145">Кроссдоменные политики</span><span class="sxs-lookup"><span data-stu-id="4246a-145">Cross domain policies</span></span>](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   <span data-ttu-id="4246a-146">[Разрешение кросс-доменных вызовов](api-management-cross-domain-policies.md#AllowCrossDomainCalls) – делает API доступным из клиентов на основе браузеров Adobe Flash и Microsoft Silverlight.</span><span class="sxs-lookup"><span data-stu-id="4246a-146">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
    -   <span data-ttu-id="4246a-147">[CORS](api-management-cross-domain-policies.md#CORS) – добавляет поддержку общего доступа к ресурсам независимо от источника (CORS) для операции или API, чтобы разрешить кросс-доменные вызовы от клиентов на основе браузера.</span><span class="sxs-lookup"><span data-stu-id="4246a-147">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
    -   <span data-ttu-id="4246a-148">[JSONP](api-management-cross-domain-policies.md#JSONP) – добавляет поддержку JSON с заполнением (JSONP) для операции или API, чтобы разрешить кросс-доменные вызовы из браузерных клиентов JavaScript.</span><span class="sxs-lookup"><span data-stu-id="4246a-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
-   [<span data-ttu-id="4246a-149">Политики преобразования</span><span class="sxs-lookup"><span data-stu-id="4246a-149">Transformation policies</span></span>](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   <span data-ttu-id="4246a-150">[Преобразование JSON в XML](api-management-transformation-policies.md#ConvertJSONtoXML) – преобразует текст запроса или ответа в формате JSON в формат XML.</span><span class="sxs-lookup"><span data-stu-id="4246a-150">[Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON to XML.</span></span>  
  
    -   <span data-ttu-id="4246a-151">[Преобразование XML в JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) – преобразует текст запроса или ответа в формате XML в формат JSON.</span><span class="sxs-lookup"><span data-stu-id="4246a-151">[Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML to JSON.</span></span>  
  
    -   <span data-ttu-id="4246a-152">[Поиск и замена строки в тексте](api-management-transformation-policies.md#Findandreplacestringinbody) – отыскивает подстроку запроса или ответа и заменяет ее на другую подстроку.</span><span class="sxs-lookup"><span data-stu-id="4246a-152">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
    -   <span data-ttu-id="4246a-153">[Маскировка URL-адресов в содержимом](api-management-transformation-policies.md#MaskURLSContent) — перезаписывает (маскирует) ссылки в тексте ответа так, чтобы каждая из них указывала на эквивалентную ссылку через шлюз.</span><span class="sxs-lookup"><span data-stu-id="4246a-153">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>  
  
    -   <span data-ttu-id="4246a-154">[Задание внутренней службы](api-management-transformation-policies.md#SetBackendService) – изменяет внутреннюю службу для входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="4246a-154">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes the backend service for an incoming request.</span></span>  
  
    -   <span data-ttu-id="4246a-155">[Задание текста](api-management-transformation-policies.md#SetBody) – задает текст сообщения для входящих и исходящих запросов.</span><span class="sxs-lookup"><span data-stu-id="4246a-155">[Set body](api-management-transformation-policies.md#SetBody) - Sets the message body for incoming and outgoing requests.</span></span>  
  
    -   <span data-ttu-id="4246a-156">[Установка HTTP-заголовка](api-management-transformation-policies.md#SetHTTPheader) -– назначает значение существующему заголовку ответа и/или запроса или добавляет новый заголовок ответа и/или запроса.</span><span class="sxs-lookup"><span data-stu-id="4246a-156">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
    -   <span data-ttu-id="4246a-157">[Настройка параметра строки запроса](api-management-transformation-policies.md#SetQueryStringParameter) - добавляет, заменяет значение или удаляет параметр строки запроса.</span><span class="sxs-lookup"><span data-stu-id="4246a-157">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
    -   <span data-ttu-id="4246a-158">[Перезапись URL-адреса](api-management-transformation-policies.md#RewriteURL) – преобразует URL-адрес запроса из его общедоступной формы в форму, ожидаемую веб-службой.</span><span class="sxs-lookup"><span data-stu-id="4246a-158">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form to the form expected by the web service.</span></span>  
  
    -   <span data-ttu-id="4246a-159">[Преобразование XML с помощью XSLT](api-management-transformation-policies.md#XSLTransform) — применяет преобразование данных в формате XSL в формат XML в тексте запроса или ответа.</span><span class="sxs-lookup"><span data-stu-id="4246a-159">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation to XML in the request or response body.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="4246a-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4246a-160">Next steps</span></span>
<span data-ttu-id="4246a-161">Дополнительные сведения о работе с политиками см. в статье со справочными материалами по [политикам в службе управления API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="4246a-161">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
