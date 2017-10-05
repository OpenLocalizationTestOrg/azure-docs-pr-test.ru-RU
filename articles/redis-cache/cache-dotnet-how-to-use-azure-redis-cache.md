---
title: "Как использовать кэш Redis для Azure | Документация Майкрософт"
description: "Узнайте, как повысить производительность приложений Azure с помощью кэша Redis для Azure."
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
ms.openlocfilehash: 3dfc026490093523446650c510dbebdd660e8b6b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-azure-redis-cache"></a><span data-ttu-id="7cd1c-103">Как использовать кэш Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="7cd1c-103">How to Use Azure Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7cd1c-104">.NET</span><span class="sxs-lookup"><span data-stu-id="7cd1c-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="7cd1c-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7cd1c-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="7cd1c-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="7cd1c-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="7cd1c-107">Java</span><span class="sxs-lookup"><span data-stu-id="7cd1c-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="7cd1c-108">Python</span><span class="sxs-lookup"><span data-stu-id="7cd1c-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="7cd1c-109">В этом руководстве объясняется, как приступить к использованию **кэша Redis для Azure**.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-109">This guide shows you how to get started using **Azure Redis Cache**.</span></span> <span data-ttu-id="7cd1c-110">Кэш Redis для Microsoft Azure основывается на популярном продукте с открытым кодом — кэше Redis.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-110">Microsoft Azure Redis Cache is based on the popular open source Redis Cache.</span></span> <span data-ttu-id="7cd1c-111">Он дает доступ к защищенному выделенному кэшу Redis, управляемому Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-111">It gives you access to a secure, dedicated Redis cache, managed by Microsoft.</span></span> <span data-ttu-id="7cd1c-112">Кэш, созданный с использованием кэша Azure Redis, доступен из любого приложения в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-112">A cache created using Azure Redis Cache is accessible from any application within Microsoft Azure.</span></span>

<span data-ttu-id="7cd1c-113">Доступны указанные ниже уровни кэша Redis для Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-113">Microsoft Azure Redis Cache is available in the following tiers:</span></span>

