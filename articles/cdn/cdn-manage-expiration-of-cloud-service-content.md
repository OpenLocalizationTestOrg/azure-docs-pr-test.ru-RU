---
title: "истечение срока действия aaaManage веб-содержимого в сети доставки Содержимого Azure | Документы Microsoft"
description: "Узнайте, как toomanage истечения срока действия содержимого веб-приложений и облачные службы Azure, ASP.NET или IIS в Azure CDN."
services: cdn
documentationcenter: .NET
author: zhangmanling
manager: erikre
editor: 
ms.assetid: bef53fcc-bb13-4002-9324-9edee9da8288
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: a0154236c3893b627f4480e0688f555964862556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a><span data-ttu-id="6d1ba-103">Управление сроком действия содержимого веб-приложений и облачных служб Azure, ASP.NET или IIS в Azure CDN</span><span class="sxs-lookup"><span data-stu-id="6d1ba-103">Manage expiration of Azure Web Apps/Cloud Services, ASP.NET, or IIS content in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6d1ba-104">Веб-приложения и облачные службы Azure, ASP.NET или IIS</span><span class="sxs-lookup"><span data-stu-id="6d1ba-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="6d1ba-105">Служба BLOB-объектов в службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="6d1ba-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="6d1ba-106">Файлы из любого общедоступного исходного веб-сервера могут кэшироваться в Azure CDN до истечения его срока жизни.</span><span class="sxs-lookup"><span data-stu-id="6d1ba-106">Files from any publicly accessible origin web server can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="6d1ba-107">Hello TTL определяется hello [ *Cache-Control* заголовок](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) в ответ hello HTTP hello исходного сервера.</span><span class="sxs-lookup"><span data-stu-id="6d1ba-107">hello TTL is determined by hello [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in hello HTTP response from hello origin server.</span></span>  <span data-ttu-id="6d1ba-108">В этой статье описывается как tooset `Cache-Control` заголовки для веб-приложения Azure, облачных служб Azure, приложений ASP.NET и узлы служб IIS, все из которых настраиваются точно так же.</span><span class="sxs-lookup"><span data-stu-id="6d1ba-108">This article describes how tooset `Cache-Control` headers for Azure Web Apps, Azure Cloud Services, ASP.NET applications, and Internet Information Services sites, all of which are configured similarly.</span></span>

