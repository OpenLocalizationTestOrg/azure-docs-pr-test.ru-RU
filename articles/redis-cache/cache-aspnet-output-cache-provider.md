---
title: "aaaCache поставщика кэша вывода ASP.NET"
description: "Дополнительные сведения о том, как toocache вывода страницы ASP.NET с помощью кэша Azure Redis"
services: redis-cache
documentationcenter: na
author: steved0x
manager: douge
editor: tysonn
ms.assetid: 78469a66-0829-484f-8660-b2598ec60fbf
ms.service: cache
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: cache-redis
ms.workload: tbd
ms.date: 02/14/2017
ms.author: sdanie
ms.openlocfilehash: fc38cc657604b351f55ad8febac383783ac29700
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a><span data-ttu-id="727a1-103">Поставщик кэша вывода ASP.NET для кэша Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="727a1-103">ASP.NET Output Cache Provider for Azure Redis Cache</span></span>
<span data-ttu-id="727a1-104">Hello поставщика кэша вывода Redis представляет собой механизм хранения вне процесса для данных кэша вывода.</span><span class="sxs-lookup"><span data-stu-id="727a1-104">hello Redis Output Cache Provider is an out-of-process storage mechanism for output cache data.</span></span> <span data-ttu-id="727a1-105">Эти данные предназначены специально для полных HTTP-ответов (кэширование вывода страниц).</span><span class="sxs-lookup"><span data-stu-id="727a1-105">This data is specifically for full HTTP responses (page output caching).</span></span> <span data-ttu-id="727a1-106">Поставщик Hello подключается hello новой точке поставщика кэша вывода расширяемости, появившихся в ASP.NET 4.</span><span class="sxs-lookup"><span data-stu-id="727a1-106">hello provider plugs into hello new output cache provider extensibility point that was introduced in ASP.NET 4.</span></span>

