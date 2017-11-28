---
title: "aaaHow toouse хранилища BLOB-объектов из Node.js | Документы Microsoft"
description: "Храните неструктурированные данные в облаке hello с хранилищем больших двоичных объектов Azure (хранилище объектов)."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 8b0df222-1ca8-4967-8248-6d6d720947b8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 572e7fc9f7b19ff01720a7cadd495c809ed49fb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-nodejs"></a><span data-ttu-id="49102-103">Как toouse хранилища BLOB-объектов из Node.js</span><span class="sxs-lookup"><span data-stu-id="49102-103">How toouse Blob storage from Node.js</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="49102-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="49102-104">Overview</span></span>
<span data-ttu-id="49102-105">В этой статье показано, как tooperform распространенные сценарии использования хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="49102-105">This article shows you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="49102-106">образцы Hello записываются через Node.js API hello.</span><span class="sxs-lookup"><span data-stu-id="49102-106">hello samples are written via hello Node.js API.</span></span> <span data-ttu-id="49102-107">Hello сценарии включают как tooupload, список, загрузка и удаление больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="49102-107">hello scenarios covered include how tooupload, list, download, and delete blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="49102-108">Создание приложения Node.js</span><span class="sxs-lookup"><span data-stu-id="49102-108">Create a Node.js application</span></span>
<span data-ttu-id="49102-109">Инструкции о том, как toocreate приложения Node.js, см. раздел [создание веб-приложения в службе приложений Azure Node.js], [построения и развертывания tooan приложений Node.js облачной службы Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) — с помощью Windows PowerShell или [сборки и развертывание приложения tooAzure web Node.js, с помощью Web Matrix](https://www.microsoft.com/web/webmatrix/).</span><span class="sxs-lookup"><span data-stu-id="49102-109">For instructions on how toocreate a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) -- using Windows PowerShell, or [Build and deploy a Node.js web app tooAzure using Web Matrix](https://www.microsoft.com/web/webmatrix/).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="49102-110">Настройка хранилища tooaccess приложения</span><span class="sxs-lookup"><span data-stu-id="49102-110">Configure your application tooaccess storage</span></span>
<span data-ttu-id="49102-111">toouse хранилища Azure необходимо hello пакет SDK хранилища Azure для Node.js, включающий набор библиотек удобства, взаимодействующих со службами REST hello хранилища.</span><span class="sxs-lookup"><span data-stu-id="49102-111">toouse Azure storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="49102-112">С помощью диспетчера пакетов узла (NPM) tooobtain hello пакета</span><span class="sxs-lookup"><span data-stu-id="49102-112">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="49102-113">Использовать интерфейс командной строки, такие как **PowerShell** (Windows), **терминалов** (Mac), или **Bash** (Unix), toonavigate toohello папку, где создан примера приложение.</span><span class="sxs-lookup"><span data-stu-id="49102-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), toonavigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="49102-114">Тип **npm установить хранилища azure** в командном окне приветствия.</span><span class="sxs-lookup"><span data-stu-id="49102-114">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="49102-115">Выходные данные команды hello — примерно toohello следующий пример кода.</span><span class="sxs-lookup"><span data-stu-id="49102-115">Output from hello command is similar toohello following code example.</span></span>

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
3. <span data-ttu-id="49102-116">Вы можете вручную запустить hello **ls** tooverify команды, **узел\_модули** папка была создана.</span><span class="sxs-lookup"><span data-stu-id="49102-116">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="49102-117">В этой папке найти hello **хранилища azure** пакет, который содержит необходимые хранилища tooaccess библиотеки hello.</span><span class="sxs-lookup"><span data-stu-id="49102-117">Inside that folder, find hello **azure-storage** package, which contains hello libraries that you need tooaccess storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="49102-118">Импорт пакета hello</span><span class="sxs-lookup"><span data-stu-id="49102-118">Import hello package</span></span>
<span data-ttu-id="49102-119">С помощью блокнота или другого текстового редактора, добавьте следующие toohello вверху hello hello **server.js** файл приложения hello предполагаемой toouse хранилища:</span><span class="sxs-lookup"><span data-stu-id="49102-119">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application where you intend toouse storage:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="49102-120">Настройка подключения к службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="49102-120">Set up an Azure Storage connection</span></span>
<span data-ttu-id="49102-121">Hello модуль Azure будет считывать переменные среды hello `AZURE_STORAGE_ACCOUNT` и `AZURE_STORAGE_ACCESS_KEY`, или `AZURE_STORAGE_CONNECTION_STRING`, сведения, необходимые учетной записи хранилища Azure tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="49102-121">hello Azure module will read hello environment variables `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY`, or `AZURE_STORAGE_CONNECTION_STRING`, for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="49102-122">Если эти переменные среды не установлены, необходимо указать сведения об учетной записи hello при вызове **createBlobService**.</span><span class="sxs-lookup"><span data-stu-id="49102-122">If these environment variables are not set, you must specify hello account information when calling **createBlobService**.</span></span>

<span data-ttu-id="49102-123">Пример настройки переменных среды hello в hello [портал Azure](https://portal.azure.com) Azure веб-приложение в разделе [Node.js веб-приложения с использованием hello службы таблиц Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="49102-123">For an example of setting hello environment variables in hello [Azure portal](https://portal.azure.com) for an Azure web app, see [Node.js web app using hello Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-container"></a><span data-ttu-id="49102-124">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="49102-124">Create a container</span></span>
<span data-ttu-id="49102-125">Hello **BlobService** объектов позволяет работать с контейнерами и BLOB-объектов.</span><span class="sxs-lookup"><span data-stu-id="49102-125">hello **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="49102-126">Hello следующий код создает **BlobService** объекта.</span><span class="sxs-lookup"><span data-stu-id="49102-126">hello following code creates a **BlobService** object.</span></span> <span data-ttu-id="49102-127">Добавьте следующее hello вверху hello **server.js**:</span><span class="sxs-lookup"><span data-stu-id="49102-127">Add hello following near hello top of **server.js**:</span></span>

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> <span data-ttu-id="49102-128">Вы можете анонимный доступ к большой двоичный объект с помощью **createBlobServiceAnonymous** и указать адрес узла hello.</span><span class="sxs-lookup"><span data-stu-id="49102-128">You can access a blob anonymously by using **createBlobServiceAnonymous** and providing hello host address.</span></span> <span data-ttu-id="49102-129">Например, воспользуйтесь `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span><span class="sxs-lookup"><span data-stu-id="49102-129">For example, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="49102-130">использовать новый контейнер toocreate **createContainerIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="49102-130">toocreate a new container, use **createContainerIfNotExists**.</span></span> <span data-ttu-id="49102-131">Hello следующий пример кода создает новый контейнер с именем «mycontainer»:</span><span class="sxs-lookup"><span data-stu-id="49102-131">hello following code example creates a new container named 'mycontainer':</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

<span data-ttu-id="49102-132">Если контейнер hello вновь создан, `result.created` имеет значение true.</span><span class="sxs-lookup"><span data-stu-id="49102-132">If hello container is newly created, `result.created` is true.</span></span> <span data-ttu-id="49102-133">Если контейнер hello уже существует, `result.created` имеет значение false.</span><span class="sxs-lookup"><span data-stu-id="49102-133">If hello container already exists, `result.created` is false.</span></span> <span data-ttu-id="49102-134">`response`содержит сведения об операции hello, включая сведения hello ETag для контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="49102-134">`response` contains information about hello operation, including hello ETag information for hello container.</span></span>

### <a name="container-security"></a><span data-ttu-id="49102-135">Безопасность контейнера</span><span class="sxs-lookup"><span data-stu-id="49102-135">Container security</span></span>
<span data-ttu-id="49102-136">По умолчанию все контейнеры частные, и доступ к ним не может быть анонимным.</span><span class="sxs-lookup"><span data-stu-id="49102-136">By default, new containers are private and cannot be accessed anonymously.</span></span> <span data-ttu-id="49102-137">контейнер hello toomake public, его можно открыть анонимно, можно задать уровень доступа для контейнера hello слишком**большого двоичного объекта** или **контейнер**.</span><span class="sxs-lookup"><span data-stu-id="49102-137">toomake hello container public so that you can access it anonymously, you can set hello container's access level too**blob** or **container**.</span></span>

* <span data-ttu-id="49102-138">**большой двоичный объект** -позволяет анонимный доступ для чтения tooblob содержимого и метаданных в контейнере, но не toocontainer метаданные, такие как перечисление всех больших двоичных объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="49102-138">**blob** - allows anonymous read access tooblob content and metadata within this container, but not toocontainer metadata such as listing all blobs within a container</span></span>
* <span data-ttu-id="49102-139">**контейнер** -разрешает анонимный доступ для чтения tooblob содержимого и метаданных, а также метаданные контейнера</span><span class="sxs-lookup"><span data-stu-id="49102-139">**container** - allows anonymous read access tooblob content and metadata as well as container metadata</span></span>

<span data-ttu-id="49102-140">Hello следующий пример кода демонстрирует уровень доступа hello слишком**больших двоичных объектов**:</span><span class="sxs-lookup"><span data-stu-id="49102-140">hello following code example demonstrates setting hello access level too**blob**:</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access tooblob
      // content and metadata within this container
    }
});
```

<span data-ttu-id="49102-141">Кроме того, можно изменить уровень доступа hello контейнера с помощью **setContainerAcl** toospecify уровень доступа hello.</span><span class="sxs-lookup"><span data-stu-id="49102-141">Alternatively, you can modify hello access level of a container by using **setContainerAcl** toospecify hello access level.</span></span> <span data-ttu-id="49102-142">Hello следующий код уровня toocontainer hello изменения доступа пример:</span><span class="sxs-lookup"><span data-stu-id="49102-142">hello following code example changes hello access level toocontainer:</span></span>

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set too'container'
  }
});
```

<span data-ttu-id="49102-143">Hello результат содержит сведения об операции hello, включая текущий hello **ETag** для контейнера hello.</span><span class="sxs-lookup"><span data-stu-id="49102-143">hello result contains information about hello operation, including hello current **ETag** for hello container.</span></span>

### <a name="filters"></a><span data-ttu-id="49102-144">Фильтры</span><span class="sxs-lookup"><span data-stu-id="49102-144">Filters</span></span>
<span data-ttu-id="49102-145">Можно применить необязательно фильтрации операций toooperations выполняется с использованием **BlobService**.</span><span class="sxs-lookup"><span data-stu-id="49102-145">You can apply optional filtering operations toooperations performed using **BlobService**.</span></span> <span data-ttu-id="49102-146">К операциям фильтрации могут относиться ведение журнала, автоматический повтор и т. д. Фильтры являются объектами, которые реализуют метод с сигнатурой hello:</span><span class="sxs-lookup"><span data-stu-id="49102-146">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="49102-147">После выполнения его предварительной обработки параметров запроса hello, метод hello должен toocall «Далее», передача обратный вызов с hello следующие подписи:</span><span class="sxs-lookup"><span data-stu-id="49102-147">After doing its preprocessing on hello request options, hello method needs toocall "next", passing a callback with hello following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="49102-148">В этот обратный вызов, а после обработки returnObject hello (hello ответ от сервера toohello hello запроса), обратного вызова hello необходимы tooeither рядом вызова, если он существует toocontinue обработки других фильтров, или просто вызвать службу hello tooend finalCallback вызов.</span><span class="sxs-lookup"><span data-stu-id="49102-148">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback tooend hello service invocation.</span></span>

<span data-ttu-id="49102-149">Два фильтра, которые реализовать логику повторных попыток входят в состав hello Azure SDK для Node.js **ExponentialRetryPolicyFilter** и **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="49102-149">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="49102-150">Hello следующий код создает **BlobService** объект, который использует hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="49102-150">hello following creates a **BlobService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="49102-151">Отправка BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="49102-151">Upload a blob into a container</span></span>
<span data-ttu-id="49102-152">Существует три типа больших двоичных объектов: блочные, страничные и добавочные.</span><span class="sxs-lookup"><span data-stu-id="49102-152">There are three types of blobs: block blobs, page blobs and append blobs.</span></span> <span data-ttu-id="49102-153">Блочные большие двоичные объекты позволяют toomore эффективной загрузки больших объемов данных.</span><span class="sxs-lookup"><span data-stu-id="49102-153">Block blobs allow you toomore efficiently upload large data.</span></span> <span data-ttu-id="49102-154">Добавочные BLOB-объекты оптимизированы для операций добавления.</span><span class="sxs-lookup"><span data-stu-id="49102-154">Append blobs are optimized for append operations.</span></span> <span data-ttu-id="49102-155">Страничные BLOB-объекты оптимизированы для операций чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="49102-155">Page blobs are optimized for read/write operations.</span></span> <span data-ttu-id="49102-156">Дополнительные сведения см. в статье [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx) (Основные сведения о блочных, добавочных и страничных BLOB-объектах).</span><span class="sxs-lookup"><span data-stu-id="49102-156">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

### <a name="block-blobs"></a><span data-ttu-id="49102-157">Blob-блоки</span><span class="sxs-lookup"><span data-stu-id="49102-157">Block blobs</span></span>
<span data-ttu-id="49102-158">tooupload данных tooa блочного BLOB-объекта, используйте hello следующие:</span><span class="sxs-lookup"><span data-stu-id="49102-158">tooupload data tooa block blob, use hello following:</span></span>

* <span data-ttu-id="49102-159">**createBlockBlobFromLocalFile** - создает новый большой двоичный объект и загружает содержимое файла hello</span><span class="sxs-lookup"><span data-stu-id="49102-159">**createBlockBlobFromLocalFile** - creates a new block blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="49102-160">**createBlockBlobFromStream** - создает новый большой двоичный объект и отправляет hello содержимое потока</span><span class="sxs-lookup"><span data-stu-id="49102-160">**createBlockBlobFromStream** - creates a new block blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="49102-161">**createBlockBlobFromText** - создает новый большой двоичный объект и загружает содержимое строки hello</span><span class="sxs-lookup"><span data-stu-id="49102-161">**createBlockBlobFromText** - creates a new block blob and uploads hello contents of a string</span></span>
* <span data-ttu-id="49102-162">**createWriteStreamToBlockBlob** -предоставляет большой двоичный объект блока записи потока tooa</span><span class="sxs-lookup"><span data-stu-id="49102-162">**createWriteStreamToBlockBlob** - provides a write stream tooa block blob</span></span>

<span data-ttu-id="49102-163">Hello следующий пример кода загружает содержимое hello hello **test.txt** файла в **«myblob»**.</span><span class="sxs-lookup"><span data-stu-id="49102-163">hello following code example uploads hello contents of hello **test.txt** file into **myblob**.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="49102-164">Hello `result` возвращаемые этими методами содержится информация о hello операцию, например hello **ETag** hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="49102-164">hello `result` returned by these methods contains information on hello operation, such as hello **ETag** of hello blob.</span></span>

### <a name="append-blobs"></a><span data-ttu-id="49102-165">Добавочные BLOB-объекты</span><span class="sxs-lookup"><span data-stu-id="49102-165">Append blobs</span></span>
<span data-ttu-id="49102-166">новый tooa данных tooupload append больших двоичных объектов, используйте hello ниже:</span><span class="sxs-lookup"><span data-stu-id="49102-166">tooupload data tooa new append blob, use hello following:</span></span>

* <span data-ttu-id="49102-167">**createAppendBlobFromLocalFile** - создает новый добавочный большой двоичный объект и загружает содержимое файла hello</span><span class="sxs-lookup"><span data-stu-id="49102-167">**createAppendBlobFromLocalFile** - creates a new append blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="49102-168">**createAppendBlobFromStream** - создает новый добавочный большой двоичный объект и отправляет hello содержимое потока</span><span class="sxs-lookup"><span data-stu-id="49102-168">**createAppendBlobFromStream** - creates a new append blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="49102-169">**createAppendBlobFromText** - создает новый добавочный большой двоичный объект и загружает содержимое строки hello</span><span class="sxs-lookup"><span data-stu-id="49102-169">**createAppendBlobFromText** - creates a new append blob and uploads hello contents of a string</span></span>
* <span data-ttu-id="49102-170">**createWriteStreamToNewAppendBlob** — создает новый добавочный большой двоичный объект, а затем предоставляет tooit toowrite потока</span><span class="sxs-lookup"><span data-stu-id="49102-170">**createWriteStreamToNewAppendBlob** - creates a new append blob and then provides a stream toowrite tooit</span></span>

<span data-ttu-id="49102-171">Hello следующий пример кода загружает содержимое hello hello **test.txt** файла в **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="49102-171">hello following code example uploads hello contents of hello **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="49102-172">tooappend в существующие tooan блок append большого двоичного объекта, используйте hello следующие:</span><span class="sxs-lookup"><span data-stu-id="49102-172">tooappend a block tooan existing append blob, use hello following:</span></span>

* <span data-ttu-id="49102-173">**appendFromLocalFile** -добавить содержимое hello tooan файл существующих append больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="49102-173">**appendFromLocalFile** - append hello contents of a file tooan existing append blob</span></span>
* <span data-ttu-id="49102-174">**appendFromStream** -добавить содержимое hello tooan поток существующих append больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="49102-174">**appendFromStream** - append hello contents of a stream tooan existing append blob</span></span>
* <span data-ttu-id="49102-175">**appendFromText** -добавить содержимое hello tooan строка существующих append больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="49102-175">**appendFromText** - append hello contents of a string tooan existing append blob</span></span>
* <span data-ttu-id="49102-176">**appendBlockFromStream** -добавить содержимое hello tooan поток существующих append больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="49102-176">**appendBlockFromStream** - append hello contents of a stream tooan existing append blob</span></span>
* <span data-ttu-id="49102-177">**appendBlockFromText** -добавить содержимое hello tooan строка существующих append больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="49102-177">**appendBlockFromText** - append hello contents of a string tooan existing append blob</span></span>

> [!NOTE]
> <span data-ttu-id="49102-178">API-интерфейсы appendFromXXX будет выполнять некоторые вызовы ненужные server быстро tooavoid toofail проверки на стороне клиента.</span><span class="sxs-lookup"><span data-stu-id="49102-178">appendFromXXX APIs will do some client-side validation toofail fast tooavoid unnecessary server calls.</span></span> <span data-ttu-id="49102-179">appendBlockFromXXX не будут делать этого.</span><span class="sxs-lookup"><span data-stu-id="49102-179">appendBlockFromXXX won't.</span></span>
>
>

<span data-ttu-id="49102-180">Hello следующий пример кода загружает содержимое hello hello **test.txt** файла в **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="49102-180">hello following code example uploads hello contents of hello **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text toobe appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a><span data-ttu-id="49102-181">Blob-страницы</span><span class="sxs-lookup"><span data-stu-id="49102-181">Page blobs</span></span>
<span data-ttu-id="49102-182">tooupload данных tooa страничного большого двоичного объекта, используйте hello следующие:</span><span class="sxs-lookup"><span data-stu-id="49102-182">tooupload data tooa page blob, use hello following:</span></span>

* <span data-ttu-id="49102-183">**createPageBlob** — создает новый страничный BLOB-объект заданной длины.</span><span class="sxs-lookup"><span data-stu-id="49102-183">**createPageBlob** - creates a new page blob of a specific length</span></span>
* <span data-ttu-id="49102-184">**createPageBlobFromLocalFile** - создает новый большой двоичный объект страницы и загружает содержимое файла hello</span><span class="sxs-lookup"><span data-stu-id="49102-184">**createPageBlobFromLocalFile** - creates a new page blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="49102-185">**createPageBlobFromStream** - создает новый большой двоичный объект страницы и передает hello содержимое потока</span><span class="sxs-lookup"><span data-stu-id="49102-185">**createPageBlobFromStream** - creates a new page blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="49102-186">**createWriteStreamToExistingPageBlob** -предоставляет записи потока tooan существующий страничный большой двоичный объект</span><span class="sxs-lookup"><span data-stu-id="49102-186">**createWriteStreamToExistingPageBlob** - provides a write stream tooan existing page blob</span></span>
* <span data-ttu-id="49102-187">**createWriteStreamToNewPageBlob** — создает новый большой двоичный объект страницы, а затем предоставляет tooit toowrite потока</span><span class="sxs-lookup"><span data-stu-id="49102-187">**createWriteStreamToNewPageBlob** - creates a new page blob and then provides a stream toowrite tooit</span></span>

<span data-ttu-id="49102-188">Hello следующий пример кода загружает содержимое hello hello **test.txt** файла в **mypageblob**.</span><span class="sxs-lookup"><span data-stu-id="49102-188">hello following code example uploads hello contents of hello **test.txt** file into **mypageblob**.</span></span>

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> <span data-ttu-id="49102-189">Страничные Вlob-объекты состоят из 512-байтовых "страниц".</span><span class="sxs-lookup"><span data-stu-id="49102-189">Page blobs consist of 512-byte 'pages'.</span></span> <span data-ttu-id="49102-190">При отправке файлов с размером, не кратным 512, может возникать ошибка.</span><span class="sxs-lookup"><span data-stu-id="49102-190">You will receive an error when uploading data with a size that is not a multiple of 512.</span></span>
>
>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="49102-191">Перечисление hello больших двоичных объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="49102-191">List hello blobs in a container</span></span>
<span data-ttu-id="49102-192">toolist hello BLOB-объектов в контейнере, используйте hello **listBlobsSegmented** метод.</span><span class="sxs-lookup"><span data-stu-id="49102-192">toolist hello blobs in a container, use hello **listBlobsSegmented** method.</span></span> <span data-ttu-id="49102-193">Если вы хотите tooreturn большие двоичные объекты с определенным префиксом, используйте **listBlobsSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="49102-193">If you'd like tooreturn blobs with a specific prefix, use **listBlobsSegmentedWithPrefix**.</span></span>

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains hello entries
      // If not all blobs were returned, result.continuationToken has hello continuation token.
  }
});
```

