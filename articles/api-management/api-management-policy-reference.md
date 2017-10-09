---
title: "aaaAzure Справочник по политикам управления API"
description: "Дополнительные сведения о доступных tooconfigure hello политики управления API."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 9d4ac609-b221-4032-93ae-e27a1254d43d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7ee194f4d6f172bf836c789cbe8ab732e18a7e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-policy-reference"></a><span data-ttu-id="374d7-103">Справочник по политикам службы управления Azure API </span><span class="sxs-lookup"><span data-stu-id="374d7-103">Azure API Management Policy Reference</span></span>
<span data-ttu-id="374d7-104">Этот раздел содержит индекс для политик hello в hello [Справочник по политикам управления API][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="374d7-104">This section provides an index for hello policies in hello [API Management policy reference][API Management policy reference].</span></span> <span data-ttu-id="374d7-105">Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в службе управления API][Policies in API Management].</span><span class="sxs-lookup"><span data-stu-id="374d7-105">For information on adding and configuring policies, see [Policies in API Management][Policies in API Management].</span></span>

<span data-ttu-id="374d7-106">Выражения политики может использоваться как значения атрибутов или текстовыми значениями в любой hello политиках управления интерфейсами API, если политика hello не указывает иное.</span><span class="sxs-lookup"><span data-stu-id="374d7-106">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="374d7-107">Некоторые политики, такие как hello [поток управления] [ Control flow] и [переменным] [ Set variable] политики основаны на выражениях политики.</span><span class="sxs-lookup"><span data-stu-id="374d7-107">Some policies such as hello [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="374d7-108">Чтобы узнать больше, ознакомьтесь с [расширенными политиками][Advanced policies] и [выражениями политики][Policy expressions].</span><span class="sxs-lookup"><span data-stu-id="374d7-108">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions]</span></span>

