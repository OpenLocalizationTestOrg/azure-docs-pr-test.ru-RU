---
title: "Приступая к работе с хранилищем таблиц Azure с помощью .NET | Документация Майкрософт"
description: "Хранение структурированных данных в облаке в хранилище таблиц Azure (хранилище данных NoSQL)."
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
ms.openlocfilehash: ab77fe512d275a92da19bb5dc03da347922238a5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-table-storage-using-net"></a><span data-ttu-id="0b134-103">Приступая к работе с хранилищем таблиц Azure с помощью .NET</span><span class="sxs-lookup"><span data-stu-id="0b134-103">Get started with Azure Table storage using .NET</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="0b134-104">Хранилище таблиц Azure — это служба, которая хранит структурированные данные NoSQL в облаке, предоставляя хранилище ключей и атрибутов с бессхемной конструкцией.</span><span class="sxs-lookup"><span data-stu-id="0b134-104">Azure Table storage is a service that stores structured NoSQL data in the cloud, providing a key/attribute store with a schemaless design.</span></span> <span data-ttu-id="0b134-105">Такая конструкция хранилища таблиц позволяет легко адаптировать данные по мере расширения приложения.</span><span class="sxs-lookup"><span data-stu-id="0b134-105">Because Table storage is schemaless, it's easy to adapt your data as the needs of your application evolve.</span></span> <span data-ttu-id="0b134-106">Разным типам приложений может быть предоставлен быстрый и экономичный доступ к хранилищу таблиц. Такое хранилище обычно дешевле, чем традиционные хранилища SQL для похожих объемов данных.</span><span class="sxs-lookup"><span data-stu-id="0b134-106">Access to Table storage data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span></span>

<span data-ttu-id="0b134-107">Хранилище таблиц можно использовать для хранения гибких наборов данных, например пользовательских данных для веб-приложений, адресных книг, сведений об устройстве или метаданных любого другого типа, которые требуются вашей службе.</span><span class="sxs-lookup"><span data-stu-id="0b134-107">You can use Table storage to store flexible datasets like user data for web applications, address books, device information, or other types of metadata your service requires.</span></span> <span data-ttu-id="0b134-108">В таблице можно хранить любое количество сущностей, а учетная запись хранения может содержать любое количество таблиц в пределах емкости учетной записи.</span><span class="sxs-lookup"><span data-stu-id="0b134-108">You can store any number of entities in a table, and a storage account may contain any number of tables, up to the capacity limit of the storage account.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="0b134-109">О данном учебнике</span><span class="sxs-lookup"><span data-stu-id="0b134-109">About this tutorial</span></span>
<span data-ttu-id="0b134-110">В этом руководстве объясняется, как использовать [клиентскую библиотеку хранилища Azure для .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) в распространенных сценариях хранилища таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="0b134-110">This tutorial shows you how to use the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) in some common Azure Table storage scenarios.</span></span> <span data-ttu-id="0b134-111">Эти сценарии представлены с помощью примеров C# для создания и удаления таблиц, а также вставки, обновления, удаления и запроса данных таблицы.</span><span class="sxs-lookup"><span data-stu-id="0b134-111">These scenarios are presented using C# examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b134-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0b134-112">Prerequisites</span></span>

<span data-ttu-id="0b134-113">Для работы с этим руководством требуются следующие компоненты.</span><span class="sxs-lookup"><span data-stu-id="0b134-113">You need the following to complete this tutorial successfully:</span></span>

