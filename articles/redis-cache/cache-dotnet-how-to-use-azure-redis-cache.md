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
# <a name="how-toouse-azure-redis-cache"></a>Как tooUse Redis для Azure кэша
> [!div class="op_single_selector"]
> * [.NET](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [ASP.NET](cache-web-app-howto.md)
> * [Node.js](cache-nodejs-get-started.md)
> * [Java](cache-java-get-started.md)
> * [Python](cache-python-get-started.md)
> 
> 

В этом руководстве показано, как tooget запущена с помощью **кэш Azure Redis**. Кэш Redis Microsoft Azure основан на hello открытым исходным кодом кэша Redis. Он предоставляет доступ к tooa безопасного выделенному кэшу Redis, управляемый корпорацией Майкрософт. Кэш, созданный с использованием кэша Azure Redis, доступен из любого приложения в Microsoft Azure.

Кэш Microsoft Azure Redis доступна hello следующие уровни:

* **Basic** — один узел. Несколько размеров too53 Гбайт.
* **Стандартный** — два узла: основной и реплика. Несколько размеров too53 Гбайт. СОГЛАШЕНИЕ ОБ УРОВНЕ ОБСЛУЖИВАНИЯ 99,9 %.
* **Premium** — двумя узлами первичный/реплика с вверх too10 сегментов. Несколько размеров от 6 ГБ too530 ГБ. Все функции уровня "Стандартный", а также дополнительные функции, включая поддержку [кластера Redis](cache-how-to-premium-clustering.md), [сохраняемости Redis](cache-how-to-premium-persistence.md) и [виртуальной сети Azure](cache-how-to-premium-vnet.md). СОГЛАШЕНИЕ ОБ УРОВНЕ ОБСЛУЖИВАНИЯ 99,9 %.

Каждый уровень отличается доступными возможностями и ценой. Дополнительные сведения о ценах на кэш см. на [этой странице][Cache Pricing Details].

В этом руководстве показано, как toouse hello [StackExchange.Redis] [ StackExchange.Redis] клиента с помощью C\# кода. Hello сценарии включают **создания и настройки кэша**, **настройке клиентов кэша**, и **добавления и удаления объектов из кэша hello**. Дополнительные сведения об использовании кэша Redis для Azure см. в разделе [Дальнейшие действия][Next Steps]. Пошаговый учебник построения ASP.NET MVC, веб-приложения в кэш Redis см. в разделе [как веб-приложения в кэш Redis toocreate](cache-web-app-howto.md).

<a name="getting-started-cache-service"></a>

## <a name="get-started-with-azure-redis-cache"></a>Начало работы с кэшем Redis для Azure
Начать работу с кэшем Azure Redis просто. tooget к работе, можно подготовить и настройте кэш. Далее следует настроить клиенты кэша hello для доступа к кэшем hello. После настройки клиентов кэша hello можно начать работу с ними.

* [Создание кэша hello][Create hello cache]
* [Настройка клиентов кэша hello][Configure hello cache clients]

<a name="create-cache"></a>

## <a name="create-a-cache"></a>Создание кэша
[!INCLUDE [redis-cache-create](../../includes/redis-cache-create.md)]

### <a name="tooaccess-your-cache-after-its-created"></a>tooaccess кэша после его создания
[!INCLUDE [redis-cache-create](../../includes/redis-cache-browse.md)]

Дополнительные сведения о настройке кэша см. в разделе [как tooconfigure кэш Azure Redis](cache-configure.md).

<a name="NuGet"></a>

## <a name="configure-hello-cache-clients"></a>Настройка клиентов кэша hello
[!INCLUDE [redis-cache-configure](../../includes/redis-cache-configure-stackexchange-redis-nuget.md)]

Когда клиентский проект настроен для кэширования, можно использовать hello методик, описанных в следующих разделах для работы с кэшем hello.

<a name="working-with-caches"></a>

## <a name="working-with-caches"></a>Работа с кэшами
Hello в этом разделе описывается, как tooperform распространенные задачи с кэшем.

* [Подключение toohello кэша][Connect toohello cache]
* [Добавление и извлечение объектов из кэша hello][Add and retrieve objects from hello cache]
* [Работа с объектами .NET в кэше hello](#work-with-net-objects-in-the-cache)

<a name="connect-to-cache"></a>

## <a name="connect-toohello-cache"></a>Подключение toohello кэша
tooprogrammatically работы с кэшем, требуется ссылка toohello кэша. Добавьте следующие toohello начало любого файла, из которого требуется toouse hello StackExchange.Redis клиента tooaccess кэш Azure Redis hello.

    using StackExchange.Redis;

> [!NOTE]
> Hello клиента StackExchange.Redis требуется платформа .NET Framework 4 или более поздней версии.
> 
> 

Здравствуйте подключения toohello кэша Redis для Azure управляется hello `ConnectionMultiplexer` класса. Этот класс должны быть общими и в клиентском приложении многократно и не обязательно toobe создан для каждой операции. 

tooconnect tooan кэша Redis для Azure и возвращаться подключенного экземпляра `ConnectionMultiplexer`, hello вызов статических `Connect` метод и передайте его в hello кэшировать конечную точку и ключ. Используйте ключ hello, созданные из hello портал управления Azure как параметр password hello.

    ConnectionMultiplexer connection = ConnectionMultiplexer.Connect("contoso5.redis.cache.windows.net,abortConnect=false,ssl=true,password=...");

> [!IMPORTANT]
> Внимание! Никогда не храните учетные данные в исходном коде. tookeep этот простой пример, я отображения их в исходном коде hello. В разделе [как строки приложения и строк соединения работает] [ How Application Strings and Connection Strings Work] сведения о том, как toostore учетные данные.
> 
> 

Если вы не хотите toouse SSL, установите `ssl=false` или пропустите hello `ssl` параметра.

> [!NOTE]
> Hello не SSL-порт отключен по умолчанию для нового кэша. Инструкции по включению hello не SSL-порт. в разделе [порты доступа](cache-configure.md#access-ports).
> 
> 

Один из подходов toosharing `ConnectionMultiplexer` toohave статическое свойство, которое возвращает подключенный экземпляр, аналогичные toohello следующий пример является экземпляр приложения. Такой подход обеспечивает tooinitialize потокобезопасным способом только одного подключенного `ConnectionMultiplexer` экземпляра. В этих примерах `abortConnect` является набор toofalse, это означает, что hello вызов завершается успешно, даже если не будет установлено подключение toohello кэша Redis для Azure. Одна важная особенность `ConnectionMultiplexer` — что автоматически восстанавливается подключение toohello кэша после hello проблемы в сети или по другим причинам не будут разрешены.

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

Дополнительные сведения по вариантам расширенных настроек соединения см. в статье [Модель конфигурации StackExchange.Redis][StackExchange.Redis configuration model].

[!INCLUDE [redis-cache-create](../../includes/redis-cache-access-keys.md)]

После установления соединения hello вернуть базу данных кэша redis ссылки toohello, вызывающему Привет `ConnectionMultiplexer.GetDatabase` метод. Hello объект, возвращенный hello `GetDatabase` метод является облегченным сквозным объектом и не обязательно toobe хранятся.

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

Кэшах Azure Redis имеется определенное количество баз данных (по умолчанию 16), которые могут быть toologically используется отдельный hello данных в кэше Redis. Дополнительные сведения см. в разделах [What are Redis databases?](cache-configure.md#default-redis-server-configuration) (Что такое базы данных Redis) и [Конфигурация сервера Redis по умолчанию](cache-faq.md#what-are-redis-databases).

Теперь, когда вы знаете, как экземпляр кэша Azure Redis tooan tooconnect и возврат toohello ссылки кэша базы данных, давайте взглянем на работе с кэшем hello.

<a name="add-object"></a>

## <a name="add-and-retrieve-objects-from-hello-cache"></a>Добавление и извлечение объектов из кэша hello
Элементы можно хранятся в и извлекаются из кэша с использованием hello `StringSet` и `StringGet` методы.

    // If key1 exists, it is overwritten.
    cache.StringSet("key1", "value1");

    string value = cache.StringGet("key1");

Redis хранилищ, большинство данных в виде строки Redis, а эти строки может содержать несколько типов данных, включая сериализованные двоичные данные, которые можно использовать при сохранении .NET объектов в кэше hello.

При вызове `StringGet`, hello объект существует, возвращается, и если оно отсутствует, `null` возвращается. Если `null` возвращается, можно получить значение hello из hello необходимый источник данных и сохранить его в кэше hello для последующего использования. Этот шаблон использования называется hello отдельно от кэша шаблоном.

    string value = cache.StringGet("key1");
    if (value == null)
    {
        // hello item keyed by "key1" is not in hello cache. Obtain
        // it from hello desired data source and add it toohello cache.
        value = GetValueFromDataSource();

        cache.StringSet("key1", value);
    }

Можно также использовать `RedisValue`, как показано в следующий пример hello. `RedisValue` содержит неявные операторы для работы с целочисленными типами данных и могут быть полезны, если `null` — ожидаемое значение кэшированного элемента.


    RedisValue value = cache.StringGet("key1");
    if (!value.HasValue)
    {
        value = GetValueFromDataSource();
        cache.StringSet("key1", value);
    }


срок годности hello toospecify элемента в кэше hello, используйте hello `TimeSpan` параметр `StringSet`.

    cache.StringSet("key1", "value1", TimeSpan.FromMinutes(90));

## <a name="work-with-net-objects-in-hello-cache"></a>Работа с объектами .NET в кэше hello
Кэш Redis для Azure может кэшировать объекты .NET и примитивные типы данных, но прежде чем объект .NET можно будет сохранить в кэше, он должен быть сериализован. Этой сериализации объекта .NET hello отвечает разработчик приложения hello и обеспечивает гибкость hello разработчика по выбору hello hello сериализатор.

Один простой способ tooserialize объектов — toouse hello `JsonConvert` методы сериализации в [Newtonsoft.Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/8.0.1-beta1) и сериализации tooand из JSON. Hello пример get и set, с помощью `Employee` экземпляр объекта.

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

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello, выполните следующие дополнительные сведения о кэше Redis для Azure toolearn ссылки.

* Проверьте hello поставщики ASP.NET для кэша Redis для Azure.
  * [Поставщик состояний сеансов Redis для Azure](cache-aspnet-session-state-provider.md)
  * [Поставщик кэша вывода ASP.NET для кэша Redis для Azure](cache-aspnet-output-cache-provider.md)
* [Включить диагностику кэша](cache-how-to-monitor.md#enable-cache-diagnostics) так, чтобы [монитор](cache-how-to-monitor.md) hello работоспособности кэша. Можно просмотреть метрики в hello портал Azure и вы также можете hello [Загрузите и прочтите](https://github.com/rustd/RedisSamples/tree/master/CustomMonitoring) их с помощью средств hello по своему усмотрению.
* Извлечение hello [документации по клиенту кэша StackExchange.Redis][StackExchange.Redis cache client documentation].
  * Доступ к кэшу Redis для Azure можно получить из многих клиентов Redis и языков разработки. Дополнительные сведения см. на странице [http://redis.io/clients][http://redis.io/clients].
* Кэш Redis для Azure можно также использовать со сторонними службами и средствами, например с Redsmin и Redis Desktop Manager.
  * Дополнительные сведения о Redsmin см. в разделе [как tooretrieve подключение к redis для Azure — строку и использовать его с Redsmin][How tooretrieve an Azure Redis connection string and use it with Redsmin].
  * Вы можете открыть и проверить свои данные в кэше Redis для Azure с помощью графического пользовательского интерфейса [RedisDesktopManager](https://github.com/uglide/RedisDesktopManager).
* В разделе hello [redis] [ redis] документации и сведения о [типы данных redis] [ redis data types] и [введение пятнадцать минут типы данных tooRedis][a fifteen minute introduction tooRedis data types].

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


