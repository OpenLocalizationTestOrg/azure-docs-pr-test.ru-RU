---
title: "aaaPartitioning и масштабирование в базе данных Azure Cosmos | Документы Microsoft"
description: "Дополнительные сведения о том, как секционирования работы в базе данных Azure Cosmos как tooconfigure секционирования и ключи секций и как toopick hello справа ключ раздела для вашего приложения."
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
ms.openlocfilehash: 30621d2ba0b89efb72005680d5f3a73998347514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="partitioning-in-azure-cosmos-db-using-hello-documentdb-api"></a><span data-ttu-id="d317a-103">Секционирование в базу данных Cosmos Azure, используя hello DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="d317a-103">Partitioning in Azure Cosmos DB using hello DocumentDB API</span></span>

<span data-ttu-id="d317a-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) является toohelp служба, предоставляющая глобальной распределенной базы данных моделей, можно добиться быстрого и предсказуемая производительность и масштабируемость без проблем вместе с приложением при увеличении его.</span><span class="sxs-lookup"><span data-stu-id="d317a-104">[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) is a global distributed, multi-model database service designed toohelp you achieve fast, predictable performance and scale seamlessly along with your application as it grows.</span></span> 

<span data-ttu-id="d317a-105">Приводятся общие сведения о том, как toowork с секционированием Cosmos DB контейнеров с hello DocumentDB API.</span><span class="sxs-lookup"><span data-stu-id="d317a-105">This article provides an overview of how toowork with partitioning of Cosmos DB containers with hello DocumentDB API.</span></span> <span data-ttu-id="d317a-106">Обзор концепций и рекомендации для секционирования с использованием любого API базы данных Azure Cosmos DB см. [в этой статье](../cosmos-db/partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="d317a-106">See [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

<span data-ttu-id="d317a-107">tooget к выполнению кода, загрузите проект hello из [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="d317a-107">tooget started with code, download hello project from [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<span data-ttu-id="d317a-108">После считывания в этой статье, можно будет tooanswer hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="d317a-108">After reading this article, you will be able tooanswer hello following questions:</span></span>   

* <span data-ttu-id="d317a-109">Как работает секционирование в Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="d317a-109">How does partitioning work in Azure Cosmos DB?</span></span>
* <span data-ttu-id="d317a-110">Как настроить секционирование в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d317a-110">How do I configure partitioning in Azure Cosmos DB</span></span>
* <span data-ttu-id="d317a-111">Что такое ключи секций и как выбрать hello правильный ключ секции для моего приложения?</span><span class="sxs-lookup"><span data-stu-id="d317a-111">What are partition keys, and how do I pick hello right partition key for my application?</span></span>

<span data-ttu-id="d317a-112">tooget к выполнению кода, загрузите проект hello из [пример драйвера тестирование в производительности для Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="d317a-112">tooget started with code, download hello project from [Azure Cosmos DB Performance Testing Driver Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark).</span></span> 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a><span data-ttu-id="d317a-113">Ключи секции</span><span class="sxs-lookup"><span data-stu-id="d317a-113">Partition keys</span></span>

<span data-ttu-id="d317a-114">В hello DocumentDB API укажите hello определение ключа раздела в форме hello пути JSON.</span><span class="sxs-lookup"><span data-stu-id="d317a-114">In hello DocumentDB API, you specify hello partition key definition in hello form of a JSON path.</span></span> <span data-ttu-id="d317a-115">Hello следующей таблице показаны примеры определения ключа секции и hello значения, соответствующие tooeach.</span><span class="sxs-lookup"><span data-stu-id="d317a-115">hello following table shows examples of partition key definitions and hello values corresponding tooeach.</span></span> <span data-ttu-id="d317a-116">ключ раздела Hello указывается как путь, например `/department` представляет hello свойство отдела.</span><span class="sxs-lookup"><span data-stu-id="d317a-116">hello partition key is specified as a path, e.g. `/department` represents hello property department.</span></span> 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><span data-ttu-id="d317a-117"><strong>Ключ секции</strong></span><span class="sxs-lookup"><span data-stu-id="d317a-117"><strong>Partition Key</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="d317a-118"><strong>Описание</strong></span><span class="sxs-lookup"><span data-stu-id="d317a-118"><strong>Description</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="d317a-119">/department</span><span class="sxs-lookup"><span data-stu-id="d317a-119">/department</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="d317a-120">Соответствует значение toohello doc.department, где элемент hello doc.</span><span class="sxs-lookup"><span data-stu-id="d317a-120">Corresponds toohello value of doc.department where doc is hello item.</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="d317a-121">/properties/name</span><span class="sxs-lookup"><span data-stu-id="d317a-121">/properties/name</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="d317a-122">Соответствует значение toohello doc.properties.name, где doc — элемент hello (вложенного свойства).</span><span class="sxs-lookup"><span data-stu-id="d317a-122">Corresponds toohello value of doc.properties.name where doc is hello item (nested property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="d317a-123">/id</span><span class="sxs-lookup"><span data-stu-id="d317a-123">/id</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="d317a-124">Соответствующее значение toohello doc.id (ключ идентификатора и секции hello же свойство).</span><span class="sxs-lookup"><span data-stu-id="d317a-124">Corresponds toohello value of doc.id (id and partition key are hello same property).</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="d317a-125">/"имя отдела"</span><span class="sxs-lookup"><span data-stu-id="d317a-125">/"department name"</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="d317a-126">Соответствует значение toohello doc [«название отдела»], где элемент hello doc.</span><span class="sxs-lookup"><span data-stu-id="d317a-126">Corresponds toohello value of doc["department name"] where doc is hello item.</span></span></p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> <span data-ttu-id="d317a-127">Hello для ключа раздела используется следующий синтаксис аналогичные toohello пути для путей политики индексирования с hello ключевое различие, hello путь соответствует свойству toohello вместо значения hello, т. е. имеется не подстановочному знаку в конце hello.</span><span class="sxs-lookup"><span data-stu-id="d317a-127">hello syntax for partition key is similar toohello path specification for indexing policy paths with hello key difference that hello path corresponds toohello property instead of hello value, i.e. there is no wild card at hello end.</span></span> <span data-ttu-id="d317a-128">Например, для индексации значений в отделе используется /department/?,</span><span class="sxs-lookup"><span data-stu-id="d317a-128">For example, you would specify /department/?</span></span> <span data-ttu-id="d317a-129">tooindex hello значения в группе отдела, но указать /department как определение ключа секции hello.</span><span class="sxs-lookup"><span data-stu-id="d317a-129">tooindex hello values under department, but specify /department as hello partition key definition.</span></span> <span data-ttu-id="d317a-130">ключ раздела Hello индексируется неявно и не может быть исключен из индексирования с помощью индексирования переопределения параметров политики.</span><span class="sxs-lookup"><span data-stu-id="d317a-130">hello partition key is implicitly indexed and cannot be excluded from indexing using indexing policy overrides.</span></span>
> 
> 

<span data-ttu-id="d317a-131">Давайте посмотрим, как выбор hello ключ раздела влияет на производительность приложения hello.</span><span class="sxs-lookup"><span data-stu-id="d317a-131">Let's look at how hello choice of partition key impacts hello performance of your application.</span></span>

## <a name="working-with-hello-azure-cosmos-db-sdks"></a><span data-ttu-id="d317a-132">Работа с hello Azure Cosmos DB SDK</span><span class="sxs-lookup"><span data-stu-id="d317a-132">Working with hello Azure Cosmos DB SDKs</span></span>
<span data-ttu-id="d317a-133">В Azure Cosmos DB добавлена поддержка автоматического секционирования с использованием [REST API версии 2015-12-16](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="d317a-133">Azure Cosmos DB added support for automatic partitioning with [REST API version 2015-12-16](/rest/api/documentdb/).</span></span> <span data-ttu-id="d317a-134">В контейнерах toocreate секционированы заказ, необходимо загрузить пакет SDK версии 1.6.0 или более поздней версии в один из hello поддерживается пакет SDK платформы (.NET, Node.js, Java, Python, MongoDB).</span><span class="sxs-lookup"><span data-stu-id="d317a-134">In order toocreate partitioned containers, you must download SDK versions 1.6.0 or newer in one of hello supported SDK platforms (.NET, Node.js, Java, Python, MongoDB).</span></span> 

### <a name="creating-containers"></a><span data-ttu-id="d317a-135">Создание контейнеров</span><span class="sxs-lookup"><span data-stu-id="d317a-135">Creating containers</span></span>
<span data-ttu-id="d317a-136">Hello ниже приведен пример toocreate .NET фрагмент данных телеметрии устройства toostore контейнера из 20 000 единиц запросов в секунду, пропускной способности.</span><span class="sxs-lookup"><span data-stu-id="d317a-136">hello following sample shows a .NET snippet toocreate a container toostore device telemetry data of 20,000 request units per second of throughput.</span></span> <span data-ttu-id="d317a-137">Hello SDK устанавливает значение OfferThroughput hello (который в свою очередь устанавливает hello `x-ms-offer-throughput` заголовок запроса в hello REST API).</span><span class="sxs-lookup"><span data-stu-id="d317a-137">hello SDK sets hello OfferThroughput value (which in turn sets hello `x-ms-offer-throughput` request header in hello REST API).</span></span> <span data-ttu-id="d317a-138">Здесь мы устанавливаем hello `/deviceId` в качестве ключа секции hello.</span><span class="sxs-lookup"><span data-stu-id="d317a-138">Here we set hello `/deviceId` as hello partition key.</span></span> <span data-ttu-id="d317a-139">Выбор Hello ключа раздела сохраняется вместе с остальной hello метаданных контейнера hello, такие как имя и политика индексирования.</span><span class="sxs-lookup"><span data-stu-id="d317a-139">hello choice of partition key is saved along with hello rest of hello container metadata like name and indexing policy.</span></span>

<span data-ttu-id="d317a-140">Для этого примера мы выбрали `deviceId` так, как мы знаем, что (a), так как существует большое количество устройств, записи могут распространяться по разделам равномерно и позволяет нам tooscale hello базы данных tooingest больших объемов данных и (б) многие запросы hello, например Выборка hello последнюю чтения для устройства, которые deviceId одной области tooa и могут извлекаться из одной секции.</span><span class="sxs-lookup"><span data-stu-id="d317a-140">For this sample, we picked `deviceId` since we know that (a) since there are a large number of devices, writes can be distributed across partitions evenly and allowing us tooscale hello database tooingest massive volumes of data and (b) many of hello requests like fetching hello latest reading for a device are scoped tooa single deviceId and can be retrieved from a single partition.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
await client.CreateDatabaseAsync(new Database { Id = "db" });

// Container for device telemetry. Here hello property deviceId will be used as hello partition key too
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

<span data-ttu-id="d317a-141">Этот метод выполняет вызов tooCosmos DB API REST и службу hello подготовит число секций, основанных на запрошенный hello пропускную способность.</span><span class="sxs-lookup"><span data-stu-id="d317a-141">This method makes a REST API call tooCosmos DB, and hello service will provision a number of partitions based on hello requested throughput.</span></span> <span data-ttu-id="d317a-142">Пропускная способность hello контейнера можно изменить, как производительность должна развиваться.</span><span class="sxs-lookup"><span data-stu-id="d317a-142">You can change hello throughput of a container as your performance needs evolve.</span></span> 

### <a name="reading-and-writing-items"></a><span data-ttu-id="d317a-143">Чтение и запись элементов</span><span class="sxs-lookup"><span data-stu-id="d317a-143">Reading and writing items</span></span>
<span data-ttu-id="d317a-144">Пора перейти к вставке данных в Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d317a-144">Now, let's insert data into Cosmos DB.</span></span> <span data-ttu-id="d317a-145">Ниже приведен пример класса, содержащего чтения устройства и вызова tooCreateDocumentAsync tooinsert новое устройство чтения в контейнер.</span><span class="sxs-lookup"><span data-stu-id="d317a-145">Here's a sample class containing a device reading, and a call tooCreateDocumentAsync tooinsert a new device reading into a container.</span></span> <span data-ttu-id="d317a-146">Ниже приведен пример использования hello DocumentDB API:</span><span class="sxs-lookup"><span data-stu-id="d317a-146">This is an example leveraging hello DocumentDB API:</span></span>

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

// Create a document. Here hello partition key is extracted as "XMS-0001" based on hello collection definition
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

<span data-ttu-id="d317a-147">Давайте прочитать элемент hello вместе с ключом раздела и идентификатор, обновите его и в качестве последнего шага, удалите его с ключом раздела и идентификатор. Обратите внимание, что операции чтения hello включать значение PartitionKey (соответствующий toohello `x-ms-documentdb-partitionkey` заголовок запроса в hello REST API).</span><span class="sxs-lookup"><span data-stu-id="d317a-147">Let's read hello item by its partition key and id, update it, and then as a final step, delete it by partition key and id. Note that hello reads include a PartitionKey value (corresponding toohello `x-ms-documentdb-partitionkey` request header in hello REST API).</span></span>

```csharp
// Read document. Needs hello partition key and hello ID toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;

// Update hello document. Partition key is not required, again extracted from hello document
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

### <a name="querying-partitioned-containers"></a><span data-ttu-id="d317a-148">Запрос секционированных контейнеров</span><span class="sxs-lookup"><span data-stu-id="d317a-148">Querying partitioned containers</span></span>
<span data-ttu-id="d317a-149">При запросе данных в секционированных контейнеры Cosmos DB автоматически маршруты hello секций toohello запросов соответствующие значения ключа раздела toohello, указанных в фильтре hello (если таковые имеются).</span><span class="sxs-lookup"><span data-stu-id="d317a-149">When you query data in partitioned containers, Cosmos DB automatically routes hello query toohello partitions corresponding toohello partition key values specified in hello filter (if there are any).</span></span> <span data-ttu-id="d317a-150">Например этот запрос является перенаправленное toojust hello содержащего hello секции ключ раздела «XMS-0001».</span><span class="sxs-lookup"><span data-stu-id="d317a-150">For example, this query is routed toojust hello partition containing hello partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="d317a-151">Hello следующий запрос не имеет фильтр на ключ секционирования hello (DeviceId) и fanned out tooall секций, где он выполняется для hello секционирования индекса.</span><span class="sxs-lookup"><span data-stu-id="d317a-151">hello following query does not have a filter on hello partition key (DeviceId) and is fanned out tooall partitions where it is executed against hello partition's index.</span></span> <span data-ttu-id="d317a-152">Обратите внимание, что toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` в hello REST API) toohave hello SDK tooexecute запросов в секциях.</span><span class="sxs-lookup"><span data-stu-id="d317a-152">Note that you have toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello REST API) toohave hello SDK tooexecute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

<span data-ttu-id="d317a-153">Cosmos DB поддерживает [статистические функции](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` и `AVG` для секционированных контейнеров с помощью SQL с пакетом SDK 1.12.0 и выше.</span><span class="sxs-lookup"><span data-stu-id="d317a-153">Cosmos DB supports [aggregate functions](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` and `AVG` over partitioned containers using SQL starting with SDKs 1.12.0 and above.</span></span> <span data-ttu-id="d317a-154">Запросы должна содержать один статистический оператор и должен включать одного значения в проекции hello.</span><span class="sxs-lookup"><span data-stu-id="d317a-154">Queries must include a single aggregate operator, and must include a single value in hello projection.</span></span>

### <a name="parallel-query-execution"></a><span data-ttu-id="d317a-155">Параллельное выполнение запросов</span><span class="sxs-lookup"><span data-stu-id="d317a-155">Parallel query execution</span></span>
<span data-ttu-id="d317a-156">пакеты SDK DB Cosmos 1.9.0 Hello и выше поддерживается параметры выполнения параллельных запросов, позволяющих tooperform низкой задержкой запросов в секционированных коллекций даже в том случае, если они должны tootouch большее число секций.</span><span class="sxs-lookup"><span data-stu-id="d317a-156">hello Cosmos DB SDKs 1.9.0 and above support parallel query execution options, which allow you tooperform low latency queries against partitioned collections, even when they need tootouch a large number of partitions.</span></span> <span data-ttu-id="d317a-157">Например приветствия при следующем запросе является настроенным toorun параллельно в секциях.</span><span class="sxs-lookup"><span data-stu-id="d317a-157">For example, hello following query is configured toorun in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="d317a-158">Вы можете управлять параллельного выполнения запросов, настроив hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="d317a-158">You can manage parallel query execution by tuning hello following parameters:</span></span>

* <span data-ttu-id="d317a-159">Установив `MaxDegreeOfParallelism`, можно управлять степенью параллелизма, т. е. hello максимального количества одновременных сетевых подключений toohello контейнера секций hello.</span><span class="sxs-lookup"><span data-stu-id="d317a-159">By setting `MaxDegreeOfParallelism`, you can control hello degree of parallelism i.e., hello maximum number of simultaneous network connections toohello container's partitions.</span></span> <span data-ttu-id="d317a-160">Если присвоить этому слишком 1 hello SDK управляет hello степень параллелизма.</span><span class="sxs-lookup"><span data-stu-id="d317a-160">If you set this too-1, hello degree of parallelism is managed by hello SDK.</span></span> <span data-ttu-id="d317a-161">Если hello `MaxDegreeOfParallelism` не задан или имеет too0, которое является значением по умолчанию hello, будет иметь секции контейнера toohello одного сетевого подключения.</span><span class="sxs-lookup"><span data-stu-id="d317a-161">If hello `MaxDegreeOfParallelism` is not specified or set too0, which is hello default value, there will be a single network connection toohello container's partitions.</span></span>
* <span data-ttu-id="d317a-162">Параметр `MaxBufferedItemCount` обеспечивает баланс между задержкой запросов и использованием памяти на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="d317a-162">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="d317a-163">Если этот параметр не указан или задайте слишком 1 hello SDK управляет hello количество элементов в буфер во время выполнения параллельных запросов.</span><span class="sxs-lookup"><span data-stu-id="d317a-163">If you omit this parameter or set this too-1, hello number of items buffered during parallel query execution is managed by hello SDK.</span></span>

<span data-ttu-id="d317a-164">Учитывая hello такое же состояние коллекции hello, параллельный запрос возвращает результаты hello порядок таким же как и последовательного выполнения.</span><span class="sxs-lookup"><span data-stu-id="d317a-164">Given hello same state of hello collection, a parallel query will return results in hello same order as in serial execution.</span></span> <span data-ttu-id="d317a-165">При выполнении запроса между разделами, включающего Сортировка (ORDER BY и TOP), проблемы Azure Cosmos DB SDK hello hello запроса в параллельном режиме между секции и выполняет слияние частично отсортированные результаты hello клиента стороне tooproduce глобально упорядочиваются результаты.</span><span class="sxs-lookup"><span data-stu-id="d317a-165">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), hello Azure Cosmos DB SDK issues hello query in parallel across partitions and merges partially sorted results in hello client side tooproduce globally ordered results.</span></span>

### <a name="executing-stored-procedures"></a><span data-ttu-id="d317a-166">Выполнение хранимых процедур</span><span class="sxs-lookup"><span data-stu-id="d317a-166">Executing stored procedures</span></span>
<span data-ttu-id="d317a-167">Также можно выполнить атомарные транзакции с документами с hello таким же Идентификатором устройства, например если обслуживание статистических выражений или hello последнее состояние устройства в один элемент.</span><span class="sxs-lookup"><span data-stu-id="d317a-167">You can also execute atomic transactions against documents with hello same device ID, e.g. if you're maintaining aggregates or hello latest state of a device in a single item.</span></span> 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
<span data-ttu-id="d317a-168">В следующем разделе hello рассматривается как toopartitioned контейнеры можно перемещать из одной секции контейнеров.</span><span class="sxs-lookup"><span data-stu-id="d317a-168">In hello next section, we look at how you can move toopartitioned containers from single-partition containers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d317a-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d317a-169">Next steps</span></span>
<span data-ttu-id="d317a-170">В этой статье мы предоставляем Общие сведения о том, как toowork с секционированием Azure Cosmos DB контейнеров с hello DocumentDB API.</span><span class="sxs-lookup"><span data-stu-id="d317a-170">In this article, we provided an overview of how toowork with partitioning of Azure Cosmos DB containers with hello DocumentDB API.</span></span> <span data-ttu-id="d317a-171">Обзор концепций и рекомендации для секционирования с использованием любого API базы данных Azure Cosmos DB см. [в этой статье](../cosmos-db/partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="d317a-171">Also see [partitioning and horizontal scaling](../cosmos-db/partition-data.md) for an overview of concepts and best practices for partitioning with any Azure Cosmos DB API.</span></span> 

* <span data-ttu-id="d317a-172">Выполняйте проверку масштабирования и производительности с помощью базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d317a-172">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="d317a-173">Пример см. в статье [Проверка производительности и масштабирования с помощью Azure DocumentDB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="d317a-173">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="d317a-174">Приступить к созданию кода с hello [пакетов SDK](documentdb-sdk-dotnet.md) или hello [API-интерфейса REST](/rest/api/documentdb/)</span><span class="sxs-lookup"><span data-stu-id="d317a-174">Get started coding with hello [SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/)</span></span>
* <span data-ttu-id="d317a-175">Дополнительные сведения о подготовленной пропускной способности в базе данных Azure Cosmos DB см. в [этой статье](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="d317a-175">Learn about [provisioned throughput in Azure Cosmos DB](request-units.md)</span></span>

