---
title: "Политики кэширования в службе управления API Azure | Документация Майкрософт"
description: "Сведения о политиках кэширования, доступных для использования в службе управления API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 8147199c-24d8-439f-b2a9-da28a70a890c
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2a8f012e7e223ef5c1683c8a6c5ecf2f3e96bed8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-caching-policies"></a><span data-ttu-id="e7061-103">Политики кэширования в службе управления API</span><span class="sxs-lookup"><span data-stu-id="e7061-103">API Management caching policies</span></span>
<span data-ttu-id="e7061-104">В этой статье рассматриваются приведенные ниже политики управления API.</span><span class="sxs-lookup"><span data-stu-id="e7061-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="e7061-105">Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в управлении API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="e7061-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="e7061-106"><a name="CachingPolicies"></a> Политики кэширования</span><span class="sxs-lookup"><span data-stu-id="e7061-106"><a name="CachingPolicies"></a> Caching policies</span></span>  
  
-   <span data-ttu-id="e7061-107">Политики кэширования ответов</span><span class="sxs-lookup"><span data-stu-id="e7061-107">Response caching policies</span></span>  
  
    -   <span data-ttu-id="e7061-108">[Получение из кэша](api-management-caching-policies.md#GetFromCache) — выполнение поиска в кэше и возврат допустимых кэшированных ответов при их наличии.</span><span class="sxs-lookup"><span data-stu-id="e7061-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span></span>  
  
    -   <span data-ttu-id="e7061-109">[Сохранение в кэше](api-management-caching-policies.md#StoreToCache) — помещение ответа в кэш в соответствии с заданной конфигурацией управления кэшем.</span><span class="sxs-lookup"><span data-stu-id="e7061-109">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches responses according to the specified cache control configuration.</span></span>  
  
-   <span data-ttu-id="e7061-110">Политики кэширования значений</span><span class="sxs-lookup"><span data-stu-id="e7061-110">Value caching policies</span></span>  
  
    -   <span data-ttu-id="e7061-111">[Получение значения из кэша](#GetFromCacheByKey) — получение кэшированного элемента по ключу.</span><span class="sxs-lookup"><span data-stu-id="e7061-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="e7061-112">[Сохранение значения в кэше](#StoreToCacheByKey) — сохранение элемента в кэше по ключу.</span><span class="sxs-lookup"><span data-stu-id="e7061-112">[Store value in cache](#StoreToCacheByKey) - Store an item in the cache by key.</span></span>  
  
    -   <span data-ttu-id="e7061-113">[Удалить значение из кэша](#RemoveCacheByKey) — удаление элемента в кэше по ключу.</span><span class="sxs-lookup"><span data-stu-id="e7061-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>  
  
##  <span data-ttu-id="e7061-114"><a name="GetFromCache"></a> Получение из кэша</span><span class="sxs-lookup"><span data-stu-id="e7061-114"><a name="GetFromCache"></a> Get from cache</span></span>  
 <span data-ttu-id="e7061-115">Политика `cache-lookup` используется для поиска в кэше и возврата допустимого кэшированного ответа при его наличии.</span><span class="sxs-lookup"><span data-stu-id="e7061-115">Use the `cache-lookup` policy to perform cache look up and return a valid cached response when available.</span></span> <span data-ttu-id="e7061-116">Эту политику можно применять в тех случаях, когда содержимое ответа остается неизменным в течение определенного интервала времени.</span><span class="sxs-lookup"><span data-stu-id="e7061-116">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="e7061-117">Кэширование ответов уменьшает требования к пропускной способности и вычислительной мощности, накладываемые на внутренний веб-сервер, а также снижает время задержки для потребителей API.</span><span class="sxs-lookup"><span data-stu-id="e7061-117">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="e7061-118">Одновременно с этой политикой должна быть определена соответствующая политика [сохранения в кэш](api-management-caching-policies.md#StoreToCache).</span><span class="sxs-lookup"><span data-stu-id="e7061-118">This policy must have a corresponding [Store to cache](api-management-caching-policies.md#StoreToCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e7061-119">Правило политики</span><span class="sxs-lookup"><span data-stu-id="e7061-119">Policy statement</span></span>  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression to evaluate)">  
  <vary-by-header>Accept</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Accept-Charset</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Authorization</vary-by-header>  
  <!-- should be present when allow-authorized-response-caching is "true"-->  
  <vary-by-header>header name</vary-by-header>  
  <!-- optional, can repeated several times -->  
  <vary-by-query-parameter>parameter name</vary-by-query-parameter>  
  <!-- optional, can repeated several times -->  
</cache-lookup>  
```  
  
### <a name="examples"></a><span data-ttu-id="e7061-120">Примеры</span><span class="sxs-lookup"><span data-stu-id="e7061-120">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="e7061-121">Пример</span><span class="sxs-lookup"><span data-stu-id="e7061-121">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="none" must-revalidate="true">  
            <vary-by-query-parameter>version</vary-by-query-parameter>  
        </cache-lookup>           
    </inbound>  
    <outbound>  
        <cache-store duration="seconds" />  
        <base />          
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="e7061-122">Пример с использованием выражений политики</span><span class="sxs-lookup"><span data-stu-id="e7061-122">Example using policy expressions</span></span>  
 <span data-ttu-id="e7061-123">Этот пример демонстрирует, как настроить в службе управления API период хранения ответов в кэше, соответствующий длительности кэширования ответа в серверной службе, которая задается директивой `Cache-Control` на сервере.</span><span class="sxs-lookup"><span data-stu-id="e7061-123">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="e7061-124">Пример настройки и использования этой политики см. в видео [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Облачное покрытие, серия 177. Дополнительные возможности службы управления API с Владом Виноградским) начиная с 25:25.</span><span class="sxs-lookup"><span data-stu-id="e7061-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
```xml  
<!-- The following cache policy snippets demonstrate how to control API Management reponse cache duration with Cache-Control headers sent by the backend service. -->  
  
<!-- Copy this snippet into the inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into the outbound section. Note that cache duration is set to the max-age value provided in the Cache-Control header received from the backend service or to the deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="e7061-125">Чтобы узнать больше, см. статью [API Management policy expressions](api-management-policy-expressions.md) (Выражения политики управления API) и раздел [Context variable](api-management-policy-expressions.md#ContextVariables) (Переменная контекста).</span><span class="sxs-lookup"><span data-stu-id="e7061-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="e7061-126">Элементы</span><span class="sxs-lookup"><span data-stu-id="e7061-126">Elements</span></span>  
  
|<span data-ttu-id="e7061-127">Имя</span><span class="sxs-lookup"><span data-stu-id="e7061-127">Name</span></span>|<span data-ttu-id="e7061-128">Описание</span><span class="sxs-lookup"><span data-stu-id="e7061-128">Description</span></span>|<span data-ttu-id="e7061-129">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e7061-129">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e7061-130">cache-lookup</span><span class="sxs-lookup"><span data-stu-id="e7061-130">cache-lookup</span></span>|<span data-ttu-id="e7061-131">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="e7061-131">Root element.</span></span>|<span data-ttu-id="e7061-132">Да</span><span class="sxs-lookup"><span data-stu-id="e7061-132">Yes</span></span>|  
|<span data-ttu-id="e7061-133">vary-by-header</span><span class="sxs-lookup"><span data-stu-id="e7061-133">vary-by-header</span></span>|<span data-ttu-id="e7061-134">Начало кэширования ответов по значению определенного заголовка, например Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span><span class="sxs-lookup"><span data-stu-id="e7061-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span></span>|<span data-ttu-id="e7061-135">Нет</span><span class="sxs-lookup"><span data-stu-id="e7061-135">No</span></span>|  
|<span data-ttu-id="e7061-136">vary-by-query-parameter</span><span class="sxs-lookup"><span data-stu-id="e7061-136">vary-by-query-parameter</span></span>|<span data-ttu-id="e7061-137">Запускается процесс кэширования ответов для значения заданных параметров запроса.</span><span class="sxs-lookup"><span data-stu-id="e7061-137">Start caching responses per value of specified query parameters.</span></span> <span data-ttu-id="e7061-138">Введите один или несколько параметров.</span><span class="sxs-lookup"><span data-stu-id="e7061-138">Enter a single or multiple parameters.</span></span> <span data-ttu-id="e7061-139">В качестве разделителя используйте точку с запятой.</span><span class="sxs-lookup"><span data-stu-id="e7061-139">Use semicolon as a separator.</span></span> <span data-ttu-id="e7061-140">Если значение не задано, используются все параметры запроса.</span><span class="sxs-lookup"><span data-stu-id="e7061-140">If none are specified, all query parameters are used.</span></span>|<span data-ttu-id="e7061-141">Нет</span><span class="sxs-lookup"><span data-stu-id="e7061-141">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e7061-142">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="e7061-142">Attributes</span></span>  
  
|<span data-ttu-id="e7061-143">Имя</span><span class="sxs-lookup"><span data-stu-id="e7061-143">Name</span></span>|<span data-ttu-id="e7061-144">Описание</span><span class="sxs-lookup"><span data-stu-id="e7061-144">Description</span></span>|<span data-ttu-id="e7061-145">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e7061-145">Required</span></span>|<span data-ttu-id="e7061-146">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e7061-146">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e7061-147">allow-private-response-caching</span><span class="sxs-lookup"><span data-stu-id="e7061-147">allow-private-response-caching</span></span>|<span data-ttu-id="e7061-148">Если задано значение `true`, разрешается кэширование запросов, содержащих заголовок авторизации.</span><span class="sxs-lookup"><span data-stu-id="e7061-148">When set to `true`, allows caching of requests that contain an Authorization header.</span></span>|<span data-ttu-id="e7061-149">Нет</span><span class="sxs-lookup"><span data-stu-id="e7061-149">No</span></span>|<span data-ttu-id="e7061-150">нет</span><span class="sxs-lookup"><span data-stu-id="e7061-150">false</span></span>|  
|<span data-ttu-id="e7061-151">downstream-caching-type</span><span class="sxs-lookup"><span data-stu-id="e7061-151">downstream-caching-type</span></span>|<span data-ttu-id="e7061-152">Для этого атрибута следует указать одно из таких значений:</span><span class="sxs-lookup"><span data-stu-id="e7061-152">This attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="e7061-153">- none — нисходящее кэширование не разрешено;</span><span class="sxs-lookup"><span data-stu-id="e7061-153">-   none - downstream caching is not allowed.</span></span><br /><span data-ttu-id="e7061-154">- private — разрешено нисходящее частное кэширование;</span><span class="sxs-lookup"><span data-stu-id="e7061-154">-   private - downstream private caching is allowed.</span></span><br /><span data-ttu-id="e7061-155">- public — разрешено частное и совместно используемое нисходящее кэширование.</span><span class="sxs-lookup"><span data-stu-id="e7061-155">-   public - private and shared downstream caching is allowed.</span></span>|<span data-ttu-id="e7061-156">Нет</span><span class="sxs-lookup"><span data-stu-id="e7061-156">No</span></span>|<span data-ttu-id="e7061-157">Нет</span><span class="sxs-lookup"><span data-stu-id="e7061-157">none</span></span>|  
|<span data-ttu-id="e7061-158">must-revalidate</span><span class="sxs-lookup"><span data-stu-id="e7061-158">must-revalidate</span></span>|<span data-ttu-id="e7061-159">Если включено нисходящее кэширование, этот атрибут включает или отключает директиву управления кэшем `must-revalidate` в ответах шлюза.</span><span class="sxs-lookup"><span data-stu-id="e7061-159">When downstream caching is enabled this attribute turns on or off  the `must-revalidate` cache control directive in gateway responses.</span></span>|<span data-ttu-id="e7061-160">Нет</span><span class="sxs-lookup"><span data-stu-id="e7061-160">No</span></span>|<span data-ttu-id="e7061-161">Да</span><span class="sxs-lookup"><span data-stu-id="e7061-161">true</span></span>|  
|<span data-ttu-id="e7061-162">vary-by-developer</span><span class="sxs-lookup"><span data-stu-id="e7061-162">vary-by-developer</span></span>|<span data-ttu-id="e7061-163">Установите значение `true`, если нужно кэшировать ответы в зависимости от ключа разработчика.</span><span class="sxs-lookup"><span data-stu-id="e7061-163">Set to `true` to cache responses per developer key.</span></span>|<span data-ttu-id="e7061-164">Нет</span><span class="sxs-lookup"><span data-stu-id="e7061-164">No</span></span>|<span data-ttu-id="e7061-165">нет</span><span class="sxs-lookup"><span data-stu-id="e7061-165">false</span></span>|  
|<span data-ttu-id="e7061-166">vary-by-developer-groups</span><span class="sxs-lookup"><span data-stu-id="e7061-166">vary-by-developer-groups</span></span>|<span data-ttu-id="e7061-167">Установите значение `true`, если нужно кэшировать ответы в зависимости от роли пользователя.</span><span class="sxs-lookup"><span data-stu-id="e7061-167">Set to `true` to cache responses per user role.</span></span>|<span data-ttu-id="e7061-168">Нет</span><span class="sxs-lookup"><span data-stu-id="e7061-168">No</span></span>|<span data-ttu-id="e7061-169">нет</span><span class="sxs-lookup"><span data-stu-id="e7061-169">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e7061-170">Использование</span><span class="sxs-lookup"><span data-stu-id="e7061-170">Usage</span></span>  
 <span data-ttu-id="e7061-171">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e7061-171">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e7061-172">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="e7061-172">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="e7061-173">**Области политики:** API, operation, product.</span><span class="sxs-lookup"><span data-stu-id="e7061-173">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="e7061-174"><a name="StoreToCache"></a> Сохранение в кэше</span><span class="sxs-lookup"><span data-stu-id="e7061-174"><a name="StoreToCache"></a> Store to cache</span></span>  
 <span data-ttu-id="e7061-175">Политика `cache-store` помещает в кэш ответы в соответствии с заданными настройками кэша.</span><span class="sxs-lookup"><span data-stu-id="e7061-175">The `cache-store` policy caches responses according to the specified cache settings.</span></span> <span data-ttu-id="e7061-176">Эту политику можно применять в тех случаях, когда содержимое ответа остается неизменным в течение определенного интервала времени.</span><span class="sxs-lookup"><span data-stu-id="e7061-176">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="e7061-177">Кэширование ответов уменьшает требования к пропускной способности и вычислительной мощности, накладываемые на внутренний веб-сервер, а также снижает время задержки для потребителей API.</span><span class="sxs-lookup"><span data-stu-id="e7061-177">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="e7061-178">Одновременно с этой политикой должна быть определена соответствующая политика [получения из кэша](api-management-caching-policies.md#GetFromCache).</span><span class="sxs-lookup"><span data-stu-id="e7061-178">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e7061-179">Правило политики</span><span class="sxs-lookup"><span data-stu-id="e7061-179">Policy statement</span></span>  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a><span data-ttu-id="e7061-180">Примеры</span><span class="sxs-lookup"><span data-stu-id="e7061-180">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="e7061-181">Пример</span><span class="sxs-lookup"><span data-stu-id="e7061-181">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
          <cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false">  
                <vary-by-query-parameter>parameter name</vary-by-query-parameter> <!-- optional, can repeated several times -->  
        </cache-lookup>  
    </inbound>  
    <outbound>  
        <base />  
            <cache-store duration="3600" />  
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="e7061-182">Пример с использованием выражений политики</span><span class="sxs-lookup"><span data-stu-id="e7061-182">Example using policy expressions</span></span>  
 <span data-ttu-id="e7061-183">Этот пример демонстрирует, как настроить в службе управления API период хранения ответов в кэше, соответствующий длительности кэширования ответа в серверной службе, которая задается директивой `Cache-Control` на сервере.</span><span class="sxs-lookup"><span data-stu-id="e7061-183">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="e7061-184">Пример настройки и использования этой политики см. в видео [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Облачное покрытие, серия 177. Дополнительные возможности службы управления API с Владом Виноградским) начиная с 25:25.</span><span class="sxs-lookup"><span data-stu-id="e7061-184">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
```xml  
<!-- The following cache policy snippets demonstrate how to control API Management reponse cache duration with Cache-Control headers sent by the backend service. -->  
  
<!-- Copy this snippet into the inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into the outbound section. Note that cache duration is set to the max-age value provided in the Cache-Control header received from the backend service or to the deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="e7061-185">Чтобы узнать больше, см. статью [API Management policy expressions](api-management-policy-expressions.md) (Выражения политики управления API) и раздел [Context variable](api-management-policy-expressions.md#ContextVariables) (Переменная контекста).</span><span class="sxs-lookup"><span data-stu-id="e7061-185">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="e7061-186">Элементы</span><span class="sxs-lookup"><span data-stu-id="e7061-186">Elements</span></span>  
  
|<span data-ttu-id="e7061-187">Имя</span><span class="sxs-lookup"><span data-stu-id="e7061-187">Name</span></span>|<span data-ttu-id="e7061-188">Описание</span><span class="sxs-lookup"><span data-stu-id="e7061-188">Description</span></span>|<span data-ttu-id="e7061-189">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e7061-189">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e7061-190">cache-store</span><span class="sxs-lookup"><span data-stu-id="e7061-190">cache-store</span></span>|<span data-ttu-id="e7061-191">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="e7061-191">Root element.</span></span>|<span data-ttu-id="e7061-192">Да</span><span class="sxs-lookup"><span data-stu-id="e7061-192">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e7061-193">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="e7061-193">Attributes</span></span>  
  
|<span data-ttu-id="e7061-194">Имя</span><span class="sxs-lookup"><span data-stu-id="e7061-194">Name</span></span>|<span data-ttu-id="e7061-195">Описание</span><span class="sxs-lookup"><span data-stu-id="e7061-195">Description</span></span>|<span data-ttu-id="e7061-196">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e7061-196">Required</span></span>|<span data-ttu-id="e7061-197">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e7061-197">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e7061-198">длительность</span><span class="sxs-lookup"><span data-stu-id="e7061-198">duration</span></span>|<span data-ttu-id="e7061-199">Срок жизни кэшированных записей (в секундах).</span><span class="sxs-lookup"><span data-stu-id="e7061-199">Time-to-live of the cached entries, specified in seconds.</span></span>|<span data-ttu-id="e7061-200">Да</span><span class="sxs-lookup"><span data-stu-id="e7061-200">Yes</span></span>|<span data-ttu-id="e7061-201">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e7061-201">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e7061-202">Использование</span><span class="sxs-lookup"><span data-stu-id="e7061-202">Usage</span></span>  
 <span data-ttu-id="e7061-203">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e7061-203">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e7061-204">**Разделы политики:** outbound.</span><span class="sxs-lookup"><span data-stu-id="e7061-204">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="e7061-205">**Области политики:** API, operation, product.</span><span class="sxs-lookup"><span data-stu-id="e7061-205">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="e7061-206"><a name="GetFromCacheByKey"></a> Получение значения из кэша</span><span class="sxs-lookup"><span data-stu-id="e7061-206"><a name="GetFromCacheByKey"></a> Get value from cache</span></span>  
 <span data-ttu-id="e7061-207">Используйте политику `cache-lookup-value`, чтобы выполнять поиск в кэше по ключу и возвращать кэшированное значение.</span><span class="sxs-lookup"><span data-stu-id="e7061-207">Use the `cache-lookup-value` policy to perform cache lookup by key and return a cached value.</span></span> <span data-ttu-id="e7061-208">Ключ может содержать произвольное строковое значение и обычно указывается с помощью выражения политики.</span><span class="sxs-lookup"><span data-stu-id="e7061-208">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="e7061-209">Одновременно с этой политикой должна быть определена соответствующая политика [сохранения значения в кэш](#StoreToCacheByKey).</span><span class="sxs-lookup"><span data-stu-id="e7061-209">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e7061-210">Правило политики</span><span class="sxs-lookup"><span data-stu-id="e7061-210">Policy statement</span></span>  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value to use if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a><span data-ttu-id="e7061-211">Пример</span><span class="sxs-lookup"><span data-stu-id="e7061-211">Example</span></span>  
 <span data-ttu-id="e7061-212">Дополнительные сведения и примеры этой политики см. в статье [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/) (Пользовательское кэширование в службе управления API Azure).</span><span class="sxs-lookup"><span data-stu-id="e7061-212">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="e7061-213">Элементы</span><span class="sxs-lookup"><span data-stu-id="e7061-213">Elements</span></span>  
  
|<span data-ttu-id="e7061-214">Имя</span><span class="sxs-lookup"><span data-stu-id="e7061-214">Name</span></span>|<span data-ttu-id="e7061-215">Описание</span><span class="sxs-lookup"><span data-stu-id="e7061-215">Description</span></span>|<span data-ttu-id="e7061-216">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e7061-216">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e7061-217">cache-lookup-value</span><span class="sxs-lookup"><span data-stu-id="e7061-217">cache-lookup-value</span></span>|<span data-ttu-id="e7061-218">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="e7061-218">Root element.</span></span>|<span data-ttu-id="e7061-219">Да</span><span class="sxs-lookup"><span data-stu-id="e7061-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e7061-220">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="e7061-220">Attributes</span></span>  
  
|<span data-ttu-id="e7061-221">Имя</span><span class="sxs-lookup"><span data-stu-id="e7061-221">Name</span></span>|<span data-ttu-id="e7061-222">Описание</span><span class="sxs-lookup"><span data-stu-id="e7061-222">Description</span></span>|<span data-ttu-id="e7061-223">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e7061-223">Required</span></span>|<span data-ttu-id="e7061-224">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e7061-224">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e7061-225">default-value</span><span class="sxs-lookup"><span data-stu-id="e7061-225">default-value</span></span>|<span data-ttu-id="e7061-226">Значение, которое присваивается переменной, если поиск в кэше по ключу не дал результатов.</span><span class="sxs-lookup"><span data-stu-id="e7061-226">A value that will be assigned to the variable if the cache key lookup resulted in a miss.</span></span> <span data-ttu-id="e7061-227">Если этот атрибут не указан, присваивается значение `null`.</span><span class="sxs-lookup"><span data-stu-id="e7061-227">If this attribute is not specified, `null` is assigned.</span></span>|<span data-ttu-id="e7061-228">Нет</span><span class="sxs-lookup"><span data-stu-id="e7061-228">No</span></span>|`null`|  
|<span data-ttu-id="e7061-229">key</span><span class="sxs-lookup"><span data-stu-id="e7061-229">key</span></span>|<span data-ttu-id="e7061-230">Значение ключа кэша, которое нужно использовать при поиске.</span><span class="sxs-lookup"><span data-stu-id="e7061-230">Cache key value to use in the lookup.</span></span>|<span data-ttu-id="e7061-231">Да</span><span class="sxs-lookup"><span data-stu-id="e7061-231">Yes</span></span>|<span data-ttu-id="e7061-232">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e7061-232">N/A</span></span>|  
|<span data-ttu-id="e7061-233">variable-name</span><span class="sxs-lookup"><span data-stu-id="e7061-233">variable-name</span></span>|<span data-ttu-id="e7061-234">Имя [переменной контекста](api-management-policy-expressions.md#ContextVariables), которой присваивается найденное значение, если поиск завершится успешно.</span><span class="sxs-lookup"><span data-stu-id="e7061-234">Name of the [context variable](api-management-policy-expressions.md#ContextVariables) the looked up value will be assigned to, if lookup is successful.</span></span> <span data-ttu-id="e7061-235">Если поиск не даст результатов, этой переменной присваивается значение, указанное в атрибуте `default-value`. Если атрибут `default-value` не задан, присваивается значение `null`.</span><span class="sxs-lookup"><span data-stu-id="e7061-235">If lookup results in a miss, the variable will be assigned the value of the `default-value` attribute or `null`, if the `default-value` attribute is omitted.</span></span>|<span data-ttu-id="e7061-236">Да</span><span class="sxs-lookup"><span data-stu-id="e7061-236">Yes</span></span>|<span data-ttu-id="e7061-237">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e7061-237">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e7061-238">Использование</span><span class="sxs-lookup"><span data-stu-id="e7061-238">Usage</span></span>  
 <span data-ttu-id="e7061-239">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e7061-239">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e7061-240">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="e7061-240">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="e7061-241">**Области политики:** global, API, operation, product.</span><span class="sxs-lookup"><span data-stu-id="e7061-241">**Policy scopes:** global, API, operation, product</span></span>  
  
##  <span data-ttu-id="e7061-242"><a name="StoreToCacheByKey"></a> Сохранение значения в кэш</span><span class="sxs-lookup"><span data-stu-id="e7061-242"><a name="StoreToCacheByKey"></a> Store value in cache</span></span>  
 <span data-ttu-id="e7061-243">Политика `cache-store-value` выполняет сохранение в кэш по ключу.</span><span class="sxs-lookup"><span data-stu-id="e7061-243">The `cache-store-value` performs cache storage by key.</span></span> <span data-ttu-id="e7061-244">Ключ может содержать произвольное строковое значение и обычно указывается с помощью выражения политики.</span><span class="sxs-lookup"><span data-stu-id="e7061-244">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="e7061-245">Одновременно с этой политикой должна быть определена соответствующая политика [получения значения из кэша](#GetFromCacheByKey).</span><span class="sxs-lookup"><span data-stu-id="e7061-245">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e7061-246">Правило политики</span><span class="sxs-lookup"><span data-stu-id="e7061-246">Policy statement</span></span>  
  
```xml  
<cache-store-value key="cache key value" value="value to cache" duration="seconds" />  
```  
  
### <a name="example"></a><span data-ttu-id="e7061-247">Пример</span><span class="sxs-lookup"><span data-stu-id="e7061-247">Example</span></span>  
 <span data-ttu-id="e7061-248">Дополнительные сведения и примеры этой политики см. в статье [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/) (Пользовательское кэширование в службе управления API Azure).</span><span class="sxs-lookup"><span data-stu-id="e7061-248">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="e7061-249">Элементы</span><span class="sxs-lookup"><span data-stu-id="e7061-249">Elements</span></span>  
  
|<span data-ttu-id="e7061-250">Имя</span><span class="sxs-lookup"><span data-stu-id="e7061-250">Name</span></span>|<span data-ttu-id="e7061-251">Описание</span><span class="sxs-lookup"><span data-stu-id="e7061-251">Description</span></span>|<span data-ttu-id="e7061-252">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e7061-252">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e7061-253">cache-store-value</span><span class="sxs-lookup"><span data-stu-id="e7061-253">cache-store-value</span></span>|<span data-ttu-id="e7061-254">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="e7061-254">Root element.</span></span>|<span data-ttu-id="e7061-255">Да</span><span class="sxs-lookup"><span data-stu-id="e7061-255">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e7061-256">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="e7061-256">Attributes</span></span>  
  
|<span data-ttu-id="e7061-257">Имя</span><span class="sxs-lookup"><span data-stu-id="e7061-257">Name</span></span>|<span data-ttu-id="e7061-258">Описание</span><span class="sxs-lookup"><span data-stu-id="e7061-258">Description</span></span>|<span data-ttu-id="e7061-259">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e7061-259">Required</span></span>|<span data-ttu-id="e7061-260">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e7061-260">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e7061-261">длительность</span><span class="sxs-lookup"><span data-stu-id="e7061-261">duration</span></span>|<span data-ttu-id="e7061-262">Кэшированные значения сохраняются в течение указанного здесь времени (в секундах).</span><span class="sxs-lookup"><span data-stu-id="e7061-262">Value will be cached for the provided duration value, specified in seconds.</span></span>|<span data-ttu-id="e7061-263">Да</span><span class="sxs-lookup"><span data-stu-id="e7061-263">Yes</span></span>|<span data-ttu-id="e7061-264">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e7061-264">N/A</span></span>|  
|<span data-ttu-id="e7061-265">key</span><span class="sxs-lookup"><span data-stu-id="e7061-265">key</span></span>|<span data-ttu-id="e7061-266">Ключ кэша, под которым будет храниться значение.</span><span class="sxs-lookup"><span data-stu-id="e7061-266">Cache key the value will be stored under.</span></span>|<span data-ttu-id="e7061-267">Да</span><span class="sxs-lookup"><span data-stu-id="e7061-267">Yes</span></span>|<span data-ttu-id="e7061-268">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e7061-268">N/A</span></span>|  
|<span data-ttu-id="e7061-269">значение</span><span class="sxs-lookup"><span data-stu-id="e7061-269">value</span></span>|<span data-ttu-id="e7061-270">Значение, которое нужно кэшировать.</span><span class="sxs-lookup"><span data-stu-id="e7061-270">The value to be cached.</span></span>|<span data-ttu-id="e7061-271">Да</span><span class="sxs-lookup"><span data-stu-id="e7061-271">Yes</span></span>|<span data-ttu-id="e7061-272">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e7061-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e7061-273">Использование</span><span class="sxs-lookup"><span data-stu-id="e7061-273">Usage</span></span>  
 <span data-ttu-id="e7061-274">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e7061-274">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e7061-275">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="e7061-275">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="e7061-276">**Области политики:** global, API, operation, product.</span><span class="sxs-lookup"><span data-stu-id="e7061-276">**Policy scopes:** global, API, operation, product</span></span>  
  
###  <span data-ttu-id="e7061-277"><a name="RemoveCacheByKey"></a> Удаление значения из кэша</span><span class="sxs-lookup"><span data-stu-id="e7061-277"><a name="RemoveCacheByKey"></a> Remove value from cache</span></span>  
 <span data-ttu-id="e7061-278">Политика `cache-remove-value` удаляет кэшированный элемент, определяемый по соответствующему ключу.</span><span class="sxs-lookup"><span data-stu-id="e7061-278">The             `cache-remove-value` deletes a cached item identified by its key.</span></span> <span data-ttu-id="e7061-279">Ключ может содержать произвольное строковое значение и обычно указывается с помощью выражения политики.</span><span class="sxs-lookup"><span data-stu-id="e7061-279">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
#### <a name="policy-statement"></a><span data-ttu-id="e7061-280">Правило политики</span><span class="sxs-lookup"><span data-stu-id="e7061-280">Policy statement</span></span>  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="e7061-281">Пример</span><span class="sxs-lookup"><span data-stu-id="e7061-281">Example</span></span>  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a><span data-ttu-id="e7061-282">Элементы</span><span class="sxs-lookup"><span data-stu-id="e7061-282">Elements</span></span>  
  
|<span data-ttu-id="e7061-283">Имя</span><span class="sxs-lookup"><span data-stu-id="e7061-283">Name</span></span>|<span data-ttu-id="e7061-284">Описание</span><span class="sxs-lookup"><span data-stu-id="e7061-284">Description</span></span>|<span data-ttu-id="e7061-285">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e7061-285">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e7061-286">cache-remove-value</span><span class="sxs-lookup"><span data-stu-id="e7061-286">cache-remove-value</span></span>|<span data-ttu-id="e7061-287">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="e7061-287">Root element.</span></span>|<span data-ttu-id="e7061-288">Да</span><span class="sxs-lookup"><span data-stu-id="e7061-288">Yes</span></span>|  
  
#### <a name="attributes"></a><span data-ttu-id="e7061-289">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="e7061-289">Attributes</span></span>  
  
|<span data-ttu-id="e7061-290">Имя</span><span class="sxs-lookup"><span data-stu-id="e7061-290">Name</span></span>|<span data-ttu-id="e7061-291">Описание</span><span class="sxs-lookup"><span data-stu-id="e7061-291">Description</span></span>|<span data-ttu-id="e7061-292">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e7061-292">Required</span></span>|<span data-ttu-id="e7061-293">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e7061-293">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e7061-294">key</span><span class="sxs-lookup"><span data-stu-id="e7061-294">key</span></span>|<span data-ttu-id="e7061-295">Ключ кэшированного ранее значения, которое нужно удалить из кэша.</span><span class="sxs-lookup"><span data-stu-id="e7061-295">The key of the previously cached value to be removed from the cache.</span></span>|<span data-ttu-id="e7061-296">Да</span><span class="sxs-lookup"><span data-stu-id="e7061-296">Yes</span></span>|<span data-ttu-id="e7061-297">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e7061-297">N/A</span></span>|  
  
#### <a name="usage"></a><span data-ttu-id="e7061-298">Использование</span><span class="sxs-lookup"><span data-stu-id="e7061-298">Usage</span></span>  
 <span data-ttu-id="e7061-299">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) политики.</span><span class="sxs-lookup"><span data-stu-id="e7061-299">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="e7061-300">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="e7061-300">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="e7061-301">**Области политики:** global, API, operation, product.</span><span class="sxs-lookup"><span data-stu-id="e7061-301">**Policy scopes:** global, API, operation, product</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="e7061-302">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e7061-302">Next steps</span></span>
<span data-ttu-id="e7061-303">Дополнительные сведения о работе с политиками см. в статье со справочными материалами по [политикам в службе управления API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="e7061-303">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  