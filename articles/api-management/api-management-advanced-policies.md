---
title: "Дополнительные политики управления API aaaAzure | Документы Microsoft"
description: "Дополнительные сведения о hello Дополнительные политики, доступные для использования в службе управления API Azure."
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
ms.openlocfilehash: 8245e7a4c9d432b7b4d362192e357829fcabad55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-advanced-policies"></a><span data-ttu-id="1352e-103">Расширенные политики в службе управления API</span><span class="sxs-lookup"><span data-stu-id="1352e-103">API Management advanced policies</span></span>
<span data-ttu-id="1352e-104">Здесь вы найдете ссылку для hello следующих политиках управления интерфейсами API.</span><span class="sxs-lookup"><span data-stu-id="1352e-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="1352e-105">Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в управлении API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="1352e-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="1352e-106"><a name="AdvancedPolicies"></a> Расширенные политики</span><span class="sxs-lookup"><span data-stu-id="1352e-106"><a name="AdvancedPolicies"></a> Advanced policies</span></span>  
  
-   <span data-ttu-id="1352e-107">[Поток управления](api-management-advanced-policies.md#choose) — условно применяет операторы политики на основе результатов вычисления логических hello hello [выражений](api-management-policy-expressions.md).</span><span class="sxs-lookup"><span data-stu-id="1352e-107">[Control flow](api-management-advanced-policies.md#choose) - Conditionally applies policy statements based on hello results of hello evaluation of Boolean [expressions](api-management-policy-expressions.md).</span></span>  
  
-   <span data-ttu-id="1352e-108">[Прямой запрос](#ForwardRequest) -пересылает hello запроса toohello внутренней службы.</span><span class="sxs-lookup"><span data-stu-id="1352e-108">[Forward request](#ForwardRequest) - Forwards hello request toohello backend service.</span></span>

-   <span data-ttu-id="1352e-109">[Ограничения параллелизма](#LimitConcurrency) -предотвращает заключены политики из более чем hello указанное число запросов во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="1352e-109">[Limit concurrency](#LimitConcurrency) - Prevents enclosed policies from executing by more than hello specified number of requests at a time.</span></span>
  
-   <span data-ttu-id="1352e-110">[Журнал tooEvent концентратора](#log-to-eventhub) -отправляет сообщения в hello указан формат tooan концентратора событий определяются сущности средства ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="1352e-110">[Log tooEvent Hub](#log-to-eventhub) - Sends messages in hello specified format tooan Event Hub defined by a Logger entity.</span></span> 

-   <span data-ttu-id="1352e-111">[Макета ответа](#mock-response) -прерываний конвейера выполнения и возвращает ответ на сгенерированные непосредственно toohello вызывающего объекта.</span><span class="sxs-lookup"><span data-stu-id="1352e-111">[Mock response](#mock-response) - Aborts pipeline execution and returns a mocked response directly toohello caller.</span></span>
  
-   <span data-ttu-id="1352e-112">[Повторите](#Retry) -повторных попыток выполнения hello заключены операторы политики, если и пока не будет выполнено условие hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-112">[Retry](#Retry) - Retries execution of hello enclosed policy statements, if and until hello condition is met.</span></span> <span data-ttu-id="1352e-113">Выполнение будет сквозные hello определенные промежутки времени и копирование toohello указанное число повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="1352e-113">Execution will repeat at hello specified time intervals and up toohello specified retry count.</span></span>  
  
-   <span data-ttu-id="1352e-114">[Вернуть ответ](#ReturnResponse) -конвейера прерывания выполнения и возвращает hello указанного ответа непосредственно toohello вызывающего объекта.</span><span class="sxs-lookup"><span data-stu-id="1352e-114">[Return response](#ReturnResponse) - Aborts pipeline execution and returns hello specified response directly toohello caller.</span></span> 
  
-   <span data-ttu-id="1352e-115">[Отправка запроса на один из способов](#SendOneWayRequest) -отправляет toohello запроса указан URL-адрес без ожидания ответа.</span><span class="sxs-lookup"><span data-stu-id="1352e-115">[Send one way request](#SendOneWayRequest) - Sends a request toohello specified URL without waiting for a response.</span></span>  
  
-   <span data-ttu-id="1352e-116">[Отправка запроса](#SendRequest) -отправляет toohello запроса указан URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="1352e-116">[Send request](#SendRequest) - Sends a request toohello specified URL.</span></span>  

-   <span data-ttu-id="1352e-117">[Задайте прокси-сервер HTTP](#SetHttpProxy) -позволяет tooroute пересылать запросы через прокси-сервер HTTP.</span><span class="sxs-lookup"><span data-stu-id="1352e-117">[Set HTTP proxy](#SetHttpProxy) - Allows you tooroute forwarded requests via an HTTP proxy.</span></span>  

-   <span data-ttu-id="1352e-118">[Установка метода запроса](#SetRequestMethod) -позволяет toochange метод hello HTTP для запроса.</span><span class="sxs-lookup"><span data-stu-id="1352e-118">[Set request method](#SetRequestMethod) - Allows you toochange hello HTTP method for a request.</span></span>  
  
-   <span data-ttu-id="1352e-119">[Задать код состояния](#SetStatus) -toohello код состояния hello HTTP изменения заданного значения.</span><span class="sxs-lookup"><span data-stu-id="1352e-119">[Set status code](#SetStatus) - Changes hello HTTP status code toohello specified value.</span></span>  
  
-   <span data-ttu-id="1352e-120">[Задание переменной](api-management-advanced-policies.md#set-variable) — сохраняет значение в именованной переменной [контекста](api-management-policy-expressions.md#ContextVariables) для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="1352e-120">[Set variable](api-management-advanced-policies.md#set-variable) - Persists a value in a named [context](api-management-policy-expressions.md#ContextVariables) variable for later access.</span></span>  

-   <span data-ttu-id="1352e-121">[Трассировки](#Trace) -добавляет строку в hello [инспектора API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) выходных данных.</span><span class="sxs-lookup"><span data-stu-id="1352e-121">[Trace](#Trace) - Adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span>  
  
-   <span data-ttu-id="1352e-122">[Подождите](#Wait) -ожидает заключены [запрос на отправку](api-management-advanced-policies.md#SendRequest), [получить значение из кэша](api-management-caching-policies.md#GetFromCacheByKey), или [поток управления](api-management-advanced-policies.md#choose) toocomplete политики, прежде чем продолжить.</span><span class="sxs-lookup"><span data-stu-id="1352e-122">[Wait](#Wait) - Waits for enclosed [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), or [Control flow](api-management-advanced-policies.md#choose) policies toocomplete before proceeding.</span></span>  
  
##  <span data-ttu-id="1352e-123"><a name="choose"></a> Управление потоками</span><span class="sxs-lookup"><span data-stu-id="1352e-123"><a name="choose"></a> Control flow</span></span>  
 <span data-ttu-id="1352e-124">Hello `choose` политики применяются встраиваемые правила, операторы в зависимости от результата вычисления логических выражений, аналогичные tooan if-then-else или коммутатор hello конструкции в языке программирования.</span><span class="sxs-lookup"><span data-stu-id="1352e-124">hello `choose` policy applies enclosed policy statements based on hello outcome of evaluation of Boolean expressions, similar tooan if-then-else or a switch construct in a programming language.</span></span>  
  
###  <span data-ttu-id="1352e-125"><a name="ChoosePolicyStatement"></a> Правило политики</span><span class="sxs-lookup"><span data-stu-id="1352e-125"><a name="ChoosePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<choose>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <when condition="Boolean expression | Boolean constant">   
        <!— one or more policy statements toobe applied if hello above condition is true  -->  
    </when>   
    <otherwise>   
        <!— one or more policy statements toobe applied if none of hello above conditions are true  -->  
</otherwise>   
</choose>  
```  
  
 <span data-ttu-id="1352e-126">Hello политика потока управления должен содержать по крайней мере один `<when/>` элемента.</span><span class="sxs-lookup"><span data-stu-id="1352e-126">hello control flow policy must contain at least one `<when/>` element.</span></span> <span data-ttu-id="1352e-127">Hello `<otherwise/>` элемент является необязательным.</span><span class="sxs-lookup"><span data-stu-id="1352e-127">hello `<otherwise/>` element is optional.</span></span> <span data-ttu-id="1352e-128">Условия в `<when/>` элементы оцениваются в порядке их следования в политике hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-128">Conditions in `<when/>` elements are evaluated in order of their appearance within hello policy.</span></span> <span data-ttu-id="1352e-129">Правила политики, включенные в hello сначала `<when/>` элемент с атрибутом условия, равным `true` будут применены.</span><span class="sxs-lookup"><span data-stu-id="1352e-129">Policy statement(s) enclosed within hello first `<when/>` element with condition attribute equals `true` will be applied.</span></span> <span data-ttu-id="1352e-130">Политики, заключенный в hello `<otherwise/>` элемент, если он имеется, будут применяться, если все из hello `<when/>` являются атрибуты условий для элемента `false`.</span><span class="sxs-lookup"><span data-stu-id="1352e-130">Policies enclosed within hello `<otherwise/>` element, if present, will be applied if all of hello `<when/>` element condition attributes are `false`.</span></span>  
  
### <a name="examples"></a><span data-ttu-id="1352e-131">Примеры</span><span class="sxs-lookup"><span data-stu-id="1352e-131">Examples</span></span>  
  
####  <span data-ttu-id="1352e-132"><a name="ChooseExample"></a> Пример</span><span class="sxs-lookup"><span data-stu-id="1352e-132"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="1352e-133">Hello ниже приведен пример [set-variable](api-management-advanced-policies.md#set-variable) политики и две политики потока управления.</span><span class="sxs-lookup"><span data-stu-id="1352e-133">hello following example demonstrates a [set-variable](api-management-advanced-policies.md#set-variable) policy and two control flow policies.</span></span>  
  
 <span data-ttu-id="1352e-134">политика задания переменной в Hello находится в разделе "Входящие" Здравствуйте и создает `isMobile` логическое [контекста](api-management-policy-expressions.md#ContextVariables) переменной, которая имеет значение tootrue, если hello `User-Agent` заголовок запроса содержит текст hello `iPad` или `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="1352e-134">hello set variable policy is in hello inbound section and creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set tootrue if hello `User-Agent` request header contains hello text `iPad` or `iPhone`.</span></span>  
  
 <span data-ttu-id="1352e-135">Первая политика потока управления Hello также находится в разделе "Входящие" Здравствуйте и определяет условное применение одной из двух [параметра строки запроса](api-management-transformation-policies.md#SetQueryStringParameter) политики в зависимости от значения hello hello `isMobile` переменной контекста.</span><span class="sxs-lookup"><span data-stu-id="1352e-135">hello first control flow policy is also in hello inbound section, and conditionally applies one of two [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policies depending on hello value of hello `isMobile` context variable.</span></span>  
  
 <span data-ttu-id="1352e-136">Hello Вторая политика потока управления находится в разделе "Исходящие" hello и условно применяет hello [tooJSON преобразование XML](api-management-transformation-policies.md#ConvertXMLtoJSON) политики при `isMobile` задано слишком`true`.</span><span class="sxs-lookup"><span data-stu-id="1352e-136">hello second control flow policy is in hello outbound section and conditionally applies hello [Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) policy when `isMobile` is set too`true`.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="1352e-137">Пример</span><span class="sxs-lookup"><span data-stu-id="1352e-137">Example</span></span>  
 <span data-ttu-id="1352e-138">В этом примере показано, как tooperform фильтрация содержимого, удалив элементы данных из ответа hello получил от службы внутренних hello при использовании hello `Starter` продукта.</span><span class="sxs-lookup"><span data-stu-id="1352e-138">This example shows how tooperform content filtering by removing data elements from hello response received from hello backend service when using hello `Starter` product.</span></span> <span data-ttu-id="1352e-139">Демонстрацию настройке и использовании этой политики см. в разделе [177 серии охватывают облачные: более возможности API управления с помощью Влад Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) и too34:30 Перемотка вперед.</span><span class="sxs-lookup"><span data-stu-id="1352e-139">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too34:30.</span></span> <span data-ttu-id="1352e-140">Начинаются с 31:50 toosee Обзор [hello темной API прогноз Sky](https://developer.forecast.io/) для этой демонстрации.</span><span class="sxs-lookup"><span data-stu-id="1352e-140">Start  at 31:50 toosee an overview of [hello Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into hello outbound section tooremove a number of data elements from hello response received from hello backend service based on hello name of hello api product -->  
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
  
### <a name="elements"></a><span data-ttu-id="1352e-141">Элементы</span><span class="sxs-lookup"><span data-stu-id="1352e-141">Elements</span></span>  
  
|<span data-ttu-id="1352e-142">Элемент</span><span class="sxs-lookup"><span data-stu-id="1352e-142">Element</span></span>|<span data-ttu-id="1352e-143">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-143">Description</span></span>|<span data-ttu-id="1352e-144">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-144">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1352e-145">choose</span><span class="sxs-lookup"><span data-stu-id="1352e-145">choose</span></span>|<span data-ttu-id="1352e-146">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="1352e-146">Root element.</span></span>|<span data-ttu-id="1352e-147">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-147">Yes</span></span>|  
|<span data-ttu-id="1352e-148">when</span><span class="sxs-lookup"><span data-stu-id="1352e-148">when</span></span>|<span data-ttu-id="1352e-149">Здравствуйте, toouse условие для hello `if` или `ifelse` части hello `choose` политики.</span><span class="sxs-lookup"><span data-stu-id="1352e-149">hello condition toouse for hello `if` or `ifelse` parts of hello `choose` policy.</span></span> <span data-ttu-id="1352e-150">Если hello `choose` политика содержит несколько `when` разделы, они вычисляются последовательно.</span><span class="sxs-lookup"><span data-stu-id="1352e-150">If hello `choose` policy has multiple `when` sections, they are evaluated sequentially.</span></span> <span data-ttu-id="1352e-151">Здравствуйте, один раз `condition` when элемент оценивается как слишком`true`, последующие `when` оценки условий.</span><span class="sxs-lookup"><span data-stu-id="1352e-151">Once hello `condition` of a when element evaluates too`true`, no further `when` conditions are evaluated.</span></span>|<span data-ttu-id="1352e-152">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-152">Yes</span></span>|  
|<span data-ttu-id="1352e-153">otherwise</span><span class="sxs-lookup"><span data-stu-id="1352e-153">otherwise</span></span>|<span data-ttu-id="1352e-154">Содержит фрагмент toobe hello политики, используется, если ни один из hello `when` условия соблюдаются слишком`true`.</span><span class="sxs-lookup"><span data-stu-id="1352e-154">Contains hello policy snippet toobe used if none of hello `when` conditions evaluate too`true`.</span></span>|<span data-ttu-id="1352e-155">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-155">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1352e-156">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="1352e-156">Attributes</span></span>  
  
|<span data-ttu-id="1352e-157">Атрибут</span><span class="sxs-lookup"><span data-stu-id="1352e-157">Attribute</span></span>|<span data-ttu-id="1352e-158">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-158">Description</span></span>|<span data-ttu-id="1352e-159">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-159">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="1352e-160">condition="Логическое выражение &#124; Логическая константа"</span><span class="sxs-lookup"><span data-stu-id="1352e-160">condition="Boolean expression &#124; Boolean constant"</span></span>|<span data-ttu-id="1352e-161">Логическое выражение или константа tooevaluated при Здравствуйте, содержащий Hello `when` вычисляется правила политики.</span><span class="sxs-lookup"><span data-stu-id="1352e-161">hello Boolean expression or constant tooevaluated when hello containing `when` policy statement is evaluated.</span></span>|<span data-ttu-id="1352e-162">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-162">Yes</span></span>|  
  
###  <span data-ttu-id="1352e-163"><a name="ChooseUsage"></a> Использование</span><span class="sxs-lookup"><span data-stu-id="1352e-163"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="1352e-164">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1352e-164">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1352e-165">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="1352e-165">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1352e-166">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="1352e-166">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1352e-167"><a name="ForwardRequest"></a> Перенаправляющий запрос</span><span class="sxs-lookup"><span data-stu-id="1352e-167"><a name="ForwardRequest"></a> Forward request</span></span>  
 <span data-ttu-id="1352e-168">Hello `forward-request` политика направляет hello входящего запроса toohello серверной службе указанный в запросе hello [контекста](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="1352e-168">hello `forward-request` policy forwards hello incoming request toohello backend service specified in hello request [context](api-management-policy-expressions.md#ContextVariables).</span></span> <span data-ttu-id="1352e-169">Hello URL-адрес внутренней службы задается в hello API [параметры](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) и может быть изменено с помощью hello [задать серверной службы](api-management-transformation-policies.md) политики.</span><span class="sxs-lookup"><span data-stu-id="1352e-169">hello backend service URL is specified in hello API  [settings](https://azure.microsoft.com/documentation/articles/api-management-howto-create-apis/#configure-api-settings) and can be changed using hello [set backend service](api-management-transformation-policies.md) policy.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="1352e-170">Удаление результатов этой политики в запросе hello не направляются toohello серверной службы hello политики и в разделе "Исходящие" hello вычисляются сразу после успешного завершения hello политик hello в hello входящих раздела.</span><span class="sxs-lookup"><span data-stu-id="1352e-170">Removing this policy results in hello request not being forwarded toohello backend service and hello policies in hello outbound section are evaluated immediately upon hello successful completion of hello policies in hello inbound section.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1352e-171">Правило политики</span><span class="sxs-lookup"><span data-stu-id="1352e-171">Policy statement</span></span>  
  
```xml  
<forward-request timeout="time in seconds" follow-redirects="true | false"/>  
```  
  
### <a name="examples"></a><span data-ttu-id="1352e-172">Примеры</span><span class="sxs-lookup"><span data-stu-id="1352e-172">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="1352e-173">Пример</span><span class="sxs-lookup"><span data-stu-id="1352e-173">Example</span></span>  
 <span data-ttu-id="1352e-174">Hello следующую политику уровня API направляет все запросы toohello серверной службы с интервалом 60 секунд времени ожидания.</span><span class="sxs-lookup"><span data-stu-id="1352e-174">hello following API level policy forwards all requests toohello backend service with a timeout interval of 60 seconds.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="1352e-175">Пример</span><span class="sxs-lookup"><span data-stu-id="1352e-175">Example</span></span>  
 <span data-ttu-id="1352e-176">Этот уровень политики операция использует hello `base` элемент tooinherit hello серверной политики из hello родительской API уровня области.</span><span class="sxs-lookup"><span data-stu-id="1352e-176">This operation level policy uses hello `base` element tooinherit hello backend policy from hello parent API level scope.</span></span>  
  
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
  
#### <a name="example"></a><span data-ttu-id="1352e-177">Пример</span><span class="sxs-lookup"><span data-stu-id="1352e-177">Example</span></span>  
 <span data-ttu-id="1352e-178">Эта политика уровня операции явным образом направляет все запросы toohello серверной службы с временем ожидания 120 и не наследует родительский hello API уровня политики.</span><span class="sxs-lookup"><span data-stu-id="1352e-178">This operation level policy explicitly forwards all requests toohello backend service with a timeout of 120 and does not inherit hello parent API level backend policy.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <forward-request timeout="120"/>   
        <!-- effective policy. note hello absence of <base/> -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="1352e-179">Пример</span><span class="sxs-lookup"><span data-stu-id="1352e-179">Example</span></span>  
 <span data-ttu-id="1352e-180">Этот уровень политики операции не перенаправляет запросы toohello внутренней службы.</span><span class="sxs-lookup"><span data-stu-id="1352e-180">This operation level policy does not forward requests toohello backend service.</span></span>  
  
```xml  
<!-- operation level -->  
<policies>  
    <inbound>  
        <base/>  
    </inbound>  
    <backend>  
        <!-- no forwarding toobackend -->  
    </backend>  
    <outbound>  
        <base/>          
    </outbound>  
</policies>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="1352e-181">Элементы</span><span class="sxs-lookup"><span data-stu-id="1352e-181">Elements</span></span>  
  
|<span data-ttu-id="1352e-182">Элемент</span><span class="sxs-lookup"><span data-stu-id="1352e-182">Element</span></span>|<span data-ttu-id="1352e-183">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-183">Description</span></span>|<span data-ttu-id="1352e-184">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-184">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1352e-185">forward-request</span><span class="sxs-lookup"><span data-stu-id="1352e-185">forward-request</span></span>|<span data-ttu-id="1352e-186">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="1352e-186">Root element.</span></span>|<span data-ttu-id="1352e-187">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-187">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1352e-188">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="1352e-188">Attributes</span></span>  
  
|<span data-ttu-id="1352e-189">Атрибут</span><span class="sxs-lookup"><span data-stu-id="1352e-189">Attribute</span></span>|<span data-ttu-id="1352e-190">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-190">Description</span></span>|<span data-ttu-id="1352e-191">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-191">Required</span></span>|<span data-ttu-id="1352e-192">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="1352e-192">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1352e-193">timeout="целое число"</span><span class="sxs-lookup"><span data-stu-id="1352e-193">timeout="integer"</span></span>|<span data-ttu-id="1352e-194">Hello интервал времени ожидания в секундах перед сбоем hello вызовов toohello внутренней службы.</span><span class="sxs-lookup"><span data-stu-id="1352e-194">hello timeout interval in seconds before hello call toohello backend service fails.</span></span>|<span data-ttu-id="1352e-195">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-195">No</span></span>|<span data-ttu-id="1352e-196">Время ожидания отсутствует</span><span class="sxs-lookup"><span data-stu-id="1352e-196">No timeout</span></span>|  
|<span data-ttu-id="1352e-197">follow-redirects="true &#124; false"</span><span class="sxs-lookup"><span data-stu-id="1352e-197">follow-redirects="true &#124; false"</span></span>|<span data-ttu-id="1352e-198">Указывает, следуют hello шлюза или возвращаемый вызывающий объект toohello перенаправлений с серверной службе hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-198">Specifies whether redirects from hello backend service are followed by hello gateway or returned toohello caller.</span></span>|<span data-ttu-id="1352e-199">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-199">No</span></span>|<span data-ttu-id="1352e-200">нет</span><span class="sxs-lookup"><span data-stu-id="1352e-200">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1352e-201">Использование</span><span class="sxs-lookup"><span data-stu-id="1352e-201">Usage</span></span>  
 <span data-ttu-id="1352e-202">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1352e-202">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1352e-203">**Разделы политики:** backend.</span><span class="sxs-lookup"><span data-stu-id="1352e-203">**Policy sections:** backend</span></span>  
  
-   <span data-ttu-id="1352e-204">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="1352e-204">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1352e-205"><a name="LimitConcurrency"></a> Ограничение параллелизма</span><span class="sxs-lookup"><span data-stu-id="1352e-205"><a name="LimitConcurrency"></a> Limit concurrency</span></span>  
 <span data-ttu-id="1352e-206">Hello `limit-concurrency` политика запрещает заключенными политики выполнения более чем hello заданного количества запросов в определенный момент времени.</span><span class="sxs-lookup"><span data-stu-id="1352e-206">hello `limit-concurrency` policy prevents enclosed policies from executing by more than hello specified number of requests at a given time.</span></span> <span data-ttu-id="1352e-207">После превышения порогового значения hello, новые запросы добавляются tooa очереди, пока не удастся hello максимум длины очереди.</span><span class="sxs-lookup"><span data-stu-id="1352e-207">Upon exceeding hello threshold, new requests are added tooa queue, until hello maximum queue length is achieved.</span></span> <span data-ttu-id="1352e-208">Когда очередь заполнится, новые запросы немедленно завершатся ошибкой.</span><span class="sxs-lookup"><span data-stu-id="1352e-208">Upon queue exhaustion, new requests will fail immediately.</span></span>
  
###  <span data-ttu-id="1352e-209"><a name="LimitConcurrencyStatement"></a> Правило политики</span><span class="sxs-lookup"><span data-stu-id="1352e-209"><a name="LimitConcurrencyStatement"></a> Policy statement</span></span>  
  
```xml  
<limit-concurrency key="expression" max-count="number" timeout="in seconds" max-queue-length="number">
        <!— nested policy statements -->  
</limit-concurrency>
``` 

### <a name="examples"></a><span data-ttu-id="1352e-210">Примеры</span><span class="sxs-lookup"><span data-stu-id="1352e-210">Examples</span></span>  
  
####  <span data-ttu-id="1352e-211"><a name="ChooseExample"></a> Пример</span><span class="sxs-lookup"><span data-stu-id="1352e-211"><a name="ChooseExample"></a> Example</span></span>  
 <span data-ttu-id="1352e-212">Hello следующем примере показано, как toolimit число запросов, пересылаемые tooa серверной части, на основе значения hello переменной контекста.</span><span class="sxs-lookup"><span data-stu-id="1352e-212">hello following example demonstrates how toolimit number of requests forwarded tooa backend based on hello value of a context variable.</span></span>
 
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

### <a name="elements"></a><span data-ttu-id="1352e-213">Элементы</span><span class="sxs-lookup"><span data-stu-id="1352e-213">Elements</span></span>  
  
|<span data-ttu-id="1352e-214">Элемент</span><span class="sxs-lookup"><span data-stu-id="1352e-214">Element</span></span>|<span data-ttu-id="1352e-215">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-215">Description</span></span>|<span data-ttu-id="1352e-216">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-216">Required</span></span>|  
|-------------|-----------------|--------------|    
|<span data-ttu-id="1352e-217">limit-concurrency</span><span class="sxs-lookup"><span data-stu-id="1352e-217">limit-concurrency</span></span>|<span data-ttu-id="1352e-218">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="1352e-218">Root element.</span></span>|<span data-ttu-id="1352e-219">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1352e-220">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="1352e-220">Attributes</span></span>  
  
|<span data-ttu-id="1352e-221">Атрибут</span><span class="sxs-lookup"><span data-stu-id="1352e-221">Attribute</span></span>|<span data-ttu-id="1352e-222">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-222">Description</span></span>|<span data-ttu-id="1352e-223">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-223">Required</span></span>|<span data-ttu-id="1352e-224">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="1352e-224">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="1352e-225">key</span><span class="sxs-lookup"><span data-stu-id="1352e-225">key</span></span>|<span data-ttu-id="1352e-226">Строка.</span><span class="sxs-lookup"><span data-stu-id="1352e-226">A string.</span></span> <span data-ttu-id="1352e-227">Допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="1352e-227">Expression allowed.</span></span> <span data-ttu-id="1352e-228">Указывает область hello параллелизма.</span><span class="sxs-lookup"><span data-stu-id="1352e-228">Specifies hello concurrency scope.</span></span> <span data-ttu-id="1352e-229">Используется несколькими политиками.</span><span class="sxs-lookup"><span data-stu-id="1352e-229">Can be shared by multiple policies.</span></span>|<span data-ttu-id="1352e-230">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-230">Yes</span></span>|<span data-ttu-id="1352e-231">Недоступно</span><span class="sxs-lookup"><span data-stu-id="1352e-231">N/A</span></span>|  
|<span data-ttu-id="1352e-232">max-count</span><span class="sxs-lookup"><span data-stu-id="1352e-232">max-count</span></span>|<span data-ttu-id="1352e-233">Целое число.</span><span class="sxs-lookup"><span data-stu-id="1352e-233">An integer.</span></span> <span data-ttu-id="1352e-234">Указывает максимальное число запросов, разрешенных политикой tooenter hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-234">Specifies a maximum number of requests that are allowed tooenter hello policy.</span></span>|<span data-ttu-id="1352e-235">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-235">Yes</span></span>|<span data-ttu-id="1352e-236">Недоступно</span><span class="sxs-lookup"><span data-stu-id="1352e-236">N/A</span></span>|  
|<span data-ttu-id="1352e-237">timeout</span><span class="sxs-lookup"><span data-stu-id="1352e-237">timeout</span></span>|<span data-ttu-id="1352e-238">Целое число.</span><span class="sxs-lookup"><span data-stu-id="1352e-238">An integer.</span></span> <span data-ttu-id="1352e-239">Допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="1352e-239">Expression allowed.</span></span> <span data-ttu-id="1352e-240">Указывает количество секунд, запрос будет ожидать tooenter области до появления в hello «403 слишком много запросов»</span><span class="sxs-lookup"><span data-stu-id="1352e-240">Specifies hello number of seconds a request should wait tooenter a scope before failing with "403 Too Many Requests"</span></span>|<span data-ttu-id="1352e-241">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-241">No</span></span>|<span data-ttu-id="1352e-242">Infinity</span><span class="sxs-lookup"><span data-stu-id="1352e-242">Infinity</span></span>|  
|<span data-ttu-id="1352e-243">max-queue-length</span><span class="sxs-lookup"><span data-stu-id="1352e-243">max-queue-length</span></span>|<span data-ttu-id="1352e-244">Целое число.</span><span class="sxs-lookup"><span data-stu-id="1352e-244">An integer.</span></span> <span data-ttu-id="1352e-245">Допустимое выражение.</span><span class="sxs-lookup"><span data-stu-id="1352e-245">Expression allowed.</span></span> <span data-ttu-id="1352e-246">Указывает hello максимум длины очереди.</span><span class="sxs-lookup"><span data-stu-id="1352e-246">Specifies hello maximum queue length.</span></span> <span data-ttu-id="1352e-247">Входящие запросы попытки tooenter эта политика будет остановлен с «403 слишком много запросов» немедленно при исчерпании hello очереди.</span><span class="sxs-lookup"><span data-stu-id="1352e-247">Incoming requests trying tooenter this policy will be terminated with “403 Too Many Requests” immediately when hello queue is exhausted.</span></span>|<span data-ttu-id="1352e-248">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-248">No</span></span>|<span data-ttu-id="1352e-249">Infinity</span><span class="sxs-lookup"><span data-stu-id="1352e-249">Infinity</span></span>|  
  
###  <span data-ttu-id="1352e-250"><a name="ChooseUsage"></a> Использование</span><span class="sxs-lookup"><span data-stu-id="1352e-250"><a name="ChooseUsage"></a> Usage</span></span>  
 <span data-ttu-id="1352e-251">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1352e-251">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1352e-252">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="1352e-252">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1352e-253">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="1352e-253">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="1352e-254"><a name="log-to-eventhub"></a>Журнал tooEvent концентратора</span><span class="sxs-lookup"><span data-stu-id="1352e-254"><a name="log-to-eventhub"></a> Log tooEvent Hub</span></span>  
 <span data-ttu-id="1352e-255">Hello `log-to-eventhub` политики отправляет сообщения в hello указан формат tooan концентратора событий, определяемые сущности средства ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="1352e-255">hello `log-to-eventhub` policy sends messages in hello specified format tooan Event Hub defined by a Logger entity.</span></span> <span data-ttu-id="1352e-256">Как и предполагает его имя, hello политика используется для сохранения выбранного запроса или ответа сведения о контексте для анализа сети или вне сети.</span><span class="sxs-lookup"><span data-stu-id="1352e-256">As its name implies, hello policy is used for saving selected request or response context information for online or offline analysis.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="1352e-257">Пошаговое руководство по настройке концентратора событий и ведение журнала событий, в разделе [как события управления API toolog концентраторов событий Azure с](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="1352e-257">For a step-by-step guide on configuring an event hub and logging events, see [How toolog API Management events with Azure Event Hubs](https://azure.microsoft.com/documentation/articles/api-management-howto-log-event-hubs/).</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1352e-258">Правило политики</span><span class="sxs-lookup"><span data-stu-id="1352e-258">Policy statement</span></span>  
  
```xml  
<log-to-eventhub logger-id="id of hello logger entity" partition-id="index of hello partition where messages are sent" partition-key="value used for partition assignment">  
  Expression returning a string toobe logged  
</log-to-eventhub>  
  
```  
  
### <a name="example"></a><span data-ttu-id="1352e-259">Пример</span><span class="sxs-lookup"><span data-stu-id="1352e-259">Example</span></span>  
 <span data-ttu-id="1352e-260">Любая строка может использоваться как toobe значение hello в концентраторы событий в журнал.</span><span class="sxs-lookup"><span data-stu-id="1352e-260">Any string can be used as hello value toobe logged in Event Hubs.</span></span> <span data-ttu-id="1352e-261">В этом примере hello даты и времени, имя развертывания службы, код запроса, IP-адрес и имя операции для всех входящих звонков, средства ведения журнала зарегистрирована hello концентратора событий регистрируется toohello `contoso-logger` идентификатор.</span><span class="sxs-lookup"><span data-stu-id="1352e-261">In this example hello date and time, deployment service name, request id, ip address, and operation name for all inbound calls are logged toohello event hub Logger registered with hello `contoso-logger` id.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="1352e-262">Элементы</span><span class="sxs-lookup"><span data-stu-id="1352e-262">Elements</span></span>  
  
|<span data-ttu-id="1352e-263">Элемент</span><span class="sxs-lookup"><span data-stu-id="1352e-263">Element</span></span>|<span data-ttu-id="1352e-264">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-264">Description</span></span>|<span data-ttu-id="1352e-265">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-265">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1352e-266">log-to-eventhub</span><span class="sxs-lookup"><span data-stu-id="1352e-266">log-to-eventhub</span></span>|<span data-ttu-id="1352e-267">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="1352e-267">Root element.</span></span> <span data-ttu-id="1352e-268">Hello значение этого элемента — концентратора событий tooyour toolog строку hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-268">hello value of this element is hello string toolog tooyour event hub.</span></span>|<span data-ttu-id="1352e-269">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-269">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1352e-270">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="1352e-270">Attributes</span></span>  
  
|<span data-ttu-id="1352e-271">Атрибут</span><span class="sxs-lookup"><span data-stu-id="1352e-271">Attribute</span></span>|<span data-ttu-id="1352e-272">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-272">Description</span></span>|<span data-ttu-id="1352e-273">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-273">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="1352e-274">logger-id</span><span class="sxs-lookup"><span data-stu-id="1352e-274">logger-id</span></span>|<span data-ttu-id="1352e-275">Идентификатор Hello hello средства ведения журнала зарегистрированные в службе управления API.</span><span class="sxs-lookup"><span data-stu-id="1352e-275">hello id of hello Logger registered with your API Management service.</span></span>|<span data-ttu-id="1352e-276">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-276">Yes</span></span>|  
|<span data-ttu-id="1352e-277">partition-id</span><span class="sxs-lookup"><span data-stu-id="1352e-277">partition-id</span></span>|<span data-ttu-id="1352e-278">Указывает индекс hello hello раздела, куда должны отправляться сообщения.</span><span class="sxs-lookup"><span data-stu-id="1352e-278">Specifies hello index of hello partition where messages are sent.</span></span>|<span data-ttu-id="1352e-279">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="1352e-279">Optional.</span></span> <span data-ttu-id="1352e-280">Этот атрибут не может использоваться, если используется `partition-key`.</span><span class="sxs-lookup"><span data-stu-id="1352e-280">This attribute may not be used if `partition-key` is used.</span></span>|  
|<span data-ttu-id="1352e-281">partition-key</span><span class="sxs-lookup"><span data-stu-id="1352e-281">partition-key</span></span>|<span data-ttu-id="1352e-282">Задает значение hello, используемое для назначения раздела при отправке сообщений.</span><span class="sxs-lookup"><span data-stu-id="1352e-282">Specifies hello value used for partition assignment when messages are sent.</span></span>|<span data-ttu-id="1352e-283">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="1352e-283">Optional.</span></span> <span data-ttu-id="1352e-284">Этот атрибут не может использоваться, если используется `partition-id`.</span><span class="sxs-lookup"><span data-stu-id="1352e-284">This attribute may not be used if `partition-id` is used.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1352e-285">Использование</span><span class="sxs-lookup"><span data-stu-id="1352e-285">Usage</span></span>  
 <span data-ttu-id="1352e-286">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1352e-286">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1352e-287">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="1352e-287">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1352e-288">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="1352e-288">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="1352e-289"><a name="mock-response"></a> Макетирование ответа</span><span class="sxs-lookup"><span data-stu-id="1352e-289"><a name="mock-response"></a> Mock response</span></span>  
<span data-ttu-id="1352e-290">Hello `mock-response`, как имя hello подразумевает, — использовать toomock интерфейсы API и операции.</span><span class="sxs-lookup"><span data-stu-id="1352e-290">hello `mock-response`, as hello name implies, is used toomock APIs and operations.</span></span> <span data-ttu-id="1352e-291">Он прерывает выполнение обычный конвейер и возвращает вызывающему объекту toohello макеты ответа.</span><span class="sxs-lookup"><span data-stu-id="1352e-291">It aborts normal pipeline execution and returns a mocked response toohello caller.</span></span> <span data-ttu-id="1352e-292">политика Hello всегда пытается tooreturn отклики наилучшее качество.</span><span class="sxs-lookup"><span data-stu-id="1352e-292">hello policy always tries tooreturn responses of highest fidelity.</span></span> <span data-ttu-id="1352e-293">При возможности, она предпочитает примеры содержимого ответа.</span><span class="sxs-lookup"><span data-stu-id="1352e-293">It prefers response content examples, whenever available.</span></span> <span data-ttu-id="1352e-294">Она создает примеры ответов из схем, если схемы указаны, а примеры — нет.</span><span class="sxs-lookup"><span data-stu-id="1352e-294">It generates sample responses from schemas, when schemas are provided and examples are not.</span></span> <span data-ttu-id="1352e-295">Если не найдены ни примеры, ни схемы, возвращаются ответы без содержимого.</span><span class="sxs-lookup"><span data-stu-id="1352e-295">If neither examples or schemas are found, responses with no content are returned.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="1352e-296">Правило политики</span><span class="sxs-lookup"><span data-stu-id="1352e-296">Policy statement</span></span>  
  
```xml  
<mock-response status-code="code" content-type="media type"/>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="1352e-297">Примеры</span><span class="sxs-lookup"><span data-stu-id="1352e-297">Examples</span></span>  
  
```xml  
<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code. First found content type is used. If no example or schema is found, hello content is empty. -->
<mock-response/>

<!-- Returns 200 OK status code. Content is based on an example or schema, if provided for this 
status code and media type. If no example or schema found, hello content is empty. -->
<mock-response status-code='200' content-type='application/json'/>  
```  
  
### <a name="elements"></a><span data-ttu-id="1352e-298">Элементы</span><span class="sxs-lookup"><span data-stu-id="1352e-298">Elements</span></span>  
  
|<span data-ttu-id="1352e-299">Элемент</span><span class="sxs-lookup"><span data-stu-id="1352e-299">Element</span></span>|<span data-ttu-id="1352e-300">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-300">Description</span></span>|<span data-ttu-id="1352e-301">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-301">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1352e-302">mock-response</span><span class="sxs-lookup"><span data-stu-id="1352e-302">mock-response</span></span>|<span data-ttu-id="1352e-303">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="1352e-303">Root element.</span></span>|<span data-ttu-id="1352e-304">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-304">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1352e-305">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="1352e-305">Attributes</span></span>  
  
|<span data-ttu-id="1352e-306">Атрибут</span><span class="sxs-lookup"><span data-stu-id="1352e-306">Attribute</span></span>|<span data-ttu-id="1352e-307">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-307">Description</span></span>|<span data-ttu-id="1352e-308">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-308">Required</span></span>|<span data-ttu-id="1352e-309">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="1352e-309">Default</span></span>|  
|---------------|-----------------|--------------|--------------|  
|<span data-ttu-id="1352e-310">status-code</span><span class="sxs-lookup"><span data-stu-id="1352e-310">status-code</span></span>|<span data-ttu-id="1352e-311">Указывает код состояния ответа и соответствующий пример используется tooselect или схемы.</span><span class="sxs-lookup"><span data-stu-id="1352e-311">Specifies response status code and is used tooselect corresponding example or schema.</span></span>|<span data-ttu-id="1352e-312">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-312">No</span></span>|<span data-ttu-id="1352e-313">200</span><span class="sxs-lookup"><span data-stu-id="1352e-313">200</span></span>|  
|<span data-ttu-id="1352e-314">content-type</span><span class="sxs-lookup"><span data-stu-id="1352e-314">content-type</span></span>|<span data-ttu-id="1352e-315">Указывает `Content-Type` значение заголовка ответа и соответствующий пример используется tooselect или схемы.</span><span class="sxs-lookup"><span data-stu-id="1352e-315">Specifies `Content-Type` response header value and is used tooselect corresponding example or schema.</span></span>|<span data-ttu-id="1352e-316">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-316">No</span></span>|<span data-ttu-id="1352e-317">None</span><span class="sxs-lookup"><span data-stu-id="1352e-317">None</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1352e-318">Использование</span><span class="sxs-lookup"><span data-stu-id="1352e-318">Usage</span></span>  
 <span data-ttu-id="1352e-319">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1352e-319">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1352e-320">**Разделы политики:** inbound, outbound, on-error.</span><span class="sxs-lookup"><span data-stu-id="1352e-320">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="1352e-321">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="1352e-321">**Policy scopes:** all scopes</span></span>

##  <span data-ttu-id="1352e-322"><a name="Retry"></a> Повтор</span><span class="sxs-lookup"><span data-stu-id="1352e-322"><a name="Retry"></a> Retry</span></span>  
 <span data-ttu-id="1352e-323">Hello `retry` политики один раз выполняет свои дочерние политики, а затем повторяет их выполнение до попытки hello `condition` становится `false` или повторите `count` израсходована.</span><span class="sxs-lookup"><span data-stu-id="1352e-323">hello             `retry` policy executes its child policies once and then retries their execution until hello retry `condition` becomes            `false` or retry            `count` is exhausted.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1352e-324">Правило политики</span><span class="sxs-lookup"><span data-stu-id="1352e-324">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="1352e-325">Пример</span><span class="sxs-lookup"><span data-stu-id="1352e-325">Example</span></span>  
 <span data-ttu-id="1352e-326">Копирование tooten раз, используя алгоритм повторения экспоненциального следующий пример запроса forewarding повторяется в hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-326">In hello following example request forewarding is retried up tooten times using exponential retry algorithm.</span></span> <span data-ttu-id="1352e-327">Поскольку `first-fast-retry` задано toofalse, все повторных попыток, алгоритм повторного exponsntial toohello субъекта.</span><span class="sxs-lookup"><span data-stu-id="1352e-327">Since                    `first-fast-retry` is set toofalse, all retry attempts are subject toohello exponsntial retry algorithm.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="1352e-328">Элементы</span><span class="sxs-lookup"><span data-stu-id="1352e-328">Elements</span></span>  
  
|<span data-ttu-id="1352e-329">Элемент</span><span class="sxs-lookup"><span data-stu-id="1352e-329">Element</span></span>|<span data-ttu-id="1352e-330">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-330">Description</span></span>|<span data-ttu-id="1352e-331">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-331">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1352e-332">retry</span><span class="sxs-lookup"><span data-stu-id="1352e-332">retry</span></span>|<span data-ttu-id="1352e-333">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="1352e-333">Root element.</span></span> <span data-ttu-id="1352e-334">Может содержать любые другие политики в качестве дочерних элементов.</span><span class="sxs-lookup"><span data-stu-id="1352e-334">May contain any other policies as its child elements.</span></span>|<span data-ttu-id="1352e-335">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-335">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1352e-336">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="1352e-336">Attributes</span></span>  
  
|<span data-ttu-id="1352e-337">Атрибут</span><span class="sxs-lookup"><span data-stu-id="1352e-337">Attribute</span></span>|<span data-ttu-id="1352e-338">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-338">Description</span></span>|<span data-ttu-id="1352e-339">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-339">Required</span></span>|<span data-ttu-id="1352e-340">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="1352e-340">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1352e-341">condition</span><span class="sxs-lookup"><span data-stu-id="1352e-341">condition</span></span>|<span data-ttu-id="1352e-342">Логический литерал или [выражение](api-management-policy-expressions.md), указывающее, что нужно сделать: прекратить повторные попытки (`false`) или продолжить (`true`).</span><span class="sxs-lookup"><span data-stu-id="1352e-342">A boolean literal or [expression](api-management-policy-expressions.md) specifying if retries should be stopped (`false`) or continued (`true`).</span></span>|<span data-ttu-id="1352e-343">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-343">Yes</span></span>|<span data-ttu-id="1352e-344">Недоступно</span><span class="sxs-lookup"><span data-stu-id="1352e-344">N/A</span></span>|  
|<span data-ttu-id="1352e-345">count</span><span class="sxs-lookup"><span data-stu-id="1352e-345">count</span></span>|<span data-ttu-id="1352e-346">Положительное число, указывающее максимальное число повторных попыток tooattempt hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-346">A positive number specifying hello maximum number of retries tooattempt.</span></span>|<span data-ttu-id="1352e-347">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-347">Yes</span></span>|<span data-ttu-id="1352e-348">Недоступно</span><span class="sxs-lookup"><span data-stu-id="1352e-348">N/A</span></span>|  
|<span data-ttu-id="1352e-349">interval</span><span class="sxs-lookup"><span data-stu-id="1352e-349">interval</span></span>|<span data-ttu-id="1352e-350">Положительное число, в секундах, указав hello интервал ожидания между попытками повтора hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-350">A positive number in seconds specifying hello wait interval between hello retry attempts.</span></span>|<span data-ttu-id="1352e-351">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-351">Yes</span></span>|<span data-ttu-id="1352e-352">Недоступно</span><span class="sxs-lookup"><span data-stu-id="1352e-352">N/A</span></span>|  
|<span data-ttu-id="1352e-353">max-interval</span><span class="sxs-lookup"><span data-stu-id="1352e-353">max-interval</span></span>|<span data-ttu-id="1352e-354">Положительное число, в секундах, указав hello интервал ожидания между попытками повтора hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-354">A positive number in seconds specifying hello maximum wait interval between hello retry attempts.</span></span> <span data-ttu-id="1352e-355">Это используется tooimplement алгоритм экспоненциального повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="1352e-355">It is used tooimplement an exponential retry algorithm.</span></span>|<span data-ttu-id="1352e-356">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-356">No</span></span>|<span data-ttu-id="1352e-357">Недоступно</span><span class="sxs-lookup"><span data-stu-id="1352e-357">N/A</span></span>|  
|<span data-ttu-id="1352e-358">delta</span><span class="sxs-lookup"><span data-stu-id="1352e-358">delta</span></span>|<span data-ttu-id="1352e-359">Положительное число, в секундах, указав приращения интервал ожидания hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-359">A positive number in seconds specifying hello wait interval increment.</span></span> <span data-ttu-id="1352e-360">Это алгоритмы линейной и экспоненциальный повторных попыток используется tooimplement hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-360">It is used tooimplement hello linear and exponential retry algorithms.</span></span>|<span data-ttu-id="1352e-361">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-361">No</span></span>|<span data-ttu-id="1352e-362">Недоступно</span><span class="sxs-lookup"><span data-stu-id="1352e-362">N/A</span></span>|  
|<span data-ttu-id="1352e-363">first-fast-retry</span><span class="sxs-lookup"><span data-stu-id="1352e-363">first-fast-retry</span></span>|<span data-ttu-id="1352e-364">Если задать слишком `true` , первой попытки повтора hello вступает в силу немедленно.</span><span class="sxs-lookup"><span data-stu-id="1352e-364">If set too                                   `true` , hello first retry attempt is performed immediately.</span></span>|<span data-ttu-id="1352e-365">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-365">No</span></span>|`false`|  
  
> [!NOTE]
>  <span data-ttu-id="1352e-366">Если только hello `interval` указано, **фиксированной** выполняются интервал повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="1352e-366">When only hello `interval` is specified, **fixed** interval retries are performed.</span></span>  
>  <span data-ttu-id="1352e-367">Если только hello `interval` и `delta` указаны, **линейной** используется алгоритм интервал повторения, где время ожидания между повторными попытками вычисляемые соответствующим hello следующую формулу - `interval + (count - 1)*delta`.</span><span class="sxs-lookup"><span data-stu-id="1352e-367">When only hello `interval` and `delta` are specified, a **linear** interval retry algorithm is used, where wait time between retries is calculated according hello following formula - `interval + (count - 1)*delta`.</span></span>  
>  <span data-ttu-id="1352e-368">Здравствуйте, когда `interval`, `max-interval` и `delta` указаны, **экспоненциального** применяется алгоритм интервал повторения, где hello время ожидания между повторными попытками hello растут по экспоненте значению hello `interval`значение toohello `max-interval` toohello ниже в соответствии с forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span><span class="sxs-lookup"><span data-stu-id="1352e-368">When hello `interval`, `max-interval` and `delta` are specified, **exponential** interval retry algorithm is applied, where hello wait time between hello retries is growing exponentially from hello value of `interval` toohello value `max-interval` according toohello following forumula - `min(interval + (2^count - 1) * random(delta * 0.8, delta * 1.2), max-interval)`.</span></span>  
  
### <a name="usage"></a><span data-ttu-id="1352e-369">Использование</span><span class="sxs-lookup"><span data-stu-id="1352e-369">Usage</span></span>  
 <span data-ttu-id="1352e-370">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="1352e-370">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span> <span data-ttu-id="1352e-371">Обратите внимание, что эта политика наследует ограничения использования дочерних политик.</span><span class="sxs-lookup"><span data-stu-id="1352e-371">Note that child policy usage restrictions will be inherited by this policy.</span></span>  
  
-   <span data-ttu-id="1352e-372">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="1352e-372">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1352e-373">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="1352e-373">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1352e-374"><a name="ReturnResponse"></a> Возврат ответа</span><span class="sxs-lookup"><span data-stu-id="1352e-374"><a name="ReturnResponse"></a> Return response</span></span>  
 <span data-ttu-id="1352e-375">Hello `return-response` политики прерывает выполнение конвейера и возвращает пользовательский ответ toohello вызывающего или по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1352e-375">hello `return-response` policy aborts pipeline execution and returns either a default or custom response toohello caller.</span></span> <span data-ttu-id="1352e-376">По умолчанию возвращается код `200 OK` без текста.</span><span class="sxs-lookup"><span data-stu-id="1352e-376">Default response is `200 OK` with no body.</span></span> <span data-ttu-id="1352e-377">Можно указать настраиваемый ответ с помощью переменной контекста или правил политики.</span><span class="sxs-lookup"><span data-stu-id="1352e-377">Custom response can be specified via a context variable or policy statements.</span></span> <span data-ttu-id="1352e-378">Если указаны оба hello содержащихся в переменной контекста hello изменении ответа посредством инструкции политики hello перед возвращением toohello вызывающего объекта.</span><span class="sxs-lookup"><span data-stu-id="1352e-378">When both are provided, hello response contained within hello context variable is modified by hello policy statements before being returned toohello caller.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1352e-379">Правило политики</span><span class="sxs-lookup"><span data-stu-id="1352e-379">Policy statement</span></span>  
  
```xml  
<return-response response-variable-name="existing context variable">  
  <set-header/>  
  <set-body/>  
  <set-status/>  
</return-response>  
  
```  
  
### <a name="example"></a><span data-ttu-id="1352e-380">Пример</span><span class="sxs-lookup"><span data-stu-id="1352e-380">Example</span></span>  
  
```xml  
<return-response>  
   <set-status code="401" reason="Unauthorized"/>  
   <set-header name="WWW-Authenticate" exists-action="override">  
      <value>Bearer error="invalid_token"</value>  
   </set-header>  
</return-response>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="1352e-381">Элементы</span><span class="sxs-lookup"><span data-stu-id="1352e-381">Elements</span></span>  
  
|<span data-ttu-id="1352e-382">Элемент</span><span class="sxs-lookup"><span data-stu-id="1352e-382">Element</span></span>|<span data-ttu-id="1352e-383">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-383">Description</span></span>|<span data-ttu-id="1352e-384">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-384">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1352e-385">return-response</span><span class="sxs-lookup"><span data-stu-id="1352e-385">return-response</span></span>|<span data-ttu-id="1352e-386">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="1352e-386">Root element.</span></span>|<span data-ttu-id="1352e-387">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-387">Yes</span></span>|  
|<span data-ttu-id="1352e-388">set-header</span><span class="sxs-lookup"><span data-stu-id="1352e-388">set-header</span></span>|<span data-ttu-id="1352e-389">Правило политики [set-header](api-management-transformation-policies.md#SetHTTPheader).</span><span class="sxs-lookup"><span data-stu-id="1352e-389">A [set-header](api-management-transformation-policies.md#SetHTTPheader) policy statement.</span></span>|<span data-ttu-id="1352e-390">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-390">No</span></span>|  
|<span data-ttu-id="1352e-391">set-body</span><span class="sxs-lookup"><span data-stu-id="1352e-391">set-body</span></span>|<span data-ttu-id="1352e-392">Правило политики [set-body](api-management-transformation-policies.md#SetBody).</span><span class="sxs-lookup"><span data-stu-id="1352e-392">A [set-body](api-management-transformation-policies.md#SetBody) policy statement.</span></span>|<span data-ttu-id="1352e-393">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-393">No</span></span>|  
|<span data-ttu-id="1352e-394">set-status</span><span class="sxs-lookup"><span data-stu-id="1352e-394">set-status</span></span>|<span data-ttu-id="1352e-395">Правило политики [set-status](api-management-advanced-policies.md#SetStatus).</span><span class="sxs-lookup"><span data-stu-id="1352e-395">A [set-status](api-management-advanced-policies.md#SetStatus) policy statement.</span></span>|<span data-ttu-id="1352e-396">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-396">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1352e-397">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="1352e-397">Attributes</span></span>  
  
|<span data-ttu-id="1352e-398">Атрибут</span><span class="sxs-lookup"><span data-stu-id="1352e-398">Attribute</span></span>|<span data-ttu-id="1352e-399">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-399">Description</span></span>|<span data-ttu-id="1352e-400">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-400">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="1352e-401">response-variable-name</span><span class="sxs-lookup"><span data-stu-id="1352e-401">response-variable-name</span></span>|<span data-ttu-id="1352e-402">Hello переменной контекста hello ссылка на имя, например, вышестоящим [запрос на отправку](api-management-advanced-policies.md#SendRequest) политики и содержащий `Response` объекта</span><span class="sxs-lookup"><span data-stu-id="1352e-402">hello name of hello context variable referenced from, for example, an upstream [send-request](api-management-advanced-policies.md#SendRequest) policy and containing a `Response` object</span></span>|<span data-ttu-id="1352e-403">необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="1352e-403">Optional.</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1352e-404">Использование</span><span class="sxs-lookup"><span data-stu-id="1352e-404">Usage</span></span>  
 <span data-ttu-id="1352e-405">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1352e-405">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1352e-406">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="1352e-406">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1352e-407">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="1352e-407">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1352e-408"><a name="SendOneWayRequest"></a> Отправка одностороннего запроса</span><span class="sxs-lookup"><span data-stu-id="1352e-408"><a name="SendOneWayRequest"></a> Send one way request</span></span>  
 <span data-ttu-id="1352e-409">Hello `send-one-way-request` политики отправляет hello предоставленный toohello URL-адрес указан без ожидания ответа.</span><span class="sxs-lookup"><span data-stu-id="1352e-409">hello `send-one-way-request` policy sends hello provided request toohello specified URL without waiting for a response.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1352e-410">Правило политики</span><span class="sxs-lookup"><span data-stu-id="1352e-410">Policy statement</span></span>  
  
```xml  
<send-one-way-request mode="new | copy">  
  <url>...</url>  
  <method>...</method>  
  <header name="" exists-action="override | skip | append | delete">...</header>  
  <body>...</body>  
</send-one-way-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="1352e-411">Пример</span><span class="sxs-lookup"><span data-stu-id="1352e-411">Example</span></span>  
 <span data-ttu-id="1352e-412">Эта политика образец показывает пример использования hello `send-one-way-request` toosend политики сообщение tooa резерв чата Если hello код ответа HTTP больше или равно too500.</span><span class="sxs-lookup"><span data-stu-id="1352e-412">This sample policy shows an example of using hello `send-one-way-request` policy toosend a message tooa Slack chat room if hello HTTP response code is greater than or equal too500.</span></span> <span data-ttu-id="1352e-413">Дополнительные сведения об этом образце см. в разделе [с помощью внешних служб из hello службы управления API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="1352e-413">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="1352e-414">Элементы</span><span class="sxs-lookup"><span data-stu-id="1352e-414">Elements</span></span>  
  
|<span data-ttu-id="1352e-415">Элемент</span><span class="sxs-lookup"><span data-stu-id="1352e-415">Element</span></span>|<span data-ttu-id="1352e-416">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-416">Description</span></span>|<span data-ttu-id="1352e-417">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-417">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1352e-418">send-one-way-request</span><span class="sxs-lookup"><span data-stu-id="1352e-418">send-one-way-request</span></span>|<span data-ttu-id="1352e-419">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="1352e-419">Root element.</span></span>|<span data-ttu-id="1352e-420">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-420">Yes</span></span>|  
|<span data-ttu-id="1352e-421">url</span><span class="sxs-lookup"><span data-stu-id="1352e-421">url</span></span>|<span data-ttu-id="1352e-422">URL-адрес Hello hello запроса.</span><span class="sxs-lookup"><span data-stu-id="1352e-422">hello URL of hello request.</span></span>|<span data-ttu-id="1352e-423">Нет, если mode=copy. В противном случае да.</span><span class="sxs-lookup"><span data-stu-id="1352e-423">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="1352e-424">метод</span><span class="sxs-lookup"><span data-stu-id="1352e-424">method</span></span>|<span data-ttu-id="1352e-425">Здравствуйте, метод HTTP для запроса hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-425">hello HTTP method for hello request.</span></span>|<span data-ttu-id="1352e-426">Нет, если mode=copy. В противном случае да.</span><span class="sxs-lookup"><span data-stu-id="1352e-426">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="1352e-427">Верхний колонтитул</span><span class="sxs-lookup"><span data-stu-id="1352e-427">header</span></span>|<span data-ttu-id="1352e-428">Заголовок запроса.</span><span class="sxs-lookup"><span data-stu-id="1352e-428">Request header.</span></span> <span data-ttu-id="1352e-429">Используйте несколько элементов заголовка для нескольких заголовков запросов.</span><span class="sxs-lookup"><span data-stu-id="1352e-429">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="1352e-430">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-430">No</span></span>|  
|<span data-ttu-id="1352e-431">текст</span><span class="sxs-lookup"><span data-stu-id="1352e-431">body</span></span>|<span data-ttu-id="1352e-432">текст запроса Hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-432">hello request body.</span></span>|<span data-ttu-id="1352e-433">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-433">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1352e-434">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="1352e-434">Attributes</span></span>  
  
|<span data-ttu-id="1352e-435">Атрибут</span><span class="sxs-lookup"><span data-stu-id="1352e-435">Attribute</span></span>|<span data-ttu-id="1352e-436">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-436">Description</span></span>|<span data-ttu-id="1352e-437">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-437">Required</span></span>|<span data-ttu-id="1352e-438">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="1352e-438">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1352e-439">mode="строка"</span><span class="sxs-lookup"><span data-stu-id="1352e-439">mode="string"</span></span>|<span data-ttu-id="1352e-440">Определяет, является ли новый запрос или копию hello текущего запроса.</span><span class="sxs-lookup"><span data-stu-id="1352e-440">Determines whether this is a new request or a copy of hello current request.</span></span> <span data-ttu-id="1352e-441">В режиме исходящие режим = копирования не инициализирует hello текст запроса.</span><span class="sxs-lookup"><span data-stu-id="1352e-441">In outbound mode, mode=copy does not initialize hello request body.</span></span>|<span data-ttu-id="1352e-442">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-442">No</span></span>|<span data-ttu-id="1352e-443">Создать</span><span class="sxs-lookup"><span data-stu-id="1352e-443">New</span></span>|  
|<span data-ttu-id="1352e-444">name</span><span class="sxs-lookup"><span data-stu-id="1352e-444">name</span></span>|<span data-ttu-id="1352e-445">Указывает имя набора toobe заголовок hello hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-445">Specifies hello name of hello header toobe set.</span></span>|<span data-ttu-id="1352e-446">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-446">Yes</span></span>|<span data-ttu-id="1352e-447">Недоступно</span><span class="sxs-lookup"><span data-stu-id="1352e-447">N/A</span></span>|  
|<span data-ttu-id="1352e-448">exists-action</span><span class="sxs-lookup"><span data-stu-id="1352e-448">exists-action</span></span>|<span data-ttu-id="1352e-449">Задает tootake какие действия при hello заголовок уже задан.</span><span class="sxs-lookup"><span data-stu-id="1352e-449">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="1352e-450">Этот атрибут должен иметь одно из последующих значений hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-450">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="1352e-451">-Переопределите - значение hello заменяет существующий заголовок hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-451">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="1352e-452">-skip — не заменяет существующее значение заголовка hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-452">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="1352e-453">-Добавить - добавляет значение существующего заголовка hello значение toohello.</span><span class="sxs-lookup"><span data-stu-id="1352e-453">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="1352e-454">-delete — удаляет hello заголовок из запроса hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-454">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="1352e-455">Если задано слишком`override` перечислении нескольких записей с hello одинаковые имена, результаты в заголовке hello, соответствующим tooall записей о наборах (которые будут указаны несколько раз); в результате hello устанавливается только значения из списка.</span><span class="sxs-lookup"><span data-stu-id="1352e-455">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="1352e-456">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-456">No</span></span>|<span data-ttu-id="1352e-457">override</span><span class="sxs-lookup"><span data-stu-id="1352e-457">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1352e-458">Использование</span><span class="sxs-lookup"><span data-stu-id="1352e-458">Usage</span></span>  
 <span data-ttu-id="1352e-459">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1352e-459">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1352e-460">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="1352e-460">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1352e-461">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="1352e-461">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1352e-462"><a name="SendRequest"></a> Отправка запроса</span><span class="sxs-lookup"><span data-stu-id="1352e-462"><a name="SendRequest"></a> Send request</span></span>  
 <span data-ttu-id="1352e-463">Hello `send-request` политики отправляет toohello указан URL-адрес, больше не ожидания не hello задавать значение времени ожидания запроса указано hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-463">hello `send-request` policy sends hello provided request toohello specified URL, waiting no longer than hello set timeout value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1352e-464">Правило политики</span><span class="sxs-lookup"><span data-stu-id="1352e-464">Policy statement</span></span>  
  
```xml  
<send-request mode="new|copy" response-variable-name="" timeout="60 sec" ignore-error  
="false|true">  
  <set-url>...</set-url>  
  <set-method>...</set-method>  
  <set-header name="" exists-action="override|skip|append|delete">...</set-header>  
  <set-body>...</set-body>  
</send-request>  
  
```  
  
### <a name="example"></a><span data-ttu-id="1352e-465">Пример</span><span class="sxs-lookup"><span data-stu-id="1352e-465">Example</span></span>  
 <span data-ttu-id="1352e-466">Этот пример одним из способов tooverify маркер ссылки с сервера авторизации.</span><span class="sxs-lookup"><span data-stu-id="1352e-466">This example shows one way tooverify a reference token with an authorization server.</span></span> <span data-ttu-id="1352e-467">Дополнительные сведения об этом образце см. в разделе [с помощью внешних служб из hello службы управления API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="1352e-467">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
```xml  
<inbound>  
  <!-- Extract Token from Authorization header parameter -->  
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />  
  
  <!-- Send request tooToken Server toovalidate token (see RFC 7662) -->  
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
  
### <a name="elements"></a><span data-ttu-id="1352e-468">Элементы</span><span class="sxs-lookup"><span data-stu-id="1352e-468">Elements</span></span>  
  
|<span data-ttu-id="1352e-469">Элемент</span><span class="sxs-lookup"><span data-stu-id="1352e-469">Element</span></span>|<span data-ttu-id="1352e-470">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-470">Description</span></span>|<span data-ttu-id="1352e-471">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-471">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1352e-472">send-request</span><span class="sxs-lookup"><span data-stu-id="1352e-472">send-request</span></span>|<span data-ttu-id="1352e-473">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="1352e-473">Root element.</span></span>|<span data-ttu-id="1352e-474">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-474">Yes</span></span>|  
|<span data-ttu-id="1352e-475">url</span><span class="sxs-lookup"><span data-stu-id="1352e-475">url</span></span>|<span data-ttu-id="1352e-476">URL-адрес Hello hello запроса.</span><span class="sxs-lookup"><span data-stu-id="1352e-476">hello URL of hello request.</span></span>|<span data-ttu-id="1352e-477">Нет, если mode=copy. В противном случае да.</span><span class="sxs-lookup"><span data-stu-id="1352e-477">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="1352e-478">метод</span><span class="sxs-lookup"><span data-stu-id="1352e-478">method</span></span>|<span data-ttu-id="1352e-479">Здравствуйте, метод HTTP для запроса hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-479">hello HTTP method for hello request.</span></span>|<span data-ttu-id="1352e-480">Нет, если mode=copy. В противном случае да.</span><span class="sxs-lookup"><span data-stu-id="1352e-480">No if mode=copy; otherwise yes.</span></span>|  
|<span data-ttu-id="1352e-481">Верхний колонтитул</span><span class="sxs-lookup"><span data-stu-id="1352e-481">header</span></span>|<span data-ttu-id="1352e-482">Заголовок запроса.</span><span class="sxs-lookup"><span data-stu-id="1352e-482">Request header.</span></span> <span data-ttu-id="1352e-483">Используйте несколько элементов заголовка для нескольких заголовков запросов.</span><span class="sxs-lookup"><span data-stu-id="1352e-483">Use multiple header elements for multiple request headers.</span></span>|<span data-ttu-id="1352e-484">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-484">No</span></span>|  
|<span data-ttu-id="1352e-485">текст</span><span class="sxs-lookup"><span data-stu-id="1352e-485">body</span></span>|<span data-ttu-id="1352e-486">текст запроса Hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-486">hello request body.</span></span>|<span data-ttu-id="1352e-487">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-487">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1352e-488">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="1352e-488">Attributes</span></span>  
  
|<span data-ttu-id="1352e-489">Атрибут</span><span class="sxs-lookup"><span data-stu-id="1352e-489">Attribute</span></span>|<span data-ttu-id="1352e-490">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-490">Description</span></span>|<span data-ttu-id="1352e-491">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-491">Required</span></span>|<span data-ttu-id="1352e-492">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="1352e-492">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1352e-493">mode="строка"</span><span class="sxs-lookup"><span data-stu-id="1352e-493">mode="string"</span></span>|<span data-ttu-id="1352e-494">Определяет, является ли новый запрос или копию hello текущего запроса.</span><span class="sxs-lookup"><span data-stu-id="1352e-494">Determines whether this is a new request or a copy of hello current request.</span></span> <span data-ttu-id="1352e-495">В режиме исходящие режим = копирования не инициализирует hello текст запроса.</span><span class="sxs-lookup"><span data-stu-id="1352e-495">In outbound mode, mode=copy does not initialize hello request body.</span></span>|<span data-ttu-id="1352e-496">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-496">No</span></span>|<span data-ttu-id="1352e-497">Создать</span><span class="sxs-lookup"><span data-stu-id="1352e-497">New</span></span>|  
|<span data-ttu-id="1352e-498">response-variable-name="строка"</span><span class="sxs-lookup"><span data-stu-id="1352e-498">response-variable-name="string"</span></span>|<span data-ttu-id="1352e-499">Если не указано, используется `context.Response`.</span><span class="sxs-lookup"><span data-stu-id="1352e-499">If not present, `context.Response` is used.</span></span>|<span data-ttu-id="1352e-500">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-500">No</span></span>|<span data-ttu-id="1352e-501">Недоступно</span><span class="sxs-lookup"><span data-stu-id="1352e-501">N/A</span></span>|  
|<span data-ttu-id="1352e-502">timeout="целое число"</span><span class="sxs-lookup"><span data-stu-id="1352e-502">timeout="integer"</span></span>|<span data-ttu-id="1352e-503">Hello интервал времени ожидания в секундах перед вызовом hello toohello URL-адрес завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="1352e-503">hello timeout interval in seconds before hello call toohello URL fails.</span></span>|<span data-ttu-id="1352e-504">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-504">No</span></span>|<span data-ttu-id="1352e-505">60</span><span class="sxs-lookup"><span data-stu-id="1352e-505">60</span></span>|  
|<span data-ttu-id="1352e-506">ignore-error</span><span class="sxs-lookup"><span data-stu-id="1352e-506">ignore-error</span></span>|<span data-ttu-id="1352e-507">Если значение true, а hello запрос приведет к ошибке:</span><span class="sxs-lookup"><span data-stu-id="1352e-507">If true and hello request results in an error:</span></span><br /><br /> <span data-ttu-id="1352e-508">если response-variable-name указано, он будет содержать значение null;</span><span class="sxs-lookup"><span data-stu-id="1352e-508">-   If response-variable-name was specified it will contain a null value.</span></span><br /><span data-ttu-id="1352e-509">если response-variable-name не указано, контекст запроса не будет обновлен.</span><span class="sxs-lookup"><span data-stu-id="1352e-509">-   If response-variable-name was not specified, context.Request will not be updated.</span></span>|<span data-ttu-id="1352e-510">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-510">No</span></span>|<span data-ttu-id="1352e-511">нет</span><span class="sxs-lookup"><span data-stu-id="1352e-511">false</span></span>|  
|<span data-ttu-id="1352e-512">name</span><span class="sxs-lookup"><span data-stu-id="1352e-512">name</span></span>|<span data-ttu-id="1352e-513">Указывает имя набора toobe заголовок hello hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-513">Specifies hello name of hello header toobe set.</span></span>|<span data-ttu-id="1352e-514">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-514">Yes</span></span>|<span data-ttu-id="1352e-515">Недоступно</span><span class="sxs-lookup"><span data-stu-id="1352e-515">N/A</span></span>|  
|<span data-ttu-id="1352e-516">exists-action</span><span class="sxs-lookup"><span data-stu-id="1352e-516">exists-action</span></span>|<span data-ttu-id="1352e-517">Задает tootake какие действия при hello заголовок уже задан.</span><span class="sxs-lookup"><span data-stu-id="1352e-517">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="1352e-518">Этот атрибут должен иметь одно из последующих значений hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-518">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="1352e-519">-Переопределите - значение hello заменяет существующий заголовок hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-519">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="1352e-520">-skip — не заменяет существующее значение заголовка hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-520">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="1352e-521">-Добавить - добавляет значение существующего заголовка hello значение toohello.</span><span class="sxs-lookup"><span data-stu-id="1352e-521">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="1352e-522">-delete — удаляет hello заголовок из запроса hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-522">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="1352e-523">Если задано слишком`override` перечислении нескольких записей с hello одинаковые имена, результаты в заголовке hello, соответствующим tooall записей о наборах (которые будут указаны несколько раз); в результате hello устанавливается только значения из списка.</span><span class="sxs-lookup"><span data-stu-id="1352e-523">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="1352e-524">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-524">No</span></span>|<span data-ttu-id="1352e-525">override</span><span class="sxs-lookup"><span data-stu-id="1352e-525">override</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1352e-526">Использование</span><span class="sxs-lookup"><span data-stu-id="1352e-526">Usage</span></span>  
 <span data-ttu-id="1352e-527">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1352e-527">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1352e-528">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="1352e-528">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1352e-529">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="1352e-529">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1352e-530"><a name="SetHttpProxy"></a> Установка прокси-сервера HTTP</span><span class="sxs-lookup"><span data-stu-id="1352e-530"><a name="SetHttpProxy"></a> Set HTTP proxy</span></span>  
 <span data-ttu-id="1352e-531">Hello `proxy` политика позволяет tooroute toobackends пересылки запросов через прокси-сервер HTTP.</span><span class="sxs-lookup"><span data-stu-id="1352e-531">hello `proxy` policy allows you tooroute requests forwarded toobackends via an HTTP proxy.</span></span> <span data-ttu-id="1352e-532">Между шлюзом hello и прокси-сервера hello поддерживается только HTTP (не HTTPS).</span><span class="sxs-lookup"><span data-stu-id="1352e-532">Only HTTP (not HTTPS) is supported between hello gateway and hello proxy.</span></span> <span data-ttu-id="1352e-533">Используются только базовая проверка подлинности и проверка подлинности NTLM.</span><span class="sxs-lookup"><span data-stu-id="1352e-533">Basic and NTLM authentication only.</span></span>
  
### <a name="policy-statement"></a><span data-ttu-id="1352e-534">Правило политики</span><span class="sxs-lookup"><span data-stu-id="1352e-534">Policy statement</span></span>  
  
```xml  
<proxy url="http://hostname-or-ip:port" username="username" password="password" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="1352e-535">Пример</span><span class="sxs-lookup"><span data-stu-id="1352e-535">Example</span></span>  
<span data-ttu-id="1352e-536">Обратите внимание на использование hello [свойства](api-management-howto-properties.md) как значения hello имя пользователя и пароль tooavoid, хранение конфиденциальных сведений в документе политики hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-536">Note hello use of [properties](api-management-howto-properties.md) as values of hello username and password tooavoid storing sensitive information in hello policy document.</span></span>  
  
```xml  
<proxy url="http://192.168.1.1:8080" username={{username}} password={{password}} />
  
```  
  
### <a name="elements"></a><span data-ttu-id="1352e-537">Элементы</span><span class="sxs-lookup"><span data-stu-id="1352e-537">Elements</span></span>  
  
|<span data-ttu-id="1352e-538">Элемент</span><span class="sxs-lookup"><span data-stu-id="1352e-538">Element</span></span>|<span data-ttu-id="1352e-539">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-539">Description</span></span>|<span data-ttu-id="1352e-540">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-540">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1352e-541">proxy</span><span class="sxs-lookup"><span data-stu-id="1352e-541">proxy</span></span>|<span data-ttu-id="1352e-542">Корневой элемент</span><span class="sxs-lookup"><span data-stu-id="1352e-542">Root element</span></span>|<span data-ttu-id="1352e-543">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-543">Yes</span></span>|  

### <a name="attributes"></a><span data-ttu-id="1352e-544">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="1352e-544">Attributes</span></span>  
  
|<span data-ttu-id="1352e-545">Атрибут</span><span class="sxs-lookup"><span data-stu-id="1352e-545">Attribute</span></span>|<span data-ttu-id="1352e-546">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-546">Description</span></span>|<span data-ttu-id="1352e-547">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-547">Required</span></span>|<span data-ttu-id="1352e-548">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="1352e-548">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1352e-549">url="string"</span><span class="sxs-lookup"><span data-stu-id="1352e-549">url="string"</span></span>|<span data-ttu-id="1352e-550">URL-адрес прокси-сервера в виде hello. http://Host: Port.</span><span class="sxs-lookup"><span data-stu-id="1352e-550">Proxy URL in hello form of http://host:port.</span></span>|<span data-ttu-id="1352e-551">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-551">Yes</span></span>|<span data-ttu-id="1352e-552">Недоступно</span><span class="sxs-lookup"><span data-stu-id="1352e-552">N/A</span></span>|  
|<span data-ttu-id="1352e-553">username="string"</span><span class="sxs-lookup"><span data-stu-id="1352e-553">username="string"</span></span>|<span data-ttu-id="1352e-554">Toobe имя пользователя, используемый для проверки подлинности с прокси-сервером hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-554">Username toobe used for authentication with hello proxy.</span></span>|<span data-ttu-id="1352e-555">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-555">No</span></span>|<span data-ttu-id="1352e-556">Недоступно</span><span class="sxs-lookup"><span data-stu-id="1352e-556">N/A</span></span>|  
|<span data-ttu-id="1352e-557">password="string"</span><span class="sxs-lookup"><span data-stu-id="1352e-557">password="string"</span></span>|<span data-ttu-id="1352e-558">Toobe пароль, используемый для проверки подлинности с прокси-сервером hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-558">Password toobe used for authentication with hello proxy.</span></span>|<span data-ttu-id="1352e-559">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-559">No</span></span>|<span data-ttu-id="1352e-560">Недоступно</span><span class="sxs-lookup"><span data-stu-id="1352e-560">N/A</span></span>|  

### <a name="usage"></a><span data-ttu-id="1352e-561">Использование</span><span class="sxs-lookup"><span data-stu-id="1352e-561">Usage</span></span>  
 <span data-ttu-id="1352e-562">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1352e-562">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1352e-563">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="1352e-563">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="1352e-564">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="1352e-564">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="1352e-565"><a name="SetRequestMethod"></a> Задание метода запроса</span><span class="sxs-lookup"><span data-stu-id="1352e-565"><a name="SetRequestMethod"></a> Set request method</span></span>  
 <span data-ttu-id="1352e-566">Hello `set-method` политика позволяет toochange метод запроса hello HTTP для запроса.</span><span class="sxs-lookup"><span data-stu-id="1352e-566">hello `set-method` policy allows you toochange hello HTTP request method for a request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1352e-567">Правило политики</span><span class="sxs-lookup"><span data-stu-id="1352e-567">Policy statement</span></span>  
  
```xml  
<set-method>METHOD</set-method>  
  
```  
  
### <a name="example"></a><span data-ttu-id="1352e-568">Пример</span><span class="sxs-lookup"><span data-stu-id="1352e-568">Example</span></span>  
 <span data-ttu-id="1352e-569">Пример политики, которая использует hello `set-method` политики показан пример отправки сообщения tooa резерв чата, если hello код ответа HTTP больше или равно too500.</span><span class="sxs-lookup"><span data-stu-id="1352e-569">This sample policy that uses hello `set-method` policy shows an example of sending a message tooa Slack chat room if hello HTTP response code is greater than or equal too500.</span></span> <span data-ttu-id="1352e-570">Дополнительные сведения об этом образце см. в разделе [с помощью внешних служб из hello службы управления API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span><span class="sxs-lookup"><span data-stu-id="1352e-570">For more information on this sample, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/).</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="1352e-571">Элементы</span><span class="sxs-lookup"><span data-stu-id="1352e-571">Elements</span></span>  
  
|<span data-ttu-id="1352e-572">Элемент</span><span class="sxs-lookup"><span data-stu-id="1352e-572">Element</span></span>|<span data-ttu-id="1352e-573">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-573">Description</span></span>|<span data-ttu-id="1352e-574">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-574">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1352e-575">set-method</span><span class="sxs-lookup"><span data-stu-id="1352e-575">set-method</span></span>|<span data-ttu-id="1352e-576">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="1352e-576">Root element.</span></span> <span data-ttu-id="1352e-577">значение Hello элемента hello задает метод HTTP hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-577">hello value of hello element specifies hello HTTP method.</span></span>|<span data-ttu-id="1352e-578">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-578">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1352e-579">Использование</span><span class="sxs-lookup"><span data-stu-id="1352e-579">Usage</span></span>  
 <span data-ttu-id="1352e-580">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1352e-580">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1352e-581">**Разделы политики:** inbound, on-error.</span><span class="sxs-lookup"><span data-stu-id="1352e-581">**Policy sections:** inbound, on-error</span></span>  
  
-   <span data-ttu-id="1352e-582">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="1352e-582">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1352e-583"><a name="SetStatus"></a> Задание кода состояния</span><span class="sxs-lookup"><span data-stu-id="1352e-583"><a name="SetStatus"></a> Set status code</span></span>  
 <span data-ttu-id="1352e-584">Hello `set-status` политики наборов hello HTTP состояние кода toohello заданное значение.</span><span class="sxs-lookup"><span data-stu-id="1352e-584">hello `set-status` policy sets hello HTTP status code toohello specified value.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1352e-585">Правило политики</span><span class="sxs-lookup"><span data-stu-id="1352e-585">Policy statement</span></span>  
  
```xml  
<set-status code="" reason=""/>  
  
```  
  
### <a name="example"></a><span data-ttu-id="1352e-586">Пример</span><span class="sxs-lookup"><span data-stu-id="1352e-586">Example</span></span>  
 <span data-ttu-id="1352e-587">В этом примере показано, как tooreturn ответ 401, если маркер авторизации hello является недопустимым.</span><span class="sxs-lookup"><span data-stu-id="1352e-587">This example shows how tooreturn a 401 response if hello authorization token is invalid.</span></span> <span data-ttu-id="1352e-588">Дополнительные сведения см. в разделе [с помощью внешних служб из hello службы управления API Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span><span class="sxs-lookup"><span data-stu-id="1352e-588">For more information, see [Using external services from hello Azure API Management service](https://azure.microsoft.com/documentation/articles/api-management-sample-send-request/)</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="1352e-589">Элементы</span><span class="sxs-lookup"><span data-stu-id="1352e-589">Elements</span></span>  
  
|<span data-ttu-id="1352e-590">Элемент</span><span class="sxs-lookup"><span data-stu-id="1352e-590">Element</span></span>|<span data-ttu-id="1352e-591">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-591">Description</span></span>|<span data-ttu-id="1352e-592">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-592">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1352e-593">set-status</span><span class="sxs-lookup"><span data-stu-id="1352e-593">set-status</span></span>|<span data-ttu-id="1352e-594">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="1352e-594">Root element.</span></span>|<span data-ttu-id="1352e-595">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-595">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1352e-596">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="1352e-596">Attributes</span></span>  
  
|<span data-ttu-id="1352e-597">Атрибут</span><span class="sxs-lookup"><span data-stu-id="1352e-597">Attribute</span></span>|<span data-ttu-id="1352e-598">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-598">Description</span></span>|<span data-ttu-id="1352e-599">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-599">Required</span></span>|<span data-ttu-id="1352e-600">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="1352e-600">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1352e-601">code="целое число"</span><span class="sxs-lookup"><span data-stu-id="1352e-601">code="integer"</span></span>|<span data-ttu-id="1352e-602">tooreturn код состояния Hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="1352e-602">hello HTTP status code tooreturn.</span></span>|<span data-ttu-id="1352e-603">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-603">Yes</span></span>|<span data-ttu-id="1352e-604">Недоступно</span><span class="sxs-lookup"><span data-stu-id="1352e-604">N/A</span></span>|  
|<span data-ttu-id="1352e-605">reason="строка"</span><span class="sxs-lookup"><span data-stu-id="1352e-605">reason="string"</span></span>|<span data-ttu-id="1352e-606">Описание hello причину для возврата hello код состояния.</span><span class="sxs-lookup"><span data-stu-id="1352e-606">A description of hello reason for returning hello status code.</span></span>|<span data-ttu-id="1352e-607">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-607">Yes</span></span>|<span data-ttu-id="1352e-608">Недоступно</span><span class="sxs-lookup"><span data-stu-id="1352e-608">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1352e-609">Использование</span><span class="sxs-lookup"><span data-stu-id="1352e-609">Usage</span></span>  
 <span data-ttu-id="1352e-610">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1352e-610">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1352e-611">**Разделы политики:** outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="1352e-611">**Policy sections:** outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1352e-612">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="1352e-612">**Policy scopes:** all scopes</span></span>  

##  <span data-ttu-id="1352e-613"><a name="set-variable"></a> Задание переменной</span><span class="sxs-lookup"><span data-stu-id="1352e-613"><a name="set-variable"></a> Set variable</span></span>  
 <span data-ttu-id="1352e-614">Hello `set-variable` объявляет политики [контекста](api-management-policy-expressions.md#ContextVariables) переменной и присвоение ей значения, указанного с помощью [выражение](api-management-policy-expressions.md) или строковым литералом.</span><span class="sxs-lookup"><span data-stu-id="1352e-614">hello `set-variable` policy declares a [context](api-management-policy-expressions.md#ContextVariables) variable and assigns it a value specified via an [expression](api-management-policy-expressions.md) or a string literal.</span></span> <span data-ttu-id="1352e-615">Если hello выражение содержит литерал, он будет преобразован тип string и hello tooa hello значения будет `System.String`.</span><span class="sxs-lookup"><span data-stu-id="1352e-615">if hello expression contains a literal it will be converted tooa string and hello type of hello value will be `System.String`.</span></span>  
  
###  <span data-ttu-id="1352e-616"><a name="set-variablePolicyStatement"></a> Правило политики</span><span class="sxs-lookup"><span data-stu-id="1352e-616"><a name="set-variablePolicyStatement"></a> Policy statement</span></span>  
  
```xml  
<set-variable name="variable name" value="Expression | String literal" />  
```  
  
###  <span data-ttu-id="1352e-617"><a name="set-variableExample"></a> Пример</span><span class="sxs-lookup"><span data-stu-id="1352e-617"><a name="set-variableExample"></a> Example</span></span>  
 <span data-ttu-id="1352e-618">Hello ниже приведен пример политика задания переменной в hello входящих раздела.</span><span class="sxs-lookup"><span data-stu-id="1352e-618">hello following example demonstrates a set variable policy in hello inbound section.</span></span> <span data-ttu-id="1352e-619">Эта политика задания переменной создает `isMobile` логическое [контекста](api-management-policy-expressions.md#ContextVariables) переменной, которая имеет значение tootrue, если hello `User-Agent` заголовок запроса содержит текст hello `iPad` или `iPhone`.</span><span class="sxs-lookup"><span data-stu-id="1352e-619">This set variable policy creates an `isMobile` Boolean [context](api-management-policy-expressions.md#ContextVariables) variable that is set tootrue if hello `User-Agent` request header contains hello text `iPad` or `iPhone`.</span></span>  
  
```xml  
<set-variable name="IsMobile" value="@(context.Request.Headers["User-Agent"].Contains("iPad") || context.Request.Headers["User-Agent"].Contains("iPhone"))" />  
```  
  
### <a name="elements"></a><span data-ttu-id="1352e-620">Элементы</span><span class="sxs-lookup"><span data-stu-id="1352e-620">Elements</span></span>  
  
|<span data-ttu-id="1352e-621">Элемент</span><span class="sxs-lookup"><span data-stu-id="1352e-621">Element</span></span>|<span data-ttu-id="1352e-622">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-622">Description</span></span>|<span data-ttu-id="1352e-623">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-623">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1352e-624">set-variable</span><span class="sxs-lookup"><span data-stu-id="1352e-624">set-variable</span></span>|<span data-ttu-id="1352e-625">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="1352e-625">Root element.</span></span>|<span data-ttu-id="1352e-626">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-626">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1352e-627">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="1352e-627">Attributes</span></span>  
  
|<span data-ttu-id="1352e-628">Атрибут</span><span class="sxs-lookup"><span data-stu-id="1352e-628">Attribute</span></span>|<span data-ttu-id="1352e-629">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-629">Description</span></span>|<span data-ttu-id="1352e-630">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-630">Required</span></span>|  
|---------------|-----------------|--------------|  
|<span data-ttu-id="1352e-631">name</span><span class="sxs-lookup"><span data-stu-id="1352e-631">name</span></span>|<span data-ttu-id="1352e-632">Имя переменной hello Hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-632">hello name of hello variable.</span></span>|<span data-ttu-id="1352e-633">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-633">Yes</span></span>|  
|<span data-ttu-id="1352e-634">value</span><span class="sxs-lookup"><span data-stu-id="1352e-634">value</span></span>|<span data-ttu-id="1352e-635">значение переменной hello Hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-635">hello value of hello variable.</span></span> <span data-ttu-id="1352e-636">Это может быть выражение или литеральное значение.</span><span class="sxs-lookup"><span data-stu-id="1352e-636">This can be an expression or a literal value.</span></span>|<span data-ttu-id="1352e-637">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-637">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1352e-638">Использование</span><span class="sxs-lookup"><span data-stu-id="1352e-638">Usage</span></span>  
 <span data-ttu-id="1352e-639">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1352e-639">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1352e-640">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="1352e-640">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1352e-641">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="1352e-641">**Policy scopes:** all scopes</span></span>  
  
###  <span data-ttu-id="1352e-642"><a name="set-variableAllowedTypes"></a> Допустимые типы</span><span class="sxs-lookup"><span data-stu-id="1352e-642"><a name="set-variableAllowedTypes"></a> Allowed types</span></span>  
 <span data-ttu-id="1352e-643">Выражения, используемые в hello `set-variable` политики должен возвращать hello следующие базовые типы.</span><span class="sxs-lookup"><span data-stu-id="1352e-643">Expressions used in hello `set-variable` policy must return one of hello following basic types.</span></span>  
  
-   <span data-ttu-id="1352e-644">System.Boolean</span><span class="sxs-lookup"><span data-stu-id="1352e-644">System.Boolean</span></span>  
  
-   <span data-ttu-id="1352e-645">System.SByte</span><span class="sxs-lookup"><span data-stu-id="1352e-645">System.SByte</span></span>  
  
-   <span data-ttu-id="1352e-646">System.Byte</span><span class="sxs-lookup"><span data-stu-id="1352e-646">System.Byte</span></span>  
  
-   <span data-ttu-id="1352e-647">System.UInt16</span><span class="sxs-lookup"><span data-stu-id="1352e-647">System.UInt16</span></span>  
  
-   <span data-ttu-id="1352e-648">System.UInt32</span><span class="sxs-lookup"><span data-stu-id="1352e-648">System.UInt32</span></span>  
  
-   <span data-ttu-id="1352e-649">System.UInt64</span><span class="sxs-lookup"><span data-stu-id="1352e-649">System.UInt64</span></span>  
  
-   <span data-ttu-id="1352e-650">System.Int16</span><span class="sxs-lookup"><span data-stu-id="1352e-650">System.Int16</span></span>  
  
-   <span data-ttu-id="1352e-651">System.Int32</span><span class="sxs-lookup"><span data-stu-id="1352e-651">System.Int32</span></span>  
  
-   <span data-ttu-id="1352e-652">System.Int64</span><span class="sxs-lookup"><span data-stu-id="1352e-652">System.Int64</span></span>  
  
-   <span data-ttu-id="1352e-653">System.Decimal</span><span class="sxs-lookup"><span data-stu-id="1352e-653">System.Decimal</span></span>  
  
-   <span data-ttu-id="1352e-654">System.Single</span><span class="sxs-lookup"><span data-stu-id="1352e-654">System.Single</span></span>  
  
-   <span data-ttu-id="1352e-655">System.Double</span><span class="sxs-lookup"><span data-stu-id="1352e-655">System.Double</span></span>  
  
-   <span data-ttu-id="1352e-656">System.Guid</span><span class="sxs-lookup"><span data-stu-id="1352e-656">System.Guid</span></span>  
  
-   <span data-ttu-id="1352e-657">System.String</span><span class="sxs-lookup"><span data-stu-id="1352e-657">System.String</span></span>  
  
-   <span data-ttu-id="1352e-658">System.Char</span><span class="sxs-lookup"><span data-stu-id="1352e-658">System.Char</span></span>  
  
-   <span data-ttu-id="1352e-659">System.DateTime</span><span class="sxs-lookup"><span data-stu-id="1352e-659">System.DateTime</span></span>  
  
-   <span data-ttu-id="1352e-660">System.TimeSpan</span><span class="sxs-lookup"><span data-stu-id="1352e-660">System.TimeSpan</span></span>  
  
-   <span data-ttu-id="1352e-661">System.Byte?</span><span class="sxs-lookup"><span data-stu-id="1352e-661">System.Byte?</span></span>  
  
-   <span data-ttu-id="1352e-662">System.UInt16?</span><span class="sxs-lookup"><span data-stu-id="1352e-662">System.UInt16?</span></span>  
  
-   <span data-ttu-id="1352e-663">System.UInt32?</span><span class="sxs-lookup"><span data-stu-id="1352e-663">System.UInt32?</span></span>  
  
-   <span data-ttu-id="1352e-664">System.UInt64?</span><span class="sxs-lookup"><span data-stu-id="1352e-664">System.UInt64?</span></span>  
  
-   <span data-ttu-id="1352e-665">System.Int16?</span><span class="sxs-lookup"><span data-stu-id="1352e-665">System.Int16?</span></span>  
  
-   <span data-ttu-id="1352e-666">System.Int32?</span><span class="sxs-lookup"><span data-stu-id="1352e-666">System.Int32?</span></span>  
  
-   <span data-ttu-id="1352e-667">System.Int64?</span><span class="sxs-lookup"><span data-stu-id="1352e-667">System.Int64?</span></span>  
  
-   <span data-ttu-id="1352e-668">System.Decimal?</span><span class="sxs-lookup"><span data-stu-id="1352e-668">System.Decimal?</span></span>  
  
-   <span data-ttu-id="1352e-669">System.Single?</span><span class="sxs-lookup"><span data-stu-id="1352e-669">System.Single?</span></span>  
  
-   <span data-ttu-id="1352e-670">System.Double?</span><span class="sxs-lookup"><span data-stu-id="1352e-670">System.Double?</span></span>  
  
-   <span data-ttu-id="1352e-671">System.Guid?</span><span class="sxs-lookup"><span data-stu-id="1352e-671">System.Guid?</span></span>  
  
-   <span data-ttu-id="1352e-672">System.String?</span><span class="sxs-lookup"><span data-stu-id="1352e-672">System.String?</span></span>  
  
-   <span data-ttu-id="1352e-673">System.Char?</span><span class="sxs-lookup"><span data-stu-id="1352e-673">System.Char?</span></span>  
  
-   <span data-ttu-id="1352e-674">System.DateTime?</span><span class="sxs-lookup"><span data-stu-id="1352e-674">System.DateTime?</span></span>  

##  <span data-ttu-id="1352e-675"><a name="Trace"></a> Трассировка</span><span class="sxs-lookup"><span data-stu-id="1352e-675"><a name="Trace"></a> Trace</span></span>  
 <span data-ttu-id="1352e-676">Hello `trace` политики добавляет строку в hello [инспектора API](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) выходных данных.</span><span class="sxs-lookup"><span data-stu-id="1352e-676">hello             `trace` policy adds a string into hello [API Inspector](https://azure.microsoft.com/en-us/documentation/articles/api-management-howto-api-inspector/) output.</span></span> <span data-ttu-id="1352e-677">Hello политики будет выполняться только если трассировка инициируется, т. е. `Ocp-Apim-Trace` заголовок запроса представить и задать слишком`true` и `Ocp-Apim-Subscription-Key` заголовок запроса присутствует и имеет допустимый ключ, связанный с учетной записью администратора hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-677">hello policy will execute only when tracing is triggered, i.e. `Ocp-Apim-Trace` request header is present and set too`true` and `Ocp-Apim-Subscription-Key` request header is present and holds a valid key associated with hello admin account.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1352e-678">Правило политики</span><span class="sxs-lookup"><span data-stu-id="1352e-678">Policy statement</span></span>  
  
```xml  
  
<trace source="arbitrary string literal"/>  
    <!-- string expression or literal -->  
</trace>  
  
```  
  
### <a name="elements"></a><span data-ttu-id="1352e-679">Элементы</span><span class="sxs-lookup"><span data-stu-id="1352e-679">Elements</span></span>  
  
|<span data-ttu-id="1352e-680">Элемент</span><span class="sxs-lookup"><span data-stu-id="1352e-680">Element</span></span>|<span data-ttu-id="1352e-681">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-681">Description</span></span>|<span data-ttu-id="1352e-682">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-682">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1352e-683">trace</span><span class="sxs-lookup"><span data-stu-id="1352e-683">trace</span></span>|<span data-ttu-id="1352e-684">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="1352e-684">Root element.</span></span>|<span data-ttu-id="1352e-685">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-685">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1352e-686">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="1352e-686">Attributes</span></span>  
  
|<span data-ttu-id="1352e-687">Атрибут</span><span class="sxs-lookup"><span data-stu-id="1352e-687">Attribute</span></span>|<span data-ttu-id="1352e-688">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-688">Description</span></span>|<span data-ttu-id="1352e-689">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-689">Required</span></span>|<span data-ttu-id="1352e-690">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="1352e-690">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1352e-691">источник</span><span class="sxs-lookup"><span data-stu-id="1352e-691">source</span></span>|<span data-ttu-id="1352e-692">Строка литерала может применяться toohello trace viewer и указав источник приветственное сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-692">String literal meaningful toohello trace viewer and specifying hello source of hello message.</span></span>|<span data-ttu-id="1352e-693">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-693">Yes</span></span>|<span data-ttu-id="1352e-694">Недоступно</span><span class="sxs-lookup"><span data-stu-id="1352e-694">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1352e-695">Использование</span><span class="sxs-lookup"><span data-stu-id="1352e-695">Usage</span></span>  
 <span data-ttu-id="1352e-696">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="1352e-696">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="1352e-697">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="1352e-697">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="1352e-698">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="1352e-698">**Policy scopes:** all scopes</span></span>  
  
##  <span data-ttu-id="1352e-699"><a name="Wait"></a> Ожидание</span><span class="sxs-lookup"><span data-stu-id="1352e-699"><a name="Wait"></a> Wait</span></span>  
 <span data-ttu-id="1352e-700">Hello `wait` политики выполняет его непосредственных дочерних политик в параллельном режиме и ожидает либо все, либо один из его непосредственных дочерних политик toocomplete, до ее завершения.</span><span class="sxs-lookup"><span data-stu-id="1352e-700">hello `wait` policy executes its immediate child policies in parallel, and waits for either all or one of its immediate child policies toocomplete before it completes.</span></span> <span data-ttu-id="1352e-701">Hello политики ожидания могут иметь в качестве его непосредственных дочерних политик [запрос на отправку](api-management-advanced-policies.md#SendRequest), [получить значение из кэша](api-management-caching-policies.md#GetFromCacheByKey), и [поток управления](api-management-advanced-policies.md#choose) политики.</span><span class="sxs-lookup"><span data-stu-id="1352e-701">hello wait policy can have as its immediate child policies [Send request](api-management-advanced-policies.md#SendRequest), [Get value from cache](api-management-caching-policies.md#GetFromCacheByKey), and [Control flow](api-management-advanced-policies.md#choose) policies.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="1352e-702">Правило политики</span><span class="sxs-lookup"><span data-stu-id="1352e-702">Policy statement</span></span>  
  
```xml  
<wait for="all|any">  
  <!--Wait policy can contain send-request, cache-lookup-value,   
        and choose policies as child elements -->  
</wait>  
  
```  
  
### <a name="example"></a><span data-ttu-id="1352e-703">Пример</span><span class="sxs-lookup"><span data-stu-id="1352e-703">Example</span></span>  
 <span data-ttu-id="1352e-704">В следующий пример hello есть два `choose` политик в качестве непосредственных дочерних политики hello `wait` политики.</span><span class="sxs-lookup"><span data-stu-id="1352e-704">In hello following example there are two `choose` policies as immediate child policies of hello `wait` policy.</span></span> <span data-ttu-id="1352e-705">Каждая из этих политик `choose` выполняется в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="1352e-705">Each of these `choose` policies executes in parallel.</span></span> <span data-ttu-id="1352e-706">Каждый `choose` политики пытается tooretrieve кэшированное значение.</span><span class="sxs-lookup"><span data-stu-id="1352e-706">Each `choose` policy attempts tooretrieve a cached value.</span></span> <span data-ttu-id="1352e-707">В случае пропуска кэша серверная служба называется значением tooprovide hello.</span><span class="sxs-lookup"><span data-stu-id="1352e-707">If there is a cache miss, a backend service is called tooprovide hello value.</span></span> <span data-ttu-id="1352e-708">В этом примере hello `wait` политики для завершения всех ее непосредственных дочерних политик завершить, так как hello `for` атрибута задано слишком`all`.</span><span class="sxs-lookup"><span data-stu-id="1352e-708">In this example hello `wait` policy does not complete until all of its immediate child policies complete, because hello `for` attribute is set too`all`.</span></span>   <span data-ttu-id="1352e-709">В этот примере hello контекста переменных (`execute-branch-one`, `value-one`, `execute-branch-two`, и `value-two`) объявлены вне области hello этот пример политики.</span><span class="sxs-lookup"><span data-stu-id="1352e-709">In this example hello context variables (`execute-branch-one`, `value-one`, `execute-branch-two`, and `value-two`) are declared outside of hello scope of this example policy.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="1352e-710">Элементы</span><span class="sxs-lookup"><span data-stu-id="1352e-710">Elements</span></span>  
  
|<span data-ttu-id="1352e-711">Элемент</span><span class="sxs-lookup"><span data-stu-id="1352e-711">Element</span></span>|<span data-ttu-id="1352e-712">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-712">Description</span></span>|<span data-ttu-id="1352e-713">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-713">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="1352e-714">wait</span><span class="sxs-lookup"><span data-stu-id="1352e-714">wait</span></span>|<span data-ttu-id="1352e-715">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="1352e-715">Root element.</span></span> <span data-ttu-id="1352e-716">Может содержать в качестве дочерних элементов только политики `send-request`, `cache-lookup-value` и `choose`.</span><span class="sxs-lookup"><span data-stu-id="1352e-716">May contain as child elements only `send-request`, `cache-lookup-value`, and `choose` policies.</span></span>|<span data-ttu-id="1352e-717">Да</span><span class="sxs-lookup"><span data-stu-id="1352e-717">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="1352e-718">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="1352e-718">Attributes</span></span>  
  
|<span data-ttu-id="1352e-719">Атрибут</span><span class="sxs-lookup"><span data-stu-id="1352e-719">Attribute</span></span>|<span data-ttu-id="1352e-720">Описание</span><span class="sxs-lookup"><span data-stu-id="1352e-720">Description</span></span>|<span data-ttu-id="1352e-721">Обязательно</span><span class="sxs-lookup"><span data-stu-id="1352e-721">Required</span></span>|<span data-ttu-id="1352e-722">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="1352e-722">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="1352e-723">for</span><span class="sxs-lookup"><span data-stu-id="1352e-723">for</span></span>|<span data-ttu-id="1352e-724">Определяет, является ли hello `wait` политики ожидает все toobe политики непосредственных дочерних завершена или только один.</span><span class="sxs-lookup"><span data-stu-id="1352e-724">Determines whether hello `wait` policy waits for all immediate child policies toobe completed or just one.</span></span> <span data-ttu-id="1352e-725">Допустимые значения:</span><span class="sxs-lookup"><span data-stu-id="1352e-725">Allowed values are:</span></span><br /><br /> <span data-ttu-id="1352e-726">-   `all`-ожидания для всех toocomplete непосредственных дочерних политик</span><span class="sxs-lookup"><span data-stu-id="1352e-726">-   `all` - wait for all immediate child policies toocomplete</span></span><br /><span data-ttu-id="1352e-727">-любое - ожидания любой toocomplete политики непосредственных дочерних.</span><span class="sxs-lookup"><span data-stu-id="1352e-727">-   any - wait for any immediate child policy toocomplete.</span></span> <span data-ttu-id="1352e-728">После завершения первой политики непосредственных дочерних hello hello `wait` политики завершается, и любые другие политики непосредственных дочерних выполнение завершается.</span><span class="sxs-lookup"><span data-stu-id="1352e-728">Once hello first immediate child policy has completed, hello `wait` policy completes and execution of any other immediate child policies is terminated.</span></span>|<span data-ttu-id="1352e-729">Нет</span><span class="sxs-lookup"><span data-stu-id="1352e-729">No</span></span>|<span data-ttu-id="1352e-730">все</span><span class="sxs-lookup"><span data-stu-id="1352e-730">all</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="1352e-731">Использование</span><span class="sxs-lookup"><span data-stu-id="1352e-731">Usage</span></span>  
 <span data-ttu-id="1352e-732">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="1352e-732">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="1352e-733">**Разделы политики:** inbound, outbound, backend.</span><span class="sxs-lookup"><span data-stu-id="1352e-733">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="1352e-734">**Области политики:** все области.</span><span class="sxs-lookup"><span data-stu-id="1352e-734">**Policy scopes:**all scopes</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="1352e-735">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1352e-735">Next steps</span></span>
<span data-ttu-id="1352e-736">Дополнительные сведения о работе с политиками см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="1352e-736">For more information working with policies, see:</span></span>
-   [<span data-ttu-id="1352e-737">Политики в управлении API</span><span class="sxs-lookup"><span data-stu-id="1352e-737">Policies in API Management</span></span>](api-management-howto-policies.md) 
-   [<span data-ttu-id="1352e-738">Выражения политики</span><span class="sxs-lookup"><span data-stu-id="1352e-738">Policy expressions</span></span>](api-management-policy-expressions.md)
