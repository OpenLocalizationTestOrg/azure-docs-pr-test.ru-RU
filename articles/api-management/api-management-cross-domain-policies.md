---
title: "aaaAzure API управления политики взаимодействия доменов | Документы Microsoft"
description: "Дополнительные сведения о hello политики взаимодействия доменов можно использовать в службе управления API Azure."
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
ms.openlocfilehash: dd5ebfd65b92ebd0c1f589a2bac669a3928d40b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-cross-domain-policies"></a><span data-ttu-id="23c7b-103">API Management cross domain policies (Междоменные политики службы управления API).</span><span class="sxs-lookup"><span data-stu-id="23c7b-103">API Management cross domain policies</span></span>
<span data-ttu-id="23c7b-104">Здесь вы найдете ссылку для hello следующих политиках управления интерфейсами API.</span><span class="sxs-lookup"><span data-stu-id="23c7b-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="23c7b-105">Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в управлении API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="23c7b-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="23c7b-106"><a name="CrossDomainPolicies"></a> Политики междоменного доступа</span><span class="sxs-lookup"><span data-stu-id="23c7b-106"><a name="CrossDomainPolicies"></a> Cross domain policies</span></span>  
  
-   <span data-ttu-id="23c7b-107">[Разрешить междоменные вызовы](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -становится доступным hello API из клиентов Adobe Flash и Microsoft Silverlight на основе браузера.</span><span class="sxs-lookup"><span data-stu-id="23c7b-107">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
-   <span data-ttu-id="23c7b-108">[CORS](api-management-cross-domain-policies.md#CORS) -добавляет ресурсов независимо от источника (CORS) для управления доступом поддерживает операцию tooan или API tooallow междоменные вызовы из браузерных клиентов.</span><span class="sxs-lookup"><span data-stu-id="23c7b-108">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
-   <span data-ttu-id="23c7b-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - добавляет JSON с заполнением (JSONP) поддержка tooan операции или API tooallow междоменные вызовы из браузерных клиентов JavaScript.</span><span class="sxs-lookup"><span data-stu-id="23c7b-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
##  <span data-ttu-id="23c7b-110"><a name="AllowCrossDomainCalls"></a> Разрешение междоменных вызовов</span><span class="sxs-lookup"><span data-stu-id="23c7b-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls</span></span>  
 <span data-ttu-id="23c7b-111">Используйте hello `cross-domain` hello toomake политики API, доступную с клиентов Adobe Flash и Microsoft Silverlight на основе браузера.</span><span class="sxs-lookup"><span data-stu-id="23c7b-111">Use hello `cross-domain` policy toomake hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="23c7b-112">Правило политики</span><span class="sxs-lookup"><span data-stu-id="23c7b-112">Policy statement</span></span>  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in hello Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a><span data-ttu-id="23c7b-113">Пример</span><span class="sxs-lookup"><span data-stu-id="23c7b-113">Example</span></span>  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a><span data-ttu-id="23c7b-114">Элементы</span><span class="sxs-lookup"><span data-stu-id="23c7b-114">Elements</span></span>  
  
|<span data-ttu-id="23c7b-115">Имя</span><span class="sxs-lookup"><span data-stu-id="23c7b-115">Name</span></span>|<span data-ttu-id="23c7b-116">Описание</span><span class="sxs-lookup"><span data-stu-id="23c7b-116">Description</span></span>|<span data-ttu-id="23c7b-117">Обязательно</span><span class="sxs-lookup"><span data-stu-id="23c7b-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="23c7b-118">cross-domain</span><span class="sxs-lookup"><span data-stu-id="23c7b-118">cross-domain</span></span>|<span data-ttu-id="23c7b-119">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="23c7b-119">Root element.</span></span> <span data-ttu-id="23c7b-120">Дочерние элементы должны соответствовать toohello [спецификация файла междоменной политики Adobe](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span><span class="sxs-lookup"><span data-stu-id="23c7b-120">Child elements must conform toohello [Adobe cross-domain policy file specification](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span></span>|<span data-ttu-id="23c7b-121">Да</span><span class="sxs-lookup"><span data-stu-id="23c7b-121">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="23c7b-122">Использование</span><span class="sxs-lookup"><span data-stu-id="23c7b-122">Usage</span></span>  
 <span data-ttu-id="23c7b-123">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="23c7b-123">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="23c7b-124">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="23c7b-124">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="23c7b-125">**Области политики:** global.</span><span class="sxs-lookup"><span data-stu-id="23c7b-125">**Policy scopes:** global</span></span>  
  
##  <span data-ttu-id="23c7b-126"><a name="CORS"></a> CORS</span><span class="sxs-lookup"><span data-stu-id="23c7b-126"><a name="CORS"></a> CORS</span></span>  
 <span data-ttu-id="23c7b-127">Hello `cors` политики добавляет ресурсов независимо от источника (CORS) для управления доступом поддерживает операцию tooan или API tooallow междоменные вызовы из браузерных клиентов.</span><span class="sxs-lookup"><span data-stu-id="23c7b-127">hello `cors` policy adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
 <span data-ttu-id="23c7b-128">CORS позволяет браузеру и toointeract сервера и определения запросов независимо от наличия определенного tooallow независимо от источника (т. е. вызовы XMLHttpRequests из кода JavaScript на веб-странице tooother домены).</span><span class="sxs-lookup"><span data-stu-id="23c7b-128">CORS allows a browser and a server toointeract and determine whether or not tooallow specific cross-origin requests (i.e. XMLHttpRequests calls made from JavaScript on a web page tooother domains).</span></span> <span data-ttu-id="23c7b-129">Это обеспечивает большую гибкость, чем просто разрешение запросов из одного источника, и более высокую защищенность, чем разрешение всех запросов независимо от источника.</span><span class="sxs-lookup"><span data-stu-id="23c7b-129">This allows for more flexibility than only allowing same-origin requests, but is more secure than allowing all cross-origin requests.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="23c7b-130">Правило политики</span><span class="sxs-lookup"><span data-stu-id="23c7b-130">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="23c7b-131">Пример</span><span class="sxs-lookup"><span data-stu-id="23c7b-131">Example</span></span>  
 <span data-ttu-id="23c7b-132">В этом примере показано, как запрашивает предварительных toosupport, например с пользовательскими заголовками, и методы, отличные от GET и POST.</span><span class="sxs-lookup"><span data-stu-id="23c7b-132">This example demonstrates how toosupport pre-flight requests, such as those with custom headers or methods other than GET and POST.</span></span> <span data-ttu-id="23c7b-133">toosupport пользовательских заголовков и дополнительных команд HTTP используйте hello `allowed-methods` и `allowed-headers` разделов, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="23c7b-133">toosupport custom headers and additional HTTP verbs, use hello `allowed-methods` and `allowed-headers` sections as shown in hello following example.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="23c7b-134">Элементы</span><span class="sxs-lookup"><span data-stu-id="23c7b-134">Elements</span></span>  
  
|<span data-ttu-id="23c7b-135">Имя</span><span class="sxs-lookup"><span data-stu-id="23c7b-135">Name</span></span>|<span data-ttu-id="23c7b-136">Описание</span><span class="sxs-lookup"><span data-stu-id="23c7b-136">Description</span></span>|<span data-ttu-id="23c7b-137">Обязательно</span><span class="sxs-lookup"><span data-stu-id="23c7b-137">Required</span></span>|<span data-ttu-id="23c7b-138">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="23c7b-138">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="23c7b-139">cors</span><span class="sxs-lookup"><span data-stu-id="23c7b-139">cors</span></span>|<span data-ttu-id="23c7b-140">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="23c7b-140">Root element.</span></span>|<span data-ttu-id="23c7b-141">Да</span><span class="sxs-lookup"><span data-stu-id="23c7b-141">Yes</span></span>|<span data-ttu-id="23c7b-142">Недоступно</span><span class="sxs-lookup"><span data-stu-id="23c7b-142">N/A</span></span>|  
|<span data-ttu-id="23c7b-143">allowed-origins</span><span class="sxs-lookup"><span data-stu-id="23c7b-143">allowed-origins</span></span>|<span data-ttu-id="23c7b-144">Содержит `origin` элементы, описывающие hello допускается источники для междоменных запросах.</span><span class="sxs-lookup"><span data-stu-id="23c7b-144">Contains `origin` elements that describe hello allowed origins for cross-domain requests.</span></span> <span data-ttu-id="23c7b-145">`allowed-origins`может содержать один `origin` элемент, который задает `*` tooallow любые источники, одного или нескольких `origin` элементов, содержащих URI.</span><span class="sxs-lookup"><span data-stu-id="23c7b-145">`allowed-origins` can contain either a single `origin` element that specifies `*` tooallow any origin, or one or more `origin` elements that contain a URI.</span></span>|<span data-ttu-id="23c7b-146">Да</span><span class="sxs-lookup"><span data-stu-id="23c7b-146">Yes</span></span>|<span data-ttu-id="23c7b-147">Недоступно</span><span class="sxs-lookup"><span data-stu-id="23c7b-147">N/A</span></span>|  
|<span data-ttu-id="23c7b-148">origin</span><span class="sxs-lookup"><span data-stu-id="23c7b-148">origin</span></span>|<span data-ttu-id="23c7b-149">Hello значение может быть либо `*` tooallow все источники, или URI, указывающий один источник.</span><span class="sxs-lookup"><span data-stu-id="23c7b-149">hello value can be either `*` tooallow all origins, or a URI that specifies a single origin.</span></span> <span data-ttu-id="23c7b-150">Hello URI должен включать схему, узел и порт.</span><span class="sxs-lookup"><span data-stu-id="23c7b-150">hello URI must include a scheme, host, and port.</span></span>|<span data-ttu-id="23c7b-151">Да</span><span class="sxs-lookup"><span data-stu-id="23c7b-151">Yes</span></span>|<span data-ttu-id="23c7b-152">Если hello порт указан в URI, используется порт 80 для HTTP и порт 443 для HTTPS используется.</span><span class="sxs-lookup"><span data-stu-id="23c7b-152">If hello port is omitted in a URI, port 80 is used for HTTP and port 443 is used for HTTPS.</span></span>|  
|<span data-ttu-id="23c7b-153">allowed-methods</span><span class="sxs-lookup"><span data-stu-id="23c7b-153">allowed-methods</span></span>|<span data-ttu-id="23c7b-154">Этот элемент является обязательным, если разрешены методы, отличные от GET или POST.</span><span class="sxs-lookup"><span data-stu-id="23c7b-154">This element is required if methods other than GET or POST are allowed.</span></span> <span data-ttu-id="23c7b-155">Содержит `method` элементы, которые задают hello поддерживается HTTP-команды.</span><span class="sxs-lookup"><span data-stu-id="23c7b-155">Contains `method` elements that specify hello supported HTTP verbs.</span></span>|<span data-ttu-id="23c7b-156">Нет</span><span class="sxs-lookup"><span data-stu-id="23c7b-156">No</span></span>|<span data-ttu-id="23c7b-157">Если этот раздел отсутствует, поддерживаются методы GET и POST.</span><span class="sxs-lookup"><span data-stu-id="23c7b-157">If this section is not present, GET and POST are supported.</span></span>|  
|<span data-ttu-id="23c7b-158">метод</span><span class="sxs-lookup"><span data-stu-id="23c7b-158">method</span></span>|<span data-ttu-id="23c7b-159">Задает команду HTTP.</span><span class="sxs-lookup"><span data-stu-id="23c7b-159">Specifies an HTTP verb.</span></span>|<span data-ttu-id="23c7b-160">По крайней мере один `method` элемент является обязательным, если hello `allowed-methods` раздел присутствует.</span><span class="sxs-lookup"><span data-stu-id="23c7b-160">At least one `method` element is required if hello `allowed-methods` section is present.</span></span>|<span data-ttu-id="23c7b-161">Недоступно</span><span class="sxs-lookup"><span data-stu-id="23c7b-161">N/A</span></span>|  
|<span data-ttu-id="23c7b-162">allowed-headers</span><span class="sxs-lookup"><span data-stu-id="23c7b-162">allowed-headers</span></span>|<span data-ttu-id="23c7b-163">Этот элемент содержит `header` элементы, указывающие имена заголовков hello, которые могут быть включены в запрос hello.</span><span class="sxs-lookup"><span data-stu-id="23c7b-163">This element contains `header` elements specifying names of hello headers that can be included in hello request.</span></span>|<span data-ttu-id="23c7b-164">Нет</span><span class="sxs-lookup"><span data-stu-id="23c7b-164">No</span></span>|<span data-ttu-id="23c7b-165">Недоступно</span><span class="sxs-lookup"><span data-stu-id="23c7b-165">N/A</span></span>|  
|<span data-ttu-id="23c7b-166">expose-headers</span><span class="sxs-lookup"><span data-stu-id="23c7b-166">expose-headers</span></span>|<span data-ttu-id="23c7b-167">Этот элемент содержит `header` элементы, указывающие имена hello заголовки, которые будут доступны hello клиента.</span><span class="sxs-lookup"><span data-stu-id="23c7b-167">This element contains `header` elements specifying names of hello headers that will be accessible by hello client.</span></span>|<span data-ttu-id="23c7b-168">Нет</span><span class="sxs-lookup"><span data-stu-id="23c7b-168">No</span></span>|<span data-ttu-id="23c7b-169">Недоступно</span><span class="sxs-lookup"><span data-stu-id="23c7b-169">N/A</span></span>|  
|<span data-ttu-id="23c7b-170">Верхний колонтитул</span><span class="sxs-lookup"><span data-stu-id="23c7b-170">header</span></span>|<span data-ttu-id="23c7b-171">Задает имя заголовка.</span><span class="sxs-lookup"><span data-stu-id="23c7b-171">Specifies a header name.</span></span>|<span data-ttu-id="23c7b-172">По крайней мере один `header` элемент является обязательным в `allowed-headers` или `expose-headers` при наличии раздела hello.</span><span class="sxs-lookup"><span data-stu-id="23c7b-172">At least one `header` element is required in `allowed-headers` or `expose-headers` if hello section is present.</span></span>|<span data-ttu-id="23c7b-173">Недоступно</span><span class="sxs-lookup"><span data-stu-id="23c7b-173">N/A</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="23c7b-174">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="23c7b-174">Attributes</span></span>  
  
|<span data-ttu-id="23c7b-175">Имя</span><span class="sxs-lookup"><span data-stu-id="23c7b-175">Name</span></span>|<span data-ttu-id="23c7b-176">Описание</span><span class="sxs-lookup"><span data-stu-id="23c7b-176">Description</span></span>|<span data-ttu-id="23c7b-177">Обязательно</span><span class="sxs-lookup"><span data-stu-id="23c7b-177">Required</span></span>|<span data-ttu-id="23c7b-178">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="23c7b-178">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="23c7b-179">allow-credentials</span><span class="sxs-lookup"><span data-stu-id="23c7b-179">allow-credentials</span></span>|<span data-ttu-id="23c7b-180">Hello `Access-Control-Allow-Credentials` заголовок в hello предварительный ответ будет toohello значение этого атрибута и влияют на hello клиента возможность toosubmit и учетные данные в междоменных запросах.</span><span class="sxs-lookup"><span data-stu-id="23c7b-180">hello `Access-Control-Allow-Credentials` header in hello preflight response will be set toohello value of this attribute and affect hello client’s ability toosubmit credentials in cross-domain requests.</span></span>|<span data-ttu-id="23c7b-181">Нет</span><span class="sxs-lookup"><span data-stu-id="23c7b-181">No</span></span>|<span data-ttu-id="23c7b-182">нет</span><span class="sxs-lookup"><span data-stu-id="23c7b-182">false</span></span>|  
|<span data-ttu-id="23c7b-183">preflight-result-max-age</span><span class="sxs-lookup"><span data-stu-id="23c7b-183">preflight-result-max-age</span></span>|<span data-ttu-id="23c7b-184">Hello `Access-Control-Max-Age` заголовок в hello предварительный ответ будет toohello значение этого атрибута и влияют на агент пользователя hello возможность toocache предварительный ответ.</span><span class="sxs-lookup"><span data-stu-id="23c7b-184">hello `Access-Control-Max-Age` header in hello preflight response will be set toohello value of this attribute and affect hello user agent’s ability toocache pre-flight response.</span></span>|<span data-ttu-id="23c7b-185">Нет</span><span class="sxs-lookup"><span data-stu-id="23c7b-185">No</span></span>|<span data-ttu-id="23c7b-186">0</span><span class="sxs-lookup"><span data-stu-id="23c7b-186">0</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="23c7b-187">Использование</span><span class="sxs-lookup"><span data-stu-id="23c7b-187">Usage</span></span>  
 <span data-ttu-id="23c7b-188">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="23c7b-188">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="23c7b-189">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="23c7b-189">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="23c7b-190">**Области политики:** API, operation.</span><span class="sxs-lookup"><span data-stu-id="23c7b-190">**Policy scopes:** API, operation</span></span>  
  
##  <span data-ttu-id="23c7b-191"><a name="JSONP"></a> JSONP</span><span class="sxs-lookup"><span data-stu-id="23c7b-191"><a name="JSONP"></a> JSONP</span></span>  
 <span data-ttu-id="23c7b-192">Hello `jsonp` политики добавляет заполнение операция tooan поддержки (JSONP) или API tooallow междоменные вызовы из браузерных клиентов JavaScript.</span><span class="sxs-lookup"><span data-stu-id="23c7b-192">hello `jsonp` policy adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span> <span data-ttu-id="23c7b-193">JSONP — это метод, используемый в данных toorequest программы JavaScript на сервере в другом домене.</span><span class="sxs-lookup"><span data-stu-id="23c7b-193">JSONP is a method used in JavaScript programs toorequest data from a server in a different domain.</span></span> <span data-ttu-id="23c7b-194">JSONP позволяет обойти ограничение hello, большинство веб-браузеров, где доступ tooweb страницы должны принадлежать hello того же домена.</span><span class="sxs-lookup"><span data-stu-id="23c7b-194">JSONP bypasses hello limitation enforced by most web browsers where access tooweb pages must be in hello same domain.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="23c7b-195">Правило политики</span><span class="sxs-lookup"><span data-stu-id="23c7b-195">Policy statement</span></span>  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a><span data-ttu-id="23c7b-196">Пример</span><span class="sxs-lookup"><span data-stu-id="23c7b-196">Example</span></span>  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 <span data-ttu-id="23c7b-197">При вызове метода hello без hello параметр обратного вызова? cb = XXX, возвращается обычный JSON (без оболочки вызова функции).</span><span class="sxs-lookup"><span data-stu-id="23c7b-197">If you call hello method without hello callback parameter ?cb=XXX it will return plain JSON (without a function call wrapper).</span></span>  
  
 <span data-ttu-id="23c7b-198">Если добавляется параметр обратного вызова hello `?cb=XXX` он вернет результат JSONP, упаковки hello исходные результаты JSON вокруг hello функции обратного вызова, как`XYZ('<json result goes here>');`</span><span class="sxs-lookup"><span data-stu-id="23c7b-198">If you add hello callback parameter `?cb=XXX` it will return a JSONP result, wrapping hello original JSON results around hello callback function like `XYZ('<json result goes here>');`</span></span>  
  
### <a name="elements"></a><span data-ttu-id="23c7b-199">Элементы</span><span class="sxs-lookup"><span data-stu-id="23c7b-199">Elements</span></span>  
  
|<span data-ttu-id="23c7b-200">Имя</span><span class="sxs-lookup"><span data-stu-id="23c7b-200">Name</span></span>|<span data-ttu-id="23c7b-201">Описание</span><span class="sxs-lookup"><span data-stu-id="23c7b-201">Description</span></span>|<span data-ttu-id="23c7b-202">Обязательно</span><span class="sxs-lookup"><span data-stu-id="23c7b-202">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="23c7b-203">jsonp</span><span class="sxs-lookup"><span data-stu-id="23c7b-203">jsonp</span></span>|<span data-ttu-id="23c7b-204">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="23c7b-204">Root element.</span></span>|<span data-ttu-id="23c7b-205">Да</span><span class="sxs-lookup"><span data-stu-id="23c7b-205">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="23c7b-206">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="23c7b-206">Attributes</span></span>  
  
|<span data-ttu-id="23c7b-207">Имя</span><span class="sxs-lookup"><span data-stu-id="23c7b-207">Name</span></span>|<span data-ttu-id="23c7b-208">Описание</span><span class="sxs-lookup"><span data-stu-id="23c7b-208">Description</span></span>|<span data-ttu-id="23c7b-209">Обязательно</span><span class="sxs-lookup"><span data-stu-id="23c7b-209">Required</span></span>|<span data-ttu-id="23c7b-210">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="23c7b-210">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="23c7b-211">callback-parameter-name</span><span class="sxs-lookup"><span data-stu-id="23c7b-211">callback-parameter-name</span></span>|<span data-ttu-id="23c7b-212">Hello вызову функции JavaScript между доменами с префиксом hello полное доменное имя, где hello находится функция.</span><span class="sxs-lookup"><span data-stu-id="23c7b-212">hello cross-domain JavaScript function call prefixed with hello fully qualified domain name where hello function resides.</span></span>|<span data-ttu-id="23c7b-213">Да</span><span class="sxs-lookup"><span data-stu-id="23c7b-213">Yes</span></span>|<span data-ttu-id="23c7b-214">Недоступно</span><span class="sxs-lookup"><span data-stu-id="23c7b-214">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="23c7b-215">Использование</span><span class="sxs-lookup"><span data-stu-id="23c7b-215">Usage</span></span>  
 <span data-ttu-id="23c7b-216">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="23c7b-216">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="23c7b-217">**Разделы политики:** outbound.</span><span class="sxs-lookup"><span data-stu-id="23c7b-217">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="23c7b-218">**Области политики:** global, product, API, operation.</span><span class="sxs-lookup"><span data-stu-id="23c7b-218">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="23c7b-219">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="23c7b-219">Next steps</span></span>
<span data-ttu-id="23c7b-220">Дополнительные сведения о работе с политиками см. в статье со справочными материалами по [политикам в службе управления API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="23c7b-220">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  