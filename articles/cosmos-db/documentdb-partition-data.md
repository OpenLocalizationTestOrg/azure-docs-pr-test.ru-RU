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
# <a name="partitioning-in-azure-cosmos-db-using-hello-documentdb-api"></a>Секционирование в базу данных Cosmos Azure, используя hello DocumentDB API

[Microsoft Azure Cosmos DB](../cosmos-db/introduction.md) является toohelp служба, предоставляющая глобальной распределенной базы данных моделей, можно добиться быстрого и предсказуемая производительность и масштабируемость без проблем вместе с приложением при увеличении его. 

Приводятся общие сведения о том, как toowork с секционированием Cosmos DB контейнеров с hello DocumentDB API. Обзор концепций и рекомендации для секционирования с использованием любого API базы данных Azure Cosmos DB см. [в этой статье](../cosmos-db/partition-data.md). 

tooget к выполнению кода, загрузите проект hello из [Github](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark). 

После считывания в этой статье, можно будет tooanswer hello следующие вопросы:   

* Как работает секционирование в Azure Cosmos DB?
* Как настроить секционирование в Azure Cosmos DB
* Что такое ключи секций и как выбрать hello правильный ключ секции для моего приложения?

tooget к выполнению кода, загрузите проект hello из [пример драйвера тестирование в производительности для Azure Cosmos DB](https://github.com/Azure/azure-documentdb-dotnet/tree/a2d61ddb53f8ab2a23d3ce323c77afcf5a608f52/samples/documentdb-benchmark). 

<!-- placeholder until we have a permanent solution-->
<a name="partition-keys"></a>
<a name="single-partition-and-partitioned-collections"></a>
<a name="migrating-from-single-partition"></a>

## <a name="partition-keys"></a>Ключи секции

В hello DocumentDB API укажите hello определение ключа раздела в форме hello пути JSON. Hello следующей таблице показаны примеры определения ключа секции и hello значения, соответствующие tooeach. ключ раздела Hello указывается как путь, например `/department` представляет hello свойство отдела. 

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>Ключ секции</strong></p></td>
            <td valign="top"><p><strong>Описание</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>/department</p></td>
            <td valign="top"><p>Соответствует значение toohello doc.department, где элемент hello doc.</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/properties/name</p></td>
            <td valign="top"><p>Соответствует значение toohello doc.properties.name, где doc — элемент hello (вложенного свойства).</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/id</p></td>
            <td valign="top"><p>Соответствующее значение toohello doc.id (ключ идентификатора и секции hello же свойство).</p></td>
        </tr>
        <tr>
            <td valign="top"><p>/"имя отдела"</p></td>
            <td valign="top"><p>Соответствует значение toohello doc [«название отдела»], где элемент hello doc.</p></td>
        </tr>
    </tbody>
</table>

> [!NOTE]
> Hello для ключа раздела используется следующий синтаксис аналогичные toohello пути для путей политики индексирования с hello ключевое различие, hello путь соответствует свойству toohello вместо значения hello, т. е. имеется не подстановочному знаку в конце hello. Например, для индексации значений в отделе используется /department/?, tooindex hello значения в группе отдела, но указать /department как определение ключа секции hello. ключ раздела Hello индексируется неявно и не может быть исключен из индексирования с помощью индексирования переопределения параметров политики.
> 
> 

Давайте посмотрим, как выбор hello ключ раздела влияет на производительность приложения hello.

## <a name="working-with-hello-azure-cosmos-db-sdks"></a>Работа с hello Azure Cosmos DB SDK
В Azure Cosmos DB добавлена поддержка автоматического секционирования с использованием [REST API версии 2015-12-16](/rest/api/documentdb/). В контейнерах toocreate секционированы заказ, необходимо загрузить пакет SDK версии 1.6.0 или более поздней версии в один из hello поддерживается пакет SDK платформы (.NET, Node.js, Java, Python, MongoDB). 

### <a name="creating-containers"></a>Создание контейнеров
Hello ниже приведен пример toocreate .NET фрагмент данных телеметрии устройства toostore контейнера из 20 000 единиц запросов в секунду, пропускной способности. Hello SDK устанавливает значение OfferThroughput hello (который в свою очередь устанавливает hello `x-ms-offer-throughput` заголовок запроса в hello REST API). Здесь мы устанавливаем hello `/deviceId` в качестве ключа секции hello. Выбор Hello ключа раздела сохраняется вместе с остальной hello метаданных контейнера hello, такие как имя и политика индексирования.

Для этого примера мы выбрали `deviceId` так, как мы знаем, что (a), так как существует большое количество устройств, записи могут распространяться по разделам равномерно и позволяет нам tooscale hello базы данных tooingest больших объемов данных и (б) многие запросы hello, например Выборка hello последнюю чтения для устройства, которые deviceId одной области tooa и могут извлекаться из одной секции.

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

Этот метод выполняет вызов tooCosmos DB API REST и службу hello подготовит число секций, основанных на запрошенный hello пропускную способность. Пропускная способность hello контейнера можно изменить, как производительность должна развиваться. 

### <a name="reading-and-writing-items"></a>Чтение и запись элементов
Пора перейти к вставке данных в Cosmos DB. Ниже приведен пример класса, содержащего чтения устройства и вызова tooCreateDocumentAsync tooinsert новое устройство чтения в контейнер. Ниже приведен пример использования hello DocumentDB API:

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

Давайте прочитать элемент hello вместе с ключом раздела и идентификатор, обновите его и в качестве последнего шага, удалите его с ключом раздела и идентификатор. Обратите внимание, что операции чтения hello включать значение PartitionKey (соответствующий toohello `x-ms-documentdb-partitionkey` заголовок запроса в hello REST API).

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

### <a name="querying-partitioned-containers"></a>Запрос секционированных контейнеров
При запросе данных в секционированных контейнеры Cosmos DB автоматически маршруты hello секций toohello запросов соответствующие значения ключа раздела toohello, указанных в фильтре hello (если таковые имеются). Например этот запрос является перенаправленное toojust hello содержащего hello секции ключ раздела «XMS-0001».

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
Hello следующий запрос не имеет фильтр на ключ секционирования hello (DeviceId) и fanned out tooall секций, где он выполняется для hello секционирования индекса. Обратите внимание, что toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` в hello REST API) toohave hello SDK tooexecute запросов в секциях.

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

Cosmos DB поддерживает [статистические функции](documentdb-sql-query.md#Aggregates) `COUNT`, `MIN`, `MAX`, `SUM` и `AVG` для секционированных контейнеров с помощью SQL с пакетом SDK 1.12.0 и выше. Запросы должна содержать один статистический оператор и должен включать одного значения в проекции hello.

### <a name="parallel-query-execution"></a>Параллельное выполнение запросов
пакеты SDK DB Cosmos 1.9.0 Hello и выше поддерживается параметры выполнения параллельных запросов, позволяющих tooperform низкой задержкой запросов в секционированных коллекций даже в том случае, если они должны tootouch большее число секций. Например приветствия при следующем запросе является настроенным toorun параллельно в секциях.

```csharp
// Cross-partition Order By Queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
Вы можете управлять параллельного выполнения запросов, настроив hello следующие параметры:

* Установив `MaxDegreeOfParallelism`, можно управлять степенью параллелизма, т. е. hello максимального количества одновременных сетевых подключений toohello контейнера секций hello. Если присвоить этому слишком 1 hello SDK управляет hello степень параллелизма. Если hello `MaxDegreeOfParallelism` не задан или имеет too0, которое является значением по умолчанию hello, будет иметь секции контейнера toohello одного сетевого подключения.
* Параметр `MaxBufferedItemCount` обеспечивает баланс между задержкой запросов и использованием памяти на стороне клиента. Если этот параметр не указан или задайте слишком 1 hello SDK управляет hello количество элементов в буфер во время выполнения параллельных запросов.

Учитывая hello такое же состояние коллекции hello, параллельный запрос возвращает результаты hello порядок таким же как и последовательного выполнения. При выполнении запроса между разделами, включающего Сортировка (ORDER BY и TOP), проблемы Azure Cosmos DB SDK hello hello запроса в параллельном режиме между секции и выполняет слияние частично отсортированные результаты hello клиента стороне tooproduce глобально упорядочиваются результаты.

### <a name="executing-stored-procedures"></a>Выполнение хранимых процедур
Также можно выполнить атомарные транзакции с документами с hello таким же Идентификатором устройства, например если обслуживание статистических выражений или hello последнее состояние устройства в один элемент. 

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```
   
В следующем разделе hello рассматривается как toopartitioned контейнеры можно перемещать из одной секции контейнеров.

## <a name="next-steps"></a>Дальнейшие действия
В этой статье мы предоставляем Общие сведения о том, как toowork с секционированием Azure Cosmos DB контейнеров с hello DocumentDB API. Обзор концепций и рекомендации для секционирования с использованием любого API базы данных Azure Cosmos DB см. [в этой статье](../cosmos-db/partition-data.md). 

* Выполняйте проверку масштабирования и производительности с помощью базы данных Azure Cosmos DB. Пример см. в статье [Проверка производительности и масштабирования с помощью Azure DocumentDB](performance-testing.md).
* Приступить к созданию кода с hello [пакетов SDK](documentdb-sdk-dotnet.md) или hello [API-интерфейса REST](/rest/api/documentdb/)
* Дополнительные сведения о подготовленной пропускной способности в базе данных Azure Cosmos DB см. в [этой статье](request-units.md).

