---
title: "aaaHow tooUse кэша Redis для Azure | Документы Microsoft"
description: "Узнайте, как tooimprove hello производительности приложений Azure с помощью кэша Azure Redis"
services: redis-cache,app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: c502f74c-44de-4087-8303-1b1f43da12d5
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/27/2017
ms.author: sdanie
ms.openlocfilehash: 763d70c10972eec9a1885969e8da5bf1c4084727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-redis-cache"></a><span data-ttu-id="b4daa-103">Как tooUse Redis для Azure кэша</span><span class="sxs-lookup"><span data-stu-id="b4daa-103">How tooUse Azure Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b4daa-104">.NET</span><span class="sxs-lookup"><span data-stu-id="b4daa-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="b4daa-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b4daa-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="b4daa-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="b4daa-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="b4daa-107">Java</span><span class="sxs-lookup"><span data-stu-id="b4daa-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="b4daa-108">Python</span><span class="sxs-lookup"><span data-stu-id="b4daa-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="b4daa-109">В этом руководстве показано, как tooget запущена с помощью **кэш Azure Redis**.</span><span class="sxs-lookup"><span data-stu-id="b4daa-109">This guide shows you how tooget started using **Azure Redis Cache**.</span></span> <span data-ttu-id="b4daa-110">Кэш Redis Microsoft Azure основан на hello открытым исходным кодом кэша Redis.</span><span class="sxs-lookup"><span data-stu-id="b4daa-110">Microsoft Azure Redis Cache is based on hello popular open source Redis Cache.</span></span> <span data-ttu-id="b4daa-111">Он предоставляет доступ к tooa безопасного выделенному кэшу Redis, управляемый корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="b4daa-111">It gives you access tooa secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="b4daa-112">Кэш, созданный с использованием кэша Azure Redis, доступен из любого приложения в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b4daa-112">A cache created using Azure Redis Cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="b4daa-113">Кэш Microsoft Azure Redis доступна hello следующие уровни:</span><span class="sxs-lookup"><span data-stu-id="b4daa-113">Microsoft Azure Redis Cache is available in hello following tiers:</span></span>

