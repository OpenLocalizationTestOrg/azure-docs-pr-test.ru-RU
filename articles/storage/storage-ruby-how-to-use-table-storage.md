---
title: "Как использовать хранилище таблиц Azure из Ruby | Документация Майкрософт"
description: "Хранение структурированных данных в облаке в хранилище таблиц Azure (хранилище данных NoSQL)."
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: 
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 03f466cb08ed2ccbd2985471d0956af9e66d97f1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-table-storage-from-ruby"></a><span data-ttu-id="df052-103">Использование табличного хранилища Azure в Ruby</span><span class="sxs-lookup"><span data-stu-id="df052-103">How to use Azure Table Storage from Ruby</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="df052-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="df052-104">Overview</span></span>
<span data-ttu-id="df052-105">В этом руководстве показано, как реализовать типичные сценарии с использованием службы таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="df052-105">This guide shows you how to perform common scenarios using the Azure Table service.</span></span> <span data-ttu-id="df052-106">Примеры написаны с помощью Ruby API.</span><span class="sxs-lookup"><span data-stu-id="df052-106">The samples are written using the Ruby API.</span></span> <span data-ttu-id="df052-107">Здесь описаны такие сценарии, как **создание и удаление таблицы, вставка и запрос сущностей в таблице**.</span><span class="sxs-lookup"><span data-stu-id="df052-107">The scenarios covered include **creating and deleting a table, inserting and querying entities in a table**.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="df052-108">Создание приложения Ruby</span><span class="sxs-lookup"><span data-stu-id="df052-108">Create a Ruby application</span></span>
<span data-ttu-id="df052-109">Инструкции по созданию приложение Ruby см. в статье [Веб-приложение Ruby on Rails на виртуальной машине Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="df052-109">For instructions how to create a Ruby application, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="df052-110">Настройка приложения для доступа к хранилищу</span><span class="sxs-lookup"><span data-stu-id="df052-110">Configure your application to access Storage</span></span>
<span data-ttu-id="df052-111">Чтобы использовать службу хранилища Azure, скачайте пакет Azure для Ruby, который содержит набор библиотек, взаимодействующих со службами REST хранилища.</span><span class="sxs-lookup"><span data-stu-id="df052-111">To use Azure Storage, you need to download and use the Ruby azure package which includes a set of convenience libraries that communicate with the Storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="df052-112">Использование RubyGems для получения пакета</span><span class="sxs-lookup"><span data-stu-id="df052-112">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="df052-113">Используйте интерфейс командной строки, например **PowerShell** (Windows), **Terminal** (Mac) или **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="df052-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="df052-114">Введите **gem install azure** в окне командной строки, чтобы установить пакеты и зависимости.</span><span class="sxs-lookup"><span data-stu-id="df052-114">Type **gem install azure** in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="df052-115">Импорт пакета</span><span class="sxs-lookup"><span data-stu-id="df052-115">Import the package</span></span>
<span data-ttu-id="df052-116">С помощью любого текстового редактора добавьте указанный код в начало файла Ruby, где планируется использовать службу хранилища.</span><span class="sxs-lookup"><span data-stu-id="df052-116">Use your favorite text editor, add the following to the top of the Ruby file where you intend to use Storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="df052-117">Настройка подключения к службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="df052-117">Set up an Azure Storage connection</span></span>
<span data-ttu-id="df052-118">Модуль Azure считывает переменные среды **AZURE\_STORAGE\_ACCOUNT** и **AZURE\_STORAGE\_ACCESS\_KEY**, чтобы получить информацию, необходимую для подключения к учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="df052-118">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** for information required to connect to your Azure Storage account.</span></span> <span data-ttu-id="df052-119">Если эти переменные среды не заданы, необходимо указать сведения об учетной записи перед использованием **Azure::TableService** с помощью следующего кода:</span><span class="sxs-lookup"><span data-stu-id="df052-119">If these environment variables are not set, you must specify the account information before using **Azure::TableService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="df052-120">Вот как можно получить эти значения из классический учетной записи хранения или учетной записи хранения Resource Manager на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="df052-120">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="df052-121">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="df052-121">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="df052-122">Перейдите к учетной записи хранения, которая будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="df052-122">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="df052-123">В колонке "Параметры" справа щелкните **Ключи доступа**.</span><span class="sxs-lookup"><span data-stu-id="df052-123">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="df052-124">В колонке "Ключи доступа" вы увидите ключи доступа 1 и 2.</span><span class="sxs-lookup"><span data-stu-id="df052-124">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="df052-125">Можно использовать любой из них.</span><span class="sxs-lookup"><span data-stu-id="df052-125">You can use either of these.</span></span>
5. <span data-ttu-id="df052-126">Щелкните значок копирования, чтобы скопировать ключ в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="df052-126">Click the copy icon to copy the key to the clipboard.</span></span>

<span data-ttu-id="df052-127">Вот как можно получить эти значения из классический учетной записи хранения на классическом портале Azure.</span><span class="sxs-lookup"><span data-stu-id="df052-127">To obtain these values from a classic storage account in the classic Azure portal:</span></span>

1. <span data-ttu-id="df052-128">Перейдите на [классический портал Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="df052-128">Log in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="df052-129">Перейдите к учетной записи хранения, которая будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="df052-129">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="df052-130">Щелкните **УПРАВЛЕНИЕ КЛЮЧАМИ ДОСТУПА** в нижней части области навигации.</span><span class="sxs-lookup"><span data-stu-id="df052-130">Click **MANAGE ACCESS KEYS** at the bottom of the navigation pane.</span></span>
4. <span data-ttu-id="df052-131">Во всплывающем диалоговом окне вы увидите имя учетной записи хранения, первичный ключ доступа и вторичный ключ доступа.</span><span class="sxs-lookup"><span data-stu-id="df052-131">In the pop-up dialog, you'll see the storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="df052-132">В качестве ключа доступа можно использовать либо первичный, либо вторичный ключ.</span><span class="sxs-lookup"><span data-stu-id="df052-132">For access key, you can use either the primary one or the secondary one.</span></span>
5. <span data-ttu-id="df052-133">Щелкните значок копирования, чтобы скопировать ключ в буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="df052-133">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="df052-134">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="df052-134">Create a table</span></span>
<span data-ttu-id="df052-135">Объект **Azure::TableService** позволяет работать с таблицами и сущностями.</span><span class="sxs-lookup"><span data-stu-id="df052-135">The **Azure::TableService** object lets you work with tables and entities.</span></span> <span data-ttu-id="df052-136">Чтобы создать таблицу, используйте метод **create\_table()**.</span><span class="sxs-lookup"><span data-stu-id="df052-136">To create a table, use the **create\_table()** method.</span></span> <span data-ttu-id="df052-137">В следующем примере создается таблица или выводится ошибка, если она возникла.</span><span class="sxs-lookup"><span data-stu-id="df052-137">The following example creates a table or prints the error if there is any.</span></span>

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="df052-138">Добавление сущности в таблицу</span><span class="sxs-lookup"><span data-stu-id="df052-138">Add an entity to a table</span></span>
<span data-ttu-id="df052-139">Чтобы добавить сущность, сначала создайте хэш-объект, который определяет свойства сущности.</span><span class="sxs-lookup"><span data-stu-id="df052-139">To add an entity, first create a hash object that defines your entity properties.</span></span> <span data-ttu-id="df052-140">Обратите внимание, что для каждой сущности необходимо указать **PartitionKey** и **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="df052-140">Note that for every entity you must specify a **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="df052-141">Это уникальные идентификаторы сущностей, которые можно запросить гораздо быстрее, чем для других свойств.</span><span class="sxs-lookup"><span data-stu-id="df052-141">These are the unique identifiers of your entities, and are values that can be queried much faster than your other properties.</span></span> <span data-ttu-id="df052-142">Служба хранилища Azure использует **PartitionKey** , чтобы автоматически распространять сущности таблицы на множество узлов хранилища.</span><span class="sxs-lookup"><span data-stu-id="df052-142">Azure Storage uses **PartitionKey** to automatically distribute the table's entities over many storage nodes.</span></span> <span data-ttu-id="df052-143">Сущности с одним значением **PartitionKey** хранятся на одном узле.</span><span class="sxs-lookup"><span data-stu-id="df052-143">Entities with the same **PartitionKey** are stored on the same node.</span></span> <span data-ttu-id="df052-144">**RowKey** — это уникальный идентификатор сущности в разделе, которому она принадлежит.</span><span class="sxs-lookup"><span data-stu-id="df052-144">The **RowKey** is the unique ID of the entity within the partition it belongs to.</span></span>

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a><span data-ttu-id="df052-145">Обновление сущности</span><span class="sxs-lookup"><span data-stu-id="df052-145">Update an entity</span></span>
<span data-ttu-id="df052-146">Для обновления имеющейся сущности доступно несколько методов:</span><span class="sxs-lookup"><span data-stu-id="df052-146">There are multiple methods available to update an existing entity:</span></span>

* <span data-ttu-id="df052-147">**update\_entity():** обновляет имеющуюся сущность путем ее замены.</span><span class="sxs-lookup"><span data-stu-id="df052-147">**update\_entity():** Update an existing entity by replacing it.</span></span>
* <span data-ttu-id="df052-148">**merge\_entity():** обновляет сущность посредством объединения новых значений свойств с имеющейся сущностью.</span><span class="sxs-lookup"><span data-stu-id="df052-148">**merge\_entity():** Updates an existing entity by merging new property values into the existing entity.</span></span>
* <span data-ttu-id="df052-149">**insert\_or\_merge\_entity():** обновляет имеющуюся сущность путем ее замены.</span><span class="sxs-lookup"><span data-stu-id="df052-149">**insert\_or\_merge\_entity():** Updates an existing entity by replacing it.</span></span> <span data-ttu-id="df052-150">Если сущность не существует, будет вставлена новая сущность.</span><span class="sxs-lookup"><span data-stu-id="df052-150">If no entity exists, a new one will be inserted:</span></span>
* <span data-ttu-id="df052-151">**insert\_or\_replace\_entity():** обновляет сущность посредством объединения новых значений свойств с имеющейся сущностью.</span><span class="sxs-lookup"><span data-stu-id="df052-151">**insert\_or\_replace\_entity():** Updates an existing entity by merging new property values into the existing entity.</span></span> <span data-ttu-id="df052-152">Если сущность не существует, будет вставлена новая сущность.</span><span class="sxs-lookup"><span data-stu-id="df052-152">If no entity exists, a new one will be inserted.</span></span>

<span data-ttu-id="df052-153">В следующем примере показано обновление сущности с помощью метода **update\_entity()**.</span><span class="sxs-lookup"><span data-stu-id="df052-153">The following example demonstrates updating an entity using **update\_entity()**:</span></span>

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

<span data-ttu-id="df052-154">Если сущность, которая обновляется, не существует, при использовании метода **update\_entity()** или **merge\_entity()** операция завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="df052-154">With **update\_entity()** and **merge\_entity()**, if the entity that you are updating doesn't exist then the update operation will fail.</span></span> <span data-ttu-id="df052-155">Поэтому, если вы хотите сохранить сущность независимо от того, существует она или нет, используйте метод **insert\_or\_replace\_entity()** или **insert\_or\_merge\_entity()**.</span><span class="sxs-lookup"><span data-stu-id="df052-155">Therefore if you wish to store an entity regardless of whether it already exists, you should instead use **insert\_or\_replace\_entity()** or **insert\_or\_merge\_entity()**.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="df052-156">Работа с группами сущностей</span><span class="sxs-lookup"><span data-stu-id="df052-156">Work with groups of entities</span></span>
<span data-ttu-id="df052-157">Иногда имеет смысл отправлять совместно несколько операций в пакете для атомарной обработки сервером.</span><span class="sxs-lookup"><span data-stu-id="df052-157">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span></span> <span data-ttu-id="df052-158">Для этого сначала требуется создать объект **Batch**, а затем использовать метод **execute\_batch()** для **TableService**.</span><span class="sxs-lookup"><span data-stu-id="df052-158">To accomplish that, you first create a **Batch** object and then use the **execute\_batch()** method on **TableService**.</span></span> <span data-ttu-id="df052-159">В следующем примере показана отправка двух сущностей с RowKey 2 и 3 в пакете.</span><span class="sxs-lookup"><span data-stu-id="df052-159">The following example demonstrates submitting two entities with RowKey 2 and 3 in a batch.</span></span> <span data-ttu-id="df052-160">Обратите внимание, что пример работает только для сущностей с одинаковым значением PartitionKey.</span><span class="sxs-lookup"><span data-stu-id="df052-160">Notice that it only works for entities with the same PartitionKey.</span></span>

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="df052-161">Запрос сущности</span><span class="sxs-lookup"><span data-stu-id="df052-161">Query for an entity</span></span>
<span data-ttu-id="df052-162">Чтобы отправить запрос к сущности в таблице, используйте метод **get\_entity()**: передайте имя таблицы, **PartitionKey** и **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="df052-162">To query an entity in a table, use the **get\_entity()** method, by passing the table name, **PartitionKey** and **RowKey**.</span></span>

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="df052-163">Запрос набора сущностей</span><span class="sxs-lookup"><span data-stu-id="df052-163">Query a set of entities</span></span>
<span data-ttu-id="df052-164">Чтобы отправить запрос к набору сущностей в таблице, создайте хэш-объект запроса и используйте метод **query\_entities()**.</span><span class="sxs-lookup"><span data-stu-id="df052-164">To query a set of entities in a table, create a query hash object and use the **query\_entities()** method.</span></span> <span data-ttu-id="df052-165">В следующем примере показано, как получить все сущности с одним значением **PartitionKey**:</span><span class="sxs-lookup"><span data-stu-id="df052-165">The following example demonstrates getting all the entities with the same **PartitionKey**:</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> <span data-ttu-id="df052-166">Если полученный в результате набор слишком велик и не может быть возвращен в одном запросе, возвращается токен продолжения, который можно использовать для извлечения последующих страниц.</span><span class="sxs-lookup"><span data-stu-id="df052-166">If the result set is too large for a single query to return, a continuation token will be returned which you can use to retrieve subsequent pages.</span></span>
>
>

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="df052-167">Запрос подмножества свойств сущности</span><span class="sxs-lookup"><span data-stu-id="df052-167">Query a subset of entity properties</span></span>
<span data-ttu-id="df052-168">Запрос к таблице может получить лишь несколько свойств сущности.</span><span class="sxs-lookup"><span data-stu-id="df052-168">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="df052-169">Этот метод, который называется "проекцией", снижает потребление пропускной способности и может повысить производительность запросов, особенно для крупных сущностей.</span><span class="sxs-lookup"><span data-stu-id="df052-169">This technique, called "projection", reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="df052-170">Используйте предложение select и передайте имена свойств, которые необходимо передать клиенту.</span><span class="sxs-lookup"><span data-stu-id="df052-170">Use the select clause and pass the names of the properties you would like to bring over to the client.</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a><span data-ttu-id="df052-171">Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="df052-171">Delete an entity</span></span>
<span data-ttu-id="df052-172">Чтобы удалить сущность, используйте метод **delete\_entity()**.</span><span class="sxs-lookup"><span data-stu-id="df052-172">To delete an entity, use the **delete\_entity()** method.</span></span> <span data-ttu-id="df052-173">Необходимо передать имя таблицы, содержащей сущность, а также свойства PartitionKey и RowKey сущности.</span><span class="sxs-lookup"><span data-stu-id="df052-173">You need to pass in the name of the table which contains the entity, the PartitionKey and RowKey of the entity.</span></span>

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a><span data-ttu-id="df052-174">Удаление таблицы</span><span class="sxs-lookup"><span data-stu-id="df052-174">Delete a table</span></span>
<span data-ttu-id="df052-175">Чтобы удалить таблицу, используйте метод **delete\_table()** и передайте имя удаляемой таблицы.</span><span class="sxs-lookup"><span data-stu-id="df052-175">To delete a table, use the **delete\_table()** method and pass in the name of the table you want to delete.</span></span>

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a><span data-ttu-id="df052-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="df052-176">Next steps</span></span>

* <span data-ttu-id="df052-177">[Обозреватель хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) — это бесплатное автономное приложение от корпорации Майкрософт, позволяющее визуализировать данные из службы хранилища Azure на платформе Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="df052-177">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="df052-178">[пакетов SDK Azure для Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) на веб-сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="df052-178">[Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

