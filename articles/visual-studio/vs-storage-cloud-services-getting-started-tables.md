---
title: "aaaGet работы с Visual Studio и хранилище таблиц подключенных служб (облачных служб) | Документы Microsoft"
description: "Как tooget запущена с помощью хранилища Azure таблицы в проект облачной службы в Visual Studio после подключения tooa учетной записи хранилища с помощью Visual Studio подключенные службы"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: a3a11ed8-ba7f-4193-912b-e555f5b72184
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 36da6ed4a12a3595e7234482e3040ecee8c33b8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="6e8d2-103">Начало работы с табличным хранилищем Azure и подключенными службами Visual Studio (проектами облачных служб)</span><span class="sxs-lookup"><span data-stu-id="6e8d2-103">Getting started with Azure table storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="6e8d2-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="6e8d2-104">Overview</span></span>
<span data-ttu-id="6e8d2-105">В этой статье описывается, как tooget запущена с помощью табличного хранилища Azure в Visual Studio после создания или ссылка на учетную запись хранилища Azure в проекте облачных служб с помощью Visual Studio hello **Добавление подключенных служб** диалоговое окно .</span><span class="sxs-lookup"><span data-stu-id="6e8d2-105">This article describes how tooget started using Azure table storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using hello Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="6e8d2-106">Hello **Добавление подключенных служб** операция устанавливает пакеты tooaccess hello соответствующие NuGet хранилища Azure в проекте и добавляет строку hello подключения для hello учетную запись хранилища, tooyour файлы конфигурации проекта.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-106">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="6e8d2-107">Hello службы хранилища таблиц Azure позволяет toostore больших объемов структурированных данных.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-107">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="6e8d2-108">Hello служба находится в хранилище данных NoSQL, принимающий вызовам c аутентификацией внутри и вне hello облако Azure.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-108">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="6e8d2-109">Таблицы Azure идеально подходят для хранения нереляционных структурированных данных.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-109">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="6e8d2-110">tooget работы, необходимо сначала toocreate таблицу в учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-110">tooget started, you first need toocreate a table in your storage account.</span></span> <span data-ttu-id="6e8d2-111">Мы покажем, как toocreate Azure в код, а также как tooperform основной таблицы и сущности операции, такие как добавление, изменение, чтение или чтение таблицы сущности.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-111">We'll show you how toocreate an Azure table in code, and also how tooperform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="6e8d2-112">Hello примеры на языке C\# кода и использовать hello [клиентская библиотека хранилища Microsoft Azure для .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="6e8d2-112">hello samples are written in C\# code and use hello [Microsoft Azure Storage client library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="6e8d2-113">**Примечание:** некоторые интерфейсы API, выполнения вызовов хранилища tooAzure hello являются асинхронными.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-113">**NOTE:** Some of hello APIs that perform calls out tooAzure storage are asynchronous.</span></span> <span data-ttu-id="6e8d2-114">Дополнительные сведения см. в статье [Asynchronous Programming with async and await (C#)](http://msdn.microsoft.com/library/hh191443.aspx) (Асинхронное программирование с использованием ключевых слов Async и Await (C#)).</span><span class="sxs-lookup"><span data-stu-id="6e8d2-114">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="6e8d2-115">Приведенный ниже код Hello предполагается, что используются асинхронные методы программирования.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-115">hello code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="6e8d2-116">Дополнительные сведения о выполнении программных операций с таблицами см. в статье [Приступая к работе с хранилищем таблиц Azure с помощью .NET](../storage/storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="6e8d2-116">See [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md) for more information on programmatically manipulating tables.</span></span>
* <span data-ttu-id="6e8d2-117">Общие сведения о службе хранилища Azure см. в [документации по службе хранилища](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="6e8d2-117">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="6e8d2-118">Общие сведения об облачных службах Azure см. в [документации по облачным службам](https://azure.microsoft.com/documentation/services/cloud-services/).</span><span class="sxs-lookup"><span data-stu-id="6e8d2-118">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="6e8d2-119">Дополнительную информацию о программировании для ASP.NET см. в разделе [ASP.NET](http://www.asp.net).</span><span class="sxs-lookup"><span data-stu-id="6e8d2-119">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="6e8d2-120">Доступ к таблицам в коде</span><span class="sxs-lookup"><span data-stu-id="6e8d2-120">Access tables in code</span></span>
<span data-ttu-id="6e8d2-121">tooaccess таблиц в проектах облачных служб, необходимо tooinclude hello следующие элементы tooany C# исходные файлы, доступ к хранилищу таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-121">tooaccess tables in cloud service projects, you need tooinclude hello following items tooany C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="6e8d2-122">Убедитесь, что объявления пространств имен hello hello верхней части файла hello C# включить эти **с помощью** инструкции.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-122">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="6e8d2-123">Получите объект **CloudStorageAccount** , представляющий данные учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-123">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="6e8d2-124">Используйте следующий код tooget hello соединения строки и хранения данных учетной записи хранения из конфигурации службы Azure hello hello.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-124">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > <span data-ttu-id="6e8d2-125">Используйте все hello над кодом перед кода hello в hello следующие примеры.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-125">Use all of hello above code in front of hello code in hello following samples.</span></span>
   > 
   > 
3. <span data-ttu-id="6e8d2-126">Получить **CloudTableClient** объектов tooreference hello таблицы в учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-126">Get a **CloudTableClient** object tooreference hello table objects in your storage account.</span></span>
   
         // Create hello table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="6e8d2-127">Получить **CloudTable** ссылки на объект tooreference определенной таблицы и сущности.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-127">Get a **CloudTable** reference object tooreference a specific table and entities.</span></span>
   
        // Get a reference tooa table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="6e8d2-128">Создание таблицы в коде</span><span class="sxs-lookup"><span data-stu-id="6e8d2-128">Create a table in code</span></span>
<span data-ttu-id="6e8d2-129">hello toocreate таблицы Azure, просто добавьте вызов слишком**CreateIfNotExistsAsync** toohello после получения **CloudTable** объекта, как описано в разделе «Доступ таблицы в коде» hello.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-129">toocreate hello Azure table, just add a call too**CreateIfNotExistsAsync** toohello after you get a **CloudTable** object as described in hello "Access tables in code" section.</span></span>

    // Create hello CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="6e8d2-130">Добавьте таблицу tooa сущности</span><span class="sxs-lookup"><span data-stu-id="6e8d2-130">Add an entity tooa table</span></span>
<span data-ttu-id="6e8d2-131">tooadd таблицу tooa сущности, создайте класс, определяющий hello свойства сущности.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-131">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="6e8d2-132">Hello следующий код определяет класс сущности с именем **CustomerEntity** , использует hello имени клиента в качестве ключа строку hello и hello последнее имя в качестве ключа секции hello.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-132">hello following code defines an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and hello last name as hello partition key.</span></span>

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

<span data-ttu-id="6e8d2-133">Операции с таблицей с использованием сущностей выполняются с помощью hello **CloudTable** , созданного ранее в «Таблицы доступ в коде».</span><span class="sxs-lookup"><span data-stu-id="6e8d2-133">Table operations involving entities are done using hello **CloudTable** object that you created earlier in "Access tables in code."</span></span> <span data-ttu-id="6e8d2-134">Hello **TableOperation** toobe операции hello сделать представляет объект.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-134">hello **TableOperation** object represents hello operation toobe done.</span></span> <span data-ttu-id="6e8d2-135">Здравствуйте, следуя примере кода показано, как toocreate **CloudTable** объекта и **CustomerEntity** объекта.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-135">hello following code example shows how toocreate a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="6e8d2-136">операции hello tooprepare **TableOperation** создается сущность customer tooinsert hello в таблицу hello.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-136">tooprepare hello operation, a **TableOperation** is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="6e8d2-137">Наконец, выполняется операция hello путем вызова **CloudTable.ExecuteAsync**.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-137">Finally, hello operation is executed by calling **CloudTable.ExecuteAsync**.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="6e8d2-138">Вставка пакета сущностей</span><span class="sxs-lookup"><span data-stu-id="6e8d2-138">Insert a batch of entities</span></span>
<span data-ttu-id="6e8d2-139">В таблицу можно вставить несколько сущностей с помощью одной операции записи.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-139">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="6e8d2-140">Hello следующем примере кода создаются два объекта сущности («Джефф Smith» и «Ben Smith»), добавляет их tooa **TableBatchOperation** объектов с помощью hello метод вставки и затем запускает hello операции путем вызова  **CloudTable.ExecuteBatchAsync**.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-140">hello following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them tooa **TableBatchOperation** object using hello Insert method, and then starts hello operation by calling **CloudTable.ExecuteBatchAsync**.</span></span>

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

## <a name="get-all-of-hello-entities-in-a-partition"></a><span data-ttu-id="6e8d2-141">Получить все сущности hello в секции</span><span class="sxs-lookup"><span data-stu-id="6e8d2-141">Get all of hello entities in a partition</span></span>
<span data-ttu-id="6e8d2-142">таблицы для всех сущностей hello в секции, используйте tooquery **TableQuery** объекта.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-142">tooquery a table for all of hello entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="6e8d2-143">Hello следующий пример кода задает фильтр для сущности, где ключ раздела hello 'Smith'.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-143">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="6e8d2-144">Этот пример выводит hello поля в каждой сущности в консоли toohello результаты запроса hello.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-144">This example prints hello fields of each entity in hello query results toohello console.</span></span>

    // Construct hello query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

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

    return View();


## <a name="get-a-single-entity"></a><span data-ttu-id="6e8d2-145">Получение одной сущности</span><span class="sxs-lookup"><span data-stu-id="6e8d2-145">Get a single entity</span></span>
<span data-ttu-id="6e8d2-146">Можно написать tooget запроса конкретную сущность.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-146">You can write a query tooget a single, specific entity.</span></span> <span data-ttu-id="6e8d2-147">Hello следующий код использует **TableOperation** объекта toospecify клиент с именем 'Ben Smith'.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-147">hello following code uses a **TableOperation** object toospecify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="6e8d2-148">Этот метод возвращает только одну сущность, а не коллекцию и hello возвращаемое значение в **TableResult.Result** — **CustomerEntity** объекта.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-148">This method returns just one entity, rather than a collection, and hello returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="6e8d2-149">Указание ключи секций и строк в запросе является hello самый быстрый способ tooretrieve одной сущности из hello **таблицы** службы.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-149">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="6e8d2-150">Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="6e8d2-150">Delete an entity</span></span>
<span data-ttu-id="6e8d2-151">После нахождения сущности ее можно удалить.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-151">You can delete an entity after you find it.</span></span> <span data-ttu-id="6e8d2-152">Hello следующий код ищет сущность «клиент» с именем «Ben Smith», и если она его находит, она удаляет.</span><span class="sxs-lookup"><span data-stu-id="6e8d2-152">hello following code looks for a customer entity named "Ben Smith", and if it finds it, it deletes it.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6e8d2-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6e8d2-153">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

