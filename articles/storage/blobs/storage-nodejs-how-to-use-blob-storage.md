---
title: "Как использовать хранилище BLOB-объектов из Node.js | Документация Майкрософт"
description: "Хранение неструктурированных данных в облаке в хранилище BLOB-объектов Azure."
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
ms.openlocfilehash: e83ad647f6b7c70f34ef0c69b5bf322da5b6d60d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-nodejs"></a><span data-ttu-id="fa62c-103">Использование хранилища больших двоичных объектов из Node.js</span><span class="sxs-lookup"><span data-stu-id="fa62c-103">How to use Blob storage from Node.js</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="fa62c-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="fa62c-104">Overview</span></span>
<span data-ttu-id="fa62c-105">В этой статье описано, как реализовать типичные сценарии с использованием хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="fa62c-105">This article shows you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="fa62c-106">Примеры написаны с использованием интерфейса API Node.js.</span><span class="sxs-lookup"><span data-stu-id="fa62c-106">The samples are written via the Node.js API.</span></span> <span data-ttu-id="fa62c-107">Рассмотренные сценарии включают загрузку, получение списка, загрузку и удаление больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="fa62c-107">The scenarios covered include how to upload, list, download, and delete blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="fa62c-108">Создание приложения Node.js</span><span class="sxs-lookup"><span data-stu-id="fa62c-108">Create a Node.js application</span></span>
<span data-ttu-id="fa62c-109">Инструкции по созданию приложения Node.js см. в статьях [Создание веб-приложения Node.js в службе приложений Azure], [Сборка и развертывание приложения Node.js в облачной службе Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (с помощью Windows PowerShell) и [Создание и развертывание веб-приложения Node.js в Azure с использованием WebMatrix](https://www.microsoft.com/web/webmatrix/).</span><span class="sxs-lookup"><span data-stu-id="fa62c-109">For instructions on how to create a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application to an Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) -- using Windows PowerShell, or [Build and deploy a Node.js web app to Azure using Web Matrix](https://www.microsoft.com/web/webmatrix/).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="fa62c-110">Настройка приложения для доступа к хранилищу</span><span class="sxs-lookup"><span data-stu-id="fa62c-110">Configure your application to access storage</span></span>
<span data-ttu-id="fa62c-111">Для использования службы хранилища Azure необходим пакет SDK для службы хранилища Azure для Node.js, который содержит набор удобных библиотек, взаимодействующих со службами REST хранилища.</span><span class="sxs-lookup"><span data-stu-id="fa62c-111">To use Azure storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="fa62c-112">Использование диспетчера пакета Node (NPM) для получения пакета</span><span class="sxs-lookup"><span data-stu-id="fa62c-112">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="fa62c-113">В интерфейсе командной строки, например в **PowerShell** (Windows), **Terminal** (Mac) или **Bash** (Unix), перейдите в папку, в которой вы создали приложение.</span><span class="sxs-lookup"><span data-stu-id="fa62c-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), to navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="fa62c-114">Введите в командной строке **npm install azure-storage** .</span><span class="sxs-lookup"><span data-stu-id="fa62c-114">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="fa62c-115">Результат выполнения этой команды будет аналогичен следующему примеру кода:</span><span class="sxs-lookup"><span data-stu-id="fa62c-115">Output from the command is similar to the following code example.</span></span>

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
3. <span data-ttu-id="fa62c-116">Выполнив команду **ls** вручную, можно убедиться, что папка **node\_modules** создана.</span><span class="sxs-lookup"><span data-stu-id="fa62c-116">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="fa62c-117">В этом каталоге найдите пакет **azure-storage** , который содержит библиотеки, необходимые для доступа к хранилищу.</span><span class="sxs-lookup"><span data-stu-id="fa62c-117">Inside that folder, find the **azure-storage** package, which contains the libraries that you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="fa62c-118">Импорт пакета</span><span class="sxs-lookup"><span data-stu-id="fa62c-118">Import the package</span></span>
<span data-ttu-id="fa62c-119">С помощью Блокнота или другого текстового редактора добавьте следующий код в начало файла **server.js** приложения, в котором планируется использовать хранилище.</span><span class="sxs-lookup"><span data-stu-id="fa62c-119">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application where you intend to use storage:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="fa62c-120">Настройка подключения к службе хранилища Azure</span><span class="sxs-lookup"><span data-stu-id="fa62c-120">Set up an Azure Storage connection</span></span>
<span data-ttu-id="fa62c-121">Модуль Azure считает переменные среды `AZURE_STORAGE_ACCOUNT` и `AZURE_STORAGE_ACCESS_KEY` или `AZURE_STORAGE_CONNECTION_STRING` для получения сведений, необходимых для подключения к учетной записи хранения Azure.</span><span class="sxs-lookup"><span data-stu-id="fa62c-121">The Azure module will read the environment variables `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY`, or `AZURE_STORAGE_CONNECTION_STRING`, for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="fa62c-122">Если эти переменные среды не заданы, при вызове **createBlobService**необходимо указать данные учетной записи.</span><span class="sxs-lookup"><span data-stu-id="fa62c-122">If these environment variables are not set, you must specify the account information when calling **createBlobService**.</span></span>

<span data-ttu-id="fa62c-123">Пример настройки переменных среды для веб-приложения Azure на [портале Azure](https://portal.azure.com) см. в статье [Веб-приложение Node.js, использующее службу таблиц Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="fa62c-123">For an example of setting the environment variables in the [Azure portal](https://portal.azure.com) for an Azure web app, see [Node.js web app using the Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-container"></a><span data-ttu-id="fa62c-124">Создание контейнера</span><span class="sxs-lookup"><span data-stu-id="fa62c-124">Create a container</span></span>
<span data-ttu-id="fa62c-125">Объект **BlobService** позволяет работать с контейнерами и большими двоичными объектами.</span><span class="sxs-lookup"><span data-stu-id="fa62c-125">The **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="fa62c-126">Указанный ниже код создает объект **BlobService** .</span><span class="sxs-lookup"><span data-stu-id="fa62c-126">The following code creates a **BlobService** object.</span></span> <span data-ttu-id="fa62c-127">Добавьте следующий код в начало файла **server.js**:</span><span class="sxs-lookup"><span data-stu-id="fa62c-127">Add the following near the top of **server.js**:</span></span>

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> <span data-ttu-id="fa62c-128">Для анонимного доступа к большому двоичному объекту воспользуйтесь **createBlobServiceAnonymous** и укажите адрес узла.</span><span class="sxs-lookup"><span data-stu-id="fa62c-128">You can access a blob anonymously by using **createBlobServiceAnonymous** and providing the host address.</span></span> <span data-ttu-id="fa62c-129">Например, воспользуйтесь `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span><span class="sxs-lookup"><span data-stu-id="fa62c-129">For example, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="fa62c-130">Чтобы создать новый контейнер, используйте **createContainerIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="fa62c-130">To create a new container, use **createContainerIfNotExists**.</span></span> <span data-ttu-id="fa62c-131">Код в следующем примере создает новый контейнер с именем mycontainer.</span><span class="sxs-lookup"><span data-stu-id="fa62c-131">The following code example creates a new container named 'mycontainer':</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

<span data-ttu-id="fa62c-132">Если контейнер только что создан, `result.created` имеет значение true.</span><span class="sxs-lookup"><span data-stu-id="fa62c-132">If the container is newly created, `result.created` is true.</span></span> <span data-ttu-id="fa62c-133">Если контейнер уже существует, `result.created` будет иметь значение false.</span><span class="sxs-lookup"><span data-stu-id="fa62c-133">If the container already exists, `result.created` is false.</span></span> <span data-ttu-id="fa62c-134">`response` будет содержать сведения об операции, включая сведения ETag для контейнера.</span><span class="sxs-lookup"><span data-stu-id="fa62c-134">`response` contains information about the operation, including the ETag information for the container.</span></span>

### <a name="container-security"></a><span data-ttu-id="fa62c-135">Безопасность контейнера</span><span class="sxs-lookup"><span data-stu-id="fa62c-135">Container security</span></span>
<span data-ttu-id="fa62c-136">По умолчанию все контейнеры частные, и доступ к ним не может быть анонимным.</span><span class="sxs-lookup"><span data-stu-id="fa62c-136">By default, new containers are private and cannot be accessed anonymously.</span></span> <span data-ttu-id="fa62c-137">Чтобы сделать контейнер общедоступным (чтобы к нему можно было подключаться анонимно), установите для уровня доступа к контейнеру значение **blob** или **container**.</span><span class="sxs-lookup"><span data-stu-id="fa62c-137">To make the container public so that you can access it anonymously, you can set the container's access level to **blob** or **container**.</span></span>

* <span data-ttu-id="fa62c-138">**blob** можно осуществлять анонимный доступ для чтения к содержимому и метаданным больших двоичных объектов внутри этого контейнера, но не к метаданным контейнера, например для перечисления всех больших двоичных объектов в контейнере.</span><span class="sxs-lookup"><span data-stu-id="fa62c-138">**blob** - allows anonymous read access to blob content and metadata within this container, but not to container metadata such as listing all blobs within a container</span></span>
* <span data-ttu-id="fa62c-139">**container** разрешается анонимный доступ на чтение содержимого и метаданных больших двоичных объектов, а также метаданных контейнера.</span><span class="sxs-lookup"><span data-stu-id="fa62c-139">**container** - allows anonymous read access to blob content and metadata as well as container metadata</span></span>

<span data-ttu-id="fa62c-140">В следующем примере кода показана установка уровня доступа **blob**:</span><span class="sxs-lookup"><span data-stu-id="fa62c-140">The following code example demonstrates setting the access level to **blob**:</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access to blob
      // content and metadata within this container
    }
});
```

<span data-ttu-id="fa62c-141">Кроме того, можно изменить уровень доступа к контейнеру, используя метод **setContainerAcl** для указания уровня доступа.</span><span class="sxs-lookup"><span data-stu-id="fa62c-141">Alternatively, you can modify the access level of a container by using **setContainerAcl** to specify the access level.</span></span> <span data-ttu-id="fa62c-142">В следующем примере кода уровень доступа изменяется на "container":</span><span class="sxs-lookup"><span data-stu-id="fa62c-142">The following code example changes the access level to container:</span></span>

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set to 'container'
  }
});
```

<span data-ttu-id="fa62c-143">Результат содержит сведения об операции, включая текущий **ETag** для контейнера.</span><span class="sxs-lookup"><span data-stu-id="fa62c-143">The result contains information about the operation, including the current **ETag** for the container.</span></span>

### <a name="filters"></a><span data-ttu-id="fa62c-144">Фильтры</span><span class="sxs-lookup"><span data-stu-id="fa62c-144">Filters</span></span>
<span data-ttu-id="fa62c-145">С помощью **BlobService** к выполняемым операциям можно применить дополнительную фильтрацию.</span><span class="sxs-lookup"><span data-stu-id="fa62c-145">You can apply optional filtering operations to operations performed using **BlobService**.</span></span> <span data-ttu-id="fa62c-146">К операциям фильтрации могут относиться ведение журнала, автоматический повтор и т. д. Фильтры являются объектами, реализующими метод со следующей сигнатурой:</span><span class="sxs-lookup"><span data-stu-id="fa62c-146">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="fa62c-147">Выполнив предварительную обработку параметров запроса, метод должен вызвать next, передав ему обратный вызов со следующей сигнатурой:</span><span class="sxs-lookup"><span data-stu-id="fa62c-147">After doing its preprocessing on the request options, the method needs to call "next", passing a callback with the following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="fa62c-148">В этой функции обратного вызова и после обработки returnObject (ответ на запрос к серверу) функция обратного вызова должна либо вызвать "next", если он существует, чтобы продолжить обработку других фильтров, либо в противном случае просто вызвать "finalCallback" для завершения обращения к службе.</span><span class="sxs-lookup"><span data-stu-id="fa62c-148">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback to end the service invocation.</span></span>

<span data-ttu-id="fa62c-149">В пакет SDK Azure для Node.js включены два фильтра, реализующие логику повторных попыток: **ExponentialRetryPolicyFilter** и **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="fa62c-149">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="fa62c-150">Следующий код создает объект **BlobService**, использующий фильтр **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="fa62c-150">The following creates a **BlobService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="fa62c-151">Отправка BLOB-объекта в контейнер</span><span class="sxs-lookup"><span data-stu-id="fa62c-151">Upload a blob into a container</span></span>
<span data-ttu-id="fa62c-152">Существует три типа больших двоичных объектов: блочные, страничные и добавочные.</span><span class="sxs-lookup"><span data-stu-id="fa62c-152">There are three types of blobs: block blobs, page blobs and append blobs.</span></span> <span data-ttu-id="fa62c-153">Блочные BLOB-объекты позволяют более эффективно отправлять данные большого размера.</span><span class="sxs-lookup"><span data-stu-id="fa62c-153">Block blobs allow you to more efficiently upload large data.</span></span> <span data-ttu-id="fa62c-154">Добавочные BLOB-объекты оптимизированы для операций добавления.</span><span class="sxs-lookup"><span data-stu-id="fa62c-154">Append blobs are optimized for append operations.</span></span> <span data-ttu-id="fa62c-155">Страничные BLOB-объекты оптимизированы для операций чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="fa62c-155">Page blobs are optimized for read/write operations.</span></span> <span data-ttu-id="fa62c-156">Дополнительные сведения см. в статье [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx) (Основные сведения о блочных, добавочных и страничных BLOB-объектах).</span><span class="sxs-lookup"><span data-stu-id="fa62c-156">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

### <a name="block-blobs"></a><span data-ttu-id="fa62c-157">Blob-блоки</span><span class="sxs-lookup"><span data-stu-id="fa62c-157">Block blobs</span></span>
<span data-ttu-id="fa62c-158">Чтобы загрузить данные в blob-блок, используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="fa62c-158">To upload data to a block blob, use the following:</span></span>

* <span data-ttu-id="fa62c-159">**createBlockBlobFromLocalFile** — создает новый blob-блок и отправляет содержимое файла;</span><span class="sxs-lookup"><span data-stu-id="fa62c-159">**createBlockBlobFromLocalFile** - creates a new block blob and uploads the contents of a file</span></span>
* <span data-ttu-id="fa62c-160">**createBlockBlobFromStream** — создает новый блочный BLOB-объект и загружает содержимое потока</span><span class="sxs-lookup"><span data-stu-id="fa62c-160">**createBlockBlobFromStream** - creates a new block blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="fa62c-161">**createBlockBlobFromText** — создает новый блочный BLOB-объект и загружает содержимое строки</span><span class="sxs-lookup"><span data-stu-id="fa62c-161">**createBlockBlobFromText** - creates a new block blob and uploads the contents of a string</span></span>
* <span data-ttu-id="fa62c-162">**createWriteStreamToBlockBlob** — предоставляет поток записи в блочный BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="fa62c-162">**createWriteStreamToBlockBlob** - provides a write stream to a block blob</span></span>

<span data-ttu-id="fa62c-163">В следующем примере кода содержимое файла **test.txt** передается в **myblob**.</span><span class="sxs-lookup"><span data-stu-id="fa62c-163">The following code example uploads the contents of the **test.txt** file into **myblob**.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="fa62c-164">Возвращаемое этими методами `result` содержит сведения об операции, такие как **ETag** большого двоичного объекта.</span><span class="sxs-lookup"><span data-stu-id="fa62c-164">The `result` returned by these methods contains information on the operation, such as the **ETag** of the blob.</span></span>

### <a name="append-blobs"></a><span data-ttu-id="fa62c-165">Добавочные BLOB-объекты</span><span class="sxs-lookup"><span data-stu-id="fa62c-165">Append blobs</span></span>
<span data-ttu-id="fa62c-166">Для отправки данных в новый добавочный BLOB-объект используйте указанные далее команды.</span><span class="sxs-lookup"><span data-stu-id="fa62c-166">To upload data to a new append blob, use the following:</span></span>

* <span data-ttu-id="fa62c-167">**createAppendBlobFromLocalFile** — создает добавочный BLOB-объект и передает содержимое файла.</span><span class="sxs-lookup"><span data-stu-id="fa62c-167">**createAppendBlobFromLocalFile** - creates a new append blob and uploads the contents of a file</span></span>
* <span data-ttu-id="fa62c-168">**createAppendBlobFromText** — создает добавочный BLOB-объект и передает содержимое потока.</span><span class="sxs-lookup"><span data-stu-id="fa62c-168">**createAppendBlobFromStream** - creates a new append blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="fa62c-169">**createAppendBlobFromStream** — создает добавочный BLOB-объект и передает содержимое строки.</span><span class="sxs-lookup"><span data-stu-id="fa62c-169">**createAppendBlobFromText** - creates a new append blob and uploads the contents of a string</span></span>
* <span data-ttu-id="fa62c-170">**createWriteStreamToNewAppendBlob** — создает добавочный BLOB-объект, а затем предоставляет поток для записи в него.</span><span class="sxs-lookup"><span data-stu-id="fa62c-170">**createWriteStreamToNewAppendBlob** - creates a new append blob and then provides a stream to write to it</span></span>

<span data-ttu-id="fa62c-171">В следующем примере кода содержимое файла **test.txt** передается в **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="fa62c-171">The following code example uploads the contents of the **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="fa62c-172">Чтобы добавить блок в существующий добавочный BLOB-объект, используйте указанные далее команды:</span><span class="sxs-lookup"><span data-stu-id="fa62c-172">To append a block to an existing append blob, use the following:</span></span>

* <span data-ttu-id="fa62c-173">**appendFromLocalFile** — добавляет содержимое файла в существующий добавочный BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="fa62c-173">**appendFromLocalFile** - append the contents of a file to an existing append blob</span></span>
* <span data-ttu-id="fa62c-174">**appendFromStream** — добавляет содержимое потока в существующий добавочный BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="fa62c-174">**appendFromStream** - append the contents of a stream to an existing append blob</span></span>
* <span data-ttu-id="fa62c-175">**appendFromText** — добавляет содержимое строки в существующий добавочный BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="fa62c-175">**appendFromText** - append the contents of a string to an existing append blob</span></span>
* <span data-ttu-id="fa62c-176">**appendBlockFromStream** — добавляет содержимое потока в существующий добавочный BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="fa62c-176">**appendBlockFromStream** - append the contents of a stream to an existing append blob</span></span>
* <span data-ttu-id="fa62c-177">**appendBlockFromText** — добавляет содержимое строки в существующий добавочный BLOB-объект.</span><span class="sxs-lookup"><span data-stu-id="fa62c-177">**appendBlockFromText** - append the contents of a string to an existing append blob</span></span>

> [!NOTE]
> <span data-ttu-id="fa62c-178">Чтобы исключить ненужные вызовы сервера, интерфейсы API appendFromXXX будут выполнять проверку на стороне клиента с быстрым прекращением.</span><span class="sxs-lookup"><span data-stu-id="fa62c-178">appendFromXXX APIs will do some client-side validation to fail fast to avoid unnecessary server calls.</span></span> <span data-ttu-id="fa62c-179">appendBlockFromXXX не будут делать этого.</span><span class="sxs-lookup"><span data-stu-id="fa62c-179">appendBlockFromXXX won't.</span></span>
>
>

<span data-ttu-id="fa62c-180">В следующем примере кода содержимое файла **test.txt** передается в **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="fa62c-180">The following code example uploads the contents of the **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text to be appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a><span data-ttu-id="fa62c-181">Blob-страницы</span><span class="sxs-lookup"><span data-stu-id="fa62c-181">Page blobs</span></span>
<span data-ttu-id="fa62c-182">Чтобы загрузить данные в blob-страницу, используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="fa62c-182">To upload data to a page blob, use the following:</span></span>

* <span data-ttu-id="fa62c-183">**createPageBlob** — создает новый страничный BLOB-объект заданной длины.</span><span class="sxs-lookup"><span data-stu-id="fa62c-183">**createPageBlob** - creates a new page blob of a specific length</span></span>
* <span data-ttu-id="fa62c-184">**createPageBlobFromLocalFile** — создает новый страничный BLOB-объект и загружает содержимое файла.</span><span class="sxs-lookup"><span data-stu-id="fa62c-184">**createPageBlobFromLocalFile** - creates a new page blob and uploads the contents of a file</span></span>
* <span data-ttu-id="fa62c-185">**createPageBlobFromStream** — создает новый страничный BLOB-объект и загружает содержимое потока</span><span class="sxs-lookup"><span data-stu-id="fa62c-185">**createPageBlobFromStream** - creates a new page blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="fa62c-186">**createWriteStreamToExistingPageBlob** -предоставляет поток записи существующий страничный BLOB-объект</span><span class="sxs-lookup"><span data-stu-id="fa62c-186">**createWriteStreamToExistingPageBlob** - provides a write stream to an existing page blob</span></span>
* <span data-ttu-id="fa62c-187">**createWriteStreamToNewPageBlob** — создает страничный BLOB-объект, а затем предоставляет поток для записи в него.</span><span class="sxs-lookup"><span data-stu-id="fa62c-187">**createWriteStreamToNewPageBlob** - creates a new page blob and then provides a stream to write to it</span></span>

<span data-ttu-id="fa62c-188">В следующем примере кода содержимое файла **test.txt** передается в **mypageblob**.</span><span class="sxs-lookup"><span data-stu-id="fa62c-188">The following code example uploads the contents of the **test.txt** file into **mypageblob**.</span></span>

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> <span data-ttu-id="fa62c-189">Страничные Вlob-объекты состоят из 512-байтовых "страниц".</span><span class="sxs-lookup"><span data-stu-id="fa62c-189">Page blobs consist of 512-byte 'pages'.</span></span> <span data-ttu-id="fa62c-190">При отправке файлов с размером, не кратным 512, может возникать ошибка.</span><span class="sxs-lookup"><span data-stu-id="fa62c-190">You will receive an error when uploading data with a size that is not a multiple of 512.</span></span>
>
>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="fa62c-191">Перечисление BLOB-объектов в контейнере</span><span class="sxs-lookup"><span data-stu-id="fa62c-191">List the blobs in a container</span></span>
<span data-ttu-id="fa62c-192">Чтобы перечислить blob-объекты в контейнере, используйте метод **listBlobsSegmented** .</span><span class="sxs-lookup"><span data-stu-id="fa62c-192">To list the blobs in a container, use the **listBlobsSegmented** method.</span></span> <span data-ttu-id="fa62c-193">Если вы хотите возвращать большие двоичные объекты с заданном префиксом, используйте **listBlobsSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="fa62c-193">If you'd like to return blobs with a specific prefix, use **listBlobsSegmentedWithPrefix**.</span></span>

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains the entries
      // If not all blobs were returned, result.continuationToken has the continuation token.
  }
});
```

