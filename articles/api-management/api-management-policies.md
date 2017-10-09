---
title: "политики управления API aaaAzure | Документы Microsoft"
description: "Дополнительные сведения о политиках hello, доступные для использования в службе управления API Azure."
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
ms.openlocfilehash: 1c468ff37d73359f1dd694b91e20c2ca04f8934e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-policies"></a><span data-ttu-id="c0913-103">Политики управления API</span><span class="sxs-lookup"><span data-stu-id="c0913-103">API Management policies</span></span>
<span data-ttu-id="c0913-104">Этот раздел предоставляет справку для следующих политиках управления интерфейсами API hello.</span><span class="sxs-lookup"><span data-stu-id="c0913-104">This section provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="c0913-105">Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в управлении API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="c0913-105">For information on adding and configuring policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
  
 <span data-ttu-id="c0913-106">Политики — это мощная возможность системы hello, разрешить издателю hello поведение hello toochange hello API через конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="c0913-106">Policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="c0913-107">Политики представляют собой набор инструкций, которые выполняются последовательно, по запросу hello или ответу API-интерфейса.</span><span class="sxs-lookup"><span data-stu-id="c0913-107">Policies are a collection of Statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="c0913-108">Среди наиболее популярных инструкций вспомнить преобразование формата XML tooJSON и toorestrict hello объема входящих вызовов от разработчика ограничение частоты вызовов.</span><span class="sxs-lookup"><span data-stu-id="c0913-108">Popular Statements include format conversion from XML tooJSON and call rate limiting toorestrict hello amount of incoming calls from a developer.</span></span> <span data-ttu-id="c0913-109">Стандартной hello доступны многие дополнительные политики.</span><span class="sxs-lookup"><span data-stu-id="c0913-109">Many more policies are available out of hello box.</span></span>  
  
 <span data-ttu-id="c0913-110">Выражения политики может использоваться как значения атрибутов или текстовыми значениями в любой hello политиках управления интерфейсами API, если политика hello не указывает иное.</span><span class="sxs-lookup"><span data-stu-id="c0913-110">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="c0913-111">Некоторые политики, такие как hello [поток управления](api-management-advanced-policies.md#choose) и [переменным](api-management-advanced-policies.md#set-variable) политики основаны на выражениях политики.</span><span class="sxs-lookup"><span data-stu-id="c0913-111">Some policies such as hello [Control flow](api-management-advanced-policies.md#choose) and [Set variable](api-management-advanced-policies.md#set-variable) policies are based on policy expressions.</span></span> <span data-ttu-id="c0913-112">Дополнительную информацию см. в документации по [расширенным политикам](api-management-advanced-policies.md#AdvancedPolicies) и [выражениям политики](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="c0913-112">For more information, see [Advanced policies](api-management-advanced-policies.md#AdvancedPolicies) and [Policy expressions](api-management-policy-expressions.md).</span></span>  
  
##  <span data-ttu-id="c0913-113"><a name="ProxyPolicies"></a> Политики</span><span class="sxs-lookup"><span data-stu-id="c0913-113"><a name="ProxyPolicies"></a> Policies</span></span>  
  
-   [<span data-ttu-id="c0913-114">Политики ограничения доступа</span><span class="sxs-lookup"><span data-stu-id="c0913-114">Access restriction policies</span></span>](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   <span data-ttu-id="c0913-115">[Проверка заголовка HTTP](api-management-access-restriction-policies.md#CheckHTTPHeader) – обеспечивает принудительный ввод заголовка HTTP и/или его значения.</span><span class="sxs-lookup"><span data-stu-id="c0913-115">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
    -   <span data-ttu-id="c0913-116">[Ограничение частоты вызовов по подписке](api-management-access-restriction-policies.md#LimitCallRate) — предотвращает пики использования API, ограничивая частоту вызовов для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="c0913-116">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="c0913-117">[Ограничение частоты вызовов по ключу](api-management-access-restriction-policies.md#LimitCallRateByKey) — предотвращает пики использования API, ограничивая частоту вызовов по ключу.</span><span class="sxs-lookup"><span data-stu-id="c0913-117">[Limit call rate by key](api-management-access-restriction-policies.md#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="c0913-118">[Ограничение IP-адресов вызывающих объектов](api-management-access-restriction-policies.md#RestrictCallerIPs) – фильтрует (разрешает или запрещает) вызовы с конкретных IP-адресов и/или диапазонов адресов.</span><span class="sxs-lookup"><span data-stu-id="c0913-118">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
    -   <span data-ttu-id="c0913-119">[Задание квоты использования по подписке](api-management-access-restriction-policies.md#SetUsageQuota) -позволяет tooenforce задание продлеваемой или бессрочной квоты объема вызовов или полосы пропускания, для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="c0913-119">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
    -   <span data-ttu-id="c0913-120">[Задание квоты использования ключом](api-management-access-restriction-policies.md#SetUsageQuotaByKey) -позволяет tooenforce задание продлеваемой или бессрочной квоты объема вызовов или полосы пропускания, на основе каждого ключа.</span><span class="sxs-lookup"><span data-stu-id="c0913-120">[Set usage quota by key](api-management-access-restriction-policies.md#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
    -   <span data-ttu-id="c0913-121">[Проверка JWT](api-management-access-restriction-policies.md#ValidateJWT) – обеспечивает принудительное задание и проверку JWT, извлеченного из заданного заголовка HTTP или параметра запроса.</span><span class="sxs-lookup"><span data-stu-id="c0913-121">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
-   [<span data-ttu-id="c0913-122">Расширенные политики</span><span class="sxs-lookup"><span data-stu-id="c0913-122">Advanced policies</span></span>](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   <span data-ttu-id="c0913-123">[Поток управления](api-management-advanced-policies.md#choose) — условно применяет операторы политики на основании оценки hello логических выражений.</span><span class="sxs-lookup"><span data-stu-id="c0913-123">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on hello evaluation of Boolean expressions.</span></span>  
  
    -   <span data-ttu-id="c0913-124">[Прямой запрос](api-management-advanced-policies.md#ForwardRequest) -пересылает hello запроса toohello внутренней службы.</span><span class="sxs-lookup"><span data-stu-id="c0913-124">[Forward request](api-management-advanced-policies.md#ForwardRequest) - Forwards hello request toohello backend service.</span></span>  
  
    -   <span data-ttu-id="c0913-125">[Журнал tooEvent концентратора](api-management-advanced-policies.md#log-to-eventhub) -отправляет сообщения hello указанный формат tooa сообщение целевому определяются сущности средства ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="c0913-125">[Log tooEvent Hub](api-management-advanced-policies.md#log-to-eventhub) - Sends messages in hello specified format tooa message target defined by a Logger entity.</span></span>  
  
    -   <span data-ttu-id="c0913-126">[Повторите](api-management-advanced-policies.md#Retry) -повторных попыток выполнения hello заключены операторы политики, если и пока не будет выполнено условие hello.</span><span class="sxs-lookup"><span data-stu-id="c0913-126">[Retry](api-management-advanced-policies.md#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="c0913-127">Выполнение будет сквозные hello определенные промежутки времени и копирование toohello указанное число повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="c0913-127">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>  
  
    -   <span data-ttu-id="c0913-128">[Вернуть ответ](api-management-advanced-policies.md#ReturnResponse) -конвейера прерывания выполнения и возвращает hello указанного ответа непосредственно toohello вызывающего объекта.</span><span class="sxs-lookup"><span data-stu-id="c0913-128">[Return response](api-management-advanced-policies.md#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span>  
  
    -   <span data-ttu-id="c0913-129">[Отправка запроса на один из способов](api-management-advanced-policies.md#SendOneWayRequest) -отправляет toohello запроса указан URL-адрес без ожидания ответа.</span><span class="sxs-lookup"><span data-stu-id="c0913-129">[Send one way request](api-management-advanced-policies.md#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>  
  
    -   <span data-ttu-id="c0913-130">[Отправка запроса](api-management-advanced-policies.md#SendRequest) -отправляет toohello запроса указан URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="c0913-130">[Send request](api-management-advanced-policies.md#SendRequest) - Sends a request toohello specified URL.</span></span>  
  
    -   <span data-ttu-id="c0913-131">[Задание переменной](api-management-advanced-policies.md#set-variable) — сохраняет значение в именованной переменной контекста для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="c0913-131">[Set variable](api-management-advanced-policies.md#set-variable) - Persist a value in a named context variable for later access.</span></span>  
  
    -   <span data-ttu-id="c0913-132">[Установка метода запроса](api-management-advanced-policies.md#SetRequestMethod) -позволяет toochange метод hello HTTP для запроса.</span><span class="sxs-lookup"><span data-stu-id="c0913-132">[Set request method](api-management-advanced-policies.md#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>  
  
    -   <span data-ttu-id="c0913-133">[Задать код состояния](api-management-advanced-policies.md#SetStatus) -toohello код состояния hello HTTP изменения заданного значения.</span><span class="sxs-lookup"><span data-stu-id="c0913-133">[Set status code](api-management-advanced-policies.md#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>  
  
    -   <span data-ttu-id="c0913-134">[Трассировки](api-management-advanced-policies.md#Trace) -добавляет строку в hello [инспектора API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) выходных данных.</span><span class="sxs-lookup"><span data-stu-id="c0913-134">[Trace](api-management-advanced-policies.md#Trace) - Adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
    -   <span data-ttu-id="c0913-135">[Подождите](api-management-advanced-policies.md#Wait) -ожидает заключены [запрос на отправку](api-management-advanced-policies.md#SendRequest), [получить значение из кэша](api-management-caching-policies.md#GetFromCacheByKey), или [поток управления](api-management-advanced-policies.md#choose) toocomplete политики, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="c0913-135">[Wait](api-management-advanced-policies.md#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies toocomplete before proceeding.</span></span>  
  
-   [<span data-ttu-id="c0913-136">Политики аутентификации</span><span class="sxs-lookup"><span data-stu-id="c0913-136">Authentication policies</span></span>](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   <span data-ttu-id="c0913-137">[Обычная проверка подлинности](api-management-authentication-policies.md#Basic) – обычная проверка подлинности внутренней службы.</span><span class="sxs-lookup"><span data-stu-id="c0913-137">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
    -   <span data-ttu-id="c0913-138">[Аутентификация с помощью сертификата клиента](api-management-authentication-policies.md#ClientCertificate) – аутентификация внутренней службы с помощью сертификатов клиентов.</span><span class="sxs-lookup"><span data-stu-id="c0913-138">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
-   [<span data-ttu-id="c0913-139">Политики кэширования</span><span class="sxs-lookup"><span data-stu-id="c0913-139">Caching policies</span></span>](api-management-caching-policies.md#CachingPolicies)  
  
    -   <span data-ttu-id="c0913-140">[Получение из кэша](api-management-caching-policies.md#GetFromCache) – выполнение операции поиска в кэше и возврат допустимого кэшированного ответа при его наличии.</span><span class="sxs-lookup"><span data-stu-id="c0913-140">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached response when available.</span></span>  
  
    -   <span data-ttu-id="c0913-141">[Хранить toocache](api-management-caching-policies.md#StoreToCache) -кэши ответа в соответствии с toohello указана конфигурация управления кэша.</span><span class="sxs-lookup"><span data-stu-id="c0913-141">[Store toocache](api-management-caching-policies.md#StoreToCache) - Caches response according toohello specified cache control configuration.</span></span>  
  
    -   <span data-ttu-id="c0913-142">[Получение значения из кэша](api-management-caching-policies.md#GetFromCacheByKey) — получение кэшированного элемента по ключу.</span><span class="sxs-lookup"><span data-stu-id="c0913-142">[Get value from cache](api-management-caching-policies.md#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="c0913-143">[Сохраните значение в кэше](api-management-caching-policies.md#StoreToCacheByKey) -хранения элемента в кэше hello по ключу.</span><span class="sxs-lookup"><span data-stu-id="c0913-143">[Store value in cache](api-management-caching-policies.md#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>  
  
    -   <span data-ttu-id="c0913-144">[Удалить значение из кэша](api-management-caching-policies.md#RemoveCacheByKey) -удалить элемент из кэша hello по ключу.</span><span class="sxs-lookup"><span data-stu-id="c0913-144">[Remove value from cache](api-management-caching-policies.md#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>  
  
-   [<span data-ttu-id="c0913-145">Кроссдоменные политики</span><span class="sxs-lookup"><span data-stu-id="c0913-145">Cross domain policies</span></span>](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   <span data-ttu-id="c0913-146">[Разрешить междоменные вызовы](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -становится доступным hello API из клиентов Adobe Flash и Microsoft Silverlight на основе браузера.</span><span class="sxs-lookup"><span data-stu-id="c0913-146">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
    -   <span data-ttu-id="c0913-147">[CORS](api-management-cross-domain-policies.md#CORS) -добавляет ресурсов независимо от источника (CORS) для управления доступом поддерживает операцию tooan или API tooallow междоменные вызовы из браузерных клиентов.</span><span class="sxs-lookup"><span data-stu-id="c0913-147">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
    -   <span data-ttu-id="c0913-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - добавляет JSON с заполнением (JSONP) поддержка tooan операции или API tooallow междоменные вызовы из браузерных клиентов JavaScript.</span><span class="sxs-lookup"><span data-stu-id="c0913-148">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
-   [<span data-ttu-id="c0913-149">Политики преобразования</span><span class="sxs-lookup"><span data-stu-id="c0913-149">Transformation policies</span></span>](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   <span data-ttu-id="c0913-150">[Преобразование JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - преобразует запрос или текст ответа от JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="c0913-150">[Convert JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON tooXML.</span></span>  
  
    -   <span data-ttu-id="c0913-151">[Преобразование XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - преобразует запрос, или из XML tooJSON текст ответа.</span><span class="sxs-lookup"><span data-stu-id="c0913-151">[Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML tooJSON.</span></span>  
  
    -   <span data-ttu-id="c0913-152">[Поиск и замена строки в тексте](api-management-transformation-policies.md#Findandreplacestringinbody) – отыскивает подстроку запроса или ответа и заменяет ее на другую подстроку.</span><span class="sxs-lookup"><span data-stu-id="c0913-152">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
    -   <span data-ttu-id="c0913-153">[Маскировать URL-адреса в содержимом](api-management-transformation-policies.md#MaskURLSContent) -загрузочную запись (маскировка) ссылок в ответ hello текста, чтобы они указывали toohello равнозначными ссылками через шлюз hello.</span><span class="sxs-lookup"><span data-stu-id="c0913-153">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>  
  
    -   <span data-ttu-id="c0913-154">[Задать серверной службе](api-management-transformation-policies.md#SetBackendService) -изменяет hello серверную службу для входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="c0913-154">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes hello backend service for an incoming request.</span></span>  
  
    -   <span data-ttu-id="c0913-155">[Задайте текст](api-management-transformation-policies.md#SetBody) -задает текст сообщения hello для входящих и исходящих запросов.</span><span class="sxs-lookup"><span data-stu-id="c0913-155">[Set body](api-management-transformation-policies.md#SetBody) - Sets hello message body for incoming and outgoing requests.</span></span>  
  
    -   <span data-ttu-id="c0913-156">[Задание заголовка HTTP](api-management-transformation-policies.md#SetHTTPheader) - назначает значение tooan существующего ответа и/или заголовка запроса или Добавление нового заголовка ответа и/или запроса.</span><span class="sxs-lookup"><span data-stu-id="c0913-156">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
    -   <span data-ttu-id="c0913-157">[Настройка параметра строки запроса](api-management-transformation-policies.md#SetQueryStringParameter) - добавляет, заменяет значение или удаляет параметр строки запроса.</span><span class="sxs-lookup"><span data-stu-id="c0913-157">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
    -   <span data-ttu-id="c0913-158">[Замена URL-адреса](api-management-transformation-policies.md#RewriteURL) -преобразование URL-АДРЕСЕ запроса из общеупотребительной формы формы toohello ожидаемый hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="c0913-158">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form toohello form expected by hello web service.</span></span>  
  
    -   <span data-ttu-id="c0913-159">[Преобразования XML с помощью XSLT](api-management-transformation-policies.md#XSLTransform) -применяется tooXML преобразование XSL в тексте запроса или ответа hello.</span><span class="sxs-lookup"><span data-stu-id="c0913-159">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="c0913-160">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c0913-160">Next steps</span></span>
<span data-ttu-id="c0913-161">Дополнительные сведения о работе с политиками см. в статье со справочными материалами по [политикам в службе управления API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="c0913-161">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
