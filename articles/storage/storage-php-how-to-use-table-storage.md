---
title: "Как использовать хранилище таблиц из PHP | Документация Майкрософт"
description: "Вы узнаете, как использовать службу таблиц в PHP для создания и удаления таблиц, вставки, удаления строк и создания запросов для таблиц."
services: storage
documentationcenter: php
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 1e57f371-6208-4753-b2a0-05db4aede8e3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 15d3216ef5bb1d7ff312bd886837a3a7b0335afd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-table-storage-from-php"></a><span data-ttu-id="ab49d-103">Использование табличного хранилища из PHP</span><span class="sxs-lookup"><span data-stu-id="ab49d-103">How to use table storage from PHP</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="ab49d-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="ab49d-104">Overview</span></span>
<span data-ttu-id="ab49d-105">В этом руководстве показано, как реализовать типичные сценарии с использованием службы таблиц Azure.</span><span class="sxs-lookup"><span data-stu-id="ab49d-105">This guide shows you how to perform common scenarios using the Azure Table service.</span></span> <span data-ttu-id="ab49d-106">Примеры написаны на PHP и используют [пакет SDK Azure для PHP][download].</span><span class="sxs-lookup"><span data-stu-id="ab49d-106">The samples are written in PHP and use the [Azure SDK for PHP][download].</span></span> <span data-ttu-id="ab49d-107">Здесь описаны такие сценарии, как **создание и удаление таблицы, а также вставка, удаление и запрос сущностей в таблице**.</span><span class="sxs-lookup"><span data-stu-id="ab49d-107">The scenarios covered include **creating and deleting a table, and inserting, deleting, and querying entities in a table**.</span></span> <span data-ttu-id="ab49d-108">Дополнительные сведения о службе таблиц Azure см. в разделе [Дальнейшие действия](#next-steps).</span><span class="sxs-lookup"><span data-stu-id="ab49d-108">For more information on the Azure Table service, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="ab49d-109">Создание приложения PHP</span><span class="sxs-lookup"><span data-stu-id="ab49d-109">Create a PHP application</span></span>
<span data-ttu-id="ab49d-110">Единственным требованием для создания приложения PHP, которое получает доступ к службе таблиц Azure, является ссылка на классы в пакете Azure SDK для PHP непосредственно из кода.</span><span class="sxs-lookup"><span data-stu-id="ab49d-110">The only requirement for creating a PHP application that accesses the Azure Table service is the referencing of classes in the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="ab49d-111">Можно использовать любые средства разработки для создания приложения, включая программу "Блокнот".</span><span class="sxs-lookup"><span data-stu-id="ab49d-111">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="ab49d-112">В этом руководстве используются компоненты службы таблиц, которые могут вызываться локально из приложения PHP или в коде, работающем в веб-роли, рабочей роли или на веб-сайте Azure.</span><span class="sxs-lookup"><span data-stu-id="ab49d-112">In this guide, you use Table service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="ab49d-113">Получение клиентских библиотек Azure</span><span class="sxs-lookup"><span data-stu-id="ab49d-113">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-the-table-service"></a><span data-ttu-id="ab49d-114">Настройка приложения для доступа к службе таблиц</span><span class="sxs-lookup"><span data-stu-id="ab49d-114">Configure your application to access the Table service</span></span>
<span data-ttu-id="ab49d-115">Чтобы использовать интерфейсы API службы таблиц Azure, необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="ab49d-115">To use the Azure Table service APIs, you need to:</span></span>

1. <span data-ttu-id="ab49d-116">Ссылка на файл автозагрузчика с использованием оператора [require_once][require_once].</span><span class="sxs-lookup"><span data-stu-id="ab49d-116">Reference the autoloader file using the [require_once][require_once] statement, and</span></span>
2. <span data-ttu-id="ab49d-117">Ссылка на любые классы, которые могут использоваться.</span><span class="sxs-lookup"><span data-stu-id="ab49d-117">Reference any classes you might use.</span></span>

<span data-ttu-id="ab49d-118">В следующем примере показано, как включить файл автозагрузчика и сослаться на класс **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="ab49d-118">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="ab49d-119">В примере этой статьи предполагается, что установлены клиентские библиотеки PHP для Azure с помощью Composer.</span><span class="sxs-lookup"><span data-stu-id="ab49d-119">The examples in this article assume you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="ab49d-120">Если вы установили эти библиотеки вручную, то необходимо добавить ссылку на файл автозагрузчика <code>WindowsAzure.php</code> .</span><span class="sxs-lookup"><span data-stu-id="ab49d-120">If you installed the libraries manually, you need to reference the <code>WindowsAzure.php</code> autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="ab49d-121">В приведенных ниже примерах всегда отображается оператор `require_once` , однако ссылки приводятся только на классы, которые необходимы для выполнения этого примера.</span><span class="sxs-lookup"><span data-stu-id="ab49d-121">In the examples below, the `require_once` statement is always shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="ab49d-122">Настройка подключения к службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="ab49d-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="ab49d-123">Для создания клиента службы таблиц Azure необходимо сначала сформировать правильную строку подключения.</span><span class="sxs-lookup"><span data-stu-id="ab49d-123">To instantiate an Azure Table service client, you must first have a valid connection string.</span></span> <span data-ttu-id="ab49d-124">Формат строки подключения к службе таблиц:</span><span class="sxs-lookup"><span data-stu-id="ab49d-124">The format for the Table service connection string is:</span></span>

<span data-ttu-id="ab49d-125">Для доступа к службе в режиме реального времени:</span><span class="sxs-lookup"><span data-stu-id="ab49d-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="ab49d-126">Для доступа к хранилищу эмулятора:</span><span class="sxs-lookup"><span data-stu-id="ab49d-126">For accessing the emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="ab49d-127">Чтобы создать клиент любой службы Azure, необходимо использовать класс **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="ab49d-127">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="ab49d-128">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="ab49d-128">You can:</span></span>

* <span data-ttu-id="ab49d-129">передать строку подключения напрямую или</span><span class="sxs-lookup"><span data-stu-id="ab49d-129">pass the connection string directly to it or</span></span>
* <span data-ttu-id="ab49d-130">использовать **CloudConfigurationManager (CCM)** для проверки нескольких внешних источников на наличие строки подключения:</span><span class="sxs-lookup"><span data-stu-id="ab49d-130">use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="ab49d-131">по умолчанию предоставляется поддержка одного внешнего источника — переменных среды.</span><span class="sxs-lookup"><span data-stu-id="ab49d-131">by default, it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="ab49d-132">можно добавить новые источники, расширив класс **ConnectionStringSource**</span><span class="sxs-lookup"><span data-stu-id="ab49d-132">you can add new sources by extending the **ConnectionStringSource** class</span></span>

<span data-ttu-id="ab49d-133">В приведенных здесь примерах строка подключения передается напрямую.</span><span class="sxs-lookup"><span data-stu-id="ab49d-133">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a><span data-ttu-id="ab49d-134">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="ab49d-134">Create a table</span></span>
<span data-ttu-id="ab49d-135">Объект **TableRestProxy** позволяет создать таблицу с помощью метода **createTable**.</span><span class="sxs-lookup"><span data-stu-id="ab49d-135">A **TableRestProxy** object lets you create a table with the **createTable** method.</span></span> <span data-ttu-id="ab49d-136">При создании таблицы можно задать время ожидания службы таблиц.</span><span class="sxs-lookup"><span data-stu-id="ab49d-136">When creating a table, you can set the Table service timeout.</span></span> <span data-ttu-id="ab49d-137">(Дополнительные сведения о времени ожидания службы таблиц см. в статье [Setting Timeouts for Table Service Operations][table-service-timeouts] (Настройка времени ожидания для операций службы таблиц).)</span><span class="sxs-lookup"><span data-stu-id="ab49d-137">(For more information about the Table service timeout, see [Setting Timeouts for Table Service Operations][table-service-timeouts].)</span></span>

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

<span data-ttu-id="ab49d-138">Дополнительные сведения об ограничениях имен таблиц см. в статье [Understanding the Table Service Data Model][table-data-model] (Общие сведения о модели данных службы таблиц).</span><span class="sxs-lookup"><span data-stu-id="ab49d-138">For information about restrictions on table names, see [Understanding the Table Service Data Model][table-data-model].</span></span>

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="ab49d-139">Добавление сущности в таблицу</span><span class="sxs-lookup"><span data-stu-id="ab49d-139">Add an entity to a table</span></span>
<span data-ttu-id="ab49d-140">Чтобы добавить сущность в таблицу, создайте новый объект **Entity** и передайте его в **TableRestProxy->insertEntity**.</span><span class="sxs-lookup"><span data-stu-id="ab49d-140">To add an entity to a table, create a new **Entity** object and pass it to **TableRestProxy->insertEntity**.</span></span> <span data-ttu-id="ab49d-141">Обратите внимание, что при создании сущности необходимо задать свойства `PartitionKey` и `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="ab49d-141">Note that when you create an entity, you must specify a `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="ab49d-142">Это уникальные идентификаторы сущности и значения, которые можно запросить гораздо быстрее, чем другие свойства сущности.</span><span class="sxs-lookup"><span data-stu-id="ab49d-142">These are the unique identifiers for an entity and are values that can be queried much faster than other entity properties.</span></span> <span data-ttu-id="ab49d-143">Система использует `PartitionKey`, чтобы автоматически распространять сущности таблицы на несколько узлов хранилища.</span><span class="sxs-lookup"><span data-stu-id="ab49d-143">The system uses `PartitionKey` to automatically distribute the table's entities over many storage nodes.</span></span> <span data-ttu-id="ab49d-144">Сущности с одинаковым значением `PartitionKey` хранятся на одном узле.</span><span class="sxs-lookup"><span data-stu-id="ab49d-144">Entities with the same `PartitionKey` are stored on the same node.</span></span> <span data-ttu-id="ab49d-145">(Операции с несколькими сущностями, хранящимися на одном узле, выполняются эффективнее, чем с сущностями с разных узлов). `RowKey` — это уникальный идентификатор сущности в разделе.</span><span class="sxs-lookup"><span data-stu-id="ab49d-145">(Operations on multiple entities stored on the same node perform better than on entities stored across different nodes.) The `RowKey` is the unique ID of an entity within a partition.</span></span>

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

<span data-ttu-id="ab49d-146">Дополнительные сведения о типах и свойствах таблиц см. в статье [Understanding the Table Service Data Model][table-data-model] (Общие сведения о модели данных службы таблиц).</span><span class="sxs-lookup"><span data-stu-id="ab49d-146">For information about Table properties and types, see [Understanding the Table Service Data Model][table-data-model].</span></span>

<span data-ttu-id="ab49d-147">Класс **TableRestProxy** предлагает два альтернативных способа вставки сущностей: **insertOrMergeEntity** и **insertOrReplaceEntity**.</span><span class="sxs-lookup"><span data-stu-id="ab49d-147">The **TableRestProxy** class offers two alternative methods for inserting entities: **insertOrMergeEntity** and **insertOrReplaceEntity**.</span></span> <span data-ttu-id="ab49d-148">Чтобы использовать эти методы, создайте новый объект **Entity** и передайте его в качестве параметра в любой из этих методов.</span><span class="sxs-lookup"><span data-stu-id="ab49d-148">To use these methods, create a new **Entity** and pass it as a parameter to either method.</span></span> <span data-ttu-id="ab49d-149">Каждый метод вставит эту сущность, если она не существует.</span><span class="sxs-lookup"><span data-stu-id="ab49d-149">Each method will insert the entity if it does not exist.</span></span> <span data-ttu-id="ab49d-150">Если сущность уже существует, **insertOrMergeEntity** обновляет значения свойств, если свойства уже существуют, и добавляет новые свойства, если они не существуют, в то время как **insertOrReplaceEntity** полностью заменяет существующую сущность.</span><span class="sxs-lookup"><span data-stu-id="ab49d-150">If the entity already exists, **insertOrMergeEntity** updates property values if the properties already exist and adds new properties if they do not exist, while **insertOrReplaceEntity** completely replaces an existing entity.</span></span> <span data-ttu-id="ab49d-151">Следующий пример показывает, как использовать **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="ab49d-151">The following example shows how to use **insertOrMergeEntity**.</span></span> <span data-ttu-id="ab49d-152">Если сущность со значением `PartitionKey` "tasksSeattle" и значением `RowKey` "1" еще не существует, она будет вставлена.</span><span class="sxs-lookup"><span data-stu-id="ab49d-152">If the entity with `PartitionKey` "tasksSeattle" and `RowKey` "1" does not already exist, it will be inserted.</span></span> <span data-ttu-id="ab49d-153">Но если она была вставлена ранее (как показано в приведенном выше примере), будет обновлено свойство `DueDate` и добавлено свойство `Status`.</span><span class="sxs-lookup"><span data-stu-id="ab49d-153">However, if it has previously been inserted (as shown in the example above), the `DueDate` property will be updated, and the `Status` property will be added.</span></span> <span data-ttu-id="ab49d-154">Свойства `Description` и `Location` также будут обновлены, однако до таких значений, которые фактически равны предыдущим.</span><span class="sxs-lookup"><span data-stu-id="ab49d-154">The `Description` and `Location` properties are also updated, but with values that effectively leave them unchanged.</span></span> <span data-ttu-id="ab49d-155">Если эти два последних свойства не были добавлены, как показано в примере, но существовали в целевой сущности, их текущие значения остаются без изменений.</span><span class="sxs-lookup"><span data-stu-id="ab49d-155">If these latter two properties were not added as shown in the example, but existed on the target entity, their existing values would remain unchanged.</span></span>

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

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="ab49d-156">Извлечение одной сущности</span><span class="sxs-lookup"><span data-stu-id="ab49d-156">Retrieve a single entity</span></span>
<span data-ttu-id="ab49d-157">Метод **TableRestProxy->getEntity** позволяет получить одну сущность, запрашивая ее значения `PartitionKey` и `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="ab49d-157">The **TableRestProxy->getEntity** method allows you to retrieve a single entity by querying for its `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="ab49d-158">В приведенном ниже примере ключ раздела `tasksSeattle` и ключ строки `1` передаются в метод **getEntity**.</span><span class="sxs-lookup"><span data-stu-id="ab49d-158">In the example below, the partition key `tasksSeattle` and row key `1` are passed to the **getEntity** method.</span></span>

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

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="ab49d-159">Получение всех сущностей в разделе</span><span class="sxs-lookup"><span data-stu-id="ab49d-159">Retrieve all entities in a partition</span></span>
<span data-ttu-id="ab49d-160">Запросы сущностей создаются с помощью фильтров (дополнительные сведения см. в статье [Querying Tables and Entities][filters] (Запросы таблиц и сущностей)).</span><span class="sxs-lookup"><span data-stu-id="ab49d-160">Entity queries are constructed using filters (for more information, see [Querying Tables and Entities][filters]).</span></span> <span data-ttu-id="ab49d-161">Для получения всех сущностей в разделе используйте фильтр "PartitionKey eq *имя_раздела*".</span><span class="sxs-lookup"><span data-stu-id="ab49d-161">To retrieve all entities in partition, use the filter "PartitionKey eq *partition_name*".</span></span> <span data-ttu-id="ab49d-162">В следующем примере показано, как получить все сущности в разделе `tasksSeattle`, передав фильтр в метод **queryEntities**.</span><span class="sxs-lookup"><span data-stu-id="ab49d-162">The following example shows how to retrieve all entities in the `tasksSeattle` partition by passing a filter to the **queryEntities** method.</span></span>

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

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a><span data-ttu-id="ab49d-163">Получение диапазона сущностей в разделе</span><span class="sxs-lookup"><span data-stu-id="ab49d-163">Retrieve a subset of entities in a partition</span></span>
<span data-ttu-id="ab49d-164">Процедуру, аналогичную приведенной в предыдущем примере, можно использовать для получения любого подмножества сущностей в разделе.</span><span class="sxs-lookup"><span data-stu-id="ab49d-164">The same pattern used in the previous example can be used to retrieve any subset of entities in a partition.</span></span> <span data-ttu-id="ab49d-165">Получаемое подмножество сущностей определяется используемым фильтром (дополнительные сведения см. в статье [Querying Tables and Entities][filters] (Запросы таблиц и сущностей)). В следующем примере показано, как использовать фильтр для получения всех сущностей с определенным значением `Location` и значением `DueDate`, которое меньше указанной даты.</span><span class="sxs-lookup"><span data-stu-id="ab49d-165">The subset of entities you retrieve are determined by the filter you use (for more information, see [Querying Tables and Entities][filters]).The following example shows how to use a filter to retrieve all entities with a specific `Location` and a `DueDate` less than a specified date.</span></span>

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

## <a name="retrieve-a-subset-of-entity-properties"></a><span data-ttu-id="ab49d-166">Запрос подмножества свойств сущности</span><span class="sxs-lookup"><span data-stu-id="ab49d-166">Retrieve a subset of entity properties</span></span>
<span data-ttu-id="ab49d-167">Запрос позволяет получить подмножество свойств сущности.</span><span class="sxs-lookup"><span data-stu-id="ab49d-167">A query can retrieve a subset of entity properties.</span></span> <span data-ttu-id="ab49d-168">Этот метод, который называется *проекцией*, снижает потребление полосы пропускания и может повысить производительность запросов, особенно для крупных сущностей.</span><span class="sxs-lookup"><span data-stu-id="ab49d-168">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="ab49d-169">Чтобы задать свойство для извлечения, передайте имя этого свойства в метод **Query->addSelectField**.</span><span class="sxs-lookup"><span data-stu-id="ab49d-169">To specify a property to be retrieved, pass the name of the property to the **Query->addSelectField** method.</span></span> <span data-ttu-id="ab49d-170">Этот метод можно вызывать несколько раз для добавления дополнительных свойств.</span><span class="sxs-lookup"><span data-stu-id="ab49d-170">You can call this method multiple times to add more properties.</span></span> <span data-ttu-id="ab49d-171">После выполнения **TableRestProxy->queryEntities** возвращаемые сущности будут иметь только выбранные свойства.</span><span class="sxs-lookup"><span data-stu-id="ab49d-171">After executing **TableRestProxy->queryEntities**, the returned entities will only have the selected properties.</span></span> <span data-ttu-id="ab49d-172">(Если вы хотите вернуть подмножество сущностей таблицы, используйте фильтр из приведенных выше запросов.)</span><span class="sxs-lookup"><span data-stu-id="ab49d-172">(If you want to return a subset of Table entities, use a filter as shown in the queries above.)</span></span>

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

## <a name="update-an-entity"></a><span data-ttu-id="ab49d-173">Обновление сущности</span><span class="sxs-lookup"><span data-stu-id="ab49d-173">Update an entity</span></span>
<span data-ttu-id="ab49d-174">Существующие сущности можно обновить, воспользовавшись методами **Entity->setProperty** и **Entity->addProperty** для сущности, а затем вызвав **TableRestProxy->updateEntity**.</span><span class="sxs-lookup"><span data-stu-id="ab49d-174">An existing entity can be updated by using the **Entity->setProperty** and **Entity->addProperty** methods on the entity, and then calling **TableRestProxy->updateEntity**.</span></span> <span data-ttu-id="ab49d-175">Следующий пример извлекает сущность, изменяет одно свойство, удаляет другое свойство и добавляет новое свойство.</span><span class="sxs-lookup"><span data-stu-id="ab49d-175">The following example retrieves an entity, modifies one property, removes another property, and adds a new property.</span></span> <span data-ttu-id="ab49d-176">Обратите внимание, что свойство можно удалить, установив для него значение **null**.</span><span class="sxs-lookup"><span data-stu-id="ab49d-176">Note that you can remove a property by setting its value to **null**.</span></span>

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

## <a name="delete-an-entity"></a><span data-ttu-id="ab49d-177">Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="ab49d-177">Delete an entity</span></span>
<span data-ttu-id="ab49d-178">Чтобы удалить сущность, передайте имя таблицы и значения `PartitionKey` и `RowKey` сущности в метод **TableRestProxy->deleteEntity**.</span><span class="sxs-lookup"><span data-stu-id="ab49d-178">To delete an entity, pass the table name, and the entity's `PartitionKey` and `RowKey` to the **TableRestProxy->deleteEntity** method.</span></span>

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

<span data-ttu-id="ab49d-179">Обратите внимание, что для проверки на наличие конфликтов можно задать Etag для удаляемой сущности, воспользовавшись методом **DeleteEntityOptions->setEtag** и передав объект **DeleteEntityOptions** в **deleteEntity** в качестве четвертого параметра.</span><span class="sxs-lookup"><span data-stu-id="ab49d-179">Note that for concurrency checks, you can set the Etag for an entity to be deleted by using the **DeleteEntityOptions->setEtag** method and passing the **DeleteEntityOptions** object to **deleteEntity** as a fourth parameter.</span></span>

## <a name="batch-table-operations"></a><span data-ttu-id="ab49d-180">Пакетные операции с таблицами</span><span class="sxs-lookup"><span data-stu-id="ab49d-180">Batch table operations</span></span>
<span data-ttu-id="ab49d-181">Метод **TableRestProxy->batch** позволяет выполнять несколько операций в одном запросе.</span><span class="sxs-lookup"><span data-stu-id="ab49d-181">The **TableRestProxy->batch** method allows you to execute multiple operations in a single request.</span></span> <span data-ttu-id="ab49d-182">Здесь шаблон включает в себя добавление операций в объект **BatchRequest** и последующую передачу объекта **BatchRequest** в метод **TableRestProxy->batch**.</span><span class="sxs-lookup"><span data-stu-id="ab49d-182">The pattern here involves adding operations to **BatchRequest** object and then passing the **BatchRequest** object to the **TableRestProxy->batch** method.</span></span> <span data-ttu-id="ab49d-183">Чтобы добавить операцию в объект **BatchRequest** , можно вызвать любой из следующих методов несколько раз:</span><span class="sxs-lookup"><span data-stu-id="ab49d-183">To add an operation to a **BatchRequest** object, you can call any of the following methods multiple times:</span></span>

* <span data-ttu-id="ab49d-184">**addInsertEntity** (добавляет операцию insertEntity)</span><span class="sxs-lookup"><span data-stu-id="ab49d-184">**addInsertEntity** (adds an insertEntity operation)</span></span>
* <span data-ttu-id="ab49d-185">**addUpdateEntity** (добавляет операцию updateEntity)</span><span class="sxs-lookup"><span data-stu-id="ab49d-185">**addUpdateEntity** (adds an updateEntity operation)</span></span>
* <span data-ttu-id="ab49d-186">**addMergeEntity** (добавляет операцию mergeEntity)</span><span class="sxs-lookup"><span data-stu-id="ab49d-186">**addMergeEntity** (adds a mergeEntity operation)</span></span>
* <span data-ttu-id="ab49d-187">**addInsertOrReplaceEntity** (добавляет операцию insertOrReplaceEntity)</span><span class="sxs-lookup"><span data-stu-id="ab49d-187">**addInsertOrReplaceEntity** (adds an insertOrReplaceEntity operation)</span></span>
* <span data-ttu-id="ab49d-188">**addInsertOrMergeEntity** (добавляет операцию insertOrMergeEntity)</span><span class="sxs-lookup"><span data-stu-id="ab49d-188">**addInsertOrMergeEntity** (adds an insertOrMergeEntity operation)</span></span>
* <span data-ttu-id="ab49d-189">**addDeleteEntity** (добавляет операцию deleteEntity)</span><span class="sxs-lookup"><span data-stu-id="ab49d-189">**addDeleteEntity** (adds a deleteEntity operation)</span></span>

<span data-ttu-id="ab49d-190">Следующий пример показывает, как выполнить операции **insertEntity** и **deleteEntity** в одном запросе:</span><span class="sxs-lookup"><span data-stu-id="ab49d-190">The following example shows how to execute **insertEntity** and **deleteEntity** operations in a single request:</span></span>

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

<span data-ttu-id="ab49d-191">Дополнительные сведения о пакетной обработке операций с таблицами см. в статье [Performing Entity Group Transactions][entity-group-transactions] (Выполнение групповых транзакций для сущности).</span><span class="sxs-lookup"><span data-stu-id="ab49d-191">For more information about batching Table operations, see [Performing Entity Group Transactions][entity-group-transactions].</span></span>

## <a name="delete-a-table"></a><span data-ttu-id="ab49d-192">Удаление таблицы</span><span class="sxs-lookup"><span data-stu-id="ab49d-192">Delete a table</span></span>
<span data-ttu-id="ab49d-193">Наконец, чтобы удалить таблицу, следует передать имя таблицы в метод **TableRestProxy->deleteTable**.</span><span class="sxs-lookup"><span data-stu-id="ab49d-193">Finally, to delete a table, pass the table name to the **TableRestProxy->deleteTable** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ab49d-194">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ab49d-194">Next steps</span></span>
<span data-ttu-id="ab49d-195">Вы изучили основные сведения о службе таблиц Azure. Дополнительные сведения о более сложных задачах хранилища можно найти по приведенным ниже ссылкам.</span><span class="sxs-lookup"><span data-stu-id="ab49d-195">Now that you've learned the basics of the Azure Table service, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="ab49d-196">[Обозреватель хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) — это бесплатное автономное приложение от корпорации Майкрософт, позволяющее визуализировать данные из службы хранилища Azure на платформе Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="ab49d-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

* <span data-ttu-id="ab49d-197">[Центр разработчиков PHP](/develop/php/)</span><span class="sxs-lookup"><span data-stu-id="ab49d-197">[PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
