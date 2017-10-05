---
title: "Как использовать хранилище таблиц Azure из Node.js | Документация Майкрософт"
description: "Хранение структурированных данных в облаке в хранилище таблиц Azure (хранилище данных NoSQL)."
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 539212c6abe7738c022d67245f8992516f0899ff
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-table-storage-from-nodejs"></a><span data-ttu-id="1d29c-103">Использование табличного хранилища Azure из Node.js</span><span class="sxs-lookup"><span data-stu-id="1d29c-103">How to use Azure Table storage from Node.js</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="1d29c-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="1d29c-104">Overview</span></span>
<span data-ttu-id="1d29c-105">В этом разделе рассматривается реализация типичных сценариев с помощью службы таблиц Azure в приложении Node.js.</span><span class="sxs-lookup"><span data-stu-id="1d29c-105">This topic shows how to perform common scenarios using the Azure Table service in a Node.js application.</span></span>

<span data-ttu-id="1d29c-106">В примерах кода в этом разделе предполагается, что приложение Node.js уже создано.</span><span class="sxs-lookup"><span data-stu-id="1d29c-106">The code examples in this topic assume you already have a Node.js application.</span></span> <span data-ttu-id="1d29c-107">Инструкции по созданию приложения Node.js в Azure см. в любой из следующих статей:</span><span class="sxs-lookup"><span data-stu-id="1d29c-107">For information about how to create a Node.js application in Azure, see any of these topics:</span></span>

