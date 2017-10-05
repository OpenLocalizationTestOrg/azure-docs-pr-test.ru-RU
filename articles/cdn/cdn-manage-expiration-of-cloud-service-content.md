---
title: "Управление сроком действия веб-содержимого в Azure CDN | Документация Майкрософт"
description: "Узнайте, как управлять сроком действия содержимого веб-приложений и облачных служб Azure, ASP.NET или IIS в Azure CDN."
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
ms.openlocfilehash: c207d780857a61d4b1fc0f39e6185cae67abc955
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-expiration-of-azure-web-appscloud-services-aspnet-or-iis-content-in-azure-cdn"></a><span data-ttu-id="245b5-103">Управление сроком действия содержимого веб-приложений и облачных служб Azure, ASP.NET или IIS в Azure CDN</span><span class="sxs-lookup"><span data-stu-id="245b5-103">Manage expiration of Azure Web Apps/Cloud Services, ASP.NET, or IIS content in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="245b5-104">Веб-приложения и облачные службы Azure, ASP.NET или IIS</span><span class="sxs-lookup"><span data-stu-id="245b5-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="245b5-105">Служба BLOB-объектов в службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="245b5-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="245b5-106">Файлы из любого общедоступного исходного веб-сервера могут кэшироваться в Azure CDN до истечения его срока жизни.</span><span class="sxs-lookup"><span data-stu-id="245b5-106">Files from any publicly accessible origin web server can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="245b5-107">Срок жизни определяется [заголовком *Cache-Control*](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9), указанным в HTTP-ответе исходного сервера.</span><span class="sxs-lookup"><span data-stu-id="245b5-107">The TTL is determined by the [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in the HTTP response from the origin server.</span></span>  <span data-ttu-id="245b5-108">В этой статье описано, как настроить заголовки `Cache-Control` для веб-приложений Azure, облачных служб Azure, приложений ASP.NET и сайтов IIS, которые все настроены аналогичным образом.</span><span class="sxs-lookup"><span data-stu-id="245b5-108">This article describes how to set `Cache-Control` headers for Azure Web Apps, Azure Cloud Services, ASP.NET applications, and Internet Information Services sites, all of which are configured similarly.</span></span>

> [!TIP]
> <span data-ttu-id="245b5-109">Вы можете не указывать срок жизни для файла.</span><span class="sxs-lookup"><span data-stu-id="245b5-109">You may choose to set no TTL on a file.</span></span>  <span data-ttu-id="245b5-110">Тогда Azure CDN по умолчанию применит срок жизни длительностью семь дней.</span><span class="sxs-lookup"><span data-stu-id="245b5-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="245b5-111">Дополнительные сведения о том, как Azure CDN ускоряет доступ к файлам и другим ресурсам, см. в статье [Общие сведения о сети доставки содержимого (CDN) Azure](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="245b5-111">For more information about how Azure CDN works to speed up access to files and other resources, see the [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> 

## <a name="setting-cache-control-headers-in-configuration"></a><span data-ttu-id="245b5-112">Настройка заголовков Cache-Control в конфигурации</span><span class="sxs-lookup"><span data-stu-id="245b5-112">Setting Cache-Control Headers in configuration</span></span>
<span data-ttu-id="245b5-113">Вы можете управлять частотой обновления статического содержимого, такого как изображения и таблицы стилей, изменяя файлы **applicationHost.config** или **web.config** своего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="245b5-113">For static content, such as images and style sheets, you can control the update frequency by modifying the **applicationHost.config** or **web.config** files for your web application.</span></span>  <span data-ttu-id="245b5-114">Элемент **system.webServer\staticContent\clientCache** в файле конфигурации установит заголовок `Cache-Control` для содержимого.</span><span class="sxs-lookup"><span data-stu-id="245b5-114">The **system.webServer\staticContent\clientCache** element in the configuration file will set the `Cache-Control` header for your content.</span></span> <span data-ttu-id="245b5-115">Параметры конфигурации файла **web.config**будут влиять на все элементы в этой папке и вложенных в нее папках, если это не переопределено на уровне вложенной папки.</span><span class="sxs-lookup"><span data-stu-id="245b5-115">For **web.config**, the configuration settings will affect everything in the folder and all subfolders, unless overridden at the subfolder level.</span></span>  <span data-ttu-id="245b5-116">Например, можно установить значение по умолчанию для срока жизни в корневой папке, чтобы все статическое содержимое кэшировалось в течение 3 дней, но предусмотреть вложенную папку с содержимым, которое изменяется чаще, и задать для нее частоту кэширования 6 часов.</span><span class="sxs-lookup"><span data-stu-id="245b5-116">For example, you can set a default time-to-live at the root to have all static content cached for 3 days, but have a subfolder that has more variable content with a cache setting of 6 hours.</span></span>  <span data-ttu-id="245b5-117">Файл **applicationHost.config** повлияет на все приложения на сайте, но может быть переопределен в файлах **web.config** приложений.</span><span class="sxs-lookup"><span data-stu-id="245b5-117">For **applicationHost.config**, all applications on the site will be affected, but can be overridden in **web.config** files in the applications.</span></span>

<span data-ttu-id="245b5-118">В следующем XML-коде показан пример использования параметра **clientCache** для указания максимального возраста "3 дня":</span><span class="sxs-lookup"><span data-stu-id="245b5-118">The following XML shows an example of setting **clientCache** to specify a maximum age of 3 days:</span></span>  

