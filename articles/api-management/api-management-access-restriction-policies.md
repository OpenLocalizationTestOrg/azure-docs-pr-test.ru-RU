---
title: "политики ограниченного использования программ для доступа к API управления aaaAzure | Документы Microsoft"
description: "Дополнительные сведения о политиках ограниченного использования программ hello доступа доступны для использования в службе управления API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 034febe3-465f-4840-9fc6-c448ef520b0f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 0ef368c2781d9a5cf9eaaa41a47489c904ed3198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-access-restriction-policies"></a><span data-ttu-id="b077e-103">Политики ограничения доступа в службе управления API</span><span class="sxs-lookup"><span data-stu-id="b077e-103">API Management access restriction policies</span></span>
<span data-ttu-id="b077e-104">Здесь вы найдете ссылку для hello следующих политиках управления интерфейсами API.</span><span class="sxs-lookup"><span data-stu-id="b077e-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="b077e-105">Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в управлении API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="b077e-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="b077e-106"><a name="AccessRestrictionPolicies"></a> Политики ограничения доступа</span><span class="sxs-lookup"><span data-stu-id="b077e-106"><a name="AccessRestrictionPolicies"></a> Access restriction policies</span></span>  
  
-   <span data-ttu-id="b077e-107">[Проверка заголовка HTTP](api-management-access-restriction-policies.md#CheckHTTPHeader) – обеспечивает принудительный ввод заголовка HTTP и/или его значения.</span><span class="sxs-lookup"><span data-stu-id="b077e-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
-   <span data-ttu-id="b077e-108">[Ограничение частоты вызовов по подписке](api-management-access-restriction-policies.md#LimitCallRate) — предотвращает пики использования API, ограничивая частоту вызовов для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="b077e-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="b077e-109">[Ограничение частоты вызовов по ключу](#LimitCallRateByKey) — предотвращает пики использования API, ограничивая частоту вызовов по ключу.</span><span class="sxs-lookup"><span data-stu-id="b077e-109">[Limit call rate by key](#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
-   <span data-ttu-id="b077e-110">[Ограничение IP-адресов вызывающих объектов](api-management-access-restriction-policies.md#RestrictCallerIPs) – фильтрует (разрешает или запрещает) вызовы с конкретных IP-адресов и/или диапазонов адресов.</span><span class="sxs-lookup"><span data-stu-id="b077e-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
-   <span data-ttu-id="b077e-111">[Задание квоты использования по подписке](api-management-access-restriction-policies.md#SetUsageQuota) -позволяет tooenforce задание продлеваемой или бессрочной квоты объема вызовов или полосы пропускания, для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="b077e-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="b077e-112">[Задание квоты использования ключом](#SetUsageQuotaByKey) -позволяет tooenforce задание продлеваемой или бессрочной квоты объема вызовов или полосы пропускания, на основе каждого ключа.</span><span class="sxs-lookup"><span data-stu-id="b077e-112">[Set usage quota by key](#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
-   <span data-ttu-id="b077e-113">[Проверка JWT](api-management-access-restriction-policies.md#ValidateJWT) – обеспечивает принудительное задание и проверку JWT, извлеченного из заданного заголовка HTTP или параметра запроса.</span><span class="sxs-lookup"><span data-stu-id="b077e-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
##  <span data-ttu-id="b077e-114"><a name="CheckHTTPHeader"></a> Проверка заголовка HTTP</span><span class="sxs-lookup"><span data-stu-id="b077e-114"><a name="CheckHTTPHeader"></a> Check HTTP header</span></span>  
 <span data-ttu-id="b077e-115">Используйте hello `check-header` tooenforce политики, что запрос содержит указанный заголовок HTTP.</span><span class="sxs-lookup"><span data-stu-id="b077e-115">Use hello `check-header` policy tooenforce that a request has a specified HTTP header.</span></span> <span data-ttu-id="b077e-116">При необходимости можно было проверить toosee Если заголовок hello имеет определенное значение или диапазону допустимых значений.</span><span class="sxs-lookup"><span data-stu-id="b077e-116">You can optionally check toosee if hello header has a specific value or check for a range of allowed values.</span></span> <span data-ttu-id="b077e-117">При невозможности проверки hello hello политики обработка запроса прекращается и возвращает hello HTTP состояние код и сообщение об ошибке указано политикой hello.</span><span class="sxs-lookup"><span data-stu-id="b077e-117">If hello check fails, hello policy terminates request processing and returns hello HTTP status code and error message specified by hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b077e-118">Правило политики</span><span class="sxs-lookup"><span data-stu-id="b077e-118">Policy statement</span></span>  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a><span data-ttu-id="b077e-119">Пример</span><span class="sxs-lookup"><span data-stu-id="b077e-119">Example</span></span>  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a><span data-ttu-id="b077e-120">Элементы</span><span class="sxs-lookup"><span data-stu-id="b077e-120">Elements</span></span>  
  
|<span data-ttu-id="b077e-121">Имя</span><span class="sxs-lookup"><span data-stu-id="b077e-121">Name</span></span>|<span data-ttu-id="b077e-122">Описание</span><span class="sxs-lookup"><span data-stu-id="b077e-122">Description</span></span>|<span data-ttu-id="b077e-123">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b077e-123">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b077e-124">check-header</span><span class="sxs-lookup"><span data-stu-id="b077e-124">check-header</span></span>|<span data-ttu-id="b077e-125">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="b077e-125">Root element.</span></span>|<span data-ttu-id="b077e-126">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-126">Yes</span></span>|  
|<span data-ttu-id="b077e-127">значение</span><span class="sxs-lookup"><span data-stu-id="b077e-127">value</span></span>|<span data-ttu-id="b077e-128">Допустимое значение заголовка HTTP.</span><span class="sxs-lookup"><span data-stu-id="b077e-128">Allowed HTTP header value.</span></span> <span data-ttu-id="b077e-129">Если указаны элементы с несколькими значениями, hello проверка считается успешно, если один из значения hello соответствие.</span><span class="sxs-lookup"><span data-stu-id="b077e-129">When multiple value elements are specified, hello check is considered a success if any one of hello values is a match.</span></span>|<span data-ttu-id="b077e-130">Нет</span><span class="sxs-lookup"><span data-stu-id="b077e-130">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="b077e-131">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="b077e-131">Attributes</span></span>  
  
|<span data-ttu-id="b077e-132">Имя</span><span class="sxs-lookup"><span data-stu-id="b077e-132">Name</span></span>|<span data-ttu-id="b077e-133">Описание</span><span class="sxs-lookup"><span data-stu-id="b077e-133">Description</span></span>|<span data-ttu-id="b077e-134">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b077e-134">Required</span></span>|<span data-ttu-id="b077e-135">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="b077e-135">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b077e-136">failed-check-error-message</span><span class="sxs-lookup"><span data-stu-id="b077e-136">failed-check-error-message</span></span>|<span data-ttu-id="b077e-137">Ошибка tooreturn сообщений в текст ответа hello HTTP, если hello заголовок не существует или имеет недопустимое значение.</span><span class="sxs-lookup"><span data-stu-id="b077e-137">Error message tooreturn in hello HTTP response body if hello header doesn't exist or has an invalid value.</span></span> <span data-ttu-id="b077e-138">Это сообщение должно содержать правильно экранированные специальные символы.</span><span class="sxs-lookup"><span data-stu-id="b077e-138">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="b077e-139">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-139">Yes</span></span>|<span data-ttu-id="b077e-140">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-140">N/A</span></span>|  
|<span data-ttu-id="b077e-141">failed-check-httpcode</span><span class="sxs-lookup"><span data-stu-id="b077e-141">failed-check-httpcode</span></span>|<span data-ttu-id="b077e-142">Tooreturn код состояния HTTP, если hello заголовок не существует или имеет недопустимое значение.</span><span class="sxs-lookup"><span data-stu-id="b077e-142">HTTP Status code tooreturn if hello header doesn't exist or has an invalid value.</span></span>|<span data-ttu-id="b077e-143">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-143">Yes</span></span>|<span data-ttu-id="b077e-144">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-144">N/A</span></span>|  
|<span data-ttu-id="b077e-145">header-name</span><span class="sxs-lookup"><span data-stu-id="b077e-145">header-name</span></span>|<span data-ttu-id="b077e-146">Имя Hello hello toocheck заголовка HTTP.</span><span class="sxs-lookup"><span data-stu-id="b077e-146">hello name of hello HTTP Header toocheck.</span></span>|<span data-ttu-id="b077e-147">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-147">Yes</span></span>|<span data-ttu-id="b077e-148">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-148">N/A</span></span>|  
|<span data-ttu-id="b077e-149">ignore-case</span><span class="sxs-lookup"><span data-stu-id="b077e-149">ignore-case</span></span>|<span data-ttu-id="b077e-150">Можно задать tooTrue или False.</span><span class="sxs-lookup"><span data-stu-id="b077e-150">Can be set tooTrue or False.</span></span> <span data-ttu-id="b077e-151">Если набор tooTrue регистр учитывается, если значение заголовка hello сравнивается hello набором допустимых значений.</span><span class="sxs-lookup"><span data-stu-id="b077e-151">If set tooTrue case is ignored when hello header value is compared against hello set of acceptable values.</span></span>|<span data-ttu-id="b077e-152">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-152">Yes</span></span>|<span data-ttu-id="b077e-153">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-153">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b077e-154">Использование</span><span class="sxs-lookup"><span data-stu-id="b077e-154">Usage</span></span>  
 <span data-ttu-id="b077e-155">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="b077e-155">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b077e-156">**Разделы политики:** inbound, outbound.</span><span class="sxs-lookup"><span data-stu-id="b077e-156">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="b077e-157">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="b077e-157">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="b077e-158"><a name="LimitCallRate"></a> Ограничение частоты вызовов по подписке</span><span class="sxs-lookup"><span data-stu-id="b077e-158"><a name="LimitCallRate"></a> Limit call rate by subscription</span></span>  
 <span data-ttu-id="b077e-159">Hello `rate-limit` политики предотвращает использование API пики на основе каждой подписки, ограничивая hello вызвать указанный tooa скорость номеров за указанный период времени.</span><span class="sxs-lookup"><span data-stu-id="b077e-159">hello `rate-limit` policy prevents API usage spikes on a per subscription basis by limiting hello call rate tooa specified number per a specified time period.</span></span> <span data-ttu-id="b077e-160">При запуске этой политики вызывающий объект hello получает `429 Too Many Requests` код состояния ответа.</span><span class="sxs-lookup"><span data-stu-id="b077e-160">When this policy is triggered hello caller receives a `429 Too Many Requests` response status code.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="b077e-161">Эту политику можно использовать для каждого документа политики только один раз.</span><span class="sxs-lookup"><span data-stu-id="b077e-161">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="b077e-162">[Выражения политики](api-management-policy-expressions.md) не может использоваться в атрибутах hello политики для этой политики.</span><span class="sxs-lookup"><span data-stu-id="b077e-162">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b077e-163">Правило политики</span><span class="sxs-lookup"><span data-stu-id="b077e-163">Policy statement</span></span>  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a><span data-ttu-id="b077e-164">Пример</span><span class="sxs-lookup"><span data-stu-id="b077e-164">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit calls="20" renewal-period="90" />  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="b077e-165">Элементы</span><span class="sxs-lookup"><span data-stu-id="b077e-165">Elements</span></span>  
  
|<span data-ttu-id="b077e-166">Имя</span><span class="sxs-lookup"><span data-stu-id="b077e-166">Name</span></span>|<span data-ttu-id="b077e-167">Описание</span><span class="sxs-lookup"><span data-stu-id="b077e-167">Description</span></span>|<span data-ttu-id="b077e-168">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b077e-168">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b077e-169">set-limit</span><span class="sxs-lookup"><span data-stu-id="b077e-169">set-limit</span></span>|<span data-ttu-id="b077e-170">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="b077e-170">Root element.</span></span>|<span data-ttu-id="b077e-171">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-171">Yes</span></span>|  
|<span data-ttu-id="b077e-172">api</span><span class="sxs-lookup"><span data-stu-id="b077e-172">api</span></span>|<span data-ttu-id="b077e-173">Добавьте один или несколько из этих элементов tooimpose ограничение частоты вызовов по интерфейсам API в пределах продукта hello.</span><span class="sxs-lookup"><span data-stu-id="b077e-173">Add one  or more of these elements tooimpose a call rate limit on APIs within hello product.</span></span> <span data-ttu-id="b077e-174">Ограничения частоты вызовов продукта и API применяются раздельно.</span><span class="sxs-lookup"><span data-stu-id="b077e-174">Product and API call rate limits are applied independently.</span></span>|<span data-ttu-id="b077e-175">Нет</span><span class="sxs-lookup"><span data-stu-id="b077e-175">No</span></span>|  
|<span data-ttu-id="b077e-176">операция</span><span class="sxs-lookup"><span data-stu-id="b077e-176">operation</span></span>|<span data-ttu-id="b077e-177">Добавьте один или несколько из этих элементов tooimpose ограничение частоты вызовов операций в пределах интерфейса API.</span><span class="sxs-lookup"><span data-stu-id="b077e-177">Add one  or more of these elements tooimpose a call rate limit on operations within an API.</span></span> <span data-ttu-id="b077e-178">Ограничения частоты вызовов продукта, API и операции применяются раздельно.</span><span class="sxs-lookup"><span data-stu-id="b077e-178">Product, API, and operation call rate limits are applied independently.</span></span>|<span data-ttu-id="b077e-179">Нет</span><span class="sxs-lookup"><span data-stu-id="b077e-179">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="b077e-180">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="b077e-180">Attributes</span></span>  
  
|<span data-ttu-id="b077e-181">Имя</span><span class="sxs-lookup"><span data-stu-id="b077e-181">Name</span></span>|<span data-ttu-id="b077e-182">Описание</span><span class="sxs-lookup"><span data-stu-id="b077e-182">Description</span></span>|<span data-ttu-id="b077e-183">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b077e-183">Required</span></span>|<span data-ttu-id="b077e-184">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="b077e-184">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b077e-185">name</span><span class="sxs-lookup"><span data-stu-id="b077e-185">name</span></span>|<span data-ttu-id="b077e-186">Hello имя hello API какие ограничение частоты tooapply hello.</span><span class="sxs-lookup"><span data-stu-id="b077e-186">hello name of hello API for which tooapply hello rate limit.</span></span>|<span data-ttu-id="b077e-187">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-187">Yes</span></span>|<span data-ttu-id="b077e-188">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-188">N/A</span></span>|  
|<span data-ttu-id="b077e-189">calls</span><span class="sxs-lookup"><span data-stu-id="b077e-189">calls</span></span>|<span data-ttu-id="b077e-190">Здравствуйте, максимальное общее число вызовов, допускается hello временной интервал, указанный в hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="b077e-190">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="b077e-191">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-191">Yes</span></span>|<span data-ttu-id="b077e-192">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-192">N/A</span></span>|  
|<span data-ttu-id="b077e-193">renewal-period</span><span class="sxs-lookup"><span data-stu-id="b077e-193">renewal-period</span></span>|<span data-ttu-id="b077e-194">Здравствуйте, период времени в секундах, после которого hello сброса квоты.</span><span class="sxs-lookup"><span data-stu-id="b077e-194">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="b077e-195">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-195">Yes</span></span>|<span data-ttu-id="b077e-196">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-196">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b077e-197">Использование</span><span class="sxs-lookup"><span data-stu-id="b077e-197">Usage</span></span>  
 <span data-ttu-id="b077e-198">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="b077e-198">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b077e-199">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="b077e-199">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="b077e-200">**Области политики:** product.</span><span class="sxs-lookup"><span data-stu-id="b077e-200">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="b077e-201"><a name="LimitCallRateByKey"></a> Ограничение частоты вызовов по ключу</span><span class="sxs-lookup"><span data-stu-id="b077e-201"><a name="LimitCallRateByKey"></a> Limit call rate by key</span></span>  
 <span data-ttu-id="b077e-202">Hello `rate-limit-by-key` политики предотвращает использование API пики на основе каждого ключа, ограничивая hello вызвать указанный tooa скорость номеров за указанный период времени.</span><span class="sxs-lookup"><span data-stu-id="b077e-202">hello `rate-limit-by-key` policy prevents API usage spikes on a per key basis by limiting hello call rate tooa specified number per a specified time period.</span></span> <span data-ttu-id="b077e-203">ключ Hello может иметь произвольное строковое значение и обычно обеспечивается с помощью выражения политики.</span><span class="sxs-lookup"><span data-stu-id="b077e-203">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="b077e-204">Необязательный шаг условия могут быть добавлены toospecify, какие запросы должны быть подсчитаны расчете предельного числа hello.</span><span class="sxs-lookup"><span data-stu-id="b077e-204">Optional increment condition can be added toospecify which requests should be counted towards hello limit.</span></span> <span data-ttu-id="b077e-205">При запуске этой политики вызывающий объект hello получает `429 Too Many Requests` код состояния ответа.</span><span class="sxs-lookup"><span data-stu-id="b077e-205">When this policy is triggered hello caller receives a `429 Too Many Requests` response status code.</span></span>  
  
 <span data-ttu-id="b077e-206">Дополнительные сведения и примеры этой политики см. в статье [Расширенное регулирование запросов с помощью управления API](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="b077e-206">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="b077e-207">Эту политику можно использовать для каждого документа политики только один раз.</span><span class="sxs-lookup"><span data-stu-id="b077e-207">This policy can be used only once per policy document.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b077e-208">Правило политики</span><span class="sxs-lookup"><span data-stu-id="b077e-208">Policy statement</span></span>  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="b077e-209">Пример</span><span class="sxs-lookup"><span data-stu-id="b077e-209">Example</span></span>  
 <span data-ttu-id="b077e-210">В следующем примере hello ограничение частоты hello шифруется по IP-адресу hello вызывающего объекта.</span><span class="sxs-lookup"><span data-stu-id="b077e-210">In hello following example, hello rate limit is keyed by hello caller IP address.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit-by-key  calls="10"  
              renewal-period="60"  
              increment-condition="@(context.Response.StatusCode == 200)"  
              counter-key="@(context.Request.IpAddress)"/>  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="b077e-211">Элементы</span><span class="sxs-lookup"><span data-stu-id="b077e-211">Elements</span></span>  
  
|<span data-ttu-id="b077e-212">Имя</span><span class="sxs-lookup"><span data-stu-id="b077e-212">Name</span></span>|<span data-ttu-id="b077e-213">Описание</span><span class="sxs-lookup"><span data-stu-id="b077e-213">Description</span></span>|<span data-ttu-id="b077e-214">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b077e-214">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b077e-215">set-limit</span><span class="sxs-lookup"><span data-stu-id="b077e-215">set-limit</span></span>|<span data-ttu-id="b077e-216">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="b077e-216">Root element.</span></span>|<span data-ttu-id="b077e-217">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-217">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="b077e-218">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="b077e-218">Attributes</span></span>  
  
|<span data-ttu-id="b077e-219">Имя</span><span class="sxs-lookup"><span data-stu-id="b077e-219">Name</span></span>|<span data-ttu-id="b077e-220">Описание</span><span class="sxs-lookup"><span data-stu-id="b077e-220">Description</span></span>|<span data-ttu-id="b077e-221">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b077e-221">Required</span></span>|<span data-ttu-id="b077e-222">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="b077e-222">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b077e-223">calls</span><span class="sxs-lookup"><span data-stu-id="b077e-223">calls</span></span>|<span data-ttu-id="b077e-224">Здравствуйте, максимальное общее число вызовов, допускается hello временной интервал, указанный в hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="b077e-224">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="b077e-225">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-225">Yes</span></span>|<span data-ttu-id="b077e-226">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-226">N/A</span></span>|  
|<span data-ttu-id="b077e-227">counter-key</span><span class="sxs-lookup"><span data-stu-id="b077e-227">counter-key</span></span>|<span data-ttu-id="b077e-228">Hello ключа toouse для политики ограничения скорости hello.</span><span class="sxs-lookup"><span data-stu-id="b077e-228">hello key toouse for hello rate limit policy.</span></span>|<span data-ttu-id="b077e-229">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-229">Yes</span></span>|<span data-ttu-id="b077e-230">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-230">N/A</span></span>|  
|<span data-ttu-id="b077e-231">increment-condition</span><span class="sxs-lookup"><span data-stu-id="b077e-231">increment-condition</span></span>|<span data-ttu-id="b077e-232">Hello логическое выражение, указывающее, если запрос hello следует засчитывается квоты hello (`true`).</span><span class="sxs-lookup"><span data-stu-id="b077e-232">hello boolean expression specifying if hello request should be counted towards hello quota (`true`).</span></span>|<span data-ttu-id="b077e-233">Нет</span><span class="sxs-lookup"><span data-stu-id="b077e-233">No</span></span>|<span data-ttu-id="b077e-234">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-234">N/A</span></span>|  
|<span data-ttu-id="b077e-235">renewal-period</span><span class="sxs-lookup"><span data-stu-id="b077e-235">renewal-period</span></span>|<span data-ttu-id="b077e-236">Здравствуйте, период времени в секундах, после которого hello сброса квоты.</span><span class="sxs-lookup"><span data-stu-id="b077e-236">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="b077e-237">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-237">Yes</span></span>|<span data-ttu-id="b077e-238">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-238">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b077e-239">Использование</span><span class="sxs-lookup"><span data-stu-id="b077e-239">Usage</span></span>  
 <span data-ttu-id="b077e-240">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="b077e-240">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b077e-241">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="b077e-241">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="b077e-242">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="b077e-242">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="b077e-243"><a name="RestrictCallerIPs"></a> Ограничение IP-адресов вызывающих объектов</span><span class="sxs-lookup"><span data-stu-id="b077e-243"><a name="RestrictCallerIPs"></a> Restrict caller IPs</span></span>  
 <span data-ttu-id="b077e-244">Hello `ip-filter` политики Фильтрация (разрешение или запрет) вызовов с конкретных IP-адресов и/или диапазоны адресов.</span><span class="sxs-lookup"><span data-stu-id="b077e-244">hello `ip-filter` policy filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b077e-245">Правило политики</span><span class="sxs-lookup"><span data-stu-id="b077e-245">Policy statement</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a><span data-ttu-id="b077e-246">Пример</span><span class="sxs-lookup"><span data-stu-id="b077e-246">Example</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a><span data-ttu-id="b077e-247">Элементы</span><span class="sxs-lookup"><span data-stu-id="b077e-247">Elements</span></span>  
  
|<span data-ttu-id="b077e-248">Имя</span><span class="sxs-lookup"><span data-stu-id="b077e-248">Name</span></span>|<span data-ttu-id="b077e-249">Описание</span><span class="sxs-lookup"><span data-stu-id="b077e-249">Description</span></span>|<span data-ttu-id="b077e-250">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b077e-250">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b077e-251">ip-filter</span><span class="sxs-lookup"><span data-stu-id="b077e-251">ip-filter</span></span>|<span data-ttu-id="b077e-252">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="b077e-252">Root element.</span></span>|<span data-ttu-id="b077e-253">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-253">Yes</span></span>|  
|<span data-ttu-id="b077e-254">address</span><span class="sxs-lookup"><span data-stu-id="b077e-254">address</span></span>|<span data-ttu-id="b077e-255">Указывает один IP-адрес, на какие toofilter.</span><span class="sxs-lookup"><span data-stu-id="b077e-255">Specifies a single IP address on which toofilter.</span></span>|<span data-ttu-id="b077e-256">По крайней мере один элемент `address` или `address-range` является обязательным.</span><span class="sxs-lookup"><span data-stu-id="b077e-256">At least one `address` or `address-range` element is required.</span></span>|  
|<span data-ttu-id="b077e-257">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="b077e-257">address-range from="address" to="address"</span></span>|<span data-ttu-id="b077e-258">Указывает диапазон IP-адресов, на какие toofilter.</span><span class="sxs-lookup"><span data-stu-id="b077e-258">Specifies a range of IP address on which toofilter.</span></span>|<span data-ttu-id="b077e-259">По крайней мере один элемент `address` или `address-range` является обязательным.</span><span class="sxs-lookup"><span data-stu-id="b077e-259">At least one `address` or `address-range` element is required.</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="b077e-260">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="b077e-260">Attributes</span></span>  
  
|<span data-ttu-id="b077e-261">Имя</span><span class="sxs-lookup"><span data-stu-id="b077e-261">Name</span></span>|<span data-ttu-id="b077e-262">Описание</span><span class="sxs-lookup"><span data-stu-id="b077e-262">Description</span></span>|<span data-ttu-id="b077e-263">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b077e-263">Required</span></span>|<span data-ttu-id="b077e-264">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="b077e-264">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b077e-265">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="b077e-265">address-range from="address" to="address"</span></span>|<span data-ttu-id="b077e-266">Диапазон IP-адресов tooallow или запретить доступ.</span><span class="sxs-lookup"><span data-stu-id="b077e-266">A range of IP addresses tooallow or deny access for.</span></span>|<span data-ttu-id="b077e-267">Требуется, если hello `address-range` используется элемент.</span><span class="sxs-lookup"><span data-stu-id="b077e-267">Required when hello `address-range` element is used.</span></span>|<span data-ttu-id="b077e-268">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-268">N/A</span></span>|  
|<span data-ttu-id="b077e-269">ip-filter action="allow &#124; forbid"</span><span class="sxs-lookup"><span data-stu-id="b077e-269">ip-filter action="allow &#124; forbid"</span></span>|<span data-ttu-id="b077e-270">Определяет, следует разрешить вызовы или не для hello указан IP-адреса и диапазоны.</span><span class="sxs-lookup"><span data-stu-id="b077e-270">Specifies whether calls should be allowed or not for hello specified IP addresses and ranges.</span></span>|<span data-ttu-id="b077e-271">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-271">Yes</span></span>|<span data-ttu-id="b077e-272">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b077e-273">Использование</span><span class="sxs-lookup"><span data-stu-id="b077e-273">Usage</span></span>  
 <span data-ttu-id="b077e-274">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="b077e-274">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b077e-275">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="b077e-275">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="b077e-276">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="b077e-276">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="b077e-277"><a name="SetUsageQuota"></a> Задание квоты использования по подписке</span><span class="sxs-lookup"><span data-stu-id="b077e-277"><a name="SetUsageQuota"></a> Set usage quota by subscription</span></span>  
 <span data-ttu-id="b077e-278">Hello `quota` политика принудительно применяет задание продлеваемой или бессрочной квоты объема вызовов или полосы пропускания, для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="b077e-278">hello `quota` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="b077e-279">Эту политику можно использовать для каждого документа политики только один раз.</span><span class="sxs-lookup"><span data-stu-id="b077e-279">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="b077e-280">[Выражения политики](api-management-policy-expressions.md) не может использоваться в атрибутах hello политики для этой политики.</span><span class="sxs-lookup"><span data-stu-id="b077e-280">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b077e-281">Правило политики</span><span class="sxs-lookup"><span data-stu-id="b077e-281">Policy statement</span></span>  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a><span data-ttu-id="b077e-282">Пример</span><span class="sxs-lookup"><span data-stu-id="b077e-282">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota calls="10000" bandwidth="40000" renewal-period="3600" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="b077e-283">Элементы</span><span class="sxs-lookup"><span data-stu-id="b077e-283">Elements</span></span>  
  
|<span data-ttu-id="b077e-284">Имя</span><span class="sxs-lookup"><span data-stu-id="b077e-284">Name</span></span>|<span data-ttu-id="b077e-285">Описание</span><span class="sxs-lookup"><span data-stu-id="b077e-285">Description</span></span>|<span data-ttu-id="b077e-286">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b077e-286">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b077e-287">quota</span><span class="sxs-lookup"><span data-stu-id="b077e-287">quota</span></span>|<span data-ttu-id="b077e-288">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="b077e-288">Root element.</span></span>|<span data-ttu-id="b077e-289">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-289">Yes</span></span>|  
|<span data-ttu-id="b077e-290">api</span><span class="sxs-lookup"><span data-stu-id="b077e-290">api</span></span>|<span data-ttu-id="b077e-291">Добавьте один или несколько из этих элементов tooimpose квоты на интерфейсы API в пределах продукта hello.</span><span class="sxs-lookup"><span data-stu-id="b077e-291">Add one  or more of these elements tooimpose a quota on APIs within hello product.</span></span> <span data-ttu-id="b077e-292">Квоты продукта и API применяются раздельно.</span><span class="sxs-lookup"><span data-stu-id="b077e-292">Product and API quotas are applied independently.</span></span>|<span data-ttu-id="b077e-293">Нет</span><span class="sxs-lookup"><span data-stu-id="b077e-293">No</span></span>|  
|<span data-ttu-id="b077e-294">операция</span><span class="sxs-lookup"><span data-stu-id="b077e-294">operation</span></span>|<span data-ttu-id="b077e-295">Добавьте один или несколько из этих элементов tooimpose квоты на операции в пределах интерфейса API.</span><span class="sxs-lookup"><span data-stu-id="b077e-295">Add one  or more of these elements tooimpose a quota on operations within an API.</span></span> <span data-ttu-id="b077e-296">Квоты продукта, API и операции применяются раздельно.</span><span class="sxs-lookup"><span data-stu-id="b077e-296">Product, API, and operation quotas are applied independently.</span></span>|<span data-ttu-id="b077e-297">Нет</span><span class="sxs-lookup"><span data-stu-id="b077e-297">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="b077e-298">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="b077e-298">Attributes</span></span>  
  
|<span data-ttu-id="b077e-299">Имя</span><span class="sxs-lookup"><span data-stu-id="b077e-299">Name</span></span>|<span data-ttu-id="b077e-300">Описание</span><span class="sxs-lookup"><span data-stu-id="b077e-300">Description</span></span>|<span data-ttu-id="b077e-301">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b077e-301">Required</span></span>|<span data-ttu-id="b077e-302">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="b077e-302">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b077e-303">name</span><span class="sxs-lookup"><span data-stu-id="b077e-303">name</span></span>|<span data-ttu-id="b077e-304">Имя Hello hello API или операция, для которых hello применяется Квота.</span><span class="sxs-lookup"><span data-stu-id="b077e-304">hello name of hello API or operation for which hello quota applies.</span></span>|<span data-ttu-id="b077e-305">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-305">Yes</span></span>|<span data-ttu-id="b077e-306">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-306">N/A</span></span>|  
|<span data-ttu-id="b077e-307">bandwidth</span><span class="sxs-lookup"><span data-stu-id="b077e-307">bandwidth</span></span>|<span data-ttu-id="b077e-308">Здравствуйте, максимальное общее число килобайт допускается hello временной интервал, указанный в hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="b077e-308">hello maximum total number of kilobytes allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="b077e-309">Необходимо указать атрибут `calls`, `bandwidth` или оба вместе.</span><span class="sxs-lookup"><span data-stu-id="b077e-309">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="b077e-310">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-310">N/A</span></span>|  
|<span data-ttu-id="b077e-311">calls</span><span class="sxs-lookup"><span data-stu-id="b077e-311">calls</span></span>|<span data-ttu-id="b077e-312">Здравствуйте, максимальное общее число вызовов, допускается hello временной интервал, указанный в hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="b077e-312">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="b077e-313">Необходимо указать атрибут `calls`, `bandwidth` или оба вместе.</span><span class="sxs-lookup"><span data-stu-id="b077e-313">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="b077e-314">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-314">N/A</span></span>|  
|<span data-ttu-id="b077e-315">renewal-period</span><span class="sxs-lookup"><span data-stu-id="b077e-315">renewal-period</span></span>|<span data-ttu-id="b077e-316">Здравствуйте, период времени в секундах, после которого hello сброса квоты.</span><span class="sxs-lookup"><span data-stu-id="b077e-316">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="b077e-317">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-317">Yes</span></span>|<span data-ttu-id="b077e-318">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-318">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b077e-319">Использование</span><span class="sxs-lookup"><span data-stu-id="b077e-319">Usage</span></span>  
 <span data-ttu-id="b077e-320">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="b077e-320">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b077e-321">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="b077e-321">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="b077e-322">**Области политики:** product.</span><span class="sxs-lookup"><span data-stu-id="b077e-322">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="b077e-323"><a name="SetUsageQuotaByKey"></a> Задание квоты использования по ключу</span><span class="sxs-lookup"><span data-stu-id="b077e-323"><a name="SetUsageQuotaByKey"></a> Set usage quota by key</span></span>  
 <span data-ttu-id="b077e-324">Hello `quota-by-key` политика принудительно применяет задание продлеваемой или бессрочной квоты объема вызовов или полосы пропускания, на основе каждого ключа.</span><span class="sxs-lookup"><span data-stu-id="b077e-324">hello `quota-by-key` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span> <span data-ttu-id="b077e-325">ключ Hello может иметь произвольное строковое значение и обычно обеспечивается с помощью выражения политики.</span><span class="sxs-lookup"><span data-stu-id="b077e-325">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="b077e-326">Необязательный шаг условия могут быть добавлены toospecify, какие запросы должны быть засчитывается hello квоты.</span><span class="sxs-lookup"><span data-stu-id="b077e-326">Optional increment condition can be added toospecify which requests should be counted towards hello quota.</span></span>  
  
 <span data-ttu-id="b077e-327">Дополнительные сведения и примеры этой политики см. в статье [Расширенное регулирование запросов с помощью управления API](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="b077e-327">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="b077e-328">Эту политику можно использовать для каждого документа политики только один раз.</span><span class="sxs-lookup"><span data-stu-id="b077e-328">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="b077e-329">[Выражения политики](api-management-policy-expressions.md) не может использоваться в атрибутах hello политики для этой политики.</span><span class="sxs-lookup"><span data-stu-id="b077e-329">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b077e-330">Правило политики</span><span class="sxs-lookup"><span data-stu-id="b077e-330">Policy statement</span></span>  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="b077e-331">Пример</span><span class="sxs-lookup"><span data-stu-id="b077e-331">Example</span></span>  
 <span data-ttu-id="b077e-332">В следующем примере hello Квота hello шифруется по IP-адресу hello вызывающего объекта.</span><span class="sxs-lookup"><span data-stu-id="b077e-332">In hello following example, hello quota is keyed by hello caller IP address.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota-by-key calls="10000" bandwidth="40000" renewal-period="3600"  
                      increment-condition="@(context.Response.StatusCode >= 200 && context.Response.StatusCode < 400)"  
                      counter-key="@(context.Request.IpAddress)" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="b077e-333">Элементы</span><span class="sxs-lookup"><span data-stu-id="b077e-333">Elements</span></span>  
  
|<span data-ttu-id="b077e-334">Имя</span><span class="sxs-lookup"><span data-stu-id="b077e-334">Name</span></span>|<span data-ttu-id="b077e-335">Описание</span><span class="sxs-lookup"><span data-stu-id="b077e-335">Description</span></span>|<span data-ttu-id="b077e-336">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b077e-336">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="b077e-337">quota</span><span class="sxs-lookup"><span data-stu-id="b077e-337">quota</span></span>|<span data-ttu-id="b077e-338">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="b077e-338">Root element.</span></span>|<span data-ttu-id="b077e-339">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-339">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="b077e-340">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="b077e-340">Attributes</span></span>  
  
|<span data-ttu-id="b077e-341">Имя</span><span class="sxs-lookup"><span data-stu-id="b077e-341">Name</span></span>|<span data-ttu-id="b077e-342">Описание</span><span class="sxs-lookup"><span data-stu-id="b077e-342">Description</span></span>|<span data-ttu-id="b077e-343">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b077e-343">Required</span></span>|<span data-ttu-id="b077e-344">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="b077e-344">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b077e-345">bandwidth</span><span class="sxs-lookup"><span data-stu-id="b077e-345">bandwidth</span></span>|<span data-ttu-id="b077e-346">Здравствуйте, максимальное общее число килобайт допускается hello временной интервал, указанный в hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="b077e-346">hello maximum total number of kilobytes allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="b077e-347">Необходимо указать атрибут `calls`, `bandwidth` или оба вместе.</span><span class="sxs-lookup"><span data-stu-id="b077e-347">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="b077e-348">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-348">N/A</span></span>|  
|<span data-ttu-id="b077e-349">calls</span><span class="sxs-lookup"><span data-stu-id="b077e-349">calls</span></span>|<span data-ttu-id="b077e-350">Здравствуйте, максимальное общее число вызовов, допускается hello временной интервал, указанный в hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="b077e-350">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="b077e-351">Необходимо указать атрибут `calls`, `bandwidth` или оба вместе.</span><span class="sxs-lookup"><span data-stu-id="b077e-351">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="b077e-352">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-352">N/A</span></span>|  
|<span data-ttu-id="b077e-353">counter-key</span><span class="sxs-lookup"><span data-stu-id="b077e-353">counter-key</span></span>|<span data-ttu-id="b077e-354">Hello ключа toouse политики квоты hello.</span><span class="sxs-lookup"><span data-stu-id="b077e-354">hello key toouse for hello quota policy.</span></span>|<span data-ttu-id="b077e-355">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-355">Yes</span></span>|<span data-ttu-id="b077e-356">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-356">N/A</span></span>|  
|<span data-ttu-id="b077e-357">increment-condition</span><span class="sxs-lookup"><span data-stu-id="b077e-357">increment-condition</span></span>|<span data-ttu-id="b077e-358">Hello логическое выражение, указывающее, если запрос hello следует засчитывается квоты hello (`true`)</span><span class="sxs-lookup"><span data-stu-id="b077e-358">hello boolean expression specifying if hello request should be counted towards hello quota (`true`)</span></span>|<span data-ttu-id="b077e-359">Нет</span><span class="sxs-lookup"><span data-stu-id="b077e-359">No</span></span>|<span data-ttu-id="b077e-360">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-360">N/A</span></span>|  
|<span data-ttu-id="b077e-361">renewal-period</span><span class="sxs-lookup"><span data-stu-id="b077e-361">renewal-period</span></span>|<span data-ttu-id="b077e-362">Здравствуйте, период времени в секундах, после которого hello сброса квоты.</span><span class="sxs-lookup"><span data-stu-id="b077e-362">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="b077e-363">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-363">Yes</span></span>|<span data-ttu-id="b077e-364">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-364">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b077e-365">Использование</span><span class="sxs-lookup"><span data-stu-id="b077e-365">Usage</span></span>  
 <span data-ttu-id="b077e-366">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="b077e-366">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b077e-367">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="b077e-367">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="b077e-368">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="b077e-368">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="b077e-369"><a name="ValidateJWT"></a> Проверка JWT</span><span class="sxs-lookup"><span data-stu-id="b077e-369"><a name="ValidateJWT"></a> Validate JWT</span></span>  
 <span data-ttu-id="b077e-370">Hello `validate-jwt` политика обеспечивает существование и подтверждение JWT, извлеченных из любого указанного заголовка HTTP или параметра запроса.</span><span class="sxs-lookup"><span data-stu-id="b077e-370">hello `validate-jwt` policy enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="b077e-371">Hello `validate-jwt` политика требует этого hello `exp` зарегистрированных утверждений является включено в токене JWT hello, за исключением случаев `require-expiration-time` атрибут задан и имеет слишком`false`.</span><span class="sxs-lookup"><span data-stu-id="b077e-371">hello `validate-jwt` policy requires that hello `exp` registered claim is inlcuded in hello JWT token, unless `require-expiration-time` attribute is specified and set too`false`.</span></span>  
> <span data-ttu-id="b077e-372">Hello `validate-jwt` политики поддерживает HS256 и RS256 алгоритма подписи.</span><span class="sxs-lookup"><span data-stu-id="b077e-372">hello `validate-jwt` policy supports HS256 and RS256 signing algorithms.</span></span> <span data-ttu-id="b077e-373">HS256 hello ключа необходимо указать встроенный в политике hello в форме hello в кодировке base64.</span><span class="sxs-lookup"><span data-stu-id="b077e-373">For HS256 hello key must be provided inline within hello policy in hello base64 encoded form.</span></span> <span data-ttu-id="b077e-374">Для RS256 hello ключ имеет toobe предоставляете посредством конечной точки конфигурации Open ID.</span><span class="sxs-lookup"><span data-stu-id="b077e-374">For RS256 hello key has toobe provide via an Open ID configuration endpoint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="b077e-375">Правило политики</span><span class="sxs-lookup"><span data-stu-id="b077e-375">Policy statement</span></span>  
  
```xml  
<validate-jwt   
    header-name="name of http header containing hello token (use query-parameter-name attribute if hello token is passed in hello URL)"   
    failed-validation-httpcode="http status code tooreturn on failure"   
    failed-validation-error-message="error message tooreturn on failure"   
    require-expiration-time="true|false"
    require-scheme="scheme"
    require-signed-tokens="true|false"   
    clock-skew="allowed clock skew in seconds">  
  <issuer-signing-keys>  
    <key>base64 encoded signing key</key>  
    <!-- if there are multiple keys, then add additional key elements -->  
  </issuer-signing-keys>  
  <audiences>  
    <audience>audience string</audience>  
    <!-- if there are multiple possible audiences, then add additional audience elements -->  
  </audiences>  
  <issuers>  
    <issuer>issuer string</issuer>  
    <!-- if there are multiple possible issuers, then add additional issuer elements -->  
  </issuers>  
  <required-claims>  
    <claim name="name of hello claim as it appears in hello token" match="all|any">  
      <value>claim value as it is expected tooappear in hello token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of hello configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="b077e-376">Примеры</span><span class="sxs-lookup"><span data-stu-id="b077e-376">Examples</span></span>  
  
#### <a name="azure-mobile-services-token-validation"></a><span data-ttu-id="b077e-377">Проверка маркеров мобильных служб Azure</span><span class="sxs-lookup"><span data-stu-id="b077e-377">Azure Mobile Services token validation</span></span>  
  
```xml  
<validate-jwt header-name="x-zumo-auth" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Supplied access token is invalid.">  
    <issuers>  
        <issuer>urn:microsoft:windows-azure:zumo</issuer>  
    </issuers>  
    <audiences>  
        <audience>Facebook</audience>  
    </audiences>  
    <issuer-signing-keys>  
        <zumo-master-key id="0">insert key here</zumo-master-key>  
    </issuer-signing-keys>  
</validate-jwt>  
```  
  
#### <a name="azure-active-directory-token-validation"></a><span data-ttu-id="b077e-378">Проверка маркеров Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b077e-378">Azure Active Directory token validation</span></span>  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration" />  
    <audiences>
        <audience>25eef6e4-c905-4a07-8eb4-0d08d5df8b3f</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  

  
#### <a name="azure-active-directory-b2c-token-validation"></a><span data-ttu-id="b077e-379">Проверка токена Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="b077e-379">Azure Active Directory B2C token validation</span></span>  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/tfp/contoso.onmicrosoft.com/b2c_1_signin/v2.0/.well-known/openid-configuration" />
    <audiences>
        <audience>d313c4e4-de5f-4197-9470-e509a2f0b806</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  
  
#### <a name="authorize-access-toooperations-based-on-token-claims"></a><span data-ttu-id="b077e-380">Авторизовать toooperations доступа на основе маркеров утверждений</span><span class="sxs-lookup"><span data-stu-id="b077e-380">Authorize access toooperations based on token claims</span></span>  
 <span data-ttu-id="b077e-381">В этом примере показано, как toouse hello [проверка JWT](api-management-access-restriction-policies.md#ValidateJWT) toopre политики-авторизовать toooperations доступа на основе маркеров утверждений.</span><span class="sxs-lookup"><span data-stu-id="b077e-381">This example shows how toouse hello [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy toopre-authorize access toooperations based on token claims.</span></span> <span data-ttu-id="b077e-382">Демонстрацию настройке и использовании этой политики см. в разделе [177 серии охватывают облачные: более возможности API управления с помощью Влад Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) и too13:50 Перемотка вперед.</span><span class="sxs-lookup"><span data-stu-id="b077e-382">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too13:50.</span></span> <span data-ttu-id="b077e-383">Перемотка вперед too15:00 toosee hello политики, настроенные в редакторе hello политики и затем too18:50 демонстрацию вызова операции из портала разработчиков hello как с и без hello требуется маркер авторизации.</span><span class="sxs-lookup"><span data-stu-id="b077e-383">Fast forward too15:00 toosee hello policies configured in hello policy editor and then too18:50 for a demonstration of calling an operation from hello developer portal both with and without hello required authorization token.</span></span>  
  
```xml  
<!-- Copy hello following snippet into hello inbound section at hello api (or higher) level toopre-authorize access toooperations based on token claims -->  
<set-variable name="signingKey" value="insert signing key here" />  
<choose>  
  <when condition="@(context.Request.Method.Equals("patch",StringComparison.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="edit">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <when condition="@(new [] {"post", "put"}.Contains(context.Request.Method,StringComparer.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="create">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <otherwise>  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
    </validate-jwt>  
  </otherwise>  
</choose>  
```  
  
### <a name="elements"></a><span data-ttu-id="b077e-384">Элементы</span><span class="sxs-lookup"><span data-stu-id="b077e-384">Elements</span></span>  
  
|<span data-ttu-id="b077e-385">Элемент</span><span class="sxs-lookup"><span data-stu-id="b077e-385">Element</span></span>|<span data-ttu-id="b077e-386">Описание</span><span class="sxs-lookup"><span data-stu-id="b077e-386">Description</span></span>|<span data-ttu-id="b077e-387">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b077e-387">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="b077e-388">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="b077e-388">validate-jwt</span></span>|<span data-ttu-id="b077e-389">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="b077e-389">Root element.</span></span>|<span data-ttu-id="b077e-390">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-390">Yes</span></span>|  
|<span data-ttu-id="b077e-391">audiences</span><span class="sxs-lookup"><span data-stu-id="b077e-391">audiences</span></span>|<span data-ttu-id="b077e-392">Содержит список допустимых заявок audience, могут быть представлены на маркер hello.</span><span class="sxs-lookup"><span data-stu-id="b077e-392">Contains a list of acceptable audience claims that can be present on hello token.</span></span> <span data-ttu-id="b077e-393">При наличии нескольких значений audience каждое значение проверяется либо до их исчерпания (в этом случае проверка будет не пройдена), либо до обнаружения подходящего значения.</span><span class="sxs-lookup"><span data-stu-id="b077e-393">If multiple audience values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span> <span data-ttu-id="b077e-394">Необходимо указать по крайней мере один элемент audience.</span><span class="sxs-lookup"><span data-stu-id="b077e-394">At least one audience must be specified.</span></span>|<span data-ttu-id="b077e-395">Нет</span><span class="sxs-lookup"><span data-stu-id="b077e-395">No</span></span>|  
|<span data-ttu-id="b077e-396">issuer-signing-keys</span><span class="sxs-lookup"><span data-stu-id="b077e-396">issuer-signing-keys</span></span>|<span data-ttu-id="b077e-397">Список ключей, используемых toovalidate безопасности в кодировке Base64 подписи токенов.</span><span class="sxs-lookup"><span data-stu-id="b077e-397">A list of Base64-encoded security keys used toovalidate signed tokens.</span></span> <span data-ttu-id="b077e-398">При наличии нескольких ключей безопасности каждый ключ проверяется либо до их исчерпания (в этом случае проверка будет не пройдена), либо до обнаружения подходящего ключа (удобно для смены маркеров).</span><span class="sxs-lookup"><span data-stu-id="b077e-398">If multiple security keys are present, then each key is tried until either all are exhausted (in which case validation fails) or until one succeeds (useful for token rollover).</span></span> <span data-ttu-id="b077e-399">Ключевые элементы имеют дополнительный `id` toomatch атрибут, используемый для `kid` утверждения.</span><span class="sxs-lookup"><span data-stu-id="b077e-399">Key elements have an optional `id` attribute used toomatch against `kid` claim.</span></span>|<span data-ttu-id="b077e-400">Нет</span><span class="sxs-lookup"><span data-stu-id="b077e-400">No</span></span>|  
|<span data-ttu-id="b077e-401">issuers</span><span class="sxs-lookup"><span data-stu-id="b077e-401">issuers</span></span>|<span data-ttu-id="b077e-402">Список допустимых субъектов, выпустивших токен hello.</span><span class="sxs-lookup"><span data-stu-id="b077e-402">A list of acceptable principals that issued hello token.</span></span> <span data-ttu-id="b077e-403">При наличии нескольких значений элемента issuer каждое значение проверяется либо до их исчерпания (в этом случае проверка будет не пройдена), либо до обнаружения подходящего значения.</span><span class="sxs-lookup"><span data-stu-id="b077e-403">If multiple issuer values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span>|<span data-ttu-id="b077e-404">Нет</span><span class="sxs-lookup"><span data-stu-id="b077e-404">No</span></span>|  
|<span data-ttu-id="b077e-405">openid-config</span><span class="sxs-lookup"><span data-stu-id="b077e-405">openid-config</span></span>|<span data-ttu-id="b077e-406">элемент Hello, используемая для указания совместимые конечной точки конфигурации Open ID из которого можно получить ключи подписывания и издателя.</span><span class="sxs-lookup"><span data-stu-id="b077e-406">hello element used for specifying a compliant Open ID configuration endpoint from which signing keys and issuer can be obtained.</span></span>|<span data-ttu-id="b077e-407">Нет</span><span class="sxs-lookup"><span data-stu-id="b077e-407">No</span></span>|  
|<span data-ttu-id="b077e-408">required-claims</span><span class="sxs-lookup"><span data-stu-id="b077e-408">required-claims</span></span>|<span data-ttu-id="b077e-409">Содержит список утверждений, которые toobe присутствует для hello маркер для его toobe считается действительным.</span><span class="sxs-lookup"><span data-stu-id="b077e-409">Contains a list of claims expected toobe present on hello token for it toobe considered valid.</span></span> <span data-ttu-id="b077e-410">Здравствуйте, когда `match` атрибута задано слишком`all` все значения утверждений в политике hello должны присутствовать в маркере hello для проверки toosucceed.</span><span class="sxs-lookup"><span data-stu-id="b077e-410">When hello `match` attribute is set too`all` every claim value in hello policy must be present in hello token for validation toosucceed.</span></span> <span data-ttu-id="b077e-411">Здравствуйте, когда `match` атрибута задано слишком`any` по крайней мере одно утверждение должны присутствовать в маркере hello для проверки toosucceed.</span><span class="sxs-lookup"><span data-stu-id="b077e-411">When hello `match` attribute is set too`any` at least one claim must be present in hello token for validation toosucceed.</span></span>|<span data-ttu-id="b077e-412">Нет</span><span class="sxs-lookup"><span data-stu-id="b077e-412">No</span></span>|  
|<span data-ttu-id="b077e-413">zumo-master-key</span><span class="sxs-lookup"><span data-stu-id="b077e-413">zumo-master-key</span></span>|<span data-ttu-id="b077e-414">Главный ключ для маркеров, выданных мобильными службами Azure.</span><span class="sxs-lookup"><span data-stu-id="b077e-414">Master key for tokens issued by Azure Mobile Services</span></span>|<span data-ttu-id="b077e-415">Нет</span><span class="sxs-lookup"><span data-stu-id="b077e-415">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="b077e-416">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="b077e-416">Attributes</span></span>  
  
|<span data-ttu-id="b077e-417">Имя</span><span class="sxs-lookup"><span data-stu-id="b077e-417">Name</span></span>|<span data-ttu-id="b077e-418">Описание</span><span class="sxs-lookup"><span data-stu-id="b077e-418">Description</span></span>|<span data-ttu-id="b077e-419">Обязательно</span><span class="sxs-lookup"><span data-stu-id="b077e-419">Required</span></span>|<span data-ttu-id="b077e-420">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="b077e-420">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="b077e-421">clock-skew</span><span class="sxs-lookup"><span data-stu-id="b077e-421">clock-skew</span></span>|<span data-ttu-id="b077e-422">Интервал времени.</span><span class="sxs-lookup"><span data-stu-id="b077e-422">Timespan.</span></span> <span data-ttu-id="b077e-423">Предоставляет кратковременную отсрочку в том случае, если утверждение истечения срока действия маркера hello присутствует в маркере hello и выходит за пределы текущего hello даты / времени.</span><span class="sxs-lookup"><span data-stu-id="b077e-423">Provides some small leeway in case hello token's expiration claim is present in hello token and is past hello current date / time.</span></span>|<span data-ttu-id="b077e-424">Нет</span><span class="sxs-lookup"><span data-stu-id="b077e-424">No</span></span>|<span data-ttu-id="b077e-425">0 секунд</span><span class="sxs-lookup"><span data-stu-id="b077e-425">0 seconds</span></span>|  
|<span data-ttu-id="b077e-426">failed-validation-error-message</span><span class="sxs-lookup"><span data-stu-id="b077e-426">failed-validation-error-message</span></span>|<span data-ttu-id="b077e-427">Ошибка tooreturn сообщений в текст ответа hello HTTP, если hello JWT не проходит проверку.</span><span class="sxs-lookup"><span data-stu-id="b077e-427">Error message tooreturn in hello HTTP response body if hello JWT does not pass validation.</span></span> <span data-ttu-id="b077e-428">Это сообщение должно содержать правильно экранированные специальные символы.</span><span class="sxs-lookup"><span data-stu-id="b077e-428">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="b077e-429">Нет</span><span class="sxs-lookup"><span data-stu-id="b077e-429">No</span></span>|<span data-ttu-id="b077e-430">Сообщение об ошибке по умолчанию зависит от проблемы проверки, например "JWT отсутствует".</span><span class="sxs-lookup"><span data-stu-id="b077e-430">Default error message depends on validation issue, for example "JWT not present."</span></span>|  
|<span data-ttu-id="b077e-431">failed-validation-httpcode</span><span class="sxs-lookup"><span data-stu-id="b077e-431">failed-validation-httpcode</span></span>|<span data-ttu-id="b077e-432">Tooreturn код состояния HTTP, если hello JWT не проходит проверку.</span><span class="sxs-lookup"><span data-stu-id="b077e-432">HTTP Status code tooreturn if hello JWT doesn't pass validation.</span></span>|<span data-ttu-id="b077e-433">Нет</span><span class="sxs-lookup"><span data-stu-id="b077e-433">No</span></span>|<span data-ttu-id="b077e-434">401</span><span class="sxs-lookup"><span data-stu-id="b077e-434">401</span></span>|  
|<span data-ttu-id="b077e-435">header-name</span><span class="sxs-lookup"><span data-stu-id="b077e-435">header-name</span></span>|<span data-ttu-id="b077e-436">Hello имя заголовка hello HTTP, удерживая токен hello.</span><span class="sxs-lookup"><span data-stu-id="b077e-436">hello name of hello HTTP header holding hello token.</span></span>|<span data-ttu-id="b077e-437">Необходимо указать один из двух атрибутов (`header-name` или `query-paremeter-name`), но не оба.</span><span class="sxs-lookup"><span data-stu-id="b077e-437">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="b077e-438">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-438">N/A</span></span>|  
|<span data-ttu-id="b077e-439">id</span><span class="sxs-lookup"><span data-stu-id="b077e-439">id</span></span>|<span data-ttu-id="b077e-440">Hello `id` атрибут hello `key` элемент позволяет toospecify hello строку, которая будет сопоставлена с `kid` утверждений в токен (при его наличии) toofind hello out hello toouse соответствующего ключа для проверки подписи.</span><span class="sxs-lookup"><span data-stu-id="b077e-440">hello `id` attribute on hello `key` element allows you toospecify hello string that will be matched against `kid` claim in hello token (if present) toofind out hello appropriate key toouse for signature validation.</span></span>|<span data-ttu-id="b077e-441">Нет</span><span class="sxs-lookup"><span data-stu-id="b077e-441">No</span></span>|<span data-ttu-id="b077e-442">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-442">N/A</span></span>|  
|<span data-ttu-id="b077e-443">match</span><span class="sxs-lookup"><span data-stu-id="b077e-443">match</span></span>|<span data-ttu-id="b077e-444">Hello `match` атрибут hello `claim` элемент указывает, должен ли все значения утверждений в политике hello присутствует hello маркер для проверки toosucceed.</span><span class="sxs-lookup"><span data-stu-id="b077e-444">hello `match` attribute on hello `claim` element specifies whether every claim value in hello policy must be present in hello token for validation toosucceed.</span></span> <span data-ttu-id="b077e-445">Возможные значения:</span><span class="sxs-lookup"><span data-stu-id="b077e-445">Possible values are:</span></span><br /><br /> <span data-ttu-id="b077e-446">-                          `all`-все значения утверждений в политике hello должны присутствовать в маркере hello для проверки toosucceed.</span><span class="sxs-lookup"><span data-stu-id="b077e-446">-                          `all` - every claim value in hello policy must be present in hello token for validation toosucceed.</span></span><br /><br /> <span data-ttu-id="b077e-447">-                          `any`-значение хотя бы одно утверждение должны присутствовать в маркере hello для проверки toosucceed.</span><span class="sxs-lookup"><span data-stu-id="b077e-447">-                          `any` - at least one claim value must be present in hello token for validation toosucceed.</span></span>|<span data-ttu-id="b077e-448">Нет</span><span class="sxs-lookup"><span data-stu-id="b077e-448">No</span></span>|<span data-ttu-id="b077e-449">все</span><span class="sxs-lookup"><span data-stu-id="b077e-449">all</span></span>|  
|<span data-ttu-id="b077e-450">query-paremeter-name</span><span class="sxs-lookup"><span data-stu-id="b077e-450">query-paremeter-name</span></span>|<span data-ttu-id="b077e-451">Hello имя параметра запроса hello hello, содержащий токен hello.</span><span class="sxs-lookup"><span data-stu-id="b077e-451">hello name of hello hello query parameter holding hello token.</span></span>|<span data-ttu-id="b077e-452">Необходимо указать один из двух атрибутов (`header-name` или `query-paremeter-name`), но не оба.</span><span class="sxs-lookup"><span data-stu-id="b077e-452">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="b077e-453">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-453">N/A</span></span>|  
|<span data-ttu-id="b077e-454">require-expiration-time</span><span class="sxs-lookup"><span data-stu-id="b077e-454">require-expiration-time</span></span>|<span data-ttu-id="b077e-455">Логическое значение.</span><span class="sxs-lookup"><span data-stu-id="b077e-455">Boolean.</span></span> <span data-ttu-id="b077e-456">Указывает, требуется ли утверждение истечения срока действия маркера hello.</span><span class="sxs-lookup"><span data-stu-id="b077e-456">Specifies whether an expiration claim is required in hello token.</span></span>|<span data-ttu-id="b077e-457">Нет</span><span class="sxs-lookup"><span data-stu-id="b077e-457">No</span></span>|<span data-ttu-id="b077e-458">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-458">true</span></span>|
|<span data-ttu-id="b077e-459">require-scheme</span><span class="sxs-lookup"><span data-stu-id="b077e-459">require-scheme</span></span>|<span data-ttu-id="b077e-460">Здравствуйте, имя схемы токенов hello, например "Bearer".</span><span class="sxs-lookup"><span data-stu-id="b077e-460">hello name of hello token scheme, e.g. "Bearer".</span></span> <span data-ttu-id="b077e-461">Если этот атрибут задан, политики hello обеспечит, указано, что схема присутствует в hello значение заголовка авторизации.</span><span class="sxs-lookup"><span data-stu-id="b077e-461">When this attribute is set, hello policy will ensure that specified scheme is present in hello Authorization header value.</span></span>|<span data-ttu-id="b077e-462">Нет</span><span class="sxs-lookup"><span data-stu-id="b077e-462">No</span></span>|<span data-ttu-id="b077e-463">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-463">N/A</span></span>|
|<span data-ttu-id="b077e-464">require-signed-tokens</span><span class="sxs-lookup"><span data-stu-id="b077e-464">require-signed-tokens</span></span>|<span data-ttu-id="b077e-465">Логическое значение.</span><span class="sxs-lookup"><span data-stu-id="b077e-465">Boolean.</span></span> <span data-ttu-id="b077e-466">Указывает, является ли токен обязательный toobe подписи.</span><span class="sxs-lookup"><span data-stu-id="b077e-466">Specifies whether a token is required toobe signed.</span></span>|<span data-ttu-id="b077e-467">Нет</span><span class="sxs-lookup"><span data-stu-id="b077e-467">No</span></span>|<span data-ttu-id="b077e-468">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-468">true</span></span>|  
|<span data-ttu-id="b077e-469">url</span><span class="sxs-lookup"><span data-stu-id="b077e-469">url</span></span>|<span data-ttu-id="b077e-470">URL-адрес конечной точки конфигурации Open ID, по которому можно получить метаданные конфигурации Open ID.</span><span class="sxs-lookup"><span data-stu-id="b077e-470">Open ID configuration endpoint URL from where Open ID configuration metadata can be obtained.</span></span> <span data-ttu-id="b077e-471">Для Azure Active Directory используйте hello URL-адреса: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` подставив имя клиента каталога, например `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="b077e-471">For Azure Active Directory use hello following URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituting your directory tenant name, e.g. `contoso.onmicrosoft.com`.</span></span>|<span data-ttu-id="b077e-472">Да</span><span class="sxs-lookup"><span data-stu-id="b077e-472">Yes</span></span>|<span data-ttu-id="b077e-473">Недоступно</span><span class="sxs-lookup"><span data-stu-id="b077e-473">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="b077e-474">Использование</span><span class="sxs-lookup"><span data-stu-id="b077e-474">Usage</span></span>  
 <span data-ttu-id="b077e-475">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="b077e-475">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="b077e-476">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="b077e-476">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="b077e-477">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="b077e-477">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="b077e-478">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b077e-478">Next steps</span></span>
<span data-ttu-id="b077e-479">Дополнительные сведения о работе с политиками см. в статье со справочными материалами по [политикам в службе управления API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="b077e-479">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
