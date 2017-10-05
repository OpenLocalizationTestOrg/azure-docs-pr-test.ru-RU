---
title: "Расширенные политики службы управления API Azure | Документация Майкрософт"
description: "Сведения о расширенных политиках, доступных для использования в службе управления API Azure."
services: api-management
documentationcenter: 
author: vladvino
manager: erikre
editor: 
ms.assetid: 8a13348b-7856-428f-8e35-9e4273d94323
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 0c65ac74316421a0258f01143baa25ffecb5be3b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="api-management-advanced-policies"></a><span data-ttu-id="3df60-103">Расширенные политики в службе управления API</span><span class="sxs-lookup"><span data-stu-id="3df60-103">API Management advanced policies</span></span>
<span data-ttu-id="3df60-104">В этой статье рассматриваются приведенные ниже политики управления API.</span><span class="sxs-lookup"><span data-stu-id="3df60-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="3df60-105">Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в управлении API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="3df60-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="3df60-106"><a name="AdvancedPolicies"></a> Расширенные политики</span><span class="sxs-lookup"><span data-stu-id="3df60-106"><a name="AdvancedPolicies"></a> Advanced policies</span></span>  
  
-   <span data-ttu-id="3df60-107">[Управление потоками](api-management-advanced-policies.md#choose) — условно применяет правила политики на основе результатов вычисления логических [выражений](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="3df60-107">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on the results of the evaluation of Boolean [expressions](api-management-policy-expressions.md).</span></span>  
  
-   <span data-ttu-id="3df60-108">[Перенаправляющий запрос](#ForwardRequest) — перенаправляет запрос в серверную службу.</span><span class="sxs-lookup"><span data-stu-id="3df60-108">[Forward request](#ForwardRequest) - Forwards the request to the backend service.</span></span>

-   <span data-ttu-id="3df60-109">[Ограничения параллелизма](#LimitConcurrency) не позволяет, чтобы заключенные политики одновременно выполнялись запросами, количество которых выше указанного.</span><span class="sxs-lookup"><span data-stu-id="3df60-109">[Limit concurrency](#LimitConcurrency) - Prevents enclosed policies from executing by more than the specified number of requests at a time.</span></span>
  
-   <span data-ttu-id="3df60-110">[Регистрация в концентраторе событий](#log-to-eventhub) — отправляет сообщения в концентратор событий, который указан сущностью Logger.</span><span class="sxs-lookup"><span data-stu-id="3df60-110">[Log to Event Hub](#log-to-eventhub) - Sends messages in the specified format to an Event Hub defined by a Logger entity.</span></span> 

-   <span data-ttu-id="3df60-111">[Макетирование ответа](#mock-response) — прекращает выполнение конвейера и возвращает макетированный ответ непосредственно вызывающему объекту.</span><span class="sxs-lookup"><span data-stu-id="3df60-111">[Mock response](#mock-response) - Aborts pipeline execution and returns a mocked response directly to the caller.</span></span>
  
-   <span data-ttu-id="3df60-112">[Повторить](#Retry) — повторяет выполнение инструкций встраиваемой политики, если не выполнено условие и до тех пор пока оно не будет выполнено.</span><span class="sxs-lookup"><span data-stu-id="3df60-112">[Retry](#Retry) - Retries execution of the enclosed policy statements, if and until the condition is met.</span></span> <span data-ttu-id="3df60-113">Выполнение будет повторяться через определенные промежутки времени и до указанного количества повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="3df60-113">Execution will repeat at the specified time intervals and up to the specified retry count.</span></span>  
  
-   <span data-ttu-id="3df60-114">[Возврат ответа](#ReturnResponse) — прекращает выполнение конвейера и возвращает указанный ответ непосредственно вызывающему объекту.</span><span class="sxs-lookup"><span data-stu-id="3df60-114">[Return response](#ReturnResponse) - Aborts pipeline execution and returns the specified response directly to the caller.</span></span> 
  
-   <span data-ttu-id="3df60-115">[Отправка одностороннего запроса](#SendOneWayRequest) — отправляет запрос на указанный URL-адрес и не ожидает ответа.</span><span class="sxs-lookup"><span data-stu-id="3df60-115">[Send one way request](#SendOneWayRequest) - Sends a request to the specified URL without waiting for a response.</span></span>  
  
-   <span data-ttu-id="3df60-116">[Отправка запроса](#SendRequest) — отправляет запрос на указанный URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="3df60-116">[Send request](#SendRequest) - Sends a request to the specified URL.</span></span>  

-   <span data-ttu-id="3df60-117">[Установка прокси-сервера HTTP](#SetHttpProxy) — позволяет маршрутизировать перенаправленные запросы через прокси-сервер HTTP.</span><span class="sxs-lookup"><span data-stu-id="3df60-117">[Set HTTP proxy](#SetHttpProxy) - Allows you to route forwarded requests via an HTTP proxy.</span></span>  

-   <span data-ttu-id="3df60-118">[Установка метода запроса](#SetRequestMethod) — позволяет изменить метод HTTP для запроса.</span><span class="sxs-lookup"><span data-stu-id="3df60-118">[Set request method](#SetRequestMethod) - Allows you to change the HTTP method for a request.</span></span>  
  
-   <span data-ttu-id="3df60-119">[Установка кода состояния](#SetStatus) — меняет код состояния HTTP на указанное значение.</span><span class="sxs-lookup"><span data-stu-id="3df60-119">[Set status code](#SetStatus) - Changes the HTTP status code to the specified value.</span></span>  
  
-   <span data-ttu-id="3df60-120">[Задание переменной](api-management-advanced-policies.md#set-variable) — сохраняет значение в именованной переменной [контекста](api-management-policy-expressions.md#ContextVariables) для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="3df60-120">[Set variable](api-management-advanced-policies.md#set-variable) - Persists a value in a named [context](api-management-policy-expressions.md#ContextVariables) variable for later access.</span></span>  

-   <span data-ttu-id="3df60-121">[Трассировка](#Trace) — добавляет строку в выходные данные [инспектора API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/).</span><span class="sxs-lookup"><span data-stu-id="3df60-121">[Trace](#Trace) - Adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
-   <span data-ttu-id="3df60-122">[Ожидание](#Wait) — ожидает завершения вложенных политик [отправки запроса](api-management-advanced-policies.md#SendRequest), [получения значения из кэша](api-management-caching-policies.md#GetFromCacheByKey) или [управления потоком](api-management-advanced-policies.md#choose) перед продолжением.</span><span class="sxs-lookup"><span data-stu-id="3df60-122">[Wait](#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies to complete before proceeding.</span></span>  
  
##  <span data-ttu-id="3df60-123"><a name="choose"></a> Управление потоками</span><span class="sxs-lookup"><span data-stu-id="3df60-123"><a name="choose"></a> Control flow</span></span>  
 <span data-ttu-id="3df60-124">Политика `choose` применяет правила встраиваемой политики на основании результата вычисления логических выражений, подобных if-then-else или конструкции switch в языке программирования.</span><span class="sxs-lookup"><span data-stu-id="3df60-124">The `choose` policy applies enclosed policy statements based on the outcome of evaluation of Boolean expressions, similar to an if-then-else or a switch construct in a programming language.</span></span>  
  
###  <span data-ttu-id="3df60-125"><a name="ChoosePolicyStatement"></a> Правило политики</span><span class="sxs-lookup"><span data-stu-id="3df60-125"><a name="ChoosePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<choose>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements to be applied if the above condition is true  -->  
    </when>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements to be applied if the above condition is true  -->  
    </when>   
    <otherwise>   
        <!— one or more policy statements to be applied if none of the above conditions are true  -->  
</otherwise>   
</choose>  
```  
  
 <span data-ttu-id="3df60-126">Политика потока управления должна содержать по крайней мере один элемент `<when/>`.</span><span class="sxs-lookup"><span data-stu-id="3df60-126">The control flow policy must contain at least one `<when/>` element.</span></span> <span data-ttu-id="3df60-127">Элемент `<otherwise/>` необязательный.</span><span class="sxs-lookup"><span data-stu-id="3df60-127">The `<otherwise/>` element is optional.</span></span> <span data-ttu-id="3df60-128">Условия в элементах `<when/>` вычисляются в порядке их расположения в политике.</span><span class="sxs-lookup"><span data-stu-id="3df60-128">Conditions in `<when/>` elements are evaluated in order of their appearance within the policy.</span></span> <span data-ttu-id="3df60-129">Будут применены правила политики, включенные в первом элементе `<when/>` с атрибутом условия `true`.</span><span class="sxs-lookup"><span data-stu-id="3df60-129">Policy statement(s) enclosed within the first `<when/>` element with condition attribute equals `true` will be applied.</span></span> <span data-ttu-id="3df60-130">Политики, включенные в элементе `<otherwise/>` (если он имеется), будут применены, если все атрибуты условий элемента `<when/>` имеют значение `false`.</span><span class="sxs-lookup"><span data-stu-id="3df60-130">Policies enclosed within the `<otherwise/>` element, if present, will be applied if all of the `<when/>` element condition attributes are `false`.</span></span>  
  
### <a name="examples"></a><span data-ttu-id="3df60-131">Примеры</span><span class="sxs-lookup"><span data-stu-id="3df60-131">Examples</span></span>  
  
####  <span data-ttu-id="3df60-132"><a name="ChooseExample"></a> Пример</span><span class="sxs-lookup"><span data-stu-id="3df60-132"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="3df60-133">В следующем примере демонстрируется политика [set-variable](api-management-advanced-policies.md#set-variable) и две политики управления потоками.</span><span class="sxs-lookup"><span data-stu-id="3df60-133">The following example demonstrates a [set-variable](api-management-advanced-policies.md#set-variable) policy and two control flow policies.</span></span>  
  
 <span data-ttu-id="3df60-134">Политика задания переменной находится в разделе inbound и создает логическую переменную [контекста](api-management-policy-expressions.md#ContextVariables) `isMobile`, которой присваивается значение true, если заголовок запроса `User-Agent` содержит текст `iPad` или `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="3df60-134">The set variable policy is in the inbound section and creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set to true if the `User-Agent` request header contains the text `iPad` or `iPhone`.</span></span>  
  
 <span data-ttu-id="3df60-135">Первая политика управления потоками также находится в разделе inbound и условно применяет одну из двух политик [установки параметра строки запроса](api-management-transformation-policies.md#SetQueryStringParameter) в зависимости от значения переменной контекста `isMobile`.</span><span class="sxs-lookup"><span data-stu-id="3df60-135">The first control flow policy is also in the inbound section, and conditionally applies one of two [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policies depending on the value of the `isMobile` context variable.</span></span>  
  
 <span data-ttu-id="3df60-136">Вторая политика управления потоками находится в разделе outbound и условно применяет политику [преобразования XML в JSON](api-management-transformation-policies.md#ConvertXMLtoJSON), если переменная `isMobile` имеет значение `true`.</span><span class="sxs-lookup"><span data-stu-id="3df60-136">The second control flow policy is in the outbound section and conditionally applies the [Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) policy when `isMobile` is set to `true`.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <set-variable name="isMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
        <base />  
        <choose>  
            <when condition="@(context.Variables.GetValueOrDefault<bool>("isMobile"))">  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>true</value>  
                </set-query-parameter>  
            </when>  
            <otherwise>  
                <set-query-parameter name="mobile" exists-action="override">  
                    <value>false</value>  
                </set-query-parameter>  
            </otherwise>  
        </choose>  
    </inbound>  
    <outbound>  
        <base />  
        <choose>  
            <when condition="@(context.GetValueOrDefault<bool>("isMobile"))">  
                <xml-to-json kind="direct" apply="always" consider-accept-header="false"/>  
            </when>  
        </choose>  
    </outbound>  
</policies>  
```  
  
#### <a name="example"></a><span data-ttu-id="3df60-137">Пример</span><span class="sxs-lookup"><span data-stu-id="3df60-137">Example</span></span>  
 <span data-ttu-id="3df60-138">В этом примере показано, как выполнить фильтрацию содержимого путем удаления элементов данных из ответа, полученного из внутренней службы при использовании продукта `Starter`.</span><span class="sxs-lookup"><span data-stu-id="3df60-138">This example shows how to perform content filtering by removing data elements from the response received from the backend service when using the `Starter` product.</span></span> <span data-ttu-id="3df60-139">Пример настройки и использования этой политики см. в видео [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Cloud Cover, эпизод 177: возможности управления API с Владом Виноградским) с отметки времени 34:30.</span><span class="sxs-lookup"><span data-stu-id="3df60-139">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 34:30.</span></span> <span data-ttu-id="3df60-140">Начните с отметки времени 31:50, чтобы узнать общие сведения о [прогнозном API Dark Sky](https://developer.forecast.io/), используемом для этого примера.</span><span class="sxs-lookup"><span data-stu-id="3df60-140">Start  at 31:50 to see an overview of [The Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into the outbound section to remove a number of data elements from the response received from the backend service based on the name of the api product -->  
<choose>  
  <when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals("Starter"))">  
    <set-body>@{  
        var response = context.Response.Body.As<JObject>();  
        foreach (var key in new [] {"minutely", "hourly", "daily", "flags"}) {  
          response.Property (key).Remove ();  
        }  
        return response.ToString();  
      }  
    </set-body>  
  </when>  
</choose>  
```  
  
### <a name="elements"></a><span data-ttu-id="3df60-141">Элементы</span><span class="sxs-lookup"><span data-stu-id="3df60-141">Elements</span></span>  
  
|<span data-ttu-id="3df60-142">Элемент</span><span class="sxs-lookup"><span data-stu-id="3df60-142">Element</span></span>|<span data-ttu-id="3df60-143">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-143">Description</span></span>|<span data-ttu-id="3df60-144">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-144">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="3df60-145">choose</span><span class="sxs-lookup"><span data-stu-id="3df60-145">choose</span></span>|<span data-ttu-id="3df60-146">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="3df60-146">Root element.</span></span>|<span data-ttu-id="3df60-147">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-147">Yes</span></span>|  
|<span data-ttu-id="3df60-148">when</span><span class="sxs-lookup"><span data-stu-id="3df60-148">when</span></span>|<span data-ttu-id="3df60-149">Условие для применения в частях `if` или `ifelse` политики `choose`.</span><span class="sxs-lookup"><span data-stu-id="3df60-149">The condition to use for the `if` or `ifelse` parts of the `choose` policy.</span></span> <span data-ttu-id="3df60-150">Если политика `choose` имеет несколько разделов `when`, они вычисляются последовательно.</span><span class="sxs-lookup"><span data-stu-id="3df60-150">If the `choose` policy has multiple `when` sections, they are evaluated sequentially.</span></span> <span data-ttu-id="3df60-151">Когда `condition` элемента when принимает значение `true`, никакие последующие условия `when` не вычисляются.</span><span class="sxs-lookup"><span data-stu-id="3df60-151">Once the `condition` of a when element evaluates to `true`, no further `when` conditions are evaluated.</span></span>|<span data-ttu-id="3df60-152">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-152">Yes</span></span>|  
|<span data-ttu-id="3df60-153">otherwise</span><span class="sxs-lookup"><span data-stu-id="3df60-153">otherwise</span></span>|<span data-ttu-id="3df60-154">Содержит фрагмент кода политики, который используется в том случае, если ни одно из условий `when` не принимает значение `true`.</span><span class="sxs-lookup"><span data-stu-id="3df60-154">Contains the policy snippet to be used if none of the `when` conditions evaluate to `true`.</span></span>|<span data-ttu-id="3df60-155">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-155">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3df60-156">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="3df60-156">Attributes</span></span>  
  
|<span data-ttu-id="3df60-157">Атрибут</span><span class="sxs-lookup"><span data-stu-id="3df60-157">Attribute</span></span>|<span data-ttu-id="3df60-158">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-158">Description</span></span>|<span data-ttu-id="3df60-159">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-159">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="3df60-160">condition="Логическое выражение &#124; Логическая константа"</span><span class="sxs-lookup"><span data-stu-id="3df60-160">condition="Boolean expression &#124; Boolean constant"</span></span>|<span data-ttu-id="3df60-161">Логическое выражение или константа, которую необходимо вычислить, когда вычисляется правило политики, содержащей `when`.</span><span class="sxs-lookup"><span data-stu-id="3df60-161">The Boolean expression or constant to evaluated when the containing `when` policy statement is evaluated.</span></span>|<span data-ttu-id="3df60-162">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-162">Yes</span></span>|  
  
###  <span data-ttu-id="3df60-163"><a name="ChooseUsage"></a> Использование</span><span class="sxs-lookup"><span data-stu-id="3df60-163"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="3df60-164">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3df60-164">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3df60-165">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="3df60-165">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="3df60-166">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="3df60-166">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="3df60-167"><a name="ForwardRequest"></a> Перенаправляющий запрос</span><span class="sxs-lookup"><span data-stu-id="3df60-167"><a name="ForwardRequest"></a> Forward request</span></span>  
 <span data-ttu-id="3df60-168">Политика `forward-request` перенаправляет входящий запрос во внутреннюю службу, указанную в [контексте](api-management-policy-expressions.md#ContextVariables) запроса.</span><span class="sxs-lookup"><span data-stu-id="3df60-168">The `forward-request` policy forwards the incoming request to the backend service specified in the request [context](api-management-policy-expressions.md#ContextVariables).</span></span> <span data-ttu-id="3df60-169">URL-адрес внутренней службы, заданный в [параметрах](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) API, может быть изменен с помощью политики [задания внутренней службы](api-management-transformation-policies.md).</span><span class="sxs-lookup"><span data-stu-id="3df60-169">The backend service URL is specified in the API  [settings](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) and can be changed using the [set backend service](api-management-transformation-policies.md) policy.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="3df60-170">Удаление этой политики приводит к тому, что запрос не перенаправляется во внутреннюю службу и политики в разделе outbound вычисляются сразу после успешного завершения обработки политик в разделе inbound.</span><span class="sxs-lookup"><span data-stu-id="3df60-170">Removing this policy results in the request not being forwarded to the backend service and the policies in the outbound section are evaluated immediately upon the successful completion of the policies in the inbound section.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3df60-171">Правило политики</span><span class="sxs-lookup"><span data-stu-id="3df60-171">Policy statement</span></span>  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a><span data-ttu-id="3df60-172">Примеры</span><span class="sxs-lookup"><span data-stu-id="3df60-172">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="3df60-173">Пример</span><span class="sxs-lookup"><span data-stu-id="3df60-173">Example</span></span>  
 <span data-ttu-id="3df60-174">Следующая политика уровня API перенаправляет все запросы к внутренней службе с интервалом времени ожидания 60 секунд.</span><span class="sxs-lookup"><span data-stu-id="3df60-174">The following API level policy forwards all requests to the backend service with a timeout interval of 60 seconds.</span></span>  
  
```xml  
<!-- api level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="60"/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="3df60-175">Пример</span><span class="sxs-lookup"><span data-stu-id="3df60-175">Example</span></span>  
 <span data-ttu-id="3df60-176">Эта политика уровня операций использует элемент `base`, чтобы наследовать внутреннюю политику от родительской области уровня API.</span><span class="sxs-lookup"><span data-stu-id="3df60-176">This operation level policy uses the `base` element to inherit the backend policy from the parent API level scope.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <base/>  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="3df60-177">Пример</span><span class="sxs-lookup"><span data-stu-id="3df60-177">Example</span></span>  
 <span data-ttu-id="3df60-178">Эта политика уровня операций явным образом перенаправляет все запросы во внутреннюю службу с временем ожидания 120 секунд и не наследует родительскую политику уровня API.</span><span class="sxs-lookup"><span data-stu-id="3df60-178">This operation level policy explicitly forwards all requests to the backend service with a timeout of 120 and does not inherit the parent API level backend policy.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="120"/>   
        <!-- effective policy. note the absence of <base/> -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="3df60-179">Пример</span><span class="sxs-lookup"><span data-stu-id="3df60-179">Example</span></span>  
 <span data-ttu-id="3df60-180">Эта политика уровня операций не перенаправляет запросы во внутреннюю службу.</span><span class="sxs-lookup"><span data-stu-id="3df60-180">This operation level policy does not forward requests to the backend service.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <!-- no forwarding to backend -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="3df60-181">Элементы</span><span class="sxs-lookup"><span data-stu-id="3df60-181">Elements</span></span>  
  
|<span data-ttu-id="3df60-182">Элемент</span><span class="sxs-lookup"><span data-stu-id="3df60-182">Element</span></span>|<span data-ttu-id="3df60-183">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-183">Description</span></span>|<span data-ttu-id="3df60-184">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-184">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="3df60-185">forward-request</span><span class="sxs-lookup"><span data-stu-id="3df60-185">forward-request</span></span>|<span data-ttu-id="3df60-186">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="3df60-186">Root element.</span></span>|<span data-ttu-id="3df60-187">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-187">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3df60-188">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="3df60-188">Attributes</span></span>  
  
|<span data-ttu-id="3df60-189">Атрибут</span><span class="sxs-lookup"><span data-stu-id="3df60-189">Attribute</span></span>|<span data-ttu-id="3df60-190">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-190">Description</span></span>|<span data-ttu-id="3df60-191">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-191">Required</span></span>|<span data-ttu-id="3df60-192">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="3df60-192">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="3df60-193">timeout="целое число"</span><span class="sxs-lookup"><span data-stu-id="3df60-193">timeout="integer"</span></span>|<span data-ttu-id="3df60-194">Интервал времени ожидания в секундах до того, как вызов, адресованный внутренней службе, завершится сбоем.</span><span class="sxs-lookup"><span data-stu-id="3df60-194">The timeout interval in seconds before the call to the backend service fails.</span></span>|<span data-ttu-id="3df60-195">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-195">No</span></span>|<span data-ttu-id="3df60-196">Время ожидания отсутствует</span><span class="sxs-lookup"><span data-stu-id="3df60-196">No timeout</span></span>|  
|<span data-ttu-id="3df60-197">follow-redirects="true &#124; false"</span><span class="sxs-lookup"><span data-stu-id="3df60-197">follow-redirects="true &#124; false"</span></span>|<span data-ttu-id="3df60-198">Указывает, что происходит с перенаправлениями от внутренней службы: шлюз выполняет их или они возвращаются вызывающему объекту.</span><span class="sxs-lookup"><span data-stu-id="3df60-198">Specifies whether redirects from the backend service are followed by the gateway or returned to the caller.</span></span>|<span data-ttu-id="3df60-199">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-199">No</span></span>|<span data-ttu-id="3df60-200">нет</span><span class="sxs-lookup"><span data-stu-id="3df60-200">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3df60-201">Использование</span><span class="sxs-lookup"><span data-stu-id="3df60-201">Usage</span></span>  
 <span data-ttu-id="3df60-202">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3df60-202">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3df60-203">**Разделы политики:** backend.</span><span class="sxs-lookup"><span data-stu-id="3df60-203">**Policy sections:** backend</span></span>  
  
-   <span data-ttu-id="3df60-204">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="3df60-204">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="3df60-205"><a name="LimitConcurrency"></a> Ограничение параллелизма</span><span class="sxs-lookup"><span data-stu-id="3df60-205"><a name="LimitConcurrency"></a> Limit concurrency</span></span>  
 <span data-ttu-id="3df60-206">Политика `limit-concurrency` не позволяет, чтобы заключенные политики одновременно выполнялись запросами, количество которых выше указанного.</span><span class="sxs-lookup"><span data-stu-id="3df60-206">The `limit-concurrency` policy prevents enclosed policies from executing by more than the specified number of requests at a given time.</span></span> <span data-ttu-id="3df60-207">Если превышено пороговое значение, новые запросы добавляются в очередь, пока не будет достигнута максимальная ее длина.</span><span class="sxs-lookup"><span data-stu-id="3df60-207">Upon exceeding the threshold, new requests are added to a queue, until the maximum queue length is achieved.</span></span> <span data-ttu-id="3df60-208">Когда очередь заполнится, новые запросы немедленно завершатся ошибкой.</span><span class="sxs-lookup"><span data-stu-id="3df60-208">Upon queue exhaustion, new requests will fail immediately.</span></span>
  
###  <span data-ttu-id="3df60-209"><a name="LimitConcurrencyStatement"></a> Правило политики</span><span class="sxs-lookup"><span data-stu-id="3df60-209"><a name="LimitConcurrencyStatement"></a> Policy statement</span></span>  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a><span data-ttu-id="3df60-210">Примеры</span><span class="sxs-lookup"><span data-stu-id="3df60-210">Examples</span></span>  
  
####  <span data-ttu-id="3df60-211"><a name="ChooseExample"></a> Пример</span><span class="sxs-lookup"><span data-stu-id="3df60-211"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="3df60-212">Ниже приведен пример, как ограничить число запросов, пересылаемых в серверную часть, на основе значения переменной контекста.</span><span class="sxs-lookup"><span data-stu-id="3df60-212">The following example demonstrates how to limit number of requests forwarded to a backend based on the value of a context variable.</span></span>
 
```xml  
<policies>
  <inbound>…</inbound>
  <backend>
    <limit-concurrency key="@((string)context.Variables["connectionId"])" max-count="3" timeout="60">
      <forward-request timeout="120"/>
    <limit-concurrency/>
  </backend>
  <outbound>…</outbound>
</policies>
```

### <a name="elements"></a><span data-ttu-id="3df60-213">Элементы</span><span class="sxs-lookup"><span data-stu-id="3df60-213">Elements</span></span>  
  
|<span data-ttu-id="3df60-214">Элемент</span><span class="sxs-lookup"><span data-stu-id="3df60-214">Element</span></span>|<span data-ttu-id="3df60-215">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-215">Description</span></span>|<span data-ttu-id="3df60-216">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-216">Required</span></span>|  
|-------------|-----------------|--------------|    
|<span data-ttu-id="3df60-217">limit-concurrency</span><span class="sxs-lookup"><span data-stu-id="3df60-217">limit-concurrency</span></span>|<span data-ttu-id="3df60-218">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="3df60-218">Root element.</span></span>|<span data-ttu-id="3df60-219">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3df60-220">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="3df60-220">Attributes</span></span>  
  
|<span data-ttu-id="3df60-221">Атрибут</span><span class="sxs-lookup"><span data-stu-id="3df60-221">Attribute</span></span>|<span data-ttu-id="3df60-222">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-222">Description</span></span>|<span data-ttu-id="3df60-223">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-223">Required</span></span>|<span data-ttu-id="3df60-224">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="3df60-224">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="3df60-225">key</span><span class="sxs-lookup"><span data-stu-id="3df60-225">key</span></span>|<span data-ttu-id="3df60-226">Строка.</span><span class="sxs-lookup"><span data-stu-id="3df60-226">A string.</span></span> <span data-ttu-id="3df60-227">Допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="3df60-227">Expression allowed.</span></span> <span data-ttu-id="3df60-228">Задает область параллелизма.</span><span class="sxs-lookup"><span data-stu-id="3df60-228">Specifies the concurrency scope.</span></span> <span data-ttu-id="3df60-229">Используется несколькими политиками.</span><span class="sxs-lookup"><span data-stu-id="3df60-229">Can be shared by multiple policies.</span></span>|<span data-ttu-id="3df60-230">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-230">Yes</span></span>|<span data-ttu-id="3df60-231">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3df60-231">N/A</span></span>|  
|<span data-ttu-id="3df60-232">max-count</span><span class="sxs-lookup"><span data-stu-id="3df60-232">max-count</span></span>|<span data-ttu-id="3df60-233">Целое число.</span><span class="sxs-lookup"><span data-stu-id="3df60-233">An integer.</span></span> <span data-ttu-id="3df60-234">Указывает максимальное количество запросов для ввода политики.</span><span class="sxs-lookup"><span data-stu-id="3df60-234">Specifies a maximum number of requests that are allowed to enter the policy.</span></span>|<span data-ttu-id="3df60-235">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-235">Yes</span></span>|<span data-ttu-id="3df60-236">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3df60-236">N/A</span></span>|  
|<span data-ttu-id="3df60-237">timeout</span><span class="sxs-lookup"><span data-stu-id="3df60-237">timeout</span></span>|<span data-ttu-id="3df60-238">Целое число.</span><span class="sxs-lookup"><span data-stu-id="3df60-238">An integer.</span></span> <span data-ttu-id="3df60-239">Допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="3df60-239">Expression allowed.</span></span> <span data-ttu-id="3df60-240">Указывает количество секунд, которые запрос ожидает для входа в область, прежде чем произойдет ошибка "403 — слишком много запросов".</span><span class="sxs-lookup"><span data-stu-id="3df60-240">Specifies the number of seconds a request should wait to enter a scope before failing with "403 Too Many Requests"</span></span>|<span data-ttu-id="3df60-241">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-241">No</span></span>|<span data-ttu-id="3df60-242">Infinity</span><span class="sxs-lookup"><span data-stu-id="3df60-242">Infinity</span></span>|  
|<span data-ttu-id="3df60-243">max-queue-length</span><span class="sxs-lookup"><span data-stu-id="3df60-243">max-queue-length</span></span>|<span data-ttu-id="3df60-244">Целое число.</span><span class="sxs-lookup"><span data-stu-id="3df60-244">An integer.</span></span> <span data-ttu-id="3df60-245">Допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="3df60-245">Expression allowed.</span></span> <span data-ttu-id="3df60-246">Указывает максимальную длину очереди.</span><span class="sxs-lookup"><span data-stu-id="3df60-246">Specifies the maximum queue length.</span></span> <span data-ttu-id="3df60-247">При попытке получить доступ к этой политике входящие запросы немедленно завершатся ошибкой "403 — слишком много запросов" сразу после заполнения очереди.</span><span class="sxs-lookup"><span data-stu-id="3df60-247">Incoming requests trying to enter this policy will be terminated with “403 Too Many Requests” immediately when the queue is exhausted.</span></span>|<span data-ttu-id="3df60-248">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-248">No</span></span>|<span data-ttu-id="3df60-249">Infinity</span><span class="sxs-lookup"><span data-stu-id="3df60-249">Infinity</span></span>|  
  
###  <span data-ttu-id="3df60-250"><a name="ChooseUsage"></a> Использование</span><span class="sxs-lookup"><span data-stu-id="3df60-250"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="3df60-251">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3df60-251">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3df60-252">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="3df60-252">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="3df60-253">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="3df60-253">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="3df60-254"><a name="log-to-eventhub"></a> Регистрация в концентраторе событий</span><span class="sxs-lookup"><span data-stu-id="3df60-254"><a name="log-to-eventhub"></a> Log to Event Hub</span></span>  
 <span data-ttu-id="3df60-255">Политика `log-to-eventhub` отправляет сообщения в определенном формате концентратору событий, который указан сущностью Logger.</span><span class="sxs-lookup"><span data-stu-id="3df60-255">The `log-to-eventhub` policy sends messages in the specified format to an Event Hub defined by a Logger entity.</span></span> <span data-ttu-id="3df60-256">Как и предполагает ее имя, эта политика используется для сохранения контекстных сведений выбранного запроса или ответа для сетевого или автономного анализа.</span><span class="sxs-lookup"><span data-stu-id="3df60-256">As its name implies, the policy is used for saving selected request or response context information for online or offline analysis.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="3df60-257">Пошаговое руководство по настройке концентратора событий и ведению журнала событий см. в статье [Как регистрировать события в концентраторах событий Azure в службе управления Azure API](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="3df60-257">For a step-by-step guide on configuring an event hub and logging events, see [How to log API Management events with Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3df60-258">Правило политики</span><span class="sxs-lookup"><span data-stu-id="3df60-258">Policy statement</span></span>  
  
```xml  
<log-to-eventhub logger-id="id of the logger entity" partition-id="index of the partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string to be logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a><span data-ttu-id="3df60-259">Пример</span><span class="sxs-lookup"><span data-stu-id="3df60-259">Example</span></span>  
 <span data-ttu-id="3df60-260">Любую строку можно использовать как значение для регистрации в концентраторе событий.</span><span class="sxs-lookup"><span data-stu-id="3df60-260">Any string can be used as the value to be logged in Event Hubs.</span></span> <span data-ttu-id="3df60-261">В этом примере дата и время, имя службы развертывания, идентификатор запроса, IP-адрес и имя операции для всех входящих вызовов записываются в средство ведения журналов в концентраторе событий, зарегистрированное с помощью идентификатора `contoso-logger`.</span><span class="sxs-lookup"><span data-stu-id="3df60-261">In this example the date and time, deployment service name, request id, ip address, and operation name for all inbound calls are logged to the event hub Logger registered with the `contoso-logger` id.</span></span>  
  
```xml  
<policies>  
  <inbound>  
    <log-to-eventhub logger-id ='contoso-logger'>  
      @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name) )   
    </log-to-eventhub>  
  </inbound>  
  <outbound>          
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="3df60-262">Элементы</span><span class="sxs-lookup"><span data-stu-id="3df60-262">Elements</span></span>  
  
|<span data-ttu-id="3df60-263">Элемент</span><span class="sxs-lookup"><span data-stu-id="3df60-263">Element</span></span>|<span data-ttu-id="3df60-264">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-264">Description</span></span>|<span data-ttu-id="3df60-265">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-265">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="3df60-266">log-to-eventhub</span><span class="sxs-lookup"><span data-stu-id="3df60-266">log-to-eventhub</span></span>|<span data-ttu-id="3df60-267">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="3df60-267">Root element.</span></span> <span data-ttu-id="3df60-268">Значение этого элемента — это строка, которая будет зарегистрирована в концентраторе событий.</span><span class="sxs-lookup"><span data-stu-id="3df60-268">The value of this element is the string to log to your event hub.</span></span>|<span data-ttu-id="3df60-269">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-269">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3df60-270">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="3df60-270">Attributes</span></span>  
  
|<span data-ttu-id="3df60-271">Атрибут</span><span class="sxs-lookup"><span data-stu-id="3df60-271">Attribute</span></span>|<span data-ttu-id="3df60-272">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-272">Description</span></span>|<span data-ttu-id="3df60-273">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-273">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="3df60-274">logger-id</span><span class="sxs-lookup"><span data-stu-id="3df60-274">logger-id</span></span>|<span data-ttu-id="3df60-275">Идентификатор средства ведения журнала, зарегистрированного в службе управления API.</span><span class="sxs-lookup"><span data-stu-id="3df60-275">The id of the Logger registered with your API Management service.</span></span>|<span data-ttu-id="3df60-276">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-276">Yes</span></span>|  
|<span data-ttu-id="3df60-277">partition-id</span><span class="sxs-lookup"><span data-stu-id="3df60-277">partition-id</span></span>|<span data-ttu-id="3df60-278">Указывает индекс раздела, куда должны отправляться сообщения.</span><span class="sxs-lookup"><span data-stu-id="3df60-278">Specifies the index of the partition where messages are sent.</span></span>|<span data-ttu-id="3df60-279">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="3df60-279">Optional.</span></span> <span data-ttu-id="3df60-280">Этот атрибут не может использоваться, если используется `partition-key`.</span><span class="sxs-lookup"><span data-stu-id="3df60-280">This attribute may not be used if `partition-key` is used.</span></span>|  
|<span data-ttu-id="3df60-281">partition-key</span><span class="sxs-lookup"><span data-stu-id="3df60-281">partition-key</span></span>|<span data-ttu-id="3df60-282">Указывает значение, используемое для назначения секции при отправке сообщений.</span><span class="sxs-lookup"><span data-stu-id="3df60-282">Specifies the value used for partition assignment when messages are sent.</span></span>|<span data-ttu-id="3df60-283">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="3df60-283">Optional.</span></span> <span data-ttu-id="3df60-284">Этот атрибут не может использоваться, если используется `partition-id`.</span><span class="sxs-lookup"><span data-stu-id="3df60-284">This attribute may not be used if `partition-id` is used.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3df60-285">Использование</span><span class="sxs-lookup"><span data-stu-id="3df60-285">Usage</span></span>  
 <span data-ttu-id="3df60-286">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3df60-286">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3df60-287">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="3df60-287">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="3df60-288">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="3df60-288">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="3df60-289"><a name="mock-response"></a> Макетирование ответа</span><span class="sxs-lookup"><span data-stu-id="3df60-289"><a name="mock-response"></a> Mock response</span></span>  
<span data-ttu-id="3df60-290">Политика `mock-response`, как следует из имени, используется для макетирования интерфейсов API и операций.</span><span class="sxs-lookup"><span data-stu-id="3df60-290">The `mock-response`, as the name implies, is used to mock APIs and operations.</span></span> <span data-ttu-id="3df60-291">Она прекращает выполнение конвейера и возвращает макетированный ответ вызывающему объекту.</span><span class="sxs-lookup"><span data-stu-id="3df60-291">It aborts normal pipeline execution and returns a mocked response to the caller.</span></span> <span data-ttu-id="3df60-292">Эта политика всегда пытается вернуть ответы наивысшего качества.</span><span class="sxs-lookup"><span data-stu-id="3df60-292">The policy always tries to return responses of highest fidelity.</span></span> <span data-ttu-id="3df60-293">При возможности, она предпочитает примеры содержимого ответа.</span><span class="sxs-lookup"><span data-stu-id="3df60-293">It prefers response content examples, whenever available.</span></span> <span data-ttu-id="3df60-294">Она создает примеры ответов из схем, если схемы указаны, а примеры — нет.</span><span class="sxs-lookup"><span data-stu-id="3df60-294">It generates sample responses from schemas, when schemas are provided and examples are not.</span></span> <span data-ttu-id="3df60-295">Если не найдены ни примеры, ни схемы, возвращаются ответы без содержимого.</span><span class="sxs-lookup"><span data-stu-id="3df60-295">If neither examples or schemas are found, responses with no content are returned.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="3df60-296">Правило политики</span><span class="sxs-lookup"><span data-stu-id="3df60-296">Policy statement</span></span>  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="3df60-297">Примеры</span><span class="sxs-lookup"><span data-stu-id="3df60-297">Examples</span></span>  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, the content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, the content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a><span data-ttu-id="3df60-298">Элементы</span><span class="sxs-lookup"><span data-stu-id="3df60-298">Elements</span></span>  
  
|<span data-ttu-id="3df60-299">Элемент</span><span class="sxs-lookup"><span data-stu-id="3df60-299">Element</span></span>|<span data-ttu-id="3df60-300">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-300">Description</span></span>|<span data-ttu-id="3df60-301">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-301">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="3df60-302">mock-response</span><span class="sxs-lookup"><span data-stu-id="3df60-302">mock-response</span></span>|<span data-ttu-id="3df60-303">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="3df60-303">Root element.</span></span>|<span data-ttu-id="3df60-304">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-304">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3df60-305">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="3df60-305">Attributes</span></span>  
  
|<span data-ttu-id="3df60-306">Атрибут</span><span class="sxs-lookup"><span data-stu-id="3df60-306">Attribute</span></span>|<span data-ttu-id="3df60-307">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-307">Description</span></span>|<span data-ttu-id="3df60-308">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-308">Required</span></span>|<span data-ttu-id="3df60-309">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="3df60-309">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="3df60-310">status-code</span><span class="sxs-lookup"><span data-stu-id="3df60-310">status-code</span></span>|<span data-ttu-id="3df60-311">Указывает код состояния ответа и позволяет выбрать соответствующий пример или схему.</span><span class="sxs-lookup"><span data-stu-id="3df60-311">Specifies response status code and is used to select corresponding example or schema.</span></span>|<span data-ttu-id="3df60-312">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-312">No</span></span>|<span data-ttu-id="3df60-313">200</span><span class="sxs-lookup"><span data-stu-id="3df60-313">200</span></span>|  
|<span data-ttu-id="3df60-314">content-type</span><span class="sxs-lookup"><span data-stu-id="3df60-314">content-type</span></span>|<span data-ttu-id="3df60-315">Указывает значение заголовка ответа `Content-Type` и позволяет выбрать соответствующий пример или схему.</span><span class="sxs-lookup"><span data-stu-id="3df60-315">Specifies `Content-Type` response header value and is used to select corresponding example or schema.</span></span>|<span data-ttu-id="3df60-316">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-316">No</span></span>|<span data-ttu-id="3df60-317">None</span><span class="sxs-lookup"><span data-stu-id="3df60-317">None</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3df60-318">Использование</span><span class="sxs-lookup"><span data-stu-id="3df60-318">Usage</span></span>  
 <span data-ttu-id="3df60-319">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3df60-319">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3df60-320">**Разделы политики:** inbound, outbound, on-error.</span><span class="sxs-lookup"><span data-stu-id="3df60-320">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="3df60-321">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="3df60-321">**Policy scopes:** all scopes</span></span>

##  <span data-ttu-id="3df60-322"><a name="Retry"></a> Повтор</span><span class="sxs-lookup"><span data-stu-id="3df60-322"><a name="Retry"></a> Retry</span></span>  
 <span data-ttu-id="3df60-323">Политика `retry` выполняет свои дочерние политики один раз и затем повторяет их выполнение до тех пор, пока параметр `condition` попыток не примет значение `false` или параметр `count` попыток не будет исчерпан.</span><span class="sxs-lookup"><span data-stu-id="3df60-323">The             `retry` policy executes its child policies once and then retries their execution until the retry `condition` becomes            `false` or retry            `count` is exhausted.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3df60-324">Правило политики</span><span class="sxs-lookup"><span data-stu-id="3df60-324">Policy statement</span></span>  
  
```xml  
  
<retry  
    condition="boolean expression or literal"  
    count="number of retry attempts"  
    interval="retry interval in seconds"  
    max-interval="maximum retry interval in seconds"  
    delta="retry interval delta in seconds"  
    first-fast-retry="boolean expression or literal">  
        <!-- One or more child policies. No restrictions -->  
</retry>  
  
```  
  
### <a name="example"></a><span data-ttu-id="3df60-325">Пример</span><span class="sxs-lookup"><span data-stu-id="3df60-325">Example</span></span>  
 <span data-ttu-id="3df60-326">В следующем примере перенаправление запроса повторяется до 10 раз, следуя экспоненциальному алгоритму повторения.</span><span class="sxs-lookup"><span data-stu-id="3df60-326">In the following example request forewarding is retried up to ten times using exponential retry algorithm.</span></span> <span data-ttu-id="3df60-327">Так как `first-fast-retry` имеет значение false, все попытки повтора выполняются в соответствии с экспоненциальным алгоритмом повторения.</span><span class="sxs-lookup"><span data-stu-id="3df60-327">Since                    `first-fast-retry` is set to false, all retry attempts are subject to the exponsntial retry algorithm.</span></span>  
  
```xml  
  
<retry  
    condition="@(context.Response.StatusCode == 500)"  
    count="10"  
    interval="10"  
    max-interval="100"  
    delta="10"  
    first-fast-retry="false">  
        <forward-request />  
</retry>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="3df60-328">Элементы</span><span class="sxs-lookup"><span data-stu-id="3df60-328">Elements</span></span>  
  
|<span data-ttu-id="3df60-329">Элемент</span><span class="sxs-lookup"><span data-stu-id="3df60-329">Element</span></span>|<span data-ttu-id="3df60-330">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-330">Description</span></span>|<span data-ttu-id="3df60-331">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-331">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="3df60-332">retry</span><span class="sxs-lookup"><span data-stu-id="3df60-332">retry</span></span>|<span data-ttu-id="3df60-333">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="3df60-333">Root element.</span></span> <span data-ttu-id="3df60-334">Может содержать любые другие политики в качестве дочерних элементов.</span><span class="sxs-lookup"><span data-stu-id="3df60-334">May contain any other policies as its child elements.</span></span>|<span data-ttu-id="3df60-335">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-335">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3df60-336">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="3df60-336">Attributes</span></span>  
  
|<span data-ttu-id="3df60-337">Атрибут</span><span class="sxs-lookup"><span data-stu-id="3df60-337">Attribute</span></span>|<span data-ttu-id="3df60-338">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-338">Description</span></span>|<span data-ttu-id="3df60-339">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-339">Required</span></span>|<span data-ttu-id="3df60-340">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="3df60-340">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="3df60-341">condition</span><span class="sxs-lookup"><span data-stu-id="3df60-341">condition</span></span>|<span data-ttu-id="3df60-342">Логический литерал или [выражение](api-management-policy-expressions.md), указывающее, что нужно сделать: прекратить повторные попытки (`false`) или продолжить (`true`).</span><span class="sxs-lookup"><span data-stu-id="3df60-342">A boolean literal or [expression](api-management-policy-expressions.md) specifying if retries should be stopped (`false`) or continued (`true`).</span></span>|<span data-ttu-id="3df60-343">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-343">Yes</span></span>|<span data-ttu-id="3df60-344">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3df60-344">N/A</span></span>|  
|<span data-ttu-id="3df60-345">count</span><span class="sxs-lookup"><span data-stu-id="3df60-345">count</span></span>|<span data-ttu-id="3df60-346">Положительное число, определяющее максимальное число повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="3df60-346">A positive number specifying the maximum number of retries to attempt.</span></span>|<span data-ttu-id="3df60-347">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-347">Yes</span></span>|<span data-ttu-id="3df60-348">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3df60-348">N/A</span></span>|  
|<span data-ttu-id="3df60-349">interval</span><span class="sxs-lookup"><span data-stu-id="3df60-349">interval</span></span>|<span data-ttu-id="3df60-350">Положительное значение в секундах, определяющее интервал ожидания между повторными попытками.</span><span class="sxs-lookup"><span data-stu-id="3df60-350">A positive number in seconds specifying the wait interval between the retry attempts.</span></span>|<span data-ttu-id="3df60-351">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-351">Yes</span></span>|<span data-ttu-id="3df60-352">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3df60-352">N/A</span></span>|  
|<span data-ttu-id="3df60-353">max-interval</span><span class="sxs-lookup"><span data-stu-id="3df60-353">max-interval</span></span>|<span data-ttu-id="3df60-354">Положительное значение в секундах, определяющее максимальный интервал ожидания между повторными попытками.</span><span class="sxs-lookup"><span data-stu-id="3df60-354">A positive number in seconds specifying the maximum wait interval between the retry attempts.</span></span> <span data-ttu-id="3df60-355">Оно используется для реализации экспоненциального алгоритма повторения.</span><span class="sxs-lookup"><span data-stu-id="3df60-355">It is used to implement an exponential retry algorithm.</span></span>|<span data-ttu-id="3df60-356">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-356">No</span></span>|<span data-ttu-id="3df60-357">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3df60-357">N/A</span></span>|  
|<span data-ttu-id="3df60-358">delta</span><span class="sxs-lookup"><span data-stu-id="3df60-358">delta</span></span>|<span data-ttu-id="3df60-359">Положительное значение в секундах, определяющее увеличение интервала ожидания.</span><span class="sxs-lookup"><span data-stu-id="3df60-359">A positive number in seconds specifying the wait interval increment.</span></span> <span data-ttu-id="3df60-360">Используется для реализации линейного и экспоненциального алгоритмов повторения.</span><span class="sxs-lookup"><span data-stu-id="3df60-360">It is used to implement the linear and exponential retry algorithms.</span></span>|<span data-ttu-id="3df60-361">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-361">No</span></span>|<span data-ttu-id="3df60-362">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3df60-362">N/A</span></span>|  
|<span data-ttu-id="3df60-363">first-fast-retry</span><span class="sxs-lookup"><span data-stu-id="3df60-363">first-fast-retry</span></span>|<span data-ttu-id="3df60-364">Если присвоено значение `true`, первая попытка повтора выполняется немедленно.</span><span class="sxs-lookup"><span data-stu-id="3df60-364">If set to                                    `true` , the first retry attempt is performed immediately.</span></span>|<span data-ttu-id="3df60-365">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-365">No</span></span>|`false`|  
  
> [!NOTE]
>  <span data-ttu-id="3df60-366">Если указан только параметр `interval`, попытки выполняются с **фиксированным** интервалом.</span><span class="sxs-lookup"><span data-stu-id="3df60-366">When only the `interval` is specified, **fixed** interval retries are performed.</span></span>  
>  <span data-ttu-id="3df60-367">Если указаны параметры `interval` и `delta`, применяется **линейный** алгоритм повторения, где время ожидания между повторениями вычисляется согласно формуле `interval + (count - 1)*delta`.</span><span class="sxs-lookup"><span data-stu-id="3df60-367">When only the `interval` and `delta` are specified, a **linear** interval retry algorithm is used, where wait time between retries is calculated according the following formula - `interval + (count - 1)*delta`.</span></span>  
>  <span data-ttu-id="3df60-368">Если указаны параметры `interval`, `max-interval` и `delta`, применяется **экспоненциальный** алгоритм повторения, где время ожидания между повторениями растет экспоненциально от значения `interval` до значения `max-interval` согласно формуле `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span><span class="sxs-lookup"><span data-stu-id="3df60-368">When the `interval`, `max-interval` and `delta` are specified, **exponential** interval retry algorithm is applied, where the wait time between the retries is growing exponentially from the value of `interval` to the value `max-interval` according to the following forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span></span>  
  
### <a name="usage"></a><span data-ttu-id="3df60-369">Использование</span><span class="sxs-lookup"><span data-stu-id="3df60-369">Usage</span></span>  
 <span data-ttu-id="3df60-370">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) политики.</span><span class="sxs-lookup"><span data-stu-id="3df60-370">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span> <span data-ttu-id="3df60-371">Обратите внимание, что эта политика наследует ограничения использования дочерних политик.</span><span class="sxs-lookup"><span data-stu-id="3df60-371">Note that child policy usage restrictions will be inherited by this policy.</span></span>  
  
-   <span data-ttu-id="3df60-372">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="3df60-372">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="3df60-373">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="3df60-373">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="3df60-374"><a name="ReturnResponse"></a> Возврат ответа</span><span class="sxs-lookup"><span data-stu-id="3df60-374"><a name="ReturnResponse"></a> Return response</span></span>  
 <span data-ttu-id="3df60-375">Политика `return-response` прерывает выполнение конвейера и возвращает вызывающему объекту ответ по умолчанию или настраиваемый ответ.</span><span class="sxs-lookup"><span data-stu-id="3df60-375">The `return-response` policy aborts pipeline execution and returns either a default or custom response to the caller.</span></span> <span data-ttu-id="3df60-376">По умолчанию возвращается код `200 OK` без текста.</span><span class="sxs-lookup"><span data-stu-id="3df60-376">Default response is `200 OK` with no body.</span></span> <span data-ttu-id="3df60-377">Можно указать настраиваемый ответ с помощью переменной контекста или правил политики.</span><span class="sxs-lookup"><span data-stu-id="3df60-377">Custom response can be specified via a context variable or policy statements.</span></span> <span data-ttu-id="3df60-378">Если указаны оба, ответ, содержащийся в переменной контекста, изменяется правилами политики перед возвращением вызывающему объекту.</span><span class="sxs-lookup"><span data-stu-id="3df60-378">When both are provided, the response contained within the context variable is modified by the policy statements before being returned to the caller.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3df60-379">Правило политики</span><span class="sxs-lookup"><span data-stu-id="3df60-379">Policy statement</span></span>  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a><span data-ttu-id="3df60-380">Пример</span><span class="sxs-lookup"><span data-stu-id="3df60-380">Example</span></span>  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="3df60-381">Элементы</span><span class="sxs-lookup"><span data-stu-id="3df60-381">Elements</span></span>  
  
|<span data-ttu-id="3df60-382">Элемент</span><span class="sxs-lookup"><span data-stu-id="3df60-382">Element</span></span>|<span data-ttu-id="3df60-383">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-383">Description</span></span>|<span data-ttu-id="3df60-384">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-384">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="3df60-385">return-response</span><span class="sxs-lookup"><span data-stu-id="3df60-385">return-response</span></span>|<span data-ttu-id="3df60-386">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="3df60-386">Root element.</span></span>|<span data-ttu-id="3df60-387">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-387">Yes</span></span>|  
|<span data-ttu-id="3df60-388">set-header</span><span class="sxs-lookup"><span data-stu-id="3df60-388">set-header</span></span>|<span data-ttu-id="3df60-389">Правило политики [set-header](api-management-transformation-policies.md#SetHTTPheader).</span><span class="sxs-lookup"><span data-stu-id="3df60-389">A [set-header](api-management-transformation-policies.md#SetHTTPheader) policy statement.</span></span>|<span data-ttu-id="3df60-390">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-390">No</span></span>|  
|<span data-ttu-id="3df60-391">set-body</span><span class="sxs-lookup"><span data-stu-id="3df60-391">set-body</span></span>|<span data-ttu-id="3df60-392">Правило политики [set-body](api-management-transformation-policies.md#SetBody).</span><span class="sxs-lookup"><span data-stu-id="3df60-392">A [set-body](api-management-transformation-policies.md#SetBody) policy statement.</span></span>|<span data-ttu-id="3df60-393">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-393">No</span></span>|  
|<span data-ttu-id="3df60-394">set-status</span><span class="sxs-lookup"><span data-stu-id="3df60-394">set-status</span></span>|<span data-ttu-id="3df60-395">Правило политики [set-status](api-management-advanced-policies.md#SetStatus).</span><span class="sxs-lookup"><span data-stu-id="3df60-395">A [set-status](api-management-advanced-policies.md#SetStatus) policy statement.</span></span>|<span data-ttu-id="3df60-396">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-396">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3df60-397">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="3df60-397">Attributes</span></span>  
  
|<span data-ttu-id="3df60-398">Атрибут</span><span class="sxs-lookup"><span data-stu-id="3df60-398">Attribute</span></span>|<span data-ttu-id="3df60-399">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-399">Description</span></span>|<span data-ttu-id="3df60-400">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-400">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="3df60-401">response-variable-name</span><span class="sxs-lookup"><span data-stu-id="3df60-401">response-variable-name</span></span>|<span data-ttu-id="3df60-402">Имя переменной контекста, на которую ссылается, например, вышестоящая политика [send-request](api-management-advanced-policies.md#SendRequest) и которая содержит объект `Response`.</span><span class="sxs-lookup"><span data-stu-id="3df60-402">The name of the context variable referenced from, for example, an upstream [send-request](api-management-advanced-policies.md#SendRequest) policy and containing a `Response` object</span></span>|<span data-ttu-id="3df60-403">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="3df60-403">Optional.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3df60-404">Использование</span><span class="sxs-lookup"><span data-stu-id="3df60-404">Usage</span></span>  
 <span data-ttu-id="3df60-405">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3df60-405">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3df60-406">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="3df60-406">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="3df60-407">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="3df60-407">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="3df60-408"><a name="SendOneWayRequest"></a> Отправка одностороннего запроса</span><span class="sxs-lookup"><span data-stu-id="3df60-408"><a name="SendOneWayRequest"></a> Send one way request</span></span>  
 <span data-ttu-id="3df60-409">Политика `send-one-way-request` отправляет запрос на указанный URL-адрес и не ожидает ответа.</span><span class="sxs-lookup"><span data-stu-id="3df60-409">The `send-one-way-request` policy sends the provided request to the specified URL without waiting for a response.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3df60-410">Правило политики</span><span class="sxs-lookup"><span data-stu-id="3df60-410">Policy statement</span></span>  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="3df60-411">Пример</span><span class="sxs-lookup"><span data-stu-id="3df60-411">Example</span></span>  
 <span data-ttu-id="3df60-412">В этом примере политики демонстрируется использование политики `send-one-way-request` для отправки сообщения в чат Slack, если код HTTP-ответа больше или равен 500.</span><span class="sxs-lookup"><span data-stu-id="3df60-412">This sample policy shows an example of using the `send-one-way-request` policy to send a message to a Slack chat room if the HTTP response code is greater than or equal to 500.</span></span> <span data-ttu-id="3df60-413">Дополнительные сведения об этом примере см. в статье [Использование внешних служб из службы управления API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="3df60-413">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="3df60-414">Элементы</span><span class="sxs-lookup"><span data-stu-id="3df60-414">Elements</span></span>  
  
|<span data-ttu-id="3df60-415">Элемент</span><span class="sxs-lookup"><span data-stu-id="3df60-415">Element</span></span>|<span data-ttu-id="3df60-416">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-416">Description</span></span>|<span data-ttu-id="3df60-417">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-417">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="3df60-418">send-one-way-request</span><span class="sxs-lookup"><span data-stu-id="3df60-418">send-one-way-request</span></span>|<span data-ttu-id="3df60-419">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="3df60-419">Root element.</span></span>|<span data-ttu-id="3df60-420">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-420">Yes</span></span>|  
|<span data-ttu-id="3df60-421">url</span><span class="sxs-lookup"><span data-stu-id="3df60-421">url</span></span>|<span data-ttu-id="3df60-422">URL-адрес запроса.</span><span class="sxs-lookup"><span data-stu-id="3df60-422">The URL of the request.</span></span>|<span data-ttu-id="3df60-423">Нет, если mode=copy. В противном случае да.</span><span class="sxs-lookup"><span data-stu-id="3df60-423">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="3df60-424">метод</span><span class="sxs-lookup"><span data-stu-id="3df60-424">method</span></span>|<span data-ttu-id="3df60-425">Метод HTTP, используемый для запроса.</span><span class="sxs-lookup"><span data-stu-id="3df60-425">The HTTP method for the request.</span></span>|<span data-ttu-id="3df60-426">Нет, если mode=copy. В противном случае да.</span><span class="sxs-lookup"><span data-stu-id="3df60-426">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="3df60-427">Верхний колонтитул</span><span class="sxs-lookup"><span data-stu-id="3df60-427">header</span></span>|<span data-ttu-id="3df60-428">Заголовок запроса.</span><span class="sxs-lookup"><span data-stu-id="3df60-428">Request header.</span></span> <span data-ttu-id="3df60-429">Используйте несколько элементов заголовка для нескольких заголовков запросов.</span><span class="sxs-lookup"><span data-stu-id="3df60-429">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="3df60-430">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-430">No</span></span>|  
|<span data-ttu-id="3df60-431">текст</span><span class="sxs-lookup"><span data-stu-id="3df60-431">body</span></span>|<span data-ttu-id="3df60-432">Текст запроса.</span><span class="sxs-lookup"><span data-stu-id="3df60-432">The request body.</span></span>|<span data-ttu-id="3df60-433">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-433">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3df60-434">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="3df60-434">Attributes</span></span>  
  
|<span data-ttu-id="3df60-435">Атрибут</span><span class="sxs-lookup"><span data-stu-id="3df60-435">Attribute</span></span>|<span data-ttu-id="3df60-436">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-436">Description</span></span>|<span data-ttu-id="3df60-437">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-437">Required</span></span>|<span data-ttu-id="3df60-438">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="3df60-438">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="3df60-439">mode="строка"</span><span class="sxs-lookup"><span data-stu-id="3df60-439">mode="string"</span></span>|<span data-ttu-id="3df60-440">Определяет, является ли это новым запросом или копией текущего запроса.</span><span class="sxs-lookup"><span data-stu-id="3df60-440">Determines whether this is a new request or a copy of the current request.</span></span> <span data-ttu-id="3df60-441">В исходящем режиме mode=copy не инициализирует текст запроса.</span><span class="sxs-lookup"><span data-stu-id="3df60-441">In outbound mode, mode=copy does not initialize the request body.</span></span>|<span data-ttu-id="3df60-442">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-442">No</span></span>|<span data-ttu-id="3df60-443">Создать</span><span class="sxs-lookup"><span data-stu-id="3df60-443">New</span></span>|  
|<span data-ttu-id="3df60-444">name</span><span class="sxs-lookup"><span data-stu-id="3df60-444">name</span></span>|<span data-ttu-id="3df60-445">Указывает имя заголовка, которое должно быть установлено.</span><span class="sxs-lookup"><span data-stu-id="3df60-445">Specifies the name of the header to be set.</span></span>|<span data-ttu-id="3df60-446">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-446">Yes</span></span>|<span data-ttu-id="3df60-447">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3df60-447">N/A</span></span>|  
|<span data-ttu-id="3df60-448">exists-action</span><span class="sxs-lookup"><span data-stu-id="3df60-448">exists-action</span></span>|<span data-ttu-id="3df60-449">Указывает действие, которое должно быть выполнено, когда заголовок уже задан.</span><span class="sxs-lookup"><span data-stu-id="3df60-449">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="3df60-450">Атрибут должен иметь одно из следующих значений:</span><span class="sxs-lookup"><span data-stu-id="3df60-450">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="3df60-451">override — заменяет значение имеющегося заголовка;</span><span class="sxs-lookup"><span data-stu-id="3df60-451">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="3df60-452">skip — не заменяет значение имеющегося заголовка;</span><span class="sxs-lookup"><span data-stu-id="3df60-452">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="3df60-453">append — добавляет значение к значению имеющегося заголовка;</span><span class="sxs-lookup"><span data-stu-id="3df60-453">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="3df60-454">delete — удаляет заголовок из запроса.</span><span class="sxs-lookup"><span data-stu-id="3df60-454">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="3df60-455">Если установлено значение `override`, перечисление нескольких записей с одним и тем же именем будет приводить к тому, что заголовок будет устанавливаться в соответствии со всеми записями (будут перечисляться несколько раз). В результате будут установлены только перечисленные значения.</span><span class="sxs-lookup"><span data-stu-id="3df60-455">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="3df60-456">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-456">No</span></span>|<span data-ttu-id="3df60-457">override</span><span class="sxs-lookup"><span data-stu-id="3df60-457">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3df60-458">Использование</span><span class="sxs-lookup"><span data-stu-id="3df60-458">Usage</span></span>  
 <span data-ttu-id="3df60-459">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3df60-459">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3df60-460">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="3df60-460">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="3df60-461">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="3df60-461">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="3df60-462"><a name="SendRequest"></a> Отправка запроса</span><span class="sxs-lookup"><span data-stu-id="3df60-462"><a name="SendRequest"></a> Send request</span></span>  
 <span data-ttu-id="3df60-463">Политика `send-request` отправляет запрос по указанному URL-адресу с задержкой, не превышающей заданное значение времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="3df60-463">The `send-request` policy sends the provided request to the specified URL, waiting no longer than the set timeout value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3df60-464">Правило политики</span><span class="sxs-lookup"><span data-stu-id="3df60-464">Policy statement</span></span>  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="3df60-465">Пример</span><span class="sxs-lookup"><span data-stu-id="3df60-465">Example</span></span>  
 <span data-ttu-id="3df60-466">В этом примере показан один из способов проверки маркера ссылки на сервере авторизации.</span><span class="sxs-lookup"><span data-stu-id="3df60-466">This example shows one way to verify a reference token with an authorization server.</span></span> <span data-ttu-id="3df60-467">Дополнительные сведения об этом примере см. в статье [Использование внешних служб из службы управления API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="3df60-467">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<inbound>  
  <!-- Extract Token from Authorization header parameter -->  
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />  
  
  <!-- Send request to Token Server to validate token (see RFC 7662) -->  
  <send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">  
    <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>  
    <set-method>POST</set-method>  
    <set-header name="Authorization" exists-action="override">  
      <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>  
    </set-header>  
    <set-header name="Content-Type" exists-action="override">  
      <value>application/x-www-form-urlencoded</value>  
    </set-header>  
    <set-body>@($"token={(string)context.Variables["token"]}")</set-body>  
  </send-request>  
  
  <choose>  
        <!-- Check active property in response -->  
        <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
            <!-- Return 401 Unauthorized with http-problem payload -->  
            <return-response response-variable-name="existing response variable">  
                <set-status code="401" reason="Unauthorized" />  
                <set-header name="WWW-Authenticate" exists-action="override">  
                    <value>Bearer error="invalid_token"</value>  
                </set-header>  
            </return-response>  
        </when>  
    </choose>  
  <base />  
</inbound>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="3df60-468">Элементы</span><span class="sxs-lookup"><span data-stu-id="3df60-468">Elements</span></span>  
  
|<span data-ttu-id="3df60-469">Элемент</span><span class="sxs-lookup"><span data-stu-id="3df60-469">Element</span></span>|<span data-ttu-id="3df60-470">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-470">Description</span></span>|<span data-ttu-id="3df60-471">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-471">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="3df60-472">send-request</span><span class="sxs-lookup"><span data-stu-id="3df60-472">send-request</span></span>|<span data-ttu-id="3df60-473">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="3df60-473">Root element.</span></span>|<span data-ttu-id="3df60-474">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-474">Yes</span></span>|  
|<span data-ttu-id="3df60-475">url</span><span class="sxs-lookup"><span data-stu-id="3df60-475">url</span></span>|<span data-ttu-id="3df60-476">URL-адрес запроса.</span><span class="sxs-lookup"><span data-stu-id="3df60-476">The URL of the request.</span></span>|<span data-ttu-id="3df60-477">Нет, если mode=copy. В противном случае да.</span><span class="sxs-lookup"><span data-stu-id="3df60-477">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="3df60-478">метод</span><span class="sxs-lookup"><span data-stu-id="3df60-478">method</span></span>|<span data-ttu-id="3df60-479">Метод HTTP, используемый для запроса.</span><span class="sxs-lookup"><span data-stu-id="3df60-479">The HTTP method for the request.</span></span>|<span data-ttu-id="3df60-480">Нет, если mode=copy. В противном случае да.</span><span class="sxs-lookup"><span data-stu-id="3df60-480">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="3df60-481">Верхний колонтитул</span><span class="sxs-lookup"><span data-stu-id="3df60-481">header</span></span>|<span data-ttu-id="3df60-482">Заголовок запроса.</span><span class="sxs-lookup"><span data-stu-id="3df60-482">Request header.</span></span> <span data-ttu-id="3df60-483">Используйте несколько элементов заголовка для нескольких заголовков запросов.</span><span class="sxs-lookup"><span data-stu-id="3df60-483">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="3df60-484">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-484">No</span></span>|  
|<span data-ttu-id="3df60-485">текст</span><span class="sxs-lookup"><span data-stu-id="3df60-485">body</span></span>|<span data-ttu-id="3df60-486">Текст запроса.</span><span class="sxs-lookup"><span data-stu-id="3df60-486">The request body.</span></span>|<span data-ttu-id="3df60-487">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-487">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3df60-488">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="3df60-488">Attributes</span></span>  
  
|<span data-ttu-id="3df60-489">Атрибут</span><span class="sxs-lookup"><span data-stu-id="3df60-489">Attribute</span></span>|<span data-ttu-id="3df60-490">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-490">Description</span></span>|<span data-ttu-id="3df60-491">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-491">Required</span></span>|<span data-ttu-id="3df60-492">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="3df60-492">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="3df60-493">mode="строка"</span><span class="sxs-lookup"><span data-stu-id="3df60-493">mode="string"</span></span>|<span data-ttu-id="3df60-494">Определяет, является ли это новым запросом или копией текущего запроса.</span><span class="sxs-lookup"><span data-stu-id="3df60-494">Determines whether this is a new request or a copy of the current request.</span></span> <span data-ttu-id="3df60-495">В исходящем режиме mode=copy не инициализирует текст запроса.</span><span class="sxs-lookup"><span data-stu-id="3df60-495">In outbound mode, mode=copy does not initialize the request body.</span></span>|<span data-ttu-id="3df60-496">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-496">No</span></span>|<span data-ttu-id="3df60-497">Создать</span><span class="sxs-lookup"><span data-stu-id="3df60-497">New</span></span>|  
|<span data-ttu-id="3df60-498">response-variable-name="строка"</span><span class="sxs-lookup"><span data-stu-id="3df60-498">response-variable-name="string"</span></span>|<span data-ttu-id="3df60-499">Если не указано, используется `context.Response`.</span><span class="sxs-lookup"><span data-stu-id="3df60-499">If not present, `context.Response` is used.</span></span>|<span data-ttu-id="3df60-500">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-500">No</span></span>|<span data-ttu-id="3df60-501">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3df60-501">N/A</span></span>|  
|<span data-ttu-id="3df60-502">timeout="целое число"</span><span class="sxs-lookup"><span data-stu-id="3df60-502">timeout="integer"</span></span>|<span data-ttu-id="3df60-503">Интервал времени ожидания в секундах до того, как вызов, адресованный URL-адресу, завершится сбоем.</span><span class="sxs-lookup"><span data-stu-id="3df60-503">The timeout interval in seconds before the call to the URL fails.</span></span>|<span data-ttu-id="3df60-504">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-504">No</span></span>|<span data-ttu-id="3df60-505">60</span><span class="sxs-lookup"><span data-stu-id="3df60-505">60</span></span>|  
|<span data-ttu-id="3df60-506">ignore-error</span><span class="sxs-lookup"><span data-stu-id="3df60-506">ignore-error</span></span>|<span data-ttu-id="3df60-507">Если получено значение true и запрос завершился ошибкой:</span><span class="sxs-lookup"><span data-stu-id="3df60-507">If true and the request results in an error:</span></span><br /><br /> <span data-ttu-id="3df60-508">если response-variable-name указано, он будет содержать значение null;</span><span class="sxs-lookup"><span data-stu-id="3df60-508">-   If response-variable-name was specified it will contain a null value.</span></span><br /><span data-ttu-id="3df60-509">если response-variable-name не указано, контекст запроса не будет обновлен.</span><span class="sxs-lookup"><span data-stu-id="3df60-509">-   If response-variable-name was not specified, context.Request will not be updated.</span></span>|<span data-ttu-id="3df60-510">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-510">No</span></span>|<span data-ttu-id="3df60-511">нет</span><span class="sxs-lookup"><span data-stu-id="3df60-511">false</span></span>|  
|<span data-ttu-id="3df60-512">name</span><span class="sxs-lookup"><span data-stu-id="3df60-512">name</span></span>|<span data-ttu-id="3df60-513">Указывает имя заголовка, которое должно быть установлено.</span><span class="sxs-lookup"><span data-stu-id="3df60-513">Specifies the name of the header to be set.</span></span>|<span data-ttu-id="3df60-514">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-514">Yes</span></span>|<span data-ttu-id="3df60-515">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3df60-515">N/A</span></span>|  
|<span data-ttu-id="3df60-516">exists-action</span><span class="sxs-lookup"><span data-stu-id="3df60-516">exists-action</span></span>|<span data-ttu-id="3df60-517">Указывает действие, которое должно быть выполнено, когда заголовок уже задан.</span><span class="sxs-lookup"><span data-stu-id="3df60-517">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="3df60-518">Атрибут должен иметь одно из следующих значений:</span><span class="sxs-lookup"><span data-stu-id="3df60-518">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="3df60-519">override — заменяет значение имеющегося заголовка;</span><span class="sxs-lookup"><span data-stu-id="3df60-519">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="3df60-520">skip — не заменяет значение имеющегося заголовка;</span><span class="sxs-lookup"><span data-stu-id="3df60-520">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="3df60-521">append — добавляет значение к значению имеющегося заголовка;</span><span class="sxs-lookup"><span data-stu-id="3df60-521">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="3df60-522">delete — удаляет заголовок из запроса.</span><span class="sxs-lookup"><span data-stu-id="3df60-522">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="3df60-523">Если установлено значение `override`, перечисление нескольких записей с одним и тем же именем будет приводить к тому, что заголовок будет устанавливаться в соответствии со всеми записями (будут перечисляться несколько раз). В результате будут установлены только перечисленные значения.</span><span class="sxs-lookup"><span data-stu-id="3df60-523">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="3df60-524">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-524">No</span></span>|<span data-ttu-id="3df60-525">override</span><span class="sxs-lookup"><span data-stu-id="3df60-525">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3df60-526">Использование</span><span class="sxs-lookup"><span data-stu-id="3df60-526">Usage</span></span>  
 <span data-ttu-id="3df60-527">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3df60-527">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3df60-528">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="3df60-528">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="3df60-529">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="3df60-529">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="3df60-530"><a name="SetHttpProxy"></a> Установка прокси-сервера HTTP</span><span class="sxs-lookup"><span data-stu-id="3df60-530"><a name="SetHttpProxy"></a> Set HTTP proxy</span></span>  
 <span data-ttu-id="3df60-531">Политика `proxy` позволяет маршрутизировать запросы, перенаправленные в серверную часть, через прокси-сервер HTTP.</span><span class="sxs-lookup"><span data-stu-id="3df60-531">The `proxy` policy allows you to route requests forwarded to backends via an HTTP proxy.</span></span> <span data-ttu-id="3df60-532">Между шлюзом и прокси-сервером поддерживается только протокол HTTP (не HTTPS).</span><span class="sxs-lookup"><span data-stu-id="3df60-532">Only HTTP (not HTTPS) is supported between the gateway and the proxy.</span></span> <span data-ttu-id="3df60-533">Используются только базовая проверка подлинности и проверка подлинности NTLM.</span><span class="sxs-lookup"><span data-stu-id="3df60-533">Basic and NTLM authentication only.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="3df60-534">Правило политики</span><span class="sxs-lookup"><span data-stu-id="3df60-534">Policy statement</span></span>  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="3df60-535">Пример</span><span class="sxs-lookup"><span data-stu-id="3df60-535">Example</span></span>  
<span data-ttu-id="3df60-536">Обратите внимание на использование [свойства](api-management-howto-properties.md) в качестве значений имени пользователя и пароля, чтобы избегать хранения конфиденциальных сведений в документе политики.</span><span class="sxs-lookup"><span data-stu-id="3df60-536">Note the use of [properties](api-management-howto-properties.md) as values of the username and password to avoid storing sensitive information in the policy document.</span></span>  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a><span data-ttu-id="3df60-537">Элементы</span><span class="sxs-lookup"><span data-stu-id="3df60-537">Elements</span></span>  
  
|<span data-ttu-id="3df60-538">Элемент</span><span class="sxs-lookup"><span data-stu-id="3df60-538">Element</span></span>|<span data-ttu-id="3df60-539">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-539">Description</span></span>|<span data-ttu-id="3df60-540">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-540">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="3df60-541">proxy</span><span class="sxs-lookup"><span data-stu-id="3df60-541">proxy</span></span>|<span data-ttu-id="3df60-542">Корневой элемент</span><span class="sxs-lookup"><span data-stu-id="3df60-542">Root element</span></span>|<span data-ttu-id="3df60-543">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-543">Yes</span></span>|  

### <a name="attributes"></a><span data-ttu-id="3df60-544">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="3df60-544">Attributes</span></span>  
  
|<span data-ttu-id="3df60-545">Атрибут</span><span class="sxs-lookup"><span data-stu-id="3df60-545">Attribute</span></span>|<span data-ttu-id="3df60-546">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-546">Description</span></span>|<span data-ttu-id="3df60-547">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-547">Required</span></span>|<span data-ttu-id="3df60-548">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="3df60-548">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="3df60-549">url="string"</span><span class="sxs-lookup"><span data-stu-id="3df60-549">url="string"</span></span>|<span data-ttu-id="3df60-550">URL-адрес прокси-сервера в виде http://host:port.</span><span class="sxs-lookup"><span data-stu-id="3df60-550">Proxy URL in the form of http://host:port.</span></span>|<span data-ttu-id="3df60-551">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-551">Yes</span></span>|<span data-ttu-id="3df60-552">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3df60-552">N/A</span></span>|  
|<span data-ttu-id="3df60-553">username="string"</span><span class="sxs-lookup"><span data-stu-id="3df60-553">username="string"</span></span>|<span data-ttu-id="3df60-554">Имя пользователя, которое следует использовать для проверки подлинности на прокси-сервере.</span><span class="sxs-lookup"><span data-stu-id="3df60-554">Username to be used for authentication with the proxy.</span></span>|<span data-ttu-id="3df60-555">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-555">No</span></span>|<span data-ttu-id="3df60-556">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3df60-556">N/A</span></span>|  
|<span data-ttu-id="3df60-557">password="string"</span><span class="sxs-lookup"><span data-stu-id="3df60-557">password="string"</span></span>|<span data-ttu-id="3df60-558">Пароль, который следует использовать для проверки подлинности на прокси-сервере.</span><span class="sxs-lookup"><span data-stu-id="3df60-558">Password to be used for authentication with the proxy.</span></span>|<span data-ttu-id="3df60-559">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-559">No</span></span>|<span data-ttu-id="3df60-560">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3df60-560">N/A</span></span>|  

### <a name="usage"></a><span data-ttu-id="3df60-561">Использование</span><span class="sxs-lookup"><span data-stu-id="3df60-561">Usage</span></span>  
 <span data-ttu-id="3df60-562">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3df60-562">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3df60-563">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="3df60-563">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="3df60-564">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="3df60-564">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="3df60-565"><a name="SetRequestMethod"></a> Задание метода запроса</span><span class="sxs-lookup"><span data-stu-id="3df60-565"><a name="SetRequestMethod"></a> Set request method</span></span>  
 <span data-ttu-id="3df60-566">Политика `set-method` позволяет изменить метод HTTP-запроса для запроса.</span><span class="sxs-lookup"><span data-stu-id="3df60-566">The `set-method` policy allows you to change the HTTP request method for a request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3df60-567">Правило политики</span><span class="sxs-lookup"><span data-stu-id="3df60-567">Policy statement</span></span>  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a><span data-ttu-id="3df60-568">Пример</span><span class="sxs-lookup"><span data-stu-id="3df60-568">Example</span></span>  
 <span data-ttu-id="3df60-569">В этом примере политики демонстрируется использование политики `set-method` для отправки сообщения в чат Slack, если код HTTP-ответа больше или равен 500.</span><span class="sxs-lookup"><span data-stu-id="3df60-569">This sample policy that uses the `set-method` policy shows an example of sending a message to a Slack chat room if the HTTP response code is greater than or equal to 500.</span></span> <span data-ttu-id="3df60-570">Дополнительные сведения об этом примере см. в статье [Использование внешних служб из службы управления API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="3df60-570">For more information on this sample, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<choose>  
    <when condition="@(context.Response.StatusCode >= 500)">  
      <send-one-way-request mode="new">  
        <set-url>https://hooks.slack.com/services/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</set-url>  
        <set-method>POST</set-method>  
        <set-body>@{  
                return new JObject(  
                        new JProperty("username","APIM Alert"),  
                        new JProperty("icon_emoji", ":ghost:"),  
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",  
                                                context.Request.Method,  
                                                context.Request.Url.Path + context.Request.Url.QueryString,  
                                                context.Request.Url.Host,  
                                                context.Response.StatusCode,  
                                                context.Response.StatusReason,  
                                                context.User.Email  
                                                ))  
                        ).ToString();  
            }</set-body>  
      </send-one-way-request>  
    </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="3df60-571">Элементы</span><span class="sxs-lookup"><span data-stu-id="3df60-571">Elements</span></span>  
  
|<span data-ttu-id="3df60-572">Элемент</span><span class="sxs-lookup"><span data-stu-id="3df60-572">Element</span></span>|<span data-ttu-id="3df60-573">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-573">Description</span></span>|<span data-ttu-id="3df60-574">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-574">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="3df60-575">set-method</span><span class="sxs-lookup"><span data-stu-id="3df60-575">set-method</span></span>|<span data-ttu-id="3df60-576">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="3df60-576">Root element.</span></span> <span data-ttu-id="3df60-577">Значение элемента задает метод HTTP.</span><span class="sxs-lookup"><span data-stu-id="3df60-577">The value of the element specifies the HTTP method.</span></span>|<span data-ttu-id="3df60-578">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-578">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3df60-579">Использование</span><span class="sxs-lookup"><span data-stu-id="3df60-579">Usage</span></span>  
 <span data-ttu-id="3df60-580">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3df60-580">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3df60-581">**Разделы политики:** inbound, on-error.</span><span class="sxs-lookup"><span data-stu-id="3df60-581">**Policy sections:** inbound, on-error</span></span>  
  
-   <span data-ttu-id="3df60-582">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="3df60-582">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="3df60-583"><a name="SetStatus"></a> Задание кода состояния</span><span class="sxs-lookup"><span data-stu-id="3df60-583"><a name="SetStatus"></a> Set status code</span></span>  
 <span data-ttu-id="3df60-584">Политика `set-status` меняет код состояния HTTP на указанное значение.</span><span class="sxs-lookup"><span data-stu-id="3df60-584">The `set-status` policy sets the HTTP status code to the specified value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3df60-585">Правило политики</span><span class="sxs-lookup"><span data-stu-id="3df60-585">Policy statement</span></span>  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a><span data-ttu-id="3df60-586">Пример</span><span class="sxs-lookup"><span data-stu-id="3df60-586">Example</span></span>  
 <span data-ttu-id="3df60-587">В этом примере показано, как вернуть ответ 401, если маркер проверки подлинности является недопустимым.</span><span class="sxs-lookup"><span data-stu-id="3df60-587">This example shows how to return a 401 response if the authorization token is invalid.</span></span> <span data-ttu-id="3df60-588">Дополнительные сведения см. в статье [Использование внешних служб из службы управления API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="3df60-588">For more information, see [Using external services from the Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span></span>  
  
```xml  
<choose>  
  <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">  
    <return-response response-variable-name="existing response variable">  
      <set-status code="401" reason="Unauthorized" />  
      <set-header name="WWW-Authenticate" exists-action="override">  
        <value>Bearer error="invalid_token"</value>  
      </set-header>  
    </return-response>  
  </when>  
</choose>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="3df60-589">Элементы</span><span class="sxs-lookup"><span data-stu-id="3df60-589">Elements</span></span>  
  
|<span data-ttu-id="3df60-590">Элемент</span><span class="sxs-lookup"><span data-stu-id="3df60-590">Element</span></span>|<span data-ttu-id="3df60-591">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-591">Description</span></span>|<span data-ttu-id="3df60-592">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-592">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="3df60-593">set-status</span><span class="sxs-lookup"><span data-stu-id="3df60-593">set-status</span></span>|<span data-ttu-id="3df60-594">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="3df60-594">Root element.</span></span>|<span data-ttu-id="3df60-595">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-595">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3df60-596">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="3df60-596">Attributes</span></span>  
  
|<span data-ttu-id="3df60-597">Атрибут</span><span class="sxs-lookup"><span data-stu-id="3df60-597">Attribute</span></span>|<span data-ttu-id="3df60-598">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-598">Description</span></span>|<span data-ttu-id="3df60-599">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-599">Required</span></span>|<span data-ttu-id="3df60-600">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="3df60-600">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="3df60-601">code="целое число"</span><span class="sxs-lookup"><span data-stu-id="3df60-601">code="integer"</span></span>|<span data-ttu-id="3df60-602">Код состояния HTTP для возврата.</span><span class="sxs-lookup"><span data-stu-id="3df60-602">The HTTP status code to return.</span></span>|<span data-ttu-id="3df60-603">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-603">Yes</span></span>|<span data-ttu-id="3df60-604">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3df60-604">N/A</span></span>|  
|<span data-ttu-id="3df60-605">reason="строка"</span><span class="sxs-lookup"><span data-stu-id="3df60-605">reason="string"</span></span>|<span data-ttu-id="3df60-606">Описание причины для возврата кода состояния.</span><span class="sxs-lookup"><span data-stu-id="3df60-606">A description of the reason for returning the status code.</span></span>|<span data-ttu-id="3df60-607">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-607">Yes</span></span>|<span data-ttu-id="3df60-608">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3df60-608">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3df60-609">Использование</span><span class="sxs-lookup"><span data-stu-id="3df60-609">Usage</span></span>  
 <span data-ttu-id="3df60-610">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3df60-610">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3df60-611">**Разделы политики:** outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="3df60-611">**Policy sections:** outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="3df60-612">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="3df60-612">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="3df60-613"><a name="set-variable"></a> Задание переменной</span><span class="sxs-lookup"><span data-stu-id="3df60-613"><a name="set-variable"></a> Set variable</span></span>  
 <span data-ttu-id="3df60-614">Политика `set-variable` объявляет [переменную](api-management-policy-expressions.md#ContextVariables) контекста и присваивает ей значение, заданное с помощью [выражение](api-management-policy-expressions.md) или строкового литерала.</span><span class="sxs-lookup"><span data-stu-id="3df60-614">The `set-variable` policy declares a [context](api-management-policy-expressions.md#ContextVariables) variable and assigns it a value specified via an [expression](api-management-policy-expressions.md) or a string literal.</span></span> <span data-ttu-id="3df60-615">Если выражение содержит литерал, он будет преобразован в строку и будет иметь тип значения `System.String`.</span><span class="sxs-lookup"><span data-stu-id="3df60-615">if the expression contains a literal it will be converted to a string and the type of the value will be `System.String`.</span></span>  
  
###  <span data-ttu-id="3df60-616"><a name="set-variablePolicyStatement"></a> Правило политики</span><span class="sxs-lookup"><span data-stu-id="3df60-616"><a name="set-variablePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <span data-ttu-id="3df60-617"><a name="set-variableExample"></a> Пример</span><span class="sxs-lookup"><span data-stu-id="3df60-617"><a name="set-variableExample"></a> Example</span></span>  
 <span data-ttu-id="3df60-618">В следующем примере демонстрируется политика задания переменной в разделе inbound.</span><span class="sxs-lookup"><span data-stu-id="3df60-618">The following example demonstrates a set variable policy in the inbound section.</span></span> <span data-ttu-id="3df60-619">Политика задания переменной создает логическую переменную [контекста](api-management-policy-expressions.md#ContextVariables) `isMobile`, которой присваивается значение true, если заголовок запроса `User-Agent` содержит текст `iPad` или `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="3df60-619">This set variable policy creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set to true if the `User-Agent` request header contains the text `iPad` or `iPhone`.</span></span>  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a><span data-ttu-id="3df60-620">Элементы</span><span class="sxs-lookup"><span data-stu-id="3df60-620">Elements</span></span>  
  
|<span data-ttu-id="3df60-621">Элемент</span><span class="sxs-lookup"><span data-stu-id="3df60-621">Element</span></span>|<span data-ttu-id="3df60-622">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-622">Description</span></span>|<span data-ttu-id="3df60-623">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-623">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="3df60-624">set-variable</span><span class="sxs-lookup"><span data-stu-id="3df60-624">set-variable</span></span>|<span data-ttu-id="3df60-625">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="3df60-625">Root element.</span></span>|<span data-ttu-id="3df60-626">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-626">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3df60-627">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="3df60-627">Attributes</span></span>  
  
|<span data-ttu-id="3df60-628">Атрибут</span><span class="sxs-lookup"><span data-stu-id="3df60-628">Attribute</span></span>|<span data-ttu-id="3df60-629">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-629">Description</span></span>|<span data-ttu-id="3df60-630">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-630">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="3df60-631">name</span><span class="sxs-lookup"><span data-stu-id="3df60-631">name</span></span>|<span data-ttu-id="3df60-632">Имя переменной.</span><span class="sxs-lookup"><span data-stu-id="3df60-632">The name of the variable.</span></span>|<span data-ttu-id="3df60-633">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-633">Yes</span></span>|  
|<span data-ttu-id="3df60-634">значение</span><span class="sxs-lookup"><span data-stu-id="3df60-634">value</span></span>|<span data-ttu-id="3df60-635">Значение переменной.</span><span class="sxs-lookup"><span data-stu-id="3df60-635">The value of the variable.</span></span> <span data-ttu-id="3df60-636">Это может быть выражение или литеральное значение.</span><span class="sxs-lookup"><span data-stu-id="3df60-636">This can be an expression or a literal value.</span></span>|<span data-ttu-id="3df60-637">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-637">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3df60-638">Использование</span><span class="sxs-lookup"><span data-stu-id="3df60-638">Usage</span></span>  
 <span data-ttu-id="3df60-639">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3df60-639">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3df60-640">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="3df60-640">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="3df60-641">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="3df60-641">**Policy scopes:** all scopes</span></span>  
  
###  <span data-ttu-id="3df60-642"><a name="set-variableAllowedTypes"></a> Допустимые типы</span><span class="sxs-lookup"><span data-stu-id="3df60-642"><a name="set-variableAllowedTypes"></a> Allowed types</span></span>  
 <span data-ttu-id="3df60-643">Выражения, используемые в политике `set-variable`, должны возвращать один из следующих основных типов.</span><span class="sxs-lookup"><span data-stu-id="3df60-643">Expressions used in the `set-variable` policy must return one of the following basic types.</span></span>  
  
-   <span data-ttu-id="3df60-644">System.Boolean</span><span class="sxs-lookup"><span data-stu-id="3df60-644">System.Boolean</span></span>  
  
-   <span data-ttu-id="3df60-645">System.SByte</span><span class="sxs-lookup"><span data-stu-id="3df60-645">System.SByte</span></span>  
  
-   <span data-ttu-id="3df60-646">System.Byte</span><span class="sxs-lookup"><span data-stu-id="3df60-646">System.Byte</span></span>  
  
-   <span data-ttu-id="3df60-647">System.UInt16</span><span class="sxs-lookup"><span data-stu-id="3df60-647">System.UInt16</span></span>  
  
-   <span data-ttu-id="3df60-648">System.UInt32</span><span class="sxs-lookup"><span data-stu-id="3df60-648">System.UInt32</span></span>  
  
-   <span data-ttu-id="3df60-649">System.UInt64</span><span class="sxs-lookup"><span data-stu-id="3df60-649">System.UInt64</span></span>  
  
-   <span data-ttu-id="3df60-650">System.Int16</span><span class="sxs-lookup"><span data-stu-id="3df60-650">System.Int16</span></span>  
  
-   <span data-ttu-id="3df60-651">System.Int32</span><span class="sxs-lookup"><span data-stu-id="3df60-651">System.Int32</span></span>  
  
-   <span data-ttu-id="3df60-652">System.Int64</span><span class="sxs-lookup"><span data-stu-id="3df60-652">System.Int64</span></span>  
  
-   <span data-ttu-id="3df60-653">System.Decimal</span><span class="sxs-lookup"><span data-stu-id="3df60-653">System.Decimal</span></span>  
  
-   <span data-ttu-id="3df60-654">System.Single</span><span class="sxs-lookup"><span data-stu-id="3df60-654">System.Single</span></span>  
  
-   <span data-ttu-id="3df60-655">System.Double</span><span class="sxs-lookup"><span data-stu-id="3df60-655">System.Double</span></span>  
  
-   <span data-ttu-id="3df60-656">System.Guid</span><span class="sxs-lookup"><span data-stu-id="3df60-656">System.Guid</span></span>  
  
-   <span data-ttu-id="3df60-657">System.String</span><span class="sxs-lookup"><span data-stu-id="3df60-657">System.String</span></span>  
  
-   <span data-ttu-id="3df60-658">System.Char</span><span class="sxs-lookup"><span data-stu-id="3df60-658">System.Char</span></span>  
  
-   <span data-ttu-id="3df60-659">System.DateTime</span><span class="sxs-lookup"><span data-stu-id="3df60-659">System.DateTime</span></span>  
  
-   <span data-ttu-id="3df60-660">System.TimeSpan</span><span class="sxs-lookup"><span data-stu-id="3df60-660">System.TimeSpan</span></span>  
  
-   <span data-ttu-id="3df60-661">System.Byte?</span><span class="sxs-lookup"><span data-stu-id="3df60-661">System.Byte?</span></span>  
  
-   <span data-ttu-id="3df60-662">System.UInt16?</span><span class="sxs-lookup"><span data-stu-id="3df60-662">System.UInt16?</span></span>  
  
-   <span data-ttu-id="3df60-663">System.UInt32?</span><span class="sxs-lookup"><span data-stu-id="3df60-663">System.UInt32?</span></span>  
  
-   <span data-ttu-id="3df60-664">System.UInt64?</span><span class="sxs-lookup"><span data-stu-id="3df60-664">System.UInt64?</span></span>  
  
-   <span data-ttu-id="3df60-665">System.Int16?</span><span class="sxs-lookup"><span data-stu-id="3df60-665">System.Int16?</span></span>  
  
-   <span data-ttu-id="3df60-666">System.Int32?</span><span class="sxs-lookup"><span data-stu-id="3df60-666">System.Int32?</span></span>  
  
-   <span data-ttu-id="3df60-667">System.Int64?</span><span class="sxs-lookup"><span data-stu-id="3df60-667">System.Int64?</span></span>  
  
-   <span data-ttu-id="3df60-668">System.Decimal?</span><span class="sxs-lookup"><span data-stu-id="3df60-668">System.Decimal?</span></span>  
  
-   <span data-ttu-id="3df60-669">System.Single?</span><span class="sxs-lookup"><span data-stu-id="3df60-669">System.Single?</span></span>  
  
-   <span data-ttu-id="3df60-670">System.Double?</span><span class="sxs-lookup"><span data-stu-id="3df60-670">System.Double?</span></span>  
  
-   <span data-ttu-id="3df60-671">System.Guid?</span><span class="sxs-lookup"><span data-stu-id="3df60-671">System.Guid?</span></span>  
  
-   <span data-ttu-id="3df60-672">System.String?</span><span class="sxs-lookup"><span data-stu-id="3df60-672">System.String?</span></span>  
  
-   <span data-ttu-id="3df60-673">System.Char?</span><span class="sxs-lookup"><span data-stu-id="3df60-673">System.Char?</span></span>  
  
-   <span data-ttu-id="3df60-674">System.DateTime?</span><span class="sxs-lookup"><span data-stu-id="3df60-674">System.DateTime?</span></span>  

##  <span data-ttu-id="3df60-675"><a name="Trace"></a> Трассировка</span><span class="sxs-lookup"><span data-stu-id="3df60-675"><a name="Trace"></a> Trace</span></span>  
 <span data-ttu-id="3df60-676">Политика `trace` добавляет строку в выходные данные [инспектора API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/).</span><span class="sxs-lookup"><span data-stu-id="3df60-676">The             `trace` policy adds a string into the [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span> <span data-ttu-id="3df60-677">Политика будет выполняться, только если инициирована трассировка, т. е. заголовок запроса `Ocp-Apim-Trace` присутствует и имеет значение `true`, а заголовок запроса `Ocp-Apim-Subscription-Key` присутствует и содержит допустимый ключ, связанный с учетной записью администратора.</span><span class="sxs-lookup"><span data-stu-id="3df60-677">The policy will execute only when tracing is triggered, i.e. `Ocp-Apim-Trace` request header is present and set to `true` and `Ocp-Apim-Subscription-Key` request header is present and holds a valid key associated with the admin account.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3df60-678">Правило политики</span><span class="sxs-lookup"><span data-stu-id="3df60-678">Policy statement</span></span>  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="3df60-679">Элементы</span><span class="sxs-lookup"><span data-stu-id="3df60-679">Elements</span></span>  
  
|<span data-ttu-id="3df60-680">Элемент</span><span class="sxs-lookup"><span data-stu-id="3df60-680">Element</span></span>|<span data-ttu-id="3df60-681">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-681">Description</span></span>|<span data-ttu-id="3df60-682">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-682">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="3df60-683">trace</span><span class="sxs-lookup"><span data-stu-id="3df60-683">trace</span></span>|<span data-ttu-id="3df60-684">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="3df60-684">Root element.</span></span>|<span data-ttu-id="3df60-685">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-685">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3df60-686">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="3df60-686">Attributes</span></span>  
  
|<span data-ttu-id="3df60-687">Атрибут</span><span class="sxs-lookup"><span data-stu-id="3df60-687">Attribute</span></span>|<span data-ttu-id="3df60-688">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-688">Description</span></span>|<span data-ttu-id="3df60-689">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-689">Required</span></span>|<span data-ttu-id="3df60-690">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="3df60-690">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="3df60-691">источник</span><span class="sxs-lookup"><span data-stu-id="3df60-691">source</span></span>|<span data-ttu-id="3df60-692">Строковый литерал, понятный средству просмотра трассировки и указывающий источник сообщения.</span><span class="sxs-lookup"><span data-stu-id="3df60-692">String literal meaningful to the trace viewer and specifying the source of the message.</span></span>|<span data-ttu-id="3df60-693">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-693">Yes</span></span>|<span data-ttu-id="3df60-694">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3df60-694">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3df60-695">Использование</span><span class="sxs-lookup"><span data-stu-id="3df60-695">Usage</span></span>  
 <span data-ttu-id="3df60-696">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) политики.</span><span class="sxs-lookup"><span data-stu-id="3df60-696">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="3df60-697">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="3df60-697">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="3df60-698">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="3df60-698">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="3df60-699"><a name="Wait"></a> Ожидание</span><span class="sxs-lookup"><span data-stu-id="3df60-699"><a name="Wait"></a> Wait</span></span>  
 <span data-ttu-id="3df60-700">Политика `wait` параллельно выполняет свои непосредственные дочерние политики и ожидает выполнения всех или одной из них, прежде чем будет завершена.</span><span class="sxs-lookup"><span data-stu-id="3df60-700">The `wait` policy executes its immediate child policies in parallel, and waits for either all or one of its immediate child policies to complete before it completes.</span></span> <span data-ttu-id="3df60-701">Политика ожидания может иметь в качестве непосредственных дочерних следующие политики: [Отправка запроса](api-management-advanced-policies.md#SendRequest), [Получение значения из кэша](api-management-caching-policies.md#GetFromCacheByKey) и [Управление потоками](api-management-advanced-policies.md#choose).</span><span class="sxs-lookup"><span data-stu-id="3df60-701">The wait policy can have as its immediate child policies [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), and [Control flow](api-management-advanced-policies.md#choose) policies.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3df60-702">Правило политики</span><span class="sxs-lookup"><span data-stu-id="3df60-702">Policy statement</span></span>  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a><span data-ttu-id="3df60-703">Пример</span><span class="sxs-lookup"><span data-stu-id="3df60-703">Example</span></span>  
 <span data-ttu-id="3df60-704">В следующем примере две политики `choose` являются непосредственными дочерними политиками политики `wait`.</span><span class="sxs-lookup"><span data-stu-id="3df60-704">In the following example there are two `choose` policies as immediate child policies of the `wait` policy.</span></span> <span data-ttu-id="3df60-705">Каждая из этих политик `choose` выполняется в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="3df60-705">Each of these `choose` policies executes in parallel.</span></span> <span data-ttu-id="3df60-706">Каждая политика `choose` пытается извлечь кэшированное значение.</span><span class="sxs-lookup"><span data-stu-id="3df60-706">Each `choose` policy attempts to retrieve a cached value.</span></span> <span data-ttu-id="3df60-707">В случае промаха кэша для получения значения вызывается внутренняя служба.</span><span class="sxs-lookup"><span data-stu-id="3df60-707">If there is a cache miss, a backend service is called to provide the value.</span></span> <span data-ttu-id="3df60-708">В этом примере политика `wait` не завершается, пока не завершатся все ее непосредственные дочерние политики, так как атрибут `for` имеет значение `all`.</span><span class="sxs-lookup"><span data-stu-id="3df60-708">In this example the `wait` policy does not complete until all of its immediate child policies complete, because the `for` attribute is set to `all`.</span></span>   <span data-ttu-id="3df60-709">В этом примере переменные контекста (`execute-branch-one`, `value-one`, `execute-branch-two` и `value-two`) объявляются вне области этого примера политики.</span><span class="sxs-lookup"><span data-stu-id="3df60-709">In this example the context variables (`execute-branch-one`, `value-one`, `execute-branch-two`, and `value-two`) are declared outside of the scope of this example policy.</span></span>  
  
```xml  
<wait for="all">  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-one="])">  
      <cache-lookup-value key="key-one" variable-name="value-one" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-one="))">  
          <send-request mode="new" response-variable-name="value-one">  
            <set-url>https://backend-one</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
  <choose>  
    <when condition="@((bool)context.Variables["execute-branch-two="])">  
      <cache-lookup-value key="key-two" variable-name="value-two" />  
      <choose>  
        <when condition="@(!context.Variables.ContainsKey("value-two="))">  
          <send-request mode="new" response-variable-name="value-two">  
            <set-url>https://backend-two</set-url>  
            <set-method>GET</set-method>  
          </send-request>  
        </when>  
      </choose>  
    </when>  
  </choose>  
</wait>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="3df60-710">Элементы</span><span class="sxs-lookup"><span data-stu-id="3df60-710">Elements</span></span>  
  
|<span data-ttu-id="3df60-711">Элемент</span><span class="sxs-lookup"><span data-stu-id="3df60-711">Element</span></span>|<span data-ttu-id="3df60-712">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-712">Description</span></span>|<span data-ttu-id="3df60-713">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-713">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="3df60-714">wait</span><span class="sxs-lookup"><span data-stu-id="3df60-714">wait</span></span>|<span data-ttu-id="3df60-715">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="3df60-715">Root element.</span></span> <span data-ttu-id="3df60-716">Может содержать в качестве дочерних элементов только политики `send-request`, `cache-lookup-value` и `choose`.</span><span class="sxs-lookup"><span data-stu-id="3df60-716">May contain as child elements only `send-request`, `cache-lookup-value`, and `choose` policies.</span></span>|<span data-ttu-id="3df60-717">Да</span><span class="sxs-lookup"><span data-stu-id="3df60-717">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3df60-718">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="3df60-718">Attributes</span></span>  
  
|<span data-ttu-id="3df60-719">Атрибут</span><span class="sxs-lookup"><span data-stu-id="3df60-719">Attribute</span></span>|<span data-ttu-id="3df60-720">Описание</span><span class="sxs-lookup"><span data-stu-id="3df60-720">Description</span></span>|<span data-ttu-id="3df60-721">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3df60-721">Required</span></span>|<span data-ttu-id="3df60-722">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="3df60-722">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="3df60-723">for</span><span class="sxs-lookup"><span data-stu-id="3df60-723">for</span></span>|<span data-ttu-id="3df60-724">Определяет, ожидает ли политика `wait` завершения всех непосредственных дочерних политик или только одной.</span><span class="sxs-lookup"><span data-stu-id="3df60-724">Determines whether the `wait` policy waits for all immediate child policies to be completed or just one.</span></span> <span data-ttu-id="3df60-725">Допустимые значения:</span><span class="sxs-lookup"><span data-stu-id="3df60-725">Allowed values are:</span></span><br /><br /> <span data-ttu-id="3df60-726">—-    `all`: ожидание завершения всех непосредственных дочерних политик;</span><span class="sxs-lookup"><span data-stu-id="3df60-726">-   `all` - wait for all immediate child policies to complete</span></span><br /><span data-ttu-id="3df60-727">— any: ожидание завершения любой непосредственной дочерней политики.</span><span class="sxs-lookup"><span data-stu-id="3df60-727">-   any - wait for any immediate child policy to complete.</span></span> <span data-ttu-id="3df60-728">После завершения первой непосредственной дочерней политики политика `wait` завершается и прерывает выполнение других непосредственных дочерних политик.</span><span class="sxs-lookup"><span data-stu-id="3df60-728">Once the first immediate child policy has completed, the `wait` policy completes and execution of any other immediate child policies is terminated.</span></span>|<span data-ttu-id="3df60-729">Нет</span><span class="sxs-lookup"><span data-stu-id="3df60-729">No</span></span>|<span data-ttu-id="3df60-730">все</span><span class="sxs-lookup"><span data-stu-id="3df60-730">all</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3df60-731">Использование</span><span class="sxs-lookup"><span data-stu-id="3df60-731">Usage</span></span>  
 <span data-ttu-id="3df60-732">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3df60-732">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3df60-733">**Разделы политики:** inbound, outbound, backend.</span><span class="sxs-lookup"><span data-stu-id="3df60-733">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="3df60-734">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="3df60-734">**Policy scopes:**all scopes</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="3df60-735">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3df60-735">Next steps</span></span>
<span data-ttu-id="3df60-736">Дополнительные сведения о работе с политиками см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="3df60-736">For more information working with policies, see:</span></span>
-   [<span data-ttu-id="3df60-737">Политики в управлении API</span><span class="sxs-lookup"><span data-stu-id="3df60-737">Policies in API Management</span></span>](api-management-howto-policies.md) 
-   [<span data-ttu-id="3df60-738">Выражения политики</span><span class="sxs-lookup"><span data-stu-id="3df60-738">Policy expressions</span></span>](api-management-policy-expressions.md)
