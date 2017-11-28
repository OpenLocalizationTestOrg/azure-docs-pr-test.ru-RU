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
# <a name="how-toouse-table-storage-from-php"></a><span data-ttu-id="83d22-103">Как toouse таблицу хранилища из PHP</span><span class="sxs-lookup"><span data-stu-id="83d22-103">How toouse table storage from PHP</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="83d22-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="83d22-104">Overview</span></span>
<span data-ttu-id="83d22-105">В этом руководстве показано, как с помощью распространенных сценариев tooperform hello службы таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="83d22-105">This guide shows you how tooperform common scenarios using hello Azure Table service.</span></span> <span data-ttu-id="83d22-106">Hello примеры написаны на PHP и использовать hello [пакет Azure SDK для PHP][download].</span><span class="sxs-lookup"><span data-stu-id="83d22-106">hello samples are written in PHP and use hello [Azure SDK for PHP][download].</span></span> <span data-ttu-id="83d22-107">Hello сценарии включают **Создание и удаление таблицы и вставка, удаление и выполнения запросов к сущностям в таблице**.</span><span class="sxs-lookup"><span data-stu-id="83d22-107">hello scenarios covered include **creating and deleting a table, and inserting, deleting, and querying entities in a table**.</span></span> <span data-ttu-id="83d22-108">Дополнительные сведения о hello службы таблиц Azure см. в разделе hello [дальнейшие действия](#next-steps) раздела.</span><span class="sxs-lookup"><span data-stu-id="83d22-108">For more information on hello Azure Table service, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="83d22-109">Создание приложения PHP</span><span class="sxs-lookup"><span data-stu-id="83d22-109">Create a PHP application</span></span>
<span data-ttu-id="83d22-110">Здравствуйте, используется только для создания приложения PHP, которое обращается к службе таблиц Azure hello hello ссылки на классы в hello Azure SDK для PHP из кода.</span><span class="sxs-lookup"><span data-stu-id="83d22-110">hello only requirement for creating a PHP application that accesses hello Azure Table service is hello referencing of classes in hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="83d22-111">Можно использовать любой toocreate средства разработки приложения, включая «Блокнот».</span><span class="sxs-lookup"><span data-stu-id="83d22-111">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="83d22-112">В этом руководстве используются компоненты службы таблиц, которые могут вызываться локально из приложения PHP или в коде, работающем в веб-роли, рабочей роли или на веб-сайте Azure.</span><span class="sxs-lookup"><span data-stu-id="83d22-112">In this guide, you use Table service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="83d22-113">Получить клиентские библиотеки Azure hello</span><span class="sxs-lookup"><span data-stu-id="83d22-113">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-table-service"></a><span data-ttu-id="83d22-114">Для настройки приложения tooaccess hello таблицы</span><span class="sxs-lookup"><span data-stu-id="83d22-114">Configure your application tooaccess hello Table service</span></span>
<span data-ttu-id="83d22-115">toouse hello Azure API службы таблиц, необходимо:</span><span class="sxs-lookup"><span data-stu-id="83d22-115">toouse hello Azure Table service APIs, you need to:</span></span>

1. <span data-ttu-id="83d22-116">Файл автозагрузчика hello ссылка, с помощью hello [require_once] [ require_once] инструкции, и</span><span class="sxs-lookup"><span data-stu-id="83d22-116">Reference hello autoloader file using hello [require_once][require_once] statement, and</span></span>
2. <span data-ttu-id="83d22-117">Ссылка на любые классы, которые могут использоваться.</span><span class="sxs-lookup"><span data-stu-id="83d22-117">Reference any classes you might use.</span></span>

<span data-ttu-id="83d22-118">Hello следующем примере показано, как tooinclude hello автозагрузчика файла и ссылку hello **ServicesBuilder** класса.</span><span class="sxs-lookup"><span data-stu-id="83d22-118">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="83d22-119">Примеры Hello в этой статье предполагается, что вы установили hello клиентские библиотеки PHP для Azure через редактор.</span><span class="sxs-lookup"><span data-stu-id="83d22-119">hello examples in this article assume you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="83d22-120">При установке библиотеки hello вручную необходимо tooreference hello <code>WindowsAzure.php</code> автозагрузчика файла.</span><span class="sxs-lookup"><span data-stu-id="83d22-120">If you installed hello libraries manually, you need tooreference hello <code>WindowsAzure.php</code> autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="83d22-121">В ниже примерах hello, hello `require_once` инструкции всегда отображаются, но указываются только классы hello, необходимые для tooexecute пример hello.</span><span class="sxs-lookup"><span data-stu-id="83d22-121">In hello examples below, hello `require_once` statement is always shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="83d22-122">Настройка подключения к службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="83d22-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="83d22-123">tooinstantiate клиента службы таблиц Azure, сначала нужно допустимую строку соединения.</span><span class="sxs-lookup"><span data-stu-id="83d22-123">tooinstantiate an Azure Table service client, you must first have a valid connection string.</span></span> <span data-ttu-id="83d22-124">Hello для hello строку подключения таблицы службы выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="83d22-124">hello format for hello Table service connection string is:</span></span>

<span data-ttu-id="83d22-125">Для доступа к службе в режиме реального времени:</span><span class="sxs-lookup"><span data-stu-id="83d22-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="83d22-126">Для доступа к хранилищу эмулятор hello:</span><span class="sxs-lookup"><span data-stu-id="83d22-126">For accessing hello emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="83d22-127">toocreate любого клиента службы Azure необходимо toouse hello **ServicesBuilder** класса.</span><span class="sxs-lookup"><span data-stu-id="83d22-127">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="83d22-128">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="83d22-128">You can:</span></span>

* <span data-ttu-id="83d22-129">Передайте hello подключения напрямую строка tooit или</span><span class="sxs-lookup"><span data-stu-id="83d22-129">pass hello connection string directly tooit or</span></span>
* <span data-ttu-id="83d22-130">использовать hello **CloudConfigurationManager (CCM)** toocheck нескольких внешних источников для hello строки подключения:</span><span class="sxs-lookup"><span data-stu-id="83d22-130">use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="83d22-131">по умолчанию предоставляется поддержка одного внешнего источника — переменных среды.</span><span class="sxs-lookup"><span data-stu-id="83d22-131">by default, it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="83d22-132">можно добавлять новые источники, расширяя hello **ConnectionStringSource** класса</span><span class="sxs-lookup"><span data-stu-id="83d22-132">you can add new sources by extending hello **ConnectionStringSource** class</span></span>

<span data-ttu-id="83d22-133">Приведенные ниже примеры hello hello строки подключения будут передаваться напрямую.</span><span class="sxs-lookup"><span data-stu-id="83d22-133">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a><span data-ttu-id="83d22-134">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="83d22-134">Create a table</span></span>
<span data-ttu-id="83d22-135">Объект **TableRestProxy** объектов позволяет создать таблицу с hello **createTable** метод.</span><span class="sxs-lookup"><span data-stu-id="83d22-135">A **TableRestProxy** object lets you create a table with hello **createTable** method.</span></span> <span data-ttu-id="83d22-136">При создании таблицы, можно задать время ожидания службы таблицы hello.</span><span class="sxs-lookup"><span data-stu-id="83d22-136">When creating a table, you can set hello Table service timeout.</span></span> <span data-ttu-id="83d22-137">(Дополнительные сведения о времени ожидания службы таблицы hello см. в разделе [задание времени ожидания для операций службы таблиц][table-service-timeouts].)</span><span class="sxs-lookup"><span data-stu-id="83d22-137">(For more information about hello Table service timeout, see [Setting Timeouts for Table Service Operations][table-service-timeouts].)</span></span>

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

<span data-ttu-id="83d22-138">Сведения об ограничениях на имена таблиц см. в разделе [hello основные сведения о модели данных службы таблиц][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="83d22-138">For information about restrictions on table names, see [Understanding hello Table Service Data Model][table-data-model].</span></span>

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="83d22-139">Добавьте таблицу tooa сущности</span><span class="sxs-lookup"><span data-stu-id="83d22-139">Add an entity tooa table</span></span>
<span data-ttu-id="83d22-140">tooadd таблицу tooa сущности, создайте новый **сущности** и передать его слишком**TableRestProxy -> insertEntity**.</span><span class="sxs-lookup"><span data-stu-id="83d22-140">tooadd an entity tooa table, create a new **Entity** object and pass it too**TableRestProxy->insertEntity**.</span></span> <span data-ttu-id="83d22-141">Обратите внимание, что при создании сущности необходимо задать свойства `PartitionKey` и `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="83d22-141">Note that when you create an entity, you must specify a `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="83d22-142">Это hello уникальные идентификаторы для сущности, — это значения, которые могут запрашиваться гораздо быстрее, чем другие свойства сущности.</span><span class="sxs-lookup"><span data-stu-id="83d22-142">These are hello unique identifiers for an entity and are values that can be queried much faster than other entity properties.</span></span> <span data-ttu-id="83d22-143">Hello система использует `PartitionKey` tooautomatically распределения сущностей таблицы hello по многим узлам хранилища.</span><span class="sxs-lookup"><span data-stu-id="83d22-143">hello system uses `PartitionKey` tooautomatically distribute hello table's entities over many storage nodes.</span></span> <span data-ttu-id="83d22-144">Здравствуйте сущности с одинаковым `PartitionKey` хранятся на hello того же узла.</span><span class="sxs-lookup"><span data-stu-id="83d22-144">Entities with hello same `PartitionKey` are stored on hello same node.</span></span> <span data-ttu-id="83d22-145">(Операции на несколько сущностей, хранящихся на hello же выполнять лучше, чем на записи, которые хранятся на разных узлах.) Hello `RowKey` hello уникальным идентификатором сущности внутри секции.</span><span class="sxs-lookup"><span data-stu-id="83d22-145">(Operations on multiple entities stored on hello same node perform better than on entities stored across different nodes.) hello `RowKey` is hello unique ID of an entity within a partition.</span></span>

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

<span data-ttu-id="83d22-146">Сведения о таблице свойств и типов, см. в разделе [hello основные сведения о модели данных службы таблиц][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="83d22-146">For information about Table properties and types, see [Understanding hello Table Service Data Model][table-data-model].</span></span>

<span data-ttu-id="83d22-147">Hello **TableRestProxy** класс предлагает два альтернативных методов для вставки сущностей: **insertOrMergeEntity** и **insertOrReplaceEntity**.</span><span class="sxs-lookup"><span data-stu-id="83d22-147">hello **TableRestProxy** class offers two alternative methods for inserting entities: **insertOrMergeEntity** and **insertOrReplaceEntity**.</span></span> <span data-ttu-id="83d22-148">toouse эти методы, создайте новый **сущности** и передайте его в качестве параметра метода tooeither.</span><span class="sxs-lookup"><span data-stu-id="83d22-148">toouse these methods, create a new **Entity** and pass it as a parameter tooeither method.</span></span> <span data-ttu-id="83d22-149">Каждый метод будет вставлять hello сущности, если он не существует.</span><span class="sxs-lookup"><span data-stu-id="83d22-149">Each method will insert hello entity if it does not exist.</span></span> <span data-ttu-id="83d22-150">Если сущность hello уже существует, **insertOrMergeEntity** обновляет значения свойств, если свойства hello уже существует и добавляет новые свойства, если они не существуют, а **insertOrReplaceEntity** полностью заменяет существующую сущность.</span><span class="sxs-lookup"><span data-stu-id="83d22-150">If hello entity already exists, **insertOrMergeEntity** updates property values if hello properties already exist and adds new properties if they do not exist, while **insertOrReplaceEntity** completely replaces an existing entity.</span></span> <span data-ttu-id="83d22-151">Следующий пример показывает как Hello toouse **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="83d22-151">hello following example shows how toouse **insertOrMergeEntity**.</span></span> <span data-ttu-id="83d22-152">Если сущность с hello `PartitionKey` «tasksSeattle» и `RowKey` «1» еще не существует, он будет вставлен.</span><span class="sxs-lookup"><span data-stu-id="83d22-152">If hello entity with `PartitionKey` "tasksSeattle" and `RowKey` "1" does not already exist, it will be inserted.</span></span> <span data-ttu-id="83d22-153">Тем не менее, если он ранее был вставлен (как показано в приведенном выше примере hello), hello `DueDate` свойство будет обновляться и hello `Status` свойство будет добавлено.</span><span class="sxs-lookup"><span data-stu-id="83d22-153">However, if it has previously been inserted (as shown in hello example above), hello `DueDate` property will be updated, and hello `Status` property will be added.</span></span> <span data-ttu-id="83d22-154">Hello `Description` и `Location` свойства также будут обновлены, но со значениями, эффективно оставить их без изменений.</span><span class="sxs-lookup"><span data-stu-id="83d22-154">hello `Description` and `Location` properties are also updated, but with values that effectively leave them unchanged.</span></span> <span data-ttu-id="83d22-155">Если последний этих свойств не добавлено, как показано в примере hello, но существующие на целевую сущность hello, их существующие значения останется без изменений.</span><span class="sxs-lookup"><span data-stu-id="83d22-155">If these latter two properties were not added as shown in hello example, but existed on hello target entity, their existing values would remain unchanged.</span></span>

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

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="83d22-156">Извлечение одной сущности</span><span class="sxs-lookup"><span data-stu-id="83d22-156">Retrieve a single entity</span></span>
<span data-ttu-id="83d22-157">Hello **TableRestProxy -> getEntity** метод позволяет tooretrieve одной сущности, запрашивая его `PartitionKey` и `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="83d22-157">hello **TableRestProxy->getEntity** method allows you tooretrieve a single entity by querying for its `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="83d22-158">В следующем примере hello, hello ключ раздела `tasksSeattle` и ключом строки `1` передаются toohello **getEntity** метод.</span><span class="sxs-lookup"><span data-stu-id="83d22-158">In hello example below, hello partition key `tasksSeattle` and row key `1` are passed toohello **getEntity** method.</span></span>

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

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="83d22-159">Получение всех сущностей в разделе</span><span class="sxs-lookup"><span data-stu-id="83d22-159">Retrieve all entities in a partition</span></span>
<span data-ttu-id="83d22-160">Запросы сущностей создаются с помощью фильтров (дополнительные сведения см. в статье [Querying Tables and Entities][filters] (Запросы таблиц и сущностей)).</span><span class="sxs-lookup"><span data-stu-id="83d22-160">Entity queries are constructed using filters (for more information, see [Querying Tables and Entities][filters]).</span></span> <span data-ttu-id="83d22-161">tooretrieve все сущности в секции, используйте фильтр hello «PartitionKey eq *имя_раздела*».</span><span class="sxs-lookup"><span data-stu-id="83d22-161">tooretrieve all entities in partition, use hello filter "PartitionKey eq *partition_name*".</span></span> <span data-ttu-id="83d22-162">Следующий пример показывает как Hello tooretrieve все сущности в hello `tasksSeattle` секции, передав toohello фильтра **queryEntities** метод.</span><span class="sxs-lookup"><span data-stu-id="83d22-162">hello following example shows how tooretrieve all entities in hello `tasksSeattle` partition by passing a filter toohello **queryEntities** method.</span></span>

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

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a><span data-ttu-id="83d22-163">Получение диапазона сущностей в разделе</span><span class="sxs-lookup"><span data-stu-id="83d22-163">Retrieve a subset of entities in a partition</span></span>
<span data-ttu-id="83d22-164">Здравствуйте, же шаблон, используемый в предыдущем примере hello может быть используется tooretrieve любого подмножества сущностей из секции.</span><span class="sxs-lookup"><span data-stu-id="83d22-164">hello same pattern used in hello previous example can be used tooretrieve any subset of entities in a partition.</span></span> <span data-ttu-id="83d22-165">Hello подмножества сущностей можно получить, определяются hello фильтра используется (Дополнительные сведения см. в разделе [запрос таблицами и сущностями][filters]) .hello следующий пример показывает как toouse tooretrieve фильтра все сущности с определенным `Location` и `DueDate` меньше указанной даты.</span><span class="sxs-lookup"><span data-stu-id="83d22-165">hello subset of entities you retrieve are determined by hello filter you use (for more information, see [Querying Tables and Entities][filters]).hello following example shows how toouse a filter tooretrieve all entities with a specific `Location` and a `DueDate` less than a specified date.</span></span>

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

## <a name="retrieve-a-subset-of-entity-properties"></a><span data-ttu-id="83d22-166">Запрос подмножества свойств сущности</span><span class="sxs-lookup"><span data-stu-id="83d22-166">Retrieve a subset of entity properties</span></span>
<span data-ttu-id="83d22-167">Запрос позволяет получить подмножество свойств сущности.</span><span class="sxs-lookup"><span data-stu-id="83d22-167">A query can retrieve a subset of entity properties.</span></span> <span data-ttu-id="83d22-168">Этот метод, который называется *проекцией*, снижает потребление полосы пропускания и может повысить производительность запросов, особенно для крупных сущностей.</span><span class="sxs-lookup"><span data-stu-id="83d22-168">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="83d22-169">получить toobe свойство toospecify, передать имя hello hello свойство toohello **запроса -> addSelectField** метод.</span><span class="sxs-lookup"><span data-stu-id="83d22-169">toospecify a property toobe retrieved, pass hello name of hello property toohello **Query->addSelectField** method.</span></span> <span data-ttu-id="83d22-170">Дополнительные свойства можно вызвать этот метод tooadd несколько раз.</span><span class="sxs-lookup"><span data-stu-id="83d22-170">You can call this method multiple times tooadd more properties.</span></span> <span data-ttu-id="83d22-171">После выполнения **TableRestProxy -> queryEntities**, hello возвращаемых сущностей будет иметь только свойства выбранного hello.</span><span class="sxs-lookup"><span data-stu-id="83d22-171">After executing **TableRestProxy->queryEntities**, hello returned entities will only have hello selected properties.</span></span> <span data-ttu-id="83d22-172">(Если требуется tooreturn подмножество сущностей таблицы, с помощью фильтра как показано в приведенном выше запросах hello.)</span><span class="sxs-lookup"><span data-stu-id="83d22-172">(If you want tooreturn a subset of Table entities, use a filter as shown in hello queries above.)</span></span>

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

## <a name="update-an-entity"></a><span data-ttu-id="83d22-173">Обновление сущности</span><span class="sxs-lookup"><span data-stu-id="83d22-173">Update an entity</span></span>
<span data-ttu-id="83d22-174">Сущность можно обновлять с помощью hello **сущности -> setProperty** и **сущности -> addProperty** методы hello сущности, а затем вызов метода **TableRestProxy -> updateEntity** .</span><span class="sxs-lookup"><span data-stu-id="83d22-174">An existing entity can be updated by using hello **Entity->setProperty** and **Entity->addProperty** methods on hello entity, and then calling **TableRestProxy->updateEntity**.</span></span> <span data-ttu-id="83d22-175">Hello следующий пример извлекает сущность, изменяет одно свойство, удаляет другого свойства и добавляет новое свойство.</span><span class="sxs-lookup"><span data-stu-id="83d22-175">hello following example retrieves an entity, modifies one property, removes another property, and adds a new property.</span></span> <span data-ttu-id="83d22-176">Обратите внимание, что свойство можно удалить путем изменения его значения слишком**null**.</span><span class="sxs-lookup"><span data-stu-id="83d22-176">Note that you can remove a property by setting its value too**null**.</span></span>

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

## <a name="delete-an-entity"></a><span data-ttu-id="83d22-177">Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="83d22-177">Delete an entity</span></span>
<span data-ttu-id="83d22-178">toodelete сущности, передайте имя таблицы hello и hello сущности `PartitionKey` и `RowKey` toohello **TableRestProxy -> deleteEntity** метод.</span><span class="sxs-lookup"><span data-stu-id="83d22-178">toodelete an entity, pass hello table name, and hello entity's `PartitionKey` and `RowKey` toohello **TableRestProxy->deleteEntity** method.</span></span>

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

<span data-ttu-id="83d22-179">Обратите внимание, что для проверки параллелизма можно задать hello Etag для сущности toobe удалена с помощью hello **DeleteEntityOptions -> setEtag** метода и передача hello **DeleteEntityOptions** объекта слишком**deleteEntity** как четвертый параметр.</span><span class="sxs-lookup"><span data-stu-id="83d22-179">Note that for concurrency checks, you can set hello Etag for an entity toobe deleted by using hello **DeleteEntityOptions->setEtag** method and passing hello **DeleteEntityOptions** object too**deleteEntity** as a fourth parameter.</span></span>

## <a name="batch-table-operations"></a><span data-ttu-id="83d22-180">Пакетные операции с таблицами</span><span class="sxs-lookup"><span data-stu-id="83d22-180">Batch table operations</span></span>
<span data-ttu-id="83d22-181">Hello **TableRestProxy -> пакет** метод позволяет tooexecute несколько операций в одном запросе.</span><span class="sxs-lookup"><span data-stu-id="83d22-181">hello **TableRestProxy->batch** method allows you tooexecute multiple operations in a single request.</span></span> <span data-ttu-id="83d22-182">Hello здесь шаблон включает в себя добавление операций слишком**BatchRequest** объекта и затем передачу hello **BatchRequest** объекта toohello **TableRestProxy -> пакет** метод.</span><span class="sxs-lookup"><span data-stu-id="83d22-182">hello pattern here involves adding operations too**BatchRequest** object and then passing hello **BatchRequest** object toohello **TableRestProxy->batch** method.</span></span> <span data-ttu-id="83d22-183">Операция tooa tooadd **BatchRequest** объекта можно вызывать любые hello следующие методы несколько раз:</span><span class="sxs-lookup"><span data-stu-id="83d22-183">tooadd an operation tooa **BatchRequest** object, you can call any of hello following methods multiple times:</span></span>

* <span data-ttu-id="83d22-184">**addInsertEntity** (добавляет операцию insertEntity)</span><span class="sxs-lookup"><span data-stu-id="83d22-184">**addInsertEntity** (adds an insertEntity operation)</span></span>
* <span data-ttu-id="83d22-185">**addUpdateEntity** (добавляет операцию updateEntity)</span><span class="sxs-lookup"><span data-stu-id="83d22-185">**addUpdateEntity** (adds an updateEntity operation)</span></span>
* <span data-ttu-id="83d22-186">**addMergeEntity** (добавляет операцию mergeEntity)</span><span class="sxs-lookup"><span data-stu-id="83d22-186">**addMergeEntity** (adds a mergeEntity operation)</span></span>
* <span data-ttu-id="83d22-187">**addInsertOrReplaceEntity** (добавляет операцию insertOrReplaceEntity)</span><span class="sxs-lookup"><span data-stu-id="83d22-187">**addInsertOrReplaceEntity** (adds an insertOrReplaceEntity operation)</span></span>
* <span data-ttu-id="83d22-188">**addInsertOrMergeEntity** (добавляет операцию insertOrMergeEntity)</span><span class="sxs-lookup"><span data-stu-id="83d22-188">**addInsertOrMergeEntity** (adds an insertOrMergeEntity operation)</span></span>
* <span data-ttu-id="83d22-189">**addDeleteEntity** (добавляет операцию deleteEntity)</span><span class="sxs-lookup"><span data-stu-id="83d22-189">**addDeleteEntity** (adds a deleteEntity operation)</span></span>

<span data-ttu-id="83d22-190">Следующий пример показывает как Hello tooexecute **insertEntity** и **deleteEntity** операций в одном запросе:</span><span class="sxs-lookup"><span data-stu-id="83d22-190">hello following example shows how tooexecute **insertEntity** and **deleteEntity** operations in a single request:</span></span>

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

<span data-ttu-id="83d22-191">Дополнительные сведения о пакетной обработке операций с таблицами см. в статье [Performing Entity Group Transactions][entity-group-transactions] (Выполнение групповых транзакций для сущности).</span><span class="sxs-lookup"><span data-stu-id="83d22-191">For more information about batching Table operations, see [Performing Entity Group Transactions][entity-group-transactions].</span></span>

## <a name="delete-a-table"></a><span data-ttu-id="83d22-192">Удаление таблицы</span><span class="sxs-lookup"><span data-stu-id="83d22-192">Delete a table</span></span>
<span data-ttu-id="83d22-193">Наконец, toodelete таблицы, передайте hello таблицы имя toohello **TableRestProxy -> deleteTable** метод.</span><span class="sxs-lookup"><span data-stu-id="83d22-193">Finally, toodelete a table, pass hello table name toohello **TableRestProxy->deleteTable** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="83d22-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="83d22-194">Next steps</span></span>
<span data-ttu-id="83d22-195">Теперь, когда вы узнали основы hello hello службы таблиц Azure, выполните эти ссылки toolearn о более сложных задач хранилища.</span><span class="sxs-lookup"><span data-stu-id="83d22-195">Now that you've learned hello basics of hello Azure Table service, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="83d22-196">[Обозреватель хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) является бесплатной, отдельное приложение от Майкрософт, позволяющая toowork визуально с помощью данных из хранилища Azure в Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="83d22-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

* <span data-ttu-id="83d22-197">[Центр разработчиков PHP](/develop/php/)</span><span class="sxs-lookup"><span data-stu-id="83d22-197">[PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