> [!TIP]
> <span data-ttu-id="6d1ba-109">Вы можете tooset не TTL в файле.</span><span class="sxs-lookup"><span data-stu-id="6d1ba-109">You may choose tooset no TTL on a file.</span></span>  <span data-ttu-id="6d1ba-110">Тогда Azure CDN по умолчанию применит срок жизни длительностью семь дней.</span><span class="sxs-lookup"><span data-stu-id="6d1ba-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="6d1ba-111">Дополнительные сведения о работе toospeed toofiles доступ и другие ресурсы в сети доставки Содержимого Azure см. в разделе hello [Общие сведения о Azure CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6d1ba-111">For more information about how Azure CDN works toospeed up access toofiles and other resources, see hello [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a><span data-ttu-id="6d1ba-112">Настройка заголовков Cache-Control в конфигурации</span><span class="sxs-lookup"><span data-stu-id="6d1ba-112">Setting Cache-Control Headers in configuration</span></span>
<span data-ttu-id="6d1ba-113">Для статического содержимого, такие как изображения и таблицы стилей, можно управлять частотой обновления hello, изменяя hello **applicationHost.config** или **web.config** файлы для веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="6d1ba-113">For static content, such as images and style sheets, you can control hello update frequency by modifying hello **applicationHost.config** or **web.config** files for your web application.</span></span>  <span data-ttu-id="6d1ba-114">Hello **system.webServer\staticContent\clientCache** элемент в файле конфигурации hello установит hello `Cache-Control` заголовок для содержимого.</span><span class="sxs-lookup"><span data-stu-id="6d1ba-114">hello **system.webServer\staticContent\clientCache** element in hello configuration file will set hello `Cache-Control` header for your content.</span></span> <span data-ttu-id="6d1ba-115">Для **web.config**, параметры конфигурации hello повлияют на все содержимое в hello и все вложенные папки, если не переопределено на уровне вложенную Привет.</span><span class="sxs-lookup"><span data-stu-id="6d1ba-115">For **web.config**, hello configuration settings will affect everything in hello folder and all subfolders, unless overridden at hello subfolder level.</span></span>  <span data-ttu-id="6d1ba-116">Например можно задать значение по умолчанию срока жизни в toohave корневой hello все статическое содержимое в кэше в течение трех дней, но иметь вложенную папку с более переменной содержимого с кэширования составляет 6 часов.</span><span class="sxs-lookup"><span data-stu-id="6d1ba-116">For example, you can set a default time-to-live at hello root toohave all static content cached for 3 days, but have a subfolder that has more variable content with a cache setting of 6 hours.</span></span>  <span data-ttu-id="6d1ba-117">Для **applicationHost.config**, все приложения на сайте hello будут затронуты, но могут быть переопределены в **web.config** файлы в приложениях hello.</span><span class="sxs-lookup"><span data-stu-id="6d1ba-117">For **applicationHost.config**, all applications on hello site will be affected, but can be overridden in **web.config** files in hello applications.</span></span>

<span data-ttu-id="6d1ba-118">Hello следующий XML-КОДЕ показан пример установки **clientCache** toospecify a максимальный срок хранения, равным 3 дням:</span><span class="sxs-lookup"><span data-stu-id="6d1ba-118">hello following XML shows an example of setting **clientCache** toospecify a maximum age of 3 days:</span></span>  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

<span data-ttu-id="6d1ba-119">Указание **UseMaxAge** добавляет `Cache-Control: max-age=<nnn>` toohello ответ заголовок на основании hello значение, указанное в hello **CacheControlMaxAge** атрибута.</span><span class="sxs-lookup"><span data-stu-id="6d1ba-119">Specifying **UseMaxAge** adds a `Cache-Control: max-age=<nnn>` header toohello response based on hello value specified in hello **CacheControlMaxAge** attribute.</span></span> <span data-ttu-id="6d1ba-120">имеет формат Hello hello timespan для hello **cacheControlMaxAge** атрибут <days>.<hours>:<min>:<sec>.</span><span class="sxs-lookup"><span data-stu-id="6d1ba-120">hello format of hello timespan is for hello **cacheControlMaxAge** attribute is <days>.<hours>:<min>:<sec>.</span></span> <span data-ttu-id="6d1ba-121">Дополнительные сведения о hello **clientCache** узел, в разделе [кэш клиента <clientCache> ](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span><span class="sxs-lookup"><span data-stu-id="6d1ba-121">For more information on hello **clientCache** node, see [Client Cache <clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span></span>  

## <a name="setting-cache-control-headers-in-code"></a><span data-ttu-id="6d1ba-122">Настройка заголовков Cache-Control в коде</span><span class="sxs-lookup"><span data-stu-id="6d1ba-122">Setting Cache-Control Headers in Code</span></span>
<span data-ttu-id="6d1ba-123">Для приложений ASP.NET, можно задать поведение кэширования CDN hello программно, параметр hello **HttpResponse.Cache** свойство.</span><span class="sxs-lookup"><span data-stu-id="6d1ba-123">For ASP.NET applications, you can set hello CDN caching behavior programmatically by setting hello **HttpResponse.Cache** property.</span></span> <span data-ttu-id="6d1ba-124">Дополнительные сведения о hello **HttpResponse.Cache** свойство, в разделе [свойство HttpResponse.Cache](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) и [класс HttpCachePolicy](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d1ba-124">For more information on hello **HttpResponse.Cache** property, see [HttpResponse.Cache Property](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) and [HttpCachePolicy Class](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

<span data-ttu-id="6d1ba-125">Если вы хотите tooprogrammatically кэшировать содержимое приложения в ASP.NET, убедитесь, что помечены как кэшируемые содержимое hello, присвоив свойству HttpCacheability слишком*открытый*.</span><span class="sxs-lookup"><span data-stu-id="6d1ba-125">If you want tooprogrammatically cache application content in ASP.NET, make sure that hello content is marked as cacheable by setting HttpCacheability too*Public*.</span></span> <span data-ttu-id="6d1ba-126">Кроме того, убедитесь, что задан проверяющий элемент управления кэша.</span><span class="sxs-lookup"><span data-stu-id="6d1ba-126">Also, ensure that a cache validator is set.</span></span> <span data-ttu-id="6d1ba-127">проверяющий элемент управления кэша Hello может быть последнее изменение отметки времени, заданная при вызове SetLastModified, или значение etag, установленное при вызове SetETag.</span><span class="sxs-lookup"><span data-stu-id="6d1ba-127">hello cache validator can be a Last Modified timestamp set by calling SetLastModified, or an etag value set by calling SetETag.</span></span> <span data-ttu-id="6d1ba-128">При необходимости можно также указать срок хранения кэша, вызвав SetExpires, или можно положиться на эвристический метод кэширования по умолчанию hello описано ранее в этом документе.</span><span class="sxs-lookup"><span data-stu-id="6d1ba-128">Optionally, you can also specify a cache expiration time by calling SetExpires, or you can rely on hello default cache heuristics described earlier in this document.</span></span>  

<span data-ttu-id="6d1ba-129">Например toocache содержимое за один час, добавьте hello следующее:</span><span class="sxs-lookup"><span data-stu-id="6d1ba-129">For example, toocache content for one hour, add hello following:</span></span>  

```csharp
// Set hello caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a><span data-ttu-id="6d1ba-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6d1ba-130">Next Steps</span></span>
* [<span data-ttu-id="6d1ba-131">Ознакомления с подробными сведениями о hello **clientCache** элемент</span><span class="sxs-lookup"><span data-stu-id="6d1ba-131">Read details about hello **clientCache** element</span></span>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)
* [<span data-ttu-id="6d1ba-132">Ознакомьтесь с документацией hello для hello **HttpResponse.Cache** свойство</span><span class="sxs-lookup"><span data-stu-id="6d1ba-132">Read hello documentation for hello **HttpResponse.Cache** Property</span></span>](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) 
* <span data-ttu-id="6d1ba-133">[Ознакомьтесь с документацией hello для hello **класс HttpCachePolicy**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="6d1ba-133">[Read hello documentation for hello **HttpCachePolicy Class**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

