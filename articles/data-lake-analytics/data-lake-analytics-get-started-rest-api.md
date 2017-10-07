---
title: "aaaGet к выполнению аналитики Озера данных с помощью API-интерфейса REST | Документы Microsoft"
description: "Используйте API-интерфейс REST WebHDFS операции tooperform аналитике Озера данных"
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
ms.openlocfilehash: a0b13d521821fd2d74716cc52485585feb7c51b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a><span data-ttu-id="878f2-103">Начало работы с Azure Data Lake Analytics с помощью интерфейсов REST API</span><span class="sxs-lookup"><span data-stu-id="878f2-103">Get started with Azure Data Lake Analytics using REST APIs</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="878f2-104">Узнайте, как toouse WebHDFS REST API и API-интерфейсы REST аналитика Озера данных toomanage аналитики Озера данных учетных записей, заданий и каталога.</span><span class="sxs-lookup"><span data-stu-id="878f2-104">Learn how toouse WebHDFS REST APIs and Data Lake Analytics REST APIs toomanage Data Lake Analytics accounts, jobs, and catalog.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="878f2-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="878f2-105">Prerequisites</span></span>
* <span data-ttu-id="878f2-106">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="878f2-106">**An Azure subscription**.</span></span> <span data-ttu-id="878f2-107">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="878f2-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="878f2-108">**Создание приложения Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="878f2-108">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="878f2-109">Используйте приложение аналитики Озера данных hello tooauthenticate приложения hello Azure AD с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="878f2-109">You use hello Azure AD application tooauthenticate hello Data Lake Analytics application with Azure AD.</span></span> <span data-ttu-id="878f2-110">Существуют tooauthenticate различные подходы с Azure AD, которые являются **проверки подлинности для конечных пользователей** или **проверки подлинности службы для службы**.</span><span class="sxs-lookup"><span data-stu-id="878f2-110">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="878f2-111">Инструкции и Дополнительные сведения о том, как tooauthenticate, в разделе [аутентификация с помощью аналитики Озера данных Azure Active Directory с помощью](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="878f2-111">For instructions and more information on how tooauthenticate, see [Authenticate with Data Lake Analytics using Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="878f2-112">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="878f2-112">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="878f2-113">В этой статье используется toodemonstrate перелистывание как вызывает toomake API-интерфейса REST для учетной записи аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="878f2-113">This article uses cURL toodemonstrate how toomake REST API calls against a Data Lake Analytics account.</span></span>

## <a name="authenticate-with-azure-active-directory"></a><span data-ttu-id="878f2-114">Проверка подлинности с помощью Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="878f2-114">Authenticate with Azure Active Directory</span></span>
<span data-ttu-id="878f2-115">Существует два метода проверки подлинности с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="878f2-115">There are two methods for authenticating with Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="878f2-116">Проверка подлинности пользователя (интерактивная)</span><span class="sxs-lookup"><span data-stu-id="878f2-116">End-user authentication (interactive)</span></span>
<span data-ttu-id="878f2-117">При использовании этого метода приложение запрашивает toolog пользователя hello в, и все hello операции выполняются в контексте hello hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="878f2-117">Using this method, application prompts hello user toolog in and all hello operations are performed in hello context of hello user.</span></span> 

<span data-ttu-id="878f2-118">Выполните приведенные ниже действия, чтобы использовать интерактивную проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="878f2-118">Follow these steps for interactive authentication:</span></span>

