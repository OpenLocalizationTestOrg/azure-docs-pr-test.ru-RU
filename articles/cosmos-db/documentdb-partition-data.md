---
title: "Секционирование и масштабирование в базе данных Azure Cosmos DB | Документация Майкрософт"
description: "Сведения о работе секционирования в базе данных Azure Cosmos DB, настройке секционирования и ключей секций, а также о выборе подходящего ключа секции для вашего приложения."
services: cosmos-db
author: arramac
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 702c39b4-1798-48dd-9993-4493a2f6df9e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 81010d91ac7fe8fa7149c52ed56af304cf4e83d9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="partitioning-in-azure-cosmos-db-using-the-documentdb-api"></a><span data-ttu-id="cb8b1-103">Секционирование в базе данных Azure Cosmos DB с помощью API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="cb8b1-103">Partitioning in Azure Cosmos DB using the DocumentDB API</span></span>

<span data-ttu-id="cb8b1-104">[База данных Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) — это глобально распределенная, многомодельная служба базы данных, созданная для обеспечения высокой производительности и прогнозируемости, а также легкой масштабируемости по мере расширения вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) is a global distributed, multi-model database service designed to help you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> 

<span data-ttu-id="cb8b1-105">В этой статье описаны способы работы с секционированием контейнеров Cosmos DB с помощью API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-105">This article provides an overview of how to work with partitioning of Cosmos DB containers with the DocumentDB API.</span></span> <span data-ttu-id="cb8b1-106">Обзор концепций и рекомендации для секционирования с использованием любого API базы данных Azure Cosmos DB см. [в этой статье](../cosmos-db/partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="cb8b1-106">See [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

