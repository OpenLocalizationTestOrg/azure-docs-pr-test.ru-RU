---
title: "aaaMove данные из Salesforce с помощью фабрики данных | Документы Microsoft"
description: "Дополнительные сведения о том, как toomove данные из Salesforce с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: dbe3bfd6-fa6a-491a-9638-3a9a10d396d1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: c1bde2a333f5a3c0a995eb8c13ecf585132888b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a>Перемещение данных из Salesforce с помощью фабрики данных Azure
В этой статье рассматриваются способы действие копирования данных toocopy фабрики данных Azure из хранилища данных tooany Salesforce, перечислены под заголовком столбца приемник hello hello [поддерживаемые источники и приемники](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы. Эта статья основана на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования и сочетания поддерживаемых данных хранилища.

Фабрика данных Azure в настоящее время поддерживает только для перемещения данных из Salesforce слишком[приемника хранилища данных поддерживается](data-factory-data-movement-activities.md#supported-data-stores-and-formats), но не поддерживает перемещение данных из других tooSalesforce хранилищ данных.

## <a name="supported-versions"></a>Поддерживаемые версии
Этот соединитель поддерживает следующие выпусков Salesforce hello: Developer Edition, Professional Edition, Enterprise Edition или выпуск неограниченное. Он также поддерживает копирование из рабочей среды Salesforce, песочницы и пользовательского домена.

## <a name="prerequisites"></a>Предварительные требования
* Требуется включить разрешения API. Дополнительные сведения о включении доступа к API в Salesforce с помощью набора разрешений см. [здесь](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/).
* toocopy данные из хранилищ данных Salesforce tooon организациями, необходимо иметь по крайней мере 2.0 шлюза управления данных, установленный в локальной среде.

## <a name="salesforce-request-limits"></a>Ограничения запросов Salesforce
Для Salesforce установлены ограничения на общее число запросов API и одновременных запросов API. Обратите внимание hello после точки.

- Если hello число одновременных запросов превышает предел hello, регулирование и вы увидите случайные сбои.
- Если hello общее число запросов превышает предел hello, hello учетной записи Salesforce будет заблокирован на 24 часа.

Может также возникать ошибка «REQUEST_LIMIT_EXCEEDED» hello в обоих случаях. Hello» API ограничения запросов» в разделе hello [Salesforce разработчика ограничения](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) Дополнительные сведения см.

## <a name="getting-started"></a>Приступая к работе
Вы можете создать конвейер с действием копирования, который перемещает данные из Salesforce, с помощью разных инструментов и интерфейсов API.

toocreate простым способом Hello конвейера — toouse hello **мастер копирования**. В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.

Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**. В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования. 

Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello. 

1. Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.
2. Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования. 
3. Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных. 

При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически. При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.  Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из Salesforce в разделе [пример JSON: копирует данные из Salesforce tooAzure большого двоичного объекта](#json-example-copy-data-from-salesforce-to-azure-blob) этой статьи. 

Hello в следующих разделах подробно JSON свойства, которые являются определенной tooSalesforce используется toodefine фабрики данных сущности: 

## <a name="linked-service-properties"></a>Свойства связанной службы
Привет, в следующей таблице приводится описание элементов JSON, которые зависят от конкретного toohello Salesforce связанные службы.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| type |свойство типа Hello должно быть присвоено: **Salesforce**. |Да |
| environmentUrl | Укажите URL-адрес Salesforce экземпляр hello. <br><br> — URL-адрес по умолчанию — https://login.salesforce.com. <br> -toocopy данных из "песочницы", укажите «https://test.salesforce.com». <br> -задать toocopy данные из пользовательского домена, например, «https://[domain].my.salesforce.com». |Нет |
| Имя пользователя |Укажите имя пользователя для учетной записи пользователя hello. |Да |
| пароль |Укажите пароль для учетной записи пользователя hello. |Да |
| securityToken |Укажите маркер безопасности для учетной записи пользователя hello. В разделе [получение токена безопасности](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) инструкции tooreset/get маркер безопасности. toolearn о маркерах безопасности, см в разделе [безопасности и hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm). |Да |

## <a name="dataset-properties"></a>Свойства набора данных
Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи. Разделы structure, availability и policy JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).

Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello. Hello typeProperties статьи для набора данных типа hello **RelationalTable** имеет hello следующие свойства:

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| tableName |Имя таблицы hello в Salesforce. |Нет (если для свойства **RelationalSource** задано значение **query**). |

> [!IMPORTANT]
> для любого пользовательского объекта требуется Hello «__c» часть hello имя API.

![Фабрика данных — подключение к Salesforce — имя API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a>Свойства действия копирования
Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи. Такие свойства, как имя, описание, входные и выходные таблицы, различные политики, доступны для всех типов действий.

Hello свойства, доступные в Здравствуйте раздел typeProperties hello активности hello другой стороны, могут различаться для каждого типа действия. Для действия копирования они зависят от типов источников и приемников hello.

В действии копирования, когда источник hello типа hello **RelationalSource** (включая Salesforce), hello следующие свойства доступны в разделе "typeProperties":

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| query |Используйте данные tooread hello пользовательского запроса. |Запрос SQL-92 или запрос, написанный на [объектно-ориентированном языке запросов Salesforce (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) . Пример: `select * from MyTable__c`. |Нет (если hello **tableName** из hello **dataset** указан) |

> [!IMPORTANT]
> для любого пользовательского объекта требуется Hello «__c» часть hello имя API.

![Фабрика данных — подключение к Salesforce — имя API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a>Советы по запросам
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a>Получение данных с использованием предложения WHERE в столбце даты и времени
Если указать hello SOQL или SQL-запрос toohello внимания оплаты различие формата даты и времени. Например:

* **Пример SOQL**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`
* **Пример SQL**:
    * **С помощью запроса hello toospecify мастер копирования:**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`
    * **С помощью JSON редактирование запроса hello toospecify (escape-знак правильно):**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`

### <a name="retrieving-data-from-salesforce-report"></a>Извлечение данных из отчета Salesforce
Из отчетов Salesforce можно извлекать данные, указывая запросы в формате `{call "<report name>"}`, например: `"query": "{call \"TestReport\"}"`.

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a>Восстановление удаленных записей из корзины Salesforce
записи tooquery hello мягкий удалены из корзины Salesforce, можно указать **«IsDeleted = 1»** в запросе. Например,

* Укажите tooquery только записи удалены hello, «выберите * из MyTable__c **где IsDeleted = 1**»
* Укажите tooquery все hello записей, включая существующие hello и удалении hello» выберите * из MyTable__c **где IsDeleted = 0 или IsDeleted = 1**»

## <a name="json-example-copy-data-from-salesforce-tooazure-blob"></a>Пример JSON: копирует данные из Salesforce tooAzure больших двоичных объектов
Hello ниже приведен пример определения JSON можно использовать toocreate конвейера с помощью hello [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Они показывают как toocopy данные из Salesforce tooAzure хранилища больших двоичных объектов. Тем не менее, данные могут быть скопированный tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.   

Ниже приведены hello артефактов фабрики данных, вам потребуется toocreate tooimplement hello сценария. последующих список hello Hello разделах содержатся подробные сведения об этих действиях.

* Связанной службы типа hello [Salesforce](#linked-service-properties)
* Связанной службы типа hello [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)
* Входным [dataset](data-factory-create-datasets.md) типа hello [RelationalTable](#dataset-properties)
* Вывод [dataset](data-factory-create-datasets.md) типа hello [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
* [Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [RelationalSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

**Связанная служба SalesForce**

В этом примере используется hello **Salesforce** связанной службы. В разделе hello [Salesforce связанная служба](#linked-service-properties) раздел для hello свойств, поддерживаемых этой связанной службы.  В разделе [получение токена безопасности](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) инструкции как tooreset/get hello маркера безопасности.

```json
{
    "name": "SalesforceLinkedService",
    "properties":
    {
        "type": "Salesforce",
        "typeProperties":
        {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```
**Связанная служба хранения Azure**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
    }
}
```
**Входной набор данных Salesforce**

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"  
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Установка **внешних** слишком**true** информирует hello служба фабрики данных, набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.

> [!IMPORTANT]
> для любого пользовательского объекта требуется Hello «__c» часть hello имя API.

![Фабрика данных — подключение к Salesforce — имя API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

**Выходной набор данных большого двоичного объекта Azure**

Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1).

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/alltypes_c"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Конвейер с действием копирования**

Hello конвейера содержит действие копирования, который настроен toouse hello входные и выходные наборы данных, а — запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**RelationalSource**и hello **приемник** тип установлен слишком**BlobSink**.

В разделе [свойства типа RelationalSource](#copy-activity-properties) hello список свойств, которые поддерживаются hello RelationalSource.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "SalesforceInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"                
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }
        ]
    }
}
```
> [!IMPORTANT]
> для любого пользовательского объекта требуется Hello «__c» часть hello имя API.

![Фабрика данных — подключение к Salesforce — имя API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a>Сопоставление типов для Salesforce
| Тип данных Salesforce | Тип на основе .NET |
| --- | --- |
| Автонумерация |Строка |
| Флажок |Логический |
| Валюта |Double |
| Дата |DateTime |
| Дата и время |DateTime |
| Email |Строка |
| Идентификатор |Строка |
| Связь для подстановки |Строка |
| Список множественного выбора |Строка |
| Number |Double |
| Процент |Double |
| Номер телефона |Строка |
| Список выбора |Строка |
| текст |Строка |
| Текстовое поле |Строка |
| Текстовое поле (длинное) |Строка |
| Текстовое поле (расширенное) |Строка |
| Текст (зашифрованный) |Строка |
| URL-адрес |Строка |

> [!NOTE]
> toomap столбцы из источника toocolumns набора данных из набора данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a>Производительность и настройка
. В разделе hello [действие копирования производительности и руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.
