---
title: "Azure Cosmos DB: Разработку с использованием hello API DocumentDB в .NET | Документы Microsoft"
description: "Узнайте, как toodevelop с API Azure Cosmos DB DocumentDB, с помощью .NET"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: 0d3d17afa782054c8fdf3cbac421e5a5d0a6800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmosdb-develop-with-hello-documentdb-api-in-net"></a>Azure CosmosDB: Разработку с использованием hello API DocumentDB в .NET

Azure Cosmos DB — это глобально распределенная многомодельная служба базы данных Майкрософт. Вы можете быстро создать и запрашивать документа, ключ значение и graph баз данных, все из которых преимущества глобального распространения hello и возможности горизонтального масштабирования в основе hello Azure Cosmos БД. 

В этом учебнике показано, как toocreate Azure Cosmos DB учетной записи с помощью hello портал Azure, а затем создать базу данных документов и коллекции с [ключ раздела](documentdb-partition-data.md#partition-keys) с помощью hello [API .NET для DocumentDB](documentdb-introduction.md). Определив ключ раздела при создании коллекции, приложения подготавливается tooscale усилий по мере роста данных. 

Hello этого учебника описаны следующие задачи с помощью hello [API .NET для DocumentDB](documentdb-sdk-dotnet.md):

> [!div class="checklist"]
> * создание учетной записи Azure Cosmos DB;
> * создание базы данных и коллекции с ключом секции;
> * создание документов JSON;
> * обновление документа;
> * запрос секционированных коллекций;
> * выполнение хранимых процедур;
> * Удаление документа
> * удаление базы данных.

## <a name="prerequisites"></a>Предварительные требования
Убедитесь, что у вас есть следующие hello:

* Активная учетная запись Azure. Если у вас ее нет, зарегистрируйте [бесплатную учетную запись](https://azure.microsoft.com/free/). 
    * Кроме того, можно использовать hello [DB эмулятор Azure Cosmos](local-emulator.md) для этого учебника, если вы хотите toouse локальную среду, эмулирующую службы Azure DocumentDB hello в целях разработки.
* [Visual Studio](http://www.visualstudio.com/)

## <a name="create-an-azure-cosmos-db-account"></a>создание учетной записи Azure Cosmos DB;

Давайте начнем с создания учетной записи Azure Cosmos DB в hello портал Azure.

> [!TIP]
> * Уже есть учетная запись Azure Cosmos DB? Если Да, пропустить слишком[Настройка решения Visual Studio](#SetupVS)
> * У вас была учетная запись Azure DocumentDB? Если таким образом, учетной записи теперь учетную запись Azure Cosmos DB и можно сразу перейти слишком[Настройка решения Visual Studio](#SetupVS).  
> * Если вы используете hello Azure Cosmos DB эмулятор, выполните действия hello в [DB эмулятор Azure Cosmos](local-emulator.md) toosetup hello эмулятора и пропускать слишком[настроить решение Visual Studio](#SetupVS). 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a>Настройка решения Visual Studio
1. Откройте **Visual Studio** у себя на компьютере.
2. На hello **файл** последовательно выберите пункты **New**и нажмите кнопку **проекта**.
3. В hello **новый проект** диалогового окна выберите **шаблоны** / **Visual C#** / **консольного приложения (.NET Framework)**, имя проекта и нажмите кнопку **ОК**.
   ![Снимок экрана: hello окно нового проекта](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)

4. В hello **обозревателе решений**, щелкните правой кнопкой мыши новое консольное приложение, который находится под управлением решения Visual Studio, и нажмите кнопку **управление пакетами NuGet...**
    
    ![Снимок hello справа щелчок меню для проекта hello](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. В hello **NuGet** щелкните **Обзор**и тип **documentdb** в поле поиска hello.
<!---stopped here--->
6. В результатах поиска hello, найти **Microsoft.Azure.DocumentDB** и нажмите кнопку **установить**.
   Идентификатор пакета Hello hello клиентской библиотеки DB Cosmos Azure [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).
   ![Снимок экрана: hello меню NuGet для поиска Azure SDK клиента DB Cosmos](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)

    Если вы получите сообщение о рецензировании решения toohello изменения, нажмите кнопку **ОК**. Если появится сообщение о принятии условий лицензионного соглашения, щелкните **Принимаю**.

## <a id="Connect"></a>Добавьте ссылки на проект tooyour
Hello оставшихся шагов этого учебника укажите hello DocumentDB API код фрагменты необходимые toocreate и обновления Azure Cosmos DB ресурсов в проекте.

Во-первых добавьте эти ссылки tooyour приложения.
<!---These aren't added by default when you install hello pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <a id="add-references"></a>Подключение приложения

Добавьте эти две константы и переменную *client* в приложение.

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

Затем, head обратно toohello [портал Azure](https://portal.azure.com) tooretrieve URL-адрес конечной точки и первичный ключ. URL-адрес конечной точки Hello и первичный ключ, необходимые для вашего приложения toounderstand где tooconnect, а для Azure Cosmos DB tootrust подключения вашего приложения.

В hello портал Azure, перейдите учетная запись Azure Cosmos DB tooyour, щелкните **ключи**, а затем нажмите кнопку **ключи для чтения и записи**.

Скопируйте hello URI с портала hello и вставьте его через `<your endpoint URL>` в файл program.cs hello. Затем копирования hello первичный ключ с портала hello и вставьте его поверх `<your primary key>`. Быть убедиться, что hello tooremove `<` и `>` из этих значений.

![Снимок экрана: hello портал Azure используется hello NoSQL учебника toocreate консольное приложение C#. Показывает учетную запись Azure Cosmos DB, с hello ключи, выделяются в колонке учетная запись Azure Cosmos DB hello и hello URI, а также значения ПЕРВИЧНОГО ключа, выделяются в колонке ключи hello](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <a id="instantiate"></a>Создать экземпляр hello DocumentClient

Теперь создайте новый экземпляр hello **DocumentClient**.

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <a id="create-database"></a>Создание базы данных

Создайте базу данных Azure Cosmos [базы данных](documentdb-resources.md#databases) с помощью hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) метода или [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) метод hello  **DocumentClient** класс из hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md). База данных находится hello логический контейнер для хранения документов JSON, секционированный по коллекциям.

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a>Выбор ключа секции 

Коллекции — это контейнеры для хранения документов. Они являются логическими ресурсами и [могут включать в себя одну или несколько физических секций](partition-data.md). Объект [ключ раздела](documentdb-partition-data.md) является свойства (или пути) в документы, используемые toodistribute данных между серверами hello или секций. Все документы с одинаковым ключом секции хранятся в hello hello одной секции. 

Очень важное решение toomake определить ключ раздела, перед тем как создать коллекцию. Ключи секций представляют собой свойства (или пути) в документах, которые могут быть используемые toodistribute Azure Cosmos DB данных между несколькими серверами или секций. Cosmos DB хэширует значение ключа секции hello и использует секции hello toodetermine результат hello хэшируются в какой документ toostore hello. Все документы с одинаковым ключом секции хранятся в hello hello одной секции и ключи разделов нельзя изменять после создания коллекции. 

В этом учебнике мы создадим ключ раздела hello tooset слишком`/deviceId` таким образом, hello все данные hello для одного устройства хранится в одной секции. Вы хотите toochoose ключа раздела, который имеет большое количество значений, каждое из которых используются в о hello же частотой tooensure Cosmos DB может выполнять балансировку нагрузки при расширении данных, что добиться hello пропускную способность коллекции hello. 

Дополнительные сведения о секционировании см. в разделе [как toopartition и масштабирования в Azure Cosmos DB?](partition-data.md) 

## <a id="CreateColl"></a>Создание коллекции 

Теперь, когда мы знаем, нашей ключ раздела `/deviceId`, позволяет создавать [коллекции](documentdb-resources.md#collections) с помощью hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) метода или [ CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) метод hello **DocumentClient** класса. Коллекция представляет собой контейнер документов JSON и любую связанную с ними логику в виде приложения JavaScript. 

> [!WARNING]
> Создание коллекции имеет цены последствия, как при резервировании пропускной способности для hello toocommunicate приложений с Azure Cosmos DB. Дополнительные сведения см. на нашей [странице цен](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

```csharp
// Collection for device telemetry. Here hello JSON property deviceId is used  
// as hello partition key toospread across partitions. Configured for 2500 RU/s  
// throughput and an indexing policy that supports sorting against any  
// number or string property. .
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 2500 });
```

Этот метод делает REST API вызовите tooAzure Cosmos DB и hello Подготовка службы число секций, основанных на запрошенный hello пропускную способность. Пропускная способность hello коллекции можно изменить, как производительность должна развиваться, с помощью пакета SDK для hello или hello [портал Azure](set-throughput.md).

## <a id="CreateDoc"></a>Создание документов JSON
Вставьте несколько документов JSON в базу данных Azure Cosmos DB. Объект [документа](documentdb-resources.md#documents) могут быть созданы с помощью hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) метод hello **DocumentClient** класса. Документы относятся к пользовательскому (произвольному) содержимому JSON. Этот пример класса содержит чтения устройства и вызова tooCreateDocumentAsync tooinsert новое устройство чтения в коллекцию.

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

// Create a document. Here hello partition key is extracted 
// as "XMS-0001" based on hello collection definition
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
## <a name="read-data"></a>Считывание данных

Давайте чтения документа hello вместе с ключом раздела и идентификатор, с помощью метода ReadDocumentAsync hello. Обратите внимание, что операции чтения hello включать значение PartitionKey (соответствующий toohello `x-ms-documentdb-partitionkey` заголовок запроса в hello REST API).

```csharp
// Read document. Needs hello partition key and hello Id toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a>Обновление данных

Теперь давайте обновление некоторых данных с использованием метода ReplaceDocumentAsync hello.

```csharp
// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a>Удаление данных

Позволяет удалить документа с ключом раздела и идентификатор с помощью метода DeleteDocumentAsync hello.

```csharp
// Delete a document. hello partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a>Запрос секционированных коллекций

При запросе данных в секционированных коллекций Azure Cosmos DB автоматически маршруты hello секций toohello запросов соответствующие значения ключа раздела toohello, указанных в фильтре hello (если таковые имеются). Например этот запрос является перенаправленное toojust hello содержащего hello секции ключ раздела «XMS-0001».

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

## <a name="parallel-query-execution"></a>Параллельное выполнение запросов
Hello Azure пакеты SDK DocumentDB DB Cosmos 1.9.0 и выше поддерживается параметры выполнения параллельных запросов, позволяющих tooperform низкой задержкой запросов в секционированных коллекций даже в том случае, если они должны tootouch большее число секций. Например приветствия при следующем запросе является настроенным toorun параллельно в секциях.

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
Вы можете управлять параллельного выполнения запросов, настроив hello следующие параметры:

* Установив `MaxDegreeOfParallelism`, можно управлять степенью параллелизма, т. е. hello максимального количества одновременных сетевых подключений toohello коллекцию секций hello. Если присвоить этому слишком 1 hello SDK управляет hello степень параллелизма. Если hello `MaxDegreeOfParallelism` не задан или имеет too0, которое является значением по умолчанию hello, будет коллекции соединений одного сетевого toohello секций.
* Параметр `MaxBufferedItemCount` обеспечивает баланс между задержкой запросов и использованием памяти на стороне клиента. Если этот параметр не указан или задайте слишком 1 hello SDK управляет hello количество элементов в буфер во время выполнения параллельных запросов.

Учитывая hello такое же состояние коллекции hello, параллельный запрос возвращает результаты hello порядок таким же как и последовательного выполнения. При выполнении запроса между разделами, включающего Сортировка (ORDER BY и TOP), hello DocumentDB SDK выдает запрос hello параллельно в секциях и выполняет слияние частично отсортированные результаты в hello клиента стороне tooproduce глобально упорядочиваются результаты.

## <a name="execute-stored-procedures"></a>Выполнение хранимых процедур
Наконец, можно выполнять атомарные транзакции с документами с hello таким же Идентификатором устройства, например если обслуживание статистических выражений или hello последнее состояние устройств в одном документе, добавив следующий проект tooyour кода hello.

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

Вот и все! Это основные компоненты hello Azure Cosmos DB приложение, использующее масштаб данных секции tooefficiently ключа распределения по секциям.  

## <a name="clean-up-resources"></a>Очистка ресурсов

Если вы не будете toocontinue toouse это приложение, необходимо удалите все ресурсы, созданные в этом учебнике в hello портал Azure с hello следующие шаги:

1. Hello слева в меню портала Azure hello, пункт **групп ресурсов** и нажмите кнопку hello уникальное имя созданного ресурса hello. 
2. На странице группы ресурсов, нажмите кнопку **удаление**, введите имя hello toodelete ресурсов hello в hello текстовое поле и нажмите кнопку **удалить**.

## <a name="next-steps"></a>Дальнейшие действия

В этом учебнике вы сделали hello следующее: 

> [!div class="checklist"]
> * создали учетную запись Azure Cosmos DB;
> * создали базу данных и коллекцию с ключом секции;
> * создали документы JSON;
> * обновили документ;
> * запросили секционированные коллекции;
> * выполнили хранимую процедуру;
> * удалили документ;
> * удалили базу данных.

Теперь можно продолжить toohello следующее руководство и импортировать учетную запись Cosmos DB tooyour дополнительные данные. 

> [!div class="nextstepaction"]
> [Импорт данных в DocumentDB с помощью средства миграции базы данных](import-data.md)