* [<span data-ttu-id="1d29c-108">Создание веб-приложения Node.js в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="1d29c-108">Create a Node.js web app in Azure App Service</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="1d29c-109">Создание и развертывание веб-приложения Node.js в Azure с использованием WebMatrix</span><span class="sxs-lookup"><span data-stu-id="1d29c-109">Build and deploy a Node.js web app to Azure using WebMatrix</span></span>](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* <span data-ttu-id="1d29c-110">[Создание и развертывание приложения Node.js в облачной службе Azure](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (с помощью Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="1d29c-110">[Build and deploy a Node.js application to an Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-to-access-azure-storage"></a><span data-ttu-id="1d29c-111">Настройка приложения для доступа к хранилищу Azure</span><span class="sxs-lookup"><span data-stu-id="1d29c-111">Configure your application to access Azure Storage</span></span>
<span data-ttu-id="1d29c-112">Чтобы использовать службу хранилища Azure, вам понадобится пакет SDK службы хранилища Azure для Node.js, который содержит набор полезных библиотек, взаимодействующих со службами REST хранилища.</span><span class="sxs-lookup"><span data-stu-id="1d29c-112">To use Azure Storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-install-the-package"></a><span data-ttu-id="1d29c-113">Использование диспетчера пакета Node (NPM) для установки пакета</span><span class="sxs-lookup"><span data-stu-id="1d29c-113">Use Node Package Manager (NPM) to install the package</span></span>
1. <span data-ttu-id="1d29c-114">Используя интерфейс командной строки, например **PowerShell** (Windows), **Terminal** (Mac) или **Bash** (Unix), перейдите в папку, в которой вы создали приложение.</span><span class="sxs-lookup"><span data-stu-id="1d29c-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate to the folder where you created your application.</span></span>
2. <span data-ttu-id="1d29c-115">Введите в командной строке **npm install azure-storage** .</span><span class="sxs-lookup"><span data-stu-id="1d29c-115">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="1d29c-116">Результат выполнения этой команды будет аналогичен следующему примеру:</span><span class="sxs-lookup"><span data-stu-id="1d29c-116">Output from the command is similar to the following example.</span></span>

       azure-storage@0.5.0 node_modules\azure-storage
       +-- extend@1.2.1
       +-- xmlbuilder@0.4.3
       +-- mime@1.2.11
       +-- node-uuid@1.4.3
       +-- validator@3.22.2
       +-- underscore@1.4.4
       +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
       +-- xml2js@0.2.7 (sax@0.5.2)
       +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. <span data-ttu-id="1d29c-117">Выполнив команду **ls** вручную, можно убедиться, что папка **node\_modules** создана.</span><span class="sxs-lookup"><span data-stu-id="1d29c-117">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="1d29c-118">В этой папке находится пакет **azure-storage** , содержащий библиотеки, необходимые для доступа к хранилищу.</span><span class="sxs-lookup"><span data-stu-id="1d29c-118">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="1d29c-119">Импорт пакета</span><span class="sxs-lookup"><span data-stu-id="1d29c-119">Import the package</span></span>
<span data-ttu-id="1d29c-120">Добавьте следующий код в начало файла **server.js** в приложении:</span><span class="sxs-lookup"><span data-stu-id="1d29c-120">Add the following code to the top of the **server.js** file in your application:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="1d29c-121">Настройка подключения к службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="1d29c-121">Set up an Azure Storage connection</span></span>
<span data-ttu-id="1d29c-122">Модуль Azure считывает переменные среды AZURE\_STORAGE\_ACCOUNT и AZURE\_STORAGE\_ACCESS\_KEY или AZURE\_STORAGE\_CONNECTION\_STRING, чтобы получить информацию, необходимую для подключения к учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="1d29c-122">The azure module will read the environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="1d29c-123">Если эти переменные среды не заданы, при вызове **TableService**необходимо указать сведения об учетной записи.</span><span class="sxs-lookup"><span data-stu-id="1d29c-123">If these environment variables are not set, you must specify the account information when calling **TableService**.</span></span>

<span data-ttu-id="1d29c-124">Пример настройки переменных среды для веб-сайта Azure на [портале Azure](https://portal.azure.com) см. в статье [Веб-приложение Node.js, использующее службу таблиц Azure](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="1d29c-124">For an example of setting the environment variables in the [Azure portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using the Azure Table Service](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-table"></a><span data-ttu-id="1d29c-125">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="1d29c-125">Create a table</span></span>
<span data-ttu-id="1d29c-126">Следующий код создает объект **TableService** и использует его для создания новой таблицы.</span><span class="sxs-lookup"><span data-stu-id="1d29c-126">The following code creates a **TableService** object and uses it to create a new table.</span></span> <span data-ttu-id="1d29c-127">Добавьте в начало **server.js**следующий код.</span><span class="sxs-lookup"><span data-stu-id="1d29c-127">Add the following near the top of **server.js**.</span></span>

```nodejs
var tableSvc = azure.createTableService();
```

<span data-ttu-id="1d29c-128">Вызов **createTableIfNotExists** создает новую таблицу с определенным именем, если она уже не существует.</span><span class="sxs-lookup"><span data-stu-id="1d29c-128">The call to **createTableIfNotExists** will create a new table with the specified name if it does not already exist.</span></span> <span data-ttu-id="1d29c-129">В следующем примере создается новая таблица с именем "mytable", если она еще не создана:</span><span class="sxs-lookup"><span data-stu-id="1d29c-129">The following example creates a new table named 'mytable' if it does not already exist:</span></span>

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

<span data-ttu-id="1d29c-130">`result.created` будет иметь значение `true`, если была создана новая таблица, и `false`, если таблица уже существует.</span><span class="sxs-lookup"><span data-stu-id="1d29c-130">The `result.created` will be `true` if a new table is created, and `false` if the table already exists.</span></span> <span data-ttu-id="1d29c-131">`response` будет содержать информацию о запросе.</span><span class="sxs-lookup"><span data-stu-id="1d29c-131">The `response` will contain information about the request.</span></span>

### <a name="filters"></a><span data-ttu-id="1d29c-132">Фильтры</span><span class="sxs-lookup"><span data-stu-id="1d29c-132">Filters</span></span>
<span data-ttu-id="1d29c-133">Дополнительные операции фильтрации можно применить к выполняемым операциям, используя **TableService**.</span><span class="sxs-lookup"><span data-stu-id="1d29c-133">Optional filtering operations can be applied to operations performed using **TableService**.</span></span> <span data-ttu-id="1d29c-134">К операциям фильтрации могут относиться ведение журнала, автоматический повтор и т. д. Фильтры являются объектами, реализующими метод со следующей сигнатурой:</span><span class="sxs-lookup"><span data-stu-id="1d29c-134">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="1d29c-135">Выполнив предварительную обработку параметров запроса, метод должен вызвать next, передавая функцию обратного вызова со следующей сигнатурой:</span><span class="sxs-lookup"><span data-stu-id="1d29c-135">After doing its preprocessing on the request options, the method needs to call "next", passing a callback with the following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="1d29c-136">В этом примере, а также после обработки returnObject (ответа на запрос к серверу) функция обратного вызова должна вызвать функцию next (если она существует), чтобы продолжить обработку других фильтров. В противном случае она просто вызывает finalCallback, чтобы завершить вызов службы.</span><span class="sxs-lookup"><span data-stu-id="1d29c-136">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback otherwise to end the service invocation.</span></span>

<span data-ttu-id="1d29c-137">В пакет SDK Azure для Node.js включены два фильтра, реализующие логику повторных попыток: **ExponentialRetryPolicyFilter** и **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="1d29c-137">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="1d29c-138">Следующий код создает объект **TableService**, использующий фильтр **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="1d29c-138">The following creates a **TableService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="1d29c-139">Добавление сущности в таблицу</span><span class="sxs-lookup"><span data-stu-id="1d29c-139">Add an entity to a table</span></span>
<span data-ttu-id="1d29c-140">Чтобы добавить сущность, сначала создайте объект, который определяет свойства сущности.</span><span class="sxs-lookup"><span data-stu-id="1d29c-140">To add an entity, first create an object that defines your entity properties.</span></span> <span data-ttu-id="1d29c-141">Все сущности должны содержать ключи **PartitionKey** и **RowKey**, которые выступают ее уникальными идентификаторами.</span><span class="sxs-lookup"><span data-stu-id="1d29c-141">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for the entity.</span></span>

* <span data-ttu-id="1d29c-142">**PartitionKey** — определяет раздел, в котором хранится сущность.</span><span class="sxs-lookup"><span data-stu-id="1d29c-142">**PartitionKey** - determines the partition that the entity is stored in</span></span>
* <span data-ttu-id="1d29c-143">**RowKey** — уникально определяет сущность в разделе.</span><span class="sxs-lookup"><span data-stu-id="1d29c-143">**RowKey** - uniquely identifies the entity within the partition</span></span>

<span data-ttu-id="1d29c-144">**PartitionKey** и **RowKey** должны быть строковыми значениями.</span><span class="sxs-lookup"><span data-stu-id="1d29c-144">Both **PartitionKey** and **RowKey** must be string values.</span></span> <span data-ttu-id="1d29c-145">Дополнительные сведения см. в статье [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) (Общие сведения о модели данных службы таблиц).</span><span class="sxs-lookup"><span data-stu-id="1d29c-145">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="1d29c-146">Ниже приводится пример задания сущности.</span><span class="sxs-lookup"><span data-stu-id="1d29c-146">The following is an example of defining an entity.</span></span> <span data-ttu-id="1d29c-147">Обратите внимание, что **dueDate** определяется как тип **Edm.DateTime**.</span><span class="sxs-lookup"><span data-stu-id="1d29c-147">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span></span> <span data-ttu-id="1d29c-148">Задание типа необязательно, типы будут определяться, если они не заданы.</span><span class="sxs-lookup"><span data-stu-id="1d29c-148">Specifying the type is optional, and types will be inferred if not specified.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> <span data-ttu-id="1d29c-149">Для каждой записи есть поле **Timestamp** , значение которого задается Azure при вставке или обновлении сущности.</span><span class="sxs-lookup"><span data-stu-id="1d29c-149">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span></span>
>
>

<span data-ttu-id="1d29c-150">Чтобы создать сущность, можно также использовать **entityGenerator** .</span><span class="sxs-lookup"><span data-stu-id="1d29c-150">You can also use the **entityGenerator** to create entities.</span></span> <span data-ttu-id="1d29c-151">В следующем примере код создает сущность для той же задачи с использованием **entityGenerator**.</span><span class="sxs-lookup"><span data-stu-id="1d29c-151">The following example creates the same task entity using the **entityGenerator**.</span></span>

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out the trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

<span data-ttu-id="1d29c-152">Чтобы добавить сущность в таблицу, передайте объект сущности в метод **insertEntity** .</span><span class="sxs-lookup"><span data-stu-id="1d29c-152">To add an entity to your table, pass the entity object to the **insertEntity** method.</span></span>

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

<span data-ttu-id="1d29c-153">Если операция успешна, `result` будет содержать [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) вставленной записи, а `response` — информацию об операции.</span><span class="sxs-lookup"><span data-stu-id="1d29c-153">If the operation is successful, `result` will contain the [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of the inserted record and `response` will contain information about the operation.</span></span>

<span data-ttu-id="1d29c-154">Пример ответа:</span><span class="sxs-lookup"><span data-stu-id="1d29c-154">Example response:</span></span>

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> <span data-ttu-id="1d29c-155">По умолчанию метод **insertEntity** не возвращает вставленную сущность как часть информации, содержащейся в `response`.</span><span class="sxs-lookup"><span data-stu-id="1d29c-155">By default, **insertEntity** does not return the inserted entity as part of the `response` information.</span></span> <span data-ttu-id="1d29c-156">Если вы хотите выполнить другие операции с этой сущностью или кэшировать информацию, необходимо, чтобы она была возвращена как часть `result`.</span><span class="sxs-lookup"><span data-stu-id="1d29c-156">If you plan on performing other operations on this entity, or wish to cache the information, it can be useful to have it returned as part of the `result`.</span></span> <span data-ttu-id="1d29c-157">Это можно сделать следующим образом, включив **echoContent** :</span><span class="sxs-lookup"><span data-stu-id="1d29c-157">You can do this by enabling **echoContent** as follows:</span></span>
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a><span data-ttu-id="1d29c-158">Обновление сущности</span><span class="sxs-lookup"><span data-stu-id="1d29c-158">Update an entity</span></span>
<span data-ttu-id="1d29c-159">Для обновления имеющейся сущности доступно несколько методов:</span><span class="sxs-lookup"><span data-stu-id="1d29c-159">There are multiple methods available to update an existing entity:</span></span>

* <span data-ttu-id="1d29c-160">**replaceEntity** — обновляет имеющуюся сущность с ее заменой.</span><span class="sxs-lookup"><span data-stu-id="1d29c-160">**replaceEntity** - updates an existing entity by replacing it</span></span>
* <span data-ttu-id="1d29c-161">**mergeEntity** — обновляет сущность посредством объединения новых значений свойств с имеющейся сущностью.</span><span class="sxs-lookup"><span data-stu-id="1d29c-161">**mergeEntity** - updates an existing entity by merging new property values into the existing entity</span></span>
* <span data-ttu-id="1d29c-162">**insertOrReplaceEntity** — обновляет имеющуюся сущность с ее заменой.</span><span class="sxs-lookup"><span data-stu-id="1d29c-162">**insertOrReplaceEntity** - updates an existing entity by replacing it.</span></span> <span data-ttu-id="1d29c-163">Если сущность не существует, будет вставлена новая сущность.</span><span class="sxs-lookup"><span data-stu-id="1d29c-163">If no entity exists, a new one will be inserted</span></span>
* <span data-ttu-id="1d29c-164">**insertOrMergeEntity** — обновляет сущность посредством объединения новых значений свойств с имеющейся сущностью.</span><span class="sxs-lookup"><span data-stu-id="1d29c-164">**insertOrMergeEntity** - updates an existing entity by merging new property values into the existing.</span></span> <span data-ttu-id="1d29c-165">Если сущность не существует, будет вставлена новая сущность.</span><span class="sxs-lookup"><span data-stu-id="1d29c-165">If no entity exists, a new one will be inserted</span></span>

<span data-ttu-id="1d29c-166">В следующем примере показано обновление сущности с помощью **replaceEntity**.</span><span class="sxs-lookup"><span data-stu-id="1d29c-166">The following example demonstrates updating an entity using **replaceEntity**:</span></span>

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> <span data-ttu-id="1d29c-167">По умолчанию обновление сущности не проверяет, были ли обновляемые данные ранее изменены другим процессом.</span><span class="sxs-lookup"><span data-stu-id="1d29c-167">By default, updating an entity does not check to see if the data being updated has previously been modified by another process.</span></span> <span data-ttu-id="1d29c-168">Поддержка одновременных обновлений:</span><span class="sxs-lookup"><span data-stu-id="1d29c-168">To support concurrent updates:</span></span>
>
> 1. <span data-ttu-id="1d29c-169">Получите ETag обновляемого объекта.</span><span class="sxs-lookup"><span data-stu-id="1d29c-169">Get the ETag of the object being updated.</span></span> <span data-ttu-id="1d29c-170">Он возвращается в составе `response` для всех операций с сущностями и может быть извлечен с помощью `response['.metadata'].etag`.</span><span class="sxs-lookup"><span data-stu-id="1d29c-170">This is returned as part of the `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span></span>
> 2. <span data-ttu-id="1d29c-171">При выполнении операции обновления с сущностью предварительно добавьте информацию ETag, извлеченную для новой сущности.</span><span class="sxs-lookup"><span data-stu-id="1d29c-171">When performing an update operation on an entity, add the ETag information previously retrieved to the new entity.</span></span> <span data-ttu-id="1d29c-172">Например:</span><span class="sxs-lookup"><span data-stu-id="1d29c-172">For example:</span></span>
>
>       <span data-ttu-id="1d29c-173">entity2['.metadata'].etag = currentEtag;</span><span class="sxs-lookup"><span data-stu-id="1d29c-173">entity2['.metadata'].etag = currentEtag;</span></span>
> 3. <span data-ttu-id="1d29c-174">Выполните операцию обновления.</span><span class="sxs-lookup"><span data-stu-id="1d29c-174">Perform the update operation.</span></span> <span data-ttu-id="1d29c-175">Если сущность была изменена с момента получения значения ETag, например, другим экземпляром вашего приложения, будет возвращена ошибка `error` , указывающая, что определенное в запросе условие обновления не выполнено.</span><span class="sxs-lookup"><span data-stu-id="1d29c-175">If the entity has been modified since you retrieved the ETag value, such as another instance of your application, an `error` will be returned stating that the update condition specified in the request was not satisfied.</span></span>
>
>

<span data-ttu-id="1d29c-176">Если при использовании **replaceEntity** и **mergeEntity** обновляемая сущность не существует, операция завершается ошибкой.</span><span class="sxs-lookup"><span data-stu-id="1d29c-176">With **replaceEntity** and **mergeEntity**, if the entity that is being updated doesn't exist, then the update operation will fail.</span></span> <span data-ttu-id="1d29c-177">Поэтому, если вы хотите сохранить сущность независимо от того, существует она или нет, используйте метод **insertOrReplaceEntity** или **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="1d29c-177">Therefore if you wish to store an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span></span>

<span data-ttu-id="1d29c-178">`result` должен содержать значение **Etag** обновленной сущности в случае успешного выполнения операций.</span><span class="sxs-lookup"><span data-stu-id="1d29c-178">The `result` for successful update operations will contain the **Etag** of the updated entity.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="1d29c-179">Работа с группами сущностей</span><span class="sxs-lookup"><span data-stu-id="1d29c-179">Work with groups of entities</span></span>
<span data-ttu-id="1d29c-180">Иногда имеет смысл отправлять совместно несколько операций в пакете для атомарной обработки сервером.</span><span class="sxs-lookup"><span data-stu-id="1d29c-180">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span></span> <span data-ttu-id="1d29c-181">Чтобы сделать это, используйте класс **TableBatch** для создания пакета, а затем метод **executeBatch** из **TableService** для выполнения пакетных операций.</span><span class="sxs-lookup"><span data-stu-id="1d29c-181">To accomplish that, use the **TableBatch** class to create a batch, and then use the **executeBatch** method of **TableService** to perform the batched operations.</span></span>

 <span data-ttu-id="1d29c-182">В следующем примере показана отправка двух сущностей в пакете:</span><span class="sxs-lookup"><span data-stu-id="1d29c-182">The following example demonstrates submitting two entities in a batch:</span></span>

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash the dishes'},
  dueDate: {'_':new Date(2015, 6, 20)}
};

var batch = new azure.TableBatch();

batch.insertEntity(task1, {echoContent: true});
batch.insertEntity(task2, {echoContent: true});

tableSvc.executeBatch('mytable', batch, function (error, result, response) {
  if(!error) {
    // Batch completed
  }
});
```

<span data-ttu-id="1d29c-183">В успешных пакетных операциях `result` содержит информацию обо всех операциях в пакете.</span><span class="sxs-lookup"><span data-stu-id="1d29c-183">For successful batch operations, `result` will contain information for each operation in the batch.</span></span>

### <a name="work-with-batched-operations"></a><span data-ttu-id="1d29c-184">Работа с пакетными операциями</span><span class="sxs-lookup"><span data-stu-id="1d29c-184">Work with batched operations</span></span>
<span data-ttu-id="1d29c-185">Операции, добавленные в пакет, можно проверить, просмотрев свойство `operations` .</span><span class="sxs-lookup"><span data-stu-id="1d29c-185">Operations added to a batch can be inspected by viewing the `operations` property.</span></span> <span data-ttu-id="1d29c-186">Для работы с операциями можно также использовать следующие методы:</span><span class="sxs-lookup"><span data-stu-id="1d29c-186">You can also use the following methods to work with operations:</span></span>

* <span data-ttu-id="1d29c-187">**clear** — удаляет все операции из пакета.</span><span class="sxs-lookup"><span data-stu-id="1d29c-187">**clear** - clears all operations from a batch</span></span>
* <span data-ttu-id="1d29c-188">**getOperations** — получает операцию из пакета.</span><span class="sxs-lookup"><span data-stu-id="1d29c-188">**getOperations** - gets an operation from the batch</span></span>
* <span data-ttu-id="1d29c-189">**hasOperations** — возвращает значение true, если пакет содержит операции.</span><span class="sxs-lookup"><span data-stu-id="1d29c-189">**hasOperations** - returns true if the batch contains operations</span></span>
* <span data-ttu-id="1d29c-190">**removeOperations** — удаляет операцию.</span><span class="sxs-lookup"><span data-stu-id="1d29c-190">**removeOperations** - removes an operation</span></span>
* <span data-ttu-id="1d29c-191">**size** — возвращает количество операций в пакете.</span><span class="sxs-lookup"><span data-stu-id="1d29c-191">**size** - returns the number of operations in the batch</span></span>

## <a name="retrieve-an-entity-by-key"></a><span data-ttu-id="1d29c-192">Получение сущности по ключу</span><span class="sxs-lookup"><span data-stu-id="1d29c-192">Retrieve an entity by key</span></span>
<span data-ttu-id="1d29c-193">Чтобы возвратить определенную сущность на основе значений ключей **PartitionKey** и **RowKey**, используйте метод **retrieveEntity**.</span><span class="sxs-lookup"><span data-stu-id="1d29c-193">To return a specific entity based on the **PartitionKey** and **RowKey**, use the **retrieveEntity** method.</span></span>

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains the entity
  }
});
```

<span data-ttu-id="1d29c-194">После завершения этой операции `result` будет содержать сущность.</span><span class="sxs-lookup"><span data-stu-id="1d29c-194">Once this operation is complete, `result` will contain the entity.</span></span>

## <a name="query-a-set-of-entities"></a><span data-ttu-id="1d29c-195">Запрос набора сущностей</span><span class="sxs-lookup"><span data-stu-id="1d29c-195">Query a set of entities</span></span>
<span data-ttu-id="1d29c-196">Чтобы запросить таблицу, используйте объект **TableQuery** для создания выражения запроса с помощью следующих предложений:</span><span class="sxs-lookup"><span data-stu-id="1d29c-196">To query a table, use the **TableQuery** object to build up a query expression using the following clauses:</span></span>

* <span data-ttu-id="1d29c-197">**select** — поля, возвращаемые из запроса.</span><span class="sxs-lookup"><span data-stu-id="1d29c-197">**select** - the fields to be returned from the query</span></span>
* <span data-ttu-id="1d29c-198">**where** — предложение where.</span><span class="sxs-lookup"><span data-stu-id="1d29c-198">**where** - the where clause</span></span>

  * <span data-ttu-id="1d29c-199">**and** — условие `and` в предложении where.</span><span class="sxs-lookup"><span data-stu-id="1d29c-199">**and** - an `and` where condition</span></span>
  * <span data-ttu-id="1d29c-200">**or** — условие `or` в предложении where.</span><span class="sxs-lookup"><span data-stu-id="1d29c-200">**or** - an `or` where condition</span></span>
* <span data-ttu-id="1d29c-201">**top** — количество извлекаемых элементов.</span><span class="sxs-lookup"><span data-stu-id="1d29c-201">**top** - the number of items to fetch</span></span>

<span data-ttu-id="1d29c-202">Следующий пример собирает запрос, который возвращает первые пять элементов с использованием ключа PartitionKey со значением hometasks.</span><span class="sxs-lookup"><span data-stu-id="1d29c-202">The following example builds a query that will return the top five items with a PartitionKey of 'hometasks'.</span></span>

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

<span data-ttu-id="1d29c-203">Так как параметр **select** не используется, возвращаются все поля.</span><span class="sxs-lookup"><span data-stu-id="1d29c-203">Since **select** is not used, all fields will be returned.</span></span> <span data-ttu-id="1d29c-204">Чтобы выполнить запрос сущности в таблице, используйте **queryEntities**.</span><span class="sxs-lookup"><span data-stu-id="1d29c-204">To perform the query against a table, use **queryEntities**.</span></span> <span data-ttu-id="1d29c-205">В следующем примере используется запрос для возврата сущностей из таблицы 'mytable'.</span><span class="sxs-lookup"><span data-stu-id="1d29c-205">The following example uses this query to return entities from 'mytable'.</span></span>

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

<span data-ttu-id="1d29c-206">В случае успешного выполнения `result.entries` будет содержать массив сущностей, соответствующих запросу.</span><span class="sxs-lookup"><span data-stu-id="1d29c-206">If successful, `result.entries` will contain an array of entities that match the query.</span></span> <span data-ttu-id="1d29c-207">Если запросу не удалось вернуть все сущности, `result.continuationToken` не будет иметь значение*null* и его можно будет использовать в качестве третьего параметра **queryEntities** для получения других результатов.</span><span class="sxs-lookup"><span data-stu-id="1d29c-207">If the query was unable to return all entities, `result.continuationToken` will be non-*null* and can be used as the third parameter of **queryEntities** to retrieve more results.</span></span> <span data-ttu-id="1d29c-208">В начальном запросе третий параметр должен иметь значение *null* .</span><span class="sxs-lookup"><span data-stu-id="1d29c-208">For the initial query, use *null* for the third parameter.</span></span>

### <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="1d29c-209">Запрос подмножества свойств сущности</span><span class="sxs-lookup"><span data-stu-id="1d29c-209">Query a subset of entity properties</span></span>
<span data-ttu-id="1d29c-210">Запрос к таблице может получить лишь несколько полей сущности.</span><span class="sxs-lookup"><span data-stu-id="1d29c-210">A query to a table can retrieve just a few fields from an entity.</span></span>
<span data-ttu-id="1d29c-211">Этот позволяет снизить потребление пропускной способности и может повысить производительность запросов, особенно для крупных сущностей.</span><span class="sxs-lookup"><span data-stu-id="1d29c-211">This reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="1d29c-212">С помощью предложения **select** передайте имена возвращаемых полей.</span><span class="sxs-lookup"><span data-stu-id="1d29c-212">Use the **select** clause and pass the names of the fields to be returned.</span></span> <span data-ttu-id="1d29c-213">Например, следующий запрос возвратит только поля **description** и **dueDate**.</span><span class="sxs-lookup"><span data-stu-id="1d29c-213">For example, the following query will return only the **description** and **dueDate** fields.</span></span>

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a><span data-ttu-id="1d29c-214">Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="1d29c-214">Delete an entity</span></span>
<span data-ttu-id="1d29c-215">Сущность можно удалить с помощью ее ключей раздела и строки.</span><span class="sxs-lookup"><span data-stu-id="1d29c-215">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="1d29c-216">В этом примере объект **task1** содержит значения ключей **RowKey** и **PartitionKey** удаляемой сущности.</span><span class="sxs-lookup"><span data-stu-id="1d29c-216">In this example, the **task1** object contains the **RowKey** and **PartitionKey** values of the entity to be deleted.</span></span> <span data-ttu-id="1d29c-217">Затем этот объект передается в метод **deleteEntity** .</span><span class="sxs-lookup"><span data-stu-id="1d29c-217">Then the object is passed to the **deleteEntity** method.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'}
};

tableSvc.deleteEntity('mytable', task, function(error, response){
  if(!error) {
    // Entity deleted
  }
});
```

> [!NOTE]
> <span data-ttu-id="1d29c-218">Следует рассмотреть использование тегов ETag при удалении элементов, чтобы гарантировать отсутствие в них изменений, внесенных другим процессом.</span><span class="sxs-lookup"><span data-stu-id="1d29c-218">Consider using ETags when deleting items, to ensure that the item hasn't been modified by another process.</span></span> <span data-ttu-id="1d29c-219">Сведения об использовании тегов ETag см. в разделе [Обновление сущности](#update-an-entity).</span><span class="sxs-lookup"><span data-stu-id="1d29c-219">See [Update an entity](#update-an-entity) for information on using ETags.</span></span>
>
>

## <a name="delete-a-table"></a><span data-ttu-id="1d29c-220">Удаление таблицы</span><span class="sxs-lookup"><span data-stu-id="1d29c-220">Delete a table</span></span>
<span data-ttu-id="1d29c-221">Следующий код удаляет таблицу из учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="1d29c-221">The following code deletes a table from a storage account.</span></span>

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

<span data-ttu-id="1d29c-222">Если неизвестно, существует ли таблица, используйте **deleteTableIfExists**.</span><span class="sxs-lookup"><span data-stu-id="1d29c-222">If you are uncertain whether the table exists, use **deleteTableIfExists**.</span></span>

## <a name="use-continuation-tokens"></a><span data-ttu-id="1d29c-223">Использование маркеров продолжения</span><span class="sxs-lookup"><span data-stu-id="1d29c-223">Use continuation tokens</span></span>
<span data-ttu-id="1d29c-224">При выполнении запросов к таблицам для получения больших объемов результатов следует искать маркеры продолжения.</span><span class="sxs-lookup"><span data-stu-id="1d29c-224">When you are querying tables for large amounts of results, look for continuation tokens.</span></span> <span data-ttu-id="1d29c-225">По вашему запросу может быть найден большой объем данных, который, возможно, не удастся реализовать, если не создать метод определения наличия маркера продолжения.</span><span class="sxs-lookup"><span data-stu-id="1d29c-225">There may be large amounts of data available for your query that you might not realize if you do not build to recognize when a continuation token is present.</span></span>

<span data-ttu-id="1d29c-226">При наличии такого маркера объект результатов, возвращаемый при запросе сущностей, задает свойство `continuationToken` .</span><span class="sxs-lookup"><span data-stu-id="1d29c-226">The results object returned during querying entities sets a `continuationToken` property when such a token is present.</span></span> <span data-ttu-id="1d29c-227">В последствии его можно использовать при выполнении запроса для продолжения и перемещения между разделами и сущностями таблицы.</span><span class="sxs-lookup"><span data-stu-id="1d29c-227">You can then use this when performing a query to continue to move across the partition and table entities.</span></span>

<span data-ttu-id="1d29c-228">При выполнении запросов для экземпляра объекта запроса и функции обратного вызова можно указать параметр continuationToken:</span><span class="sxs-lookup"><span data-stu-id="1d29c-228">When querying, a continuationToken parameter may be provided between the query object instance and the callback function:</span></span>

```nodejs
var nextContinuationToken = null;
dc.table.queryEntities(tableName,
    query,
    nextContinuationToken,
    function (error, results) {
        if (error) throw error;

        // iterate through results.entries with results

        if (results.continuationToken) {
            nextContinuationToken = results.continuationToken;
        }

    });
```

<span data-ttu-id="1d29c-229">Если обратиться к объекту `continuationToken`, то вы обнаружите, что он имеет такие свойства, как `nextPartitionKey`, `nextRowKey` и `targetLocation`, которые можно использовать для итерации по всем результатам.</span><span class="sxs-lookup"><span data-stu-id="1d29c-229">If you inspect the `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used to iterate through all the results.</span></span>

<span data-ttu-id="1d29c-230">Кроме того, на сайте GitHub в репозитории Node.js для службы хранилища Azure есть пример использования маркеров продолжения.</span><span class="sxs-lookup"><span data-stu-id="1d29c-230">There is also a continuation sample within the Azure Storage Node.js repo on GitHub.</span></span> <span data-ttu-id="1d29c-231">Поищите `examples/samples/continuationsample.js`.</span><span class="sxs-lookup"><span data-stu-id="1d29c-231">Look for `examples/samples/continuationsample.js`.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="1d29c-232">Работа с подписями общего доступа</span><span class="sxs-lookup"><span data-stu-id="1d29c-232">Work with shared access signatures</span></span>
<span data-ttu-id="1d29c-233">Подписанные URL-адреса (SAS) — безопасный способ предоставить детальный доступ к таблицам без указания имени или ключей своей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="1d29c-233">Shared access signatures (SAS) are a secure way to provide granular access to tables without providing your storage account name or keys.</span></span> <span data-ttu-id="1d29c-234">SAS часто используется для предоставления ограниченного доступа к данным, например, позволяет мобильному приложению запрашивать записи.</span><span class="sxs-lookup"><span data-stu-id="1d29c-234">SAS are often used to provide limited access to your data, such as allowing a mobile app to query records.</span></span>

<span data-ttu-id="1d29c-235">Надежное приложение, например облачная служба, создает подписанный URL-адрес с помощью метода **generateSharedAccessSignature** из **TableService** и передает этот адрес ненадежному или частично надежному приложению, например мобильному приложению.</span><span class="sxs-lookup"><span data-stu-id="1d29c-235">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **TableService**, and provides it to an untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="1d29c-236">Подпись SAS создается с использованием политики, которая описывает даты начала и окончания срока действия SAS, а также уровень доступа, который предоставляется держателю подписи SAS.</span><span class="sxs-lookup"><span data-stu-id="1d29c-236">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span></span>

<span data-ttu-id="1d29c-237">В следующем примере создается новая общая политика, которая позволяет держателю подписи SAS запрашивать ('r') в таблице в течение 100 минут с момента своего создания.</span><span class="sxs-lookup"><span data-stu-id="1d29c-237">The following example generates a new shared access policy that will allow the SAS holder to query ('r') the table, and expires 100 minutes after the time it is created.</span></span>

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
};

var tableSAS = tableSvc.generateSharedAccessSignature('mytable', sharedAccessPolicy);
var host = tableSvc.host;
```

<span data-ttu-id="1d29c-238">Обратите внимание, что также должна быть предоставлена информация узла, поскольку она требуется держателю SAS для совершения попыток доступа к таблице.</span><span class="sxs-lookup"><span data-stu-id="1d29c-238">Note that the host information must be provided also, as it is required when the SAS holder attempts to access the table.</span></span>

<span data-ttu-id="1d29c-239">Клиентское приложение далее использует подпись SAS с помощью **TableServiceWithSAS** для выполнения операций с таблицей.</span><span class="sxs-lookup"><span data-stu-id="1d29c-239">The client application then uses the SAS with **TableServiceWithSAS** to perform operations against the table.</span></span> <span data-ttu-id="1d29c-240">Следующий пример выполняет подключение к таблице и выполняет запрос.</span><span class="sxs-lookup"><span data-stu-id="1d29c-240">The following example connects to the table and performs a query.</span></span>

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains the entities
  }
});
```

<span data-ttu-id="1d29c-241">Поскольку подпись SAS была создана только для доступа с выполнение запроса, если выполняется попытка вставки, обновления или удаления сущностей, будет возвращена ошибка.</span><span class="sxs-lookup"><span data-stu-id="1d29c-241">Since the SAS was generated with only query access, if an attempt were made to insert, update, or delete entities, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="1d29c-242">Списки управления доступом</span><span class="sxs-lookup"><span data-stu-id="1d29c-242">Access Control Lists</span></span>
<span data-ttu-id="1d29c-243">Можно также использовать список управления доступом (ACL) для задания политики доступа подписи SAS.</span><span class="sxs-lookup"><span data-stu-id="1d29c-243">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span></span> <span data-ttu-id="1d29c-244">Это может оказаться полезным, когда необходимо предоставить доступ к таблице нескольким клиентам, но с различной политикой доступа для каждого из них.</span><span class="sxs-lookup"><span data-stu-id="1d29c-244">This is useful if you wish to allow multiple clients to access the table, but provide different access policies for each client.</span></span>

<span data-ttu-id="1d29c-245">ACL реализуется с помощью массива политик доступа, каждая из которых связана со своим идентификатором.</span><span class="sxs-lookup"><span data-stu-id="1d29c-245">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="1d29c-246">В следующем примере определяются две политики, по одной для пользователей user1 и user2:</span><span class="sxs-lookup"><span data-stu-id="1d29c-246">The following example defines two policies, one for 'user1' and one for 'user2':</span></span>

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="1d29c-247">В этом примере код получает текущий список ACL для таблицы **hometasks**, а затем добавляет новые политики с помощью **setTableAcl**.</span><span class="sxs-lookup"><span data-stu-id="1d29c-247">The following example gets the current ACL for the **hometasks** table, and then adds the new policies using **setTableAcl**.</span></span> <span data-ttu-id="1d29c-248">Такой подход допускает выполнение:</span><span class="sxs-lookup"><span data-stu-id="1d29c-248">This approach allows:</span></span>

```nodejs
var extend = require('extend');
tableSvc.getTableAcl('hometasks', function(error, result, response) {
if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    tableSvc.setTableAcl('hometasks', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="1d29c-249">После задания ACL можно создать подпись SAS на основе идентификатора политики.</span><span class="sxs-lookup"><span data-stu-id="1d29c-249">Once the ACL has been set, you can then create a SAS based on the ID for a policy.</span></span> <span data-ttu-id="1d29c-250">В следующем примере создается новая подпись SAS для пользователя 'user2':</span><span class="sxs-lookup"><span data-stu-id="1d29c-250">The following example creates a new SAS for 'user2':</span></span>

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="1d29c-251">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1d29c-251">Next steps</span></span>
<span data-ttu-id="1d29c-252">Для получения дополнительных сведений см. следующие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="1d29c-252">For more information, see the following resources.</span></span>

* <span data-ttu-id="1d29c-253">[Обозреватель хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) — это бесплатное автономное приложение от корпорации Майкрософт, позволяющее визуализировать данные из службы хранилища Azure на платформе Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="1d29c-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="1d29c-254">[Пакет SDK службы хранилища Azure для Node](https://github.com/Azure/azure-storage-node) на веб-сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="1d29c-254">[Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) repository on GitHub.</span></span>
* [<span data-ttu-id="1d29c-255">центре разработчиков Node.js</span><span class="sxs-lookup"><span data-stu-id="1d29c-255">Node.js Developer Center</span></span>](/develop/nodejs/)
* [<span data-ttu-id="1d29c-256">Создание приложения Node.js и его развертывание на веб-сайт Azure</span><span class="sxs-lookup"><span data-stu-id="1d29c-256">Create and deploy a Node.js application to an Azure website</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)