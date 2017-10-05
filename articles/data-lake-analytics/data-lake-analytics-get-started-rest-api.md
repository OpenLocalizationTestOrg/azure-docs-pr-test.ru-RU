---
title: "Начало работы с Data Lake Analytics с помощью интерфейсов REST API | Документация Майкрософт"
description: "Использование интерфейсов REST API WebHDFS для выполнения операций в Data Lake Analytics"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 5e133d92-baaa-44c9-890c-ab2d85c91122
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: jgao
ms.openlocfilehash: 332d7af2539eea8890745005104ac5b0921c2b7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a><span data-ttu-id="e37d3-103">Начало работы с Azure Data Lake Analytics с помощью интерфейсов REST API</span><span class="sxs-lookup"><span data-stu-id="e37d3-103">Get started with Azure Data Lake Analytics using REST APIs</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="e37d3-104">Узнайте, как использовать интерфейсы REST API WebHDFS и Data Lake Analytics, чтобы управлять учетными записями, заданиями и каталогом Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="e37d3-104">Learn how to use WebHDFS REST APIs and Data Lake Analytics REST APIs to manage Data Lake Analytics accounts, jobs, and catalog.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e37d3-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e37d3-105">Prerequisites</span></span>
* <span data-ttu-id="e37d3-106">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="e37d3-106">**An Azure subscription**.</span></span> <span data-ttu-id="e37d3-107">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e37d3-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e37d3-108">**Создание приложения Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e37d3-108">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="e37d3-109">Это приложение будет использоваться для проверки подлинности приложения Data Lake Analytics в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e37d3-109">You use the Azure AD application to authenticate the Data Lake Analytics application with Azure AD.</span></span> <span data-ttu-id="e37d3-110">Есть разные способы проверки подлинности приложения с помощью Azure AD: **проверка подлинности пользователя** и **проверка подлинности со взаимодействием между службами**.</span><span class="sxs-lookup"><span data-stu-id="e37d3-110">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="e37d3-111">Инструкции и дополнительные сведения о проверке подлинности см. в статье [Аутентификация в Data Lake Store с помощью Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="e37d3-111">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Analytics using Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="e37d3-112">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="e37d3-112">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="e37d3-113">В этой статье для демонстрации вызовов REST API к учетной записи Data Lake Analytics используется cURL.</span><span class="sxs-lookup"><span data-stu-id="e37d3-113">This article uses cURL to demonstrate how to make REST API calls against a Data Lake Analytics account.</span></span>

## <a name="authenticate-with-azure-active-directory"></a><span data-ttu-id="e37d3-114">Проверка подлинности с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e37d3-114">Authenticate with Azure Active Directory</span></span>
<span data-ttu-id="e37d3-115">Существует два метода проверки подлинности с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e37d3-115">There are two methods for authenticating with Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="e37d3-116">Проверка подлинности пользователя (интерактивная)</span><span class="sxs-lookup"><span data-stu-id="e37d3-116">End-user authentication (interactive)</span></span>
<span data-ttu-id="e37d3-117">Если используется этот метод, в приложении пользователю предлагается войти в систему, и все операции выполняются в контексте пользователя.</span><span class="sxs-lookup"><span data-stu-id="e37d3-117">Using this method, application prompts the user to log in and all the operations are performed in the context of the user.</span></span> 

<span data-ttu-id="e37d3-118">Выполните приведенные ниже действия, чтобы использовать интерактивную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="e37d3-118">Follow these steps for interactive authentication:</span></span>

