---
title: "Политики ограничения доступа в службе управления API Azure | Документация Майкрософт"
description: "Сведения о политиках ограничения, доступных для использования в службе управления API Azure."
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
ms.openlocfilehash: 4c9991baf3fbcf3b8ea01f8dd573e2336db88b68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-access-restriction-policies"></a><span data-ttu-id="d858d-103">Политики ограничения доступа в службе управления API</span><span class="sxs-lookup"><span data-stu-id="d858d-103">API Management access restriction policies</span></span>
<span data-ttu-id="d858d-104">В этой статье рассматриваются приведенные ниже политики управления API.</span><span class="sxs-lookup"><span data-stu-id="d858d-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="d858d-105">Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в управлении API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="d858d-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="d858d-106"><a name="AccessRestrictionPolicies"></a> Политики ограничения доступа</span><span class="sxs-lookup"><span data-stu-id="d858d-106"><a name="AccessRestrictionPolicies"></a> Access restriction policies</span></span>  
  
-   <span data-ttu-id="d858d-107">[Проверка заголовка HTTP](api-management-access-restriction-policies.md#CheckHTTPHeader) – обеспечивает принудительный ввод заголовка HTTP и/или его значения.</span><span class="sxs-lookup"><span data-stu-id="d858d-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
-   <span data-ttu-id="d858d-108">[Ограничение частоты вызовов по подписке](api-management-access-restriction-policies.md#LimitCallRate) — предотвращает пики использования API, ограничивая частоту вызовов для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="d858d-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="d858d-109">[Ограничение частоты вызовов по ключу](#LimitCallRateByKey) — предотвращает пики использования API, ограничивая частоту вызовов по ключу.</span><span class="sxs-lookup"><span data-stu-id="d858d-109">[Limit call rate by key](#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
-   <span data-ttu-id="d858d-110">[Ограничение IP-адресов вызывающих объектов](api-management-access-restriction-policies.md#RestrictCallerIPs) – фильтрует (разрешает или запрещает) вызовы с конкретных IP-адресов и/или диапазонов адресов.</span><span class="sxs-lookup"><span data-stu-id="d858d-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
-   <span data-ttu-id="d858d-111">[Задание квоты использования по подписке](api-management-access-restriction-policies.md#SetUsageQuota) — позволяет принудительно устанавливать возобновляемую или действующую в течение срока службы квоту на число вызовов и (или) квоту пропускной способности для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="d858d-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="d858d-112">[Задание квоты использования по ключу](#SetUsageQuotaByKey) — позволяет принудительно устанавливать возобновляемую или действующую в течение срока службы квоту на число вызовов и (или) квоту пропускной способности для каждого ключа.</span><span class="sxs-lookup"><span data-stu-id="d858d-112">[Set usage quota by key](#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
-   <span data-ttu-id="d858d-113">[Проверка JWT](api-management-access-restriction-policies.md#ValidateJWT) – обеспечивает принудительное задание и проверку JWT, извлеченного из заданного заголовка HTTP или параметра запроса.</span><span class="sxs-lookup"><span data-stu-id="d858d-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
##  <span data-ttu-id="d858d-114"><a name="CheckHTTPHeader"></a> Проверка заголовка HTTP</span><span class="sxs-lookup"><span data-stu-id="d858d-114"><a name="CheckHTTPHeader"></a> Check HTTP header</span></span>  
 <span data-ttu-id="d858d-115">Используйте политику `check-header`, чтобы запрос содержал заданный заголовок HTTP.</span><span class="sxs-lookup"><span data-stu-id="d858d-115">Use the `check-header` policy to enforce that a request has a specified HTTP header.</span></span> <span data-ttu-id="d858d-116">При необходимости можно проверить, содержит ли заголовок определенное значение, или проверить диапазон допустимых значений.</span><span class="sxs-lookup"><span data-stu-id="d858d-116">You can optionally check to see if the header has a specific value or check for a range of allowed values.</span></span> <span data-ttu-id="d858d-117">При сбое проверки политика завершает обработку запроса, после чего возвращает код состояния HTTP и сообщение об ошибке, указанное в политике.</span><span class="sxs-lookup"><span data-stu-id="d858d-117">If the check fails, the policy terminates request processing and returns the HTTP status code and error message specified by the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d858d-118">Правило политики</span><span class="sxs-lookup"><span data-stu-id="d858d-118">Policy statement</span></span>  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a><span data-ttu-id="d858d-119">Пример</span><span class="sxs-lookup"><span data-stu-id="d858d-119">Example</span></span>  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a><span data-ttu-id="d858d-120">Элементы</span><span class="sxs-lookup"><span data-stu-id="d858d-120">Elements</span></span>  
  
|<span data-ttu-id="d858d-121">Имя</span><span class="sxs-lookup"><span data-stu-id="d858d-121">Name</span></span>|<span data-ttu-id="d858d-122">Описание</span><span class="sxs-lookup"><span data-stu-id="d858d-122">Description</span></span>|<span data-ttu-id="d858d-123">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d858d-123">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d858d-124">check-header</span><span class="sxs-lookup"><span data-stu-id="d858d-124">check-header</span></span>|<span data-ttu-id="d858d-125">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="d858d-125">Root element.</span></span>|<span data-ttu-id="d858d-126">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-126">Yes</span></span>|  
|<span data-ttu-id="d858d-127">значение</span><span class="sxs-lookup"><span data-stu-id="d858d-127">value</span></span>|<span data-ttu-id="d858d-128">Допустимое значение заголовка HTTP.</span><span class="sxs-lookup"><span data-stu-id="d858d-128">Allowed HTTP header value.</span></span> <span data-ttu-id="d858d-129">Если указано несколько элементов value и одно из значений совпадает, проверка считается успешной.</span><span class="sxs-lookup"><span data-stu-id="d858d-129">When multiple value elements are specified, the check is considered a success if any one of the values is a match.</span></span>|<span data-ttu-id="d858d-130">Нет</span><span class="sxs-lookup"><span data-stu-id="d858d-130">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d858d-131">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="d858d-131">Attributes</span></span>  
  
|<span data-ttu-id="d858d-132">Имя</span><span class="sxs-lookup"><span data-stu-id="d858d-132">Name</span></span>|<span data-ttu-id="d858d-133">Описание</span><span class="sxs-lookup"><span data-stu-id="d858d-133">Description</span></span>|<span data-ttu-id="d858d-134">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d858d-134">Required</span></span>|<span data-ttu-id="d858d-135">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d858d-135">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d858d-136">failed-check-error-message</span><span class="sxs-lookup"><span data-stu-id="d858d-136">failed-check-error-message</span></span>|<span data-ttu-id="d858d-137">Сообщение об ошибке, возвращаемое в тексте ответа HTTP, если заголовок не существует или имеет недопустимое значение.</span><span class="sxs-lookup"><span data-stu-id="d858d-137">Error message to return in the HTTP response body if the header doesn't exist or has an invalid value.</span></span> <span data-ttu-id="d858d-138">Это сообщение должно содержать правильно экранированные специальные символы.</span><span class="sxs-lookup"><span data-stu-id="d858d-138">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="d858d-139">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-139">Yes</span></span>|<span data-ttu-id="d858d-140">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-140">N/A</span></span>|  
|<span data-ttu-id="d858d-141">failed-check-httpcode</span><span class="sxs-lookup"><span data-stu-id="d858d-141">failed-check-httpcode</span></span>|<span data-ttu-id="d858d-142">Код состояния HTTP, который возвращается, если заголовок не существует или имеет недопустимое значение.</span><span class="sxs-lookup"><span data-stu-id="d858d-142">HTTP Status code to return if the header doesn't exist or has an invalid value.</span></span>|<span data-ttu-id="d858d-143">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-143">Yes</span></span>|<span data-ttu-id="d858d-144">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-144">N/A</span></span>|  
|<span data-ttu-id="d858d-145">header-name</span><span class="sxs-lookup"><span data-stu-id="d858d-145">header-name</span></span>|<span data-ttu-id="d858d-146">Имя заголовка HTTP для проверки.</span><span class="sxs-lookup"><span data-stu-id="d858d-146">The name of the HTTP Header to check.</span></span>|<span data-ttu-id="d858d-147">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-147">Yes</span></span>|<span data-ttu-id="d858d-148">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-148">N/A</span></span>|  
|<span data-ttu-id="d858d-149">ignore-case</span><span class="sxs-lookup"><span data-stu-id="d858d-149">ignore-case</span></span>|<span data-ttu-id="d858d-150">Можно задать значение true или false.</span><span class="sxs-lookup"><span data-stu-id="d858d-150">Can be set to True or False.</span></span> <span data-ttu-id="d858d-151">Если задано значение true и значение заголовка сравнивается с набором допустимых значений, регистр игнорируется.</span><span class="sxs-lookup"><span data-stu-id="d858d-151">If set to True case is ignored when the header value is compared against the set of acceptable values.</span></span>|<span data-ttu-id="d858d-152">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-152">Yes</span></span>|<span data-ttu-id="d858d-153">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-153">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d858d-154">Использование</span><span class="sxs-lookup"><span data-stu-id="d858d-154">Usage</span></span>  
 <span data-ttu-id="d858d-155">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d858d-155">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d858d-156">**Разделы политики:** inbound, outbound.</span><span class="sxs-lookup"><span data-stu-id="d858d-156">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="d858d-157">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="d858d-157">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d858d-158"><a name="LimitCallRate"></a> Ограничение частоты вызовов по подписке</span><span class="sxs-lookup"><span data-stu-id="d858d-158"><a name="LimitCallRate"></a> Limit call rate by subscription</span></span>  
 <span data-ttu-id="d858d-159">Политика `rate-limit` предотвращает пики использования API для каждой подписки, ограничивая частоту вызовов до указанного числа за определенный период времени.</span><span class="sxs-lookup"><span data-stu-id="d858d-159">The `rate-limit` policy prevents API usage spikes on a per subscription basis by limiting the call rate to a specified number per a specified time period.</span></span> <span data-ttu-id="d858d-160">При запуске этой политики вызывающий объект получает код состояния ответа `429 Too Many Requests`.</span><span class="sxs-lookup"><span data-stu-id="d858d-160">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="d858d-161">Эту политику можно использовать для каждого документа политики только один раз.</span><span class="sxs-lookup"><span data-stu-id="d858d-161">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="d858d-162">Для данной политики [выражения политики](api-management-policy-expressions.md) нельзя использовать в атрибутах политики.</span><span class="sxs-lookup"><span data-stu-id="d858d-162">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d858d-163">Правило политики</span><span class="sxs-lookup"><span data-stu-id="d858d-163">Policy statement</span></span>  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a><span data-ttu-id="d858d-164">Пример</span><span class="sxs-lookup"><span data-stu-id="d858d-164">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="d858d-165">Элементы</span><span class="sxs-lookup"><span data-stu-id="d858d-165">Elements</span></span>  
  
|<span data-ttu-id="d858d-166">Имя</span><span class="sxs-lookup"><span data-stu-id="d858d-166">Name</span></span>|<span data-ttu-id="d858d-167">Описание</span><span class="sxs-lookup"><span data-stu-id="d858d-167">Description</span></span>|<span data-ttu-id="d858d-168">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d858d-168">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d858d-169">set-limit</span><span class="sxs-lookup"><span data-stu-id="d858d-169">set-limit</span></span>|<span data-ttu-id="d858d-170">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="d858d-170">Root element.</span></span>|<span data-ttu-id="d858d-171">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-171">Yes</span></span>|  
|<span data-ttu-id="d858d-172">api</span><span class="sxs-lookup"><span data-stu-id="d858d-172">api</span></span>|<span data-ttu-id="d858d-173">Добавьте один или несколько таких элементов, чтобы установить ограничение частоты вызовов для интерфейсов API в пределах продукта.</span><span class="sxs-lookup"><span data-stu-id="d858d-173">Add one  or more of these elements to impose a call rate limit on APIs within the product.</span></span> <span data-ttu-id="d858d-174">Ограничения частоты вызовов продукта и API применяются раздельно.</span><span class="sxs-lookup"><span data-stu-id="d858d-174">Product and API call rate limits are applied independently.</span></span>|<span data-ttu-id="d858d-175">Нет</span><span class="sxs-lookup"><span data-stu-id="d858d-175">No</span></span>|  
|<span data-ttu-id="d858d-176">операция</span><span class="sxs-lookup"><span data-stu-id="d858d-176">operation</span></span>|<span data-ttu-id="d858d-177">Добавьте один или несколько таких элементов, чтобы установить ограничение частоты вызовов для операций в API.</span><span class="sxs-lookup"><span data-stu-id="d858d-177">Add one  or more of these elements to impose a call rate limit on operations within an API.</span></span> <span data-ttu-id="d858d-178">Ограничения частоты вызовов продукта, API и операции применяются раздельно.</span><span class="sxs-lookup"><span data-stu-id="d858d-178">Product, API, and operation call rate limits are applied independently.</span></span>|<span data-ttu-id="d858d-179">Нет</span><span class="sxs-lookup"><span data-stu-id="d858d-179">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d858d-180">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="d858d-180">Attributes</span></span>  
  
|<span data-ttu-id="d858d-181">Имя</span><span class="sxs-lookup"><span data-stu-id="d858d-181">Name</span></span>|<span data-ttu-id="d858d-182">Описание</span><span class="sxs-lookup"><span data-stu-id="d858d-182">Description</span></span>|<span data-ttu-id="d858d-183">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d858d-183">Required</span></span>|<span data-ttu-id="d858d-184">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d858d-184">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d858d-185">name</span><span class="sxs-lookup"><span data-stu-id="d858d-185">name</span></span>|<span data-ttu-id="d858d-186">Имя API, для которого применяется ограничение частоты.</span><span class="sxs-lookup"><span data-stu-id="d858d-186">The name of the API for which to apply the rate limit.</span></span>|<span data-ttu-id="d858d-187">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-187">Yes</span></span>|<span data-ttu-id="d858d-188">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-188">N/A</span></span>|  
|<span data-ttu-id="d858d-189">calls</span><span class="sxs-lookup"><span data-stu-id="d858d-189">calls</span></span>|<span data-ttu-id="d858d-190">Максимальное общее число вызовов, разрешенное в течение периода времени, указанного в `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="d858d-190">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="d858d-191">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-191">Yes</span></span>|<span data-ttu-id="d858d-192">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-192">N/A</span></span>|  
|<span data-ttu-id="d858d-193">renewal-period</span><span class="sxs-lookup"><span data-stu-id="d858d-193">renewal-period</span></span>|<span data-ttu-id="d858d-194">Период времени (в секундах), по окончании которого сбрасывается квота.</span><span class="sxs-lookup"><span data-stu-id="d858d-194">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="d858d-195">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-195">Yes</span></span>|<span data-ttu-id="d858d-196">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-196">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d858d-197">Использование</span><span class="sxs-lookup"><span data-stu-id="d858d-197">Usage</span></span>  
 <span data-ttu-id="d858d-198">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d858d-198">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d858d-199">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="d858d-199">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="d858d-200">**Области политики:** product.</span><span class="sxs-lookup"><span data-stu-id="d858d-200">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="d858d-201"><a name="LimitCallRateByKey"></a> Ограничение частоты вызовов по ключу</span><span class="sxs-lookup"><span data-stu-id="d858d-201"><a name="LimitCallRateByKey"></a> Limit call rate by key</span></span>  
 <span data-ttu-id="d858d-202">Политика `rate-limit-by-key` предотвращает пики использования API для каждого ключа, ограничивая частоту вызовов до указанного числа за определенный период времени.</span><span class="sxs-lookup"><span data-stu-id="d858d-202">The `rate-limit-by-key` policy prevents API usage spikes on a per key basis by limiting the call rate to a specified number per a specified time period.</span></span> <span data-ttu-id="d858d-203">Ключ может содержать произвольное строковое значение и обычно указывается с помощью выражения политики.</span><span class="sxs-lookup"><span data-stu-id="d858d-203">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="d858d-204">Чтобы указать, какие запросы следует учитывать для ограничения, можно добавить дополнительное условие увеличения.</span><span class="sxs-lookup"><span data-stu-id="d858d-204">Optional increment condition can be added to specify which requests should be counted towards the limit.</span></span> <span data-ttu-id="d858d-205">При запуске этой политики вызывающий объект получает код состояния ответа `429 Too Many Requests`.</span><span class="sxs-lookup"><span data-stu-id="d858d-205">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span></span>  
  
 <span data-ttu-id="d858d-206">Дополнительные сведения и примеры этой политики см. в статье [Расширенное регулирование запросов с помощью управления API](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="d858d-206">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="d858d-207">Эту политику можно использовать для каждого документа политики только один раз.</span><span class="sxs-lookup"><span data-stu-id="d858d-207">This policy can be used only once per policy document.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d858d-208">Правило политики</span><span class="sxs-lookup"><span data-stu-id="d858d-208">Policy statement</span></span>  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="d858d-209">Пример</span><span class="sxs-lookup"><span data-stu-id="d858d-209">Example</span></span>  
 <span data-ttu-id="d858d-210">В следующем примере ограничение частоты содержит ключ, состоящий из IP-адреса вызывающего объекта.</span><span class="sxs-lookup"><span data-stu-id="d858d-210">In the following example, the rate limit is keyed by the caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="d858d-211">Элементы</span><span class="sxs-lookup"><span data-stu-id="d858d-211">Elements</span></span>  
  
|<span data-ttu-id="d858d-212">Имя</span><span class="sxs-lookup"><span data-stu-id="d858d-212">Name</span></span>|<span data-ttu-id="d858d-213">Описание</span><span class="sxs-lookup"><span data-stu-id="d858d-213">Description</span></span>|<span data-ttu-id="d858d-214">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d858d-214">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d858d-215">set-limit</span><span class="sxs-lookup"><span data-stu-id="d858d-215">set-limit</span></span>|<span data-ttu-id="d858d-216">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="d858d-216">Root element.</span></span>|<span data-ttu-id="d858d-217">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-217">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d858d-218">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="d858d-218">Attributes</span></span>  
  
|<span data-ttu-id="d858d-219">Имя</span><span class="sxs-lookup"><span data-stu-id="d858d-219">Name</span></span>|<span data-ttu-id="d858d-220">Описание</span><span class="sxs-lookup"><span data-stu-id="d858d-220">Description</span></span>|<span data-ttu-id="d858d-221">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d858d-221">Required</span></span>|<span data-ttu-id="d858d-222">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d858d-222">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d858d-223">calls</span><span class="sxs-lookup"><span data-stu-id="d858d-223">calls</span></span>|<span data-ttu-id="d858d-224">Максимальное общее число вызовов, разрешенное в течение периода времени, указанного в `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="d858d-224">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="d858d-225">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-225">Yes</span></span>|<span data-ttu-id="d858d-226">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-226">N/A</span></span>|  
|<span data-ttu-id="d858d-227">counter-key</span><span class="sxs-lookup"><span data-stu-id="d858d-227">counter-key</span></span>|<span data-ttu-id="d858d-228">Ключ, используемый для политики ограничения частоты.</span><span class="sxs-lookup"><span data-stu-id="d858d-228">The key to use for the rate limit policy.</span></span>|<span data-ttu-id="d858d-229">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-229">Yes</span></span>|<span data-ttu-id="d858d-230">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-230">N/A</span></span>|  
|<span data-ttu-id="d858d-231">increment-condition</span><span class="sxs-lookup"><span data-stu-id="d858d-231">increment-condition</span></span>|<span data-ttu-id="d858d-232">Логическое выражение, указывающее, следует ли учитывать запрос для квоты (`true`).</span><span class="sxs-lookup"><span data-stu-id="d858d-232">The boolean expression specifying if the request should be counted towards the quota (`true`).</span></span>|<span data-ttu-id="d858d-233">Нет</span><span class="sxs-lookup"><span data-stu-id="d858d-233">No</span></span>|<span data-ttu-id="d858d-234">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-234">N/A</span></span>|  
|<span data-ttu-id="d858d-235">renewal-period</span><span class="sxs-lookup"><span data-stu-id="d858d-235">renewal-period</span></span>|<span data-ttu-id="d858d-236">Период времени (в секундах), по окончании которого сбрасывается квота.</span><span class="sxs-lookup"><span data-stu-id="d858d-236">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="d858d-237">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-237">Yes</span></span>|<span data-ttu-id="d858d-238">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-238">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d858d-239">Использование</span><span class="sxs-lookup"><span data-stu-id="d858d-239">Usage</span></span>  
 <span data-ttu-id="d858d-240">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d858d-240">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d858d-241">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="d858d-241">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="d858d-242">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="d858d-242">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d858d-243"><a name="RestrictCallerIPs"></a> Ограничение IP-адресов вызывающих объектов</span><span class="sxs-lookup"><span data-stu-id="d858d-243"><a name="RestrictCallerIPs"></a> Restrict caller IPs</span></span>  
 <span data-ttu-id="d858d-244">Политика `ip-filter` фильтрует (разрешает и запрещает) вызовы с конкретных IP-адресов и (или) диапазонов адресов.</span><span class="sxs-lookup"><span data-stu-id="d858d-244">The `ip-filter` policy filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d858d-245">Правило политики</span><span class="sxs-lookup"><span data-stu-id="d858d-245">Policy statement</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a><span data-ttu-id="d858d-246">Пример</span><span class="sxs-lookup"><span data-stu-id="d858d-246">Example</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a><span data-ttu-id="d858d-247">Элементы</span><span class="sxs-lookup"><span data-stu-id="d858d-247">Elements</span></span>  
  
|<span data-ttu-id="d858d-248">Имя</span><span class="sxs-lookup"><span data-stu-id="d858d-248">Name</span></span>|<span data-ttu-id="d858d-249">Описание</span><span class="sxs-lookup"><span data-stu-id="d858d-249">Description</span></span>|<span data-ttu-id="d858d-250">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d858d-250">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d858d-251">ip-filter</span><span class="sxs-lookup"><span data-stu-id="d858d-251">ip-filter</span></span>|<span data-ttu-id="d858d-252">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="d858d-252">Root element.</span></span>|<span data-ttu-id="d858d-253">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-253">Yes</span></span>|  
|<span data-ttu-id="d858d-254">address</span><span class="sxs-lookup"><span data-stu-id="d858d-254">address</span></span>|<span data-ttu-id="d858d-255">Указывает один IP-адрес для фильтрации.</span><span class="sxs-lookup"><span data-stu-id="d858d-255">Specifies a single IP address on which to filter.</span></span>|<span data-ttu-id="d858d-256">По крайней мере один элемент `address` или `address-range` является обязательным.</span><span class="sxs-lookup"><span data-stu-id="d858d-256">At least one `address` or `address-range` element is required.</span></span>|  
|<span data-ttu-id="d858d-257">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="d858d-257">address-range from="address" to="address"</span></span>|<span data-ttu-id="d858d-258">Указывает диапазон IP-адресов для фильтрации.</span><span class="sxs-lookup"><span data-stu-id="d858d-258">Specifies a range of IP address on which to filter.</span></span>|<span data-ttu-id="d858d-259">По крайней мере один элемент `address` или `address-range` является обязательным.</span><span class="sxs-lookup"><span data-stu-id="d858d-259">At least one `address` or `address-range` element is required.</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d858d-260">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="d858d-260">Attributes</span></span>  
  
|<span data-ttu-id="d858d-261">Имя</span><span class="sxs-lookup"><span data-stu-id="d858d-261">Name</span></span>|<span data-ttu-id="d858d-262">Описание</span><span class="sxs-lookup"><span data-stu-id="d858d-262">Description</span></span>|<span data-ttu-id="d858d-263">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d858d-263">Required</span></span>|<span data-ttu-id="d858d-264">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d858d-264">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d858d-265">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="d858d-265">address-range from="address" to="address"</span></span>|<span data-ttu-id="d858d-266">Диапазон IP-адресов, для которого действует разрешение или запрет доступа.</span><span class="sxs-lookup"><span data-stu-id="d858d-266">A range of IP addresses to allow or deny access for.</span></span>|<span data-ttu-id="d858d-267">Обязательный атрибут, если используется элемент `address-range`.</span><span class="sxs-lookup"><span data-stu-id="d858d-267">Required when the `address-range` element is used.</span></span>|<span data-ttu-id="d858d-268">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-268">N/A</span></span>|  
|<span data-ttu-id="d858d-269">ip-filter action="allow &#124; forbid"</span><span class="sxs-lookup"><span data-stu-id="d858d-269">ip-filter action="allow &#124; forbid"</span></span>|<span data-ttu-id="d858d-270">Указывает, должны ли быть разрешены или запрещены вызовы для указанных IP-адресов и диапазонов.</span><span class="sxs-lookup"><span data-stu-id="d858d-270">Specifies whether calls should be allowed or not for the specified IP addresses and ranges.</span></span>|<span data-ttu-id="d858d-271">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-271">Yes</span></span>|<span data-ttu-id="d858d-272">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d858d-273">Использование</span><span class="sxs-lookup"><span data-stu-id="d858d-273">Usage</span></span>  
 <span data-ttu-id="d858d-274">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d858d-274">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d858d-275">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="d858d-275">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="d858d-276">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="d858d-276">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d858d-277"><a name="SetUsageQuota"></a> Задание квоты использования по подписке</span><span class="sxs-lookup"><span data-stu-id="d858d-277"><a name="SetUsageQuota"></a> Set usage quota by subscription</span></span>  
 <span data-ttu-id="d858d-278">Политика `quota` принудительно устанавливает возобновляемую или действующую в течение срока службы квоту на число вызовов и (или) квоту пропускной способности для каждой подписки.</span><span class="sxs-lookup"><span data-stu-id="d858d-278">The `quota` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="d858d-279">Эту политику можно использовать для каждого документа политики только один раз.</span><span class="sxs-lookup"><span data-stu-id="d858d-279">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="d858d-280">Для данной политики [выражения политики](api-management-policy-expressions.md) нельзя использовать в атрибутах политики.</span><span class="sxs-lookup"><span data-stu-id="d858d-280">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d858d-281">Правило политики</span><span class="sxs-lookup"><span data-stu-id="d858d-281">Policy statement</span></span>  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a><span data-ttu-id="d858d-282">Пример</span><span class="sxs-lookup"><span data-stu-id="d858d-282">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="d858d-283">Элементы</span><span class="sxs-lookup"><span data-stu-id="d858d-283">Elements</span></span>  
  
|<span data-ttu-id="d858d-284">Имя</span><span class="sxs-lookup"><span data-stu-id="d858d-284">Name</span></span>|<span data-ttu-id="d858d-285">Описание</span><span class="sxs-lookup"><span data-stu-id="d858d-285">Description</span></span>|<span data-ttu-id="d858d-286">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d858d-286">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d858d-287">quota</span><span class="sxs-lookup"><span data-stu-id="d858d-287">quota</span></span>|<span data-ttu-id="d858d-288">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="d858d-288">Root element.</span></span>|<span data-ttu-id="d858d-289">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-289">Yes</span></span>|  
|<span data-ttu-id="d858d-290">api</span><span class="sxs-lookup"><span data-stu-id="d858d-290">api</span></span>|<span data-ttu-id="d858d-291">Добавьте один или несколько таких элементов, чтобы установить квоту для интерфейсов API в пределах продукта.</span><span class="sxs-lookup"><span data-stu-id="d858d-291">Add one  or more of these elements to impose a quota on APIs within the product.</span></span> <span data-ttu-id="d858d-292">Квоты продукта и API применяются раздельно.</span><span class="sxs-lookup"><span data-stu-id="d858d-292">Product and API quotas are applied independently.</span></span>|<span data-ttu-id="d858d-293">Нет</span><span class="sxs-lookup"><span data-stu-id="d858d-293">No</span></span>|  
|<span data-ttu-id="d858d-294">операция</span><span class="sxs-lookup"><span data-stu-id="d858d-294">operation</span></span>|<span data-ttu-id="d858d-295">Добавьте один или несколько таких элементов, чтобы установить квоту для операций в API.</span><span class="sxs-lookup"><span data-stu-id="d858d-295">Add one  or more of these elements to impose a quota on operations within an API.</span></span> <span data-ttu-id="d858d-296">Квоты продукта, API и операции применяются раздельно.</span><span class="sxs-lookup"><span data-stu-id="d858d-296">Product, API, and operation quotas are applied independently.</span></span>|<span data-ttu-id="d858d-297">Нет</span><span class="sxs-lookup"><span data-stu-id="d858d-297">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d858d-298">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="d858d-298">Attributes</span></span>  
  
|<span data-ttu-id="d858d-299">Имя</span><span class="sxs-lookup"><span data-stu-id="d858d-299">Name</span></span>|<span data-ttu-id="d858d-300">Описание</span><span class="sxs-lookup"><span data-stu-id="d858d-300">Description</span></span>|<span data-ttu-id="d858d-301">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d858d-301">Required</span></span>|<span data-ttu-id="d858d-302">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d858d-302">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d858d-303">name</span><span class="sxs-lookup"><span data-stu-id="d858d-303">name</span></span>|<span data-ttu-id="d858d-304">Имя API или операции, к которой применяется квота.</span><span class="sxs-lookup"><span data-stu-id="d858d-304">The name of the API or operation for which the quota applies.</span></span>|<span data-ttu-id="d858d-305">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-305">Yes</span></span>|<span data-ttu-id="d858d-306">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-306">N/A</span></span>|  
|<span data-ttu-id="d858d-307">bandwidth</span><span class="sxs-lookup"><span data-stu-id="d858d-307">bandwidth</span></span>|<span data-ttu-id="d858d-308">Максимальное общее число килобайтов, разрешенное в течение периода времени, указанного в `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="d858d-308">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="d858d-309">Необходимо указать атрибут `calls`, `bandwidth` или оба вместе.</span><span class="sxs-lookup"><span data-stu-id="d858d-309">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="d858d-310">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-310">N/A</span></span>|  
|<span data-ttu-id="d858d-311">calls</span><span class="sxs-lookup"><span data-stu-id="d858d-311">calls</span></span>|<span data-ttu-id="d858d-312">Максимальное общее число вызовов, разрешенное в течение периода времени, указанного в `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="d858d-312">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="d858d-313">Необходимо указать атрибут `calls`, `bandwidth` или оба вместе.</span><span class="sxs-lookup"><span data-stu-id="d858d-313">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="d858d-314">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-314">N/A</span></span>|  
|<span data-ttu-id="d858d-315">renewal-period</span><span class="sxs-lookup"><span data-stu-id="d858d-315">renewal-period</span></span>|<span data-ttu-id="d858d-316">Период времени (в секундах), по окончании которого сбрасывается квота.</span><span class="sxs-lookup"><span data-stu-id="d858d-316">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="d858d-317">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-317">Yes</span></span>|<span data-ttu-id="d858d-318">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-318">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d858d-319">Использование</span><span class="sxs-lookup"><span data-stu-id="d858d-319">Usage</span></span>  
 <span data-ttu-id="d858d-320">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d858d-320">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d858d-321">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="d858d-321">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="d858d-322">**Области политики:** product.</span><span class="sxs-lookup"><span data-stu-id="d858d-322">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="d858d-323"><a name="SetUsageQuotaByKey"></a> Задание квоты использования по ключу</span><span class="sxs-lookup"><span data-stu-id="d858d-323"><a name="SetUsageQuotaByKey"></a> Set usage quota by key</span></span>  
 <span data-ttu-id="d858d-324">Политика `quota-by-key` принудительно устанавливает возобновляемую или действующую в течение срока службы квоту на число вызовов и (или) квоту пропускной способности для каждого ключа.</span><span class="sxs-lookup"><span data-stu-id="d858d-324">The `quota-by-key` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span> <span data-ttu-id="d858d-325">Ключ может содержать произвольное строковое значение и обычно указывается с помощью выражения политики.</span><span class="sxs-lookup"><span data-stu-id="d858d-325">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="d858d-326">Чтобы указать, какие запросы следует учитывать в квоте, можно добавить дополнительное условие увеличения.</span><span class="sxs-lookup"><span data-stu-id="d858d-326">Optional increment condition can be added to specify which requests should be counted towards the quota.</span></span>  
  
 <span data-ttu-id="d858d-327">Дополнительные сведения и примеры этой политики см. в статье [Расширенное регулирование запросов с помощью управления API](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="d858d-327">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="d858d-328">Эту политику можно использовать для каждого документа политики только один раз.</span><span class="sxs-lookup"><span data-stu-id="d858d-328">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="d858d-329">Для данной политики [выражения политики](api-management-policy-expressions.md) нельзя использовать в атрибутах политики.</span><span class="sxs-lookup"><span data-stu-id="d858d-329">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d858d-330">Правило политики</span><span class="sxs-lookup"><span data-stu-id="d858d-330">Policy statement</span></span>  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="d858d-331">Пример</span><span class="sxs-lookup"><span data-stu-id="d858d-331">Example</span></span>  
 <span data-ttu-id="d858d-332">В следующем примере квота содержит ключ, состоящий из IP-адреса вызывающего объекта.</span><span class="sxs-lookup"><span data-stu-id="d858d-332">In the following example, the quota is keyed by the caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="d858d-333">Элементы</span><span class="sxs-lookup"><span data-stu-id="d858d-333">Elements</span></span>  
  
|<span data-ttu-id="d858d-334">Имя</span><span class="sxs-lookup"><span data-stu-id="d858d-334">Name</span></span>|<span data-ttu-id="d858d-335">Описание</span><span class="sxs-lookup"><span data-stu-id="d858d-335">Description</span></span>|<span data-ttu-id="d858d-336">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d858d-336">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d858d-337">quota</span><span class="sxs-lookup"><span data-stu-id="d858d-337">quota</span></span>|<span data-ttu-id="d858d-338">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="d858d-338">Root element.</span></span>|<span data-ttu-id="d858d-339">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-339">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d858d-340">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="d858d-340">Attributes</span></span>  
  
|<span data-ttu-id="d858d-341">Имя</span><span class="sxs-lookup"><span data-stu-id="d858d-341">Name</span></span>|<span data-ttu-id="d858d-342">Описание</span><span class="sxs-lookup"><span data-stu-id="d858d-342">Description</span></span>|<span data-ttu-id="d858d-343">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d858d-343">Required</span></span>|<span data-ttu-id="d858d-344">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d858d-344">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d858d-345">bandwidth</span><span class="sxs-lookup"><span data-stu-id="d858d-345">bandwidth</span></span>|<span data-ttu-id="d858d-346">Максимальное общее число килобайтов, разрешенное в течение периода времени, указанного в `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="d858d-346">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="d858d-347">Необходимо указать атрибут `calls`, `bandwidth` или оба вместе.</span><span class="sxs-lookup"><span data-stu-id="d858d-347">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="d858d-348">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-348">N/A</span></span>|  
|<span data-ttu-id="d858d-349">calls</span><span class="sxs-lookup"><span data-stu-id="d858d-349">calls</span></span>|<span data-ttu-id="d858d-350">Максимальное общее число вызовов, разрешенное в течение периода времени, указанного в `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="d858d-350">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="d858d-351">Необходимо указать атрибут `calls`, `bandwidth` или оба вместе.</span><span class="sxs-lookup"><span data-stu-id="d858d-351">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="d858d-352">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-352">N/A</span></span>|  
|<span data-ttu-id="d858d-353">counter-key</span><span class="sxs-lookup"><span data-stu-id="d858d-353">counter-key</span></span>|<span data-ttu-id="d858d-354">Ключ, используемый для политики квоты.</span><span class="sxs-lookup"><span data-stu-id="d858d-354">The key to use for the quota policy.</span></span>|<span data-ttu-id="d858d-355">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-355">Yes</span></span>|<span data-ttu-id="d858d-356">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-356">N/A</span></span>|  
|<span data-ttu-id="d858d-357">increment-condition</span><span class="sxs-lookup"><span data-stu-id="d858d-357">increment-condition</span></span>|<span data-ttu-id="d858d-358">Логическое выражение, указывающее, следует ли учитывать запрос для квоты (`true`).</span><span class="sxs-lookup"><span data-stu-id="d858d-358">The boolean expression specifying if the request should be counted towards the quota (`true`)</span></span>|<span data-ttu-id="d858d-359">Нет</span><span class="sxs-lookup"><span data-stu-id="d858d-359">No</span></span>|<span data-ttu-id="d858d-360">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-360">N/A</span></span>|  
|<span data-ttu-id="d858d-361">renewal-period</span><span class="sxs-lookup"><span data-stu-id="d858d-361">renewal-period</span></span>|<span data-ttu-id="d858d-362">Период времени (в секундах), по окончании которого сбрасывается квота.</span><span class="sxs-lookup"><span data-stu-id="d858d-362">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="d858d-363">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-363">Yes</span></span>|<span data-ttu-id="d858d-364">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-364">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d858d-365">Использование</span><span class="sxs-lookup"><span data-stu-id="d858d-365">Usage</span></span>  
 <span data-ttu-id="d858d-366">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d858d-366">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d858d-367">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="d858d-367">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="d858d-368">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="d858d-368">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d858d-369"><a name="ValidateJWT"></a> Проверка JWT</span><span class="sxs-lookup"><span data-stu-id="d858d-369"><a name="ValidateJWT"></a> Validate JWT</span></span>  
 <span data-ttu-id="d858d-370">Политика `validate-jwt` обеспечивает принудительное задание и проверку маркера JWT, извлеченного из заданного заголовка HTTP или параметра запроса.</span><span class="sxs-lookup"><span data-stu-id="d858d-370">The `validate-jwt` policy enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="d858d-371">Для политики `validate-jwt` требуется, чтобы зарегистрированное утверждение `exp` было включено в маркер JWT, только если для атрибута `require-expiration-time` не задано значение `false`.</span><span class="sxs-lookup"><span data-stu-id="d858d-371">The `validate-jwt` policy requires that the `exp` registered claim is inlcuded in the JWT token, unless `require-expiration-time` attribute is specified and set to `false`.</span></span>  
> <span data-ttu-id="d858d-372">Политика `validate-jwt` поддерживает алгоритмы подписывания HS256 и RS256.</span><span class="sxs-lookup"><span data-stu-id="d858d-372">The `validate-jwt` policy supports HS256 and RS256 signing algorithms.</span></span> <span data-ttu-id="d858d-373">Для HS256 необходимо, чтобы ключ содержался внутри политики в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d858d-373">For HS256 the key must be provided inline within the policy in the base64 encoded form.</span></span> <span data-ttu-id="d858d-374">Для RS256 ключ должен предоставляться через конечную точку конфигурации Open ID.</span><span class="sxs-lookup"><span data-stu-id="d858d-374">For RS256 the key has to be provide via an Open ID configuration endpoint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d858d-375">Правило политики</span><span class="sxs-lookup"><span data-stu-id="d858d-375">Policy statement</span></span>  
  
```xml  
<validate-jwt   
    header-name="name of http header containing the token (use query-parameter-name attribute if the token is passed in the URL)"   
    failed-validation-httpcode="http status code to return on failure"   
    failed-validation-error-message="error message to return on failure"   
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
    <claim name="name of the claim as it appears in the token" match="all|any">  
      <value>claim value as it is expected to appear in the token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of the configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="d858d-376">Примеры</span><span class="sxs-lookup"><span data-stu-id="d858d-376">Examples</span></span>  
  
#### <a name="azure-mobile-services-token-validation"></a><span data-ttu-id="d858d-377">Проверка маркеров мобильных служб Azure</span><span class="sxs-lookup"><span data-stu-id="d858d-377">Azure Mobile Services token validation</span></span>  
  
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
  
#### <a name="azure-active-directory-token-validation"></a><span data-ttu-id="d858d-378">Проверка маркеров Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d858d-378">Azure Active Directory token validation</span></span>  
  
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

  
#### <a name="azure-active-directory-b2c-token-validation"></a><span data-ttu-id="d858d-379">Проверка токена Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="d858d-379">Azure Active Directory B2C token validation</span></span>  
  
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
  
#### <a name="authorize-access-to-operations-based-on-token-claims"></a><span data-ttu-id="d858d-380">Авторизация доступа к операциям на основе утверждений маркера</span><span class="sxs-lookup"><span data-stu-id="d858d-380">Authorize access to operations based on token claims</span></span>  
 <span data-ttu-id="d858d-381">В этом примере показано, как использовать политику [проверки JWT](api-management-access-restriction-policies.md#ValidateJWT) для предварительной авторизации доступа к операциям на основе утверждений маркера.</span><span class="sxs-lookup"><span data-stu-id="d858d-381">This example shows how to use the [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy to pre-authorize access to operations based on token claims.</span></span> <span data-ttu-id="d858d-382">Пример настройки и использования этой политики см. в видео [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Cloud Cover, эпизод 177: возможности управления API с Владом Виноградским) с отметки времени 13:50.</span><span class="sxs-lookup"><span data-stu-id="d858d-382">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 13:50.</span></span> <span data-ttu-id="d858d-383">Перемотайте вперед до отметки времени 15:00, чтобы просмотреть политики, настроенные в редакторе политик, и до 18:50, чтобы просмотреть демонстрацию вызова операции с портала разработчика с обязательным маркером авторизации и без него.</span><span class="sxs-lookup"><span data-stu-id="d858d-383">Fast forward to 15:00 to see the policies configured in the policy editor and then to 18:50 for a demonstration of calling an operation from the developer portal both with and without the required authorization token.</span></span>  
  
```xml  
<!-- Copy the following snippet into the inbound section at the api (or higher) level to pre-authorize access to operations based on token claims -->  
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
  
### <a name="elements"></a><span data-ttu-id="d858d-384">Элементы</span><span class="sxs-lookup"><span data-stu-id="d858d-384">Elements</span></span>  
  
|<span data-ttu-id="d858d-385">Элемент</span><span class="sxs-lookup"><span data-stu-id="d858d-385">Element</span></span>|<span data-ttu-id="d858d-386">Описание</span><span class="sxs-lookup"><span data-stu-id="d858d-386">Description</span></span>|<span data-ttu-id="d858d-387">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d858d-387">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="d858d-388">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="d858d-388">validate-jwt</span></span>|<span data-ttu-id="d858d-389">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="d858d-389">Root element.</span></span>|<span data-ttu-id="d858d-390">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-390">Yes</span></span>|  
|<span data-ttu-id="d858d-391">audiences</span><span class="sxs-lookup"><span data-stu-id="d858d-391">audiences</span></span>|<span data-ttu-id="d858d-392">Содержит список допустимых утверждений audience, которые могут присутствовать в маркере.</span><span class="sxs-lookup"><span data-stu-id="d858d-392">Contains a list of acceptable audience claims that can be present on the token.</span></span> <span data-ttu-id="d858d-393">При наличии нескольких значений audience каждое значение проверяется либо до их исчерпания (в этом случае проверка будет не пройдена), либо до обнаружения подходящего значения.</span><span class="sxs-lookup"><span data-stu-id="d858d-393">If multiple audience values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span> <span data-ttu-id="d858d-394">Необходимо указать по крайней мере один элемент audience.</span><span class="sxs-lookup"><span data-stu-id="d858d-394">At least one audience must be specified.</span></span>|<span data-ttu-id="d858d-395">Нет</span><span class="sxs-lookup"><span data-stu-id="d858d-395">No</span></span>|  
|<span data-ttu-id="d858d-396">issuer-signing-keys</span><span class="sxs-lookup"><span data-stu-id="d858d-396">issuer-signing-keys</span></span>|<span data-ttu-id="d858d-397">Список ключей безопасности в кодировке Base64, используемых для проверки подписанных маркеров.</span><span class="sxs-lookup"><span data-stu-id="d858d-397">A list of Base64-encoded security keys used to validate signed tokens.</span></span> <span data-ttu-id="d858d-398">При наличии нескольких ключей безопасности каждый ключ проверяется либо до их исчерпания (в этом случае проверка будет не пройдена), либо до обнаружения подходящего ключа (удобно для смены маркеров).</span><span class="sxs-lookup"><span data-stu-id="d858d-398">If multiple security keys are present, then each key is tried until either all are exhausted (in which case validation fails) or until one succeeds (useful for token rollover).</span></span> <span data-ttu-id="d858d-399">Ключи могут содержать дополнительный атрибут `id`, используемый для сопоставления с утверждением `kid`.</span><span class="sxs-lookup"><span data-stu-id="d858d-399">Key elements have an optional `id` attribute used to match against `kid` claim.</span></span>|<span data-ttu-id="d858d-400">Нет</span><span class="sxs-lookup"><span data-stu-id="d858d-400">No</span></span>|  
|<span data-ttu-id="d858d-401">issuers</span><span class="sxs-lookup"><span data-stu-id="d858d-401">issuers</span></span>|<span data-ttu-id="d858d-402">Список допустимых субъектов-служб, выдавших маркер.</span><span class="sxs-lookup"><span data-stu-id="d858d-402">A list of acceptable principals that issued the token.</span></span> <span data-ttu-id="d858d-403">При наличии нескольких значений элемента issuer каждое значение проверяется либо до их исчерпания (в этом случае проверка будет не пройдена), либо до обнаружения подходящего значения.</span><span class="sxs-lookup"><span data-stu-id="d858d-403">If multiple issuer values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span>|<span data-ttu-id="d858d-404">Нет</span><span class="sxs-lookup"><span data-stu-id="d858d-404">No</span></span>|  
|<span data-ttu-id="d858d-405">openid-config</span><span class="sxs-lookup"><span data-stu-id="d858d-405">openid-config</span></span>|<span data-ttu-id="d858d-406">Элемент, используемый для указания соответствующей конечной точки конфигурации Open ID, из которой можно получить ключи подписывания и элемент issuer.</span><span class="sxs-lookup"><span data-stu-id="d858d-406">The element used for specifying a compliant Open ID configuration endpoint from which signing keys and issuer can be obtained.</span></span>|<span data-ttu-id="d858d-407">Нет</span><span class="sxs-lookup"><span data-stu-id="d858d-407">No</span></span>|  
|<span data-ttu-id="d858d-408">required-claims</span><span class="sxs-lookup"><span data-stu-id="d858d-408">required-claims</span></span>|<span data-ttu-id="d858d-409">Содержит список утверждений, которые должны содержаться в маркере, который будет считаться допустимым.</span><span class="sxs-lookup"><span data-stu-id="d858d-409">Contains a list of claims expected to be present on the token for it to be considered valid.</span></span> <span data-ttu-id="d858d-410">Если для атрибута `match` задано значение `all`, каждое значение утверждения в политике должно присутствовать в маркере для успешного завершения проверки.</span><span class="sxs-lookup"><span data-stu-id="d858d-410">When the `match` attribute is set to `all` every claim value in the policy must be present in the token for validation to succeed.</span></span> <span data-ttu-id="d858d-411">Если для атрибута `match` задано значение `any`, в маркере должно присутствовать по крайней мере одно утверждение для успешного завершения проверки.</span><span class="sxs-lookup"><span data-stu-id="d858d-411">When the `match` attribute is set to `any` at least one claim must be present in the token for validation to succeed.</span></span>|<span data-ttu-id="d858d-412">Нет</span><span class="sxs-lookup"><span data-stu-id="d858d-412">No</span></span>|  
|<span data-ttu-id="d858d-413">zumo-master-key</span><span class="sxs-lookup"><span data-stu-id="d858d-413">zumo-master-key</span></span>|<span data-ttu-id="d858d-414">Главный ключ для маркеров, выданных мобильными службами Azure.</span><span class="sxs-lookup"><span data-stu-id="d858d-414">Master key for tokens issued by Azure Mobile Services</span></span>|<span data-ttu-id="d858d-415">Нет</span><span class="sxs-lookup"><span data-stu-id="d858d-415">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d858d-416">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="d858d-416">Attributes</span></span>  
  
|<span data-ttu-id="d858d-417">Имя</span><span class="sxs-lookup"><span data-stu-id="d858d-417">Name</span></span>|<span data-ttu-id="d858d-418">Описание</span><span class="sxs-lookup"><span data-stu-id="d858d-418">Description</span></span>|<span data-ttu-id="d858d-419">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d858d-419">Required</span></span>|<span data-ttu-id="d858d-420">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d858d-420">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d858d-421">clock-skew</span><span class="sxs-lookup"><span data-stu-id="d858d-421">clock-skew</span></span>|<span data-ttu-id="d858d-422">Интервал времени.</span><span class="sxs-lookup"><span data-stu-id="d858d-422">Timespan.</span></span> <span data-ttu-id="d858d-423">Предоставляет дополнительный запас времени в том случае, если в маркере присутствует утверждение срока действия с истекшим периодом.</span><span class="sxs-lookup"><span data-stu-id="d858d-423">Provides some small leeway in case the token's expiration claim is present in the token and is past the current date / time.</span></span>|<span data-ttu-id="d858d-424">Нет</span><span class="sxs-lookup"><span data-stu-id="d858d-424">No</span></span>|<span data-ttu-id="d858d-425">0 секунд</span><span class="sxs-lookup"><span data-stu-id="d858d-425">0 seconds</span></span>|  
|<span data-ttu-id="d858d-426">failed-validation-error-message</span><span class="sxs-lookup"><span data-stu-id="d858d-426">failed-validation-error-message</span></span>|<span data-ttu-id="d858d-427">Сообщение об ошибке, которое возвращается в текст HTTP-ответа, если JWT не прошел проверку.</span><span class="sxs-lookup"><span data-stu-id="d858d-427">Error message to return in the HTTP response body if the JWT does not pass validation.</span></span> <span data-ttu-id="d858d-428">Это сообщение должно содержать правильно экранированные специальные символы.</span><span class="sxs-lookup"><span data-stu-id="d858d-428">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="d858d-429">Нет</span><span class="sxs-lookup"><span data-stu-id="d858d-429">No</span></span>|<span data-ttu-id="d858d-430">Сообщение об ошибке по умолчанию зависит от проблемы проверки, например "JWT отсутствует".</span><span class="sxs-lookup"><span data-stu-id="d858d-430">Default error message depends on validation issue, for example "JWT not present."</span></span>|  
|<span data-ttu-id="d858d-431">failed-validation-httpcode</span><span class="sxs-lookup"><span data-stu-id="d858d-431">failed-validation-httpcode</span></span>|<span data-ttu-id="d858d-432">Код состояния HTTP, который возвращается, если JWT не прошел проверку.</span><span class="sxs-lookup"><span data-stu-id="d858d-432">HTTP Status code to return if the JWT doesn't pass validation.</span></span>|<span data-ttu-id="d858d-433">Нет</span><span class="sxs-lookup"><span data-stu-id="d858d-433">No</span></span>|<span data-ttu-id="d858d-434">401</span><span class="sxs-lookup"><span data-stu-id="d858d-434">401</span></span>|  
|<span data-ttu-id="d858d-435">header-name</span><span class="sxs-lookup"><span data-stu-id="d858d-435">header-name</span></span>|<span data-ttu-id="d858d-436">Имя заголовка НТТР, содержащего маркер.</span><span class="sxs-lookup"><span data-stu-id="d858d-436">The name of the HTTP header holding the token.</span></span>|<span data-ttu-id="d858d-437">Необходимо указать один из двух атрибутов (`header-name` или `query-paremeter-name`), но не оба.</span><span class="sxs-lookup"><span data-stu-id="d858d-437">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="d858d-438">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-438">N/A</span></span>|  
|<span data-ttu-id="d858d-439">id</span><span class="sxs-lookup"><span data-stu-id="d858d-439">id</span></span>|<span data-ttu-id="d858d-440">Атрибут `id` в элементе `key` позволяет указать строку, которая будет сопоставлена с утверждением `kid` в маркере (при наличии), чтобы найти подходящий ключ для проверки подписи.</span><span class="sxs-lookup"><span data-stu-id="d858d-440">The `id` attribute on the `key` element allows you to specify the string that will be matched against `kid` claim in the token (if present) to find out the appropriate key to use for signature validation.</span></span>|<span data-ttu-id="d858d-441">Нет</span><span class="sxs-lookup"><span data-stu-id="d858d-441">No</span></span>|<span data-ttu-id="d858d-442">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-442">N/A</span></span>|  
|<span data-ttu-id="d858d-443">match</span><span class="sxs-lookup"><span data-stu-id="d858d-443">match</span></span>|<span data-ttu-id="d858d-444">Атрибут `match` в элементе `claim` указывает, должно ли присутствовать каждое значение утверждения политики в маркере для успешного завершения проверки.</span><span class="sxs-lookup"><span data-stu-id="d858d-444">The `match` attribute on the `claim` element specifies whether every claim value in the policy must be present in the token for validation to succeed.</span></span> <span data-ttu-id="d858d-445">Возможные значения:</span><span class="sxs-lookup"><span data-stu-id="d858d-445">Possible values are:</span></span><br /><br /> <span data-ttu-id="d858d-446">-                          `all` — каждое значение утверждения в политике должно присутствовать в маркере для успешного завершения проверки.</span><span class="sxs-lookup"><span data-stu-id="d858d-446">-                          `all` - every claim value in the policy must be present in the token for validation to succeed.</span></span><br /><br /> <span data-ttu-id="d858d-447">-                          `any` — в маркере должно присутствовать по крайней мере одно значение утверждения для успешного завершения проверки.</span><span class="sxs-lookup"><span data-stu-id="d858d-447">-                          `any` - at least one claim value must be present in the token for validation to succeed.</span></span>|<span data-ttu-id="d858d-448">Нет</span><span class="sxs-lookup"><span data-stu-id="d858d-448">No</span></span>|<span data-ttu-id="d858d-449">все</span><span class="sxs-lookup"><span data-stu-id="d858d-449">all</span></span>|  
|<span data-ttu-id="d858d-450">query-paremeter-name</span><span class="sxs-lookup"><span data-stu-id="d858d-450">query-paremeter-name</span></span>|<span data-ttu-id="d858d-451">Имя параметра запроса, содержащего маркер.</span><span class="sxs-lookup"><span data-stu-id="d858d-451">The name of the the query parameter holding the token.</span></span>|<span data-ttu-id="d858d-452">Необходимо указать один из двух атрибутов (`header-name` или `query-paremeter-name`), но не оба.</span><span class="sxs-lookup"><span data-stu-id="d858d-452">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="d858d-453">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-453">N/A</span></span>|  
|<span data-ttu-id="d858d-454">require-expiration-time</span><span class="sxs-lookup"><span data-stu-id="d858d-454">require-expiration-time</span></span>|<span data-ttu-id="d858d-455">Логическое значение.</span><span class="sxs-lookup"><span data-stu-id="d858d-455">Boolean.</span></span> <span data-ttu-id="d858d-456">Указывает, требуется ли утверждение истечения срока действия для маркера.</span><span class="sxs-lookup"><span data-stu-id="d858d-456">Specifies whether an expiration claim is required in the token.</span></span>|<span data-ttu-id="d858d-457">Нет</span><span class="sxs-lookup"><span data-stu-id="d858d-457">No</span></span>|<span data-ttu-id="d858d-458">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-458">true</span></span>|
|<span data-ttu-id="d858d-459">require-scheme</span><span class="sxs-lookup"><span data-stu-id="d858d-459">require-scheme</span></span>|<span data-ttu-id="d858d-460">Имя схемы маркера, например "Bearer".</span><span class="sxs-lookup"><span data-stu-id="d858d-460">The name of the token scheme, e.g. "Bearer".</span></span> <span data-ttu-id="d858d-461">Когда задан этот атрибут, политики обеспечивают присутствие указанной схемы в значении заголовка Authorization.</span><span class="sxs-lookup"><span data-stu-id="d858d-461">When this attribute is set, the policy will ensure that specified scheme is present in the Authorization header value.</span></span>|<span data-ttu-id="d858d-462">Нет</span><span class="sxs-lookup"><span data-stu-id="d858d-462">No</span></span>|<span data-ttu-id="d858d-463">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-463">N/A</span></span>|
|<span data-ttu-id="d858d-464">require-signed-tokens</span><span class="sxs-lookup"><span data-stu-id="d858d-464">require-signed-tokens</span></span>|<span data-ttu-id="d858d-465">Логическое значение.</span><span class="sxs-lookup"><span data-stu-id="d858d-465">Boolean.</span></span> <span data-ttu-id="d858d-466">Указывает, должен ли быть подписан маркер.</span><span class="sxs-lookup"><span data-stu-id="d858d-466">Specifies whether a token is required to be signed.</span></span>|<span data-ttu-id="d858d-467">Нет</span><span class="sxs-lookup"><span data-stu-id="d858d-467">No</span></span>|<span data-ttu-id="d858d-468">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-468">true</span></span>|  
|<span data-ttu-id="d858d-469">url</span><span class="sxs-lookup"><span data-stu-id="d858d-469">url</span></span>|<span data-ttu-id="d858d-470">URL-адрес конечной точки конфигурации Open ID, по которому можно получить метаданные конфигурации Open ID.</span><span class="sxs-lookup"><span data-stu-id="d858d-470">Open ID configuration endpoint URL from where Open ID configuration metadata can be obtained.</span></span> <span data-ttu-id="d858d-471">Для Azure Active Directory используйте URL-адрес `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration`, подставив необходимое имя клиента каталога, например `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="d858d-471">For Azure Active Directory use the following URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituting your directory tenant name, e.g. `contoso.onmicrosoft.com`.</span></span>|<span data-ttu-id="d858d-472">Да</span><span class="sxs-lookup"><span data-stu-id="d858d-472">Yes</span></span>|<span data-ttu-id="d858d-473">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d858d-473">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d858d-474">Использование</span><span class="sxs-lookup"><span data-stu-id="d858d-474">Usage</span></span>  
 <span data-ttu-id="d858d-475">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d858d-475">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d858d-476">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="d858d-476">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="d858d-477">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="d858d-477">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="d858d-478">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d858d-478">Next steps</span></span>
<span data-ttu-id="d858d-479">Дополнительные сведения о работе с политиками см. в статье со справочными материалами по [политикам в службе управления API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="d858d-479">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
