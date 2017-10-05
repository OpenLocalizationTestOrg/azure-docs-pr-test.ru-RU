---
title: "Работа с датами в Azure Cosmos DB | Документация Майкрософт"
description: "Сведения о работе с датами в Azure Cosmos DB."
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
ms.openlocfilehash: b6a77e33eea24000037ffb31d7aae3cb1d345ce9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="working-with-dates-in-azure-cosmos-db"></a><span data-ttu-id="71e74-103">Работа с датами в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="71e74-103">Working with Dates in Azure Cosmos DB</span></span>
<span data-ttu-id="71e74-104">Azure Cosmos DB обеспечивает гибкость схемы данных и обширные возможности индексирования благодаря использованию собственной модели данных на основе [JSON](http://www.json.org).</span><span class="sxs-lookup"><span data-stu-id="71e74-104">Azure Cosmos DB delivers schema flexibility and rich indexing via a native [JSON](http://www.json.org) data model.</span></span> <span data-ttu-id="71e74-105">Все ресурсы Azure Cosmos DB, включая базы данных, коллекции, документы и хранимые процедуры, моделируются и хранятся в виде документов JSON.</span><span class="sxs-lookup"><span data-stu-id="71e74-105">All Azure Cosmos DB resources including databases, collections, documents, and stored procedures are modeled and stored as JSON documents.</span></span> <span data-ttu-id="71e74-106">Чтобы гарантировать свойство переносимости, JSON (и Azure Cosmos DB) поддерживает только небольшой набор основных типов: строка, число, логическое значение, массив, объект и Null.</span><span class="sxs-lookup"><span data-stu-id="71e74-106">As a requirement for being portable, JSON (and Azure Cosmos DB) supports only a small set of basic types: String, Number, Boolean, Array, Object, and Null.</span></span> <span data-ttu-id="71e74-107">Но JSON благодаря своей гибкости позволяет разработчикам и платформам моделировать и более сложные типы, составляя их из поддерживаемых примитивов в виде объектов или массивов.</span><span class="sxs-lookup"><span data-stu-id="71e74-107">However, JSON is flexible and allow developers and frameworks to represent more complex types using these primitives and composing them as objects or arrays.</span></span> 

<span data-ttu-id="71e74-108">Помимо основных типов многим приложениям требуется формат [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) для представления дат и отметок времени.</span><span class="sxs-lookup"><span data-stu-id="71e74-108">In addition to the basic types, many applications need the [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) type to represent dates and timestamps.</span></span> <span data-ttu-id="71e74-109">В этой статье описывается, как разработчики могут хранить, извлекать и искать даты в Azure Cosmos DB с помощью пакета SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="71e74-109">This article describes how developers can store, retrieve, and query dates in Azure Cosmos DB using the .NET SDK.</span></span>

## <a name="storing-datetimes"></a><span data-ttu-id="71e74-110">Хранение значений даты и времени</span><span class="sxs-lookup"><span data-stu-id="71e74-110">Storing DateTimes</span></span>
<span data-ttu-id="71e74-111">По умолчанию [пакет SDK для Azure Cosmos DB](documentdb-sdk-dotnet.md) сериализует значения даты и времени в формате строк [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874).</span><span class="sxs-lookup"><span data-stu-id="71e74-111">By default, the [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) serializes DateTime values as [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) strings.</span></span> <span data-ttu-id="71e74-112">Многим приложениям вполне достаточно используемого по умолчанию строкового представления дат и времени, поскольку оно:</span><span class="sxs-lookup"><span data-stu-id="71e74-112">Most applications can use the default string representation for DateTime for the following reasons:</span></span>

* <span data-ttu-id="71e74-113">позволяет сравнивать строки, а следовательно и сохранять относительный порядок значений даты и времени, после преобразования в строки;</span><span class="sxs-lookup"><span data-stu-id="71e74-113">Strings can be compared, and the relative ordering of the DateTime values is preserved when they are transformed to strings.</span></span> 
* <span data-ttu-id="71e74-114">не требует создавать пользовательский код или специальные атрибуты для преобразования JSON;</span><span class="sxs-lookup"><span data-stu-id="71e74-114">This approach doesn't require any custom code or attributes for JSON conversion.</span></span>
* <span data-ttu-id="71e74-115">сохраняет даты в понятном для человека формате JSON;</span><span class="sxs-lookup"><span data-stu-id="71e74-115">The dates as stored in JSON are human readable.</span></span>
* <span data-ttu-id="71e74-116">Позволяет воспользоваться преимуществами индексов Azure Cosmos DB для быстрой обработки запросов.</span><span class="sxs-lookup"><span data-stu-id="71e74-116">This approach can take advantage of Azure Cosmos DB's index for fast query performance.</span></span>

<span data-ttu-id="71e74-117">Например, следующий фрагмент кода сохраняет объект `Order`, содержащий два свойства в формате даты и времени (`ShipDate` и `OrderDate`) в виде документа, использующего пакет SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="71e74-117">For example, the following snippet stores an `Order` object containing two DateTime properties - `ShipDate` and `OrderDate` as a document using the .NET SDK:</span></span>

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

<span data-ttu-id="71e74-118">Этот документ хранится в Azure Cosmos DB в следующем виде:</span><span class="sxs-lookup"><span data-stu-id="71e74-118">This document is stored in Azure Cosmos DB as follows:</span></span>

    {
        "id": "09152014101",
        "OrderDate": "2014-09-15T23:14:25.7251173Z",
        "ShipDate": "2014-09-30T23:14:25.7251173Z",
        "Total": 113.39
    }
    

<span data-ttu-id="71e74-119">Кроме того, вы можете хранить даты как отметки времени Unix, то есть как число, представляющее количество секунд, прошедших с 1 января 1970 года.</span><span class="sxs-lookup"><span data-stu-id="71e74-119">Alternatively, you can store DateTimes as Unix timestamps, that is, as a number representing the number of elapsed seconds since January 1, 1970.</span></span> <span data-ttu-id="71e74-120">Внутреннее свойство Azure Cosmos DB для отметки времени (`_ts`) использует именно этот подход.</span><span class="sxs-lookup"><span data-stu-id="71e74-120">Azure Cosmos DB's internal Timestamp (`_ts`) property follows this approach.</span></span> <span data-ttu-id="71e74-121">Для сериализации значений даты и времени в числа используйте класс [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx).</span><span class="sxs-lookup"><span data-stu-id="71e74-121">You can use the [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) class to serialize DateTimes as numbers.</span></span> 

## <a name="indexing-datetimes-for-range-queries"></a><span data-ttu-id="71e74-122">Индексирование значений даты и времени для запросов в диапазоне</span><span class="sxs-lookup"><span data-stu-id="71e74-122">Indexing DateTimes for range queries</span></span>
<span data-ttu-id="71e74-123">Запросы в диапазоне часто применяются для значений даты и времени.</span><span class="sxs-lookup"><span data-stu-id="71e74-123">Range queries are common with DateTime values.</span></span> <span data-ttu-id="71e74-124">Например, они позволяют найти все заказы, созданные не позднее вчерашнего дня, или все заказы, отправленные за последние пять минут.</span><span class="sxs-lookup"><span data-stu-id="71e74-124">For example, if you need to find all orders created since yesterday, or find all orders shipped in the last five minutes, you need to perform range queries.</span></span> <span data-ttu-id="71e74-125">Для эффективного выполнения таких запросов вам потребуется коллекция для индексирования строк по диапазонам.</span><span class="sxs-lookup"><span data-stu-id="71e74-125">To execute these queries efficiently, you must configure your collection for Range indexing on strings.</span></span>

    DocumentCollection collection = new DocumentCollection { Id = "orders" };
    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    await client.CreateDocumentCollectionAsync("/dbs/orderdb", collection);

<span data-ttu-id="71e74-126">Дополнительные сведения о настройке политик индексирования см. в статье [Как работает индексирование данных в Azure Cosmos DB?](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="71e74-126">You can learn more about how to configure indexing policies at [Azure Cosmos DB Indexing Policies](indexing-policies.md).</span></span>

## <a name="querying-datetimes-in-linq"></a><span data-ttu-id="71e74-127">Запрос по датам и времени в LINQ</span><span class="sxs-lookup"><span data-stu-id="71e74-127">Querying DateTimes in LINQ</span></span>
<span data-ttu-id="71e74-128">Пакет DocumentDB SDK для .NET автоматически поддерживает запросы с использованием LINQ к данным, хранящимся в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="71e74-128">The DocumentDB .NET SDK automatically supports querying data stored in Azure Cosmos DB via LINQ.</span></span> <span data-ttu-id="71e74-129">Например следующий фрагмент кода демонстрирует запрос LINQ, который отбирает все заказы, доставленные за последние три дня.</span><span class="sxs-lookup"><span data-stu-id="71e74-129">For example, the following snippet shows a LINQ query that filters orders that were shipped in the last three days.</span></span>

    IQueryable<Order> orders = client.CreateDocumentQuery<Order>("/dbs/orderdb/colls/orders")
        .Where(o => o.ShipDate >= DateTime.UtcNow.AddDays(-3));
          
    // Translated to the following SQL statement and executed on Azure Cosmos DB
    SELECT * FROM root WHERE (root["ShipDate"] >= "2016-12-18T21:55:03.45569Z")

<span data-ttu-id="71e74-130">Дополнительные сведения о языке запросов SQL в Azure Cosmos DB и о поставщике LINQ см. в статье [SQL-запросы для API DocumentDB в Azure Cosmos DB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="71e74-130">You can learn more about Azure Cosmos DB's SQL query language and the LINQ provider at [Querying Cosmos DB](documentdb-sql-query.md).</span></span>

<span data-ttu-id="71e74-131">В этой статье мы рассмотрели способы хранения, индексирования и получения значений дат и времени в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="71e74-131">In this article, we looked at how to store, index, and query DateTimes in Azure Cosmos DB.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71e74-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="71e74-132">Next Steps</span></span>
* <span data-ttu-id="71e74-133">Скачайте и запустите [примеры кода, хранящиеся на GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples).</span><span class="sxs-lookup"><span data-stu-id="71e74-133">Download and run the [Code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)</span></span>
* <span data-ttu-id="71e74-134">Узнайте подробнее о [запросах API в DocumentDB](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="71e74-134">Learn more about [DocumentDB API Query](documentdb-sql-query.md)</span></span>
* <span data-ttu-id="71e74-135">Дополнительные сведения о политиках индексации в Azure Cosmos DB см. в [этой статье](indexing-policies.md).</span><span class="sxs-lookup"><span data-stu-id="71e74-135">Learn more about [Azure Cosmos DB Indexing Policies](indexing-policies.md)</span></span>