1. <span data-ttu-id="e37d3-119">В приложении перенаправьте пользователя на следующий URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="e37d3-119">Through your application, redirect the user to the following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="e37d3-120">\<<REDIRECT-URI> должен быть закодирован для использования в URL-адресе.</span><span class="sxs-lookup"><span data-stu-id="e37d3-120">\<REDIRECT-URI> needs to be encoded for use in a URL.</span></span> <span data-ttu-id="e37d3-121">Поэтому для https://localhost используйте `https%3A%2F%2Flocalhost`.</span><span class="sxs-lookup"><span data-stu-id="e37d3-121">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="e37d3-122">В целях обучения можно заменить значения заполнителей в URL-адресе выше и вставить его в адресную строку веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="e37d3-122">For the purpose of this tutorial, you can replace the placeholder values in the URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="e37d3-123">Вы перейдете на страницу аутентификации с помощью учетной записи Azure.</span><span class="sxs-lookup"><span data-stu-id="e37d3-123">You will be redirected to authenticate using your Azure login.</span></span> <span data-ttu-id="e37d3-124">После входа в систему вы увидите ответ в адресной строке браузера.</span><span class="sxs-lookup"><span data-stu-id="e37d3-124">Once you succesfully log in, the response is displayed in the browser's address bar.</span></span> <span data-ttu-id="e37d3-125">Ответ имеет следующий формат.</span><span class="sxs-lookup"><span data-stu-id="e37d3-125">The response will be in the following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="e37d3-126">Запишите код авторизации из ответа.</span><span class="sxs-lookup"><span data-stu-id="e37d3-126">Capture the authorization code from the response.</span></span> <span data-ttu-id="e37d3-127">В этом учебнике вы можете скопировать код авторизации из адресной строки веб-браузера и передать его в запрос POST к конечной точке маркера, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="e37d3-127">For this tutorial, you can copy the authorization code from the address bar of the web browser and pass it in the POST request to the token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="e37d3-128">В этом случае кодировать \<REDIRECT-URI> не нужно.</span><span class="sxs-lookup"><span data-stu-id="e37d3-128">In this case, the \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="e37d3-129">Ответ является объектом JSON, содержащим маркер доступа (например, `"access_token": "<ACCESS_TOKEN>"`) и маркер обновления (например, `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="e37d3-129">The response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="e37d3-130">Приложение использует маркер доступа для обращения к хранилищу озера данных Azure, а маркер обновления — для получения другого маркера доступа, когда срок действия текущего маркера доступа истечет.</span><span class="sxs-lookup"><span data-stu-id="e37d3-130">Your application uses the access token when accessing Azure Data Lake Store and the refresh token to get another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="e37d3-131">По истечении срока действия маркера доступа можно запросить новый маркер доступа, используя маркер обновления, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="e37d3-131">When the access token expires, you can request a new access token using the refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="e37d3-132">Дополнительные сведения об интерактивной проверке подлинности пользователей см. в статье [Авторизация доступа к веб-приложениям с помощью OAuth 2.0 и Azure Active Directory](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span><span class="sxs-lookup"><span data-stu-id="e37d3-132">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="e37d3-133">Проверка подлинности с взаимодействием между службами (неинтерактивная)</span><span class="sxs-lookup"><span data-stu-id="e37d3-133">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="e37d3-134">Если используется этот метод, приложение предоставляет свои собственные учетные данные для выполнения операций.</span><span class="sxs-lookup"><span data-stu-id="e37d3-134">Using this method, application provides its own credentials to perform the operations.</span></span> <span data-ttu-id="e37d3-135">В этом случае необходимо отправить запрос POST, аналогичный показанному ниже.</span><span class="sxs-lookup"><span data-stu-id="e37d3-135">For this, you must issue a POST request like the one shown below:</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="e37d3-136">Выходные данные этого запроса будут содержать маркер авторизации (обозначен `access-token` в приведенных ниже выходных данных) для дальнейшей передачи в вызовах REST API.</span><span class="sxs-lookup"><span data-stu-id="e37d3-136">The output of this request will include an authorization token (denoted by `access-token` in the output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="e37d3-137">Сохраните этот маркер в текстовый файл. Он потребуется в данной статье позднее.</span><span class="sxs-lookup"><span data-stu-id="e37d3-137">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="e37d3-138">В этой статье используется **неинтерактивный** подход.</span><span class="sxs-lookup"><span data-stu-id="e37d3-138">This article uses the **non-interactive** approach.</span></span> <span data-ttu-id="e37d3-139">Дополнительные сведения о неинтерактивном подходе (вызовы между службами) см. в [этой статье](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="e37d3-139">For more information on non-interactive (service-to-service calls), see [Service to service calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="e37d3-140">Создание учетной записи аналитики озера данных</span><span class="sxs-lookup"><span data-stu-id="e37d3-140">Create a Data Lake Analytics account</span></span>
<span data-ttu-id="e37d3-141">Перед тем как создать учетную запись Data Lake Analytics, необходимо создать группу ресурсов Azure и учетную запись Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="e37d3-141">You must create an Azure Resource group, and a Data Lake Store account before you can create a Data Lake Analytics account.</span></span>  <span data-ttu-id="e37d3-142">Дополнительные сведения см. в разделе [Создание учетной записи Data Lake Store](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="e37d3-142">See [Create a Data Lake Store account](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span></span>

<span data-ttu-id="e37d3-143">Чтобы создать учетную запись, используйте следующую команду cURL:</span><span class="sxs-lookup"><span data-stu-id="e37d3-143">The following Curl command shows how to create an account:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

<span data-ttu-id="e37d3-144">Замените \<`REDACTED`\> маркером авторизации, \<`AzureSubscriptionID`\> — идентификатором подписки, \<`AzureResourceGroupName`\> — именем существующей группы ресурсов Azure, а \<`NewAzureDataLakeAnalyticsAccountName`\> — новым именем учетной записи Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="e37d3-144">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`NewAzureDataLakeAnalyticsAccountName`\> with a new Data Lake Analytics Account name.</span></span> <span data-ttu-id="e37d3-145">Полезные данные запроса для этой команды находятся в файле **CreateDatalakeAnalyticsAccountRequest.json**, предоставленном для приведенного выше параметра `-d`.</span><span class="sxs-lookup"><span data-stu-id="e37d3-145">The request payload for this command is contained in the **CreateDatalakeAnalyticsAccountRequest.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="e37d3-146">Содержимое файла input.json выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e37d3-146">The contents of the input.json file resemble the following:</span></span>

    {  
        "location": "East US 2",  
        "name": "myadla1004",  
        "tags": {},  
        "properties": {  
            "defaultDataLakeStoreAccount": "my1004store",  
            "dataLakeStoreAccounts": [  
                {  
                    "name": "my1004store"  
                }     
            ]
        }  
    }  


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a><span data-ttu-id="e37d3-147">Список учетных записей Data Lake Analytics в подписке</span><span class="sxs-lookup"><span data-stu-id="e37d3-147">List Data Lake Analytics accounts in a subscription</span></span>
<span data-ttu-id="e37d3-148">Чтобы получить список учетных записей в подписке, используйте следующую команду cURL:</span><span class="sxs-lookup"><span data-stu-id="e37d3-148">The following Curl command shows how to list accounts in a subscription:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

<span data-ttu-id="e37d3-149">Замените \<`REDACTED`\> маркером авторизации, а \<`AzureSubscriptionID`\> — идентификатором подписки.</span><span class="sxs-lookup"><span data-stu-id="e37d3-149">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID.</span></span> <span data-ttu-id="e37d3-150">Выходные данные должны быть следующего вида.</span><span class="sxs-lookup"><span data-stu-id="e37d3-150">The output is similar to:</span></span>

    {
        "value": [
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla0831.azuredatalakeanalytics.net",
                "accountId": "21e74660-0941-4880-ae72-b143c2615ea9",
                "creationTime": "2016-09-01T12:49:12.7451428Z",
                "lastModifiedTime": "2016-09-01T12:49:12.7451428Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla0831rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla0831",
            "name": "myadla0831",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            },
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla1004.azuredatalakeanalytics.net",
                "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
                "creationTime": "2016-10-04T20:46:42.287147Z",
                "lastModifiedTime": "2016-10-04T20:46:42.287147Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
            "name": "myadla1004",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            }
        ]
    }

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="e37d3-151">Получение сведений об учетной записи Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="e37d3-151">Get information about a Data Lake Analytics account</span></span>
<span data-ttu-id="e37d3-152">Чтобы получить сведения об учетной записи, используйте следующую команду cURL:</span><span class="sxs-lookup"><span data-stu-id="e37d3-152">The following Curl command shows how to get an account information:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