<span data-ttu-id="49102-194">Hello `result` содержит `entries` коллекции, который является массивом объектов, которые описывают каждый BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="49102-194">hello `result` contains an `entries` collection, which is an array of objects that describe each blob.</span></span> <span data-ttu-id="49102-195">Здравствуйте, если все большие двоичные объекты, не может быть возвращен, `result` также предоставляет `continuationToken`, который может использоваться в качестве hello второй параметр tooretrieve дополнительных записей.</span><span class="sxs-lookup"><span data-stu-id="49102-195">If all blobs cannot be returned, hello `result` also provides a `continuationToken`, which you may use as hello second parameter tooretrieve additional entries.</span></span>

## <a name="download-blobs"></a><span data-ttu-id="49102-196">Скачивание больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="49102-196">Download blobs</span></span>
<span data-ttu-id="49102-197">toodownload данные из большого двоичного объекта используйте hello ниже:</span><span class="sxs-lookup"><span data-stu-id="49102-197">toodownload data from a blob, use hello following:</span></span>

* <span data-ttu-id="49102-198">**getBlobToLocalFile** -записывает содержимое toofile hello больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="49102-198">**getBlobToLocalFile** - writes hello blob contents toofile</span></span>
* <span data-ttu-id="49102-199">**getBlobToStream** -записывает поток tooa содержимое большого двоичного объекта hello</span><span class="sxs-lookup"><span data-stu-id="49102-199">**getBlobToStream** - writes hello blob contents tooa stream</span></span>
* <span data-ttu-id="49102-200">**getBlobToText** -записывает содержимое большого двоичного объекта hello tooa строку</span><span class="sxs-lookup"><span data-stu-id="49102-200">**getBlobToText** - writes hello blob contents tooa string</span></span>
* <span data-ttu-id="49102-201">**createReadStream** -предоставляет tooread поток из большого двоичного объекта hello</span><span class="sxs-lookup"><span data-stu-id="49102-201">**createReadStream** - provides a stream tooread from hello blob</span></span>

