---
title: "Политики междоменного доступа в службе управления API Azure | Документация Майкрософт"
description: "Сведения о политиках междоменного доступа, доступных для использования в службе управления API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7689d277-8abe-472a-a78c-e6d4bd43455d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: ddca9e35b44a21294abbb5eaa4418bcdb85494cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-cross-domain-policies"></a><span data-ttu-id="3aa51-103">API Management cross domain policies (Междоменные политики службы управления API).</span><span class="sxs-lookup"><span data-stu-id="3aa51-103">API Management cross domain policies</span></span>
<span data-ttu-id="3aa51-104">В этой статье рассматриваются приведенные ниже политики управления API.</span><span class="sxs-lookup"><span data-stu-id="3aa51-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="3aa51-105">Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в управлении API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="3aa51-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="3aa51-106"><a name="CrossDomainPolicies"></a> Политики междоменного доступа</span><span class="sxs-lookup"><span data-stu-id="3aa51-106"><a name="CrossDomainPolicies"></a> Cross domain policies</span></span>  
  
-   <span data-ttu-id="3aa51-107">[Разрешение кросс-доменных вызовов](api-management-cross-domain-policies.md#AllowCrossDomainCalls) – делает API доступным из клиентов на основе браузеров Adobe Flash и Microsoft Silverlight.</span><span class="sxs-lookup"><span data-stu-id="3aa51-107">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
-   <span data-ttu-id="3aa51-108">[CORS](api-management-cross-domain-policies.md#CORS) – добавляет поддержку общего доступа к ресурсам независимо от источника (CORS) для операции или API, чтобы разрешить кросс-доменные вызовы от клиентов на основе браузера.</span><span class="sxs-lookup"><span data-stu-id="3aa51-108">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
-   <span data-ttu-id="3aa51-109">[JSONP](api-management-cross-domain-policies.md#JSONP) – добавляет поддержку JSON с заполнением (JSONP) для операции или API, чтобы разрешить кросс-доменные вызовы из браузерных клиентов JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3aa51-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
##  <span data-ttu-id="3aa51-110"><a name="AllowCrossDomainCalls"></a> Разрешение междоменных вызовов</span><span class="sxs-lookup"><span data-stu-id="3aa51-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls</span></span>  
 <span data-ttu-id="3aa51-111">Используйте политику `cross-domain`, чтобы разрешить доступ к API из браузерных клиентов на базе Adobe Flash и Microsoft Silverlight.</span><span class="sxs-lookup"><span data-stu-id="3aa51-111">Use the `cross-domain` policy to make the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3aa51-112">Правило политики</span><span class="sxs-lookup"><span data-stu-id="3aa51-112">Policy statement</span></span>  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in the Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a><span data-ttu-id="3aa51-113">Пример</span><span class="sxs-lookup"><span data-stu-id="3aa51-113">Example</span></span>  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a><span data-ttu-id="3aa51-114">Элементы</span><span class="sxs-lookup"><span data-stu-id="3aa51-114">Elements</span></span>  
  
|<span data-ttu-id="3aa51-115">Имя</span><span class="sxs-lookup"><span data-stu-id="3aa51-115">Name</span></span>|<span data-ttu-id="3aa51-116">Описание</span><span class="sxs-lookup"><span data-stu-id="3aa51-116">Description</span></span>|<span data-ttu-id="3aa51-117">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3aa51-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="3aa51-118">cross-domain</span><span class="sxs-lookup"><span data-stu-id="3aa51-118">cross-domain</span></span>|<span data-ttu-id="3aa51-119">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="3aa51-119">Root element.</span></span> <span data-ttu-id="3aa51-120">Дочерние элементы должны соответствовать [спецификации Adobe для файлов политики междоменного доступа](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span><span class="sxs-lookup"><span data-stu-id="3aa51-120">Child elements must conform to the [Adobe cross-domain policy file specification](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span></span>|<span data-ttu-id="3aa51-121">Да</span><span class="sxs-lookup"><span data-stu-id="3aa51-121">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3aa51-122">Использование</span><span class="sxs-lookup"><span data-stu-id="3aa51-122">Usage</span></span>  
 <span data-ttu-id="3aa51-123">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3aa51-123">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3aa51-124">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="3aa51-124">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="3aa51-125">**Области политики:** global.</span><span class="sxs-lookup"><span data-stu-id="3aa51-125">**Policy scopes:** global</span></span>  
  
##  <span data-ttu-id="3aa51-126"><a name="CORS"></a> CORS</span><span class="sxs-lookup"><span data-stu-id="3aa51-126"><a name="CORS"></a> CORS</span></span>  
 <span data-ttu-id="3aa51-127">Политика `cors` добавляет поддержку общего доступа к ресурсам независимо от источника (CORS) для операции или API, чтобы разрешить междоменные вызовы из браузерных клиентов.</span><span class="sxs-lookup"><span data-stu-id="3aa51-127">The `cors` policy adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
 <span data-ttu-id="3aa51-128">CORS позволяет браузеру и серверу взаимодействовать друг с другом и определять, разрешать конкретные запросы независимо от источника или нет (то есть, вызовы XMLHttpRequests, отправляемые из кода JavaScript на веб-странице в другие домены).</span><span class="sxs-lookup"><span data-stu-id="3aa51-128">CORS allows a browser and a server to interact and determine whether or not to allow specific cross-origin requests (i.e. XMLHttpRequests calls made from JavaScript on a web page to other domains).</span></span> <span data-ttu-id="3aa51-129">Это обеспечивает большую гибкость, чем просто разрешение запросов из одного источника, и более высокую защищенность, чем разрешение всех запросов независимо от источника.</span><span class="sxs-lookup"><span data-stu-id="3aa51-129">This allows for more flexibility than only allowing same-origin requests, but is more secure than allowing all cross-origin requests.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3aa51-130">Правило политики</span><span class="sxs-lookup"><span data-stu-id="3aa51-130">Policy statement</span></span>  
  
```xml  
<cors allow-credentials="false|true">  
    <allowed-origins>  
        <origin>origin uri</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="number of seconds">  
        <method>http verb</method>  
    </allowed-methods>  
    <allowed-headers>  
        <header>header name</header>  
    </allowed-headers>  
    <expose-headers>  
        <header>header name</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="example"></a><span data-ttu-id="3aa51-131">Пример</span><span class="sxs-lookup"><span data-stu-id="3aa51-131">Example</span></span>  
 <span data-ttu-id="3aa51-132">В этом примере показано, как обеспечить поддержку предварительных запросов, например с пользовательскими заголовками или методами, отличными от GET и POST.</span><span class="sxs-lookup"><span data-stu-id="3aa51-132">This example demonstrates how to support pre-flight requests, such as those with custom headers or methods other than GET and POST.</span></span> <span data-ttu-id="3aa51-133">Для поддержки пользовательских заголовков и дополнительных команд HTTP используйте разделы `allowed-methods` и `allowed-headers`, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="3aa51-133">To support custom headers and additional HTTP verbs, use the `allowed-methods` and `allowed-headers` sections as shown in the following example.</span></span>  
  
```xml  
<cors allow-credentials="true">  
    <allowed-origins>  
        <!-- Localhost useful for development -->  
        <origin>http://localhost:8080/</origin>  
        <origin>http://example.com/</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="300">  
        <method>GET</method>  
        <method>POST</method>  
        <method>PATCH</method>  
        <method>DELETE</method>  
    </allowed-methods>  
    <allowed-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
        <header>x-zumo-version</header>  
        <header>x-zumo-auth</header>  
        <header>content-type</header>  
        <header>accept</header>  
    </allowed-headers>  
    <expose-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="elements"></a><span data-ttu-id="3aa51-134">Элементы</span><span class="sxs-lookup"><span data-stu-id="3aa51-134">Elements</span></span>  
  
|<span data-ttu-id="3aa51-135">Имя</span><span class="sxs-lookup"><span data-stu-id="3aa51-135">Name</span></span>|<span data-ttu-id="3aa51-136">Описание</span><span class="sxs-lookup"><span data-stu-id="3aa51-136">Description</span></span>|<span data-ttu-id="3aa51-137">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3aa51-137">Required</span></span>|<span data-ttu-id="3aa51-138">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="3aa51-138">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="3aa51-139">cors</span><span class="sxs-lookup"><span data-stu-id="3aa51-139">cors</span></span>|<span data-ttu-id="3aa51-140">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="3aa51-140">Root element.</span></span>|<span data-ttu-id="3aa51-141">Да</span><span class="sxs-lookup"><span data-stu-id="3aa51-141">Yes</span></span>|<span data-ttu-id="3aa51-142">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3aa51-142">N/A</span></span>|  
|<span data-ttu-id="3aa51-143">allowed-origins</span><span class="sxs-lookup"><span data-stu-id="3aa51-143">allowed-origins</span></span>|<span data-ttu-id="3aa51-144">Содержит элементы `origin`, описывающие разрешенные источники для междоменных запросов.</span><span class="sxs-lookup"><span data-stu-id="3aa51-144">Contains `origin` elements that describe the allowed origins for cross-domain requests.</span></span> <span data-ttu-id="3aa51-145">`allowed-origins` может содержать один элемент `origin` со значением `*`, если нужно разрешить любые источники, либо один или несколько элементов `origin`, содержащих URI источников.</span><span class="sxs-lookup"><span data-stu-id="3aa51-145">`allowed-origins` can contain either a single `origin` element that specifies `*` to allow any origin, or one or more `origin` elements that contain a URI.</span></span>|<span data-ttu-id="3aa51-146">Да</span><span class="sxs-lookup"><span data-stu-id="3aa51-146">Yes</span></span>|<span data-ttu-id="3aa51-147">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3aa51-147">N/A</span></span>|  
|<span data-ttu-id="3aa51-148">origin</span><span class="sxs-lookup"><span data-stu-id="3aa51-148">origin</span></span>|<span data-ttu-id="3aa51-149">В качестве значений допускается `*`, которое разрешает любые источники, или URI конкретного источника.</span><span class="sxs-lookup"><span data-stu-id="3aa51-149">The value can be either `*` to allow all origins, or a URI that specifies a single origin.</span></span> <span data-ttu-id="3aa51-150">URI-адрес должен включать схему, узел и порт.</span><span class="sxs-lookup"><span data-stu-id="3aa51-150">The URI must include a scheme, host, and port.</span></span>|<span data-ttu-id="3aa51-151">Да</span><span class="sxs-lookup"><span data-stu-id="3aa51-151">Yes</span></span>|<span data-ttu-id="3aa51-152">Если в URI не указан порт, используется порт 80 для HTTP и порт 443 для HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3aa51-152">If the port is omitted in a URI, port 80 is used for HTTP and port 443 is used for HTTPS.</span></span>|  
|<span data-ttu-id="3aa51-153">allowed-methods</span><span class="sxs-lookup"><span data-stu-id="3aa51-153">allowed-methods</span></span>|<span data-ttu-id="3aa51-154">Этот элемент является обязательным, если разрешены методы, отличные от GET или POST.</span><span class="sxs-lookup"><span data-stu-id="3aa51-154">This element is required if methods other than GET or POST are allowed.</span></span> <span data-ttu-id="3aa51-155">Содержит элементы `method`, перечисляющие поддерживаемые HTTP-команды.</span><span class="sxs-lookup"><span data-stu-id="3aa51-155">Contains `method` elements that specify the supported HTTP verbs.</span></span>|<span data-ttu-id="3aa51-156">Нет</span><span class="sxs-lookup"><span data-stu-id="3aa51-156">No</span></span>|<span data-ttu-id="3aa51-157">Если этот раздел отсутствует, поддерживаются методы GET и POST.</span><span class="sxs-lookup"><span data-stu-id="3aa51-157">If this section is not present, GET and POST are supported.</span></span>|  
|<span data-ttu-id="3aa51-158">метод</span><span class="sxs-lookup"><span data-stu-id="3aa51-158">method</span></span>|<span data-ttu-id="3aa51-159">Задает команду HTTP.</span><span class="sxs-lookup"><span data-stu-id="3aa51-159">Specifies an HTTP verb.</span></span>|<span data-ttu-id="3aa51-160">Если раздел `allowed-methods` присутствует, в нем обязательно должен быть по крайней мере один элемент `method`.</span><span class="sxs-lookup"><span data-stu-id="3aa51-160">At least one `method` element is required if the `allowed-methods` section is present.</span></span>|<span data-ttu-id="3aa51-161">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3aa51-161">N/A</span></span>|  
|<span data-ttu-id="3aa51-162">allowed-headers</span><span class="sxs-lookup"><span data-stu-id="3aa51-162">allowed-headers</span></span>|<span data-ttu-id="3aa51-163">Этот элемент содержит элементы `header`, указывающие имена заголовков, которые могут быть включены в запрос.</span><span class="sxs-lookup"><span data-stu-id="3aa51-163">This element contains `header` elements specifying names of the headers that can be included in the request.</span></span>|<span data-ttu-id="3aa51-164">Нет</span><span class="sxs-lookup"><span data-stu-id="3aa51-164">No</span></span>|<span data-ttu-id="3aa51-165">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3aa51-165">N/A</span></span>|  
|<span data-ttu-id="3aa51-166">expose-headers</span><span class="sxs-lookup"><span data-stu-id="3aa51-166">expose-headers</span></span>|<span data-ttu-id="3aa51-167">Этот элемент содержит элементы `header`, указывающие имена заголовков, которые будут доступны клиенту.</span><span class="sxs-lookup"><span data-stu-id="3aa51-167">This element contains `header` elements specifying names of the headers that will be accessible by the client.</span></span>|<span data-ttu-id="3aa51-168">Нет</span><span class="sxs-lookup"><span data-stu-id="3aa51-168">No</span></span>|<span data-ttu-id="3aa51-169">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3aa51-169">N/A</span></span>|  
|<span data-ttu-id="3aa51-170">Верхний колонтитул</span><span class="sxs-lookup"><span data-stu-id="3aa51-170">header</span></span>|<span data-ttu-id="3aa51-171">Задает имя заголовка.</span><span class="sxs-lookup"><span data-stu-id="3aa51-171">Specifies a header name.</span></span>|<span data-ttu-id="3aa51-172">Если присутствует раздел `allowed-headers` или `expose-headers`, в нем обязательно должен быть по крайней мере один элемент `header`.</span><span class="sxs-lookup"><span data-stu-id="3aa51-172">At least one `header` element is required in `allowed-headers` or `expose-headers` if the section is present.</span></span>|<span data-ttu-id="3aa51-173">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3aa51-173">N/A</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3aa51-174">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="3aa51-174">Attributes</span></span>  
  
|<span data-ttu-id="3aa51-175">Имя</span><span class="sxs-lookup"><span data-stu-id="3aa51-175">Name</span></span>|<span data-ttu-id="3aa51-176">Описание</span><span class="sxs-lookup"><span data-stu-id="3aa51-176">Description</span></span>|<span data-ttu-id="3aa51-177">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3aa51-177">Required</span></span>|<span data-ttu-id="3aa51-178">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="3aa51-178">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="3aa51-179">allow-credentials</span><span class="sxs-lookup"><span data-stu-id="3aa51-179">allow-credentials</span></span>|<span data-ttu-id="3aa51-180">Заголовок `Access-Control-Allow-Credentials` в ответе на предварительный запрос получит значение, указанное в этом атрибуте. Этот заголовок определяет, может ли клиент передавать в междоменных запросах учетные данные.</span><span class="sxs-lookup"><span data-stu-id="3aa51-180">The `Access-Control-Allow-Credentials` header in the preflight response will be set to the value of this attribute and affect the client’s ability to submit credentials in cross-domain requests.</span></span>|<span data-ttu-id="3aa51-181">Нет</span><span class="sxs-lookup"><span data-stu-id="3aa51-181">No</span></span>|<span data-ttu-id="3aa51-182">нет</span><span class="sxs-lookup"><span data-stu-id="3aa51-182">false</span></span>|  
|<span data-ttu-id="3aa51-183">preflight-result-max-age</span><span class="sxs-lookup"><span data-stu-id="3aa51-183">preflight-result-max-age</span></span>|<span data-ttu-id="3aa51-184">Заголовок `Access-Control-Max-Age` в ответе на предварительный запрос получит значение, указанное в этом атрибуте. Этот заголовок определяет, может ли клиент кэшировать ответы на предварительные запросы.</span><span class="sxs-lookup"><span data-stu-id="3aa51-184">The `Access-Control-Max-Age` header in the preflight response will be set to the value of this attribute and affect the user agent’s ability to cache pre-flight response.</span></span>|<span data-ttu-id="3aa51-185">Нет</span><span class="sxs-lookup"><span data-stu-id="3aa51-185">No</span></span>|<span data-ttu-id="3aa51-186">0</span><span class="sxs-lookup"><span data-stu-id="3aa51-186">0</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3aa51-187">Использование</span><span class="sxs-lookup"><span data-stu-id="3aa51-187">Usage</span></span>  
 <span data-ttu-id="3aa51-188">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3aa51-188">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3aa51-189">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="3aa51-189">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="3aa51-190">**Области политики:** API, operation.</span><span class="sxs-lookup"><span data-stu-id="3aa51-190">**Policy scopes:** API, operation</span></span>  
  
##  <span data-ttu-id="3aa51-191"><a name="JSONP"></a> JSONP</span><span class="sxs-lookup"><span data-stu-id="3aa51-191"><a name="JSONP"></a> JSONP</span></span>  
 <span data-ttu-id="3aa51-192">Политика `jsonp` добавляет поддержку JSON с заполнением (JSONP) для операции или API, чтобы разрешить междоменные вызовы из браузерных клиентов на основе JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3aa51-192">The `jsonp` policy adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span> <span data-ttu-id="3aa51-193">JSONP — это метод, который используется в программах JavaScript для запроса данных из сервера в другом домене.</span><span class="sxs-lookup"><span data-stu-id="3aa51-193">JSONP is a method used in JavaScript programs to request data from a server in a different domain.</span></span> <span data-ttu-id="3aa51-194">JSONP обходит ограничение, принудительно устанавливаемое большинством веб-браузеров, когда доступ к веб-страницам должен выполняться в том же домене.</span><span class="sxs-lookup"><span data-stu-id="3aa51-194">JSONP bypasses the limitation enforced by most web browsers where access to web pages must be in the same domain.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="3aa51-195">Правило политики</span><span class="sxs-lookup"><span data-stu-id="3aa51-195">Policy statement</span></span>  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a><span data-ttu-id="3aa51-196">Пример</span><span class="sxs-lookup"><span data-stu-id="3aa51-196">Example</span></span>  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 <span data-ttu-id="3aa51-197">Если метод вызывается без параметра обратного вызова ?cb=XXX, будет возвращаться простой JSON (без оболочки для вызовов функции).</span><span class="sxs-lookup"><span data-stu-id="3aa51-197">If you call the method without the callback parameter ?cb=XXX it will return plain JSON (without a function call wrapper).</span></span>  
  
 <span data-ttu-id="3aa51-198">Если добавить к запросу параметр обратного вызова `?cb=XXX`, возвращается результат JSONP, заключающий в исходные результаты JSON функцию обратного вызова, например, `XYZ('<json result goes here>');`</span><span class="sxs-lookup"><span data-stu-id="3aa51-198">If you add the callback parameter `?cb=XXX` it will return a JSONP result, wrapping the original JSON results around the callback function like `XYZ('<json result goes here>');`</span></span>  
  
### <a name="elements"></a><span data-ttu-id="3aa51-199">Элементы</span><span class="sxs-lookup"><span data-stu-id="3aa51-199">Elements</span></span>  
  
|<span data-ttu-id="3aa51-200">Имя</span><span class="sxs-lookup"><span data-stu-id="3aa51-200">Name</span></span>|<span data-ttu-id="3aa51-201">Описание</span><span class="sxs-lookup"><span data-stu-id="3aa51-201">Description</span></span>|<span data-ttu-id="3aa51-202">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3aa51-202">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="3aa51-203">jsonp</span><span class="sxs-lookup"><span data-stu-id="3aa51-203">jsonp</span></span>|<span data-ttu-id="3aa51-204">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="3aa51-204">Root element.</span></span>|<span data-ttu-id="3aa51-205">Да</span><span class="sxs-lookup"><span data-stu-id="3aa51-205">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="3aa51-206">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="3aa51-206">Attributes</span></span>  
  
|<span data-ttu-id="3aa51-207">Имя</span><span class="sxs-lookup"><span data-stu-id="3aa51-207">Name</span></span>|<span data-ttu-id="3aa51-208">Описание</span><span class="sxs-lookup"><span data-stu-id="3aa51-208">Description</span></span>|<span data-ttu-id="3aa51-209">Обязательно</span><span class="sxs-lookup"><span data-stu-id="3aa51-209">Required</span></span>|<span data-ttu-id="3aa51-210">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="3aa51-210">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="3aa51-211">callback-parameter-name</span><span class="sxs-lookup"><span data-stu-id="3aa51-211">callback-parameter-name</span></span>|<span data-ttu-id="3aa51-212">Кросс-доменный вызов функции JavaScript, в качестве префикса в котором присутствует полное имя домена, в котором находится функция.</span><span class="sxs-lookup"><span data-stu-id="3aa51-212">The cross-domain JavaScript function call prefixed with the fully qualified domain name where the function resides.</span></span>|<span data-ttu-id="3aa51-213">Да</span><span class="sxs-lookup"><span data-stu-id="3aa51-213">Yes</span></span>|<span data-ttu-id="3aa51-214">Недоступно</span><span class="sxs-lookup"><span data-stu-id="3aa51-214">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="3aa51-215">Использование</span><span class="sxs-lookup"><span data-stu-id="3aa51-215">Usage</span></span>  
 <span data-ttu-id="3aa51-216">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="3aa51-216">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="3aa51-217">**Разделы политики:** outbound.</span><span class="sxs-lookup"><span data-stu-id="3aa51-217">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="3aa51-218">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="3aa51-218">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="3aa51-219">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3aa51-219">Next steps</span></span>
<span data-ttu-id="3aa51-220">Дополнительные сведения о работе с политиками см. в статье со справочными материалами по [политикам в службе управления API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="3aa51-220">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  