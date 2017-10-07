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
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a>Начало работы с Azure Data Lake Analytics с помощью интерфейсов REST API
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Узнайте, как toouse WebHDFS REST API и API-интерфейсы REST аналитика Озера данных toomanage аналитики Озера данных учетных записей, заданий и каталога. 

## <a name="prerequisites"></a>Предварительные требования
* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Создание приложения Azure Active Directory**. Используйте приложение аналитики Озера данных hello tooauthenticate приложения hello Azure AD с Azure AD. Существуют tooauthenticate различные подходы с Azure AD, которые являются **проверки подлинности для конечных пользователей** или **проверки подлинности службы для службы**. Инструкции и Дополнительные сведения о том, как tooauthenticate, в разделе [аутентификация с помощью аналитики Озера данных Azure Active Directory с помощью](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).
* [cURL](http://curl.haxx.se/). В этой статье используется toodemonstrate перелистывание как вызывает toomake API-интерфейса REST для учетной записи аналитики Озера данных.

## <a name="authenticate-with-azure-active-directory"></a>Проверка подлинности с помощью Azure Active Directory
Существует два метода проверки подлинности с помощью Azure Active Directory.

### <a name="end-user-authentication-interactive"></a>Проверка подлинности пользователя (интерактивная)
При использовании этого метода приложение запрашивает toolog пользователя hello в, и все hello операции выполняются в контексте hello hello пользователя. 

Выполните приведенные ниже действия, чтобы использовать интерактивную проверку подлинности.

1. Через приложения перенаправить пользователя toohello hello, URL-адреса:
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > \<URI ПЕРЕНАПРАВЛЕНИЯ > должен toobe кодируется для использования в URL-адрес. Поэтому для https://localhost используйте `https%3A%2F%2Flocalhost`.
   > 
   > 
   
    Для целей этого учебника hello можно заменить значения заполнителей hello в URL-АДРЕСЕ hello выше и вставьте его в адресной строке веб-браузера. Будет перенаправленный tooauthenticate, с помощью Azure имени входа. После входа в систему можно успешно hello ответ отображается в адресной строке браузера hello. Hello ответ будут иметь hello следующий формат:
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. Захватить hello код авторизации из ответа hello. В этом учебнике можно скопировать код авторизации hello из адресной строки hello hello веб-браузера и передайте его в hello POST запроса toohello конечную точку токена, как показано ниже:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > В этом случае hello \<URI ПЕРЕНАПРАВЛЕНИЯ > не должны быть закодированы.
   > 
   > 
3. Hello ответ — объект JSON, который содержит маркер доступа (например, `"access_token": "<ACCESS_TOKEN>"`) и токена обновления (например, `"refresh_token": "<REFRESH_TOKEN>"`). Приложение использует маркер доступа hello при доступе к хранилищу Озера данных Azure и tooget токена обновления hello другой маркер доступа после истечения срока действия маркера доступа.
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. После истечения срока действия маркера доступа hello, вы можете запросить новый токен доступа с помощью токена обновления hello, как показано ниже:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

Дополнительные сведения об интерактивной проверке подлинности пользователей см. в статье [Авторизация доступа к веб-приложениям с помощью OAuth 2.0 и Azure Active Directory](https://msdn.microsoft.com/library/azure/dn645542.aspx).

### <a name="service-to-service-authentication-non-interactive"></a>Проверка подлинности с взаимодействием между службами (неинтерактивная)
При использовании этого метода приложение предоставляет свои собственные учетные данные tooperform hello операции. Для этого необходимо выдать запрос POST, как hello приведенное ниже: 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

Hello результат этого запроса будет включать маркер авторизации (обозначается `access-token` в выходных данных hello ниже), впоследствии будет передаваться с вызовы REST API. Сохраните этот маркер в текстовый файл. Он потребуется в данной статье позднее.

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

В этой статье используется hello **неинтерактивной** подход. Дополнительные сведения о пакетном (service to service вызовов) см. в разделе [tooservice вызовы с использованием учетных данных службы](https://msdn.microsoft.com/library/azure/dn645543.aspx).

## <a name="create-a-data-lake-analytics-account"></a>Создание учетной записи аналитики озера данных
Перед тем как создать учетную запись Data Lake Analytics, необходимо создать группу ресурсов Azure и учетную запись Data Lake Store.  Дополнительные сведения см. в разделе [Создание учетной записи Data Lake Store](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).

Здравствуйте, следующая команда показывает перелистывание как toocreate учетной записи:

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

Замените \< `REDACTED` \> маркером авторизации hello \< `AzureSubscriptionID` \> своим Идентификатором подписки, \< `AzureResourceGroupName` \> с существующим ресурсом Azure Имя группы и \< `NewAzureDataLakeAnalyticsAccountName` \> с новым именем учетной записи аналитики Озера данных. Hello полезные данные запроса для этой команды, содержащиеся в hello **CreateDatalakeAnalyticsAccountRequest.json** файл, предоставленный для hello `-d` описание параметра. Hello содержимое файла input.json hello напоминают hello следующее:

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


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a>Список учетных записей Data Lake Analytics в подписке
Hello следующую команду Curl показано, как toolist учетные записи в подписке.

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

Замените \< `REDACTED` \> маркером авторизации hello \< `AzureSubscriptionID` \> вашим идентификатором подписки. Hello выходные данные выглядят аналогично:

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

## <a name="get-information-about-a-data-lake-analytics-account"></a>Получение сведений об учетной записи Data Lake Analytics
Здравствуйте, следующая команда показывает перелистывание как tooget сведения об учетной записи:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

Замените \< `REDACTED` \> маркером авторизации hello \< `AzureSubscriptionID` \> своим Идентификатором подписки, \< `AzureResourceGroupName` \> с существующим ресурсом Azure Имя группы и \< `DataLakeAnalyticsAccountName` \> с именем hello существующей учетной записи аналитики Озера данных. Hello выходные данные выглядят аналогично:

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

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a>Список хранилищ Data Lake Store учетной записи Data Lake Analytics
Hello следующую команду Curl показано, как toolist Озера данных хранятся в учетной записи:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

Замените \< `REDACTED` \> маркером авторизации hello \< `AzureSubscriptionID` \> своим Идентификатором подписки, \< `AzureResourceGroupName` \> с существующим ресурсом Azure Имя группы и \< `DataLakeAnalyticsAccountName` \> с именем hello существующей учетной записи аналитики Озера данных. Hello выходные данные выглядят аналогично:

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

## <a name="submit-u-sql-jobs"></a>Отправка заданий U-SQL
Здравствуйте, следующая команда показывает перелистывание как задание toosubmit U-SQL:

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

Замените \< `REDACTED` \> маркером авторизации hello \< `DataLakeAnalyticsAccountName` \> с именем hello существующей учетной записи аналитики Озера данных. Hello полезные данные запроса для этой команды, содержащиеся в hello **SubmitADLAJob.json** файл, предоставленный для hello `-d` описание параметра. Hello содержимое файла input.json hello напоминают hello следующее:

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

Hello выходные данные выглядят аналогично:

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


## <a name="list-u-sql-jobs"></a>Получение списка заданий U-SQL
Здравствуйте, следующая команда показывает перелистывание как задания toolist U-SQL:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

Замените \< `REDACTED` \> маркером авторизации hello и \< `DataLakeAnalyticsAccountName` \> с именем hello существующей учетной записи аналитики Озера данных. 

Hello выходные данные выглядят аналогично:

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


## <a name="get-catalog-items"></a>Получение элементов каталога
Hello следующую команду Curl показано, как базы данных hello tooget от hello каталога:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

Hello выходные данные выглядят аналогично:

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a>См. также
* в разделе toosee более сложный запрос, [веб-сайта анализ журналов с помощью аналитики Озера данных Azure](data-lake-analytics-analyze-weblogs.md).
* tooget к разработке приложений U-SQL, в разделе [сценариев разработки U-SQL, с помощью средства Озера данных для Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
* в разделе toolearn U-SQL [Приступая к работе с Azure аналитика Озера данных U-SQL языка](data-lake-analytics-u-sql-get-started.md).
* Задачи управления описываются в руководстве по [управлению Azure Data Lake Analytics с помощью портала Azure](data-lake-analytics-manage-use-portal.md).
* в разделе tooget содержится обзор аналитики Озера данных, [Обзор аналитики Озера данных Azure](data-lake-analytics-overview.md).
* toosee hello же учебника при помощи других средств, щелкните селекторы вкладку hello на hello вверху страницы приветствия.

