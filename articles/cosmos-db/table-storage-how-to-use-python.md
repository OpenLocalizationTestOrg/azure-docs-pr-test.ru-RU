---
title: "aaaHow toouse хранилище таблиц Azure с Python | Документы Microsoft"
description: "Хранения структурированных данных в облаке hello, с помощью хранилища таблиц Azure, хранилище данных NoSQL."
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 7ddb9f3e-4e6d-4103-96e6-f0351d69a17b
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/16/2017
ms.author: mimig
ms.openlocfilehash: 3382fcd5667a93d5533b5f8fad1d3d1c27f23482
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-in-python"></a>Как toouse хранилища таблиц на Python

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

В этом руководстве показано, как hello распространенных сценариев хранилища таблиц Azure tooperform в Python с помощью [пакет SDK хранилища Microsoft Azure для Python](https://github.com/Azure/azure-storage-python). Hello сценарии включают создание и удаление таблицы, вставка и выполнения запросов к сущностям.

При одновременной ликвидации hello сценарии в этом учебнике вы можете toorefer toohello [пакет SDK хранилища Azure для Python API-ссылка](https://azure-storage.readthedocs.io/en/latest/index.html).

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-hello-azure-storage-sdk-for-python"></a>Установка hello пакет SDK хранилища Azure для Python

После создания учетной записи хранилища, следующим шагом является tooinstall hello [пакет SDK хранилища Microsoft Azure для Python](https://github.com/Azure/azure-storage-python). Для получения сведений об установке hello SDK, см. toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) файл hello SDK хранилища для репозитория Python на GitHub.

## <a name="create-a-table"></a>Создание таблицы

toowork с hello Python службы таблиц Azure, необходимо импортировать hello [TableService] [ py_TableService] модуля. Поскольку вы будете работать с сущностями в таблице, необходимо также hello [сущности] [ py_Entity] класса. Добавьте следующий код верхней hello вашей Python файл tooimport оба.

```python
from azure.storage.table import TableService, Entity
```

Создайте объект [TableService][py_TableService], передав ключ учетной записи и имя учетной записи хранения. Замените `myaccount` и `mykey` имя учетной записи и ключа и вызова [create_table] [ py_create_table] toocreate hello таблица в хранилище Azure.

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-tooa-table"></a>Добавьте таблицу tooa сущности

tooadd сущность сначала создать объект, представляющий сущности, затем передайте hello объекта toohello [TableService][py_TableService].[ insert_entity] [ py_insert_entity] метод. Hello объекта сущности может быть словарь или объект типа [сущности][py_Entity]и определяет вашего лица имена и значения свойств. Каждой сущности должны содержать необходимые hello [PartitionKey и RowKey](#partitionkey-and-rowkey) свойства, в добавление tooany другие свойства необходимо указать для сущности hello.

В этом примере создается объект словаря представляет сущность, затем передает его toohello [insert_entity] [ py_insert_entity] tooadd метод его toohello таблицы:

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

В этом примере создается [сущности] [ py_Entity] объекта, а затем передает его toohello [insert_entity] [ py_insert_entity] tooadd метод его toohello таблицы:

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash hello car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a>PartitionKey и RowKey

Для каждой сущности необходимо указать свойства **PartitionKey** и **RowKey**. Это hello уникальные идентификаторы объектов, как вместе они формируют hello первичного ключа сущности. С помощью этих значений можно отправлять запросы быстрее, чем к другим свойствам, так как индексируются только эти свойства.

Здравствуйте, служба таблиц использует **PartitionKey** toointelligently распределения таблицы сущностей по узлам хранилища. Сущности, которые hello же **PartitionKey** хранятся на hello того же узла. **RowKey** hello уникальным идентификатором hello сущности внутри раздела hello, он принадлежит.

## <a name="update-an-entity"></a>Обновление сущности

tooupdate всех значений свойств сущности, вызовите hello [update_entity] [ py_update_entity] метод. В этом примере показано, как tooreplace существующую сущность с обновленной версии:

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

Если hello сущности, которая обновляется еще не существует, то hello операция обновления завершится ошибкой. Toostore сущность ли он существует, или нет, используйте [insert_or_replace_entity][py_insert_or_replace_entity]. В следующем примере hello первый вызов hello заменяет существующую сущность hello. При втором вызове Hello вставит новую сущность, так как сущность с hello указан PartitionKey и RowKey существует в таблице hello.

```python
# Replace hello entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> Hello [update_entity] [ py_update_entity] метод заменяет все свойства и значения существующей сущности, который затем можно также использовать свойства tooremove из имеющейся сущности. Можно использовать hello [merge_entity] [ py_merge_entity] tooupdate метод существующей сущности со значениями новых или измененных свойств без полной замены hello сущности.

## <a name="modify-multiple-entities"></a>Изменение нескольких сущностей

tooensure Здравствуйте atomic обработки запроса службой таблиц hello, вы можете отправить несколько операций вместе в одном пакете. Во-первых, используйте hello [TableBatch] [ py_TableBatch] класса tooadd один пакет нескольких операций tooa. Затем вызовите [TableService][py_TableService].[ commit_batch] [ py_commit_batch] toosubmit операции hello в атомарной операции. Все сущности toobe, изменения в пакете должны находиться в hello одной секции.

В этом примере показано добавление двух сущностей в пакете:

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean hello bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

Пакеты также может использоваться с синтаксисом диспетчера контекста hello:

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean hello bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a>Запрос сущности

tooquery для сущности в таблице, передать его PartitionKey и RowKey toohello [TableService][py_TableService].[ get_entity] [ py_get_entity] метод.

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a>Запрос набора сущностей

Вы можете запросить набор сущностей, указав строку фильтра с hello **фильтра** параметра. Этот пример находит все задачи в Сиэтле, используя фильтр PartitionKey:

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a>Запрос подмножества свойств сущности

Также можно ограничить свойства, возвращаемые для каждой сущности в запросе. Этот метод, который называется *проекцией*, снижает потребление пропускной способности и может повысить производительность запросов, особенно для больших сущностей и наборов результатов. Используйте hello **выберите** имена параметра и передайте hello hello свойства, которые вы хотите вернул toohello клиента.

запрос Hello в hello, следующий код возвращает только hello описания сущности в таблице hello.

> [!NOTE]
> Здравствуйте, следующий фрагмент кода работает только с hello хранилища Azure. Не поддерживается эмулятором хранилища hello.

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a>Удаление сущности

Удаление сущности, передав его PartitionKey и RowKey toohello [delete_entity] [ py_delete_entity] метод.

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a>Удаление таблицы

Если вы больше не нужна, таблицы или любого hello сущностей внутри него, вызовите hello [delete_table] [ py_delete_table] toopermanently метод удалить таблицу hello из хранилища Azure.

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a>Дальнейшие действия

* [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html) (Справочник по пакету SDK службы хранилища Azure для API Python)
* [Пакет SDK службы хранилища Azure для Python](https://github.com/Azure/azure-storage-python)
* [Центр по разработке для Python](https://azure.microsoft.com/develop/python/)
* [Приступая к работе с обозревателем службы хранилища (предварительная версия)](../vs-azure-tools-storage-manage-with-storage-explorer.md). Обозреватель службы хранилища Microsoft Azure — бесплатное кроссплатформенное приложение для визуализации данных службы хранилища Azure в Windows, macOS и Linux.

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
