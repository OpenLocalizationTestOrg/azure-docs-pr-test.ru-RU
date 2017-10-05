---
title: "Состояние сеанса с кэшем Redis для Azure в службе приложений Azure"
description: "Узнайте, как использовать службу кэша Azure для поддержки кэширования состояний сеансов ASP.NET."
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
ms.openlocfilehash: 64fa909daf92b2b1f0cf4c7b334edba807fe7228
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="session-state-with-azure-redis-cache-in-azure-app-service"></a><span data-ttu-id="31d74-103">Состояние сеанса с кэшем Redis для Azure в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="31d74-103">Session state with Azure Redis cache in Azure App Service</span></span>
<span data-ttu-id="31d74-104">В этом разделе объясняется, как использовать службу кэша Redis для Azure для состояния сеанса.</span><span class="sxs-lookup"><span data-stu-id="31d74-104">This topic explains how to use the Azure Redis Cache Service for session state.</span></span>

<span data-ttu-id="31d74-105">Если ваше веб-приложение ASP.NET использует состояние сеанса, вам потребуется настроить поставщик состояния внешнего сеанса (либо службу Redis Cache или поставщик состояния сеанса SQL Server).</span><span class="sxs-lookup"><span data-stu-id="31d74-105">If your ASP.NET web app uses session state, you will need to configure an external session state provider (either the Redis Cache Service or a SQL Server session state provider).</span></span> <span data-ttu-id="31d74-106">Если вы используете дату сеанса и не используете внешний поставщик, вы будете ограничены одним экземпляром вашего веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="31d74-106">If you use session state, and don't use an external provider, you will be limited to one instance of your web app.</span></span> <span data-ttu-id="31d74-107">Служба Redis Cache самая простая, и включить ее можно очень быстро.</span><span class="sxs-lookup"><span data-stu-id="31d74-107">The Redis Cache Service is the fastest and simplest to enable.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="31d74-108"><a id="createcache"></a>Создание кэша</span><span class="sxs-lookup"><span data-stu-id="31d74-108"><a id="createcache"></a>Create the Cache</span></span>
<span data-ttu-id="31d74-109">Следуйте [этим инструкциям](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache), чтобы создать кэш.</span><span class="sxs-lookup"><span data-stu-id="31d74-109">Follow [these directions](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-cache) to create the cache.</span></span>

## <span data-ttu-id="31d74-110"><a id="configureproject"></a>Добавление пакета NuGet RedisSessionStateProvider в веб-приложение</span><span class="sxs-lookup"><span data-stu-id="31d74-110"><a id="configureproject"></a>Add the RedisSessionStateProvider NuGet package to your web app</span></span>
<span data-ttu-id="31d74-111">Установите пакет NuGet `RedisSessionStateProvider` .</span><span class="sxs-lookup"><span data-stu-id="31d74-111">Install the NuGet `RedisSessionStateProvider` package.</span></span>  <span data-ttu-id="31d74-112">Используйте следующую команду, чтобы установить из консоли менеджера пакетов (**Инструменты** > **Диспетчер пакетов NuGet** > **Консоль диспетчера пакетов**):</span><span class="sxs-lookup"><span data-stu-id="31d74-112">Use the following command to install from the package manager console (**Tools** > **NuGet Package Manager** > **Package Manager Console**):</span></span>

  `PM> Install-Package Microsoft.Web.RedisSessionStateProvider`

<span data-ttu-id="31d74-113">Чтобы выполнить установку из меню **Сервис** > **Диспетчер пакетов NuGet** > **Управление пакетами NugGet для решения**, выполните поиск по запросу `RedisSessionStateProvider`.</span><span class="sxs-lookup"><span data-stu-id="31d74-113">To install from **Tools** > **NuGet Package Manager** > **Manage NugGet Packages for Solution**, search for `RedisSessionStateProvider`.</span></span>