<span data-ttu-id="e37d3-153">Замените \<`REDACTED`\> маркером авторизации, \<`AzureSubscriptionID`\> — идентификатором подписки, \<`AzureResourceGroupName`\> — именем существующей группы ресурсов Azure, а \<`DataLakeAnalyticsAccountName`\> — именем существующей учетной записи Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="e37d3-153">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="e37d3-154">Выходные данные должны быть следующего вида.</span><span class="sxs-lookup"><span data-stu-id="e37d3-154">The output is similar to:</span></span>

    {
        "properties": {
            "defaultDataLakeStoreAccount": "my1004store",
            "dataLakeStoreAccounts": [
            {
                "properties": {
                "suffix": "azuredatalakestore.net"
                },
                "name": "my1004store"
            }
            ],
            "provisioningState": "Creating",
            "state": null,
            "endpoint": null,
            "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
            "creationTime": null,
            "lastModifiedTime": null
        },
        "location": "East US 2",
        "tags": {},
        "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
        "name": "myadla1004",
        "type": "Microsoft.DataLakeAnalytics/accounts"
    }

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a><span data-ttu-id="e37d3-155">Список хранилищ Data Lake Store учетной записи Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="e37d3-155">List Data Lake Stores of a Data Lake Analytics account</span></span>
<span data-ttu-id="e37d3-156">Чтобы получить список хранилищ Data Lake Store учетной записи, используйте следующую команду cURL:</span><span class="sxs-lookup"><span data-stu-id="e37d3-156">The following Curl command shows how to list Data Lake Stores of an account:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

