---
title: "Начало работы с Azure Data Lake Store с помощью пакета Python SDK | Документация Майкрософт"
description: "Узнайте, как использовать пакет Python SDK для работы с учетными записями и файловой системой Data Lake Store."
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
ms.openlocfilehash: 375a603360ac249fc1b08923a94c85652390a3fc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-python"></a><span data-ttu-id="4e8be-103">Начало работы с Azure Data Lake Store с помощью Python</span><span class="sxs-lookup"><span data-stu-id="4e8be-103">Get started with Azure Data Lake Store using Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4e8be-104">Портал</span><span class="sxs-lookup"><span data-stu-id="4e8be-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="4e8be-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e8be-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="4e8be-106">Пакет SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="4e8be-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="4e8be-107">Пакет SDK для Java</span><span class="sxs-lookup"><span data-stu-id="4e8be-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="4e8be-108">REST API</span><span class="sxs-lookup"><span data-stu-id="4e8be-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="4e8be-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="4e8be-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="4e8be-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="4e8be-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="4e8be-111">Python</span><span class="sxs-lookup"><span data-stu-id="4e8be-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="4e8be-112">Узнайте, как с помощью пакета Python SDK для Azure Data Lake Store выполнять базовые операции, такие как создание папок, отправка и скачивание файлов данных и т. д. Дополнительные сведения об Azure Data Lake Store см. в [этой статье](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4e8be-112">Learn how to use the Python SDK for Azure and Azure Data Lake Store to perform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e8be-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4e8be-113">Prerequisites</span></span>

* <span data-ttu-id="4e8be-114">**Python**.</span><span class="sxs-lookup"><span data-stu-id="4e8be-114">**Python**.</span></span> <span data-ttu-id="4e8be-115">Скачать Python можно [здесь](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="4e8be-115">You can download Python from [here](https://www.python.org/downloads/).</span></span> <span data-ttu-id="4e8be-116">В этой статье используется версия Python 3.5.2.</span><span class="sxs-lookup"><span data-stu-id="4e8be-116">This article uses Python 3.5.2.</span></span>

* <span data-ttu-id="4e8be-117">**Подписка Azure**.</span><span class="sxs-lookup"><span data-stu-id="4e8be-117">**An Azure subscription**.</span></span> <span data-ttu-id="4e8be-118">Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4e8be-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="4e8be-119">**Создание приложения Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4e8be-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="4e8be-120">Это приложение будет использоваться для проверки подлинности приложения Data Lake Store в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e8be-120">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="4e8be-121">Есть разные способы проверки подлинности приложения с помощью Azure AD: **проверка подлинности пользователя** и **проверка подлинности со взаимодействием между службами**.</span><span class="sxs-lookup"><span data-stu-id="4e8be-121">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="4e8be-122">Инструкции и дополнительные сведения об аутентификации см. в разделах [Аутентификация пользователей](data-lake-store-end-user-authenticate-using-active-directory.md) и [Аутентификация между службами](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="4e8be-122">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="install-the-modules"></a><span data-ttu-id="4e8be-123">Установка модулей</span><span class="sxs-lookup"><span data-stu-id="4e8be-123">Install the modules</span></span>

<span data-ttu-id="4e8be-124">Для работы с Data Lake Store с использованием Python необходимо установить три модуля.</span><span class="sxs-lookup"><span data-stu-id="4e8be-124">To work with Data Lake Store using Python, you need to install three modules.</span></span>

* <span data-ttu-id="4e8be-125">Модуль `azure-mgmt-resource`.</span><span class="sxs-lookup"><span data-stu-id="4e8be-125">The `azure-mgmt-resource` module.</span></span> <span data-ttu-id="4e8be-126">Включает в себя модули Azure для Active Directory и т. д.</span><span class="sxs-lookup"><span data-stu-id="4e8be-126">This includes Azure modules for Active Directory, etc..</span></span>
* <span data-ttu-id="4e8be-127">Модуль `azure-mgmt-datalake-store`.</span><span class="sxs-lookup"><span data-stu-id="4e8be-127">The `azure-mgmt-datalake-store` module.</span></span> <span data-ttu-id="4e8be-128">Включает в себя операции по управлению учетной записью Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4e8be-128">This includes the Azure Data Lake Store account management operations.</span></span> <span data-ttu-id="4e8be-129">Дополнительные сведения см. в [справочнике по модулю управления Azure Data Lake Store](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span><span class="sxs-lookup"><span data-stu-id="4e8be-129">For more information on this module, see [Azure Data Lake Store Management module reference](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span></span>
* <span data-ttu-id="4e8be-130">Модуль `azure-datalake-store`.</span><span class="sxs-lookup"><span data-stu-id="4e8be-130">The `azure-datalake-store` module.</span></span> <span data-ttu-id="4e8be-131">Включает в себя операции по управлению файловой системой Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4e8be-131">This includes the Azure Data Lake Store filesystem operations.</span></span> <span data-ttu-id="4e8be-132">Дополнительные сведения см. в [справочнике по модулю файловой системы Azure Data Lake Store](http://azure-datalake-store.readthedocs.io/en/latest/).</span><span class="sxs-lookup"><span data-stu-id="4e8be-132">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span></span>

<span data-ttu-id="4e8be-133">Чтобы установить модули, используйте следующие команды.</span><span class="sxs-lookup"><span data-stu-id="4e8be-133">Use the following commands to install the modules.</span></span>

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a><span data-ttu-id="4e8be-134">Создание приложения Python</span><span class="sxs-lookup"><span data-stu-id="4e8be-134">Create a new Python application</span></span>

1. <span data-ttu-id="4e8be-135">Для создания приложения Python используйте IDE по своему усмотрению, например **mysample.py**.</span><span class="sxs-lookup"><span data-stu-id="4e8be-135">In the IDE of your choice create a new Python application, for example, **mysample.py**.</span></span>

2. <span data-ttu-id="4e8be-136">Чтобы импортировать необходимые модули, добавьте следующие строки.</span><span class="sxs-lookup"><span data-stu-id="4e8be-136">Add the following lines to import the required modules</span></span>

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

3. <span data-ttu-id="4e8be-137">Сохраните изменения в mysample.py.</span><span class="sxs-lookup"><span data-stu-id="4e8be-137">Save changes to mysample.py.</span></span>

## <a name="authentication"></a><span data-ttu-id="4e8be-138">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="4e8be-138">Authentication</span></span>

<span data-ttu-id="4e8be-139">В этом разделе мы рассмотрим различные способы проверки подлинности в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e8be-139">In this section, we talk about the different ways to authenticate with Azure AD.</span></span> <span data-ttu-id="4e8be-140">Доступны следующие варианты.</span><span class="sxs-lookup"><span data-stu-id="4e8be-140">The options available are:</span></span>

* <span data-ttu-id="4e8be-141">Аутентификация пользователей</span><span class="sxs-lookup"><span data-stu-id="4e8be-141">End-user authentication</span></span>
* <span data-ttu-id="4e8be-142">Взаимодействие между службами</span><span class="sxs-lookup"><span data-stu-id="4e8be-142">Service-to-service authentication</span></span>
* <span data-ttu-id="4e8be-143">Многофакторная проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="4e8be-143">Multi-factor authentication</span></span>

<span data-ttu-id="4e8be-144">Эти параметры проверки подлинности необходимо использовать для управления учетными записями и для модулей управления файловой системы.</span><span class="sxs-lookup"><span data-stu-id="4e8be-144">You must use these authentication options for both account management and filesystem management modules.</span></span>

### <a name="end-user-authentication-for-account-management"></a><span data-ttu-id="4e8be-145">Проверка подлинности пользователя для управления учетными записями</span><span class="sxs-lookup"><span data-stu-id="4e8be-145">End-user authentication for account management</span></span>

<span data-ttu-id="4e8be-146">Используйте этот метод проверки подлинности в Azure AD для операций управления учетными записями (создание, удаление учетной записи Data Lake Store и т. п.).</span><span class="sxs-lookup"><span data-stu-id="4e8be-146">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="4e8be-147">Необходимо указать имя пользователя и пароль для Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e8be-147">You must provide username and password for an Azure AD user.</span></span> <span data-ttu-id="4e8be-148">Обратите внимание, что для пользователей не следует настраивать многофакторную идентификацию.</span><span class="sxs-lookup"><span data-stu-id="4e8be-148">Note that the user should not be configured for multi-factor authentication.</span></span>

    user = input('Enter the user to authenticate with that has permission to subscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a><span data-ttu-id="4e8be-149">Проверка подлинности конечных пользователей для операций файловой системы</span><span class="sxs-lookup"><span data-stu-id="4e8be-149">End-user authentication for filesystem operations</span></span>

<span data-ttu-id="4e8be-150">Используется для проверки подлинности в Azure AD для операций файловой системы (создание папки, отправка файла и т. д.).</span><span class="sxs-lookup"><span data-stu-id="4e8be-150">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="4e8be-151">Используйте этот метод для существующих **собственных клиентских приложений** Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e8be-151">Use this with an existing Azure AD **native client** application.</span></span> <span data-ttu-id="4e8be-152">Для пользователя Azure AD, учетные данные которого вы используете, не должна быть настроена многофакторная идентификация.</span><span class="sxs-lookup"><span data-stu-id="4e8be-152">The Azure AD user you provide credentials for should not be configured for multi-factor authentication.</span></span>

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter the user to authenticate with that has permission to subscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a><span data-ttu-id="4e8be-153">Проверки подлинности через секрет клиента со взаимодействием между службами для управления учетными записями</span><span class="sxs-lookup"><span data-stu-id="4e8be-153">Service-to-service authentication with client secret for account management</span></span>

<span data-ttu-id="4e8be-154">Используйте этот метод проверки подлинности в Azure AD для операций управления учетными записями (создание, удаление учетной записи Data Lake Store и т. п.).</span><span class="sxs-lookup"><span data-stu-id="4e8be-154">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="4e8be-155">Следующий фрагмент можно использовать для проверки подлинности приложения в неинтерактивном режиме с помощью секрета клиента или субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="4e8be-155">The following snippet can be used to authenticate your application non-interactively, using the client secret for an application / service principal.</span></span> <span data-ttu-id="4e8be-156">Примените этот фрагмент кода к существующему веб-приложению Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e8be-156">Use this with an existing Azure AD "Web App" application.</span></span>

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a><span data-ttu-id="4e8be-157">Проверка подлинности между службами через секрет клиента для операций файловой системы</span><span class="sxs-lookup"><span data-stu-id="4e8be-157">Service-to-service authentication with client secret for filesystem operations</span></span>

<span data-ttu-id="4e8be-158">Используется для проверки подлинности в Azure AD для операций файловой системы (создание папки, отправка файла и т. д.).</span><span class="sxs-lookup"><span data-stu-id="4e8be-158">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="4e8be-159">Следующий фрагмент можно использовать для проверки подлинности приложения в неинтерактивном режиме с помощью секрета клиента или субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="4e8be-159">The following snippet can be used to authenticate your application non-interactively, using the client secret for an application / service principal.</span></span> <span data-ttu-id="4e8be-160">Примените этот фрагмент кода к существующему веб-приложению Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e8be-160">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a><span data-ttu-id="4e8be-161">Многофакторная идентификация для управления учетными записями</span><span class="sxs-lookup"><span data-stu-id="4e8be-161">Multi-factor authentication for account management</span></span>

<span data-ttu-id="4e8be-162">Используйте этот метод проверки подлинности в Azure AD для операций управления учетными записями (создание, удаление учетной записи Data Lake Store и т. п.).</span><span class="sxs-lookup"><span data-stu-id="4e8be-162">Use this to authenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="4e8be-163">Следующий фрагмент кода можно использовать для проверки подлинности приложения с помощью многофакторной идентификации.</span><span class="sxs-lookup"><span data-stu-id="4e8be-163">The following snippet can be used to authenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="4e8be-164">Примените этот фрагмент кода к существующему веб-приложению Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e8be-164">Use this with an existing Azure AD "Web App" application.</span></span>

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

### <a name="multi-factor-authentication-for-filesystem-management"></a><span data-ttu-id="4e8be-165">Многофакторная идентификация для управления файловой системой</span><span class="sxs-lookup"><span data-stu-id="4e8be-165">Multi-factor authentication for filesystem management</span></span>

<span data-ttu-id="4e8be-166">Используется для проверки подлинности в Azure AD для операций файловой системы (создание папки, отправка файла и т. д.).</span><span class="sxs-lookup"><span data-stu-id="4e8be-166">Use this to authenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="4e8be-167">Следующий фрагмент кода можно использовать для проверки подлинности приложения с помощью многофакторной идентификации.</span><span class="sxs-lookup"><span data-stu-id="4e8be-167">The following snippet can be used to authenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="4e8be-168">Примените этот фрагмент кода к существующему веб-приложению Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4e8be-168">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="4e8be-169">Создание группы ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="4e8be-169">Create an Azure Resource Group</span></span>

<span data-ttu-id="4e8be-170">Чтобы создать группу ресурсов Azure, используйте следующий фрагмент кода.</span><span class="sxs-lookup"><span data-stu-id="4e8be-170">Use the following code snippet to create an Azure Resource Group:</span></span>

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

## <a name="create-clients-and-data-lake-store-account"></a><span data-ttu-id="4e8be-171">Создание клиентов и учетной записи Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4e8be-171">Create clients and Data Lake Store account</span></span>

<span data-ttu-id="4e8be-172">Следующий фрагмент кода сначала создает клиент учетной записи Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4e8be-172">The following snippet first creates the Data Lake Store account client.</span></span> <span data-ttu-id="4e8be-173">Затем он использует объект клиента для создания учетной записи Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4e8be-173">It uses the client object to create a Data Lake Store account.</span></span> <span data-ttu-id="4e8be-174">И наконец, он создает объект клиента файловой системы.</span><span class="sxs-lookup"><span data-stu-id="4e8be-174">Finally, the snippet creates a filesystem client object.</span></span>

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

## <a name="list-the-data-lake-store-accounts"></a><span data-ttu-id="4e8be-175">Получение списка учетных записей Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4e8be-175">List the Data Lake Store accounts</span></span>

    ## List the existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a><span data-ttu-id="4e8be-176">Создайте каталог</span><span class="sxs-lookup"><span data-stu-id="4e8be-176">Create a directory</span></span>

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a><span data-ttu-id="4e8be-177">Отправить файл.</span><span class="sxs-lookup"><span data-stu-id="4e8be-177">Upload a file</span></span>


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a><span data-ttu-id="4e8be-178">Скачивание файла</span><span class="sxs-lookup"><span data-stu-id="4e8be-178">Download a file</span></span>

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a><span data-ttu-id="4e8be-179">Удаление каталога</span><span class="sxs-lookup"><span data-stu-id="4e8be-179">Delete a directory</span></span>

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a><span data-ttu-id="4e8be-180">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="4e8be-180">See also</span></span>

- [<span data-ttu-id="4e8be-181">Защита данных в хранилище озера данных</span><span class="sxs-lookup"><span data-stu-id="4e8be-181">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
- [<span data-ttu-id="4e8be-182">Использование аналитики озера данных Azure с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="4e8be-182">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [<span data-ttu-id="4e8be-183">Использование Azure HDInsight с хранилищем озера данных</span><span class="sxs-lookup"><span data-stu-id="4e8be-183">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
- [<span data-ttu-id="4e8be-184">Data Lake Store .NET Reference (Справочник по пакету SDK .NET для Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="4e8be-184">Data Lake Store .NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt581387.aspx)
- [<span data-ttu-id="4e8be-185">Data Lake Store REST Reference (Справочник по REST для Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="4e8be-185">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
