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
# <a name="azure-api-management-policy-reference"></a>Справочник по политикам службы управления Azure API 
Этот раздел содержит индекс для политик hello в hello [Справочник по политикам управления API][API Management policy reference]. Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в службе управления API][Policies in API Management].

Выражения политики может использоваться как значения атрибутов или текстовыми значениями в любой hello политиках управления интерфейсами API, если политика hello не указывает иное. Некоторые политики, такие как hello [поток управления] [ Control flow] и [переменным] [ Set variable] политики основаны на выражениях политики. Чтобы узнать больше, ознакомьтесь с [расширенными политиками][Advanced policies] и [выражениями политики][Policy expressions].

## <a name="policy-reference-index"></a>Справочные указатели по политикам
* [Политики ограничения доступа][Access restriction policies]
  * [Проверка заголовка HTTP][Check HTTP header] — обеспечивает принудительный ввод заголовка HTTP и (или) его значения.
  * [Ограничение частоты вызовов по подписке][Limit call rate by subscription] — предотвращает пики использования API, ограничивая частоту вызовов для каждой подписки.
  * [Ограничение частоты вызовов по ключу](https://msdn.microsoft.com/library/azure/dn894078.aspx#LimitCallRateByKey) — предотвращает пики использования API, ограничивая частоту вызовов по ключу.
  * [Ограничение IP-адресов вызывающих объектов][Restrict caller IPs] — фильтрует (разрешает или запрещает) вызовы с конкретных IP-адресов и (или) диапазонов адресов.
  * [Задание квоты использования по подписке] [ Set usage quota by subscription] -позволяет tooenforce задание продлеваемой или бессрочной квоты объема вызовов или полосы пропускания, для каждой подписки.
  * [Задание квоты использования ключом](https://msdn.microsoft.com/library/azure/dn894078.aspx#SetUsageQuotaByKey) -позволяет tooenforce задание продлеваемой или бессрочной квоты объема вызовов или полосы пропускания, на основе каждого ключа.
  * [Проверка JWT][Validate JWT] — обеспечивает принудительное задание и проверку маркера JWT, извлеченного из заданного заголовка HTTP или параметра запроса.
* [Расширенные политики][Advanced policies]
  * [Поток управления] [ Control flow] — условно применяет операторы политики на основе результатов вычисления логических hello hello [выражений][expressions].
  * [Прямой запрос] [ Forward request] -пересылает hello запроса toohello внутренней службы.
  * [Журнал tooEvent концентратора] [ Log tooEvent Hub] -отправляет сообщения hello указанный формат tooa сообщение целевому определяется [средства ведения журнала](https://msdn.microsoft.com/library/azure/mt592020.aspx#Logger) сущности.
  * [Повторите](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Retry) -повторных попыток выполнения hello заключены операторы политики, если и пока не будет выполнено условие hello. Выполнение будет сквозные hello определенные промежутки времени и копирование toohello указанное число повторных попыток.
  * [Вернуть ответ](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) -конвейера прерывания выполнения и возвращает hello указанного ответа непосредственно toohello вызывающего объекта.
  * [Отправка запроса на один из способов](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) -отправляет toohello запроса указан URL-адрес без ожидания ответа.
  * [Отправка запроса](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) -отправляет toohello запроса указан URL-адрес.
  * [Установка метода запроса](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetRequestMethod) -позволяет toochange метод hello HTTP для запроса.
  * [Задать состояние](https://msdn.microsoft.com/library/azure/dn894085.aspx#SetStatus) -toohello код состояния hello HTTP изменения заданного значения.
  * [Задание переменной][Set variable] — сохраняет значение в именованной переменной [контекста][context] для последующего использования.
  * [Трассировки](https://msdn.microsoft.com/en-us/library/dn894085.aspx#Trace) -добавляет строку в hello [инспектора API](api-management-howto-api-inspector.md) выходных данных.
  * [Подождите](https://msdn.microsoft.com/library/azure/dn894085.aspx#Wait) — ожидает отправки вложенный запрос, получение значения из кэша или управлять toocomplete политики потока, прежде чем продолжить.
* [Политики аутентификации][Authentication policies]
  * [Обычная проверка подлинности][Authenticate with Basic] – обычная проверка подлинности внутренней службы.
  * [Аутентификация с помощью сертификата клиента][Authenticate with client certificate] – аутентификация внутренней службы с помощью сертификатов клиентов.
* [Политики кэширования][Caching policies] 
  * [Получение из кэша][Get from cache] — выполнение поиска в кэше и возврат допустимого кэшированного ответа при его наличии.
  * [Хранить toocache] [ Store toocache] -кэши ответа в соответствии с toohello указана конфигурация управления кэша.
  * [Получение значения из кэша](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) — получение кэшированного элемента по ключу.
  * [Сохраните значение в кэше](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) -хранения элемента в кэше hello по ключу.
  * [Удалить значение из кэша](https://msdn.microsoft.com/en-us/library/dn894086.aspx#RemoveCacheByKey) -удалить элемент из кэша hello по ключу.
* [Междоменные политики][Cross domain policies] 
  * [Разрешить междоменные вызовы] [ Allow cross-domain calls] -становится доступным hello API из клиентов Adobe Flash и Microsoft Silverlight на основе браузера.
  * [CORS] [ CORS] -добавляет ресурсов независимо от источника (CORS) для управления доступом поддерживает операцию tooan или API tooallow междоменные вызовы из браузерных клиентов.
  * [JSONP] [ JSONP] - добавляет JSON с заполнением (JSONP) поддержка tooan операции или API tooallow междоменные вызовы из браузерных клиентов JavaScript.
* [Политики преобразования][Transformation policies] 
  * [Преобразование JSON tooXML] [ Convert JSON tooXML] - преобразует запрос или текст ответа от JSON tooXML.
  * [Преобразование XML tooJSON] [ Convert XML tooJSON] - преобразует запрос, или из XML tooJSON текст ответа.
  * [Поиск и замена строки в тексте][Find and replace string in body] — позволяет найти подстроку запроса или ответа и заменить ее на другую подстроку.
  * [Маскировать URL-адреса в содержимом] [ Mask URLs in content] -загрузочную запись (маскировка) ссылок в ответ hello текста, чтобы они указывали toohello равнозначными ссылками через шлюз hello.
  * [Задать серверная служба] [ Set backend service] -изменяет hello серверную службу для входящего запроса.
  * [Задайте текст] [ Set body] -задает текст сообщения hello для входящих и исходящих запросов.
  * [Задание заголовка HTTP] [ Set HTTP header] - назначает значение tooan существующего ответа и/или заголовка запроса или Добавление нового заголовка ответа и/или запроса.
  * [Настройка параметра строки запроса][Set query string parameter] — добавляет, заменяет значение или удаляет параметр строки запроса.
  * [Замена URL-адреса] [ Rewrite URL] -преобразование URL-АДРЕСЕ запроса из общеупотребительной формы формы toohello ожидаемый hello веб-службы.

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о выражениях политики см. следующие видео hello.

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


