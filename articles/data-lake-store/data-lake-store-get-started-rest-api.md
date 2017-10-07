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
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a>Начало работы с хранилищем озера данных Azure с помощью интерфейсов REST API
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

В этой статье вы узнаете, как toouse WebHDFS интерфейсы API REST и API REST хранилища Озера данных tooperform учетной записи управления, а также операций файловой системы в хранилище Озера данных Azure. Хранилище озера данных располагает собственными интерфейсами REST API для операций управления учетными записями. Однако поскольку хранилище озера данных совместимо с экосистемой HDFS и Hadoop, оно поддерживает использование интерфейсов REST AP WebHDFS для выполнения операций файловой системы.

> [!NOTE]
> Подробные сведения о поддержке hello API-интерфейса REST для хранилища Озера данных. в разделе [справочнике API REST хранилища Озера данных Azure](https://msdn.microsoft.com/library/mt693424.aspx).
> 
> 

## <a name="prerequisites"></a>Предварительные требования
* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Создание приложения Azure Active Directory**. Использовать хранилище Озера данных приложение hello tooauthenticate hello Azure AD приложения с Azure AD. Существуют tooauthenticate различные подходы с Azure AD, которые являются **проверки подлинности для конечных пользователей** или **проверки подлинности службы для службы**. Инструкции и Дополнительные сведения о том, как tooauthenticate, в разделе [проверки подлинности для конечных пользователей](data-lake-store-end-user-authenticate-using-active-directory.md) или [проверки подлинности службы для службы](data-lake-store-authenticate-using-active-directory.md).
* [cURL](http://curl.haxx.se/). В этой статье используется toodemonstrate перелистывание как вызывает toomake API-интерфейса REST для учетной записи хранилища Озера данных.

## <a name="how-do-i-authenticate-using-azure-active-directory"></a>Как выполнить аутентификацию с помощью Azure Active Directory?
Можно использовать два подхода tooauthenticate, с помощью Azure Active Directory.

### <a name="end-user-authentication-interactive"></a>Проверка подлинности пользователя (интерактивная)
В этом случае приложение hello предлагает toolog пользователя hello в и все hello операции выполняются в контексте hello hello пользователя. Выполните следующие шаги для проверки подлинности интерактивных hello.

1. Через приложения перенаправить пользователя toohello hello, URL-адреса:
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > \<URI ПЕРЕНАПРАВЛЕНИЯ > должен toobe кодируется для использования в URL-адрес. Поэтому для https://localhost используйте `https%3A%2F%2Flocalhost`.
   > 
   > 
   
    Для целей этого учебника hello можно заменить значения заполнителей hello в URL-АДРЕСЕ hello выше и вставьте его в адресной строке веб-браузера. Будет перенаправленный tooauthenticate, с помощью Azure имени входа. После успешного входа ответ hello отображается в адресной строке браузера hello. Hello ответ будут иметь hello следующий формат:
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. Захватить hello код авторизации из ответа hello. В этом учебнике можно скопировать код авторизации hello из адресной строки hello hello веб-браузера и передайте его в hello POST запроса toohello конечную точку токена, как показано ниже:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
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
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

Дополнительные сведения об интерактивной проверке подлинности пользователей см. в статье [Авторизация доступа к веб-приложениям с помощью OAuth 2.0 и Azure Active Directory](https://msdn.microsoft.com/library/azure/dn645542.aspx).

### <a name="service-to-service-authentication-non-interactive"></a>Проверка подлинности с взаимодействием между службами (неинтерактивная)
В этом случае приложение hello hello предоставляет свои собственные учетные данные tooperform hello операции. Для этого необходимо выдать запрос POST, как hello показанной ниже. 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

Hello результат этого запроса будет включать маркер авторизации (обозначается `access-token` в выходных данных hello ниже), впоследствии будет передаваться с вызовы REST API. Сохраните этот маркер в текстовый файл. Он потребуется в данной статье позднее.

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

В этой статье используется hello **неинтерактивной** подход. Дополнительные сведения о пакетном (service to service вызовов) см. в разделе [tooservice вызовы с использованием учетных данных службы](https://msdn.microsoft.com/library/azure/dn645543.aspx).

## <a name="create-a-data-lake-store-account"></a>Создание учетной записи хранения озера данных
Эта операция зависит от hello API-интерфейса REST вызов определенных [здесь](https://msdn.microsoft.com/library/mt694078.aspx).

Используйте следующую команду перелистывание hello. Замените **\<yourstorename>** именем своего хранилища Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

В hello выше команд замените \< `REDACTED` \> с маркером авторизации hello получены ранее. Hello полезные данные запроса для этой команды, содержащиеся в hello **input.json** файл, предоставленный для hello `-d` описание параметра. Hello содержимое файла input.json hello напоминают hello следующее:

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a>Создание папок в учетной записи хранения озера данных
Эта операция зависит от hello WebHDFS REST API вызов определенных [здесь](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).

Используйте следующую команду перелистывание hello. Замените **\<yourstorename>** именем своего хранилища Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

В hello выше команд замените \< `REDACTED` \> с маркером авторизации hello получены ранее. Эта команда создает каталог с именем **mytempdir** в корневой папке hello вашей учетной записи хранилища Озера данных.

При успешном завершении операции hello, вы увидите ответа следующим образом:

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a>Вывод списка папок в учетной записи хранения озера данных
Эта операция зависит от hello WebHDFS REST API вызов определенных [здесь](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).

Используйте следующую команду перелистывание hello. Замените **\<yourstorename>** именем своего хранилища Data Lake Store.

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

В hello выше команд замените \< `REDACTED` \> с маркером авторизации hello получены ранее.

При успешном завершении операции hello, вы увидите ответа следующим образом:

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

## <a name="upload-data-into-a-data-lake-store-account"></a>Отправка данных в учетную запись хранения озера данных Azure
Эта операция зависит от hello WebHDFS REST API вызов определенных [здесь](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).

Используйте следующую команду перелистывание hello. Замените **\<yourstorename>** именем своего хранилища Data Lake Store.

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

В hello выше синтаксис **-T** параметр — расположение hello вы отправляете файл hello.

Hello выходные данные выглядят аналогично toohello следующее:
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a>Чтение данных из учетной записи хранения озера данных
Эта операция зависит от hello WebHDFS REST API вызов определенных [здесь](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).

Процесс чтения данных из учетной записи хранения озера данных состоит из двух этапов.

* Отправке запроса GET к конечной точке hello `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`. Возвращает расположение toosubmit hello следующий запрос GET к.
* Отправьте запрос GET hello с конечной точкой, hello `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`. Это позволит отобразить hello содержимое файла hello.

Тем не менее, так как нет никаких различий в hello входных параметров между hello сначала и hello второй шаг, вы можете использовать hello `-L` параметр toosubmit hello первого запроса. `-L`по существу, параметр объединяет два запроса в одну и сделает перелистывание повтора hello запрос на новое место hello. Наконец, hello по всем вызовам hello запроса выводятся данные, как показано ниже. Замените **\<yourstorename>** именем своего хранилища Data Lake Store.

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

Вы должны увидеть следующие выходные данные как toohello.

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a>Переименование файла в учетной записи хранения озера данных
Эта операция зависит от hello WebHDFS REST API вызов определенных [здесь](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).

Используйте следующие hello cURL команда toorename файла. Замените **\<yourstorename>** именем своего хранилища Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

Вы должны увидеть следующие выходные данные как toohello.

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a>Удаление файла из учетной записи хранения озера данных
Эта операция зависит от hello WebHDFS REST API вызов определенных [здесь](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).

Используйте следующие hello cURL команда toodelete файла. Замените **\<yourstorename>** именем своего хранилища Data Lake Store.

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

Вы должны увидеть результаты hello следующим образом:

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a>Удаление учетной записи хранения озера данных
Эта операция зависит от hello API-интерфейса REST вызов определенных [здесь](https://msdn.microsoft.com/library/mt694075.aspx).

Используйте следующие hello cURL toodelete команда учетной записи хранилища Озера данных. Замените **\<yourstorename>** именем своего хранилища Data Lake Store.

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

Вы должны увидеть результаты hello следующим образом:

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a>См. также
* [Приложения больших данных с открытым исходным кодом, которые работают с хранилищем озера данных Azure](data-lake-store-compatible-oss-other-applications.md)

