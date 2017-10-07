---
title: "aaaHow toouse хранилище таблиц (C++) | Документы Microsoft"
description: "Хранения структурированных данных в облаке hello, с помощью хранилища таблиц Azure, хранилище данных NoSQL."
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
ms.openlocfilehash: 8eee0031350ab6ff3f76fb288b2f896687aa17a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-c"></a><span data-ttu-id="3547f-103">Как toouse хранилище таблиц из C++</span><span class="sxs-lookup"><span data-stu-id="3547f-103">How toouse Table storage from C++</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="3547f-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="3547f-104">Overview</span></span>
<span data-ttu-id="3547f-105">В этом руководстве будет показано, как tooperform распространенных сценариев с помощью hello службы хранилища таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="3547f-105">This guide will show you how tooperform common scenarios by using hello Azure Table storage service.</span></span> <span data-ttu-id="3547f-106">Примеры Hello на языке C++ и использовать hello [клиентская библиотека хранилища Azure для C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="3547f-106">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="3547f-107">Hello сценарии включают **Создание и удаление таблицы** и **работа с сущностями таблицы**.</span><span class="sxs-lookup"><span data-stu-id="3547f-107">hello scenarios covered include **creating and deleting a table** and **working with table entities**.</span></span>

> [!NOTE]
> <span data-ttu-id="3547f-108">Это руководство по цели hello клиентская библиотека хранилища Azure для C++ версии 1.0.0 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="3547f-108">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="3547f-109">Hello рекомендуемое версии клиентской библиотеки хранилища 2.2.0, которая доступна через [NuGet](http://www.nuget.org/packages/wastorage) или [GitHub](https://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="3547f-109">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="3547f-110">Создание приложения на C++</span><span class="sxs-lookup"><span data-stu-id="3547f-110">Create a C++ application</span></span>
<span data-ttu-id="3547f-111">В этом руководстве будут использоваться компоненты хранилища, которые могут выполняться в приложениях на C++.</span><span class="sxs-lookup"><span data-stu-id="3547f-111">In this guide, you will use storage features that can be run within a C++ application.</span></span> <span data-ttu-id="3547f-112">toodo таким образом, вам потребуется tooinstall hello клиентская библиотека хранилища Azure для C++ и создать учетную запись хранилища Azure в подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="3547f-112">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>  

<span data-ttu-id="3547f-113">hello tooinstall клиентская библиотека хранилища Azure для C++, можно использовать следующие методы hello:</span><span class="sxs-lookup"><span data-stu-id="3547f-113">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="3547f-114">**Linux —** следуйте инструкциям hello hello [клиентская библиотека хранилища Azure для C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) страницы.</span><span class="sxs-lookup"><span data-stu-id="3547f-114">**Linux:** Follow hello instructions given on hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="3547f-115">**Windows:** в Visual Studio нажмите **Инструменты > Диспетчер пакетов NuGet > Консоль диспетчера пакетов**.</span><span class="sxs-lookup"><span data-stu-id="3547f-115">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="3547f-116">Команда hello введите следующее в hello [консоль диспетчера пакетов NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="3547f-116">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press Enter.</span></span>  
  
     <span data-ttu-id="3547f-117">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="3547f-117">Install-Package wastorage</span></span>

## <a name="configure-your-application-tooaccess-table-storage"></a><span data-ttu-id="3547f-118">Настройка вашего приложения tooaccess хранилище таблиц</span><span class="sxs-lookup"><span data-stu-id="3547f-118">Configure your application tooaccess Table storage</span></span>
<span data-ttu-id="3547f-119">Добавьте следующие hello включать инструкции toohello верхней части файла C++ hello место toouse hello хранилища Azure API-интерфейсы tooaccess таблиц:</span><span class="sxs-lookup"><span data-stu-id="3547f-119">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess tables:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="3547f-120">Настройка строки подключения к хранилищу Azure</span><span class="sxs-lookup"><span data-stu-id="3547f-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="3547f-121">Клиент хранилища Azure использует хранилища конечные точки toostore соединения строки и учетные данные для доступа к службам данных управления.</span><span class="sxs-lookup"><span data-stu-id="3547f-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="3547f-122">При запуске клиентского приложения, необходимо указать строку соединения хранения hello в кодировке hello.</span><span class="sxs-lookup"><span data-stu-id="3547f-122">When running a client application, you must provide hello storage connection string in hello following format.</span></span> <span data-ttu-id="3547f-123">Имя учетной записи и hello хранилища ключи доступа к хранилищу для учетной записи хранения hello используйте hello, перечисленные в hello [портала Azure](https://portal.azure.com) для hello *AccountName* и *AccountKey* значения.</span><span class="sxs-lookup"><span data-stu-id="3547f-123">Use hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="3547f-124">Сведения об учетных записях хранения и ключах доступа см. в статье [Об учетных записях хранения Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="3547f-124">For information on storage accounts and access keys, see [About Azure storage accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="3547f-125">В этом примере показано, как объявить строки подключения hello toohold статического поля:</span><span class="sxs-lookup"><span data-stu-id="3547f-125">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="3547f-126">tootest приложения на локальном компьютере под управлением Windows, можно использовать hello Azure [эмулятор хранилища](storage-use-emulator.md) , установленная с hello [пакета Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="3547f-126">tootest your application in your local Windows-based computer, you can use hello Azure [storage emulator](storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="3547f-127">Эмулятор хранилища Hello — это программа, которая имитирует hello Azure BLOB-объектов, очередей и таблиц служб, доступных на локальном компьютере разработчика.</span><span class="sxs-lookup"><span data-stu-id="3547f-127">hello storage emulator is a utility that simulates hello Azure Blob, Queue, and Table services available on your local development machine.</span></span> <span data-ttu-id="3547f-128">Hello следующем примере показано, как объявить статическое поле toohold hello соединения строки tooyour эмулятора локального хранилища:</span><span class="sxs-lookup"><span data-stu-id="3547f-128">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>  

```cpp
// Define hello connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="3547f-129">toostart Здравствуйте эмулятор хранилища Azure, щелкните hello **запустить** или клавишу ключ Windows hello.</span><span class="sxs-lookup"><span data-stu-id="3547f-129">toostart hello Azure storage emulator, click hello **Start** button or press hello Windows key.</span></span> <span data-ttu-id="3547f-130">Начните вводить **эмулятор хранилища Azure**, а затем выберите **эмулятор хранилища Microsoft Azure** hello списке приложений.</span><span class="sxs-lookup"><span data-stu-id="3547f-130">Begin typing **Azure Storage Emulator**, and then select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>  

<span data-ttu-id="3547f-131">Hello следующие образцы предполагается, что используется один из этих двух методов tooget hello строки подключения к хранилищу.</span><span class="sxs-lookup"><span data-stu-id="3547f-131">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="3547f-132">Получить строку подключения</span><span class="sxs-lookup"><span data-stu-id="3547f-132">Retrieve your connection string</span></span>
<span data-ttu-id="3547f-133">Можно использовать hello **cloud_storage_account** класса toorepresent сведения об учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="3547f-133">You can use hello **cloud_storage_account** class toorepresent your storage account information.</span></span> <span data-ttu-id="3547f-134">tooretrieve данные из строки подключения к хранилищу hello учетной записи хранилища, можно использовать метод parse hello.</span><span class="sxs-lookup"><span data-stu-id="3547f-134">tooretrieve your storage account information from hello storage connection string, you can use hello parse method.</span></span>

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="3547f-135">Затем следует получить tooa ссылку **cloud_table_client** класса, как она дает возможность ссылаться на объекты для таблиц и сущностей, сохраненными в hello службы хранилища таблиц.</span><span class="sxs-lookup"><span data-stu-id="3547f-135">Next, get a reference tooa **cloud_table_client** class, as it lets you get reference objects for tables and entities stored within hello Table storage service.</span></span> <span data-ttu-id="3547f-136">Hello следующий код создает **cloud_table_client** объекта с помощью объекта учетной записи хранилища hello, мы получить выше:</span><span class="sxs-lookup"><span data-stu-id="3547f-136">hello following code creates a **cloud_table_client** object by using hello storage account object we retrieved above:</span></span>  

```cpp
// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a><span data-ttu-id="3547f-137">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="3547f-137">Create a table</span></span>
<span data-ttu-id="3547f-138">Объект **cloud_table_client** позволяет получить эталонные объекты для таблиц и сущностей.</span><span class="sxs-lookup"><span data-stu-id="3547f-138">A **cloud_table_client** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="3547f-139">Hello следующий код создает **cloud_table_client** объекта и использует его toocreate новую таблицу.</span><span class="sxs-lookup"><span data-stu-id="3547f-139">hello following code creates a **cloud_table_client** object and uses it toocreate a new table.</span></span>

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="3547f-140">Добавьте таблицу tooa сущности</span><span class="sxs-lookup"><span data-stu-id="3547f-140">Add an entity tooa table</span></span>
<span data-ttu-id="3547f-141">tooadd таблицу tooa сущности, создайте новый **table_entity** и передать его слишком**table_operation::insert_entity**.</span><span class="sxs-lookup"><span data-stu-id="3547f-141">tooadd an entity tooa table, create a new **table_entity** object and pass it too**table_operation::insert_entity**.</span></span> <span data-ttu-id="3547f-142">Hello следующий код использует имя клиента hello как ключ строки hello и фамилию в качестве ключа секции hello.</span><span class="sxs-lookup"><span data-stu-id="3547f-142">hello following code uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="3547f-143">Вместе секции и ключом строки идентификации сущности hello hello таблицы.</span><span class="sxs-lookup"><span data-stu-id="3547f-143">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="3547f-144">Ключи секций сущности с одинаковым ключом секции, которые могут запрашиваться быстрее, чем с различными приветствия, но с помощью различных разделов обеспечивает улучшенную масштабируемость параллельной операции.</span><span class="sxs-lookup"><span data-stu-id="3547f-144">Entities with hello same partition key can be queried faster than those with different partition keys, but using diverse partition keys allows for greater parallel operation scalability.</span></span> <span data-ttu-id="3547f-145">Дополнительные сведения см. в статье [Производительность хранилища Microsoft Azure и контрольный список масштабируемости](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="3547f-145">For more information, see [Microsoft Azure storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<span data-ttu-id="3547f-146">Hello следующий код создает новый экземпляр **table_entity** с хранимых данных toobe некоторых клиентов система.</span><span class="sxs-lookup"><span data-stu-id="3547f-146">hello following code creates a new instance of **table_entity** with some customer data toobe stored.</span></span> <span data-ttu-id="3547f-147">Здравствуйте, следующий код вызывает метод **table_operation::insert_entity** toocreate **table_operation** объекта tooinsert сущность в таблицу, и связывает hello новая сущность таблицы с ним.</span><span class="sxs-lookup"><span data-stu-id="3547f-147">hello code next calls **table_operation::insert_entity** toocreate a **table_operation** object tooinsert an entity into a table, and associates hello new table entity with it.</span></span> <span data-ttu-id="3547f-148">Наконец, hello код вызывает метод execute hello на hello **cloud_table** объекта.</span><span class="sxs-lookup"><span data-stu-id="3547f-148">Finally, hello code calls hello execute method on hello **cloud_table** object.</span></span> <span data-ttu-id="3547f-149">И новый hello **table_operation** отправляет запрос toohello службы tooinsert hello новый клиент сущности таблицы в таблицу «people» hello.</span><span class="sxs-lookup"><span data-stu-id="3547f-149">And hello new **table_operation** sends a request toohello Table service tooinsert hello new customer entity into hello "people" table.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create hello table operation that inserts hello customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute hello insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="3547f-150">Вставка пакета сущностей</span><span class="sxs-lookup"><span data-stu-id="3547f-150">Insert a batch of entities</span></span>
<span data-ttu-id="3547f-151">Пакет toohello сущностей службы таблиц можно вставить в одну операцию записи.</span><span class="sxs-lookup"><span data-stu-id="3547f-151">You can insert a batch of entities toohello Table service in one write operation.</span></span> <span data-ttu-id="3547f-152">Hello следующий код создает **table_batch_operation** объекта, а затем добавляет три вставить tooit операций.</span><span class="sxs-lookup"><span data-stu-id="3547f-152">hello following code creates a **table_batch_operation** object, and then adds three insert operations tooit.</span></span> <span data-ttu-id="3547f-153">Каждой операции вставки добавляется путем создания нового объекта сущностей задания его значений, и последующего вызова hello вставьте метод hello **table_batch_operation** сущности hello объекта tooassociate с новым операции вставки.</span><span class="sxs-lookup"><span data-stu-id="3547f-153">Each insert operation is added by creating a new entity object, setting its values, and then calling hello insert method on hello **table_batch_operation** object tooassociate hello entity with a new insert operation.</span></span> <span data-ttu-id="3547f-154">Затем **cloud_table.execute** вызывается операция tooexecute hello.</span><span class="sxs-lookup"><span data-stu-id="3547f-154">Then, **cloud_table.execute** is called tooexecute hello operation.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it toohello table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it toohello table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity tooadd toohello table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities toohello batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute hello batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

<span data-ttu-id="3547f-155">Некоторые действия toonote на пакетные операции:</span><span class="sxs-lookup"><span data-stu-id="3547f-155">Some things toonote on batch operations:</span></span>  

* <span data-ttu-id="3547f-156">Можно выполнять копирование too100 insert, delete, merge, replace, операции insert или merge и вставки или замены в любой комбинации в одном пакете.</span><span class="sxs-lookup"><span data-stu-id="3547f-156">You can perform up too100 insert, delete, merge, replace, insert-or-merge, and insert-or-replace operations in any combination in a single batch.</span></span>  
* <span data-ttu-id="3547f-157">В него входит только операция hello в пакете hello пакетная операция может быть операцией извлечения.</span><span class="sxs-lookup"><span data-stu-id="3547f-157">A batch operation can have a retrieve operation, if it is hello only operation in hello batch.</span></span>  
* <span data-ttu-id="3547f-158">Все сущности в одной пакетной операции должен иметь hello же ключ секционирования.</span><span class="sxs-lookup"><span data-stu-id="3547f-158">All entities in a single batch operation must have hello same partition key.</span></span>  
* <span data-ttu-id="3547f-159">Пакетная операция представляет ограниченный tooa полезных данных 4 МБ.</span><span class="sxs-lookup"><span data-stu-id="3547f-159">A batch operation is limited tooa 4-MB data payload.</span></span>  

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="3547f-160">Получение всех сущностей в разделе</span><span class="sxs-lookup"><span data-stu-id="3547f-160">Retrieve all entities in a partition</span></span>
<span data-ttu-id="3547f-161">таблицы для всех сущностей в секции, используйте tooquery **table_query** объекта.</span><span class="sxs-lookup"><span data-stu-id="3547f-161">tooquery a table for all entities in a partition, use a **table_query** object.</span></span> <span data-ttu-id="3547f-162">Hello следующий пример кода задает фильтр для сущности, где ключ раздела hello 'Smith'.</span><span class="sxs-lookup"><span data-stu-id="3547f-162">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="3547f-163">Этот пример выводит hello поля в каждой сущности в консоли toohello результаты запроса hello.</span><span class="sxs-lookup"><span data-stu-id="3547f-163">This example prints hello fields of each entity in hello query results toohello console.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct hello query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print hello fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

<span data-ttu-id="3547f-164">запрос Hello в этом примере переводит все сущности hello, соответствующие условиям фильтра hello.</span><span class="sxs-lookup"><span data-stu-id="3547f-164">hello query in this example brings all hello entities that match hello filter criteria.</span></span> <span data-ttu-id="3547f-165">Если вы используете большие таблицы и часто требуется сущностей таблицы toodownload hello, рекомендуется хранить данные в хранилище Azure BLOB-объектов вместо.</span><span class="sxs-lookup"><span data-stu-id="3547f-165">If you have large tables and need toodownload hello table entities often, we recommend that you store your data in Azure storage blobs instead.</span></span>

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="3547f-166">Получение диапазона сущностей в разделе</span><span class="sxs-lookup"><span data-stu-id="3547f-166">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="3547f-167">Если вы не хотите tooquery все сущности hello в секции, можно указать диапазон, объединяя hello фильтра ключа секции с фильтром ключа строк.</span><span class="sxs-lookup"><span data-stu-id="3547f-167">If you don't want tooquery all hello entities in a partition, you can specify a range by combining hello partition key filter with a row key filter.</span></span> <span data-ttu-id="3547f-168">Hello следующий пример кода использует два tooget фильтры всех сущностей в разделе «Smith», где начинается с буквы, более ранних, чем 'E' hello алфавита ключ строки hello (имя), а затем выводит результаты запроса hello.</span><span class="sxs-lookup"><span data-stu-id="3547f-168">hello following code example uses two filters tooget all entities in partition 'Smith' where hello row key (first name) starts with a letter earlier than 'E' in hello alphabet and then prints hello query results.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through hello results, displaying information about hello entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="3547f-169">Извлечение одной сущности</span><span class="sxs-lookup"><span data-stu-id="3547f-169">Retrieve a single entity</span></span>
<span data-ttu-id="3547f-170">Можно написать tooretrieve запроса конкретную сущность.</span><span class="sxs-lookup"><span data-stu-id="3547f-170">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="3547f-171">Hello следующий код использует **table_operation::retrieve_entity** toospecify hello клиента «Джефф Петров».</span><span class="sxs-lookup"><span data-stu-id="3547f-171">hello following code uses **table_operation::retrieve_entity** toospecify hello customer 'Jeff Smith'.</span></span> <span data-ttu-id="3547f-172">Этот метод возвращает только одну сущность, а не коллекцию и hello возвращенное значение находится в **table_result**.</span><span class="sxs-lookup"><span data-stu-id="3547f-172">This method returns just one entity, rather than a collection, and hello returned value is in **table_result**.</span></span> <span data-ttu-id="3547f-173">Указание ключи секций и строк в запросе является hello самый быстрый способ tooretrieve одной сущности из службы таблиц hello.</span><span class="sxs-lookup"><span data-stu-id="3547f-173">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output hello entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a><span data-ttu-id="3547f-174">Замена сущности</span><span class="sxs-lookup"><span data-stu-id="3547f-174">Replace an entity</span></span>
<span data-ttu-id="3547f-175">tooreplace сущности, получить его из службы таблиц hello, изменить объект сущности hello и сохранять изменения hello обратно toohello службы таблиц.</span><span class="sxs-lookup"><span data-stu-id="3547f-175">tooreplace an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="3547f-176">Hello следующий код позволяет изменить адрес электронной почты и номер телефона существующего клиента.</span><span class="sxs-lookup"><span data-stu-id="3547f-176">hello following code changes an existing customer's phone number and email address.</span></span> <span data-ttu-id="3547f-177">Вместо вызова метода **table_operation::insert_entity** этот код использует **table_operation::replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="3547f-177">Instead of calling **table_operation::insert_entity**, this code uses **table_operation::replace_entity**.</span></span> <span data-ttu-id="3547f-178">В этом случае toobe сущности hello полностью заменить на сервере hello, пока не изменят hello объекта на сервере hello, так как он был извлечен, в этом случае hello операция завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="3547f-178">This causes hello entity toobe fully replaced on hello server, unless hello entity on hello server has changed since it was retrieved, in which case hello operation will fail.</span></span> <span data-ttu-id="3547f-179">Эта ошибка является tooprevent приложение случайно перезаписанный изменения внесены между hello извлечения и обновления приложения другим компонентом.</span><span class="sxs-lookup"><span data-stu-id="3547f-179">This failure is tooprevent your application from inadvertently overwriting a change made between hello retrieval and update by another component of your application.</span></span> <span data-ttu-id="3547f-180">Hello правильной обработки данного сбоя — tooretrieve hello сущность снова, внесенные изменения (если она все еще действует) и затем выполнять другую **table_operation::replace_entity** операции.</span><span class="sxs-lookup"><span data-stu-id="3547f-180">hello proper handling of this failure is tooretrieve hello entity again, make your changes (if still valid), and then perform another **table_operation::replace_entity** operation.</span></span> <span data-ttu-id="3547f-181">Hello следующем разделе будет показано, как toooverride это поведение.</span><span class="sxs-lookup"><span data-stu-id="3547f-181">hello next section will show you how toooverride this behavior.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation tooreplace hello entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="3547f-182">Вставка или замена сущности</span><span class="sxs-lookup"><span data-stu-id="3547f-182">Insert-or-replace an entity</span></span>
<span data-ttu-id="3547f-183">**table_operation::replace_entity** операции могут завершаться hello объекта было изменено, поскольку он был извлечен из сервера hello.</span><span class="sxs-lookup"><span data-stu-id="3547f-183">**table_operation::replace_entity** operations will fail if hello entity has been changed since it was retrieved from hello server.</span></span> <span data-ttu-id="3547f-184">Кроме того, необходимо извлечь hello сущности с hello сервера сначала для **table_operation::replace_entity** toobe успешно.</span><span class="sxs-lookup"><span data-stu-id="3547f-184">Furthermore, you must retrieve hello entity from hello server first in order for **table_operation::replace_entity** toobe successful.</span></span> <span data-ttu-id="3547f-185">Иногда, тем не менее, вы не знаете Если hello сущность существует на сервере hello и неприменимы hello текущие значения, сохраненные в ней — обновление перезаписывать их все.</span><span class="sxs-lookup"><span data-stu-id="3547f-185">Sometimes, however, you don't know if hello entity exists on hello server and hello current values stored in it are irrelevant—your update should overwrite them all.</span></span> <span data-ttu-id="3547f-186">tooaccomplish это, следует использовать **table_operation::insert_or_replace_entity** операции.</span><span class="sxs-lookup"><span data-stu-id="3547f-186">tooaccomplish this, you would use a **table_operation::insert_or_replace_entity** operation.</span></span> <span data-ttu-id="3547f-187">Эта операция вставляет сущность hello, если она не существует, или заменяет его, если это так, независимо от того, когда была произведена hello последнего обновления.</span><span class="sxs-lookup"><span data-stu-id="3547f-187">This operation inserts hello entity if it doesn't exist, or replaces it if it does, regardless of when hello last update was made.</span></span> <span data-ttu-id="3547f-188">В следующем примере кода hello, по-прежнему получить сущность customer hello Джефф Смит, но затем сохраняется задней toohello серверу с помощью **table_operation::insert_or_replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="3547f-188">In hello following code example, hello customer entity for Jeff Smith is still retrieved, but it is then saved back toohello server via **table_operation::insert_or_replace_entity**.</span></span> <span data-ttu-id="3547f-189">Все изменения, сделанные сущности toohello между hello операции извлечения и обновления будут перезаписаны.</span><span class="sxs-lookup"><span data-stu-id="3547f-189">Any updates made toohello entity between hello retrieval and update operation will be overwritten.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation tooinsert-or-replace hello entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="3547f-190">Запрос подмножества свойств сущности</span><span class="sxs-lookup"><span data-stu-id="3547f-190">Query a subset of entity properties</span></span>
<span data-ttu-id="3547f-191">Таблицы tooa запроса можно получить только несколько свойств сущности.</span><span class="sxs-lookup"><span data-stu-id="3547f-191">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="3547f-192">Hello запрос в hello, следующий код использует hello **table_query::set_select_columns** метод tooreturn только hello адреса электронной почты сущности в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="3547f-192">hello query in hello following code uses hello **table_query::set_select_columns** method tooreturn only hello email addresses of entities in hello table.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define hello query, and select only hello Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display hello results.
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
> <span data-ttu-id="3547f-193">Запрос нескольких свойств сущности является более эффективной операцией, чем запрос всех свойств.</span><span class="sxs-lookup"><span data-stu-id="3547f-193">Querying a few properties from an entity is a more efficient operation than retrieving all properties.</span></span>
> 
> 

## <a name="delete-an-entity"></a><span data-ttu-id="3547f-194">Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="3547f-194">Delete an entity</span></span>
<span data-ttu-id="3547f-195">Сущность можно легко удалить после ее получения.</span><span class="sxs-lookup"><span data-stu-id="3547f-195">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="3547f-196">Когда извлекается hello объекта, вызовите **table_operation::delete_entity** с toodelete hello сущности.</span><span class="sxs-lookup"><span data-stu-id="3547f-196">Once hello entity is retrieved, call **table_operation::delete_entity** with hello entity toodelete.</span></span> <span data-ttu-id="3547f-197">Затем вызовите hello **cloud_table.execute** метод.</span><span class="sxs-lookup"><span data-stu-id="3547f-197">Then call hello **cloud_table.execute** method.</span></span> <span data-ttu-id="3547f-198">Hello следующий код извлекает и удаляет сущность с ключом раздела «Smith» и ключ строки «Джефф».</span><span class="sxs-lookup"><span data-stu-id="3547f-198">hello following code retrieves and deletes an entity with a partition key of "Smith" and a row key of "Jeff".</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a><span data-ttu-id="3547f-199">Удаление таблицы</span><span class="sxs-lookup"><span data-stu-id="3547f-199">Delete a table</span></span>
<span data-ttu-id="3547f-200">Наконец hello, следующий пример кода удаляет таблицу из учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="3547f-200">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="3547f-201">Таблицы, которая была удалена, будет недоступен toobe повторно создан для определенного периода времени после удаления hello.</span><span class="sxs-lookup"><span data-stu-id="3547f-201">A table that has been deleted will be unavailable toobe re-created for a period of time following hello deletion.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a><span data-ttu-id="3547f-202">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3547f-202">Next steps</span></span>
<span data-ttu-id="3547f-203">Теперь, когда вы узнали основы hello хранилища таблицы, выполните следующие дополнительные сведения о хранилище Azure toolearn ссылки.</span><span class="sxs-lookup"><span data-stu-id="3547f-203">Now that you've learned hello basics of table storage, follow these links toolearn more about Azure Storage:</span></span>  

* <span data-ttu-id="3547f-204">[Обозреватель хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) является бесплатной, отдельное приложение от Майкрософт, позволяющая toowork визуально с помощью данных из хранилища Azure в Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="3547f-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* [<span data-ttu-id="3547f-205">Как toouse хранилища BLOB-объектов из C++</span><span class="sxs-lookup"><span data-stu-id="3547f-205">How toouse Blob storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="3547f-206">Как toouse хранилища очередей из C++</span><span class="sxs-lookup"><span data-stu-id="3547f-206">How toouse Queue storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="3547f-207">Перечисление ресурсов хранилища Azure в C++</span><span class="sxs-lookup"><span data-stu-id="3547f-207">List Azure Storage resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="3547f-208">Справочник по клиентской библиотеке хранилища для C++</span><span class="sxs-lookup"><span data-stu-id="3547f-208">Storage Client Library for C++ reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="3547f-209">Документация по службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="3547f-209">Azure Storage documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
