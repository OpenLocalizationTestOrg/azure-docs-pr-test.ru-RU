---
title: "aaaHow toouse хранилище таблиц Azure из Node.js | Документы Microsoft"
description: "Хранения структурированных данных в облаке hello, с помощью хранилища таблиц Azure, хранилище данных NoSQL."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 990a71337b806d759d0277a7691712346db7b355
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-nodejs"></a><span data-ttu-id="c9ad2-103">Как toouse хранилище таблиц Azure из Node.js</span><span class="sxs-lookup"><span data-stu-id="c9ad2-103">How toouse Azure Table storage from Node.js</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="c9ad2-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="c9ad2-104">Overview</span></span>
<span data-ttu-id="c9ad2-105">В этом разделе показано, как служба tooperform распространенные сценарии, с помощью hello таблиц Azure в приложение Node.js.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-105">This topic shows how tooperform common scenarios using hello Azure Table service in a Node.js application.</span></span>

<span data-ttu-id="c9ad2-106">Примеры кода Hello в этом разделе предполагается, что у вас уже есть приложение Node.js.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-106">hello code examples in this topic assume you already have a Node.js application.</span></span> <span data-ttu-id="c9ad2-107">Сведения о том, как toocreate приложения Node.js в Azure, смотрите в любом из следующих разделов:</span><span class="sxs-lookup"><span data-stu-id="c9ad2-107">For information about how toocreate a Node.js application in Azure, see any of these topics:</span></span>