## <a name="policy-reference-index"></a><span data-ttu-id="374d7-109">Справочные указатели по политикам</span><span class="sxs-lookup"><span data-stu-id="374d7-109">Policy reference index</span></span>
* <span data-ttu-id="374d7-110">[Политики ограничения доступа][Access restriction policies]</span><span class="sxs-lookup"><span data-stu-id="374d7-110">[Access restriction policies][Access restriction policies]</span></span>
  * <span data-ttu-id="374d7-111">[Проверка заголовка HTTP][Check HTTP header] — обеспечивает принудительный ввод заголовка HTTP и (или) его значения.</span><span class="sxs-lookup"><span data-stu-id="374d7-111">[Check HTTP header][Check HTTP header] - Enforces existence and/or value of a HTTP Header.</span></span>
  * <span data-ttu-id="374d7-112">[Ограничение частоты вызовов по подписке][Limit call rate by subscription] — предотвращает пики использования API, ограничивая частоту вызовов для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="374d7-112">[Limit call rate by subscription][Limit call rate by subscription] - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>
  * <span data-ttu-id="374d7-113">[Ограничение частоты вызовов по ключу](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) — предотвращает пики использования API, ограничивая частоту вызовов по ключу.</span><span class="sxs-lookup"><span data-stu-id="374d7-113">[Limit call rate by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>
  * <span data-ttu-id="374d7-114">[Ограничение IP-адресов вызывающих объектов][Restrict caller IPs] — фильтрует (разрешает или запрещает) вызовы с конкретных IP-адресов и (или) диапазонов адресов.</span><span class="sxs-lookup"><span data-stu-id="374d7-114">[Restrict caller IPs][Restrict caller IPs] - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>
  * <span data-ttu-id="374d7-115">[Задание квоты использования по подписке] [ Set usage quota by subscription] -позволяет tooenforce задание продлеваемой или бессрочной квоты объема вызовов или полосы пропускания, для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="374d7-115">[Set usage quota by subscription][Set usage quota by subscription] - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>
  * <span data-ttu-id="374d7-116">[Задание квоты использования ключом](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) -позволяет tooenforce задание продлеваемой или бессрочной квоты объема вызовов или полосы пропускания, на основе каждого ключа.</span><span class="sxs-lookup"><span data-stu-id="374d7-116">[Set usage quota by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>
  * <span data-ttu-id="374d7-117">[Проверка JWT][Validate JWT] — обеспечивает принудительное задание и проверку маркера JWT, извлеченного из заданного заголовка HTTP или параметра запроса.</span><span class="sxs-lookup"><span data-stu-id="374d7-117">[Validate JWT][Validate JWT] - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>
* <span data-ttu-id="374d7-118">[Расширенные политики][Advanced policies]</span><span class="sxs-lookup"><span data-stu-id="374d7-118">[Advanced policies][Advanced policies]</span></span>
  * <span data-ttu-id="374d7-119">[Поток управления] [ Control flow] — условно применяет операторы политики на основе результатов вычисления логических hello hello [выражений][expressions].</span><span class="sxs-lookup"><span data-stu-id="374d7-119">[Control flow][Control flow] - Conditionally applies policy statements based on hello results of hello evaluation of Boolean [expressions][expressions].</span></span>
  * <span data-ttu-id="374d7-120">[Прямой запрос] [ Forward request] -пересылает hello запроса toohello внутренней службы.</span><span class="sxs-lookup"><span data-stu-id="374d7-120">[Forward request][Forward request] - Forwards hello request toohello backend service.</span></span>
  * <span data-ttu-id="374d7-121">[Журнал tooEvent концентратора] [ Log tooEvent Hub] -отправляет сообщения hello указанный формат tooa сообщение целевому определяется [средства ведения журнала](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) сущности.</span><span class="sxs-lookup"><span data-stu-id="374d7-121">[Log tooEvent Hub][Log tooEvent Hub] - Sends messages in hello specified format tooa message target defined by a [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entity.</span></span>
  * <span data-ttu-id="374d7-122">[Повторите](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) -повторных попыток выполнения hello заключены операторы политики, если и пока не будет выполнено условие hello.</span><span class="sxs-lookup"><span data-stu-id="374d7-122">[Retry](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="374d7-123">Выполнение будет сквозные hello определенные промежутки времени и копирование toohello указанное число повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="374d7-123">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>
  * <span data-ttu-id="374d7-124">[Вернуть ответ](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) -конвейера прерывания выполнения и возвращает hello указанного ответа непосредственно toohello вызывающего объекта.</span><span class="sxs-lookup"><span data-stu-id="374d7-124">[Return response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span>
  * <span data-ttu-id="374d7-125">[Отправка запроса на один из способов](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) -отправляет toohello запроса указан URL-адрес без ожидания ответа.</span><span class="sxs-lookup"><span data-stu-id="374d7-125">[Send one way request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>
  * <span data-ttu-id="374d7-126">[Отправка запроса](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) -отправляет toohello запроса указан URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="374d7-126">[Send request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) - Sends a request toohello specified URL.</span></span>
  * <span data-ttu-id="374d7-127">[Установка метода запроса](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) -позволяет toochange метод hello HTTP для запроса.</span><span class="sxs-lookup"><span data-stu-id="374d7-127">[Set request method](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>
  * <span data-ttu-id="374d7-128">[Задать состояние](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) -toohello код состояния hello HTTP изменения заданного значения.</span><span class="sxs-lookup"><span data-stu-id="374d7-128">[Set status](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>
  * <span data-ttu-id="374d7-129">[Задание переменной][Set variable] — сохраняет значение в именованной переменной [контекста][context] для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="374d7-129">[Set variable][Set variable] - Persist a value in a named [context][context] variable for later access.</span></span>
  * <span data-ttu-id="374d7-130">[Трассировки](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) -добавляет строку в hello [инспектора API](api-management-howto-api-inspector.md) выходных данных.</span><span class="sxs-lookup"><span data-stu-id="374d7-130">[Trace](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) - Adds a string into hello [API Inspector](api-management-howto-api-inspector.md) output.</span></span>
  * <span data-ttu-id="374d7-131">[Подождите](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) — ожидает отправки вложенный запрос, получение значения из кэша или управлять toocomplete политики потока, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="374d7-131">[Wait](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - Waits for enclosed Send request, Get value from cache, or Control flow policies toocomplete before proceeding.</span></span>
* <span data-ttu-id="374d7-132">[Политики аутентификации][Authentication policies]</span><span class="sxs-lookup"><span data-stu-id="374d7-132">[Authentication policies][Authentication policies]</span></span>
  * <span data-ttu-id="374d7-133">[Обычная проверка подлинности][Authenticate with Basic] – обычная проверка подлинности внутренней службы.</span><span class="sxs-lookup"><span data-stu-id="374d7-133">[Authenticate with Basic][Authenticate with Basic] - Authenticate with a backend service using Basic authentication.</span></span>
  * <span data-ttu-id="374d7-134">[Аутентификация с помощью сертификата клиента][Authenticate with client certificate] – аутентификация внутренней службы с помощью сертификатов клиентов.</span><span class="sxs-lookup"><span data-stu-id="374d7-134">[Authenticate with client certificate][Authenticate with client certificate] - Authenticate with a backend service using client certificates.</span></span>
* <span data-ttu-id="374d7-135">[Политики кэширования][Caching policies]</span><span class="sxs-lookup"><span data-stu-id="374d7-135">[Caching policies][Caching policies]</span></span> 
  * <span data-ttu-id="374d7-136">[Получение из кэша][Get from cache] — выполнение поиска в кэше и возврат допустимого кэшированного ответа при его наличии.</span><span class="sxs-lookup"><span data-stu-id="374d7-136">[Get from cache][Get from cache] - Perform cache look up and return a valid cached response when available.</span></span>
  * <span data-ttu-id="374d7-137">[Хранить toocache] [ Store toocache] -кэши ответа в соответствии с toohello указана конфигурация управления кэша.</span><span class="sxs-lookup"><span data-stu-id="374d7-137">[Store toocache][Store toocache] - Caches response according toohello specified cache control configuration.</span></span>
  * <span data-ttu-id="374d7-138">[Получение значения из кэша](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) — получение кэшированного элемента по ключу.</span><span class="sxs-lookup"><span data-stu-id="374d7-138">[Get value from cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>
  * <span data-ttu-id="374d7-139">[Сохраните значение в кэше](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) -хранения элемента в кэше hello по ключу.</span><span class="sxs-lookup"><span data-stu-id="374d7-139">[Store value in cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>
  * <span data-ttu-id="374d7-140">[Удалить значение из кэша](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) -удалить элемент из кэша hello по ключу.</span><span class="sxs-lookup"><span data-stu-id="374d7-140">[Remove value from cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>
* <span data-ttu-id="374d7-141">[Междоменные политики][Cross domain policies]</span><span class="sxs-lookup"><span data-stu-id="374d7-141">[Cross domain policies][Cross domain policies]</span></span> 
  * <span data-ttu-id="374d7-142">[Разрешить междоменные вызовы] [ Allow cross-domain calls] -становится доступным hello API из клиентов Adobe Flash и Microsoft Silverlight на основе браузера.</span><span class="sxs-lookup"><span data-stu-id="374d7-142">[Allow cross-domain calls][Allow cross-domain calls] - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>
  * <span data-ttu-id="374d7-143">[CORS] [ CORS] -добавляет ресурсов независимо от источника (CORS) для управления доступом поддерживает операцию tooan или API tooallow междоменные вызовы из браузерных клиентов.</span><span class="sxs-lookup"><span data-stu-id="374d7-143">[CORS][CORS] - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>
  * <span data-ttu-id="374d7-144">[JSONP] [ JSONP] - добавляет JSON с заполнением (JSONP) поддержка tooan операции или API tooallow междоменные вызовы из браузерных клиентов JavaScript.</span><span class="sxs-lookup"><span data-stu-id="374d7-144">[JSONP][JSONP] - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>
* <span data-ttu-id="374d7-145">[Политики преобразования][Transformation policies]</span><span class="sxs-lookup"><span data-stu-id="374d7-145">[Transformation policies][Transformation policies]</span></span> 
  * <span data-ttu-id="374d7-146">[Преобразование JSON tooXML] [ Convert JSON tooXML] - преобразует запрос или текст ответа от JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="374d7-146">[Convert JSON tooXML][Convert JSON tooXML] - Converts request or response body from JSON tooXML.</span></span>
  * <span data-ttu-id="374d7-147">[Преобразование XML tooJSON] [ Convert XML tooJSON] - преобразует запрос, или из XML tooJSON текст ответа.</span><span class="sxs-lookup"><span data-stu-id="374d7-147">[Convert XML tooJSON][Convert XML tooJSON] - Converts request or response body from XML tooJSON.</span></span>
  * <span data-ttu-id="374d7-148">[Поиск и замена строки в тексте][Find and replace string in body] — позволяет найти подстроку запроса или ответа и заменить ее на другую подстроку.</span><span class="sxs-lookup"><span data-stu-id="374d7-148">[Find and replace string in body][Find and replace string in body] - Finds a request or response substring and replaces it with a different substring.</span></span>
  * <span data-ttu-id="374d7-149">[Маскировать URL-адреса в содержимом] [ Mask URLs in content] -загрузочную запись (маскировка) ссылок в ответ hello текста, чтобы они указывали toohello равнозначными ссылками через шлюз hello.</span><span class="sxs-lookup"><span data-stu-id="374d7-149">[Mask URLs in content][Mask URLs in content] - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>
  * <span data-ttu-id="374d7-150">[Задать серверная служба] [ Set backend service] -изменяет hello серверную службу для входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="374d7-150">[Set backend service][Set backend service] - Changes hello backend service for an incoming request.</span></span>
  * <span data-ttu-id="374d7-151">[Задайте текст] [ Set body] -задает текст сообщения hello для входящих и исходящих запросов.</span><span class="sxs-lookup"><span data-stu-id="374d7-151">[Set body][Set body] - Sets hello message body for incoming and outgoing requests.</span></span>
  * <span data-ttu-id="374d7-152">[Задание заголовка HTTP] [ Set HTTP header] - назначает значение tooan существующего ответа и/или заголовка запроса или Добавление нового заголовка ответа и/или запроса.</span><span class="sxs-lookup"><span data-stu-id="374d7-152">[Set HTTP header][Set HTTP header] - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>
  * <span data-ttu-id="374d7-153">[Настройка параметра строки запроса][Set query string parameter] — добавляет, заменяет значение или удаляет параметр строки запроса.</span><span class="sxs-lookup"><span data-stu-id="374d7-153">[Set query string parameter][Set query string parameter] - Adds, replaces value of, or deletes request query string parameter.</span></span>
  * <span data-ttu-id="374d7-154">[Замена URL-адреса] [ Rewrite URL] -преобразование URL-АДРЕСЕ запроса из общеупотребительной формы формы toohello ожидаемый hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="374d7-154">[Rewrite URL][Rewrite URL] - Converts a request URL from its public form toohello form expected by hello web service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="374d7-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="374d7-155">Next steps</span></span>
<span data-ttu-id="374d7-156">Дополнительные сведения о выражениях политики см. следующие видео hello.</span><span class="sxs-lookup"><span data-stu-id="374d7-156">For more information on policy expressions, see hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Access restriction policies]: https://msdn.microsoft.com/library/azure/dn894078.aspx
[Check HTTP header]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#CheckHTTPHeader
[Limit call rate by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#LimitCallRate
[Restrict caller IPs]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#RestrictCallerIPs
[Set usage quota by subscription]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#SetUsageQuota
[Validate JWT]: https://msdn.microsoft.com/library/azure/034febe3-465f-4840-9fc6-c448ef520b0f#ValidateJWT

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx
[context]: https://msdn.microsoft.com/library/azure/ea160028-fc04-4782-aa26-4b8329df3448#ContextVariables
[Forward request]: https://msdn.microsoft.com/library/azure/dn894085.aspx#ForwardRequest
[Log tooEvent Hub]: https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub

[Authentication policies]: https://msdn.microsoft.com/library/azure/dn894079.aspx
[Authenticate with Basic]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#Basic
[Authenticate with client certificate]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#ClientCertificate
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx
[Get from cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#GetFromCache
[Store toocache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#StoreToCache

[Cross domain policies]: https://msdn.microsoft.com/library/azure/dn894084.aspx
[Allow cross-domain calls]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#AllowCrossDomainCalls
[CORS]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#CORS
[JSONP]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#JSONP

[Transformation policies]: https://msdn.microsoft.com/library/azure/dn894083.aspx
[Convert JSON tooXML]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertJSONtoXML
[Convert XML tooJSON]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertXMLtoJSON
[Find and replace string in body]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#Findandreplacestringinbody
[Mask URLs in content]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#MaskURLSContent
[Set backend service]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetBackendService
[Set body]: https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBody
[Set HTTP header]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetHTTPheader
[Set query string parameter]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#SetQueryStringParameter
[Rewrite URL]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#RewriteURL



[Policies in API Management]: api-management-howto-policies.md
[API Management policy reference]: https://msdn.microsoft.com/library/azure/dn894081.aspx

[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx


