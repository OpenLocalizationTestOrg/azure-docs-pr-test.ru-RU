---
title: "aaaGet работы с помощью пакета Azure SDK для Node.js хранилища Озера данных Azure | Документы Microsoft"
description: "Узнайте, как toouse toowork Node.js с учетными записями хранилища Озера данных и hello файловой системы."
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 2fee173c-69ae-4e1d-8773-48618cda9e16
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/06/2017
ms.author: nitinme
ms.openlocfilehash: ce36a2e0de4e091a4e85ed784a3381415ef6f9e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a><span data-ttu-id="9ca2c-103">Начало работы с Azure Data Lake Store с помощью пакета Azure SDK для Node.js</span><span class="sxs-lookup"><span data-stu-id="9ca2c-103">Get started with Azure Data Lake Store using Azure SDK for Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9ca2c-104">Портал</span><span class="sxs-lookup"><span data-stu-id="9ca2c-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="9ca2c-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9ca2c-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="9ca2c-106">Пакет SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="9ca2c-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="9ca2c-107">Пакет SDK для Java</span><span class="sxs-lookup"><span data-stu-id="9ca2c-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="9ca2c-108">REST API</span><span class="sxs-lookup"><span data-stu-id="9ca2c-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="9ca2c-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9ca2c-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="9ca2c-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="9ca2c-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="9ca2c-111">Python</span><span class="sxs-lookup"><span data-stu-id="9ca2c-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> <span data-ttu-id="9ca2c-112">Для загрузки и большого объема данных (больших файлов, большое количество файлов или оба), мы рекомендуем использовать hello [Python SDK](data-lake-store-get-started-python.md), hello [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), или [Azure PowerShell](data-lake-store-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9ca2c-112">For uploading and downloading large amount of data (large files, a large number of files, or both), we recommend that you use hello [Python SDK](data-lake-store-get-started-python.md), hello [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), or [Azure PowerShell](data-lake-store-get-started-powershell.md).</span></span> <span data-ttu-id="9ca2c-113">Эти параметры имеют более высокую производительность, как они используют перемещения данных tooparallelize hello несколько потоков.</span><span class="sxs-lookup"><span data-stu-id="9ca2c-113">These options have better performance as they use multiple threads tooparallelize hello data movement.</span></span>
> 
> 

<span data-ttu-id="9ca2c-114">Узнайте, как toouse hello Azure SDK для Node.js toocreate учетную запись хранилища Озера данных Azure и выполнять основные операции, такие как создавать папки, отправка и загрузка файлов данных, удалите учетную запись, и т. д. Дополнительные сведения о хранилище озера данных см. в [обзоре Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9ca2c-114">Learn how toouse hello Azure SDK for Node.js toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span> <span data-ttu-id="9ca2c-115">В настоящее время поддерживает SDK hello</span><span class="sxs-lookup"><span data-stu-id="9ca2c-115">Currently, hello SDK supports</span></span>

* <span data-ttu-id="9ca2c-116">**Node.js версии 0.10.0 или выше;**</span><span class="sxs-lookup"><span data-stu-id="9ca2c-116">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="9ca2c-117">**версию REST API для учетной записи: 2015-10-01-preview;**</span><span class="sxs-lookup"><span data-stu-id="9ca2c-117">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="9ca2c-118">**версию REST API для файловой системы: 2015-10-01-preview.**</span><span class="sxs-lookup"><span data-stu-id="9ca2c-118">**REST API version for FileSystem: 2015-10-01-preview**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ca2c-119">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9ca2c-119">Prerequisites</span></span>
<span data-ttu-id="9ca2c-120">Прежде чем приступать к этой статье, необходимо иметь следующие hello:</span><span class="sxs-lookup"><span data-stu-id="9ca2c-120">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="9ca2c-121">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="9ca2c-121">**An Azure subscription**.</span></span> <span data-ttu-id="9ca2c-122">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9ca2c-122">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="9ca2c-123">**Создание приложения Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9ca2c-123">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="9ca2c-124">Использовать хранилище Озера данных приложение hello tooauthenticate hello Azure AD приложения с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ca2c-124">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="9ca2c-125">Существуют tooauthenticate различные подходы с Azure AD, которые являются **проверки подлинности для конечных пользователей** или **проверки подлинности службы для службы**.</span><span class="sxs-lookup"><span data-stu-id="9ca2c-125">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="9ca2c-126">Инструкции и Дополнительные сведения о том, как tooauthenticate, в разделе [проверки подлинности для конечных пользователей](data-lake-store-end-user-authenticate-using-active-directory.md) или [проверки подлинности службы для службы](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="9ca2c-126">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="how-tooinstall"></a><span data-ttu-id="9ca2c-127">Как tooInstall</span><span class="sxs-lookup"><span data-stu-id="9ca2c-127">How tooInstall</span></span>
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="9ca2c-128">Проверка подлинности с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9ca2c-128">Authenticate using Azure Active Directory</span></span>
<span data-ttu-id="9ca2c-129">фрагменты кода Hello ниже показано два отдельных способов проверки подлинности с помощью хранилища Озера данных, с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9ca2c-129">hello snippets below show two separate ways of authenticating with Data Lake Store using Azure AD.</span></span> <span data-ttu-id="9ca2c-130">Подробное рассмотрение на различные методы toouse для проверки подлинности в хранилище Озера данных см. в разделе [аутентификация с помощью хранилища Озера данных Azure Active Directory с помощью](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="9ca2c-130">For a detailed discussion on various methods toouse for authentication with Data Lake Store, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="9ca2c-131">в приведенном ниже фрагменте Hello также требует входных данных, таких как Azure AD доменное имя, идентификатор клиента приложения Azure AD и т. д. Эти сведения можно получить из приложения Azure AD, сначала необходимо создать, hello сведения о которых также включаются в ссылку выше.</span><span class="sxs-lookup"><span data-stu-id="9ca2c-131">hello snippet below also requires inputs like Azure AD domain name, client ID for an Azure AD app, etc. All these details can be retrieved from an Azure AD application that you must created, hello details of which are also included in link above.</span></span>

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-hello-data-lake-store-clients"></a><span data-ttu-id="9ca2c-132">Создание клиентов хранилища Озера данных hello</span><span class="sxs-lookup"><span data-stu-id="9ca2c-132">Create hello Data Lake Store Clients</span></span>
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="9ca2c-133">Создание учетной записи хранения озера данных</span><span class="sxs-lookup"><span data-stu-id="9ca2c-133">Create a Data Lake Store Account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlsacct';
var location = 'eastus2';

// account object toocreate
var accountToCreate = {
  tags: {
    testtag1: 'testvalue1',
    testtag2: 'testvalue2'
  },
  name: accountName,
  location: location
};

client.account.create(resourceGroupName, accountName, accountToCreate, function (err, result, request, response) {
  if (err) {
    console.log(err);
    /*err has reference toohello actual request and response, so you can see what was sent and received on hello wire.
      hello structure of err looks like this:
      err: {
        code: 'Error Code',
        message: 'Error Message',
        body: 'hello response body if any',
        request: reference tooa stripped version of http request
        response: reference tooa stripped version of hello response
      }
    */
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="create-a-file-with-content"></a><span data-ttu-id="9ca2c-134">Создание файла с содержимым</span><span class="sxs-lookup"><span data-stu-id="9ca2c-134">Create a file with content</span></span>
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var fileToCreate = '/myfolder/myfile.txt';
var options = {
  streamContents: new Buffer('some string content')
}

filesystemClient.fileSystem.listFileStatus(accountName, fileToCreate, options, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    // no result is returned, only a 201 response for success.
    console.log('response is: ' + util.inspect(response, {depth: null}));
  }
});
```

## <a name="get-a-list-of-files-and-folders"></a><span data-ttu-id="9ca2c-135">Получение списка файлов и папок</span><span class="sxs-lookup"><span data-stu-id="9ca2c-135">Get a list of files and folders</span></span>
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var pathToEnumerate = '/myfolder';
filesystemClient.fileSystem.listFileStatus(accountName, pathToEnumerate, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="see-also"></a><span data-ttu-id="9ca2c-136">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="9ca2c-136">See also</span></span>
* [<span data-ttu-id="9ca2c-137">Пакет Microsoft Azure SDK для Node.js</span><span class="sxs-lookup"><span data-stu-id="9ca2c-137">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="9ca2c-138">Пакет Microsoft Azure SDK для Node.js — управление аналитикой озера данных</span><span class="sxs-lookup"><span data-stu-id="9ca2c-138">Microsoft Azure SDK for Node.js - Data Lake Analytics Management</span></span>](https://www.npmjs.com/package/azure-arm-datalake-analytics)