<span data-ttu-id="e37d3-157">Замените \<`REDACTED`\> маркером авторизации, \<`AzureSubscriptionID`\> — идентификатором подписки, \<`AzureResourceGroupName`\> — именем существующей группы ресурсов Azure, а \<`DataLakeAnalyticsAccountName`\> — именем существующей учетной записи Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="e37d3-157">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="e37d3-158">Выходные данные должны быть следующего вида.</span><span class="sxs-lookup"><span data-stu-id="e37d3-158">The output is similar to:</span></span>

    {
        "value": [
            {
            "properties": {
                "suffix": "azuredatalakestore.net"
            },
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004/dataLakeStoreAccounts/my1004store",
            "name": "my1004store",
            "type": "Microsoft.DataLakeAnalytics/accounts/dataLakeStoreAccounts"
            }
        ]
    }

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="e37d3-159">Отправка заданий U-SQL</span><span class="sxs-lookup"><span data-stu-id="e37d3-159">Submit U-SQL jobs</span></span>
<span data-ttu-id="e37d3-160">Чтобы отправить задание U-SQL, используйте следующую команду cURL:</span><span class="sxs-lookup"><span data-stu-id="e37d3-160">The following Curl command shows how to submit a U-SQL job:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

<span data-ttu-id="e37d3-161">Замените \<`REDACTED`\> маркером авторизации, а \<`DataLakeAnalyticsAccountName`\> — именем существующей учетной записи Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="e37d3-161">Replace \<`REDACTED`\> with the authorization token, \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="e37d3-162">Полезные данные запроса для этой команды находятся в файле **SubmitADLAJob.json**, предоставленном для приведенного выше параметра `-d`.</span><span class="sxs-lookup"><span data-stu-id="e37d3-162">The request payload for this command is contained in the **SubmitADLAJob.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="e37d3-163">Содержимое файла input.json выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e37d3-163">The contents of the input.json file resemble the following:</span></span>

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "properties": {
            "type": "USql",
            "script": "@searchlog =\n    EXTRACT UserId          int,\n            Start           DateTime,\n            Region          string,\n            Query          
        string,\n            Duration        int?,\n            Urls            string,\n            ClickedUrls     string\n    FROM \"/Samples/Data/SearchLog.tsv\"\n    US
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    TO \"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

<span data-ttu-id="e37d3-164">Выходные данные должны быть следующего вида.</span><span class="sxs-lookup"><span data-stu-id="e37d3-164">The output is similar to:</span></span>

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "myadl@SPI",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "2016-10-05T13:54:59.9871859+00:00",
        "state": "Compiling",
        "result": "Succeeded",
        "stateAuditRecords": [
            {
            "newState": "New",
            "timeStamp": "2016-10-05T13:54:59.9871859+00:00",
            "details": "userName:myadl@SPI;submitMachine:N/A"
            }
        ],
        "properties": {
            "owner": "myadl@SPI",
            "resources": [],
            "runtimeVersion": "default",
            "rootProcessNodeId": "00000000-0000-0000-0000-000000000000",
            "algebraFilePath": "adl://myadls0831.azuredatalakestore.net/system/jobservice/jobs/Usql/2016/10/05/13/54/8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a/algebra.xml",
            "compileMode": "Semantic",
            "errorSource": "Unknown",
            "totalCompilationTime": "PT0S",
            "totalPausedTime": "PT0S",
            "totalQueuedTime": "PT0S",
            "totalRunningTime": "PT0S",
            "type": "USql"
        }
    }