<span data-ttu-id="fa62c-194">`result` содержит коллекцию `entries`, которая представляет собой массив объектов, описывающих каждый из больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="fa62c-194">The `result` contains an `entries` collection, which is an array of objects that describe each blob.</span></span> <span data-ttu-id="fa62c-195">Если все большие двоичные объекты возвратить нельзя, `result` также предоставляет `continuationToken`, который можно использовать в качестве второго параметра для извлечения дополнительных записей.</span><span class="sxs-lookup"><span data-stu-id="fa62c-195">If all blobs cannot be returned, the `result` also provides a `continuationToken`, which you may use as the second parameter to retrieve additional entries.</span></span>

## <a name="download-blobs"></a><span data-ttu-id="fa62c-196">Скачивание больших двоичных объектов</span><span class="sxs-lookup"><span data-stu-id="fa62c-196">Download blobs</span></span>
<span data-ttu-id="fa62c-197">Чтобы загрузить данные из BLOB-объекта, используйте следующие команды:</span><span class="sxs-lookup"><span data-stu-id="fa62c-197">To download data from a blob, use the following:</span></span>

* <span data-ttu-id="fa62c-198">**getBlobToLocalFile** — записывает содержимое большого двоичного объекта в файл.</span><span class="sxs-lookup"><span data-stu-id="fa62c-198">**getBlobToLocalFile** - writes the blob contents to file</span></span>
* <span data-ttu-id="fa62c-199">**getBlobToStream** — записывает содержимое большого двоичного объекта в поток</span><span class="sxs-lookup"><span data-stu-id="fa62c-199">**getBlobToStream** - writes the blob contents to a stream</span></span>
* <span data-ttu-id="fa62c-200">**getBlobToText** — записывает содержимое большого двоичного объекта в строку.</span><span class="sxs-lookup"><span data-stu-id="fa62c-200">**getBlobToText** - writes the blob contents to a string</span></span>
* <span data-ttu-id="fa62c-201">**createReadStream** - обеспечивает поток для чтения из blob-объекта</span><span class="sxs-lookup"><span data-stu-id="fa62c-201">**createReadStream** - provides a stream to read from the blob</span></span>

<span data-ttu-id="fa62c-202">В следующем примере кода **getBlobToStream** используется для скачивания содержимого большого двоичного объекта **myblob** и его сохранения в файле **output.txt** с помощью потока.</span><span class="sxs-lookup"><span data-stu-id="fa62c-202">The following code example demonstrates using **getBlobToStream** to download the contents of the **myblob** blob and store it to the **output.txt** file by using a stream:</span></span>

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

<span data-ttu-id="fa62c-203">`result` содержит сведения о большом двоичном объекте, включая сведения **ETag** .</span><span class="sxs-lookup"><span data-stu-id="fa62c-203">The `result` contains information about the blob, including **ETag** information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="fa62c-204">Удаление большого двоичного объекта</span><span class="sxs-lookup"><span data-stu-id="fa62c-204">Delete a blob</span></span>
<span data-ttu-id="fa62c-205">Наконец, чтобы удалить BLOB-объект, вызовите **deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="fa62c-205">Finally, to delete a blob, call **deleteBlob**.</span></span> <span data-ttu-id="fa62c-206">Следующий пример кода удаляет большой двоичный объект с именем **myblob**.</span><span class="sxs-lookup"><span data-stu-id="fa62c-206">The following code example deletes the blob named **myblob**.</span></span>

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a><span data-ttu-id="fa62c-207">Одновременный доступ</span><span class="sxs-lookup"><span data-stu-id="fa62c-207">Concurrent access</span></span>
<span data-ttu-id="fa62c-208">Чтобы реализовать одновременный доступ нескольких клиентов или экземпляров процесса к BLOB-объекту, можно использовать **ETags** или **lease**.</span><span class="sxs-lookup"><span data-stu-id="fa62c-208">To support concurrent access to a blob from multiple clients or multiple process instances, you can use **ETags** or **leases**.</span></span>

