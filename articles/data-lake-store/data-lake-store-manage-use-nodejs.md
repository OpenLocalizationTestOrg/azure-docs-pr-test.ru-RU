---
title: "Начало работы с Azure Data Lake Store с помощью пакета SDK для Node.js | Документация Майкрософт"
description: "Сведения об использовании пакета SDK для Node.js при работе с учетными записями и файловой системой Data Lake Store."
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
ms.openlocfilehash: 8c7a2e6ca061bbfa077592efb73d592906c3d070
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a><span data-ttu-id="cd4c2-103">Начало работы с Azure Data Lake Store с помощью пакета Azure SDK для Node.js</span><span class="sxs-lookup"><span data-stu-id="cd4c2-103">Get started with Azure Data Lake Store using Azure SDK for Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cd4c2-104">Портал</span><span class="sxs-lookup"><span data-stu-id="cd4c2-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="cd4c2-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd4c2-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="cd4c2-106">Пакет SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="cd4c2-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="cd4c2-107">Пакет SDK для Java</span><span class="sxs-lookup"><span data-stu-id="cd4c2-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="cd4c2-108">REST API</span><span class="sxs-lookup"><span data-stu-id="cd4c2-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="cd4c2-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="cd4c2-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="cd4c2-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="cd4c2-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="cd4c2-111">Python</span><span class="sxs-lookup"><span data-stu-id="cd4c2-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> <span data-ttu-id="cd4c2-112">Для передачи и скачивания больших объемов данных (больших файлов, большого количества файлов или и того, и другого) мы рекомендуем использовать [пакет SDK для Python](data-lake-store-get-started-python.md), [пакет SDK для .NET](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md) или [Azure PowerShell](data-lake-store-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="cd4c2-112">For uploading and downloading large amount of data (large files, a large number of files, or both), we recommend that you use the [Python SDK](data-lake-store-get-started-python.md), the [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), or [Azure PowerShell](data-lake-store-get-started-powershell.md).</span></span> <span data-ttu-id="cd4c2-113">Они имеют повышенную производительность, так как используют несколько потоков для параллельной передачи данных.</span><span class="sxs-lookup"><span data-stu-id="cd4c2-113">These options have better performance as they use multiple threads to parallelize the data movement.</span></span>
> 
> 

<span data-ttu-id="cd4c2-114">Узнайте, как с помощью пакета Azure SDK для Node.js создать учетную запись Azure Data Lake Store и выполнять базовые операции, такие как создание папок, передача и загрузка файлов данных, удаление учетной записи и т. д. Дополнительные сведения о хранилище озера данных см. в [обзоре Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cd4c2-114">Learn how to use the Azure SDK for Node.js to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span> <span data-ttu-id="cd4c2-115">В настоящее время пакет SDK поддерживает следующее:</span><span class="sxs-lookup"><span data-stu-id="cd4c2-115">Currently, the SDK supports</span></span>

* <span data-ttu-id="cd4c2-116">**Node.js версии 0.10.0 или выше;**</span><span class="sxs-lookup"><span data-stu-id="cd4c2-116">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="cd4c2-117">**версию REST API для учетной записи: 2015-10-01-preview;**</span><span class="sxs-lookup"><span data-stu-id="cd4c2-117">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="cd4c2-118">**версию REST API для файловой системы: 2015-10-01-preview.**</span><span class="sxs-lookup"><span data-stu-id="cd4c2-118">**REST API version for FileSystem: 2015-10-01-preview**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cd4c2-119">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cd4c2-119">Prerequisites</span></span>
<span data-ttu-id="cd4c2-120">Перед началом работы с этой статьей необходимо иметь следующее:</span><span class="sxs-lookup"><span data-stu-id="cd4c2-120">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="cd4c2-121">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="cd4c2-121">**An Azure subscription**.</span></span> <span data-ttu-id="cd4c2-122">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cd4c2-122">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="cd4c2-123">**Создание приложения Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cd4c2-123">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="cd4c2-124">Это приложение будет использоваться для проверки подлинности приложения Data Lake Store в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd4c2-124">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="cd4c2-125">Есть разные способы проверки подлинности приложения с помощью Azure AD: **проверка подлинности пользователя** и **проверка подлинности со взаимодействием между службами**.</span><span class="sxs-lookup"><span data-stu-id="cd4c2-125">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="cd4c2-126">Инструкции и дополнительные сведения об аутентификации см. в разделах [Аутентификация пользователей](data-lake-store-end-user-authenticate-using-active-directory.md) и [Аутентификация между службами](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="cd4c2-126">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="how-to-install"></a><span data-ttu-id="cd4c2-127">Установка</span><span class="sxs-lookup"><span data-stu-id="cd4c2-127">How to Install</span></span>
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="cd4c2-128">Проверка подлинности с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cd4c2-128">Authenticate using Azure Active Directory</span></span>
<span data-ttu-id="cd4c2-129">Приведенные ниже фрагменты кода — это два разных варианта проверки подлинности в Data Lake Store с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cd4c2-129">The snippets below show two separate ways of authenticating with Data Lake Store using Azure AD.</span></span> <span data-ttu-id="cd4c2-130">Подробные сведения о разных методах проверки подлинности в Data Lake Store см. в [этой статье](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="cd4c2-130">For a detailed discussion on various methods to use for authentication with Data Lake Store, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="cd4c2-131">В приведенный ниже фрагмент кода также необходимо добавить такие входные параметры, как доменное имя Azure AD, идентификатор клиента для приложения Azure AD и т. д. Все эти данные можно получить в созданном приложении Azure AD, сведения о котором также содержатся в указанной выше статье.</span><span class="sxs-lookup"><span data-stu-id="cd4c2-131">The snippet below also requires inputs like Azure AD domain name, client ID for an Azure AD app, etc. All these details can be retrieved from an Azure AD application that you must created, the details of which are also included in link above.</span></span>

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-the-data-lake-store-clients"></a><span data-ttu-id="cd4c2-132">Создание клиентов Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="cd4c2-132">Create the Data Lake Store Clients</span></span>
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="cd4c2-133">Создание учетной записи хранения озера данных</span><span class="sxs-lookup"><span data-stu-id="cd4c2-133">Create a Data Lake Store Account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlsacct';
var location = 'eastus2';

// account object to create
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
    /*err has reference to the actual request and response, so you can see what was sent and received on the wire.
      The structure of err looks like this:
      err: {
        code: 'Error Code',
        message: 'Error Message',
        body: 'The response body if any',
        request: reference to a stripped version of http request
        response: reference to a stripped version of the response
      }
    */
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="create-a-file-with-content"></a><span data-ttu-id="cd4c2-134">Создание файла с содержимым</span><span class="sxs-lookup"><span data-stu-id="cd4c2-134">Create a file with content</span></span>
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

## <a name="get-a-list-of-files-and-folders"></a><span data-ttu-id="cd4c2-135">Получение списка файлов и папок</span><span class="sxs-lookup"><span data-stu-id="cd4c2-135">Get a list of files and folders</span></span>
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

## <a name="see-also"></a><span data-ttu-id="cd4c2-136">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="cd4c2-136">See also</span></span>
* [<span data-ttu-id="cd4c2-137">Пакет Microsoft Azure SDK для Node.js</span><span class="sxs-lookup"><span data-stu-id="cd4c2-137">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="cd4c2-138">Пакет Microsoft Azure SDK для Node.js — управление аналитикой озера данных</span><span class="sxs-lookup"><span data-stu-id="cd4c2-138">Microsoft Azure SDK for Node.js - Data Lake Analytics Management</span></span>](https://www.npmjs.com/package/azure-arm-datalake-analytics)

