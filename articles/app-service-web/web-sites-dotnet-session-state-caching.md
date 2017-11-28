---
title: "состояние aaaSession с кэшем Azure Redis в службе приложений Azure"
description: "Узнайте, как toouse hello кэширования по состояния сеанса для службы кэша Azure toosupport ASP.NET."
services: app-service\web
documentationcenter: .net
author: Rick-Anderson
manager: erikre
editor: none
ms.assetid: 4f98d289-2698-464d-85cd-99ec40fad1f2
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 06/27/2016
ms.author: riande
ms.openlocfilehash: f689b6754ea072aa195f822ab6482f4bf2748375
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a><span data-ttu-id="95ec3-103">Состояние сеанса с кэшем Redis для Azure в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="95ec3-103">Session state with Azure Redis cache in Azure App Service</span></span>
<span data-ttu-id="95ec3-104">В этом разделе объясняется, как toouse hello служба кэша Redis Azure для хранения состояния сеанса.</span><span class="sxs-lookup"><span data-stu-id="95ec3-104">This topic explains how toouse hello Azure Redis Cache Service for session state.</span></span>

<span data-ttu-id="95ec3-105">Если веб-приложения ASP.NET использует состояние сеанса, необходимо будет tooconfigure поставщик состояния сеанса внешних (hello служба кэша Redis или поставщик состояния сеанса SQL Server).</span><span class="sxs-lookup"><span data-stu-id="95ec3-105">If your ASP.NET web app uses session state, you will need tooconfigure an external session state provider (either hello Redis Cache Service or a SQL Server session state provider).</span></span> <span data-ttu-id="95ec3-106">Если используются состояние сеанса, а не использовать внешнего поставщика, можно только tooone экземпляр веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="95ec3-106">If you use session state, and don't use an external provider, you will be limited tooone instance of your web app.</span></span> <span data-ttu-id="95ec3-107">Hello служба кэша Redis является быстрым и простым tooenable hello.</span><span class="sxs-lookup"><span data-stu-id="95ec3-107">hello Redis Cache Service is hello fastest and simplest tooenable.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="95ec3-108"><a id="createcache"></a>Создать hello кэша</span><span class="sxs-lookup"><span data-stu-id="95ec3-108"><a id="createcache"></a>Create hello Cache</span></span>
<span data-ttu-id="95ec3-109">Выполните [этим указаниям](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) toocreate hello кэша.</span><span class="sxs-lookup"><span data-stu-id="95ec3-109">Follow [these directions](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) toocreate hello cache.</span></span>

## <span data-ttu-id="95ec3-110"><a id="configureproject"></a>Добавить hello RedisSessionStateProvider NuGet пакета tooyour веб-приложения</span><span class="sxs-lookup"><span data-stu-id="95ec3-110"><a id="configureproject"></a>Add hello RedisSessionStateProvider NuGet package tooyour web app</span></span>
<span data-ttu-id="95ec3-111">Установка hello NuGet `RedisSessionStateProvider` пакета.</span><span class="sxs-lookup"><span data-stu-id="95ec3-111">Install hello NuGet `RedisSessionStateProvider` package.</span></span>  <span data-ttu-id="95ec3-112">Используйте hello следующая команда tooinstall из консоли диспетчера пакетов hello (**средства** > **диспетчера пакетов NuGet** > **консоль диспетчера пакетов**):</span><span class="sxs-lookup"><span data-stu-id="95ec3-112">Use hello following command tooinstall from hello package manager console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span></span>

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

<span data-ttu-id="95ec3-113">tooinstall из **средства** > **диспетчера пакетов NuGet** > **управление фрагментом пакетами для решения**, поиск `RedisSessionStateProvider`.</span><span class="sxs-lookup"><span data-stu-id="95ec3-113">tooinstall from **Tools** > **NuGet Package Manager** > **Manage NugGet Packages for Solution**, search for `RedisSessionStateProvider`.</span></span>

