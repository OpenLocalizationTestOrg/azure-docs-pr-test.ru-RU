---
title: "Пользовательское кэширование в службе управления API Azure"
description: "Информация о кэшировании элементов с помощью ключа в службе управления API Azure"
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
ms.openlocfilehash: f5d5f44e34fbcd122a10be0ca5b3001760c4c64d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="custom-caching-in-azure-api-management"></a><span data-ttu-id="21533-103">Пользовательское кэширование в службе управления API Azure</span><span class="sxs-lookup"><span data-stu-id="21533-103">Custom caching in Azure API Management</span></span>
<span data-ttu-id="21533-104">В службе управления API Azure есть встроенная поддержка [кэширования ответов HTTP](api-management-howto-cache.md) с помощью URL-адреса ресурса в качестве ключа.</span><span class="sxs-lookup"><span data-stu-id="21533-104">Azure API Management service has built-in support for [HTTP response caching](api-management-howto-cache.md) using the resource URL as the key.</span></span> <span data-ttu-id="21533-105">Ключ можно изменить с помощью заголовков запроса, используя свойства `vary-by` .</span><span class="sxs-lookup"><span data-stu-id="21533-105">The key can be modified by request headers using the `vary-by` properties.</span></span> <span data-ttu-id="21533-106">Этот способ подходит для кэширования всех ответов HTTP (или представлений), но иногда его можно использовать только для кэширования части представления.</span><span class="sxs-lookup"><span data-stu-id="21533-106">This is useful for caching entire HTTP responses (aka representations), but sometimes it is useful to just cache a portion of a representation.</span></span> <span data-ttu-id="21533-107">Новые политики [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) и [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) позволяют сохранять и извлекать произвольные фрагменты данных из определений политики.</span><span class="sxs-lookup"><span data-stu-id="21533-107">The new [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) and [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) policies provide the ability to store and retrieve arbitrary pieces of data from within policy definitions.</span></span> <span data-ttu-id="21533-108">Эта возможность также полезна для ранее представленной политики [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) , так как теперь можно кэшировать ответы от внешних служб.</span><span class="sxs-lookup"><span data-stu-id="21533-108">This ability also adds value to the previously introduced [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy because you can now cache responses from external services.</span></span>

## <a name="architecture"></a><span data-ttu-id="21533-109">Архитектура</span><span class="sxs-lookup"><span data-stu-id="21533-109">Architecture</span></span>
<span data-ttu-id="21533-110">Служба управления API использует общий кэш данных клиентов таким образом, чтобы при увеличении масштаба до нескольких единиц вы по-прежнему имели доступ к тем же кэшированным данным.</span><span class="sxs-lookup"><span data-stu-id="21533-110">API Management service uses a shared per-tenant data cache so that, as you scale up to multiple units you will still get access to the same cached data.</span></span> <span data-ttu-id="21533-111">Но если вы работаете с развертыванием в нескольких регионах, в каждом регионе существует отдельный кэш.</span><span class="sxs-lookup"><span data-stu-id="21533-111">However, when working with a multi-region deployment there are independent caches within each of the regions.</span></span> <span data-ttu-id="21533-112">Поэтому важно обрабатывать кэш как хранилище данных, которое является единственным источником конкретной информации.</span><span class="sxs-lookup"><span data-stu-id="21533-112">Due to this, it is important to not treat the cache as a data store, where it is the only source of some piece of information.</span></span> <span data-ttu-id="21533-113">Если вы так и делали, а затем решили воспользоваться преимуществами развертывания в нескольких регионах, клиенты с пользователями, которые ездят в командировки, могут потерять доступ к кэшированным данным.</span><span class="sxs-lookup"><span data-stu-id="21533-113">If you did, and later decided to take advantage of the multi-region deployment, then customers with users that travel may lose access to that cached data.</span></span>

## <a name="fragment-caching"></a><span data-ttu-id="21533-114">Кэширование фрагментов</span><span class="sxs-lookup"><span data-stu-id="21533-114">Fragment caching</span></span>
<span data-ttu-id="21533-115">В определенных случаях возвращаемые ответы содержат часть данных, которые трудно определить и которые остаются новыми в течение приемлемого времени.</span><span class="sxs-lookup"><span data-stu-id="21533-115">There are certain cases where responses being returned contain some portion of data that is expensive to determine and yet remains fresh for a reasonable amount of time.</span></span> <span data-ttu-id="21533-116">Например, рассмотрим созданную авиакомпанией службу, которая предоставляет сведения о бронировании авиабилетов, статусе рейсов и другую информацию. Если пользователь является участником программы сбора баллов авиакомпании, он также увидит их текущее состояние и накопленные мили.</span><span class="sxs-lookup"><span data-stu-id="21533-116">As an example, consider a service built by an airline that provides information relating flight reservations, flight status, etc. If the user is a member of the airlines points program, they would also have information relating to their current status and mileage accumulated.</span></span> <span data-ttu-id="21533-117">Эта информация о пользователе может храниться в другой системе, но, возможно, придется включить ее в ответы, возвращаемые на запрос о статусе рейсов и бронировании билетов.</span><span class="sxs-lookup"><span data-stu-id="21533-117">This user-related information might be stored in a different system, but it may be desirable to include it in responses returned about flight status and reservations.</span></span> <span data-ttu-id="21533-118">Это можно сделать с помощью кэширования фрагментов.</span><span class="sxs-lookup"><span data-stu-id="21533-118">This can be done using a process called fragment caching.</span></span> <span data-ttu-id="21533-119">Основное представление может быть возвращено с сервера-источника с помощью специального маркера, который указывает, где нужно вставить информацию о пользователе.</span><span class="sxs-lookup"><span data-stu-id="21533-119">The primary representation can be returned from the origin server using some kind of token to indicate where the user-related information is to be inserted.</span></span> 

<span data-ttu-id="21533-120">Рассмотрим следующий ответ JSON с API серверной части:</span><span class="sxs-lookup"><span data-stu-id="21533-120">Consider the following JSON response from a backend API.</span></span>

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

<span data-ttu-id="21533-121">Также рассмотрим дополнительный ресурс по адресу `/userprofile/{userid}` :</span><span class="sxs-lookup"><span data-stu-id="21533-121">And secondary resource at `/userprofile/{userid}` that looks like,</span></span>

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

<span data-ttu-id="21533-122">Чтобы определить информацию соответствующего пользователя, которая должна быть включена, необходимо определить конечного пользователя.</span><span class="sxs-lookup"><span data-stu-id="21533-122">In order to determine the appropriate user information to include, we need to identify who the end user is.</span></span> <span data-ttu-id="21533-123">Этот механизм зависит от реализации.</span><span class="sxs-lookup"><span data-stu-id="21533-123">This mechanism is implementation dependent.</span></span> <span data-ttu-id="21533-124">В качестве примера я использую утверждение `Subject` маркера `JWT`.</span><span class="sxs-lookup"><span data-stu-id="21533-124">As an example, I am using the `Subject` claim of a `JWT` token.</span></span> 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

<span data-ttu-id="21533-125">Мы сохраняем это значение `enduserid` в переменной контекста для дальнейшего использования.</span><span class="sxs-lookup"><span data-stu-id="21533-125">We store this `enduserid` value in a context variable for later use.</span></span> <span data-ttu-id="21533-126">Затем нужно определить, получил ли предыдущий запрос сведения о пользователе и сохранил ли их в кэше.</span><span class="sxs-lookup"><span data-stu-id="21533-126">The next step is to determine if a previous request has already retrieved the user information and stored it in the cache.</span></span> <span data-ttu-id="21533-127">Для этого мы используем политику `cache-lookup-value` .</span><span class="sxs-lookup"><span data-stu-id="21533-127">For this we use the `cache-lookup-value` policy.</span></span>

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

<span data-ttu-id="21533-128">Если в кэше нет записи, которая соответствует значению ключа, переменная контекста `userprofile` не создается.</span><span class="sxs-lookup"><span data-stu-id="21533-128">If there is no entry in the cache that corresponds to the key value, then no `userprofile` context variable will be created.</span></span> <span data-ttu-id="21533-129">Проверим правильность подстановки с помощью политики потока управления `choose` .</span><span class="sxs-lookup"><span data-stu-id="21533-129">We check the success of the lookup using the `choose` control flow policy.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If the userprofile context variable doesn’t exist, make an HTTP request to retrieve it.  -->
    </when>
</choose>
```

<span data-ttu-id="21533-130">Если переменная контекста `userprofile` не существует, нам нужно выполнить запрос HTTP, чтобы получить ее.</span><span class="sxs-lookup"><span data-stu-id="21533-130">If the `userprofile` context variable doesn’t exist, then we are going to have to make an HTTP request to retrieve it.</span></span>

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points to the profile for the current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="21533-131">Чтобы создать URL-адрес ресурса профиля пользователя, используем `enduserid` .</span><span class="sxs-lookup"><span data-stu-id="21533-131">We use the `enduserid` to construct the URL to the user profile resource.</span></span> <span data-ttu-id="21533-132">После получения ответа можно будет извлечь текст из ответа и снова сохранить его в переменной контекста.</span><span class="sxs-lookup"><span data-stu-id="21533-132">Once we have the response, we can pull the body text out of the response and store it back into a context variable.</span></span>

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

<span data-ttu-id="21533-133">Чтобы не выполнять этот HTTP-запрос еще раз, когда тот же пользователь выполняет другой запрос, можно сохранить профиль пользователя в кэше.</span><span class="sxs-lookup"><span data-stu-id="21533-133">To avoid us having to make this HTTP request again, when the same user makes another request, we can store the user profile in the cache.</span></span>

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

<span data-ttu-id="21533-134">Значение сохраняется в кэше с помощью того же ключа, который изначально использовался для его извлечения.</span><span class="sxs-lookup"><span data-stu-id="21533-134">We store the value in the cache using the exact same key that we originally attempted to retrieve it with.</span></span> <span data-ttu-id="21533-135">Длительность хранения значения зависит от частоты изменения информации и толерантности пользователей к устаревшим сведениям.</span><span class="sxs-lookup"><span data-stu-id="21533-135">The duration that we choose to store the value should be based on how often the information changes and how tolerant users are to out of date information.</span></span> 

<span data-ttu-id="21533-136">Важно осознавать, что извлечение из кэша все еще выполняется как внепроцессный сетевой запрос и может добавить десятки миллисекунд к запросу.</span><span class="sxs-lookup"><span data-stu-id="21533-136">It is important to realize that retrieving from the cache is still an out-of-process, network request and potentially can still add tens of milliseconds to the request.</span></span> <span data-ttu-id="21533-137">Преимущества можно заметить, когда определение сведений профиля пользователя занимает значительно больше времени, чем извлечение данных из кэша, из-за запросов к базе данных и статистической обработки информации с нескольких серверов.</span><span class="sxs-lookup"><span data-stu-id="21533-137">The benefits come when determining the user profile information takes significantly longer than that due to needing to do database queries or aggregate information from multiple back-ends.</span></span>

<span data-ttu-id="21533-138">В самом конце процесса нам нужно обновить возвращенный ответ с информацией профиля пользователя.</span><span class="sxs-lookup"><span data-stu-id="21533-138">The final step in the process is to update the returned response with our user profile information.</span></span>

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

<span data-ttu-id="21533-139">Я решил использовать кавычки как часть маркера, чтобы, даже если не произойдет замена, ответ по-прежнему содержал допустимые данные JSON.</span><span class="sxs-lookup"><span data-stu-id="21533-139">I chose to include the quotation marks as part of the token so that even when the replace doesn’t occur, the response was still valid JSON.</span></span> <span data-ttu-id="21533-140">Основная цель этого подхода — упростить отладку.</span><span class="sxs-lookup"><span data-stu-id="21533-140">This was primarily to make debugging easier.</span></span>

<span data-ttu-id="21533-141">Выполнив все действия, в качестве результата вы получите политику, которая выглядит приблизительно так:</span><span class="sxs-lookup"><span data-stu-id="21533-141">Once you combine all these steps together, the end result is a policy that looks like the following one.</span></span>

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in the cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in the cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request to get user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points to the profile for the current end-user -->
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

<span data-ttu-id="21533-142">Этот метод кэширования используется в основном на веб-сайтах, на которых HTML формируется на стороне сервера для отображения в виде одной страницы.</span><span class="sxs-lookup"><span data-stu-id="21533-142">This caching approach is primarily used in web sites where HTML is composed on the server side so that it can be rendered as a single page.</span></span> <span data-ttu-id="21533-143">Этот метод также можно использовать в API-интерфейсах, в которых клиенты не могут выполнять клиентское HTTP-кэширование или в которых нежелательно возлагать ответственность за кэширование на клиент.</span><span class="sxs-lookup"><span data-stu-id="21533-143">However, it can also be useful in APIs where clients cannot do client side HTTP caching or it is desirable not to put that responsibility on the client.</span></span>

<span data-ttu-id="21533-144">Такое же кэширование фрагментов можно выполнить на внутренних веб-серверах с помощью сервера кэширования Redis. Однако для этой задачи лучше использовать службу управления API, если кэшированные фрагменты и основные ответы поступают с разных серверов.</span><span class="sxs-lookup"><span data-stu-id="21533-144">This same kind of fragment caching can also be done on the backend web servers using a Redis caching server, however, using the API Management service to perform this work is useful when the cached fragments are coming from different back-ends than the primary responses.</span></span>

## <a name="transparent-versioning"></a><span data-ttu-id="21533-145">Прозрачное управление версиями</span><span class="sxs-lookup"><span data-stu-id="21533-145">Transparent versioning</span></span>
<span data-ttu-id="21533-146">Это управление рекомендуется использовать для нескольких версий реализации API, которые должны поддерживаться одновременно.</span><span class="sxs-lookup"><span data-stu-id="21533-146">It is common practice for multiple different implementation versions of an API to be supported at any one time.</span></span> <span data-ttu-id="21533-147">Оно обеспечивает поддержку различных сред (разработки, тестирования, производства и т. д.) или поддержку более старых версий API, благодаря чему пользователи API получают дополнительное время для перехода на более новые версии.</span><span class="sxs-lookup"><span data-stu-id="21533-147">This is perhaps to support different environments, like dev, test, production, etc, or it may be to support older versions of the API to give time for API consumers to migrate to newer versions.</span></span> 

<span data-ttu-id="21533-148">Чтобы не заставлять разработчика клиента изменять URL-адреса с `/v1/customers` на `/v2/customers`, рекомендуется хранить в данных профиля пользователя версию API, которую предпочитает пользователь, и вызывать соответствующий внутренний URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="21533-148">One approach to handling this instead of requiring client developers to change the URLs from `/v1/customers` to `/v2/customers` is to store in the consumer’s profile data which version of the API they currently wish to use and call the appropriate backend URL.</span></span> <span data-ttu-id="21533-149">Чтобы определить правильный внутренний URL-адрес для вызова конкретного клиента, необходимо запросить конкретные данные конфигурации.</span><span class="sxs-lookup"><span data-stu-id="21533-149">In order to determine the correct backend URL to call for a particular client, it is necessary to query some configuration data.</span></span> <span data-ttu-id="21533-150">Кэшируя эти данные конфигурации, мы можем свести к минимуму снижение производительности во время выполнения поиска.</span><span class="sxs-lookup"><span data-stu-id="21533-150">By caching this configuration data, we can minimize the performance penalty of doing this lookup.</span></span>

<span data-ttu-id="21533-151">Сначала следует определить идентификатор, который используется для настройки нужной версии.</span><span class="sxs-lookup"><span data-stu-id="21533-151">The first step is to determine the identifier used to configure the desired version.</span></span> <span data-ttu-id="21533-152">В этом примере я решил связать версию с ключом подписки продукта.</span><span class="sxs-lookup"><span data-stu-id="21533-152">In this example, I chose to associate the version to the product subscription key.</span></span> 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

<span data-ttu-id="21533-153">Затем выполним поиск по кэшу, чтобы выяснить, извлечена ли нужная клиентская версия.</span><span class="sxs-lookup"><span data-stu-id="21533-153">We then do a cache lookup to see if we already have retrieved the desired client version.</span></span>

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

<span data-ttu-id="21533-154">Затем проверим, удалось ли найти ее в кэше.</span><span class="sxs-lookup"><span data-stu-id="21533-154">Then we check to see if we did not find it in the cache.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

<span data-ttu-id="21533-155">Если не удалось, ее нужно извлечь.</span><span class="sxs-lookup"><span data-stu-id="21533-155">If we didn’t then we go and retrieve it.</span></span>

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

<span data-ttu-id="21533-156">Извлеките текст из ответа.</span><span class="sxs-lookup"><span data-stu-id="21533-156">Extract the response body text from the response.</span></span>

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

<span data-ttu-id="21533-157">Сохраните его в кэше для дальнейшего использования.</span><span class="sxs-lookup"><span data-stu-id="21533-157">Store it back in the cache for future use.</span></span>

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

<span data-ttu-id="21533-158">Наконец, обновите внутренний URL-адрес, чтобы выбрать версию службы, которую предпочитает клиент.</span><span class="sxs-lookup"><span data-stu-id="21533-158">And finally update the back-end URL to select the version of the service desired by the client.</span></span>

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

<span data-ttu-id="21533-159">Полная политика выглядит так:</span><span class="sxs-lookup"><span data-stu-id="21533-159">The completely policy is as follows.</span></span>

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in the cache, make a request for it and store it -->
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

<span data-ttu-id="21533-160">Разрешение пользователям API прозрачно управлять доступом клиентов к версиям серверной части без необходимости обновления и повторного развертывания клиентов решает многие проблемы управления версиями API.</span><span class="sxs-lookup"><span data-stu-id="21533-160">Enabling API consumers to transparently control which backend version is being accessed by clients without having to update and redeploy clients is a elegant solution that addresses many API versioning concerns.</span></span>

## <a name="tenant-isolation"></a><span data-ttu-id="21533-161">Изоляция клиентов</span><span class="sxs-lookup"><span data-stu-id="21533-161">Tenant Isolation</span></span>
<span data-ttu-id="21533-162">Некоторые компании с крупными развертываниями, состоящими из нескольких клиентов, создают отдельные группы клиентов на отдельных развернутых серверах.</span><span class="sxs-lookup"><span data-stu-id="21533-162">In larger, multi-tenant deployments some companies create separate groups of tenants on distinct deployments of backend hardware.</span></span> <span data-ttu-id="21533-163">Это минимизирует число пользователей, которых может коснуться ошибка оборудования на сервере.</span><span class="sxs-lookup"><span data-stu-id="21533-163">This minimizes the number of customers who are impacted by a hardware issue on the backend.</span></span> <span data-ttu-id="21533-164">Этот подход также обеспечивает поэтапное развертывание новых версий программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="21533-164">It also enables new software versions to be rolled out in stages.</span></span> <span data-ttu-id="21533-165">В идеале эта архитектура серверной части должна быть прозрачной для пользователей API.</span><span class="sxs-lookup"><span data-stu-id="21533-165">Ideally this backend architecture should be transparent to API consumers.</span></span> <span data-ttu-id="21533-166">Этого можно добиться за счет такого же прозрачного управления версиями, которое реализуется посредством управления внутренними URL-адресами с помощью состояния конфигурации для каждого ключа API.</span><span class="sxs-lookup"><span data-stu-id="21533-166">This can be achieved in a similar way to transparent versioning because it is based on the same technique of manipulating the backend URL using configuration state per API key.</span></span>  

<span data-ttu-id="21533-167">Вместо возвращения предпочтительной версии API для каждого ключа подписки вы будете возвращать идентификатор клиента для назначенной группы оборудования.</span><span class="sxs-lookup"><span data-stu-id="21533-167">Instead of returning a preferred version of the API for each subscription key, you would return an identifier that relates a tenant to the assigned hardware group.</span></span> <span data-ttu-id="21533-168">Этот идентификатор можно использовать для создания соответствующих внутренних URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="21533-168">That identifier can be used to construct the appropriate backend URL.</span></span>

## <a name="summary"></a><span data-ttu-id="21533-169">Сводка</span><span class="sxs-lookup"><span data-stu-id="21533-169">Summary</span></span>
<span data-ttu-id="21533-170">Использование кэширования службы управления API Azure для хранения любых данных обеспечивает эффективный доступ к данным конфигурации, которые могут повлиять на способ обработки входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="21533-170">The freedom to use the Azure API management cache for storing any kind of data enables efficient access to configuration data that can affect the way an inbound request is processed.</span></span> <span data-ttu-id="21533-171">Этот подход также можно использовать для хранения фрагментов данных, которые могут дополнять ответы, возвращаемые из серверной части API.</span><span class="sxs-lookup"><span data-stu-id="21533-171">It can also be used to store data fragments that can augment responses, returned from a backend API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="21533-172">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="21533-172">Next steps</span></span>
<span data-ttu-id="21533-173">Отправьте нам свой отзыв в дискуссию Disqus к данной статье, если эти политики позволяют вам использовать другие сценарии либо если вы хотите, но пока не можете использовать те или иные сценарии.</span><span class="sxs-lookup"><span data-stu-id="21533-173">Please give us your feedback in the Disqus thread for this topic if there are other scenarios that these policies have enabled for you, or if there are scenarios you would like to achieve but do not feel are currently possible.</span></span>

