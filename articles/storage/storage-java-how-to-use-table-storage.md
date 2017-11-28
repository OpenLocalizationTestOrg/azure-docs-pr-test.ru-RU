---
title: "Как использовать хранилище таблиц из Java | Документация Майкрософт"
description: "Хранение структурированных данных в облаке в хранилище таблиц Azure (хранилище данных NoSQL)."
services: storage
documentationcenter: java
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 45145189-e67f-4ca6-b15d-43af7bfd3f97
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: a4d6f144cc6940ffe2b2c6f27553cd7aa3bcb381
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-table-storage-from-java"></a><span data-ttu-id="23079-103">Использование табличного хранилища из Java</span><span class="sxs-lookup"><span data-stu-id="23079-103">How to use Table storage from Java</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="23079-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="23079-104">Overview</span></span>
<span data-ttu-id="23079-105">В этом руководстве показано, как реализовать типичные сценарии с использованием службы табличного хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="23079-105">This guide will show you how to perform common scenarios using the Azure Table storage service.</span></span> <span data-ttu-id="23079-106">Примеры написаны на Java и используют [пакет SDK службы хранилища Azure для Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="23079-106">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="23079-107">Рассматриваются сценарии **создания**, **перечисления** и **удаления** таблиц, а также **вставки**, **запроса**, **изменения** и **удаления** сущностей в таблице.</span><span class="sxs-lookup"><span data-stu-id="23079-107">The scenarios covered include **creating**, **listing**, and **deleting** tables, as well as **inserting**, **querying**, **modifying**, and **deleting** entities in a table.</span></span> <span data-ttu-id="23079-108">Дополнительные сведения о таблицах см. в разделе [Дальнейшие действия](#Next-Steps).</span><span class="sxs-lookup"><span data-stu-id="23079-108">For more information on tables, see the [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="23079-109">Примечание. Пакет SDK доступен для разработчиков, которые используют хранилище Azure на устройствах под управлением Android.</span><span class="sxs-lookup"><span data-stu-id="23079-109">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="23079-110">Дополнительные сведения см. в разделе [Microsoft Azure Storage SDK for Android][Azure Storage SDK for Android] (Пакет SDK хранилища Azure для Android).</span><span class="sxs-lookup"><span data-stu-id="23079-110">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="23079-111">Создание приложения Java</span><span class="sxs-lookup"><span data-stu-id="23079-111">Create a Java application</span></span>
<span data-ttu-id="23079-112">В этом руководстве будут использоваться компоненты хранилища, которые могут быть вызваны локально в приложении Java или в коде, работающем в веб-роли или рабочей роли в Azure.</span><span class="sxs-lookup"><span data-stu-id="23079-112">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="23079-113">Для этого необходимо установить пакет SDK для Java (JDK) и создать учетную запись хранения Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="23079-113">To do so, you will need to install the Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="23079-114">После того, как это будет сделано, необходимо убедиться, что ваша система разработки отвечает минимальным требованиям и зависимостям, указанным в репозитории [пакета SDK службы хранилища Azure для Java][Azure Storage SDK for Java] на сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="23079-114">Once you have done so, you will need to verify that your development system meets the minimum requirements and dependencies which are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="23079-115">Если ваша система отвечает указанным требованиям можно приступить к выполнению инструкций по загрузке библиотек хранилища Azure для Java из репозитория и их установке на своей системе.</span><span class="sxs-lookup"><span data-stu-id="23079-115">If your system meets those requirements, you can follow the instructions for downloading and installing the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="23079-116">После завершение этих задач вы сможете приступить к созданию приложения Java с использованием примеров из данной статьи.</span><span class="sxs-lookup"><span data-stu-id="23079-116">Once you have completed those tasks, you will be able to create a Java application which uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-table-storage"></a><span data-ttu-id="23079-117">Настройка приложения для доступа к хранилищу таблиц</span><span class="sxs-lookup"><span data-stu-id="23079-117">Configure your application to access table storage</span></span>
<span data-ttu-id="23079-118">Если нужно использовать API-интерфейсы хранилища Microsoft Azure для доступа к таблицам, добавьте следующие инструкции импорта в верхнюю часть файла Java.</span><span class="sxs-lookup"><span data-stu-id="23079-118">Add the following import statements to the top of the Java file where you want to use Microsoft Azure storage APIs to access tables:</span></span>

```java
// Include the following imports to use table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="23079-119">Настройка строки подключения к хранилищу Azure</span><span class="sxs-lookup"><span data-stu-id="23079-119">Set up an Azure storage connection string</span></span>
<span data-ttu-id="23079-120">Клиент хранилища Azure использует строку подключения с целью хранения конечных точек и учетных данных для доступа к службам управления данными.</span><span class="sxs-lookup"><span data-stu-id="23079-120">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="23079-121">При работе в клиентском приложении необходимо указать для хранилища строку подключения в следующем формате, используя имя своей учетной записи хранения и первичный ключ доступа для учетной записи хранения, указанные на [портале Azure](https://portal.azure.com) значениями *AccountName* и *AccountKey*.</span><span class="sxs-lookup"><span data-stu-id="23079-121">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="23079-122">В этом примере показано, как объявить статическое поле для размещения строки подключения:</span><span class="sxs-lookup"><span data-stu-id="23079-122">This example shows how you can declare a static field to hold the connection string:</span></span>

```java
// Define the connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="23079-123">Если приложение выполняется в роли на платформе Microsoft Azure, эта строка может храниться в файле конфигурации службы *ServiceConfiguration.cscfg*, для доступа к которой можно использовать вызов метода **RoleEnvironment.getConfigurationSettings** .</span><span class="sxs-lookup"><span data-stu-id="23079-123">In an application running within a role in Microsoft Azure, this string can be stored in the service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="23079-124">Ниже приведен пример получения строки подключения из элемента **Setting** с именем *StorageConnectionString* в файле конфигурации службы:</span><span class="sxs-lookup"><span data-stu-id="23079-124">Here's an example of getting the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="23079-125">В приведенных ниже примерах предполагается, что вы использовали одно из этих двух определений для получения строки подключения к хранилищу.</span><span class="sxs-lookup"><span data-stu-id="23079-125">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="how-to-create-a-table"></a><span data-ttu-id="23079-126">Практическое руководство. Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="23079-126">How to: Create a table</span></span>
<span data-ttu-id="23079-127">Объект **CloudTableClient** позволяет ссылаться на объекты таблиц и сущностей.</span><span class="sxs-lookup"><span data-stu-id="23079-127">A **CloudTableClient** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="23079-128">Следующий код создает объект **CloudTableClient** и использует его для создания нового объекта **CloudTable**, который представляет таблицу people.</span><span class="sxs-lookup"><span data-stu-id="23079-128">The following code creates a **CloudTableClient** object and uses it to create a new **CloudTable** object which represents a table named "people".</span></span> <span data-ttu-id="23079-129">(Примечание. Есть и другие способы создания объектов **CloudStorageAccount**. Дополнительные сведения см. в разделе **CloudStorageAccount** в [справочнике по пакету SDK для клиента службы хранилища Azure].)</span><span class="sxs-lookup"><span data-stu-id="23079-129">(Note: There are additional ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference].)</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create the table if it doesn't exist.
    String tableName = "people";
    CloudTable cloudTable = tableClient.getTableReference(tableName);
    cloudTable.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-the-tables"></a><span data-ttu-id="23079-130">Как перечислять таблицы</span><span class="sxs-lookup"><span data-stu-id="23079-130">How to: List the tables</span></span>
<span data-ttu-id="23079-131">Чтобы получить список таблиц, вызовите метод **CloudTableClient.listTables()** для извлечения пригодного к итерации списка имен таблиц.</span><span class="sxs-lookup"><span data-stu-id="23079-131">To get a list of tables, call the **CloudTableClient.listTables()** method to retrieve an iterable list of table names.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Loop through the collection of table names.
    for (String table : tableClient.listTables())
    {
        // Output each table name.
        System.out.println(table);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-an-entity-to-a-table"></a><span data-ttu-id="23079-132">Практическое руководство. Добавление сущности в таблицу</span><span class="sxs-lookup"><span data-stu-id="23079-132">How to: Add an entity to a table</span></span>
<span data-ttu-id="23079-133">Сущности сопоставляются с объектами Java с помощью настраиваемого класса, реализующего **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="23079-133">Entities map to Java objects using a custom class implementing **TableEntity**.</span></span> <span data-ttu-id="23079-134">Для удобства класс **TableServiceEntity** реализует **TableEntity** и использует отражение для сопоставления свойств с указанными для свойств методами получения и задания.</span><span class="sxs-lookup"><span data-stu-id="23079-134">For convenience, the **TableServiceEntity** class implements **TableEntity** and uses reflection to map properties to getter and setter methods named for the properties.</span></span> <span data-ttu-id="23079-135">Чтобы добавить сущность в таблицу, сначала создайте класс, который определяет свойства сущности.</span><span class="sxs-lookup"><span data-stu-id="23079-135">To add an entity to a table, first create a class that defines the properties of your entity.</span></span> <span data-ttu-id="23079-136">Следующий код определяет класс сущностей, который использует имя клиента как ключ строки, а фамилию клиента — как ключ раздела.</span><span class="sxs-lookup"><span data-stu-id="23079-136">The following code defines an entity class which uses the customer's first name as the row key, and last name as the partition key.</span></span> <span data-ttu-id="23079-137">Вместе ключ раздела и ключ строки сущности уникальным образом идентифицируют сущность в таблице.</span><span class="sxs-lookup"><span data-stu-id="23079-137">Together, an entity's partition and row key uniquely identify the entity in the table.</span></span> <span data-ttu-id="23079-138">Сущности с одним ключом раздела можно запрашивать быстрее, чем сущности с разными ключами раздела.</span><span class="sxs-lookup"><span data-stu-id="23079-138">Entities with the same partition key can be queried faster than those with different partition keys.</span></span>

```java
public class CustomerEntity extends TableServiceEntity {
    public CustomerEntity(String lastName, String firstName) {
        this.partitionKey = lastName;
        this.rowKey = firstName;
    }

    public CustomerEntity() { }

    String email;
    String phoneNumber;

    public String getEmail() {
        return this.email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getPhoneNumber() {
        return this.phoneNumber;
    }

    public void setPhoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
    }
}
```

<span data-ttu-id="23079-139">Табличные операций, включающие сущности, требуют объект **TableOperation** .</span><span class="sxs-lookup"><span data-stu-id="23079-139">Table operations involving entities require a **TableOperation** object.</span></span> <span data-ttu-id="23079-140">Этот объект определяет выполняемую для сущности операцию, которую можно запустить с помощью объекта **CloudTable** .</span><span class="sxs-lookup"><span data-stu-id="23079-140">This object defines the operation to be performed on an entity, which can be executed with a **CloudTable** object.</span></span> <span data-ttu-id="23079-141">В следующем коде создается новый экземпляр класса **CustomerEntity** с сохраняемыми данными клиента.</span><span class="sxs-lookup"><span data-stu-id="23079-141">The following code creates a new instance of the **CustomerEntity** class with some customer data to be stored.</span></span> <span data-ttu-id="23079-142">Далее код вызывает **TableOperation.insertOrReplace**, чтобы создать объект **TableOperation** для вставки сущности в таблицу, а также связывает с ним новый объект **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="23079-142">The code next calls **TableOperation.insertOrReplace** to create a **TableOperation** object to insert an entity into a table, and associates the new **CustomerEntity** with it.</span></span> <span data-ttu-id="23079-143">Наконец код вызывает метод **execute** объекта **CloudTable**, определяя таблицу people и новый объект **TableOperation**, который затем отправляет запрос в службу хранилища для вставки новой сущности клиента в таблицу people или замены сущности, если она уже существует.</span><span class="sxs-lookup"><span data-stu-id="23079-143">Finally, the code calls the **execute** method on the **CloudTable** object, specifying the "people" table and the new **TableOperation**, which then sends a request to the storage service to insert the new customer entity into the "people" table, or replace the entity if it already exists.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.setEmail("Walter@contoso.com");
    customer1.setPhoneNumber("425-555-0101");

    // Create an operation to add the new customer to the people table.
    TableOperation insertCustomer1 = TableOperation.insertOrReplace(customer1);

    // Submit the operation to the table service.
    cloudTable.execute(insertCustomer1);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-a-batch-of-entities"></a><span data-ttu-id="23079-144">Практическое руководство. Вставка пакета сущностей</span><span class="sxs-lookup"><span data-stu-id="23079-144">How to: Insert a batch of entities</span></span>
<span data-ttu-id="23079-145">Вы можете вставить пакет сущностей в таблицу в одной операции записи.</span><span class="sxs-lookup"><span data-stu-id="23079-145">You can insert a batch of entities to the table service in one write operation.</span></span> <span data-ttu-id="23079-146">Следующий код создает объект **TableBatchOperation** , а затем добавляет в него три операции вставки.</span><span class="sxs-lookup"><span data-stu-id="23079-146">The following code creates a **TableBatchOperation** object, then adds three insert operations to it.</span></span> <span data-ttu-id="23079-147">Каждая операция вставки добавляется путем создания нового объекта сущности, установки его значений и последующего вызова метода **insert** для объекта **TableBatchOperation**, чтобы связать сущность с новой операцией вставки.</span><span class="sxs-lookup"><span data-stu-id="23079-147">Each insert operation is added by creating a new entity object, setting its values, and then calling the **insert** method on the **TableBatchOperation** object to associate the entity with a new insert operation.</span></span> <span data-ttu-id="23079-148">Затем код вызывает метод **execute** объекта **CloudTable**, определяя таблицу people и объект **TableBatchOperation**, который отправляет пакет операций таблицы в службу хранилища в одном запросе.</span><span class="sxs-lookup"><span data-stu-id="23079-148">Then the code calls **execute** on the **CloudTable** object, specifying the "people" table and the **TableBatchOperation** object, which sends the batch of table operations to the storage service in a single request.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Define a batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a customer entity to add to the table.
    CustomerEntity customer = new CustomerEntity("Smith", "Jeff");
    customer.setEmail("Jeff@contoso.com");
    customer.setPhoneNumber("425-555-0104");
    batchOperation.insertOrReplace(customer);

    // Create another customer entity to add to the table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.setEmail("Ben@contoso.com");
    customer2.setPhoneNumber("425-555-0102");
    batchOperation.insertOrReplace(customer2);

    // Create a third customer entity to add to the table.
    CustomerEntity customer3 = new CustomerEntity("Smith", "Denise");
    customer3.setEmail("Denise@contoso.com");
    customer3.setPhoneNumber("425-555-0103");
    batchOperation.insertOrReplace(customer3);

    // Execute the batch of operations on the "people" table.
    cloudTable.execute(batchOperation);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="23079-149">Некоторые другие примечания к пакетным операциям:</span><span class="sxs-lookup"><span data-stu-id="23079-149">Some things to note on batch operations:</span></span>

* <span data-ttu-id="23079-150">В отдельном пакете можно выполнить до 100 операций вставки, удаления, объединения, замены, вставки или замены и вставки или замены операций в любом сочетании.</span><span class="sxs-lookup"><span data-stu-id="23079-150">You can perform up to 100 insert, delete, merge, replace, insert or merge, and insert or replace operations in any combination in a single batch.</span></span>
* <span data-ttu-id="23079-151">Пакетная операция может иметь операцию извлечения, если она является единственной операцией в пакете.</span><span class="sxs-lookup"><span data-stu-id="23079-151">A batch operation can have a retrieve operation, if it is the only operation in the batch.</span></span>
* <span data-ttu-id="23079-152">У всех сущностей в одной пакетной операции должен быть одинаковый ключ раздела.</span><span class="sxs-lookup"><span data-stu-id="23079-152">All entities in a single batch operation must have the same partition key.</span></span>
* <span data-ttu-id="23079-153">Объем полезных данных пакетной операции ограничен размером 4 МБ.</span><span class="sxs-lookup"><span data-stu-id="23079-153">A batch operation is limited to a 4MB data payload.</span></span>

## <a name="how-to-retrieve-all-entities-in-a-partition"></a><span data-ttu-id="23079-154">Практическое руководство. Получение всех сущностей в разделе</span><span class="sxs-lookup"><span data-stu-id="23079-154">How to: Retrieve all entities in a partition</span></span>
<span data-ttu-id="23079-155">Чтобы запросить из таблицы сущности раздела, можно использовать **TableQuery**.</span><span class="sxs-lookup"><span data-stu-id="23079-155">To query a table for entities in a partition, you can use a **TableQuery**.</span></span> <span data-ttu-id="23079-156">Вызовите **TableQuery.from**, чтобы создать запрос для определенной таблицы, который возвращает результаты заданного типа.</span><span class="sxs-lookup"><span data-stu-id="23079-156">Call **TableQuery.from** to create a query on a particular table that returns a specified result type.</span></span> <span data-ttu-id="23079-157">Следующий код задает фильтр для сущностей с ключомраздела "Smith".</span><span class="sxs-lookup"><span data-stu-id="23079-157">The following code specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="23079-158">**TableQuery.generateFilterCondition** — это вспомогательный метод для создания фильтров запросов.</span><span class="sxs-lookup"><span data-stu-id="23079-158">**TableQuery.generateFilterCondition** is a helper method to create filters for queries.</span></span> <span data-ttu-id="23079-159">Вызовите **where** по ссылке, которую вернул метод **TableQuery.from**, чтобы применить фильтр к запросу.</span><span class="sxs-lookup"><span data-stu-id="23079-159">Call **where** on the reference returned by the **TableQuery.from** method to apply the filter to the query.</span></span> <span data-ttu-id="23079-160">При выполнении запроса с помощью вызова **execute** для объекта **CloudTable** он возвращает **Iterator** с указанным типом результата **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="23079-160">When the query is executed with a call to **execute** on the **CloudTable** object, it returns an **Iterator** with the **CustomerEntity** result type specified.</span></span> <span data-ttu-id="23079-161">Затем можно использовать возвращенное значение **Iterator** в каждом цикле для получения результатов.</span><span class="sxs-lookup"><span data-stu-id="23079-161">You can then use the **Iterator** returned in a for each loop to consume the results.</span></span> <span data-ttu-id="23079-162">Этот код выводит на консоль поля каждой сущности в результатах запроса.</span><span class="sxs-lookup"><span data-stu-id="23079-162">This code prints the fields of each entity in the query results to the console.</span></span>

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where the partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Specify a partition query, using "Smith" as the partition key filter.
    TableQuery<CustomerEntity> partitionQuery =
        TableQuery.from(CustomerEntity.class)
        .where(partitionFilter);

    // Loop through the results, displaying information about the entity.
    for (CustomerEntity entity : cloudTable.execute(partitionQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="23079-163">Практическое руководство. Получение диапазона сущностей в разделе</span><span class="sxs-lookup"><span data-stu-id="23079-163">How to: Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="23079-164">Если вы не хотите запрашивать все сущности в разделе, можно указать диапазон с помощью операторов сравнения в фильтре.</span><span class="sxs-lookup"><span data-stu-id="23079-164">If you don't want to query all the entities in a partition, you can specify a range by using comparison operators in a filter.</span></span> <span data-ttu-id="23079-165">В следующем коде совместно используются два фильтра для получения всех сущностей в разделе "Smith", где ключ строки (имя) начинается с буквы до "E" в алфавите.</span><span class="sxs-lookup"><span data-stu-id="23079-165">The following code combines two filters to get all entities in partition "Smith" where the row key (first name) starts with a letter up to 'E' in the alphabet.</span></span> <span data-ttu-id="23079-166">После чего результаты запроса выводятся на консоль.</span><span class="sxs-lookup"><span data-stu-id="23079-166">Then it prints the query results.</span></span> <span data-ttu-id="23079-167">Если вы используете сущности, добавленные в таблицу во время работы с разделом о пакетной вставке, то на этот раз возвращаются только две сущности (Ben Smith и Denise Smith), а Jeff Smith не выводится.</span><span class="sxs-lookup"><span data-stu-id="23079-167">If you use the entities added to the table in the batch insert section of this guide, only two entities are returned this time (Ben and Denise Smith); Jeff Smith is not included.</span></span>

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where the partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Create a filter condition where the row key is less than the letter "E".
    String rowFilter = TableQuery.generateFilterCondition(
        ROW_KEY,
        QueryComparisons.LESS_THAN,
        "E");

    // Combine the two conditions into a filter expression.
    String combinedFilter = TableQuery.combineFilters(partitionFilter,
        Operators.AND, rowFilter);

    // Specify a range query, using "Smith" as the partition key,
    // with the row key being up to the letter "E".
    TableQuery<CustomerEntity> rangeQuery =
        TableQuery.from(CustomerEntity.class)
        .where(combinedFilter);

    // Loop through the results, displaying information about the entity
    for (CustomerEntity entity : cloudTable.execute(rangeQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-single-entity"></a><span data-ttu-id="23079-168">Практическое руководство. Извлечение одной сущности</span><span class="sxs-lookup"><span data-stu-id="23079-168">How to: Retrieve a single entity</span></span>
<span data-ttu-id="23079-169">Можно написать запрос для получения отдельной сущности.</span><span class="sxs-lookup"><span data-stu-id="23079-169">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="23079-170">В следующем коде выполняется вызов **TableOperation.retrieve** с параметрами ключа раздела и ключа строки для указания клиента Jeff Smith вместо создания **TableQuery** и применения фильтров с таким же результатом.</span><span class="sxs-lookup"><span data-stu-id="23079-170">The following code calls **TableOperation.retrieve** with partition key and row key parameters to specify the customer "Jeff Smith", instead of creating a **TableQuery** and using filters to do the same thing.</span></span> <span data-ttu-id="23079-171">При выполнении операция извлечения возвращает только одну сущность, а не коллекцию.</span><span class="sxs-lookup"><span data-stu-id="23079-171">When executed, the retrieve operation returns just one entity, rather than a collection.</span></span> <span data-ttu-id="23079-172">Метод **getResultAsType** приводит результат к типу назначенной цели — объекту **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="23079-172">The **getResultAsType** method casts the result to the type of the assignment target, a **CustomerEntity** object.</span></span> <span data-ttu-id="23079-173">Если этот тип не совместим с типом, указанным в запросе, возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="23079-173">If this type is not compatible with the type specified for the query, an exception will be thrown.</span></span> <span data-ttu-id="23079-174">Значение NULL возвращается, если ни одна сущность не подходит по ключам раздела и строки.</span><span class="sxs-lookup"><span data-stu-id="23079-174">A null value is returned if no entity has an exact partition and row key match.</span></span> <span data-ttu-id="23079-175">Указание ключа раздела и ключа строки в запросе — самый быстрый способ извлечь одну сущность из службы таблиц.</span><span class="sxs-lookup"><span data-stu-id="23079-175">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff"
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit the operation to the table service and get the specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Output the entity.
    if (specificEntity != null)
    {
        System.out.println(specificEntity.getPartitionKey() +
            " " + specificEntity.getRowKey() +
            "\t" + specificEntity.getEmail() +
            "\t" + specificEntity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-modify-an-entity"></a><span data-ttu-id="23079-176">Практическое руководство. Изменение сущности</span><span class="sxs-lookup"><span data-stu-id="23079-176">How to: Modify an entity</span></span>
<span data-ttu-id="23079-177">Чтобы изменить сущность, извлеките ее из службы таблиц, измените объект сущности и сохраните изменения в службе таблиц с помощью операции замены или объединения.</span><span class="sxs-lookup"><span data-stu-id="23079-177">To modify an entity, retrieve it from the table service, make changes to the entity object, and save the changes back to the table service with a replace or merge operation.</span></span> <span data-ttu-id="23079-178">Следующий код изменяет существующий номер телефона клиента.</span><span class="sxs-lookup"><span data-stu-id="23079-178">The following code changes an existing customer's phone number.</span></span> <span data-ttu-id="23079-179">Вместо вызова метода **TableOperation.insert**, который мы осуществляли при вставке, этот код вызывает **TableOperation.replace**.</span><span class="sxs-lookup"><span data-stu-id="23079-179">Instead of calling **TableOperation.insert** like we did to insert, this code calls **TableOperation.replace**.</span></span> <span data-ttu-id="23079-180">Метод **CloudTableClient.execute** вызывает службу таблиц и заменяет сущность, если только другое приложение не изменило ее с момента извлечения данным приложением.</span><span class="sxs-lookup"><span data-stu-id="23079-180">The **CloudTable.execute** method calls the table service, and the entity is replaced, unless another application changed it in the time since this application retrieved it.</span></span> <span data-ttu-id="23079-181">Когда это происходит, возникает исключение, и сущность необходимо получить, изменить и сохранить повторно.</span><span class="sxs-lookup"><span data-stu-id="23079-181">When that happens, an exception is thrown, and the entity must be retrieved, modified, and saved again.</span></span> <span data-ttu-id="23079-182">Этот оптимистичный шаблон повторения в случае конфликтов широко применяется в системе распределенного хранения.</span><span class="sxs-lookup"><span data-stu-id="23079-182">This optimistic concurrency retry pattern is common in a distributed storage system.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit the operation to the table service and get the specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Specify a new phone number.
    specificEntity.setPhoneNumber("425-555-0105");

    // Create an operation to replace the entity.
    TableOperation replaceEntity = TableOperation.replace(specificEntity);

    // Submit the operation to the table service.
    cloudTable.execute(replaceEntity);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-query-a-subset-of-entity-properties"></a><span data-ttu-id="23079-183">Практическое руководство. Запрос подмножества свойств сущности</span><span class="sxs-lookup"><span data-stu-id="23079-183">How to: Query a subset of entity properties</span></span>
<span data-ttu-id="23079-184">Запрос к таблице может получить лишь несколько свойств сущности.</span><span class="sxs-lookup"><span data-stu-id="23079-184">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="23079-185">Этот метод, который называется "проекцией", снижает потребление пропускной способности и может повысить производительность запросов, особенно для крупных сущностей.</span><span class="sxs-lookup"><span data-stu-id="23079-185">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="23079-186">Запрос в следующем коде использует метод **select**, чтобы возвратить только адреса электронной почты сущностей в таблице.</span><span class="sxs-lookup"><span data-stu-id="23079-186">The query in the following code uses the **select** method to return only the email addresses of entities in the table.</span></span> <span data-ttu-id="23079-187">Результаты проецируются в коллекцию **String** с помощью метода **EntityResolver**, который выполняет преобразование типов сущностей, возвращенных с сервера.</span><span class="sxs-lookup"><span data-stu-id="23079-187">The results are projected into a collection of **String** with the help of an **EntityResolver**, which does the type conversion on the entities returned from the server.</span></span> <span data-ttu-id="23079-188">Дополнительные сведения о проекции см. в записи блога [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection] (Таблицы Azure: введение в Upsert и проекции в запросах).</span><span class="sxs-lookup"><span data-stu-id="23079-188">You can learn more about projection in [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span> <span data-ttu-id="23079-189">Обратите внимание, что проекция не поддерживается в эмуляторе локального хранилища, поэтому этот код выполняется только при использовании учетной записи хранения в службе таблиц.</span><span class="sxs-lookup"><span data-stu-id="23079-189">Note that projection is not supported on the local storage emulator, so this code runs only when using an account on the table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Define a projection query that retrieves only the Email property
    TableQuery<CustomerEntity> projectionQuery =
        TableQuery.from(CustomerEntity.class)
        .select(new String[] {"Email"});

    // Define a Entity resolver to project the entity to the Email value.
    EntityResolver<String> emailResolver = new EntityResolver<String>() {
        @Override
        public String resolve(String PartitionKey, String RowKey, Date timeStamp, HashMap<String, EntityProperty> properties, String etag) {
            return properties.get("Email").getValueAsString();
        }
    };

    // Loop through the results, displaying the Email values.
    for (String projectedString :
        cloudTable.execute(projectionQuery, emailResolver)) {
            System.out.println(projectedString);
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-or-replace-an-entity"></a><span data-ttu-id="23079-190">Как вставлять и заменять сущности</span><span class="sxs-lookup"><span data-stu-id="23079-190">How to: Insert or Replace an entity</span></span>
<span data-ttu-id="23079-191">Часто требуется добавить сущность в таблицу, не зная, присутствует ли она там.</span><span class="sxs-lookup"><span data-stu-id="23079-191">Often you want to add an entity to a table without knowing if it already exists in the table.</span></span> <span data-ttu-id="23079-192">Операция вставки или замены позволяет сделать один запрос, который вставит сущность, если она не существует, или заменит существующую сущность.</span><span class="sxs-lookup"><span data-stu-id="23079-192">An insert-or-replace operation allows you to make a single request which will insert the entity if it does not exist or replace the existing one if it does.</span></span> <span data-ttu-id="23079-193">В продолжение материала предыдущих примеров следующий код вставляет или заменяет сущность "Walter Harp".</span><span class="sxs-lookup"><span data-stu-id="23079-193">Building on prior examples, the following code inserts or replaces the entity for "Walter Harp".</span></span> <span data-ttu-id="23079-194">После создания новой сущности этот код вызывает метод **TableOperation.insertOrReplace**.</span><span class="sxs-lookup"><span data-stu-id="23079-194">After creating a new entity, this code calls the **TableOperation.insertOrReplace** method.</span></span> <span data-ttu-id="23079-195">Далее код вызывает метод **execute** объекта **CloudTable** с таблицей, а также табличными операциями вставки или замены в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="23079-195">This code then calls **execute** on the **CloudTable** object with the table and the insert or replace table operation as the parameters.</span></span> <span data-ttu-id="23079-196">Чтобы обновить только часть сущности, можно вместо этого использовать метод **TableOperation.insertOrMerge**.</span><span class="sxs-lookup"><span data-stu-id="23079-196">To update only part of an entity, the **TableOperation.insertOrMerge** method can be used instead.</span></span> <span data-ttu-id="23079-197">Обратите внимание, что операция вставить-или-заменить не поддерживается в эмуляторе локального хранилища, поэтому этот код выполняется только при использовании учетной записи хранения в службе таблиц.</span><span class="sxs-lookup"><span data-stu-id="23079-197">Note that insert-or-replace is not supported on the local storage emulator, so this code runs only when using an account on the table service.</span></span> <span data-ttu-id="23079-198">Дополнительные сведения об операциях "вставка или замена" и "вставка или объединение" см. в записи блога [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection] (Таблицы Azure: введение в Upsert и проекции в запросах).</span><span class="sxs-lookup"><span data-stu-id="23079-198">You can learn more about insert-or-replace and insert-or-merge in this [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer5 = new CustomerEntity("Harp", "Walter");
    customer5.setEmail("Walter@contoso.com");
    customer5.setPhoneNumber("425-555-0106");

    // Create an operation to add the new customer to the people table.
    TableOperation insertCustomer5 = TableOperation.insertOrReplace(customer5);

    // Submit the operation to the table service.
    cloudTable.execute(insertCustomer5);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-an-entity"></a><span data-ttu-id="23079-199">Практическое руководство. Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="23079-199">How to: Delete an entity</span></span>
<span data-ttu-id="23079-200">Сущность можно легко удалить после ее получения.</span><span class="sxs-lookup"><span data-stu-id="23079-200">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="23079-201">После получение сущности вызовите **TableOperation.delete** с удаляемой сущностью.</span><span class="sxs-lookup"><span data-stu-id="23079-201">Once the entity is retrieved, call **TableOperation.delete** with the entity to delete.</span></span> <span data-ttu-id="23079-202">Затем вызовите **execute** объекта **CloudTable**.</span><span class="sxs-lookup"><span data-stu-id="23079-202">Then call **execute** on the **CloudTable** object.</span></span> <span data-ttu-id="23079-203">Следующий код извлекает и удаляет сущность клиента.</span><span class="sxs-lookup"><span data-stu-id="23079-203">The following code retrieves and deletes a customer entity.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for the table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff = TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Retrieve the entity with partition key of "Smith" and row key of "Jeff".
    CustomerEntity entitySmithJeff =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Create an operation to delete the entity.
    TableOperation deleteSmithJeff = TableOperation.delete(entitySmithJeff);

    // Submit the delete operation to the table service.
    cloudTable.execute(deleteSmithJeff);
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-table"></a><span data-ttu-id="23079-204">Практическое руководство. Удаление таблицы</span><span class="sxs-lookup"><span data-stu-id="23079-204">How to: Delete a table</span></span>
<span data-ttu-id="23079-205">Наконец, следующий код удаляет таблицу из учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="23079-205">Finally, the following code deletes a table from a storage account.</span></span> <span data-ttu-id="23079-206">Удаленную таблицу нельзя воссоздать в течение определенного времени после удаления. Этот период обычно составляет менее сорока секунд.</span><span class="sxs-lookup"><span data-stu-id="23079-206">A table which has been deleted will be unavailable to be recreated for a period of time following the deletion, usually less than forty seconds.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create the table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Delete the table and all its data if it exists.
    CloudTable cloudTable = tableClient.getTableReference("people");
    cloudTable.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```
[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="next-steps"></a><span data-ttu-id="23079-207">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="23079-207">Next steps</span></span>

* <span data-ttu-id="23079-208">[Обозреватель хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) — это бесплатное автономное приложение от корпорации Майкрософт, позволяющее визуализировать данные из службы хранилища Azure на платформе Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="23079-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="23079-209">[Пакет SDK службы хранилища Azure для Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="23079-209">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="23079-210">[справочнике по пакету SDK для клиента службы хранилища Azure][справочнике по пакету SDK для клиента службы хранилища Azure]</span><span class="sxs-lookup"><span data-stu-id="23079-210">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="23079-211">[REST API службы хранилища Azure][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="23079-211">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="23079-212">[Блог рабочей группы службы хранилища Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="23079-212">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="23079-213">Дополнительную информацию см. также в [Центре разработчика Java](/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="23079-213">For more information, see also the [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
<span data-ttu-id="23079-214">[справочнике по пакету SDK для клиента службы хранилища Azure]: http://dl.windowsazure.com/storage/javadoc/</span><span class="sxs-lookup"><span data-stu-id="23079-214">[Azure Storage Client SDK Reference]: http://dl.windowsazure.com/storage/javadoc/</span></span>
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