* <span data-ttu-id="fa62c-209">**Etag** — позволяет обнаружить, что BLOB-объект или контейнер были изменены другим процессом</span><span class="sxs-lookup"><span data-stu-id="fa62c-209">**Etag** - provides a way to detect that the blob or container has been modified by another process</span></span>
* <span data-ttu-id="fa62c-210">**Lease** — аренда позволяет получить монопольный обновляемый доступ к BLOB-объекту на запись или удаление в течение заданного периода времени.</span><span class="sxs-lookup"><span data-stu-id="fa62c-210">**Lease** - provides a way to obtain exclusive, renewable, write or delete access to a blob for a period of time</span></span>

### <a name="etag"></a><span data-ttu-id="fa62c-211">ETag</span><span class="sxs-lookup"><span data-stu-id="fa62c-211">ETag</span></span>
<span data-ttu-id="fa62c-212">ETag необходимо использовать, если нужно обеспечить возможность записи в блочный BLOB-объект или страничный BLOB-объект одновременно для нескольких клиентов или экземпляров.</span><span class="sxs-lookup"><span data-stu-id="fa62c-212">Use ETags if you need to allow multiple clients or instances to write to the block Blob or page Blob simultaneously.</span></span> <span data-ttu-id="fa62c-213">ETag позволяет определить, были ли контейнер или BLOB-объект изменены с момента изначального чтения или создания. Это позволяет избежать перезаписи изменений, выполненных другим клиентом или процессом.</span><span class="sxs-lookup"><span data-stu-id="fa62c-213">The ETag allows you to determine if the container or blob was modified since you initially read or created it, which allows you to avoid overwriting changes committed by another client or process.</span></span>