<span data-ttu-id="49102-202">Hello следующем примере кода показано использование **getBlobToStream** toodownload содержимое hello hello **«myblob»** больших двоичных объектов и их сохранения toohello **output.txt** файла с помощью поток:</span><span class="sxs-lookup"><span data-stu-id="49102-202">hello following code example demonstrates using **getBlobToStream** toodownload hello contents of hello **myblob** blob and store it toohello **output.txt** file by using a stream:</span></span>

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

<span data-ttu-id="49102-203">Hello `result` содержит сведения о больших двоичных объектов hello, включая **ETag** сведения.</span><span class="sxs-lookup"><span data-stu-id="49102-203">hello `result` contains information about hello blob, including **ETag** information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="49102-204">Удаление большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="49102-204">Delete a blob</span></span>
<span data-ttu-id="49102-205">Наконец, вызовите toodelete большой двоичный объект **deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="49102-205">Finally, toodelete a blob, call **deleteBlob**.</span></span> <span data-ttu-id="49102-206">Здравствуйте, следующий пример кода удаляет hello BLOB-объекта с именем **«myblob»**.</span><span class="sxs-lookup"><span data-stu-id="49102-206">hello following code example deletes hello blob named **myblob**.</span></span>

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a><span data-ttu-id="49102-207">Одновременный доступ</span><span class="sxs-lookup"><span data-stu-id="49102-207">Concurrent access</span></span>
<span data-ttu-id="49102-208">blob tooa toosupport одновременный доступ из нескольких клиентов или несколько экземпляров процесса, можно использовать **ETags** или **аренды**.</span><span class="sxs-lookup"><span data-stu-id="49102-208">toosupport concurrent access tooa blob from multiple clients or multiple process instances, you can use **ETags** or **leases**.</span></span>

