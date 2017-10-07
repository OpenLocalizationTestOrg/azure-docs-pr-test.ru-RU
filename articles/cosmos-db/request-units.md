---
title: "aaaRequest единицы измерения и оценка пропускной способности - Azure Cosmos DB | Документы Microsoft"
description: "Узнайте, как toounderstand, укажите и Оценка требований к объему единица запроса в базе данных Azure Cosmos."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: d0a3c310-eb63-4e45-8122-b7724095c32f
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 13c4e7aeb6222fa14ef982e238716e15a0159fd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-in-azure-cosmos-db"></a><span data-ttu-id="bc1a1-103">Единицы запросов в базе данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bc1a1-103">Request Units in Azure Cosmos DB</span></span>
<span data-ttu-id="bc1a1-104">На странице базы данных Azure Cosmos DB теперь доступен [калькулятор единиц запросов](https://www.documentdb.com/capacityplanner).</span><span class="sxs-lookup"><span data-stu-id="bc1a1-104">Now available: Azure Cosmos DB [request unit calculator](https://www.documentdb.com/capacityplanner).</span></span> <span data-ttu-id="bc1a1-105">Дополнительные сведения см. в разделе [Оценка требований к пропускной способности](request-units.md#estimating-throughput-needs).</span><span class="sxs-lookup"><span data-stu-id="bc1a1-105">Learn more in [Estimating your throughput needs](request-units.md#estimating-throughput-needs).</span></span>

![Калькулятор пропускной способности][5]

## <a name="introduction"></a><span data-ttu-id="bc1a1-107">Введение</span><span class="sxs-lookup"><span data-stu-id="bc1a1-107">Introduction</span></span>
<span data-ttu-id="bc1a1-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) — это глобально распределенная многомодельная база данных Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is Microsoft's globally distributed multi-model database.</span></span> <span data-ttu-id="bc1a1-109">DB Cosmos Azure не имеют toorent виртуальных машин, развертывание программного обеспечения или наблюдение за базами данных.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-109">With Azure Cosmos DB, you don't have toorent virtual machines, deploy software, or monitor databases.</span></span> <span data-ttu-id="bc1a1-110">Azure Cosmos DB работать и постоянно отслеживает top инженеров toodeliver world класс доступности, производительности и данных защиты Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-110">Azure Cosmos DB is operated and continuously monitored by Microsoft top engineers toodeliver world class availability, performance, and data protection.</span></span> <span data-ttu-id="bc1a1-111">Вы можете получить доступ к своим данным, используя выбранные API, так как [DocumentDB SQL](documentdb-sql-query.md) (документ), MongoDB (документ), [Хранилище таблиц Azure](https://azure.microsoft.com/services/storage/tables/) (ключ — значение) и [Gremlin](https://tinkerpop.apache.org/gremlin.html) (Graph) поддерживаются изначально.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-111">You can access your data using APIs of your choice, as [DocumentDB SQL](documentdb-sql-query.md) (document), MongoDB (document), [Azure Table Storage](https://azure.microsoft.com/services/storage/tables/) (key-value), and [Gremlin](https://tinkerpop.apache.org/gremlin.html) (graph) are all natively supported.</span></span> <span data-ttu-id="bc1a1-112">Валюта Hello Azure Cosmos DB — hello запроса единицы (RU).</span><span class="sxs-lookup"><span data-stu-id="bc1a1-112">hello currency of Azure Cosmos DB is hello Request Unit (RU).</span></span> <span data-ttu-id="bc1a1-113">С RUs необязательно tooreserve возможности чтения и записи или подготовки ЦП, памяти и операций ввода-ВЫВОДА.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-113">With RUs, you do not need tooreserve read/write capacities or provision CPU, Memory and IOPS.</span></span>

<span data-ttu-id="bc1a1-114">Azure Cosmos DB поддерживает несколько API-интерфейсов с помощью различных операций, начиная от простых операций чтения и записи toocomplex запросы graph.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-114">Azure Cosmos DB supports a number of APIs with different operations ranging from simple reads and writes toocomplex graph queries.</span></span> <span data-ttu-id="bc1a1-115">Так как не все запросы равны, они назначаются нормализованное количество **единиц запросов** hello объемом вычислений требуется tooserve hello запроса.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-115">Since not all requests are equal, they are assigned a normalized quantity of **request units** based on hello amount of computation required tooserve hello request.</span></span> <span data-ttu-id="bc1a1-116">Детерминирована Hello количество единиц запроса для операции, и можно отслеживать hello количество единиц запроса, потребляемых любой операции в базе данных Azure Cosmos через заголовок ответа.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-116">hello number of request units for an operation is deterministic, and you can track hello number of request units consumed by any operation in Azure Cosmos DB via a response header.</span></span> 

<span data-ttu-id="bc1a1-117">tooprovide предсказуемой производительности, необходимо tooreserve пропускной способности в единицах 100 единиц Запросов в секунду.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-117">tooprovide predictable performance, you need tooreserve throughput in units of 100 RU/second.</span></span> 

<span data-ttu-id="bc1a1-118">После считывания в этой статье, вы будете иметь доступ tooanswer hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="bc1a1-118">After reading this article, you'll be able tooanswer hello following questions:</span></span>  

* <span data-ttu-id="bc1a1-119">Что такое единицы запросов и затраты на запросы?</span><span class="sxs-lookup"><span data-stu-id="bc1a1-119">What are request units and request charges?</span></span>
* <span data-ttu-id="bc1a1-120">Как задать количество единиц запросов для одной коллекции?</span><span class="sxs-lookup"><span data-stu-id="bc1a1-120">How do I specify request unit capacity for a collection?</span></span>
* <span data-ttu-id="bc1a1-121">Как оценить приемлемое количество единиц запросов для моего приложения?</span><span class="sxs-lookup"><span data-stu-id="bc1a1-121">How do I estimate my application's request unit needs?</span></span>
* <span data-ttu-id="bc1a1-122">Что произойдет, если превысить максимальное количество единиц запросов для одной коллекции?</span><span class="sxs-lookup"><span data-stu-id="bc1a1-122">What happens if I exceed request unit capacity for a collection?</span></span>

<span data-ttu-id="bc1a1-123">Как Azure Cosmos DB моделей базы данных, это важно toonote, что мы будем называть tooa коллекции или документа для документа API, диаграммы или узел для graph API и сущности или таблицы для таблицы API.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-123">As Azure Cosmos DB is a multi-model database, it is important toonote that we will refer tooa collection/document for a document API, a graph/node for a graph API and a table/entity for table API.</span></span> <span data-ttu-id="bc1a1-124">Пропускная способность в этом документе, Обобщим toohello понятия контейнера или элемента.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-124">Throughput this document we will generalize toohello concepts of container/item.</span></span>

## <a name="request-units-and-request-charges"></a><span data-ttu-id="bc1a1-125">Единицы запросов и затраты на запросы</span><span class="sxs-lookup"><span data-stu-id="bc1a1-125">Request units and request charges</span></span>
<span data-ttu-id="bc1a1-126">Azure Cosmos DB обеспечивает быстрый и предсказуемое производительность по *резервирование* toosatisfy ресурсов должен пропускную способность приложения.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-126">Azure Cosmos DB delivers fast, predictable performance by *reserving* resources toosatisfy your application's throughput needs.</span></span>  <span data-ttu-id="bc1a1-127">Поскольку приложения загрузки и доступ к шаблоны изменяются с течением времени, Azure Cosmos DB позволяет увеличить tooeasily или уменьшить hello объем зарезервированной пропускной способностью доступных tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-127">Because application load and access patterns change over time, Azure Cosmos DB allows you tooeasily increase or decrease hello amount of reserved throughput available tooyour application.</span></span>

<span data-ttu-id="bc1a1-128">В Azure Cosmos DB зарезервированная пропускная способность указывается в обрабатываемых единицах запросов в секунду.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-128">With Azure Cosmos DB, reserved throughput is specified in terms of request units processing per second.</span></span> <span data-ttu-id="bc1a1-129">Можно представить единиц запросов в денежном формате пропускной способности, при котором вы *зарезервировать* объем гарантируется единиц запроса доступных tooyour приложения на основе за секунду.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-129">You can think of request units as throughput currency, whereby you *reserve* an amount of guaranteed request units available tooyour application on per second basis.</span></span>  <span data-ttu-id="bc1a1-130">Каждая операция в Azure Cosmos DB (например, создание документа, выполнение запроса, обновление документа) сопровождается потреблением ресурсов ЦП, объема памяти и выполнением операций ввода-вывода.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-130">Each operation in Azure Cosmos DB - writing a document, performing a query, updating a document - consumes CPU, memory, and IOPS.</span></span>  <span data-ttu-id="bc1a1-131">Иными словами, при выполнении каждой операции взимается *плата за запрос*, которая выражается в *единицах запроса*.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-131">That is, each operation incurs a *request charge*, which is expressed in *request units*.</span></span>  <span data-ttu-id="bc1a1-132">Основные сведения о hello факторов, которые влияют на накладные расходы единица запроса, вместе с пропускной способности приложения, позволяет вашему приложению как затраты как можно эффективно вы toorun.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-132">Understanding hello factors which impact request unit charges, along with your application's throughput requirements, enables you toorun your application as cost effectively as possible.</span></span> <span data-ttu-id="bc1a1-133">обозреватель запроса Hello также — базовая hello tootest замечательных средства запроса.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-133">hello query explorer is also a wonderful tool tootest hello core of a query.</span></span>

<span data-ttu-id="bc1a1-134">Корпорация Майкрософт рекомендует Приступая к работе посмотрите следующие видео, где объясняется Aravind Ramachandran единиц запроса и прогнозируемую производительность с помощью Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-134">We recommend getting started by watching hello following video, where Aravind Ramachandran explains request units and predictable performance with Azure Cosmos DB.</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Predictable-Performance-with-DocumentDB/player]
> 
> 

## <a name="specifying-request-unit-capacity-in-azure-cosmos-db"></a><span data-ttu-id="bc1a1-135">Указание количества единиц запросов в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bc1a1-135">Specifying request unit capacity in Azure Cosmos DB</span></span>
<span data-ttu-id="bc1a1-136">При запуске новой коллекции, таблицы или диаграммы, можно указать номер hello единиц запросов в секунду (единиц Запросов в секунду) требуется найти зарезервированным.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-136">When starting a new collection, table or graph, you specify hello number of request units per second (RU per second) you want reserved.</span></span> <span data-ttu-id="bc1a1-137">На основе hello пропускная способность, Azure Cosmos DB выделяет коллекции физических секций toohost и разбиений/rebalances данных по секциям роста.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-137">Based on hello provisioned throughput, Azure Cosmos DB allocates physical partitions toohost your collection and splits/rebalances data across partitions as it grows.</span></span>

<span data-ttu-id="bc1a1-138">Azure Cosmos DB требуется toobe ключа секции указан, если коллекция инициализируется посредством 2500 единиц запроса или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-138">Azure Cosmos DB requires a partition key toobe specified when a collection is provisioned with 2,500 request units or higher.</span></span> <span data-ttu-id="bc1a1-139">Ключ раздела является также требуется tooscale пропускная способность вашей коллекции за пределы 2500 единиц запросов в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-139">A partition key is also required tooscale your collection's throughput beyond 2,500 request units in hello future.</span></span> <span data-ttu-id="bc1a1-140">Поэтому настоятельно рекомендуется tooconfigure [ключ раздела](partition-data.md) при создании контейнера, независимо от начальной пропускную способность.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-140">Therefore, it is highly recommended tooconfigure a [partition key](partition-data.md) when creating a container regardless of your initial throughput.</span></span> <span data-ttu-id="bc1a1-141">Поскольку данные могут иметь toobe разбиты на несколько секций, при необходимости toopick ключ раздела, который имеет большого количества элементов (100 toomillions уникальных значений) для коллекции, таблицы или диаграммы и запросы можно масштабировать единообразно, Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-141">Since your data might have toobe split across multiple partitions, it is necessary toopick a partition key that has a high cardinality (100 toomillions of distinct values) so that your collection/table/graph and requests can be scaled uniformly by Azure Cosmos DB.</span></span> 

> [!NOTE]
> <span data-ttu-id="bc1a1-142">Ключ раздела представляет собой логическую границу, а не физическую.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-142">A partition key is a logical boundary, and not a physical one.</span></span> <span data-ttu-id="bc1a1-143">Таким образом могут не toolimit hello количество значений ключа отдельного раздела.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-143">Therefore, you do not need toolimit hello number of distinct partition key values.</span></span> <span data-ttu-id="bc1a1-144">На самом деле является более четкое лучше toohave секции ключевых значений меньше, чем как Azure Cosmos DB содержит дополнительные параметры балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-144">It is in fact better toohave more distinct partition key values than less, as Azure Cosmos DB has more load balancing options.</span></span>

<span data-ttu-id="bc1a1-145">Ниже приведен фрагмент кода для создания коллекции с 3 000 единиц в секунду с использованием hello .NET SDK запроса:</span><span class="sxs-lookup"><span data-stu-id="bc1a1-145">Here is a code snippet for creating a collection with 3,000 request units per second using hello .NET SDK:</span></span>

```csharp
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000 });
```

<span data-ttu-id="bc1a1-146">Azure Cosmos DB использует модель резервирования пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-146">Azure Cosmos DB operates on a reservation model on throughput.</span></span> <span data-ttu-id="bc1a1-147">То есть, взимается плата за hello объем пропускной способности *зарезервированные*независимо от того, что пропускная способность используется активно *используется*.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-147">That is, you are billed for hello amount of throughput *reserved*, regardless of how much of that throughput is actively *used*.</span></span> <span data-ttu-id="bc1a1-148">Как приложения загрузки данных и использование шаблонов изменение быстрого масштабирования вверх и вниз hello объем зарезервированного RUs через пакеты SDK, или с помощью hello [портала Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="bc1a1-148">As your application's load, data, and usage patterns change you can easily scale up and down hello amount of reserved RUs through SDKs or using hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="bc1a1-149">Каждой коллекции и таблицы или диаграммы сопоставляются tooan `Offer` ресурс в Azure Cosmos DB, который содержит метаданные о hello пропускная способность.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-149">Each collection/table/graph are mapped tooan `Offer` resource in Azure Cosmos DB, which has metadata about hello provisioned throughput.</span></span> <span data-ttu-id="bc1a1-150">Можно изменить hello выделить пропускной способности, поиске hello соответствующего ресурса предложения для контейнера, а затем ее обновления на новое значение пропускной способности hello.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-150">You can change hello allocated throughput by looking up hello corresponding offer resource for a container, then updating it with hello new throughput value.</span></span> <span data-ttu-id="bc1a1-151">Ниже приведен фрагмент кода для изменения hello пропускной способности too5 коллекции, 000 единиц запросов в секунду с использованием hello .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-151">Here is a code snippet for changing hello throughput of a collection too5,000 request units per second using hello .NET SDK:</span></span>

```csharp
// Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
                .Where(r => r.ResourceLink == collection.SelfLink)    
                .AsEnumerable()
                .SingleOrDefault();

// Set hello throughput too5000 request units per second
offer = new OfferV2(offer, 5000);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="bc1a1-152">При изменении пропускной способности hello нет доступности toohello не влияние контейнера.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-152">There is no impact toohello availability of your container when you change hello throughput.</span></span> <span data-ttu-id="bc1a1-153">Обычно новые зарезервированные пропускной способности hello действует на приложения hello новый пропускной способности за несколько секунд.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-153">Typically hello new reserved throughput is effective within seconds on application of hello new throughput.</span></span>

## <a name="request-unit-considerations"></a><span data-ttu-id="bc1a1-154">Рекомендации по оценке необходимого количества единиц запросов</span><span class="sxs-lookup"><span data-stu-id="bc1a1-154">Request unit considerations</span></span>
<span data-ttu-id="bc1a1-155">При оценке hello количество tooreserve единиц запроса для контейнера Azure Cosmos DB, это hello важные tootake следующие переменные во внимание:</span><span class="sxs-lookup"><span data-stu-id="bc1a1-155">When estimating hello number of request units tooreserve for your Azure Cosmos DB container, it is important tootake hello following variables into consideration:</span></span>

* <span data-ttu-id="bc1a1-156">**Размер элемента.**</span><span class="sxs-lookup"><span data-stu-id="bc1a1-156">**Item size**.</span></span> <span data-ttu-id="bc1a1-157">Как размер единицы hello увеличивается tooread или не приведет к увеличению hello записи данных.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-157">As size increases hello units consumed tooread or write hello data will also increase.</span></span>
* <span data-ttu-id="bc1a1-158">**Число свойств элемента.**</span><span class="sxs-lookup"><span data-stu-id="bc1a1-158">**Item property count**.</span></span> <span data-ttu-id="bc1a1-159">При условии, что по умолчанию индексирование всех свойств, toowrite единицы потребляет hello, документ или узел/ntity увеличивается при увеличении числа свойство hello.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-159">Assuming default indexing of all properties, hello units consumed toowrite a document/node/ntity will increase as hello property count increases.</span></span>
* <span data-ttu-id="bc1a1-160">**Согласованность данных**.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-160">**Data consistency**.</span></span> <span data-ttu-id="bc1a1-161">При использовании уровней Strong или Bounded Staleness согласованности данных, дополнительных единиц будет использована tooread элементов.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-161">When using data consistency levels of Strong or Bounded Staleness, additional units will be consumed tooread items.</span></span>
* <span data-ttu-id="bc1a1-162">**Индексируемые свойства**.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-162">**Indexed properties**.</span></span> <span data-ttu-id="bc1a1-163">Свойства, которые индексируются по умолчанию, определяются политикой индексирования для каждого контейнера.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-163">An index policy on each container determines which properties are indexed by default.</span></span> <span data-ttu-id="bc1a1-164">Единицы потребления запроса можно уменьшить, ограничивая количество hello индексированных свойств или включив отложенного индексирования.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-164">You can reduce your request unit consumption by limiting hello number of indexed properties or by enabling lazy indexing.</span></span>
* <span data-ttu-id="bc1a1-165">**Индексирование документов**.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-165">**Document indexing**.</span></span> <span data-ttu-id="bc1a1-166">По умолчанию каждый элемент индексируется автоматически будет потреблять меньшего числа единиц запросов при выборе не tooindex некоторые элементы.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-166">By default each item is automatically indexed, you will consume fewer request units if you choose not tooindex some of your items.</span></span>
* <span data-ttu-id="bc1a1-167">**Шаблоны запросов**.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-167">**Query patterns**.</span></span> <span data-ttu-id="bc1a1-168">Hello сложность запроса влияет на количество единиц запроса используются для операции.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-168">hello complexity of a query impacts how many Request Units are consumed for an operation.</span></span> <span data-ttu-id="bc1a1-169">Hello количество предикатов, характер hello предикаты, проекции, количество определяемых пользователем функций и hello размер набора данных источника hello, все влияют на стоимость hello операций запросов.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-169">hello number of predicates, nature of hello predicates, projections, number of UDFs, and hello size of hello source data set all influence hello cost of query operations.</span></span>
* <span data-ttu-id="bc1a1-170">**Использование скриптов**.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-170">**Script usage**.</span></span>  <span data-ttu-id="bc1a1-171">С помощью запросов, хранимых процедурах и триггерах потреблять единиц запросов в зависимости от сложности hello hello операция не выполняется.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-171">As with queries, stored procedures and triggers consume request units based on hello complexity of hello operations being performed.</span></span> <span data-ttu-id="bc1a1-172">При разработке приложения, проверьте запрос платы hello заголовок toobetter понять, как каждая операция занимает емкость модулей запроса.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-172">As you develop your application, inspect hello request charge header toobetter understand how each operation is consuming request unit capacity.</span></span>

## <a name="estimating-throughput-needs"></a><span data-ttu-id="bc1a1-173">Оценка требований к пропускной способности</span><span class="sxs-lookup"><span data-stu-id="bc1a1-173">Estimating throughput needs</span></span>
<span data-ttu-id="bc1a1-174">Единица запроса — это нормализованная мера стоимости обработки запросов.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-174">A request unit is a normalized measure of request processing cost.</span></span> <span data-ttu-id="bc1a1-175">Единое одного запроса представляет tooread мощности обработки hello (через идентификатор или ссылку себя) одной 1 КБ, элемент, состоящий из 10 значений уникальное свойство (за исключением системных свойств).</span><span class="sxs-lookup"><span data-stu-id="bc1a1-175">A single request unit represents hello processing capacity required tooread (via self link or id) a single 1KB item consisting of 10 unique property values (excluding system properties).</span></span> <span data-ttu-id="bc1a1-176">Запрос toocreate (insert), замена или удаление hello же элементов будет занимать большего объема обработки из службы hello и тем самым единиц несколько запросов.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-176">A request toocreate (insert), replace or delete hello same item will consume more processing from hello service and thereby more request units.</span></span>   

> [!NOTE]
> <span data-ttu-id="bc1a1-177">Hello базовые единицы 1 запрос для 1 КБ элемент соответствует tooa простой получить по ссылке себя или идентификатор элемента hello.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-177">hello baseline of 1 request unit for a 1KB item corresponds tooa simple GET by self link or id of hello item.</span></span>
> 
> 

<span data-ttu-id="bc1a1-178">Например, вот таблицу, которая показывает, сколько запросов tooprovision единиц на трех размеров другой элемент (1 КБ, размером 4 КБ и 64 КБ) и две разные уровни производительности (500 операций чтения/сек + 100 операций записи/сек и 500 операций чтения/сек + 500 операций записи/сек).</span><span class="sxs-lookup"><span data-stu-id="bc1a1-178">For example, here's a table that shows how many request units tooprovision at three different item sizes (1KB, 4KB, and 64KB) and at two different performance levels (500 reads/second + 100 writes/second and 500 reads/second + 500 writes/second).</span></span> <span data-ttu-id="bc1a1-179">согласованность данных Hello был настроен в сеансе, а политика индексирования hello был задан tooNone.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-179">hello data consistency was configured at Session, and hello indexing policy was set tooNone.</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="bc1a1-180"><strong>Размер элемента</strong></span><span class="sxs-lookup"><span data-stu-id="bc1a1-180"><strong>Item size</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="bc1a1-181"><strong>Операций чтения в секунду</strong></span><span class="sxs-lookup"><span data-stu-id="bc1a1-181"><strong>Reads/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="bc1a1-182"><strong>Операций записи в секунду</strong></span><span class="sxs-lookup"><span data-stu-id="bc1a1-182"><strong>Writes/second</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="bc1a1-183"><strong>Единиц запросов</strong></span><span class="sxs-lookup"><span data-stu-id="bc1a1-183"><strong>Request units</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="bc1a1-184">1 КБ</span><span class="sxs-lookup"><span data-stu-id="bc1a1-184">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="bc1a1-185">500</span><span class="sxs-lookup"><span data-stu-id="bc1a1-185">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="bc1a1-186">100</span><span class="sxs-lookup"><span data-stu-id="bc1a1-186">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="bc1a1-187">(500 * 1) + (100 * 5) = 1000 единиц запросов в секунду</span><span class="sxs-lookup"><span data-stu-id="bc1a1-187">(500 * 1) + (100 * 5) = 1,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="bc1a1-188">1 КБ</span><span class="sxs-lookup"><span data-stu-id="bc1a1-188">1 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="bc1a1-189">500</span><span class="sxs-lookup"><span data-stu-id="bc1a1-189">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="bc1a1-190">500</span><span class="sxs-lookup"><span data-stu-id="bc1a1-190">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="bc1a1-191">(500 * 1) + (500 * 5) = 3000 единиц запросов в секунду</span><span class="sxs-lookup"><span data-stu-id="bc1a1-191">(500 * 1) + (500 * 5) = 3,000 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="bc1a1-192">4 КБ</span><span class="sxs-lookup"><span data-stu-id="bc1a1-192">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="bc1a1-193">500</span><span class="sxs-lookup"><span data-stu-id="bc1a1-193">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="bc1a1-194">100</span><span class="sxs-lookup"><span data-stu-id="bc1a1-194">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="bc1a1-195">(500 * 1,3) + (100 * 7) = 1350 единиц запросов в секунду</span><span class="sxs-lookup"><span data-stu-id="bc1a1-195">(500 * 1.3) + (100 * 7) = 1,350 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="bc1a1-196">4 КБ</span><span class="sxs-lookup"><span data-stu-id="bc1a1-196">4 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="bc1a1-197">500</span><span class="sxs-lookup"><span data-stu-id="bc1a1-197">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="bc1a1-198">500</span><span class="sxs-lookup"><span data-stu-id="bc1a1-198">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="bc1a1-199">(500 * 1,3) + (500 * 7) = 4150 единиц запросов в секунду</span><span class="sxs-lookup"><span data-stu-id="bc1a1-199">(500 * 1.3) + (500 * 7) = 4,150 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="bc1a1-200">64 КБ</span><span class="sxs-lookup"><span data-stu-id="bc1a1-200">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="bc1a1-201">500</span><span class="sxs-lookup"><span data-stu-id="bc1a1-201">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="bc1a1-202">100</span><span class="sxs-lookup"><span data-stu-id="bc1a1-202">100</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="bc1a1-203">(500 * 10) + (100 * 48) = 9800 единиц запросов в секунду</span><span class="sxs-lookup"><span data-stu-id="bc1a1-203">(500 * 10) + (100 * 48) = 9,800 RU/s</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="bc1a1-204">64 КБ</span><span class="sxs-lookup"><span data-stu-id="bc1a1-204">64 KB</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="bc1a1-205">500</span><span class="sxs-lookup"><span data-stu-id="bc1a1-205">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="bc1a1-206">500</span><span class="sxs-lookup"><span data-stu-id="bc1a1-206">500</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="bc1a1-207">(500 * 10) + (500 * 48) = 29 000 единиц запросов в секунду</span><span class="sxs-lookup"><span data-stu-id="bc1a1-207">(500 * 10) + (500 * 48) = 29,000 RU/s</span></span></p></td>
        </tr>
    </tbody>
</table>

### <a name="use-hello-request-unit-calculator"></a><span data-ttu-id="bc1a1-208">С помощью калькулятора единица запроса hello</span><span class="sxs-lookup"><span data-stu-id="bc1a1-208">Use hello request unit calculator</span></span>
<span data-ttu-id="bc1a1-209">Клиенты toohelp нормально настраивать их оценки пропускной способности, не существует на основе веб- [калькулятора единица запроса](https://www.documentdb.com/capacityplanner) требования toohelp оценки hello запрос устройства для обычных операций, включая:</span><span class="sxs-lookup"><span data-stu-id="bc1a1-209">toohelp customers fine tune their throughput estimations, there is a web based [request unit calculator](https://www.documentdb.com/capacityplanner) toohelp estimate hello request unit requirements for typical operations, including:</span></span>

* <span data-ttu-id="bc1a1-210">операции создания элемента (запись);</span><span class="sxs-lookup"><span data-stu-id="bc1a1-210">Item creates (writes)</span></span>
* <span data-ttu-id="bc1a1-211">операции чтения элемента;</span><span class="sxs-lookup"><span data-stu-id="bc1a1-211">Item reads</span></span>
* <span data-ttu-id="bc1a1-212">операции удаления элемента;</span><span class="sxs-lookup"><span data-stu-id="bc1a1-212">Item deletes</span></span>
* <span data-ttu-id="bc1a1-213">операции обновления элемента.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-213">Item updates</span></span>

<span data-ttu-id="bc1a1-214">Средство Hello также включает поддержку Оценка потребности в хранении данных на основе элементов образец hello вами.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-214">hello tool also includes support for estimating data storage needs based on hello sample items you provide.</span></span>

<span data-ttu-id="bc1a1-215">С помощью средства hello проста:</span><span class="sxs-lookup"><span data-stu-id="bc1a1-215">Using hello tool is simple:</span></span>

1. <span data-ttu-id="bc1a1-216">Загрузите один или несколько образцов элементов.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-216">Upload one or more representative items.</span></span>
   
    ![Отправить запрос единицы элементов toohello калькулятора][2]
2. <span data-ttu-id="bc1a1-218">требования к хранилищу данных tooestimate введите hello общее число элементов, предполагается, что toostore.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-218">tooestimate data storage requirements, enter hello total number of items you expect toostore.</span></span>
3. <span data-ttu-id="bc1a1-219">Введите hello количество элементов создание, чтение, обновление и удаление операций требуется (на основе в секунду).</span><span class="sxs-lookup"><span data-stu-id="bc1a1-219">Enter hello number of items create, read, update, and delete operations you require (on a per-second basis).</span></span> <span data-ttu-id="bc1a1-220">tooestimate плата за единицу hello запрос операций обновления элемента, отправить копию элемента образец hello на шаге 1 выше, включает в себя обновления обычно поля.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-220">tooestimate hello request unit charges of item update operations, upload a copy of hello sample item from step 1 above that includes typical field updates.</span></span>  <span data-ttu-id="bc1a1-221">Например если обновления элементов обычно изменить два свойства с именем lastLogin и userVisits, а затем просто скопировать элемент образец hello, обновить hello значения этих двух свойств и загрузить hello скопировать элемент.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-221">For example, if item updates typically modify two properties named lastLogin and userVisits, then simply copy hello sample item, update hello values for those two properties, and upload hello copied item.</span></span>
   
    ![Введите пропускной способности в калькулятор единица запроса hello][3]
4. <span data-ttu-id="bc1a1-223">Нажмите кнопку вычисления и изучить результаты hello.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-223">Click calculate and examine hello results.</span></span>
   
    ![Результаты калькулятора единиц запросов][4]

> [!NOTE]
> <span data-ttu-id="bc1a1-225">При наличии типов элементов, которые существенно отличается с точки зрения размера и hello количество индексированных свойств, затем загрузить пример каждого *тип* из toohello типичными элементами инструмент, а затем вычислить результаты hello.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-225">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then upload a sample of each *type* of typical item toohello tool and then calculate hello results.</span></span>
> 
> 

### <a name="use-hello-azure-cosmos-db-request-charge-response-header"></a><span data-ttu-id="bc1a1-226">Используйте Azure Cosmos DB запрос hello платы-заголовок ответа</span><span class="sxs-lookup"><span data-stu-id="bc1a1-226">Use hello Azure Cosmos DB request charge response header</span></span>
<span data-ttu-id="bc1a1-227">Каждый ответ от службы Azure Cosmos DB hello включает пользовательский заголовок (`x-ms-request-charge`), содержащий единиц запроса hello, использованных для запроса hello.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-227">Every response from hello Azure Cosmos DB service includes a custom header (`x-ms-request-charge`) that contains hello request units consumed for hello request.</span></span> <span data-ttu-id="bc1a1-228">Этот заголовок, также доступны пакеты SDK Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-228">This header is also accessible through hello Azure Cosmos DB SDKs.</span></span> <span data-ttu-id="bc1a1-229">В hello .NET SDK RequestCharge является свойством объекта ResourceResponse hello.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-229">In hello .NET SDK, RequestCharge is a property of hello ResourceResponse object.</span></span>  <span data-ttu-id="bc1a1-230">Для запросов hello Azure Cosmos DB запроса обозревателя в hello портал Azure сведения запроса платы для выполненных запросов.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-230">For queries, hello Azure Cosmos DB Query Explorer in hello Azure portal provides request charge information for executed queries.</span></span>

![Анализ расходов единиц Запросов в hello Explorer запроса][1]

<span data-ttu-id="bc1a1-232">С учетом этого один из методов оценки hello объем зарезервированной пропускной способностью, необходимые для приложения — toorecord запроса hello единицы издержки, связанные с запущенным обычные операции по отношению к репрезентативной элемента, используемого приложением и затем Оценка hello количество операций предполагается выполнение каждую секунду.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-232">With this in mind, one method for estimating hello amount of reserved throughput required by your application is toorecord hello request unit charge associated with running typical operations against a representative item used by your application and then estimating hello number of operations you anticipate performing each second.</span></span>  <span data-ttu-id="bc1a1-233">Быть убедиться, что toomeasure с обычных запросов и Azure Cosmos DB также использование скрипта.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-233">Be sure toomeasure and include typical queries and Azure Cosmos DB script usage as well.</span></span>

> [!NOTE]
> <span data-ttu-id="bc1a1-234">При наличии типов элементов, которые существенно отличается с точки зрения размера и hello количество индексированных свойств, затем запишите hello применяемой операции запроса единицы издержек, связанных с каждым *тип* типичные элемента.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-234">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then record hello applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

<span data-ttu-id="bc1a1-235">Например:</span><span class="sxs-lookup"><span data-stu-id="bc1a1-235">For example:</span></span>

1. <span data-ttu-id="bc1a1-236">Запишите издержки единицы hello запрос создания (Вставка) типичными элементами.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-236">Record hello request unit charge of creating (inserting) a typical item.</span></span> 
2. <span data-ttu-id="bc1a1-237">Запрос записей hello единицы платы чтения типичными элементами.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-237">Record hello request unit charge of reading a typical item.</span></span>
3. <span data-ttu-id="bc1a1-238">Издержки единица запроса записей hello обновления типичными элементами.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-238">Record hello request unit charge of updating a typical item.</span></span>
4. <span data-ttu-id="bc1a1-239">Издержки единица запроса записей hello запросов типичных, общих элементов.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-239">Record hello request unit charge of typical, common item queries.</span></span>
5. <span data-ttu-id="bc1a1-240">Записи hello запрос единицы оплата за использование все пользовательские сценарии (хранимые процедуры, триггеры, определяемые пользователем функции) инструментарию приложения hello</span><span class="sxs-lookup"><span data-stu-id="bc1a1-240">Record hello request unit charge of any custom scripts (stored procedures, triggers, user-defined functions) leveraged by hello application</span></span>
6. <span data-ttu-id="bc1a1-241">Вычисление необходимых запрос hello единицы hello предполагаемое количество операций предполагается toorun каждую секунду.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-241">Calculate hello required request units given hello estimated number of operations you anticipate toorun each second.</span></span>

### <span data-ttu-id="bc1a1-242"><a id="GetLastRequestStatistics"></a>Выполнение команды MongoDB GetLastRequestStatistics с помощью API</span><span class="sxs-lookup"><span data-stu-id="bc1a1-242"><a id="GetLastRequestStatistics"></a>Use API for MongoDB's GetLastRequestStatistics command</span></span>
<span data-ttu-id="bc1a1-243">API-Интерфейс для MongoDB поддерживает пользовательской команды *getLastRequestStatistics*, для извлечения hello запрос платы для указанных операций.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-243">API for MongoDB supports a custom command, *getLastRequestStatistics*, for retrieving hello request charge for specified operations.</span></span>

<span data-ttu-id="bc1a1-244">Например в hello оболочку Mongo, выполнение операции hello нужный запрос плата tooverify hello.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-244">For example, in hello Mongo Shell, execute hello operation you want tooverify hello request charge for.</span></span>
```
> db.sample.find()
```

<span data-ttu-id="bc1a1-245">Затем выполните команду hello *getLastRequestStatistics*.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-245">Next, execute hello command *getLastRequestStatistics*.</span></span>
```
> db.runCommand({getLastRequestStatistics: 1})
{
    "_t": "GetRequestStatisticsResponse",
    "ok": 1,
    "CommandName": "OP_QUERY",
    "RequestCharge": 2.48,
    "RequestDurationInMilliSeconds" : 4.0048
}
```

<span data-ttu-id="bc1a1-246">С учетом этого один из методов оценки hello объем зарезервированной пропускной способностью, необходимые для приложения — toorecord запроса hello единицы издержки, связанные с запущенным обычные операции по отношению к репрезентативной элемента, используемого приложением и затем Оценка hello количество операций предполагается выполнение каждую секунду.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-246">With this in mind, one method for estimating hello amount of reserved throughput required by your application is toorecord hello request unit charge associated with running typical operations against a representative item used by your application and then estimating hello number of operations you anticipate performing each second.</span></span>

> [!NOTE]
> <span data-ttu-id="bc1a1-247">При наличии типов элементов, которые существенно отличается с точки зрения размера и hello количество индексированных свойств, затем запишите hello применяемой операции запроса единицы издержек, связанных с каждым *тип* типичные элемента.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-247">If you have item types which will differ dramatically in terms of size and hello number of indexed properties, then record hello applicable operation request unit charge associated with each *type* of typical item.</span></span>
> 
> 

## <a name="use-api-for-mongodbs-portal-metrics"></a><span data-ttu-id="bc1a1-248">Использование метрик API для MongoDB, доступных на портале</span><span class="sxs-lookup"><span data-stu-id="bc1a1-248">Use API for MongoDB's portal metrics</span></span>
<span data-ttu-id="bc1a1-249">Здравствуйте, простой способ tooget, хорошо оценки запроса единицы цену за API для базы данных MongoDB toouse hello [портал Azure](https://portal.azure.com) метрики.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-249">hello simplest way tooget a good estimation of request unit charges for your API for MongoDB database is toouse hello [Azure portal](https://portal.azure.com) metrics.</span></span> <span data-ttu-id="bc1a1-250">С hello *число запросов* и *платы запроса* диаграммы, можно получить оценивает количество единиц запроса, каждая операция является использования и количество единиц запроса они потребляют относительный tooone другой.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-250">With hello *Number of requests* and *Request Charge* charts, you can get an estimation of how many request units each operation is consuming and how many request units they consume relative tooone another.</span></span>

![Метрики API для MongoDB, доступные на портале][6]

## <a name="a-request-unit-estimation-example"></a><span data-ttu-id="bc1a1-252">Пример оценки количества единиц запросов</span><span class="sxs-lookup"><span data-stu-id="bc1a1-252">A request unit estimation example</span></span>
<span data-ttu-id="bc1a1-253">Рассмотрим следующий документ около 1 КБ hello.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-253">Consider hello following ~1KB document:</span></span>

```json
{
 "id": "08259",
  "description": "Cereals ready-to-eat, KELLOGG, KELLOGG'S CRISPIX",
  "tags": [
    {
      "name": "cereals ready-to-eat"
    },
    {
      "name": "kellogg"
    },
    {
      "name": "kellogg's crispix"
    }
  ],
  "version": 1,
  "commonName": "Includes USDA Commodity B855",
  "manufacturerName": "Kellogg, Co.",
  "isFromSurvey": false,
  "foodGroup": "Breakfast Cereals",
  "nutrients": [
    {
      "id": "262",
      "description": "Caffeine",
      "nutritionValue": 0,
      "units": "mg"
    },
    {
      "id": "307",
      "description": "Sodium, Na",
      "nutritionValue": 611,
      "units": "mg"
    },
    {
      "id": "309",
      "description": "Zinc, Zn",
      "nutritionValue": 5.2,
      "units": "mg"
    }
  ],
  "servings": [
    {
      "amount": 1,
      "description": "cup (1 NLEA serving)",
      "weightInGrams": 29
    }
  ]
}
```

> [!NOTE]
> <span data-ttu-id="bc1a1-254">Документы уменьшена в базе данных Azure Cosmos, поэтому система hello вычисляемый размер документа hello выше — немного меньше, чем 1 КБ.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-254">Documents are minified in Azure Cosmos DB, so hello system calculated size of hello document above is slightly less than 1KB.</span></span>
> 
> 

<span data-ttu-id="bc1a1-255">Hello следующей таблице представлены приблизительные запрос плата за единицу для обычных операций на этом элементе (hello приблизительное запрос единицы платы предполагает уровень согласованности hello учетная запись имеет значение слишком «Сеанс» и автоматически индексируются все элементы):</span><span class="sxs-lookup"><span data-stu-id="bc1a1-255">hello following table shows approximate request unit charges for typical operations on this item (hello approximate request unit charge assumes that hello account consistency level is set too“Session” and that all items are automatically indexed):</span></span>

| <span data-ttu-id="bc1a1-256">Операция</span><span class="sxs-lookup"><span data-stu-id="bc1a1-256">Operation</span></span> | <span data-ttu-id="bc1a1-257">Затраты единиц запросов</span><span class="sxs-lookup"><span data-stu-id="bc1a1-257">Request Unit Charge</span></span> |
| --- | --- |
| <span data-ttu-id="bc1a1-258">Create item (Создание элемента)</span><span class="sxs-lookup"><span data-stu-id="bc1a1-258">Create item</span></span> |<span data-ttu-id="bc1a1-259">~ 15 ЕЗ</span><span class="sxs-lookup"><span data-stu-id="bc1a1-259">~15 RU</span></span> |
| <span data-ttu-id="bc1a1-260">Чтение элемента</span><span class="sxs-lookup"><span data-stu-id="bc1a1-260">Read item</span></span> |<span data-ttu-id="bc1a1-261">~ 1 ЕЗ</span><span class="sxs-lookup"><span data-stu-id="bc1a1-261">~1 RU</span></span> |
| <span data-ttu-id="bc1a1-262">Запрос элемента по идентификатору</span><span class="sxs-lookup"><span data-stu-id="bc1a1-262">Query item by id</span></span> |<span data-ttu-id="bc1a1-263">~ 2,5 ЕЗ</span><span class="sxs-lookup"><span data-stu-id="bc1a1-263">~2.5 RU</span></span> |

<span data-ttu-id="bc1a1-264">Кроме того в этой таблице показан запрос из приблизительных расходов единицы для типичных запросов, используемых в приложение hello.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-264">Additionally, this table shows approximate request unit charges for typical queries used in hello application:</span></span>

| <span data-ttu-id="bc1a1-265">Запрос</span><span class="sxs-lookup"><span data-stu-id="bc1a1-265">Query</span></span> | <span data-ttu-id="bc1a1-266">Затраты единиц запросов</span><span class="sxs-lookup"><span data-stu-id="bc1a1-266">Request Unit Charge</span></span> | <span data-ttu-id="bc1a1-267">Число возвращенных элементов</span><span class="sxs-lookup"><span data-stu-id="bc1a1-267"># of Returned Items</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc1a1-268">Выбор продуктов питания по идентификатору</span><span class="sxs-lookup"><span data-stu-id="bc1a1-268">Select food by id</span></span> |<span data-ttu-id="bc1a1-269">~ 2,5 ЕЗ</span><span class="sxs-lookup"><span data-stu-id="bc1a1-269">~2.5 RU</span></span> |<span data-ttu-id="bc1a1-270">1</span><span class="sxs-lookup"><span data-stu-id="bc1a1-270">1</span></span> |
| <span data-ttu-id="bc1a1-271">Выбор продуктов питания по производителю</span><span class="sxs-lookup"><span data-stu-id="bc1a1-271">Select foods by manufacturer</span></span> |<span data-ttu-id="bc1a1-272">~ 7 ЕЗ</span><span class="sxs-lookup"><span data-stu-id="bc1a1-272">~7 RU</span></span> |<span data-ttu-id="bc1a1-273">7</span><span class="sxs-lookup"><span data-stu-id="bc1a1-273">7</span></span> |
| <span data-ttu-id="bc1a1-274">Выбор группы продуктов питания и сортировка по весу</span><span class="sxs-lookup"><span data-stu-id="bc1a1-274">Select by food group and order by weight</span></span> |<span data-ttu-id="bc1a1-275">~ 70 ЕЗ</span><span class="sxs-lookup"><span data-stu-id="bc1a1-275">~70 RU</span></span> |<span data-ttu-id="bc1a1-276">100</span><span class="sxs-lookup"><span data-stu-id="bc1a1-276">100</span></span> |
| <span data-ttu-id="bc1a1-277">Выбор десяти первых продуктов питания в группе</span><span class="sxs-lookup"><span data-stu-id="bc1a1-277">Select top 10 foods in a food group</span></span> |<span data-ttu-id="bc1a1-278">~ 10 ЕЗ</span><span class="sxs-lookup"><span data-stu-id="bc1a1-278">~10 RU</span></span> |<span data-ttu-id="bc1a1-279">10</span><span class="sxs-lookup"><span data-stu-id="bc1a1-279">10</span></span> |

> [!NOTE]
> <span data-ttu-id="bc1a1-280">Плата RU различаются в зависимости от hello количество возвращаемых элементов.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-280">RU charges vary based on hello number of items returned.</span></span>
> 
> 

<span data-ttu-id="bc1a1-281">С этой информацией можно оценить требования к RU hello для этого приложения, получившего hello числа операций и запросов, что ожидается, что в секунду:</span><span class="sxs-lookup"><span data-stu-id="bc1a1-281">With this information, we can estimate hello RU requirements for this application given hello number of operations and queries we expect per second:</span></span>

| <span data-ttu-id="bc1a1-282">Операции и запросы</span><span class="sxs-lookup"><span data-stu-id="bc1a1-282">Operation/Query</span></span> | <span data-ttu-id="bc1a1-283">Предполагаемое количество в секунду</span><span class="sxs-lookup"><span data-stu-id="bc1a1-283">Estimated number per second</span></span> | <span data-ttu-id="bc1a1-284">Необходимые единицы запросов</span><span class="sxs-lookup"><span data-stu-id="bc1a1-284">Required RUs</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bc1a1-285">Create item (Создание элемента)</span><span class="sxs-lookup"><span data-stu-id="bc1a1-285">Create item</span></span> |<span data-ttu-id="bc1a1-286">10</span><span class="sxs-lookup"><span data-stu-id="bc1a1-286">10</span></span> |<span data-ttu-id="bc1a1-287">150</span><span class="sxs-lookup"><span data-stu-id="bc1a1-287">150</span></span> |
| <span data-ttu-id="bc1a1-288">Чтение элемента</span><span class="sxs-lookup"><span data-stu-id="bc1a1-288">Read item</span></span> |<span data-ttu-id="bc1a1-289">100</span><span class="sxs-lookup"><span data-stu-id="bc1a1-289">100</span></span> |<span data-ttu-id="bc1a1-290">100</span><span class="sxs-lookup"><span data-stu-id="bc1a1-290">100</span></span> |
| <span data-ttu-id="bc1a1-291">Выбор продуктов питания по производителю</span><span class="sxs-lookup"><span data-stu-id="bc1a1-291">Select foods by manufacturer</span></span> |<span data-ttu-id="bc1a1-292">25</span><span class="sxs-lookup"><span data-stu-id="bc1a1-292">25</span></span> |<span data-ttu-id="bc1a1-293">175</span><span class="sxs-lookup"><span data-stu-id="bc1a1-293">175</span></span> |
| <span data-ttu-id="bc1a1-294">Выбор продуктов питания по группе</span><span class="sxs-lookup"><span data-stu-id="bc1a1-294">Select by food group</span></span> |<span data-ttu-id="bc1a1-295">10</span><span class="sxs-lookup"><span data-stu-id="bc1a1-295">10</span></span> |<span data-ttu-id="bc1a1-296">700</span><span class="sxs-lookup"><span data-stu-id="bc1a1-296">700</span></span> |
| <span data-ttu-id="bc1a1-297">Выбор первых десяти продуктов питания</span><span class="sxs-lookup"><span data-stu-id="bc1a1-297">Select top 10</span></span> |<span data-ttu-id="bc1a1-298">15</span><span class="sxs-lookup"><span data-stu-id="bc1a1-298">15</span></span> |<span data-ttu-id="bc1a1-299">Всего 150</span><span class="sxs-lookup"><span data-stu-id="bc1a1-299">150 Total</span></span> |

<span data-ttu-id="bc1a1-300">В этом случае ожидается, что для средней пропускной способности необходимо 1,275 единиц запросов в секунду.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-300">In this case, we expect an average throughput requirement of 1,275 RU/s.</span></span>  <span data-ttu-id="bc1a1-301">Округление вверх toohello ближайшего 100, мы подготовить 1 300 единиц Запросов в секунду для этого приложения коллекции.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-301">Rounding up toohello nearest 100, we would provision 1,300 RU/s for this application's collection.</span></span>

## <span data-ttu-id="bc1a1-302"><a id="RequestRateTooLarge"></a> Превышение лимита зарезервированной пропускной способности в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bc1a1-302"><a id="RequestRateTooLarge"></a> Exceeding reserved throughput limits in Azure Cosmos DB</span></span>
<span data-ttu-id="bc1a1-303">Помните, что потребление единица запроса вычисляется как скорость Если бюджета hello пуст.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-303">Recall that request unit consumption is evaluated as a rate per second if hello budget is empty.</span></span> <span data-ttu-id="bc1a1-304">Для приложений, которые превышают hello частота единицы подготовленных запросов для контейнера, запросы, пока частота hello падает ниже уровня hello зарезервировано будет регулироваться toothat коллекции.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-304">For applications that exceed hello provisioned request unit rate for a container, requests toothat collection will be throttled until hello rate drops below hello reserved level.</span></span> <span data-ttu-id="bc1a1-305">В случае регулирования hello server предварительно завершается запрос hello с RequestRateTooLargeException (код состояния HTTP 429) и возврата hello заголовок x-ms повтора после ms, указывающий, что время ожидания перед hello количество времени, в миллисекундах, которое hello пользователя hello повторным выполнением запроса.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-305">When a throttle occurs, hello server will preemptively end hello request with RequestRateTooLargeException (HTTP status code 429) and return hello x-ms-retry-after-ms header indicating hello amount of time, in milliseconds, that hello user must wait before reattempting hello request.</span></span>

    HTTP Status 429
    Status Line: RequestRateTooLarge
    x-ms-retry-after-ms :100

<span data-ttu-id="bc1a1-306">Если вы используете hello пакет SDK для клиента .NET и LINQ-запросов, а затем большую часть времени hello, никогда не toodeal с этим исключением как текущая версия hello hello пакет SDK для клиента .NET неявно перехватывает этот ответ, отношениях hello сервер указан заголовок retry-after, и запрос hello повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-306">If you are using hello .NET Client SDK and LINQ queries, then most of hello time you never have toodeal with this exception, as hello current version of hello .NET Client SDK implicitly catches this response, respects hello server-specified retry-after header, and retries hello request.</span></span> <span data-ttu-id="bc1a1-307">Если ваша учетная запись осуществляется параллельно несколькими клиентами, будет успешным hello следующей попытки.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-307">Unless your account is being accessed concurrently by multiple clients, hello next retry will succeed.</span></span>

<span data-ttu-id="bc1a1-308">При наличии более одного клиента Суммарно превысила частота запросов hello, hello повторных попыток по умолчанию может оказаться недостаточно и hello клиент вызовет DocumentClientException с приложением toohello 429 код состояния.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-308">If you have more than one client cumulatively operating above hello request rate, hello default retry behavior may not suffice, and hello client will throw a DocumentClientException with status code 429 toohello application.</span></span> <span data-ttu-id="bc1a1-309">В таких случаях можно рассмотреть возможность обработки характер повторения и логика приложения ошибке подпрограмм обработки или увеличения hello зарезервированную полосу пропускания для контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-309">In cases such as this, you may consider handling retry behavior and logic in your application's error handling routines or increasing hello reserved throughput for hello container.</span></span>

## <span data-ttu-id="bc1a1-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> Превышение лимита зарезервированной пропускной способности в API для DocumentDB</span><span class="sxs-lookup"><span data-stu-id="bc1a1-310"><a id="RequestRateTooLargeAPIforMongoDB"></a> Exceeding reserved throughput limits in API for MongoDB</span></span>
<span data-ttu-id="bc1a1-311">Приложения, которые превышают единицы hello подготовить запрос для коллекции будет регулироваться пока частота hello падает ниже уровня hello зарезервировано.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-311">Applications that exceed hello provisioned request units for a collection will be throttled until hello rate drops below hello reserved level.</span></span> <span data-ttu-id="bc1a1-312">В случае регулирования серверной hello предварительно завершается hello запрос с *16500* код ошибки - *слишком много запросов*.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-312">When a throttle occurs, hello backend will preemptively end hello request with a *16500* error code - *Too Many Requests*.</span></span> <span data-ttu-id="bc1a1-313">По умолчанию API для MongoDB автоматически повторит попытку too10 времени перед возвратом *слишком много запросов* код ошибки.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-313">By default, API for MongoDB will automatically retry up too10 times before returning a *Too Many Requests* error code.</span></span> <span data-ttu-id="bc1a1-314">Если вы получили многие *слишком много запросов* коды ошибок, можно либо добавить поведение повтора в код подпрограмм обработки ошибок приложения или [увеличение hello зарезервированную полосу пропускания для hello коллекции](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="bc1a1-314">If you are receiving many *Too Many Requests* error codes, you may consider either adding retry behavior in your application's error handling routines or [increasing hello reserved throughput for hello collection](set-throughput.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc1a1-315">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bc1a1-315">Next steps</span></span>
<span data-ttu-id="bc1a1-316">toolearn Дополнительные сведения о зарезервированных пропускной способности с Azure Cosmos DB баз данных, изучить эти ресурсы.</span><span class="sxs-lookup"><span data-stu-id="bc1a1-316">toolearn more about reserved throughput with Azure Cosmos DB databases, explore these resources:</span></span>

* [<span data-ttu-id="bc1a1-317">Страница цен на Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="bc1a1-317">Azure Cosmos DB pricing</span></span>](https://azure.microsoft.com/pricing/details/cosmos-db/)
* [<span data-ttu-id="bc1a1-318">Секционирование в базе данных Azure Cosmos DB с помощью API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="bc1a1-318">Partitioning data in Azure Cosmos DB</span></span>](partition-data.md)

<span data-ttu-id="bc1a1-319">toolearn Дополнительные сведения о базе данных Azure Cosmos, в разделе hello Azure Cosmos DB [документации](https://azure.microsoft.com/documentation/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="bc1a1-319">toolearn more about Azure Cosmos DB, see hello Azure Cosmos DB [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/).</span></span> 

<span data-ttu-id="bc1a1-320">tooget к работе с масштаб и производительность тестирование с помощью Azure Cosmos DB, в разделе [производительности и масштабирования тестирование с помощью Azure Cosmos DB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="bc1a1-320">tooget started with scale and performance testing with Azure Cosmos DB, see [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md).</span></span>

[1]: ./media/request-units/queryexplorer.png 
[2]: ./media/request-units/RUEstimatorUpload.png
[3]: ./media/request-units/RUEstimatorDocuments.png
[4]: ./media/request-units/RUEstimatorResults.png
[5]: ./media/request-units/RUCalculator2.png
[6]: ./media/request-units/api-for-mongodb-metrics.png
