---
title: "aaaCustom кэширования в Azure API Management"
description: "Узнайте, как элементы toocache ключом в службе управления API Azure"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 772bc8dd-5cda-41c4-95bf-b9f6f052bc85
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 681380743c8c96af5d0a8e25948a8c0663e9fd35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="custom-caching-in-azure-api-management"></a>Пользовательское кэширование в службе управления API Azure
Служба управления API Azure имеет встроенную поддержку [кэширование ответов HTTP](api-management-howto-cache.md) с помощью URL-адрес ресурса hello в качестве ключа hello. Hello ключа могут быть изменены с помощью hello заголовки запроса `vary-by` свойства. Это полезно для кэширования всей откликов HTTP (также называемого представления), но иногда бывает полезным toojust кэша часть представление. новый Hello [значение для подстановки кэша](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) и [значение для хранилища кэша](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) политики предоставляют возможность hello toostore и извлекать произвольные фрагменты данных из группы определения политик. Эта возможность также добавляет значение toohello ранее представленные [запрос на отправку](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) политики, так как теперь можно кэшировать ответы от внешних служб.

## <a name="architecture"></a>Архитектура
Служба управления API использует кэш данных общего клиента, чтобы, как вертикальное масштабирование единиц toomultiple будет по-прежнему получить доступ toohello же кэшированных данных. Однако при работе с развертывание в нескольких регионах существуют кэши независимо в каждой из областей hello. Из-за toothis, очень важно toonot считать hello кэша хранилища данных, где единственным источником hello некоторые фрагмента данных. При не была, а позднее решили tootake преимуществами развертывание в нескольких регионах hello, клиенты с пользователями, которые перемещаются может потерять доступ к данным в кэше toothat.

## <a name="fragment-caching"></a>Кэширование фрагментов
Существует несколько случаев, в которых возвращается ответы содержат некоторую часть данных и еще остается в течение приемлемого времени свежей дорогих toodetermine. Например, рассмотрим созданную авиакомпанией службу, которая предоставляет сведения о бронировании авиабилетов, статусе рейсов и другую информацию. Если hello пользователь является членом hello авиакомпании точек программы, они бы также сведения, касающиеся tootheir текущего состояния и накапливаются расстояния. Эти сведения, связанные с пользователем может храниться в другую систему, но может быть нежелательно tooinclude в ответах возвращается состояние рейсов и резервирования. Это можно сделать с помощью кэширования фрагментов. Hello основного представления могут быть возвращены из hello исходного сервера с помощью какого-либо вида маркера tooindicate, где toobe вставить информацию о пользователе hello. 

Рассмотрим следующий ответ JSON с API внутреннего сервера hello.

```json
{
  "airline" : "Air Canada",
  "flightno" : "871",
  "status" : "ontime",
  "gate" : "B40",
  "terminal" : "2A",
  "userprofile" : "$userprofile$"
}  
```

Также рассмотрим дополнительный ресурс по адресу `/userprofile/{userid}` :

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

В порядке toodetermine hello соответствующего пользователя сведения tooinclude нам нужна tooidentify кто hello конечным пользователем. Этот механизм зависит от реализации. Например, я использую hello `Subject` утверждение с правом `JWT` токена. 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

Мы сохраняем это значение `enduserid` в переменной контекста для дальнейшего использования. Hello следующим шагом является toodetermine, если предыдущий запрос уже получены сведения о пользователе hello и сохранить ее в кэше hello. Для этого мы используем hello `cache-lookup-value` политики.

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

Если отсутствует запись в кэше hello, соответствующий toohello значение ключа, то нет `userprofile` будет создана переменная контекста. Мы проверяем, успех hello hello уточняющего запроса с помощью hello `choose` политика потока управления.

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If hello userprofile context variable doesn’t exist, make an HTTP request tooretrieve it.  -->
    </when>
</choose>
```

Если hello `userprofile` переменной контекста не существует, то мы не toomake HTTP запроса будет toohave tooretrieve его.

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points toohello profile for hello current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

Мы используем hello `enduserid` ресурс профиля пользователя toohello URL-адрес tooconstruct hello. После получения ответа hello, мы основной текст hello из hello ответа по запросу и сохранить его в переменной контекста.

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

tooavoid предоставлять toomake это HTTP-запрос еще раз, когда hello того же пользователя выполняет другой запрос, сохранить профиль пользователя hello в кэше hello.

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

Значение hello хранятся в кэше hello, с помощью того же ключа с точное hello мы изначально попыток tooretrieve с. Hello длительность, мы выбираем toostore hello значение должно быть основано на частоту hello изменения сведений о и устойчивость пользователи являются tooout дат. 

Это важные toorealize, что извлечение из кэша hello по-прежнему out of process, сетевой запрос, который потенциально по-прежнему можно добавить десятков миллисекунд toohello запроса. преимущества Hello поступать при определении данных профиля пользователя hello занимает намного больше, выполнения запросов к базе данных toodo tooneeding или статистические данные из нескольких интерфейсов назад.

Hello заключительный этап hello — tooupdate hello, возвращается ответ с нашей данных профиля пользователя.

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

Я выбрал tooinclude hello кавычки как часть токена hello, чтобы даже в том случае, если не происходит замена hello, hello ответ был по-прежнему допустимых данных JSON. Это было в основном toomake отладки.

После объединить эти шаги hello конечным результатом является политику, которая выглядит одном hello.

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in hello cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in hello cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request tooget user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points toohello profile for hello current end-user -->
                    <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),(string)context.Variables["enduserid"]).AbsoluteUri)</set-url>
                    <set-method>GET</set-method>
                </send-request>

                <!-- Store response body in context variable -->
                <set-variable
                  name="userprofile"
                  value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />

                <!-- Store result in cache -->
                <cache-store-value
                  key="@("userprofile-" + context.Variables["enduserid"])"
                  value="@((string)context.Variables["userprofile"])"
                  duration="100000" />
            </when>
        </choose>
        <base />
    </inbound>
    <outbound>
        <!-- Update response body with user profile-->
        <find-and-replace
              from='"$userprofile$"'
              to="@((string)context.Variables["userprofile"])" />
        <base />
    </outbound>
</policies>
```

