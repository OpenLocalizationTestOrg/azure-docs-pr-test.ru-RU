---
title: "aaaTransform данных с помощью скрипт U-SQL - Azure | Документы Microsoft"
description: "Узнайте, как службы вычислений tooprocess или преобразования данных, выполняя сценарии U-SQL на аналитики Озера данных Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e17c1255-62c2-4e2e-bb60-d25274903e80
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: spelluru
ms.openlocfilehash: 51fdb40334d0c131720f65c3a96b4c5045a98b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a>Преобразование данных с помощью сценариев U-SQL в Azure Data Lake Analytics 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Действие Hive](data-factory-hive-activity.md) 
> * [Действие Pig](data-factory-pig-activity.md)
> * [Действие MapReduce](data-factory-map-reduce.md)
> * [Потоковая активность Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Действие Spark](data-factory-spark.md)
> * [Действие выполнения пакета машинного обучения](data-factory-azure-ml-batch-execution-activity.md)
> * [Действие "Обновить ресурс" в службе машинного обучения](data-factory-azure-ml-update-resource-activity.md)
> * [Действие хранимой процедуры](data-factory-stored-proc-activity.md)
> * [Действие U-SQL в Data Lake Analytics](data-factory-usql-activity.md)
> * [Настраиваемое действие .NET](data-factory-use-custom-activities.md)

Конвейер в фабрике данных Azure обрабатывает данные в связанной службе хранилища с помощью связанных вычислительных служб. В нем содержится последовательность действий, каждое из которых выполняет определенную операцию обработки. В этой статье описывается hello **действия U-SQL аналитики Озера данных** , на котором запущена **U-SQL** скрипта на **аналитики Озера данных Azure** вычислений связанной службы. 

> [!NOTE]
> Перед созданием конвейера с действием U-SQL в Data Lake Analytics следует создать учетную запись Data Lake Analytics. toolearn о аналитики Озера данных Azure, в разделе [Приступая к работе с аналитики Озера данных Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md).
> 
> Просмотрите hello [сборки в первом учебнике конвейера](data-factory-build-your-first-pipeline.md) для фабрики данных toocreate подробное описание действий, связанных служб, наборы данных и конвейера. Редактор фабрики данных или toocreate сущностей фабрики данных в Visual Studio или Azure PowerShell с помощью фрагментов JSON.

## <a name="supported-authentication-types"></a>Поддерживаемые типы аутентификации
Действие U-SQL поддерживает указанные ниже типы проверки подлинности Data Lake Analytics.
* Проверка подлинности субъекта-службы
* Проверка подлинности учетных данных пользователя (OAuth) 

