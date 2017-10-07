---
title: "API-Интерфейс REST tooget aaaUse hello работы с хранилища Озера данных | Документы Microsoft"
description: "Использование API-интерфейс REST WebHDFS tooperform операций в хранилище Озера данных"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57ac6501-cb71-4f75-82c2-acc07c562889
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: 62fce8293dfee730a61f2a3d37fc138ce7c3afdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a><span data-ttu-id="1e7e9-103">Начало работы с хранилищем озера данных Azure с помощью интерфейсов REST API</span><span class="sxs-lookup"><span data-stu-id="1e7e9-103">Get started with Azure Data Lake Store using REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1e7e9-104">Портал</span><span class="sxs-lookup"><span data-stu-id="1e7e9-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="1e7e9-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e7e9-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="1e7e9-106">Пакет SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="1e7e9-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="1e7e9-107">Пакет SDK для Java</span><span class="sxs-lookup"><span data-stu-id="1e7e9-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="1e7e9-108">REST API</span><span class="sxs-lookup"><span data-stu-id="1e7e9-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="1e7e9-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1e7e9-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="1e7e9-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="1e7e9-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="1e7e9-111">Python</span><span class="sxs-lookup"><span data-stu-id="1e7e9-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="1e7e9-112">В этой статье вы узнаете, как toouse WebHDFS интерфейсы API REST и API REST хранилища Озера данных tooperform учетной записи управления, а также операций файловой системы в хранилище Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-112">In this article, you will learn how toouse WebHDFS REST APIs and Data Lake Store REST APIs tooperform account management as well as filesystem operations on Azure Data Lake Store.</span></span> <span data-ttu-id="1e7e9-113">Хранилище озера данных располагает собственными интерфейсами REST API для операций управления учетными записями.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-113">Azure Data Lake Store exposes its own REST APIs for account management operations.</span></span> <span data-ttu-id="1e7e9-114">Однако поскольку хранилище озера данных совместимо с экосистемой HDFS и Hadoop, оно поддерживает использование интерфейсов REST AP WebHDFS для выполнения операций файловой системы.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-114">However, because Data Lake Store is compatible with HDFS and Hadoop ecosystem, it supports using WebHDFS REST APIs for filesystem operations.</span></span>