<span data-ttu-id="fa62c-214">Условия ETag можно задать с помощью необязательного параметра `options.accessConditions` .</span><span class="sxs-lookup"><span data-stu-id="fa62c-214">You can set ETag conditions by using the optional `options.accessConditions` parameter.</span></span> <span data-ttu-id="fa62c-215">В следующем примере кода текстовый файл **test.txt** передается только в том случае, если большой двоичный объект уже существует, а значение ETag для него соответствует содержащемуся в `etagToMatch`.</span><span class="sxs-lookup"><span data-stu-id="fa62c-215">The following code example only uploads the **test.txt** file if the blob already exists and has the ETag value contained by `etagToMatch`.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="fa62c-216">Общая схема действий при использовании Etag такова:</span><span class="sxs-lookup"><span data-stu-id="fa62c-216">When you're using ETags, the general pattern is:</span></span>

1. <span data-ttu-id="fa62c-217">Получить ETag в результате операции создания перечисления или получения</span><span class="sxs-lookup"><span data-stu-id="fa62c-217">Obtain the ETag as the result of a create, list, or get operation.</span></span>
2. <span data-ttu-id="fa62c-218">Выполнить действие по проверке отсутствия изменений в значении ETag.</span><span class="sxs-lookup"><span data-stu-id="fa62c-218">Perform an action, checking that the ETag value has not been modified.</span></span>