* <span data-ttu-id="49102-209">**ETag** -предоставляет toodetect способом, который hello большого двоичного объекта или контейнера был изменен другим процессом</span><span class="sxs-lookup"><span data-stu-id="49102-209">**Etag** - provides a way toodetect that hello blob or container has been modified by another process</span></span>
* <span data-ttu-id="49102-210">**Аренда** — предоставляет способ tooobtain монопольный, обновляемым, запись или удаление больших двоичных объектов tooa доступ в течение заданного времени</span><span class="sxs-lookup"><span data-stu-id="49102-210">**Lease** - provides a way tooobtain exclusive, renewable, write or delete access tooa blob for a period of time</span></span>

### <a name="etag"></a><span data-ttu-id="49102-211">ETag</span><span class="sxs-lookup"><span data-stu-id="49102-211">ETag</span></span>
<span data-ttu-id="49102-212">Используйте теги eTag, если требуется tooallow клиентов или экземпляров toowrite toohello блочного большого двоичного объекта или страницы больших двоичных объектов одновременно.</span><span class="sxs-lookup"><span data-stu-id="49102-212">Use ETags if you need tooallow multiple clients or instances toowrite toohello block Blob or page Blob simultaneously.</span></span> <span data-ttu-id="49102-213">Hello ETag можно toodetermine, если hello контейнера или большого двоичного объекта был изменен с момента его изначально чтения или она создана, позволяющий tooavoid перезапись изменений, зафиксированных другим клиентом или процессом.</span><span class="sxs-lookup"><span data-stu-id="49102-213">hello ETag allows you toodetermine if hello container or blob was modified since you initially read or created it, which allows you tooavoid overwriting changes committed by another client or process.</span></span>