* [<span data-ttu-id="0b134-114">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0b134-114">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="0b134-115">Клиентская библиотека хранилища Azure для .NET</span><span class="sxs-lookup"><span data-stu-id="0b134-115">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="0b134-116">Диспетчер конфигураций Azure для .NET</span><span class="sxs-lookup"><span data-stu-id="0b134-116">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [<span data-ttu-id="0b134-117">Учетная запись хранения Azure</span><span class="sxs-lookup"><span data-stu-id="0b134-117">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="0b134-118">Другие примеры</span><span class="sxs-lookup"><span data-stu-id="0b134-118">More samples</span></span>
<span data-ttu-id="0b134-119">Дополнительные примеры использования хранилища таблиц см. в статье [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/) (Приступая к работе с хранилищем таблиц Azure в .NET).</span><span class="sxs-lookup"><span data-stu-id="0b134-119">For additional examples using Table storage, see [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/).</span></span> <span data-ttu-id="0b134-120">Вы можете скачать пример приложения и запустить его или просмотреть код на GitHub.</span><span class="sxs-lookup"><span data-stu-id="0b134-120">You can download the sample application and run it, or browse the code on GitHub.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="0b134-121">Добавление директив using</span><span class="sxs-lookup"><span data-stu-id="0b134-121">Add using directives</span></span>
<span data-ttu-id="0b134-122">Добавьте в верхнюю часть файла `Program.cs` следующие директивы **using**:</span><span class="sxs-lookup"><span data-stu-id="0b134-122">Add the following **using** directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="0b134-123">Анализ строки подключения</span><span class="sxs-lookup"><span data-stu-id="0b134-123">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-table-service-client"></a><span data-ttu-id="0b134-124">Создание клиента службы таблиц</span><span class="sxs-lookup"><span data-stu-id="0b134-124">Create the Table service client</span></span>
<span data-ttu-id="0b134-125">Класс [CloudTableClient][dotnet_CloudTableClient] позволяет получать таблицы и сущности, хранящиеся в хранилище таблиц.</span><span class="sxs-lookup"><span data-stu-id="0b134-125">The [CloudTableClient][dotnet_CloudTableClient] class enables you to retrieve tables and entities stored in Table storage.</span></span> <span data-ttu-id="0b134-126">Вот один из способов создать клиент службы таблиц.</span><span class="sxs-lookup"><span data-stu-id="0b134-126">Here's one way to create the Table service client:</span></span>

```csharp
// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

<span data-ttu-id="0b134-127">Теперь вы можете написать код, который считывает и записывает данные в хранилище таблиц.</span><span class="sxs-lookup"><span data-stu-id="0b134-127">Now you are ready to write code that reads data from and writes data to Table storage.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="0b134-128">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="0b134-128">Create a table</span></span>
<span data-ttu-id="0b134-129">В этом примере показано, как создать таблицу, если она не существует:</span><span class="sxs-lookup"><span data-stu-id="0b134-129">This example shows how to create a table if it does not already exist:</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Retrieve a reference to the table.
CloudTable table = tableClient.GetTableReference("people");

// Create the table if it doesn't exist.
table.CreateIfNotExists();
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="0b134-130">Добавление сущности в таблицу</span><span class="sxs-lookup"><span data-stu-id="0b134-130">Add an entity to a table</span></span>
<span data-ttu-id="0b134-131">Сущности сопоставляются с объектами C# с помощью настраиваемого класса, производного от [TableEntity][dotnet_TableEntity].</span><span class="sxs-lookup"><span data-stu-id="0b134-131">Entities map to C# objects by using a custom class derived from [TableEntity][dotnet_TableEntity].</span></span> <span data-ttu-id="0b134-132">Чтобы добавить сущность в таблицу, создайте класс, который определяет свойства сущности.</span><span class="sxs-lookup"><span data-stu-id="0b134-132">To add an entity to a table, create a class that defines the properties of your entity.</span></span> <span data-ttu-id="0b134-133">Следующий код определяет класс сущностей, который использует имя клиента как ключ строки, а фамилию клиента — как ключ раздела.</span><span class="sxs-lookup"><span data-stu-id="0b134-133">The following code defines an entity class that uses the customer's first name as the row key and last name as the partition key.</span></span> <span data-ttu-id="0b134-134">Вместе ключ раздела и ключ строки сущности уникальным образом идентифицируют сущность в таблице.</span><span class="sxs-lookup"><span data-stu-id="0b134-134">Together, an entity's partition and row key uniquely identify it in the table.</span></span> <span data-ttu-id="0b134-135">Сущности с одинаковым ключом раздела можно запрашивать быстрее, чем с разными ключами раздела, но использование различных ключей разделов обеспечивает более высокую масштабируемость параллельных операций.</span><span class="sxs-lookup"><span data-stu-id="0b134-135">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="0b134-136">Чтобы сущности могли храниться в таблицах, они должны быть поддерживаемого типа, например производными от класса [TableEntity][dotnet_TableEntity].</span><span class="sxs-lookup"><span data-stu-id="0b134-136">Entities to be stored in tables must be of a supported type, for example derived from the [TableEntity][dotnet_TableEntity] class.</span></span> <span data-ttu-id="0b134-137">Свойства сущности, которые вы хотите хранить в таблице, должны быть открытыми свойствами типа и поддерживать получение и настройку значений.</span><span class="sxs-lookup"><span data-stu-id="0b134-137">Entity properties you'd like to store in a table must be public properties of the type, and support both getting and setting of values.</span></span> <span data-ttu-id="0b134-138">Кроме того, тип сущности *должен* предоставлять конструктор без параметров.</span><span class="sxs-lookup"><span data-stu-id="0b134-138">Also, your entity type *must* expose a parameter-less constructor.</span></span>

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

<span data-ttu-id="0b134-139">Табличные операции, включающие сущности, выполняются с использованием объекта [CloudTable][dotnet_CloudTable], созданного ранее в разделе "Создание таблицы".</span><span class="sxs-lookup"><span data-stu-id="0b134-139">Table operations that involve entities are performed via the [CloudTable][dotnet_CloudTable] object that you created earlier in the "Create a table" section.</span></span> <span data-ttu-id="0b134-140">Выполняемая операция представляется объектом [TableOperation][dotnet_TableOperation].</span><span class="sxs-lookup"><span data-stu-id="0b134-140">The operation to be performed is represented by a [TableOperation][dotnet_TableOperation] object.</span></span> <span data-ttu-id="0b134-141">В следующем примере кода показано создание объекта [CloudTable][dotnet_CloudTable] и объекта **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="0b134-141">The following code example shows the creation of the [CloudTable][dotnet_CloudTable] object and then a **CustomerEntity** object.</span></span> <span data-ttu-id="0b134-142">Чтобы подготовить операцию, создается объект [TableOperation][dotnet_TableOperation] для вставки сущности customer в таблицу.</span><span class="sxs-lookup"><span data-stu-id="0b134-142">To prepare the operation, a [TableOperation][dotnet_TableOperation] object is created to insert the customer entity into the table.</span></span> <span data-ttu-id="0b134-143">Наконец, операция выполняется при вызове [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute].</span><span class="sxs-lookup"><span data-stu-id="0b134-143">Finally, the operation is executed by calling [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute].</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute the insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="0b134-144">Вставка пакета сущностей</span><span class="sxs-lookup"><span data-stu-id="0b134-144">Insert a batch of entities</span></span>
<span data-ttu-id="0b134-145">Вы можете вставить пакет сущностей в таблицу в одной операции записи.</span><span class="sxs-lookup"><span data-stu-id="0b134-145">You can insert a batch of entities into a table in one write operation.</span></span> <span data-ttu-id="0b134-146">Некоторые другие примечания к пакетным операциям:</span><span class="sxs-lookup"><span data-stu-id="0b134-146">Some other notes on batch operations:</span></span>

* <span data-ttu-id="0b134-147">Можно выполнять операции обновления, удаления и вставки в одной операции пакета.</span><span class="sxs-lookup"><span data-stu-id="0b134-147">You can perform updates, deletes, and inserts in the same single batch operation.</span></span>
* <span data-ttu-id="0b134-148">Одна пакетная операция может включать до 100 сущностей.</span><span class="sxs-lookup"><span data-stu-id="0b134-148">A single batch operation can include up to 100 entities.</span></span>
* <span data-ttu-id="0b134-149">У всех сущностей в одной пакетной операции должен быть одинаковый ключ раздела.</span><span class="sxs-lookup"><span data-stu-id="0b134-149">All entities in a single batch operation must have the same partition key.</span></span>
* <span data-ttu-id="0b134-150">Хотя запрос можно выполнить как пакетную операцию, он должен быть единственной операцией в пакете.</span><span class="sxs-lookup"><span data-stu-id="0b134-150">While it is possible to perform a query as a batch operation, it must be the only operation in the batch.</span></span>

<span data-ttu-id="0b134-151">В следующем примере кода создается два объекта сущности, которые добавляются в [TableBatchOperation][dotnet_TableBatchOperation] с помощью метода [Insert][dotnet_TableBatchOperation_Insert].</span><span class="sxs-lookup"><span data-stu-id="0b134-151">The following code example creates two entity objects and adds each to [TableBatchOperation][dotnet_TableBatchOperation] by using the [Insert][dotnet_TableBatchOperation_Insert] method.</span></span> <span data-ttu-id="0b134-152">Затем вызывается метод [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch] для выполнения операции.</span><span class="sxs-lookup"><span data-stu-id="0b134-152">Then, [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch] is called to execute the operation.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create the batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it to the table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it to the table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities to the batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute the batch operation.
table.ExecuteBatch(batchOperation);
```

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="0b134-153">Получение всех сущностей в разделе</span><span class="sxs-lookup"><span data-stu-id="0b134-153">Retrieve all entities in a partition</span></span>
<span data-ttu-id="0b134-154">Чтобы запросить таблицу для всех сущностей в разделе, используйте объект [TableQuery][dotnet_TableQuery].</span><span class="sxs-lookup"><span data-stu-id="0b134-154">To query a table for all entities in a partition, use a [TableQuery][dotnet_TableQuery] object.</span></span> <span data-ttu-id="0b134-155">Следующий пример кода задает фильтр для сущностей с ключом раздела Smith.</span><span class="sxs-lookup"><span data-stu-id="0b134-155">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="0b134-156">Этот пример выводит на консоль поля каждой сущности в результатах запроса.</span><span class="sxs-lookup"><span data-stu-id="0b134-156">This example prints the fields of each entity in the query results to the console.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Construct the query operation for all customer entities where PartitionKey="Smith".
TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

// Print the fields for each customer.
foreach (CustomerEntity entity in table.ExecuteQuery(query))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="0b134-157">Получение диапазона сущностей в разделе</span><span class="sxs-lookup"><span data-stu-id="0b134-157">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="0b134-158">Если вы не хотите запрашивать все сущности в разделе, можно указать диапазон, объединив фильтр ключа раздела с фильтром ключа строк.</span><span class="sxs-lookup"><span data-stu-id="0b134-158">If you don't want to query all entities in a partition, you can specify a range by combining the partition key filter with a row key filter.</span></span> <span data-ttu-id="0b134-159">В следующем примере кода используются два фильтра для получения всех сущностей в разделе Smith, где ключ строки (имя) начинается с буквы алфавита до "E", после чего результаты запроса выводятся в консоль.</span><span class="sxs-lookup"><span data-stu-id="0b134-159">The following code example uses two filters to get all entities in partition 'Smith' where the row key (first name) starts with a letter before 'E' in the alphabet, then prints the query results.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create the table query.
TableQuery<CustomerEntity> rangeQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "E")));

