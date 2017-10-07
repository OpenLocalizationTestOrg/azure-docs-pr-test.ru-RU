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
# <a name="get-started-with-azure-table-storage-using-net"></a>Приступая к работе с хранилищем таблиц Azure с помощью .NET
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

Хранилище таблиц Azure — это служба, хранит структурированные NoSQL хранить данные в облаке hello, предоставляя ключевой атрибут с schemaless конструктора. Так как хранилище таблиц schemaless, это легко tooadapt данных в качестве hello потребностей вашего приложения evolve. Доступ к данным хранилища tooTable быстрый и экономичный для многих типов приложений и обычно ниже стоимости традиционные SQL аналогичные объемами данных.

Гибкие наборы таблицы хранилища toostore и связанных данных как пользовательские данные можно использовать для веб-приложений, адресные книги, сведения об устройстве или другие виды метаданные, необходимые для службы. Можно хранить любое число сущностей в таблице, и учетную запись хранилища может содержать любое количество таблиц, копирование toohello пределу пропускной способности hello учетной записи хранилища.

### <a name="about-this-tutorial"></a>О данном учебнике
В этом учебнике показано как toouse hello [клиентская библиотека хранилища Azure для .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) в некоторые распространенные сценарии хранилища таблиц Azure. Эти сценарии представлены с помощью примеров C# для создания и удаления таблиц, а также вставки, обновления, удаления и запроса данных таблицы.

## <a name="prerequisites"></a>Предварительные требования