<span data-ttu-id="49102-214">Можно задать условия ETag с помощью hello необязательно `options.accessConditions` параметра.</span><span class="sxs-lookup"><span data-stu-id="49102-214">You can set ETag conditions by using hello optional `options.accessConditions` parameter.</span></span> <span data-ttu-id="49102-215">Hello следующий пример кода только передает hello **test.txt** содержится файл, если hello BLOB-объект уже существует и имеет значение ETag hello `etagToMatch`.</span><span class="sxs-lookup"><span data-stu-id="49102-215">hello following code example only uploads hello **test.txt** file if hello blob already exists and has hello ETag value contained by `etagToMatch`.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="49102-216">Если вы используете теги eTag, hello общим шаблоном является:</span><span class="sxs-lookup"><span data-stu-id="49102-216">When you're using ETags, hello general pattern is:</span></span>

1. <span data-ttu-id="49102-217">Получите hello ETag результате hello create, список или операции get.</span><span class="sxs-lookup"><span data-stu-id="49102-217">Obtain hello ETag as hello result of a create, list, or get operation.</span></span>
2. <span data-ttu-id="49102-218">Выполнить действие, проверка, hello значение ETag не был изменен.</span><span class="sxs-lookup"><span data-stu-id="49102-218">Perform an action, checking that hello ETag value has not been modified.</span></span>

