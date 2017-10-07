---
title: "aaaGet к работе с хранилищем таблиц Azure, с помощью .NET | Документы Microsoft"
description: "Хранения структурированных данных в облаке hello, с помощью хранилища таблиц Azure, хранилище данных NoSQL."
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fe46d883-7bed-49dd-980e-5c71df36adb3
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 04/10/2017
ms.author: mimig
ms.openlocfilehash: a3e9a4c6f6fd5e724535b86a3f99cd4c161de6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-using-net"></a><span data-ttu-id="63de2-103">Приступая к работе с хранилищем таблиц Azure с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="63de2-103">Get started with Azure Table storage using .NET</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="63de2-104">Хранилище таблиц Azure — это служба, хранит структурированные NoSQL хранить данные в облаке hello, предоставляя ключевой атрибут с schemaless конструктора.</span><span class="sxs-lookup"><span data-stu-id="63de2-104">Azure Table storage is a service that stores structured NoSQL data in hello cloud, providing a key/attribute store with a schemaless design.</span></span> <span data-ttu-id="63de2-105">Так как хранилище таблиц schemaless, это легко tooadapt данных в качестве hello потребностей вашего приложения evolve.</span><span class="sxs-lookup"><span data-stu-id="63de2-105">Because Table storage is schemaless, it's easy tooadapt your data as hello needs of your application evolve.</span></span> <span data-ttu-id="63de2-106">Доступ к данным хранилища tooTable быстрый и экономичный для многих типов приложений и обычно ниже стоимости традиционные SQL аналогичные объемами данных.</span><span class="sxs-lookup"><span data-stu-id="63de2-106">Access tooTable storage data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span></span>

<span data-ttu-id="63de2-107">Гибкие наборы таблицы хранилища toostore и связанных данных как пользовательские данные можно использовать для веб-приложений, адресные книги, сведения об устройстве или другие виды метаданные, необходимые для службы.</span><span class="sxs-lookup"><span data-stu-id="63de2-107">You can use Table storage toostore flexible datasets like user data for web applications, address books, device information, or other types of metadata your service requires.</span></span> <span data-ttu-id="63de2-108">Можно хранить любое число сущностей в таблице, и учетную запись хранилища может содержать любое количество таблиц, копирование toohello пределу пропускной способности hello учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="63de2-108">You can store any number of entities in a table, and a storage account may contain any number of tables, up toohello capacity limit of hello storage account.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="63de2-109">О данном учебнике</span><span class="sxs-lookup"><span data-stu-id="63de2-109">About this tutorial</span></span>
<span data-ttu-id="63de2-110">В этом учебнике показано как toouse hello [клиентская библиотека хранилища Azure для .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) в некоторые распространенные сценарии хранилища таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="63de2-110">This tutorial shows you how toouse hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) in some common Azure Table storage scenarios.</span></span> <span data-ttu-id="63de2-111">Эти сценарии представлены с помощью примеров C# для создания и удаления таблиц, а также вставки, обновления, удаления и запроса данных таблицы.</span><span class="sxs-lookup"><span data-stu-id="63de2-111">These scenarios are presented using C# examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63de2-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="63de2-112">Prerequisites</span></span>

<span data-ttu-id="63de2-113">Вы должны hello следующие toocomplete этого учебника успешно:</span><span class="sxs-lookup"><span data-stu-id="63de2-113">You need hello following toocomplete this tutorial successfully:</span></span>

