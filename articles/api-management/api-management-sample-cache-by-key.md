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
# <a name="custom-caching-in-azure-api-management"></a><span data-ttu-id="59be1-103">Пользовательское кэширование в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="59be1-103">Custom caching in Azure API Management</span></span>
<span data-ttu-id="59be1-104">Служба управления API Azure имеет встроенную поддержку [кэширование ответов HTTP](api-management-howto-cache.md) с помощью URL-адрес ресурса hello в качестве ключа hello.</span><span class="sxs-lookup"><span data-stu-id="59be1-104">Azure API Management service has built-in support for [HTTP response caching](api-management-howto-cache.md) using hello resource URL as hello key.</span></span> <span data-ttu-id="59be1-105">Hello ключа могут быть изменены с помощью hello заголовки запроса `vary-by` свойства.</span><span class="sxs-lookup"><span data-stu-id="59be1-105">hello key can be modified by request headers using hello `vary-by` properties.</span></span> <span data-ttu-id="59be1-106">Это полезно для кэширования всей откликов HTTP (также называемого представления), но иногда бывает полезным toojust кэша часть представление.</span><span class="sxs-lookup"><span data-stu-id="59be1-106">This is useful for caching entire HTTP responses (aka representations), but sometimes it is useful toojust cache a portion of a representation.</span></span> <span data-ttu-id="59be1-107">новый Hello [значение для подстановки кэша](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) и [значение для хранилища кэша](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) политики предоставляют возможность hello toostore и извлекать произвольные фрагменты данных из группы определения политик.</span><span class="sxs-lookup"><span data-stu-id="59be1-107">hello new [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) and [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) policies provide hello ability toostore and retrieve arbitrary pieces of data from within policy definitions.</span></span> <span data-ttu-id="59be1-108">Эта возможность также добавляет значение toohello ранее представленные [запрос на отправку](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) политики, так как теперь можно кэшировать ответы от внешних служб.</span><span class="sxs-lookup"><span data-stu-id="59be1-108">This ability also adds value toohello previously introduced [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy because you can now cache responses from external services.</span></span>

## <a name="architecture"></a><span data-ttu-id="59be1-109">Архитектура</span><span class="sxs-lookup"><span data-stu-id="59be1-109">Architecture</span></span>
<span data-ttu-id="59be1-110">Служба управления API использует кэш данных общего клиента, чтобы, как вертикальное масштабирование единиц toomultiple будет по-прежнему получить доступ toohello же кэшированных данных.</span><span class="sxs-lookup"><span data-stu-id="59be1-110">API Management service uses a shared per-tenant data cache so that, as you scale up toomultiple units you will still get access toohello same cached data.</span></span> <span data-ttu-id="59be1-111">Однако при работе с развертывание в нескольких регионах существуют кэши независимо в каждой из областей hello.</span><span class="sxs-lookup"><span data-stu-id="59be1-111">However, when working with a multi-region deployment there are independent caches within each of hello regions.</span></span> <span data-ttu-id="59be1-112">Из-за toothis, очень важно toonot считать hello кэша хранилища данных, где единственным источником hello некоторые фрагмента данных.</span><span class="sxs-lookup"><span data-stu-id="59be1-112">Due toothis, it is important toonot treat hello cache as a data store, where it is hello only source of some piece of information.</span></span> <span data-ttu-id="59be1-113">При не была, а позднее решили tootake преимуществами развертывание в нескольких регионах hello, клиенты с пользователями, которые перемещаются может потерять доступ к данным в кэше toothat.</span><span class="sxs-lookup"><span data-stu-id="59be1-113">If you did, and later decided tootake advantage of hello multi-region deployment, then customers with users that travel may lose access toothat cached data.</span></span>

## <a name="fragment-caching"></a><span data-ttu-id="59be1-114">Кэширование фрагментов</span><span class="sxs-lookup"><span data-stu-id="59be1-114">Fragment caching</span></span>
<span data-ttu-id="59be1-115">Существует несколько случаев, в которых возвращается ответы содержат некоторую часть данных и еще остается в течение приемлемого времени свежей дорогих toodetermine.</span><span class="sxs-lookup"><span data-stu-id="59be1-115">There are certain cases where responses being returned contain some portion of data that is expensive toodetermine and yet remains fresh for a reasonable amount of time.</span></span> <span data-ttu-id="59be1-116">Например, рассмотрим созданную авиакомпанией службу, которая предоставляет сведения о бронировании авиабилетов, статусе рейсов и другую информацию. Если hello пользователь является членом hello авиакомпании точек программы, они бы также сведения, касающиеся tootheir текущего состояния и накапливаются расстояния.</span><span class="sxs-lookup"><span data-stu-id="59be1-116">As an example, consider a service built by an airline that provides information relating flight reservations, flight status, etc. If hello user is a member of hello airlines points program, they would also have information relating tootheir current status and mileage accumulated.</span></span> <span data-ttu-id="59be1-117">Эти сведения, связанные с пользователем может храниться в другую систему, но может быть нежелательно tooinclude в ответах возвращается состояние рейсов и резервирования.</span><span class="sxs-lookup"><span data-stu-id="59be1-117">This user-related information might be stored in a different system, but it may be desirable tooinclude it in responses returned about flight status and reservations.</span></span> <span data-ttu-id="59be1-118">Это можно сделать с помощью кэширования фрагментов.</span><span class="sxs-lookup"><span data-stu-id="59be1-118">This can be done using a process called fragment caching.</span></span> <span data-ttu-id="59be1-119">Hello основного представления могут быть возвращены из hello исходного сервера с помощью какого-либо вида маркера tooindicate, где toobe вставить информацию о пользователе hello.</span><span class="sxs-lookup"><span data-stu-id="59be1-119">hello primary representation can be returned from hello origin server using some kind of token tooindicate where hello user-related information is toobe inserted.</span></span> 

<span data-ttu-id="59be1-120">Рассмотрим следующий ответ JSON с API внутреннего сервера hello.</span><span class="sxs-lookup"><span data-stu-id="59be1-120">Consider hello following JSON response from a backend API.</span></span>

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

<span data-ttu-id="59be1-121">Также рассмотрим дополнительный ресурс по адресу `/userprofile/{userid}` :</span><span class="sxs-lookup"><span data-stu-id="59be1-121">And secondary resource at `/userprofile/{userid}` that looks like,</span></span>

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

<span data-ttu-id="59be1-122">В порядке toodetermine hello соответствующего пользователя сведения tooinclude нам нужна tooidentify кто hello конечным пользователем.</span><span class="sxs-lookup"><span data-stu-id="59be1-122">In order toodetermine hello appropriate user information tooinclude, we need tooidentify who hello end user is.</span></span> <span data-ttu-id="59be1-123">Этот механизм зависит от реализации.</span><span class="sxs-lookup"><span data-stu-id="59be1-123">This mechanism is implementation dependent.</span></span> <span data-ttu-id="59be1-124">Например, я использую hello `Subject` утверждение с правом `JWT` токена.</span><span class="sxs-lookup"><span data-stu-id="59be1-124">As an example, I am using hello `Subject` claim of a `JWT` token.</span></span> 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

<span data-ttu-id="59be1-125">Мы сохраняем это значение `enduserid` в переменной контекста для дальнейшего использования.</span><span class="sxs-lookup"><span data-stu-id="59be1-125">We store this `enduserid` value in a context variable for later use.</span></span> <span data-ttu-id="59be1-126">Hello следующим шагом является toodetermine, если предыдущий запрос уже получены сведения о пользователе hello и сохранить ее в кэше hello.</span><span class="sxs-lookup"><span data-stu-id="59be1-126">hello next step is toodetermine if a previous request has already retrieved hello user information and stored it in hello cache.</span></span> <span data-ttu-id="59be1-127">Для этого мы используем hello `cache-lookup-value` политики.</span><span class="sxs-lookup"><span data-stu-id="59be1-127">For this we use hello `cache-lookup-value` policy.</span></span>

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

<span data-ttu-id="59be1-128">Если отсутствует запись в кэше hello, соответствующий toohello значение ключа, то нет `userprofile` будет создана переменная контекста.</span><span class="sxs-lookup"><span data-stu-id="59be1-128">If there is no entry in hello cache that corresponds toohello key value, then no `userprofile` context variable will be created.</span></span> <span data-ttu-id="59be1-129">Мы проверяем, успех hello hello уточняющего запроса с помощью hello `choose` политика потока управления.</span><span class="sxs-lookup"><span data-stu-id="59be1-129">We check hello success of hello lookup using hello `choose` control flow policy.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If hello userprofile context variable doesn’t exist, make an HTTP request tooretrieve it.  -->
    </when>
</choose>
```

<span data-ttu-id="59be1-130">Если hello `userprofile` переменной контекста не существует, то мы не toomake HTTP запроса будет toohave tooretrieve его.</span><span class="sxs-lookup"><span data-stu-id="59be1-130">If hello `userprofile` context variable doesn’t exist, then we are going toohave toomake an HTTP request tooretrieve it.</span></span>

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

<span data-ttu-id="59be1-131">Мы используем hello `enduserid` ресурс профиля пользователя toohello URL-адрес tooconstruct hello.</span><span class="sxs-lookup"><span data-stu-id="59be1-131">We use hello `enduserid` tooconstruct hello URL toohello user profile resource.</span></span> <span data-ttu-id="59be1-132">После получения ответа hello, мы основной текст hello из hello ответа по запросу и сохранить его в переменной контекста.</span><span class="sxs-lookup"><span data-stu-id="59be1-132">Once we have hello response, we can pull hello body text out of hello response and store it back into a context variable.</span></span>

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

<span data-ttu-id="59be1-133">tooavoid предоставлять toomake это HTTP-запрос еще раз, когда hello того же пользователя выполняет другой запрос, сохранить профиль пользователя hello в кэше hello.</span><span class="sxs-lookup"><span data-stu-id="59be1-133">tooavoid us having toomake this HTTP request again, when hello same user makes another request, we can store hello user profile in hello cache.</span></span>

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

<span data-ttu-id="59be1-134">Значение hello хранятся в кэше hello, с помощью того же ключа с точное hello мы изначально попыток tooretrieve с.</span><span class="sxs-lookup"><span data-stu-id="59be1-134">We store hello value in hello cache using hello exact same key that we originally attempted tooretrieve it with.</span></span> <span data-ttu-id="59be1-135">Hello длительность, мы выбираем toostore hello значение должно быть основано на частоту hello изменения сведений о и устойчивость пользователи являются tooout дат.</span><span class="sxs-lookup"><span data-stu-id="59be1-135">hello duration that we choose toostore hello value should be based on how often hello information changes and how tolerant users are tooout of date information.</span></span> 

<span data-ttu-id="59be1-136">Это важные toorealize, что извлечение из кэша hello по-прежнему out of process, сетевой запрос, который потенциально по-прежнему можно добавить десятков миллисекунд toohello запроса.</span><span class="sxs-lookup"><span data-stu-id="59be1-136">It is important toorealize that retrieving from hello cache is still an out-of-process, network request and potentially can still add tens of milliseconds toohello request.</span></span> <span data-ttu-id="59be1-137">преимущества Hello поступать при определении данных профиля пользователя hello занимает намного больше, выполнения запросов к базе данных toodo tooneeding или статистические данные из нескольких интерфейсов назад.</span><span class="sxs-lookup"><span data-stu-id="59be1-137">hello benefits come when determining hello user profile information takes significantly longer than that due tooneeding toodo database queries or aggregate information from multiple back-ends.</span></span>

<span data-ttu-id="59be1-138">Hello заключительный этап hello — tooupdate hello, возвращается ответ с нашей данных профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="59be1-138">hello final step in hello process is tooupdate hello returned response with our user profile information.</span></span>

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

<span data-ttu-id="59be1-139">Я выбрал tooinclude hello кавычки как часть токена hello, чтобы даже в том случае, если не происходит замена hello, hello ответ был по-прежнему допустимых данных JSON.</span><span class="sxs-lookup"><span data-stu-id="59be1-139">I chose tooinclude hello quotation marks as part of hello token so that even when hello replace doesn’t occur, hello response was still valid JSON.</span></span> <span data-ttu-id="59be1-140">Это было в основном toomake отладки.</span><span class="sxs-lookup"><span data-stu-id="59be1-140">This was primarily toomake debugging easier.</span></span>

<span data-ttu-id="59be1-141">После объединить эти шаги hello конечным результатом является политику, которая выглядит одном hello.</span><span class="sxs-lookup"><span data-stu-id="59be1-141">Once you combine all these steps together, hello end result is a policy that looks like hello following one.</span></span>

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

<span data-ttu-id="59be1-142">Этот подход кэширования в основном используется в веб-сайтов которой HTML состоит на стороне сервера hello, чтобы он может быть отображен в виде одной страницы.</span><span class="sxs-lookup"><span data-stu-id="59be1-142">This caching approach is primarily used in web sites where HTML is composed on hello server side so that it can be rendered as a single page.</span></span> <span data-ttu-id="59be1-143">Тем не менее, его также можно использовать в API-интерфейсы, где клиенты не могут выполнять клиента стороне кэширования HTTP или желательно не tooput эту ответственность на приветствия клиента.</span><span class="sxs-lookup"><span data-stu-id="59be1-143">However, it can also be useful in APIs where clients cannot do client side HTTP caching or it is desirable not tooput that responsibility on hello client.</span></span>

<span data-ttu-id="59be1-144">Такого же вида фрагментарное кэширование может также выполняться на hello серверной части веб-серверов с помощью Redis, кэширование сервера, однако с помощью tooperform службы управления API hello эту работу полезно hello кэширования фрагментов соединяющиеся из разных назад элементов, чем hello Основные ответы.</span><span class="sxs-lookup"><span data-stu-id="59be1-144">This same kind of fragment caching can also be done on hello backend web servers using a Redis caching server, however, using hello API Management service tooperform this work is useful when hello cached fragments are coming from different back-ends than hello primary responses.</span></span>

## <a name="transparent-versioning"></a><span data-ttu-id="59be1-145">Прозрачное управление версиями</span><span class="sxs-lookup"><span data-stu-id="59be1-145">Transparent versioning</span></span>
<span data-ttu-id="59be1-146">Это принято для нескольких версий другую реализацию toobe API, поддерживаемые в любой момент времени.</span><span class="sxs-lookup"><span data-stu-id="59be1-146">It is common practice for multiple different implementation versions of an API toobe supported at any one time.</span></span> <span data-ttu-id="59be1-147">Это, возможно, toosupport различных средах, таких как разработки, тестирования, производства, и т.д., или может оказаться более старых версий toosupport время toogive hello API для API потребители toomigrate toonewer версий.</span><span class="sxs-lookup"><span data-stu-id="59be1-147">This is perhaps toosupport different environments, like dev, test, production, etc, or it may be toosupport older versions of hello API toogive time for API consumers toomigrate toonewer versions.</span></span> 

<span data-ttu-id="59be1-148">Один из подходов toohandling этом вместо от необходимости разработчики URL-адреса toochange hello из клиента `/v1/customers` слишком`/v2/customers` — toostore в hello потребителя данных профиля, какую версию hello API они в настоящее время обратиться toouse и вызовите соответствующий hello Внутренний URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="59be1-148">One approach toohandling this instead of requiring client developers toochange hello URLs from `/v1/customers` too`/v2/customers` is toostore in hello consumer’s profile data which version of hello API they currently wish toouse and call hello appropriate backend URL.</span></span> <span data-ttu-id="59be1-149">Порядок toodetermine hello правильный внутренний URL-адрес toocall для конкретного клиента, при необходимости tooquery некоторые данные конфигурации.</span><span class="sxs-lookup"><span data-stu-id="59be1-149">In order toodetermine hello correct backend URL toocall for a particular client, it is necessary tooquery some configuration data.</span></span> <span data-ttu-id="59be1-150">Кэширование эти данные конфигурации, мы минимизировать потери производительности hello, выполнив этот поиск.</span><span class="sxs-lookup"><span data-stu-id="59be1-150">By caching this configuration data, we can minimize hello performance penalty of doing this lookup.</span></span>

<span data-ttu-id="59be1-151">Первым шагом Hello — идентификатор hello toodetermine используемых tooconfigure hello нужную версию.</span><span class="sxs-lookup"><span data-stu-id="59be1-151">hello first step is toodetermine hello identifier used tooconfigure hello desired version.</span></span> <span data-ttu-id="59be1-152">В этом примере я выбрал подписки ключ продукта toohello tooassociate hello версии.</span><span class="sxs-lookup"><span data-stu-id="59be1-152">In this example, I chose tooassociate hello version toohello product subscription key.</span></span> 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

<span data-ttu-id="59be1-153">Если мы уже извлекли hello желаемую версии мы затем выполните toosee уточняющего запроса кэша.</span><span class="sxs-lookup"><span data-stu-id="59be1-153">We then do a cache lookup toosee if we already have retrieved hello desired client version.</span></span>

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

<span data-ttu-id="59be1-154">Затем мы проверяем toosee, если его не удалось найти в кэше hello.</span><span class="sxs-lookup"><span data-stu-id="59be1-154">Then we check toosee if we did not find it in hello cache.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

<span data-ttu-id="59be1-155">Если не удалось, ее нужно извлечь.</span><span class="sxs-lookup"><span data-stu-id="59be1-155">If we didn’t then we go and retrieve it.</span></span>

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

<span data-ttu-id="59be1-156">Основной текст ответа hello Извлеките из ответа hello.</span><span class="sxs-lookup"><span data-stu-id="59be1-156">Extract hello response body text from hello response.</span></span>

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

<span data-ttu-id="59be1-157">Храните его обратно в кэш hello для использования в будущем.</span><span class="sxs-lookup"><span data-stu-id="59be1-157">Store it back in hello cache for future use.</span></span>

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

<span data-ttu-id="59be1-158">И наконец обновление hello серверной части URL-адрес tooselect hello версия службы hello клиентом hello.</span><span class="sxs-lookup"><span data-stu-id="59be1-158">And finally update hello back-end URL tooselect hello version of hello service desired by hello client.</span></span>

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

<span data-ttu-id="59be1-159">Hello полностью политики выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="59be1-159">hello completely policy is as follows.</span></span>

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

<span data-ttu-id="59be1-160">Включение системы управления API потребители tootransparently серверной версии осуществляется клиентами без необходимости tooupdate и повторное развертывание клиентов — элегантное решение, которое решает многие проблемы управления версиями API.</span><span class="sxs-lookup"><span data-stu-id="59be1-160">Enabling API consumers tootransparently control which backend version is being accessed by clients without having tooupdate and redeploy clients is a elegant solution that addresses many API versioning concerns.</span></span>

## <a name="tenant-isolation"></a><span data-ttu-id="59be1-161">Изоляция клиентов</span><span class="sxs-lookup"><span data-stu-id="59be1-161">Tenant Isolation</span></span>
<span data-ttu-id="59be1-162">Некоторые компании с крупными развертываниями, состоящими из нескольких клиентов, создают отдельные группы клиентов на отдельных развернутых серверах.</span><span class="sxs-lookup"><span data-stu-id="59be1-162">In larger, multi-tenant deployments some companies create separate groups of tenants on distinct deployments of backend hardware.</span></span> <span data-ttu-id="59be1-163">Это сводит к минимуму hello количество клиентов, которые будут затронуты проблемой с оборудованием на серверной hello.</span><span class="sxs-lookup"><span data-stu-id="59be1-163">This minimizes hello number of customers who are impacted by a hardware issue on hello backend.</span></span> <span data-ttu-id="59be1-164">Он также обеспечивает новые toobe версии программного обеспечения, распространен на этапах.</span><span class="sxs-lookup"><span data-stu-id="59be1-164">It also enables new software versions toobe rolled out in stages.</span></span> <span data-ttu-id="59be1-165">Эта архитектура серверной желательно прозрачный tooAPI потребителей.</span><span class="sxs-lookup"><span data-stu-id="59be1-165">Ideally this backend architecture should be transparent tooAPI consumers.</span></span> <span data-ttu-id="59be1-166">Это можно сделать в аналогичные версий tootransparent способом, так как она основана на hello же метод управления hello URL-адрес внутреннего использования состояния конфигурации на ключ API.</span><span class="sxs-lookup"><span data-stu-id="59be1-166">This can be achieved in a similar way tootransparent versioning because it is based on hello same technique of manipulating hello backend URL using configuration state per API key.</span></span>  

<span data-ttu-id="59be1-167">Вместо возвращения предпочтительную версию hello API для каждого ключа подписки, возвратят идентификатор, который связывает группу клиента toohello назначенный оборудования.</span><span class="sxs-lookup"><span data-stu-id="59be1-167">Instead of returning a preferred version of hello API for each subscription key, you would return an identifier that relates a tenant toohello assigned hardware group.</span></span> <span data-ttu-id="59be1-168">Этот идентификатор может быть URL-адрес соответствующего внутреннего используется tooconstruct hello.</span><span class="sxs-lookup"><span data-stu-id="59be1-168">That identifier can be used tooconstruct hello appropriate backend URL.</span></span>

## <a name="summary"></a><span data-ttu-id="59be1-169">Сводка</span><span class="sxs-lookup"><span data-stu-id="59be1-169">Summary</span></span>
<span data-ttu-id="59be1-170">Hello свободу toouse hello кэш управления Azure API для хранения любого типа данных включает данные tooconfiguration эффективного доступа, которые могут повлиять на способ hello обработки входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="59be1-170">hello freedom toouse hello Azure API management cache for storing any kind of data enables efficient access tooconfiguration data that can affect hello way an inbound request is processed.</span></span> <span data-ttu-id="59be1-171">Он также может быть используется toostore фрагменты данных, которые можно дополнить ответы, возвращаемые API внутреннего сервера.</span><span class="sxs-lookup"><span data-stu-id="59be1-171">It can also be used toostore data fragments that can augment responses, returned from a backend API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59be1-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="59be1-172">Next steps</span></span>
<span data-ttu-id="59be1-173">Проверьте свой отзыв в hello Disqus потока для данного раздела при наличии других сценариев, эти политики включен автоматически, или скриптов, требующий tooachieve, но не уверены, что в данный момент возможны.</span><span class="sxs-lookup"><span data-stu-id="59be1-173">Please give us your feedback in hello Disqus thread for this topic if there are other scenarios that these policies have enabled for you, or if there are scenarios you would like tooachieve but do not feel are currently possible.</span></span>

