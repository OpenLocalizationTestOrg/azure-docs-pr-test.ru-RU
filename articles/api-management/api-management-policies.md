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
# <a name="api-management-policies"></a>Политики управления API
Этот раздел предоставляет справку для следующих политиках управления интерфейсами API hello. Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в управлении API](api-management-howto-policies.md).  
  
 Политики — это мощная возможность системы hello, разрешить издателю hello поведение hello toochange hello API через конфигурацию. Политики представляют собой набор инструкций, которые выполняются последовательно, по запросу hello или ответу API-интерфейса. Среди наиболее популярных инструкций вспомнить преобразование формата XML tooJSON и toorestrict hello объема входящих вызовов от разработчика ограничение частоты вызовов. Стандартной hello доступны многие дополнительные политики.  
  
 Выражения политики может использоваться как значения атрибутов или текстовыми значениями в любой hello политиках управления интерфейсами API, если политика hello не указывает иное. Некоторые политики, такие как hello [поток управления](api-management-advanced-policies.md#choose) и [переменным](api-management-advanced-policies.md#set-variable) политики основаны на выражениях политики. Дополнительную информацию см. в документации по [расширенным политикам](api-management-advanced-policies.md#AdvancedPolicies) и [выражениям политики](api-management-policy-expressions.md).  
  
##  <a name="ProxyPolicies"></a> Политики  
  
-   [Политики ограничения доступа](api-management-access-restriction-policies.md#AccessRestrictionPolicies)  
  
    -   [Проверка заголовка HTTP](api-management-access-restriction-policies.md#CheckHTTPHeader) – обеспечивает принудительный ввод заголовка HTTP и/или его значения.  
  
    -   [Ограничение частоты вызовов по подписке](api-management-access-restriction-policies.md#LimitCallRate) — предотвращает пики использования API, ограничивая частоту вызовов для каждой подписки.  
  
    -   [Ограничение частоты вызовов по ключу](api-management-access-restriction-policies.md#LimitCallRateByKey) — предотвращает пики использования API, ограничивая частоту вызовов по ключу.  
  
    -   [Ограничение IP-адресов вызывающих объектов](api-management-access-restriction-policies.md#RestrictCallerIPs) – фильтрует (разрешает или запрещает) вызовы с конкретных IP-адресов и/или диапазонов адресов.  
  
    -   [Задание квоты использования по подписке](api-management-access-restriction-policies.md#SetUsageQuota) -позволяет tooenforce задание продлеваемой или бессрочной квоты объема вызовов или полосы пропускания, для каждой подписки.  
  
    -   [Задание квоты использования ключом](api-management-access-restriction-policies.md#SetUsageQuotaByKey) -позволяет tooenforce задание продлеваемой или бессрочной квоты объема вызовов или полосы пропускания, на основе каждого ключа.  
  
    -   [Проверка JWT](api-management-access-restriction-policies.md#ValidateJWT) – обеспечивает принудительное задание и проверку JWT, извлеченного из заданного заголовка HTTP или параметра запроса.  
  
-   [Расширенные политики](api-management-advanced-policies.md#AdvancedPolicies)  
  
    -   [Поток управления](api-management-advanced-policies.md#choose) — условно применяет операторы политики на основании оценки hello логических выражений.  
  
    -   [Прямой запрос](api-management-advanced-policies.md#ForwardRequest) -пересылает hello запроса toohello внутренней службы.  
  
    -   [Журнал tooEvent концентратора](api-management-advanced-policies.md#log-to-eventhub) -отправляет сообщения hello указанный формат tooa сообщение целевому определяются сущности средства ведения журнала.  
  
    -   [Повторите](api-management-advanced-policies.md#Retry) -повторных попыток выполнения hello заключены операторы политики, если и пока не будет выполнено условие hello. Выполнение будет сквозные hello определенные промежутки времени и копирование toohello указанное число повторных попыток.  
  
    -   [Вернуть ответ](api-management-advanced-policies.md#ReturnResponse) -конвейера прерывания выполнения и возвращает hello указанного ответа непосредственно toohello вызывающего объекта.  
  
    -   [Отправка запроса на один из способов](api-management-advanced-policies.md#SendOneWayRequest) -отправляет toohello запроса указан URL-адрес без ожидания ответа.  
  
    -   [Отправка запроса](api-management-advanced-policies.md#SendRequest) -отправляет toohello запроса указан URL-адрес.  
  
    -   [Задание переменной](api-management-advanced-policies.md#set-variable) — сохраняет значение в именованной переменной контекста для последующего использования.  
  
    -   [Установка метода запроса](api-management-advanced-policies.md#SetRequestMethod) -позволяет toochange метод hello HTTP для запроса.  
  
    -   [Задать код состояния](api-management-advanced-policies.md#SetStatus) -toohello код состояния hello HTTP изменения заданного значения.  
  
    -   [Трассировки](api-management-advanced-policies.md#Trace) -добавляет строку в hello [инспектора API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) выходных данных.  
  
    -   [Подождите](api-management-advanced-policies.md#Wait) -ожидает заключены [запрос на отправку](api-management-advanced-policies.md#SendRequest), [получить значение из кэша](api-management-caching-policies.md#GetFromCacheByKey), или [поток управления](api-management-advanced-policies.md#choose) toocomplete политики, прежде чем продолжить.  
  
-   [Политики аутентификации](api-management-authentication-policies.md#AuthenticationPolicies)  
  
    -   [Обычная проверка подлинности](api-management-authentication-policies.md#Basic) – обычная проверка подлинности внутренней службы.  
  
    -   [Аутентификация с помощью сертификата клиента](api-management-authentication-policies.md#ClientCertificate) – аутентификация внутренней службы с помощью сертификатов клиентов.  
  
-   [Политики кэширования](api-management-caching-policies.md#CachingPolicies)  
  
    -   [Получение из кэша](api-management-caching-policies.md#GetFromCache) – выполнение операции поиска в кэше и возврат допустимого кэшированного ответа при его наличии.  
  
    -   [Хранить toocache](api-management-caching-policies.md#StoreToCache) -кэши ответа в соответствии с toohello указана конфигурация управления кэша.  
  
    -   [Получение значения из кэша](api-management-caching-policies.md#GetFromCacheByKey) — получение кэшированного элемента по ключу.  
  
    -   [Сохраните значение в кэше](api-management-caching-policies.md#StoreToCacheByKey) -хранения элемента в кэше hello по ключу.  
  
    -   [Удалить значение из кэша](api-management-caching-policies.md#RemoveCacheByKey) -удалить элемент из кэша hello по ключу.  
  
-   [Кроссдоменные политики](api-management-cross-domain-policies.md#CrossDomainPolicies)  
  
    -   [Разрешить междоменные вызовы](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -становится доступным hello API из клиентов Adobe Flash и Microsoft Silverlight на основе браузера.  
  
    -   [CORS](api-management-cross-domain-policies.md#CORS) -добавляет ресурсов независимо от источника (CORS) для управления доступом поддерживает операцию tooan или API tooallow междоменные вызовы из браузерных клиентов.  
  
    -   [JSONP](api-management-cross-domain-policies.md#JSONP) - добавляет JSON с заполнением (JSONP) поддержка tooan операции или API tooallow междоменные вызовы из браузерных клиентов JavaScript.  
  
-   [Политики преобразования](api-management-transformation-policies.md#TransformationPolicies)  
  
    -   [Преобразование JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - преобразует запрос или текст ответа от JSON tooXML.  
  
    -   [Преобразование XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - преобразует запрос, или из XML tooJSON текст ответа.  
  
    -   [Поиск и замена строки в тексте](api-management-transformation-policies.md#Findandreplacestringinbody) – отыскивает подстроку запроса или ответа и заменяет ее на другую подстроку.  
  
    -   [Маскировать URL-адреса в содержимом](api-management-transformation-policies.md#MaskURLSContent) -загрузочную запись (маскировка) ссылок в ответ hello текста, чтобы они указывали toohello равнозначными ссылками через шлюз hello.  
  
    -   [Задать серверной службе](api-management-transformation-policies.md#SetBackendService) -изменяет hello серверную службу для входящего запроса.  
  
    -   [Задайте текст](api-management-transformation-policies.md#SetBody) -задает текст сообщения hello для входящих и исходящих запросов.  
  
    -   [Задание заголовка HTTP](api-management-transformation-policies.md#SetHTTPheader) - назначает значение tooan существующего ответа и/или заголовка запроса или Добавление нового заголовка ответа и/или запроса.  
  
    -   [Настройка параметра строки запроса](api-management-transformation-policies.md#SetQueryStringParameter) - добавляет, заменяет значение или удаляет параметр строки запроса.  
  
    -   [Замена URL-адреса](api-management-transformation-policies.md#RewriteURL) -преобразование URL-АДРЕСЕ запроса из общеупотребительной формы формы toohello ожидаемый hello веб-службы.  
  
    -   [Преобразования XML с помощью XSLT](api-management-transformation-policies.md#XSLTransform) -применяется tooXML преобразование XSL в тексте запроса или ответа hello.  
  
## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о работе с политиками см. в статье со справочными материалами по [политикам в службе управления API](api-management-howto-policies.md).  
