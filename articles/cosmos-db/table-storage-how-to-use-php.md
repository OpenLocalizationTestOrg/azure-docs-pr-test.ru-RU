---
title: "Как использовать хранилище таблиц из PHP | Документация Майкрософт"
description: "Вы узнаете, как использовать службу таблиц в PHP для создания и удаления таблиц, вставки, удаления строк и создания запросов для таблиц."
services: cosmos-db
documentationcenter: php
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 1e57f371-6208-4753-b2a0-05db4aede8e3
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 7a48446a11c5c6db0c9f4fdd8872b1e3c12e85c3
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="how-to-use-table-storage-from-php"></a>Использование табличного хранилища из PHP
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Обзор
В этом руководстве показано, как реализовать типичные сценарии с использованием службы таблиц Azure. Примеры написаны на PHP и используют [пакет SDK Azure для PHP][download]. Здесь описаны такие сценарии, как **создание и удаление таблицы, а также вставка, удаление и запрос сущностей в таблице**. Дополнительные сведения о службе таблиц Azure см. в разделе [Дальнейшие действия](#next-steps).

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Создание приложения PHP
Единственным требованием для создания приложения PHP, которое получает доступ к службе таблиц Azure, является ссылка на классы в пакете Azure SDK для PHP непосредственно из кода. Можно использовать любые средства разработки для создания приложения, включая программу "Блокнот".

В этом руководстве используются компоненты службы таблиц, которые могут вызываться локально из приложения PHP или в коде, работающем в веб-роли, рабочей роли или на веб-сайте Azure.

## <a name="get-the-azure-client-libraries"></a>Получение клиентских библиотек Azure
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-the-table-service"></a>Настройка приложения для доступа к службе таблиц
Чтобы использовать интерфейсы API службы таблиц Azure, необходимо следующее:

1. Ссылка на файл автозагрузчика с использованием оператора [require_once][require_once].
2. Ссылка на любые классы, которые могут использоваться.

В следующем примере показано, как включить файл автозагрузчика и сослаться на класс **ServicesBuilder** .

> [!NOTE]
> В примере этой статьи предполагается, что установлены клиентские библиотеки PHP для Azure с помощью Composer. Если вы установили эти библиотеки вручную, то необходимо добавить ссылку на файл автозагрузчика <code>WindowsAzure.php</code> .
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

В приведенных ниже примерах всегда отображается оператор `require_once` , однако ссылки приводятся только на классы, которые необходимы для выполнения этого примера.

## <a name="set-up-an-azure-storage-connection"></a>Настройка подключения к службе хранилища Azure
Для создания клиента службы таблиц Azure необходимо сначала сформировать правильную строку подключения. Формат строки подключения к службе таблиц:

Для доступа к службе в режиме реального времени:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Для доступа к хранилищу эмулятора:

```php
UseDevelopmentStorage=true
```

Чтобы создать клиент любой службы Azure, необходимо использовать класс **ServicesBuilder** . Вы можете:

* передать строку подключения напрямую или
* использовать **CloudConfigurationManager (CCM)** для проверки нескольких внешних источников на наличие строки подключения:
  * по умолчанию предоставляется поддержка одного внешнего источника — переменных среды.
  * можно добавить новые источники, расширив класс **ConnectionStringSource**

В приведенных здесь примерах строка подключения передается напрямую.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a>Создание таблицы
Объект **TableRestProxy** позволяет создать таблицу с помощью метода **createTable**. При создании таблицы можно задать время ожидания службы таблиц. (Дополнительные сведения о времени ожидания службы таблиц см. в статье [Setting Timeouts for Table Service Operations][table-service-timeouts] (Настройка времени ожидания для операций службы таблиц).)

```php
require_once 'vendor\autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Create table.
    $tableRestProxy->createTable("mytable");
}
catch(ServiceException $e){
    $code = $e->getCode();
    $error_message = $e->getMessage();
    // Handle exception based on error codes and messages.
    // Error codes and messages can be found here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
}
```

Дополнительные сведения об ограничениях имен таблиц см. в статье [Understanding the Table Service Data Model][table-data-model] (Общие сведения о модели данных службы таблиц).

## <a name="add-an-entity-to-a-table"></a>Добавление сущности в таблицу
Чтобы добавить сущность в таблицу, создайте новый объект **Entity** и передайте его в **TableRestProxy->insertEntity**. Обратите внимание, что при создании сущности необходимо задать свойства `PartitionKey` и `RowKey`. Это уникальные идентификаторы сущности и значения, которые можно запросить гораздо быстрее, чем другие свойства сущности. Система использует `PartitionKey`, чтобы автоматически распространять сущности таблицы на несколько узлов хранилища. Сущности с одинаковым значением `PartitionKey` хранятся на одном узле. (Операции с несколькими сущностями, хранящимися на одном узле, выполняются эффективнее, чем с сущностями с разных узлов). `RowKey` — это уникальный идентификатор сущности в разделе.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$entity = new Entity();
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");
$entity->addProperty("Description", null, "Take out the trash.");
$entity->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity->addProperty("Location", EdmType::STRING, "Home");

try{
    $tableRestProxy->insertEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
}
```

Дополнительные сведения о типах и свойствах таблиц см. в статье [Understanding the Table Service Data Model][table-data-model] (Общие сведения о модели данных службы таблиц).

Класс **TableRestProxy** предлагает два альтернативных способа вставки сущностей: **insertOrMergeEntity** и **insertOrReplaceEntity**. Чтобы использовать эти методы, создайте новый объект **Entity** и передайте его в качестве параметра в любой из этих методов. Каждый метод вставит эту сущность, если она не существует. Если сущность уже существует, **insertOrMergeEntity** обновляет значения свойств, если свойства уже существуют, и добавляет новые свойства, если они не существуют, в то время как **insertOrReplaceEntity** полностью заменяет существующую сущность. Следующий пример показывает, как использовать **insertOrMergeEntity**. Если сущность со значением `PartitionKey` "tasksSeattle" и значением `RowKey` "1" еще не существует, она будет вставлена. Но если она была вставлена ранее (как показано в приведенном выше примере), будет обновлено свойство `DueDate` и добавлено свойство `Status`. Свойства `Description` и `Location` также будут обновлены, однако до таких значений, которые фактически равны предыдущим. Если эти два последних свойства не были добавлены, как показано в примере, но существовали в целевой сущности, их текущие значения остаются без изменений.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

//Create new entity.
$entity = new Entity();

// PartitionKey and RowKey are required.
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");

// If entity exists, existing properties are updated with new values and
// new properties are added. Missing properties are unchanged.
$entity->addProperty("Description", null, "Take out the trash.");
$entity->addProperty("DueDate", EdmType::DATETIME, new DateTime()); // Modified the DueDate field.
$entity->addProperty("Location", EdmType::STRING, "Home");
$entity->addProperty("Status", EdmType::STRING, "Complete"); // Added Status field.

try    {
    // Calling insertOrReplaceEntity, instead of insertOrMergeEntity as shown,
    // would simply replace the entity with PartitionKey "tasksSeattle" and RowKey "1".
    $tableRestProxy->insertOrMergeEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="retrieve-a-single-entity"></a>Извлечение одной сущности
Метод **TableRestProxy->getEntity** позволяет получить одну сущность, запрашивая ее значения `PartitionKey` и `RowKey`. В приведенном ниже примере ключ раздела `tasksSeattle` и ключ строки `1` передаются в метод **getEntity**.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    $result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entity = $result->getEntity();

echo $entity->getPartitionKey().":".$entity->getRowKey();
```

## <a name="retrieve-all-entities-in-a-partition"></a>Получение всех сущностей в разделе
Запросы сущностей создаются с помощью фильтров (дополнительные сведения см. в статье [Querying Tables and Entities][filters] (Запросы таблиц и сущностей)). Для получения всех сущностей в разделе используйте фильтр "PartitionKey eq *имя_раздела*". В следующем примере показано, как получить все сущности в разделе `tasksSeattle`, передав фильтр в метод **queryEntities**.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "PartitionKey eq 'tasksSeattle'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a>Получение диапазона сущностей в разделе
Процедуру, аналогичную приведенной в предыдущем примере, можно использовать для получения любого подмножества сущностей в разделе. Получаемое подмножество сущностей определяется используемым фильтром (дополнительные сведения см. в статье [Querying Tables and Entities][filters] (Запросы таблиц и сущностей)). В следующем примере показано, как использовать фильтр для получения всех сущностей с определенным значением `Location` и значением `DueDate`, которое меньше указанной даты.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "Location eq 'Office' and DueDate lt '2012-11-5'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entity-properties"></a>Запрос подмножества свойств сущности
Запрос позволяет получить подмножество свойств сущности. Этот метод, который называется *проекцией*, снижает потребление полосы пропускания и может повысить производительность запросов, особенно для крупных сущностей. Чтобы задать свойство для извлечения, передайте имя этого свойства в метод **Query->addSelectField**. Этот метод можно вызывать несколько раз для добавления дополнительных свойств. После выполнения **TableRestProxy->queryEntities** возвращаемые сущности будут иметь только выбранные свойства. (Если вы хотите вернуть подмножество сущностей таблицы, используйте фильтр из приведенных выше запросов.)

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\QueryEntitiesOptions;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$options = new QueryEntitiesOptions();
$options->addSelectField("Description");

try    {
    $result = $tableRestProxy->queryEntities("mytable", $options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

// All entities in the table are returned, regardless of whether
// they have the Description field.
// To limit the results returned, use a filter.
$entities = $result->getEntities();

foreach($entities as $entity){
    $description = $entity->getProperty("Description")->getValue();
    echo $description."<br />";
}
```

## <a name="update-an-entity"></a>Обновление сущности
Существующие сущности можно обновить, воспользовавшись методами **Entity->setProperty** и **Entity->addProperty** для сущности, а затем вызвав **TableRestProxy->updateEntity**. Следующий пример извлекает сущность, изменяет одно свойство, удаляет другое свойство и добавляет новое свойство. Обратите внимание, что свойство можно удалить, установив для него значение **null**.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);

$entity = $result->getEntity();

$entity->setPropertyValue("DueDate", new DateTime()); //Modified DueDate.

$entity->setPropertyValue("Location", null); //Removed Location.

$entity->addProperty("Status", EdmType::STRING, "In progress"); //Added Status.

try    {
    $tableRestProxy->updateEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-an-entity"></a>Удаление сущности
Чтобы удалить сущность, передайте имя таблицы и значения `PartitionKey` и `RowKey` сущности в метод **TableRestProxy->deleteEntity**.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete entity.
    $tableRestProxy->deleteEntity("mytable", "tasksSeattle", "2");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

Обратите внимание, что для проверки на наличие конфликтов можно задать Etag для удаляемой сущности, воспользовавшись методом **DeleteEntityOptions->setEtag** и передав объект **DeleteEntityOptions** в **deleteEntity** в качестве четвертого параметра.

## <a name="batch-table-operations"></a>Пакетные операции с таблицами
Метод **TableRestProxy->batch** позволяет выполнять несколько операций в одном запросе. Здесь шаблон включает в себя добавление операций в объект **BatchRequest** и последующую передачу объекта **BatchRequest** в метод **TableRestProxy->batch**. Чтобы добавить операцию в объект **BatchRequest** , можно вызвать любой из следующих методов несколько раз:

* **addInsertEntity** (добавляет операцию insertEntity)
* **addUpdateEntity** (добавляет операцию updateEntity)
* **addMergeEntity** (добавляет операцию mergeEntity)
* **addInsertOrReplaceEntity** (добавляет операцию insertOrReplaceEntity)
* **addInsertOrMergeEntity** (добавляет операцию insertOrMergeEntity)
* **addDeleteEntity** (добавляет операцию deleteEntity)

Следующий пример показывает, как выполнить операции **insertEntity** и **deleteEntity** в одном запросе:

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;
use MicrosoftAzure\Storage\Table\Models\BatchOperations;

    // Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

// Create list of batch operation.
$operations = new BatchOperations();

$entity1 = new Entity();
$entity1->setPartitionKey("tasksSeattle");
$entity1->setRowKey("2");
$entity1->addProperty("Description", null, "Clean roof gutters.");
$entity1->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity1->addProperty("Location", EdmType::STRING, "Home");

// Add operation to list of batch operations.
$operations->addInsertEntity("mytable", $entity1);

// Add operation to list of batch operations.
$operations->addDeleteEntity("mytable", "tasksSeattle", "1");

try    {
    $tableRestProxy->batch($operations);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

Дополнительные сведения о пакетной обработке операций с таблицами см. в статье [Performing Entity Group Transactions][entity-group-transactions] (Выполнение групповых транзакций для сущности).

## <a name="delete-a-table"></a>Удаление таблицы
Наконец, чтобы удалить таблицу, следует передать имя таблицы в метод **TableRestProxy->deleteTable**.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete table.
    $tableRestProxy->deleteTable("mytable");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a>Дальнейшие действия
Вы изучили основные сведения о службе таблиц Azure. Дополнительные сведения о более сложных задачах хранилища можно найти по приведенным ниже ссылкам.

* [Обозреватель хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) — это бесплатное автономное приложение от корпорации Майкрософт, позволяющее визуализировать данные из службы хранилища Azure на платформе Windows, macOS и Linux.

* [Центр разработчиков PHP](/develop/php/)

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
