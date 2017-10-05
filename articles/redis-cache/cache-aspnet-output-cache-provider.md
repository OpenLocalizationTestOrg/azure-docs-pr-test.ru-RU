---
title: "Кэширование поставщика кэша вывода ASP.NET"
description: "Информация о том, как выходные данные страницы ASP.NET кэшируются с помощью кэша Redis для Azure."
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
ms.openlocfilehash: 845f25637a0e48460fc76c1ee36060274b3cec38
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="aspnet-output-cache-provider-for-azure-redis-cache"></a><span data-ttu-id="483c3-103">Поставщик кэша вывода ASP.NET для кэша Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="483c3-103">ASP.NET Output Cache Provider for Azure Redis Cache</span></span>
<span data-ttu-id="483c3-104">Поставщик кэша вывода Redis представляет собой механизм внепроцессного хранения для выходных данных кэширования.</span><span class="sxs-lookup"><span data-stu-id="483c3-104">The Redis Output Cache Provider is an out-of-process storage mechanism for output cache data.</span></span> <span data-ttu-id="483c3-105">Эти данные предназначены специально для полных HTTP-ответов (кэширование вывода страниц).</span><span class="sxs-lookup"><span data-stu-id="483c3-105">This data is specifically for full HTTP responses (page output caching).</span></span> <span data-ttu-id="483c3-106">Поставщик подключается к новой точке расширения поставщика вывода кэша, которая появилась в ASP.NET 4.</span><span class="sxs-lookup"><span data-stu-id="483c3-106">The provider plugs into the new output cache provider extensibility point that was introduced in ASP.NET 4.</span></span>