* <span data-ttu-id="b4daa-114">**Basic** — один узел.</span><span class="sxs-lookup"><span data-stu-id="b4daa-114">**Basic** – Single node.</span></span> <span data-ttu-id="b4daa-115">Несколько размеров too53 Гбайт.</span><span class="sxs-lookup"><span data-stu-id="b4daa-115">Multiple sizes up too53 GB.</span></span>
* <span data-ttu-id="b4daa-116">**Стандартный** — два узла: основной и реплика.</span><span class="sxs-lookup"><span data-stu-id="b4daa-116">**Standard** – Two-node Primary/Replica.</span></span> <span data-ttu-id="b4daa-117">Несколько размеров too53 Гбайт.</span><span class="sxs-lookup"><span data-stu-id="b4daa-117">Multiple sizes up too53 GB.</span></span> <span data-ttu-id="b4daa-118">СОГЛАШЕНИЕ ОБ УРОВНЕ ОБСЛУЖИВАНИЯ 99,9 %.</span><span class="sxs-lookup"><span data-stu-id="b4daa-118">99.9% SLA.</span></span>
* <span data-ttu-id="b4daa-119">**Premium** — двумя узлами первичный/реплика с вверх too10 сегментов.</span><span class="sxs-lookup"><span data-stu-id="b4daa-119">**Premium** – Two-node Primary/Replica with up too10 shards.</span></span> <span data-ttu-id="b4daa-120">Несколько размеров от 6 ГБ too530 ГБ.</span><span class="sxs-lookup"><span data-stu-id="b4daa-120">Multiple sizes from 6 GB too530 GB.</span></span> <span data-ttu-id="b4daa-121">Все функции уровня "Стандартный", а также дополнительные функции, включая поддержку [кластера Redis](cache-how-to-premium-clustering.md), [сохраняемости Redis](cache-how-to-premium-persistence.md) и [виртуальной сети Azure](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="b4daa-121">All Standard tier features and more including support for [Redis cluster](cache-how-to-premium-clustering.md), [Redis persistence](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="b4daa-122">СОГЛАШЕНИЕ ОБ УРОВНЕ ОБСЛУЖИВАНИЯ 99,9 %.</span><span class="sxs-lookup"><span data-stu-id="b4daa-122">99.9% SLA.</span></span>

<span data-ttu-id="b4daa-123">Каждый уровень отличается доступными возможностями и ценой.</span><span class="sxs-lookup"><span data-stu-id="b4daa-123">Each tier differs in terms of features and pricing.</span></span> <span data-ttu-id="b4daa-124">Дополнительные сведения о ценах на кэш см. на [этой странице][Cache Pricing Details].</span><span class="sxs-lookup"><span data-stu-id="b4daa-124">For information on pricing, see [Cache Pricing Details][Cache Pricing Details].</span></span>

<span data-ttu-id="b4daa-125">В этом руководстве показано, как toouse hello [StackExchange.Redis] [ StackExchange.Redis] клиента с помощью C\# кода.</span><span class="sxs-lookup"><span data-stu-id="b4daa-125">This guide shows you how toouse hello [StackExchange.Redis][StackExchange.Redis] client using C\# code.</span></span> <span data-ttu-id="b4daa-126">Hello сценарии включают **создания и настройки кэша**, **настройке клиентов кэша**, и **добавления и удаления объектов из кэша hello**.</span><span class="sxs-lookup"><span data-stu-id="b4daa-126">hello scenarios covered include **creating and configuring a cache**, **configuring cache clients**, and **adding and removing objects from hello cache**.</span></span> <span data-ttu-id="b4daa-127">Дополнительные сведения об использовании кэша Redis для Azure см. в разделе [Дальнейшие действия][Next Steps].</span><span class="sxs-lookup"><span data-stu-id="b4daa-127">For more information on using Azure Redis Cache, see [Next Steps][Next Steps].</span></span> <span data-ttu-id="b4daa-128">Пошаговый учебник построения ASP.NET MVC, веб-приложения в кэш Redis см. в разделе [как веб-приложения в кэш Redis toocreate](cache-web-app-howto.md).</span><span class="sxs-lookup"><span data-stu-id="b4daa-128">For a step-by-step tutorial of building an ASP.NET MVC web app with Redis Cache, see [How toocreate a Web App with Redis Cache](cache-web-app-howto.md).</span></span>

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a><span data-ttu-id="b4daa-129">Начало работы с кэшем Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="b4daa-129">Get Started with Azure Redis Cache</span></span>
<span data-ttu-id="b4daa-130">Начать работу с кэшем Azure Redis просто.</span><span class="sxs-lookup"><span data-stu-id="b4daa-130">Getting started with Azure Redis Cache is easy.</span></span> <span data-ttu-id="b4daa-131">tooget к работе, можно подготовить и настройте кэш.</span><span class="sxs-lookup"><span data-stu-id="b4daa-131">tooget started, you provision and configure a cache.</span></span> <span data-ttu-id="b4daa-132">Далее следует настроить клиенты кэша hello для доступа к кэшем hello.</span><span class="sxs-lookup"><span data-stu-id="b4daa-132">Next, you configure hello cache clients so they can access hello cache.</span></span> <span data-ttu-id="b4daa-133">После настройки клиентов кэша hello можно начать работу с ними.</span><span class="sxs-lookup"><span data-stu-id="b4daa-133">Once hello cache clients are configured, you can begin working with them.</span></span>

* <span data-ttu-id="b4daa-134">[Создание кэша hello][Create hello cache]</span><span class="sxs-lookup"><span data-stu-id="b4daa-134">[Create hello cache][Create hello cache]</span></span>
* <span data-ttu-id="b4daa-135">[Настройка клиентов кэша hello][Configure hello cache clients]</span><span class="sxs-lookup"><span data-stu-id="b4daa-135">[Configure hello cache clients][Configure hello cache clients]</span></span>

<a name="create-cache"></a>

## <a name="create-a-cache"></a><span data-ttu-id="b4daa-136">Создание кэша</span><span class="sxs-lookup"><span data-stu-id="b4daa-136">Create a cache</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="tooaccess-your-cache-after-its-created"></a><span data-ttu-id="b4daa-137">tooaccess кэша после его создания</span><span class="sxs-lookup"><span data-stu-id="b4daa-137">tooaccess your cache after it's created</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="b4daa-138">Дополнительные сведения о настройке кэша см. в разделе [как tooconfigure кэш Azure Redis](cache-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b4daa-138">For more information about configuring your cache, see [How tooconfigure Azure Redis Cache](cache-configure.md).</span></span>

<a name="NuGet"></a>

## <a name="configure-hello-cache-clients"></a><span data-ttu-id="b4daa-139">Настройка клиентов кэша hello</span><span class="sxs-lookup"><span data-stu-id="b4daa-139">Configure hello cache clients</span></span>
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

<span data-ttu-id="b4daa-140">Когда клиентский проект настроен для кэширования, можно использовать hello методик, описанных в следующих разделах для работы с кэшем hello.</span><span class="sxs-lookup"><span data-stu-id="b4daa-140">Once your client project is configured for caching, you can use hello techniques described in hello following sections for working with your cache.</span></span>

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a><span data-ttu-id="b4daa-141">Работа с кэшами</span><span class="sxs-lookup"><span data-stu-id="b4daa-141">Working with Caches</span></span>
<span data-ttu-id="b4daa-142">Hello в этом разделе описывается, как tooperform распространенные задачи с кэшем.</span><span class="sxs-lookup"><span data-stu-id="b4daa-142">hello steps in this section describe how tooperform common tasks with Cache.</span></span>

* <span data-ttu-id="b4daa-143">[Подключение toohello кэша][Connect toohello cache]</span><span class="sxs-lookup"><span data-stu-id="b4daa-143">[Connect toohello cache][Connect toohello cache]</span></span>
* <span data-ttu-id="b4daa-144">[Добавление и извлечение объектов из кэша hello][Add and retrieve objects from hello cache]</span><span class="sxs-lookup"><span data-stu-id="b4daa-144">[Add and retrieve objects from hello cache][Add and retrieve objects from hello cache]</span></span>
* [<span data-ttu-id="b4daa-145">Работа с объектами .NET в кэше hello</span><span class="sxs-lookup"><span data-stu-id="b4daa-145">Work with .NET objects in hello cache</span></span>](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-toohello-cache"></a><span data-ttu-id="b4daa-146">Подключение toohello кэша</span><span class="sxs-lookup"><span data-stu-id="b4daa-146">Connect toohello cache</span></span>
<span data-ttu-id="b4daa-147">tooprogrammatically работы с кэшем, требуется ссылка toohello кэша.</span><span class="sxs-lookup"><span data-stu-id="b4daa-147">tooprogrammatically work with a cache, you need a reference toohello cache.</span></span> <span data-ttu-id="b4daa-148">Добавьте следующие toohello начало любого файла, из которого требуется toouse hello StackExchange.Redis клиента tooaccess кэш Azure Redis hello.</span><span class="sxs-lookup"><span data-stu-id="b4daa-148">Add hello following toohello top of any file from which you want toouse hello StackExchange.Redis client tooaccess an Azure Redis Cache.</span></span>

    using StackExchange.Redis;

> [!NOTE]
> <span data-ttu-id="b4daa-149">Hello клиента StackExchange.Redis требуется платформа .NET Framework 4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="b4daa-149">hello StackExchange.Redis client requires .NET Framework 4 or higher.</span></span>
> 
> 

<span data-ttu-id="b4daa-150">Здравствуйте подключения toohello кэша Redis для Azure управляется hello `ConnectionMultiplexer` класса.</span><span class="sxs-lookup"><span data-stu-id="b4daa-150">hello connection toohello Azure Redis Cache is managed by hello `ConnectionMultiplexer` class.</span></span> <span data-ttu-id="b4daa-151">Этот класс должны быть общими и в клиентском приложении многократно и не обязательно toobe создан для каждой операции.</span><span class="sxs-lookup"><span data-stu-id="b4daa-151">This class should be shared and reused throughout your client application, and does not need toobe created on a per operation basis.</span></span> 

<span data-ttu-id="b4daa-152">tooconnect tooan кэша Redis для Azure и возвращаться подключенного экземпляра `ConnectionMultiplexer`, hello вызов статических `Connect` метод и передайте его в hello кэшировать конечную точку и ключ.</span><span class="sxs-lookup"><span data-stu-id="b4daa-152">tooconnect tooan Azure Redis Cache and be returned an instance of a connected `ConnectionMultiplexer`, call hello static `Connect` method and pass in hello cache endpoint and key.</span></span> <span data-ttu-id="b4daa-153">Используйте ключ hello, созданные из hello портал управления Azure как параметр password hello.</span><span class="sxs-lookup"><span data-stu-id="b4daa-153">Use hello key generated from hello Azure portal as hello password parameter.</span></span>

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> <span data-ttu-id="b4daa-154">Внимание! Никогда не храните учетные данные в исходном коде.</span><span class="sxs-lookup"><span data-stu-id="b4daa-154">Warning: Never store credentials in source code.</span></span> <span data-ttu-id="b4daa-155">tookeep этот простой пример, я отображения их в исходном коде hello.</span><span class="sxs-lookup"><span data-stu-id="b4daa-155">tookeep this sample simple, I’m showing them in hello source code.</span></span> <span data-ttu-id="b4daa-156">В разделе [как строки приложения и строк соединения работает] [ How Application Strings and Connection Strings Work] сведения о том, как toostore учетные данные.</span><span class="sxs-lookup"><span data-stu-id="b4daa-156">See [How Application Strings and Connection Strings Work][How Application Strings and Connection Strings Work] for information on how toostore credentials.</span></span>
> 
> 

<span data-ttu-id="b4daa-157">Если вы не хотите toouse SSL, установите `ssl=false` или пропустите hello `ssl` параметра.</span><span class="sxs-lookup"><span data-stu-id="b4daa-157">If you don't want toouse SSL, either set `ssl=false` or omit hello `ssl` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="b4daa-158">Hello не SSL-порт отключен по умолчанию для нового кэша.</span><span class="sxs-lookup"><span data-stu-id="b4daa-158">hello non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="b4daa-159">Инструкции по включению hello не SSL-порт. в разделе [порты доступа](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="b4daa-159">For instructions on enabling hello non-SSL port, see [Access Ports](cache-configure.md#access-ports).</span></span>
> 
> 

<span data-ttu-id="b4daa-160">Один из подходов toosharing `ConnectionMultiplexer` toohave статическое свойство, которое возвращает подключенный экземпляр, аналогичные toohello следующий пример является экземпляр приложения.</span><span class="sxs-lookup"><span data-stu-id="b4daa-160">One approach toosharing a `ConnectionMultiplexer` instance in your application is toohave a static property that returns a connected instance, similar toohello following example.</span></span> <span data-ttu-id="b4daa-161">Такой подход обеспечивает tooinitialize потокобезопасным способом только одного подключенного `ConnectionMultiplexer` экземпляра.</span><span class="sxs-lookup"><span data-stu-id="b4daa-161">This approach provides a thread-safe way tooinitialize only a single connected `ConnectionMultiplexer` instance.</span></span> <span data-ttu-id="b4daa-162">В этих примерах `abortConnect` является набор toofalse, это означает, что hello вызов завершается успешно, даже если не будет установлено подключение toohello кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="b4daa-162">In these examples `abortConnect` is set toofalse, which means that hello call succeeds even if a connection toohello Azure Redis Cache is not established.</span></span> <span data-ttu-id="b4daa-163">Одна важная особенность `ConnectionMultiplexer` — что автоматически восстанавливается подключение toohello кэша после hello проблемы в сети или по другим причинам не будут разрешены.</span><span class="sxs-lookup"><span data-stu-id="b4daa-163">One key feature of `ConnectionMultiplexer` is that it automatically restores connectivity toohello cache once hello network issue or other causes are resolved.</span></span>

    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        return ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");
    });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

<span data-ttu-id="b4daa-164">Дополнительные сведения по вариантам расширенных настроек соединения см. в статье [Модель конфигурации StackExchange.Redis][StackExchange.Redis configuration model].</span><span class="sxs-lookup"><span data-stu-id="b4daa-164">For more information on advanced connection configuration options, see [StackExchange.Redis configuration model][StackExchange.Redis configuration model].</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<span data-ttu-id="b4daa-165">После установления соединения hello вернуть базу данных кэша redis ссылки toohello, вызывающему Привет `ConnectionMultiplexer.GetDatabase` метод.</span><span class="sxs-lookup"><span data-stu-id="b4daa-165">Once hello connection is established, return a reference toohello redis cache database by calling hello `ConnectionMultiplexer.GetDatabase` method.</span></span> <span data-ttu-id="b4daa-166">Hello объект, возвращенный hello `GetDatabase` метод является облегченным сквозным объектом и не обязательно toobe хранятся.</span><span class="sxs-lookup"><span data-stu-id="b4daa-166">hello object returned from hello `GetDatabase` method is a lightweight pass-through object and does not need toobe stored.</span></span>

    // Connection refers tooa property that returns a ConnectionMultiplexer
    // as shown in hello previous example.
    IDatabase cache = Connection.GetDatabase();

    // Perform cache operations using hello cache object...
    // Simple put of integral data types into hello cache
    cache.StringSet("key1", "value");
    cache.StringSet("key2", 25);

    // Simple get of data types from hello cache
    string key1 = cache.StringGet("key1");
    int key2 = (int)cache.StringGet("key2");

<span data-ttu-id="b4daa-167">Кэшах Azure Redis имеется определенное количество баз данных (по умолчанию 16), которые могут быть toologically используется отдельный hello данных в кэше Redis.</span><span class="sxs-lookup"><span data-stu-id="b4daa-167">Azure Redis caches have a configurable number of databases (default of 16) that can be used toologically separate hello data within a Redis cache.</span></span> <span data-ttu-id="b4daa-168">Дополнительные сведения см. в разделах [What are Redis databases?](cache-configure.md#default-redis-server-configuration) (Что такое базы данных Redis) и [Конфигурация сервера Redis по умолчанию](cache-faq.md#what-are-redis-databases).</span><span class="sxs-lookup"><span data-stu-id="b4daa-168">For more information, see [What are Redis databases?](cache-faq.md#what-are-redis-databases) and [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span></span>

<span data-ttu-id="b4daa-169">Теперь, когда вы знаете, как экземпляр кэша Azure Redis tooan tooconnect и возврат toohello ссылки кэша базы данных, давайте взглянем на работе с кэшем hello.</span><span class="sxs-lookup"><span data-stu-id="b4daa-169">Now that you know how tooconnect tooan Azure Redis Cache instance and return a reference toohello cache database, let's look at working with hello cache.</span></span>

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-hello-cache"></a><span data-ttu-id="b4daa-170">Добавление и извлечение объектов из кэша hello</span><span class="sxs-lookup"><span data-stu-id="b4daa-170">Add and retrieve objects from hello cache</span></span>
<span data-ttu-id="b4daa-171">Элементы можно хранятся в и извлекаются из кэша с использованием hello `StringSet` и `StringGet` методы.</span><span class="sxs-lookup"><span data-stu-id="b4daa-171">Items can be stored in and retrieved from a cache by using hello `StringSet` and `StringGet` methods.</span></span>

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

<span data-ttu-id="b4daa-172">Redis хранилищ, большинство данных в виде строки Redis, а эти строки может содержать несколько типов данных, включая сериализованные двоичные данные, которые можно использовать при сохранении .NET объектов в кэше hello.</span><span class="sxs-lookup"><span data-stu-id="b4daa-172">Redis stores most data as Redis strings, but these strings can contain many types of data, including serialized binary data, which can be used when storing .NET objects in hello cache.</span></span>

<span data-ttu-id="b4daa-173">При вызове `StringGet`, hello объект существует, возвращается, и если оно отсутствует, `null` возвращается.</span><span class="sxs-lookup"><span data-stu-id="b4daa-173">When calling `StringGet`, if hello object exists, it is returned, and if it does not, `null` is returned.</span></span> <span data-ttu-id="b4daa-174">Если `null` возвращается, можно получить значение hello из hello необходимый источник данных и сохранить его в кэше hello для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="b4daa-174">If `null` is returned, you can retrieve hello value from hello desired data source and store it in hello cache for subsequent use.</span></span> <span data-ttu-id="b4daa-175">Этот шаблон использования называется hello отдельно от кэша шаблоном.</span><span class="sxs-lookup"><span data-stu-id="b4daa-175">This usage pattern is known as hello cache-aside pattern.</span></span>

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // hello item keyed by "key1" is not in hello cache. Obtain
        // it from hello desired data source and add it toohello cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

<span data-ttu-id="b4daa-176">Можно также использовать `RedisValue`, как показано в следующий пример hello.</span><span class="sxs-lookup"><span data-stu-id="b4daa-176">You can also use `RedisValue`, as shown in hello following example.</span></span> <span data-ttu-id="b4daa-177">`RedisValue` содержит неявные операторы для работы с целочисленными типами данных и могут быть полезны, если `null` — ожидаемое значение кэшированного элемента.</span><span class="sxs-lookup"><span data-stu-id="b4daa-177">`RedisValue` has implicit operators for working with integral data types, and can be useful if `null` is an expected value for a cached item.</span></span>


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


<span data-ttu-id="b4daa-178">срок годности hello toospecify элемента в кэше hello, используйте hello `TimeSpan` параметр `StringSet`.</span><span class="sxs-lookup"><span data-stu-id="b4daa-178">toospecify hello expiration of an item in hello cache, use hello `TimeSpan` parameter of `StringSet`.</span></span>

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-hello-cache"></a><span data-ttu-id="b4daa-179">Работа с объектами .NET в кэше hello</span><span class="sxs-lookup"><span data-stu-id="b4daa-179">Work with .NET objects in hello cache</span></span>
<span data-ttu-id="b4daa-180">Кэш Redis для Azure может кэшировать объекты .NET и примитивные типы данных, но прежде чем объект .NET можно будет сохранить в кэше, он должен быть сериализован.</span><span class="sxs-lookup"><span data-stu-id="b4daa-180">Azure Redis Cache can cache both .NET objects and primitive data types, but before a .NET object can be cached it must be serialized.</span></span> <span data-ttu-id="b4daa-181">Этой сериализации объекта .NET hello отвечает разработчик приложения hello и обеспечивает гибкость hello разработчика по выбору hello hello сериализатор.</span><span class="sxs-lookup"><span data-stu-id="b4daa-181">This .NET object serialization is hello responsibility of hello application developer, and gives hello developer flexibility in hello choice of hello serializer.</span></span>

<span data-ttu-id="b4daa-182">Один простой способ tooserialize объектов — toouse hello `JsonConvert` методы сериализации в [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) и сериализации tooand из JSON.</span><span class="sxs-lookup"><span data-stu-id="b4daa-182">One simple way tooserialize objects is toouse hello `JsonConvert` serialization methods in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) and serialize tooand from JSON.</span></span> <span data-ttu-id="b4daa-183">Hello пример get и set, с помощью `Employee` экземпляр объекта.</span><span class="sxs-lookup"><span data-stu-id="b4daa-183">hello following example shows a get and set using an `Employee` object instance.</span></span>

    class Employee
    {
        public int Id { get; set; }
        public string Name { get; set; }

        public Employee(int EmployeeId, string Name)
        {
            this.Id = EmployeeId;
            this.Name = Name;
        }
    }

    // Store toocache
    cache.StringSet("e25", JsonConvert.SerializeObject(new Employee(25, "Clayton Gragg")));

    // Retrieve from cache
    Employee e25 = JsonConvert.DeserializeObject<Employee>(cache.StringGet("e25"));

<a name="next-steps"></a>

## <a name="next-steps"></a><span data-ttu-id="b4daa-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b4daa-184">Next Steps</span></span>
<span data-ttu-id="b4daa-185">Теперь, когда вы узнали основы hello, выполните следующие дополнительные сведения о кэше Redis для Azure toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="b4daa-185">Now that you've learned hello basics, follow these links toolearn more about Azure Redis Cache.</span></span>

* <span data-ttu-id="b4daa-186">Проверьте hello поставщики ASP.NET для кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="b4daa-186">Check out hello ASP.NET providers for Azure Redis Cache.</span></span>
  * [<span data-ttu-id="b4daa-187">Поставщик состояний сеансов Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="b4daa-187">Azure Redis Session State Provider</span></span>](cache-aspnet-session-state-provider.md)
  * [<span data-ttu-id="b4daa-188">Поставщик кэша вывода ASP.NET для кэша Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="b4daa-188">Azure Redis Cache ASP.NET Output Cache Provider</span></span>](cache-aspnet-output-cache-provider.md)
* <span data-ttu-id="b4daa-189">[Включить диагностику кэша](cache-how-to-monitor.md#enable-cache-diagnostics) так, чтобы [монитор](cache-how-to-monitor.md) hello работоспособности кэша.</span><span class="sxs-lookup"><span data-stu-id="b4daa-189">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) hello health of your cache.</span></span> <span data-ttu-id="b4daa-190">Можно просмотреть метрики в hello портал Azure и вы также можете hello [Загрузите и прочтите](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) их с помощью средств hello по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="b4daa-190">You can view hello metrics in hello Azure portal and you can also [download and review](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) them using hello tools of your choice.</span></span>
* <span data-ttu-id="b4daa-191">Извлечение hello [документации по клиенту кэша StackExchange.Redis][StackExchange.Redis cache client documentation].</span><span class="sxs-lookup"><span data-stu-id="b4daa-191">Check out hello [StackExchange.Redis cache client documentation][StackExchange.Redis cache client documentation].</span></span>
  * <span data-ttu-id="b4daa-192">Доступ к кэшу Redis для Azure можно получить из многих клиентов Redis и языков разработки.</span><span class="sxs-lookup"><span data-stu-id="b4daa-192">Azure Redis Cache can be accessed from many Redis clients and development languages.</span></span> <span data-ttu-id="b4daa-193">Дополнительные сведения см. на странице [http://redis.io/clients][http://redis.io/clients].</span><span class="sxs-lookup"><span data-stu-id="b4daa-193">For more information, see [http://redis.io/clients][http://redis.io/clients].</span></span>
* <span data-ttu-id="b4daa-194">Кэш Redis для Azure можно также использовать со сторонними службами и средствами, например с Redsmin и Redis Desktop Manager.</span><span class="sxs-lookup"><span data-stu-id="b4daa-194">Azure Redis Cache can also be used with third-party services and tools such as Redsmin and Redis Desktop Manager.</span></span>
  * <span data-ttu-id="b4daa-195">Дополнительные сведения о Redsmin см. в разделе [как tooretrieve подключение к redis для Azure — строку и использовать его с Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].</span><span class="sxs-lookup"><span data-stu-id="b4daa-195">For more information about Redsmin, see [How tooretrieve an Azure Redis connection string and use it with Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].</span></span>
  * <span data-ttu-id="b4daa-196">Вы можете открыть и проверить свои данные в кэше Redis для Azure с помощью графического пользовательского интерфейса [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span><span class="sxs-lookup"><span data-stu-id="b4daa-196">Access and inspect your data in Azure Redis Cache with a GUI using [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span></span>
* <span data-ttu-id="b4daa-197">В разделе hello [redis] [ redis] документации и сведения о [типы данных redis] [ redis data types] и [введение пятнадцать минут типы данных tooRedis][a fifteen minute introduction tooRedis data types].</span><span class="sxs-lookup"><span data-stu-id="b4daa-197">See hello [redis][redis] documentation and read about [redis data types][redis data types] and [a fifteen minute introduction tooRedis data types][a fifteen minute introduction tooRedis data types].</span></span>

<!-- INTRA-TOPIC LINKS -->
[Next Steps]: #next-steps
[Introduction tooAzure Redis Cache (Video)]: #video
[What is Azure Redis Cache?]: #what-is
[Create an Azure Cache]: #create-cache
[Which type of caching is right for me?]: #choosing-cache
[Prepare Your Visual Studio Project tooUse Azure Caching]: #prepare-vs
[Configure Your Application tooUse Caching]: #configure-app
[Get Started with Azure Redis Cache]: #getting-started-cache-service
[Create hello cache]: #create-cache
[Configure hello cache]: #enable-caching
[Configure hello cache clients]: #NuGet
[Working with Caches]: #working-with-caches
[Connect toohello cache]: #connect-to-cache
[Add and retrieve objects from hello cache]: #add-object
[Specify hello expiration of an object in hello cache]: #specify-expiration
[Store ASP.NET session state in hello cache]: #store-session


<!-- IMAGES -->


[StackExchangeNuget]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-stackexchange-redis.png

[NuGetMenu]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-nuget-menu.png

[CacheProperties]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-properties.png

[ManageKeys]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-manage-keys.png

[SessionStateNuGet]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-session-state-provider.png

[BrowseCaches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-browse-caches.png

[Caches]: ./media/cache-dotnet-how-to-use-azure-redis-cache/redis-cache-caches.png







<!-- LINKS -->
[http://redis.io/clients]: http://redis.io/clients
[Develop in other languages for Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn690470.aspx
[How tooretrieve an Azure Redis connection string and use it with Redsmin]: https://redsmin.uservoice.com/knowledgebase/articles/485711-how-to-connect-redsmin-to-azure-redis-cache
[Azure Redis Session State Provider]: http://go.microsoft.com/fwlink/?LinkId=398249
[How to: Configure a Cache Client Programmatically]: http://msdn.microsoft.com/library/windowsazure/gg618003.aspx
[Session State Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320835
[Azure AppFabric Cache: Caching Session State]: http://www.microsoft.com/showcase/details.aspx?uuid=87c833e9-97a9-42b2-8bb1-7601f9b5ca20
[Output Cache Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320837
[Azure Shared Caching]: http://msdn.microsoft.com/library/windowsazure/gg278356.aspx
[Team Blog]: http://blogs.msdn.com/b/windowsazure/
[Azure Caching]: http://www.microsoft.com/showcase/Search.aspx?phrase=azure+caching
[How tooConfigure Virtual Machine Sizes]: http://go.microsoft.com/fwlink/?LinkId=164387
[Azure Caching Capacity Planning Considerations]: http://go.microsoft.com/fwlink/?LinkId=320167
[Azure Caching]: http://go.microsoft.com/fwlink/?LinkId=252658
[How to: Set hello Cacheability of an ASP.NET Page Declaratively]: http://msdn.microsoft.com/library/zd1ysf1y.aspx
[How to: Set a Page's Cacheability Programmatically]: http://msdn.microsoft.com/library/z852zf6b.aspx
[Configure a cache in Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn793612.aspx

[StackExchange.Redis configuration model]: https://stackexchange.github.io/StackExchange.Redis/Configuration

[Work with .NET objects in hello cache]: http://msdn.microsoft.com/library/dn690521.aspx#Objects


[NuGet Package Manager Installation]: http://go.microsoft.com/fwlink/?LinkId=240311
[Cache Pricing Details]: http://www.windowsazure.com/pricing/details/cache/
[Azure portal]: https://portal.azure.com/

[Overview of Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=320830
[Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=398247

[Migrate tooAzure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=317347
[Azure Redis Cache Samples]: http://go.microsoft.com/fwlink/?LinkId=320840
[Using Resource groups toomanage your Azure resources]: ../azure-resource-manager/resource-group-overview.md

[StackExchange.Redis]: http://github.com/StackExchange/StackExchange.Redis
[StackExchange.Redis cache client documentation]: http://github.com/StackExchange/StackExchange.Redis#documentation

[Redis]: http://redis.io/documentation
[Redis data types]: http://redis.io/topics/data-types
[a fifteen minute introduction tooRedis data types]: http://redis.io/topics/data-types-intro

[How Application Strings and Connection Strings Work]: http://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/


