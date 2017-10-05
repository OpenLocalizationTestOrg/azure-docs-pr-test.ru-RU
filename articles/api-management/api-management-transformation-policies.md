---
title: "Политики преобразования службы управления API Azure | Документация Майкрософт"
description: "Сведения о политиках преобразования, доступных для использования в службе управления API Azure."
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
ms.openlocfilehash: c2bed904b82c569b28a6e00d0cc9b49107c148dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-transformation-policies"></a><span data-ttu-id="d5b26-103">Политики преобразования службы управления API</span><span class="sxs-lookup"><span data-stu-id="d5b26-103">API Management transformation policies</span></span>
<span data-ttu-id="d5b26-104">В этой статье рассматриваются приведенные ниже политики управления API.</span><span class="sxs-lookup"><span data-stu-id="d5b26-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="d5b26-105">Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в управлении API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="d5b26-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="d5b26-106"><a name="TransformationPolicies"></a> Политики преобразования</span><span class="sxs-lookup"><span data-stu-id="d5b26-106"><a name="TransformationPolicies"></a> Transformation policies</span></span>  
  
-   <span data-ttu-id="d5b26-107">[Преобразование JSON в XML](api-management-transformation-policies.md#ConvertJSONtoXML) – преобразует текст запроса или ответа в формате JSON в формат XML.</span><span class="sxs-lookup"><span data-stu-id="d5b26-107">[Convert JSON to XML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON to XML.</span></span>  
  
-   <span data-ttu-id="d5b26-108">[Преобразование XML в JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) – преобразует текст запроса или ответа в формате XML в формат JSON.</span><span class="sxs-lookup"><span data-stu-id="d5b26-108">[Convert XML to JSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML to JSON.</span></span>  
  
-   <span data-ttu-id="d5b26-109">[Поиск и замена строки в тексте](api-management-transformation-policies.md#Findandreplacestringinbody) – отыскивает подстроку запроса или ответа и заменяет ее на другую подстроку.</span><span class="sxs-lookup"><span data-stu-id="d5b26-109">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
-   <span data-ttu-id="d5b26-110">[Маскировка URL-адресов в содержимом](api-management-transformation-policies.md#MaskURLSContent) — перезаписывает (маскирует) ссылки в тексте ответа так, чтобы каждая из них указывала на эквивалентную ссылку через шлюз.</span><span class="sxs-lookup"><span data-stu-id="d5b26-110">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span>  
  
-   <span data-ttu-id="d5b26-111">[Задание внутренней службы](api-management-transformation-policies.md#SetBackendService) – изменяет внутреннюю службу для входящего запроса.</span><span class="sxs-lookup"><span data-stu-id="d5b26-111">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes the backend service for an incoming request.</span></span>  
  
-   <span data-ttu-id="d5b26-112">[Задание текста](api-management-transformation-policies.md#SetBody) – задает текст сообщения для входящих и исходящих запросов.</span><span class="sxs-lookup"><span data-stu-id="d5b26-112">[Set body](api-management-transformation-policies.md#SetBody) - Sets the message body for incoming and outgoing requests.</span></span>  
  
-   <span data-ttu-id="d5b26-113">[Установка HTTP-заголовка](api-management-transformation-policies.md#SetHTTPheader) -– назначает значение существующему заголовку ответа и/или запроса или добавляет новый заголовок ответа и/или запроса.</span><span class="sxs-lookup"><span data-stu-id="d5b26-113">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
-   <span data-ttu-id="d5b26-114">[Настройка параметра строки запроса](api-management-transformation-policies.md#SetQueryStringParameter) - добавляет, заменяет значение или удаляет параметр строки запроса.</span><span class="sxs-lookup"><span data-stu-id="d5b26-114">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
-   <span data-ttu-id="d5b26-115">[Перезапись URL-адреса](api-management-transformation-policies.md#RewriteURL) – преобразует URL-адрес запроса из его общедоступной формы в форму, ожидаемую веб-службой.</span><span class="sxs-lookup"><span data-stu-id="d5b26-115">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form to the form expected by the web service.</span></span>  
  
-   <span data-ttu-id="d5b26-116">[Преобразование XML с помощью XSLT](api-management-transformation-policies.md#XSLTransform) — применяет преобразование данных в формате XSL в формат XML в тексте запроса или ответа.</span><span class="sxs-lookup"><span data-stu-id="d5b26-116">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation to XML in the request or response body.</span></span>  
  
##  <span data-ttu-id="d5b26-117"><a name="ConvertJSONtoXML"></a> Преобразование JSON в XML</span><span class="sxs-lookup"><span data-stu-id="d5b26-117"><a name="ConvertJSONtoXML"></a> Convert JSON to XML</span></span>  
 <span data-ttu-id="d5b26-118">Политика `json-to-xml` преобразует текст запроса или ответа в формате JSON в формат XML.</span><span class="sxs-lookup"><span data-stu-id="d5b26-118">The `json-to-xml` policy converts a request or response body from JSON to XML.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d5b26-119">Правило политики</span><span class="sxs-lookup"><span data-stu-id="d5b26-119">Policy statement</span></span>  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="d5b26-120">Пример</span><span class="sxs-lookup"><span data-stu-id="d5b26-120">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="d5b26-121">Элементы</span><span class="sxs-lookup"><span data-stu-id="d5b26-121">Elements</span></span>  
  
|<span data-ttu-id="d5b26-122">Имя</span><span class="sxs-lookup"><span data-stu-id="d5b26-122">Name</span></span>|<span data-ttu-id="d5b26-123">Описание</span><span class="sxs-lookup"><span data-stu-id="d5b26-123">Description</span></span>|<span data-ttu-id="d5b26-124">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5b26-124">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d5b26-125">json-to-xml</span><span class="sxs-lookup"><span data-stu-id="d5b26-125">json-to-xml</span></span>|<span data-ttu-id="d5b26-126">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="d5b26-126">Root element.</span></span>|<span data-ttu-id="d5b26-127">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-127">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d5b26-128">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="d5b26-128">Attributes</span></span>  
  
|<span data-ttu-id="d5b26-129">Имя</span><span class="sxs-lookup"><span data-stu-id="d5b26-129">Name</span></span>|<span data-ttu-id="d5b26-130">Описание</span><span class="sxs-lookup"><span data-stu-id="d5b26-130">Description</span></span>|<span data-ttu-id="d5b26-131">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5b26-131">Required</span></span>|<span data-ttu-id="d5b26-132">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d5b26-132">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d5b26-133">apply</span><span class="sxs-lookup"><span data-stu-id="d5b26-133">apply</span></span>|<span data-ttu-id="d5b26-134">Для атрибута нужно задать одно из следующих значений:</span><span class="sxs-lookup"><span data-stu-id="d5b26-134">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="d5b26-135">always — всегда применять преобразование;</span><span class="sxs-lookup"><span data-stu-id="d5b26-135">-   always - always apply conversion.</span></span><br /><span data-ttu-id="d5b26-136">content-type-json — преобразовать только в том случае, если в заголовке ответа Content-Type указано наличие формата JSON.</span><span class="sxs-lookup"><span data-stu-id="d5b26-136">-   content-type-json - convert only if response Content-Type header indicates presence of JSON.</span></span>|<span data-ttu-id="d5b26-137">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-137">Yes</span></span>|<span data-ttu-id="d5b26-138">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d5b26-138">N/A</span></span>|  
|<span data-ttu-id="d5b26-139">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="d5b26-139">consider-accept-header</span></span>|<span data-ttu-id="d5b26-140">Для атрибута нужно задать одно из следующих значений:</span><span class="sxs-lookup"><span data-stu-id="d5b26-140">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="d5b26-141">true — применять преобразование, только если JSON запрашивается в заголовке запроса Accept;</span><span class="sxs-lookup"><span data-stu-id="d5b26-141">-   true - apply conversion if JSON is requested in request Accept header.</span></span><br /><span data-ttu-id="d5b26-142">false — всегда применять преобразование.</span><span class="sxs-lookup"><span data-stu-id="d5b26-142">-   false -always apply conversion.</span></span>|<span data-ttu-id="d5b26-143">Нет</span><span class="sxs-lookup"><span data-stu-id="d5b26-143">No</span></span>|<span data-ttu-id="d5b26-144">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-144">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d5b26-145">Использование</span><span class="sxs-lookup"><span data-stu-id="d5b26-145">Usage</span></span>  
 <span data-ttu-id="d5b26-146">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d5b26-146">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d5b26-147">**Разделы политики:** inbound, outbound, on-error.</span><span class="sxs-lookup"><span data-stu-id="d5b26-147">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="d5b26-148">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="d5b26-148">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d5b26-149"><a name="ConvertXMLtoJSON"></a> Преобразование XML в JSON</span><span class="sxs-lookup"><span data-stu-id="d5b26-149"><a name="ConvertXMLtoJSON"></a> Convert XML to JSON</span></span>  
 <span data-ttu-id="d5b26-150">Политика `xml-to-json` преобразует текст запроса или ответа в формате XML в формат JSON.</span><span class="sxs-lookup"><span data-stu-id="d5b26-150">The `xml-to-json` policy converts a request or response body from XML to JSON.</span></span> <span data-ttu-id="d5b26-151">Эту политику можно использовать для модернизации интерфейсов API, основанных на серверных веб-службах (только XML).</span><span class="sxs-lookup"><span data-stu-id="d5b26-151">This policy can be used to modernize APIs based on XML-only backend web services.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d5b26-152">Правило политики</span><span class="sxs-lookup"><span data-stu-id="d5b26-152">Policy statement</span></span>  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="d5b26-153">Пример</span><span class="sxs-lookup"><span data-stu-id="d5b26-153">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="d5b26-154">Элементы</span><span class="sxs-lookup"><span data-stu-id="d5b26-154">Elements</span></span>  
  
|<span data-ttu-id="d5b26-155">Имя</span><span class="sxs-lookup"><span data-stu-id="d5b26-155">Name</span></span>|<span data-ttu-id="d5b26-156">Описание</span><span class="sxs-lookup"><span data-stu-id="d5b26-156">Description</span></span>|<span data-ttu-id="d5b26-157">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5b26-157">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d5b26-158">xml-to-json</span><span class="sxs-lookup"><span data-stu-id="d5b26-158">xml-to-json</span></span>|<span data-ttu-id="d5b26-159">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="d5b26-159">Root element.</span></span>|<span data-ttu-id="d5b26-160">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-160">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d5b26-161">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="d5b26-161">Attributes</span></span>  
  
|<span data-ttu-id="d5b26-162">Имя</span><span class="sxs-lookup"><span data-stu-id="d5b26-162">Name</span></span>|<span data-ttu-id="d5b26-163">Описание</span><span class="sxs-lookup"><span data-stu-id="d5b26-163">Description</span></span>|<span data-ttu-id="d5b26-164">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5b26-164">Required</span></span>|<span data-ttu-id="d5b26-165">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d5b26-165">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d5b26-166">kind</span><span class="sxs-lookup"><span data-stu-id="d5b26-166">kind</span></span>|<span data-ttu-id="d5b26-167">Для атрибута нужно задать одно из следующих значений:</span><span class="sxs-lookup"><span data-stu-id="d5b26-167">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="d5b26-168">javascript-friendly — преобразованный JSON имеет форму, понятную разработчикам JavaScript;</span><span class="sxs-lookup"><span data-stu-id="d5b26-168">-   javascript-friendly - the converted JSON has a form friendly to JavaScript developers.</span></span><br /><span data-ttu-id="d5b26-169">direct — преобразованный JSON отражает структуру исходного XML-документа.</span><span class="sxs-lookup"><span data-stu-id="d5b26-169">-   direct - the converted JSON reflects the original XML document's structure.</span></span>|<span data-ttu-id="d5b26-170">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-170">Yes</span></span>|<span data-ttu-id="d5b26-171">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d5b26-171">N/A</span></span>|  
|<span data-ttu-id="d5b26-172">apply</span><span class="sxs-lookup"><span data-stu-id="d5b26-172">apply</span></span>|<span data-ttu-id="d5b26-173">Для атрибута нужно задать одно из следующих значений:</span><span class="sxs-lookup"><span data-stu-id="d5b26-173">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="d5b26-174">always — всегда применять преобразование;</span><span class="sxs-lookup"><span data-stu-id="d5b26-174">-   always - convert always.</span></span><br /><span data-ttu-id="d5b26-175">content-type-xml — преобразовать только в том случае, если в заголовке ответа Content-Type указано наличие формата XML.</span><span class="sxs-lookup"><span data-stu-id="d5b26-175">-   content-type-xml - convert only if response Content-Type header indicates presence of XML.</span></span>|<span data-ttu-id="d5b26-176">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-176">Yes</span></span>|<span data-ttu-id="d5b26-177">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d5b26-177">N/A</span></span>|  
|<span data-ttu-id="d5b26-178">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="d5b26-178">consider-accept-header</span></span>|<span data-ttu-id="d5b26-179">Для атрибута нужно задать одно из следующих значений:</span><span class="sxs-lookup"><span data-stu-id="d5b26-179">The attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="d5b26-180">true — применять преобразование, только если XML запрашивается в заголовке запроса Accept;</span><span class="sxs-lookup"><span data-stu-id="d5b26-180">-   true - apply conversion if XML is requested in request Accept header.</span></span><br /><span data-ttu-id="d5b26-181">false — всегда применять преобразование.</span><span class="sxs-lookup"><span data-stu-id="d5b26-181">-   false -always apply conversion.</span></span>|<span data-ttu-id="d5b26-182">Нет</span><span class="sxs-lookup"><span data-stu-id="d5b26-182">No</span></span>|<span data-ttu-id="d5b26-183">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-183">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d5b26-184">Использование</span><span class="sxs-lookup"><span data-stu-id="d5b26-184">Usage</span></span>  
 <span data-ttu-id="d5b26-185">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d5b26-185">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d5b26-186">**Разделы политики:** inbound, outbound, on-error.</span><span class="sxs-lookup"><span data-stu-id="d5b26-186">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="d5b26-187">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="d5b26-187">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d5b26-188"><a name="Findandreplacestringinbody"></a> Поиск и замена строки в тексте</span><span class="sxs-lookup"><span data-stu-id="d5b26-188"><a name="Findandreplacestringinbody"></a> Find and replace string in body</span></span>  
 <span data-ttu-id="d5b26-189">Политика `find-and-replace` отыскивает подстроку запроса или ответа и заменяет ее на другую подстроку.</span><span class="sxs-lookup"><span data-stu-id="d5b26-189">The `find-and-replace` policy finds a request or response substring and replaces it with a different substring.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d5b26-190">Правило политики</span><span class="sxs-lookup"><span data-stu-id="d5b26-190">Policy statement</span></span>  
  
```xml  
<find-and-replace from="what to replace" to="replacement" />  
```  
  
### <a name="example"></a><span data-ttu-id="d5b26-191">Пример</span><span class="sxs-lookup"><span data-stu-id="d5b26-191">Example</span></span>  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a><span data-ttu-id="d5b26-192">Элементы</span><span class="sxs-lookup"><span data-stu-id="d5b26-192">Elements</span></span>  
  
|<span data-ttu-id="d5b26-193">Имя</span><span class="sxs-lookup"><span data-stu-id="d5b26-193">Name</span></span>|<span data-ttu-id="d5b26-194">Описание</span><span class="sxs-lookup"><span data-stu-id="d5b26-194">Description</span></span>|<span data-ttu-id="d5b26-195">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5b26-195">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d5b26-196">find-and-replace</span><span class="sxs-lookup"><span data-stu-id="d5b26-196">find-and-replace</span></span>|<span data-ttu-id="d5b26-197">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="d5b26-197">Root element.</span></span>|<span data-ttu-id="d5b26-198">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-198">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d5b26-199">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="d5b26-199">Attributes</span></span>  
  
|<span data-ttu-id="d5b26-200">Имя</span><span class="sxs-lookup"><span data-stu-id="d5b26-200">Name</span></span>|<span data-ttu-id="d5b26-201">Описание</span><span class="sxs-lookup"><span data-stu-id="d5b26-201">Description</span></span>|<span data-ttu-id="d5b26-202">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5b26-202">Required</span></span>|<span data-ttu-id="d5b26-203">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d5b26-203">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d5b26-204">from</span><span class="sxs-lookup"><span data-stu-id="d5b26-204">from</span></span>|<span data-ttu-id="d5b26-205">Строка, которую нужно найти.</span><span class="sxs-lookup"><span data-stu-id="d5b26-205">The string to search for.</span></span>|<span data-ttu-id="d5b26-206">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-206">Yes</span></span>|<span data-ttu-id="d5b26-207">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d5b26-207">N/A</span></span>|  
|<span data-ttu-id="d5b26-208">значение</span><span class="sxs-lookup"><span data-stu-id="d5b26-208">to</span></span>|<span data-ttu-id="d5b26-209">Строка замены.</span><span class="sxs-lookup"><span data-stu-id="d5b26-209">The replacement string.</span></span> <span data-ttu-id="d5b26-210">Укажите строку замены с нулевой длиной для удаления строки поиска.</span><span class="sxs-lookup"><span data-stu-id="d5b26-210">Specify a zero length replacement string to remove the search string.</span></span>|<span data-ttu-id="d5b26-211">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-211">Yes</span></span>|<span data-ttu-id="d5b26-212">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d5b26-212">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d5b26-213">Использование</span><span class="sxs-lookup"><span data-stu-id="d5b26-213">Usage</span></span>  
 <span data-ttu-id="d5b26-214">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d5b26-214">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d5b26-215">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="d5b26-215">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="d5b26-216">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="d5b26-216">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d5b26-217"><a name="MaskURLSContent"></a> Маскировка URL-адресов в содержимом</span><span class="sxs-lookup"><span data-stu-id="d5b26-217"><a name="MaskURLSContent"></a> Mask URLs in content</span></span>  
 <span data-ttu-id="d5b26-218">Политика `redirect-content-urls` перезаписывает (маскирует) ссылки в тексте ответа так, чтобы каждая из них указывала на эквивалентную ссылку через шлюз.</span><span class="sxs-lookup"><span data-stu-id="d5b26-218">The `redirect-content-urls` policy re-writes (masks) links in the response body so that they point to the equivalent link via the gateway.</span></span> <span data-ttu-id="d5b26-219">Используйте в разделе outbound, чтобы перезаписать ссылки текста ответа так, чтобы они указывали на шлюз.</span><span class="sxs-lookup"><span data-stu-id="d5b26-219">Use in the outbound section to re-write response body links to make them point to the gateway.</span></span> <span data-ttu-id="d5b26-220">Используйте в разделе inbound для обратного эффекта.</span><span class="sxs-lookup"><span data-stu-id="d5b26-220">Use in the inbound section for an opposite effect.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="d5b26-221">Эта политика не изменяет значения заголовка, например заголовка `Location`.</span><span class="sxs-lookup"><span data-stu-id="d5b26-221">This policy does not change any header values such as `Location` headers.</span></span> <span data-ttu-id="d5b26-222">Чтобы изменить значения заголовка, используйте политику [set-header](api-management-transformation-policies.md#SetHTTPheader).</span><span class="sxs-lookup"><span data-stu-id="d5b26-222">To change header values, use the [set-header](api-management-transformation-policies.md#SetHTTPheader) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d5b26-223">Правило политики</span><span class="sxs-lookup"><span data-stu-id="d5b26-223">Policy statement</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a><span data-ttu-id="d5b26-224">Пример</span><span class="sxs-lookup"><span data-stu-id="d5b26-224">Example</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a><span data-ttu-id="d5b26-225">Элементы</span><span class="sxs-lookup"><span data-stu-id="d5b26-225">Elements</span></span>  
  
|<span data-ttu-id="d5b26-226">Имя</span><span class="sxs-lookup"><span data-stu-id="d5b26-226">Name</span></span>|<span data-ttu-id="d5b26-227">Описание</span><span class="sxs-lookup"><span data-stu-id="d5b26-227">Description</span></span>|<span data-ttu-id="d5b26-228">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5b26-228">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d5b26-229">redirect-content-urls</span><span class="sxs-lookup"><span data-stu-id="d5b26-229">redirect-content-urls</span></span>|<span data-ttu-id="d5b26-230">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="d5b26-230">Root element.</span></span>|<span data-ttu-id="d5b26-231">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-231">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d5b26-232">Использование</span><span class="sxs-lookup"><span data-stu-id="d5b26-232">Usage</span></span>  
 <span data-ttu-id="d5b26-233">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d5b26-233">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d5b26-234">**Разделы политики:** inbound, outbound.</span><span class="sxs-lookup"><span data-stu-id="d5b26-234">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="d5b26-235">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="d5b26-235">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d5b26-236"><a name="SetBackendService"></a> Задание внутренней службы</span><span class="sxs-lookup"><span data-stu-id="d5b26-236"><a name="SetBackendService"></a> Set backend service</span></span>  
 <span data-ttu-id="d5b26-237">Используйте политику `set-backend-service` для перенаправления входящего запроса во внутреннюю службу, отличную от указанной в параметрах API для этой операции.</span><span class="sxs-lookup"><span data-stu-id="d5b26-237">Use the `set-backend-service` policy to redirect an incoming request to a different backend than the one specified in the API settings for that operation.</span></span> <span data-ttu-id="d5b26-238">Эта политика изменяет базовый URL-адрес внутренней службы входящего запроса на URL-адрес, указанный в политике.</span><span class="sxs-lookup"><span data-stu-id="d5b26-238">This policy changes the backend service base URL of the incoming request to the one specified in the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d5b26-239">Правило политики</span><span class="sxs-lookup"><span data-stu-id="d5b26-239">Policy statement</span></span>  
  
```xml  
<set-backend-service base-url="base URL of the backend service" />  
```  
  
### <a name="example"></a><span data-ttu-id="d5b26-240">Пример</span><span class="sxs-lookup"><span data-stu-id="d5b26-240">Example</span></span>  
  
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
<span data-ttu-id="d5b26-241">В этом примере политика задания внутренней службы направляет запросы на основе значения версии, переданного в строке запроса во внутреннюю службу, отличную от указанной в API.</span><span class="sxs-lookup"><span data-stu-id="d5b26-241">In this example the set backend service policy routes requests based on the version value passed in the query string to a different backend service than the one specified in the API.</span></span>
  
<span data-ttu-id="d5b26-242">Изначально базовый URL-адрес внутренней службы является производным от параметров API.</span><span class="sxs-lookup"><span data-stu-id="d5b26-242">Initially the backend service base URL is derived from the API settings.</span></span> <span data-ttu-id="d5b26-243">Поэтому URL-адрес запроса `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` становится `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef`, где `http://contoso.com/api/10.4/` — URL-адрес внутренней службы, указанной в параметрах API.</span><span class="sxs-lookup"><span data-stu-id="d5b26-243">So the request URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` becomes `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` where `http://contoso.com/api/10.4/` is the backend service URL specified in the API settings.</span></span>  
  
<span data-ttu-id="d5b26-244">Когда применяется правило политики [<choose\>](api-management-advanced-policies.md#choose), базовый URL-адрес внутренней службы может снова измениться на `http://contoso.com/api/8.2` или `http://contoso.com/api/9.1` в зависимости от значения параметра запроса версии.</span><span class="sxs-lookup"><span data-stu-id="d5b26-244">When the [<choose\>](api-management-advanced-policies.md#choose) policy statement is applied the backend service base URL may change again either to `http://contoso.com/api/8.2` or `http://contoso.com/api/9.1`, depending on the value of the version request query parameter.</span></span> <span data-ttu-id="d5b26-245">Например, если значение — `"2013-15"`, URL-адрес последнего запроса становится `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span><span class="sxs-lookup"><span data-stu-id="d5b26-245">For example, if the value is `"2013-15"` the final request URL becomes `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span></span>  
  
<span data-ttu-id="d5b26-246">Если требуются дополнительные преобразования запроса, можно воспользоваться другими [политиками преобразования](api-management-transformation-policies.md#TransformationPolicies).</span><span class="sxs-lookup"><span data-stu-id="d5b26-246">If further transformation of the request is desired, other [Transformation policies](api-management-transformation-policies.md#TransformationPolicies) can be used.</span></span> <span data-ttu-id="d5b26-247">Например, чтобы удалить параметр запроса версии после направления запроса в конкретную серверную часть версии, для удаления атрибута избыточной версии можно использовать политику [Настройка параметра строки запроса](api-management-transformation-policies.md#SetQueryStringParameter).</span><span class="sxs-lookup"><span data-stu-id="d5b26-247">For example, to remove the version query parameter now that the request is being routed to a version specific backend, the  [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policy can be used to remove the now redundant version attribute.</span></span>  
  
### <a name="example"></a><span data-ttu-id="d5b26-248">Пример</span><span class="sxs-lookup"><span data-stu-id="d5b26-248">Example</span></span>  
  
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
<span data-ttu-id="d5b26-249">В этом примере политика направляет запрос к внутренней службе Service Fabric, используя строку запроса userId в качестве ключа секции и используя первичную реплику секции.</span><span class="sxs-lookup"><span data-stu-id="d5b26-249">In this example the policy routes the request to a service fabric backend, using the userId query string as the partition key and using the primary replica of the partition.</span></span>  

### <a name="elements"></a><span data-ttu-id="d5b26-250">Элементы</span><span class="sxs-lookup"><span data-stu-id="d5b26-250">Elements</span></span>  
  
|<span data-ttu-id="d5b26-251">Имя</span><span class="sxs-lookup"><span data-stu-id="d5b26-251">Name</span></span>|<span data-ttu-id="d5b26-252">Описание</span><span class="sxs-lookup"><span data-stu-id="d5b26-252">Description</span></span>|<span data-ttu-id="d5b26-253">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5b26-253">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d5b26-254">set-backend-service</span><span class="sxs-lookup"><span data-stu-id="d5b26-254">set-backend-service</span></span>|<span data-ttu-id="d5b26-255">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="d5b26-255">Root element.</span></span>|<span data-ttu-id="d5b26-256">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-256">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d5b26-257">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="d5b26-257">Attributes</span></span>  
  
|<span data-ttu-id="d5b26-258">Имя</span><span class="sxs-lookup"><span data-stu-id="d5b26-258">Name</span></span>|<span data-ttu-id="d5b26-259">Описание</span><span class="sxs-lookup"><span data-stu-id="d5b26-259">Description</span></span>|<span data-ttu-id="d5b26-260">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5b26-260">Required</span></span>|<span data-ttu-id="d5b26-261">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d5b26-261">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d5b26-262">base-url</span><span class="sxs-lookup"><span data-stu-id="d5b26-262">base-url</span></span>|<span data-ttu-id="d5b26-263">Новый базовый URL-адрес внутренней службы.</span><span class="sxs-lookup"><span data-stu-id="d5b26-263">New backend service base URL.</span></span>|<span data-ttu-id="d5b26-264">Нет</span><span class="sxs-lookup"><span data-stu-id="d5b26-264">No</span></span>|<span data-ttu-id="d5b26-265">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d5b26-265">N/A</span></span>|  
|<span data-ttu-id="d5b26-266">backend-id</span><span class="sxs-lookup"><span data-stu-id="d5b26-266">backend-id</span></span>|<span data-ttu-id="d5b26-267">Идентификатор серверной части для перенаправления.</span><span class="sxs-lookup"><span data-stu-id="d5b26-267">Identifier of the backend to route to.</span></span>|<span data-ttu-id="d5b26-268">Нет</span><span class="sxs-lookup"><span data-stu-id="d5b26-268">No</span></span>|<span data-ttu-id="d5b26-269">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d5b26-269">N/A</span></span>|  
|<span data-ttu-id="d5b26-270">sf-partition-key</span><span class="sxs-lookup"><span data-stu-id="d5b26-270">sf-partition-key</span></span>|<span data-ttu-id="d5b26-271">Применяется только, когда серверной частью является служба Service Fabric и она задана с помощью атрибута backend-id.</span><span class="sxs-lookup"><span data-stu-id="d5b26-271">Only applicable when the backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="d5b26-272">Используется для разрешения определенной секции в имени службы разрешения имен.</span><span class="sxs-lookup"><span data-stu-id="d5b26-272">Used to resolve a specific partition from the name resolution service.</span></span>|<span data-ttu-id="d5b26-273">Нет</span><span class="sxs-lookup"><span data-stu-id="d5b26-273">No</span></span>|<span data-ttu-id="d5b26-274">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d5b26-274">N/A</span></span>|  
|<span data-ttu-id="d5b26-275">sf-replica-type</span><span class="sxs-lookup"><span data-stu-id="d5b26-275">sf-replica-type</span></span>|<span data-ttu-id="d5b26-276">Применяется только, когда серверной частью является служба Service Fabric и она задана с помощью атрибута backend-id.</span><span class="sxs-lookup"><span data-stu-id="d5b26-276">Only applicable when the backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="d5b26-277">Контролирует, куда должен отправляться запрос: в первичную или вторичную реплику секции.</span><span class="sxs-lookup"><span data-stu-id="d5b26-277">Controls if the request should go to the primary or secondary replica of a partition.</span></span> |<span data-ttu-id="d5b26-278">Нет</span><span class="sxs-lookup"><span data-stu-id="d5b26-278">No</span></span>|<span data-ttu-id="d5b26-279">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d5b26-279">N/A</span></span>|    
|<span data-ttu-id="d5b26-280">sf-resolve-condition</span><span class="sxs-lookup"><span data-stu-id="d5b26-280">sf-resolve-condition</span></span>|<span data-ttu-id="d5b26-281">Применяется только, когда серверной частью является служба Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d5b26-281">Only applicable when the backend is a Service Fabric service.</span></span> <span data-ttu-id="d5b26-282">Условие, определяющее, необходимо ли повторить вызов к серверной части Service Fabric с новым разрешением.</span><span class="sxs-lookup"><span data-stu-id="d5b26-282">Condition identifying if the call to Service Fabric backend has to be repeated with new resolution.</span></span>|<span data-ttu-id="d5b26-283">Нет</span><span class="sxs-lookup"><span data-stu-id="d5b26-283">No</span></span>|<span data-ttu-id="d5b26-284">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d5b26-284">N/A</span></span>|    
|<span data-ttu-id="d5b26-285">sf-service-instance-name</span><span class="sxs-lookup"><span data-stu-id="d5b26-285">sf-service-instance-name</span></span>|<span data-ttu-id="d5b26-286">Применяется только, когда серверной частью является служба Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d5b26-286">Only applicable when the backend is a Service Fabric service.</span></span> <span data-ttu-id="d5b26-287">Разрешает изменение экземпляров службы в среде выполнения.</span><span class="sxs-lookup"><span data-stu-id="d5b26-287">Allows to change service instances at runtime.</span></span> |<span data-ttu-id="d5b26-288">Нет</span><span class="sxs-lookup"><span data-stu-id="d5b26-288">No</span></span>|<span data-ttu-id="d5b26-289">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d5b26-289">N/A</span></span>|    

### <a name="usage"></a><span data-ttu-id="d5b26-290">Использование</span><span class="sxs-lookup"><span data-stu-id="d5b26-290">Usage</span></span>  
 <span data-ttu-id="d5b26-291">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d5b26-291">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d5b26-292">**Разделы политики:** inbound, backend.</span><span class="sxs-lookup"><span data-stu-id="d5b26-292">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="d5b26-293">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="d5b26-293">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d5b26-294"><a name="SetBody"></a> Задание текста</span><span class="sxs-lookup"><span data-stu-id="d5b26-294"><a name="SetBody"></a> Set body</span></span>  
 <span data-ttu-id="d5b26-295">Используйте политику `set-body`, чтобы задать текст сообщения для входящих и исходящих запросов.</span><span class="sxs-lookup"><span data-stu-id="d5b26-295">Use the `set-body` policy to set the message body for incoming and outgoing requests.</span></span> <span data-ttu-id="d5b26-296">Для доступа к тексту сообщения можно использовать свойство `context.Request.Body` или `context.Response.Body` в зависимости от того, где находится политика: в разделе inbound или outbound.</span><span class="sxs-lookup"><span data-stu-id="d5b26-296">To access the message body you can use the `context.Request.Body` property or the `context.Response.Body`, depending on whether the policy is in the inbound or outbound section.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="d5b26-297">Обратите внимание, что по умолчанию при доступе к тексту сообщения с помощью `context.Request.Body` или `context.Response.Body` исходный текст сообщения теряется и его необходимо задать, возвратив текст обратно в выражение.</span><span class="sxs-lookup"><span data-stu-id="d5b26-297">Note that by default when you access the message body using `context.Request.Body` or `context.Response.Body`, the original message body is lost and must be set by returning the body back in the expression.</span></span> <span data-ttu-id="d5b26-298">Чтобы сохранить содержимое текста, при доступе к сообщению присвойте параметру `preserveContent` значение `true`.</span><span class="sxs-lookup"><span data-stu-id="d5b26-298">To preserve the body content, set the `preserveContent` parameter to `true` when accessing the message.</span></span> <span data-ttu-id="d5b26-299">Если для параметра `preserveContent` задано значение `true` и в выражении возвращается другой текст, используется возвращаемый текст.</span><span class="sxs-lookup"><span data-stu-id="d5b26-299">If `preserveContent` is set to `true` and a different body is returned by the expression, the returned body is used.</span></span>  
>   
>  <span data-ttu-id="d5b26-300">Учтите следующие рекомендации при использовании политики `set-body`.</span><span class="sxs-lookup"><span data-stu-id="d5b26-300">Please note the following considerations when using the `set-body` policy.</span></span>  
>   
>  -   <span data-ttu-id="d5b26-301">Если для возврата нового или обновленного текста используется политика `set-body`, для параметра `preserveContent` не требуется задавать значение `true`, так как вы явно указываете новое содержимое текста.</span><span class="sxs-lookup"><span data-stu-id="d5b26-301">If you are using the `set-body` policy to return a new or updated body you don't need to set `preserveContent` to `true` because you are explicitly supplying the new body contents.</span></span>  
> -   <span data-ttu-id="d5b26-302">Сохранять содержимое ответа во входящем конвейере не имеет смысла, так как ответа еще нет.</span><span class="sxs-lookup"><span data-stu-id="d5b26-302">Preserving the content of a response in the inbound pipeline doesn't make sense because there is no response yet.</span></span>  
> -   <span data-ttu-id="d5b26-303">Сохранять содержимое запроса в исходящем конвейере не имеет смысла, так как на этом этапе запрос уже был отправлен в серверную часть.</span><span class="sxs-lookup"><span data-stu-id="d5b26-303">Preserving the content of a request in the outbound pipeline doesn't make sense because the request has already been sent to the backend at this point.</span></span>  
> -   <span data-ttu-id="d5b26-304">Если эта политика используется при отсутствии текста сообщения, например во входящем параметре GET, возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="d5b26-304">If this policy is used when there is no message body, for example in an inbound GET, an exception is thrown.</span></span>  
  
 <span data-ttu-id="d5b26-305">Дополнительные сведения см. в разделах `context.Request.Body`, `context.Response.Body` и `IMessage` в таблице [Переменная контекста](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="d5b26-305">For more information, see the `context.Request.Body`, `context.Response.Body`, and the `IMessage` sections in the [Context variable](api-management-policy-expressions.md#ContextVariables) table.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d5b26-306">Правило политики</span><span class="sxs-lookup"><span data-stu-id="d5b26-306">Policy statement</span></span>  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a><span data-ttu-id="d5b26-307">Примеры</span><span class="sxs-lookup"><span data-stu-id="d5b26-307">Examples</span></span>  
  
#### <a name="literal-text-example"></a><span data-ttu-id="d5b26-308">Пример литерального текста</span><span class="sxs-lookup"><span data-stu-id="d5b26-308">Literal text example</span></span>  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-the-body-as-a-string-note-that-we-are-preserving-the-original-request-body-so-that-we-can-access-it-later-in-the-pipeline"></a><span data-ttu-id="d5b26-309">Пример доступа к тексту как к строке</span><span class="sxs-lookup"><span data-stu-id="d5b26-309">Example accessing the body as a string.</span></span> <span data-ttu-id="d5b26-310">Обратите внимание, что мы сохраняем исходный текст запроса, чтобы позже можно было обратиться к нему в конвейере.</span><span class="sxs-lookup"><span data-stu-id="d5b26-310">Note that we are preserving the original request body so that we can access it later in the pipeline.</span></span>
  
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
  
#### <a name="example-accessing-the-body-as-a-jobject-note-that-since-we-are-not-reserving-the-original-request-body-accesing-it-later-in-the-pipeline-will-result-in-an-exception"></a><span data-ttu-id="d5b26-311">Пример доступа к тексту как к объекту JObject</span><span class="sxs-lookup"><span data-stu-id="d5b26-311">Example accessing the body as a JObject.</span></span> <span data-ttu-id="d5b26-312">Обратите внимание, что мы не резервировали исходный текст запроса, поэтому попытка получить к нему доступ позже в конвейере приведет к возникновению исключения.</span><span class="sxs-lookup"><span data-stu-id="d5b26-312">Note that since we are not reserving the original request body, accesing it later in the pipeline will result in an exception.</span></span>  
  
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
  
#### <a name="filter-response-based-on-product"></a><span data-ttu-id="d5b26-313">Фильтрация ответа в зависимости от продукта</span><span class="sxs-lookup"><span data-stu-id="d5b26-313">Filter response based on product</span></span>  
 <span data-ttu-id="d5b26-314">В этом примере показано, как выполнить фильтрацию содержимого путем удаления элементов данных из ответа, полученного из внутренней службы при использовании продукта `Starter`.</span><span class="sxs-lookup"><span data-stu-id="d5b26-314">This example shows how to perform content filtering by removing data elements from the response received from the backend service when using the `Starter` product.</span></span> <span data-ttu-id="d5b26-315">Пример настройки и использования этой политики см. в видео [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Cloud Cover, эпизод 177: возможности управления API с Владом Виноградским) с отметки времени 34:30.</span><span class="sxs-lookup"><span data-stu-id="d5b26-315">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 34:30.</span></span> <span data-ttu-id="d5b26-316">Начните с отметки времени 31:50, чтобы узнать общие сведения о [прогнозном API Dark Sky](https://developer.forecast.io/), используемом для этого примера.</span><span class="sxs-lookup"><span data-stu-id="d5b26-316">Start  at 31:50 to see an overview of [The Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
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

### <a name="using-liquid-templates-with-set-body"></a><span data-ttu-id="d5b26-317">Использование шаблонов Liquid с политикой set-body</span><span class="sxs-lookup"><span data-stu-id="d5b26-317">Using Liquid templates with set body</span></span> 
<span data-ttu-id="d5b26-318">В политике `set-body` можно настроить использование языка шаблонов [Liquid](https://shopify.github.io/liquid/basics/introduction/) для преобразования текста запроса или ответа.</span><span class="sxs-lookup"><span data-stu-id="d5b26-318">The `set-body` policy can be configured to use the [Liquid](https://shopify.github.io/liquid/basics/introduction/) templating language to transfom the body of a request or response.</span></span> <span data-ttu-id="d5b26-319">Это может быть очень эффективным, когда требуется полностью изменить формат сообщения.</span><span class="sxs-lookup"><span data-stu-id="d5b26-319">This can be very effective if you need to completely reshape the format of your message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d5b26-320">Реализация шаблонов Liquid, используемая в политике `set-body`, настраивается в режиме C#.</span><span class="sxs-lookup"><span data-stu-id="d5b26-320">The implementation of Liquid used in the `set-body` policy is configured in 'C# mode'.</span></span> <span data-ttu-id="d5b26-321">Это особенно важно при выполнении действий, таких как фильтрация.</span><span class="sxs-lookup"><span data-stu-id="d5b26-321">This is particularly important when doing things such as filtering.</span></span> <span data-ttu-id="d5b26-322">Например, если применяется фильтр по дате, то необходимо использовать стиль Pascal и форматирование даты C#, как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="d5b26-322">As an example, using a date filter requires the use of Pascal casing and C# date formatting e.g.:</span></span>
>
> <span data-ttu-id="d5b26-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span><span class="sxs-lookup"><span data-stu-id="d5b26-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d5b26-324">Чтобы с помощью шаблона Liquid правильно выполнить привязку к тексту XML, используйте политику `set-header`. Задайте для Content-Type значение application/xml или text/xml (или любой другой тип, заканчивающийся на +xml). Для текста JSON значение должно быть application/json или text/json (или любой другой тип, заканчивающийся на +json).</span><span class="sxs-lookup"><span data-stu-id="d5b26-324">In order to correctly bind to an XML body using the Liquid template, use a `set-header` policy to set Content-Type to either application/xml, text/xml (or any type ending with +xml); for a JSON body, it must be application/json, text/json (or any type ending with +json).</span></span>

#### <a name="convert-json-to-soap-using-a-liquid-template"></a><span data-ttu-id="d5b26-325">Преобразование JSON в SOAP с помощью шаблона Liquid</span><span class="sxs-lookup"><span data-stu-id="d5b26-325">Convert JSON to SOAP using a Liquid template</span></span>
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

#### <a name="tranform-json-using-a-liquid-template"></a><span data-ttu-id="d5b26-326">Преобразование JSON с помощью шаблона Liquid</span><span class="sxs-lookup"><span data-stu-id="d5b26-326">Tranform JSON using a Liquid template</span></span>
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a><span data-ttu-id="d5b26-327">Элементы</span><span class="sxs-lookup"><span data-stu-id="d5b26-327">Elements</span></span>  
  
|<span data-ttu-id="d5b26-328">Имя</span><span class="sxs-lookup"><span data-stu-id="d5b26-328">Name</span></span>|<span data-ttu-id="d5b26-329">Описание</span><span class="sxs-lookup"><span data-stu-id="d5b26-329">Description</span></span>|<span data-ttu-id="d5b26-330">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5b26-330">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d5b26-331">set-body</span><span class="sxs-lookup"><span data-stu-id="d5b26-331">set-body</span></span>|<span data-ttu-id="d5b26-332">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="d5b26-332">Root element.</span></span> <span data-ttu-id="d5b26-333">Содержит текст или выражения, которые возвращают текст.</span><span class="sxs-lookup"><span data-stu-id="d5b26-333">Contains the body text or an expressions that returns a body.</span></span>|<span data-ttu-id="d5b26-334">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-334">Yes</span></span>|  

### <a name="properties"></a><span data-ttu-id="d5b26-335">Свойства</span><span class="sxs-lookup"><span data-stu-id="d5b26-335">Properties</span></span>  
  
|<span data-ttu-id="d5b26-336">Имя</span><span class="sxs-lookup"><span data-stu-id="d5b26-336">Name</span></span>|<span data-ttu-id="d5b26-337">Описание</span><span class="sxs-lookup"><span data-stu-id="d5b26-337">Description</span></span>|<span data-ttu-id="d5b26-338">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5b26-338">Required</span></span>|<span data-ttu-id="d5b26-339">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d5b26-339">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d5b26-340">шаблон</span><span class="sxs-lookup"><span data-stu-id="d5b26-340">template</span></span>|<span data-ttu-id="d5b26-341">Используется для изменения режима шаблона, в котором будет выполняться политика set-body.</span><span class="sxs-lookup"><span data-stu-id="d5b26-341">Used to change the templating mode that the set body policy will run in.</span></span> <span data-ttu-id="d5b26-342">В настоящее время поддерживается только одно значение:</span><span class="sxs-lookup"><span data-stu-id="d5b26-342">Currently the only supported value is:</span></span><br /><br /><span data-ttu-id="d5b26-343">- liquid — политика set-body будет использовать подсистему шаблонов Liquid.</span><span class="sxs-lookup"><span data-stu-id="d5b26-343">- liquid - the set body policy will use the liquid templating engine</span></span> |<span data-ttu-id="d5b26-344">Нет</span><span class="sxs-lookup"><span data-stu-id="d5b26-344">No</span></span>|<span data-ttu-id="d5b26-345">liquid</span><span class="sxs-lookup"><span data-stu-id="d5b26-345">liquid</span></span>|  

<span data-ttu-id="d5b26-346">Для доступа к сведениям о запросе и ответе шаблон Liquid можно привязать к объекту context с помощью следующих свойств:</span><span class="sxs-lookup"><span data-stu-id="d5b26-346">For accessing information about the request and response, the Liquid template can bind to a context object with the following properties:</span></span> <br />
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



### <a name="usage"></a><span data-ttu-id="d5b26-347">Использование</span><span class="sxs-lookup"><span data-stu-id="d5b26-347">Usage</span></span>  
 <span data-ttu-id="d5b26-348">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d5b26-348">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d5b26-349">**Разделы политики:** inbound, outbound, backend.</span><span class="sxs-lookup"><span data-stu-id="d5b26-349">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="d5b26-350">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="d5b26-350">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d5b26-351"><a name="SetHTTPheader"></a> Установка HTTP-заголовка</span><span class="sxs-lookup"><span data-stu-id="d5b26-351"><a name="SetHTTPheader"></a> Set HTTP header</span></span>  
 <span data-ttu-id="d5b26-352">Политика `set-header` назначает значение имеющемуся заголовку ответа и/или запроса или добавляет новый заголовок ответа и/или запроса.</span><span class="sxs-lookup"><span data-stu-id="d5b26-352">The `set-header` policy assigns a value to an existing response and/or request header or adds a new response and/or request header.</span></span>  
  
 <span data-ttu-id="d5b26-353">Вставляет список HTTP-заголовков в HTTP-сообщение.</span><span class="sxs-lookup"><span data-stu-id="d5b26-353">Inserts a list of HTTP headers into an HTTP message.</span></span> <span data-ttu-id="d5b26-354">Если эта политика находится во входящем конвейере, она устанавливает HTTP-заголовки для запроса, передаваемого в целевую службу.</span><span class="sxs-lookup"><span data-stu-id="d5b26-354">When placed in an inbound pipeline, this policy sets the HTTP headers for the request being passed to the target service.</span></span> <span data-ttu-id="d5b26-355">Если эта политика находится в исходящем конвейере, она устанавливает HTTP-заголовки для ответа, отправляемого клиенту шлюза.</span><span class="sxs-lookup"><span data-stu-id="d5b26-355">When placed in an outbound pipeline, this policy sets the HTTP headers for the response being sent to the gateway’s client.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d5b26-356">Правило политики</span><span class="sxs-lookup"><span data-stu-id="d5b26-356">Policy statement</span></span>  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with the same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a><span data-ttu-id="d5b26-357">Примеры</span><span class="sxs-lookup"><span data-stu-id="d5b26-357">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="d5b26-358">Пример</span><span class="sxs-lookup"><span data-stu-id="d5b26-358">Example</span></span>  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-to-the-backend-service"></a><span data-ttu-id="d5b26-359">Пересылка контекстных сведений во внутреннюю службу</span><span class="sxs-lookup"><span data-stu-id="d5b26-359">Forward context information to the backend service</span></span>  
 <span data-ttu-id="d5b26-360">В этом примере показано, как применить политику на уровне API для предоставления контекстных сведений внутренней службе.</span><span class="sxs-lookup"><span data-stu-id="d5b26-360">This example shows how to apply policy at the API level to supply context information to the backend service.</span></span> <span data-ttu-id="d5b26-361">Пример настройки и использования этой политики см. в видео [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Cloud Cover, эпизод 177: возможности управления API с Владом Виноградским) с отметки времени 10:30.</span><span class="sxs-lookup"><span data-stu-id="d5b26-361">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30.</span></span> <span data-ttu-id="d5b26-362">На отметке времени 12:10 демонстрируется вызов операции на портале разработчика, где можно просмотреть политику в действии.</span><span class="sxs-lookup"><span data-stu-id="d5b26-362">At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into the inbound element to forward some context information, user id and the region the gateway is hosted in, to the backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 <span data-ttu-id="d5b26-363">Чтобы узнать больше, см. статью [API Management policy expressions](api-management-policy-expressions.md) (Выражения политики управления API) и раздел [Context variable](api-management-policy-expressions.md#ContextVariables) (Переменная контекста).</span><span class="sxs-lookup"><span data-stu-id="d5b26-363">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="d5b26-364">Элементы</span><span class="sxs-lookup"><span data-stu-id="d5b26-364">Elements</span></span>  
  
|<span data-ttu-id="d5b26-365">Имя</span><span class="sxs-lookup"><span data-stu-id="d5b26-365">Name</span></span>|<span data-ttu-id="d5b26-366">Описание</span><span class="sxs-lookup"><span data-stu-id="d5b26-366">Description</span></span>|<span data-ttu-id="d5b26-367">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5b26-367">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d5b26-368">set-header</span><span class="sxs-lookup"><span data-stu-id="d5b26-368">set-header</span></span>|<span data-ttu-id="d5b26-369">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="d5b26-369">Root element.</span></span>|<span data-ttu-id="d5b26-370">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-370">Yes</span></span>|  
|<span data-ttu-id="d5b26-371">значение</span><span class="sxs-lookup"><span data-stu-id="d5b26-371">value</span></span>|<span data-ttu-id="d5b26-372">Указывает значение заголовка, которое должно быть установлено.</span><span class="sxs-lookup"><span data-stu-id="d5b26-372">Specifies the value of the header to be set.</span></span> <span data-ttu-id="d5b26-373">Для нескольких заголовков с одним и тем же именем добавьте дополнительные элементы `value`.</span><span class="sxs-lookup"><span data-stu-id="d5b26-373">For multiple headers with the same name add additional `value` elements.</span></span>|<span data-ttu-id="d5b26-374">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-374">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="d5b26-375">Свойства</span><span class="sxs-lookup"><span data-stu-id="d5b26-375">Properties</span></span>  
  
|<span data-ttu-id="d5b26-376">Имя</span><span class="sxs-lookup"><span data-stu-id="d5b26-376">Name</span></span>|<span data-ttu-id="d5b26-377">Описание</span><span class="sxs-lookup"><span data-stu-id="d5b26-377">Description</span></span>|<span data-ttu-id="d5b26-378">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5b26-378">Required</span></span>|<span data-ttu-id="d5b26-379">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d5b26-379">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d5b26-380">exists-action</span><span class="sxs-lookup"><span data-stu-id="d5b26-380">exists-action</span></span>|<span data-ttu-id="d5b26-381">Указывает действие, которое должно быть выполнено, когда заголовок уже задан.</span><span class="sxs-lookup"><span data-stu-id="d5b26-381">Specifies what action to take when the header is already specified.</span></span> <span data-ttu-id="d5b26-382">Атрибут должен иметь одно из следующих значений:</span><span class="sxs-lookup"><span data-stu-id="d5b26-382">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="d5b26-383">override — заменяет значение имеющегося заголовка;</span><span class="sxs-lookup"><span data-stu-id="d5b26-383">-   override - replaces the value of the existing header.</span></span><br /><span data-ttu-id="d5b26-384">skip — не заменяет значение имеющегося заголовка;</span><span class="sxs-lookup"><span data-stu-id="d5b26-384">-   skip - does not replace the existing header value.</span></span><br /><span data-ttu-id="d5b26-385">append — добавляет значение к значению имеющегося заголовка;</span><span class="sxs-lookup"><span data-stu-id="d5b26-385">-   append - appends the value to the existing header value.</span></span><br /><span data-ttu-id="d5b26-386">delete — удаляет заголовок из запроса.</span><span class="sxs-lookup"><span data-stu-id="d5b26-386">-   delete - removes the header from the request.</span></span><br /><br /> <span data-ttu-id="d5b26-387">Если установлено значение `override`, перечисление нескольких записей с одним и тем же именем будет приводить к тому, что заголовок будет устанавливаться в соответствии со всеми записями (будут перечисляться несколько раз). В результате будут установлены только перечисленные значения.</span><span class="sxs-lookup"><span data-stu-id="d5b26-387">When set to `override` enlisting multiple entries with the same name results in the header being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="d5b26-388">Нет</span><span class="sxs-lookup"><span data-stu-id="d5b26-388">No</span></span>|<span data-ttu-id="d5b26-389">override</span><span class="sxs-lookup"><span data-stu-id="d5b26-389">override</span></span>|  
|<span data-ttu-id="d5b26-390">name</span><span class="sxs-lookup"><span data-stu-id="d5b26-390">name</span></span>|<span data-ttu-id="d5b26-391">Указывает имя заголовка, которое должно быть установлено.</span><span class="sxs-lookup"><span data-stu-id="d5b26-391">Specifies name of the header to be set.</span></span>|<span data-ttu-id="d5b26-392">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-392">Yes</span></span>|<span data-ttu-id="d5b26-393">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d5b26-393">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d5b26-394">Использование</span><span class="sxs-lookup"><span data-stu-id="d5b26-394">Usage</span></span>  
 <span data-ttu-id="d5b26-395">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d5b26-395">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d5b26-396">**Разделы политики:** inbound, outbound, backend, on-error.</span><span class="sxs-lookup"><span data-stu-id="d5b26-396">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="d5b26-397">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="d5b26-397">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d5b26-398"><a name="SetQueryStringParameter"></a> Настройка параметра строки запроса</span><span class="sxs-lookup"><span data-stu-id="d5b26-398"><a name="SetQueryStringParameter"></a> Set query string parameter</span></span>  
 <span data-ttu-id="d5b26-399">Политика `set-query-parameter` добавляет, заменяет значение или удаляет параметр строки запроса.</span><span class="sxs-lookup"><span data-stu-id="d5b26-399">The `set-query-parameter` policy adds, replaces value of, or deletes request query string parameter.</span></span> <span data-ttu-id="d5b26-400">Можно использовать для передачи параметров запроса, ожидаемых внутренней службой, которые являются необязательными или никогда не присутствуют в запросе.</span><span class="sxs-lookup"><span data-stu-id="d5b26-400">Can be used to pass query parameters expected by the backend service which are optional or never present in the request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d5b26-401">Правило политики</span><span class="sxs-lookup"><span data-stu-id="d5b26-401">Policy statement</span></span>  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with the same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a><span data-ttu-id="d5b26-402">Примеры</span><span class="sxs-lookup"><span data-stu-id="d5b26-402">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="d5b26-403">Пример</span><span class="sxs-lookup"><span data-stu-id="d5b26-403">Example</span></span>  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with the same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-to-the-backend-service"></a><span data-ttu-id="d5b26-404">Пересылка контекстных сведений во внутреннюю службу</span><span class="sxs-lookup"><span data-stu-id="d5b26-404">Forward context information to the backend service</span></span>  
 <span data-ttu-id="d5b26-405">В этом примере показано, как применить политику на уровне API для предоставления контекстных сведений внутренней службе.</span><span class="sxs-lookup"><span data-stu-id="d5b26-405">This example shows how to apply policy at the API level to supply context information to the backend service.</span></span> <span data-ttu-id="d5b26-406">Пример настройки и использования этой политики см. в видео [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Cloud Cover, эпизод 177: возможности управления API с Владом Виноградским) с отметки времени 10:30.</span><span class="sxs-lookup"><span data-stu-id="d5b26-406">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 10:30.</span></span> <span data-ttu-id="d5b26-407">На отметке времени 12:10 демонстрируется вызов операции на портале разработчика, где можно просмотреть политику в действии.</span><span class="sxs-lookup"><span data-stu-id="d5b26-407">At 12:10 there is a demo of calling an operation in the developer portal where you can see the policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into the inbound element to forward a piece of context, product name in this example, to the backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 <span data-ttu-id="d5b26-408">Чтобы узнать больше, см. статью [API Management policy expressions](api-management-policy-expressions.md) (Выражения политики управления API) и раздел [Context variable](api-management-policy-expressions.md#ContextVariables) (Переменная контекста).</span><span class="sxs-lookup"><span data-stu-id="d5b26-408">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="d5b26-409">Элементы</span><span class="sxs-lookup"><span data-stu-id="d5b26-409">Elements</span></span>  
  
|<span data-ttu-id="d5b26-410">Имя</span><span class="sxs-lookup"><span data-stu-id="d5b26-410">Name</span></span>|<span data-ttu-id="d5b26-411">Описание</span><span class="sxs-lookup"><span data-stu-id="d5b26-411">Description</span></span>|<span data-ttu-id="d5b26-412">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5b26-412">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d5b26-413">set-query-parameter</span><span class="sxs-lookup"><span data-stu-id="d5b26-413">set-query-parameter</span></span>|<span data-ttu-id="d5b26-414">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="d5b26-414">Root element.</span></span>|<span data-ttu-id="d5b26-415">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-415">Yes</span></span>|  
|<span data-ttu-id="d5b26-416">значение</span><span class="sxs-lookup"><span data-stu-id="d5b26-416">value</span></span>|<span data-ttu-id="d5b26-417">Указывает значение параметра запроса, которое должно быть установлено.</span><span class="sxs-lookup"><span data-stu-id="d5b26-417">Specifies the value of the query parameter to be set.</span></span> <span data-ttu-id="d5b26-418">Для нескольких параметров запроса с одним и тем же именем добавьте дополнительные элементы `value`.</span><span class="sxs-lookup"><span data-stu-id="d5b26-418">For multiple query parameters with the same name add additional `value` elements.</span></span>|<span data-ttu-id="d5b26-419">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-419">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="d5b26-420">Свойства</span><span class="sxs-lookup"><span data-stu-id="d5b26-420">Properties</span></span>  
  
|<span data-ttu-id="d5b26-421">Имя</span><span class="sxs-lookup"><span data-stu-id="d5b26-421">Name</span></span>|<span data-ttu-id="d5b26-422">Описание</span><span class="sxs-lookup"><span data-stu-id="d5b26-422">Description</span></span>|<span data-ttu-id="d5b26-423">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5b26-423">Required</span></span>|<span data-ttu-id="d5b26-424">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d5b26-424">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d5b26-425">exists-action</span><span class="sxs-lookup"><span data-stu-id="d5b26-425">exists-action</span></span>|<span data-ttu-id="d5b26-426">Указывает действие, которое должно быть выполнено, когда параметр запроса уже задан.</span><span class="sxs-lookup"><span data-stu-id="d5b26-426">Specifies what action to take when the query parameter is already specified.</span></span> <span data-ttu-id="d5b26-427">Атрибут должен иметь одно из следующих значений:</span><span class="sxs-lookup"><span data-stu-id="d5b26-427">This attribute must have one of the following values.</span></span><br /><br /> <span data-ttu-id="d5b26-428">override — заменяет значение имеющегося параметра;</span><span class="sxs-lookup"><span data-stu-id="d5b26-428">-   override - replaces the value of the existing parameter.</span></span><br /><span data-ttu-id="d5b26-429">skip — не заменяет значение имеющегося параметра запроса;</span><span class="sxs-lookup"><span data-stu-id="d5b26-429">-   skip - does not replace the existing query parameter value.</span></span><br /><span data-ttu-id="d5b26-430">append — добавляет значение к значению имеющегося параметра запроса;</span><span class="sxs-lookup"><span data-stu-id="d5b26-430">-   append - appends the value to the existing query parameter value.</span></span><br /><span data-ttu-id="d5b26-431">delete — удаляет параметр запроса из запроса.</span><span class="sxs-lookup"><span data-stu-id="d5b26-431">-   delete - removes the query parameter from the request.</span></span><br /><br /> <span data-ttu-id="d5b26-432">Если установлено значение `override`, перечисление нескольких записей с одним и тем же именем будет приводить к тому, что параметр запроса будет устанавливаться в соответствии со всеми записями (будут перечисляться несколько раз). В результате будут установлены только перечисленные значения.</span><span class="sxs-lookup"><span data-stu-id="d5b26-432">When set to `override` enlisting multiple entries with the same name results in the query parameter being set according to all entries (which will be listed multiple times); only listed values will be set in the result.</span></span>|<span data-ttu-id="d5b26-433">Нет</span><span class="sxs-lookup"><span data-stu-id="d5b26-433">No</span></span>|<span data-ttu-id="d5b26-434">override</span><span class="sxs-lookup"><span data-stu-id="d5b26-434">override</span></span>|  
|<span data-ttu-id="d5b26-435">name</span><span class="sxs-lookup"><span data-stu-id="d5b26-435">name</span></span>|<span data-ttu-id="d5b26-436">Указывает имя параметра запроса, которое должно быть установлено.</span><span class="sxs-lookup"><span data-stu-id="d5b26-436">Specifies name of the query parameter to be set.</span></span>|<span data-ttu-id="d5b26-437">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-437">Yes</span></span>|<span data-ttu-id="d5b26-438">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d5b26-438">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d5b26-439">Использование</span><span class="sxs-lookup"><span data-stu-id="d5b26-439">Usage</span></span>  
 <span data-ttu-id="d5b26-440">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d5b26-440">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d5b26-441">**Разделы политики:** inbound, backend.</span><span class="sxs-lookup"><span data-stu-id="d5b26-441">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="d5b26-442">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="d5b26-442">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="d5b26-443"><a name="RewriteURL"></a> Перезапись URL-адреса</span><span class="sxs-lookup"><span data-stu-id="d5b26-443"><a name="RewriteURL"></a> Rewrite URL</span></span>  
 <span data-ttu-id="d5b26-444">Политика `rewrite-uri` преобразовывает URL-адрес запроса из его общедоступной формы в форму, ожидаемую веб-службой, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="d5b26-444">The `rewrite-uri` policy converts a request URL from its public form to the form expected by the web service, as shown in the following example.</span></span>  
  
-   <span data-ttu-id="d5b26-445">Открытый URL — `http://api.example.com/storenumber/ordernumber`.</span><span class="sxs-lookup"><span data-stu-id="d5b26-445">Public URL - `http://api.example.com/storenumber/ordernumber`</span></span>  
  
-   <span data-ttu-id="d5b26-446">URL-адрес запроса — `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`.</span><span class="sxs-lookup"><span data-stu-id="d5b26-446">Request URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span></span>  
  
 <span data-ttu-id="d5b26-447">Эту политику можно использовать, когда дружественный для пользователя и/или браузера URL-адрес должен быть преобразован в формат URL-адреса, ожидаемый веб-службой.</span><span class="sxs-lookup"><span data-stu-id="d5b26-447">This policy can be used when a human and/or browser-friendly URL should be transformed into the URL format expected by the web service.</span></span> <span data-ttu-id="d5b26-448">Эту политику необходимо применять только при указании URL-адресов в другом формате, например "чистых" URL-адресов, URL-адресов типа RESTful, дружественных для пользователя URL-адресов или дружественных для SEO URL-адресов, которые представляют собой чисто структурные URL-адреса, не содержащие строку запроса. Вместо этого они содержат только путь к ресурсу (после схемы и полномочий).</span><span class="sxs-lookup"><span data-stu-id="d5b26-448">This policy only needs to be applied when exposing an alternative URL format, such as clean URLs, RESTful URLs, user-friendly URLs or SEO-friendly URLs that are purely structural URLs that do not contain a query string and instead contain only the path of the resource (after the scheme and the authority).</span></span> <span data-ttu-id="d5b26-449">Это часто делает в эстетических целях, для удобства и простоты использования или для оптимизации поисковых систем (SEO).</span><span class="sxs-lookup"><span data-stu-id="d5b26-449">This is often done for aesthetic, usability, or search engine optimization (SEO) purposes.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="d5b26-450">Используя политику, можно добавлять только параметры строки запроса.</span><span class="sxs-lookup"><span data-stu-id="d5b26-450">You can only add query string parameters using the policy.</span></span> <span data-ttu-id="d5b26-451">Нельзя добавлять дополнительный параметр пути к шаблону в URL-адрес перезаписи.</span><span class="sxs-lookup"><span data-stu-id="d5b26-451">You cannot add extra template path parameters in the rewrite URL.</span></span>  

### <a name="policy-statement"></a><span data-ttu-id="d5b26-452">Правило политики</span><span class="sxs-lookup"><span data-stu-id="d5b26-452">Policy statement</span></span>  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a><span data-ttu-id="d5b26-453">Пример</span><span class="sxs-lookup"><span data-stu-id="d5b26-453">Example</span></span>  
  
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
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
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
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set to /get?a={b} -->
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

### <a name="elements"></a><span data-ttu-id="d5b26-454">Элементы</span><span class="sxs-lookup"><span data-stu-id="d5b26-454">Elements</span></span>  
  
|<span data-ttu-id="d5b26-455">Имя</span><span class="sxs-lookup"><span data-stu-id="d5b26-455">Name</span></span>|<span data-ttu-id="d5b26-456">Описание</span><span class="sxs-lookup"><span data-stu-id="d5b26-456">Description</span></span>|<span data-ttu-id="d5b26-457">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5b26-457">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d5b26-458">rewrite-uri</span><span class="sxs-lookup"><span data-stu-id="d5b26-458">rewrite-uri</span></span>|<span data-ttu-id="d5b26-459">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="d5b26-459">Root element.</span></span>|<span data-ttu-id="d5b26-460">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-460">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d5b26-461">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="d5b26-461">Attributes</span></span>  
  
|<span data-ttu-id="d5b26-462">Атрибут</span><span class="sxs-lookup"><span data-stu-id="d5b26-462">Attribute</span></span>|<span data-ttu-id="d5b26-463">Описание</span><span class="sxs-lookup"><span data-stu-id="d5b26-463">Description</span></span>|<span data-ttu-id="d5b26-464">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5b26-464">Required</span></span>|<span data-ttu-id="d5b26-465">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d5b26-465">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="d5b26-466">шаблон</span><span class="sxs-lookup"><span data-stu-id="d5b26-466">template</span></span>|<span data-ttu-id="d5b26-467">Фактический URL-адрес веб-службы с любыми параметрами строки запроса.</span><span class="sxs-lookup"><span data-stu-id="d5b26-467">The actual web service URL with any query string parameters.</span></span> <span data-ttu-id="d5b26-468">При использовании выражений все значение должно быть выражением.</span><span class="sxs-lookup"><span data-stu-id="d5b26-468">When using expressions, the whole value must be an expression.</span></span>|<span data-ttu-id="d5b26-469">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-469">Yes</span></span>|<span data-ttu-id="d5b26-470">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d5b26-470">N/A</span></span>|  
|<span data-ttu-id="d5b26-471">copy-unmatched-params</span><span class="sxs-lookup"><span data-stu-id="d5b26-471">copy-unmatched-params</span></span>|<span data-ttu-id="d5b26-472">Указывает, добавляются ли в определяемый шаблоном перезаписи URL-адрес параметры запроса во входящем запросе, отсутствующие в исходном шаблоне URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="d5b26-472">Specifies whether query parameters in the incoming request not present in the original URL template are added to the URL defined by the re-write template</span></span>|<span data-ttu-id="d5b26-473">Нет</span><span class="sxs-lookup"><span data-stu-id="d5b26-473">No</span></span>|<span data-ttu-id="d5b26-474">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-474">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d5b26-475">Использование</span><span class="sxs-lookup"><span data-stu-id="d5b26-475">Usage</span></span>  
 <span data-ttu-id="d5b26-476">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d5b26-476">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d5b26-477">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="d5b26-477">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="d5b26-478">**Области политики:** product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="d5b26-478">**Policy scopes:** product, API, operation</span></span>  
  
##  <span data-ttu-id="d5b26-479"><a name="XSLTransform"></a> Преобразование XML с помощью XSLT</span><span class="sxs-lookup"><span data-stu-id="d5b26-479"><a name="XSLTransform"></a> Transform XML using an XSLT</span></span>  
 <span data-ttu-id="d5b26-480">Политика `Transform XML using an XSLT` применяет преобразование данных в формате XSL в формат XML в тексте запроса или ответа.</span><span class="sxs-lookup"><span data-stu-id="d5b26-480">The `Transform XML using an XSLT` policy applies an XSL transformation to XML in the request or response body.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d5b26-481">Правило политики</span><span class="sxs-lookup"><span data-stu-id="d5b26-481">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="d5b26-482">Пример</span><span class="sxs-lookup"><span data-stu-id="d5b26-482">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="d5b26-483">Элементы</span><span class="sxs-lookup"><span data-stu-id="d5b26-483">Elements</span></span>  
  
|<span data-ttu-id="d5b26-484">Имя</span><span class="sxs-lookup"><span data-stu-id="d5b26-484">Name</span></span>|<span data-ttu-id="d5b26-485">Описание</span><span class="sxs-lookup"><span data-stu-id="d5b26-485">Description</span></span>|<span data-ttu-id="d5b26-486">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d5b26-486">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d5b26-487">xsl-transform</span><span class="sxs-lookup"><span data-stu-id="d5b26-487">xsl-transform</span></span>|<span data-ttu-id="d5b26-488">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="d5b26-488">Root element.</span></span>|<span data-ttu-id="d5b26-489">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-489">Yes</span></span>|  
|<span data-ttu-id="d5b26-490">Параметр</span><span class="sxs-lookup"><span data-stu-id="d5b26-490">parameter</span></span>|<span data-ttu-id="d5b26-491">Используется для определения переменных, используемых при преобразовании.</span><span class="sxs-lookup"><span data-stu-id="d5b26-491">Used to define variables used in the transform</span></span>|<span data-ttu-id="d5b26-492">Нет</span><span class="sxs-lookup"><span data-stu-id="d5b26-492">No</span></span>|  
|<span data-ttu-id="d5b26-493">xsl:stylesheet</span><span class="sxs-lookup"><span data-stu-id="d5b26-493">xsl:stylesheet</span></span>|<span data-ttu-id="d5b26-494">Корневой элемент таблицы стилей.</span><span class="sxs-lookup"><span data-stu-id="d5b26-494">Root stylesheet element.</span></span> <span data-ttu-id="d5b26-495">Все определенные элементы и атрибуты соответствуют стандарту [спецификации XSLT](http://www.w3.org/TR/xslt).</span><span class="sxs-lookup"><span data-stu-id="d5b26-495">All elements and attributes defined within follow the standard [XSLT specification](http://www.w3.org/TR/xslt)</span></span>|<span data-ttu-id="d5b26-496">Да</span><span class="sxs-lookup"><span data-stu-id="d5b26-496">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d5b26-497">Использование</span><span class="sxs-lookup"><span data-stu-id="d5b26-497">Usage</span></span>  
 <span data-ttu-id="d5b26-498">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d5b26-498">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d5b26-499">**Разделы политики:** inbound, outbound.</span><span class="sxs-lookup"><span data-stu-id="d5b26-499">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="d5b26-500">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="d5b26-500">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="d5b26-501">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d5b26-501">Next steps</span></span>
<span data-ttu-id="d5b26-502">Дополнительные сведения о работе с политиками см. в статье со справочными материалами по [политикам в службе управления API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="d5b26-502">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