Мы рекомендуем использовать проверку подлинности субъекта-службы, особенно для выполнения U-SQL по расписанию. При проверке подлинности учетных данных пользователя может истечь срок действия маркера. Сведения о конфигурации, в разделе hello [связанные свойства службы](#azure-data-lake-analytics-linked-service) раздела.

## <a name="azure-data-lake-analytics-linked-service"></a>Связанная служба аналитики озера данных Azure
Вы создаете **аналитики Озера данных Azure** связанные toolink служба фабрики данных Azure tooan службы вычислений аналитики Озера данных Azure. действия U-SQL аналитики Озера данных в конвейере hello Hello ссылается toothis связанной службы. 

Hello следующей таблице приводится описание hello универсальных свойств, используемых в определении JSON hello. Вы можете выбирать между проверкой подлинности на основе субъекта-службы и учетных данных пользователя.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| **type** |свойство типа Hello должно быть присвоено: **AzureDataLakeAnalytics**. |Да |
| **accountName** |Имя учетной записи аналитики озера данных Azure. |Да |
| **dataLakeAnalyticsUri** |Универсальный код ресурса (URI) аналитики озера данных Azure. |Нет |
| **subscriptionId** |Идентификатор подписки Azure |Нет (если не указан, подписка hello используется фабрики данных). |
| **resourceGroupName** |Имя группы ресурсов Azure |Нет (если не указан, группа ресурсов для hello используется фабрики данных). |

### <a name="service-principal-authentication-recommended"></a>Проверка подлинности на основе субъекта-службы (рекомендуется)
toouse основной проверки подлинности службы, регистрация сущности приложения в Azure Active Directory (Azure AD) и предоставьте его hello доступа к хранилищу Озера tooData. Подробные инструкции см. в статье [Аутентификация между службами в Data Lake Store с помощью Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md). Запишите следующие значения, которые вы используете hello toodefine hello связанной службы:
* Идентификатор приложения
* Ключ приложения 
* Tenant ID

Используйте основной проверки подлинности службы, указав hello следующие свойства:

| Свойство | Описание | Обязательно |
|:--- |:--- |:--- |
| **servicePrincipalId** | Укажите идентификатор клиента приложения hello. | Да |
| **servicePrincipalKey** | Укажите ключ приложения hello. | Да |
| **tenant** | Укажите информацию о клиенте hello (имя или клиента код домена), в которой расположено приложение. Его можно получить путем наведения указателя мыши hello в правом верхнем углу hello hello портал Azure. | Да |

**Пример. Проверка подлинности на основе субъекта-службы**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Использование проверки подлинности на основе учетных данных пользователя
Кроме того можно использовать проверку подлинности учетных данных пользователя для аналитики Озера данных, указав hello следующие свойства:

| Свойство | Описание | Обязательно |
|:--- |:--- |:--- |
| **authorization** | Нажмите кнопку hello **авторизовать** в hello редактор фабрики данных и ввести учетные данные, назначает hello автоматически авторизации URL-адрес toothis свойство. | Да |
| **sessionId** | Идентификатор сеанса OAuth из сеанса авторизации OAuth hello. Каждый идентификатор сеанса является уникальным и используется только один раз. Этот параметр автоматически создается при использовании hello редактор фабрики данных. | Да |

**Пример. Использование проверки подлинности на основе учетных данных пользователя**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a>Срок действия маркера
Здравствуйте, код авторизации, созданный с помощью hello **авторизовать** кнопку срок действия истекает спустя некоторое время. См. в следующей таблице для hello сроков действия для различных типов учетных записей пользователей hello. Может появиться сообщение об ошибке после hello hello проверки подлинности при **истечения срока действия маркера**: Ошибка действия учетных данных: invalid_grant - AADSTS70002: ошибка при проверке учетных данных. AADSTS70008: hello предоставляется право доступа просрочен или отозван. Идентификатор отслеживания: d18629e8-af88-43c5-88e3-d8419eb1fca1 Идентификатор корреляции: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Временная отметка: 2015-12-15 21:09:31Z".

| Тип пользователя | Срок действия |
|:--- |:--- |
| Учетные записи пользователей, которые не управляются с помощью Azure Active Directory (@hotmail.com, @live.com и т. д.) |12 часов |
| Учетные записи пользователей, которые управляются Azure Active Directory (AAD) |Запустите через 14 дней после последнего фрагмента hello. <br/><br/>90 дней, если срез, основанный на связанной службе на основе OAuth, выполняется по крайней мере раз в 14 дней. |

tooavoid и разрешения этой ошибки, повторно авторизовать с помощью hello **авторизовать** когда hello **истечения срока действия маркера** и повторного развертывания hello связанной службы. Значения свойств **sessionId** и **authorization** также можно задавать программно с помощью кода:

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

В разделе [класс AzureDataLakeStoreLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [класс AzureDataLakeAnalyticsLinkedService](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), и [AuthorizationSessionGetResponse класса](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) подробные сведения о hello фабрики данных классы, используемые в коде hello. Добавьте ссылку на: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll для hello WindowsFormsWebAuthenticationDialog класса. 

## <a name="data-lake-analytics-u-sql-activity"></a>Действие U-SQL в аналитике озера данных
Привет, следующий фрагмент JSON определяет конвейера действием U-SQL аналитики Озера данных. Определение действия Hello имеет ссылку toohello службы связаны аналитики Озера данных Azure, созданную ранее.   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline toocompute events for en-gb locale and date less than 2012/02/19.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00Z",
        "end": "2015-08-08T01:00:00Z",
        "isPaused": false
    }
}
```

Hello следующей таблице описаны имена и описания свойства, которые являются определенной toothis действия. 

| Свойство | Описание | Обязательно |
|:--- |:--- |:--- |
| type |свойство типа Hello должно быть задано слишком**DataLakeAnalyticsU SQL**. |Да |
| scriptPath |Toofolder путь, содержащий скрипт hello U-SQL. Имя файла hello учитывается регистр. |Нет (если используется скрипт) |
| scriptLinkedService |Связанной службы, которая связывает hello хранилища, содержащий фабрики данных toohello сценария hello |Нет (если используется скрипт) |
| script |Указание сценария непосредственно в строке вместо использования scriptPath и scriptLinkedService. Например, `"script": "CREATE DATABASE test"`. |Нет (при использовании scriptPath и scriptLinkedService) |
| degreeOfParallelism |Максимальное количество узлов Hello одновременно использовать toorun hello задания. |Нет |
| priority |Определяет, какие задания из всех, поставленных в очередь должна быть выбранного toorun сначала. Hello hello снижать hello более высокий приоритет hello. |Нет |
| parameters |Параметры для скрипта hello U-SQL |Нет |
| runtimeVersion | Версия среды выполнения toouse engine hello U-SQL | Нет | 
| compilationMode | <p>Режим компиляции U-SQL. Может иметь одно из следующих значений.</p> <ul><li>**Semantic**: выполнение только семантических проверок и необходимых проверок работоспособности.</li><li>**Full:** выполнение полной компиляции hello, включая проверку синтаксиса оптимизации, создание кода, и т. д.</li><li>**SingleBox:** выполнения полной компиляции hello с tooSingleBox параметр TargetType.</li></ul><p>Если не указать значение для этого свойства, hello сервер определяет режим оптимальной компиляции hello. </p>| Нет | 

В разделе [SearchLogProcessing.txt сценарий определения](#sample-u-sql-script) hello скрипт определения. 

## <a name="sample-input-and-output-datasets"></a>Примеры входных и выходных наборов данных
### <a name="input-dataset"></a>Входной набор данных
В этом примере hello входные данные хранятся в хранилище Озера данных Azure (SearchLog.tsv файл в папке datalake или ввода hello). 

```json
{
    "name": "DataLakeTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}    
```

### <a name="output-dataset"></a>Выходной набор данных
В этом примере hello выходных данных, полученных при hello скрипт U-SQL хранится в хранилище Озера данных Azure (datalake/выходная папка). 

```json
{
    "name": "EventsByRegionTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="sample-data-lake-store-linked-service"></a>Пример связанной службы Data Lake Store
Вот определение hello образца hello хранилища Озера данных Azure связанной службы, используемые наборы данных hello ввода вывода. 

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
        }
    }
}
```

В разделе [перемещения tooand данных из хранилища Озера данных Azure](data-factory-azure-datalake-connector.md) статьи для описания свойств JSON. 

## <a name="sample-u-sql-script"></a>Пример сценария U-SQL

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    too@out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

Здравствуйте, значения для  **@in**  и  **@out**  параметры в сценарий hello U-SQL, передаются динамически по ADF с помощью раздела «параметры» hello. См. раздел «Параметры» hello в определении конвейера hello.

Другие свойства, такие как degreeOfParallelism и приоритет также можно указать в определении конвейера для hello заданий, запускаемых на hello Служба аналитики Озера данных Azure.

## <a name="dynamic-parameters"></a>Динамические параметры
Увеличение и уменьшение hello пример конвейера определения параметров назначаются с фиксированными значениями. 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

Вместо этого — toouse возможных динамических параметров. Например: 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

В этом случае входные файлы по-прежнему извлекаются из папки /datalake/input hello и выходные файлы создаются в папке /datalake/output hello. имена файлов Hello являются динамическими по времени начала фрагмента hello.  