```xml
<configuration>
    <system.webServer>
        <staticContent>
            <clientCache cacheControlMode="UseMaxAge" cacheControlMaxAge="3.00:00:00" />
        </staticContent>
    </system.webServer>
</configuration>
```

<span data-ttu-id="245b5-119">При указании **UseMaxAge** в ответ добавляется заголовок `Cache-Control: max-age=<nnn>` на основе значения, указанного в атрибуте **CacheControlMaxAge**.</span><span class="sxs-lookup"><span data-stu-id="245b5-119">Specifying **UseMaxAge** adds a `Cache-Control: max-age=<nnn>` header to the response based on the value specified in the **CacheControlMaxAge** attribute.</span></span> <span data-ttu-id="245b5-120">Формат временного диапазона для атрибута **cacheControlMaxAge** имеет вид <days>.<hours>:<min>:<sec>.</span><span class="sxs-lookup"><span data-stu-id="245b5-120">The format of the timespan is for the **cacheControlMaxAge** attribute is <days>.<hours>:<min>:<sec>.</span></span> <span data-ttu-id="245b5-121">Дополнительные сведения об узле **clientCache** см. по [этой ссылке<clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span><span class="sxs-lookup"><span data-stu-id="245b5-121">For more information on the **clientCache** node, see [Client Cache <clientCache>](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span></span>  

## <a name="setting-cache-control-headers-in-code"></a><span data-ttu-id="245b5-122">Настройка заголовков Cache-Control в коде</span><span class="sxs-lookup"><span data-stu-id="245b5-122">Setting Cache-Control Headers in Code</span></span>
<span data-ttu-id="245b5-123">Для приложений ASP.NET можно настроить режим кэша CDN программно, задав свойство **HttpResponse.Cache**.</span><span class="sxs-lookup"><span data-stu-id="245b5-123">For ASP.NET applications, you can set the CDN caching behavior programmatically by setting the **HttpResponse.Cache** property.</span></span> <span data-ttu-id="245b5-124">Дополнительные сведения о свойстве **HttpResponse.Cache**, см. в разделах [Свойство HttpResponse.Cache](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) и [Класс HttpCachePolicy](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="245b5-124">For more information on the **HttpResponse.Cache** property, see [HttpResponse.Cache Property](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx) and [HttpCachePolicy Class](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

<span data-ttu-id="245b5-125">Если требуется программно кэшировать содержимое приложения в ASP.NET, убедитесь, что это содержимое помечено как кэшируемое, присвоив HttpCacheability значение *Public*.</span><span class="sxs-lookup"><span data-stu-id="245b5-125">If you want to programmatically cache application content in ASP.NET, make sure that the content is marked as cacheable by setting HttpCacheability to *Public*.</span></span> <span data-ttu-id="245b5-126">Кроме того, убедитесь, что задан проверяющий элемент управления кэша.</span><span class="sxs-lookup"><span data-stu-id="245b5-126">Also, ensure that a cache validator is set.</span></span> <span data-ttu-id="245b5-127">Проверяющий элемент управления кэша может быть меткой времени последнего изменения, заданной с помощью вызова SetLastModified, или значением etag, заданным с помощью вызова SetETag.</span><span class="sxs-lookup"><span data-stu-id="245b5-127">The cache validator can be a Last Modified timestamp set by calling SetLastModified, or an etag value set by calling SetETag.</span></span> <span data-ttu-id="245b5-128">При необходимости можно также указать срок действия кэша, вызвав SetExpires, или можно положиться на эвристику кэширования по умолчанию, описанную ранее в этом документе.</span><span class="sxs-lookup"><span data-stu-id="245b5-128">Optionally, you can also specify a cache expiration time by calling SetExpires, or you can rely on the default cache heuristics described earlier in this document.</span></span>  

<span data-ttu-id="245b5-129">Например, для кэширования содержимого на срок в один час добавьте следующие строки:</span><span class="sxs-lookup"><span data-stu-id="245b5-129">For example, to cache content for one hour, add the following:</span></span>  

```csharp
// Set the caching parameters.
Response.Cache.SetExpires(DateTime.Now.AddHours(1));
Response.Cache.SetCacheability(HttpCacheability.Public);
Response.Cache.SetLastModified(DateTime.Now);
```

## <a name="next-steps"></a><span data-ttu-id="245b5-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="245b5-130">Next Steps</span></span>
* <span data-ttu-id="245b5-131">[Сведения об элементе **clientCache**](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache).</span><span class="sxs-lookup"><span data-stu-id="245b5-131">[Read details about the **clientCache** element](http://www.iis.net/ConfigReference/system.webServer/staticContent/clientCache)</span></span>
* <span data-ttu-id="245b5-132">[Документация по свойству **HttpResponse.Cache**](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx).</span><span class="sxs-lookup"><span data-stu-id="245b5-132">[Read the documentation for the **HttpResponse.Cache** Property](http://msdn.microsoft.com/library/system.web.httpresponse.cache.aspx)</span></span> 
* <span data-ttu-id="245b5-133">[Документация по **HttpCachePolicy Class**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span><span class="sxs-lookup"><span data-stu-id="245b5-133">[Read the documentation for the **HttpCachePolicy Class**](http://msdn.microsoft.com/library/system.web.httpcachepolicy.aspx).</span></span>  

