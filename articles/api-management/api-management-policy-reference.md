---
title: "Справочник по политикам службы управления Azure API"
description: "Сведения о политиках, доступных для настройки службы управления API."
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
ms.openlocfilehash: adc0c4415e10ddd0b4994cecef17f026546e91a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="azure-api-management-policy-reference"></a><span data-ttu-id="0d969-103">Справочник по политикам службы управления Azure API </span><span class="sxs-lookup"><span data-stu-id="0d969-103">Azure API Management Policy Reference</span></span>
<span data-ttu-id="0d969-104">Этот раздел содержит указатель политик, перечисленных в [справочнике по политикам службы управления API][API Management policy reference].</span><span class="sxs-lookup"><span data-stu-id="0d969-104">This section provides an index for the policies in the [API Management policy reference][API Management policy reference].</span></span> <span data-ttu-id="0d969-105">Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в службе управления API][Policies in API Management].</span><span class="sxs-lookup"><span data-stu-id="0d969-105">For information on adding and configuring policies, see [Policies in API Management][Policies in API Management].</span></span>

<span data-ttu-id="0d969-106">Выражения политики можно использовать в качестве значений атрибутов или текстовых значений в любой политике управления API, если в ней не указано иное.</span><span class="sxs-lookup"><span data-stu-id="0d969-106">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="0d969-107">Некоторые политики (включая [Поток управления][Control flow] и [Задание переменной][Set variable]) основаны на выражениях политики.</span><span class="sxs-lookup"><span data-stu-id="0d969-107">Some policies such as the [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="0d969-108">Чтобы узнать больше, ознакомьтесь с [расширенными политиками][Advanced policies] и [выражениями политики][Policy expressions].</span><span class="sxs-lookup"><span data-stu-id="0d969-108">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions]</span></span>