<span data-ttu-id="49102-219">Если было изменено значение hello, это указывает, что другой клиент или экземпляр изменены hello большого двоичного объекта или контейнера со времени получения hello значение ETag.</span><span class="sxs-lookup"><span data-stu-id="49102-219">If hello value was modified, this indicates that another client or instance modified hello blob or container since you obtained hello ETag value.</span></span>

### <a name="lease"></a><span data-ttu-id="49102-220">Lease</span><span class="sxs-lookup"><span data-stu-id="49102-220">Lease</span></span>
<span data-ttu-id="49102-221">Можно приобрести новую аренду с помощью hello **acquireLease** метод, указывая hello большого двоичного объекта или контейнера, на котором необходимо tooobtain аренду на.</span><span class="sxs-lookup"><span data-stu-id="49102-221">You can acquire a new lease by using hello **acquireLease** method, specifying hello blob or container that you wish tooobtain a lease on.</span></span> <span data-ttu-id="49102-222">Например, следующий код hello аренды на **«myblob»**.</span><span class="sxs-lookup"><span data-stu-id="49102-222">For example, hello following code acquires a lease on **myblob**.</span></span>

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

<span data-ttu-id="49102-223">В последующих операциях в **«myblob»** необходимо предоставить hello `options.leaseId` параметра.</span><span class="sxs-lookup"><span data-stu-id="49102-223">Subsequent operations on **myblob** must provide hello `options.leaseId` parameter.</span></span> <span data-ttu-id="49102-224">Идентификатор возвращается в виде аренды Hello `result.id` из **acquireLease**.</span><span class="sxs-lookup"><span data-stu-id="49102-224">hello lease ID is returned as `result.id` from **acquireLease**.</span></span>

