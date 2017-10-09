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
# <a name="get-started-with-azure-data-lake-store-using-python"></a>Начало работы с Azure Data Lake Store с помощью Python

> [!div class="op_single_selector"]
> * [Портал](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [Пакет SDK для .NET](data-lake-store-get-started-net-sdk.md)
> * [Пакет SDK для Java](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Узнайте, как toouse hello Python SDK для Azure и хранилища Озера данных Azure tooperform основные операции, такие как создание папками, отправка и загрузка файлов данных и т. д. Дополнительные сведения об Azure Data Lake Store см. в [этой статье](data-lake-store-overview.md).

## <a name="prerequisites"></a>Предварительные требования

* **Python**. Скачать Python можно [здесь](https://www.python.org/downloads/). В этой статье используется версия Python 3.5.2.

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Создание приложения Azure Active Directory**. Использовать хранилище Озера данных приложение hello tooauthenticate hello Azure AD приложения с Azure AD. Существуют tooauthenticate различные подходы с Azure AD, которые являются **проверки подлинности для конечных пользователей** или **проверки подлинности службы для службы**. Инструкции и Дополнительные сведения о том, как tooauthenticate, в разделе [проверки подлинности для конечных пользователей](data-lake-store-end-user-authenticate-using-active-directory.md) или [проверки подлинности службы для службы](data-lake-store-authenticate-using-active-directory.md).

## <a name="install-hello-modules"></a>Установка модулей hello

toowork с помощью Python хранилища Озера данных необходимо tooinstall три модуля.

* Hello `azure-mgmt-resource` модуля. Включает в себя модули Azure для Active Directory и т. д.
* Hello `azure-mgmt-datalake-store` модуля. Сюда входят операции управления учетной записи хранилища Озера данных Azure hello. Дополнительные сведения см. в [справочнике по модулю управления Azure Data Lake Store](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).
* Hello `azure-datalake-store` модуля. Сюда входят операции файловой системы hello хранилища Озера данных Azure. Дополнительные сведения см. в [справочнике по модулю файловой системы Azure Data Lake Store](http://azure-datalake-store.readthedocs.io/en/latest/).

Используйте следующие команды tooinstall hello модули hello.

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a>Создание приложения Python

1. В hello IDE по своему выбору создайте новое приложение Python, например, **mysample.py**.

2. Добавьте следующие строки tooimport hello необходимые модули hello

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

3. Сохраните изменения toomysample.py.

## <a name="authentication"></a>Аутентификация

В этом разделе мы расскажем hello tooauthenticate различными способами с помощью Azure AD. Hello доступные значения:

* Аутентификация пользователей
* Взаимодействие между службами
* Многофакторная проверка подлинности

Эти параметры проверки подлинности необходимо использовать для управления учетными записями и для модулей управления файловой системы.

### <a name="end-user-authentication-for-account-management"></a>Проверка подлинности пользователя для управления учетными записями

Используйте этот tooauthenticate с Azure AD для операций управления учетными записями (Создание, удаление хранилища Озера данных и т. д.). Необходимо указать имя пользователя и пароль для Azure AD. Обратите внимание, что этот пользователь hello не должны быть настроены для многофакторной проверки подлинности.

    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a>Проверка подлинности конечных пользователей для операций файловой системы

Используйте этот tooauthenticate с Azure AD для операций файловой системы (создать папку, загруженный файл, и т. д.). Используйте этот метод для существующих **собственных клиентских приложений** Azure AD. Укажите учетные данные для пользователя Hello Azure AD не должны быть настроены для многофакторной проверки подлинности.

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a>Проверки подлинности через секрет клиента со взаимодействием между службами для управления учетными записями

Используйте этот tooauthenticate с Azure AD для операций управления учетными записями (Создание, удаление хранилища Озера данных и т. д.). Здравствуйте, следующий фрагмент кода может быть используется tooauthenticate приложения не в интерактивном режиме, с помощью hello секрет клиента для приложения / службы субъекта. Примените этот фрагмент кода к существующему веб-приложению Azure AD.

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a>Проверка подлинности между службами через секрет клиента для операций файловой системы

Используйте этот tooauthenticate с Azure AD для операций файловой системы (создать папку, загруженный файл, и т. д.). Здравствуйте, следующий фрагмент кода может быть используется tooauthenticate приложения не в интерактивном режиме, с помощью hello секрет клиента для приложения / службы субъекта. Примените этот фрагмент кода к существующему веб-приложению Azure AD.

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a>Многофакторная идентификация для управления учетными записями

Используйте этот tooauthenticate с Azure AD для операций управления учетными записями (Создание, удаление хранилища Озера данных и т. д.). Hello следующий фрагмент кода можно использовать tooauthenticate приложения с помощью многофакторной проверки подлинности. Примените этот фрагмент кода к существующему веб-приложению Azure AD.

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

### <a name="multi-factor-authentication-for-filesystem-management"></a>Многофакторная идентификация для управления файловой системой

Используйте этот tooauthenticate с Azure AD для операций файловой системы (создать папку, загруженный файл, и т. д.). Hello следующий фрагмент кода можно использовать tooauthenticate приложения с помощью многофакторной проверки подлинности. Примените этот фрагмент кода к существующему веб-приложению Azure AD.

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a>Создание группы ресурсов Azure

Используйте следующий фрагмент кода toocreate группу ресурсов Azure hello.

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

## <a name="create-clients-and-data-lake-store-account"></a>Создание клиентов и учетной записи Data Lake Store

Привет, сначала следующий фрагмент кода создает hello хранилища Озера данных учетной записи клиента. Она использует hello клиентского объекта toocreate учетной записи хранилища Озера данных. Наконец hello фрагмент кода создает объект клиента файловой системы.

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

## <a name="list-hello-data-lake-store-accounts"></a>Список учетных записей хранилища Озера данных hello

    ## List hello existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a>Создайте каталог

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a>Отправить файл.


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a>Скачивание файла

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a>Удаление каталога

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a>Дополнительные материалы

- [Защита данных в хранилище озера данных](data-lake-store-secure-data.md)
- [Использование аналитики озера данных Azure с хранилищем озера данных](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [Использование Azure HDInsight с хранилищем озера данных](data-lake-store-hdinsight-hadoop-use-portal.md)
- [Data Lake Store .NET Reference (Справочник по пакету SDK .NET для Data Lake Store)](https://msdn.microsoft.com/library/mt581387.aspx)
- [Data Lake Store REST Reference (Справочник по REST для Data Lake Store)](https://msdn.microsoft.com/library/mt693424.aspx)