## <a name="list-u-sql-jobs"></a><span data-ttu-id="e37d3-165">Получение списка заданий U-SQL</span><span class="sxs-lookup"><span data-stu-id="e37d3-165">List U-SQL jobs</span></span>
<span data-ttu-id="e37d3-166">Чтобы получить список заданий U-SQL, используйте следующую команду cURL:</span><span class="sxs-lookup"><span data-stu-id="e37d3-166">The following Curl command shows how to list U-SQL jobs:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

<span data-ttu-id="e37d3-167">Замените \<`REDACTED`\> маркером авторизации, а \<`DataLakeAnalyticsAccountName`\> — именем существующей учетной записи Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="e37d3-167">Replace \<`REDACTED`\> with the authorization token, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> 

<span data-ttu-id="e37d3-168">Выходные данные должны быть следующего вида.</span><span class="sxs-lookup"><span data-stu-id="e37d3-168">The output is similar to:</span></span>

    {
    "value": [
        {
        "jobId": "65cf1691-9dbe-43cd-90ed-1cafbfb406fb",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someone@microsoft.com",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:46:53 GMT",
        "startTime": "Wed, 05 Oct 2016 13:47:33 GMT",
        "endTime": "Wed, 05 Oct 2016 13:48:07 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        },
        {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someoneadl@SPI",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:54:59 GMT",
        "startTime": "Wed, 05 Oct 2016 13:55:43 GMT",
        "endTime": "Wed, 05 Oct 2016 13:56:11 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        }
    ],
    "nextLink": null,
    "count": null
    }


## <a name="get-catalog-items"></a><span data-ttu-id="e37d3-169">Получение элементов каталога</span><span class="sxs-lookup"><span data-stu-id="e37d3-169">Get catalog items</span></span>
<span data-ttu-id="e37d3-170">Чтобы получить базы данных из каталога, используйте следующую команду cURL:</span><span class="sxs-lookup"><span data-stu-id="e37d3-170">The following Curl command shows how to get the databases from the catalog:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

<span data-ttu-id="e37d3-171">Выходные данные должны быть следующего вида.</span><span class="sxs-lookup"><span data-stu-id="e37d3-171">The output is similar to:</span></span>

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a><span data-ttu-id="e37d3-172">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="e37d3-172">See also</span></span>
* <span data-ttu-id="e37d3-173">Более сложный запрос можно посмотреть в статье [Анализ журналов веб-сайта с помощью аналитики озера данных Azure](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="e37d3-173">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="e37d3-174">Чтобы приступить к разработке приложений U-SQL, ознакомьтесь со статьей [Разработка скриптов U-SQL с помощью средств озера данных для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e37d3-174">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="e37d3-175">Для знакомства с U-SQL см. статью о [начале работы с языком U-SQL для Azure Data Lake Analytics](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e37d3-175">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="e37d3-176">Задачи управления описываются в руководстве по [управлению Azure Data Lake Analytics с помощью портала Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e37d3-176">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="e37d3-177">Общие сведения об Azure Data Lake Analytics см. в [этой статье](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e37d3-177">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
* <span data-ttu-id="e37d3-178">Для просмотра учебника с помощью других средств используйте вкладки-селекторы в верхней части страницы.</span><span class="sxs-lookup"><span data-stu-id="e37d3-178">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>

