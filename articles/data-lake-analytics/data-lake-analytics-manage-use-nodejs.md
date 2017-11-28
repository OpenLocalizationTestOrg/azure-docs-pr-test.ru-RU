---
title: "Управление Azure Data Lake Analytics с помощью пакета SDK Azure для Node.js | Документация Майкрософт"
description: "Узнайте, как управлять учетными записями, источниками данных, заданиями и пользователями аналитики озера данных Azure с помощью пакета SDK Azure для Node.js."
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 9de1bcf4-b15b-4d0b-9284-8889ecf0c438
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 769cf9b09eecd204c8b5b944065dad57a6d73231
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-sdk-for-nodejs"></a><span data-ttu-id="a4c23-103">Управление аналитикой озера данных Azure с помощью пакета SDK Azure для Node.js</span><span class="sxs-lookup"><span data-stu-id="a4c23-103">Manage Azure Data Lake Analytics using Azure SDK for Node.js</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="a4c23-104">Используя пакет SDK Azure для Node.js, можно управлять учетными записями, заданиями и каталогами аналитики озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="a4c23-104">The Azure SDK for Node.js can be used for managing Azure Data Lake Analytics accounts, jobs and catalogs.</span></span> <span data-ttu-id="a4c23-105">Для просмотра статей, посвященных управлению с помощью других средств, щелкните средство выбора вкладок выше.</span><span class="sxs-lookup"><span data-stu-id="a4c23-105">To see management topic using other tools, click the tab select above.</span></span>

<span data-ttu-id="a4c23-106">Сейчас он поддерживает:</span><span class="sxs-lookup"><span data-stu-id="a4c23-106">Right now it supports:</span></span>

* <span data-ttu-id="a4c23-107">**Node.js версии 0.10.0 или выше;**</span><span class="sxs-lookup"><span data-stu-id="a4c23-107">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="a4c23-108">**версию REST API для учетной записи: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="a4c23-108">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="a4c23-109">**версию REST API для каталога: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="a4c23-109">**REST API version for Catalog: 2015-10-01-preview**</span></span>
* <span data-ttu-id="a4c23-110">**версию REST API для задания: 2016-03-20-preview**</span><span class="sxs-lookup"><span data-stu-id="a4c23-110">**REST API version for Job: 2016-03-20-preview**</span></span>

## <a name="features"></a><span data-ttu-id="a4c23-111">Функции</span><span class="sxs-lookup"><span data-stu-id="a4c23-111">Features</span></span>
* <span data-ttu-id="a4c23-112">Управление учетными записями: создание, получение, получение списков, обновление и удаление.</span><span class="sxs-lookup"><span data-stu-id="a4c23-112">Account management: create, get, list, update, and delete.</span></span>
* <span data-ttu-id="a4c23-113">Управление заданиями: отправка, получение, перечисление и отмена.</span><span class="sxs-lookup"><span data-stu-id="a4c23-113">Job management: submit, get, list, and cancel.</span></span>
* <span data-ttu-id="a4c23-114">Управление каталогами: получение и перечисление.</span><span class="sxs-lookup"><span data-stu-id="a4c23-114">Catalog management: get and list.</span></span>

## <a name="how-to-install"></a><span data-ttu-id="a4c23-115">Установка</span><span class="sxs-lookup"><span data-stu-id="a4c23-115">How to Install</span></span>
```bash
npm install azure-arm-datalake-analytics
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="a4c23-116">Проверка подлинности с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a4c23-116">Authenticate using Azure Active Directory</span></span>
 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-the-data-lake-analytics-client"></a><span data-ttu-id="a4c23-117">Создание клиента аналитики озера данных</span><span class="sxs-lookup"><span data-stu-id="a4c23-117">Create the Data Lake Analytics client</span></span>
```javascript
var adlaManagement = require("azure-arm-datalake-analytics");
var acccountClient = new adlaManagement.DataLakeAnalyticsAccountClient(credentials, 'your-subscription-id');
var jobClient = new adlaManagement.DataLakeAnalyticsJobClient(credentials, 'azuredatalakeanalytics.net');
var catalogClient = new adlaManagement.DataLakeAnalyticsCatalogClient(credentials, 'azuredatalakeanalytics.net');
```

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="a4c23-118">Создание учетной записи аналитики озера данных</span><span class="sxs-lookup"><span data-stu-id="a4c23-118">Create a Data Lake Analytics account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlaacct';
var location = 'eastus2';

// A Data Lake Store account must already have been created to create
// a Data Lake Analytics account. See the Data Lake Store readme for
// information on doing so. For now, we assume one exists already.
var datalakeStoreAccountName = 'existingadlsaccount';

// account object to create
var accountToCreate = {
  tags: {
    testtag1: 'testvalue1',
    testtag2: 'testvalue2'
  },
  name: accountName,
  location: location,
  properties: {
    defaultDataLakeStoreAccount: datalakeStoreAccountName,
    dataLakeStoreAccounts: [
      {
        name: datalakeStoreAccountName
      }
    ]
  }
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

## <a name="get-a-list-of-jobs"></a><span data-ttu-id="a4c23-119">Получение списка заданий</span><span class="sxs-lookup"><span data-stu-id="a4c23-119">Get a list of jobs</span></span>
```javascript
var util = require('util');
var accountName = 'testadlaacct';
jobClient.job.list(accountName, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="get-a-list-of-databases-in-the-data-lake-analytics-catalog"></a><span data-ttu-id="a4c23-120">Получение списка баз данных в каталоге аналитики озера данных</span><span class="sxs-lookup"><span data-stu-id="a4c23-120">Get a list of databases in the Data Lake Analytics Catalog</span></span>
```javascript
var util = require('util');
var accountName = 'testadlaacct';
catalogClient.catalog.listDatabases(accountName, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="see-also"></a><span data-ttu-id="a4c23-121">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="a4c23-121">See also</span></span>
* [<span data-ttu-id="a4c23-122">Пакет Microsoft Azure SDK для Node.js</span><span class="sxs-lookup"><span data-stu-id="a4c23-122">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="a4c23-123">Пакет Microsoft Azure SDK для Node.js — управление хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="a4c23-123">Microsoft Azure SDK for Node.js - Data Lake Store Management</span></span>](https://github.com/Azure/azure-sdk-for-node/tree/autorest/lib/services/dataLake.Store)

