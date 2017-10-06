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
# <a name="working-with-dates-in-azure-cosmos-db"></a>Работа с датами в Azure Cosmos DB
Azure Cosmos DB обеспечивает гибкость схемы данных и обширные возможности индексирования благодаря использованию собственной модели данных на основе [JSON](http://www.json.org). Все ресурсы Azure Cosmos DB, включая базы данных, коллекции, документы и хранимые процедуры, моделируются и хранятся в виде документов JSON. Чтобы гарантировать свойство переносимости, JSON (и Azure Cosmos DB) поддерживает только небольшой набор основных типов: строка, число, логическое значение, массив, объект и Null. Тем не менее JSON является гибким и позволяют разработчикам и платформ toorepresent более сложных типов с помощью следующих примитивов и составление их как объекты или массивы. 

В дополнение toohello базовых типов, многие приложения должны hello [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx) введите даты toorepresent и отметки времени. В этой статье описывается, как разработчики могут хранить, извлечения и запрос даты в базу данных Cosmos Azure, используя hello .NET SDK.

## <a name="storing-datetimes"></a>Хранение значений даты и времени
По умолчанию hello [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) сериализует значения DateTime как [ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874) строки. Большинство приложений можно использовать строковое представление по умолчанию hello объекта DateTime для hello следующих причин:

* Сравнение строк может выполняться и hello относительный порядок hello значений даты и времени сохраняется при преобразованный toostrings. 
* не требует создавать пользовательский код или специальные атрибуты для преобразования JSON;
* Hello даты, как хранятся в формате JSON доступны для чтения.
* Позволяет воспользоваться преимуществами индексов Azure Cosmos DB для быстрой обработки запросов.

Здравствуйте, например, следующий фрагмент хранилищ `Order` объекта, содержащего два свойства даты и времени — `ShipDate` и `OrderDate` как документ с помощью hello .NET SDK:

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

Этот документ хранится в Azure Cosmos DB в следующем виде:

    {
        "id": "09152014101",
        "OrderDate": "2014-09-15T23:14:25.7251173Z",
        "ShipDate": "2014-09-30T23:14:25.7251173Z",
        "Total": 113.39
    }
    

Кроме того можно хранить даты как отметки времени Unix, т. е как число, представляющее количество hello в секундах, прошедшее с 1 января 1970 года. Внутреннее свойство Azure Cosmos DB для отметки времени (`_ts`) использует именно этот подход. Можно использовать hello [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx) класса tooserialize даты как числа. 

## <a name="indexing-datetimes-for-range-queries"></a>Индексирование значений даты и времени для запросов в диапазоне
Запросы в диапазоне часто применяются для значений даты и времени. Например если требуется toofind все заказы, созданные со вчерашнего дня, или найти все заказы, входящий в комплект поставки hello последние пять минут, необходимо tooperform запросов в диапазоне. Эти запросы, эффективно tooexecute, необходимо настроить коллекции для индексирования диапазон строк.

    DocumentCollection collection = new DocumentCollection { Id = "orders" };
    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    await client.CreateDocumentCollectionAsync("/dbs/orderdb", collection);

Дополнительные сведения о том, как индексирование политик на tooconfigure [политики индексирования Azure Cosmos DB](indexing-policies.md).

## <a name="querying-datetimes-in-linq"></a>Запрос по датам и времени в LINQ
Hello DocumentDB .NET SDK автоматически поддерживает запросы к данным, хранящимся в базе данных Azure Cosmos через LINQ. Например hello следующем фрагменте кода показан запрос LINQ заказов, фильтры, которые поставлялись в hello последние три дня.

    IQueryable<Order> orders = client.CreateDocumentQuery<Order>("/dbs/orderdb/colls/orders")
        .Where(o => o.ShipDate >= DateTime.UtcNow.AddDays(-3));
          
    // Translated toohello following SQL statement and executed on Azure Cosmos DB
    SELECT * FROM root WHERE (root["ShipDate"] >= "2016-12-18T21:55:03.45569Z")

Дополнительные сведения о Azure Cosmos DB поставщик запросов SQL языка и hello LINQ на [запрос DB Cosmos](documentdb-sql-query.md).

В этой статье мы рассмотрели как toostore, и индекс и запрос даты в базе данных Azure Cosmos.

## <a name="next-steps"></a>Дальнейшие действия
* Загрузите и запустите hello [код примеров на GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)
* Узнайте подробнее о [запросах API в DocumentDB](documentdb-sql-query.md).
* Дополнительные сведения о политиках индексации в Azure Cosmos DB см. в [этой статье](indexing-policies.md).
