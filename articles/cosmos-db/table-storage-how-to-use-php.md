---
title: "хранилище таблиц toouse aaaHow из PHP | Документы Microsoft"
description: "Узнайте, как toouse hello службы таблиц из PHP toocreate и удалить таблицу и insert, delete и таблица hello запроса."
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
ms.openlocfilehash: 5b7c92221069d1c2a6ca951c06ae8eea8bb8478c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-php"></a>Как toouse таблицу хранилища из PHP
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Обзор
В этом руководстве показано, как с помощью распространенных сценариев tooperform hello службы таблиц Azure. Hello примеры написаны на PHP и использовать hello [пакет Azure SDK для PHP][download]. Hello сценарии включают **Создание и удаление таблицы и вставка, удаление и выполнения запросов к сущностям в таблице**. Дополнительные сведения о hello службы таблиц Azure см. в разделе hello [дальнейшие действия](#next-steps) раздела.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Создание приложения PHP
Здравствуйте, используется только для создания приложения PHP, которое обращается к службе таблиц Azure hello hello ссылки на классы в hello Azure SDK для PHP из кода. Можно использовать любой toocreate средства разработки приложения, включая «Блокнот».

В этом руководстве используются компоненты службы таблиц, которые могут вызываться локально из приложения PHP или в коде, работающем в веб-роли, рабочей роли или на веб-сайте Azure.

## <a name="get-hello-azure-client-libraries"></a>Получить клиентские библиотеки Azure hello
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-table-service"></a>Для настройки приложения tooaccess hello таблицы
toouse hello Azure API службы таблиц, необходимо:

1. Файл автозагрузчика hello ссылка, с помощью hello [require_once] [ require_once] инструкции, и
2. Ссылка на любые классы, которые могут использоваться.

Hello следующем примере показано, как tooinclude hello автозагрузчика файла и ссылку hello **ServicesBuilder** класса.

> [!NOTE]
> Примеры Hello в этой статье предполагается, что вы установили hello клиентские библиотеки PHP для Azure через редактор. При установке библиотеки hello вручную необходимо tooreference hello <code>WindowsAzure.php</code> автозагрузчика файла.
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

В ниже примерах hello, hello `require_once` инструкции всегда отображаются, но указываются только классы hello, необходимые для tooexecute пример hello.

## <a name="set-up-an-azure-storage-connection"></a>Настройка подключения к службе хранилища Azure
tooinstantiate клиента службы таблиц Azure, сначала нужно допустимую строку соединения. Hello для hello строку подключения таблицы службы выглядит следующим образом:

Для доступа к службе в режиме реального времени:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Для доступа к хранилищу эмулятор hello:

```php
UseDevelopmentStorage=true
```

toocreate любого клиента службы Azure необходимо toouse hello **ServicesBuilder** класса. Вы можете:

* Передайте hello подключения напрямую строка tooit или
* использовать hello **CloudConfigurationManager (CCM)** toocheck нескольких внешних источников для hello строки подключения:
  * по умолчанию предоставляется поддержка одного внешнего источника — переменных среды.
  * можно добавлять новые источники, расширяя hello **ConnectionStringSource** класса

Приведенные ниже примеры hello hello строки подключения будут передаваться напрямую.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a>Создание таблицы
Объект **TableRestProxy** объектов позволяет создать таблицу с hello **createTable** метод. При создании таблицы, можно задать время ожидания службы таблицы hello. (Дополнительные сведения о времени ожидания службы таблицы hello см. в разделе [задание времени ожидания для операций службы таблиц][table-service-timeouts].)

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

Сведения об ограничениях на имена таблиц см. в разделе [hello основные сведения о модели данных службы таблиц][table-data-model].

## <a name="add-an-entity-tooa-table"></a>Добавьте таблицу tooa сущности
tooadd таблицу tooa сущности, создайте новый **сущности** и передать его слишком**TableRestProxy -> insertEntity**. Обратите внимание, что при создании сущности необходимо задать свойства `PartitionKey` и `RowKey`. Это hello уникальные идентификаторы для сущности, — это значения, которые могут запрашиваться гораздо быстрее, чем другие свойства сущности. Hello система использует `PartitionKey` tooautomatically распределения сущностей таблицы hello по многим узлам хранилища. Здравствуйте сущности с одинаковым `PartitionKey` хранятся на hello того же узла. (Операции на несколько сущностей, хранящихся на hello же выполнять лучше, чем на записи, которые хранятся на разных узлах.) Hello `RowKey` hello уникальным идентификатором сущности внутри секции.

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
$entity->addProperty("Description", null, "Take out hello trash.");
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

Сведения о таблице свойств и типов, см. в разделе [hello основные сведения о модели данных службы таблиц][table-data-model].

Hello **TableRestProxy** класс предлагает два альтернативных методов для вставки сущностей: **insertOrMergeEntity** и **insertOrReplaceEntity**. toouse эти методы, создайте новый **сущности** и передайте его в качестве параметра метода tooeither. Каждый метод будет вставлять hello сущности, если он не существует. Если сущность hello уже существует, **insertOrMergeEntity** обновляет значения свойств, если свойства hello уже существует и добавляет новые свойства, если они не существуют, а **insertOrReplaceEntity** полностью заменяет существующую сущность. Следующий пример показывает как Hello toouse **insertOrMergeEntity**. Если сущность с hello `PartitionKey` «tasksSeattle» и `RowKey` «1» еще не существует, он будет вставлен. Тем не менее, если он ранее был вставлен (как показано в приведенном выше примере hello), hello `DueDate` свойство будет обновляться и hello `Status` свойство будет добавлено. Hello `Description` и `Location` свойства также будут обновлены, но со значениями, эффективно оставить их без изменений. Если последний этих свойств не добавлено, как показано в примере hello, но существующие на целевую сущность hello, их существующие значения останется без изменений.

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
$entity->addProperty("Description", null, "Take out hello trash.");
$entity->addProperty("DueDate", EdmType::DATETIME, new DateTime()); // Modified hello DueDate field.
$entity->addProperty("Location", EdmType::STRING, "Home");
$entity->addProperty("Status", EdmType::STRING, "Complete"); // Added Status field.

try    {
    // Calling insertOrReplaceEntity, instead of insertOrMergeEntity as shown,
    // would simply replace hello entity with PartitionKey "tasksSeattle" and RowKey "1".
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
Hello **TableRestProxy -> getEntity** метод позволяет tooretrieve одной сущности, запрашивая его `PartitionKey` и `RowKey`. В следующем примере hello, hello ключ раздела `tasksSeattle` и ключом строки `1` передаются toohello **getEntity** метод.

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
Запросы сущностей создаются с помощью фильтров (дополнительные сведения см. в статье [Querying Tables and Entities][filters] (Запросы таблиц и сущностей)). tooretrieve все сущности в секции, используйте фильтр hello «PartitionKey eq *имя_раздела*». Следующий пример показывает как Hello tooretrieve все сущности в hello `tasksSeattle` секции, передав toohello фильтра **queryEntities** метод.

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
Здравствуйте, же шаблон, используемый в предыдущем примере hello может быть используется tooretrieve любого подмножества сущностей из секции. Hello подмножества сущностей можно получить, определяются hello фильтра используется (Дополнительные сведения см. в разделе [запрос таблицами и сущностями][filters]) .hello следующий пример показывает как toouse tooretrieve фильтра все сущности с определенным `Location` и `DueDate` меньше указанной даты.

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
Запрос позволяет получить подмножество свойств сущности. Этот метод, который называется *проекцией*, снижает потребление полосы пропускания и может повысить производительность запросов, особенно для крупных сущностей. получить toobe свойство toospecify, передать имя hello hello свойство toohello **запроса -> addSelectField** метод. Дополнительные свойства можно вызвать этот метод tooadd несколько раз. После выполнения **TableRestProxy -> queryEntities**, hello возвращаемых сущностей будет иметь только свойства выбранного hello. (Если требуется tooreturn подмножество сущностей таблицы, с помощью фильтра как показано в приведенном выше запросах hello.)

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

// All entities in hello table are returned, regardless of whether
// they have hello Description field.
// toolimit hello results returned, use a filter.
$entities = $result->getEntities();

foreach($entities as $entity){
    $description = $entity->getProperty("Description")->getValue();
    echo $description."<br />";
}
```

## <a name="update-an-entity"></a>Обновление сущности
Сущность можно обновлять с помощью hello **сущности -> setProperty** и **сущности -> addProperty** методы hello сущности, а затем вызов метода **TableRestProxy -> updateEntity** . Hello следующий пример извлекает сущность, изменяет одно свойство, удаляет другого свойства и добавляет новое свойство. Обратите внимание, что свойство можно удалить путем изменения его значения слишком**null**.

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
toodelete сущности, передайте имя таблицы hello и hello сущности `PartitionKey` и `RowKey` toohello **TableRestProxy -> deleteEntity** метод.

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

Обратите внимание, что для проверки параллелизма можно задать hello Etag для сущности toobe удалена с помощью hello **DeleteEntityOptions -> setEtag** метода и передача hello **DeleteEntityOptions** объекта слишком**deleteEntity** как четвертый параметр.

## <a name="batch-table-operations"></a>Пакетные операции с таблицами
Hello **TableRestProxy -> пакет** метод позволяет tooexecute несколько операций в одном запросе. Hello здесь шаблон включает в себя добавление операций слишком**BatchRequest** объекта и затем передачу hello **BatchRequest** объекта toohello **TableRestProxy -> пакет** метод. Операция tooa tooadd **BatchRequest** объекта можно вызывать любые hello следующие методы несколько раз:

* **addInsertEntity** (добавляет операцию insertEntity)
* **addUpdateEntity** (добавляет операцию updateEntity)
* **addMergeEntity** (добавляет операцию mergeEntity)
* **addInsertOrReplaceEntity** (добавляет операцию insertOrReplaceEntity)
* **addInsertOrMergeEntity** (добавляет операцию insertOrMergeEntity)
* **addDeleteEntity** (добавляет операцию deleteEntity)

Следующий пример показывает как Hello tooexecute **insertEntity** и **deleteEntity** операций в одном запросе:

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

// Add operation toolist of batch operations.
$operations->addInsertEntity("mytable", $entity1);

// Add operation toolist of batch operations.
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
Наконец, toodelete таблицы, передайте hello таблицы имя toohello **TableRestProxy -> deleteTable** метод.

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
Теперь, когда вы узнали основы hello hello службы таблиц Azure, выполните эти ссылки toolearn о более сложных задач хранилища.

* [Обозреватель хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) является бесплатной, отдельное приложение от Майкрософт, позволяющая toowork визуально с помощью данных из хранилища Azure в Windows, macOS и Linux.

* [Центр разработчиков PHP](/develop/php/)

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
