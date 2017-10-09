---
title: "aaaHow tooget работы с Visual Studio и хранилище таблиц подключенных служб (ASP.NET Core) | Документы Microsoft"
description: "Как tooget к работе с хранилищем таблиц Azure в проекте ASP.NET Core в Visual Studio после подключения tooa учетной записи хранилища с помощью Visual Studio подключенные службы"
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
ms.openlocfilehash: e3eb3f3e65456108dd3cde7e3e470f98ba456e35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-started-with-azure-table-storage-and-visual-studio-connected-services"></a><span data-ttu-id="18f43-103">Как tooget работу с Visual Studio и хранилище таблиц Azure подключенных служб</span><span class="sxs-lookup"><span data-stu-id="18f43-103">How tooget started with Azure Table storage and Visual Studio connected services</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="18f43-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="18f43-104">Overview</span></span>
<span data-ttu-id="18f43-105">В этой статье описывается, как получить работы с использованием таблиц Azure hello хранилища в Visual Studio после создания или ссылка на учетную запись хранилища Azure в проекте ASP.NET Core с помощью Visual Studio **Добавление подключенных служб** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="18f43-105">This article describes how get started using Azure Table storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="18f43-106">Hello службы хранилища таблиц Azure позволяет toostore больших объемов структурированных данных.</span><span class="sxs-lookup"><span data-stu-id="18f43-106">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="18f43-107">Служба Hello является хранилищем данных NoSQL, принимающий вызовам c аутентификацией внутри и вне hello облако Azure.</span><span class="sxs-lookup"><span data-stu-id="18f43-107">hello service is a NoSQL data store that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="18f43-108">Таблицы Azure идеально подходят для хранения нереляционных структурированных данных.</span><span class="sxs-lookup"><span data-stu-id="18f43-108">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="18f43-109">Hello **Добавление подключенных служб** операция устанавливает пакеты tooaccess hello соответствующие NuGet хранилища Azure в проекте и добавляет строку hello подключения для hello учетную запись хранилища, tooyour файлы конфигурации проекта.</span><span class="sxs-lookup"><span data-stu-id="18f43-109">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="18f43-110">Более общие сведения об использовании хранилища таблиц Azure см. в разделе [Приступая к работе с хранилищем таблиц Azure с помощью .NET](../storage/storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="18f43-110">For more general information about using Azure Table storage, see [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="18f43-111">tooget работы, необходимо сначала toocreate таблицу в учетной записи.</span><span class="sxs-lookup"><span data-stu-id="18f43-111">tooget started, you first need toocreate a table in your storage account.</span></span> <span data-ttu-id="18f43-112">Мы покажем, как toocreate Azure таблицу в коде.</span><span class="sxs-lookup"><span data-stu-id="18f43-112">We'll show you how toocreate an Azure table in code.</span></span> <span data-ttu-id="18f43-113">Мы также покажем, как базовая таблица tooperform и операции с сущностями, например добавление, изменение, чтение и чтение таблицу сущностей.</span><span class="sxs-lookup"><span data-stu-id="18f43-113">We'll also show you how tooperform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="18f43-114">Hello примеры на языке C\# кода и использовать hello клиентская библиотека хранилища Azure для .NET.</span><span class="sxs-lookup"><span data-stu-id="18f43-114">hello samples are written in C\# code and use hello Azure Storage Client Library for .NET.</span></span>

<span data-ttu-id="18f43-115">**Примечание** -некоторые интерфейсы API, которые выполняют вызовы out tooAzure хранилища в ASP.NET Core hello являются асинхронными.</span><span class="sxs-lookup"><span data-stu-id="18f43-115">**NOTE** - Some of hello APIs that perform calls out tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="18f43-116">Дополнительные сведения см. в статье [Asynchronous Programming with async and await (C#)](http://msdn.microsoft.com/library/hh191443.aspx) (Асинхронное программирование с использованием ключевых слов Async и Await (C#)).</span><span class="sxs-lookup"><span data-stu-id="18f43-116">See [Asynchronous Programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="18f43-117">Приведенный ниже код Hello предполагается, что используются асинхронные методы программирования.</span><span class="sxs-lookup"><span data-stu-id="18f43-117">hello code below assumes Async programming methods are being used.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="18f43-118">Доступ к таблицам в коде</span><span class="sxs-lookup"><span data-stu-id="18f43-118">Access tables in code</span></span>
<span data-ttu-id="18f43-119">tooaccess таблицами в проектах ASP.NET Core, необходимо tooinclude hello следующие элементы tooany C# исходные файлы, доступ к хранилищу таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="18f43-119">tooaccess tables in ASP.NET Core projects, you need tooinclude hello following items tooany C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="18f43-120">Убедитесь, что объявления пространств имен hello hello верхней части файла hello C# включить эти **с помощью** инструкции.</span><span class="sxs-lookup"><span data-stu-id="18f43-120">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="18f43-121">Получите объект **CloudStorageAccount** , представляющий данные учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="18f43-121">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="18f43-122">Hello используйте следующий код tooget hello хранения строки соединения и сведения об учетной записи хранилища из конфигурации службы Azure hello.</span><span class="sxs-lookup"><span data-stu-id="18f43-122">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    <span data-ttu-id="18f43-123">**Примечание** -используются hello над кодом перед кода hello из hello следующие примеры.</span><span class="sxs-lookup"><span data-stu-id="18f43-123">**NOTE** - Use all of hello above code in front of hello code in hello following samples.</span></span>
3. <span data-ttu-id="18f43-124">Получить **CloudTableClient** объектов tooreference hello таблицы в учетной записи.</span><span class="sxs-lookup"><span data-stu-id="18f43-124">Get a **CloudTableClient** object tooreference hello table objects in your storage account.</span></span>  
   
        // Create hello table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="18f43-125">Получить **CloudTable** ссылки на объект tooreference определенной таблицы и сущности.</span><span class="sxs-lookup"><span data-stu-id="18f43-125">Get a **CloudTable** reference object tooreference a specific table and entities.</span></span>
   
        // Get a reference tooa table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="18f43-126">Создание таблицы в коде</span><span class="sxs-lookup"><span data-stu-id="18f43-126">Create a table in code</span></span>
<span data-ttu-id="18f43-127">hello toocreate таблицы Azure, просто добавьте вызов слишком**CreateIfNotExistsAsync()**.</span><span class="sxs-lookup"><span data-stu-id="18f43-127">toocreate hello Azure table, just add a call too**CreateIfNotExistsAsync()**.</span></span>

    // Create hello CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="18f43-128">Добавьте таблицу tooa сущности</span><span class="sxs-lookup"><span data-stu-id="18f43-128">Add an entity tooa table</span></span>
<span data-ttu-id="18f43-129">tooadd tooa сущности таблицы, необходимо создать класс, который определяет hello свойства сущности.</span><span class="sxs-lookup"><span data-stu-id="18f43-129">tooadd an entity tooa table you create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="18f43-130">Hello следующий код определяет класс сущности с именем **CustomerEntity** , использует hello имени клиента в качестве ключа строку hello и фамилию в качестве ключа секции hello.</span><span class="sxs-lookup"><span data-stu-id="18f43-130">hello following code defines an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and last name as hello partition key.</span></span>

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

<span data-ttu-id="18f43-131">Операции с таблицей с использованием сущностей выполняются с помощью hello **CloudTable** объекта, созданного ранее в «Таблицы доступ в коде».</span><span class="sxs-lookup"><span data-stu-id="18f43-131">Table operations involving entities are done using hello **CloudTable** object you created earlier in "Access tables in code."</span></span> <span data-ttu-id="18f43-132">Hello **TableOperation** toobe операции hello сделать представляет объект.</span><span class="sxs-lookup"><span data-stu-id="18f43-132">hello **TableOperation** object represents hello operation toobe done.</span></span> <span data-ttu-id="18f43-133">Здравствуйте, следуя примере кода показано, как toocreate **CloudTable** объекта и **CustomerEntity** объекта.</span><span class="sxs-lookup"><span data-stu-id="18f43-133">hello following code example shows how toocreate a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="18f43-134">операции hello tooprepare **TableOperation** создается сущность customer tooinsert hello в таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="18f43-134">tooprepare hello operation, a **TableOperation** is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="18f43-135">Наконец hello операция выполняется путем вызова CloudTable.ExecuteAsync.</span><span class="sxs-lookup"><span data-stu-id="18f43-135">Finally, hello operation is executed by calling CloudTable.ExecuteAsync.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="18f43-136">Вставка пакета сущностей</span><span class="sxs-lookup"><span data-stu-id="18f43-136">Insert a batch of entities</span></span>
<span data-ttu-id="18f43-137">В таблицу можно вставить несколько сущностей с помощью одной операции записи.</span><span class="sxs-lookup"><span data-stu-id="18f43-137">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="18f43-138">Hello следующем примере кода создаются два объекта сущности («Джефф Smith» и «Ben Smith»), добавляет их tooa **TableBatchOperation** объекта с помощью hello **вставить** метода, а затем запускает операцию hello вызов CloudTable.ExecuteBatchAsync.</span><span class="sxs-lookup"><span data-stu-id="18f43-138">hello following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them tooa **TableBatchOperation** object using hello **Insert** method, and then starts hello operation by calling CloudTable.ExecuteBatchAsync.</span></span>

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
    await peopleTable.ExecuteBatchAsync(batchOperation);

## <a name="get-all-of-hello-entities-in-a-partition"></a><span data-ttu-id="18f43-139">Получить все сущности hello в секции</span><span class="sxs-lookup"><span data-stu-id="18f43-139">Get all of hello entities in a partition</span></span>
<span data-ttu-id="18f43-140">таблицы для всех сущностей hello в секции, используйте tooquery **TableQuery** объекта.</span><span class="sxs-lookup"><span data-stu-id="18f43-140">tooquery a table for all of hello entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="18f43-141">Hello следующий пример кода задает фильтр для сущности, где ключ раздела hello 'Smith'.</span><span class="sxs-lookup"><span data-stu-id="18f43-141">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="18f43-142">Этот пример выводит hello поля в каждой сущности в консоли toohello результаты запроса hello.</span><span class="sxs-lookup"><span data-stu-id="18f43-142">This example prints hello fields of each entity in hello query results toohello console.</span></span>

    // Construct hello query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

    // Print hello fields for each customer.
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

## <a name="get-a-single-entity"></a><span data-ttu-id="18f43-143">Получение одной сущности</span><span class="sxs-lookup"><span data-stu-id="18f43-143">Get a single entity</span></span>
<span data-ttu-id="18f43-144">Можно написать tooget запроса конкретную сущность.</span><span class="sxs-lookup"><span data-stu-id="18f43-144">You can write a query tooget a single, specific entity.</span></span> <span data-ttu-id="18f43-145">Hello следующий код использует **TableOperation** объекта toospecify клиент с именем 'Ben Smith'.</span><span class="sxs-lookup"><span data-stu-id="18f43-145">hello following code uses a **TableOperation** object toospecify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="18f43-146">Этот метод возвращает только одну сущность, а не коллекцию и hello возвращаемое значение в **TableResult.Result** — **CustomerEntity** объекта.</span><span class="sxs-lookup"><span data-stu-id="18f43-146">This method returns just one entity, rather than a collection, and hello returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="18f43-147">Указание ключи секций и строк в запросе является hello самый быстрый способ tooretrieve одной сущности из hello **таблицы** службы.</span><span class="sxs-lookup"><span data-stu-id="18f43-147">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="18f43-148">Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="18f43-148">Delete an entity</span></span>
<span data-ttu-id="18f43-149">После нахождения сущности ее можно удалить.</span><span class="sxs-lookup"><span data-stu-id="18f43-149">You can delete an entity after you find it.</span></span> <span data-ttu-id="18f43-150">Hello следующий код ищет сущность «клиент» с именем «Ben Smith» и если она его находит, она удаляет.</span><span class="sxs-lookup"><span data-stu-id="18f43-150">hello following code looks for a customer entity named "Ben Smith" and if it finds it, it deletes it.</span></span>

    // Create a retrieve operation that expects a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello operation.
    TableResult retrievedResult = peopleTable.Execute(retrieveOperation);

    // Assign hello result tooa CustomerEntity object.
    CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

    // Create hello Delete TableOperation and then execute it.
    if (deleteEntity != null)
    {
       TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

       // Execute hello operation.
       await peopleTable.ExecuteAsync(deleteOperation);

       Console.WriteLine("Entity deleted.");
    }

    else
       Console.WriteLine("Couldn't delete hello entity.");

## <a name="next-steps"></a><span data-ttu-id="18f43-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="18f43-151">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