<span data-ttu-id="fa62c-219">Если значение было изменено, это означает, что другой клиент или экземпляр изменил BLOB-объект или контейнер с момента получения значения ETag.</span><span class="sxs-lookup"><span data-stu-id="fa62c-219">If the value was modified, this indicates that another client or instance modified the blob or container since you obtained the ETag value.</span></span>

### <a name="lease"></a><span data-ttu-id="fa62c-220">Lease</span><span class="sxs-lookup"><span data-stu-id="fa62c-220">Lease</span></span>
<span data-ttu-id="fa62c-221">Для приобретения новой аренды можно воспользоваться методом **acquireLease** , указав большой двоичный объект или контейнер, для которого вы хотите получить аренду.</span><span class="sxs-lookup"><span data-stu-id="fa62c-221">You can acquire a new lease by using the **acquireLease** method, specifying the blob or container that you wish to obtain a lease on.</span></span> <span data-ttu-id="fa62c-222">Например, следующий код получает аренду для **myblob**.</span><span class="sxs-lookup"><span data-stu-id="fa62c-222">For example, the following code acquires a lease on **myblob**.</span></span>

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

<span data-ttu-id="fa62c-223">В последующих операциях с **myblob** необходимо указывать параметр `options.leaseId`.</span><span class="sxs-lookup"><span data-stu-id="fa62c-223">Subsequent operations on **myblob** must provide the `options.leaseId` parameter.</span></span> <span data-ttu-id="fa62c-224">Идентификатор аренды возвращается методом **acquireLease** в виде `result.id`.</span><span class="sxs-lookup"><span data-stu-id="fa62c-224">The lease ID is returned as `result.id` from **acquireLease**.</span></span>