> [!NOTE]
> <span data-ttu-id="1e7e9-115">Подробные сведения о поддержке hello API-интерфейса REST для хранилища Озера данных. в разделе [справочнике API REST хранилища Озера данных Azure](https://msdn.microsoft.com/library/mt693424.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e7e9-115">For detailed information on hello REST API support for Data Lake Store, see [Azure Data Lake Store REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="1e7e9-116">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="1e7e9-116">Prerequisites</span></span>
* <span data-ttu-id="1e7e9-117">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-117">**An Azure subscription**.</span></span> <span data-ttu-id="1e7e9-118">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1e7e9-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1e7e9-119">**Создание приложения Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="1e7e9-120">Использовать хранилище Озера данных приложение hello tooauthenticate hello Azure AD приложения с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-120">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="1e7e9-121">Существуют tooauthenticate различные подходы с Azure AD, которые являются **проверки подлинности для конечных пользователей** или **проверки подлинности службы для службы**.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-121">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="1e7e9-122">Инструкции и Дополнительные сведения о том, как tooauthenticate, в разделе [проверки подлинности для конечных пользователей](data-lake-store-end-user-authenticate-using-active-directory.md) или [проверки подлинности службы для службы](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="1e7e9-122">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="1e7e9-123">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="1e7e9-123">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="1e7e9-124">В этой статье используется toodemonstrate перелистывание как вызывает toomake API-интерфейса REST для учетной записи хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-124">This article uses cURL toodemonstrate how toomake REST API calls against a Data Lake Store account.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="1e7e9-125">Как выполнить аутентификацию с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1e7e9-125">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="1e7e9-126">Можно использовать два подхода tooauthenticate, с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-126">You can use two approaches tooauthenticate using Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="1e7e9-127">Проверка подлинности пользователя (интерактивная)</span><span class="sxs-lookup"><span data-stu-id="1e7e9-127">End-user authentication (interactive)</span></span>
<span data-ttu-id="1e7e9-128">В этом случае приложение hello предлагает toolog пользователя hello в и все hello операции выполняются в контексте hello hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-128">In this scenario, hello application prompts hello user toolog in and all hello operations are performed in hello context of hello user.</span></span> <span data-ttu-id="1e7e9-129">Выполните следующие шаги для проверки подлинности интерактивных hello.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-129">Perform hello following steps for interactive authentication.</span></span>

1. <span data-ttu-id="1e7e9-130">Через приложения перенаправить пользователя toohello hello, URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="1e7e9-130">Through your application, redirect hello user toohello following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="1e7e9-131">\<URI ПЕРЕНАПРАВЛЕНИЯ > должен toobe кодируется для использования в URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-131">\<REDIRECT-URI> needs toobe encoded for use in a URL.</span></span> <span data-ttu-id="1e7e9-132">Поэтому для https://localhost используйте `https%3A%2F%2Flocalhost`.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-132">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="1e7e9-133">Для целей этого учебника hello можно заменить значения заполнителей hello в URL-АДРЕСЕ hello выше и вставьте его в адресной строке веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-133">For hello purpose of this tutorial, you can replace hello placeholder values in hello URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="1e7e9-134">Будет перенаправленный tooauthenticate, с помощью Azure имени входа.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-134">You will be redirected tooauthenticate using your Azure login.</span></span> <span data-ttu-id="1e7e9-135">После успешного входа ответ hello отображается в адресной строке браузера hello.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-135">Once you successfully log in, hello response is displayed in hello browser's address bar.</span></span> <span data-ttu-id="1e7e9-136">Hello ответ будут иметь hello следующий формат:</span><span class="sxs-lookup"><span data-stu-id="1e7e9-136">hello response will be in hello following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="1e7e9-137">Захватить hello код авторизации из ответа hello.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-137">Capture hello authorization code from hello response.</span></span> <span data-ttu-id="1e7e9-138">В этом учебнике можно скопировать код авторизации hello из адресной строки hello hello веб-браузера и передайте его в hello POST запроса toohello конечную точку токена, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="1e7e9-138">For this tutorial, you can copy hello authorization code from hello address bar of hello web browser and pass it in hello POST request toohello token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="1e7e9-139">В этом случае hello \<URI ПЕРЕНАПРАВЛЕНИЯ > не должны быть закодированы.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-139">In this case, hello \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="1e7e9-140">Hello ответ — объект JSON, который содержит маркер доступа (например, `"access_token": "<ACCESS_TOKEN>"`) и токена обновления (например, `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="1e7e9-140">hello response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="1e7e9-141">Приложение использует маркер доступа hello при доступе к хранилищу Озера данных Azure и tooget токена обновления hello другой маркер доступа после истечения срока действия маркера доступа.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-141">Your application uses hello access token when accessing Azure Data Lake Store and hello refresh token tooget another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="1e7e9-142">После истечения срока действия маркера доступа hello, вы можете запросить новый токен доступа с помощью токена обновления hello, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="1e7e9-142">When hello access token expires, you can request a new access token using hello refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="1e7e9-143">Дополнительные сведения об интерактивной проверке подлинности пользователей см. в статье [Авторизация доступа к веб-приложениям с помощью OAuth 2.0 и Azure Active Directory](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e7e9-143">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="1e7e9-144">Проверка подлинности с взаимодействием между службами (неинтерактивная)</span><span class="sxs-lookup"><span data-stu-id="1e7e9-144">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="1e7e9-145">В этом случае приложение hello hello предоставляет свои собственные учетные данные tooperform hello операции.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-145">In this scenario, hello hello application provides its own credentials tooperform hello operations.</span></span> <span data-ttu-id="1e7e9-146">Для этого необходимо выдать запрос POST, как hello показанной ниже.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-146">For this, you must issue a POST request like hello one shown below.</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="1e7e9-147">Hello результат этого запроса будет включать маркер авторизации (обозначается `access-token` в выходных данных hello ниже), впоследствии будет передаваться с вызовы REST API.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-147">hello output of this request will include an authorization token (denoted by `access-token` in hello output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="1e7e9-148">Сохраните этот маркер в текстовый файл. Он потребуется в данной статье позднее.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-148">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="1e7e9-149">В этой статье используется hello **неинтерактивной** подход.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-149">This article uses hello **non-interactive** approach.</span></span> <span data-ttu-id="1e7e9-150">Дополнительные сведения о пакетном (service to service вызовов) см. в разделе [tooservice вызовы с использованием учетных данных службы](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e7e9-150">For more information on non-interactive (service-to-service calls), see [Service tooservice calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="1e7e9-151">Создание учетной записи хранения озера данных</span><span class="sxs-lookup"><span data-stu-id="1e7e9-151">Create a Data Lake Store account</span></span>
<span data-ttu-id="1e7e9-152">Эта операция зависит от hello API-интерфейса REST вызов определенных [здесь](https://msdn.microsoft.com/library/mt694078.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e7e9-152">This operation is based on hello REST API call defined [here](https://msdn.microsoft.com/library/mt694078.aspx).</span></span>

<span data-ttu-id="1e7e9-153">Используйте следующую команду перелистывание hello.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-153">Use hello following cURL command.</span></span> <span data-ttu-id="1e7e9-154">Замените **\<yourstorename>** именем своего хранилища Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-154">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

<span data-ttu-id="1e7e9-155">В hello выше команд замените \< `REDACTED` \> с маркером авторизации hello получены ранее.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-155">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span> <span data-ttu-id="1e7e9-156">Hello полезные данные запроса для этой команды, содержащиеся в hello **input.json** файл, предоставленный для hello `-d` описание параметра.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-156">hello request payload for this command is contained in hello **input.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="1e7e9-157">Hello содержимое файла input.json hello напоминают hello следующее:</span><span class="sxs-lookup"><span data-stu-id="1e7e9-157">hello contents of hello input.json file resemble hello following:</span></span>

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="1e7e9-158">Создание папок в учетной записи хранения озера данных</span><span class="sxs-lookup"><span data-stu-id="1e7e9-158">Create folders in a Data Lake Store account</span></span>
<span data-ttu-id="1e7e9-159">Эта операция зависит от hello WebHDFS REST API вызов определенных [здесь](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="1e7e9-159">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span></span>

<span data-ttu-id="1e7e9-160">Используйте следующую команду перелистывание hello.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-160">Use hello following cURL command.</span></span> <span data-ttu-id="1e7e9-161">Замените **\<yourstorename>** именем своего хранилища Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-161">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

<span data-ttu-id="1e7e9-162">В hello выше команд замените \< `REDACTED` \> с маркером авторизации hello получены ранее.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-162">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span> <span data-ttu-id="1e7e9-163">Эта команда создает каталог с именем **mytempdir** в корневой папке hello вашей учетной записи хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-163">This command creates a directory called **mytempdir** under hello root folder of your Data Lake Store account.</span></span>

<span data-ttu-id="1e7e9-164">При успешном завершении операции hello, вы увидите ответа следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1e7e9-164">You should see a response like this if hello operation completes successfully:</span></span>

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a><span data-ttu-id="1e7e9-165">Вывод списка папок в учетной записи хранения озера данных</span><span class="sxs-lookup"><span data-stu-id="1e7e9-165">List folders in a Data Lake Store account</span></span>
<span data-ttu-id="1e7e9-166">Эта операция зависит от hello WebHDFS REST API вызов определенных [здесь](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="1e7e9-166">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span></span>

<span data-ttu-id="1e7e9-167">Используйте следующую команду перелистывание hello.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-167">Use hello following cURL command.</span></span> <span data-ttu-id="1e7e9-168">Замените **\<yourstorename>** именем своего хранилища Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-168">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

<span data-ttu-id="1e7e9-169">В hello выше команд замените \< `REDACTED` \> с маркером авторизации hello получены ранее.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-169">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span>

<span data-ttu-id="1e7e9-170">При успешном завершении операции hello, вы увидите ответа следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1e7e9-170">You should see a response like this if hello operation completes successfully:</span></span>

    {
    "FileStatuses": {
        "FileStatus": [{
            "length": 0,
            "pathSuffix": "mytempdir",
            "type": "DIRECTORY",
            "blockSize": 268435456,
            "accessTime": 1458324719512,
            "modificationTime": 1458324719512,
            "replication": 0,
            "permission": "777",
            "owner": "NotSupportYet",
            "group": "NotSupportYet"
        }]
    }
    }

## <a name="upload-data-into-a-data-lake-store-account"></a><span data-ttu-id="1e7e9-171">Отправка данных в учетную запись хранения озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="1e7e9-171">Upload data into a Data Lake Store account</span></span>
<span data-ttu-id="1e7e9-172">Эта операция зависит от hello WebHDFS REST API вызов определенных [здесь](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span><span class="sxs-lookup"><span data-stu-id="1e7e9-172">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span></span>

<span data-ttu-id="1e7e9-173">Используйте следующую команду перелистывание hello.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-173">Use hello following cURL command.</span></span> <span data-ttu-id="1e7e9-174">Замените **\<yourstorename>** именем своего хранилища Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-174">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

<span data-ttu-id="1e7e9-175">В hello выше синтаксис **-T** параметр — расположение hello вы отправляете файл hello.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-175">In hello above syntax **-T** parameter is hello location of hello file you are uploading.</span></span>

<span data-ttu-id="1e7e9-176">Hello выходные данные выглядят аналогично toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="1e7e9-176">hello output is similar toohello following:</span></span>
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a><span data-ttu-id="1e7e9-177">Чтение данных из учетной записи хранения озера данных</span><span class="sxs-lookup"><span data-stu-id="1e7e9-177">Read data from a Data Lake Store account</span></span>
<span data-ttu-id="1e7e9-178">Эта операция зависит от hello WebHDFS REST API вызов определенных [здесь](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span><span class="sxs-lookup"><span data-stu-id="1e7e9-178">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span></span>

<span data-ttu-id="1e7e9-179">Процесс чтения данных из учетной записи хранения озера данных состоит из двух этапов.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-179">Reading data from a Data Lake Store account is a two-step process.</span></span>

* <span data-ttu-id="1e7e9-180">Отправке запроса GET к конечной точке hello `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-180">You first submit a GET request against hello endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span></span> <span data-ttu-id="1e7e9-181">Возвращает расположение toosubmit hello следующий запрос GET к.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-181">This will return a location toosubmit hello next GET request to.</span></span>
* <span data-ttu-id="1e7e9-182">Отправьте запрос GET hello с конечной точкой, hello `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-182">You then submit hello GET request against hello endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span></span> <span data-ttu-id="1e7e9-183">Это позволит отобразить hello содержимое файла hello.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-183">This will display hello contents of hello file.</span></span>

<span data-ttu-id="1e7e9-184">Тем не менее, так как нет никаких различий в hello входных параметров между hello сначала и hello второй шаг, вы можете использовать hello `-L` параметр toosubmit hello первого запроса.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-184">However, because there is no difference in hello input parameters between hello first and hello second step, you can use hello `-L` parameter toosubmit hello first request.</span></span> <span data-ttu-id="1e7e9-185">`-L`по существу, параметр объединяет два запроса в одну и сделает перелистывание повтора hello запрос на новое место hello.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-185">`-L` option essentially combines two requests into one and will make cURL redo hello request on hello new location.</span></span> <span data-ttu-id="1e7e9-186">Наконец, hello по всем вызовам hello запроса выводятся данные, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-186">Finally, hello output from all hello request calls is displayed, like shown below.</span></span> <span data-ttu-id="1e7e9-187">Замените **\<yourstorename>** именем своего хранилища Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-187">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

<span data-ttu-id="1e7e9-188">Вы должны увидеть следующие выходные данные как toohello.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-188">You should see an output similar toohello following:</span></span>

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="1e7e9-189">Переименование файла в учетной записи хранения озера данных</span><span class="sxs-lookup"><span data-stu-id="1e7e9-189">Rename a file in a Data Lake Store account</span></span>
<span data-ttu-id="1e7e9-190">Эта операция зависит от hello WebHDFS REST API вызов определенных [здесь](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="1e7e9-190">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span></span>

<span data-ttu-id="1e7e9-191">Используйте следующие hello cURL команда toorename файла.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-191">Use hello following cURL command toorename a file.</span></span> <span data-ttu-id="1e7e9-192">Замените **\<yourstorename>** именем своего хранилища Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-192">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

<span data-ttu-id="1e7e9-193">Вы должны увидеть следующие выходные данные как toohello.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-193">You should see an output similar toohello following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a><span data-ttu-id="1e7e9-194">Удаление файла из учетной записи хранения озера данных</span><span class="sxs-lookup"><span data-stu-id="1e7e9-194">Delete a file from a Data Lake Store account</span></span>
<span data-ttu-id="1e7e9-195">Эта операция зависит от hello WebHDFS REST API вызов определенных [здесь](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="1e7e9-195">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span></span>

<span data-ttu-id="1e7e9-196">Используйте следующие hello cURL команда toodelete файла.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-196">Use hello following cURL command toodelete a file.</span></span> <span data-ttu-id="1e7e9-197">Замените **\<yourstorename>** именем своего хранилища Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-197">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

<span data-ttu-id="1e7e9-198">Вы должны увидеть результаты hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1e7e9-198">You should see an output like hello following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="1e7e9-199">Удаление учетной записи хранения озера данных</span><span class="sxs-lookup"><span data-stu-id="1e7e9-199">Delete a Data Lake Store account</span></span>
<span data-ttu-id="1e7e9-200">Эта операция зависит от hello API-интерфейса REST вызов определенных [здесь](https://msdn.microsoft.com/library/mt694075.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e7e9-200">This operation is based on hello REST API call defined [here](https://msdn.microsoft.com/library/mt694075.aspx).</span></span>

<span data-ttu-id="1e7e9-201">Используйте следующие hello cURL toodelete команда учетной записи хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-201">Use hello following cURL command toodelete a Data Lake Store account.</span></span> <span data-ttu-id="1e7e9-202">Замените **\<yourstorename>** именем своего хранилища Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1e7e9-202">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

<span data-ttu-id="1e7e9-203">Вы должны увидеть результаты hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="1e7e9-203">You should see an output like hello following:</span></span>

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a><span data-ttu-id="1e7e9-204">См. также</span><span class="sxs-lookup"><span data-stu-id="1e7e9-204">See also</span></span>
* [<span data-ttu-id="1e7e9-205">Приложения больших данных с открытым исходным кодом, которые работают с хранилищем озера данных Azure</span><span class="sxs-lookup"><span data-stu-id="1e7e9-205">Open Source Big Data applications compatible with Azure Data Lake Store</span></span>](data-lake-store-compatible-oss-other-applications.md)

