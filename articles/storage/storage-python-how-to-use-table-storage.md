---
title: "Как использовать хранилище таблиц Azure с Python | Документация Майкрософт"
description: "Хранение структурированных данных в облаке в хранилище таблиц Azure (хранилище данных NoSQL)."
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
ms.openlocfilehash: c310a52182bbc3cf44ed4dc6a04e97aa59200a64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-table-storage-in-python"></a><span data-ttu-id="89c67-103">Как использовать хранилище таблиц в Python</span><span class="sxs-lookup"><span data-stu-id="89c67-103">How to use Table storage in Python</span></span>

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

<span data-ttu-id="89c67-104">В этом руководстве объясняется, как реализовать типичные сценарии хранилища таблиц Azure в Python с помощью [пакета SDK для службы хранилища Microsoft Azure для Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="89c67-104">This guide shows you how to perform common Azure Table storage scenarios in Python using the [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="89c67-105">Здесь описаны такие сценарии, как создание и удаление таблицы, вставка и запрос сущностей.</span><span class="sxs-lookup"><span data-stu-id="89c67-105">The scenarios covered include creating and deleting a table, and inserting and querying entities.</span></span>

<span data-ttu-id="89c67-106">Работая над сценариями в этом руководстве, вы можете использовать в качестве справки [пакет SDK для службы хранилища Microsoft Azure для Python](https://azure-storage.readthedocs.io/en/latest/index.html).</span><span class="sxs-lookup"><span data-stu-id="89c67-106">While working through the scenarios in this tutorial, you may wish to refer to the [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-the-azure-storage-sdk-for-python"></a><span data-ttu-id="89c67-107">Установка пакета SDK для службы хранилища Microsoft Azure для Python</span><span class="sxs-lookup"><span data-stu-id="89c67-107">Install the Azure Storage SDK for Python</span></span>

<span data-ttu-id="89c67-108">После создания учетной записи хранения установите [пакет SDK для службы хранилища Microsoft Azure для Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="89c67-108">Once you've created a storage account, your next step is to install the [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="89c67-109">Дополнительные сведения по установке пакета SDK см. в файле [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) в репозитории GitHub Storage SDK for Python (пакет SDK для службы хранилища для Python).</span><span class="sxs-lookup"><span data-stu-id="89c67-109">For details on installing the SDK, refer to the [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) file in the Storage SDK for Python repository on GitHub.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="89c67-110">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="89c67-110">Create a table</span></span>

<span data-ttu-id="89c67-111">Для работы со службой таблиц Azure в Python необходимо импортировать модуль [TableService][py_TableService].</span><span class="sxs-lookup"><span data-stu-id="89c67-111">To work with the Azure Table service in Python, you must import the [TableService][py_TableService] module.</span></span> <span data-ttu-id="89c67-112">Так как вы будете работать с сущностями в таблице, вам также нужен класс [Entity][py_Entity].</span><span class="sxs-lookup"><span data-stu-id="89c67-112">Since you'll be working with Table entities, you also need the [Entity][py_Entity] class.</span></span> <span data-ttu-id="89c67-113">Добавьте следующий код в начало файла Python, чтобы импортировать модуль и класс:</span><span class="sxs-lookup"><span data-stu-id="89c67-113">Add this code near the top your Python file to import both:</span></span>

```python
from azure.storage.table import TableService, Entity
```

<span data-ttu-id="89c67-114">Создайте объект [TableService][py_TableService], передав ключ учетной записи и имя учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="89c67-114">Create a [TableService][py_TableService] object, passing in your storage account name and account key.</span></span> <span data-ttu-id="89c67-115">Замените `myaccount` и `mykey` именем и ключом своей учетной записи и вызовите метод [create_table][py_create_table], чтобы создать таблицу в службе хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="89c67-115">Replace `myaccount` and `mykey` with your account name and key, and call [create_table][py_create_table] to create the table in Azure Storage.</span></span>

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="89c67-116">Добавление сущности в таблицу</span><span class="sxs-lookup"><span data-stu-id="89c67-116">Add an entity to a table</span></span>

<span data-ttu-id="89c67-117">Чтобы добавить сущность, сначала создайте объект, который представляет сущность, затем передайте объект в метод [TableService][py_TableService].[insert_entity][py_insert_entity].</span><span class="sxs-lookup"><span data-stu-id="89c67-117">To add an entity, you first create an object that represents your entity, then pass the object to the [TableService][py_TableService].[insert_entity][py_insert_entity] method.</span></span> <span data-ttu-id="89c67-118">Объект сущности может быть словарем или объектом типа [Entity][py_Entity]. Он определяет имена и значения свойств сущности.</span><span class="sxs-lookup"><span data-stu-id="89c67-118">The entity object can be a dictionary or an object of type [Entity][py_Entity], and defines your entity's property names and values.</span></span> <span data-ttu-id="89c67-119">Каждая сущность должна включать требуемые свойства [PartitionKey и RowKey](#partitionkey-and-rowkey) помимо других свойств, определенных для сущности.</span><span class="sxs-lookup"><span data-stu-id="89c67-119">Every entity must include the required [PartitionKey and RowKey](#partitionkey-and-rowkey) properties, in addition to any other properties you define for the entity.</span></span>

<span data-ttu-id="89c67-120">В этом примере создается объект словаря, который представляет сущность, а затем передает его в метод [insert_entity][py_insert_entity], чтобы добавить его в таблицу:</span><span class="sxs-lookup"><span data-stu-id="89c67-120">This example creates a dictionary object representing an entity, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

<span data-ttu-id="89c67-121">В этом примере создается объект [Entity][py_Entity], а затем передает его в метод [insert_entity][py_insert_entity], чтобы добавить его в таблицу:</span><span class="sxs-lookup"><span data-stu-id="89c67-121">This example creates an [Entity][py_Entity] object, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span></span>

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash the car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a><span data-ttu-id="89c67-122">PartitionKey и RowKey</span><span class="sxs-lookup"><span data-stu-id="89c67-122">PartitionKey and RowKey</span></span>

<span data-ttu-id="89c67-123">Для каждой сущности необходимо указать свойства **PartitionKey** и **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="89c67-123">You must specify both a **PartitionKey** and a **RowKey** property for every entity.</span></span> <span data-ttu-id="89c67-124">Это уникальные идентификаторы сущностей, так как вместе они формируют первичный ключ сущности.</span><span class="sxs-lookup"><span data-stu-id="89c67-124">These are the unique identifiers of your entities, as together they form the primary key of an entity.</span></span> <span data-ttu-id="89c67-125">С помощью этих значений можно отправлять запросы быстрее, чем к другим свойствам, так как индексируются только эти свойства.</span><span class="sxs-lookup"><span data-stu-id="89c67-125">You can query using these values much faster than you can query any other entity properties because only these properties are indexed.</span></span>

<span data-ttu-id="89c67-126">Служба таблиц использует **PartitionKey** для интеллектуального распределения сущностей таблицы по узлам хранилища.</span><span class="sxs-lookup"><span data-stu-id="89c67-126">The Table service uses **PartitionKey** to intelligently distribute table entities across storage nodes.</span></span> <span data-ttu-id="89c67-127">Сущности с одним значением **PartitionKey** хранятся на одном узле.</span><span class="sxs-lookup"><span data-stu-id="89c67-127">Entities that have the same  **PartitionKey** are stored on the same node.</span></span> <span data-ttu-id="89c67-128">**RowKey** — это уникальный идентификатор сущности в разделе, которому она принадлежит.</span><span class="sxs-lookup"><span data-stu-id="89c67-128">**RowKey** is the unique ID of the entity within the partition it belongs to.</span></span>

## <a name="update-an-entity"></a><span data-ttu-id="89c67-129">Обновление сущности</span><span class="sxs-lookup"><span data-stu-id="89c67-129">Update an entity</span></span>

<span data-ttu-id="89c67-130">Чтобы обновить все значения свойств сущности, вызовите метод [update_entity][py_update_entity].</span><span class="sxs-lookup"><span data-stu-id="89c67-130">To update all of an entity's property values, call the [update_entity][py_update_entity] method.</span></span> <span data-ttu-id="89c67-131">Этот пример показывает, как заменить сущность обновленной версией:</span><span class="sxs-lookup"><span data-stu-id="89c67-131">This example shows how to replace an existing entity with an updated version:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

<span data-ttu-id="89c67-132">Если обновляемая сущность больше не существует, операция обновления завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="89c67-132">If the entity that is being updated doesn't already exist, then the update operation will fail.</span></span> <span data-ttu-id="89c67-133">Если вы хотите сохранить сущность независимо от того, существует она или нет, используйте метод [insert_or_replace_entity][py_insert_or_replace_entity].</span><span class="sxs-lookup"><span data-stu-id="89c67-133">If you want to store an entity whether it exists or not, use [insert_or_replace_entity][py_insert_or_replace_entity].</span></span> <span data-ttu-id="89c67-134">В следующем примере первый вызов заменит существующую сущность.</span><span class="sxs-lookup"><span data-stu-id="89c67-134">In the following example, the first call will replace the existing entity.</span></span> <span data-ttu-id="89c67-135">Второй вызов вставит новую сущность, так как в таблице нет сущности с указанными свойствами PartitionKey и RowKey.</span><span class="sxs-lookup"><span data-stu-id="89c67-135">The second call will insert a new entity, since no entity with the specified PartitionKey and RowKey exists in the table.</span></span>

```python
# Replace the entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> <span data-ttu-id="89c67-136">Метод [update_entity][py_update_entity] заменяет все свойства и значения сущности. Его также можно использовать для удаления свойства из сущности.</span><span class="sxs-lookup"><span data-stu-id="89c67-136">The [update_entity][py_update_entity] method replaces all properties and values of an existing entity, which you can also use to remove properties from an existing entity.</span></span> <span data-ttu-id="89c67-137">Чтобы обновить сущность с помощью новых или измененных значений свойств без полной замены сущности используйте метод [merge_entity][py_merge_entity].</span><span class="sxs-lookup"><span data-stu-id="89c67-137">You can use the [merge_entity][py_merge_entity] method to update an existing entity with new or modified property values without completely replacing the entity.</span></span>

## <a name="modify-multiple-entities"></a><span data-ttu-id="89c67-138">Изменение нескольких сущностей</span><span class="sxs-lookup"><span data-stu-id="89c67-138">Modify multiple entities</span></span>

<span data-ttu-id="89c67-139">Для атомарной обработки запроса службой таблиц можно отправить сразу несколько операций в пакете.</span><span class="sxs-lookup"><span data-stu-id="89c67-139">To ensure the atomic processing of a request by the Table service, you can submit multiple operations together in a batch.</span></span> <span data-ttu-id="89c67-140">Сначала используйте класс [TableBatch][py_TableBatch], чтобы добавить несколько операций в одном пакете.</span><span class="sxs-lookup"><span data-stu-id="89c67-140">First, use the [TableBatch][py_TableBatch] class to add multiple operations to a single batch.</span></span> <span data-ttu-id="89c67-141">Затем вызовите метод [TableService][py_TableService].[commit_batch][py_commit_batch], чтобы отправить операции в атомарной операции.</span><span class="sxs-lookup"><span data-stu-id="89c67-141">Next, call [TableService][py_TableService].[commit_batch][py_commit_batch] to submit the operations in an atomic operation.</span></span> <span data-ttu-id="89c67-142">Все сущности, которые должны быть изменены в пакете, должны находиться в одном разделе.</span><span class="sxs-lookup"><span data-stu-id="89c67-142">All entities to be modified in batch must be in the same partition.</span></span>

<span data-ttu-id="89c67-143">В этом примере показано добавление двух сущностей в пакете:</span><span class="sxs-lookup"><span data-stu-id="89c67-143">This example adds two entities together in a batch:</span></span>

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean the bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

<span data-ttu-id="89c67-144">Для пакетов также можно использовать синтаксис диспетчера контекста:</span><span class="sxs-lookup"><span data-stu-id="89c67-144">Batches can also be used with the context manager syntax:</span></span>

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean the bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="89c67-145">Запрос сущности</span><span class="sxs-lookup"><span data-stu-id="89c67-145">Query for an entity</span></span>

<span data-ttu-id="89c67-146">Чтобы запросить сущность в таблице, передайте ее свойства PartitionKey и RowKey в метод [TableService][py_TableService].[get_entity][py_get_entity].</span><span class="sxs-lookup"><span data-stu-id="89c67-146">To query for an entity in a table, pass its PartitionKey and RowKey to the [TableService][py_TableService].[get_entity][py_get_entity] method.</span></span>

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="89c67-147">Запрос набора сущностей</span><span class="sxs-lookup"><span data-stu-id="89c67-147">Query a set of entities</span></span>

<span data-ttu-id="89c67-148">Можно запросить набор сущностей, указав строку фильтра с помощью параметра **filter**.</span><span class="sxs-lookup"><span data-stu-id="89c67-148">You can query for a set of entities by supplying a filter string with the **filter** parameter.</span></span> <span data-ttu-id="89c67-149">Этот пример находит все задачи в Сиэтле, используя фильтр PartitionKey:</span><span class="sxs-lookup"><span data-stu-id="89c67-149">This example finds all tasks in Seattle by applying a filter on PartitionKey:</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="89c67-150">Запрос подмножества свойств сущности</span><span class="sxs-lookup"><span data-stu-id="89c67-150">Query a subset of entity properties</span></span>

<span data-ttu-id="89c67-151">Также можно ограничить свойства, возвращаемые для каждой сущности в запросе.</span><span class="sxs-lookup"><span data-stu-id="89c67-151">You can also restrict which properties are returned for each entity in a query.</span></span> <span data-ttu-id="89c67-152">Этот метод, который называется *проекцией*, снижает потребление пропускной способности и может повысить производительность запросов, особенно для больших сущностей и наборов результатов.</span><span class="sxs-lookup"><span data-stu-id="89c67-152">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities or result sets.</span></span> <span data-ttu-id="89c67-153">Используйте параметр **select** и передайте имена свойств, которые необходимо вернуть клиенту.</span><span class="sxs-lookup"><span data-stu-id="89c67-153">Use the **select** parameter and pass the names of the properties you want returned to the client.</span></span>

<span data-ttu-id="89c67-154">Запрос в следующем коде возвращает только описания сущностей в таблице.</span><span class="sxs-lookup"><span data-stu-id="89c67-154">The query in the following code returns only the descriptions of entities in the table.</span></span>

> [!NOTE]
> <span data-ttu-id="89c67-155">Следующий фрагмент работает только для службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="89c67-155">The following snippet works only against the Azure Storage.</span></span> <span data-ttu-id="89c67-156">Его не поддерживает эмулятор хранения.</span><span class="sxs-lookup"><span data-stu-id="89c67-156">It is not supported by the storage emulator.</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a><span data-ttu-id="89c67-157">Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="89c67-157">Delete an entity</span></span>

<span data-ttu-id="89c67-158">Чтобы удалить сущность, передайте ее свойства PartitionKey и RowKey в метод [delete_entity][py_delete_entity].</span><span class="sxs-lookup"><span data-stu-id="89c67-158">Delete an entity by passing its PartitionKey and RowKey to the [delete_entity][py_delete_entity] method.</span></span>

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a><span data-ttu-id="89c67-159">Удаление таблицы</span><span class="sxs-lookup"><span data-stu-id="89c67-159">Delete a table</span></span>

<span data-ttu-id="89c67-160">Если вам больше не нужна таблица или сущность в ней, вызовите метод [delete_table][py_delete_table], чтобы полностью удалить таблицу из службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="89c67-160">If you no longer need a table or any of the entities within it, call the [delete_table][py_delete_table] method to permanently delete the table from Azure Storage.</span></span>

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a><span data-ttu-id="89c67-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="89c67-161">Next steps</span></span>

* <span data-ttu-id="89c67-162">[Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html) (Справочник по пакету SDK службы хранилища Azure для API Python)</span><span class="sxs-lookup"><span data-stu-id="89c67-162">[Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html)</span></span>
* [<span data-ttu-id="89c67-163">Пакет SDK службы хранилища Azure для Python</span><span class="sxs-lookup"><span data-stu-id="89c67-163">Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)
* [<span data-ttu-id="89c67-164">Центр по разработке для Python</span><span class="sxs-lookup"><span data-stu-id="89c67-164">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* <span data-ttu-id="89c67-165">[Приступая к работе с обозревателем службы хранилища (предварительная версия)](../vs-azure-tools-storage-manage-with-storage-explorer.md). Обозреватель службы хранилища Microsoft Azure — бесплатное кроссплатформенное приложение для визуализации данных службы хранилища Azure в Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="89c67-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): A free, cross-platform application for working visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

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