Этот подход кэширования в основном используется в веб-сайтов которой HTML состоит на стороне сервера hello, чтобы он может быть отображен в виде одной страницы. Тем не менее, его также можно использовать в API-интерфейсы, где клиенты не могут выполнять клиента стороне кэширования HTTP или желательно не tooput эту ответственность на приветствия клиента.

Такого же вида фрагментарное кэширование может также выполняться на hello серверной части веб-серверов с помощью Redis, кэширование сервера, однако с помощью tooperform службы управления API hello эту работу полезно hello кэширования фрагментов соединяющиеся из разных назад элементов, чем hello Основные ответы.

## <a name="transparent-versioning"></a>Прозрачное управление версиями
Это принято для нескольких версий другую реализацию toobe API, поддерживаемые в любой момент времени. Это, возможно, toosupport различных средах, таких как разработки, тестирования, производства, и т.д., или может оказаться более старых версий toosupport время toogive hello API для API потребители toomigrate toonewer версий. 

Один из подходов toohandling этом вместо от необходимости разработчики URL-адреса toochange hello из клиента `/v1/customers` слишком`/v2/customers` — toostore в hello потребителя данных профиля, какую версию hello API они в настоящее время обратиться toouse и вызовите соответствующий hello Внутренний URL-адрес. Порядок toodetermine hello правильный внутренний URL-адрес toocall для конкретного клиента, при необходимости tooquery некоторые данные конфигурации. Кэширование эти данные конфигурации, мы минимизировать потери производительности hello, выполнив этот поиск.

Первым шагом Hello — идентификатор hello toodetermine используемых tooconfigure hello нужную версию. В этом примере я выбрал подписки ключ продукта toohello tooassociate hello версии. 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

Если мы уже извлекли hello желаемую версии мы затем выполните toosee уточняющего запроса кэша.

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

Затем мы проверяем toosee, если его не удалось найти в кэше hello.

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

Если не удалось, ее нужно извлечь.

```xml
<send-request
    mode="new"
    response-variable-name="clientconfiguresponse"
    timeout="10"
    ignore-error="true">
            <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
            <set-method>GET</set-method>
</send-request>
```

Основной текст ответа hello Извлеките из ответа hello.

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

Храните его обратно в кэш hello для использования в будущем.

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

И наконец обновление hello серверной части URL-адрес tooselect hello версия службы hello клиентом hello.

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

Hello полностью политики выглядит следующим образом.

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in hello cache, make a request for it and store it -->
    <choose>
        <when condition="@(!context.Variables.ContainsKey("clientversion"))">
            <send-request mode="new" response-variable-name="clientconfiguresponse" timeout="10" ignore-error="true">
                <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
                <set-method>GET</set-method>
            </send-request>
            <!-- Store response body in context variable -->
            <set-variable name="clientversion" value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
            <!-- Store result in cache -->
            <cache-store-value key="@("clientversion-" + context.Variables["clientid"])" value="@((string)context.Variables["clientversion"])" duration="100000" />
        </when>
    </choose>
    <set-backend-service base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
</inbound>
```

Включение системы управления API потребители tootransparently серверной версии осуществляется клиентами без необходимости tooupdate и повторное развертывание клиентов — элегантное решение, которое решает многие проблемы управления версиями API.

## <a name="tenant-isolation"></a>Изоляция клиентов
Некоторые компании с крупными развертываниями, состоящими из нескольких клиентов, создают отдельные группы клиентов на отдельных развернутых серверах. Это сводит к минимуму hello количество клиентов, которые будут затронуты проблемой с оборудованием на серверной hello. Он также обеспечивает новые toobe версии программного обеспечения, распространен на этапах. Эта архитектура серверной желательно прозрачный tooAPI потребителей. Это можно сделать в аналогичные версий tootransparent способом, так как она основана на hello же метод управления hello URL-адрес внутреннего использования состояния конфигурации на ключ API.  

Вместо возвращения предпочтительную версию hello API для каждого ключа подписки, возвратят идентификатор, который связывает группу клиента toohello назначенный оборудования. Этот идентификатор может быть URL-адрес соответствующего внутреннего используется tooconstruct hello.

## <a name="summary"></a>Сводка
Hello свободу toouse hello кэш управления Azure API для хранения любого типа данных включает данные tooconfiguration эффективного доступа, которые могут повлиять на способ hello обработки входящего запроса. Он также может быть используется toostore фрагменты данных, которые можно дополнить ответы, возвращаемые API внутреннего сервера.

## <a name="next-steps"></a>Дальнейшие действия
Проверьте свой отзыв в hello Disqus потока для данного раздела при наличии других сценариев, эти политики включен автоматически, или скриптов, требующий tooachieve, но не уверены, что в данный момент возможны.

