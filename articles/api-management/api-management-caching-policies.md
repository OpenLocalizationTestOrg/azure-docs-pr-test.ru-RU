---
title: "политики кэширования API Management aaaAzure | Документы Microsoft"
description: "Дополнительные сведения о hello, доступные для использования в службе управления API Azure политики кэширования."
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
ms.openlocfilehash: bd6b0721945609b28dbf6e7ef0631979c08c8c65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-caching-policies"></a><span data-ttu-id="e2164-103">Политики кэширования в службе управления API</span><span class="sxs-lookup"><span data-stu-id="e2164-103">API Management caching policies</span></span>
<span data-ttu-id="e2164-104">Здесь вы найдете ссылку для hello следующих политиках управления интерфейсами API.</span><span class="sxs-lookup"><span data-stu-id="e2164-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="e2164-105">Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в управлении API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="e2164-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="e2164-106"><a name="CachingPolicies"></a> Политики кэширования</span><span class="sxs-lookup"><span data-stu-id="e2164-106"><a name="CachingPolicies"></a> Caching policies</span></span>  
  
-   <span data-ttu-id="e2164-107">Политики кэширования ответов</span><span class="sxs-lookup"><span data-stu-id="e2164-107">Response caching policies</span></span>  
  
    -   <span data-ttu-id="e2164-108">[Получение из кэша](api-management-caching-policies.md#GetFromCache) — выполнение поиска в кэше и возврат допустимых кэшированных ответов при их наличии.</span><span class="sxs-lookup"><span data-stu-id="e2164-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span></span>  
  
    -   <span data-ttu-id="e2164-109">[Хранить toocache](api-management-caching-policies.md#StoreToCache) - кэши ответы в соответствии с toohello указанной конфигурации управления кэшем.</span><span class="sxs-lookup"><span data-stu-id="e2164-109">[Store toocache](api-management-caching-policies.md#StoreToCache) - Caches responses according toohello specified cache control configuration.</span></span>  
  
-   <span data-ttu-id="e2164-110">Политики кэширования значений</span><span class="sxs-lookup"><span data-stu-id="e2164-110">Value caching policies</span></span>  
  
    -   <span data-ttu-id="e2164-111">[Получение значения из кэша](#GetFromCacheByKey) — получение кэшированного элемента по ключу.</span><span class="sxs-lookup"><span data-stu-id="e2164-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="e2164-112">[Сохраните значение в кэше](#StoreToCacheByKey) -хранения элемента в кэше hello по ключу.</span><span class="sxs-lookup"><span data-stu-id="e2164-112">[Store value in cache](#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>  
  
    -   <span data-ttu-id="e2164-113">[Удалить значение из кэша](#RemoveCacheByKey) -удалить элемент из кэша hello по ключу.</span><span class="sxs-lookup"><span data-stu-id="e2164-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>  
  
##  <span data-ttu-id="e2164-114"><a name="GetFromCache"></a> Получение из кэша</span><span class="sxs-lookup"><span data-stu-id="e2164-114"><a name="GetFromCache"></a> Get from cache</span></span>  
 <span data-ttu-id="e2164-115">Используйте hello `cache-lookup` кэша политики tooperform поиска и возвращения допустимого кэшированного ответа, если оно доступно.</span><span class="sxs-lookup"><span data-stu-id="e2164-115">Use hello `cache-lookup` policy tooperform cache look up and return a valid cached response when available.</span></span> <span data-ttu-id="e2164-116">Эту политику можно применять в тех случаях, когда содержимое ответа остается неизменным в течение определенного интервала времени.</span><span class="sxs-lookup"><span data-stu-id="e2164-116">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="e2164-117">Кэширование ответов снижает пропускную способность и требования к обработке, применяемая hello серверной части web server и уменьшает задержку пользователей API.</span><span class="sxs-lookup"><span data-stu-id="e2164-117">Response caching reduces bandwidth and processing requirements imposed on hello backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="e2164-118">Эта политика должна соответствовать [toocache хранилища](api-management-caching-policies.md#StoreToCache) политики.</span><span class="sxs-lookup"><span data-stu-id="e2164-118">This policy must have a corresponding [Store toocache](api-management-caching-policies.md#StoreToCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e2164-119">Правило политики</span><span class="sxs-lookup"><span data-stu-id="e2164-119">Policy statement</span></span>  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression tooevaluate)">  
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
  
### <a name="examples"></a><span data-ttu-id="e2164-120">Примеры</span><span class="sxs-lookup"><span data-stu-id="e2164-120">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="e2164-121">Пример</span><span class="sxs-lookup"><span data-stu-id="e2164-121">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="e2164-122">Пример с использованием выражений политики</span><span class="sxs-lookup"><span data-stu-id="e2164-122">Example using policy expressions</span></span>  
 <span data-ttu-id="e2164-123">В этом примере показано, как ответ API управления tootooconfigure совпадений Здравствуйте, кэширование ответов hello серверной службы в соответствии с hello длительность кэширования резервное службы `Cache-Control` директивы.</span><span class="sxs-lookup"><span data-stu-id="e2164-123">This example shows how tootooconfigure API Management response caching duration that matches hello response caching of hello backend service as specified by hello backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="e2164-124">Демонстрацию настройке и использовании этой политики см. в разделе [177 серии охватывают облачные: более возможности API управления с помощью Влад Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) и too25:25 Перемотка вперед.</span><span class="sxs-lookup"><span data-stu-id="e2164-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too25:25.</span></span>  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="e2164-125">Чтобы узнать больше, см. статью [API Management policy expressions](api-management-policy-expressions.md) (Выражения политики управления API) и раздел [Context variable](api-management-policy-expressions.md#ContextVariables) (Переменная контекста).</span><span class="sxs-lookup"><span data-stu-id="e2164-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="e2164-126">Элементы</span><span class="sxs-lookup"><span data-stu-id="e2164-126">Elements</span></span>  
  
|<span data-ttu-id="e2164-127">Имя</span><span class="sxs-lookup"><span data-stu-id="e2164-127">Name</span></span>|<span data-ttu-id="e2164-128">Описание</span><span class="sxs-lookup"><span data-stu-id="e2164-128">Description</span></span>|<span data-ttu-id="e2164-129">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e2164-129">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e2164-130">cache-lookup</span><span class="sxs-lookup"><span data-stu-id="e2164-130">cache-lookup</span></span>|<span data-ttu-id="e2164-131">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="e2164-131">Root element.</span></span>|<span data-ttu-id="e2164-132">Да</span><span class="sxs-lookup"><span data-stu-id="e2164-132">Yes</span></span>|  
|<span data-ttu-id="e2164-133">vary-by-header</span><span class="sxs-lookup"><span data-stu-id="e2164-133">vary-by-header</span></span>|<span data-ttu-id="e2164-134">Начало кэширования ответов по значению определенного заголовка, например Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span><span class="sxs-lookup"><span data-stu-id="e2164-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span></span>|<span data-ttu-id="e2164-135">Нет</span><span class="sxs-lookup"><span data-stu-id="e2164-135">No</span></span>|  
|<span data-ttu-id="e2164-136">vary-by-query-parameter</span><span class="sxs-lookup"><span data-stu-id="e2164-136">vary-by-query-parameter</span></span>|<span data-ttu-id="e2164-137">Запускается процесс кэширования ответов для значения заданных параметров запроса.</span><span class="sxs-lookup"><span data-stu-id="e2164-137">Start caching responses per value of specified query parameters.</span></span> <span data-ttu-id="e2164-138">Введите один или несколько параметров.</span><span class="sxs-lookup"><span data-stu-id="e2164-138">Enter a single or multiple parameters.</span></span> <span data-ttu-id="e2164-139">В качестве разделителя используйте точку с запятой.</span><span class="sxs-lookup"><span data-stu-id="e2164-139">Use semicolon as a separator.</span></span> <span data-ttu-id="e2164-140">Если значение не задано, используются все параметры запроса.</span><span class="sxs-lookup"><span data-stu-id="e2164-140">If none are specified, all query parameters are used.</span></span>|<span data-ttu-id="e2164-141">Нет</span><span class="sxs-lookup"><span data-stu-id="e2164-141">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e2164-142">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="e2164-142">Attributes</span></span>  
  
|<span data-ttu-id="e2164-143">Имя</span><span class="sxs-lookup"><span data-stu-id="e2164-143">Name</span></span>|<span data-ttu-id="e2164-144">Описание</span><span class="sxs-lookup"><span data-stu-id="e2164-144">Description</span></span>|<span data-ttu-id="e2164-145">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e2164-145">Required</span></span>|<span data-ttu-id="e2164-146">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e2164-146">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e2164-147">allow-private-response-caching</span><span class="sxs-lookup"><span data-stu-id="e2164-147">allow-private-response-caching</span></span>|<span data-ttu-id="e2164-148">Если задано слишком`true`, разрешает кэширование запросов, содержащих заголовок авторизации.</span><span class="sxs-lookup"><span data-stu-id="e2164-148">When set too`true`, allows caching of requests that contain an Authorization header.</span></span>|<span data-ttu-id="e2164-149">Нет</span><span class="sxs-lookup"><span data-stu-id="e2164-149">No</span></span>|<span data-ttu-id="e2164-150">нет</span><span class="sxs-lookup"><span data-stu-id="e2164-150">false</span></span>|  
|<span data-ttu-id="e2164-151">downstream-caching-type</span><span class="sxs-lookup"><span data-stu-id="e2164-151">downstream-caching-type</span></span>|<span data-ttu-id="e2164-152">Этот атрибут должен быть задан tooone из hello следующие значения.</span><span class="sxs-lookup"><span data-stu-id="e2164-152">This attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="e2164-153">- none — нисходящее кэширование не разрешено;</span><span class="sxs-lookup"><span data-stu-id="e2164-153">-   none - downstream caching is not allowed.</span></span><br /><span data-ttu-id="e2164-154">- private — разрешено нисходящее частное кэширование;</span><span class="sxs-lookup"><span data-stu-id="e2164-154">-   private - downstream private caching is allowed.</span></span><br /><span data-ttu-id="e2164-155">- public — разрешено частное и совместно используемое нисходящее кэширование.</span><span class="sxs-lookup"><span data-stu-id="e2164-155">-   public - private and shared downstream caching is allowed.</span></span>|<span data-ttu-id="e2164-156">Нет</span><span class="sxs-lookup"><span data-stu-id="e2164-156">No</span></span>|<span data-ttu-id="e2164-157">Нет</span><span class="sxs-lookup"><span data-stu-id="e2164-157">none</span></span>|  
|<span data-ttu-id="e2164-158">must-revalidate</span><span class="sxs-lookup"><span data-stu-id="e2164-158">must-revalidate</span></span>|<span data-ttu-id="e2164-159">При включенном кэшировании нижестоящим этот атрибут включает или выключает hello `must-revalidate` директиву управления кэшем в ответах шлюза.</span><span class="sxs-lookup"><span data-stu-id="e2164-159">When downstream caching is enabled this attribute turns on or off  hello `must-revalidate` cache control directive in gateway responses.</span></span>|<span data-ttu-id="e2164-160">Нет</span><span class="sxs-lookup"><span data-stu-id="e2164-160">No</span></span>|<span data-ttu-id="e2164-161">Да</span><span class="sxs-lookup"><span data-stu-id="e2164-161">true</span></span>|  
|<span data-ttu-id="e2164-162">vary-by-developer</span><span class="sxs-lookup"><span data-stu-id="e2164-162">vary-by-developer</span></span>|<span data-ttu-id="e2164-163">Значение слишком`true` toocache ответов на основе ключа разработчика.</span><span class="sxs-lookup"><span data-stu-id="e2164-163">Set too`true` toocache responses per developer key.</span></span>|<span data-ttu-id="e2164-164">Нет</span><span class="sxs-lookup"><span data-stu-id="e2164-164">No</span></span>|<span data-ttu-id="e2164-165">нет</span><span class="sxs-lookup"><span data-stu-id="e2164-165">false</span></span>|  
|<span data-ttu-id="e2164-166">vary-by-developer-groups</span><span class="sxs-lookup"><span data-stu-id="e2164-166">vary-by-developer-groups</span></span>|<span data-ttu-id="e2164-167">Значение слишком`true` toocache ответов на основе роли пользователя.</span><span class="sxs-lookup"><span data-stu-id="e2164-167">Set too`true` toocache responses per user role.</span></span>|<span data-ttu-id="e2164-168">Нет</span><span class="sxs-lookup"><span data-stu-id="e2164-168">No</span></span>|<span data-ttu-id="e2164-169">нет</span><span class="sxs-lookup"><span data-stu-id="e2164-169">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e2164-170">Использование</span><span class="sxs-lookup"><span data-stu-id="e2164-170">Usage</span></span>  
 <span data-ttu-id="e2164-171">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e2164-171">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e2164-172">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="e2164-172">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="e2164-173">**Области политики:** API, operation, product.</span><span class="sxs-lookup"><span data-stu-id="e2164-173">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="e2164-174"><a name="StoreToCache"></a>Toocache хранилища</span><span class="sxs-lookup"><span data-stu-id="e2164-174"><a name="StoreToCache"></a> Store toocache</span></span>  
 <span data-ttu-id="e2164-175">Hello `cache-store` политики кэши ответы в соответствии с toohello указаны параметры кэша.</span><span class="sxs-lookup"><span data-stu-id="e2164-175">hello `cache-store` policy caches responses according toohello specified cache settings.</span></span> <span data-ttu-id="e2164-176">Эту политику можно применять в тех случаях, когда содержимое ответа остается неизменным в течение определенного интервала времени.</span><span class="sxs-lookup"><span data-stu-id="e2164-176">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="e2164-177">Кэширование ответов снижает пропускную способность и требования к обработке, применяемая hello серверной части web server и уменьшает задержку пользователей API.</span><span class="sxs-lookup"><span data-stu-id="e2164-177">Response caching reduces bandwidth and processing requirements imposed on hello backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="e2164-178">Одновременно с этой политикой должна быть определена соответствующая политика [получения из кэша](api-management-caching-policies.md#GetFromCache).</span><span class="sxs-lookup"><span data-stu-id="e2164-178">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e2164-179">Правило политики</span><span class="sxs-lookup"><span data-stu-id="e2164-179">Policy statement</span></span>  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a><span data-ttu-id="e2164-180">Примеры</span><span class="sxs-lookup"><span data-stu-id="e2164-180">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="e2164-181">Пример</span><span class="sxs-lookup"><span data-stu-id="e2164-181">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="e2164-182">Пример с использованием выражений политики</span><span class="sxs-lookup"><span data-stu-id="e2164-182">Example using policy expressions</span></span>  
 <span data-ttu-id="e2164-183">В этом примере показано, как ответ API управления tootooconfigure совпадений Здравствуйте, кэширование ответов hello серверной службы в соответствии с hello длительность кэширования резервное службы `Cache-Control` директивы.</span><span class="sxs-lookup"><span data-stu-id="e2164-183">This example shows how tootooconfigure API Management response caching duration that matches hello response caching of hello backend service as specified by hello backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="e2164-184">Демонстрацию настройке и использовании этой политики см. в разделе [177 серии охватывают облачные: более возможности API управления с помощью Влад Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) и too25:25 Перемотка вперед.</span><span class="sxs-lookup"><span data-stu-id="e2164-184">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too25:25.</span></span>  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="e2164-185">Чтобы узнать больше, см. статью [API Management policy expressions](api-management-policy-expressions.md) (Выражения политики управления API) и раздел [Context variable](api-management-policy-expressions.md#ContextVariables) (Переменная контекста).</span><span class="sxs-lookup"><span data-stu-id="e2164-185">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="e2164-186">Элементы</span><span class="sxs-lookup"><span data-stu-id="e2164-186">Elements</span></span>  
  
|<span data-ttu-id="e2164-187">Имя</span><span class="sxs-lookup"><span data-stu-id="e2164-187">Name</span></span>|<span data-ttu-id="e2164-188">Описание</span><span class="sxs-lookup"><span data-stu-id="e2164-188">Description</span></span>|<span data-ttu-id="e2164-189">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e2164-189">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e2164-190">cache-store</span><span class="sxs-lookup"><span data-stu-id="e2164-190">cache-store</span></span>|<span data-ttu-id="e2164-191">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="e2164-191">Root element.</span></span>|<span data-ttu-id="e2164-192">Да</span><span class="sxs-lookup"><span data-stu-id="e2164-192">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e2164-193">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="e2164-193">Attributes</span></span>  
  
|<span data-ttu-id="e2164-194">Имя</span><span class="sxs-lookup"><span data-stu-id="e2164-194">Name</span></span>|<span data-ttu-id="e2164-195">Описание</span><span class="sxs-lookup"><span data-stu-id="e2164-195">Description</span></span>|<span data-ttu-id="e2164-196">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e2164-196">Required</span></span>|<span data-ttu-id="e2164-197">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e2164-197">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e2164-198">длительность</span><span class="sxs-lookup"><span data-stu-id="e2164-198">duration</span></span>|<span data-ttu-id="e2164-199">Время жизни объекта hello кэшированных записей, указанное в секундах.</span><span class="sxs-lookup"><span data-stu-id="e2164-199">Time-to-live of hello cached entries, specified in seconds.</span></span>|<span data-ttu-id="e2164-200">Да</span><span class="sxs-lookup"><span data-stu-id="e2164-200">Yes</span></span>|<span data-ttu-id="e2164-201">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e2164-201">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e2164-202">Использование</span><span class="sxs-lookup"><span data-stu-id="e2164-202">Usage</span></span>  
 <span data-ttu-id="e2164-203">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e2164-203">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e2164-204">**Разделы политики:** outbound.</span><span class="sxs-lookup"><span data-stu-id="e2164-204">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="e2164-205">**Области политики:** API, operation, product.</span><span class="sxs-lookup"><span data-stu-id="e2164-205">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="e2164-206"><a name="GetFromCacheByKey"></a> Получение значения из кэша</span><span class="sxs-lookup"><span data-stu-id="e2164-206"><a name="GetFromCacheByKey"></a> Get value from cache</span></span>  
 <span data-ttu-id="e2164-207">Используйте hello `cache-lookup-value` tooperform политики кэширования Уточняющий запрос по ключу и возвращает кэшированное значение.</span><span class="sxs-lookup"><span data-stu-id="e2164-207">Use hello `cache-lookup-value` policy tooperform cache lookup by key and return a cached value.</span></span> <span data-ttu-id="e2164-208">ключ Hello может иметь произвольное строковое значение и обычно обеспечивается с помощью выражения политики.</span><span class="sxs-lookup"><span data-stu-id="e2164-208">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="e2164-209">Одновременно с этой политикой должна быть определена соответствующая политика [сохранения значения в кэш](#StoreToCacheByKey).</span><span class="sxs-lookup"><span data-stu-id="e2164-209">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e2164-210">Правило политики</span><span class="sxs-lookup"><span data-stu-id="e2164-210">Policy statement</span></span>  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value toouse if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a><span data-ttu-id="e2164-211">Пример</span><span class="sxs-lookup"><span data-stu-id="e2164-211">Example</span></span>  
 <span data-ttu-id="e2164-212">Дополнительные сведения и примеры этой политики см. в статье [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/) (Пользовательское кэширование в службе управления API Azure).</span><span class="sxs-lookup"><span data-stu-id="e2164-212">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="e2164-213">Элементы</span><span class="sxs-lookup"><span data-stu-id="e2164-213">Elements</span></span>  
  
|<span data-ttu-id="e2164-214">Имя</span><span class="sxs-lookup"><span data-stu-id="e2164-214">Name</span></span>|<span data-ttu-id="e2164-215">Описание</span><span class="sxs-lookup"><span data-stu-id="e2164-215">Description</span></span>|<span data-ttu-id="e2164-216">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e2164-216">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e2164-217">cache-lookup-value</span><span class="sxs-lookup"><span data-stu-id="e2164-217">cache-lookup-value</span></span>|<span data-ttu-id="e2164-218">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="e2164-218">Root element.</span></span>|<span data-ttu-id="e2164-219">Да</span><span class="sxs-lookup"><span data-stu-id="e2164-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e2164-220">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="e2164-220">Attributes</span></span>  
  
|<span data-ttu-id="e2164-221">Имя</span><span class="sxs-lookup"><span data-stu-id="e2164-221">Name</span></span>|<span data-ttu-id="e2164-222">Описание</span><span class="sxs-lookup"><span data-stu-id="e2164-222">Description</span></span>|<span data-ttu-id="e2164-223">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e2164-223">Required</span></span>|<span data-ttu-id="e2164-224">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e2164-224">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e2164-225">default-value</span><span class="sxs-lookup"><span data-stu-id="e2164-225">default-value</span></span>|<span data-ttu-id="e2164-226">Значение, которое будет присвоено переменной toohello, если поиск ключа кэша hello привело к созданию промах.</span><span class="sxs-lookup"><span data-stu-id="e2164-226">A value that will be assigned toohello variable if hello cache key lookup resulted in a miss.</span></span> <span data-ttu-id="e2164-227">Если этот атрибут не указан, присваивается значение `null`.</span><span class="sxs-lookup"><span data-stu-id="e2164-227">If this attribute is not specified, `null` is assigned.</span></span>|<span data-ttu-id="e2164-228">Нет</span><span class="sxs-lookup"><span data-stu-id="e2164-228">No</span></span>|`null`|  
|<span data-ttu-id="e2164-229">key</span><span class="sxs-lookup"><span data-stu-id="e2164-229">key</span></span>|<span data-ttu-id="e2164-230">Кэшировать toouse значение ключа в уточняющем запросе hello.</span><span class="sxs-lookup"><span data-stu-id="e2164-230">Cache key value toouse in hello lookup.</span></span>|<span data-ttu-id="e2164-231">Да</span><span class="sxs-lookup"><span data-stu-id="e2164-231">Yes</span></span>|<span data-ttu-id="e2164-232">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e2164-232">N/A</span></span>|  
|<span data-ttu-id="e2164-233">variable-name</span><span class="sxs-lookup"><span data-stu-id="e2164-233">variable-name</span></span>|<span data-ttu-id="e2164-234">Имя hello [переменной контекста](api-management-policy-expressions.md#ContextVariables) hello, поиск значения будет назначаться, при успешном выполнении уточняющего запроса.</span><span class="sxs-lookup"><span data-stu-id="e2164-234">Name of hello [context variable](api-management-policy-expressions.md#ContextVariables) hello looked up value will be assigned to, if lookup is successful.</span></span> <span data-ttu-id="e2164-235">При поиске промах, hello переменной назначается значение hello hello `default-value` атрибута или `null`, если hello `default-value` атрибут опущен.</span><span class="sxs-lookup"><span data-stu-id="e2164-235">If lookup results in a miss, hello variable will be assigned hello value of hello `default-value` attribute or `null`, if hello `default-value` attribute is omitted.</span></span>|<span data-ttu-id="e2164-236">Да</span><span class="sxs-lookup"><span data-stu-id="e2164-236">Yes</span></span>|<span data-ttu-id="e2164-237">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e2164-237">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e2164-238">Использование</span><span class="sxs-lookup"><span data-stu-id="e2164-238">Usage</span></span>  
 <span data-ttu-id="e2164-239">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e2164-239">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e2164-240">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="e2164-240">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="e2164-241">**Области политики:** global, API, operation, product.</span><span class="sxs-lookup"><span data-stu-id="e2164-241">**Policy scopes:** global, API, operation, product</span></span>  
  
##  <span data-ttu-id="e2164-242"><a name="StoreToCacheByKey"></a> Сохранение значения в кэш</span><span class="sxs-lookup"><span data-stu-id="e2164-242"><a name="StoreToCacheByKey"></a> Store value in cache</span></span>  
 <span data-ttu-id="e2164-243">Hello `cache-store-value` выполняет хранилища кэша по ключу.</span><span class="sxs-lookup"><span data-stu-id="e2164-243">hello `cache-store-value` performs cache storage by key.</span></span> <span data-ttu-id="e2164-244">ключ Hello может иметь произвольное строковое значение и обычно обеспечивается с помощью выражения политики.</span><span class="sxs-lookup"><span data-stu-id="e2164-244">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="e2164-245">Одновременно с этой политикой должна быть определена соответствующая политика [получения значения из кэша](#GetFromCacheByKey).</span><span class="sxs-lookup"><span data-stu-id="e2164-245">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e2164-246">Правило политики</span><span class="sxs-lookup"><span data-stu-id="e2164-246">Policy statement</span></span>  
  
```xml  
<cache-store-value key="cache key value" value="value toocache" duration="seconds" />  
```  
  
### <a name="example"></a><span data-ttu-id="e2164-247">Пример</span><span class="sxs-lookup"><span data-stu-id="e2164-247">Example</span></span>  
 <span data-ttu-id="e2164-248">Дополнительные сведения и примеры этой политики см. в статье [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/) (Пользовательское кэширование в службе управления API Azure).</span><span class="sxs-lookup"><span data-stu-id="e2164-248">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="e2164-249">Элементы</span><span class="sxs-lookup"><span data-stu-id="e2164-249">Elements</span></span>  
  
|<span data-ttu-id="e2164-250">Имя</span><span class="sxs-lookup"><span data-stu-id="e2164-250">Name</span></span>|<span data-ttu-id="e2164-251">Описание</span><span class="sxs-lookup"><span data-stu-id="e2164-251">Description</span></span>|<span data-ttu-id="e2164-252">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e2164-252">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e2164-253">cache-store-value</span><span class="sxs-lookup"><span data-stu-id="e2164-253">cache-store-value</span></span>|<span data-ttu-id="e2164-254">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="e2164-254">Root element.</span></span>|<span data-ttu-id="e2164-255">Да</span><span class="sxs-lookup"><span data-stu-id="e2164-255">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e2164-256">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="e2164-256">Attributes</span></span>  
  
|<span data-ttu-id="e2164-257">Имя</span><span class="sxs-lookup"><span data-stu-id="e2164-257">Name</span></span>|<span data-ttu-id="e2164-258">Описание</span><span class="sxs-lookup"><span data-stu-id="e2164-258">Description</span></span>|<span data-ttu-id="e2164-259">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e2164-259">Required</span></span>|<span data-ttu-id="e2164-260">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e2164-260">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e2164-261">длительность</span><span class="sxs-lookup"><span data-stu-id="e2164-261">duration</span></span>|<span data-ttu-id="e2164-262">Значение будет кэшироваться hello указанное значение длительности, указанное в секундах.</span><span class="sxs-lookup"><span data-stu-id="e2164-262">Value will be cached for hello provided duration value, specified in seconds.</span></span>|<span data-ttu-id="e2164-263">Да</span><span class="sxs-lookup"><span data-stu-id="e2164-263">Yes</span></span>|<span data-ttu-id="e2164-264">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e2164-264">N/A</span></span>|  
|<span data-ttu-id="e2164-265">key</span><span class="sxs-lookup"><span data-stu-id="e2164-265">key</span></span>|<span data-ttu-id="e2164-266">Значение ключа hello кэша будет храниться в группе.</span><span class="sxs-lookup"><span data-stu-id="e2164-266">Cache key hello value will be stored under.</span></span>|<span data-ttu-id="e2164-267">Да</span><span class="sxs-lookup"><span data-stu-id="e2164-267">Yes</span></span>|<span data-ttu-id="e2164-268">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e2164-268">N/A</span></span>|  
|<span data-ttu-id="e2164-269">value</span><span class="sxs-lookup"><span data-stu-id="e2164-269">value</span></span>|<span data-ttu-id="e2164-270">toobe значение Hello в кэше.</span><span class="sxs-lookup"><span data-stu-id="e2164-270">hello value toobe cached.</span></span>|<span data-ttu-id="e2164-271">Да</span><span class="sxs-lookup"><span data-stu-id="e2164-271">Yes</span></span>|<span data-ttu-id="e2164-272">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e2164-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e2164-273">Использование</span><span class="sxs-lookup"><span data-stu-id="e2164-273">Usage</span></span>  
 <span data-ttu-id="e2164-274">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e2164-274">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e2164-275">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="e2164-275">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="e2164-276">**Области политики:** global, API, operation, product.</span><span class="sxs-lookup"><span data-stu-id="e2164-276">**Policy scopes:** global, API, operation, product</span></span>  
  
###  <span data-ttu-id="e2164-277"><a name="RemoveCacheByKey"></a> Удаление значения из кэша</span><span class="sxs-lookup"><span data-stu-id="e2164-277"><a name="RemoveCacheByKey"></a> Remove value from cache</span></span>  
 <span data-ttu-id="e2164-278">Hello `cache-remove-value` удаляет кэшированный элемент, определенный по его ключу.</span><span class="sxs-lookup"><span data-stu-id="e2164-278">hello             `cache-remove-value` deletes a cached item identified by its key.</span></span> <span data-ttu-id="e2164-279">ключ Hello может иметь произвольное строковое значение и обычно обеспечивается с помощью выражения политики.</span><span class="sxs-lookup"><span data-stu-id="e2164-279">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
#### <a name="policy-statement"></a><span data-ttu-id="e2164-280">Правило политики</span><span class="sxs-lookup"><span data-stu-id="e2164-280">Policy statement</span></span>  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="e2164-281">Пример</span><span class="sxs-lookup"><span data-stu-id="e2164-281">Example</span></span>  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a><span data-ttu-id="e2164-282">Элементы</span><span class="sxs-lookup"><span data-stu-id="e2164-282">Elements</span></span>  
  
|<span data-ttu-id="e2164-283">Имя</span><span class="sxs-lookup"><span data-stu-id="e2164-283">Name</span></span>|<span data-ttu-id="e2164-284">Описание</span><span class="sxs-lookup"><span data-stu-id="e2164-284">Description</span></span>|<span data-ttu-id="e2164-285">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e2164-285">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e2164-286">cache-remove-value</span><span class="sxs-lookup"><span data-stu-id="e2164-286">cache-remove-value</span></span>|<span data-ttu-id="e2164-287">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="e2164-287">Root element.</span></span>|<span data-ttu-id="e2164-288">Да</span><span class="sxs-lookup"><span data-stu-id="e2164-288">Yes</span></span>|  
  
#### <a name="attributes"></a><span data-ttu-id="e2164-289">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="e2164-289">Attributes</span></span>  
  
|<span data-ttu-id="e2164-290">Имя</span><span class="sxs-lookup"><span data-stu-id="e2164-290">Name</span></span>|<span data-ttu-id="e2164-291">Описание</span><span class="sxs-lookup"><span data-stu-id="e2164-291">Description</span></span>|<span data-ttu-id="e2164-292">Обязательно</span><span class="sxs-lookup"><span data-stu-id="e2164-292">Required</span></span>|<span data-ttu-id="e2164-293">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="e2164-293">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e2164-294">key</span><span class="sxs-lookup"><span data-stu-id="e2164-294">key</span></span>|<span data-ttu-id="e2164-295">ключ Hello hello кэшированные значения toobe, удаленных из кэша hello.</span><span class="sxs-lookup"><span data-stu-id="e2164-295">hello key of hello previously cached value toobe removed from hello cache.</span></span>|<span data-ttu-id="e2164-296">Да</span><span class="sxs-lookup"><span data-stu-id="e2164-296">Yes</span></span>|<span data-ttu-id="e2164-297">Недоступно</span><span class="sxs-lookup"><span data-stu-id="e2164-297">N/A</span></span>|  
  
#### <a name="usage"></a><span data-ttu-id="e2164-298">Использование</span><span class="sxs-lookup"><span data-stu-id="e2164-298">Usage</span></span>  
 <span data-ttu-id="e2164-299">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="e2164-299">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="e2164-300">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="e2164-300">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="e2164-301">**Области политики:** global, API, operation, product.</span><span class="sxs-lookup"><span data-stu-id="e2164-301">**Policy scopes:** global, API, operation, product</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="e2164-302">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e2164-302">Next steps</span></span>
<span data-ttu-id="e2164-303">Дополнительные сведения о работе с политиками см. в статье со справочными материалами по [политикам в службе управления API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="e2164-303">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  