<span data-ttu-id="483c3-107">Чтобы использовать поставщик кэша вывода Redis, сначала настройте кэш, а затем приложение ASP.NET, используя пакет NuGet поставщика кэша вывода Redis.</span><span class="sxs-lookup"><span data-stu-id="483c3-107">To use the Redis Output Cache Provider, first configure your cache, and then configure your ASP.NET application using the Redis Output Cache Provider NuGet package.</span></span> <span data-ttu-id="483c3-108">Этот раздел содержит информацию о том, как настроить приложение, чтобы оно использовало поставщик кэша вывода Redis.</span><span class="sxs-lookup"><span data-stu-id="483c3-108">This topic provides guidance on configuring your application to use the Redis Output Cache Provider.</span></span> <span data-ttu-id="483c3-109">Дополнительные сведения о создании и настройке экземпляра кэша Redis для Azure см. в разделе [Создание кэша](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="483c3-109">For more information about creating and configuring an Azure Redis Cache instance, see [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

## <a name="store-aspnet-page-output-in-the-cache"></a><span data-ttu-id="483c3-110">Сохранение выходных данных страницы ASP.NET в кэше</span><span class="sxs-lookup"><span data-stu-id="483c3-110">Store ASP.NET page output in the cache</span></span>
<span data-ttu-id="483c3-111">Чтобы настроить клиентское приложение в Visual Studio, используя пакет NuGet RedisCacheSessionState, в меню **Сервис** выберите **Диспетчер пакетов NuGet** > **Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="483c3-111">To configure a client application in Visual Studio using the Redis Cache Session State NuGet package, click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>

<span data-ttu-id="483c3-112">Выполните следующую команду в окне `Package Manager Console`:</span><span class="sxs-lookup"><span data-stu-id="483c3-112">Run the following command from the `Package Manager Console` window.</span></span>
    
```
Install-Package Microsoft.Web.RedisOutputCacheProvider
```

<span data-ttu-id="483c3-113">Пакет NuGet поставщика кэша вывода Redis имеет зависимость от пакета StackExchange.Redis.StrongName.</span><span class="sxs-lookup"><span data-stu-id="483c3-113">The Redis Output Cache Provider NuGet package has a dependency on the StackExchange.Redis.StrongName package.</span></span> <span data-ttu-id="483c3-114">Если в проекте отсутствует пакет StackExchange.Redis.StrongName, то он будет установлен.</span><span class="sxs-lookup"><span data-stu-id="483c3-114">If the StackExchange.Redis.StrongName package is not present in your project, it is installed.</span></span> <span data-ttu-id="483c3-115">Дополнительные сведения о пакете NuGet RedisOutputCacheProvider см. на странице NuGet [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/).</span><span class="sxs-lookup"><span data-stu-id="483c3-115">For more information about the Redis Output Cache Provider NuGet package, see the [RedisOutputCacheProvider](https://www.nuget.org/packages/Microsoft.Web.RedisOutputCacheProvider/) NuGet page.</span></span>

>[!NOTE]
><span data-ttu-id="483c3-116">Помимо пакета со строгим именем StackExchange.Redis.StrongName существует также версия с нестрогим именем StackExchange.Redis.</span><span class="sxs-lookup"><span data-stu-id="483c3-116">In addition to the strong-named StackExchange.Redis.StrongName package, there is also the StackExchange.Redis non-strong-named version.</span></span> <span data-ttu-id="483c3-117">Если проект использует версию с нестрогим именем StackExchange.Redis, то необходимо удалить ее. В противном случае в проекте возникнет конфликт имен.</span><span class="sxs-lookup"><span data-stu-id="483c3-117">If your project is using the non-strong-named StackExchange.Redis version you must uninstall it, otherwise you get naming conflicts in your project.</span></span> <span data-ttu-id="483c3-118">Дополнительные сведения об этих пакетах см. в разделе [Настройка клиентов кэша .NET](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span><span class="sxs-lookup"><span data-stu-id="483c3-118">For more information about these packages, see [Configure .NET cache clients](cache-dotnet-how-to-use-azure-redis-cache.md#configure-the-cache-clients).</span></span>
>
>

<span data-ttu-id="483c3-119">Пакет NuGet скачивает и добавляет требуемые ссылки на сборку и добавляет следующий раздел в файл web.config.</span><span class="sxs-lookup"><span data-stu-id="483c3-119">The NuGet package downloads and adds the required assembly references and adds the following section into your web.config file.</span></span> <span data-ttu-id="483c3-120">Этот раздел содержит необходимые настройки для приложения ASP.NET, позволяющие использовать поставщик кэша вывода Redis.</span><span class="sxs-lookup"><span data-stu-id="483c3-120">This section contains the required configuration for your ASP.NET application to use the Redis Output Cache Provider.</span></span>

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

<span data-ttu-id="483c3-121">Раздел с комментариями содержит пример атрибутов и возможные настройки для каждого из них.</span><span class="sxs-lookup"><span data-stu-id="483c3-121">The commented section provides an example of the attributes and sample settings for each attribute.</span></span>

<span data-ttu-id="483c3-122">Задайте для атрибутов значения из колонки своего кэша на портале Microsoft Azure и настройте другие параметры по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="483c3-122">Configure the attributes with the values from your cache blade in the Microsoft Azure portal, and configure the other values as desired.</span></span> <span data-ttu-id="483c3-123">Инструкции по доступу к свойствам кэша см. в разделе [Настройка параметров кэша Redis](cache-configure.md#configure-redis-cache-settings).</span><span class="sxs-lookup"><span data-stu-id="483c3-123">For instructions on accessing your cache properties, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

* <span data-ttu-id="483c3-124">**host** — укажите конечную точку кэша.</span><span class="sxs-lookup"><span data-stu-id="483c3-124">**host** – specify your cache endpoint.</span></span>
* <span data-ttu-id="483c3-125">**port** — используйте порт без или с SSL в зависимости от параметров SSL.</span><span class="sxs-lookup"><span data-stu-id="483c3-125">**port** – use either your non-SSL port or your SSL port, depending on the ssl settings.</span></span>
* <span data-ttu-id="483c3-126">**accessKey** — используйте для кэша первичный или вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="483c3-126">**accessKey** – use either the primary or secondary key for your cache.</span></span>
* <span data-ttu-id="483c3-127">**ssl** — задайте значение true, если нужно обеспечить безопасный обмен данными между клиентом и кэшем с помощью SSL. В противном случае задайте значение false.</span><span class="sxs-lookup"><span data-stu-id="483c3-127">**ssl** – true if you want to secure cache/client communications with ssl; otherwise false.</span></span> <span data-ttu-id="483c3-128">Обязательно укажите правильный порт.</span><span class="sxs-lookup"><span data-stu-id="483c3-128">Be sure to specify the correct port.</span></span>
  * <span data-ttu-id="483c3-129">Для новых кэшей не SSL порт по умолчанию запрещен.</span><span class="sxs-lookup"><span data-stu-id="483c3-129">The non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="483c3-130">Если вы хотите, чтобы для этого параметра использовался SSL-порт, укажите значение true.</span><span class="sxs-lookup"><span data-stu-id="483c3-130">Specify true for this setting to use the SSL port.</span></span> <span data-ttu-id="483c3-131">Дополнительные сведения о том, как настроить использование порта без SSL, см. в статье [Настройка кэша](cache-configure.md#access-ports) в разделе [Порты доступа](cache-configure.md).</span><span class="sxs-lookup"><span data-stu-id="483c3-131">For more information about enabling the non-SSL port, see the [Access Ports](cache-configure.md#access-ports) section in the [Configure a cache](cache-configure.md) topic.</span></span>
* <span data-ttu-id="483c3-132">**databaseId** — укажите базу данных, которую необходимо использовать для выходных данных кэша.</span><span class="sxs-lookup"><span data-stu-id="483c3-132">**databaseId** – Specified which database to use for cache output data.</span></span> <span data-ttu-id="483c3-133">Если значение в этом поле не задано, по умолчанию используется значение 0.</span><span class="sxs-lookup"><span data-stu-id="483c3-133">If not specified, the default value of 0 is used.</span></span>
* <span data-ttu-id="483c3-134">**applicationName** — ключи хранятся в кэше Redis как `<AppName>_<SessionId>_Data`.</span><span class="sxs-lookup"><span data-stu-id="483c3-134">**applicationName** – Keys are stored in redis as `<AppName>_<SessionId>_Data`.</span></span> <span data-ttu-id="483c3-135">Такая схема именования позволяет нескольким приложениям совместно использовать один ключ.</span><span class="sxs-lookup"><span data-stu-id="483c3-135">This naming scheme enables multiple applications to share the same key.</span></span> <span data-ttu-id="483c3-136">Этот параметр — необязательный, и, если для него не указано другое значение, используется значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="483c3-136">This parameter is optional and if you do not provide it a default value is used.</span></span>
* <span data-ttu-id="483c3-137">**connectionTimeoutInMilliseconds** — этот параметр позволяет переопределить параметр connectTimeout в клиенте StackExchange.Redis.</span><span class="sxs-lookup"><span data-stu-id="483c3-137">**connectionTimeoutInMilliseconds** – This setting allows you to override the connectTimeout setting in the StackExchange.Redis client.</span></span> <span data-ttu-id="483c3-138">Если для параметра connectTimeout значение не указано, по умолчанию используется значение 5000.</span><span class="sxs-lookup"><span data-stu-id="483c3-138">If not specified, the default connectTimeout setting of 5000 is used.</span></span> <span data-ttu-id="483c3-139">Дополнительную информацию см. в статье [Модель конфигурации StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="483c3-139">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>
* <span data-ttu-id="483c3-140">**operationTimeoutInMilliseconds** — этот параметр позволяет переопределить параметр syncTimeout в клиенте StackExchange.Redis.</span><span class="sxs-lookup"><span data-stu-id="483c3-140">**operationTimeoutInMilliseconds** – This setting allows you to override the syncTimeout setting in the StackExchange.Redis client.</span></span> <span data-ttu-id="483c3-141">Если для параметра syncTimeout значение не указано, по умолчанию используется значение 1000.</span><span class="sxs-lookup"><span data-stu-id="483c3-141">If not specified, the default syncTimeout setting of 1000 is used.</span></span> <span data-ttu-id="483c3-142">Дополнительную информацию см. в статье [Модель конфигурации StackExchange.Redis](http://go.microsoft.com/fwlink/?LinkId=398705).</span><span class="sxs-lookup"><span data-stu-id="483c3-142">For more information, see [StackExchange.Redis configuration model](http://go.microsoft.com/fwlink/?LinkId=398705).</span></span>

<span data-ttu-id="483c3-143">Добавьте директиву OutputCache для каждой страницы, для которой требуется кэшировать выходные данные.</span><span class="sxs-lookup"><span data-stu-id="483c3-143">Add an OutputCache directive to each page for which you wish to cache the output.</span></span>

```
<%@ OutputCache Duration="60" VaryByParam="*" %>
```

<span data-ttu-id="483c3-144">В предыдущем примере кэшированные данные страницы остаются в кэше в течение 60 секунд, а для каждой комбинации параметров кэшируется другая версия страницы.</span><span class="sxs-lookup"><span data-stu-id="483c3-144">In the previous example, the cached page data remains in the cache for 60 seconds, and a different version of the page is cached for each parameter combination.</span></span> <span data-ttu-id="483c3-145">Для получения дополнительной информации о директиве OutputCache ознакомьтесь с [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span><span class="sxs-lookup"><span data-stu-id="483c3-145">For more information about the OutputCache directive, see [@OutputCache](http://go.microsoft.com/fwlink/?linkid=320837).</span></span>

<span data-ttu-id="483c3-146">Когда эти действия будут выполнены, приложение будет соответствующим образом настроено и сможет использовать поставщик кэша вывода Redis.</span><span class="sxs-lookup"><span data-stu-id="483c3-146">Once these steps are performed, your application is configured to use the Redis Output Cache Provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="483c3-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="483c3-147">Next steps</span></span>
<span data-ttu-id="483c3-148">Посетите страницу [Поставщик состояний сеансов ASP.NET для кэша Redis для Azure](cache-aspnet-session-state-provider.md).</span><span class="sxs-lookup"><span data-stu-id="483c3-148">Check out the [ASP.NET Session State Provider for Azure Redis Cache](cache-aspnet-session-state-provider.md).</span></span>

