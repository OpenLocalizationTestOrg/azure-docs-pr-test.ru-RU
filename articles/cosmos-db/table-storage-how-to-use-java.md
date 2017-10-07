---
title: "aaaHow toouse хранилище таблиц из Java | Документы Microsoft"
description: "Хранения структурированных данных в облаке hello, с помощью хранилища таблиц Azure, хранилище данных NoSQL."
services: cosmos-db
documentationcenter: java
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 45145189-e67f-4ca6-b15d-43af7bfd3f97
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 20d03e867219cc254da8dad37cf3cf61bca65671
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-java"></a><span data-ttu-id="9ca4b-103">Как toouse хранилище таблиц из Java</span><span class="sxs-lookup"><span data-stu-id="9ca4b-103">How toouse Table storage from Java</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="9ca4b-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="9ca4b-104">Overview</span></span>
<span data-ttu-id="9ca4b-105">В этом руководстве будет показано, как tooperform распространенных сценариев использования hello службы хранилища таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-105">This guide will show you how tooperform common scenarios using hello Azure Table storage service.</span></span> <span data-ttu-id="9ca4b-106">Hello примеры написаны на Java и использовать hello [пакет SDK хранилища Azure для Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="9ca4b-106">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="9ca4b-107">Hello сценарии включают **создание**, **вывод**, и **удаление** таблиц, а также **Вставка**,  **запрос**, **изменение**, и **удаление** сущностей в таблице.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-107">hello scenarios covered include **creating**, **listing**, and **deleting** tables, as well as **inserting**, **querying**, **modifying**, and **deleting** entities in a table.</span></span> <span data-ttu-id="9ca4b-108">Дополнительные сведения о таблицах см. в разделе hello [дальнейшие действия](#Next-Steps) раздела.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-108">For more information on tables, see hello [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="9ca4b-109">Примечание. Пакет SDK доступен для разработчиков, которые используют хранилище Azure на устройствах под управлением Android.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-109">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="9ca4b-110">Дополнительные сведения см. в разделе hello [пакет SDK хранилища Azure для Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="9ca4b-110">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="9ca4b-111">Создание приложения Java</span><span class="sxs-lookup"><span data-stu-id="9ca4b-111">Create a Java application</span></span>
<span data-ttu-id="9ca4b-112">В этом руководстве будут использоваться компоненты хранилища, которые могут быть вызваны локально в приложении Java или в коде, работающем в веб-роли или рабочей роли в Azure.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-112">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="9ca4b-113">toodo таким образом, вам потребуется tooinstall hello Java Development Kit (JDK) и создать учетную запись хранилища Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-113">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="9ca4b-114">Как только вы делали, вам потребуется tooverify, разработки система удовлетворяет минимальным требованиям hello и зависимости, которые указаны в hello [пакет SDK хранилища Azure для Java] [ Azure Storage SDK for Java] репозитория в GitHub.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-114">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="9ca4b-115">Если компьютер соответствует этим требованиям, можно выполнить hello инструкции по загрузке и установке hello библиотеки хранилища Azure для Java в вашей системе из этого репозитория.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-115">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="9ca4b-116">После завершения этих задач можно будет toocreate приложения Java, использующего hello примеры в этой статье.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-116">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-table-storage"></a><span data-ttu-id="9ca4b-117">Настройка хранилища таблицы tooaccess приложения</span><span class="sxs-lookup"><span data-stu-id="9ca4b-117">Configure your application tooaccess table storage</span></span>
<span data-ttu-id="9ca4b-118">Добавьте следующие начало toohello инструкции импорта файла Java hello, место таблиц tooaccess API-интерфейсов хранилища Microsoft Azure toouse hello:</span><span class="sxs-lookup"><span data-stu-id="9ca4b-118">Add hello following import statements toohello top of hello Java file where you want toouse Microsoft Azure storage APIs tooaccess tables:</span></span>

```java
// Include hello following imports toouse table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="9ca4b-119">Настройка строки подключения к хранилищу Azure</span><span class="sxs-lookup"><span data-stu-id="9ca4b-119">Set up an Azure storage connection string</span></span>
<span data-ttu-id="9ca4b-120">Клиент хранилища Azure использует хранилища конечные точки toostore соединения строки и учетные данные для доступа к службам данных управления.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-120">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="9ca4b-121">При работе в клиентском приложении, необходимо указать строку соединения хранения hello в hello следующая формата, используя hello имя учетной записи и hello первичный ключ доступа для учетной записи хранения hello, перечисленные в hello [портал Azure](https://portal.azure.com)для hello *AccountName* и *AccountKey* значения.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-121">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="9ca4b-122">В этом примере показано, как объявить строки подключения hello toohold статического поля:</span><span class="sxs-lookup"><span data-stu-id="9ca4b-122">This example shows how you can declare a static field toohold hello connection string:</span></span>

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="9ca4b-123">Эта строка в приложения, запущенного в рамках роли в Microsoft Azure, могут храниться в файле конфигурации службы hello, *ServiceConfiguration.cscfg*и можно осуществить с помощью toohello вызова  **RoleEnvironment.getConfigurationSettings** метод.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-123">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="9ca4b-124">Ниже приведен пример получения строки подключения hello из **параметр** элемента с именем *StorageConnectionString* в файле конфигурации службы hello:</span><span class="sxs-lookup"><span data-stu-id="9ca4b-124">Here's an example of getting hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="9ca4b-125">Hello следующие образцы предполагается, что используется один из этих двух методов tooget hello строки подключения к хранилищу.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-125">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="how-to-create-a-table"></a><span data-ttu-id="9ca4b-126">Практическое руководство. Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="9ca4b-126">How to: Create a table</span></span>
<span data-ttu-id="9ca4b-127">Объект **CloudTableClient** позволяет ссылаться на объекты таблиц и сущностей.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-127">A **CloudTableClient** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="9ca4b-128">Hello следующий код создает **CloudTableClient** объекта и использует его toocreate новый **CloudTable** объект, который представляет таблицу с именем «пользователи».</span><span class="sxs-lookup"><span data-stu-id="9ca4b-128">hello following code creates a **CloudTableClient** object and uses it toocreate a new **CloudTable** object which represents a table named "people".</span></span> <span data-ttu-id="9ca4b-129">(Примечание: существуют дополнительные способы toocreate **CloudStorageAccount** объектов; Дополнительные сведения см. в разделе **CloudStorageAccount** в hello [Azure SDK Справочник по клиентской хранилища].)</span><span class="sxs-lookup"><span data-stu-id="9ca4b-129">(Note: There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].)</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create hello table if it doesn't exist.
    String tableName = "people";
    CloudTable cloudTable = tableClient.getTableReference(tableName);
    cloudTable.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-tables"></a><span data-ttu-id="9ca4b-130">Как: список таблиц hello</span><span class="sxs-lookup"><span data-stu-id="9ca4b-130">How to: List hello tables</span></span>
<span data-ttu-id="9ca4b-131">список таблиц, вызов hello tooget **CloudTableClient.listTables()** tooretrieve метод итерируемого перечень имен таблиц.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-131">tooget a list of tables, call hello **CloudTableClient.listTables()** method tooretrieve an iterable list of table names.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Loop through hello collection of table names.
    for (String table : tableClient.listTables())
    {
        // Output each table name.
        System.out.println(table);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-an-entity-tooa-table"></a><span data-ttu-id="9ca4b-132">Способ: добавьте таблицу tooa сущности</span><span class="sxs-lookup"><span data-stu-id="9ca4b-132">How to: Add an entity tooa table</span></span>
<span data-ttu-id="9ca4b-133">Сущности сопоставляют объекты tooJava, используя пользовательский класс, реализующий **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-133">Entities map tooJava objects using a custom class implementing **TableEntity**.</span></span> <span data-ttu-id="9ca4b-134">Для удобства hello **TableServiceEntity** класс реализует **TableEntity** и использует отражение toomap свойства с именем toogetter и задание значения для hello свойства.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-134">For convenience, hello **TableServiceEntity** class implements **TableEntity** and uses reflection toomap properties toogetter and setter methods named for hello properties.</span></span> <span data-ttu-id="9ca4b-135">tooadd таблицу tooa сущности сначала создать класс, определяющий hello свойства сущности.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-135">tooadd an entity tooa table, first create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="9ca4b-136">Hello следующий код определяет класс сущностей, который использует имя клиента hello как ключ строки hello и фамилию в качестве ключа секции hello.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-136">hello following code defines an entity class which uses hello customer's first name as hello row key, and last name as hello partition key.</span></span> <span data-ttu-id="9ca4b-137">Вместе секции и ключом строки идентификации сущности hello hello таблицы.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-137">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="9ca4b-138">Сущности с одинаковым ключом секции могут выполняться быстрее, чем с разными ключами секционирования приветствия.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-138">Entities with hello same partition key can be queried faster than those with different partition keys.</span></span>

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

<span data-ttu-id="9ca4b-139">Табличные операций, включающие сущности, требуют объект **TableOperation** .</span><span class="sxs-lookup"><span data-stu-id="9ca4b-139">Table operations involving entities require a **TableOperation** object.</span></span> <span data-ttu-id="9ca4b-140">Этот объект определяет toobe операции hello выполнена на сущность, которая может выполняться с **CloudTable** объекта.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-140">This object defines hello operation toobe performed on an entity, which can be executed with a **CloudTable** object.</span></span> <span data-ttu-id="9ca4b-141">Hello следующий код создает новый экземпляр hello **CustomerEntity** класса хранимых данных toobe некоторых клиентов система.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-141">hello following code creates a new instance of hello **CustomerEntity** class with some customer data toobe stored.</span></span> <span data-ttu-id="9ca4b-142">Здравствуйте, следующий код вызывает метод **TableOperation.insertOrReplace** toocreate **TableOperation** объекта tooinsert сущность в таблицу, и связывает hello новые **CustomerEntity**с ним.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-142">hello code next calls **TableOperation.insertOrReplace** toocreate a **TableOperation** object tooinsert an entity into a table, and associates hello new **CustomerEntity** with it.</span></span> <span data-ttu-id="9ca4b-143">Наконец, код hello вызывает hello **выполнение** метод hello **CloudTable** указание таблицы «people» hello и новый hello объекта **TableOperation**, которая затем отправляет запрос toohello хранилища службы tooinsert hello новой сущности customer в таблицу «люди» hello, или заменяет сущность hello в том случае, если он уже существует.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-143">Finally, hello code calls hello **execute** method on hello **CloudTable** object, specifying hello "people" table and hello new **TableOperation**, which then sends a request toohello storage service tooinsert hello new customer entity into hello "people" table, or replace hello entity if it already exists.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.setEmail("Walter@contoso.com");
    customer1.setPhoneNumber("425-555-0101");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer1 = TableOperation.insertOrReplace(customer1);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer1);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-a-batch-of-entities"></a><span data-ttu-id="9ca4b-144">Практическое руководство. Вставка пакета сущностей</span><span class="sxs-lookup"><span data-stu-id="9ca4b-144">How to: Insert a batch of entities</span></span>
<span data-ttu-id="9ca4b-145">Пакет службы таблиц toohello сущностей можно вставить в одну операцию записи.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-145">You can insert a batch of entities toohello table service in one write operation.</span></span> <span data-ttu-id="9ca4b-146">Hello следующий код создает **TableBatchOperation** объекта, а затем добавляет три вставить tooit операций.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-146">hello following code creates a **TableBatchOperation** object, then adds three insert operations tooit.</span></span> <span data-ttu-id="9ca4b-147">Каждой операции вставки добавляется путем создания нового объекта сущностей, задание его значения и последующего вызова hello **вставить** метод hello **TableBatchOperation** объекта tooassociate hello сущности с новым операции вставки.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-147">Each insert operation is added by creating a new entity object, setting its values, and then calling hello **insert** method on hello **TableBatchOperation** object tooassociate hello entity with a new insert operation.</span></span> <span data-ttu-id="9ca4b-148">Здравствуйте, затем код вызывает метод **выполнение** на hello **CloudTable** указание таблицы «people» hello и hello объекта **TableBatchOperation** объекта, который отправляет пакет hello таблицы Служба хранилища toohello операций в одном запросе.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-148">Then hello code calls **execute** on hello **CloudTable** object, specifying hello "people" table and hello **TableBatchOperation** object, which sends hello batch of table operations toohello storage service in a single request.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Define a batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a customer entity tooadd toohello table.
    CustomerEntity customer = new CustomerEntity("Smith", "Jeff");
    customer.setEmail("Jeff@contoso.com");
    customer.setPhoneNumber("425-555-0104");
    batchOperation.insertOrReplace(customer);

    // Create another customer entity tooadd toohello table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.setEmail("Ben@contoso.com");
    customer2.setPhoneNumber("425-555-0102");
    batchOperation.insertOrReplace(customer2);

    // Create a third customer entity tooadd toohello table.
    CustomerEntity customer3 = new CustomerEntity("Smith", "Denise");
    customer3.setEmail("Denise@contoso.com");
    customer3.setPhoneNumber("425-555-0103");
    batchOperation.insertOrReplace(customer3);

    // Execute hello batch of operations on hello "people" table.
    cloudTable.execute(batchOperation);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="9ca4b-149">Некоторые действия toonote на пакетные операции:</span><span class="sxs-lookup"><span data-stu-id="9ca4b-149">Some things toonote on batch operations:</span></span>

* <span data-ttu-id="9ca4b-150">Можно выполнять копирование too100 insert, delete, merge, replace, insert или merge и вставки или замены в любой комбинации в одном пакете.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-150">You can perform up too100 insert, delete, merge, replace, insert or merge, and insert or replace operations in any combination in a single batch.</span></span>
* <span data-ttu-id="9ca4b-151">В него входит только операция hello в пакете hello пакетная операция может быть операцией извлечения.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-151">A batch operation can have a retrieve operation, if it is hello only operation in hello batch.</span></span>
* <span data-ttu-id="9ca4b-152">Все сущности в одной пакетной операции должен иметь hello же ключ секционирования.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-152">All entities in a single batch operation must have hello same partition key.</span></span>
* <span data-ttu-id="9ca4b-153">Пакетная операция представляет полезные данные ограниченного tooa 4 МБ.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-153">A batch operation is limited tooa 4MB data payload.</span></span>

## <a name="how-to-retrieve-all-entities-in-a-partition"></a><span data-ttu-id="9ca4b-154">Практическое руководство. Получение всех сущностей в разделе</span><span class="sxs-lookup"><span data-stu-id="9ca4b-154">How to: Retrieve all entities in a partition</span></span>
<span data-ttu-id="9ca4b-155">tooquery таблицы для сущностей из секции, можно использовать **TableQuery**.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-155">tooquery a table for entities in a partition, you can use a **TableQuery**.</span></span> <span data-ttu-id="9ca4b-156">Вызовите **TableQuery.from** toocreate запроса на определенной таблице, которая возвращает тип, заданный результат.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-156">Call **TableQuery.from** toocreate a query on a particular table that returns a specified result type.</span></span> <span data-ttu-id="9ca4b-157">Hello следующий код задает фильтр для сущности, где ключ раздела hello 'Smith'.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-157">hello following code specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="9ca4b-158">**TableQuery.generateFilterCondition** — это вспомогательный метод toocreate фильтры для запросов.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-158">**TableQuery.generateFilterCondition** is a helper method toocreate filters for queries.</span></span> <span data-ttu-id="9ca4b-159">Вызовите **где** hello ссылки, возвращенные hello **TableQuery.from** метод tooapply hello фильтра toohello запроса.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-159">Call **where** on hello reference returned by hello **TableQuery.from** method tooapply hello filter toohello query.</span></span> <span data-ttu-id="9ca4b-160">Если hello запрос выполняется с помощью вызова слишком**выполнение** на hello **CloudTable** он возвращает **итератор** с hello **CustomerEntity**указан тип результата.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-160">When hello query is executed with a call too**execute** on hello **CloudTable** object, it returns an **Iterator** with hello **CustomerEntity** result type specified.</span></span> <span data-ttu-id="9ca4b-161">Затем можно использовать hello **итератор** возвращается в для каждого цикла tooconsume hello результатов.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-161">You can then use hello **Iterator** returned in a for each loop tooconsume hello results.</span></span> <span data-ttu-id="9ca4b-162">Этот код выводит hello поля в каждой сущности в консоли toohello результаты запроса hello.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-162">This code prints hello fields of each entity in hello query results toohello console.</span></span>

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

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Specify a partition query, using "Smith" as hello partition key filter.
    TableQuery<CustomerEntity> partitionQuery =
        TableQuery.from(CustomerEntity.class)
        .where(partitionFilter);

    // Loop through hello results, displaying information about hello entity.
    for (CustomerEntity entity : cloudTable.execute(partitionQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="9ca4b-163">Практическое руководство. Получение диапазона сущностей в разделе</span><span class="sxs-lookup"><span data-stu-id="9ca4b-163">How to: Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="9ca4b-164">Если вы не хотите tooquery все сущности hello в секции, можно указать диапазон с помощью операторов сравнения в фильтре.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-164">If you don't want tooquery all hello entities in a partition, you can specify a range by using comparison operators in a filter.</span></span> <span data-ttu-id="9ca4b-165">Здравствуйте, следующий код объединяет два фильтрует tooget всех сущностей в разделе «Smith» где ключ строки hello (имя) начинается с буквы вверх too'E "hello алфавита.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-165">hello following code combines two filters tooget all entities in partition "Smith" where hello row key (first name) starts with a letter up too'E' in hello alphabet.</span></span> <span data-ttu-id="9ca4b-166">Затем он выводит результаты запроса hello.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-166">Then it prints hello query results.</span></span> <span data-ttu-id="9ca4b-167">При использовании таблицы добавлены toohello hello сущностей в пакете hello вставить данного руководства, возвращаются только две сущности, это время (Бен и Юлия Smith); Джефф Smith не включается.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-167">If you use hello entities added toohello table in hello batch insert section of this guide, only two entities are returned this time (Ben and Denise Smith); Jeff Smith is not included.</span></span>

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

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Create a filter condition where hello row key is less than hello letter "E".
    String rowFilter = TableQuery.generateFilterCondition(
        ROW_KEY,
        QueryComparisons.LESS_THAN,
        "E");

    // Combine hello two conditions into a filter expression.
    String combinedFilter = TableQuery.combineFilters(partitionFilter,
        Operators.AND, rowFilter);

    // Specify a range query, using "Smith" as hello partition key,
    // with hello row key being up toohello letter "E".
    TableQuery<CustomerEntity> rangeQuery =
        TableQuery.from(CustomerEntity.class)
        .where(combinedFilter);

    // Loop through hello results, displaying information about hello entity
    for (CustomerEntity entity : cloudTable.execute(rangeQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-single-entity"></a><span data-ttu-id="9ca4b-168">Практическое руководство. Извлечение одной сущности</span><span class="sxs-lookup"><span data-stu-id="9ca4b-168">How to: Retrieve a single entity</span></span>
<span data-ttu-id="9ca4b-169">Можно написать tooretrieve запроса конкретную сущность.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-169">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="9ca4b-170">Hello следующий код вызывает **TableOperation.retrieve** с секции ключ и строку параметров ключа toospecify hello клиентом «Джефф Smith», вместо создания **TableQuery** и использование фильтров toodo hello одинаково.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-170">hello following code calls **TableOperation.retrieve** with partition key and row key parameters toospecify hello customer "Jeff Smith", instead of creating a **TableQuery** and using filters toodo hello same thing.</span></span> <span data-ttu-id="9ca4b-171">Во время выполнения получить hello, операция возвращает только одну сущность, а не коллекцию.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-171">When executed, hello retrieve operation returns just one entity, rather than a collection.</span></span> <span data-ttu-id="9ca4b-172">Hello **getResultAsType** метод приводит hello результат toohello тип цели назначения hello, **CustomerEntity** объекта.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-172">hello **getResultAsType** method casts hello result toohello type of hello assignment target, a **CustomerEntity** object.</span></span> <span data-ttu-id="9ca4b-173">Если этот тип несовместим с типом hello hello запросе указано, будет вызвано исключение.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-173">If this type is not compatible with hello type specified for hello query, an exception will be thrown.</span></span> <span data-ttu-id="9ca4b-174">Значение NULL возвращается, если ни одна сущность не подходит по ключам раздела и строки.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-174">A null value is returned if no entity has an exact partition and row key match.</span></span> <span data-ttu-id="9ca4b-175">Указание ключи секций и строк в запросе является hello самый быстрый способ tooretrieve одной сущности из службы таблиц hello.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-175">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff"
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Output hello entity.
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
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-modify-an-entity"></a><span data-ttu-id="9ca4b-176">Практическое руководство. Изменение сущности</span><span class="sxs-lookup"><span data-stu-id="9ca4b-176">How to: Modify an entity</span></span>
<span data-ttu-id="9ca4b-177">toomodify сущности, получить его из службы таблиц hello, сделать объект сущности toohello изменения и сохранить изменения hello задней toohello службы таблиц с помощью операции слияния или замены.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-177">toomodify an entity, retrieve it from hello table service, make changes toohello entity object, and save hello changes back toohello table service with a replace or merge operation.</span></span> <span data-ttu-id="9ca4b-178">Hello следующий код позволяет изменить номер телефона существующего клиента.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-178">hello following code changes an existing customer's phone number.</span></span> <span data-ttu-id="9ca4b-179">Вместо вызова метода **TableOperation.insert** как мы делали tooinsert, этот код вызывает **TableOperation.replace**.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-179">Instead of calling **TableOperation.insert** like we did tooinsert, this code calls **TableOperation.replace**.</span></span> <span data-ttu-id="9ca4b-180">Hello **CloudTable.execute** метод вызывает службу hello таблицы и сущности hello заменяется первоначально другое приложение его hello времени с момента получения данного приложения, его.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-180">hello **CloudTable.execute** method calls hello table service, and hello entity is replaced, unless another application changed it in hello time since this application retrieved it.</span></span> <span data-ttu-id="9ca4b-181">Когда это происходит, возникает исключение и hello сущности необходимо извлечь, изменения и снова сохранить.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-181">When that happens, an exception is thrown, and hello entity must be retrieved, modified, and saved again.</span></span> <span data-ttu-id="9ca4b-182">Этот оптимистичный шаблон повторения в случае конфликтов широко применяется в системе распределенного хранения.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-182">This optimistic concurrency retry pattern is common in a distributed storage system.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Specify a new phone number.
    specificEntity.setPhoneNumber("425-555-0105");

    // Create an operation tooreplace hello entity.
    TableOperation replaceEntity = TableOperation.replace(specificEntity);

    // Submit hello operation toohello table service.
    cloudTable.execute(replaceEntity);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-query-a-subset-of-entity-properties"></a><span data-ttu-id="9ca4b-183">Практическое руководство. Запрос подмножества свойств сущности</span><span class="sxs-lookup"><span data-stu-id="9ca4b-183">How to: Query a subset of entity properties</span></span>
<span data-ttu-id="9ca4b-184">Таблицы tooa запроса можно получить только несколько свойств сущности.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-184">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="9ca4b-185">Этот метод, который называется "проекцией", снижает потребление пропускной способности и может повысить производительность запросов, особенно для крупных сущностей.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-185">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="9ca4b-186">Hello запрос в hello, следующий код использует hello **выберите** метод tooreturn только hello адреса электронной почты сущности в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-186">hello query in hello following code uses hello **select** method tooreturn only hello email addresses of entities in hello table.</span></span> <span data-ttu-id="9ca4b-187">Hello результаты проецируются в коллекцию **строка** с помощью hello **EntityResolver**, который does hello преобразование типов сущностей hello, возвращенный от сервера hello.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-187">hello results are projected into a collection of **String** with hello help of an **EntityResolver**, which does hello type conversion on hello entities returned from hello server.</span></span> <span data-ttu-id="9ca4b-188">Дополнительные сведения о проекции см. в записи блога [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection] (Таблицы Azure: введение в Upsert и проекции в запросах).</span><span class="sxs-lookup"><span data-stu-id="9ca4b-188">You can learn more about projection in [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span> <span data-ttu-id="9ca4b-189">Обратите внимание, что проекции не поддерживается эмуляторе hello локального хранилища, поэтому этот код выполняется только при использовании учетной записи для службы таблиц hello.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-189">Note that projection is not supported on hello local storage emulator, so this code runs only when using an account on hello table service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Define a projection query that retrieves only hello Email property
    TableQuery<CustomerEntity> projectionQuery =
        TableQuery.from(CustomerEntity.class)
        .select(new String[] {"Email"});

    // Define a Entity resolver tooproject hello entity toohello Email value.
    EntityResolver<String> emailResolver = new EntityResolver<String>() {
        @Override
        public String resolve(String PartitionKey, String RowKey, Date timeStamp, HashMap<String, EntityProperty> properties, String etag) {
            return properties.get("Email").getValueAsString();
        }
    };

    // Loop through hello results, displaying hello Email values.
    for (String projectedString :
        cloudTable.execute(projectionQuery, emailResolver)) {
            System.out.println(projectedString);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-or-replace-an-entity"></a><span data-ttu-id="9ca4b-190">Как вставлять и заменять сущности</span><span class="sxs-lookup"><span data-stu-id="9ca4b-190">How to: Insert or Replace an entity</span></span>
<span data-ttu-id="9ca4b-191">Часто возникает необходимость tooadd tooa сущности таблицы, не зная, если он уже существует в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-191">Often you want tooadd an entity tooa table without knowing if it already exists in hello table.</span></span> <span data-ttu-id="9ca4b-192">Операция вставки или замены позволяет toomake одного запроса, который будет вставлять hello сущности, если он не существует, или замените hello один существующий, если он не.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-192">An insert-or-replace operation allows you toomake a single request which will insert hello entity if it does not exist or replace hello existing one if it does.</span></span> <span data-ttu-id="9ca4b-193">Основываясь на предыдущих примерах, hello следующий код вставляет или заменяет сущность hello для «Уолтер Harp».</span><span class="sxs-lookup"><span data-stu-id="9ca4b-193">Building on prior examples, hello following code inserts or replaces hello entity for "Walter Harp".</span></span> <span data-ttu-id="9ca4b-194">После создания новой сущности, этот код вызывает hello **TableOperation.insertOrReplace** метод.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-194">After creating a new entity, this code calls hello **TableOperation.insertOrReplace** method.</span></span> <span data-ttu-id="9ca4b-195">Затем этот код вызывает **выполнение** на hello **CloudTable** объекта с помощью вставки таблицы и hello hello или заменить таблицу операцию, так как параметры hello.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-195">This code then calls **execute** on hello **CloudTable** object with hello table and hello insert or replace table operation as hello parameters.</span></span> <span data-ttu-id="9ca4b-196">в сущности, tooupdate hello **TableOperation.insertOrMerge** можно метода.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-196">tooupdate only part of an entity, hello **TableOperation.insertOrMerge** method can be used instead.</span></span> <span data-ttu-id="9ca4b-197">Обратите внимание, что вставки или replace не поддерживается на эмулятор локального хранилища hello, поэтому этот код выполняется только при использовании учетной записи для службы таблиц hello.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-197">Note that insert-or-replace is not supported on hello local storage emulator, so this code runs only when using an account on hello table service.</span></span> <span data-ttu-id="9ca4b-198">Дополнительные сведения об операциях "вставка или замена" и "вставка или объединение" см. в записи блога [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection] (Таблицы Azure: введение в Upsert и проекции в запросах).</span><span class="sxs-lookup"><span data-stu-id="9ca4b-198">You can learn more about insert-or-replace and insert-or-merge in this [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer5 = new CustomerEntity("Harp", "Walter");
    customer5.setEmail("Walter@contoso.com");
    customer5.setPhoneNumber("425-555-0106");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer5 = TableOperation.insertOrReplace(customer5);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer5);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-an-entity"></a><span data-ttu-id="9ca4b-199">Практическое руководство. Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="9ca4b-199">How to: Delete an entity</span></span>
<span data-ttu-id="9ca4b-200">Сущность можно легко удалить после ее получения.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-200">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="9ca4b-201">Когда извлекается hello объекта, вызовите **TableOperation.delete** с toodelete hello сущности.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-201">Once hello entity is retrieved, call **TableOperation.delete** with hello entity toodelete.</span></span> <span data-ttu-id="9ca4b-202">Затем вызовите **выполнение** на hello **CloudTable** объекта.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-202">Then call **execute** on hello **CloudTable** object.</span></span> <span data-ttu-id="9ca4b-203">Привет, следующий код извлекает и удаляет сущность «клиент».</span><span class="sxs-lookup"><span data-stu-id="9ca4b-203">hello following code retrieves and deletes a customer entity.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff = TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    CustomerEntity entitySmithJeff =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Create an operation toodelete hello entity.
    TableOperation deleteSmithJeff = TableOperation.delete(entitySmithJeff);

    // Submit hello delete operation toohello table service.
    cloudTable.execute(deleteSmithJeff);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-table"></a><span data-ttu-id="9ca4b-204">Практическое руководство. Удаление таблицы</span><span class="sxs-lookup"><span data-stu-id="9ca4b-204">How to: Delete a table</span></span>
<span data-ttu-id="9ca4b-205">Наконец, hello следующий код удаляет таблицы из учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-205">Finally, hello following code deletes a table from a storage account.</span></span> <span data-ttu-id="9ca4b-206">Таблицы, который был удален будет недоступным toobe повторно в течение заданного времени, после удаления hello, обычно менее 40 секунд.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-206">A table which has been deleted will be unavailable toobe recreated for a period of time following hello deletion, usually less than forty seconds.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Delete hello table and all its data if it exists.
    CloudTable cloudTable = tableClient.getTableReference("people");
    cloudTable.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```
[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="next-steps"></a><span data-ttu-id="9ca4b-207">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9ca4b-207">Next steps</span></span>

* <span data-ttu-id="9ca4b-208">[Обозреватель хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) является бесплатной, отдельное приложение от Майкрософт, позволяющая toowork визуально с помощью данных из хранилища Azure в Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="9ca4b-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="9ca4b-209">[Пакет SDK службы хранилища Azure для Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="9ca4b-209">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="9ca4b-210">[Azure SDK Справочник по клиентской хранилища][Azure SDK Справочник по клиентской хранилища]</span><span class="sxs-lookup"><span data-stu-id="9ca4b-210">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="9ca4b-211">[REST API службы хранилища Azure][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="9ca4b-211">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="9ca4b-212">[Блог рабочей группы службы хранилища Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="9ca4b-212">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="9ca4b-213">Дополнительные сведения см. в разделе [Azure for Java developers](/java/azure) (Azure для разработчиков Java).</span><span class="sxs-lookup"><span data-stu-id="9ca4b-213">For more information, visit [Azure for Java developers](/java/azure).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure SDK Справочник по клиентской хранилища]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