<span data-ttu-id="95ec3-114">Дополнительные сведения см. hello [NuGet RedisSessionStateProvider страницы](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) и [Настройка клиента кэша hello](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span><span class="sxs-lookup"><span data-stu-id="95ec3-114">For more information see hello [NuGet RedisSessionStateProvider page](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) and [Configure hello cache client](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span></span>

## <span data-ttu-id="95ec3-115"><a id="configurewebconfig"></a>Изменение файла Web.Config hello</span><span class="sxs-lookup"><span data-stu-id="95ec3-115"><a id="configurewebconfig"></a>Modify hello Web.Config File</span></span>
<span data-ttu-id="95ec3-116">Кроме ссылается на сборку toomaking для кэша, hello пакет NuGet добавляет записи в заглушки hello *web.config* файла.</span><span class="sxs-lookup"><span data-stu-id="95ec3-116">In addition toomaking assembly references for Cache, hello NuGet package adds stub entries in hello *web.config* file.</span></span> 

1. <span data-ttu-id="95ec3-117">Откройте hello *web.config* и найти hello hello **sessionState** элемента.</span><span class="sxs-lookup"><span data-stu-id="95ec3-117">Open hello *web.config* and find hello hello **sessionState** element.</span></span>
2. <span data-ttu-id="95ec3-118">Введите значения hello для `host`, `accessKey`, `port` (hello SSL-порт должен быть 6380) и задайте `SSL` слишком`true`.</span><span class="sxs-lookup"><span data-stu-id="95ec3-118">Enter hello values for `host`, `accessKey`, `port` (hello SSL port should be 6380), and set `SSL` too`true`.</span></span> <span data-ttu-id="95ec3-119">Эти значения можно получить из hello [портала Azure](http://go.microsoft.com/fwlink/?LinkId=529715) колонку для экземпляра кэша.</span><span class="sxs-lookup"><span data-stu-id="95ec3-119">These values can be obtained from hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) blade for your cache instance.</span></span> <span data-ttu-id="95ec3-120">Дополнительные сведения см. в разделе [подключения кэша toohello](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span><span class="sxs-lookup"><span data-stu-id="95ec3-120">For more information, see [Connect toohello cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span></span> <span data-ttu-id="95ec3-121">Обратите внимание, что порт не SSL hello отключен по умолчанию для нового кэша.</span><span class="sxs-lookup"><span data-stu-id="95ec3-121">Note that hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="95ec3-122">Дополнительные сведения о включении порта без поддержки SSL hello см. в разделе hello [порты доступа](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) раздела hello [Настройка кэша в кэше Redis для Azure](https://msdn.microsoft.com/library/azure/dn793612.aspx) раздела.</span><span class="sxs-lookup"><span data-stu-id="95ec3-122">For more information about enabling hello non-SSL port, see hello [Access Ports](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) section in hello [Configure a cache in Azure Redis Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx) topic.</span></span> <span data-ttu-id="95ec3-123">Hello следующую разметку показывает hello изменения toohello *web.config* файла, в частности hello изменения слишком*порт*, *узла*, accessKey * и *ssl*.</span><span class="sxs-lookup"><span data-stu-id="95ec3-123">hello following markup shows hello changes toohello *web.config* file, specifically hello changes too*port*, *host*, accessKey*, and *ssl*.</span></span>
   
          <system.web>;
            <customErrors mode="Off" />;
            <authentication mode="None" />;
            <compilation debug="true" targetFramework="4.5" />;
            <httpRuntime targetFramework="4.5" />;
            <sessionState mode="Custom" customProvider="RedisSessionProvider">;
              <providers>;  
                  <!--<add name="RedisSessionProvider" 
                    host = "127.0.0.1" [String]
                    port = "" [number]
                    accessKey = "" [String]
                    ssl = "false" [true|false]
                    throwOnError = "true" [true|false]
                    retryTimeoutInMilliseconds = "0" [number]
                    databaseId = "0" [number]
                    applicationName = "" [String]
                  />;-->;
                 <add name="RedisSessionProvider" 
                      type="Microsoft.Web.Redis.RedisSessionStateProvider" 
                      port="6380"
                      host="movie2.redis.cache.windows.net" 
                      accessKey="m7PNV60CrvKpLqMUxosC3dSe6kx9nQ6jP5del8TmADk=" 
                      ssl="true" />;
              <!--<add name="MySessionStateStore" type="Microsoft.Web.Redis.RedisSessionStateProvider" host="127.0.0.1" accessKey="" ssl="false" />;-->;
              </providers>;
            </sessionState>;
          </system.web>;

## <span data-ttu-id="95ec3-124"><a id="usesessionobject"></a>Использование hello объекта сеанса в коде</span><span class="sxs-lookup"><span data-stu-id="95ec3-124"><a id="usesessionobject"></a> Use hello Session Object in Code</span></span>
<span data-ttu-id="95ec3-125">последним шагом Hello является toobegin, используя объект сеанса hello в коде ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="95ec3-125">hello final step is toobegin using hello Session object in your ASP.NET code.</span></span> <span data-ttu-id="95ec3-126">Добавление состояния toosession объектов с помощью hello **Session.Add** метод.</span><span class="sxs-lookup"><span data-stu-id="95ec3-126">You add objects toosession state by using hello **Session.Add** method.</span></span> <span data-ttu-id="95ec3-127">Этот метод использует элементы toostore пары "ключ значение" в кэш состояния сеанса hello.</span><span class="sxs-lookup"><span data-stu-id="95ec3-127">This method uses key-value pairs toostore items in hello session state cache.</span></span>

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

<span data-ttu-id="95ec3-128">Привет, следующий код получает это значение из состояния сеанса.</span><span class="sxs-lookup"><span data-stu-id="95ec3-128">hello following code retrieves this value from session state.</span></span>

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

<span data-ttu-id="95ec3-129">Можно также использовать объекты toocache кэша Redis hello в веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="95ec3-129">You can also use hello Redis Cache toocache objects in your web app.</span></span> <span data-ttu-id="95ec3-130">Дополнительные сведения см. в статье о [приложении для обработки фильмов MVC с кэшем Redis для Azure за 15 минут](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span><span class="sxs-lookup"><span data-stu-id="95ec3-130">For more info, see [MVC movie app with Azure Redis Cache in 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span></span>
<span data-ttu-id="95ec3-131">Дополнительные сведения о том, как состояние сеанса ASP.NET toouse, в разделе [Общие сведения о состоянии сеанса ASP.NET][ASP.NET Session State Overview].</span><span class="sxs-lookup"><span data-stu-id="95ec3-131">For more details about how toouse ASP.NET session state, see [ASP.NET Session State Overview][ASP.NET Session State Overview].</span></span>

> [!NOTE]
> <span data-ttu-id="95ec3-132">Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="95ec3-132">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="95ec3-133">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="95ec3-133">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="95ec3-134">Изменения</span><span class="sxs-lookup"><span data-stu-id="95ec3-134">What's changed</span></span>
* <span data-ttu-id="95ec3-135">Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="95ec3-135">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
  
  <span data-ttu-id="95ec3-136">*Автор: [Рик Андерсон (Rick Anderson)](https://twitter.com/RickAndMSFT)*</span><span class="sxs-lookup"><span data-stu-id="95ec3-136">*By [Rick Anderson](https://twitter.com/RickAndMSFT)*</span></span>

[installed hello latest]: http://www.windowsazure.com/downloads/?sdk=net  
[ASP.NET Session State Overview]: http://msdn.microsoft.com/library/ms178581.aspx

[NewIcon]: ./media/web-sites-dotnet-session-state-caching/CacheScreenshot_NewButton.png
[NewCacheDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CreateOptions.png
[CacheIcon]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheIcon.png
[NuGetDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_NuGet.png
[OutputConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_OC_WebConfig.png
[CacheConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheConfig.png
[EndpointURL]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_EndpointURL.png
[ManageKeys]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_ManageAccessKeys.png