* [<span data-ttu-id="63de2-114">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="63de2-114">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="63de2-115">Клиентская библиотека хранилища Azure для .NET</span><span class="sxs-lookup"><span data-stu-id="63de2-115">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="63de2-116">Диспетчер конфигураций Azure для .NET</span><span class="sxs-lookup"><span data-stu-id="63de2-116">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [<span data-ttu-id="63de2-117">Учетная запись хранения Azure</span><span class="sxs-lookup"><span data-stu-id="63de2-117">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="63de2-118">Другие примеры</span><span class="sxs-lookup"><span data-stu-id="63de2-118">More samples</span></span>
<span data-ttu-id="63de2-119">Дополнительные примеры использования хранилища таблиц см. в статье [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/) (Приступая к работе с хранилищем таблиц Azure в .NET).</span><span class="sxs-lookup"><span data-stu-id="63de2-119">For additional examples using Table storage, see [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/).</span></span> <span data-ttu-id="63de2-120">Можно загрузить пример приложения hello и запустите его или просмотр кода hello в GitHub.</span><span class="sxs-lookup"><span data-stu-id="63de2-120">You can download hello sample application and run it, or browse hello code on GitHub.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="63de2-121">Добавление директив using</span><span class="sxs-lookup"><span data-stu-id="63de2-121">Add using directives</span></span>
<span data-ttu-id="63de2-122">Добавьте следующее hello **с помощью** директивы toohello вверху hello `Program.cs` файла:</span><span class="sxs-lookup"><span data-stu-id="63de2-122">Add hello following **using** directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="63de2-123">Синтаксический анализ строки соединения hello</span><span class="sxs-lookup"><span data-stu-id="63de2-123">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-table-service-client"></a><span data-ttu-id="63de2-124">Создание клиента службы таблиц hello</span><span class="sxs-lookup"><span data-stu-id="63de2-124">Create hello Table service client</span></span>
<span data-ttu-id="63de2-125">Hello [CloudTableClient] [ dotnet_CloudTableClient] класс позволяет tooretrieve таблиц и сущностей, хранящихся в хранилище таблиц.</span><span class="sxs-lookup"><span data-stu-id="63de2-125">hello [CloudTableClient][dotnet_CloudTableClient] class enables you tooretrieve tables and entities stored in Table storage.</span></span> <span data-ttu-id="63de2-126">Вот клиента службы таблиц одним из способов toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="63de2-126">Here's one way toocreate hello Table service client:</span></span>

```csharp
// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

<span data-ttu-id="63de2-127">Теперь все готово toowrite код, который считывает и записывает tooTable хранения данных.</span><span class="sxs-lookup"><span data-stu-id="63de2-127">Now you are ready toowrite code that reads data from and writes data tooTable storage.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="63de2-128">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="63de2-128">Create a table</span></span>
<span data-ttu-id="63de2-129">В этом примере показано, как toocreate таблицы, если он еще не существует:</span><span class="sxs-lookup"><span data-stu-id="63de2-129">This example shows how toocreate a table if it does not already exist:</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Retrieve a reference toohello table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello table if it doesn't exist.
table.CreateIfNotExists();
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="63de2-130">Добавьте таблицу tooa сущности</span><span class="sxs-lookup"><span data-stu-id="63de2-130">Add an entity tooa table</span></span>
<span data-ttu-id="63de2-131">Сущности сопоставляют tooC # объектов с помощью пользовательского класса, производного от [TableEntity][dotnet_TableEntity].</span><span class="sxs-lookup"><span data-stu-id="63de2-131">Entities map tooC# objects by using a custom class derived from [TableEntity][dotnet_TableEntity].</span></span> <span data-ttu-id="63de2-132">tooadd таблицу tooa сущности, создайте класс, определяющий hello свойства сущности.</span><span class="sxs-lookup"><span data-stu-id="63de2-132">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="63de2-133">Hello следующий код определяет класс сущностей, который использует имя клиента hello как ключ строки hello и фамилию в качестве ключа секции hello.</span><span class="sxs-lookup"><span data-stu-id="63de2-133">hello following code defines an entity class that uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="63de2-134">Вместе секции и ключом строки однозначно идентифицируют его в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="63de2-134">Together, an entity's partition and row key uniquely identify it in hello table.</span></span> <span data-ttu-id="63de2-135">Ключи секций сущности с одинаковым ключом секции, которые могут запрашиваться быстрее, чем сущностей с различными приветствия, но с помощью различных разделов обеспечивает улучшенную масштабируемость параллельных операций.</span><span class="sxs-lookup"><span data-stu-id="63de2-135">Entities with hello same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="63de2-136">Toobe сущностей, которые хранятся в таблицах, должен иметь поддерживаемый тип, например производными hello [TableEntity] [ dotnet_TableEntity] класса.</span><span class="sxs-lookup"><span data-stu-id="63de2-136">Entities toobe stored in tables must be of a supported type, for example derived from hello [TableEntity][dotnet_TableEntity] class.</span></span> <span data-ttu-id="63de2-137">Свойства сущности, хотелось бы toostore в таблице должен быть открытым свойствам типа hello и поддерживает получение и задание значений.</span><span class="sxs-lookup"><span data-stu-id="63de2-137">Entity properties you'd like toostore in a table must be public properties of hello type, and support both getting and setting of values.</span></span> <span data-ttu-id="63de2-138">Кроме того, тип сущности *должен* предоставлять конструктор без параметров.</span><span class="sxs-lookup"><span data-stu-id="63de2-138">Also, your entity type *must* expose a parameter-less constructor.</span></span>

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

<span data-ttu-id="63de2-139">Таблица операциям, задействующим сущностей выполняются через hello [CloudTable] [ dotnet_CloudTable] объекта, созданного ранее в разделе «Создание таблицы» hello.</span><span class="sxs-lookup"><span data-stu-id="63de2-139">Table operations that involve entities are performed via hello [CloudTable][dotnet_CloudTable] object that you created earlier in hello "Create a table" section.</span></span> <span data-ttu-id="63de2-140">Hello toobe операция выполняется представленного [TableOperation] [ dotnet_TableOperation] объекта.</span><span class="sxs-lookup"><span data-stu-id="63de2-140">hello operation toobe performed is represented by a [TableOperation][dotnet_TableOperation] object.</span></span> <span data-ttu-id="63de2-141">Hello следующем примере кода показано создание hello hello [CloudTable] [ dotnet_CloudTable] объекта и затем **CustomerEntity** объекта.</span><span class="sxs-lookup"><span data-stu-id="63de2-141">hello following code example shows hello creation of hello [CloudTable][dotnet_CloudTable] object and then a **CustomerEntity** object.</span></span> <span data-ttu-id="63de2-142">операции hello tooprepare [TableOperation] [ dotnet_TableOperation] tooinsert hello сущность «клиент» создается объект в таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="63de2-142">tooprepare hello operation, a [TableOperation][dotnet_TableOperation] object is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="63de2-143">Наконец, выполняется операция hello путем вызова [CloudTable][dotnet_CloudTable].[ Выполнение][dotnet_CloudTable_Execute].</span><span class="sxs-lookup"><span data-stu-id="63de2-143">Finally, hello operation is executed by calling [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute].</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="63de2-144">Вставка пакета сущностей</span><span class="sxs-lookup"><span data-stu-id="63de2-144">Insert a batch of entities</span></span>
<span data-ttu-id="63de2-145">Вы можете вставить пакет сущностей в таблицу в одной операции записи.</span><span class="sxs-lookup"><span data-stu-id="63de2-145">You can insert a batch of entities into a table in one write operation.</span></span> <span data-ttu-id="63de2-146">Некоторые другие примечания к пакетным операциям:</span><span class="sxs-lookup"><span data-stu-id="63de2-146">Some other notes on batch operations:</span></span>

* <span data-ttu-id="63de2-147">Можно выполнять обновления, удаления и вставки в hello же одной пакетной операции.</span><span class="sxs-lookup"><span data-stu-id="63de2-147">You can perform updates, deletes, and inserts in hello same single batch operation.</span></span>
* <span data-ttu-id="63de2-148">Одна пакетная операция могут включать копирование too100 сущностей.</span><span class="sxs-lookup"><span data-stu-id="63de2-148">A single batch operation can include up too100 entities.</span></span>
* <span data-ttu-id="63de2-149">Все сущности в одной пакетной операции должен иметь hello же ключ секционирования.</span><span class="sxs-lookup"><span data-stu-id="63de2-149">All entities in a single batch operation must have hello same partition key.</span></span>
* <span data-ttu-id="63de2-150">Хотя возможных tooperform запроса как пакетная операция, он должен быть hello только операции в пакете hello.</span><span class="sxs-lookup"><span data-stu-id="63de2-150">While it is possible tooperform a query as a batch operation, it must be hello only operation in hello batch.</span></span>

<span data-ttu-id="63de2-151">Hello примере кода создаются два объекта сущности и добавляются слишком[TableBatchOperation] [ dotnet_TableBatchOperation] с помощью hello [вставить] [ dotnet_TableBatchOperation_Insert] метод.</span><span class="sxs-lookup"><span data-stu-id="63de2-151">hello following code example creates two entity objects and adds each too[TableBatchOperation][dotnet_TableBatchOperation] by using hello [Insert][dotnet_TableBatchOperation_Insert] method.</span></span> <span data-ttu-id="63de2-152">Затем [CloudTable][dotnet_CloudTable].[ ExecuteBatch] [ dotnet_CloudTable_ExecuteBatch] вызывается операция tooexecute hello.</span><span class="sxs-lookup"><span data-stu-id="63de2-152">Then, [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch] is called tooexecute hello operation.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="63de2-153">Получение всех сущностей в разделе</span><span class="sxs-lookup"><span data-stu-id="63de2-153">Retrieve all entities in a partition</span></span>
<span data-ttu-id="63de2-154">таблицы для всех сущностей в секции, используйте tooquery [TableQuery] [ dotnet_TableQuery] объекта.</span><span class="sxs-lookup"><span data-stu-id="63de2-154">tooquery a table for all entities in a partition, use a [TableQuery][dotnet_TableQuery] object.</span></span> <span data-ttu-id="63de2-155">Hello следующий пример кода задает фильтр для сущности, где ключ раздела hello 'Smith'.</span><span class="sxs-lookup"><span data-stu-id="63de2-155">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="63de2-156">Этот пример выводит hello поля в каждой сущности в консоли toohello результаты запроса hello.</span><span class="sxs-lookup"><span data-stu-id="63de2-156">This example prints hello fields of each entity in hello query results toohello console.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Construct hello query operation for all customer entities where PartitionKey="Smith".
TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

// Print hello fields for each customer.
foreach (CustomerEntity entity in table.ExecuteQuery(query))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="63de2-157">Получение диапазона сущностей в разделе</span><span class="sxs-lookup"><span data-stu-id="63de2-157">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="63de2-158">Если вы не хотите tooquery все сущности в секции, можно указать диапазон, объединяя hello фильтра ключа секции с фильтром ключа строк.</span><span class="sxs-lookup"><span data-stu-id="63de2-158">If you don't want tooquery all entities in a partition, you can specify a range by combining hello partition key filter with a row key filter.</span></span> <span data-ttu-id="63de2-159">Hello следующий пример кода использует два tooget фильтры всех сущностей в разделе «Smith», где ключ строки hello (имя) начинается с буквы в алфавите hello перед «E», а затем выводит результаты запроса hello.</span><span class="sxs-lookup"><span data-stu-id="63de2-159">hello following code example uses two filters tooget all entities in partition 'Smith' where hello row key (first name) starts with a letter before 'E' in hello alphabet, then prints hello query results.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello table query.
TableQuery<CustomerEntity> rangeQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "E")));

// Loop through hello results, displaying information about hello entity.
foreach (CustomerEntity entity in table.ExecuteQuery(rangeQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="63de2-160">Извлечение одной сущности</span><span class="sxs-lookup"><span data-stu-id="63de2-160">Retrieve a single entity</span></span>
<span data-ttu-id="63de2-161">Можно написать tooretrieve запроса конкретную сущность.</span><span class="sxs-lookup"><span data-stu-id="63de2-161">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="63de2-162">Hello следующий код использует [TableOperation] [ dotnet_TableOperation] toospecify hello клиента 'Ben Smith'.</span><span class="sxs-lookup"><span data-stu-id="63de2-162">hello following code uses [TableOperation][dotnet_TableOperation] toospecify hello customer 'Ben Smith'.</span></span> <span data-ttu-id="63de2-163">Этот метод возвращает только одну сущность, а не коллекцией и hello возвращаемое значение в [TableResult][dotnet_TableResult].[ Результат] [ dotnet_TableResult_Result] — **CustomerEntity** объекта.</span><span class="sxs-lookup"><span data-stu-id="63de2-163">This method returns just one entity rather than a collection, and hello returned value in [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result] is a **CustomerEntity** object.</span></span> <span data-ttu-id="63de2-164">Указание ключи секций и строк в запросе является hello самый быстрый способ tooretrieve одной сущности из службы таблиц hello.</span><span class="sxs-lookup"><span data-stu-id="63de2-164">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Print hello phone number of hello result.
if (retrievedResult.Result != null)
{
    Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
}
else
{
    Console.WriteLine("hello phone number could not be retrieved.");
}
```

## <a name="replace-an-entity"></a><span data-ttu-id="63de2-165">Замена сущности</span><span class="sxs-lookup"><span data-stu-id="63de2-165">Replace an entity</span></span>
<span data-ttu-id="63de2-166">tooupdate сущности, получить его из службы таблиц hello, изменить объект сущности hello и сохранять изменения hello обратно toohello службы таблиц.</span><span class="sxs-lookup"><span data-stu-id="63de2-166">tooupdate an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="63de2-167">Hello следующий код позволяет изменить номер телефона существующего клиента.</span><span class="sxs-lookup"><span data-stu-id="63de2-167">hello following code changes an existing customer's phone number.</span></span> <span data-ttu-id="63de2-168">Вместо вызова метода [Insert][dotnet_TableOperation_Insert] этот код использует операцию [Replace][dotnet_TableOperation_Replace].</span><span class="sxs-lookup"><span data-stu-id="63de2-168">Instead of calling [Insert][dotnet_TableOperation_Insert], this code uses [Replace][dotnet_TableOperation_Replace].</span></span> <span data-ttu-id="63de2-169">[Замените] [ dotnet_TableOperation_Replace] причины hello полностью заменить на сервере hello toobe сущности, пока не изменят hello объекта на сервере hello, так как он был извлечен, в этом случае hello операция завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="63de2-169">[Replace][dotnet_TableOperation_Replace] causes hello entity toobe fully replaced on hello server, unless hello entity on hello server has changed since it was retrieved, in which case hello operation will fail.</span></span> <span data-ttu-id="63de2-170">Эта ошибка является tooprevent приложение случайно перезаписанный изменения внесены между hello извлечения и обновления приложения другим компонентом.</span><span class="sxs-lookup"><span data-stu-id="63de2-170">This failure is tooprevent your application from inadvertently overwriting a change made between hello retrieval and update by another component of your application.</span></span> <span data-ttu-id="63de2-171">Hello правильной обработки данного сбоя — tooretrieve hello сущность снова, внесенные изменения (если она все еще действует) и затем выполнять другую [заменить] [ dotnet_TableOperation_Replace] операции.</span><span class="sxs-lookup"><span data-stu-id="63de2-171">hello proper handling of this failure is tooretrieve hello entity again, make your changes (if still valid), and then perform another [Replace][dotnet_TableOperation_Replace] operation.</span></span> <span data-ttu-id="63de2-172">Hello следующем разделе будет показано, как toooverride это поведение.</span><span class="sxs-lookup"><span data-stu-id="63de2-172">hello next section will show you how toooverride this behavior.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign hello result tooa CustomerEntity object.
CustomerEntity updateEntity = (CustomerEntity)retrievedResult.Result;

if (updateEntity != null)
{
    // Change hello phone number.
    updateEntity.PhoneNumber = "425-555-0105";

    // Create hello Replace TableOperation.
    TableOperation updateOperation = TableOperation.Replace(updateEntity);

    // Execute hello operation.
    table.Execute(updateOperation);

    Console.WriteLine("Entity updated.");
}
else
{
    Console.WriteLine("Entity could not be retrieved.");
}
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="63de2-173">Вставка или замена сущности</span><span class="sxs-lookup"><span data-stu-id="63de2-173">Insert-or-replace an entity</span></span>
<span data-ttu-id="63de2-174">[Замените] [ dotnet_TableOperation_Replace] операции могут завершаться hello объекта было изменено, поскольку он был извлечен из сервера hello.</span><span class="sxs-lookup"><span data-stu-id="63de2-174">[Replace][dotnet_TableOperation_Replace] operations will fail if hello entity has been changed since it was retrieved from hello server.</span></span> <span data-ttu-id="63de2-175">Кроме того, необходимо получить hello объекта с сервера hello сначала в порядке для hello [заменить] [ dotnet_TableOperation_Replace] toobe операцию успешно.</span><span class="sxs-lookup"><span data-stu-id="63de2-175">Furthermore, you must retrieve hello entity from hello server first in order for hello [Replace][dotnet_TableOperation_Replace] operation toobe successful.</span></span> <span data-ttu-id="63de2-176">Иногда тем не менее, вы не знаете Если hello сущность существует на сервере hello и hello текущие значения, сохраненные в ней не имеют значения.</span><span class="sxs-lookup"><span data-stu-id="63de2-176">Sometimes, however, you don't know if hello entity exists on hello server and hello current values stored in it are irrelevant.</span></span> <span data-ttu-id="63de2-177">Обновление должно заменить их все.</span><span class="sxs-lookup"><span data-stu-id="63de2-177">Your update should overwrite them all.</span></span> <span data-ttu-id="63de2-178">tooaccomplish это, следует использовать [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] операции.</span><span class="sxs-lookup"><span data-stu-id="63de2-178">tooaccomplish this, you would use an [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation.</span></span> <span data-ttu-id="63de2-179">Эта операция вставляет сущность hello, если она не существует, или заменяет его, если это так, независимо от того, когда была произведена hello последнего обновления.</span><span class="sxs-lookup"><span data-stu-id="63de2-179">This operation inserts hello entity if it doesn't exist, or replaces it if it does, regardless of when hello last update was made.</span></span>

<span data-ttu-id="63de2-180">В следующем примере кода hello сущность «Клиент» для «Fred Джонс» создается и вставляется в таблицу «люди» hello.</span><span class="sxs-lookup"><span data-stu-id="63de2-180">In hello following code example, a customer entity for 'Fred Jones' is created and inserted into hello 'people' table.</span></span> <span data-ttu-id="63de2-181">Теперь воспользуемся hello [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] toosave операции сущность с hello одной секции (Jones) ключа и ключа строки server toohello (Fred), этот раз с разными значениями для hello PhoneNumber свойство.</span><span class="sxs-lookup"><span data-stu-id="63de2-181">Next, we use hello [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation toosave an entity with hello same partition key (Jones) and row key (Fred) toohello server, this time with a different value for hello PhoneNumber property.</span></span> <span data-ttu-id="63de2-182">Так как мы используем операцию [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], все значения свойства заменяются.</span><span class="sxs-lookup"><span data-stu-id="63de2-182">Because we use [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], all of its property values are replaced.</span></span> <span data-ttu-id="63de2-183">Тем не менее если сущность «Fred Джонс» еще не уже существует в таблице hello, он будет были вставлены.</span><span class="sxs-lookup"><span data-stu-id="63de2-183">However, if a 'Fred Jones' entity hadn't already existed in hello table, it would have been inserted.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a customer entity.
CustomerEntity customer3 = new CustomerEntity("Jones", "Fred");
customer3.Email = "Fred@contoso.com";
customer3.PhoneNumber = "425-555-0106";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer3);

// Execute hello operation.
table.Execute(insertOperation);

// Create another customer entity with hello same partition key and row key.
// We've already created a 'Fred Jones' entity and saved it toothe
// 'people' table, but here we're specifying a different value for the
// PhoneNumber property.
CustomerEntity customer4 = new CustomerEntity("Jones", "Fred");
customer4.Email = "Fred@contoso.com";
customer4.PhoneNumber = "425-555-0107";

// Create hello InsertOrReplace TableOperation.
TableOperation insertOrReplaceOperation = TableOperation.InsertOrReplace(customer4);

// Execute hello operation. Because a 'Fred Jones' entity already exists in the
// 'people' table, its property values will be overwritten by those in this
// CustomerEntity. If 'Fred Jones' didn't already exist, hello entity would be
// added toohello table.
table.Execute(insertOrReplaceOperation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="63de2-184">Запрос подмножества свойств сущности</span><span class="sxs-lookup"><span data-stu-id="63de2-184">Query a subset of entity properties</span></span>
<span data-ttu-id="63de2-185">Запрос таблицы можно получить только несколько свойств с сущностью, а не все свойства сущности hello.</span><span class="sxs-lookup"><span data-stu-id="63de2-185">A table query can retrieve just a few properties from an entity instead of all hello entity properties.</span></span> <span data-ttu-id="63de2-186">Этот метод, который называется "проекцией", снижает потребление пропускной способности и может повысить производительность запросов, особенно для крупных сущностей.</span><span class="sxs-lookup"><span data-stu-id="63de2-186">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="63de2-187">запрос Hello в hello, следующий код возвращает hello адреса электронной почты сущностей в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="63de2-187">hello query in hello following code returns only hello email addresses of entities in hello table.</span></span> <span data-ttu-id="63de2-188">Это делается с помощью запроса [DynamicTableEntity][dotnet_DynamicTableEntity], а также [EntityResolver][dotnet_EntityResolver].</span><span class="sxs-lookup"><span data-stu-id="63de2-188">This is done by using a query of [DynamicTableEntity][dotnet_DynamicTableEntity] and also [EntityResolver][dotnet_EntityResolver].</span></span> <span data-ttu-id="63de2-189">Дополнительные сведения о проекции в hello [Upsert введение и проекции запроса блога][blog_post_upsert].</span><span class="sxs-lookup"><span data-stu-id="63de2-189">You can learn more about projection in hello [Introducing Upsert and Query Projection blog post][blog_post_upsert].</span></span> <span data-ttu-id="63de2-190">Проекции не поддерживается эмулятором хранилища hello, поэтому этот код выполняется только в том случае, если вы используете учетную запись в службе таблиц hello.</span><span class="sxs-lookup"><span data-stu-id="63de2-190">Projection is not supported by hello storage emulator, so this code runs only when you're using an account in hello Table service.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Define hello query, and select only hello Email property.
TableQuery<DynamicTableEntity> projectionQuery = new TableQuery<DynamicTableEntity>().Select(new string[] { "Email" });

// Define an entity resolver toowork with hello entity after retrieval.
EntityResolver<string> resolver = (pk, rk, ts, props, etag) => props.ContainsKey("Email") ? props["Email"].StringValue : null;

foreach (string projectedEmail in table.ExecuteQuery(projectionQuery, resolver, null, null))
{
    Console.WriteLine(projectedEmail);
}
```

## <a name="delete-an-entity"></a><span data-ttu-id="63de2-191">Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="63de2-191">Delete an entity</span></span>
<span data-ttu-id="63de2-192">Можно легко удалить сущность, после его получения с помощью hello же шаблон, показанный для обновления сущности.</span><span class="sxs-lookup"><span data-stu-id="63de2-192">You can easily delete an entity after you have retrieved it by using hello same pattern shown for updating an entity.</span></span> <span data-ttu-id="63de2-193">Привет, следующий код извлекает и удаляет сущность «клиент».</span><span class="sxs-lookup"><span data-stu-id="63de2-193">hello following code retrieves and deletes a customer entity.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that expects a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign hello result tooa CustomerEntity.
CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

// Create hello Delete TableOperation.
if (deleteEntity != null)
{
    TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

    // Execute hello operation.
    table.Execute(deleteOperation);

    Console.WriteLine("Entity deleted.");
}
else
{
    Console.WriteLine("Could not retrieve hello entity.");
}
```

## <a name="delete-a-table"></a><span data-ttu-id="63de2-194">Удаление таблицы</span><span class="sxs-lookup"><span data-stu-id="63de2-194">Delete a table</span></span>
<span data-ttu-id="63de2-195">Наконец hello, следующий пример кода удаляет таблицу из учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="63de2-195">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="63de2-196">Таблицы, которая была удалена, будет недоступен toobe повторно создан для определенного периода времени после удаления hello.</span><span class="sxs-lookup"><span data-stu-id="63de2-196">A table that has been deleted will be unavailable toobe re-created for a period of time following hello deletion.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Delete hello table it if exists.
table.DeleteIfExists();
```

## <a name="retrieve-entities-in-pages-asynchronously"></a><span data-ttu-id="63de2-197">Асинхронное получение объектов со страниц</span><span class="sxs-lookup"><span data-stu-id="63de2-197">Retrieve entities in pages asynchronously</span></span>
<span data-ttu-id="63de2-198">Если вы читаете большого числа сущностей и предполагается tooprocess и отображения объектов, как их загрузки вместо ожидания их все tooreturn, можно получить сущностей с помощью сегментированных запроса.</span><span class="sxs-lookup"><span data-stu-id="63de2-198">If you are reading a large number of entities, and you want tooprocess/display entities as they are retrieved rather than waiting for them all tooreturn, you can retrieve entities by using a segmented query.</span></span> <span data-ttu-id="63de2-199">Этот пример показывает, как большой набор результатов tooreturn ожидаете tooreturn результатов на страницах с помощью шаблона hello Async-Await, чтобы во время выполнения не блокируется.</span><span class="sxs-lookup"><span data-stu-id="63de2-199">This example shows how tooreturn results in pages by using hello Async-Await pattern so that execution is not blocked while you're waiting for a large set of results tooreturn.</span></span> <span data-ttu-id="63de2-200">Дополнительные сведения об использовании hello шаблон Async-Await в .NET, см. в разделе [асинхронное программирование с использованием Async и Await (C# и Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span><span class="sxs-lookup"><span data-stu-id="63de2-200">For more details on using hello Async-Await pattern in .NET, see [Asynchronous programming with Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span></span>

```csharp
// Initialize a default TableQuery tooretrieve all hello entities in hello table.
TableQuery<CustomerEntity> tableQuery = new TableQuery<CustomerEntity>();

// Initialize hello continuation token toonull toostart from hello beginning of hello table.
TableContinuationToken continuationToken = null;

do
{
    // Retrieve a segment (up too1,000 entities).
    TableQuerySegment<CustomerEntity> tableQueryResult =
        await table.ExecuteQuerySegmentedAsync(tableQuery, continuationToken);

    // Assign hello new continuation token tootell hello service where to
    // continue on hello next iteration (or null if it has reached hello end).
    continuationToken = tableQueryResult.ContinuationToken;

    // Print hello number of rows retrieved.
    Console.WriteLine("Rows retrieved {0}", tableQueryResult.Results.Count);

// Loop until a null continuation token is received, indicating hello end of hello table.
} while(continuationToken != null);
```

## <a name="next-steps"></a><span data-ttu-id="63de2-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="63de2-201">Next steps</span></span>
<span data-ttu-id="63de2-202">Теперь, когда вы узнали основы hello хранилища таблицы, выполните эти ссылки toolearn о более сложных задач хранилища.</span><span class="sxs-lookup"><span data-stu-id="63de2-202">Now that you've learned hello basics of Table storage, follow these links toolearn about more complex storage tasks:</span></span>

* <span data-ttu-id="63de2-203">[Обозреватель хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) является бесплатной, отдельное приложение от Майкрософт, позволяющая toowork визуально с помощью данных из хранилища Azure в Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="63de2-203">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="63de2-204">Дополнительные примеры использования хранилища таблиц см. в статье [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/) (Приступая к работе с хранилищем таблиц Azure в .NET).</span><span class="sxs-lookup"><span data-stu-id="63de2-204">See more Table storage samples in [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span></span>
* <span data-ttu-id="63de2-205">Просмотрите hello таблицы службы справочной документации для получения подробной информации о доступных API-интерфейсы:</span><span class="sxs-lookup"><span data-stu-id="63de2-205">View hello Table service reference documentation for complete details about available APIs:</span></span>
* [<span data-ttu-id="63de2-206">Справочник по клиентской библиотеке хранилища для .NET</span><span class="sxs-lookup"><span data-stu-id="63de2-206">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [<span data-ttu-id="63de2-207">Справочник по REST API</span><span class="sxs-lookup"><span data-stu-id="63de2-207">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="63de2-208">Узнайте, как код hello toosimplify создавать toowork со службой хранилища Azure с помощью hello [SDK веб-заданий Azure](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="63de2-208">Learn how toosimplify hello code you write toowork with Azure Storage by using hello [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span></span>
* <span data-ttu-id="63de2-209">Просмотрите дополнительные toolearn функция руководства о дополнительных параметрах для хранения данных в Azure.</span><span class="sxs-lookup"><span data-stu-id="63de2-209">View more feature guides toolearn about additional options for storing data in Azure.</span></span>
* <span data-ttu-id="63de2-210">[Начало работы с хранилищем больших двоичных объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) toostore неструктурированных данных.</span><span class="sxs-lookup"><span data-stu-id="63de2-210">[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) toostore unstructured data.</span></span>
* <span data-ttu-id="63de2-211">[Подключение tooSQL базы данных с помощью .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore реляционных данных.</span><span class="sxs-lookup"><span data-stu-id="63de2-211">[Connect tooSQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore relational data.</span></span>

[Download and install hello Azure SDK for .NET]: /develop/net/
[Creating an Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx

[blog_post_upsert]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx

[dotnet_api_ref]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[dotnet_CloudTableClient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtableclient.aspx
[dotnet_CloudTable]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.aspx
[dotnet_CloudTable_Execute]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.execute.aspx
[dotnet_CloudTable_ExecuteBatch]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.executebatch.aspx
[dotnet_DynamicTableEntity]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.dynamictableentity.aspx
[dotnet_EntityResolver]: https://msdn.microsoft.com/library/jj733144.aspx
[dotnet_TableBatchOperation]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.aspx
[dotnet_TableBatchOperation_Insert]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.insert.aspx
[dotnet_TableEntity]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableentity.aspx
[dotnet_TableOperation]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.aspx
[dotnet_TableOperation_Insert]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.insert.aspx
[dotnet_TableOperation_InsertOrReplace]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.insertorreplace.aspx
[dotnet_TableOperation_Replace]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.replace.aspx
[dotnet_TableQuery]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablequery.aspx
[dotnet_TableResult]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableresult.aspx
[dotnet_TableResult_Result]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableresult.result.aspx