* [<span data-ttu-id="c9ad2-108">Создание веб-приложения Node.js в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="c9ad2-108">Create a Node.js web app in Azure App Service</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="c9ad2-109">Построение и развертывание приложения tooAzure web Node.js, с помощью WebMatrix</span><span class="sxs-lookup"><span data-stu-id="c9ad2-109">Build and deploy a Node.js web app tooAzure using WebMatrix</span></span>](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* <span data-ttu-id="c9ad2-110">[Построение и развертывание tooan приложений Node.js облачной службы Azure](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (с помощью Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="c9ad2-110">[Build and deploy a Node.js application tooan Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-tooaccess-azure-storage"></a><span data-ttu-id="c9ad2-111">Настройка вашего приложения tooaccess хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="c9ad2-111">Configure your application tooaccess Azure Storage</span></span>
<span data-ttu-id="c9ad2-112">toouse хранилища Azure необходимо hello пакет SDK хранилища Azure для Node.js, включающий набор библиотек удобства, взаимодействующих со службами REST hello хранилища.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-112">toouse Azure Storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooinstall-hello-package"></a><span data-ttu-id="c9ad2-113">С помощью диспетчера пакетов узла (NPM) tooinstall hello пакета</span><span class="sxs-lookup"><span data-stu-id="c9ad2-113">Use Node Package Manager (NPM) tooinstall hello package</span></span>
1. <span data-ttu-id="c9ad2-114">Использовать интерфейс командной строки, такие как **PowerShell** (Windows), **терминалов** (Mac), или **Bash** (Unix) и перейдите в папку toohello, где вы создали приложение.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate toohello folder where you created your application.</span></span>
2. <span data-ttu-id="c9ad2-115">Тип **npm установить хранилища azure** в командном окне приветствия.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-115">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="c9ad2-116">Выходные данные команды hello — примерно toohello следующий пример.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-116">Output from hello command is similar toohello following example.</span></span>

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
3. <span data-ttu-id="c9ad2-117">Вы можете вручную запустить hello **ls** tooverify команды, **узел\_модули** папка была создана.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-117">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="c9ad2-118">В этой папке можно найти hello **хранилища azure** пакет, который содержит библиотеки hello потребуется tooaccess хранилище.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-118">Inside that folder you will find hello **azure-storage** package, which contains hello libraries you need tooaccess storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="c9ad2-119">Импорт пакета hello</span><span class="sxs-lookup"><span data-stu-id="c9ad2-119">Import hello package</span></span>
<span data-ttu-id="c9ad2-120">Добавьте следующий код toohello вверху hello hello **server.js** файл в приложении:</span><span class="sxs-lookup"><span data-stu-id="c9ad2-120">Add hello following code toohello top of hello **server.js** file in your application:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="c9ad2-121">Настройка подключения к службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="c9ad2-121">Set up an Azure Storage connection</span></span>
<span data-ttu-id="c9ad2-122">модуль Hello azure будет считывать hello переменных среды AZURE\_ХРАНИЛИЩА\_учетной записи и AZURE\_ХРАНЕНИЯ\_доступа\_ключа или AZURE\_ХРАНЕНИЯ\_подключения \_Строка для tooyour tooconnect сведения, необходимые учетной записи хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-122">hello azure module will read hello environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="c9ad2-123">Если эти переменные среды не установлены, необходимо указать сведения об учетной записи hello при вызове **TableService**.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-123">If these environment variables are not set, you must specify hello account information when calling **TableService**.</span></span>

<span data-ttu-id="c9ad2-124">Пример настройки переменных среды hello в hello [портал Azure](https://portal.azure.com) на веб-сайт Azure в разделе [Node.js веб-приложения с использованием hello службы таблиц Azure](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="c9ad2-124">For an example of setting hello environment variables in hello [Azure portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using hello Azure Table Service](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-table"></a><span data-ttu-id="c9ad2-125">Создание таблицы</span><span class="sxs-lookup"><span data-stu-id="c9ad2-125">Create a table</span></span>
<span data-ttu-id="c9ad2-126">Hello следующий код создает **TableService** объекта и использует его toocreate новую таблицу.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-126">hello following code creates a **TableService** object and uses it toocreate a new table.</span></span> <span data-ttu-id="c9ad2-127">Добавьте следующее hello вверху hello **server.js**.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-127">Add hello following near hello top of **server.js**.</span></span>

```nodejs
var tableSvc = azure.createTableService();
```

<span data-ttu-id="c9ad2-128">Здравствуйте вызов слишком**createTableIfNotExists** создаст новую таблицу с указанным именем hello, если он еще не существует.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-128">hello call too**createTableIfNotExists** will create a new table with hello specified name if it does not already exist.</span></span> <span data-ttu-id="c9ad2-129">Hello следующий пример создает новую таблицу с именем «mytable», если он еще не существует:</span><span class="sxs-lookup"><span data-stu-id="c9ad2-129">hello following example creates a new table named 'mytable' if it does not already exist:</span></span>

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

<span data-ttu-id="c9ad2-130">Hello `result.created` будет `true` Если создается новая таблица, и `false` Если hello таблица уже существует.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-130">hello `result.created` will be `true` if a new table is created, and `false` if hello table already exists.</span></span> <span data-ttu-id="c9ad2-131">Hello `response` будет содержать сведения о запросе hello.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-131">hello `response` will contain information about hello request.</span></span>

### <a name="filters"></a><span data-ttu-id="c9ad2-132">Фильтры</span><span class="sxs-lookup"><span data-stu-id="c9ad2-132">Filters</span></span>
<span data-ttu-id="c9ad2-133">Необязательный операции фильтрации может быть применен toooperations, выполняемые с помощью **TableService**.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-133">Optional filtering operations can be applied toooperations performed using **TableService**.</span></span> <span data-ttu-id="c9ad2-134">К операциям фильтрации могут относиться ведение журнала, автоматический повтор и т. д. Фильтры являются объектами, которые реализуют метод с сигнатурой hello:</span><span class="sxs-lookup"><span data-stu-id="c9ad2-134">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="c9ad2-135">После выполнения его предварительной обработки параметров запроса hello, метод hello должен toocall «Далее», передача обратный вызов с hello следующие подписи:</span><span class="sxs-lookup"><span data-stu-id="c9ad2-135">After doing its preprocessing on hello request options, hello method needs toocall "next", passing a callback with hello following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="c9ad2-136">В этот обратный вызов, а после обработки returnObject hello (hello ответ от сервера toohello hello запроса), обратного вызова hello необходимы tooeither рядом вызова, если он существует toocontinue обработки других фильтров, или просто вызвав finalCallback в противном случае tooend hello вызов службы.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-136">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback otherwise tooend hello service invocation.</span></span>

<span data-ttu-id="c9ad2-137">Два фильтра, которые реализовать логику повторных попыток входят в состав hello Azure SDK для Node.js **ExponentialRetryPolicyFilter** и **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-137">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="c9ad2-138">Hello следующий код создает **TableService** объект, который использует hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="c9ad2-138">hello following creates a **TableService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="c9ad2-139">Добавьте таблицу tooa сущности</span><span class="sxs-lookup"><span data-stu-id="c9ad2-139">Add an entity tooa table</span></span>
<span data-ttu-id="c9ad2-140">tooadd сущности, сначала создайте объект, который определяет свойства сущности.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-140">tooadd an entity, first create an object that defines your entity properties.</span></span> <span data-ttu-id="c9ad2-141">Все сущности должны содержать **PartitionKey** и **RowKey**, которые являются уникальные идентификаторы для сущности hello.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-141">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for hello entity.</span></span>

* <span data-ttu-id="c9ad2-142">**PartitionKey** -определяет hello секции, хранящиеся в сущности hello</span><span class="sxs-lookup"><span data-stu-id="c9ad2-142">**PartitionKey** - determines hello partition that hello entity is stored in</span></span>
* <span data-ttu-id="c9ad2-143">**RowKey** — уникальным образом идентифицирует сущность hello в секции hello</span><span class="sxs-lookup"><span data-stu-id="c9ad2-143">**RowKey** - uniquely identifies hello entity within hello partition</span></span>

<span data-ttu-id="c9ad2-144">**PartitionKey** и **RowKey** должны быть строковыми значениями.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-144">Both **PartitionKey** and **RowKey** must be string values.</span></span> <span data-ttu-id="c9ad2-145">Дополнительные сведения см. в разделе [hello основные сведения о модели данных службы таблиц](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="c9ad2-145">For more information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="c9ad2-146">Hello ниже приведен пример определения сущности.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-146">hello following is an example of defining an entity.</span></span> <span data-ttu-id="c9ad2-147">Обратите внимание, что **dueDate** определяется как тип **Edm.DateTime**.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-147">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span></span> <span data-ttu-id="c9ad2-148">Указание типа hello является необязательным, и типы будут будет выводиться, если не указана.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-148">Specifying hello type is optional, and types will be inferred if not specified.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> <span data-ttu-id="c9ad2-149">Для каждой записи есть поле **Timestamp** , значение которого задается Azure при вставке или обновлении сущности.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-149">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span></span>
>
>

<span data-ttu-id="c9ad2-150">Можно также использовать hello **entityGenerator** toocreate сущностей.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-150">You can also use hello **entityGenerator** toocreate entities.</span></span> <span data-ttu-id="c9ad2-151">Hello следующий пример создает hello одной сущности задачи с помощью hello **entityGenerator**.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-151">hello following example creates hello same task entity using hello **entityGenerator**.</span></span>

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out hello trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

<span data-ttu-id="c9ad2-152">tooadd таблицу tooyour сущности передать hello сущности объекта toohello **insertEntity** метод.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-152">tooadd an entity tooyour table, pass hello entity object toohello **insertEntity** method.</span></span>

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

<span data-ttu-id="c9ad2-153">Если выполнена операция hello, `result` будет содержать hello [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) из hello вставить запись и `response` будет содержать сведения об операции hello.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-153">If hello operation is successful, `result` will contain hello [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of hello inserted record and `response` will contain information about hello operation.</span></span>

<span data-ttu-id="c9ad2-154">Пример ответа:</span><span class="sxs-lookup"><span data-stu-id="c9ad2-154">Example response:</span></span>

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> <span data-ttu-id="c9ad2-155">По умолчанию **insertEntity** не возвращает сущности hello вставлены в рамках hello `response` сведения.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-155">By default, **insertEntity** does not return hello inserted entity as part of hello `response` information.</span></span> <span data-ttu-id="c9ad2-156">Если план для выполнения других операций в этой сущности, или если нужна toocache hello сведения, бывает полезно toohave, он возвращается как часть hello `result`.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-156">If you plan on performing other operations on this entity, or wish toocache hello information, it can be useful toohave it returned as part of hello `result`.</span></span> <span data-ttu-id="c9ad2-157">Это можно сделать следующим образом, включив **echoContent** :</span><span class="sxs-lookup"><span data-stu-id="c9ad2-157">You can do this by enabling **echoContent** as follows:</span></span>
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a><span data-ttu-id="c9ad2-158">Обновление сущности</span><span class="sxs-lookup"><span data-stu-id="c9ad2-158">Update an entity</span></span>
<span data-ttu-id="c9ad2-159">Существует несколько методов, доступных tooupdate существующей сущности.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-159">There are multiple methods available tooupdate an existing entity:</span></span>

* <span data-ttu-id="c9ad2-160">**replaceEntity** — обновляет имеющуюся сущность с ее заменой.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-160">**replaceEntity** - updates an existing entity by replacing it</span></span>
* <span data-ttu-id="c9ad2-161">**mergeEntity** -обновляет существующую сущность, объединив новых значений свойств в существующей сущности hello</span><span class="sxs-lookup"><span data-stu-id="c9ad2-161">**mergeEntity** - updates an existing entity by merging new property values into hello existing entity</span></span>
* <span data-ttu-id="c9ad2-162">**insertOrReplaceEntity** — обновляет имеющуюся сущность с ее заменой.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-162">**insertOrReplaceEntity** - updates an existing entity by replacing it.</span></span> <span data-ttu-id="c9ad2-163">Если сущность не существует, будет вставлена новая сущность.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-163">If no entity exists, a new one will be inserted</span></span>
* <span data-ttu-id="c9ad2-164">**insertOrMergeEntity** -обновляет существующую сущность, объединяя новые значения свойств в существующую hello.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-164">**insertOrMergeEntity** - updates an existing entity by merging new property values into hello existing.</span></span> <span data-ttu-id="c9ad2-165">Если сущность не существует, будет вставлена новая сущность.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-165">If no entity exists, a new one will be inserted</span></span>

<span data-ttu-id="c9ad2-166">Hello ниже приведен пример обновления сущности, используя **replaceEntity**:</span><span class="sxs-lookup"><span data-stu-id="c9ad2-166">hello following example demonstrates updating an entity using **replaceEntity**:</span></span>

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> <span data-ttu-id="c9ad2-167">По умолчанию обновление сущности не проверяет toosee если обновляемые данные hello ранее был изменен другим процессом.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-167">By default, updating an entity does not check toosee if hello data being updated has previously been modified by another process.</span></span> <span data-ttu-id="c9ad2-168">toosupport одновременных обновлений:</span><span class="sxs-lookup"><span data-stu-id="c9ad2-168">toosupport concurrent updates:</span></span>
>
> 1. <span data-ttu-id="c9ad2-169">Получение hello ETag обновляемый объект hello.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-169">Get hello ETag of hello object being updated.</span></span> <span data-ttu-id="c9ad2-170">Это значение возвращается как часть hello `response` для любой операции, связанные сущности и можно извлечь с помощью `response['.metadata'].etag`.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-170">This is returned as part of hello `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span></span>
> 2. <span data-ttu-id="c9ad2-171">При выполнении операции обновления на сущность, добавьте новую сущность toohello ранее получить сведения о hello ETag.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-171">When performing an update operation on an entity, add hello ETag information previously retrieved toohello new entity.</span></span> <span data-ttu-id="c9ad2-172">Например:</span><span class="sxs-lookup"><span data-stu-id="c9ad2-172">For example:</span></span>
>
>       <span data-ttu-id="c9ad2-173">entity2['.metadata'].etag = currentEtag;</span><span class="sxs-lookup"><span data-stu-id="c9ad2-173">entity2['.metadata'].etag = currentEtag;</span></span>
> 3. <span data-ttu-id="c9ad2-174">Выполните операцию обновления hello.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-174">Perform hello update operation.</span></span> <span data-ttu-id="c9ad2-175">Если сущность hello была изменена с момента получения hello значение ETag, такие как другой экземпляр приложения, `error` будет возвращаться о том, что не выполнено условие обновления hello, указанный в запросе hello.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-175">If hello entity has been modified since you retrieved hello ETag value, such as another instance of your application, an `error` will be returned stating that hello update condition specified in hello request was not satisfied.</span></span>
>
>

<span data-ttu-id="c9ad2-176">С **replaceEntity** и **mergeEntity**, если hello сущности, которая обновляется не существует, то произойдет сбой операции обновления hello.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-176">With **replaceEntity** and **mergeEntity**, if hello entity that is being updated doesn't exist, then hello update operation will fail.</span></span> <span data-ttu-id="c9ad2-177">Поэтому toostore сущности независимо от того, является ли он уже существует, используйте **insertOrReplaceEntity** или **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-177">Therefore if you wish toostore an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span></span>

<span data-ttu-id="c9ad2-178">Hello `result` для успешного обновления операции будет содержать hello **Etag** hello обновить сущности.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-178">hello `result` for successful update operations will contain hello **Etag** of hello updated entity.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="c9ad2-179">Работа с группами сущностей</span><span class="sxs-lookup"><span data-stu-id="c9ad2-179">Work with groups of entities</span></span>
<span data-ttu-id="c9ad2-180">Иногда он делает toosubmit смысле несколько операций друг с другом в tooensure пакета atomic обработки сервером hello.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-180">Sometimes it makes sense toosubmit multiple operations together in a batch tooensure atomic processing by hello server.</span></span> <span data-ttu-id="c9ad2-181">tooaccomplish, использовать hello **TableBatch** класса toocreate пакета, а затем использовать hello **executeBatch** метод **TableService** tooperform hello пакетные операции.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-181">tooaccomplish that, use hello **TableBatch** class toocreate a batch, and then use hello **executeBatch** method of **TableService** tooperform hello batched operations.</span></span>

 <span data-ttu-id="c9ad2-182">Следующий пример Hello демонстрируется отправка две сущности в пакете:</span><span class="sxs-lookup"><span data-stu-id="c9ad2-182">hello following example demonstrates submitting two entities in a batch:</span></span>

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash hello dishes'},
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

<span data-ttu-id="c9ad2-183">Для успешного пакетных операций `result` будет содержать сведения для каждой операции в пакете hello.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-183">For successful batch operations, `result` will contain information for each operation in hello batch.</span></span>

### <a name="work-with-batched-operations"></a><span data-ttu-id="c9ad2-184">Работа с пакетными операциями</span><span class="sxs-lookup"><span data-stu-id="c9ad2-184">Work with batched operations</span></span>
<span data-ttu-id="c9ad2-185">Операции добавлены tooa пакета можно проверить, просмотрев hello `operations` свойство.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-185">Operations added tooa batch can be inspected by viewing hello `operations` property.</span></span> <span data-ttu-id="c9ad2-186">Можно также использовать следующие методы toowork с операциями hello:</span><span class="sxs-lookup"><span data-stu-id="c9ad2-186">You can also use hello following methods toowork with operations:</span></span>

* <span data-ttu-id="c9ad2-187">**clear** — удаляет все операции из пакета.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-187">**clear** - clears all operations from a batch</span></span>
* <span data-ttu-id="c9ad2-188">**getOperations** -возвращает операции в пакете hello</span><span class="sxs-lookup"><span data-stu-id="c9ad2-188">**getOperations** - gets an operation from hello batch</span></span>
* <span data-ttu-id="c9ad2-189">**hasOperations** -возвращает значение true, если пакет hello содержит операции</span><span class="sxs-lookup"><span data-stu-id="c9ad2-189">**hasOperations** - returns true if hello batch contains operations</span></span>
* <span data-ttu-id="c9ad2-190">**removeOperations** — удаляет операцию.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-190">**removeOperations** - removes an operation</span></span>
* <span data-ttu-id="c9ad2-191">**размер** -возвращает hello количество операций в пакете hello</span><span class="sxs-lookup"><span data-stu-id="c9ad2-191">**size** - returns hello number of operations in hello batch</span></span>

## <a name="retrieve-an-entity-by-key"></a><span data-ttu-id="c9ad2-192">Получение сущности по ключу</span><span class="sxs-lookup"><span data-stu-id="c9ad2-192">Retrieve an entity by key</span></span>
<span data-ttu-id="c9ad2-193">определенной сущности на основании hello tooreturn **PartitionKey** и **RowKey**, использовать hello **retrieveEntity** метод.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-193">tooreturn a specific entity based on hello **PartitionKey** and **RowKey**, use hello **retrieveEntity** method.</span></span>

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains hello entity
  }
});
```

<span data-ttu-id="c9ad2-194">После завершения этой операции `result` будет содержать сущность hello.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-194">Once this operation is complete, `result` will contain hello entity.</span></span>

## <a name="query-a-set-of-entities"></a><span data-ttu-id="c9ad2-195">Запрос набора сущностей</span><span class="sxs-lookup"><span data-stu-id="c9ad2-195">Query a set of entities</span></span>
<span data-ttu-id="c9ad2-196">tooquery таблицы, используйте hello **TableQuery** toobuild выражение запроса, с помощью следующих предложений hello объекта:</span><span class="sxs-lookup"><span data-stu-id="c9ad2-196">tooquery a table, use hello **TableQuery** object toobuild up a query expression using hello following clauses:</span></span>

* <span data-ttu-id="c9ad2-197">**Выберите** -toobe hello полей, возвращаемых запросом hello</span><span class="sxs-lookup"><span data-stu-id="c9ad2-197">**select** - hello fields toobe returned from hello query</span></span>
* <span data-ttu-id="c9ad2-198">**где** — hello где предложения</span><span class="sxs-lookup"><span data-stu-id="c9ad2-198">**where** - hello where clause</span></span>

  * <span data-ttu-id="c9ad2-199">**and** — условие `and` в предложении where.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-199">**and** - an `and` where condition</span></span>
  * <span data-ttu-id="c9ad2-200">**or** — условие `or` в предложении where.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-200">**or** - an `or` where condition</span></span>
* <span data-ttu-id="c9ad2-201">**Начало** -количество элементов toofetch hello</span><span class="sxs-lookup"><span data-stu-id="c9ad2-201">**top** - hello number of items toofetch</span></span>

<span data-ttu-id="c9ad2-202">Hello следующий пример строится запрос, возвращающий hello top пяти элементов с PartitionKey «hometasks».</span><span class="sxs-lookup"><span data-stu-id="c9ad2-202">hello following example builds a query that will return hello top five items with a PartitionKey of 'hometasks'.</span></span>

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

<span data-ttu-id="c9ad2-203">Так как параметр **select** не используется, возвращаются все поля.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-203">Since **select** is not used, all fields will be returned.</span></span> <span data-ttu-id="c9ad2-204">tooperform hello запрос к таблице, используйте **queryEntities**.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-204">tooperform hello query against a table, use **queryEntities**.</span></span> <span data-ttu-id="c9ad2-205">Hello следующий пример использует этот tooreturn запросы к сущностям из «mytable».</span><span class="sxs-lookup"><span data-stu-id="c9ad2-205">hello following example uses this query tooreturn entities from 'mytable'.</span></span>

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

<span data-ttu-id="c9ad2-206">В случае успешного выполнения `result.entries` будет содержать массив объектов, соответствующих запросу hello.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-206">If successful, `result.entries` will contain an array of entities that match hello query.</span></span> <span data-ttu-id="c9ad2-207">Если hello запроса было невозможно tooreturn все сущности `result.continuationToken` будет отличных*null* и может использоваться как hello третий параметр **queryEntities** tooretrieve дополнительных результатов.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-207">If hello query was unable tooreturn all entities, `result.continuationToken` will be non-*null* and can be used as hello third parameter of **queryEntities** tooretrieve more results.</span></span> <span data-ttu-id="c9ad2-208">Начальный запрос hello, используйте *null* для третьего параметра hello.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-208">For hello initial query, use *null* for hello third parameter.</span></span>

### <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="c9ad2-209">Запрос подмножества свойств сущности</span><span class="sxs-lookup"><span data-stu-id="c9ad2-209">Query a subset of entity properties</span></span>
<span data-ttu-id="c9ad2-210">Таблицы tooa запроса можно получить лишь несколько полей из сущности.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-210">A query tooa table can retrieve just a few fields from an entity.</span></span>
<span data-ttu-id="c9ad2-211">Этот позволяет снизить потребление пропускной способности и может повысить производительность запросов, особенно для крупных сущностей.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-211">This reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="c9ad2-212">Используйте hello **выберите** возвращается предложения и передайте hello имена полей toobe hello.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-212">Use hello **select** clause and pass hello names of hello fields toobe returned.</span></span> <span data-ttu-id="c9ad2-213">Например, hello следующий запрос возвращает только hello **описание** и **dueDate** поля.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-213">For example, hello following query will return only hello **description** and **dueDate** fields.</span></span>

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a><span data-ttu-id="c9ad2-214">Удаление сущности</span><span class="sxs-lookup"><span data-stu-id="c9ad2-214">Delete an entity</span></span>
<span data-ttu-id="c9ad2-215">Сущность можно удалить с помощью ее ключей раздела и строки.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-215">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="c9ad2-216">В этом примере hello **task1** объект содержит hello **RowKey** и **PartitionKey** значения toobe сущности hello удален.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-216">In this example, hello **task1** object contains hello **RowKey** and **PartitionKey** values of hello entity toobe deleted.</span></span> <span data-ttu-id="c9ad2-217">Затем hello объекта передается toohello **deleteEntity** метод.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-217">Then hello object is passed toohello **deleteEntity** method.</span></span>

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
> <span data-ttu-id="c9ad2-218">Рассмотрите возможность использования теги eTag, при удалении элементов, tooensure, hello элемента еще не были изменены другим процессом.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-218">Consider using ETags when deleting items, tooensure that hello item hasn't been modified by another process.</span></span> <span data-ttu-id="c9ad2-219">Сведения об использовании тегов ETag см. в разделе [Обновление сущности](#update-an-entity).</span><span class="sxs-lookup"><span data-stu-id="c9ad2-219">See [Update an entity](#update-an-entity) for information on using ETags.</span></span>
>
>

## <a name="delete-a-table"></a><span data-ttu-id="c9ad2-220">Удаление таблицы</span><span class="sxs-lookup"><span data-stu-id="c9ad2-220">Delete a table</span></span>
<span data-ttu-id="c9ad2-221">Привет, следующий код удаляет таблицу из учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-221">hello following code deletes a table from a storage account.</span></span>

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

<span data-ttu-id="c9ad2-222">Если неизвестно, существует ли таблица hello, используйте **deleteTableIfExists**.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-222">If you are uncertain whether hello table exists, use **deleteTableIfExists**.</span></span>

## <a name="use-continuation-tokens"></a><span data-ttu-id="c9ad2-223">Использование маркеров продолжения</span><span class="sxs-lookup"><span data-stu-id="c9ad2-223">Use continuation tokens</span></span>
<span data-ttu-id="c9ad2-224">При выполнении запросов к таблицам для получения больших объемов результатов следует искать маркеры продолжения.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-224">When you are querying tables for large amounts of results, look for continuation tokens.</span></span> <span data-ttu-id="c9ad2-225">Может существовать больших объемов данных, могут не узнать, если при наличии токен продолжения не создавайте toorecognize запроса.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-225">There may be large amounts of data available for your query that you might not realize if you do not build toorecognize when a continuation token is present.</span></span>

<span data-ttu-id="c9ad2-226">результаты Hello объекта, возвращенного во время запроса наборов сущностей `continuationToken` свойства при наличии такой токен.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-226">hello results object returned during querying entities sets a `continuationToken` property when such a token is present.</span></span> <span data-ttu-id="c9ad2-227">Это затем можно использовать при выполнении запроса toocontinue toomove между сущностями hello секции и таблицы.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-227">You can then use this when performing a query toocontinue toomove across hello partition and table entities.</span></span>

<span data-ttu-id="c9ad2-228">При выполнении запросов, параметр continuationToken может предоставляться между экземпляром объекта запроса hello и функция обратного вызова hello:</span><span class="sxs-lookup"><span data-stu-id="c9ad2-228">When querying, a continuationToken parameter may be provided between hello query object instance and hello callback function:</span></span>

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

<span data-ttu-id="c9ad2-229">Если проверить hello `continuationToken` объект, свойства будут находиться такие как `nextPartitionKey`, `nextRowKey` и `targetLocation`, которую можно использовать tooiterate по результатам всех hello.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-229">If you inspect hello `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used tooiterate through all hello results.</span></span>

<span data-ttu-id="c9ad2-230">Также есть пример продолжения в пределах репозиторию hello Node.js хранилища Azure на GitHub.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-230">There is also a continuation sample within hello Azure Storage Node.js repo on GitHub.</span></span> <span data-ttu-id="c9ad2-231">Поищите `examples/samples/continuationsample.js`.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-231">Look for `examples/samples/continuationsample.js`.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="c9ad2-232">Работа с подписями общего доступа</span><span class="sxs-lookup"><span data-stu-id="c9ad2-232">Work with shared access signatures</span></span>
<span data-ttu-id="c9ad2-233">Подписи общего доступа (SAS) являются tootables детального доступа tooprovide безопасным способом, без указания имени учетной записи хранения или ключи.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-233">Shared access signatures (SAS) are a secure way tooprovide granular access tootables without providing your storage account name or keys.</span></span> <span data-ttu-id="c9ad2-234">SAS чаще используется tooprovide ограниченный доступ tooyour данных, например разрешение записи tooquery мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-234">SAS are often used tooprovide limited access tooyour data, such as allowing a mobile app tooquery records.</span></span>

<span data-ttu-id="c9ad2-235">Доверенного приложения, такие как облачная служба создает подписанный URL-адрес с помощью hello **generateSharedAccessSignature** из hello **TableService**и предоставляет его tooan приложения с частичным доверием или без доверия Например, мобильные приложения.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-235">A trusted application such as a cloud-based service generates a SAS using hello **generateSharedAccessSignature** of hello **TableService**, and provides it tooan untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="c9ad2-236">Hello SAS создается с помощью политики, которая описывает hello начала и окончания в какой hello действует SAS, а также hello владельца SAS уровня toohello предоставленный доступ.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-236">hello SAS is generated using a policy, which describes hello start and end dates during which hello SAS is valid, as well as hello access level granted toohello SAS holder.</span></span>

<span data-ttu-id="c9ad2-237">Hello следующий пример создает новую политику общего доступа, который позволит hello таблицы hello SAS владельца tooquery («r») и истечения срока действия 100 минут после hello время его создания.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-237">hello following example generates a new shared access policy that will allow hello SAS holder tooquery ('r') hello table, and expires 100 minutes after hello time it is created.</span></span>

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

<span data-ttu-id="c9ad2-238">Обратите внимание, что сведения об узле hello должен предоставляемых также, при необходимости при владельца SAS hello попытке tooaccess hello таблицы.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-238">Note that hello host information must be provided also, as it is required when hello SAS holder attempts tooaccess hello table.</span></span>

<span data-ttu-id="c9ad2-239">Здравствуйте клиентское приложение, а затем использует hello SAS с **TableServiceWithSAS** tooperform операций hello для таблицы.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-239">hello client application then uses hello SAS with **TableServiceWithSAS** tooperform operations against hello table.</span></span> <span data-ttu-id="c9ad2-240">Следующий пример Hello подключается toohello таблицы и выполняет запрос.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-240">hello following example connects toohello table and performs a query.</span></span>

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains hello entities
  }
});
```

<span data-ttu-id="c9ad2-241">Поскольку hello SAS был сформирован с использованием только доступ запроса, если были предпринята попытка tooinsert, обновления или удаления сущности, будет возвращена ошибка.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-241">Since hello SAS was generated with only query access, if an attempt were made tooinsert, update, or delete entities, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="c9ad2-242">Списки управления доступом</span><span class="sxs-lookup"><span data-stu-id="c9ad2-242">Access Control Lists</span></span>
<span data-ttu-id="c9ad2-243">Также можно использовать политику доступа hello tooset список управления доступом (ACL) для SAS.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-243">You can also use an Access Control List (ACL) tooset hello access policy for a SAS.</span></span> <span data-ttu-id="c9ad2-244">Это полезно в том случае, если хотите tooallow таблицы hello tooaccess несколько клиентов, но добавлены политики различный уровень доступа для каждого клиента.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-244">This is useful if you wish tooallow multiple clients tooaccess hello table, but provide different access policies for each client.</span></span>

<span data-ttu-id="c9ad2-245">ACL реализуется с помощью массива политик доступа, каждая из которых связана со своим идентификатором.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-245">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="c9ad2-246">Следующий пример Hello определяет две политики: для «user1» и для «user2»:</span><span class="sxs-lookup"><span data-stu-id="c9ad2-246">hello following example defines two policies, one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="c9ad2-247">Следующий пример возвращает Hello hello текущего списка управления Доступом для hello **hometasks** таблицы, а затем добавляет hello новые политики с помощью **setTableAcl**.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-247">hello following example gets hello current ACL for hello **hometasks** table, and then adds hello new policies using **setTableAcl**.</span></span> <span data-ttu-id="c9ad2-248">Такой подход допускает выполнение:</span><span class="sxs-lookup"><span data-stu-id="c9ad2-248">This approach allows:</span></span>

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

<span data-ttu-id="c9ad2-249">Один раз hello ACL было указано, можно создать на основе кода hello политики SAS.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-249">Once hello ACL has been set, you can then create a SAS based on hello ID for a policy.</span></span> <span data-ttu-id="c9ad2-250">Привет, следующий пример создает новый SAS для «user2»:</span><span class="sxs-lookup"><span data-stu-id="c9ad2-250">hello following example creates a new SAS for 'user2':</span></span>

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="c9ad2-251">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c9ad2-251">Next steps</span></span>
<span data-ttu-id="c9ad2-252">Дополнительные сведения см. в разделе hello следующие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-252">For more information, see hello following resources.</span></span>

* <span data-ttu-id="c9ad2-253">[Обозреватель хранилищ Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) является бесплатной, отдельное приложение от Майкрософт, позволяющая toowork визуально с помощью данных из хранилища Azure в Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="c9ad2-254">[Пакет SDK службы хранилища Azure для Node](https://github.com/Azure/azure-storage-node) на веб-сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-254">[Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) repository on GitHub.</span></span>
* [<span data-ttu-id="c9ad2-255">Центр разработчиков Node.js.</span><span class="sxs-lookup"><span data-stu-id="c9ad2-255">Node.js Developer Center</span></span>](/develop/nodejs/)
* [<span data-ttu-id="c9ad2-256">Создание и развертывание tooan приложений Node.js веб-сайте Azure</span><span class="sxs-lookup"><span data-stu-id="c9ad2-256">Create and deploy a Node.js application tooan Azure website</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