Вы должны hello следующие toocomplete этого учебника успешно:

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Клиентская библиотека хранилища Azure для .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Диспетчер конфигураций Azure для .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [Учетная запись хранения Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a>Другие примеры
Дополнительные примеры использования хранилища таблиц см. в статье [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/) (Приступая к работе с хранилищем таблиц Azure в .NET). Можно загрузить пример приложения hello и запустите его или просмотр кода hello в GitHub.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Добавление директив using
Добавьте следующее hello **с помощью** директивы toohello вверху hello `Program.cs` файла:

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-hello-connection-string"></a>Синтаксический анализ строки соединения hello
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-table-service-client"></a>Создание клиента службы таблиц hello
Hello [CloudTableClient] [ dotnet_CloudTableClient] класс позволяет tooretrieve таблиц и сущностей, хранящихся в хранилище таблиц. Вот клиента службы таблиц одним из способов toocreate hello.

```csharp
// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

Теперь все готово toowrite код, который считывает и записывает tooTable хранения данных.

## <a name="create-a-table"></a>Создание таблицы
В этом примере показано, как toocreate таблицы, если он еще не существует:

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

## <a name="add-an-entity-tooa-table"></a>Добавьте таблицу tooa сущности
Сущности сопоставляют tooC # объектов с помощью пользовательского класса, производного от [TableEntity][dotnet_TableEntity]. tooadd таблицу tooa сущности, создайте класс, определяющий hello свойства сущности. Hello следующий код определяет класс сущностей, который использует имя клиента hello как ключ строки hello и фамилию в качестве ключа секции hello. Вместе секции и ключом строки однозначно идентифицируют его в таблице hello. Ключи секций сущности с одинаковым ключом секции, которые могут запрашиваться быстрее, чем сущностей с различными приветствия, но с помощью различных разделов обеспечивает улучшенную масштабируемость параллельных операций. Toobe сущностей, которые хранятся в таблицах, должен иметь поддерживаемый тип, например производными hello [TableEntity] [ dotnet_TableEntity] класса. Свойства сущности, хотелось бы toostore в таблице должен быть открытым свойствам типа hello и поддерживает получение и задание значений. Кроме того, тип сущности *должен* предоставлять конструктор без параметров.

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

Таблица операциям, задействующим сущностей выполняются через hello [CloudTable] [ dotnet_CloudTable] объекта, созданного ранее в разделе «Создание таблицы» hello. Hello toobe операция выполняется представленного [TableOperation] [ dotnet_TableOperation] объекта. Hello следующем примере кода показано создание hello hello [CloudTable] [ dotnet_CloudTable] объекта и затем **CustomerEntity** объекта. операции hello tooprepare [TableOperation] [ dotnet_TableOperation] tooinsert hello сущность «клиент» создается объект в таблицу hello. Наконец, выполняется операция hello путем вызова [CloudTable][dotnet_CloudTable].[ Выполнение][dotnet_CloudTable_Execute].

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

## <a name="insert-a-batch-of-entities"></a>Вставка пакета сущностей
Вы можете вставить пакет сущностей в таблицу в одной операции записи. Некоторые другие примечания к пакетным операциям:

* Можно выполнять обновления, удаления и вставки в hello же одной пакетной операции.
* Одна пакетная операция могут включать копирование too100 сущностей.
* Все сущности в одной пакетной операции должен иметь hello же ключ секционирования.
* Хотя возможных tooperform запроса как пакетная операция, он должен быть hello только операции в пакете hello.

Hello примере кода создаются два объекта сущности и добавляются слишком[TableBatchOperation] [ dotnet_TableBatchOperation] с помощью hello [вставить] [ dotnet_TableBatchOperation_Insert] метод. Затем [CloudTable][dotnet_CloudTable].[ ExecuteBatch] [ dotnet_CloudTable_ExecuteBatch] вызывается операция tooexecute hello.

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

## <a name="retrieve-all-entities-in-a-partition"></a>Получение всех сущностей в разделе
таблицы для всех сущностей в секции, используйте tooquery [TableQuery] [ dotnet_TableQuery] объекта. Hello следующий пример кода задает фильтр для сущности, где ключ раздела hello 'Smith'. Этот пример выводит hello поля в каждой сущности в консоли toohello результаты запроса hello.

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

## <a name="retrieve-a-range-of-entities-in-a-partition"></a>Получение диапазона сущностей в разделе
Если вы не хотите tooquery все сущности в секции, можно указать диапазон, объединяя hello фильтра ключа секции с фильтром ключа строк. Hello следующий пример кода использует два tooget фильтры всех сущностей в разделе «Smith», где ключ строки hello (имя) начинается с буквы в алфавите hello перед «E», а затем выводит результаты запроса hello.

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

## <a name="retrieve-a-single-entity"></a>Извлечение одной сущности
Можно написать tooretrieve запроса конкретную сущность. Hello следующий код использует [TableOperation] [ dotnet_TableOperation] toospecify hello клиента 'Ben Smith'. Этот метод возвращает только одну сущность, а не коллекцией и hello возвращаемое значение в [TableResult][dotnet_TableResult].[ Результат] [ dotnet_TableResult_Result] — **CustomerEntity** объекта. Указание ключи секций и строк в запросе является hello самый быстрый способ tooretrieve одной сущности из службы таблиц hello.

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

## <a name="replace-an-entity"></a>Замена сущности
tooupdate сущности, получить его из службы таблиц hello, изменить объект сущности hello и сохранять изменения hello обратно toohello службы таблиц. Hello следующий код позволяет изменить номер телефона существующего клиента. Вместо вызова метода [Insert][dotnet_TableOperation_Insert] этот код использует операцию [Replace][dotnet_TableOperation_Replace]. [Замените] [ dotnet_TableOperation_Replace] причины hello полностью заменить на сервере hello toobe сущности, пока не изменят hello объекта на сервере hello, так как он был извлечен, в этом случае hello операция завершится ошибкой. Эта ошибка является tooprevent приложение случайно перезаписанный изменения внесены между hello извлечения и обновления приложения другим компонентом. Hello правильной обработки данного сбоя — tooretrieve hello сущность снова, внесенные изменения (если она все еще действует) и затем выполнять другую [заменить] [ dotnet_TableOperation_Replace] операции. Hello следующем разделе будет показано, как toooverride это поведение.

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

## <a name="insert-or-replace-an-entity"></a>Вставка или замена сущности
[Замените] [ dotnet_TableOperation_Replace] операции могут завершаться hello объекта было изменено, поскольку он был извлечен из сервера hello. Кроме того, необходимо получить hello объекта с сервера hello сначала в порядке для hello [заменить] [ dotnet_TableOperation_Replace] toobe операцию успешно. Иногда тем не менее, вы не знаете Если hello сущность существует на сервере hello и hello текущие значения, сохраненные в ней не имеют значения. Обновление должно заменить их все. tooaccomplish это, следует использовать [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] операции. Эта операция вставляет сущность hello, если она не существует, или заменяет его, если это так, независимо от того, когда была произведена hello последнего обновления.

В следующем примере кода hello сущность «Клиент» для «Fred Джонс» создается и вставляется в таблицу «люди» hello. Теперь воспользуемся hello [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] toosave операции сущность с hello одной секции (Jones) ключа и ключа строки server toohello (Fred), этот раз с разными значениями для hello PhoneNumber свойство. Так как мы используем операцию [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], все значения свойства заменяются. Тем не менее если сущность «Fred Джонс» еще не уже существует в таблице hello, он будет были вставлены.

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

## <a name="query-a-subset-of-entity-properties"></a>Запрос подмножества свойств сущности
Запрос таблицы можно получить только несколько свойств с сущностью, а не все свойства сущности hello. Этот метод, который называется "проекцией", снижает потребление пропускной способности и может повысить производительность запросов, особенно для крупных сущностей. запрос Hello в hello, следующий код возвращает hello адреса электронной почты сущностей в таблице hello. Это делается с помощью запроса [DynamicTableEntity][dotnet_DynamicTableEntity], а также [EntityResolver][dotnet_EntityResolver]. Дополнительные сведения о проекции в hello [Upsert введение и проекции запроса блога][blog_post_upsert]. Проекции не поддерживается эмулятором хранилища hello, поэтому этот код выполняется только в том случае, если вы используете учетную запись в службе таблиц hello.

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

## <a name="delete-an-entity"></a>Удаление сущности
Можно легко удалить сущность, после его получения с помощью hello же шаблон, показанный для обновления сущности. Привет, следующий код извлекает и удаляет сущность «клиент».

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

## <a name="delete-a-table"></a>Удаление таблицы
Наконец hello, следующий пример кода удаляет таблицу из учетной записи хранения. Таблицы, которая была удалена, будет недоступен toobe повторно создан для определенного периода времени после удаления hello.

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

## <a name="retrieve-entities-in-pages-asynchronously"></a>Асинхронное получение объектов со страниц
Если вы читаете большого числа сущностей и предполагается tooprocess и отображения объектов, как их загрузки вместо ожидания их все tooreturn, можно получить сущностей с помощью сегментированных запроса. Этот пример показывает, как большой набор результатов tooreturn ожидаете tooreturn результатов на страницах с помощью шаблона hello Async-Await, чтобы во время выполнения не блокируется. Дополнительные сведения об использовании hello шаблон Async-Await в .NET, см. в разделе [асинхронное программирование с использованием Async и Await (C# и Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).

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

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы узнали основы hello хранилища таблицы, выполните эти ссылки toolearn о более сложных задач хранилища.

* [Обозреватель хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) является бесплатной, отдельное приложение от Майкрософт, позволяющая toowork визуально с помощью данных из хранилища Azure в Windows, macOS и Linux.
* Дополнительные примеры использования хранилища таблиц см. в статье [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/) (Приступая к работе с хранилищем таблиц Azure в .NET).
* Просмотрите hello таблицы службы справочной документации для получения подробной информации о доступных API-интерфейсы:
* [Справочник по клиентской библиотеке хранилища для .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [Справочник по REST API](http://msdn.microsoft.com/library/azure/dd179355)
* Узнайте, как код hello toosimplify создавать toowork со службой хранилища Azure с помощью hello [SDK веб-заданий Azure](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)
* Просмотрите дополнительные toolearn функция руководства о дополнительных параметрах для хранения данных в Azure.
* [Начало работы с хранилищем больших двоичных объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) toostore неструктурированных данных.
* [Подключение tooSQL базы данных с помощью .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore реляционных данных.

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
