---
title: "aaaHow toouse хранилище таблиц Azure с Python | Документы Microsoft"
description: "Хранения структурированных данных в облаке hello, с помощью хранилища таблиц Azure, хранилище данных NoSQL."
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 7ddb9f3e-4e6d-4103-96e6-f0351d69a17b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/16/2017
ms.author: marsma
ms.openlocfilehash: fd0e1b05cc12618f348eaf2d85d0dce5ac32702a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-in-python"></a><span data-ttu-id="37382-103">Как toouse хранилища таблиц на Python</span><span class="sxs-lookup"><span data-stu-id="37382-103">How toouse Table storage in Python</span></span>

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

<span data-ttu-id="37382-104">В этом руководстве показано, как hello распространенных сценариев хранилища таблиц Azure tooperform в Python с помощью [пакет SDK хранилища Microsoft Azure для Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="37382-104">This guide shows you how tooperform common Azure Table storage scenarios in Python using hello [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="37382-105">Hello сценарии включают создание и удаление таблицы, вставка и выполнения запросов к сущностям.</span><span class="sxs-lookup"><span data-stu-id="37382-105">hello scenarios covered include creating and deleting a table, and inserting and querying entities.</span></span>

<span data-ttu-id="37382-106">При одновременной ликвидации hello сценарии в этом учебнике вы можете toorefer toohello [пакет SDK хранилища Azure для Python API-ссылка](https://azure-storage.readthedocs.io/en/latest/index.html).</span><span class="sxs-lookup"><span data-stu-id="37382-106">While working through hello scenarios in this tutorial, you may wish toorefer toohello [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-hello-azure-storage-sdk-for-python"></a><span data-ttu-id="37382-107">Установка hello пакет SDK хранилища Azure для Python</span><span class="sxs-lookup"><span data-stu-id="37382-107">Install hello Azure Storage SDK for Python</span></span>

<span data-ttu-id="37382-108">После создания учетной записи хранилища, следующим шагом является tooinstall hello [пакет SDK хранилища Microsoft Azure для Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="37382-108">Once you've created a storage account, your next step is tooinstall hello [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="37382-109">Для получения сведений об установке hello SDK, см. toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) файл hello SDK хранилища для репозитория Python на GitHub.</span><span class="sxs-lookup"><span data-stu-id="37382-109">For details on installing hello SDK, refer toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) file in hello Storage SDK for Python repository on GitHub.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="37382-110">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="37382-110">Create a table</span></span>

<span data-ttu-id="37382-111">toowork с hello Python службы таблиц Azure, необходимо импортировать hello [TableService] [ py_TableService] модуля.</span><span class="sxs-lookup"><span data-stu-id="37382-111">toowork with hello Azure Table service in Python, you must import hello [TableService][py_TableService] module.</span></span> <span data-ttu-id="37382-112">Поскольку вы будете работать с сущностями в таблице, необходимо также hello [сущности] [ py_Entity] класса.</span><span class="sxs-lookup"><span data-stu-id="37382-112">Since you'll be working with Table entities, you also need hello [Entity][py_Entity] class.</span></span> <span data-ttu-id="37382-113">Добавьте следующий код верхней hello вашей Python файл tooimport оба.</span><span class="sxs-lookup"><span data-stu-id="37382-113">Add this code near hello top your Python file tooimport both:</span></span>

```python
from azure.storage.table import TableService, Entity
```

<span data-ttu-id="37382-114">Создайте объект [TableService][py_TableService], передав ключ учетной записи и имя учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="37382-114">Create a [TableService][py_TableService] object, passing in your storage account name and account key.</span></span> <span data-ttu-id="37382-115">Замените `myaccount` и `mykey` имя учетной записи и ключа и вызова [create_table] [ py_create_table] toocreate hello таблица в хранилище Azure.</span><span class="sxs-lookup"><span data-stu-id="37382-115">Replace `myaccount` and `mykey` with your account name and key, and call [create_table][py_create_table] toocreate hello table in Azure Storage.</span></span>

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="37382-116">Добавьте таблицу tooa сущности</span><span class="sxs-lookup"><span data-stu-id="37382-116">Add an entity tooa table</span></span>

<span data-ttu-id="37382-117">tooadd сущность сначала создать объект, представляющий сущности, затем передайте hello объекта toohello [TableService][py_TableService].[ insert_entity] [ py_insert_entity] метод.</span><span class="sxs-lookup"><span data-stu-id="37382-117">tooadd an entity, you first create an object that represents your entity, then pass hello object toohello [TableService][py_TableService].[insert_entity][py_insert_entity] method.</span></span> <span data-ttu-id="37382-118">Hello объекта сущности может быть словарь или объект типа [сущности][py_Entity]и определяет вашего лица имена и значения свойств.</span><span class="sxs-lookup"><span data-stu-id="37382-118">hello entity object can be a dictionary or an object of type [Entity][py_Entity], and defines your entity's property names and values.</span></span> <span data-ttu-id="37382-119">Каждой сущности должны содержать необходимые hello [PartitionKey и RowKey](#partitionkey-and-rowkey) свойства, в добавление tooany другие свойства необходимо указать для сущности hello.</span><span class="sxs-lookup"><span data-stu-id="37382-119">Every entity must include hello required [PartitionKey and RowKey](#partitionkey-and-rowkey) properties, in addition tooany other properties you define for hello entity.</span></span>

<span data-ttu-id="37382-120">В этом примере создается объект словаря представляет сущность, затем передает его toohello [insert_entity] [ py_insert_entity] tooadd метод его toohello таблицы:</span><span class="sxs-lookup"><span data-stu-id="37382-120">This example creates a dictionary object representing an entity, then passes it toohello [insert_entity][py_insert_entity] method tooadd it toohello table:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

<span data-ttu-id="37382-121">В этом примере создается [сущности] [ py_Entity] объекта, а затем передает его toohello [insert_entity] [ py_insert_entity] tooadd метод его toohello таблицы:</span><span class="sxs-lookup"><span data-stu-id="37382-121">This example creates an [Entity][py_Entity] object, then passes it toohello [insert_entity][py_insert_entity] method tooadd it toohello table:</span></span>

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash hello car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a><span data-ttu-id="37382-122">PartitionKey и RowKey</span><span class="sxs-lookup"><span data-stu-id="37382-122">PartitionKey and RowKey</span></span>

<span data-ttu-id="37382-123">Для каждой сущности необходимо указать свойства **PartitionKey** и **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="37382-123">You must specify both a **PartitionKey** and a **RowKey** property for every entity.</span></span> <span data-ttu-id="37382-124">Это hello уникальные идентификаторы объектов, как вместе они формируют hello первичного ключа сущности.</span><span class="sxs-lookup"><span data-stu-id="37382-124">These are hello unique identifiers of your entities, as together they form hello primary key of an entity.</span></span> <span data-ttu-id="37382-125">С помощью этих значений можно отправлять запросы быстрее, чем к другим свойствам, так как индексируются только эти свойства.</span><span class="sxs-lookup"><span data-stu-id="37382-125">You can query using these values much faster than you can query any other entity properties because only these properties are indexed.</span></span>

<span data-ttu-id="37382-126">Здравствуйте, служба таблиц использует **PartitionKey** toointelligently распределения таблицы сущностей по узлам хранилища.</span><span class="sxs-lookup"><span data-stu-id="37382-126">hello Table service uses **PartitionKey** toointelligently distribute table entities across storage nodes.</span></span> <span data-ttu-id="37382-127">Сущности, которые hello же **PartitionKey** хранятся на hello того же узла.</span><span class="sxs-lookup"><span data-stu-id="37382-127">Entities that have hello same  **PartitionKey** are stored on hello same node.</span></span> <span data-ttu-id="37382-128">**RowKey** hello уникальным идентификатором hello сущности внутри раздела hello, он принадлежит.</span><span class="sxs-lookup"><span data-stu-id="37382-128">**RowKey** is hello unique ID of hello entity within hello partition it belongs to.</span></span>

## <a name="update-an-entity"></a><span data-ttu-id="37382-129">Обновление сущности</span><span class="sxs-lookup"><span data-stu-id="37382-129">Update an entity</span></span>

<span data-ttu-id="37382-130">tooupdate всех значений свойств сущности, вызовите hello [update_entity] [ py_update_entity] метод.</span><span class="sxs-lookup"><span data-stu-id="37382-130">tooupdate all of an entity's property values, call hello [update_entity][py_update_entity] method.</span></span> <span data-ttu-id="37382-131">В этом примере показано, как tooreplace существующую сущность с обновленной версии:</span><span class="sxs-lookup"><span data-stu-id="37382-131">This example shows how tooreplace an existing entity with an updated version:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

<span data-ttu-id="37382-132">Если hello сущности, которая обновляется еще не существует, то hello операция обновления завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="37382-132">If hello entity that is being updated doesn't already exist, then hello update operation will fail.</span></span> <span data-ttu-id="37382-133">Toostore сущность ли он существует, или нет, используйте [insert_or_replace_entity][py_insert_or_replace_entity].</span><span class="sxs-lookup"><span data-stu-id="37382-133">If you want toostore an entity whether it exists or not, use [insert_or_replace_entity][py_insert_or_replace_entity].</span></span> <span data-ttu-id="37382-134">В следующем примере hello первый вызов hello заменяет существующую сущность hello.</span><span class="sxs-lookup"><span data-stu-id="37382-134">In hello following example, hello first call will replace hello existing entity.</span></span> <span data-ttu-id="37382-135">При втором вызове Hello вставит новую сущность, так как сущность с hello указан PartitionKey и RowKey существует в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="37382-135">hello second call will insert a new entity, since no entity with hello specified PartitionKey and RowKey exists in hello table.</span></span>

```python
# Replace hello entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> <span data-ttu-id="37382-136">Hello [update_entity] [ py_update_entity] метод заменяет все свойства и значения существующей сущности, который затем можно также использовать свойства tooremove из имеющейся сущности.</span><span class="sxs-lookup"><span data-stu-id="37382-136">hello [update_entity][py_update_entity] method replaces all properties and values of an existing entity, which you can also use tooremove properties from an existing entity.</span></span> <span data-ttu-id="37382-137">Можно использовать hello [merge_entity] [ py_merge_entity] tooupdate метод существующей сущности со значениями новых или измененных свойств без полной замены hello сущности.</span><span class="sxs-lookup"><span data-stu-id="37382-137">You can use hello [merge_entity][py_merge_entity] method tooupdate an existing entity with new or modified property values without completely replacing hello entity.</span></span>

## <a name="modify-multiple-entities"></a><span data-ttu-id="37382-138">Изменение нескольких сущностей</span><span class="sxs-lookup"><span data-stu-id="37382-138">Modify multiple entities</span></span>

<span data-ttu-id="37382-139">tooensure Здравствуйте atomic обработки запроса службой таблиц hello, вы можете отправить несколько операций вместе в одном пакете.</span><span class="sxs-lookup"><span data-stu-id="37382-139">tooensure hello atomic processing of a request by hello Table service, you can submit multiple operations together in a batch.</span></span> <span data-ttu-id="37382-140">Во-первых, используйте hello [TableBatch] [ py_TableBatch] класса tooadd один пакет нескольких операций tooa.</span><span class="sxs-lookup"><span data-stu-id="37382-140">First, use hello [TableBatch][py_TableBatch] class tooadd multiple operations tooa single batch.</span></span> <span data-ttu-id="37382-141">Затем вызовите [TableService][py_TableService].[ commit_batch] [ py_commit_batch] toosubmit операции hello в атомарной операции.</span><span class="sxs-lookup"><span data-stu-id="37382-141">Next, call [TableService][py_TableService].[commit_batch][py_commit_batch] toosubmit hello operations in an atomic operation.</span></span> <span data-ttu-id="37382-142">Все сущности toobe, изменения в пакете должны находиться в hello одной секции.</span><span class="sxs-lookup"><span data-stu-id="37382-142">All entities toobe modified in batch must be in hello same partition.</span></span>

<span data-ttu-id="37382-143">В этом примере показано добавление двух сущностей в пакете:</span><span class="sxs-lookup"><span data-stu-id="37382-143">This example adds two entities together in a batch:</span></span>

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean hello bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

<span data-ttu-id="37382-144">Пакеты также может использоваться с синтаксисом диспетчера контекста hello:</span><span class="sxs-lookup"><span data-stu-id="37382-144">Batches can also be used with hello context manager syntax:</span></span>

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean hello bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="37382-145">Запрос сущности</span><span class="sxs-lookup"><span data-stu-id="37382-145">Query for an entity</span></span>

<span data-ttu-id="37382-146">tooquery для сущности в таблице, передать его PartitionKey и RowKey toohello [TableService][py_TableService].[ get_entity] [ py_get_entity] метод.</span><span class="sxs-lookup"><span data-stu-id="37382-146">tooquery for an entity in a table, pass its PartitionKey and RowKey toohello [TableService][py_TableService].[get_entity][py_get_entity] method.</span></span>

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="37382-147">Запрос набора сущностей</span><span class="sxs-lookup"><span data-stu-id="37382-147">Query a set of entities</span></span>

<span data-ttu-id="37382-148">Вы можете запросить набор сущностей, указав строку фильтра с hello **фильтра** параметра.</span><span class="sxs-lookup"><span data-stu-id="37382-148">You can query for a set of entities by supplying a filter string with hello **filter** parameter.</span></span> <span data-ttu-id="37382-149">Этот пример находит все задачи в Сиэтле, используя фильтр PartitionKey:</span><span class="sxs-lookup"><span data-stu-id="37382-149">This example finds all tasks in Seattle by applying a filter on PartitionKey:</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="37382-150">Запрос подмножества свойств сущности</span><span class="sxs-lookup"><span data-stu-id="37382-150">Query a subset of entity properties</span></span>

<span data-ttu-id="37382-151">Также можно ограничить свойства, возвращаемые для каждой сущности в запросе.</span><span class="sxs-lookup"><span data-stu-id="37382-151">You can also restrict which properties are returned for each entity in a query.</span></span> <span data-ttu-id="37382-152">Этот метод, который называется *проекцией*, снижает потребление пропускной способности и может повысить производительность запросов, особенно для больших сущностей и наборов результатов.</span><span class="sxs-lookup"><span data-stu-id="37382-152">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities or result sets.</span></span> <span data-ttu-id="37382-153">Используйте hello **выберите** имена параметра и передайте hello hello свойства, которые вы хотите вернул toohello клиента.</span><span class="sxs-lookup"><span data-stu-id="37382-153">Use hello **select** parameter and pass hello names of hello properties you want returned toohello client.</span></span>

<span data-ttu-id="37382-154">запрос Hello в hello, следующий код возвращает только hello описания сущности в таблице hello.</span><span class="sxs-lookup"><span data-stu-id="37382-154">hello query in hello following code returns only hello descriptions of entities in hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="37382-155">Здравствуйте, следующий фрагмент кода работает только с hello хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="37382-155">hello following snippet works only against hello Azure Storage.</span></span> <span data-ttu-id="37382-156">Не поддерживается эмулятором хранилища hello.</span><span class="sxs-lookup"><span data-stu-id="37382-156">It is not supported by hello storage emulator.</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a><span data-ttu-id="37382-157">Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="37382-157">Delete an entity</span></span>

<span data-ttu-id="37382-158">Удаление сущности, передав его PartitionKey и RowKey toohello [delete_entity] [ py_delete_entity] метод.</span><span class="sxs-lookup"><span data-stu-id="37382-158">Delete an entity by passing its PartitionKey and RowKey toohello [delete_entity][py_delete_entity] method.</span></span>

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a><span data-ttu-id="37382-159">Удаление таблицы</span><span class="sxs-lookup"><span data-stu-id="37382-159">Delete a table</span></span>

<span data-ttu-id="37382-160">Если вы больше не нужна, таблицы или любого hello сущностей внутри него, вызовите hello [delete_table] [ py_delete_table] toopermanently метод удалить таблицу hello из хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="37382-160">If you no longer need a table or any of hello entities within it, call hello [delete_table][py_delete_table] method toopermanently delete hello table from Azure Storage.</span></span>

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a><span data-ttu-id="37382-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="37382-161">Next steps</span></span>

* <span data-ttu-id="37382-162">[Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html) (Справочник по пакету SDK службы хранилища Azure для API Python)</span><span class="sxs-lookup"><span data-stu-id="37382-162">[Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html)</span></span>
* [<span data-ttu-id="37382-163">Пакет SDK службы хранилища Azure для Python</span><span class="sxs-lookup"><span data-stu-id="37382-163">Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)
* [<span data-ttu-id="37382-164">Центр по разработке для Python</span><span class="sxs-lookup"><span data-stu-id="37382-164">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* <span data-ttu-id="37382-165">[Приступая к работе с обозревателем службы хранилища (предварительная версия)](../vs-azure-tools-storage-manage-with-storage-explorer.md). Обозреватель службы хранилища Microsoft Azure — бесплатное кроссплатформенное приложение для визуализации данных службы хранилища Azure в Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="37382-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): A free, cross-platform application for working visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

[py_commit_batch]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.commit_batch
[py_create_table]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.create_table
[py_delete_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.delete_entity
[py_delete_table]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.delete_table
[py_Entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.models.html#azure.storage.table.models.Entity
[py_get_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.get_entity
[py_insert_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.insert_entity
[py_insert_or_replace_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.insert_or_replace_entity
[py_merge_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.merge_entity
[py_update_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.update_entity
[py_TableService]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html
[py_TableBatch]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tablebatch.html#azure.storage.table.tablebatch.TableBatch