> [!NOTE]
> <span data-ttu-id="fa62c-225">По умолчанию продолжительность аренды бесконечна.</span><span class="sxs-lookup"><span data-stu-id="fa62c-225">By default, the lease duration is infinite.</span></span> <span data-ttu-id="fa62c-226">В параметре `options.leaseDuration` можно указать конечную продолжительность аренды (от 15 до 60 секунд).</span><span class="sxs-lookup"><span data-stu-id="fa62c-226">You can specify a non-infinite duration (between 15 and 60 seconds) by providing the `options.leaseDuration` parameter.</span></span>
>
>

<span data-ttu-id="fa62c-227">Чтобы удалить аренду, используйте **releaseLease**.</span><span class="sxs-lookup"><span data-stu-id="fa62c-227">To remove a lease, use **releaseLease**.</span></span> <span data-ttu-id="fa62c-228">Чтобы приостановить аренду, но не дать другим возможность получить новую аренду до истечения срока действия первоначальной аренды, используйте **breakLease**.</span><span class="sxs-lookup"><span data-stu-id="fa62c-228">To break a lease, but prevent others from obtaining a new lease until the original duration has expired, use **breakLease**.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="fa62c-229">Работа с подписями общего доступа</span><span class="sxs-lookup"><span data-stu-id="fa62c-229">Work with shared access signatures</span></span>
<span data-ttu-id="fa62c-230">Подписанный URL-адрес (SAS) — безопасный способ предоставить детализированный доступ к большим двоичным объектам и контейнерам без указания имени или ключей своей учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="fa62c-230">Shared access signatures (SAS) are a secure way to provide granular access to blobs and containers without providing your storage account name or keys.</span></span> <span data-ttu-id="fa62c-231">Подписанные URL-адреса часто используются для предоставления ограниченного доступа к данным, например доступа к BLOB-объектам для мобильного приложения.</span><span class="sxs-lookup"><span data-stu-id="fa62c-231">Shared access signatures are often used to provide limited access to your data, such as allowing a mobile app to access blobs.</span></span>

> [!NOTE]
> <span data-ttu-id="fa62c-232">Несмотря на то что анонимный доступ к большим двоичным объектам также возможен, подписанный URL-адрес позволяет более точно управлять доступом, так как этот адрес нужно создать.</span><span class="sxs-lookup"><span data-stu-id="fa62c-232">While you can also allow anonymous access to blobs, shared access signatures allow you to provide more controlled access, as you must generate the SAS.</span></span>
>
>

<span data-ttu-id="fa62c-233">Надежное приложение, например облачная служба, создает подписанный URL-адрес с помощью метода **generateSharedAccessSignature** из **BlobService** и передает этот адрес ненадежному или частично надежному приложению, например мобильному приложению.</span><span class="sxs-lookup"><span data-stu-id="fa62c-233">A trusted application such as a cloud-based service generates shared access signatures using the **generateSharedAccessSignature** of the **BlobService**, and provides it to an untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="fa62c-234">Подписанный URL-адрес создается с использованием политики, которая описывает даты начала и окончания срока действия адреса, а также уровень доступа, который предоставляется держателю адреса.</span><span class="sxs-lookup"><span data-stu-id="fa62c-234">Shared access signatures are generated using a policy, which describes the start and end dates during which the shared access signatures are valid, as well as the access level granted to the shared access signatures holder.</span></span>

<span data-ttu-id="fa62c-235">В следующем примере кода создается новая политика общего доступа, которая позволяет держателю подписанного URL-адреса выполнять операции чтения BLOB-объекта **myblob** в течение 100 минут с момента создания политики.</span><span class="sxs-lookup"><span data-stu-id="fa62c-235">The following code example generates a new shared access policy that allows the shared access signatures holder to perform read operations on the **myblob** blob, and expires 100 minutes after the time it is created.</span></span>

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

<span data-ttu-id="fa62c-236">Обратите внимание, что также необходимо предоставить информацию об узле, так как она требуется держателю SAS для доступа к контейнеру.</span><span class="sxs-lookup"><span data-stu-id="fa62c-236">Note that the host information must be provided also, as it is required when the shared access signatures holder attempts to access the container.</span></span>

<span data-ttu-id="fa62c-237">Затем клиентское приложение выполняет операции с BLOB-объектом, используя метод **BlobServiceWithSAS** с подписанным URL-адресом.</span><span class="sxs-lookup"><span data-stu-id="fa62c-237">The client application then uses shared access signatures with **BlobServiceWithSAS** to perform operations against the blob.</span></span> <span data-ttu-id="fa62c-238">Следующая команда позволяет получить информацию о **myblob**.</span><span class="sxs-lookup"><span data-stu-id="fa62c-238">The following gets information about **myblob**.</span></span>

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