* <span data-ttu-id="7cd1c-114">**Basic** — один узел.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-114">**Basic** – Single node.</span></span> <span data-ttu-id="7cd1c-115">Множество размеров вплоть до 53 ГБ.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-115">Multiple sizes up to 53 GB.</span></span>
* <span data-ttu-id="7cd1c-116">**Стандартный** — два узла: основной и реплика.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-116">**Standard** – Two-node Primary/Replica.</span></span> <span data-ttu-id="7cd1c-117">Множество размеров вплоть до 53 ГБ.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-117">Multiple sizes up to 53 GB.</span></span> <span data-ttu-id="7cd1c-118">СОГЛАШЕНИЕ ОБ УРОВНЕ ОБСЛУЖИВАНИЯ 99,9 %.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-118">99.9% SLA.</span></span>
* <span data-ttu-id="7cd1c-119">**Премиум** — два узла (основной и реплика), включающие до 10 сегментов.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-119">**Premium** – Two-node Primary/Replica with up to 10 shards.</span></span> <span data-ttu-id="7cd1c-120">Несколько размеров: от 6 ГБ до 530 ГБ.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-120">Multiple sizes from 6 GB to 530 GB.</span></span> <span data-ttu-id="7cd1c-121">Все функции уровня "Стандартный", а также дополнительные функции, включая поддержку [кластера Redis](cache-how-to-premium-clustering.md), [сохраняемости Redis](cache-how-to-premium-persistence.md) и [виртуальной сети Azure](cache-how-to-premium-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="7cd1c-121">All Standard tier features and more including support for [Redis cluster](cache-how-to-premium-clustering.md), [Redis persistence](cache-how-to-premium-persistence.md), and [Azure Virtual Network](cache-how-to-premium-vnet.md).</span></span> <span data-ttu-id="7cd1c-122">СОГЛАШЕНИЕ ОБ УРОВНЕ ОБСЛУЖИВАНИЯ 99,9 %.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-122">99.9% SLA.</span></span>

<span data-ttu-id="7cd1c-123">Каждый уровень отличается доступными возможностями и ценой.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-123">Each tier differs in terms of features and pricing.</span></span> <span data-ttu-id="7cd1c-124">Дополнительные сведения о ценах на кэш см. на [этой странице][Cache Pricing Details].</span><span class="sxs-lookup"><span data-stu-id="7cd1c-124">For information on pricing, see [Cache Pricing Details][Cache Pricing Details].</span></span>

<span data-ttu-id="7cd1c-125">В этом руководстве показано, как использовать клиент [StackExchange.Redis][StackExchange.Redis] с помощью кода C\#.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-125">This guide shows you how to use the [StackExchange.Redis][StackExchange.Redis] client using C\# code.</span></span> <span data-ttu-id="7cd1c-126">Рассматриваемые сценарии включают **создание и настройку кэша**, **настройку клиентов кэша**, а также **добавление объектов в кэш и их удаление**.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-126">The scenarios covered include **creating and configuring a cache**, **configuring cache clients**, and **adding and removing objects from the cache**.</span></span> <span data-ttu-id="7cd1c-127">Дополнительные сведения об использовании кэша Redis для Azure см. в разделе [Дальнейшие действия][Next Steps].</span><span class="sxs-lookup"><span data-stu-id="7cd1c-127">For more information on using Azure Redis Cache, see [Next Steps][Next Steps].</span></span> <span data-ttu-id="7cd1c-128">Пошаговое руководство по созданию веб-приложения MVC ASP.NET с помощью кэша Redis см. в статье [Как создать веб-приложение с использованием кэша Redis](cache-web-app-howto.md).</span><span class="sxs-lookup"><span data-stu-id="7cd1c-128">For a step-by-step tutorial of building an ASP.NET MVC web app with Redis Cache, see [How to create a Web App with Redis Cache](cache-web-app-howto.md).</span></span>

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a><span data-ttu-id="7cd1c-129">Начало работы с кэшем Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="7cd1c-129">Get Started with Azure Redis Cache</span></span>
<span data-ttu-id="7cd1c-130">Начать работу с кэшем Azure Redis просто.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-130">Getting started with Azure Redis Cache is easy.</span></span> <span data-ttu-id="7cd1c-131">Чтобы приступить к работе, подготовьте и настройте кэш.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-131">To get started, you provision and configure a cache.</span></span> <span data-ttu-id="7cd1c-132">Затем следует настроить клиенты кэша, чтобы они могли обращаться к кэшу.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-132">Next, you configure the cache clients so they can access the cache.</span></span> <span data-ttu-id="7cd1c-133">Когда клиенты кэша настроены, с ними можно работать.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-133">Once the cache clients are configured, you can begin working with them.</span></span>

* <span data-ttu-id="7cd1c-134">[Создание кэша][Create the cache]</span><span class="sxs-lookup"><span data-stu-id="7cd1c-134">[Create the cache][Create the cache]</span></span>
* <span data-ttu-id="7cd1c-135">[Настройка клиентов кэша][Configure the cache clients]</span><span class="sxs-lookup"><span data-stu-id="7cd1c-135">[Configure the cache clients][Configure the cache clients]</span></span>

<a name="create-cache"></a>

## <a name="create-a-cache"></a><span data-ttu-id="7cd1c-136">Создание кэша</span><span class="sxs-lookup"><span data-stu-id="7cd1c-136">Create a cache</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="to-access-your-cache-after-its-created"></a><span data-ttu-id="7cd1c-137">Доступ к кэшу после его создания</span><span class="sxs-lookup"><span data-stu-id="7cd1c-137">To access your cache after it's created</span></span>
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

<span data-ttu-id="7cd1c-138">Дополнительные сведения о настройке кэша см. в статье [Настройка кэша Redis для Azure](cache-configure.md).</span><span class="sxs-lookup"><span data-stu-id="7cd1c-138">For more information about configuring your cache, see [How to configure Azure Redis Cache](cache-configure.md).</span></span>

<a name="NuGet"></a>

## <a name="configure-the-cache-clients"></a><span data-ttu-id="7cd1c-139">Настройка клиентов кэша</span><span class="sxs-lookup"><span data-stu-id="7cd1c-139">Configure the cache clients</span></span>
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

<span data-ttu-id="7cd1c-140">После настройки проекта клиента для кэширования можно использовать методы, описанные в следующих разделах, для работы с кэшем.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-140">Once your client project is configured for caching, you can use the techniques described in the following sections for working with your cache.</span></span>

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a><span data-ttu-id="7cd1c-141">Работа с кэшами</span><span class="sxs-lookup"><span data-stu-id="7cd1c-141">Working with Caches</span></span>
<span data-ttu-id="7cd1c-142">Действия, приведенные в этом разделе, описывают способы выполнения типовых задач при работе с кэшем.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-142">The steps in this section describe how to perform common tasks with Cache.</span></span>

* <span data-ttu-id="7cd1c-143">[Подключение к кэшу][Connect to the cache]</span><span class="sxs-lookup"><span data-stu-id="7cd1c-143">[Connect to the cache][Connect to the cache]</span></span>
* <span data-ttu-id="7cd1c-144">[Добавление в кэш объектов и их извлечение][Add and retrieve objects from the cache]</span><span class="sxs-lookup"><span data-stu-id="7cd1c-144">[Add and retrieve objects from the cache][Add and retrieve objects from the cache]</span></span>
* [<span data-ttu-id="7cd1c-145">Работа с объектами .NET в кэше</span><span class="sxs-lookup"><span data-stu-id="7cd1c-145">Work with .NET objects in the cache</span></span>](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-to-the-cache"></a><span data-ttu-id="7cd1c-146">Подключение к кэшу</span><span class="sxs-lookup"><span data-stu-id="7cd1c-146">Connect to the cache</span></span>
<span data-ttu-id="7cd1c-147">Чтобы программно работать с кэшем, требуется ссылка на кэш.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-147">To programmatically work with a cache, you need a reference to the cache.</span></span> <span data-ttu-id="7cd1c-148">Добавьте следующий код вверху любого файла, из которого будет использоваться клиент StackExchange.Redis для доступа к кэшу Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-148">Add the following to the top of any file from which you want to use the StackExchange.Redis client to access an Azure Redis Cache.</span></span>

    using StackExchange.Redis;

> [!NOTE]
> <span data-ttu-id="7cd1c-149">Клиенту StackExchange.Redis необходима среда .NET Framework 4 или выше.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-149">The StackExchange.Redis client requires .NET Framework 4 or higher.</span></span>
> 
> 

<span data-ttu-id="7cd1c-150">Подключение к кэшу Redis для Azure выполняется с помощью класса `ConnectionMultiplexer` .</span><span class="sxs-lookup"><span data-stu-id="7cd1c-150">The connection to the Azure Redis Cache is managed by the `ConnectionMultiplexer` class.</span></span> <span data-ttu-id="7cd1c-151">Этот класс предназначен для общего использования и повторного использования клиентским приложением и не нуждается в создании нового экземпляра для каждой отдельной операции.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-151">This class should be shared and reused throughout your client application, and does not need to be created on a per operation basis.</span></span> 

<span data-ttu-id="7cd1c-152">Для подключения к кэшу Redis для Azure и получения экземпляра подключенного класса `ConnectionMultiplexer` вызовите статический метод `Connect` и передайте ему конечную точку кэша и ключ.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-152">To connect to an Azure Redis Cache and be returned an instance of a connected `ConnectionMultiplexer`, call the static `Connect` method and pass in the cache endpoint and key.</span></span> <span data-ttu-id="7cd1c-153">Используйте в качестве параметра пароля ключ, созданный на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-153">Use the key generated from the Azure portal as the password parameter.</span></span>

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> <span data-ttu-id="7cd1c-154">Внимание! Никогда не храните учетные данные в исходном коде.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-154">Warning: Never store credentials in source code.</span></span> <span data-ttu-id="7cd1c-155">Для сохранения простоты примера они показаны в исходном коде.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-155">To keep this sample simple, I’m showing them in the source code.</span></span> <span data-ttu-id="7cd1c-156">Сведения о том, как хранить учетные данные, см. в статье [How Application Strings and Connection Strings Work][How Application Strings and Connection Strings Work] (Принципы работы строк приложений и подключения).</span><span class="sxs-lookup"><span data-stu-id="7cd1c-156">See [How Application Strings and Connection Strings Work][How Application Strings and Connection Strings Work] for information on how to store credentials.</span></span>
> 
> 

<span data-ttu-id="7cd1c-157">Если вам не требуется SSL, задайте значение `ssl=false` или пропустите параметр `ssl`.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-157">If you don't want to use SSL, either set `ssl=false` or omit the `ssl` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="7cd1c-158">Для новых кэшей не SSL порт по умолчанию запрещен.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-158">The non-SSL port is disabled by default for new caches.</span></span> <span data-ttu-id="7cd1c-159">Инструкции по включению портов, не использующих протокол SSL, см. в разделе [Порты доступа](cache-configure.md#access-ports).</span><span class="sxs-lookup"><span data-stu-id="7cd1c-159">For instructions on enabling the non-SSL port, see [Access Ports](cache-configure.md#access-ports).</span></span>
> 
> 

<span data-ttu-id="7cd1c-160">Один из способов совместного использования экземпляра `ConnectionMultiplexer` в приложении предполагает наличие статического свойства, которое возвращает подключенный экземпляр (как в приведенном ниже примере).</span><span class="sxs-lookup"><span data-stu-id="7cd1c-160">One approach to sharing a `ConnectionMultiplexer` instance in your application is to have a static property that returns a connected instance, similar to the following example.</span></span> <span data-ttu-id="7cd1c-161">Этот подход помогает потокобезопасно инициализировать только отдельный подключенный экземпляр `ConnectionMultiplexer`.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-161">This approach provides a thread-safe way to initialize only a single connected `ConnectionMultiplexer` instance.</span></span> <span data-ttu-id="7cd1c-162">В этих примерах для параметра `abortConnect` задано значение False. Это означает, что вызов завершается успешно, даже если подключение к кэшу Redis для Azure не установлено.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-162">In these examples `abortConnect` is set to false, which means that the call succeeds even if a connection to the Azure Redis Cache is not established.</span></span> <span data-ttu-id="7cd1c-163">Одна из ключевых особенностей `ConnectionMultiplexer` заключается в том, что этот параметр автоматически восстанавливает соединение с кэшем, когда устраняется проблема с сетью или другие проблемы.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-163">One key feature of `ConnectionMultiplexer` is that it automatically restores connectivity to the cache once the network issue or other causes are resolved.</span></span>

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

<span data-ttu-id="7cd1c-164">Дополнительные сведения по вариантам расширенных настроек соединения см. в статье [Модель конфигурации StackExchange.Redis][StackExchange.Redis configuration model].</span><span class="sxs-lookup"><span data-stu-id="7cd1c-164">For more information on advanced connection configuration options, see [StackExchange.Redis configuration model][StackExchange.Redis configuration model].</span></span>

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

<span data-ttu-id="7cd1c-165">Создав подключение, верните ссылку на базу данных кэша Redis с помощью метода `ConnectionMultiplexer.GetDatabase` .</span><span class="sxs-lookup"><span data-stu-id="7cd1c-165">Once the connection is established, return a reference to the redis cache database by calling the `ConnectionMultiplexer.GetDatabase` method.</span></span> <span data-ttu-id="7cd1c-166">Объект, возвращенный из метода `GetDatabase`, – это упрощенный передаваемый объект, не требующий сохранения.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-166">The object returned from the `GetDatabase` method is a lightweight pass-through object and does not need to be stored.</span></span>

    // Connection refers to a property that returns a ConnectionMultiplexer
    // as shown in the previous example.
    IDatabase cache = Connection.GetDatabase();

    // Perform cache operations using the cache object...
    // Simple put of integral data types into the cache
    cache.StringSet("key1", "value");
    cache.StringSet("key2", 25);

    // Simple get of data types from the cache
    string key1 = cache.StringGet("key1");
    int key2 = (int)cache.StringGet("key2");

<span data-ttu-id="7cd1c-167">Кэши Redis для Azure могут использовать до 16 баз данных (их количество можно указать), чтобы обеспечить логическое разделение данных в кэше Redis.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-167">Azure Redis caches have a configurable number of databases (default of 16) that can be used to logically separate the data within a Redis cache.</span></span> <span data-ttu-id="7cd1c-168">Дополнительные сведения см. в разделах [What are Redis databases?](cache-configure.md#default-redis-server-configuration) (Что такое базы данных Redis) и [Конфигурация сервера Redis по умолчанию](cache-faq.md#what-are-redis-databases).</span><span class="sxs-lookup"><span data-stu-id="7cd1c-168">For more information, see [What are Redis databases?](cache-faq.md#what-are-redis-databases) and [Default Redis server configuration](cache-configure.md#default-redis-server-configuration).</span></span>

<span data-ttu-id="7cd1c-169">Теперь нам известно, как соединяться с экземпляром кэша Redis для Azure и возвращать ссылку на базу данных кэша, поэтому давайте посмотрим, как работать с кэшем.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-169">Now that you know how to connect to an Azure Redis Cache instance and return a reference to the cache database, let's look at working with the cache.</span></span>

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-the-cache"></a><span data-ttu-id="7cd1c-170">Добавление в кэш объектов и их извлечение</span><span class="sxs-lookup"><span data-stu-id="7cd1c-170">Add and retrieve objects from the cache</span></span>
<span data-ttu-id="7cd1c-171">Элементы можно хранить в кэше и извлекать из него с помощью методов `StringSet` и `StringGet`.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-171">Items can be stored in and retrieved from a cache by using the `StringSet` and `StringGet` methods.</span></span>

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

<span data-ttu-id="7cd1c-172">Redis хранит большинство данных в строках Redis, но эти строки могут содержать данные многих типов, включая сериализованные двоичные данные, которые можно использовать при сохранении объектов .NET в кэше.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-172">Redis stores most data as Redis strings, but these strings can contain many types of data, including serialized binary data, which can be used when storing .NET objects in the cache.</span></span>

<span data-ttu-id="7cd1c-173">Если объект существует, вызов метода `StringGet` возвращает его. В противном случае возвращается значение `null`.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-173">When calling `StringGet`, if the object exists, it is returned, and if it does not, `null` is returned.</span></span> <span data-ttu-id="7cd1c-174">Если возвращается `null`, то можно извлечь значение из желаемого источника данных и сохранить его в кэше для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-174">If `null` is returned, you can retrieve the value from the desired data source and store it in the cache for subsequent use.</span></span> <span data-ttu-id="7cd1c-175">Это называется шаблоном "кэш на стороне".</span><span class="sxs-lookup"><span data-stu-id="7cd1c-175">This usage pattern is known as the cache-aside pattern.</span></span>

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // The item keyed by "key1" is not in the cache. Obtain
        // it from the desired data source and add it to the cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

<span data-ttu-id="7cd1c-176">Можно также использовать `RedisValue`, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-176">You can also use `RedisValue`, as shown in the following example.</span></span> <span data-ttu-id="7cd1c-177">`RedisValue` содержит неявные операторы для работы с целочисленными типами данных и могут быть полезны, если `null` — ожидаемое значение кэшированного элемента.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-177">`RedisValue` has implicit operators for working with integral data types, and can be useful if `null` is an expected value for a cached item.</span></span>


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


<span data-ttu-id="7cd1c-178">Чтобы указать срок действия объекта в кэше, используйте параметр `TimeSpan` метода `StringSet`.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-178">To specify the expiration of an item in the cache, use the `TimeSpan` parameter of `StringSet`.</span></span>

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-the-cache"></a><span data-ttu-id="7cd1c-179">Работа с объектами .NET в кэше</span><span class="sxs-lookup"><span data-stu-id="7cd1c-179">Work with .NET objects in the cache</span></span>
<span data-ttu-id="7cd1c-180">Кэш Redis для Azure может кэшировать объекты .NET и примитивные типы данных, но прежде чем объект .NET можно будет сохранить в кэше, он должен быть сериализован.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-180">Azure Redis Cache can cache both .NET objects and primitive data types, but before a .NET object can be cached it must be serialized.</span></span> <span data-ttu-id="7cd1c-181">За сериализацию объекта .NET отвечает разработчик приложения, что дает ему свободу в выборе сериализатора.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-181">This .NET object serialization is the responsibility of the application developer, and gives the developer flexibility in the choice of the serializer.</span></span>

<span data-ttu-id="7cd1c-182">Простой способ сериализации объектов — использовать методы сериализации `JsonConvert` в [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) и выполнять сериализацию в нотацию JSON и из нее.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-182">One simple way to serialize objects is to use the `JsonConvert` serialization methods in [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) and serialize to and from JSON.</span></span> <span data-ttu-id="7cd1c-183">В следующем примере показано получение и задание экземпляра объекта `Employee` .</span><span class="sxs-lookup"><span data-stu-id="7cd1c-183">The following example shows a get and set using an `Employee` object instance.</span></span>

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

    // Store to cache
    cache.StringSet("e25", JsonConvert.SerializeObject(new Employee(25, "Clayton Gragg")));

    // Retrieve from cache
    Employee e25 = JsonConvert.DeserializeObject<Employee>(cache.StringGet("e25"));

<a name="next-steps"></a>

## <a name="next-steps"></a><span data-ttu-id="7cd1c-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7cd1c-184">Next Steps</span></span>
<span data-ttu-id="7cd1c-185">Теперь, когда вы ознакомились с основными сведениями, используйте следующие ссылки для получения дополнительных сведений о кэше Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-185">Now that you've learned the basics, follow these links to learn more about Azure Redis Cache.</span></span>

* <span data-ttu-id="7cd1c-186">Ознакомьтесь с информацией о поставщиках ASP.NET для кэша Redis для Azure.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-186">Check out the ASP.NET providers for Azure Redis Cache.</span></span>
  * [<span data-ttu-id="7cd1c-187">Поставщик состояний сеансов Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="7cd1c-187">Azure Redis Session State Provider</span></span>](cache-aspnet-session-state-provider.md)
  * [<span data-ttu-id="7cd1c-188">Поставщик кэша вывода ASP.NET для кэша Redis для Azure</span><span class="sxs-lookup"><span data-stu-id="7cd1c-188">Azure Redis Cache ASP.NET Output Cache Provider</span></span>](cache-aspnet-output-cache-provider.md)
* <span data-ttu-id="7cd1c-189">[Включите диагностику кэша](cache-how-to-monitor.md#enable-cache-diagnostics), чтобы можно было [наблюдать](cache-how-to-monitor.md) за работоспособностью кэша.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-189">[Enable cache diagnostics](cache-how-to-monitor.md#enable-cache-diagnostics) so you can [monitor](cache-how-to-monitor.md) the health of your cache.</span></span> <span data-ttu-id="7cd1c-190">Вы можете просмотреть метрики на портале Azure. Кроме того, их можно [скачать и просмотреть](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) с помощью привычных вам инструментов.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-190">You can view the metrics in the Azure portal and you can also [download and review](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) them using the tools of your choice.</span></span>
* <span data-ttu-id="7cd1c-191">Ознакомьтесь с [документацией по клиенту кэша StackExchange.Redis][StackExchange.Redis cache client documentation].</span><span class="sxs-lookup"><span data-stu-id="7cd1c-191">Check out the [StackExchange.Redis cache client documentation][StackExchange.Redis cache client documentation].</span></span>
  * <span data-ttu-id="7cd1c-192">Доступ к кэшу Redis для Azure можно получить из многих клиентов Redis и языков разработки.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-192">Azure Redis Cache can be accessed from many Redis clients and development languages.</span></span> <span data-ttu-id="7cd1c-193">Дополнительные сведения см. на странице [http://redis.io/clients][http://redis.io/clients].</span><span class="sxs-lookup"><span data-stu-id="7cd1c-193">For more information, see [http://redis.io/clients][http://redis.io/clients].</span></span>
* <span data-ttu-id="7cd1c-194">Кэш Redis для Azure можно также использовать со сторонними службами и средствами, например с Redsmin и Redis Desktop Manager.</span><span class="sxs-lookup"><span data-stu-id="7cd1c-194">Azure Redis Cache can also be used with third-party services and tools such as Redsmin and Redis Desktop Manager.</span></span>
  * <span data-ttu-id="7cd1c-195">Дополнительные сведения о Redsmin см. в статье [How to connect Azure Redis Cache to Redsmin][How to retrieve an Azure Redis connection string and use it with Redsmin] (Как подключить кэш Redis для Azure к Redsmin).</span><span class="sxs-lookup"><span data-stu-id="7cd1c-195">For more information about Redsmin, see [How to retrieve an Azure Redis connection string and use it with Redsmin][How to retrieve an Azure Redis connection string and use it with Redsmin].</span></span>
  * <span data-ttu-id="7cd1c-196">Вы можете открыть и проверить свои данные в кэше Redis для Azure с помощью графического пользовательского интерфейса [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span><span class="sxs-lookup"><span data-stu-id="7cd1c-196">Access and inspect your data in Azure Redis Cache with a GUI using [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).</span></span>
* <span data-ttu-id="7cd1c-197">Ознакомьтесь с документацией по [Redis][redis]: прочитайте [статью о типах данных Redis][redis data types] и [пятнадцатиминутное введение в типы данных Redis][a fifteen minute introduction to Redis data types].</span><span class="sxs-lookup"><span data-stu-id="7cd1c-197">See the [redis][redis] documentation and read about [redis data types][redis data types] and [a fifteen minute introduction to Redis data types][a fifteen minute introduction to Redis data types].</span></span>

<!-- INTRA-TOPIC LINKS -->
[Next Steps]: #next-steps
[Introduction to Azure Redis Cache (Video)]: #video
[What is Azure Redis Cache?]: #what-is
[Create an Azure Cache]: #create-cache
[Which type of caching is right for me?]: #choosing-cache
[Prepare Your Visual Studio Project to Use Azure Caching]: #prepare-vs
[Configure Your Application to Use Caching]: #configure-app
[Get Started with Azure Redis Cache]: #getting-started-cache-service
[Create the cache]: #create-cache
[Configure the cache]: #enable-caching
[Configure the cache clients]: #NuGet
[Working with Caches]: #working-with-caches
[Connect to the cache]: #connect-to-cache
[Add and retrieve objects from the cache]: #add-object
[Specify the expiration of an object in the cache]: #specify-expiration
[Store ASP.NET session state in the cache]: #store-session


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
[How to retrieve an Azure Redis connection string and use it with Redsmin]: https://redsmin.uservoice.com/knowledgebase/articles/485711-how-to-connect-redsmin-to-azure-redis-cache
[Azure Redis Session State Provider]: http://go.microsoft.com/fwlink/?LinkId=398249
[How to: Configure a Cache Client Programmatically]: http://msdn.microsoft.com/library/windowsazure/gg618003.aspx
[Session State Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320835
[Azure AppFabric Cache: Caching Session State]: http://www.microsoft.com/showcase/details.aspx?uuid=87c833e9-97a9-42b2-8bb1-7601f9b5ca20
[Output Cache Provider for Azure Cache]: http://go.microsoft.com/fwlink/?LinkId=320837
[Azure Shared Caching]: http://msdn.microsoft.com/library/windowsazure/gg278356.aspx
[Team Blog]: http://blogs.msdn.com/b/windowsazure/
[Azure Caching]: http://www.microsoft.com/showcase/Search.aspx?phrase=azure+caching
[How to Configure Virtual Machine Sizes]: http://go.microsoft.com/fwlink/?LinkId=164387
[Azure Caching Capacity Planning Considerations]: http://go.microsoft.com/fwlink/?LinkId=320167
[Azure Caching]: http://go.microsoft.com/fwlink/?LinkId=252658
[How to: Set the Cacheability of an ASP.NET Page Declaratively]: http://msdn.microsoft.com/library/zd1ysf1y.aspx
[How to: Set a Page's Cacheability Programmatically]: http://msdn.microsoft.com/library/z852zf6b.aspx
[Configure a cache in Azure Redis Cache]: http://msdn.microsoft.com/library/azure/dn793612.aspx

[StackExchange.Redis configuration model]: https://stackexchange.github.io/StackExchange.Redis/Configuration

[Work with .NET objects in the cache]: http://msdn.microsoft.com/library/dn690521.aspx#Objects


[NuGet Package Manager Installation]: http://go.microsoft.com/fwlink/?LinkId=240311
[Cache Pricing Details]: http://www.windowsazure.com/pricing/details/cache/
[Azure portal]: https://portal.azure.com/

[Overview of Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=320830
[Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=398247

[Migrate to Azure Redis Cache]: http://go.microsoft.com/fwlink/?LinkId=317347
[Azure Redis Cache Samples]: http://go.microsoft.com/fwlink/?LinkId=320840
[Using Resource groups to manage your Azure resources]: ../azure-resource-manager/resource-group-overview.md

[StackExchange.Redis]: http://github.com/StackExchange/StackExchange.Redis
[StackExchange.Redis cache client documentation]: http://github.com/StackExchange/StackExchange.Redis#documentation

[Redis]: http://redis.io/documentation
[Redis data types]: http://redis.io/topics/data-types
[a fifteen minute introduction to Redis data types]: http://redis.io/topics/data-types-intro

[How Application Strings and Connection Strings Work]: http://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/


