---
title: "Перемещение данных из хранилищ данных ODBC | Документация Майкрософт"
description: "Узнайте, как перемещать данные из хранилищ данных ODBC с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ad70a598-c031-4339-a883-c6125403cb76
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 381069f8d8b5fef0d283fcfc6bc3f82fcf119c0e
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/23/2018
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a>Перемещение данных из хранилищ данных ODBC с помощью фабрики данных Azure
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Версия 1 — общедоступная](data-factory-odbc-connector.md)
> * [Версия 2 — предварительная](../connector-odbc.md)

> [!NOTE]
> Статья относится к версии 1 фабрики данных, которая является общедоступной версией. Если вы используете версию 2 службы фабрики данных, которая находится на этапе предварительной версии, см. статью [Copy data from and to ODBC data stores using Azure Data Factory](../connector-odbc.md) (Копирование данных из хранилища данных ODBC и в него с помощью фабрики данных Azure).


В этой статье описывается, как с помощью действия копирования в фабрике данных Azure перемещать данные из локального хранилища данных ODBC. Этот документ является продолжением статьи о [действиях перемещения данных](data-factory-data-movement-activities.md), в которой приведены общие сведения о перемещении данных с помощью действия копирования.

Данные из хранилища данных ODBC можно скопировать в любое хранилище данных, поддерживаемое в качестве приемника. Список хранилищ данных, которые поддерживаются в качестве приемников для действия копирования, приведен в таблице [Поддерживаемые хранилища данных и форматы](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Сейчас фабрика данных поддерживает только перемещение данных из хранилища данных ODBC в другие хранилища данных, но не наоборот. 

## <a name="enabling-connectivity"></a>Включение соединения
Служба фабрики данных поддерживает подключение к локальным источникам ODBC с помощью шлюза управления данными. В статье [Перемещение данных между локальными и облачными ресурсами](data-factory-move-data-between-onprem-and-cloud.md) приведены сведения о шлюзе управления данными и пошаговые инструкции по его настройке. Используйте шлюз для подключения к локальному хранилищу данных ODBC, даже если он размещен на виртуальной машине IaaS Azure.

Шлюз можно установить на тот же локальный компьютер или виртуальную машину Azure, что и хранилище данных ODBC. Тем не менее рекомендуется установить шлюз на отдельный компьютер или виртуальную машину IaaS SQL Azure, чтобы избежать конфликта ресурсов, а также для повышения производительности. При установке шлюза на отдельный компьютер у компьютера должен быть доступ к машине с хранилищем данных ODBC.

Помимо шлюза управления данными на компьютере с шлюзом необходимо также установить драйвер ODBC для хранилища данных.

> [!NOTE]
> Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).

## <a name="getting-started"></a>Приступая к работе
Вы можете создать конвейер с действием копирования, который перемещает данные из хранилища данных ODBC, с помощью разных инструментов и интерфейсов API.

Проще всего создать конвейер с помощью **мастера копирования**. В статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md) приведены краткие пошаговые указания по созданию конвейера с помощью мастера копирования данных.

Также для создания конвейера можно использовать следующие инструменты: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблон Azure Resource Manager**, **API .NET** и **REST API**. Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги: 

1. Создайте **связанные службы**, чтобы связать входные и выходные данные с фабрикой данных.
2. Создайте **наборы данных**, которые представляют входные и выходные данные для операции копирования. 
3. Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных. 