<span data-ttu-id="fa62c-239">Так как подписанные URL-адреса были созданы только для доступа на чтение, при попытке изменения BLOB-объекта будет возвращена ошибка.</span><span class="sxs-lookup"><span data-stu-id="fa62c-239">Since the shared access signatures were generated with read-only access, if an attempt is made to modify the blob, an error will be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="fa62c-240">Доступ к спискам управления</span><span class="sxs-lookup"><span data-stu-id="fa62c-240">Access control lists</span></span>
<span data-ttu-id="fa62c-241">Для задания политики доступа для SAS также можно использовать список управления доступом (ACL).</span><span class="sxs-lookup"><span data-stu-id="fa62c-241">You can also use an access control list (ACL) to set the access policy for SAS.</span></span> <span data-ttu-id="fa62c-242">Это может быть удобно, когда необходимо предоставить доступ к контейнеру нескольким клиентам с различной политикой доступа для каждого из них.</span><span class="sxs-lookup"><span data-stu-id="fa62c-242">This is useful if you wish to allow multiple clients to access a container but provide different access policies for each client.</span></span>

<span data-ttu-id="fa62c-243">ACL реализуется с помощью массива политик доступа, каждая из которых связана со своим идентификатором.</span><span class="sxs-lookup"><span data-stu-id="fa62c-243">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="fa62c-244">В следующем примере кода определяются две политики: одна для пользователя 'user1', вторая — для 'user2'.</span><span class="sxs-lookup"><span data-stu-id="fa62c-244">The following code example defines two policies, one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="fa62c-245">В следующем примере код получает текущий список управления доступом для **mycontainer**, а затем добавляет новые политики с помощью **setBlobAcl**.</span><span class="sxs-lookup"><span data-stu-id="fa62c-245">The following code example gets the current ACL for **mycontainer**, and then adds the new policies using **setBlobAcl**.</span></span> <span data-ttu-id="fa62c-246">Такой подход допускает выполнение:</span><span class="sxs-lookup"><span data-stu-id="fa62c-246">This approach allows:</span></span>

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

<span data-ttu-id="fa62c-247">После задания списка управления доступом можно создать подписанный URL-адрес на основе идентификатора политики.</span><span class="sxs-lookup"><span data-stu-id="fa62c-247">Once the ACL is set, you can then create shared access signatures based on the ID for a policy.</span></span> <span data-ttu-id="fa62c-248">В следующем примере кода создаются новые подписанные URL-адреса для пользователя user2:</span><span class="sxs-lookup"><span data-stu-id="fa62c-248">The following code example creates new shared access signatures for 'user2':</span></span>

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="fa62c-249">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fa62c-249">Next steps</span></span>
<span data-ttu-id="fa62c-250">Для получения дополнительных сведений см. следующие ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fa62c-250">For more information, see the following resources.</span></span>

* <span data-ttu-id="fa62c-251">[Справочник по пакету SDK службы хранилища Azure для API Node] [Azure Storage SDK for Node API Reference]</span><span class="sxs-lookup"><span data-stu-id="fa62c-251">[Azure Storage SDK for Node API Reference][Azure Storage SDK for Node API Reference]</span></span>
* <span data-ttu-id="fa62c-252">[Блог рабочей группы службы хранилища Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="fa62c-252">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>
* <span data-ttu-id="fa62c-253">Репозиторий [пакета SDK хранилища Azure для Node][Azure Storage SDK for Node] на веб-сайте GitHub.</span><span class="sxs-lookup"><span data-stu-id="fa62c-253">[Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="fa62c-254">Центр разработчиков Node.js.</span><span class="sxs-lookup"><span data-stu-id="fa62c-254">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)
* [<span data-ttu-id="fa62c-255">Приступая к работе со служебной программой командной строки AzCopy</span><span class="sxs-lookup"><span data-stu-id="fa62c-255">Transfer data with the AzCopy command-line utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

<span data-ttu-id="fa62c-256">[Веб-приложение Node.js, использующее службу таблиц Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span><span class="sxs-lookup"><span data-stu-id="fa62c-256">[Node.js web app using the Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span></span>  
<span data-ttu-id="fa62c-257">[Сборка и развертывание веб-приложения Node.js в Azure с помощью Web Matrix]: https://www.microsoft.com/web/webmatrix/</span><span class="sxs-lookup"><span data-stu-id="fa62c-257">[Build and deploy a Node.js web app to Azure using Web Matrix]: https://www.microsoft.com/web/webmatrix/</span></span>  
<span data-ttu-id="fa62c-258">[С помощью REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx [портал Azure]: https://portal.azure.com [Сборка и развертывание приложения Node.js в облачной службе Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Блог рабочей группы службы хранилища Azure]: http://blogs.msdn.com/b/windowsazurestorage/ [Справочник по пакету SDK службы хранилища Azure для API Node]: http://dl.windowsazure.com/nodestoragedocs/index.html</span><span class="sxs-lookup"><span data-stu-id="fa62c-258">[Using the REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx [Azure portal]: https://portal.azure.com [Build and deploy a Node.js application to an Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/ [Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html</span></span>
