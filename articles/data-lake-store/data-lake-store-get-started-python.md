---
title: "пакет SDK для Python tooget aaaUse hello работы с хранилища Озера данных Azure | Документы Microsoft"
description: "Узнайте, как toouse toowork пакет SDK для Python с учетными записями хранилища Озера данных и hello файловой системы."
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 75f6de6f-6fd8-48f4-8707-cb27d22d27a6
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 7061fdf25ef607608bab618a20ddd3d6fc7af01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-python"></a><span data-ttu-id="7bccd-103">Начало работы с Azure Data Lake Store с помощью Python</span><span class="sxs-lookup"><span data-stu-id="7bccd-103">Get started with Azure Data Lake Store using Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7bccd-104">Портал</span><span class="sxs-lookup"><span data-stu-id="7bccd-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="7bccd-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7bccd-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="7bccd-106">Пакет SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="7bccd-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="7bccd-107">Пакет SDK для Java</span><span class="sxs-lookup"><span data-stu-id="7bccd-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="7bccd-108">REST API</span><span class="sxs-lookup"><span data-stu-id="7bccd-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="7bccd-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="7bccd-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="7bccd-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="7bccd-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="7bccd-111">Python</span><span class="sxs-lookup"><span data-stu-id="7bccd-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="7bccd-112">Узнайте, как toouse hello Python SDK для Azure и хранилища Озера данных Azure tooperform основные операции, такие как создание папками, отправка и загрузка файлов данных и т. д. Дополнительные сведения об Azure Data Lake Store см. в [этой статье](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7bccd-112">Learn how toouse hello Python SDK for Azure and Azure Data Lake Store tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7bccd-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7bccd-113">Prerequisites</span></span>

* <span data-ttu-id="7bccd-114">**Python**.</span><span class="sxs-lookup"><span data-stu-id="7bccd-114">**Python**.</span></span> <span data-ttu-id="7bccd-115">Скачать Python можно [здесь](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="7bccd-115">You can download Python from [here](https://www.python.org/downloads/).</span></span> <span data-ttu-id="7bccd-116">В этой статье используется версия Python 3.5.2.</span><span class="sxs-lookup"><span data-stu-id="7bccd-116">This article uses Python 3.5.2.</span></span>

* <span data-ttu-id="7bccd-117">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="7bccd-117">**An Azure subscription**.</span></span> <span data-ttu-id="7bccd-118">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7bccd-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="7bccd-119">**Создание приложения Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7bccd-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="7bccd-120">Использовать хранилище Озера данных приложение hello tooauthenticate hello Azure AD приложения с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7bccd-120">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="7bccd-121">Существуют tooauthenticate различные подходы с Azure AD, которые являются **проверки подлинности для конечных пользователей** или **проверки подлинности службы для службы**.</span><span class="sxs-lookup"><span data-stu-id="7bccd-121">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="7bccd-122">Инструкции и Дополнительные сведения о том, как tooauthenticate, в разделе [проверки подлинности для конечных пользователей](data-lake-store-end-user-authenticate-using-active-directory.md) или [проверки подлинности службы для службы](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="7bccd-122">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="install-hello-modules"></a><span data-ttu-id="7bccd-123">Установка модулей hello</span><span class="sxs-lookup"><span data-stu-id="7bccd-123">Install hello modules</span></span>

<span data-ttu-id="7bccd-124">toowork с помощью Python хранилища Озера данных необходимо tooinstall три модуля.</span><span class="sxs-lookup"><span data-stu-id="7bccd-124">toowork with Data Lake Store using Python, you need tooinstall three modules.</span></span>

* <span data-ttu-id="7bccd-125">Hello `azure-mgmt-resource` модуля.</span><span class="sxs-lookup"><span data-stu-id="7bccd-125">hello `azure-mgmt-resource` module.</span></span> <span data-ttu-id="7bccd-126">Включает в себя модули Azure для Active Directory и т. д.</span><span class="sxs-lookup"><span data-stu-id="7bccd-126">This includes Azure modules for Active Directory, etc..</span></span>
* <span data-ttu-id="7bccd-127">Hello `azure-mgmt-datalake-store` модуля.</span><span class="sxs-lookup"><span data-stu-id="7bccd-127">hello `azure-mgmt-datalake-store` module.</span></span> <span data-ttu-id="7bccd-128">Сюда входят операции управления учетной записи хранилища Озера данных Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7bccd-128">This includes hello Azure Data Lake Store account management operations.</span></span> <span data-ttu-id="7bccd-129">Дополнительные сведения см. в [справочнике по модулю управления Azure Data Lake Store](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span><span class="sxs-lookup"><span data-stu-id="7bccd-129">For more information on this module, see [Azure Data Lake Store Management module reference](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span></span>
* <span data-ttu-id="7bccd-130">Hello `azure-datalake-store` модуля.</span><span class="sxs-lookup"><span data-stu-id="7bccd-130">hello `azure-datalake-store` module.</span></span> <span data-ttu-id="7bccd-131">Сюда входят операции файловой системы hello хранилища Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="7bccd-131">This includes hello Azure Data Lake Store filesystem operations.</span></span> <span data-ttu-id="7bccd-132">Дополнительные сведения см. в [справочнике по модулю файловой системы Azure Data Lake Store](http://azure-datalake-store.readthedocs.io/en/latest/).</span><span class="sxs-lookup"><span data-stu-id="7bccd-132">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span></span>

<span data-ttu-id="7bccd-133">Используйте следующие команды tooinstall hello модули hello.</span><span class="sxs-lookup"><span data-stu-id="7bccd-133">Use hello following commands tooinstall hello modules.</span></span>

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a><span data-ttu-id="7bccd-134">Создание приложения Python</span><span class="sxs-lookup"><span data-stu-id="7bccd-134">Create a new Python application</span></span>

1. <span data-ttu-id="7bccd-135">В hello IDE по своему выбору создайте новое приложение Python, например, **mysample.py**.</span><span class="sxs-lookup"><span data-stu-id="7bccd-135">In hello IDE of your choice create a new Python application, for example, **mysample.py**.</span></span>

2. <span data-ttu-id="7bccd-136">Добавьте следующие строки tooimport hello необходимые модули hello</span><span class="sxs-lookup"><span data-stu-id="7bccd-136">Add hello following lines tooimport hello required modules</span></span>

    ```
    ## Use this only for Azure AD service-to-service authentication
    from azure.common.credentials import ServicePrincipalCredentials

    ## Use this only for Azure AD end-user authentication
    from azure.common.credentials import UserPassCredentials

    ## Use this only for Azure AD multi-factor authentication
    from msrestazure.azure_active_directory import AADTokenCredentials

    ## Required for Azure Data Lake Store account management
    from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
    from azure.mgmt.datalake.store.models import DataLakeStoreAccount

    ## Required for Azure Data Lake Store filesystem management
    from azure.datalake.store import core, lib, multithread

    # Common Azure imports
    from azure.mgmt.resource.resources import ResourceManagementClient
    from azure.mgmt.resource.resources.models import ResourceGroup

    ## Use these as needed for your application
    import logging, getpass, pprint, uuid, time
    ```

3. <span data-ttu-id="7bccd-137">Сохраните изменения toomysample.py.</span><span class="sxs-lookup"><span data-stu-id="7bccd-137">Save changes toomysample.py.</span></span>

## <a name="authentication"></a><span data-ttu-id="7bccd-138">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="7bccd-138">Authentication</span></span>

<span data-ttu-id="7bccd-139">В этом разделе мы расскажем hello tooauthenticate различными способами с помощью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7bccd-139">In this section, we talk about hello different ways tooauthenticate with Azure AD.</span></span> <span data-ttu-id="7bccd-140">Hello доступные значения:</span><span class="sxs-lookup"><span data-stu-id="7bccd-140">hello options available are:</span></span>

* <span data-ttu-id="7bccd-141">Аутентификация пользователей</span><span class="sxs-lookup"><span data-stu-id="7bccd-141">End-user authentication</span></span>
* <span data-ttu-id="7bccd-142">Взаимодействие между службами</span><span class="sxs-lookup"><span data-stu-id="7bccd-142">Service-to-service authentication</span></span>
* <span data-ttu-id="7bccd-143">Многофакторная проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="7bccd-143">Multi-factor authentication</span></span>

<span data-ttu-id="7bccd-144">Эти параметры проверки подлинности необходимо использовать для управления учетными записями и для модулей управления файловой системы.</span><span class="sxs-lookup"><span data-stu-id="7bccd-144">You must use these authentication options for both account management and filesystem management modules.</span></span>

### <a name="end-user-authentication-for-account-management"></a><span data-ttu-id="7bccd-145">Проверка подлинности пользователя для управления учетными записями</span><span class="sxs-lookup"><span data-stu-id="7bccd-145">End-user authentication for account management</span></span>

<span data-ttu-id="7bccd-146">Используйте этот tooauthenticate с Azure AD для операций управления учетными записями (Создание, удаление хранилища Озера данных и т. д.).</span><span class="sxs-lookup"><span data-stu-id="7bccd-146">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="7bccd-147">Необходимо указать имя пользователя и пароль для Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7bccd-147">You must provide username and password for an Azure AD user.</span></span> <span data-ttu-id="7bccd-148">Обратите внимание, что этот пользователь hello не должны быть настроены для многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7bccd-148">Note that hello user should not be configured for multi-factor authentication.</span></span>

    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a><span data-ttu-id="7bccd-149">Проверка подлинности конечных пользователей для операций файловой системы</span><span class="sxs-lookup"><span data-stu-id="7bccd-149">End-user authentication for filesystem operations</span></span>

<span data-ttu-id="7bccd-150">Используйте этот tooauthenticate с Azure AD для операций файловой системы (создать папку, загруженный файл, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="7bccd-150">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="7bccd-151">Используйте этот метод для существующих **собственных клиентских приложений** Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7bccd-151">Use this with an existing Azure AD **native client** application.</span></span> <span data-ttu-id="7bccd-152">Укажите учетные данные для пользователя Hello Azure AD не должны быть настроены для многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7bccd-152">hello Azure AD user you provide credentials for should not be configured for multi-factor authentication.</span></span>

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a><span data-ttu-id="7bccd-153">Проверки подлинности через секрет клиента со взаимодействием между службами для управления учетными записями</span><span class="sxs-lookup"><span data-stu-id="7bccd-153">Service-to-service authentication with client secret for account management</span></span>

<span data-ttu-id="7bccd-154">Используйте этот tooauthenticate с Azure AD для операций управления учетными записями (Создание, удаление хранилища Озера данных и т. д.).</span><span class="sxs-lookup"><span data-stu-id="7bccd-154">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="7bccd-155">Здравствуйте, следующий фрагмент кода может быть используется tooauthenticate приложения не в интерактивном режиме, с помощью hello секрет клиента для приложения / службы субъекта.</span><span class="sxs-lookup"><span data-stu-id="7bccd-155">hello following snippet can be used tooauthenticate your application non-interactively, using hello client secret for an application / service principal.</span></span> <span data-ttu-id="7bccd-156">Примените этот фрагмент кода к существующему веб-приложению Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7bccd-156">Use this with an existing Azure AD "Web App" application.</span></span>

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a><span data-ttu-id="7bccd-157">Проверка подлинности между службами через секрет клиента для операций файловой системы</span><span class="sxs-lookup"><span data-stu-id="7bccd-157">Service-to-service authentication with client secret for filesystem operations</span></span>

<span data-ttu-id="7bccd-158">Используйте этот tooauthenticate с Azure AD для операций файловой системы (создать папку, загруженный файл, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="7bccd-158">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="7bccd-159">Здравствуйте, следующий фрагмент кода может быть используется tooauthenticate приложения не в интерактивном режиме, с помощью hello секрет клиента для приложения / службы субъекта.</span><span class="sxs-lookup"><span data-stu-id="7bccd-159">hello following snippet can be used tooauthenticate your application non-interactively, using hello client secret for an application / service principal.</span></span> <span data-ttu-id="7bccd-160">Примените этот фрагмент кода к существующему веб-приложению Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7bccd-160">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a><span data-ttu-id="7bccd-161">Многофакторная идентификация для управления учетными записями</span><span class="sxs-lookup"><span data-stu-id="7bccd-161">Multi-factor authentication for account management</span></span>

<span data-ttu-id="7bccd-162">Используйте этот tooauthenticate с Azure AD для операций управления учетными записями (Создание, удаление хранилища Озера данных и т. д.).</span><span class="sxs-lookup"><span data-stu-id="7bccd-162">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="7bccd-163">Hello следующий фрагмент кода можно использовать tooauthenticate приложения с помощью многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7bccd-163">hello following snippet can be used tooauthenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="7bccd-164">Примените этот фрагмент кода к существующему веб-приложению Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7bccd-164">Use this with an existing Azure AD "Web App" application.</span></span>

    authority_host_url = "https://login.microsoftonline.com"
    tenant = "FILL-IN-HERE"
    authority_url = authority_host_url + '/' + tenant
    client_id = 'FILL-IN-HERE'
    redirect = 'urn:ietf:wg:oauth:2.0:oob'
    RESOURCE = 'https://management.core.windows.net/'
    
    context = adal.AuthenticationContext(authority_url)
    code = context.acquire_user_code(RESOURCE, client_id)
    print(code['message'])
    mgmt_token = context.acquire_token_with_device_code(RESOURCE, code, client_id)
    credentials = AADTokenCredentials(mgmt_token, client_id)

### <a name="multi-factor-authentication-for-filesystem-management"></a><span data-ttu-id="7bccd-165">Многофакторная идентификация для управления файловой системой</span><span class="sxs-lookup"><span data-stu-id="7bccd-165">Multi-factor authentication for filesystem management</span></span>

<span data-ttu-id="7bccd-166">Используйте этот tooauthenticate с Azure AD для операций файловой системы (создать папку, загруженный файл, и т. д.).</span><span class="sxs-lookup"><span data-stu-id="7bccd-166">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="7bccd-167">Hello следующий фрагмент кода можно использовать tooauthenticate приложения с помощью многофакторной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="7bccd-167">hello following snippet can be used tooauthenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="7bccd-168">Примените этот фрагмент кода к существующему веб-приложению Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7bccd-168">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="7bccd-169">Создание группы ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="7bccd-169">Create an Azure Resource Group</span></span>

<span data-ttu-id="7bccd-170">Используйте следующий фрагмент кода toocreate группу ресурсов Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7bccd-170">Use hello following code snippet toocreate an Azure Resource Group:</span></span>

    ## Declare variables
    subscriptionId= 'FILL-IN-HERE'
    resourceGroup = 'FILL-IN-HERE'
    location = 'eastus2'
    
    ## Create management client object
    resourceClient = ResourceManagementClient(
        credentials,
        subscriptionId
    )
    
    ## Create an Azure Resource Group
    resourceClient.resource_groups.create_or_update(
        resourceGroup,
        ResourceGroup(
            location=location
        )
    )

## <a name="create-clients-and-data-lake-store-account"></a><span data-ttu-id="7bccd-171">Создание клиентов и учетной записи Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="7bccd-171">Create clients and Data Lake Store account</span></span>

<span data-ttu-id="7bccd-172">Привет, сначала следующий фрагмент кода создает hello хранилища Озера данных учетной записи клиента.</span><span class="sxs-lookup"><span data-stu-id="7bccd-172">hello following snippet first creates hello Data Lake Store account client.</span></span> <span data-ttu-id="7bccd-173">Она использует hello клиентского объекта toocreate учетной записи хранилища Озера данных.</span><span class="sxs-lookup"><span data-stu-id="7bccd-173">It uses hello client object toocreate a Data Lake Store account.</span></span> <span data-ttu-id="7bccd-174">Наконец hello фрагмент кода создает объект клиента файловой системы.</span><span class="sxs-lookup"><span data-stu-id="7bccd-174">Finally, hello snippet creates a filesystem client object.</span></span>

    ## Declare variables
    subscriptionId = 'FILL-IN-HERE'
    adlsAccountName = 'FILL-IN-HERE'

    ## Create management client object
    adlsAcctClient = DataLakeStoreAccountManagementClient(credentials, subscriptionId)

    ## Create a Data Lake Store account
    adlsAcctResult = adlsAcctClient.account.create(
        resourceGroup,
        adlsAccountName,
        DataLakeStoreAccount(
            location=location
        )
    ).wait()

    ## Create a filesystem client object
    adlsFileSystemClient = core.AzureDLFileSystem(token, store_name=adlsAccountName)

## <a name="list-hello-data-lake-store-accounts"></a><span data-ttu-id="7bccd-175">Список учетных записей хранилища Озера данных hello</span><span class="sxs-lookup"><span data-stu-id="7bccd-175">List hello Data Lake Store accounts</span></span>

    ## List hello existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a><span data-ttu-id="7bccd-176">Создайте каталог</span><span class="sxs-lookup"><span data-stu-id="7bccd-176">Create a directory</span></span>

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a><span data-ttu-id="7bccd-177">Отправить файл.</span><span class="sxs-lookup"><span data-stu-id="7bccd-177">Upload a file</span></span>


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a><span data-ttu-id="7bccd-178">Скачивание файла</span><span class="sxs-lookup"><span data-stu-id="7bccd-178">Download a file</span></span>

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a><span data-ttu-id="7bccd-179">Удаление каталога</span><span class="sxs-lookup"><span data-stu-id="7bccd-179">Delete a directory</span></span>

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a><span data-ttu-id="7bccd-180">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="7bccd-180">See also</span></span>

- [<span data-ttu-id="7bccd-181">Защита данных в хранилище озера данных</span><span class="sxs-lookup"><span data-stu-id="7bccd-181">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
- [<span data-ttu-id="7bccd-182">Использование аналитики озера данных Azure с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="7bccd-182">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [<span data-ttu-id="7bccd-183">Использование Azure HDInsight с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="7bccd-183">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
- [<span data-ttu-id="7bccd-184">Data Lake Store .NET Reference (Справочник по пакету SDK .NET для Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="7bccd-184">Data Lake Store .NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt581387.aspx)
- [<span data-ttu-id="7bccd-185">Data Lake Store REST Reference (Справочник по REST для Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="7bccd-185">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
