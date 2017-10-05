---
title: "Использование хранилища таблиц (C++) | Документация Майкрософт"
description: "Хранение структурированных данных в облаке в хранилище таблиц Azure (хранилище данных NoSQL)."
services: storage
documentationcenter: .net
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: f191f308-e4b2-4de9-85cb-551b82b1ea7c
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: d68843153921c72f6e808f62e82d3686c7e2f160
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-table-storage-from-c"></a><span data-ttu-id="183e6-103">Использование табличного хранилища из C++</span><span class="sxs-lookup"><span data-stu-id="183e6-103">How to use Table storage from C++</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="183e6-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="183e6-104">Overview</span></span>
<span data-ttu-id="183e6-105">В этом руководстве показано, как реализовать типичные сценарии с использованием службы табличного хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="183e6-105">This guide will show you how to perform common scenarios by using the Azure Table storage service.</span></span> <span data-ttu-id="183e6-106">Примеры написаны на C++ и используют [клиентскую библиотеку хранилища Azure для C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="183e6-106">The samples are written in C++ and use the [Azure Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="183e6-107">Здесь описаны такие сценарии, как **создание и удаление таблицы**, а также **работа с сущностями таблиц**.</span><span class="sxs-lookup"><span data-stu-id="183e6-107">The scenarios covered include **creating and deleting a table** and **working with table entities**.</span></span>

> [!NOTE]
> <span data-ttu-id="183e6-108">Данное руководство предназначено для клиентской библиотеки хранилища Azure для С++ версии 1.0.0 и выше.</span><span class="sxs-lookup"><span data-stu-id="183e6-108">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="183e6-109">Рекомендуемая версия клиентской библиотеки хранилища — 2.2.0. Она доступна на сайте [NuGet](http://www.nuget.org/packages/wastorage) или [GitHub](https://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="183e6-109">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="183e6-110">Создание приложения на C++</span><span class="sxs-lookup"><span data-stu-id="183e6-110">Create a C++ application</span></span>
<span data-ttu-id="183e6-111">В этом руководстве будут использоваться компоненты хранилища, которые могут выполняться в приложениях на C++.</span><span class="sxs-lookup"><span data-stu-id="183e6-111">In this guide, you will use storage features that can be run within a C++ application.</span></span> <span data-ttu-id="183e6-112">Для этого необходимо установить клиентскую библиотеку хранилища Azure для C++ и создать учетную запись хранения Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="183e6-112">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>  

<span data-ttu-id="183e6-113">Чтобы установить клиентскую библиотеку хранилища для C++, можно использовать следующие методы.</span><span class="sxs-lookup"><span data-stu-id="183e6-113">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="183e6-114">**Linux:** следуйте инструкциям, указанным на странице [README клиентской библиотеки службы хранилища Azure для C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) .</span><span class="sxs-lookup"><span data-stu-id="183e6-114">**Linux:** Follow the instructions given on the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="183e6-115">**Windows:** в Visual Studio нажмите **Инструменты > Диспетчер пакетов NuGet > Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="183e6-115">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="183e6-116">Введите следующую команду в [консоли диспетчера пакетов NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="183e6-116">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press Enter.</span></span>  
  
     <span data-ttu-id="183e6-117">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="183e6-117">Install-Package wastorage</span></span>

## <a name="configure-your-application-to-access-table-storage"></a><span data-ttu-id="183e6-118">Настройка приложения для доступа к хранилищу таблиц</span><span class="sxs-lookup"><span data-stu-id="183e6-118">Configure your application to access Table storage</span></span>
<span data-ttu-id="183e6-119">Добавьте следующие инструкции в начало файла C++, где требуется использовать API-интерфейсы хранилища Azure для доступа к таблицам.</span><span class="sxs-lookup"><span data-stu-id="183e6-119">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access tables:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="183e6-120">Настройка строки подключения к хранилищу Azure</span><span class="sxs-lookup"><span data-stu-id="183e6-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="183e6-121">Клиент хранилища Azure использует строку подключения с целью хранения конечных точек и учетных данных для доступа к службам управления данными.</span><span class="sxs-lookup"><span data-stu-id="183e6-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="183e6-122">При запуске клиентского приложения необходимо указать строку подключения к хранилищу в указанном формате.</span><span class="sxs-lookup"><span data-stu-id="183e6-122">When running a client application, you must provide the storage connection string in the following format.</span></span> <span data-ttu-id="183e6-123">Для значений *AccountName* и *AccountKey* используйте имя учетной записи хранения и ключ доступа к хранилищу, которые соответствуют учетной записи хранения и указаны на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="183e6-123">Use the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="183e6-124">Сведения об учетных записях хранения и ключах доступа см. в статье [Об учетных записях хранения Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="183e6-124">For information on storage accounts and access keys, see [About Azure storage accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="183e6-125">В этом примере показано, как объявить статическое поле для размещения строки подключения:</span><span class="sxs-lookup"><span data-stu-id="183e6-125">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="183e6-126">Чтобы протестировать приложение на локальном компьютере с Windows, можно использовать [эмулятор хранения](storage-use-emulator.md) Azure, устанавливаемый с [пакетом Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="183e6-126">To test your application in your local Windows-based computer, you can use the Azure [storage emulator](storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="183e6-127">Эмулятор хранения — это служебная программа, моделирующая службы больших двоичных объектов, очередей и таблиц, которые доступны в Azure на локальном компьютере разработки.</span><span class="sxs-lookup"><span data-stu-id="183e6-127">The storage emulator is a utility that simulates the Azure Blob, Queue, and Table services available on your local development machine.</span></span> <span data-ttu-id="183e6-128">В следующем примере показано, как объявить статическое поле для размещения строки подключения для эмулятора локального хранилища.</span><span class="sxs-lookup"><span data-stu-id="183e6-128">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>  

```cpp
// Define the connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="183e6-129">Чтобы запустить эмулятор хранения Azure, нажмите кнопку **Пуск** или клавишу Windows.</span><span class="sxs-lookup"><span data-stu-id="183e6-129">To start the Azure storage emulator, click the **Start** button or press the Windows key.</span></span> <span data-ttu-id="183e6-130">Начните вводить **эмулятор хранения Azure**, а затем выберите **Эмулятор хранения Microsoft Azure** из списка приложений.</span><span class="sxs-lookup"><span data-stu-id="183e6-130">Begin typing **Azure Storage Emulator**, and then select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>  

<span data-ttu-id="183e6-131">В приведенных ниже примерах предполагается, что вы использовали одно из этих двух определений для получения строки подключения к хранилищу.</span><span class="sxs-lookup"><span data-stu-id="183e6-131">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="183e6-132">Получить строку подключения</span><span class="sxs-lookup"><span data-stu-id="183e6-132">Retrieve your connection string</span></span>
<span data-ttu-id="183e6-133">Информацию о своей учетной записи хранения можно представить с помощью класса **cloud_storage_account**.</span><span class="sxs-lookup"><span data-stu-id="183e6-133">You can use the **cloud_storage_account** class to represent your storage account information.</span></span> <span data-ttu-id="183e6-134">Чтобы получить данные учетной записи хранения из строки подключения хранилища, можно использовать метод синтаксического анализа.</span><span class="sxs-lookup"><span data-stu-id="183e6-134">To retrieve your storage account information from the storage connection string, you can use the parse method.</span></span>

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="183e6-135">Затем получите ссылку на класс **cloud_table_client**. Он дает возможность извлечь эталонные объекты для таблиц и сущностей, которые хранятся в службе хранилища таблиц.</span><span class="sxs-lookup"><span data-stu-id="183e6-135">Next, get a reference to a **cloud_table_client** class, as it lets you get reference objects for tables and entities stored within the Table storage service.</span></span> <span data-ttu-id="183e6-136">Следующий код создает объект **cloud_table_client** с помощью объекта учетной записи хранения, полученного выше:</span><span class="sxs-lookup"><span data-stu-id="183e6-136">The following code creates a **cloud_table_client** object by using the storage account object we retrieved above:</span></span>  

```cpp
// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a><span data-ttu-id="183e6-137">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="183e6-137">Create a table</span></span>
<span data-ttu-id="183e6-138">Объект **cloud_table_client** позволяет получить эталонные объекты для таблиц и сущностей.</span><span class="sxs-lookup"><span data-stu-id="183e6-138">A **cloud_table_client** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="183e6-139">Следующий код создает объект **cloud_table_client** и использует его для создания таблицы.</span><span class="sxs-lookup"><span data-stu-id="183e6-139">The following code creates a **cloud_table_client** object and uses it to create a new table.</span></span>

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference to a table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="183e6-140">Добавление сущности в таблицу</span><span class="sxs-lookup"><span data-stu-id="183e6-140">Add an entity to a table</span></span>
<span data-ttu-id="183e6-141">Чтобы добавить сущность в таблицу, создайте объект **table_entity** и передайте его в **table_operation::insert_entity**.</span><span class="sxs-lookup"><span data-stu-id="183e6-141">To add an entity to a table, create a new **table_entity** object and pass it to **table_operation::insert_entity**.</span></span> <span data-ttu-id="183e6-142">Следующий код использует имя пользователя в качестве ключа строки, а фамилию клиента — как ключ раздела.</span><span class="sxs-lookup"><span data-stu-id="183e6-142">The following code uses the customer's first name as the row key and last name as the partition key.</span></span> <span data-ttu-id="183e6-143">Вместе ключ раздела и ключ строки сущности уникальным образом идентифицируют сущность в таблице.</span><span class="sxs-lookup"><span data-stu-id="183e6-143">Together, an entity's partition and row key uniquely identify the entity in the table.</span></span> <span data-ttu-id="183e6-144">Сущности с одинаковым ключом раздела можно запрашиваться быстрее, чем с разными ключами раздела, но использование различных ключей разделов обеспечивает более высокую масштабируемость параллельных операций.</span><span class="sxs-lookup"><span data-stu-id="183e6-144">Entities with the same partition key can be queried faster than those with different partition keys, but using diverse partition keys allows for greater parallel operation scalability.</span></span> <span data-ttu-id="183e6-145">Дополнительные сведения см. в статье [Производительность хранилища Microsoft Azure и контрольный список масштабируемости](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="183e6-145">For more information, see [Microsoft Azure storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<span data-ttu-id="183e6-146">Следующий код создает новый экземпляр **table_entity** с подлежащими сохранению данными клиента.</span><span class="sxs-lookup"><span data-stu-id="183e6-146">The following code creates a new instance of **table_entity** with some customer data to be stored.</span></span> <span data-ttu-id="183e6-147">Затем код вызывает **table_operation::insert_entity** в целях создания объекта **table_operation** для вставки сущности в таблицу и связывает с ним новую сущность таблицы.</span><span class="sxs-lookup"><span data-stu-id="183e6-147">The code next calls **table_operation::insert_entity** to create a **table_operation** object to insert an entity into a table, and associates the new table entity with it.</span></span> <span data-ttu-id="183e6-148">В завершение код вызывает метод Execute для объекта **cloud_table**.</span><span class="sxs-lookup"><span data-stu-id="183e6-148">Finally, the code calls the execute method on the **cloud_table** object.</span></span> <span data-ttu-id="183e6-149">Новый объект **table_operation** отправляет запрос в службу таблиц для вставки сущности нового клиента в таблицу пользователей.</span><span class="sxs-lookup"><span data-stu-id="183e6-149">And the new **table_operation** sends a request to the Table service to insert the new customer entity into the "people" table.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference to a table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create the table operation that inserts the customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute the insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="183e6-150">Вставка пакета сущностей</span><span class="sxs-lookup"><span data-stu-id="183e6-150">Insert a batch of entities</span></span>
<span data-ttu-id="183e6-151">Вы можете вставить пакет сущностей в службу таблиц за одну операцию записи.</span><span class="sxs-lookup"><span data-stu-id="183e6-151">You can insert a batch of entities to the Table service in one write operation.</span></span> <span data-ttu-id="183e6-152">Следующий код создает объект **table_batch_operation**, а затем добавляет в него три операции вставки.</span><span class="sxs-lookup"><span data-stu-id="183e6-152">The following code creates a **table_batch_operation** object, and then adds three insert operations to it.</span></span> <span data-ttu-id="183e6-153">Каждая операция вставки добавляется путем создания нового объекта сущности, установки его значений и последующего вызова метода вставки для объекта **table_batch_operation**, чтобы связать сущность с новой операцией вставки.</span><span class="sxs-lookup"><span data-stu-id="183e6-153">Each insert operation is added by creating a new entity object, setting its values, and then calling the insert method on the **table_batch_operation** object to associate the entity with a new insert operation.</span></span> <span data-ttu-id="183e6-154">Затем вызывается метод **cloud_table.execute** для выполнения операции.</span><span class="sxs-lookup"><span data-stu-id="183e6-154">Then, **cloud_table.execute** is called to execute the operation.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it to the table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it to the table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity to add to the table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities to the batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute the batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

<span data-ttu-id="183e6-155">Некоторые другие примечания к пакетным операциям:</span><span class="sxs-lookup"><span data-stu-id="183e6-155">Some things to note on batch operations:</span></span>  

* <span data-ttu-id="183e6-156">В отдельном пакете можно выполнить до 100 операций вставки, удаления, объединения, замены, вставки или слияния и вставки или замены в любом сочетании.</span><span class="sxs-lookup"><span data-stu-id="183e6-156">You can perform up to 100 insert, delete, merge, replace, insert-or-merge, and insert-or-replace operations in any combination in a single batch.</span></span>  
* <span data-ttu-id="183e6-157">Пакетная операция может иметь операцию извлечения, если она является единственной операцией в пакете.</span><span class="sxs-lookup"><span data-stu-id="183e6-157">A batch operation can have a retrieve operation, if it is the only operation in the batch.</span></span>  
* <span data-ttu-id="183e6-158">У всех сущностей в одной пакетной операции должен быть одинаковый ключ раздела.</span><span class="sxs-lookup"><span data-stu-id="183e6-158">All entities in a single batch operation must have the same partition key.</span></span>  
* <span data-ttu-id="183e6-159">Максимальный объем полезных данных пакетной операции составляет 4 МБ.</span><span class="sxs-lookup"><span data-stu-id="183e6-159">A batch operation is limited to a 4-MB data payload.</span></span>  

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="183e6-160">Получение всех сущностей в разделе</span><span class="sxs-lookup"><span data-stu-id="183e6-160">Retrieve all entities in a partition</span></span>
<span data-ttu-id="183e6-161">Чтобы запросить таблицу для всех сущностей в разделе, используйте объект **table_query**.</span><span class="sxs-lookup"><span data-stu-id="183e6-161">To query a table for all entities in a partition, use a **table_query** object.</span></span> <span data-ttu-id="183e6-162">Следующий пример кода задает фильтр для сущностей с ключом раздела "Smith".</span><span class="sxs-lookup"><span data-stu-id="183e6-162">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="183e6-163">Этот пример выводит на консоль поля каждой сущности в результатах запроса.</span><span class="sxs-lookup"><span data-stu-id="183e6-163">This example prints the fields of each entity in the query results to the console.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct the query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print the fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

<span data-ttu-id="183e6-164">В этом примере запрос отображает все сущности, соответствующие условиям фильтра.</span><span class="sxs-lookup"><span data-stu-id="183e6-164">The query in this example brings all the entities that match the filter criteria.</span></span> <span data-ttu-id="183e6-165">При наличии больших таблиц и необходимости часто загружать сущности таблицы мы рекомендуем хранить данные в хранилище BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="183e6-165">If you have large tables and need to download the table entities often, we recommend that you store your data in Azure storage blobs instead.</span></span>

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="183e6-166">Получение диапазона сущностей в разделе</span><span class="sxs-lookup"><span data-stu-id="183e6-166">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="183e6-167">Если вы не хотите запрашивать все сущности в разделе, можно указать диапазон, объединив фильтр ключа раздела с фильтром ключа строк.</span><span class="sxs-lookup"><span data-stu-id="183e6-167">If you don't want to query all the entities in a partition, you can specify a range by combining the partition key filter with a row key filter.</span></span> <span data-ttu-id="183e6-168">В следующем примере кода используются два фильтра для получения всех сущностей в разделе Smith, где ключ строки (имя) начинается с первой буквы алфавита до буквы E, после чего результаты запроса выводятся в консоль.</span><span class="sxs-lookup"><span data-stu-id="183e6-168">The following code example uses two filters to get all entities in partition 'Smith' where the row key (first name) starts with a letter earlier than 'E' in the alphabet and then prints the query results.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through the results, displaying information about the entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="183e6-169">Извлечение одной сущности</span><span class="sxs-lookup"><span data-stu-id="183e6-169">Retrieve a single entity</span></span>
<span data-ttu-id="183e6-170">Можно написать запрос для получения отдельной сущности.</span><span class="sxs-lookup"><span data-stu-id="183e6-170">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="183e6-171">Код ниже использует **table_operation::retrieve_entity** для указания клиента Jeff Smith.</span><span class="sxs-lookup"><span data-stu-id="183e6-171">The following code uses **table_operation::retrieve_entity** to specify the customer 'Jeff Smith'.</span></span> <span data-ttu-id="183e6-172">Данный метод возвращает только одну сущность, а не множество, и возвращенное значение находится в **table_result**.</span><span class="sxs-lookup"><span data-stu-id="183e6-172">This method returns just one entity, rather than a collection, and the returned value is in **table_result**.</span></span> <span data-ttu-id="183e6-173">Указание ключа раздела и ключа строки в запросе — самый быстрый способ извлечь одну сущность из службы таблиц.</span><span class="sxs-lookup"><span data-stu-id="183e6-173">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve the entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output the entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a><span data-ttu-id="183e6-174">Замена сущности</span><span class="sxs-lookup"><span data-stu-id="183e6-174">Replace an entity</span></span>
<span data-ttu-id="183e6-175">Чтобы заменить сущность, извлеките ее из службы таблиц и измените объект сущности, а затем сохраните изменения в службе таблиц.</span><span class="sxs-lookup"><span data-stu-id="183e6-175">To replace an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="183e6-176">Следующий код изменяет существующий номер телефона и адрес электронной почты клиента.</span><span class="sxs-lookup"><span data-stu-id="183e6-176">The following code changes an existing customer's phone number and email address.</span></span> <span data-ttu-id="183e6-177">Вместо вызова метода **table_operation::insert_entity** этот код использует **table_operation::replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="183e6-177">Instead of calling **table_operation::insert_entity**, this code uses **table_operation::replace_entity**.</span></span> <span data-ttu-id="183e6-178">Из-за этого сущность будет полностью заменена на сервере, если только сущность на сервере не была изменена с момента извлечения. В подобном случае операция не будет выполнена.</span><span class="sxs-lookup"><span data-stu-id="183e6-178">This causes the entity to be fully replaced on the server, unless the entity on the server has changed since it was retrieved, in which case the operation will fail.</span></span> <span data-ttu-id="183e6-179">Это необходимо, чтобы приложение случайно не перезаписало изменения, внесенные с момента извлечения до обновления другим компонентом приложения.</span><span class="sxs-lookup"><span data-stu-id="183e6-179">This failure is to prevent your application from inadvertently overwriting a change made between the retrieval and update by another component of your application.</span></span> <span data-ttu-id="183e6-180">Правильным методом устранения этой ошибки является повторное извлечение объекта, внесение необходимых изменений (если они еще действительны) и затем выполнение еще одной операции **table_operation::replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="183e6-180">The proper handling of this failure is to retrieve the entity again, make your changes (if still valid), and then perform another **table_operation::replace_entity** operation.</span></span> <span data-ttu-id="183e6-181">Ниже показано, как изменить это поведение.</span><span class="sxs-lookup"><span data-stu-id="183e6-181">The next section will show you how to override this behavior.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation to replace the entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit the operation to the Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="183e6-182">Вставка или замена сущности</span><span class="sxs-lookup"><span data-stu-id="183e6-182">Insert-or-replace an entity</span></span>
<span data-ttu-id="183e6-183">Операции **table_operation::replace_entity** завершатся ошибкой, если сущность была изменена с момента ее получения с сервера.</span><span class="sxs-lookup"><span data-stu-id="183e6-183">**table_operation::replace_entity** operations will fail if the entity has been changed since it was retrieved from the server.</span></span> <span data-ttu-id="183e6-184">Кроме того, для успешного выполнения действия **table_operation::replace_entity** необходимо сначала извлечь сущность с сервера.</span><span class="sxs-lookup"><span data-stu-id="183e6-184">Furthermore, you must retrieve the entity from the server first in order for **table_operation::replace_entity** to be successful.</span></span> <span data-ttu-id="183e6-185">Но иногда неизвестно, существует ли сущность на сервере и актуальны ли хранящиеся в ней значения. Обновление должно перезаписать их все.</span><span class="sxs-lookup"><span data-stu-id="183e6-185">Sometimes, however, you don't know if the entity exists on the server and the current values stored in it are irrelevant—your update should overwrite them all.</span></span> <span data-ttu-id="183e6-186">Для этого используйте операцию **table_operation::insert_or_replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="183e6-186">To accomplish this, you would use a **table_operation::insert_or_replace_entity** operation.</span></span> <span data-ttu-id="183e6-187">Эта операция вставляет сущность, если она не существует, или заменяет ее, если она существует, независимо от того, когда было выполнено последнее обновление.</span><span class="sxs-lookup"><span data-stu-id="183e6-187">This operation inserts the entity if it doesn't exist, or replaces it if it does, regardless of when the last update was made.</span></span> <span data-ttu-id="183e6-188">В примере кода ниже сущность клиента для Jeff Smith все равно извлекается, но затем она сохраняется на сервере с помощью операции **table_operation::insert_or_replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="183e6-188">In the following code example, the customer entity for Jeff Smith is still retrieved, but it is then saved back to the server via **table_operation::insert_or_replace_entity**.</span></span> <span data-ttu-id="183e6-189">Любые обновления сущности, внесенные между операциями извлечения и обновления, будут перезаписаны.</span><span class="sxs-lookup"><span data-stu-id="183e6-189">Any updates made to the entity between the retrieval and update operation will be overwritten.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation to insert-or-replace the entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit the operation to the Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="183e6-190">Запрос подмножества свойств сущности</span><span class="sxs-lookup"><span data-stu-id="183e6-190">Query a subset of entity properties</span></span>
<span data-ttu-id="183e6-191">Запрос к таблице может получить лишь несколько свойств сущности.</span><span class="sxs-lookup"><span data-stu-id="183e6-191">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="183e6-192">Запрос в следующем коде использует метод **table_query::set_select_columns**, чтобы возвратить только адреса электронной почты сущностей в таблице.</span><span class="sxs-lookup"><span data-stu-id="183e6-192">The query in the following code uses the **table_query::set_select_columns** method to return only the email addresses of entities in the table.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define the query, and select only the Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display the results.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key();

    const azure::storage::table_entity::properties_type& properties = it->properties();
    for (auto prop_it = properties.begin(); prop_it != properties.end(); ++prop_it)
    {
        std::wcout << ", " << prop_it->first << ": " << prop_it->second.str();
    }

    std::wcout << std::endl;
}
```

> [!NOTE]
> <span data-ttu-id="183e6-193">Запрос нескольких свойств сущности является более эффективной операцией, чем запрос всех свойств.</span><span class="sxs-lookup"><span data-stu-id="183e6-193">Querying a few properties from an entity is a more efficient operation than retrieving all properties.</span></span>
> 
> 

## <a name="delete-an-entity"></a><span data-ttu-id="183e6-194">Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="183e6-194">Delete an entity</span></span>
<span data-ttu-id="183e6-195">Сущность можно легко удалить после ее получения.</span><span class="sxs-lookup"><span data-stu-id="183e6-195">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="183e6-196">После получения сущности вызовите **table_operation::delete_entity** с подлежащей удалению сущности.</span><span class="sxs-lookup"><span data-stu-id="183e6-196">Once the entity is retrieved, call **table_operation::delete_entity** with the entity to delete.</span></span> <span data-ttu-id="183e6-197">Затем вызовите метод **cloud_table.execute**.</span><span class="sxs-lookup"><span data-stu-id="183e6-197">Then call the **cloud_table.execute** method.</span></span> <span data-ttu-id="183e6-198">Следующий код извлекает и удаляет сущность с ключом раздела Smith и ключом строки Jeff.</span><span class="sxs-lookup"><span data-stu-id="183e6-198">The following code retrieves and deletes an entity with a partition key of "Smith" and a row key of "Jeff".</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation to delete the entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit the delete operation to the Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a><span data-ttu-id="183e6-199">Удаление таблицы</span><span class="sxs-lookup"><span data-stu-id="183e6-199">Delete a table</span></span>
<span data-ttu-id="183e6-200">Наконец, следующий пример кода удаляет таблицу из учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="183e6-200">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="183e6-201">Удаленную таблицу нельзя воссоздать в течение определенного времени после удаления.</span><span class="sxs-lookup"><span data-stu-id="183e6-201">A table that has been deleted will be unavailable to be re-created for a period of time following the deletion.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation to delete the entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit the delete operation to the Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a><span data-ttu-id="183e6-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="183e6-202">Next steps</span></span>
<span data-ttu-id="183e6-203">Теперь, когда вы ознакомились с основными сведениями о хранилище таблиц, воспользуйтесь следующими ссылками для получения дополнительных сведений о службе хранилища Azure:</span><span class="sxs-lookup"><span data-stu-id="183e6-203">Now that you've learned the basics of table storage, follow these links to learn more about Azure Storage:</span></span>  

* <span data-ttu-id="183e6-204">[Обозреватель хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) — это бесплатное автономное приложение от корпорации Майкрософт, позволяющее визуализировать данные из службы хранилища Azure на платформе Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="183e6-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* [<span data-ttu-id="183e6-205">Использование хранилища BLOB-объектов из C++</span><span class="sxs-lookup"><span data-stu-id="183e6-205">How to use Blob storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="183e6-206">Использование хранилища очередей из C++</span><span class="sxs-lookup"><span data-stu-id="183e6-206">How to use Queue storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="183e6-207">Перечисление ресурсов хранилища Azure в C++</span><span class="sxs-lookup"><span data-stu-id="183e6-207">List Azure Storage resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="183e6-208">Справочник по клиентской библиотеке хранилища для C++</span><span class="sxs-lookup"><span data-stu-id="183e6-208">Storage Client Library for C++ reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="183e6-209">Документация по службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="183e6-209">Azure Storage documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
