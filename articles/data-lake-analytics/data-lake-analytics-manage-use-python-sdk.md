---
title: "aaaManage аналитики Озера данных Azure с помощью Python | Документы Microsoft"
description: "Узнайте, как toouse Python toocreate Озера данных хранения учетную запись, а также отправки заданий. "
services: data-lake-analytics
documentationcenter: 
author: matt1883
manager: jhubbard
editor: cgronlun
ms.assetid: d4213a19-4d0f-49c9-871c-9cd6ed7cf731
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: saveenr
ms.openlocfilehash: 3c0fff155db7c4fd4e84c2562816995eb156be16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-python"></a>Управление Azure Data Lake Analytics с помощью Python

## <a name="python-versions"></a>Версии Python

* Используйте 64-разрядную версию Python.
* Можно использовать стандартные Python распространения hello в  **[загружает Python.org](https://www.python.org/downloads/)**. 
* Многим разработчикам кажутся hello удобный toouse  **[распространения Anaconda Python](https://www.continuum.io/downloads)**.  
* В этой статье было написано с помощью Python версии 3.6 от стандартного распределения Python hello

## <a name="install-azure-python-sdk"></a>Установка пакета Azure SDK для Python

Установите hello следующие модули:

* Hello **ресурсов azure-mgmt** модуль включает другие модули Azure Active Directory и т. д.
* Hello **-mgmt-datalake хранилища azure** модуль включает операции управления учетной записи хранилища Озера данных Azure hello.
* Hello **хранилища azure — datalake** модуль включает операции файловой системы hello хранилища Озера данных Azure. 
* Hello **аналитики azure-datalake** модуль включает операции hello аналитики Озера данных Azure. 

Во-первых, убедитесь, hello последней `pip` , выполнив следующую команду hello:

```
python -m pip install --upgrade pip
```

При написании этого документа использовался компонент `pip version 9.0.1`.

Используйте следующие hello `pip` команды tooinstall hello модули из hello Командная строка:

```
pip install azure-mgmt-resource
pip install azure-datalake-store
pip install azure-mgmt-datalake-store
pip install azure-mgmt-datalake-analytics
```

## <a name="create-a-new-python-script"></a>Создание сценария Python

Вставьте следующий код в скрипт hello hello:

```python
## Use this only for Azure AD service-to-service authentication
#from azure.common.credentials import ServicePrincipalCredentials

## Use this only for Azure AD end-user authentication
#from azure.common.credentials import UserPassCredentials

## Required for Azure Resource Manager
from azure.mgmt.resource.resources import ResourceManagementClient
from azure.mgmt.resource.resources.models import ResourceGroup

## Required for Azure Data Lake Store account management
from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
from azure.mgmt.datalake.store.models import DataLakeStoreAccount

## Required for Azure Data Lake Store filesystem management
from azure.datalake.store import core, lib, multithread

## Required for Azure Data Lake Analytics account management
from azure.mgmt.datalake.analytics.account import DataLakeAnalyticsAccountManagementClient
from azure.mgmt.datalake.analytics.account.models import DataLakeAnalyticsAccount, DataLakeStoreAccountInfo

## Required for Azure Data Lake Analytics job management
from azure.mgmt.datalake.analytics.job import DataLakeAnalyticsJobManagementClient
from azure.mgmt.datalake.analytics.job.models import JobInformation, JobState, USqlJobProperties

## Required for Azure Data Lake Analytics catalog management
from azure.mgmt.datalake.analytics.catalog import DataLakeAnalyticsCatalogManagementClient

## Use these as needed for your application
import logging, getpass, pprint, uuid, time
```

Запустите этот скрипт tooverify приветствия, можно импортировать модули.

## <a name="authentication"></a>Аутентификация

### <a name="interactive-user-authentication-with-a-pop-up"></a>Интерактивная аутентификация пользователей с помощью всплывающего окна

Этот метод не поддерживается.

### <a name="interactive-user-authentication-with-a-device-code"></a>Интерактивная аутентификация пользователей с помощью кода устройства

```python
user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
password = getpass.getpass()
credentials = UserPassCredentials(user, password)
```

### <a name="noninteractive-authentication-with-spi-and-a-secret"></a>Неинтерактивная аутентификация с помощью SPI и секрета

```python
credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')
```

### <a name="noninteractive-authentication-with-api-and-a-certificate"></a>Неинтерактивная аутентификация с помощью API и секрета

Этот метод не поддерживается.

## <a name="common-script-variables"></a>Общие переменные сценария

Эти переменные используются в образцах hello.

```python
subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adla = '<Azure Data Lake Analytics Account Name>'
```

## <a name="create-hello-clients"></a>Создание клиентов hello

```python
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')
```

## <a name="create-an-azure-resource-group"></a>Создание группы ресурсов Azure

```python
armGroupResult = resourceClient.resource_groups.create_or_update( rg, ResourceGroup( location=location ) )
```

## <a name="create-data-lake-analytics-account"></a>Создание учетной записи аналитики озера данных

Сначала создайте учетную запись хранилища.

```python
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()
```
Затем создайте учетную запись ADLA, которая использует это хранилище.

```python
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()
```

## <a name="submit-a-job"></a>Отправка задания

```python
script = """
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
"""

jobId = str(uuid.uuid4())
jobResult = adlaJobClient.job.create(
    adla,
    jobId,
    JobInformation(
        name='Sample Job',
        type='USql',
        properties=USqlJobProperties(script=script)
    )
)
```

## <a name="wait-for-a-job-tooend"></a>Дождитесь tooend задания

```python
jobResult = adlaJobClient.job.get(adla, jobId)
while(jobResult.state != JobState.ended):
    print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
    time.sleep(3)
    jobResult = adlaJobClient.job.get(adla, jobId)

print ('Job finished with result: ' + jobResult.result.value)
```

## <a name="list-pipelines-and-recurrences"></a>Вывод списка конвейеров и повторений
В зависимости от того, вложены ли в задания метаданные конвейеров или повторений, можно отобразить список конвейеров и повторений.

```python
pipelines = adlaJobClient.pipeline.list(adla)
for p in pipelines:
    print('Pipeline: ' + p.name + ' ' + p.pipelineId)

recurrences = adlaJobClient.recurrence.list(adla)
for r in recurrences:
    print('Recurrence: ' + r.name + ' ' + r.recurrenceId)
```

## <a name="manage-compute-policies"></a>Управление политиками вычислений

Hello объекта DataLakeAnalyticsAccountManagementClient предоставляет методы для управления hello вычисления политики для учетной записи аналитики Озера данных.

### <a name="list-compute-policies"></a>Вывод списка политик вычислений

Привет, следующий код извлекает список политик вычислений для учетной записи аналитики Озера данных.

```python
policies = adlaAccountClient.computePolicies.listByAccount(rg, adla)
for p in policies:
    print('Name: ' + p.name + 'Type: ' + p.objectType + 'Max AUs / job: ' + p.maxDegreeOfParallelismPerJob + 'Min priority / job: ' + p.minPriorityPerJob)
```

### <a name="create-a-new-compute-policy"></a>Создание новой политики вычислений

Привет, следующий код создает новую политику вычислений для учетной записи аналитики Озера данных, параметр hello максимальное Сиднейское доступных toohello указан too50 пользователя и too250 приоритет задания минимального hello.

```python
userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde"
newPolicyParams = ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250)
adlaAccountClient.computePolicies.createOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams)
```

## <a name="next-steps"></a>Дальнейшие действия

- toosee hello же учебника при помощи других средств, щелкните селекторы вкладку hello на hello вверху страницы приветствия.
- в разделе toolearn U-SQL [Приступая к работе с Azure аналитика Озера данных U-SQL языка](data-lake-analytics-u-sql-get-started.md).
- Задачи управления описываются в руководстве по [управлению Azure Data Lake Analytics с помощью портала Azure](data-lake-analytics-manage-use-portal.md).

