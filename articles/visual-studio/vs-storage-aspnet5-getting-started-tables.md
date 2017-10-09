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
# <a name="how-tooget-started-with-azure-table-storage-and-visual-studio-connected-services"></a>Как tooget работу с Visual Studio и хранилище таблиц Azure подключенных служб
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Обзор
В этой статье описывается, как получить работы с использованием таблиц Azure hello хранилища в Visual Studio после создания или ссылка на учетную запись хранилища Azure в проекте ASP.NET Core с помощью Visual Studio **Добавление подключенных служб** диалогового окна.

Hello службы хранилища таблиц Azure позволяет toostore больших объемов структурированных данных. Служба Hello является хранилищем данных NoSQL, принимающий вызовам c аутентификацией внутри и вне hello облако Azure. Таблицы Azure идеально подходят для хранения нереляционных структурированных данных.

Hello **Добавление подключенных служб** операция устанавливает пакеты tooaccess hello соответствующие NuGet хранилища Azure в проекте и добавляет строку hello подключения для hello учетную запись хранилища, tooyour файлы конфигурации проекта.

Более общие сведения об использовании хранилища таблиц Azure см. в разделе [Приступая к работе с хранилищем таблиц Azure с помощью .NET](../storage/storage-dotnet-how-to-use-tables.md).

tooget работы, необходимо сначала toocreate таблицу в учетной записи. Мы покажем, как toocreate Azure таблицу в коде. Мы также покажем, как базовая таблица tooperform и операции с сущностями, например добавление, изменение, чтение и чтение таблицу сущностей. Hello примеры на языке C\# кода и использовать hello клиентская библиотека хранилища Azure для .NET.

**Примечание** -некоторые интерфейсы API, которые выполняют вызовы out tooAzure хранилища в ASP.NET Core hello являются асинхронными. Дополнительные сведения см. в статье [Asynchronous Programming with async and await (C#)](http://msdn.microsoft.com/library/hh191443.aspx) (Асинхронное программирование с использованием ключевых слов Async и Await (C#)). Приведенный ниже код Hello предполагается, что используются асинхронные методы программирования.

## <a name="access-tables-in-code"></a>Доступ к таблицам в коде
tooaccess таблицами в проектах ASP.NET Core, необходимо tooinclude hello следующие элементы tooany C# исходные файлы, доступ к хранилищу таблиц Azure.

1. Убедитесь, что объявления пространств имен hello hello верхней части файла hello C# включить эти **с помощью** инструкции.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Получите объект **CloudStorageAccount** , представляющий данные учетной записи хранения. Hello используйте следующий код tooget hello хранения строки соединения и сведения об учетной записи хранилища из конфигурации службы Azure hello.
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    **Примечание** -используются hello над кодом перед кода hello из hello следующие примеры.
3. Получить **CloudTableClient** объектов tooreference hello таблицы в учетной записи.  
   
        // Create hello table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. Получить **CloudTable** ссылки на объект tooreference определенной таблицы и сущности.
   
        // Get a reference tooa table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a>Создание таблицы в коде
hello toocreate таблицы Azure, просто добавьте вызов слишком**CreateIfNotExistsAsync()**.

    // Create hello CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a>Добавьте таблицу tooa сущности
tooadd tooa сущности таблицы, необходимо создать класс, который определяет hello свойства сущности. Hello следующий код определяет класс сущности с именем **CustomerEntity** , использует hello имени клиента в качестве ключа строку hello и фамилию в качестве ключа секции hello.

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

Операции с таблицей с использованием сущностей выполняются с помощью hello **CloudTable** объекта, созданного ранее в «Таблицы доступ в коде». Hello **TableOperation** toobe операции hello сделать представляет объект. Здравствуйте, следуя примере кода показано, как toocreate **CloudTable** объекта и **CustomerEntity** объекта. операции hello tooprepare **TableOperation** создается сущность customer tooinsert hello в таблицу hello. Наконец hello операция выполняется путем вызова CloudTable.ExecuteAsync.

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a>Вставка пакета сущностей
В таблицу можно вставить несколько сущностей с помощью одной операции записи. Hello следующем примере кода создаются два объекта сущности («Джефф Smith» и «Ben Smith»), добавляет их tooa **TableBatchOperation** объекта с помощью hello **вставить** метода, а затем запускает операцию hello вызов CloudTable.ExecuteBatchAsync.

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

## <a name="get-all-of-hello-entities-in-a-partition"></a>Получить все сущности hello в секции
таблицы для всех сущностей hello в секции, используйте tooquery **TableQuery** объекта. Hello следующий пример кода задает фильтр для сущности, где ключ раздела hello 'Smith'. Этот пример выводит hello поля в каждой сущности в консоли toohello результаты запроса hello.

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

## <a name="get-a-single-entity"></a>Получение одной сущности
Можно написать tooget запроса конкретную сущность. Hello следующий код использует **TableOperation** объекта toospecify клиент с именем 'Ben Smith'. Этот метод возвращает только одну сущность, а не коллекцию и hello возвращаемое значение в **TableResult.Result** — **CustomerEntity** объекта. Указание ключи секций и строк в запросе является hello самый быстрый способ tooretrieve одной сущности из hello **таблицы** службы.

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a>Удаление сущности
После нахождения сущности ее можно удалить. Hello следующий код ищет сущность «клиент» с именем «Ben Smith» и если она его находит, она удаляет.

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

## <a name="next-steps"></a>Дальнейшие действия
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