// Loop through the results, displaying information about the entity.
foreach (CustomerEntity entity in table.ExecuteQuery(rangeQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="0b134-160">Извлечение одной сущности</span><span class="sxs-lookup"><span data-stu-id="0b134-160">Retrieve a single entity</span></span>
<span data-ttu-id="0b134-161">Можно написать запрос для получения отдельной сущности.</span><span class="sxs-lookup"><span data-stu-id="0b134-161">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="0b134-162">В следующем примере кода с помощью объекта [TableOperation][dotnet_TableOperation] задается клиент Ben Smith.</span><span class="sxs-lookup"><span data-stu-id="0b134-162">The following code uses [TableOperation][dotnet_TableOperation] to specify the customer 'Ben Smith'.</span></span> <span data-ttu-id="0b134-163">Этот метод возвращает только одну сущность, а не коллекцию, а возвращаемое значение в [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result] является объектом **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="0b134-163">This method returns just one entity rather than a collection, and the returned value in [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result] is a **CustomerEntity** object.</span></span> <span data-ttu-id="0b134-164">Указание ключа раздела и ключа строки в запросе — самый быстрый способ извлечь одну сущность из службы таблиц.</span><span class="sxs-lookup"><span data-stu-id="0b134-164">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Print the phone number of the result.
if (retrievedResult.Result != null)
{
    Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
}
else
{
    Console.WriteLine("The phone number could not be retrieved.");
}
```

## <a name="replace-an-entity"></a><span data-ttu-id="0b134-165">Замена сущности</span><span class="sxs-lookup"><span data-stu-id="0b134-165">Replace an entity</span></span>
<span data-ttu-id="0b134-166">Чтобы обновить сущность, извлеките ее из службы таблиц, измените объект сущности и сохраните изменения в службе таблиц.</span><span class="sxs-lookup"><span data-stu-id="0b134-166">To update an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="0b134-167">Следующий код изменяет существующий номер телефона клиента.</span><span class="sxs-lookup"><span data-stu-id="0b134-167">The following code changes an existing customer's phone number.</span></span> <span data-ttu-id="0b134-168">Вместо вызова метода [Insert][dotnet_TableOperation_Insert] этот код использует операцию [Replace][dotnet_TableOperation_Replace].</span><span class="sxs-lookup"><span data-stu-id="0b134-168">Instead of calling [Insert][dotnet_TableOperation_Insert], this code uses [Replace][dotnet_TableOperation_Replace].</span></span> <span data-ttu-id="0b134-169">Операция [Replace][dotnet_TableOperation_Replace] полностью заменяет сущность на сервере, если только сущность на сервере не была изменена с момента извлечения. В таком случае операция не будет выполнена.</span><span class="sxs-lookup"><span data-stu-id="0b134-169">[Replace][dotnet_TableOperation_Replace] causes the entity to be fully replaced on the server, unless the entity on the server has changed since it was retrieved, in which case the operation will fail.</span></span> <span data-ttu-id="0b134-170">Это необходимо, чтобы приложение случайно не перезаписало изменения, внесенные с момента извлечения до обновления другим компонентом приложения.</span><span class="sxs-lookup"><span data-stu-id="0b134-170">This failure is to prevent your application from inadvertently overwriting a change made between the retrieval and update by another component of your application.</span></span> <span data-ttu-id="0b134-171">Правильный алгоритм обработки этой ошибки заключается в том, чтобы снова получить сущность, внести необходимые изменения (если это еще возможно), а затем выполнить еще одну операцию [Replace][dotnet_TableOperation_Replace].</span><span class="sxs-lookup"><span data-stu-id="0b134-171">The proper handling of this failure is to retrieve the entity again, make your changes (if still valid), and then perform another [Replace][dotnet_TableOperation_Replace] operation.</span></span> <span data-ttu-id="0b134-172">Ниже показано, как изменить это поведение.</span><span class="sxs-lookup"><span data-stu-id="0b134-172">The next section will show you how to override this behavior.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign the result to a CustomerEntity object.
CustomerEntity updateEntity = (CustomerEntity)retrievedResult.Result;

if (updateEntity != null)
{
    // Change the phone number.
    updateEntity.PhoneNumber = "425-555-0105";

    // Create the Replace TableOperation.
    TableOperation updateOperation = TableOperation.Replace(updateEntity);

    // Execute the operation.
    table.Execute(updateOperation);

    Console.WriteLine("Entity updated.");
}
else
{
    Console.WriteLine("Entity could not be retrieved.");
}
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="0b134-173">Вставка или замена сущности</span><span class="sxs-lookup"><span data-stu-id="0b134-173">Insert-or-replace an entity</span></span>
<span data-ttu-id="0b134-174">Операции [Replace][dotnet_TableOperation_Replace] завершаются ошибкой, если сущность изменена с момента получения с сервера.</span><span class="sxs-lookup"><span data-stu-id="0b134-174">[Replace][dotnet_TableOperation_Replace] operations will fail if the entity has been changed since it was retrieved from the server.</span></span> <span data-ttu-id="0b134-175">Более того, для успешного выполнения операции [Replace][dotnet_TableOperation_Replace] сначала нужно получить сущность с сервера.</span><span class="sxs-lookup"><span data-stu-id="0b134-175">Furthermore, you must retrieve the entity from the server first in order for the [Replace][dotnet_TableOperation_Replace] operation to be successful.</span></span> <span data-ttu-id="0b134-176">Тем не менее иногда вы не знаете, существует ли сущность на сервере и являются ли текущие значения, хранящиеся на нем, актуальными.</span><span class="sxs-lookup"><span data-stu-id="0b134-176">Sometimes, however, you don't know if the entity exists on the server and the current values stored in it are irrelevant.</span></span> <span data-ttu-id="0b134-177">Обновление должно заменить их все.</span><span class="sxs-lookup"><span data-stu-id="0b134-177">Your update should overwrite them all.</span></span> <span data-ttu-id="0b134-178">Для выполнения этой задачи необходимо использовать операцию [InsertOrReplace][dotnet_TableOperation_InsertOrReplace].</span><span class="sxs-lookup"><span data-stu-id="0b134-178">To accomplish this, you would use an [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation.</span></span> <span data-ttu-id="0b134-179">Эта операция вставляет сущность, если она не существует, или заменяет ее, если она существует, независимо от того, когда было выполнено последнее обновление.</span><span class="sxs-lookup"><span data-stu-id="0b134-179">This operation inserts the entity if it doesn't exist, or replaces it if it does, regardless of when the last update was made.</span></span>

<span data-ttu-id="0b134-180">В следующем примере кода сущность клиента для Fred Jones создается и вставляется в таблицу people.</span><span class="sxs-lookup"><span data-stu-id="0b134-180">In the following code example, a customer entity for 'Fred Jones' is created and inserted into the 'people' table.</span></span> <span data-ttu-id="0b134-181">Далее мы используем операцию [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] для сохранения сущности с одинаковым ключом раздела (Jones) и ключом строки (Fred) на сервере. На этот раз мы используем ее с другим значением свойства PhoneNumber.</span><span class="sxs-lookup"><span data-stu-id="0b134-181">Next, we use the [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation to save an entity with the same partition key (Jones) and row key (Fred) to the server, this time with a different value for the PhoneNumber property.</span></span> <span data-ttu-id="0b134-182">Так как мы используем операцию [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], все значения свойства заменяются.</span><span class="sxs-lookup"><span data-stu-id="0b134-182">Because we use [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], all of its property values are replaced.</span></span> <span data-ttu-id="0b134-183">Но если сущности Fred Jones еще нет в таблице, ее нужно вставить.</span><span class="sxs-lookup"><span data-stu-id="0b134-183">However, if a 'Fred Jones' entity hadn't already existed in the table, it would have been inserted.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a customer entity.
CustomerEntity customer3 = new CustomerEntity("Jones", "Fred");
customer3.Email = "Fred@contoso.com";
customer3.PhoneNumber = "425-555-0106";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer3);

// Execute the operation.
table.Execute(insertOperation);

// Create another customer entity with the same partition key and row key.
// We've already created a 'Fred Jones' entity and saved it to the
// 'people' table, but here we're specifying a different value for the
// PhoneNumber property.
CustomerEntity customer4 = new CustomerEntity("Jones", "Fred");
customer4.Email = "Fred@contoso.com";
customer4.PhoneNumber = "425-555-0107";

// Create the InsertOrReplace TableOperation.
TableOperation insertOrReplaceOperation = TableOperation.InsertOrReplace(customer4);

// Execute the operation. Because a 'Fred Jones' entity already exists in the
// 'people' table, its property values will be overwritten by those in this
// CustomerEntity. If 'Fred Jones' didn't already exist, the entity would be
// added to the table.
table.Execute(insertOrReplaceOperation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="0b134-184">Запрос подмножества свойств сущности</span><span class="sxs-lookup"><span data-stu-id="0b134-184">Query a subset of entity properties</span></span>
<span data-ttu-id="0b134-185">Запрос к таблице может получить лишь несколько свойств сущности, а не все свойства.</span><span class="sxs-lookup"><span data-stu-id="0b134-185">A table query can retrieve just a few properties from an entity instead of all the entity properties.</span></span> <span data-ttu-id="0b134-186">Этот метод, который называется "проекцией", снижает потребление пропускной способности и может повысить производительность запросов, особенно для крупных сущностей.</span><span class="sxs-lookup"><span data-stu-id="0b134-186">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="0b134-187">Запрос в следующем коде возвращает только электронные адреса сущностей в таблице.</span><span class="sxs-lookup"><span data-stu-id="0b134-187">The query in the following code returns only the email addresses of entities in the table.</span></span> <span data-ttu-id="0b134-188">Это делается с помощью запроса [DynamicTableEntity][dotnet_DynamicTableEntity], а также [EntityResolver][dotnet_EntityResolver].</span><span class="sxs-lookup"><span data-stu-id="0b134-188">This is done by using a query of [DynamicTableEntity][dotnet_DynamicTableEntity] and also [EntityResolver][dotnet_EntityResolver].</span></span> <span data-ttu-id="0b134-189">Дополнительные сведения о проекции см. в записи блога [Windows Azure Tables: Introducing Upsert and Query Projection][blog_post_upsert] (Таблицы Microsoft Azure: введение в Upsert и проекции в запросах).</span><span class="sxs-lookup"><span data-stu-id="0b134-189">You can learn more about projection in the [Introducing Upsert and Query Projection blog post][blog_post_upsert].</span></span> <span data-ttu-id="0b134-190">Проекция не поддерживается в эмуляторе хранения, поэтому этот код выполняется только при использовании учетной записи хранения в службе таблиц.</span><span class="sxs-lookup"><span data-stu-id="0b134-190">Projection is not supported by the storage emulator, so this code runs only when you're using an account in the Table service.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Define the query, and select only the Email property.
TableQuery<DynamicTableEntity> projectionQuery = new TableQuery<DynamicTableEntity>().Select(new string[] { "Email" });

// Define an entity resolver to work with the entity after retrieval.
EntityResolver<string> resolver = (pk, rk, ts, props, etag) => props.ContainsKey("Email") ? props["Email"].StringValue : null;

foreach (string projectedEmail in table.ExecuteQuery(projectionQuery, resolver, null, null))
{
    Console.WriteLine(projectedEmail);
}
```

## <a name="delete-an-entity"></a><span data-ttu-id="0b134-191">Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="0b134-191">Delete an entity</span></span>
<span data-ttu-id="0b134-192">Сущность можно легко удалить после ее получения с использованием того же шаблона, что и для обновления сущностей.</span><span class="sxs-lookup"><span data-stu-id="0b134-192">You can easily delete an entity after you have retrieved it by using the same pattern shown for updating an entity.</span></span> <span data-ttu-id="0b134-193">Следующий код извлекает и удаляет сущность клиента.</span><span class="sxs-lookup"><span data-stu-id="0b134-193">The following code retrieves and deletes a customer entity.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that expects a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign the result to a CustomerEntity.
CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

// Create the Delete TableOperation.
if (deleteEntity != null)
{
    TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

    // Execute the operation.
    table.Execute(deleteOperation);

    Console.WriteLine("Entity deleted.");
}
else
{
    Console.WriteLine("Could not retrieve the entity.");
}
```

## <a name="delete-a-table"></a><span data-ttu-id="0b134-194">Удаление таблицы</span><span class="sxs-lookup"><span data-stu-id="0b134-194">Delete a table</span></span>
<span data-ttu-id="0b134-195">Наконец, следующий пример кода удаляет таблицу из учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="0b134-195">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="0b134-196">Удаленную таблицу нельзя воссоздать в течение определенного времени после удаления.</span><span class="sxs-lookup"><span data-stu-id="0b134-196">A table that has been deleted will be unavailable to be re-created for a period of time following the deletion.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Delete the table it if exists.
table.DeleteIfExists();
```

## <a name="retrieve-entities-in-pages-asynchronously"></a><span data-ttu-id="0b134-197">Асинхронное получение объектов со страниц</span><span class="sxs-lookup"><span data-stu-id="0b134-197">Retrieve entities in pages asynchronously</span></span>
<span data-ttu-id="0b134-198">Если необходимо считать большое количество объектов, обрабатывая или отображая их по мере получения (до завершения всей операции), для их получения можно использовать сегментированный запрос.</span><span class="sxs-lookup"><span data-stu-id="0b134-198">If you are reading a large number of entities, and you want to process/display entities as they are retrieved rather than waiting for them all to return, you can retrieve entities by using a segmented query.</span></span> <span data-ttu-id="0b134-199">В этом примере объясняется, как расположить запрошенные результаты на странице с помощью алгоритма Async-Await для того, чтобы не блокировать выполнение задачи ожиданием большого объема возвращаемых данных.</span><span class="sxs-lookup"><span data-stu-id="0b134-199">This example shows how to return results in pages by using the Async-Await pattern so that execution is not blocked while you're waiting for a large set of results to return.</span></span> <span data-ttu-id="0b134-200">Дополнительные сведения об использовании алгоритма Async-Await в .NET см. в статье [Асинхронное программирование с использованием ключевых слов Async и Await (C# и Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span><span class="sxs-lookup"><span data-stu-id="0b134-200">For more details on using the Async-Await pattern in .NET, see [Asynchronous programming with Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span></span>

```csharp
// Initialize a default TableQuery to retrieve all the entities in the table.
TableQuery<CustomerEntity> tableQuery = new TableQuery<CustomerEntity>();

// Initialize the continuation token to null to start from the beginning of the table.
TableContinuationToken continuationToken = null;

do
{
    // Retrieve a segment (up to 1,000 entities).
    TableQuerySegment<CustomerEntity> tableQueryResult =
        await table.ExecuteQuerySegmentedAsync(tableQuery, continuationToken);

    // Assign the new continuation token to tell the service where to
    // continue on the next iteration (or null if it has reached the end).
    continuationToken = tableQueryResult.ContinuationToken;

    // Print the number of rows retrieved.
    Console.WriteLine("Rows retrieved {0}", tableQueryResult.Results.Count);

// Loop until a null continuation token is received, indicating the end of the table.
} while(continuationToken != null);
```

## <a name="next-steps"></a><span data-ttu-id="0b134-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0b134-201">Next steps</span></span>
<span data-ttu-id="0b134-202">Вы изучили основные сведения о табличном хранилище. Дополнительные сведения о более сложных задачах по использованию хранилища можно найти по следующим ссылкам.</span><span class="sxs-lookup"><span data-stu-id="0b134-202">Now that you've learned the basics of Table storage, follow these links to learn about more complex storage tasks:</span></span>

* <span data-ttu-id="0b134-203">[Обозреватель хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) — это бесплатное автономное приложение от корпорации Майкрософт, позволяющее визуализировать данные из службы хранилища Azure на платформе Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="0b134-203">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="0b134-204">Дополнительные примеры использования хранилища таблиц см. в статье [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/) (Приступая к работе с хранилищем таблиц Azure в .NET).</span><span class="sxs-lookup"><span data-stu-id="0b134-204">See more Table storage samples in [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span></span>
* <span data-ttu-id="0b134-205">Дополнительные сведения о доступных API-интерфейсах см. в справочной документации по службе таблиц:</span><span class="sxs-lookup"><span data-stu-id="0b134-205">View the Table service reference documentation for complete details about available APIs:</span></span>
* [<span data-ttu-id="0b134-206">Справочник по клиентской библиотеке хранилища для .NET</span><span class="sxs-lookup"><span data-stu-id="0b134-206">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [<span data-ttu-id="0b134-207">Справочник по REST API</span><span class="sxs-lookup"><span data-stu-id="0b134-207">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="0b134-208">Узнайте, как упростить код, предназначенный для работы со службой хранилища Azure, с помощью [пакета SDK для веб-заданий Azure](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="0b134-208">Learn how to simplify the code you write to work with Azure Storage by using the [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span></span>
* <span data-ttu-id="0b134-209">Просмотрите дополнительные руководства, чтобы изучить дополнительные возможности хранения данных в Azure.</span><span class="sxs-lookup"><span data-stu-id="0b134-209">View more feature guides to learn about additional options for storing data in Azure.</span></span>
* <span data-ttu-id="0b134-210">[Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) .</span><span class="sxs-lookup"><span data-stu-id="0b134-210">[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) to store unstructured data.</span></span>
* <span data-ttu-id="0b134-211">Информацию о хранении реляционных данных см. в статье [Подключение к базе данных SQL с помощью .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md).</span><span class="sxs-lookup"><span data-stu-id="0b134-211">[Connect to SQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) to store relational data.</span></span>

[Download and install the Azure SDK for .NET]: /develop/net/
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
