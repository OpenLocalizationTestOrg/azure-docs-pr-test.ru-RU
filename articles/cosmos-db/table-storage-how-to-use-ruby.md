---
title: "aaaHow toouse табличного хранилища Azure из Ruby | Документы Microsoft"
description: "Хранения структурированных данных в облаке hello, с помощью хранилища таблиц Azure, хранилище данных NoSQL."
services: cosmos-db
documentationcenter: ruby
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 2f9eb5a9160b551d6d1d198869787070c402b1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-ruby"></a><span data-ttu-id="16dbd-103">Как toouse табличного хранилища Azure из Ruby</span><span class="sxs-lookup"><span data-stu-id="16dbd-103">How toouse Azure Table Storage from Ruby</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="16dbd-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="16dbd-104">Overview</span></span>
<span data-ttu-id="16dbd-105">В этом руководстве показано, как с помощью распространенных сценариев tooperform hello службы таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="16dbd-105">This guide shows you how tooperform common scenarios using hello Azure Table service.</span></span> <span data-ttu-id="16dbd-106">образцы Hello записываются с помощью Ruby API hello.</span><span class="sxs-lookup"><span data-stu-id="16dbd-106">hello samples are written using hello Ruby API.</span></span> <span data-ttu-id="16dbd-107">Hello сценарии включают **Создание и удаление таблицы, вставка и выполнения запросов к сущностям в таблице**.</span><span class="sxs-lookup"><span data-stu-id="16dbd-107">hello scenarios covered include **creating and deleting a table, inserting and querying entities in a table**.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="16dbd-108">Создание приложения Ruby</span><span class="sxs-lookup"><span data-stu-id="16dbd-108">Create a Ruby application</span></span>
<span data-ttu-id="16dbd-109">Инструкции toocreate приложении Ruby. в статье [Ruby на направляющие веб-приложения на Виртуальной машине Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="16dbd-109">For instructions how toocreate a Ruby application, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="16dbd-110">Настройка вашего приложения tooaccess хранилища</span><span class="sxs-lookup"><span data-stu-id="16dbd-110">Configure your application tooaccess Storage</span></span>
<span data-ttu-id="16dbd-111">toouse хранилища Azure, понадобится toodownload и используйте hello Ruby azure пакет, который включает в себя набор библиотек удобства, взаимодействующих со службами хранилища REST hello.</span><span class="sxs-lookup"><span data-stu-id="16dbd-111">toouse Azure Storage, you need toodownload and use hello Ruby azure package which includes a set of convenience libraries that communicate with hello Storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="16dbd-112">Используйте RubyGems tooobtain hello пакет</span><span class="sxs-lookup"><span data-stu-id="16dbd-112">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="16dbd-113">Используйте интерфейс командной строки, например **PowerShell** (Windows), **Terminal** (Mac) или **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="16dbd-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="16dbd-114">Тип **gem установки azure** в hello команда окна tooinstall hello gem и зависимости.</span><span class="sxs-lookup"><span data-stu-id="16dbd-114">Type **gem install azure** in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="16dbd-115">Импорт пакета hello</span><span class="sxs-lookup"><span data-stu-id="16dbd-115">Import hello package</span></span>
<span data-ttu-id="16dbd-116">Используйте текстовый редактор, добавить следующие toohello вверху hello Ruby файл, куда будет toouse хранилища hello:</span><span class="sxs-lookup"><span data-stu-id="16dbd-116">Use your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse Storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="16dbd-117">Настройка подключения к службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="16dbd-117">Set up an Azure Storage connection</span></span>
<span data-ttu-id="16dbd-118">Hello модуль azure будет считывать переменные среды hello **AZURE\_ХРАНЕНИЯ\_учетной записи** и **AZURE\_ХРАНЕНИЯ\_доступа\_ключ**сведения, необходимые учетной записи хранилища Azure tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="16dbd-118">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** for information required tooconnect tooyour Azure Storage account.</span></span> <span data-ttu-id="16dbd-119">Если эти переменные среды не установлены, необходимо указать сведения об учетной записи hello перед использованием **Azure::TableService** с hello, следующий код:</span><span class="sxs-lookup"><span data-stu-id="16dbd-119">If these environment variables are not set, you must specify hello account information before using **Azure::TableService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="16dbd-120">tooobtain эти значения из классические или диспетчер ресурсов хранилища учетной записи в hello портала Azure:</span><span class="sxs-lookup"><span data-stu-id="16dbd-120">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="16dbd-121">Войдите в toohello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="16dbd-121">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="16dbd-122">Перейдите toohello необходимом toouse учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="16dbd-122">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="16dbd-123">В колонке параметров hello на hello вправо, щелкните **клавиши доступа**.</span><span class="sxs-lookup"><span data-stu-id="16dbd-123">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="16dbd-124">В колонке ключи hello доступа, отображается вы увидите ключ доступа hello 1 и ключ доступа 2.</span><span class="sxs-lookup"><span data-stu-id="16dbd-124">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="16dbd-125">Можно использовать любой из них.</span><span class="sxs-lookup"><span data-stu-id="16dbd-125">You can use either of these.</span></span>
5. <span data-ttu-id="16dbd-126">Щелкните hello скопировать значок toocopy hello ключа toohello буфер обмена.</span><span class="sxs-lookup"><span data-stu-id="16dbd-126">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="16dbd-127">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="16dbd-127">Create a table</span></span>
<span data-ttu-id="16dbd-128">Hello **Azure::TableService** объектов позволяет работать с таблицами и сущностями.</span><span class="sxs-lookup"><span data-stu-id="16dbd-128">hello **Azure::TableService** object lets you work with tables and entities.</span></span> <span data-ttu-id="16dbd-129">toocreate таблицы, используйте hello **создания\_table()** метод.</span><span class="sxs-lookup"><span data-stu-id="16dbd-129">toocreate a table, use hello **create\_table()** method.</span></span> <span data-ttu-id="16dbd-130">Hello следующий пример создает таблицу или отпечатков hello ошибки, если оно назначено.</span><span class="sxs-lookup"><span data-stu-id="16dbd-130">hello following example creates a table or prints hello error if there is any.</span></span>

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="16dbd-131">Добавьте таблицу tooa сущности</span><span class="sxs-lookup"><span data-stu-id="16dbd-131">Add an entity tooa table</span></span>
<span data-ttu-id="16dbd-132">tooadd сущности, сначала создать хэш-объект, определяющий свойства сущности.</span><span class="sxs-lookup"><span data-stu-id="16dbd-132">tooadd an entity, first create a hash object that defines your entity properties.</span></span> <span data-ttu-id="16dbd-133">Обратите внимание, что для каждой сущности необходимо указать **PartitionKey** и **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="16dbd-133">Note that for every entity you must specify a **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="16dbd-134">Это hello уникальные идентификаторы объектов и значений, которые могут запрашиваться гораздо быстрее, чем другие свойства.</span><span class="sxs-lookup"><span data-stu-id="16dbd-134">These are hello unique identifiers of your entities, and are values that can be queried much faster than your other properties.</span></span> <span data-ttu-id="16dbd-135">Хранилище Azure использует **PartitionKey** tooautomatically распределения сущностей таблицы hello по многим узлам хранилища.</span><span class="sxs-lookup"><span data-stu-id="16dbd-135">Azure Storage uses **PartitionKey** tooautomatically distribute hello table's entities over many storage nodes.</span></span> <span data-ttu-id="16dbd-136">Здравствуйте сущности с одинаковым **PartitionKey** хранятся на hello того же узла.</span><span class="sxs-lookup"><span data-stu-id="16dbd-136">Entities with hello same **PartitionKey** are stored on hello same node.</span></span> <span data-ttu-id="16dbd-137">Hello **RowKey** hello уникальным идентификатором hello сущности внутри раздела hello, он принадлежит.</span><span class="sxs-lookup"><span data-stu-id="16dbd-137">hello **RowKey** is hello unique ID of hello entity within hello partition it belongs to.</span></span>

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a><span data-ttu-id="16dbd-138">Обновление сущности</span><span class="sxs-lookup"><span data-stu-id="16dbd-138">Update an entity</span></span>
<span data-ttu-id="16dbd-139">Существует несколько методов, доступных tooupdate существующей сущности.</span><span class="sxs-lookup"><span data-stu-id="16dbd-139">There are multiple methods available tooupdate an existing entity:</span></span>

* <span data-ttu-id="16dbd-140">**update\_entity():** обновляет имеющуюся сущность путем ее замены.</span><span class="sxs-lookup"><span data-stu-id="16dbd-140">**update\_entity():** Update an existing entity by replacing it.</span></span>
* <span data-ttu-id="16dbd-141">**Слияние\_entity():** обновляет существующую сущность, объединив новых значений свойств в hello существующей сущности.</span><span class="sxs-lookup"><span data-stu-id="16dbd-141">**merge\_entity():** Updates an existing entity by merging new property values into hello existing entity.</span></span>
* <span data-ttu-id="16dbd-142">**insert\_or\_merge\_entity():** обновляет имеющуюся сущность путем ее замены.</span><span class="sxs-lookup"><span data-stu-id="16dbd-142">**insert\_or\_merge\_entity():** Updates an existing entity by replacing it.</span></span> <span data-ttu-id="16dbd-143">Если сущность не существует, будет вставлена новая сущность.</span><span class="sxs-lookup"><span data-stu-id="16dbd-143">If no entity exists, a new one will be inserted:</span></span>
* <span data-ttu-id="16dbd-144">**Вставить\_или\_заменить\_entity():** обновляет существующую сущность, объединив новых значений свойств в hello существующей сущности.</span><span class="sxs-lookup"><span data-stu-id="16dbd-144">**insert\_or\_replace\_entity():** Updates an existing entity by merging new property values into hello existing entity.</span></span> <span data-ttu-id="16dbd-145">Если сущность не существует, будет вставлена новая сущность.</span><span class="sxs-lookup"><span data-stu-id="16dbd-145">If no entity exists, a new one will be inserted.</span></span>

<span data-ttu-id="16dbd-146">Hello ниже приведен пример обновления сущности, используя **обновление\_entity()**:</span><span class="sxs-lookup"><span data-stu-id="16dbd-146">hello following example demonstrates updating an entity using **update\_entity()**:</span></span>

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

<span data-ttu-id="16dbd-147">С **обновление\_entity()** и **слияния\_entity()**, если сущности hello, обновление которого не существует, операция обновления hello завершается с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="16dbd-147">With **update\_entity()** and **merge\_entity()**, if hello entity that you are updating doesn't exist then hello update operation will fail.</span></span> <span data-ttu-id="16dbd-148">Поэтому если вы хотите toostore сущности независимо от того, является ли он уже существует, следует использовать **вставить\_или\_заменить\_entity()** или **вставить\_или \_слияния\_entity()**.</span><span class="sxs-lookup"><span data-stu-id="16dbd-148">Therefore if you wish toostore an entity regardless of whether it already exists, you should instead use **insert\_or\_replace\_entity()** or **insert\_or\_merge\_entity()**.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="16dbd-149">Работа с группами сущностей</span><span class="sxs-lookup"><span data-stu-id="16dbd-149">Work with groups of entities</span></span>
<span data-ttu-id="16dbd-150">Иногда он делает toosubmit смысле несколько операций друг с другом в tooensure пакета atomic обработки сервером hello.</span><span class="sxs-lookup"><span data-stu-id="16dbd-150">Sometimes it makes sense toosubmit multiple operations together in a batch tooensure atomic processing by hello server.</span></span> <span data-ttu-id="16dbd-151">tooaccomplish, сначала необходимо создать **пакета** объекта, а затем использовать hello **выполнение\_batch()** метод **TableService**.</span><span class="sxs-lookup"><span data-stu-id="16dbd-151">tooaccomplish that, you first create a **Batch** object and then use hello **execute\_batch()** method on **TableService**.</span></span> <span data-ttu-id="16dbd-152">Hello ниже приведен пример отправки две сущности с RowKey 2 и 3 в пакете.</span><span class="sxs-lookup"><span data-stu-id="16dbd-152">hello following example demonstrates submitting two entities with RowKey 2 and 3 in a batch.</span></span> <span data-ttu-id="16dbd-153">Обратите внимание что он только работает для сущностей с hello же PartitionKey.</span><span class="sxs-lookup"><span data-stu-id="16dbd-153">Notice that it only works for entities with hello same PartitionKey.</span></span>

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="16dbd-154">Запрос сущности</span><span class="sxs-lookup"><span data-stu-id="16dbd-154">Query for an entity</span></span>
<span data-ttu-id="16dbd-155">сущности в таблице, используйте hello tooquery **получить\_entity()** метод путем передачи имени таблицы hello, **PartitionKey** и **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="16dbd-155">tooquery an entity in a table, use hello **get\_entity()** method, by passing hello table name, **PartitionKey** and **RowKey**.</span></span>

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="16dbd-156">Запрос набора сущностей</span><span class="sxs-lookup"><span data-stu-id="16dbd-156">Query a set of entities</span></span>
<span data-ttu-id="16dbd-157">tooquery набора сущностей в таблице, создать хэш-объект запроса и использовать hello **запроса\_entities()** метод.</span><span class="sxs-lookup"><span data-stu-id="16dbd-157">tooquery a set of entities in a table, create a query hash object and use hello **query\_entities()** method.</span></span> <span data-ttu-id="16dbd-158">Hello следующем примере показано получение всех сущностей hello hello же **PartitionKey**:</span><span class="sxs-lookup"><span data-stu-id="16dbd-158">hello following example demonstrates getting all hello entities with hello same **PartitionKey**:</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> <span data-ttu-id="16dbd-159">Если результирующий набор hello слишком велик для tooreturn одного запроса, токен продолжения будут возвращены которого производится tooretrieve последующих страницах.</span><span class="sxs-lookup"><span data-stu-id="16dbd-159">If hello result set is too large for a single query tooreturn, a continuation token will be returned which you can use tooretrieve subsequent pages.</span></span>
>
>

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="16dbd-160">Запрос подмножества свойств сущности</span><span class="sxs-lookup"><span data-stu-id="16dbd-160">Query a subset of entity properties</span></span>
<span data-ttu-id="16dbd-161">Таблицы tooa запроса можно получить только несколько свойств сущности.</span><span class="sxs-lookup"><span data-stu-id="16dbd-161">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="16dbd-162">Этот метод, который называется "проекцией", снижает потребление пропускной способности и может повысить производительность запросов, особенно для крупных сущностей.</span><span class="sxs-lookup"><span data-stu-id="16dbd-162">This technique, called "projection", reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="16dbd-163">Предложение select используется hello и передайте hello имена hello свойства toobring через toohello клиента.</span><span class="sxs-lookup"><span data-stu-id="16dbd-163">Use hello select clause and pass hello names of hello properties you would like toobring over toohello client.</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a><span data-ttu-id="16dbd-164">Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="16dbd-164">Delete an entity</span></span>
<span data-ttu-id="16dbd-165">toodelete сущности, используйте hello **удаление\_entity()** метод.</span><span class="sxs-lookup"><span data-stu-id="16dbd-165">toodelete an entity, use hello **delete\_entity()** method.</span></span> <span data-ttu-id="16dbd-166">Вы должны toopass в качестве имени hello hello таблица, содержащая сущность hello, hello PartitionKey и RowKey hello сущности.</span><span class="sxs-lookup"><span data-stu-id="16dbd-166">You need toopass in hello name of hello table which contains hello entity, hello PartitionKey and RowKey of hello entity.</span></span>

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a><span data-ttu-id="16dbd-167">Удаление таблицы</span><span class="sxs-lookup"><span data-stu-id="16dbd-167">Delete a table</span></span>
<span data-ttu-id="16dbd-168">toodelete таблицы, используйте hello **удаление\_table()** метод и передайте имя hello hello toodelete таблицу.</span><span class="sxs-lookup"><span data-stu-id="16dbd-168">toodelete a table, use hello **delete\_table()** method and pass in hello name of hello table you want toodelete.</span></span>

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a><span data-ttu-id="16dbd-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="16dbd-169">Next steps</span></span>

* <span data-ttu-id="16dbd-170">[Обозреватель хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) является бесплатной, отдельное приложение от Майкрософт, позволяющая toowork визуально с помощью данных из хранилища Azure в Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="16dbd-170">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="16dbd-171">[пакетов SDK Azure для Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) на веб-сайте GitHub</span><span class="sxs-lookup"><span data-stu-id="16dbd-171">[Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