> [!NOTE]
> <span data-ttu-id="49102-225">По умолчанию срок действия аренды адреса hello бесконечна.</span><span class="sxs-lookup"><span data-stu-id="49102-225">By default, hello lease duration is infinite.</span></span> <span data-ttu-id="49102-226">Можно указать длительность бессрочной (от 15 до 60 секунд), предоставляя hello `options.leaseDuration` параметра.</span><span class="sxs-lookup"><span data-stu-id="49102-226">You can specify a non-infinite duration (between 15 and 60 seconds) by providing hello `options.leaseDuration` parameter.</span></span>
>
>

<span data-ttu-id="49102-227">использовать tooremove аренду, **releaseLease**.</span><span class="sxs-lookup"><span data-stu-id="49102-227">tooremove a lease, use **releaseLease**.</span></span> <span data-ttu-id="49102-228">toobreak аренды, но никто другой не получил новую аренду до истечения hello исходного срока хранения, используя **breakLease**.</span><span class="sxs-lookup"><span data-stu-id="49102-228">toobreak a lease, but prevent others from obtaining a new lease until hello original duration has expired, use **breakLease**.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="49102-229">Работа с подписями общего доступа</span><span class="sxs-lookup"><span data-stu-id="49102-229">Work with shared access signatures</span></span>
<span data-ttu-id="49102-230">Подписи коллективного доступа (SAS) являются tooblobs безопасным способом tooprovide детального доступа и контейнеров без указания имени учетной записи хранения или ключи.</span><span class="sxs-lookup"><span data-stu-id="49102-230">Shared access signatures (SAS) are a secure way tooprovide granular access tooblobs and containers without providing your storage account name or keys.</span></span> <span data-ttu-id="49102-231">Подписи коллективного доступа чаще используется tooprovide ограниченный доступ tooyour данных, например разрешение мобильное приложение tooaccess больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="49102-231">Shared access signatures are often used tooprovide limited access tooyour data, such as allowing a mobile app tooaccess blobs.</span></span>

> [!NOTE]
> <span data-ttu-id="49102-232">Хотя также можно разрешить анонимный доступ tooblobs, подписей общего доступа позволяют более контролируемых tooprovide доступ, как необходимо создать hello SAS.</span><span class="sxs-lookup"><span data-stu-id="49102-232">While you can also allow anonymous access tooblobs, shared access signatures allow you tooprovide more controlled access, as you must generate hello SAS.</span></span>
>
>

<span data-ttu-id="49102-233">Доверенного приложения, такие как облачная служба создает подписанных URL-адресов с помощью hello **generateSharedAccessSignature** из hello **BlobService**и предоставляет его tooan ненадежных или приложения с частичным доверием, например мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="49102-233">A trusted application such as a cloud-based service generates shared access signatures using hello **generateSharedAccessSignature** of hello **BlobService**, and provides it tooan untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="49102-234">Подписи создаются с помощью политики, которая описывает hello начала общего доступа и конечные даты, во время которого hello допустимы подписанных URL-адресов, а также hello доступ уровня предоставленный владельца toohello подписи общего доступа.</span><span class="sxs-lookup"><span data-stu-id="49102-234">Shared access signatures are generated using a policy, which describes hello start and end dates during which hello shared access signatures are valid, as well as hello access level granted toohello shared access signatures holder.</span></span>

<span data-ttu-id="49102-235">Hello следующий пример кода приводит к возникновению ошибки политику общего доступа, позволяющий подписи владельца hello общего доступа tooperform операции считывания в hello **«myblob»** больших двоичных объектов и истечения срока действия 100 минут после hello время ее создания.</span><span class="sxs-lookup"><span data-stu-id="49102-235">hello following code example generates a new shared access policy that allows hello shared access signatures holder tooperform read operations on hello **myblob** blob, and expires 100 minutes after hello time it is created.</span></span>

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
};

var blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', 'myblob', sharedAccessPolicy);
var host = blobSvc.host;
```

<span data-ttu-id="49102-236">Обратите внимание, что сведения об узле hello должен предоставляемых также, при необходимости при владельца подписи общего доступа hello попытке tooaccess hello контейнера.</span><span class="sxs-lookup"><span data-stu-id="49102-236">Note that hello host information must be provided also, as it is required when hello shared access signatures holder attempts tooaccess hello container.</span></span>

<span data-ttu-id="49102-237">Hello клиентское приложение затем использует подписанных URL-адресов с **BlobServiceWithSAS** tooperform операций, выполняемых hello большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="49102-237">hello client application then uses shared access signatures with **BlobServiceWithSAS** tooperform operations against hello blob.</span></span> <span data-ttu-id="49102-238">Hello следующие получает сведения **«myblob»**.</span><span class="sxs-lookup"><span data-stu-id="49102-238">hello following gets information about **myblob**.</span></span>

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

<span data-ttu-id="49102-239">Поскольку hello общий URL-адреса были созданы с доступом только для чтения, если предпринята toomodify hello больших двоичных объектов, будет возвращена ошибка.</span><span class="sxs-lookup"><span data-stu-id="49102-239">Since hello shared access signatures were generated with read-only access, if an attempt is made toomodify hello blob, an error will be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="49102-240">Доступ к спискам управления</span><span class="sxs-lookup"><span data-stu-id="49102-240">Access control lists</span></span>
<span data-ttu-id="49102-241">Можно также использовать политики управления доступом (ACL) список tooset hello доступа для SAS.</span><span class="sxs-lookup"><span data-stu-id="49102-241">You can also use an access control list (ACL) tooset hello access policy for SAS.</span></span> <span data-ttu-id="49102-242">Это полезно в том случае, если хотите tooallow несколько клиентов tooaccess контейнера, но добавлены политики различный уровень доступа для каждого клиента.</span><span class="sxs-lookup"><span data-stu-id="49102-242">This is useful if you wish tooallow multiple clients tooaccess a container but provide different access policies for each client.</span></span>

<span data-ttu-id="49102-243">ACL реализуется с помощью массива политик доступа, каждая из которых связана со своим идентификатором.</span><span class="sxs-lookup"><span data-stu-id="49102-243">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="49102-244">Следующий пример кода Hello определяет две политики: для «user1» и для «user2»:</span><span class="sxs-lookup"><span data-stu-id="49102-244">hello following code example defines two policies, one for 'user1' and one for 'user2':</span></span>

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.WRITE,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="49102-245">Следующий пример возвращает кода Hello hello текущего списка управления Доступом для **mycontainer**, а затем добавляет hello новые политики с помощью **setBlobAcl**.</span><span class="sxs-lookup"><span data-stu-id="49102-245">hello following code example gets hello current ACL for **mycontainer**, and then adds hello new policies using **setBlobAcl**.</span></span> <span data-ttu-id="49102-246">Такой подход допускает выполнение:</span><span class="sxs-lookup"><span data-stu-id="49102-246">This approach allows:</span></span>

```nodejs
var extend = require('extend');
blobSvc.getBlobAcl('mycontainer', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    blobSvc.setBlobAcl('mycontainer', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="49102-247">Один раз hello задан список управления Доступом, можно создать на основе кода hello политики подписанных URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="49102-247">Once hello ACL is set, you can then create shared access signatures based on hello ID for a policy.</span></span> <span data-ttu-id="49102-248">Следующий пример кода Hello создает новые подписи общего доступа для «user2»:</span><span class="sxs-lookup"><span data-stu-id="49102-248">hello following code example creates new shared access signatures for 'user2':</span></span>

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="49102-249">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="49102-249">Next steps</span></span>
<span data-ttu-id="49102-250">Дополнительные сведения см. в разделе hello следующие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="49102-250">For more information, see hello following resources.</span></span>

* <span data-ttu-id="49102-251">[Справочник по пакету SDK службы хранилища Azure для API Node] [Azure Storage SDK for Node API Reference]</span><span class="sxs-lookup"><span data-stu-id="49102-251">[Azure Storage SDK for Node API Reference][Azure Storage SDK for Node API Reference]</span></span>
* <span data-ttu-id="49102-252">[Блог рабочей группы службы хранилища Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="49102-252">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>
* <span data-ttu-id="49102-253">Репозиторий [пакета SDK хранилища Azure для Node][Azure Storage SDK for Node] на веб-сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="49102-253">[Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="49102-254">Центр разработчиков Node.js.</span><span class="sxs-lookup"><span data-stu-id="49102-254">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)
* [<span data-ttu-id="49102-255">Перенесите данные с помощью командной строки программу AzCopy hello</span><span class="sxs-lookup"><span data-stu-id="49102-255">Transfer data with hello AzCopy command-line utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

<span data-ttu-id="49102-256">[Веб-приложение node.js с помощью hello службы таблиц Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span><span class="sxs-lookup"><span data-stu-id="49102-256">[Node.js web app using hello Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span></span>  
<span data-ttu-id="49102-257">[Сборка и развертывание приложения tooAzure web Node.js, с помощью Web Matrix]: https://www.microsoft.com/web/webmatrix/</span><span class="sxs-lookup"><span data-stu-id="49102-257">[Build and deploy a Node.js web app tooAzure using Web Matrix]: https://www.microsoft.com/web/webmatrix/</span></span>  
<span data-ttu-id="49102-258">[REST API с помощью hello]: http://msdn.microsoft.com/library/azure/hh264518.aspx [Azure портал]: https://portal.azure.com [построения и развертывания tooan приложений Node.js облачной службы Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [блоге разработчиков хранилища Azure]: http:// blogs.MSDN.com/b/windowsazurestorage/ [хранилища Azure SDK для Справочник по API узел]: http://dl.windowsazure.com/nodestoragedocs/index.html</span><span class="sxs-lookup"><span data-stu-id="49102-258">[Using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx [Azure portal]: https://portal.azure.com [Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/ [Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html</span></span>
