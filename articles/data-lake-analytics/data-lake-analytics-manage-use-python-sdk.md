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
# <a name="manage-azure-data-lake-analytics-using-python"></a><span data-ttu-id="7ea69-103">Управление Azure Data Lake Analytics с помощью Python</span><span class="sxs-lookup"><span data-stu-id="7ea69-103">Manage Azure Data Lake Analytics using Python</span></span>

## <a name="python-versions"></a><span data-ttu-id="7ea69-104">Версии Python</span><span class="sxs-lookup"><span data-stu-id="7ea69-104">Python versions</span></span>

* <span data-ttu-id="7ea69-105">Используйте 64-разрядную версию Python.</span><span class="sxs-lookup"><span data-stu-id="7ea69-105">Use a 64-bit version of Python.</span></span>
* <span data-ttu-id="7ea69-106">Можно использовать стандартные Python распространения hello в  **[загружает Python.org](https://www.python.org/downloads/)**.</span><span class="sxs-lookup"><span data-stu-id="7ea69-106">You can use hello standard Python distribution found at **[Python.org downloads](https://www.python.org/downloads/)**.</span></span> 
* <span data-ttu-id="7ea69-107">Многим разработчикам кажутся hello удобный toouse  **[распространения Anaconda Python](https://www.continuum.io/downloads)**.</span><span class="sxs-lookup"><span data-stu-id="7ea69-107">Many developers find it convenient toouse hello **[Anaconda Python distribution](https://www.continuum.io/downloads)**.</span></span>  
* <span data-ttu-id="7ea69-108">В этой статье было написано с помощью Python версии 3.6 от стандартного распределения Python hello</span><span class="sxs-lookup"><span data-stu-id="7ea69-108">This article was written using Python version 3.6 from hello standard Python distribution</span></span>

## <a name="install-azure-python-sdk"></a><span data-ttu-id="7ea69-109">Установка пакета Azure SDK для Python</span><span class="sxs-lookup"><span data-stu-id="7ea69-109">Install Azure Python SDK</span></span>

<span data-ttu-id="7ea69-110">Установите hello следующие модули:</span><span class="sxs-lookup"><span data-stu-id="7ea69-110">Install hello following modules:</span></span>

* <span data-ttu-id="7ea69-111">Hello **ресурсов azure-mgmt** модуль включает другие модули Azure Active Directory и т. д.</span><span class="sxs-lookup"><span data-stu-id="7ea69-111">hello **azure-mgmt-resource** module includes other Azure modules for Active Directory, etc.</span></span>
* <span data-ttu-id="7ea69-112">Hello **-mgmt-datalake хранилища azure** модуль включает операции управления учетной записи хранилища Озера данных Azure hello.</span><span class="sxs-lookup"><span data-stu-id="7ea69-112">hello **azure-mgmt-datalake-store** module includes hello Azure Data Lake Store account management operations.</span></span>
* <span data-ttu-id="7ea69-113">Hello **хранилища azure — datalake** модуль включает операции файловой системы hello хранилища Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea69-113">hello **azure-datalake-store** module includes hello Azure Data Lake Store filesystem operations.</span></span> 
* <span data-ttu-id="7ea69-114">Hello **аналитики azure-datalake** модуль включает операции hello аналитики Озера данных Azure.</span><span class="sxs-lookup"><span data-stu-id="7ea69-114">hello **azure-datalake-analytics** module includes hello Azure Data Lake Analytics operations.</span></span> 

<span data-ttu-id="7ea69-115">Во-первых, убедитесь, hello последней `pip` , выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="7ea69-115">First, ensure you have hello latest `pip` by running hello following command:</span></span>

```
python -m pip install --upgrade pip
```

<span data-ttu-id="7ea69-116">При написании этого документа использовался компонент `pip version 9.0.1`.</span><span class="sxs-lookup"><span data-stu-id="7ea69-116">This document was written using `pip version 9.0.1`.</span></span>

<span data-ttu-id="7ea69-117">Используйте следующие hello `pip` команды tooinstall hello модули из hello Командная строка:</span><span class="sxs-lookup"><span data-stu-id="7ea69-117">Use hello following `pip` commands tooinstall hello modules from hello commandline:</span></span>

```
pip install azure-mgmt-resource
pip install azure-datalake-store
pip install azure-mgmt-datalake-store
pip install azure-mgmt-datalake-analytics
```

## <a name="create-a-new-python-script"></a><span data-ttu-id="7ea69-118">Создание сценария Python</span><span class="sxs-lookup"><span data-stu-id="7ea69-118">Create a new Python script</span></span>

<span data-ttu-id="7ea69-119">Вставьте следующий код в скрипт hello hello:</span><span class="sxs-lookup"><span data-stu-id="7ea69-119">Paste hello following code into hello script:</span></span>

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

<span data-ttu-id="7ea69-120">Запустите этот скрипт tooverify приветствия, можно импортировать модули.</span><span class="sxs-lookup"><span data-stu-id="7ea69-120">Run this script tooverify that hello modules can be imported.</span></span>

## <a name="authentication"></a><span data-ttu-id="7ea69-121">Аутентификация</span><span class="sxs-lookup"><span data-stu-id="7ea69-121">Authentication</span></span>

### <a name="interactive-user-authentication-with-a-pop-up"></a><span data-ttu-id="7ea69-122">Интерактивная аутентификация пользователей с помощью всплывающего окна</span><span class="sxs-lookup"><span data-stu-id="7ea69-122">Interactive user authentication with a pop-up</span></span>

<span data-ttu-id="7ea69-123">Этот метод не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="7ea69-123">This method is not supported.</span></span>

### <a name="interactive-user-authentication-with-a-device-code"></a><span data-ttu-id="7ea69-124">Интерактивная аутентификация пользователей с помощью кода устройства</span><span class="sxs-lookup"><span data-stu-id="7ea69-124">Interactive user authentication with a device code</span></span>

```python
user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
password = getpass.getpass()
credentials = UserPassCredentials(user, password)
```

### <a name="noninteractive-authentication-with-spi-and-a-secret"></a><span data-ttu-id="7ea69-125">Неинтерактивная аутентификация с помощью SPI и секрета</span><span class="sxs-lookup"><span data-stu-id="7ea69-125">Noninteractive authentication with SPI and a secret</span></span>

```python
credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')
```

### <a name="noninteractive-authentication-with-api-and-a-certificate"></a><span data-ttu-id="7ea69-126">Неинтерактивная аутентификация с помощью API и секрета</span><span class="sxs-lookup"><span data-stu-id="7ea69-126">Noninteractive authentication with API and a certificate</span></span>

<span data-ttu-id="7ea69-127">Этот метод не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="7ea69-127">This method is not supported.</span></span>

## <a name="common-script-variables"></a><span data-ttu-id="7ea69-128">Общие переменные сценария</span><span class="sxs-lookup"><span data-stu-id="7ea69-128">Common script variables</span></span>

<span data-ttu-id="7ea69-129">Эти переменные используются в образцах hello.</span><span class="sxs-lookup"><span data-stu-id="7ea69-129">These variables are used in hello samples.</span></span>

```python
subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adla = '<Azure Data Lake Analytics Account Name>'
```

## <a name="create-hello-clients"></a><span data-ttu-id="7ea69-130">Создание клиентов hello</span><span class="sxs-lookup"><span data-stu-id="7ea69-130">Create hello clients</span></span>

```python
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')
```

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="7ea69-131">Создание группы ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="7ea69-131">Create an Azure Resource Group</span></span>

```python
armGroupResult = resourceClient.resource_groups.create_or_update( rg, ResourceGroup( location=location ) )
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="7ea69-132">Создание учетной записи аналитики озера данных</span><span class="sxs-lookup"><span data-stu-id="7ea69-132">Create Data Lake Analytics account</span></span>

<span data-ttu-id="7ea69-133">Сначала создайте учетную запись хранилища.</span><span class="sxs-lookup"><span data-stu-id="7ea69-133">First create a store account.</span></span>

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
<span data-ttu-id="7ea69-134">Затем создайте учетную запись ADLA, которая использует это хранилище.</span><span class="sxs-lookup"><span data-stu-id="7ea69-134">Then create an ADLA account that uses that store.</span></span>

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

## <a name="submit-a-job"></a><span data-ttu-id="7ea69-135">Отправка задания</span><span class="sxs-lookup"><span data-stu-id="7ea69-135">Submit a job</span></span>

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

## <a name="wait-for-a-job-tooend"></a><span data-ttu-id="7ea69-136">Дождитесь tooend задания</span><span class="sxs-lookup"><span data-stu-id="7ea69-136">Wait for a job tooend</span></span>

```python
jobResult = adlaJobClient.job.get(adla, jobId)
while(jobResult.state != JobState.ended):
    print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
    time.sleep(3)
    jobResult = adlaJobClient.job.get(adla, jobId)

print ('Job finished with result: ' + jobResult.result.value)
```

## <a name="list-pipelines-and-recurrences"></a><span data-ttu-id="7ea69-137">Вывод списка конвейеров и повторений</span><span class="sxs-lookup"><span data-stu-id="7ea69-137">List pipelines and recurrences</span></span>
<span data-ttu-id="7ea69-138">В зависимости от того, вложены ли в задания метаданные конвейеров или повторений, можно отобразить список конвейеров и повторений.</span><span class="sxs-lookup"><span data-stu-id="7ea69-138">Depending whether your jobs have pipeline or recurrence metadata attached, you can list pipelines and recurrences.</span></span>

```python
pipelines = adlaJobClient.pipeline.list(adla)
for p in pipelines:
    print('Pipeline: ' + p.name + ' ' + p.pipelineId)

recurrences = adlaJobClient.recurrence.list(adla)
for r in recurrences:
    print('Recurrence: ' + r.name + ' ' + r.recurrenceId)
```

## <a name="manage-compute-policies"></a><span data-ttu-id="7ea69-139">Управление политиками вычислений</span><span class="sxs-lookup"><span data-stu-id="7ea69-139">Manage compute policies</span></span>

<span data-ttu-id="7ea69-140">Hello объекта DataLakeAnalyticsAccountManagementClient предоставляет методы для управления hello вычисления политики для учетной записи аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="7ea69-140">hello DataLakeAnalyticsAccountManagementClient object provides methods for managing hello compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="7ea69-141">Вывод списка политик вычислений</span><span class="sxs-lookup"><span data-stu-id="7ea69-141">List compute policies</span></span>

<span data-ttu-id="7ea69-142">Привет, следующий код извлекает список политик вычислений для учетной записи аналитики Озера данных.</span><span class="sxs-lookup"><span data-stu-id="7ea69-142">hello following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

```python
policies = adlaAccountClient.computePolicies.listByAccount(rg, adla)
for p in policies:
    print('Name: ' + p.name + 'Type: ' + p.objectType + 'Max AUs / job: ' + p.maxDegreeOfParallelismPerJob + 'Min priority / job: ' + p.minPriorityPerJob)
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="7ea69-143">Создание новой политики вычислений</span><span class="sxs-lookup"><span data-stu-id="7ea69-143">Create a new compute policy</span></span>

<span data-ttu-id="7ea69-144">Привет, следующий код создает новую политику вычислений для учетной записи аналитики Озера данных, параметр hello максимальное Сиднейское доступных toohello указан too50 пользователя и too250 приоритет задания минимального hello.</span><span class="sxs-lookup"><span data-stu-id="7ea69-144">hello following code creates a new compute policy for a Data Lake Analytics account, setting hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

```python
userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde"
newPolicyParams = ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250)
adlaAccountClient.computePolicies.createOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams)
```

## <a name="next-steps"></a><span data-ttu-id="7ea69-145">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7ea69-145">Next steps</span></span>

- <span data-ttu-id="7ea69-146">toosee hello же учебника при помощи других средств, щелкните селекторы вкладку hello на hello вверху страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="7ea69-146">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
- <span data-ttu-id="7ea69-147">в разделе toolearn U-SQL [Приступая к работе с Azure аналитика Озера данных U-SQL языка](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7ea69-147">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
- <span data-ttu-id="7ea69-148">Задачи управления описываются в руководстве по [управлению Azure Data Lake Analytics с помощью портала Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7ea69-148">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>