<span data-ttu-id="31d74-114">Для получения дополнительных сведений см. [страницу NuGet RedisSessionStateProvider](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) и [Настройка клиента кэша](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span><span class="sxs-lookup"><span data-stu-id="31d74-114">For more information see the [NuGet RedisSessionStateProvider page](http://www.nuget.org/packages/Microsoft.Web.RedisSessionStateProvider/) and [Configure the cache client](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#NuGet).</span></span>

## <span data-ttu-id="31d74-115"><a id="configurewebconfig"></a>Изменение файла Web.Config</span><span class="sxs-lookup"><span data-stu-id="31d74-115"><a id="configurewebconfig"></a>Modify the Web.Config File</span></span>
<span data-ttu-id="31d74-116">Кроме внесения ссылки на сборку для кэша, NuGet-пакет добавляет записи заглушки в файл *web.config* .</span><span class="sxs-lookup"><span data-stu-id="31d74-116">In addition to making assembly references for Cache, the NuGet package adds stub entries in the *web.config* file.</span></span> 

1. <span data-ttu-id="31d74-117">Откройте *web.config* и найдите элемент **sessionState** .</span><span class="sxs-lookup"><span data-stu-id="31d74-117">Open the *web.config* and find the the **sessionState** element.</span></span>
2. <span data-ttu-id="31d74-118">Введите значения для `host`, `accessKey`, `port` (необходимо указать 6380 в качестве порта SSL) и установите `SSL` в значение `true`.</span><span class="sxs-lookup"><span data-stu-id="31d74-118">Enter the values for `host`, `accessKey`, `port` (the SSL port should be 6380), and set `SSL` to `true`.</span></span> <span data-ttu-id="31d74-119">Эти значения можно получить в выноске для экземпляра кэша на [портале Azure](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="31d74-119">These values can be obtained from the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) blade for your cache instance.</span></span> <span data-ttu-id="31d74-120">Дополнительные сведения см. в разделе [Подключение к кэшу](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span><span class="sxs-lookup"><span data-stu-id="31d74-120">For more information, see [Connect to the cache](../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#connect-to-cache).</span></span> <span data-ttu-id="31d74-121">Обратите внимание, для новых кэшей все порты, кроме SSL, по умолчанию запрещены.</span><span class="sxs-lookup"><span data-stu-id="31d74-121">Note that the non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="31d74-122">Дополнительные сведения о том, как настроить использование порта без SSL, см. в статье [Настройка кэша Redis для Azure](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) в разделе [Порты доступа](https://msdn.microsoft.com/library/azure/dn793612.aspx).</span><span class="sxs-lookup"><span data-stu-id="31d74-122">For more information about enabling the non-SSL port, see the [Access Ports](https://msdn.microsoft.com/library/azure/dn793612.aspx#AccessPorts) section in the [Configure a cache in Azure Redis Cache](https://msdn.microsoft.com/library/azure/dn793612.aspx) topic.</span></span> <span data-ttu-id="31d74-123">В следующем примере показана изменения *web.config* файла, в частности изменения *порт*, *узла*, accessKey * и *ssl* .</span><span class="sxs-lookup"><span data-stu-id="31d74-123">The following markup shows the changes to the *web.config* file, specifically the changes to *port*, *host*, accessKey*, and *ssl*.</span></span>
   
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

## <span data-ttu-id="31d74-124"><a id="usesessionobject"></a> Использование объекта сеанса в коде</span><span class="sxs-lookup"><span data-stu-id="31d74-124"><a id="usesessionobject"></a> Use the Session Object in Code</span></span>
<span data-ttu-id="31d74-125">Последним шагом является начало использования объекта сеанса в коде ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="31d74-125">The final step is to begin using the Session object in your ASP.NET code.</span></span> <span data-ttu-id="31d74-126">Добавление объектов к состоянию сеанса выполняется с помощью метода **Session.Add** .</span><span class="sxs-lookup"><span data-stu-id="31d74-126">You add objects to session state by using the **Session.Add** method.</span></span> <span data-ttu-id="31d74-127">Этот метод использует пары "ключ-значение" для хранения элементов в кэше состояния сеанса.</span><span class="sxs-lookup"><span data-stu-id="31d74-127">This method uses key-value pairs to store items in the session state cache.</span></span>

    string strValue = "yourvalue";
    Session.Add("yourkey", strValue);

<span data-ttu-id="31d74-128">Следующий код извлекает значение из состояния сеанса.</span><span class="sxs-lookup"><span data-stu-id="31d74-128">The following code retrieves this value from session state.</span></span>

    object objValue = Session["yourkey"];
    if (objValue != null)
       strValue = (string)objValue;    

<span data-ttu-id="31d74-129">Вы можете также использовать Redis Cache для кэширования объектов в вашем веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="31d74-129">You can also use the Redis Cache to cache objects in your web app.</span></span> <span data-ttu-id="31d74-130">Дополнительные сведения см. в статье о [приложении для обработки фильмов MVC с кэшем Redis для Azure за 15 минут](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span><span class="sxs-lookup"><span data-stu-id="31d74-130">For more info, see [MVC movie app with Azure Redis Cache in 15 minutes](https://azure.microsoft.com/blog/2014/06/05/mvc-movie-app-with-azure-redis-cache-in-15-minutes/).</span></span>
<span data-ttu-id="31d74-131">См. дополнительные сведения об [использовании состояния сеанса ASP.NET][ASP.NET Session State Overview].</span><span class="sxs-lookup"><span data-stu-id="31d74-131">For more details about how to use ASP.NET session state, see [ASP.NET Session State Overview][ASP.NET Session State Overview].</span></span>

> [!NOTE]
> <span data-ttu-id="31d74-132">Чтобы приступить к работе со службой приложений Azure до создания учетной записи Azure, перейдите к разделу [Пробное использование службы приложений](https://azure.microsoft.com/try/app-service/), где вы можете быстро создать кратковременное веб-приложение начального уровня в службе приложений.</span><span class="sxs-lookup"><span data-stu-id="31d74-132">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="31d74-133">Никаких кредитных карт и обязательств.</span><span class="sxs-lookup"><span data-stu-id="31d74-133">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="31d74-134">Изменения</span><span class="sxs-lookup"><span data-stu-id="31d74-134">What's changed</span></span>
* <span data-ttu-id="31d74-135">Руководство по переходу от веб-сайтов к службе приложений см. в статье [Служба приложений Azure и существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="31d74-135">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>
  
  <span data-ttu-id="31d74-136">*Автор: [Рик Андерсон (Rick Anderson)](https://twitter.com/RickAndMSFT)*</span><span class="sxs-lookup"><span data-stu-id="31d74-136">*By [Rick Anderson](https://twitter.com/RickAndMSFT)*</span></span>

[installed the latest]: http://www.windowsazure.com/downloads/?sdk=net  
[ASP.NET Session State Overview]: http://msdn.microsoft.com/library/ms178581.aspx

[NewIcon]: ./media/web-sites-dotnet-session-state-caching/CacheScreenshot_NewButton.png
[NewCacheDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CreateOptions.png
[CacheIcon]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheIcon.png
[NuGetDialog]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_NuGet.png
[OutputConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_OC_WebConfig.png
[CacheConfig]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_CacheConfig.png
[EndpointURL]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_EndpointURL.png
[ManageKeys]: ./media/web-sites-dotnet-session-state-caching/CachingScreenshot_ManageAccessKeys.png

