---
title: "aaaWorking с датами в базе данных Azure Cosmos | Документы Microsoft"
description: "Узнайте, как в базе данных Azure Cosmos даты toowork с."
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: e587772f-ce9f-498c-a017-a51e7265bb23
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 27ec170e4bef72c0b5b456738f1275ef02543024
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-dates-in-azure-cosmos-db"></a><span data-ttu-id="5b77d-103">Работа с датами в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5b77d-103">Working with Dates in Azure Cosmos DB</span></span>
<span data-ttu-id="5b77d-104">Azure Cosmos DB обеспечивает гибкость схемы данных и обширные возможности индексирования благодаря использованию собственной модели данных на основе [JSON](http://www.json.org).</span><span class="sxs-lookup"><span data-stu-id="5b77d-104">Azure Cosmos DB delivers schema flexibility and rich indexing via a native [JSON](http://www.json.org) data model.</span></span> <span data-ttu-id="5b77d-105">Все ресурсы Azure Cosmos DB, включая базы данных, коллекции, документы и хранимые процедуры, моделируются и хранятся в виде документов JSON.</span><span class="sxs-lookup"><span data-stu-id="5b77d-105">All Azure Cosmos DB resources including databases, collections, documents, and stored procedures are modeled and stored as JSON documents.</span></span> <span data-ttu-id="5b77d-106">Чтобы гарантировать свойство переносимости, JSON (и Azure Cosmos DB) поддерживает только небольшой набор основных типов: строка, число, логическое значение, массив, объект и Null.</span><span class="sxs-lookup"><span data-stu-id="5b77d-106">As a requirement for being portable, JSON (and Azure Cosmos DB) supports only a small set of basic types: String, Number, Boolean, Array, Object, and Null.</span></span> <span data-ttu-id="5b77d-107">Тем не менее JSON является гибким и позволяют разработчикам и платформ toorepresent более сложных типов с помощью следующих примитивов и составление их как объекты или массивы.</span><span class="sxs-lookup"><span data-stu-id="5b77d-107">However, JSON is flexible and allow developers and frameworks toorepresent more complex types using these primitives and composing them as objects or arrays.</span></span> 

<span data-ttu-id="5b77d-108">В дополнение toohello базовых типов, многие приложения должны hello [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) введите даты toorepresent и отметки времени.</span><span class="sxs-lookup"><span data-stu-id="5b77d-108">In addition toohello basic types, many applications need hello [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) type toorepresent dates and timestamps.</span></span> <span data-ttu-id="5b77d-109">В этой статье описывается, как разработчики могут хранить, извлечения и запрос даты в базу данных Cosmos Azure, используя hello .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="5b77d-109">This article describes how developers can store, retrieve, and query dates in Azure Cosmos DB using hello .NET SDK.</span></span>

## <a name="storing-datetimes"></a><span data-ttu-id="5b77d-110">Хранение значений даты и времени</span><span class="sxs-lookup"><span data-stu-id="5b77d-110">Storing DateTimes</span></span>
<span data-ttu-id="5b77d-111">По умолчанию hello [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) сериализует значения DateTime как [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) строки.</span><span class="sxs-lookup"><span data-stu-id="5b77d-111">By default, hello [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) serializes DateTime values as [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) strings.</span></span> <span data-ttu-id="5b77d-112">Большинство приложений можно использовать строковое представление по умолчанию hello объекта DateTime для hello следующих причин:</span><span class="sxs-lookup"><span data-stu-id="5b77d-112">Most applications can use hello default string representation for DateTime for hello following reasons:</span></span>

* <span data-ttu-id="5b77d-113">Сравнение строк может выполняться и hello относительный порядок hello значений даты и времени сохраняется при преобразованный toostrings.</span><span class="sxs-lookup"><span data-stu-id="5b77d-113">Strings can be compared, and hello relative ordering of hello DateTime values is preserved when they are transformed toostrings.</span></span> 
* <span data-ttu-id="5b77d-114">не требует создавать пользовательский код или специальные атрибуты для преобразования JSON;</span><span class="sxs-lookup"><span data-stu-id="5b77d-114">This approach doesn't require any custom code or attributes for JSON conversion.</span></span>
* <span data-ttu-id="5b77d-115">Hello даты, как хранятся в формате JSON доступны для чтения.</span><span class="sxs-lookup"><span data-stu-id="5b77d-115">hello dates as stored in JSON are human readable.</span></span>
* <span data-ttu-id="5b77d-116">Позволяет воспользоваться преимуществами индексов Azure Cosmos DB для быстрой обработки запросов.</span><span class="sxs-lookup"><span data-stu-id="5b77d-116">This approach can take advantage of Azure Cosmos DB's index for fast query performance.</span></span>

<span data-ttu-id="5b77d-117">Здравствуйте, например, следующий фрагмент хранилищ `Order` объекта, содержащего два свойства даты и времени — `ShipDate` и `OrderDate` как документ с помощью hello .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="5b77d-117">For example, hello following snippet stores an `Order` object containing two DateTime properties - `ShipDate` and `OrderDate` as a document using hello .NET SDK:</span></span>

    public class Order
    {
        [JsonProperty(PropertyName="id")]
        public string Id { get; set; }
        public DateTime OrderDate { get; set; }
        public DateTime ShipDate { get; set; }
        public double Total { get; set; }
    }

    await client.CreateDocumentAsync("/dbs/orderdb/colls/orders", 
        new Order 
        { 
            Id = "09152014101",
            OrderDate = DateTime.UtcNow.AddDays(-30),
            ShipDate = DateTime.UtcNow.AddDays(-14), 
            Total = 113.39
        });

<span data-ttu-id="5b77d-118">Этот документ хранится в Azure Cosmos DB в следующем виде:</span><span class="sxs-lookup"><span data-stu-id="5b77d-118">This document is stored in Azure Cosmos DB as follows:</span></span>

    {
        "id": "09152014101",
        "OrderDate": "2014-09-15T23:14:25.7251173Z",
        "ShipDate": "2014-09-30T23:14:25.7251173Z",
        "Total": 113.39
    }
    

<span data-ttu-id="5b77d-119">Кроме того можно хранить даты как отметки времени Unix, т. е как число, представляющее количество hello в секундах, прошедшее с 1 января 1970 года.</span><span class="sxs-lookup"><span data-stu-id="5b77d-119">Alternatively, you can store DateTimes as Unix timestamps, that is, as a number representing hello number of elapsed seconds since January 1, 1970.</span></span> <span data-ttu-id="5b77d-120">Внутреннее свойство Azure Cosmos DB для отметки времени (`_ts`) использует именно этот подход.</span><span class="sxs-lookup"><span data-stu-id="5b77d-120">Azure Cosmos DB's internal Timestamp (`_ts`) property follows this approach.</span></span> <span data-ttu-id="5b77d-121">Можно использовать hello [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) класса tooserialize даты как числа.</span><span class="sxs-lookup"><span data-stu-id="5b77d-121">You can use hello [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) class tooserialize DateTimes as numbers.</span></span> 

## <a name="indexing-datetimes-for-range-queries"></a><span data-ttu-id="5b77d-122">Индексирование значений даты и времени для запросов в диапазоне</span><span class="sxs-lookup"><span data-stu-id="5b77d-122">Indexing DateTimes for range queries</span></span>
<span data-ttu-id="5b77d-123">Запросы в диапазоне часто применяются для значений даты и времени.</span><span class="sxs-lookup"><span data-stu-id="5b77d-123">Range queries are common with DateTime values.</span></span> <span data-ttu-id="5b77d-124">Например если требуется toofind все заказы, созданные со вчерашнего дня, или найти все заказы, входящий в комплект поставки hello последние пять минут, необходимо tooperform запросов в диапазоне.</span><span class="sxs-lookup"><span data-stu-id="5b77d-124">For example, if you need toofind all orders created since yesterday, or find all orders shipped in hello last five minutes, you need tooperform range queries.</span></span> <span data-ttu-id="5b77d-125">Эти запросы, эффективно tooexecute, необходимо настроить коллекции для индексирования диапазон строк.</span><span class="sxs-lookup"><span data-stu-id="5b77d-125">tooexecute these queries efficiently, you must configure your collection for Range indexing on strings.</span></span>

    DocumentCollection collection = new DocumentCollection { Id = "orders" };
    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    await client.CreateDocumentCollectionAsync("/dbs/orderdb", collection);

<span data-ttu-id="5b77d-126">Дополнительные сведения о том, как индексирование политик на tooconfigure [политики индексирования Azure Cosmos DB](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="5b77d-126">You can learn more about how tooconfigure indexing policies at [Azure Cosmos DB Indexing Policies](indexing-policies.md).</span></span>

## <a name="querying-datetimes-in-linq"></a><span data-ttu-id="5b77d-127">Запрос по датам и времени в LINQ</span><span class="sxs-lookup"><span data-stu-id="5b77d-127">Querying DateTimes in LINQ</span></span>
<span data-ttu-id="5b77d-128">Hello DocumentDB .NET SDK автоматически поддерживает запросы к данным, хранящимся в базе данных Azure Cosmos через LINQ.</span><span class="sxs-lookup"><span data-stu-id="5b77d-128">hello DocumentDB .NET SDK automatically supports querying data stored in Azure Cosmos DB via LINQ.</span></span> <span data-ttu-id="5b77d-129">Например hello следующем фрагменте кода показан запрос LINQ заказов, фильтры, которые поставлялись в hello последние три дня.</span><span class="sxs-lookup"><span data-stu-id="5b77d-129">For example, hello following snippet shows a LINQ query that filters orders that were shipped in hello last three days.</span></span>

    IQueryable<Order> orders = client.CreateDocumentQuery<Order>("/dbs/orderdb/colls/orders")
        .Where(o => o.ShipDate >= DateTime.UtcNow.AddDays(-3));
          
    // Translated toohello following SQL statement and executed on Azure Cosmos DB
    SELECT * FROM root WHERE (root["ShipDate"] >= "2016-12-18T21:55:03.45569Z")

<span data-ttu-id="5b77d-130">Дополнительные сведения о Azure Cosmos DB поставщик запросов SQL языка и hello LINQ на [запрос DB Cosmos](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="5b77d-130">You can learn more about Azure Cosmos DB's SQL query language and hello LINQ provider at [Querying Cosmos DB](documentdb-sql-query.md).</span></span>

<span data-ttu-id="5b77d-131">В этой статье мы рассмотрели как toostore, и индекс и запрос даты в базе данных Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5b77d-131">In this article, we looked at how toostore, index, and query DateTimes in Azure Cosmos DB.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b77d-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5b77d-132">Next Steps</span></span>
* <span data-ttu-id="5b77d-133">Загрузите и запустите hello [код примеров на GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span><span class="sxs-lookup"><span data-stu-id="5b77d-133">Download and run hello [Code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span></span>
* <span data-ttu-id="5b77d-134">Узнайте подробнее о [запросах API в DocumentDB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="5b77d-134">Learn more about [DocumentDB API Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="5b77d-135">Дополнительные сведения о политиках индексации в Azure Cosmos DB см. в [этой статье](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="5b77d-135">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>