<span data-ttu-id="cb8b1-107">Чтобы начать работу с кодом, скачайте проект с [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="cb8b1-107">To get started with code, download the project from [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<span data-ttu-id="cb8b1-108">После прочтения этой статьи вы сможете ответить на следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="cb8b1-108">After reading this article, you will be able to answer the following questions:</span></span>   

* <span data-ttu-id="cb8b1-109">Как работает секционирование в Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="cb8b1-109">How does partitioning work in Azure Cosmos DB?</span></span>
* <span data-ttu-id="cb8b1-110">Как настроить секционирование в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cb8b1-110">How do I configure partitioning in Azure Cosmos DB</span></span>
* <span data-ttu-id="cb8b1-111">Что такое ключи секций и как выбрать правильный ключ секции для моего приложения?</span><span class="sxs-lookup"><span data-stu-id="cb8b1-111">What are partition keys, and how do I pick the right partition key for my application?</span></span>

<span data-ttu-id="cb8b1-112">Чтобы начать работу с кодом, скачайте проект со страницы [примера драйвера для тестирования производительности Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="cb8b1-112">To get started with code, download the project from [Azure Cosmos DB Performance Testing Driver Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a><span data-ttu-id="cb8b1-113">Ключи секции</span><span class="sxs-lookup"><span data-stu-id="cb8b1-113">Partition keys</span></span>

<span data-ttu-id="cb8b1-114">В API DocumentDB укажите определение ключа секции в формате пути к файлу JSON.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-114">In the DocumentDB API, you specify the partition key definition in the form of a JSON path.</span></span> <span data-ttu-id="cb8b1-115">В следующей таблице приведены примеры определений для ключей секции и соответствующие значения.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-115">The following table shows examples of partition key definitions and the values corresponding to each.</span></span> <span data-ttu-id="cb8b1-116">Ключ секции указывается в виде пути, например `/department` представляет свойство отдела.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-116">The partition key is specified as a path, e.g. `/department` represents the property department.</span></span> 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="cb8b1-117"><strong>Ключ секции</strong></span><span class="sxs-lookup"><span data-stu-id="cb8b1-117"><strong>Partition Key</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="cb8b1-118"><strong>Описание</strong></span><span class="sxs-lookup"><span data-stu-id="cb8b1-118"><strong>Description</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="cb8b1-119">/department</span><span class="sxs-lookup"><span data-stu-id="cb8b1-119">/department</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="cb8b1-120">Соответствует значению doc.department, где doc — это элемент.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-120">Corresponds to the value of doc.department where doc is the item.</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="cb8b1-121">/properties/name</span><span class="sxs-lookup"><span data-stu-id="cb8b1-121">/properties/name</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="cb8b1-122">Соответствует значению doc.properties.name, где doc — это элемент (вложенное свойство).</span><span class="sxs-lookup"><span data-stu-id="cb8b1-122">Corresponds to the value of doc.properties.name where doc is the item (nested property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="cb8b1-123">/id</span><span class="sxs-lookup"><span data-stu-id="cb8b1-123">/id</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="cb8b1-124">Соответствует значению doc.id (идентификатор и ключ секции — это одно и то же свойство).</span><span class="sxs-lookup"><span data-stu-id="cb8b1-124">Corresponds to the value of doc.id (id and partition key are the same property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="cb8b1-125">/"имя отдела"</span><span class="sxs-lookup"><span data-stu-id="cb8b1-125">/"department name"</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="cb8b1-126">Соответствует значению [doc.department], где doc — это элемент.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-126">Corresponds to the value of doc["department name"] where doc is the item.</span></span></p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> <span data-ttu-id="cb8b1-127">Синтаксис ключа секции аналогичен политике индексации. Основное отличие состоит в том, что путь соответствует свойству, а не значению, т. е. в конце нет подстановочного знака.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-127">The syntax for partition key is similar to the path specification for indexing policy paths with the key difference that the path corresponds to the property instead of the value, i.e. there is no wild card at the end.</span></span> <span data-ttu-id="cb8b1-128">Например, для индексации значений в отделе используется /department/?,</span><span class="sxs-lookup"><span data-stu-id="cb8b1-128">For example, you would specify /department/?</span></span> <span data-ttu-id="cb8b1-129">а в качестве определения ключа секции — /department.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-129">to index the values under department, but specify /department as the partition key definition.</span></span> <span data-ttu-id="cb8b1-130">Ключ секции индексируется неявно и не может быть исключен из индексирования с помощью переопределений политики индексирования.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-130">The partition key is implicitly indexed and cannot be excluded from indexing using indexing policy overrides.</span></span>
> 
> 

<span data-ttu-id="cb8b1-131">Давайте рассмотрим, как выбор ключа секции влияет на производительность приложения.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-131">Let's look at how the choice of partition key impacts the performance of your application.</span></span>

## <a name="working-with-the-azure-cosmos-db-sdks"></a><span data-ttu-id="cb8b1-132">Работа с пакетами SDK для базы данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cb8b1-132">Working with the Azure Cosmos DB SDKs</span></span>
<span data-ttu-id="cb8b1-133">В Azure Cosmos DB добавлена поддержка автоматического секционирования с использованием [REST API версии 2015-12-16](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="cb8b1-133">Azure Cosmos DB added support for automatic partitioning with [REST API version 2015-12-16](/rest/api/documentdb/).</span></span> <span data-ttu-id="cb8b1-134">Для создания секционированных контейнеров необходимо скачать пакет SDK версии 1.6.0 или более поздней для одной из поддерживаемых платформ SDK (.NET, Node.js, Java, Python и MongoDB).</span><span class="sxs-lookup"><span data-stu-id="cb8b1-134">In order to create partitioned containers, you must download SDK versions 1.6.0 or newer in one of the supported SDK platforms (.NET, Node.js, Java, Python, MongoDB).</span></span> 

### <a name="creating-containers"></a><span data-ttu-id="cb8b1-135">Создание контейнеров</span><span class="sxs-lookup"><span data-stu-id="cb8b1-135">Creating containers</span></span>
<span data-ttu-id="cb8b1-136">В приведенном ниже примере показан фрагмент кода .NET для создания контейнеров, предназначенных для хранения данных телеметрии устройств, которой выделяется пропускная способность в 20 000 единиц запроса в секунду.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-136">The following sample shows a .NET snippet to create a container to store device telemetry data of 20,000 request units per second of throughput.</span></span> <span data-ttu-id="cb8b1-137">Пакет SDK устанавливает значение OfferThroughput (которое в свою очередь задает заголовок запроса `x-ms-offer-throughput` в REST API).</span><span class="sxs-lookup"><span data-stu-id="cb8b1-137">The SDK sets the OfferThroughput value (which in turn sets the `x-ms-offer-throughput` request header in the REST API).</span></span> <span data-ttu-id="cb8b1-138">Здесь мы задаем `/deviceId` в качестве ключа секции.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-138">Here we set the `/deviceId` as the partition key.</span></span> <span data-ttu-id="cb8b1-139">Выбранный ключ секции сохраняется вместе с остальными метаданными контейнера, такими как имя и политики индексирования.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-139">The choice of partition key is saved along with the rest of the container metadata like name and indexing policy.</span></span>

<span data-ttu-id="cb8b1-140">Для этого примера мы выбрали `deviceId`, т. к. нам известно, что: (а) ввиду большого количества устройств операции записи их можно равномерно распределить между секциями, что позволяет масштабировать базу данных для приема больших объемов данных; (б) многие из запросов, например получение последних показаний устройства, относятся к одному deviceId и могут быть получены из одной секции.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-140">For this sample, we picked `deviceId` since we know that (a) since there are a large number of devices, writes can be distributed across partitions evenly and allowing us to scale the database to ingest massive volumes of data and (b) many of the requests like fetching the latest reading for a device are scoped to a single deviceId and can be retrieved from a single partition.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

// Container for device telemetry. Here the property deviceId will be used as the partition key to 
// spread across partitions. Configured for 10K RU/s throughput and an indexing policy that supports 
// sorting against any number or string property.
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 20000 });
```

<span data-ttu-id="cb8b1-141">Этот метод выполняет вызов REST API в Cosmos DB, а служба подготавливает число секций, основываясь на запрошенной пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-141">This method makes a REST API call to Cosmos DB, and the service will provision a number of partitions based on the requested throughput.</span></span> <span data-ttu-id="cb8b1-142">Пропускную способность контейнера можно изменить, когда требуется повысить ее производительность.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-142">You can change the throughput of a container as your performance needs evolve.</span></span> 

### <a name="reading-and-writing-items"></a><span data-ttu-id="cb8b1-143">Чтение и запись элементов</span><span class="sxs-lookup"><span data-stu-id="cb8b1-143">Reading and writing items</span></span>
<span data-ttu-id="cb8b1-144">Пора перейти к вставке данных в Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-144">Now, let's insert data into Cosmos DB.</span></span> <span data-ttu-id="cb8b1-145">Ниже приведен пример класса, содержащего показание устройства, и вызов CreateDocumentAsync для добавления нового показания устройства в контейнер.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-145">Here's a sample class containing a device reading, and a call to CreateDocumentAsync to insert a new device reading into a container.</span></span> <span data-ttu-id="cb8b1-146">Ниже приведен пример использования API DocumentDB:</span><span class="sxs-lookup"><span data-stu-id="cb8b1-146">This is an example leveraging the DocumentDB API:</span></span>

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here the partition key is extracted as "XMS-0001" based on the collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```

<span data-ttu-id="cb8b1-147">Давайте прочитаем элемент по ключу секции и идентификатору, обновим его, а затем удалим с помощью ключа секции и идентификатора. Обратите внимание, что операции чтения включают в себя значение PartitionKey (соответствующее заголовку запроса `x-ms-documentdb-partitionkey` в REST API).</span><span class="sxs-lookup"><span data-stu-id="cb8b1-147">Let's read the item by its partition key and id, update it, and then as a final step, delete it by partition key and id. Note that the reads include a PartitionKey value (corresponding to the `x-ms-documentdb-partitionkey` request header in the REST API).</span></span>

```csharp
// Read document. Needs the partition key and the ID to be specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;

// Update the document. Partition key is not required, again extracted from the document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);

// Delete document. Needs partition key
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```

### <a name="querying-partitioned-containers"></a><span data-ttu-id="cb8b1-148">Запрос секционированных контейнеров</span><span class="sxs-lookup"><span data-stu-id="cb8b1-148">Querying partitioned containers</span></span>
<span data-ttu-id="cb8b1-149">При запросе данных из секционированных контейнеров Azure Cosmos DB автоматически направляет запрос в секции, соответствующие значению ключа секции, указанному в фильтре (если таковой имеется).</span><span class="sxs-lookup"><span data-stu-id="cb8b1-149">When you query data in partitioned containers, Cosmos DB automatically routes the query to the partitions corresponding to the partition key values specified in the filter (if there are any).</span></span> <span data-ttu-id="cb8b1-150">Например, этот запрос направляется только в секцию, которая содержит ключ секции XMS-0001.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-150">For example, this query is routed to just the partition containing the partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="cb8b1-151">Следующий запрос не имеет фильтра ключа секции (DeviceId) и "прочесывает" все секции, где он выполняется с использованием индекса секции.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-151">The following query does not have a filter on the partition key (DeviceId) and is fanned out to all partitions where it is executed against the partition's index.</span></span> <span data-ttu-id="cb8b1-152">Обратите внимание, что требуется указать EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` в REST API), чтобы пакет SDK выполнил запрос в секциях.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-152">Note that you have to specify the EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in the REST API) to have the SDK to execute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

<span data-ttu-id="cb8b1-153">Cosmos DB поддерживает [статистические функции](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` и `AVG` для секционированных контейнеров с помощью SQL с пакетом SDK 1.12.0 и выше.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-153">Cosmos DB supports [aggregate functions](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` and `AVG` over partitioned containers using SQL starting with SDKs 1.12.0 and above.</span></span> <span data-ttu-id="cb8b1-154">Запросы должны содержать один статистический оператор и одно значение в проекции.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-154">Queries must include a single aggregate operator, and must include a single value in the projection.</span></span>

### <a name="parallel-query-execution"></a><span data-ttu-id="cb8b1-155">Параллельное выполнение запросов</span><span class="sxs-lookup"><span data-stu-id="cb8b1-155">Parallel query execution</span></span>
<span data-ttu-id="cb8b1-156">Пакеты SDK для Cosmos DB версии 1.9.0 и более поздних версий поддерживают параллельное выполнение запросов, что позволяет выполнять запросы с низким уровнем задержки к секционированным коллекциям, даже если число секций в них очень велико.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-156">The Cosmos DB SDKs 1.9.0 and above support parallel query execution options, which allow you to perform low latency queries against partitioned collections, even when they need to touch a large number of partitions.</span></span> <span data-ttu-id="cb8b1-157">Например, следующий запрос настроен на выполнение параллельно по секциям.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-157">For example, the following query is configured to run in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="cb8b1-158">Вы можете управлять параллельным выполнением запросов, регулируя следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-158">You can manage parallel query execution by tuning the following parameters:</span></span>

* <span data-ttu-id="cb8b1-159">Параметр `MaxDegreeOfParallelism` позволяет управлять степенью параллелизма, т. е. устанавливать максимальное число одновременных сетевых подключений к секциям контейнера.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-159">By setting `MaxDegreeOfParallelism`, you can control the degree of parallelism i.e., the maximum number of simultaneous network connections to the container's partitions.</span></span> <span data-ttu-id="cb8b1-160">Если установить значение -1, то степень параллелизма будет регулироваться пакетом SDK.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-160">If you set this to -1, the degree of parallelism is managed by the SDK.</span></span> <span data-ttu-id="cb8b1-161">Если параметр `MaxDegreeOfParallelism` не указан или имеет значение 0 (значение по умолчанию), к секциям контейнера будет установлено одно сетевое подключение.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-161">If the `MaxDegreeOfParallelism` is not specified or set to 0, which is the default value, there will be a single network connection to the container's partitions.</span></span>
* <span data-ttu-id="cb8b1-162">Параметр `MaxBufferedItemCount` обеспечивает баланс между задержкой запросов и использованием памяти на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-162">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="cb8b1-163">Если пропустить этот параметр или задать значение -1, то число буферизованных элементов при параллельном выполнении запросов будет регулироваться пакетом SDK.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-163">If you omit this parameter or set this to -1, the number of items buffered during parallel query execution is managed by the SDK.</span></span>

<span data-ttu-id="cb8b1-164">При неизменном состоянии коллекции параллельный запрос будет возвращать результаты в том же порядке, что и при последовательном выполнении.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-164">Given the same state of the collection, a parallel query will return results in the same order as in serial execution.</span></span> <span data-ttu-id="cb8b1-165">При выполнении межсекционного запроса, включающего в себя сортировку (ORDER BY и/или TOP), пакет SDK для Azure Cosmos DB параллельно выполняет запрос между секциями и объединяет частично отсортированные результаты на стороне клиента для получения глобально упорядоченных результатов.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-165">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), the Azure Cosmos DB SDK issues the query in parallel across partitions and merges partially sorted results in the client side to produce globally ordered results.</span></span>

### <a name="executing-stored-procedures"></a><span data-ttu-id="cb8b1-166">Выполнение хранимых процедур</span><span class="sxs-lookup"><span data-stu-id="cb8b1-166">Executing stored procedures</span></span>
<span data-ttu-id="cb8b1-167">Кроме того, вы можете выполнять атомарные транзакции с документами с одинаковым идентификатором устройства, т. е. если вы храните статистические выражения или последнее состояние устройства в одном элементе.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-167">You can also execute atomic transactions against documents with the same device ID, e.g. if you're maintaining aggregates or the latest state of a device in a single item.</span></span> 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
<span data-ttu-id="cb8b1-168">В следующем разделе мы рассмотрим переход на секционированные контейнеры с односекционных контейнеров.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-168">In the next section, we look at how you can move to partitioned containers from single-partition containers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb8b1-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cb8b1-169">Next steps</span></span>
<span data-ttu-id="cb8b1-170">В этой статье описаны способы работы с секционированием контейнеров Azure Cosmos DB с помощью API DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-170">In this article, we provided an overview of how to work with partitioning of Azure Cosmos DB containers with the DocumentDB API.</span></span> <span data-ttu-id="cb8b1-171">Обзор концепций и рекомендации для секционирования с использованием любого API базы данных Azure Cosmos DB см. [в этой статье](../cosmos-db/partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="cb8b1-171">Also see [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="cb8b1-172">Выполняйте проверку масштабирования и производительности с помощью базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cb8b1-172">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="cb8b1-173">Пример см. в статье [Проверка производительности и масштабирования с помощью Azure DocumentDB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="cb8b1-173">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="cb8b1-174">Приступите к созданию кода с помощью [пакетов SDK](documentdb-sdk-dotnet.md) или [REST API](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="cb8b1-174">Get started coding with the [SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/)</span></span>
* <span data-ttu-id="cb8b1-175">Дополнительные сведения о подготовленной пропускной способности в базе данных Azure Cosmos DB см. в [этой статье](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="cb8b1-175">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>