Если вы используете мастер, то он автоматически создает определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера). При использовании инструментов и интерфейсов API (за исключением API .NET) вы самостоятельно определяете эти сущности фабрики данных в формате JSON.  Пример определений JSON для сущностей фабрики данных, которые используются для копирования данных из хранилища данных ODBC, приведены в разделе [Пример JSON. Копирование данных из хранилища данных ODBC в большой двоичный объект Azure](#json-example-copy-data-from-odbc-data-store-to-azure-blob) этой статьи. 

Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, относящихся к хранилищу данных ODBC.

## <a name="linked-service-properties"></a>Свойства связанной службы
В следующей таблице содержится описание элементов JSON, которые относятся к связанной службе ODBC.

| Свойство | ОПИСАНИЕ | Обязательно |
| --- | --- | --- |
| Тип |Для свойства type необходимо задать значение **OnPremisesOdbc** |Yes |
| connectionString |Учетные данные в строке подключения, не используемые для получения доступа, а также дополнительные зашифрованные учетные данные. Примеры приведены в следующих разделах. <br/><br/>Можно указать строку подключения с шаблоном `"Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;"` или использовать системное имя DSN (имя источника данных), которое вы настроили на компьютере шлюза с помощью `"DSN=<name of the DSN>;"` (вы все равно должны указать соответствующие учетные данные в связанной службе). |Yes |
| credential |Учетные данные в строке подключения, используемые для получения доступа и указанные в формате "драйвер-определенное свойство-значение". Пример: `"Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;"`. |Нет  |
| authenticationType |Тип проверки подлинности, используемый для подключения к хранилищу данных ODBC. Возможными значениями являются: "Анонимная" и "Обычная". |Yes |
| Имя пользователя |При использовании обычной проверки подлинности укажите имя пользователя. |Нет  |
| password |Введите пароль для учетной записи пользователя, указанной для выбранного имени пользователя. |Нет  |
| gatewayName |Имя шлюза, который следует использовать службе фабрики данных для подключения к хранилищу данных ODBC. |Yes |

### <a name="using-basic-authentication"></a>Использовать обычную проверку подлинности

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```
### <a name="using-basic-authentication-with-encrypted-credentials"></a>Использовать обычную проверку подлинности и шифрование учетных данных
Учетные данные можно зашифровать с помощью командлета [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (Azure PowerShell 1.0) или [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (Azure PowerShell 0.9 или более ранней версии).  

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a>Использовать анонимную проверку подлинности

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "mygateway"
        }
    }
}
```


## <a name="dataset-properties"></a>Свойства набора данных
Полный список разделов и свойств, используемых для определения наборов данных, см. в статье [Наборы данных](data-factory-create-datasets.md). Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).

Раздел **typeProperties** во всех типах наборов данных разный. В нем содержатся сведения о расположении данных в хранилище данных. Раздел typeProperties набора данных типа **RelationalTable** (который включает в себя набор данных ODBC) содержит следующие свойства.

| Свойство | ОПИСАНИЕ | Обязательно |
| --- | --- | --- |
| tableName |Имя таблицы в хранилище данных ODBC. |Yes |

## <a name="copy-activity-properties"></a>Свойства действия копирования
Полный список разделов и свойств, используемых для определения действий, см. в статье [Создание конвейеров](data-factory-create-pipelines.md). Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.

С другой стороны, свойства, доступные в разделе **typeProperties** действия, зависят от конкретного типа действия. Для действия копирования они различаются в зависимости от типов источников и приемников.

В случае действия копирования, когда источник относится к типу **RelationalSource** (который содержит ODBC), в разделе typeProperties доступны следующие свойства.

| Свойство | ОПИСАНИЕ | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| query |Используйте пользовательский запрос для чтения данных. |Строка запроса SQL. Например, select * from MyTable. |Yes |


