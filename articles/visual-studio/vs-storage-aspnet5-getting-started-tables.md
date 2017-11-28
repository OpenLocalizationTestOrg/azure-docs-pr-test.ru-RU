---
title: "Как приступить к работе с хранилищем таблиц и подключенными службами Visual Studio (ASP.NET Core) | Документация Майкрософт"
description: "Начало работы с хранилищем таблиц Azure в проекте ASP.NET Core в Visual Studio после подключения к учетной записи хранения с использованием подключенных служб Visual Studio."
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: c3c451d1-71ff-4222-a348-c41c98a02b85
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 8d05fe3ed9a5c66f186a930d4107162c1f322c05
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-get-started-with-azure-table-storage-and-visual-studio-connected-services"></a><span data-ttu-id="09ceb-103">Начало работы с табличным хранилищем Azure и подключенными службами Visual Studio</span><span class="sxs-lookup"><span data-stu-id="09ceb-103">How to get started with Azure Table storage and Visual Studio connected services</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="09ceb-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="09ceb-104">Overview</span></span>
<span data-ttu-id="09ceb-105">В этой статье описывается, как приступить к использованию хранилища таблиц Azure в Visual Studio после создания учетной записи хранения Azure или указания ссылки на нее в проекте ASP.NET Core с помощью диалогового окна **Добавление подключенных служб** в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="09ceb-105">This article describes how get started using Azure Table storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="09ceb-106">В службе хранилища таблиц Azure можно хранить большие объемы структурированных данных.</span><span class="sxs-lookup"><span data-stu-id="09ceb-106">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="09ceb-107">Эта служба — хранилище данных NoSQL, которое принимает вызовы внутри и снаружи облака Azure с проверкой подлинности.</span><span class="sxs-lookup"><span data-stu-id="09ceb-107">The service is a NoSQL data store that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="09ceb-108">Таблицы Azure идеально подходят для хранения нереляционных структурированных данных.</span><span class="sxs-lookup"><span data-stu-id="09ceb-108">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="09ceb-109">Операция **Добавить подключенные службы** устанавливает соответствующие пакеты NuGet для доступа к службе хранилища Azure в вашем проекте и добавляет строку подключения для учетной записи хранения в файлы конфигурации проекта.</span><span class="sxs-lookup"><span data-stu-id="09ceb-109">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="09ceb-110">Более общие сведения об использовании хранилища таблиц Azure см. в разделе [Приступая к работе с хранилищем таблиц Azure с помощью .NET](../storage/storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="09ceb-110">For more general information about using Azure Table storage, see [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="09ceb-111">Чтобы начать работу, сначала необходимо создать таблицу в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="09ceb-111">To get started, you first need to create a table in your storage account.</span></span> <span data-ttu-id="09ceb-112">Мы покажем, как создать таблицу Azure в коде.</span><span class="sxs-lookup"><span data-stu-id="09ceb-112">We'll show you how to create an Azure table in code.</span></span> <span data-ttu-id="09ceb-113">Кроме того, мы покажем, как выполнять базовые операции с таблицами и сущностями, например добавлять, изменять и читать сущности таблицы.</span><span class="sxs-lookup"><span data-stu-id="09ceb-113">We'll also show you how to perform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="09ceb-114">Примеры написаны на C\#, и в них используется библиотека клиента службы хранилища Azure для .NET.</span><span class="sxs-lookup"><span data-stu-id="09ceb-114">The samples are written in C\# code and use the Azure Storage Client Library for .NET.</span></span>

<span data-ttu-id="09ceb-115">**Примечание**. Некоторые интерфейсы API, которые выполняют вызовы к службе хранилища Azure в ASP.NET Core, являются асинхронными.</span><span class="sxs-lookup"><span data-stu-id="09ceb-115">**NOTE** - Some of the APIs that perform calls out to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="09ceb-116">Дополнительные сведения см. в статье [Asynchronous Programming with async and await (C#)](http://msdn.microsoft.com/library/hh191443.aspx) (Асинхронное программирование с использованием ключевых слов Async и Await (C#)).</span><span class="sxs-lookup"><span data-stu-id="09ceb-116">See [Asynchronous Programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="09ceb-117">В следующем примере кода предполагается, что используются асинхронные методы программирования.</span><span class="sxs-lookup"><span data-stu-id="09ceb-117">The code below assumes Async programming methods are being used.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="09ceb-118">Доступ к таблицам в коде</span><span class="sxs-lookup"><span data-stu-id="09ceb-118">Access tables in code</span></span>
<span data-ttu-id="09ceb-119">Для доступа к таблицам в проектах ASP.NET Core необходимо добавить следующие элементы во все файлы исходного кода C#, которые обращаются к хранилищу таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="09ceb-119">To access tables in ASP.NET Core projects, you need to include the following items to any C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="09ceb-120">Убедитесь, что объявления пространств имен в верхней части файла C# содержат указанные ниже выражения **using** .</span><span class="sxs-lookup"><span data-stu-id="09ceb-120">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="09ceb-121">Получите объект **CloudStorageAccount** , представляющий данные учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="09ceb-121">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="09ceb-122">Используйте следующий код, чтобы получить строку подключения и сведения об учетной записи хранения из конфигурации службы Azure.</span><span class="sxs-lookup"><span data-stu-id="09ceb-122">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    <span data-ttu-id="09ceb-123">**ПРИМЕЧАНИЕ.** Вставьте весь код, представленный выше, перед кодом в следующих примерах.</span><span class="sxs-lookup"><span data-stu-id="09ceb-123">**NOTE** - Use all of the above code in front of the code in the following samples.</span></span>
3. <span data-ttu-id="09ceb-124">Получите объект **CloudTableClient** , чтобы указать ссылку на объекты таблицы в своей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="09ceb-124">Get a **CloudTableClient** object to reference the table objects in your storage account.</span></span>  
   
        // Create the table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="09ceb-125">Получите объект ссылки **CloudTable** для указания ссылки на определенную таблицу и сущности.</span><span class="sxs-lookup"><span data-stu-id="09ceb-125">Get a **CloudTable** reference object to reference a specific table and entities.</span></span>
   
        // Get a reference to a table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="09ceb-126">Создание таблицы в коде</span><span class="sxs-lookup"><span data-stu-id="09ceb-126">Create a table in code</span></span>
<span data-ttu-id="09ceb-127">Чтобы создать таблицу Azure, просто добавьте вызов **CreateIfNotExistsAsync()**.</span><span class="sxs-lookup"><span data-stu-id="09ceb-127">To create the Azure table, just add a call to **CreateIfNotExistsAsync()**.</span></span>

    // Create the CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="09ceb-128">Добавление сущности в таблицу</span><span class="sxs-lookup"><span data-stu-id="09ceb-128">Add an entity to a table</span></span>
<span data-ttu-id="09ceb-129">Чтобы добавить сущность в таблицу, создайте класс, который определяет свойства сущности.</span><span class="sxs-lookup"><span data-stu-id="09ceb-129">To add an entity to a table you create a class that defines the properties of your entity.</span></span> <span data-ttu-id="09ceb-130">Следующий код определяет класс сущностей с именем **CustomerEntity** который использует имя клиента как ключ строки, а фамилию клиента — как ключ раздела.</span><span class="sxs-lookup"><span data-stu-id="09ceb-130">The following code defines an entity class called **CustomerEntity** that uses the customer's first name as the row key and last name as the partition key.</span></span>

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

<span data-ttu-id="09ceb-131">Операции с таблицами с участием сущностей выполняются с использованием объекта **CloudTable**. Его создание описано ранее в разделе "Доступ к таблицам в коде".</span><span class="sxs-lookup"><span data-stu-id="09ceb-131">Table operations involving entities are done using the **CloudTable** object you created earlier in "Access tables in code."</span></span> <span data-ttu-id="09ceb-132">Объект **TableOperation** представляет операции, которые необходимо выполнить.</span><span class="sxs-lookup"><span data-stu-id="09ceb-132">The **TableOperation** object represents the operation to be done.</span></span> <span data-ttu-id="09ceb-133">В следующем примере кода показано создание объектов **CloudTable** и **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="09ceb-133">The following code example shows how to create a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="09ceb-134">Чтобы подготовить операцию, создается **TableOperation** для вставки сущности customer в таблицу.</span><span class="sxs-lookup"><span data-stu-id="09ceb-134">To prepare the operation, a **TableOperation** is created to insert the customer entity into the table.</span></span> <span data-ttu-id="09ceb-135">Наконец, эта операция выполняется путем вызова CloudTable.ExecuteAsync.</span><span class="sxs-lookup"><span data-stu-id="09ceb-135">Finally, the operation is executed by calling CloudTable.ExecuteAsync.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create the TableOperation that inserts the customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute the insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="09ceb-136">Вставка пакета сущностей</span><span class="sxs-lookup"><span data-stu-id="09ceb-136">Insert a batch of entities</span></span>
<span data-ttu-id="09ceb-137">В таблицу можно вставить несколько сущностей с помощью одной операции записи.</span><span class="sxs-lookup"><span data-stu-id="09ceb-137">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="09ceb-138">Указанный ниже пример кода создает два объекта сущностей (Jeff Smith и Ben Smith), добавляет их в объект **TableBatchOperation** с помощью метода Insert и запускает операцию с помощью вызова **CloudTable.ExecuteBatchAsync**.</span><span class="sxs-lookup"><span data-stu-id="09ceb-138">The following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them to a **TableBatchOperation** object using the **Insert** method, and then starts the operation by calling CloudTable.ExecuteBatchAsync.</span></span>

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
    await peopleTable.ExecuteBatchAsync(batchOperation);

## <a name="get-all-of-the-entities-in-a-partition"></a><span data-ttu-id="09ceb-139">Получение всех сущностей в разделе</span><span class="sxs-lookup"><span data-stu-id="09ceb-139">Get all of the entities in a partition</span></span>
<span data-ttu-id="09ceb-140">Чтобы запросить все сущности из таблицы, используйте объект **TableQuery** .</span><span class="sxs-lookup"><span data-stu-id="09ceb-140">To query a table for all of the entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="09ceb-141">Следующий пример кода задает фильтр для сущностей с ключом раздела "Smith".</span><span class="sxs-lookup"><span data-stu-id="09ceb-141">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="09ceb-142">Этот пример выводит на консоль поля каждой сущности в результатах запроса.</span><span class="sxs-lookup"><span data-stu-id="09ceb-142">This example prints the fields of each entity in the query results to the console.</span></span>

    // Construct the query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

    // Print the fields for each customer.
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = await peopleTable.ExecuteQuerySegmentedAsync(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity entity in resultSegment.Results)
        {
            Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
            entity.Email, entity.PhoneNumber);
        }
    } while (token != null);

## <a name="get-a-single-entity"></a><span data-ttu-id="09ceb-143">Получение одной сущности</span><span class="sxs-lookup"><span data-stu-id="09ceb-143">Get a single entity</span></span>
<span data-ttu-id="09ceb-144">Можно написать запрос для получения отдельной сущности.</span><span class="sxs-lookup"><span data-stu-id="09ceb-144">You can write a query to get a single, specific entity.</span></span> <span data-ttu-id="09ceb-145">Следующий пример кода использует **TableOperation** для указания клиента "Ben Smith".</span><span class="sxs-lookup"><span data-stu-id="09ceb-145">The following code uses a **TableOperation** object to specify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="09ceb-146">Этот метод возвращает только одну сущность, а не коллекцию, и возвращаемое значение в **TableResult.Result** является объектом **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="09ceb-146">This method returns just one entity, rather than a collection, and the returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="09ceb-147">Указание ключа раздела и ключа строки в запросе — самый быстрый способ для получения одной сущности из службы **таблиц** .</span><span class="sxs-lookup"><span data-stu-id="09ceb-147">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print the phone number of the result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("The phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="09ceb-148">Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="09ceb-148">Delete an entity</span></span>
<span data-ttu-id="09ceb-149">После нахождения сущности ее можно удалить.</span><span class="sxs-lookup"><span data-stu-id="09ceb-149">You can delete an entity after you find it.</span></span> <span data-ttu-id="09ceb-150">В следующем примере код выполняет поиск сущности с именем "Ben Smith" и при нахождении удаляет ее.</span><span class="sxs-lookup"><span data-stu-id="09ceb-150">The following code looks for a customer entity named "Ben Smith" and if it finds it, it deletes it.</span></span>

    // Create a retrieve operation that expects a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the operation.
    TableResult retrievedResult = peopleTable.Execute(retrieveOperation);

    // Assign the result to a CustomerEntity object.
    CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

    // Create the Delete TableOperation and then execute it.
    if (deleteEntity != null)
    {
       TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

       // Execute the operation.
       await peopleTable.ExecuteAsync(deleteOperation);

       Console.WriteLine("Entity deleted.");
    }

    else
       Console.WriteLine("Couldn't delete the entity.");

## <a name="next-steps"></a><span data-ttu-id="09ceb-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="09ceb-151">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

