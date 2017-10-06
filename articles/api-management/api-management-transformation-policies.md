---
title: "политики преобразования при управлении API aaaAzure | Документы Microsoft"
description: "Дополнительные сведения о политиках hello преобразования, доступные для использования в службе управления API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7406a8ce-5f9c-4fae-9b0f-e574befb2ee9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2891cc52d0017b717b3c12a98bc4941b5fd7ea78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-transformation-policies"></a><span data-ttu-id="c58da-103">Политики преобразования службы управления API</span><span class="sxs-lookup"><span data-stu-id="c58da-103">API Management transformation policies</span></span>
<span data-ttu-id="c58da-104">Здесь вы найдете ссылку для hello следующих политиках управления интерфейсами API.</span><span class="sxs-lookup"><span data-stu-id="c58da-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="c58da-105">Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в управлении API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="c58da-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="c58da-106"><a name="TransformationPolicies"></a> Политики преобразования</span><span class="sxs-lookup"><span data-stu-id="c58da-106"><a name="TransformationPolicies"></a> Transformation policies</span></span>  
  
-   <span data-ttu-id="c58da-107">[Преобразование JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - преобразует запрос или текст ответа от JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="c58da-107">[Convert JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON tooXML.</span></span>  
  
-   <span data-ttu-id="c58da-108">[Преобразование XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - преобразует запрос, или из XML tooJSON текст ответа.</span><span class="sxs-lookup"><span data-stu-id="c58da-108">[Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML tooJSON.</span></span>  
  
-   <span data-ttu-id="c58da-109">[Поиск и замена строки в тексте](api-management-transformation-policies.md#Findandreplacestringinbody) – отыскивает подстроку запроса или ответа и заменяет ее на другую подстроку.</span><span class="sxs-lookup"><span data-stu-id="c58da-109">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
-   <span data-ttu-id="c58da-110">[Маскировать URL-адреса в содержимом](api-management-transformation-policies.md#MaskURLSContent) -загрузочную запись (маскировка) ссылок в ответ hello текста, чтобы они указывали toohello равнозначными ссылками через шлюз hello.</span><span class="sxs-lookup"><span data-stu-id="c58da-110">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>  
  
-   <span data-ttu-id="c58da-111">[Задать серверной службе](api-management-transformation-policies.md#SetBackendService) -изменяет hello серверную службу для входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="c58da-111">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes hello backend service for an incoming request.</span></span>  
  
-   <span data-ttu-id="c58da-112">[Задайте текст](api-management-transformation-policies.md#SetBody) -задает текст сообщения hello для входящих и исходящих запросов.</span><span class="sxs-lookup"><span data-stu-id="c58da-112">[Set body](api-management-transformation-policies.md#SetBody) - Sets hello message body for incoming and outgoing requests.</span></span>  
  
-   <span data-ttu-id="c58da-113">[Задание заголовка HTTP](api-management-transformation-policies.md#SetHTTPheader) - назначает значение tooan существующего ответа и/или заголовка запроса или Добавление нового заголовка ответа и/или запроса.</span><span class="sxs-lookup"><span data-stu-id="c58da-113">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
-   <span data-ttu-id="c58da-114">[Настройка параметра строки запроса](api-management-transformation-policies.md#SetQueryStringParameter) - добавляет, заменяет значение или удаляет параметр строки запроса.</span><span class="sxs-lookup"><span data-stu-id="c58da-114">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
-   <span data-ttu-id="c58da-115">[Замена URL-адреса](api-management-transformation-policies.md#RewriteURL) -преобразование URL-АДРЕСЕ запроса из общеупотребительной формы формы toohello ожидаемый hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="c58da-115">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form toohello form expected by hello web service.</span></span>  
  
-   <span data-ttu-id="c58da-116">[Преобразования XML с помощью XSLT](api-management-transformation-policies.md#XSLTransform) -применяется tooXML преобразование XSL в тексте запроса или ответа hello.</span><span class="sxs-lookup"><span data-stu-id="c58da-116">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
##  <span data-ttu-id="c58da-117"><a name="ConvertJSONtoXML"></a>Преобразовать JSON tooXML</span><span class="sxs-lookup"><span data-stu-id="c58da-117"><a name="ConvertJSONtoXML"></a> Convert JSON tooXML</span></span>  
 <span data-ttu-id="c58da-118">Hello `json-to-xml` политики преобразует тело запроса или ответа из JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="c58da-118">hello `json-to-xml` policy converts a request or response body from JSON tooXML.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c58da-119">Правило политики</span><span class="sxs-lookup"><span data-stu-id="c58da-119">Policy statement</span></span>  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="c58da-120">Пример</span><span class="sxs-lookup"><span data-stu-id="c58da-120">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <json-to-xml apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="c58da-121">Элементы</span><span class="sxs-lookup"><span data-stu-id="c58da-121">Elements</span></span>  
  
|<span data-ttu-id="c58da-122">Имя</span><span class="sxs-lookup"><span data-stu-id="c58da-122">Name</span></span>|<span data-ttu-id="c58da-123">Описание</span><span class="sxs-lookup"><span data-stu-id="c58da-123">Description</span></span>|<span data-ttu-id="c58da-124">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c58da-124">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c58da-125">json-to-xml</span><span class="sxs-lookup"><span data-stu-id="c58da-125">json-to-xml</span></span>|<span data-ttu-id="c58da-126">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="c58da-126">Root element.</span></span>|<span data-ttu-id="c58da-127">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-127">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="c58da-128">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="c58da-128">Attributes</span></span>  
  
|<span data-ttu-id="c58da-129">Имя</span><span class="sxs-lookup"><span data-stu-id="c58da-129">Name</span></span>|<span data-ttu-id="c58da-130">Описание</span><span class="sxs-lookup"><span data-stu-id="c58da-130">Description</span></span>|<span data-ttu-id="c58da-131">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c58da-131">Required</span></span>|<span data-ttu-id="c58da-132">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="c58da-132">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c58da-133">apply</span><span class="sxs-lookup"><span data-stu-id="c58da-133">apply</span></span>|<span data-ttu-id="c58da-134">Hello атрибут должен быть задан tooone из hello следующие значения.</span><span class="sxs-lookup"><span data-stu-id="c58da-134">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="c58da-135">always — всегда применять преобразование;</span><span class="sxs-lookup"><span data-stu-id="c58da-135">-   always - always apply conversion.</span></span><br /><span data-ttu-id="c58da-136">content-type-json — преобразовать только в том случае, если в заголовке ответа Content-Type указано наличие формата JSON.</span><span class="sxs-lookup"><span data-stu-id="c58da-136">-   content-type-json - convert only if response Content-Type header indicates presence of JSON.</span></span>|<span data-ttu-id="c58da-137">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-137">Yes</span></span>|<span data-ttu-id="c58da-138">Недоступно</span><span class="sxs-lookup"><span data-stu-id="c58da-138">N/A</span></span>|  
|<span data-ttu-id="c58da-139">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="c58da-139">consider-accept-header</span></span>|<span data-ttu-id="c58da-140">Hello атрибут должен быть задан tooone из hello следующие значения.</span><span class="sxs-lookup"><span data-stu-id="c58da-140">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="c58da-141">true — применять преобразование, только если JSON запрашивается в заголовке запроса Accept;</span><span class="sxs-lookup"><span data-stu-id="c58da-141">-   true - apply conversion if JSON is requested in request Accept header.</span></span><br /><span data-ttu-id="c58da-142">false — всегда применять преобразование.</span><span class="sxs-lookup"><span data-stu-id="c58da-142">-   false -always apply conversion.</span></span>|<span data-ttu-id="c58da-143">Нет</span><span class="sxs-lookup"><span data-stu-id="c58da-143">No</span></span>|<span data-ttu-id="c58da-144">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-144">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c58da-145">Использование</span><span class="sxs-lookup"><span data-stu-id="c58da-145">Usage</span></span>  
 <span data-ttu-id="c58da-146">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c58da-146">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c58da-147">**Разделы политики:** inbound, outbound, on-error.</span><span class="sxs-lookup"><span data-stu-id="c58da-147">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="c58da-148">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="c58da-148">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c58da-149"><a name="ConvertXMLtoJSON"></a>Преобразование XML tooJSON</span><span class="sxs-lookup"><span data-stu-id="c58da-149"><a name="ConvertXMLtoJSON"></a> Convert XML tooJSON</span></span>  
 <span data-ttu-id="c58da-150">Hello `xml-to-json` политики преобразует тело запроса или ответа из XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="c58da-150">hello `xml-to-json` policy converts a request or response body from XML tooJSON.</span></span> <span data-ttu-id="c58da-151">Эта политика может быть используется toomodernize API-интерфейсов на основании XML-только для внутренних веб-служб.</span><span class="sxs-lookup"><span data-stu-id="c58da-151">This policy can be used toomodernize APIs based on XML-only backend web services.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c58da-152">Правило политики</span><span class="sxs-lookup"><span data-stu-id="c58da-152">Policy statement</span></span>  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="c58da-153">Пример</span><span class="sxs-lookup"><span data-stu-id="c58da-153">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <xml-to-json kind="direct" apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="c58da-154">Элементы</span><span class="sxs-lookup"><span data-stu-id="c58da-154">Elements</span></span>  
  
|<span data-ttu-id="c58da-155">Имя</span><span class="sxs-lookup"><span data-stu-id="c58da-155">Name</span></span>|<span data-ttu-id="c58da-156">Описание</span><span class="sxs-lookup"><span data-stu-id="c58da-156">Description</span></span>|<span data-ttu-id="c58da-157">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c58da-157">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c58da-158">xml-to-json</span><span class="sxs-lookup"><span data-stu-id="c58da-158">xml-to-json</span></span>|<span data-ttu-id="c58da-159">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="c58da-159">Root element.</span></span>|<span data-ttu-id="c58da-160">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-160">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="c58da-161">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="c58da-161">Attributes</span></span>  
  
|<span data-ttu-id="c58da-162">Имя</span><span class="sxs-lookup"><span data-stu-id="c58da-162">Name</span></span>|<span data-ttu-id="c58da-163">Описание</span><span class="sxs-lookup"><span data-stu-id="c58da-163">Description</span></span>|<span data-ttu-id="c58da-164">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c58da-164">Required</span></span>|<span data-ttu-id="c58da-165">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="c58da-165">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c58da-166">kind</span><span class="sxs-lookup"><span data-stu-id="c58da-166">kind</span></span>|<span data-ttu-id="c58da-167">Hello атрибут должен быть задан tooone из hello следующие значения.</span><span class="sxs-lookup"><span data-stu-id="c58da-167">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="c58da-168">-javascript friendly: hello преобразовать JSON имеет понятное tooJavaScript разработчиков формы.</span><span class="sxs-lookup"><span data-stu-id="c58da-168">-   javascript-friendly - hello converted JSON has a form friendly tooJavaScript developers.</span></span><br /><span data-ttu-id="c58da-169">-direct: hello преобразованный JSON отражает структуру hello исходного документа XML.</span><span class="sxs-lookup"><span data-stu-id="c58da-169">-   direct - hello converted JSON reflects hello original XML document's structure.</span></span>|<span data-ttu-id="c58da-170">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-170">Yes</span></span>|<span data-ttu-id="c58da-171">Недоступно</span><span class="sxs-lookup"><span data-stu-id="c58da-171">N/A</span></span>|  
|<span data-ttu-id="c58da-172">apply</span><span class="sxs-lookup"><span data-stu-id="c58da-172">apply</span></span>|<span data-ttu-id="c58da-173">Hello атрибут должен быть задан tooone из hello следующие значения.</span><span class="sxs-lookup"><span data-stu-id="c58da-173">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="c58da-174">always — всегда применять преобразование;</span><span class="sxs-lookup"><span data-stu-id="c58da-174">-   always - convert always.</span></span><br /><span data-ttu-id="c58da-175">content-type-xml — преобразовать только в том случае, если в заголовке ответа Content-Type указано наличие формата XML.</span><span class="sxs-lookup"><span data-stu-id="c58da-175">-   content-type-xml - convert only if response Content-Type header indicates presence of XML.</span></span>|<span data-ttu-id="c58da-176">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-176">Yes</span></span>|<span data-ttu-id="c58da-177">Недоступно</span><span class="sxs-lookup"><span data-stu-id="c58da-177">N/A</span></span>|  
|<span data-ttu-id="c58da-178">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="c58da-178">consider-accept-header</span></span>|<span data-ttu-id="c58da-179">Hello атрибут должен быть задан tooone из hello следующие значения.</span><span class="sxs-lookup"><span data-stu-id="c58da-179">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="c58da-180">true — применять преобразование, только если XML запрашивается в заголовке запроса Accept;</span><span class="sxs-lookup"><span data-stu-id="c58da-180">-   true - apply conversion if XML is requested in request Accept header.</span></span><br /><span data-ttu-id="c58da-181">false — всегда применять преобразование.</span><span class="sxs-lookup"><span data-stu-id="c58da-181">-   false -always apply conversion.</span></span>|<span data-ttu-id="c58da-182">Нет</span><span class="sxs-lookup"><span data-stu-id="c58da-182">No</span></span>|<span data-ttu-id="c58da-183">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-183">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c58da-184">Использование</span><span class="sxs-lookup"><span data-stu-id="c58da-184">Usage</span></span>  
 <span data-ttu-id="c58da-185">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c58da-185">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c58da-186">**Разделы политики:** inbound, outbound, on-error.</span><span class="sxs-lookup"><span data-stu-id="c58da-186">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="c58da-187">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="c58da-187">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c58da-188"><a name="Findandreplacestringinbody"></a> Поиск и замена строки в тексте</span><span class="sxs-lookup"><span data-stu-id="c58da-188"><a name="Findandreplacestringinbody"></a> Find and replace string in body</span></span>  
 <span data-ttu-id="c58da-189">Hello `find-and-replace` политики поиск подстроки запроса или ответа и ее замена другой подстрокой.</span><span class="sxs-lookup"><span data-stu-id="c58da-189">hello `find-and-replace` policy finds a request or response substring and replaces it with a different substring.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c58da-190">Правило политики</span><span class="sxs-lookup"><span data-stu-id="c58da-190">Policy statement</span></span>  
  
```xml  
<find-and-replace from="what tooreplace" to="replacement" />  
```  
  
### <a name="example"></a><span data-ttu-id="c58da-191">Пример</span><span class="sxs-lookup"><span data-stu-id="c58da-191">Example</span></span>  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a><span data-ttu-id="c58da-192">Элементы</span><span class="sxs-lookup"><span data-stu-id="c58da-192">Elements</span></span>  
  
|<span data-ttu-id="c58da-193">Имя</span><span class="sxs-lookup"><span data-stu-id="c58da-193">Name</span></span>|<span data-ttu-id="c58da-194">Описание</span><span class="sxs-lookup"><span data-stu-id="c58da-194">Description</span></span>|<span data-ttu-id="c58da-195">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c58da-195">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c58da-196">find-and-replace</span><span class="sxs-lookup"><span data-stu-id="c58da-196">find-and-replace</span></span>|<span data-ttu-id="c58da-197">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="c58da-197">Root element.</span></span>|<span data-ttu-id="c58da-198">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-198">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="c58da-199">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="c58da-199">Attributes</span></span>  
  
|<span data-ttu-id="c58da-200">Имя</span><span class="sxs-lookup"><span data-stu-id="c58da-200">Name</span></span>|<span data-ttu-id="c58da-201">Описание</span><span class="sxs-lookup"><span data-stu-id="c58da-201">Description</span></span>|<span data-ttu-id="c58da-202">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c58da-202">Required</span></span>|<span data-ttu-id="c58da-203">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="c58da-203">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c58da-204">from</span><span class="sxs-lookup"><span data-stu-id="c58da-204">from</span></span>|<span data-ttu-id="c58da-205">toosearch строка Hello для.</span><span class="sxs-lookup"><span data-stu-id="c58da-205">hello string toosearch for.</span></span>|<span data-ttu-id="c58da-206">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-206">Yes</span></span>|<span data-ttu-id="c58da-207">Недоступно</span><span class="sxs-lookup"><span data-stu-id="c58da-207">N/A</span></span>|  
|<span data-ttu-id="c58da-208">значение</span><span class="sxs-lookup"><span data-stu-id="c58da-208">to</span></span>|<span data-ttu-id="c58da-209">Строка замены Hello.</span><span class="sxs-lookup"><span data-stu-id="c58da-209">hello replacement string.</span></span> <span data-ttu-id="c58da-210">Укажите строку нулевой длины замены строки tooremove hello поиска.</span><span class="sxs-lookup"><span data-stu-id="c58da-210">Specify a zero length replacement string tooremove hello search string.</span></span>|<span data-ttu-id="c58da-211">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-211">Yes</span></span>|<span data-ttu-id="c58da-212">Недоступно</span><span class="sxs-lookup"><span data-stu-id="c58da-212">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c58da-213">Использование</span><span class="sxs-lookup"><span data-stu-id="c58da-213">Usage</span></span>  
 <span data-ttu-id="c58da-214">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c58da-214">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c58da-215">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="c58da-215">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="c58da-216">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="c58da-216">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c58da-217"><a name="MaskURLSContent"></a> Маскировка URL-адресов в содержимом</span><span class="sxs-lookup"><span data-stu-id="c58da-217"><a name="MaskURLSContent"></a> Mask URLs in content</span></span>  
 <span data-ttu-id="c58da-218">Hello `redirect-content-urls` политики загрузочную запись (маскировка) ссылок в тексте hello, чтобы они указывали toohello равнозначными ссылками через шлюз hello.</span><span class="sxs-lookup"><span data-stu-id="c58da-218">hello `redirect-content-urls` policy re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span> <span data-ttu-id="c58da-219">Используйте в hello разделе "Исходящие" toore записи ответа текст ссылки toomake их toohello точки шлюза.</span><span class="sxs-lookup"><span data-stu-id="c58da-219">Use in hello outbound section toore-write response body links toomake them point toohello gateway.</span></span> <span data-ttu-id="c58da-220">Используйте в hello входящих раздел для получения противоположного результата.</span><span class="sxs-lookup"><span data-stu-id="c58da-220">Use in hello inbound section for an opposite effect.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="c58da-221">Эта политика не изменяет значения заголовка, например заголовка `Location`.</span><span class="sxs-lookup"><span data-stu-id="c58da-221">This policy does not change any header values such as `Location` headers.</span></span> <span data-ttu-id="c58da-222">значения заголовка toochange, использовать hello [заголовка набора](api-management-transformation-policies.md#SetHTTPheader) политики.</span><span class="sxs-lookup"><span data-stu-id="c58da-222">toochange header values, use hello [set-header](api-management-transformation-policies.md#SetHTTPheader) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c58da-223">Правило политики</span><span class="sxs-lookup"><span data-stu-id="c58da-223">Policy statement</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a><span data-ttu-id="c58da-224">Пример</span><span class="sxs-lookup"><span data-stu-id="c58da-224">Example</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a><span data-ttu-id="c58da-225">Элементы</span><span class="sxs-lookup"><span data-stu-id="c58da-225">Elements</span></span>  
  
|<span data-ttu-id="c58da-226">Имя</span><span class="sxs-lookup"><span data-stu-id="c58da-226">Name</span></span>|<span data-ttu-id="c58da-227">Описание</span><span class="sxs-lookup"><span data-stu-id="c58da-227">Description</span></span>|<span data-ttu-id="c58da-228">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c58da-228">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c58da-229">redirect-content-urls</span><span class="sxs-lookup"><span data-stu-id="c58da-229">redirect-content-urls</span></span>|<span data-ttu-id="c58da-230">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="c58da-230">Root element.</span></span>|<span data-ttu-id="c58da-231">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-231">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c58da-232">Использование</span><span class="sxs-lookup"><span data-stu-id="c58da-232">Usage</span></span>  
 <span data-ttu-id="c58da-233">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c58da-233">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c58da-234">**Разделы политики:** inbound, outbound.</span><span class="sxs-lookup"><span data-stu-id="c58da-234">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="c58da-235">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="c58da-235">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c58da-236"><a name="SetBackendService"></a> Задание внутренней службы</span><span class="sxs-lookup"><span data-stu-id="c58da-236"><a name="SetBackendService"></a> Set backend service</span></span>  
 <span data-ttu-id="c58da-237">Используйте hello `set-backend-service` tooredirect политики входящее сообщение запроса другой внутренней tooa чем hello от указанного в параметрах hello API для этой операции.</span><span class="sxs-lookup"><span data-stu-id="c58da-237">Use hello `set-backend-service` policy tooredirect an incoming request tooa different backend than hello one specified in hello API settings for that operation.</span></span> <span data-ttu-id="c58da-238">Этот параметр изменяет hello серверной службы базовый URL-адрес входящего запроса toohello hello, указанному в политике hello.</span><span class="sxs-lookup"><span data-stu-id="c58da-238">This policy changes hello backend service base URL of hello incoming request toohello one specified in hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c58da-239">Правило политики</span><span class="sxs-lookup"><span data-stu-id="c58da-239">Policy statement</span></span>  
  
```xml  
<set-backend-service base-url="base URL of hello backend service" />  
```  
  
### <a name="example"></a><span data-ttu-id="c58da-240">Пример</span><span class="sxs-lookup"><span data-stu-id="c58da-240">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <choose>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2013-05")">  
                <set-backend-service base-url="http://contoso.com/api/8.2/" />  
            </when>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2014-03")">  
                <set-backend-service base-url="http://contoso.com/api/9.1/" />  
            </when>  
        </choose>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
<span data-ttu-id="c58da-241">В этом примере hello политика задания внутренней службы направляет запросы на основе значения версии hello, переданный hello запроса строки tooa другой внутренней службе чем hello один hello, указанный в API.</span><span class="sxs-lookup"><span data-stu-id="c58da-241">In this example hello set backend service policy routes requests based on hello version value passed in hello query string tooa different backend service than hello one specified in hello API.</span></span>
  
<span data-ttu-id="c58da-242">Изначально hello базовый URL-адрес внутренней службы является производным от параметров API hello.</span><span class="sxs-lookup"><span data-stu-id="c58da-242">Initially hello backend service base URL is derived from hello API settings.</span></span> <span data-ttu-id="c58da-243">Здравствуйте, поэтому URL-адрес запроса `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` становится `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` где `http://contoso.com/api/10.4/` является hello внутренний URL-адрес службы указан в настройках hello API.</span><span class="sxs-lookup"><span data-stu-id="c58da-243">So hello request URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` becomes `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` where `http://contoso.com/api/10.4/` is hello backend service URL specified in hello API settings.</span></span>  
  
<span data-ttu-id="c58da-244">Здравствуйте, когда [< выберите\> ](api-management-advanced-policies.md#choose) применяется инструкция политики hello серверной базовый URL-адрес службы может снова измениться слишком`http://contoso.com/api/8.2` или `http://contoso.com/api/9.1`, в зависимости от hello значение параметра запроса hello версии запроса.</span><span class="sxs-lookup"><span data-stu-id="c58da-244">When hello [<choose\>](api-management-advanced-policies.md#choose) policy statement is applied hello backend service base URL may change again either too`http://contoso.com/api/8.2` or `http://contoso.com/api/9.1`, depending on hello value of hello version request query parameter.</span></span> <span data-ttu-id="c58da-245">Например, если hello значение — `"2013-15"` hello последний запрос URL-адрес становится `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span><span class="sxs-lookup"><span data-stu-id="c58da-245">For example, if hello value is `"2013-15"` hello final request URL becomes `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span></span>  
  
<span data-ttu-id="c58da-246">Если дальнейшее преобразование запроса hello не нужное, другие [политик преобразования](api-management-transformation-policies.md#TransformationPolicies) может использоваться.</span><span class="sxs-lookup"><span data-stu-id="c58da-246">If further transformation of hello request is desired, other [Transformation policies](api-management-transformation-policies.md#TransformationPolicies) can be used.</span></span> <span data-ttu-id="c58da-247">Например, tooremove hello версии запроса параметр теперь, когда hello запрос выполняется маршрутизация tooa версии конкретной серверной части, hello [параметра строки запроса](api-management-transformation-policies.md#SetQueryStringParameter) политики можно использовать tooremove hello параметре.</span><span class="sxs-lookup"><span data-stu-id="c58da-247">For example, tooremove hello version query parameter now that hello request is being routed tooa version specific backend, hello  [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policy can be used tooremove hello now redundant version attribute.</span></span>  
  
### <a name="example"></a><span data-ttu-id="c58da-248">Пример</span><span class="sxs-lookup"><span data-stu-id="c58da-248">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <set-backend-service backend-id="my-sf-service" sf-partition-key="@(context.Request.Url.Query.GetValueOrDefault("userId","")" sf-replica-type="primary" /> 
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
<span data-ttu-id="c58da-249">В этот примере hello политики маршруты hello запроса tooa службы структуры серверное приложение используя строку запроса userId hello в качестве ключа секции hello и hello основной реплики раздела hello.</span><span class="sxs-lookup"><span data-stu-id="c58da-249">In this example hello policy routes hello request tooa service fabric backend, using hello userId query string as hello partition key and using hello primary replica of hello partition.</span></span>  

### <a name="elements"></a><span data-ttu-id="c58da-250">Элементы</span><span class="sxs-lookup"><span data-stu-id="c58da-250">Elements</span></span>  
  
|<span data-ttu-id="c58da-251">Имя</span><span class="sxs-lookup"><span data-stu-id="c58da-251">Name</span></span>|<span data-ttu-id="c58da-252">Описание</span><span class="sxs-lookup"><span data-stu-id="c58da-252">Description</span></span>|<span data-ttu-id="c58da-253">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c58da-253">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c58da-254">set-backend-service</span><span class="sxs-lookup"><span data-stu-id="c58da-254">set-backend-service</span></span>|<span data-ttu-id="c58da-255">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="c58da-255">Root element.</span></span>|<span data-ttu-id="c58da-256">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-256">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="c58da-257">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="c58da-257">Attributes</span></span>  
  
|<span data-ttu-id="c58da-258">Имя</span><span class="sxs-lookup"><span data-stu-id="c58da-258">Name</span></span>|<span data-ttu-id="c58da-259">Описание</span><span class="sxs-lookup"><span data-stu-id="c58da-259">Description</span></span>|<span data-ttu-id="c58da-260">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c58da-260">Required</span></span>|<span data-ttu-id="c58da-261">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="c58da-261">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c58da-262">base-url</span><span class="sxs-lookup"><span data-stu-id="c58da-262">base-url</span></span>|<span data-ttu-id="c58da-263">Новый базовый URL-адрес внутренней службы.</span><span class="sxs-lookup"><span data-stu-id="c58da-263">New backend service base URL.</span></span>|<span data-ttu-id="c58da-264">Нет</span><span class="sxs-lookup"><span data-stu-id="c58da-264">No</span></span>|<span data-ttu-id="c58da-265">Недоступно</span><span class="sxs-lookup"><span data-stu-id="c58da-265">N/A</span></span>|  
|<span data-ttu-id="c58da-266">backend-id</span><span class="sxs-lookup"><span data-stu-id="c58da-266">backend-id</span></span>|<span data-ttu-id="c58da-267">Идентификатор hello tooroute серверной части для.</span><span class="sxs-lookup"><span data-stu-id="c58da-267">Identifier of hello backend tooroute to.</span></span>|<span data-ttu-id="c58da-268">Нет</span><span class="sxs-lookup"><span data-stu-id="c58da-268">No</span></span>|<span data-ttu-id="c58da-269">Недоступно</span><span class="sxs-lookup"><span data-stu-id="c58da-269">N/A</span></span>|  
|<span data-ttu-id="c58da-270">sf-partition-key</span><span class="sxs-lookup"><span data-stu-id="c58da-270">sf-partition-key</span></span>|<span data-ttu-id="c58da-271">Применимо только для внутреннего hello — это служба Service Fabric и задается с помощью «идентификатор серверной».</span><span class="sxs-lookup"><span data-stu-id="c58da-271">Only applicable when hello backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="c58da-272">Использовать tooresolve определенный раздел из hello службы разрешения имен.</span><span class="sxs-lookup"><span data-stu-id="c58da-272">Used tooresolve a specific partition from hello name resolution service.</span></span>|<span data-ttu-id="c58da-273">Нет</span><span class="sxs-lookup"><span data-stu-id="c58da-273">No</span></span>|<span data-ttu-id="c58da-274">Недоступно</span><span class="sxs-lookup"><span data-stu-id="c58da-274">N/A</span></span>|  
|<span data-ttu-id="c58da-275">sf-replica-type</span><span class="sxs-lookup"><span data-stu-id="c58da-275">sf-replica-type</span></span>|<span data-ttu-id="c58da-276">Применимо только для внутреннего hello — это служба Service Fabric и задается с помощью «идентификатор серверной».</span><span class="sxs-lookup"><span data-stu-id="c58da-276">Only applicable when hello backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="c58da-277">Элементы управления, если запрос hello должен составлять toohello первичной или вторичной реплики секции.</span><span class="sxs-lookup"><span data-stu-id="c58da-277">Controls if hello request should go toohello primary or secondary replica of a partition.</span></span> |<span data-ttu-id="c58da-278">Нет</span><span class="sxs-lookup"><span data-stu-id="c58da-278">No</span></span>|<span data-ttu-id="c58da-279">Недоступно</span><span class="sxs-lookup"><span data-stu-id="c58da-279">N/A</span></span>|    
|<span data-ttu-id="c58da-280">sf-resolve-condition</span><span class="sxs-lookup"><span data-stu-id="c58da-280">sf-resolve-condition</span></span>|<span data-ttu-id="c58da-281">Применимо только для внутреннего hello — это служба Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c58da-281">Only applicable when hello backend is a Service Fabric service.</span></span> <span data-ttu-id="c58da-282">Определение условия hello вызовите tooService структуры внутренних наличия toobe, повторяющимся в новое решение.</span><span class="sxs-lookup"><span data-stu-id="c58da-282">Condition identifying if hello call tooService Fabric backend has toobe repeated with new resolution.</span></span>|<span data-ttu-id="c58da-283">Нет</span><span class="sxs-lookup"><span data-stu-id="c58da-283">No</span></span>|<span data-ttu-id="c58da-284">Недоступно</span><span class="sxs-lookup"><span data-stu-id="c58da-284">N/A</span></span>|    
|<span data-ttu-id="c58da-285">sf-service-instance-name</span><span class="sxs-lookup"><span data-stu-id="c58da-285">sf-service-instance-name</span></span>|<span data-ttu-id="c58da-286">Применимо только для внутреннего hello — это служба Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c58da-286">Only applicable when hello backend is a Service Fabric service.</span></span> <span data-ttu-id="c58da-287">Позволяет toochange экземплярами служб во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="c58da-287">Allows toochange service instances at runtime.</span></span> |<span data-ttu-id="c58da-288">Нет</span><span class="sxs-lookup"><span data-stu-id="c58da-288">No</span></span>|<span data-ttu-id="c58da-289">Недоступно</span><span class="sxs-lookup"><span data-stu-id="c58da-289">N/A</span></span>|    

### <a name="usage"></a><span data-ttu-id="c58da-290">Использование</span><span class="sxs-lookup"><span data-stu-id="c58da-290">Usage</span></span>  
 <span data-ttu-id="c58da-291">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c58da-291">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c58da-292">**Разделы политики:** inbound, backend.</span><span class="sxs-lookup"><span data-stu-id="c58da-292">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="c58da-293">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="c58da-293">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c58da-294"><a name="SetBody"></a> Задание текста</span><span class="sxs-lookup"><span data-stu-id="c58da-294"><a name="SetBody"></a> Set body</span></span>  
 <span data-ttu-id="c58da-295">Используйте hello `set-body` текст сообщения hello tooset политики для входящих и исходящих запросов.</span><span class="sxs-lookup"><span data-stu-id="c58da-295">Use hello `set-body` policy tooset hello message body for incoming and outgoing requests.</span></span> <span data-ttu-id="c58da-296">tooaccess hello тело сообщения можно использовать hello `context.Request.Body` свойства или hello `context.Response.Body`в зависимости от того, является ли политика hello в hello раздел входящих или исходящих подключений.</span><span class="sxs-lookup"><span data-stu-id="c58da-296">tooaccess hello message body you can use hello `context.Request.Body` property or hello `context.Response.Body`, depending on whether hello policy is in hello inbound or outbound section.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="c58da-297">Обратите внимание, что по умолчанию при доступе к hello тела сообщения с помощью `context.Request.Body` или `context.Response.Body`, исходное сообщение hello текст будет потерян, а также необходимо задать, возвращая текст hello обратно в выражении hello.</span><span class="sxs-lookup"><span data-stu-id="c58da-297">Note that by default when you access hello message body using `context.Request.Body` or `context.Response.Body`, hello original message body is lost and must be set by returning hello body back in hello expression.</span></span> <span data-ttu-id="c58da-298">текст hello toopreserve содержимого, задайте hello `preserveContent` параметр слишком`true` при доступе к приветственное сообщение.</span><span class="sxs-lookup"><span data-stu-id="c58da-298">toopreserve hello body content, set hello `preserveContent` parameter too`true` when accessing hello message.</span></span> <span data-ttu-id="c58da-299">Если `preserveContent` задано слишком`true` и другой текст возвращается оператором выражения hello hello используется текст.</span><span class="sxs-lookup"><span data-stu-id="c58da-299">If `preserveContent` is set too`true` and a different body is returned by hello expression, hello returned body is used.</span></span>  
>   
>  <span data-ttu-id="c58da-300">Имейте в виду следующие рекомендации при использовании hello hello `set-body` политики.</span><span class="sxs-lookup"><span data-stu-id="c58da-300">Please note hello following considerations when using hello `set-body` policy.</span></span>  
>   
>  -   <span data-ttu-id="c58da-301">Если вы используете hello `set-body` tooreturn политики новый или обновленный текст, не требуется tooset `preserveContent` слишком`true` так, как вы явно указали hello новое содержимое тела.</span><span class="sxs-lookup"><span data-stu-id="c58da-301">If you are using hello `set-body` policy tooreturn a new or updated body you don't need tooset `preserveContent` too`true` because you are explicitly supplying hello new body contents.</span></span>  
> -   <span data-ttu-id="c58da-302">Сохранение hello содержимого ответа в конвейер входящих hello не имеет смысла, так как еще нет ответа.</span><span class="sxs-lookup"><span data-stu-id="c58da-302">Preserving hello content of a response in hello inbound pipeline doesn't make sense because there is no response yet.</span></span>  
> -   <span data-ttu-id="c58da-303">Сохранение содержимого hello запроса в конвейер исходящих hello не имеет смысла, так как hello запрос уже был отправлен toohello базы данных на этом этапе.</span><span class="sxs-lookup"><span data-stu-id="c58da-303">Preserving hello content of a request in hello outbound pipeline doesn't make sense because hello request has already been sent toohello backend at this point.</span></span>  
> -   <span data-ttu-id="c58da-304">Если эта политика используется при отсутствии текста сообщения, например во входящем параметре GET, возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="c58da-304">If this policy is used when there is no message body, for example in an inbound GET, an exception is thrown.</span></span>  
  
 <span data-ttu-id="c58da-305">Дополнительные сведения см. в разделе hello `context.Request.Body`, `context.Response.Body`и hello `IMessage` подразделы hello [переменной контекста](api-management-policy-expressions.md#ContextVariables) таблицы.</span><span class="sxs-lookup"><span data-stu-id="c58da-305">For more information, see hello `context.Request.Body`, `context.Response.Body`, and hello `IMessage` sections in hello [Context variable](api-management-policy-expressions.md#ContextVariables) table.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c58da-306">Правило политики</span><span class="sxs-lookup"><span data-stu-id="c58da-306">Policy statement</span></span>  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a><span data-ttu-id="c58da-307">Примеры</span><span class="sxs-lookup"><span data-stu-id="c58da-307">Examples</span></span>  
  
#### <a name="literal-text-example"></a><span data-ttu-id="c58da-308">Пример литерального текста</span><span class="sxs-lookup"><span data-stu-id="c58da-308">Literal text example</span></span>  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-string-note-that-we-are-preserving-hello-original-request-body-so-that-we-can-access-it-later-in-hello-pipeline"></a><span data-ttu-id="c58da-309">Пример, доступ к телу hello в виде строки.</span><span class="sxs-lookup"><span data-stu-id="c58da-309">Example accessing hello body as a string.</span></span> <span data-ttu-id="c58da-310">Обратите внимание что мы сохранение hello исходный текст запроса, можно обратиться к его позже в конвейере hello.</span><span class="sxs-lookup"><span data-stu-id="c58da-310">Note that we are preserving hello original request body so that we can access it later in hello pipeline.</span></span>
  
```xml  
<set-body>  
@{   
    string inBody = context.Request.Body.As<string>(preserveContent: true);   
    if (inBody[0] =='c') {   
        inBody[0] = 'm';   
    }   
    return inBody;   
}  
</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-jobject-note-that-since-we-are-not-reserving-hello-original-request-body-accesing-it-later-in-hello-pipeline-will-result-in-an-exception"></a><span data-ttu-id="c58da-311">Пример, доступ к телу hello как JObject.</span><span class="sxs-lookup"><span data-stu-id="c58da-311">Example accessing hello body as a JObject.</span></span> <span data-ttu-id="c58da-312">Обратите внимание, что так как мы не резервировании hello исходного текста запроса, доступ к его позже в конвейере hello будет приведет к исключению.</span><span class="sxs-lookup"><span data-stu-id="c58da-312">Note that since we are not reserving hello original request body, accesing it later in hello pipeline will result in an exception.</span></span>  
  
```xml  
<set-body>   
@{   
    JObject inBody = context.Request.Body.As<JObject>();   
    if (inBody.attribute == <tag>) {   
        inBody[0] = 'm';   
    }   
    return inBody.ToString();   
}   
</set-body>  
  
```  
  
#### <a name="filter-response-based-on-product"></a><span data-ttu-id="c58da-313">Фильтрация ответа в зависимости от продукта</span><span class="sxs-lookup"><span data-stu-id="c58da-313">Filter response based on product</span></span>  
 <span data-ttu-id="c58da-314">В этом примере показано, как tooperform фильтрация содержимого, удалив элементы данных из ответа hello получил от службы внутренних hello при использовании hello `Starter` продукта.</span><span class="sxs-lookup"><span data-stu-id="c58da-314">This example shows how tooperform content filtering by removing data elements from hello response received from hello backend service when using hello `Starter` product.</span></span> <span data-ttu-id="c58da-315">Демонстрацию настройке и использовании этой политики см. в разделе [177 серии охватывают облачные: более возможности API управления с помощью Влад Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) и too34:30 Перемотка вперед.</span><span class="sxs-lookup"><span data-stu-id="c58da-315">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too34:30.</span></span> <span data-ttu-id="c58da-316">Начинаются с 31:50 toosee Обзор [hello темной API прогноз Sky](https://developer.forecast.io/) для этой демонстрации.</span><span class="sxs-lookup"><span data-stu-id="c58da-316">Start  at 31:50 toosee an overview of [hello Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
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

### <a name="using-liquid-templates-with-set-body"></a><span data-ttu-id="c58da-317">Использование шаблонов Liquid с политикой set-body</span><span class="sxs-lookup"><span data-stu-id="c58da-317">Using Liquid templates with set body</span></span> 
<span data-ttu-id="c58da-318">Hello `set-body` политики может быть hello настроенных toouse [жидкости](https://shopify.github.io/liquid/basics/introduction/) шаблонов языка tootransfom hello тело запроса или ответа.</span><span class="sxs-lookup"><span data-stu-id="c58da-318">hello `set-body` policy can be configured toouse hello [Liquid](https://shopify.github.io/liquid/basics/introduction/) templating language tootransfom hello body of a request or response.</span></span> <span data-ttu-id="c58da-319">Это может быть очень эффективны, если вам требуется toocompletely изменения формы hello формат сообщения.</span><span class="sxs-lookup"><span data-stu-id="c58da-319">This can be very effective if you need toocompletely reshape hello format of your message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c58da-320">Здравствуйте, реализация жидкости, используемых в hello `set-body` политика настроена в «режиме C#».</span><span class="sxs-lookup"><span data-stu-id="c58da-320">hello implementation of Liquid used in hello `set-body` policy is configured in 'C# mode'.</span></span> <span data-ttu-id="c58da-321">Это особенно важно при выполнении действий, таких как фильтрация.</span><span class="sxs-lookup"><span data-stu-id="c58da-321">This is particularly important when doing things such as filtering.</span></span> <span data-ttu-id="c58da-322">Например, с помощью фильтра даты требует использования hello Pascal регистр и C# даты, например форматирования:</span><span class="sxs-lookup"><span data-stu-id="c58da-322">As an example, using a date filter requires hello use of Pascal casing and C# date formatting e.g.:</span></span>
>
> <span data-ttu-id="c58da-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span><span class="sxs-lookup"><span data-stu-id="c58da-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c58da-324">В порядке toocorrectly привязки tooan текст XML с помощью шаблона жидкости hello, используйте `set-header` tooset Content-Type tooeither политики приложения/xml, text/xml (или любой тип, заканчивая + xml); для текст JSON, она должна иметь приложение/json, текста и json (или любой тип конца с + json).</span><span class="sxs-lookup"><span data-stu-id="c58da-324">In order toocorrectly bind tooan XML body using hello Liquid template, use a `set-header` policy tooset Content-Type tooeither application/xml, text/xml (or any type ending with +xml); for a JSON body, it must be application/json, text/json (or any type ending with +json).</span></span>

#### <a name="convert-json-toosoap-using-a-liquid-template"></a><span data-ttu-id="c58da-325">Преобразование с помощью шаблона жидкости tooSOAP JSON</span><span class="sxs-lookup"><span data-stu-id="c58da-325">Convert JSON tooSOAP using a Liquid template</span></span>
```xml
<set-body template="liquid">
    <soap:Envelope xmlns="http://tempuri.org/" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Body>
            <GetOpenOrders>
                <cust>{{body.getOpenOrders.cust}}</cust>
            </GetOpenOrders>
        </soap:Body>
    </soap:Envelope>
</set-body>
```

#### <a name="tranform-json-using-a-liquid-template"></a><span data-ttu-id="c58da-326">Преобразование JSON с помощью шаблона Liquid</span><span class="sxs-lookup"><span data-stu-id="c58da-326">Tranform JSON using a Liquid template</span></span>
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a><span data-ttu-id="c58da-327">Элементы</span><span class="sxs-lookup"><span data-stu-id="c58da-327">Elements</span></span>  
  
|<span data-ttu-id="c58da-328">Имя</span><span class="sxs-lookup"><span data-stu-id="c58da-328">Name</span></span>|<span data-ttu-id="c58da-329">Описание</span><span class="sxs-lookup"><span data-stu-id="c58da-329">Description</span></span>|<span data-ttu-id="c58da-330">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c58da-330">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c58da-331">set-body</span><span class="sxs-lookup"><span data-stu-id="c58da-331">set-body</span></span>|<span data-ttu-id="c58da-332">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="c58da-332">Root element.</span></span> <span data-ttu-id="c58da-333">Содержит текст hello или выражения, которые возвращает текст.</span><span class="sxs-lookup"><span data-stu-id="c58da-333">Contains hello body text or an expressions that returns a body.</span></span>|<span data-ttu-id="c58da-334">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-334">Yes</span></span>|  

### <a name="properties"></a><span data-ttu-id="c58da-335">Свойства</span><span class="sxs-lookup"><span data-stu-id="c58da-335">Properties</span></span>  
  
|<span data-ttu-id="c58da-336">Имя</span><span class="sxs-lookup"><span data-stu-id="c58da-336">Name</span></span>|<span data-ttu-id="c58da-337">Описание</span><span class="sxs-lookup"><span data-stu-id="c58da-337">Description</span></span>|<span data-ttu-id="c58da-338">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c58da-338">Required</span></span>|<span data-ttu-id="c58da-339">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="c58da-339">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c58da-340">шаблон</span><span class="sxs-lookup"><span data-stu-id="c58da-340">template</span></span>|<span data-ttu-id="c58da-341">Используется toochange hello шаблонов режим, задать политику текст hello будет выполняться в.</span><span class="sxs-lookup"><span data-stu-id="c58da-341">Used toochange hello templating mode that hello set body policy will run in.</span></span> <span data-ttu-id="c58da-342">В настоящее время является hello поддерживается только значение:</span><span class="sxs-lookup"><span data-stu-id="c58da-342">Currently hello only supported value is:</span></span><br /><br /><span data-ttu-id="c58da-343">политика текст hello - жидкости - задания будет использовать модуль жидкости шаблонов hello</span><span class="sxs-lookup"><span data-stu-id="c58da-343">- liquid - hello set body policy will use hello liquid templating engine</span></span> |<span data-ttu-id="c58da-344">Нет</span><span class="sxs-lookup"><span data-stu-id="c58da-344">No</span></span>|<span data-ttu-id="c58da-345">liquid</span><span class="sxs-lookup"><span data-stu-id="c58da-345">liquid</span></span>|  

<span data-ttu-id="c58da-346">Для доступа к сведениям о hello запроса и ответа, hello жидкости шаблона можно привязать объект контекста tooa с hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="c58da-346">For accessing information about hello request and response, hello Liquid template can bind tooa context object with hello following properties:</span></span> <br />
<pre>context.
    Request.
        Url
        Method
        OriginalMethod
        OriginalUrl
        IpAddress
        MatchedParameters
        HasBody
        ClientCertificates
        Headers

    Response.
        StatusCode
        Method
        Headers
Url.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString

OriginalUrl.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString
</pre>



### <a name="usage"></a><span data-ttu-id="c58da-347">Использование</span><span class="sxs-lookup"><span data-stu-id="c58da-347">Usage</span></span>  
 <span data-ttu-id="c58da-348">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c58da-348">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c58da-349">**Разделы политики:** inbound, outbound, backend.</span><span class="sxs-lookup"><span data-stu-id="c58da-349">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="c58da-350">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="c58da-350">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c58da-351"><a name="SetHTTPheader"></a> Установка HTTP-заголовка</span><span class="sxs-lookup"><span data-stu-id="c58da-351"><a name="SetHTTPheader"></a> Set HTTP header</span></span>  
 <span data-ttu-id="c58da-352">Hello `set-header` политики присваивает значение tooan существующего ответа и/или заголовка запроса или Добавление нового заголовка ответа и/или запроса.</span><span class="sxs-lookup"><span data-stu-id="c58da-352">hello `set-header` policy assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
 <span data-ttu-id="c58da-353">Вставляет список HTTP-заголовков в HTTP-сообщение.</span><span class="sxs-lookup"><span data-stu-id="c58da-353">Inserts a list of HTTP headers into an HTTP message.</span></span> <span data-ttu-id="c58da-354">При помещении в конвейер входящих сообщений эта политика задает hello заголовки HTTP для запроса hello, передаваемые toohello целевой службы.</span><span class="sxs-lookup"><span data-stu-id="c58da-354">When placed in an inbound pipeline, this policy sets hello HTTP headers for hello request being passed toohello target service.</span></span> <span data-ttu-id="c58da-355">При помещении в конвейер исходящих сообщений эта политика задает hello заголовки HTTP для отправляемого клиент шлюза toohello hello ответа.</span><span class="sxs-lookup"><span data-stu-id="c58da-355">When placed in an outbound pipeline, this policy sets hello HTTP headers for hello response being sent toohello gateway’s client.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c58da-356">Правило политики</span><span class="sxs-lookup"><span data-stu-id="c58da-356">Policy statement</span></span>  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with hello same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a><span data-ttu-id="c58da-357">Примеры</span><span class="sxs-lookup"><span data-stu-id="c58da-357">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="c58da-358">Пример</span><span class="sxs-lookup"><span data-stu-id="c58da-358">Example</span></span>  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a><span data-ttu-id="c58da-359">Контекст сведения toohello серверная служба пересылки</span><span class="sxs-lookup"><span data-stu-id="c58da-359">Forward context information toohello backend service</span></span>  
 <span data-ttu-id="c58da-360">В этом примере показано, как политика tooapply на hello API уровня toosupply контекста сведения toohello серверной службы.</span><span class="sxs-lookup"><span data-stu-id="c58da-360">This example shows how tooapply policy at hello API level toosupply context information toohello backend service.</span></span> <span data-ttu-id="c58da-361">Демонстрацию настройке и использовании этой политики см. в разделе [177 серии охватывают облачные: более возможности API управления с помощью Влад Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) и too10:30 Перемотка вперед.</span><span class="sxs-lookup"><span data-stu-id="c58da-361">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too10:30.</span></span> <span data-ttu-id="c58da-362">В 12:10 отсутствует Демонстрация вызова операции на портале разработчиков hello, где можно просмотреть политики hello на работе.</span><span class="sxs-lookup"><span data-stu-id="c58da-362">At 12:10 there is a demo of calling an operation in hello developer portal where you can see hello policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward some context information, user id and hello region hello gateway is hosted in, toohello backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 <span data-ttu-id="c58da-363">Чтобы узнать больше, см. статью [API Management policy expressions](api-management-policy-expressions.md) (Выражения политики управления API) и раздел [Context variable](api-management-policy-expressions.md#ContextVariables) (Переменная контекста).</span><span class="sxs-lookup"><span data-stu-id="c58da-363">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="c58da-364">Элементы</span><span class="sxs-lookup"><span data-stu-id="c58da-364">Elements</span></span>  
  
|<span data-ttu-id="c58da-365">Имя</span><span class="sxs-lookup"><span data-stu-id="c58da-365">Name</span></span>|<span data-ttu-id="c58da-366">Описание</span><span class="sxs-lookup"><span data-stu-id="c58da-366">Description</span></span>|<span data-ttu-id="c58da-367">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c58da-367">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c58da-368">set-header</span><span class="sxs-lookup"><span data-stu-id="c58da-368">set-header</span></span>|<span data-ttu-id="c58da-369">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="c58da-369">Root element.</span></span>|<span data-ttu-id="c58da-370">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-370">Yes</span></span>|  
|<span data-ttu-id="c58da-371">value</span><span class="sxs-lookup"><span data-stu-id="c58da-371">value</span></span>|<span data-ttu-id="c58da-372">Указывает значение hello hello заголовок toobe набора.</span><span class="sxs-lookup"><span data-stu-id="c58da-372">Specifies hello value of hello header toobe set.</span></span> <span data-ttu-id="c58da-373">Для нескольких заголовков с hello таким же именем, добавьте дополнительные `value` элементов.</span><span class="sxs-lookup"><span data-stu-id="c58da-373">For multiple headers with hello same name add additional `value` elements.</span></span>|<span data-ttu-id="c58da-374">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-374">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="c58da-375">Свойства</span><span class="sxs-lookup"><span data-stu-id="c58da-375">Properties</span></span>  
  
|<span data-ttu-id="c58da-376">Имя</span><span class="sxs-lookup"><span data-stu-id="c58da-376">Name</span></span>|<span data-ttu-id="c58da-377">Описание</span><span class="sxs-lookup"><span data-stu-id="c58da-377">Description</span></span>|<span data-ttu-id="c58da-378">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c58da-378">Required</span></span>|<span data-ttu-id="c58da-379">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="c58da-379">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c58da-380">exists-action</span><span class="sxs-lookup"><span data-stu-id="c58da-380">exists-action</span></span>|<span data-ttu-id="c58da-381">Задает tootake какие действия при hello заголовок уже задан.</span><span class="sxs-lookup"><span data-stu-id="c58da-381">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="c58da-382">Этот атрибут должен иметь одно из последующих значений hello.</span><span class="sxs-lookup"><span data-stu-id="c58da-382">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="c58da-383">-Переопределите - значение hello заменяет существующий заголовок hello.</span><span class="sxs-lookup"><span data-stu-id="c58da-383">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="c58da-384">-skip — не заменяет существующее значение заголовка hello.</span><span class="sxs-lookup"><span data-stu-id="c58da-384">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="c58da-385">-Добавить - добавляет значение существующего заголовка hello значение toohello.</span><span class="sxs-lookup"><span data-stu-id="c58da-385">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="c58da-386">-delete — удаляет hello заголовок из запроса hello.</span><span class="sxs-lookup"><span data-stu-id="c58da-386">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="c58da-387">Если задано слишком`override` перечислении нескольких записей с hello одинаковые имена, результаты в заголовке hello, соответствующим tooall записей о наборах (которые будут указаны несколько раз); в результате hello устанавливается только значения из списка.</span><span class="sxs-lookup"><span data-stu-id="c58da-387">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="c58da-388">Нет</span><span class="sxs-lookup"><span data-stu-id="c58da-388">No</span></span>|<span data-ttu-id="c58da-389">override</span><span class="sxs-lookup"><span data-stu-id="c58da-389">override</span></span>|  
|<span data-ttu-id="c58da-390">name</span><span class="sxs-lookup"><span data-stu-id="c58da-390">name</span></span>|<span data-ttu-id="c58da-391">Указывает имя набора toobe заголовок hello.</span><span class="sxs-lookup"><span data-stu-id="c58da-391">Specifies name of hello header toobe set.</span></span>|<span data-ttu-id="c58da-392">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-392">Yes</span></span>|<span data-ttu-id="c58da-393">Недоступно</span><span class="sxs-lookup"><span data-stu-id="c58da-393">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c58da-394">Использование</span><span class="sxs-lookup"><span data-stu-id="c58da-394">Usage</span></span>  
 <span data-ttu-id="c58da-395">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c58da-395">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c58da-396">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="c58da-396">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="c58da-397">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="c58da-397">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c58da-398"><a name="SetQueryStringParameter"></a> Настройка параметра строки запроса</span><span class="sxs-lookup"><span data-stu-id="c58da-398"><a name="SetQueryStringParameter"></a> Set query string parameter</span></span>  
 <span data-ttu-id="c58da-399">Hello `set-query-parameter` добавляет политики, заменяет значение, или удаляет запрос параметра строки запроса.</span><span class="sxs-lookup"><span data-stu-id="c58da-399">hello `set-query-parameter` policy adds, replaces value of, or deletes request query string parameter.</span></span> <span data-ttu-id="c58da-400">Можно использовать toopass параметров запроса, ожидаемый hello серверной службы, которые являются необязательными, или никогда не присутствуют в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="c58da-400">Can be used toopass query parameters expected by hello backend service which are optional or never present in hello request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c58da-401">Правило политики</span><span class="sxs-lookup"><span data-stu-id="c58da-401">Policy statement</span></span>  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with hello same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a><span data-ttu-id="c58da-402">Примеры</span><span class="sxs-lookup"><span data-stu-id="c58da-402">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="c58da-403">Пример</span><span class="sxs-lookup"><span data-stu-id="c58da-403">Example</span></span>  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with hello same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a><span data-ttu-id="c58da-404">Контекст сведения toohello серверная служба пересылки</span><span class="sxs-lookup"><span data-stu-id="c58da-404">Forward context information toohello backend service</span></span>  
 <span data-ttu-id="c58da-405">В этом примере показано, как политика tooapply на hello API уровня toosupply контекста сведения toohello серверной службы.</span><span class="sxs-lookup"><span data-stu-id="c58da-405">This example shows how tooapply policy at hello API level toosupply context information toohello backend service.</span></span> <span data-ttu-id="c58da-406">Демонстрацию настройке и использовании этой политики см. в разделе [177 серии охватывают облачные: более возможности API управления с помощью Влад Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) и too10:30 Перемотка вперед.</span><span class="sxs-lookup"><span data-stu-id="c58da-406">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too10:30.</span></span> <span data-ttu-id="c58da-407">В 12:10 отсутствует Демонстрация вызова операции на портале разработчиков hello, где можно просмотреть политики hello на работе.</span><span class="sxs-lookup"><span data-stu-id="c58da-407">At 12:10 there is a demo of calling an operation in hello developer portal where you can see hello policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward a piece of context, product name in this example, toohello backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 <span data-ttu-id="c58da-408">Чтобы узнать больше, см. статью [API Management policy expressions](api-management-policy-expressions.md) (Выражения политики управления API) и раздел [Context variable](api-management-policy-expressions.md#ContextVariables) (Переменная контекста).</span><span class="sxs-lookup"><span data-stu-id="c58da-408">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="c58da-409">Элементы</span><span class="sxs-lookup"><span data-stu-id="c58da-409">Elements</span></span>  
  
|<span data-ttu-id="c58da-410">Имя</span><span class="sxs-lookup"><span data-stu-id="c58da-410">Name</span></span>|<span data-ttu-id="c58da-411">Описание</span><span class="sxs-lookup"><span data-stu-id="c58da-411">Description</span></span>|<span data-ttu-id="c58da-412">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c58da-412">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c58da-413">set-query-parameter</span><span class="sxs-lookup"><span data-stu-id="c58da-413">set-query-parameter</span></span>|<span data-ttu-id="c58da-414">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="c58da-414">Root element.</span></span>|<span data-ttu-id="c58da-415">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-415">Yes</span></span>|  
|<span data-ttu-id="c58da-416">value</span><span class="sxs-lookup"><span data-stu-id="c58da-416">value</span></span>|<span data-ttu-id="c58da-417">Указывает значение hello объекта набора toobe параметров запроса hello.</span><span class="sxs-lookup"><span data-stu-id="c58da-417">Specifies hello value of hello query parameter toobe set.</span></span> <span data-ttu-id="c58da-418">Несколько параметров запроса с hello таким же именем, добавьте дополнительные `value` элементов.</span><span class="sxs-lookup"><span data-stu-id="c58da-418">For multiple query parameters with hello same name add additional `value` elements.</span></span>|<span data-ttu-id="c58da-419">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-419">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="c58da-420">Свойства</span><span class="sxs-lookup"><span data-stu-id="c58da-420">Properties</span></span>  
  
|<span data-ttu-id="c58da-421">Имя</span><span class="sxs-lookup"><span data-stu-id="c58da-421">Name</span></span>|<span data-ttu-id="c58da-422">Описание</span><span class="sxs-lookup"><span data-stu-id="c58da-422">Description</span></span>|<span data-ttu-id="c58da-423">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c58da-423">Required</span></span>|<span data-ttu-id="c58da-424">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="c58da-424">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="c58da-425">exists-action</span><span class="sxs-lookup"><span data-stu-id="c58da-425">exists-action</span></span>|<span data-ttu-id="c58da-426">Указывает tootake какие действия, если уже задан параметр запроса hello.</span><span class="sxs-lookup"><span data-stu-id="c58da-426">Specifies what action tootake when hello query parameter is already specified.</span></span> <span data-ttu-id="c58da-427">Этот атрибут должен иметь одно из последующих значений hello.</span><span class="sxs-lookup"><span data-stu-id="c58da-427">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="c58da-428">-Переопределите - hello заменяет значение существующего параметра hello.</span><span class="sxs-lookup"><span data-stu-id="c58da-428">-   override - replaces hello value of hello existing parameter.</span></span><br /><span data-ttu-id="c58da-429">-skip — не заменяет hello значение существующего параметра запроса.</span><span class="sxs-lookup"><span data-stu-id="c58da-429">-   skip - does not replace hello existing query parameter value.</span></span><br /><span data-ttu-id="c58da-430">-Добавить - добавляет hello значение toohello значение существующего параметра запроса.</span><span class="sxs-lookup"><span data-stu-id="c58da-430">-   append - appends hello value toohello existing query parameter value.</span></span><br /><span data-ttu-id="c58da-431">-delete — удаляет параметр запроса hello из запроса hello.</span><span class="sxs-lookup"><span data-stu-id="c58da-431">-   delete - removes hello query parameter from hello request.</span></span><br /><br /> <span data-ttu-id="c58da-432">Если задано слишком`override` перечислении нескольких записей с hello одинаковые имена, результаты в параметр запроса hello, соответствующим tooall записей о наборах (которые будут указаны несколько раз); в результате hello устанавливается только значения из списка.</span><span class="sxs-lookup"><span data-stu-id="c58da-432">When set too`override` enlisting multiple entries with hello same name results in hello query parameter being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="c58da-433">Нет</span><span class="sxs-lookup"><span data-stu-id="c58da-433">No</span></span>|<span data-ttu-id="c58da-434">override</span><span class="sxs-lookup"><span data-stu-id="c58da-434">override</span></span>|  
|<span data-ttu-id="c58da-435">name</span><span class="sxs-lookup"><span data-stu-id="c58da-435">name</span></span>|<span data-ttu-id="c58da-436">Указывает имя набора toobe параметр запроса hello.</span><span class="sxs-lookup"><span data-stu-id="c58da-436">Specifies name of hello query parameter toobe set.</span></span>|<span data-ttu-id="c58da-437">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-437">Yes</span></span>|<span data-ttu-id="c58da-438">Недоступно</span><span class="sxs-lookup"><span data-stu-id="c58da-438">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c58da-439">Использование</span><span class="sxs-lookup"><span data-stu-id="c58da-439">Usage</span></span>  
 <span data-ttu-id="c58da-440">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c58da-440">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c58da-441">**Разделы политики:** inbound, backend.</span><span class="sxs-lookup"><span data-stu-id="c58da-441">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="c58da-442">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="c58da-442">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="c58da-443"><a name="RewriteURL"></a> Перезапись URL-адреса</span><span class="sxs-lookup"><span data-stu-id="c58da-443"><a name="RewriteURL"></a> Rewrite URL</span></span>  
 <span data-ttu-id="c58da-444">Hello `rewrite-uri` политики преобразование URL-АДРЕСЕ запроса из формы toohello общей формы ожидаемый hello веб-службы, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="c58da-444">hello `rewrite-uri` policy converts a request URL from its public form toohello form expected by hello web service, as shown in hello following example.</span></span>  
  
-   <span data-ttu-id="c58da-445">Открытый URL — `http://api.example.com/storenumber/ordernumber`.</span><span class="sxs-lookup"><span data-stu-id="c58da-445">Public URL - `http://api.example.com/storenumber/ordernumber`</span></span>  
  
-   <span data-ttu-id="c58da-446">URL-адрес запроса — `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`.</span><span class="sxs-lookup"><span data-stu-id="c58da-446">Request URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span></span>  
  
 <span data-ttu-id="c58da-447">Эта политика может использоваться, когда отдела или со средствами браузера URL-адрес необходимо преобразовать в формат URL-адрес hello, ожидаемый hello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="c58da-447">This policy can be used when a human and/or browser-friendly URL should be transformed into hello URL format expected by hello web service.</span></span> <span data-ttu-id="c58da-448">Этот параметр требуется только при представлении альтернативный формат URL-адрес, например чистой URL-адреса, RESTful URL-адреса, удобный для восприятия человеком или Оптимизированных для поисковых систем URL-адресов, которые являются исключительно структурными URL-адреса, которые не содержат строку запроса, а состоят только hello путь hello toobe ресурс (после hello схемы и hello полномочий).</span><span class="sxs-lookup"><span data-stu-id="c58da-448">This policy only needs toobe applied when exposing an alternative URL format, such as clean URLs, RESTful URLs, user-friendly URLs or SEO-friendly URLs that are purely structural URLs that do not contain a query string and instead contain only hello path of hello resource (after hello scheme and hello authority).</span></span> <span data-ttu-id="c58da-449">Это часто делает в эстетических целях, для удобства и простоты использования или для оптимизации поисковых систем (SEO).</span><span class="sxs-lookup"><span data-stu-id="c58da-449">This is often done for aesthetic, usability, or search engine optimization (SEO) purposes.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="c58da-450">Можно добавлять только параметры строки запроса с помощью политики hello.</span><span class="sxs-lookup"><span data-stu-id="c58da-450">You can only add query string parameters using hello policy.</span></span> <span data-ttu-id="c58da-451">Вы не может добавить дополнительные параметры шаблона пути в hello замена URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="c58da-451">You cannot add extra template path parameters in hello rewrite URL.</span></span>  

### <a name="policy-statement"></a><span data-ttu-id="c58da-452">Правило политики</span><span class="sxs-lookup"><span data-stu-id="c58da-452">Policy statement</span></span>  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a><span data-ttu-id="c58da-453">Пример</span><span class="sxs-lookup"><span data-stu-id="c58da-453">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/v2/US/hardware/{storenumber}&{ordernumber}?City=city&State=state" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put?c=d -->
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" copy-unmatched-params="false" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put -->
```

### <a name="elements"></a><span data-ttu-id="c58da-454">Элементы</span><span class="sxs-lookup"><span data-stu-id="c58da-454">Elements</span></span>  
  
|<span data-ttu-id="c58da-455">Имя</span><span class="sxs-lookup"><span data-stu-id="c58da-455">Name</span></span>|<span data-ttu-id="c58da-456">Описание</span><span class="sxs-lookup"><span data-stu-id="c58da-456">Description</span></span>|<span data-ttu-id="c58da-457">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c58da-457">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c58da-458">rewrite-uri</span><span class="sxs-lookup"><span data-stu-id="c58da-458">rewrite-uri</span></span>|<span data-ttu-id="c58da-459">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="c58da-459">Root element.</span></span>|<span data-ttu-id="c58da-460">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-460">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="c58da-461">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="c58da-461">Attributes</span></span>  
  
|<span data-ttu-id="c58da-462">Атрибут</span><span class="sxs-lookup"><span data-stu-id="c58da-462">Attribute</span></span>|<span data-ttu-id="c58da-463">Описание</span><span class="sxs-lookup"><span data-stu-id="c58da-463">Description</span></span>|<span data-ttu-id="c58da-464">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c58da-464">Required</span></span>|<span data-ttu-id="c58da-465">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="c58da-465">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="c58da-466">шаблон</span><span class="sxs-lookup"><span data-stu-id="c58da-466">template</span></span>|<span data-ttu-id="c58da-467">Hello фактический URL-адресу с все параметры строки запроса.</span><span class="sxs-lookup"><span data-stu-id="c58da-467">hello actual web service URL with any query string parameters.</span></span> <span data-ttu-id="c58da-468">При использовании выражений, hello всего значения должен быть выражением.</span><span class="sxs-lookup"><span data-stu-id="c58da-468">When using expressions, hello whole value must be an expression.</span></span>|<span data-ttu-id="c58da-469">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-469">Yes</span></span>|<span data-ttu-id="c58da-470">Недоступно</span><span class="sxs-lookup"><span data-stu-id="c58da-470">N/A</span></span>|  
|<span data-ttu-id="c58da-471">copy-unmatched-params</span><span class="sxs-lookup"><span data-stu-id="c58da-471">copy-unmatched-params</span></span>|<span data-ttu-id="c58da-472">Указывает параметры запроса в hello входящего запроса не присутствует в hello исходного URL-адрес шаблона, добавляются ли URL-адрес toohello определяется hello обновленной версии шаблона</span><span class="sxs-lookup"><span data-stu-id="c58da-472">Specifies whether query parameters in hello incoming request not present in hello original URL template are added toohello URL defined by hello re-write template</span></span>|<span data-ttu-id="c58da-473">Нет</span><span class="sxs-lookup"><span data-stu-id="c58da-473">No</span></span>|<span data-ttu-id="c58da-474">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-474">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c58da-475">Использование</span><span class="sxs-lookup"><span data-stu-id="c58da-475">Usage</span></span>  
 <span data-ttu-id="c58da-476">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c58da-476">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c58da-477">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="c58da-477">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="c58da-478">**Области политики:** product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="c58da-478">**Policy scopes:** product, API, operation</span></span>  
  
##  <span data-ttu-id="c58da-479"><a name="XSLTransform"></a> Преобразование XML с помощью XSLT</span><span class="sxs-lookup"><span data-stu-id="c58da-479"><a name="XSLTransform"></a> Transform XML using an XSLT</span></span>  
 <span data-ttu-id="c58da-480">Hello `Transform XML using an XSLT` tooXML преобразование XSL в тексте запроса или ответа hello применяется политика.</span><span class="sxs-lookup"><span data-stu-id="c58da-480">hello `Transform XML using an XSLT` policy applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="c58da-481">Правило политики</span><span class="sxs-lookup"><span data-stu-id="c58da-481">Policy statement</span></span>  
  
```xml  
<xsl-transform>  
    <parameter name="User-Agent">@(context.Request.Headers.GetValueOrDefault("User-Agent","non-specified"))</parameter>  
    <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
        <xsl:output method="xml" indent="yes" />  
        <xsl:param name="User-Agent" />  
        <xsl:template match="* | @* | node()">  
            <xsl:copy>  
                <xsl:if test="self::* and not(parent::*)">  
                    <xsl:attribute name="User-Agent">  
                        <xsl:value-of select="$User-Agent" />  
                    </xsl:attribute>  
                </xsl:if>  
                <xsl:apply-templates select="* | @* | node()" />  
            </xsl:copy>  
        </xsl:template>  
    </xsl:stylesheet>  
  </xsl-transform>  
```  
  
### <a name="example"></a><span data-ttu-id="c58da-482">Пример</span><span class="sxs-lookup"><span data-stu-id="c58da-482">Example</span></span>  
  
```xml  
<policies>  
  <inbound>  
      <base />  
  </inbound>  
  <outbound>  
      <base />  
      <xsl-transform>  
        <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
            <xsl:output omit-xml-declaration="yes" method="xml" indent="yes" />  
            <!-- Copy all nodes directly-->  
            <xsl:template match="node()| @*|*">  
                <xsl:copy>  
                    <xsl:apply-templates select="@* | node()|*" />  
                </xsl:copy>  
            </xsl:template>  
        </xsl:stylesheet>  
    </xsl-transform>  
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="c58da-483">Элементы</span><span class="sxs-lookup"><span data-stu-id="c58da-483">Elements</span></span>  
  
|<span data-ttu-id="c58da-484">Имя</span><span class="sxs-lookup"><span data-stu-id="c58da-484">Name</span></span>|<span data-ttu-id="c58da-485">Описание</span><span class="sxs-lookup"><span data-stu-id="c58da-485">Description</span></span>|<span data-ttu-id="c58da-486">Обязательно</span><span class="sxs-lookup"><span data-stu-id="c58da-486">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="c58da-487">xsl-transform</span><span class="sxs-lookup"><span data-stu-id="c58da-487">xsl-transform</span></span>|<span data-ttu-id="c58da-488">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="c58da-488">Root element.</span></span>|<span data-ttu-id="c58da-489">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-489">Yes</span></span>|  
|<span data-ttu-id="c58da-490">Параметр</span><span class="sxs-lookup"><span data-stu-id="c58da-490">parameter</span></span>|<span data-ttu-id="c58da-491">Используется toodefine переменные, используемые в преобразовании hello</span><span class="sxs-lookup"><span data-stu-id="c58da-491">Used toodefine variables used in hello transform</span></span>|<span data-ttu-id="c58da-492">Нет</span><span class="sxs-lookup"><span data-stu-id="c58da-492">No</span></span>|  
|<span data-ttu-id="c58da-493">xsl:stylesheet</span><span class="sxs-lookup"><span data-stu-id="c58da-493">xsl:stylesheet</span></span>|<span data-ttu-id="c58da-494">Корневой элемент таблицы стилей.</span><span class="sxs-lookup"><span data-stu-id="c58da-494">Root stylesheet element.</span></span> <span data-ttu-id="c58da-495">Все элементы и атрибуты, определенные в стандарту hello [спецификацию XSLT](http://www.w3.org/TR/xslt)</span><span class="sxs-lookup"><span data-stu-id="c58da-495">All elements and attributes defined within follow hello standard [XSLT specification](http://www.w3.org/TR/xslt)</span></span>|<span data-ttu-id="c58da-496">Да</span><span class="sxs-lookup"><span data-stu-id="c58da-496">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="c58da-497">Использование</span><span class="sxs-lookup"><span data-stu-id="c58da-497">Usage</span></span>  
 <span data-ttu-id="c58da-498">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="c58da-498">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="c58da-499">**Разделы политики:** inbound, outbound.</span><span class="sxs-lookup"><span data-stu-id="c58da-499">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="c58da-500">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="c58da-500">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="c58da-501">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c58da-501">Next steps</span></span>
<span data-ttu-id="c58da-502">Дополнительные сведения о работе с политиками см. в статье со справочными материалами по [политикам в службе управления API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="c58da-502">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