1. <span data-ttu-id="878f2-119">Через приложения перенаправить пользователя toohello hello, URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="878f2-119">Through your application, redirect hello user toohello following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="878f2-120">\<URI ПЕРЕНАПРАВЛЕНИЯ > должен toobe кодируется для использования в URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="878f2-120">\<REDIRECT-URI> needs toobe encoded for use in a URL.</span></span> <span data-ttu-id="878f2-121">Поэтому для https://localhost используйте `https%3A%2F%2Flocalhost`.</span><span class="sxs-lookup"><span data-stu-id="878f2-121">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="878f2-122">Для целей этого учебника hello можно заменить значения заполнителей hello в URL-АДРЕСЕ hello выше и вставьте его в адресной строке веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="878f2-122">For hello purpose of this tutorial, you can replace hello placeholder values in hello URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="878f2-123">Будет перенаправленный tooauthenticate, с помощью Azure имени входа.</span><span class="sxs-lookup"><span data-stu-id="878f2-123">You will be redirected tooauthenticate using your Azure login.</span></span> <span data-ttu-id="878f2-124">После входа в систему можно успешно hello ответ отображается в адресной строке браузера hello.</span><span class="sxs-lookup"><span data-stu-id="878f2-124">Once you succesfully log in, hello response is displayed in hello browser's address bar.</span></span> <span data-ttu-id="878f2-125">Hello ответ будут иметь hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="878f2-125">hello response will be in hello following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="878f2-126">Захватить hello код авторизации из ответа hello.</span><span class="sxs-lookup"><span data-stu-id="878f2-126">Capture hello authorization code from hello response.</span></span> <span data-ttu-id="878f2-127">В этом учебнике можно скопировать код авторизации hello из адресной строки hello hello веб-браузера и передайте его в hello POST запроса toohello конечную точку токена, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="878f2-127">For this tutorial, you can copy hello authorization code from hello address bar of hello web browser and pass it in hello POST request toohello token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="878f2-128">В этом случае hello \<URI ПЕРЕНАПРАВЛЕНИЯ > не должны быть закодированы.</span><span class="sxs-lookup"><span data-stu-id="878f2-128">In this case, hello \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="878f2-129">Hello ответ — объект JSON, который содержит маркер доступа (например, `"access_token": "<ACCESS_TOKEN>"`) и токена обновления (например, `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="878f2-129">hello response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="878f2-130">Приложение использует маркер доступа hello при доступе к хранилищу Озера данных Azure и tooget токена обновления hello другой маркер доступа после истечения срока действия маркера доступа.</span><span class="sxs-lookup"><span data-stu-id="878f2-130">Your application uses hello access token when accessing Azure Data Lake Store and hello refresh token tooget another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="878f2-131">После истечения срока действия маркера доступа hello, вы можете запросить новый токен доступа с помощью токена обновления hello, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="878f2-131">When hello access token expires, you can request a new access token using hello refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="878f2-132">Дополнительные сведения об интерактивной проверке подлинности пользователей см. в статье [Авторизация доступа к веб-приложениям с помощью OAuth 2.0 и Azure Active Directory](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span><span class="sxs-lookup"><span data-stu-id="878f2-132">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="878f2-133">Проверка подлинности с взаимодействием между службами (неинтерактивная)</span><span class="sxs-lookup"><span data-stu-id="878f2-133">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="878f2-134">При использовании этого метода приложение предоставляет свои собственные учетные данные tooperform hello операции.</span><span class="sxs-lookup"><span data-stu-id="878f2-134">Using this method, application provides its own credentials tooperform hello operations.</span></span> <span data-ttu-id="878f2-135">Для этого необходимо выдать запрос POST, как hello приведенное ниже:</span><span class="sxs-lookup"><span data-stu-id="878f2-135">For this, you must issue a POST request like hello one shown below:</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="878f2-136">Hello результат этого запроса будет включать маркер авторизации (обозначается `access-token` в выходных данных hello ниже), впоследствии будет передаваться с вызовы REST API.</span><span class="sxs-lookup"><span data-stu-id="878f2-136">hello output of this request will include an authorization token (denoted by `access-token` in hello output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="878f2-137">Сохраните этот маркер в текстовый файл. Он потребуется в данной статье позднее.</span><span class="sxs-lookup"><span data-stu-id="878f2-137">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="878f2-138">В этой статье используется hello **неинтерактивной** подход.</span><span class="sxs-lookup"><span data-stu-id="878f2-138">This article uses hello **non-interactive** approach.</span></span> <span data-ttu-id="878f2-139">Дополнительные сведения о пакетном (service to service вызовов) см. в разделе [tooservice вызовы с использованием учетных данных службы](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="878f2-139">For more information on non-interactive (service-to-service calls), see [Service tooservice calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="878f2-140">Создание учетной записи аналитики озера данных</span><span class="sxs-lookup"><span data-stu-id="878f2-140">Create a Data Lake Analytics account</span></span>
<span data-ttu-id="878f2-141">Перед тем как создать учетную запись Data Lake Analytics, необходимо создать группу ресурсов Azure и учетную запись Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="878f2-141">You must create an Azure Resource group, and a Data Lake Store account before you can create a Data Lake Analytics account.</span></span>  <span data-ttu-id="878f2-142">Дополнительные сведения см. в разделе [Создание учетной записи Data Lake Store](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="878f2-142">See [Create a Data Lake Store account](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span></span>

<span data-ttu-id="878f2-143">Здравствуйте, следующая команда показывает перелистывание как toocreate учетной записи:</span><span class="sxs-lookup"><span data-stu-id="878f2-143">hello following Curl command shows how toocreate an account:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

<span data-ttu-id="878f2-144">Замените \< `REDACTED` \> маркером авторизации hello \< `AzureSubscriptionID` \> своим Идентификатором подписки, \< `AzureResourceGroupName` \> с существующим ресурсом Azure Имя группы и \< `NewAzureDataLakeAnalyticsAccountName` \> с новым именем учетной записи аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="878f2-144">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`NewAzureDataLakeAnalyticsAccountName`\> with a new Data Lake Analytics Account name.</span></span> <span data-ttu-id="878f2-145">Hello полезные данные запроса для этой команды, содержащиеся в hello **CreateDatalakeAnalyticsAccountRequest.json** файл, предоставленный для hello `-d` описание параметра.</span><span class="sxs-lookup"><span data-stu-id="878f2-145">hello request payload for this command is contained in hello **CreateDatalakeAnalyticsAccountRequest.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="878f2-146">Hello содержимое файла input.json hello напоминают hello следующее:</span><span class="sxs-lookup"><span data-stu-id="878f2-146">hello contents of hello input.json file resemble hello following:</span></span>

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


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a><span data-ttu-id="878f2-147">Список учетных записей Data Lake Analytics в подписке</span><span class="sxs-lookup"><span data-stu-id="878f2-147">List Data Lake Analytics accounts in a subscription</span></span>
<span data-ttu-id="878f2-148">Hello следующую команду Curl показано, как toolist учетные записи в подписке.</span><span class="sxs-lookup"><span data-stu-id="878f2-148">hello following Curl command shows how toolist accounts in a subscription:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

<span data-ttu-id="878f2-149">Замените \< `REDACTED` \> маркером авторизации hello \< `AzureSubscriptionID` \> вашим идентификатором подписки.</span><span class="sxs-lookup"><span data-stu-id="878f2-149">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID.</span></span> <span data-ttu-id="878f2-150">Hello выходные данные выглядят аналогично:</span><span class="sxs-lookup"><span data-stu-id="878f2-150">hello output is similar to:</span></span>

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

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="878f2-151">Получение сведений об учетной записи Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="878f2-151">Get information about a Data Lake Analytics account</span></span>
<span data-ttu-id="878f2-152">Здравствуйте, следующая команда показывает перелистывание как tooget сведения об учетной записи:</span><span class="sxs-lookup"><span data-stu-id="878f2-152">hello following Curl command shows how tooget an account information:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

<span data-ttu-id="878f2-153">Замените \< `REDACTED` \> маркером авторизации hello \< `AzureSubscriptionID` \> своим Идентификатором подписки, \< `AzureResourceGroupName` \> с существующим ресурсом Azure Имя группы и \< `DataLakeAnalyticsAccountName` \> с именем hello существующей учетной записи аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="878f2-153">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="878f2-154">Hello выходные данные выглядят аналогично:</span><span class="sxs-lookup"><span data-stu-id="878f2-154">hello output is similar to:</span></span>

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

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a><span data-ttu-id="878f2-155">Список хранилищ Data Lake Store учетной записи Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="878f2-155">List Data Lake Stores of a Data Lake Analytics account</span></span>
<span data-ttu-id="878f2-156">Hello следующую команду Curl показано, как toolist Озера данных хранятся в учетной записи:</span><span class="sxs-lookup"><span data-stu-id="878f2-156">hello following Curl command shows how toolist Data Lake Stores of an account:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

<span data-ttu-id="878f2-157">Замените \< `REDACTED` \> маркером авторизации hello \< `AzureSubscriptionID` \> своим Идентификатором подписки, \< `AzureResourceGroupName` \> с существующим ресурсом Azure Имя группы и \< `DataLakeAnalyticsAccountName` \> с именем hello существующей учетной записи аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="878f2-157">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="878f2-158">Hello выходные данные выглядят аналогично:</span><span class="sxs-lookup"><span data-stu-id="878f2-158">hello output is similar to:</span></span>

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

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="878f2-159">Отправка заданий U-SQL</span><span class="sxs-lookup"><span data-stu-id="878f2-159">Submit U-SQL jobs</span></span>
<span data-ttu-id="878f2-160">Здравствуйте, следующая команда показывает перелистывание как задание toosubmit U-SQL:</span><span class="sxs-lookup"><span data-stu-id="878f2-160">hello following Curl command shows how toosubmit a U-SQL job:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

<span data-ttu-id="878f2-161">Замените \< `REDACTED` \> маркером авторизации hello \< `DataLakeAnalyticsAccountName` \> с именем hello существующей учетной записи аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="878f2-161">Replace \<`REDACTED`\> with hello authorization token, \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="878f2-162">Hello полезные данные запроса для этой команды, содержащиеся в hello **SubmitADLAJob.json** файл, предоставленный для hello `-d` описание параметра.</span><span class="sxs-lookup"><span data-stu-id="878f2-162">hello request payload for this command is contained in hello **SubmitADLAJob.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="878f2-163">Hello содержимое файла input.json hello напоминают hello следующее:</span><span class="sxs-lookup"><span data-stu-id="878f2-163">hello contents of hello input.json file resemble hello following:</span></span>

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
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    too\"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

<span data-ttu-id="878f2-164">Hello выходные данные выглядят аналогично:</span><span class="sxs-lookup"><span data-stu-id="878f2-164">hello output is similar to:</span></span>

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


## <a name="list-u-sql-jobs"></a><span data-ttu-id="878f2-165">Получение списка заданий U-SQL</span><span class="sxs-lookup"><span data-stu-id="878f2-165">List U-SQL jobs</span></span>
<span data-ttu-id="878f2-166">Здравствуйте, следующая команда показывает перелистывание как задания toolist U-SQL:</span><span class="sxs-lookup"><span data-stu-id="878f2-166">hello following Curl command shows how toolist U-SQL jobs:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

<span data-ttu-id="878f2-167">Замените \< `REDACTED` \> маркером авторизации hello и \< `DataLakeAnalyticsAccountName` \> с именем hello существующей учетной записи аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="878f2-167">Replace \<`REDACTED`\> with hello authorization token, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> 

<span data-ttu-id="878f2-168">Hello выходные данные выглядят аналогично:</span><span class="sxs-lookup"><span data-stu-id="878f2-168">hello output is similar to:</span></span>

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


## <a name="get-catalog-items"></a><span data-ttu-id="878f2-169">Получение элементов каталога</span><span class="sxs-lookup"><span data-stu-id="878f2-169">Get catalog items</span></span>
<span data-ttu-id="878f2-170">Hello следующую команду Curl показано, как базы данных hello tooget от hello каталога:</span><span class="sxs-lookup"><span data-stu-id="878f2-170">hello following Curl command shows how tooget hello databases from hello catalog:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

<span data-ttu-id="878f2-171">Hello выходные данные выглядят аналогично:</span><span class="sxs-lookup"><span data-stu-id="878f2-171">hello output is similar to:</span></span>

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a><span data-ttu-id="878f2-172">См. также</span><span class="sxs-lookup"><span data-stu-id="878f2-172">See also</span></span>
* <span data-ttu-id="878f2-173">в разделе toosee более сложный запрос, [веб-сайта анализ журналов с помощью аналитики Озера данных Azure](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="878f2-173">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="878f2-174">tooget к разработке приложений U-SQL, в разделе [сценариев разработки U-SQL, с помощью средства Озера данных для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="878f2-174">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="878f2-175">в разделе toolearn U-SQL [Приступая к работе с Azure аналитика Озера данных U-SQL языка](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="878f2-175">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="878f2-176">Задачи управления описываются в руководстве по [управлению Azure Data Lake Analytics с помощью портала Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="878f2-176">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="878f2-177">в разделе tooget содержится обзор аналитики Озера данных, [Обзор аналитики Озера данных Azure](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="878f2-177">tooget an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
* <span data-ttu-id="878f2-178">toosee hello же учебника при помощи других средств, щелкните селекторы вкладку hello на hello вверху страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="878f2-178">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>