<span data-ttu-id="727a1-107">Здравствуйте toouse поставщика кэша вывода Redis, сначала необходимо настроить кэш и затем настроить приложение ASP.NET с использованием пакета hello Redis NuGet поставщика кэша вывода.</span><span class="sxs-lookup"><span data-stu-id="727a1-107">toouse hello Redis Output Cache Provider, first configure your cache, and then configure your ASP.NET application using hello Redis Output Cache Provider NuGet package.</span></span> <span data-ttu-id="727a1-108">В этом разделе содержатся рекомендации по настройке вашего приложения toouse hello поставщика кэша вывода Redis.</span><span class="sxs-lookup"><span data-stu-id="727a1-108">This topic provides guidance on configuring your application toouse hello Redis Output Cache Provider.</span></span> <span data-ttu-id="727a1-109">Дополнительные сведения о создании и настройке экземпляра кэша Redis для Azure см. в разделе [Создание кэша](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="727a1-109">For more information about creating and configuring an Azure Redis Cache instance, see [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

## <a name="store-aspnet-page-output-in-hello-cache"></a><span data-ttu-id="727a1-110">Сохранение вывода страниц ASP.NET в кэше hello</span><span class="sxs-lookup"><span data-stu-id="727a1-110">Store ASP.NET page output in hello cache</span></span>
<span data-ttu-id="727a1-111">Щелкните tooconfigure клиентское приложение в Visual Studio с использованием пакета кэша NuGet состояний сеанса Redis hello, **диспетчера пакетов NuGet**, **консоль диспетчера пакетов** из hello **средства** меню.</span><span class="sxs-lookup"><span data-stu-id="727a1-111">tooconfigure a client application in Visual Studio using hello Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>

<span data-ttu-id="727a1-112">Выполнения hello следующую команду из hello `Package Manager Console` окна.</span><span class="sxs-lookup"><span data-stu-id="727a1-112">Run hello following command from hello `Package Manager Console` window.</span></span>
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

<span data-ttu-id="727a1-113">пакет Redis NuGet поставщика кэша вывода Hello имеет зависимость от пакета StackExchange.Redis.StrongName hello.</span><span class="sxs-lookup"><span data-stu-id="727a1-113">hello Redis Output Cache Provider NuGet package has a dependency on hello StackExchange.Redis.StrongName package.</span></span> <span data-ttu-id="727a1-114">Если отсутствует пакет StackExchange.Redis.StrongName hello в проекте, он устанавливается.</span><span class="sxs-lookup"><span data-stu-id="727a1-114">If hello StackExchange.Redis.StrongName package is not present in your project, it is installed.</span></span> <span data-ttu-id="727a1-115">Дополнительные сведения о пакете hello Redis NuGet поставщика кэша вывода см. в разделе hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) страница NuGet.</span><span class="sxs-lookup"><span data-stu-id="727a1-115">For more information about hello Redis Output Cache Provider NuGet package, see hello [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet page.</span></span>

>[!NOTE]
><span data-ttu-id="727a1-116">В дополнение toohello со строгими именами пакета StackExchange.Redis.StrongName имеется также hello StackExchange.Redis без строгого имени версии.</span><span class="sxs-lookup"><span data-stu-id="727a1-116">In addition toohello strong-named StackExchange.Redis.StrongName package, there is also hello StackExchange.Redis non-strong-named version.</span></span> <span data-ttu-id="727a1-117">Если проект использует hello без строгого имени версию StackExchange.Redis необходимо удалить ее, в противном случае можно получить конфликтов имен в проекте.</span><span class="sxs-lookup"><span data-stu-id="727a1-117">If your project is using hello non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span></span> <span data-ttu-id="727a1-118">Дополнительные сведения об этих пакетах см. в разделе [Настройка клиентов кэша .NET](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span><span class="sxs-lookup"><span data-stu-id="727a1-118">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>
>
>

<span data-ttu-id="727a1-119">Hello NuGet пакет загружает и добавляет hello требуется сборка ссылается на и добавляет следующий раздел в файл web.config hello.</span><span class="sxs-lookup"><span data-stu-id="727a1-119">hello NuGet package downloads and adds hello required assembly references and adds hello following section into your web.config file.</span></span> <span data-ttu-id="727a1-120">Этот раздел содержит hello требуемую конфигурацию приложения hello toouse поставщика кэша вывода Redis в ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="727a1-120">This section contains hello required configuration for your ASP.NET application toouse hello Redis Output Cache Provider.</span></span>

```xml
<caching>
  <outputCachedefault Provider="MyRedisOutputCache">
    <providers>
      <!--
      <add name="MyRedisOutputCache"
        host = "127.0.0.1" [String]
        port = "" [number]
        accessKey = "" [String]
        ssl = "false" [true|false]
        databaseId = "0" [number]
        applicationName = "" [String]
        connectionTimeoutInMilliseconds = "5000" [number]
        operationTimeoutInMilliseconds = "5000" [number]
      />
      -->
      <add name="MyRedisOutputCache" type="Microsoft.Web.Redis.RedisOutputCacheProvider" host="127.0.0.1" accessKey="" ssl="false"/>
    </providers>
  </outputCache>
</caching>
```

<span data-ttu-id="727a1-121">раздел содержит пример hello атрибутов и параметров для каждого атрибута в комментарий Hello.</span><span class="sxs-lookup"><span data-stu-id="727a1-121">hello commented section provides an example of hello attributes and sample settings for each attribute.</span></span>

<span data-ttu-id="727a1-122">Настройте атрибуты hello hello значениями из раздела кэша на портале Microsoft Azure hello и hello другие значения в случае необходимости.</span><span class="sxs-lookup"><span data-stu-id="727a1-122">Configure hello attributes with hello values from your cache blade in hello Microsoft Azure portal, and configure hello other values as desired.</span></span> <span data-ttu-id="727a1-123">Инструкции по доступу к свойствам кэша см. в разделе [Настройка параметров кэша Redis](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="727a1-123">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

* <span data-ttu-id="727a1-124">**host** — укажите конечную точку кэша.</span><span class="sxs-lookup"><span data-stu-id="727a1-124">**host** – specify your cache endpoint.</span></span>
* <span data-ttu-id="727a1-125">**порт** — использовать порт не SSL или порт SSL, в зависимости от параметров ssl hello.</span><span class="sxs-lookup"><span data-stu-id="727a1-125">**port** – use either your non-SSL port or your SSL port, depending on hello ssl settings.</span></span>
* <span data-ttu-id="727a1-126">**accessKey** — использовать либо hello первичный или вторичный ключ кэша.</span><span class="sxs-lookup"><span data-stu-id="727a1-126">**accessKey** – use either hello primary or secondary key for your cache.</span></span>
* <span data-ttu-id="727a1-127">**SSL** — значение true, если toosecure взаимодействий кэша/клиента с помощью ssl, в противном случае — значение false.</span><span class="sxs-lookup"><span data-stu-id="727a1-127">**ssl** – true if you want toosecure cache/client communications with ssl; otherwise false.</span></span> <span data-ttu-id="727a1-128">Быть убедиться, что toospecify hello правильный порт.</span><span class="sxs-lookup"><span data-stu-id="727a1-128">Be sure toospecify hello correct port.</span></span>
  * <span data-ttu-id="727a1-129">Hello не SSL-порт отключен по умолчанию для нового кэша.</span><span class="sxs-lookup"><span data-stu-id="727a1-129">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="727a1-130">Укажите значение true для этого параметра toouse hello порт SSL.</span><span class="sxs-lookup"><span data-stu-id="727a1-130">Specify true for this setting toouse hello SSL port.</span></span> <span data-ttu-id="727a1-131">Дополнительные сведения о включении порта без поддержки SSL hello см. в разделе hello [порты доступа](cache-configure.md#access-ports) раздела hello [настройте кэш](cache-configure.md) раздела.</span><span class="sxs-lookup"><span data-stu-id="727a1-131">For more information about enabling hello non-SSL port, see hello [Access Ports](cache-configure.md#access-ports) section in hello [Configure a cache](cache-configure.md) topic.</span></span>
* <span data-ttu-id="727a1-132">**databaseId** — Specified toouse какие базы данных для кэширования выходных данных.</span><span class="sxs-lookup"><span data-stu-id="727a1-132">**databaseId** – Specified which database toouse for cache output data.</span></span> <span data-ttu-id="727a1-133">Если не указан, используется значение по умолчанию hello 0.</span><span class="sxs-lookup"><span data-stu-id="727a1-133">If not specified, hello default value of 0 is used.</span></span>
* <span data-ttu-id="727a1-134">**applicationName** — ключи хранятся в кэше Redis как `<AppName>_<SessionId>_Data`.</span><span class="sxs-lookup"><span data-stu-id="727a1-134">**applicationName** – Keys are stored in redis as `<AppName>_<SessionId>_Data`.</span></span> <span data-ttu-id="727a1-135">Такая схема именования включает несколько приложений tooshare hello таким же ключом.</span><span class="sxs-lookup"><span data-stu-id="727a1-135">This naming scheme enables multiple applications tooshare hello same key.</span></span> <span data-ttu-id="727a1-136">Этот параметр — необязательный, и, если для него не указано другое значение, используется значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="727a1-136">This parameter is optional and if you do not provide it a default value is used.</span></span>
* <span data-ttu-id="727a1-137">**connectionTimeoutInMilliseconds** — этот параметр позволяет connectTimeout hello toooverride параметр в клиенте StackExchange.Redis hello.</span><span class="sxs-lookup"><span data-stu-id="727a1-137">**connectionTimeoutInMilliseconds** – This setting allows you toooverride hello connectTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="727a1-138">Если не указан, используется hello connectTimeout по умолчанию 5000.</span><span class="sxs-lookup"><span data-stu-id="727a1-138">If not specified, hello default connectTimeout setting of 5000 is used.</span></span> <span data-ttu-id="727a1-139">Дополнительную информацию см. в статье [Модель конфигурации StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="727a1-139">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>
* <span data-ttu-id="727a1-140">**operationTimeoutInMilliseconds** — этот параметр позволяет syncTimeout hello toooverride параметр в клиенте StackExchange.Redis hello.</span><span class="sxs-lookup"><span data-stu-id="727a1-140">**operationTimeoutInMilliseconds** – This setting allows you toooverride hello syncTimeout setting in hello StackExchange.Redis client.</span></span> <span data-ttu-id="727a1-141">Если не указан, используется hello syncTimeout по умолчанию 1000.</span><span class="sxs-lookup"><span data-stu-id="727a1-141">If not specified, hello default syncTimeout setting of 1000 is used.</span></span> <span data-ttu-id="727a1-142">Дополнительную информацию см. в статье [Модель конфигурации StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="727a1-142">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>

<span data-ttu-id="727a1-143">Добавьте страницу OutputCache директив tooeach, для которого вы хотите toocache hello вывода.</span><span class="sxs-lookup"><span data-stu-id="727a1-143">Add an OutputCache directive tooeach page for which you wish toocache hello output.</span></span>

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

<span data-ttu-id="727a1-144">В предыдущем примере hello hello страницы данных остается в кэше hello в кэше 60 секунд, а для каждой комбинации параметров кэшируются разные версии страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="727a1-144">In hello previous example, hello cached page data remains in hello cache for 60 seconds, and a different version of hello page is cached for each parameter combination.</span></span> <span data-ttu-id="727a1-145">Дополнительные сведения о директиве OutputCache hello. в разделе [ @OutputCache ](http://go.microsoft.com/fwlink/?linkid=320837).</span><span class="sxs-lookup"><span data-stu-id="727a1-145">For more information about hello OutputCache directive, see [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span></span>

<span data-ttu-id="727a1-146">После выполнения этих действий, приложение будет hello toouse настроенного поставщика кэша вывода Redis.</span><span class="sxs-lookup"><span data-stu-id="727a1-146">Once these steps are performed, your application is configured toouse hello Redis Output Cache Provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="727a1-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="727a1-147">Next steps</span></span>
<span data-ttu-id="727a1-148">Извлечение hello [поставщика состояний сеансов ASP.NET для кэша Azure Redis](cache-aspnet-session-state-provider.md).</span><span class="sxs-lookup"><span data-stu-id="727a1-148">Check out hello [ASP.NET Session State Provider for Azure Redis Cache](cache-aspnet-session-state-provider.md).</span></span>