## <a name="json-example-copy-data-from-odbc-data-store-to-azure-blob"></a>Пример JSON. Копирование данных из хранилища данных ODBC в большой двоичный объект Azure
Ниже приведен пример с определениями JSON, которые можно использовать для создания конвейера с помощью [портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Он демонстрирует, как скопировать данные из источника ODBC в хранилище BLOB-объектов Azure. Тем не менее данные можно копировать в любой из указанных [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) приемников. Это делается с помощью действия копирования в фабрике данных Azure.

Образец состоит из следующих сущностей фабрики данных.

1. Связанная служба типа [OnPremisesOdbc](#linked-service-properties).
2. Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Входной [набор данных](data-factory-create-datasets.md) типа [RelationalTable](#dataset-properties).
4. Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. [Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [RelationalSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

В примере данные из результата выполнения запроса к хранилищу данных ODBC каждый час копируются в BLOB-объект. Используемые в этих примерах свойства JSON описаны в разделах, следующих за примерами.

Сначала настройте шлюз управления данными. Инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .

**Связанная служба ODBC**. В этом примере используется обычная проверка подлинности. Сведения о различных типах аутентификации, которые можно использовать, см. в разделе [Свойства связанной службы ODBC](#linked-service-properties).

```json
{
    "name": "OnPremOdbcLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
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

**Входной набор данных ODBC**

В примере предполагается, что таблица MyTable уже создана в базе данных ODBC и содержит столбец с именем timestampcolumn для данных временных рядов.

Если параметру external присвоить значение true, фабрика данных воспримет этот набор данных как внешний и созданный не в результате какого-либо действия в этой службе.

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremOdbcLinkedService",
        "typeProperties": {},
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

**Выходной набор данных BLOB-объекта Azure**

Данные записываются в новый BLOB-объект каждый час (frequency: hour, interval: 1). Путь к папке BLOB-объекта вычисляется динамически на основе времени начала обрабатываемого среза. В пути к папке используется год, месяц, день и час времени начала.

```json
{
    "name": "AzureBlobOdbcDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odbc/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


**Действие копирования в конвейере с хранилищем данных ODBC (RelationalSource) в качестве источника и большим двоичным объектом в качестве приемника (BlobSink)**

Конвейер содержит действие копирования, которое использует эти входной и выходной наборы данных и выполняется каждый час. В определении JSON конвейера для типа **source** установлено значение **RelationalSource**, а для типа **sink** — значение **BlobSink**. SQL-запрос, указанный для свойства **query** , выбирает для копирования данные за последний час.

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "OdbcDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOdbcDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "OdbcToBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-odbc"></a>Сопоставление типов для ODBC
Как упоминалось в статье о [действиях перемещения данных](data-factory-data-movement-activities.md), во время копирования типы источников автоматически преобразовываются в типы приемников. Такое преобразование выполняется в два этапа:

1. Преобразование собственных типов источников в тип .NET.
2. Преобразование типа .NET в собственный тип приемника.

При перемещении данных из хранилищ данных ODBC типы данных ODBC сопоставляются с типами .NET. Ознакомьтесь со статьей [Сопоставления типов данных ODBC](https://msdn.microsoft.com/library/cc668763.aspx).

## <a name="map-source-to-sink-columns"></a>Сопоставление столбцов источника и приемника
Дополнительные сведения о сопоставлении столбцов в наборе данных, используемом в качестве источника, со столбцами в приемнике см. в [этой статье](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Повторяющиеся операции чтения из реляционных источников
При копировании данных из реляционных хранилищ важно помнить о повторяемости, чтобы избежать непредвиденных результатов. В фабрике данных Azure можно вручную повторно выполнить срез. Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно. При повторном выполнении среза в любом случае необходимо убедиться в том, что считываются те же данные, независимо от того, сколько раз выполняется срез. Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="ge-historian-store"></a>Хранилище GE Historian
Создание связанной службы ODBC для связи хранилища данных [Proficy Historian GE (теперь GE Historian)](http://www.geautomation.com/products/proficy-historian) с фабрикой данных Azure выполняется, как показано в следующем примере:

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of the GE Historian store>;",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

Установите шлюз управления данными на локальном компьютере и зарегистрируйте этот шлюз на портале. Шлюз, установленный на локальном компьютере, использует драйвер ODBC для GE Historian для подключения к хранилищу данных GE Historian. Поэтому необходимо установить драйвер на компьютере шлюза. Подробные сведения см. в разделе [Включение соединения](#enabling-connectivity).

Прежде чем использовать хранилище GE Historian в решении фабрики данных, убедитесь, что шлюз может подключаться к хранилищу данных с помощью инструкций в следующем разделе.

В начале статьи приводится подробный обзор использования хранилищ данных ODBC в качестве исходных хранилищ данных в ходе операции копирования.  

## <a name="troubleshoot-connectivity-issues"></a>Устранение проблем подключения
Для устранения проблем подключения используйте вкладку **Диагностика** **диспетчера конфигурации шлюза управления данными**.

1. Запустите **диспетчер конфигурации шлюза управления данными**. Можно запустить файл "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" напрямую или выполнить поиск по слову **шлюз**, чтобы найти ссылку на приложение **Шлюз управления данными Майкрософт**, как показано на следующем рисунке.

    ![Поиск шлюза](./media/data-factory-odbc-connector/search-gateway.png)
2. Перейдите на вкладку **Диагностика** .

    ![Диагностика шлюза](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. Выберите **тип** хранилища данных (связанная служба).
4. Укажите тип **аутентификации** и введите **учетные данные** или **строку подключения** для подключения к хранилищу данных.
5. Щелкните **Проверить подключение** , чтобы проверить подключение к хранилищу данных.

## <a name="performance-and-tuning"></a>Производительность и настройка
Ознакомьтесь со статьей [Руководство по настройке производительности действия копирования](data-factory-copy-activity-performance.md), в которой описываются ключевые факторы, влияющие на производительность перемещения данных (действие копирования) в фабрике данных Azure, и различные способы оптимизации этого процесса.