## <a name="policy-reference-index"></a><span data-ttu-id="0d969-109">Справочные указатели по политикам</span><span class="sxs-lookup"><span data-stu-id="0d969-109">Policy reference index</span></span>
* <span data-ttu-id="0d969-110">[Политики ограничения доступа][Access restriction policies]</span><span class="sxs-lookup"><span data-stu-id="0d969-110">[Access restriction policies][Access restriction policies]</span></span>
  * <span data-ttu-id="0d969-111">[Проверка заголовка HTTP][Check HTTP header] — обеспечивает принудительный ввод заголовка HTTP и (или) его значения.</span><span class="sxs-lookup"><span data-stu-id="0d969-111">[Check HTTP header][Check HTTP header] - Enforces existence and/or value of a HTTP Header.</span></span>
  * <span data-ttu-id="0d969-112">[Ограничение частоты вызовов по подписке][Limit call rate by subscription] — предотвращает пики использования API, ограничивая частоту вызовов для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="0d969-112">[Limit call rate by subscription][Limit call rate by subscription] - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>
  * <span data-ttu-id="0d969-113">[Ограничение частоты вызовов по ключу](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) — предотвращает пики использования API, ограничивая частоту вызовов по ключу.</span><span class="sxs-lookup"><span data-stu-id="0d969-113">[Limit call rate by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>
  * <span data-ttu-id="0d969-114">[Ограничение IP-адресов вызывающих объектов][Restrict caller IPs] — фильтрует (разрешает или запрещает) вызовы с конкретных IP-адресов и (или) диапазонов адресов.</span><span class="sxs-lookup"><span data-stu-id="0d969-114">[Restrict caller IPs][Restrict caller IPs] - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>
  * <span data-ttu-id="0d969-115">[Задание квоты использования по подписке][Set usage quota by subscription] — позволяет принудительно устанавливать возобновляемую или действующую в течение срока службы квоту на число вызовов и (или) квоту пропускной способности для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="0d969-115">[Set usage quota by subscription][Set usage quota by subscription] - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>
  * <span data-ttu-id="0d969-116">[Задание квоты использования по ключу](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) — позволяет принудительно устанавливать возобновляемую или действующую в течение срока службы квоту на число вызовов и (или) квоту пропускной способности для каждого ключа.</span><span class="sxs-lookup"><span data-stu-id="0d969-116">[Set usage quota by key](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>
  * <span data-ttu-id="0d969-117">[Проверка JWT][Validate JWT] — обеспечивает принудительное задание и проверку маркера JWT, извлеченного из заданного заголовка HTTP или параметра запроса.</span><span class="sxs-lookup"><span data-stu-id="0d969-117">[Validate JWT][Validate JWT] - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>
* <span data-ttu-id="0d969-118">[Расширенные политики][Advanced policies]</span><span class="sxs-lookup"><span data-stu-id="0d969-118">[Advanced policies][Advanced policies]</span></span>
  * <span data-ttu-id="0d969-119">[Поток управления][Control flow] — условно применяет правила политики на основе результатов вычисления логических [выражений][expressions].</span><span class="sxs-lookup"><span data-stu-id="0d969-119">[Control flow][Control flow] - Conditionally applies policy statements based on the results of the evaluation of Boolean [expressions][expressions].</span></span>
  * <span data-ttu-id="0d969-120">[Перенаправляющий запрос][Forward request] — перенаправляет запрос во внутреннюю службу.</span><span class="sxs-lookup"><span data-stu-id="0d969-120">[Forward request][Forward request] - Forwards the request to the backend service.</span></span>
  * <span data-ttu-id="0d969-121">[Регистрация в концентраторе событий][Log to Event Hub] — отправляет сообщения в определенном формате объекту, который указан сущностью [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger).</span><span class="sxs-lookup"><span data-stu-id="0d969-121">[Log to Event Hub][Log to Event Hub] - Sends messages in the specified format to a message target defined by a [Logger](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) entity.</span></span>
  * <span data-ttu-id="0d969-122">[Повторить](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) — повторяет выполнение инструкций встраиваемой политики, если не выполнено условие и до тех пор пока оно не будет выполнено.</span><span class="sxs-lookup"><span data-stu-id="0d969-122">[Retry](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="0d969-123">Выполнение будет повторяться через определенные промежутки времени и до указанного количества повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="0d969-123">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>
  * <span data-ttu-id="0d969-124">[Возврат ответа](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) — прекращает выполнение конвейера и возвращает указанный ответ непосредственно вызывающему объекту.</span><span class="sxs-lookup"><span data-stu-id="0d969-124">[Return response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span>
  * <span data-ttu-id="0d969-125">[Отправка одностороннего запроса](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) — отправляет запрос на указанный URL-адрес и не ожидает ответа.</span><span class="sxs-lookup"><span data-stu-id="0d969-125">[Send one way request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>
  * <span data-ttu-id="0d969-126">[Отправка запроса](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) — отправляет запрос на указанный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="0d969-126">[Send request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) - Sends a request to the specified URL.</span></span>
  * <span data-ttu-id="0d969-127">[Установка метода запроса](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) — позволяет изменить метод HTTP для запроса.</span><span class="sxs-lookup"><span data-stu-id="0d969-127">[Set request method](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>
  * <span data-ttu-id="0d969-128">[Установка кода состояния](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) — меняет код состояния HTTP на указанное значение.</span><span class="sxs-lookup"><span data-stu-id="0d969-128">[Set status](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) - Changes the HTTP status code to the specified value.</span></span>
  * <span data-ttu-id="0d969-129">[Задание переменной][Set variable] — сохраняет значение в именованной переменной [контекста][context] для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="0d969-129">[Set variable][Set variable] - Persist a value in a named [context][context] variable for later access.</span></span>
  * <span data-ttu-id="0d969-130">[Трассировка](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) — добавляет строку в выходные данные [инспектора API](api-management-howto-api-inspector.md).</span><span class="sxs-lookup"><span data-stu-id="0d969-130">[Trace](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) - Adds a string into the [API Inspector](api-management-howto-api-inspector.md) output.</span></span>
  * <span data-ttu-id="0d969-131">[Ожидание](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) — ожидает вложенный запрос отправки, получения значения из кэша или завершения политик управления потоком перед продолжением.</span><span class="sxs-lookup"><span data-stu-id="0d969-131">[Wait](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) - Waits for enclosed Send request, Get value from cache, or Control flow policies to complete before proceeding.</span></span>
* <span data-ttu-id="0d969-132">[Политики аутентификации][Authentication policies]</span><span class="sxs-lookup"><span data-stu-id="0d969-132">[Authentication policies][Authentication policies]</span></span>
  * <span data-ttu-id="0d969-133">[Обычная проверка подлинности][Authenticate with Basic] – обычная проверка подлинности внутренней службы.</span><span class="sxs-lookup"><span data-stu-id="0d969-133">[Authenticate with Basic][Authenticate with Basic] - Authenticate with a backend service using Basic authentication.</span></span>
  * <span data-ttu-id="0d969-134">[Аутентификация с помощью сертификата клиента][Authenticate with client certificate] – аутентификация внутренней службы с помощью сертификатов клиентов.</span><span class="sxs-lookup"><span data-stu-id="0d969-134">[Authenticate with client certificate][Authenticate with client certificate] - Authenticate with a backend service using client certificates.</span></span>
* <span data-ttu-id="0d969-135">[Политики кэширования][Caching policies]</span><span class="sxs-lookup"><span data-stu-id="0d969-135">[Caching policies][Caching policies]</span></span> 
  * <span data-ttu-id="0d969-136">[Получение из кэша][Get from cache] — выполнение поиска в кэше и возврат допустимого кэшированного ответа при его наличии.</span><span class="sxs-lookup"><span data-stu-id="0d969-136">[Get from cache][Get from cache] - Perform cache look up and return a valid cached response when available.</span></span>
  * <span data-ttu-id="0d969-137">[Сохранение в кэше][Store to cache] — помещение в кэш ответа в соответствии с заданной конфигурацией управления кэшем.</span><span class="sxs-lookup"><span data-stu-id="0d969-137">[Store to cache][Store to cache] - Caches response according to the specified cache control configuration.</span></span>
  * <span data-ttu-id="0d969-138">[Получение значения из кэша](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) — получение кэшированного элемента по ключу.</span><span class="sxs-lookup"><span data-stu-id="0d969-138">[Get value from cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>
  * <span data-ttu-id="0d969-139">[Сохранение значения в кэше](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) — сохранение элемента в кэше по ключу.</span><span class="sxs-lookup"><span data-stu-id="0d969-139">[Store value in cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) - Store an item in the cache by key.</span></span>
  * <span data-ttu-id="0d969-140">[Удалить значение из кэша](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) — удаление элемента в кэше по ключу.</span><span class="sxs-lookup"><span data-stu-id="0d969-140">[Remove value from cache](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>
* <span data-ttu-id="0d969-141">[Междоменные политики][Cross domain policies]</span><span class="sxs-lookup"><span data-stu-id="0d969-141">[Cross domain policies][Cross domain policies]</span></span> 
  * <span data-ttu-id="0d969-142">[Разрешение междоменных вызовов][Allow cross-domain calls] — делает API доступным из браузерных клиентов Adobe Flash и Microsoft Silverlight.</span><span class="sxs-lookup"><span data-stu-id="0d969-142">[Allow cross-domain calls][Allow cross-domain calls] - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>
  * <span data-ttu-id="0d969-143">[CORS][CORS] — добавляет поддержку общего доступа к ресурсам независимо от источника (CORS) для операции или API, чтобы разрешить междоменные вызовы из браузерных клиентов.</span><span class="sxs-lookup"><span data-stu-id="0d969-143">[CORS][CORS] - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>
  * <span data-ttu-id="0d969-144">[JSONP][JSONP] — добавляет поддержку JSON с заполнением (JSONP) для операции или API, чтобы разрешить междоменные вызовы из браузерных клиентов JavaScript.</span><span class="sxs-lookup"><span data-stu-id="0d969-144">[JSONP][JSONP] - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>
* <span data-ttu-id="0d969-145">[Политики преобразования][Transformation policies]</span><span class="sxs-lookup"><span data-stu-id="0d969-145">[Transformation policies][Transformation policies]</span></span> 
  * <span data-ttu-id="0d969-146">[Преобразование JSON в XML][Convert JSON to XML] — преобразует текст запроса или ответа в формате JSON в формат XML.</span><span class="sxs-lookup"><span data-stu-id="0d969-146">[Convert JSON to XML][Convert JSON to XML] - Converts request or response body from JSON to XML.</span></span>
  * <span data-ttu-id="0d969-147">[Преобразование XML в JSON][Convert XML to JSON] — преобразует текст запроса или ответа в формате XML в формат JSON.</span><span class="sxs-lookup"><span data-stu-id="0d969-147">[Convert XML to JSON][Convert XML to JSON] - Converts request or response body from XML to JSON.</span></span>
  * <span data-ttu-id="0d969-148">[Поиск и замена строки в тексте][Find and replace string in body] — позволяет найти подстроку запроса или ответа и заменить ее на другую подстроку.</span><span class="sxs-lookup"><span data-stu-id="0d969-148">[Find and replace string in body][Find and replace string in body] - Finds a request or response substring and replaces it with a different substring.</span></span>
  * <span data-ttu-id="0d969-149">[Маскирование URL-адресов в содержимом][Mask URLs in content] — перезаписывает (маскирует) ссылки в тексте ответа так, чтобы каждая из них указывала на эквивалентную ссылку через шлюз.</span><span class="sxs-lookup"><span data-stu-id="0d969-149">[Mask URLs in content][Mask URLs in content] - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>
  * <span data-ttu-id="0d969-150">[Задание внутренней службы][Set backend service] — изменяет внутреннюю службу для входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="0d969-150">[Set backend service][Set backend service] - Changes the backend service for an incoming request.</span></span>
  * <span data-ttu-id="0d969-151">[Задание текста][Set body] — задает текст сообщения для входящих и исходящих запросов.</span><span class="sxs-lookup"><span data-stu-id="0d969-151">[Set body][Set body] - Sets the message body for incoming and outgoing requests.</span></span>
  * <span data-ttu-id="0d969-152">[Задание заголовка HTTP][Set HTTP header] — присваивает значение существующему заголовку ответа и (или) запроса либо добавляет новый заголовок ответа и (или) запроса.</span><span class="sxs-lookup"><span data-stu-id="0d969-152">[Set HTTP header][Set HTTP header] - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>
  * <span data-ttu-id="0d969-153">[Настройка параметра строки запроса][Set query string parameter] — добавляет, заменяет значение или удаляет параметр строки запроса.</span><span class="sxs-lookup"><span data-stu-id="0d969-153">[Set query string parameter][Set query string parameter] - Adds, replaces value of, or deletes request query string parameter.</span></span>
  * <span data-ttu-id="0d969-154">[Перезапись URL-адреса][Rewrite URL] — преобразовывает URL-адрес запроса из его общедоступной формы в форму, ожидаемую веб-службой.</span><span class="sxs-lookup"><span data-stu-id="0d969-154">[Rewrite URL][Rewrite URL] - Converts a request URL from its public form to the form expected by the web service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d969-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0d969-155">Next steps</span></span>
<span data-ttu-id="0d969-156">Дополнительную информацию о выражениях политики см. в следующем видео.</span><span class="sxs-lookup"><span data-stu-id="0d969-156">For more information on policy expressions, see the following video.</span></span>

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
[Log to Event Hub]: https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub

[Authentication policies]: https://msdn.microsoft.com/library/azure/dn894079.aspx
[Authenticate with Basic]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#Basic
[Authenticate with client certificate]: https://msdn.microsoft.com/library/azure/061702a7-3a78-472b-a54a-f3b1e332490d#ClientCertificate
[Caching policies]: https://msdn.microsoft.com/library/azure/dn894086.aspx
[Get from cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#GetFromCache
[Store to cache]: https://msdn.microsoft.com/library/azure/8147199c-24d8-439f-b2a9-da28a70a890c#StoreToCache

[Cross domain policies]: https://msdn.microsoft.com/library/azure/dn894084.aspx
[Allow cross-domain calls]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#AllowCrossDomainCalls
[CORS]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#CORS
[JSONP]: https://msdn.microsoft.com/library/azure/7689d277-8abe-472a-a78c-e6d4bd43455d#JSONP

[Transformation policies]: https://msdn.microsoft.com/library/azure/dn894083.aspx
[Convert JSON to XML]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertJSONtoXML
[Convert XML to JSON]: https://msdn.microsoft.com/library/azure/7406a8ce-5f9c-4fae-9b0f-e574befb2ee9#ConvertXMLtoJSON
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


