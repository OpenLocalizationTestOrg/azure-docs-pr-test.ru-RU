---
title: "Перемещение данных из DB2 с помощью фабрики данных Azure | Документация Майкрософт"
description: "Узнайте, как перемещать данные из локальной базы данных DB2 с помощью действия копирования в фабрике данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c1644e17-4560-46bb-bf3c-b923126671f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 17ffd0de41964736d2f59b0cf891d0c6b2e7d16b
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/23/2018
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a>Перемещение данных из DB2 с помощью действия копирования в фабрике данных Azure
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Версия 1 — общедоступная](data-factory-onprem-db2-connector.md)
> * [Версия 2 — предварительная](../connector-db2.md)

> [!NOTE]
> Статья относится к версии 1 фабрики данных, которая является общедоступной версией. Если вы используете версию 2 службы фабрики данных, которая находится на этапе предварительной версии, см. статью [Copy data from DB2 by using Azure Data Factory](../connector-db2.md) (Копирование данных из DB2 с помощью фабрики данных Azure).


В этой статье описано использование действия копирования в фабрике данных Azure для копирования данных из локальной базы данных DB2 в хранилище данных. Данные можно копировать в любое хранилище из списка хранилищ в статье [Перемещение данных с помощью действия копирования](data-factory-data-movement-activities.md#supported-data-stores-and-formats), если указано, что оно поддерживается в качестве приемника. Материал данного раздела основан на статье о фабрике данных, в которой приведены общие сведения о перемещении данных с помощью действия копирования и перечислены поддерживаемые сочетания хранилищ данных. 

Сейчас фабрика данных поддерживает только перемещение данных из базы данных DB2 в другое [поддерживаемое хранилище-приемник](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Перемещение данных из других хранилищ в базу данных DB2 не поддерживается.

## <a name="prerequisites"></a>предварительным требованиям
Фабрика данных поддерживает подключение к локальной базе данных DB2 с помощью [шлюза управления данными](data-factory-data-management-gateway.md). Пошаговые инструкции по настройке шлюза для перемещения данных с помощью конвейера см. в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md).

Шлюз является обязательным, даже если база данных DB2 размещается на виртуальной машине Azure IaaS. Шлюз можно установить на ту же виртуальную машину IaaS, что и хранилище данных. Если шлюз может подключиться к базе данных, то можно установить шлюз на другой виртуальной машине.

Шлюз управления данными предоставляет встроенный драйвер DB2, поэтому при копировании данных из DB2 вам не потребуется устанавливать драйвер вручную.

> [!NOTE]
> Советы по устранению неполадок, связанных с подключением и шлюзом, см. в разделе [Устранение неполадок со шлюзом](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).


## <a name="supported-versions"></a>Поддерживаемые версии
Соединитель DB2 фабрики данных поддерживает следующие платформы и версии IBM DB2 с архитектурой распределенной реляционной базы данных (DRDA) SQL Access Manager версии 9, 10 и 11:

* IBM DB2 для z/OS версии 11.1
* IBM DB2 для z/OS версии 10.1
* IBM DB2 для i (AS400) версии 7.2
* IBM DB2 для i (AS400) версии 7.1
* IBM DB2 для Linux, UNIX и Windows (LUW) версии 11
* IBM DB2 для LUW версии 10.5
* IBM DB2 для LUW версии 10.1

> [!TIP]
> Если отобразилось сообщение об ошибке "Пакет, соответствующий запросу на выполнение инструкции SQL, не найден. SQLSTATE=51002 SQLCODE=-805", это указывает на то, что в операционной системе не создан требуемый пакет для обычного пользователя. Чтобы устранить эту проблему, выполните следующие действия для своего типа сервера DB2:
> - DB2 для i (AS400): позволяет опытному пользователю создать коллекцию для обычного пользователя перед выполнением действия копирования. Чтобы создать коллекцию, используйте команду `create collection <username>`.
> - DB2 для z/OS или LUW: использование учетной записи с высоким уровнем привилегий — опытного пользователя или администратора с правами на работу с пакетами и разрешениями BIND, BINDADD, GRANT EXECUTE TO PUBLIC — для однократного выполнения действия копирования. Необходимый пакет автоматически создается во время копирования. Для выполнения последующих действий копирования можно переключиться на обычную учетную запись.

## <a name="getting-started"></a>Приступая к работе
Вы можете создать конвейер с действием копирования для перемещения данных из локального хранилища данных DB2 с помощью различных инструментов и интерфейсов API: 

- Проще всего создать конвейер с помощью мастера копирования фабрики данных Azure. Краткие пошаговые указания по созданию конвейера с помощью мастера копирования приведены в статье [Руководство. Создание конвейера с действием копирования с помощью мастера копирования фабрики данных](data-factory-copy-data-wizard-tutorial.md). 
- Также для создания конвейера можно использовать такие инструменты, как портал Azure, Visual Studio, Azure PowerShell, шаблон Azure Resource Manager, API .NET и REST API. Пошаговые инструкции по созданию конвейера с действием копирования см. в [руководстве по действию копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

Независимо от используемого средства или API-интерфейса, для создания конвейера, который перемещает данные из источника данных в приемник, выполняются следующие шаги:

1. Создайте связанные службы, чтобы связать входные и выходные данные с фабрикой данных.
2. Создайте наборы данных, которые представляют входные и выходные данные для операции копирования. 
3. Создайте конвейер с действием копирования, который принимает входной набор данных и возвращает выходной набор данных. 

Если вы используете мастер копирования, то определения JSON для сущностей фабрики данных (связанных служб, наборов данных и конвейера) создаются автоматически. При использовании инструментов или интерфейсов API (за исключением API .NET) вы самостоятельно определяете сущности фабрики данных в формате JSON. В разделе [Пример JSON. Копирование данных из DB2 в хранилище BLOB-объектов Azure](#json-example-copy-data-from-db2-to-azure-blob) показаны определения JSON для сущностей фабрики данных, которые используются для копирования данных из локального хранилища данных DB2.

Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, характерных для хранилища данных DB2.

## <a name="db2-linked-service-properties"></a>Свойства связанной службы DB2
В следующей таблице перечислены свойства JSON, характерные для связанной службы DB2.

| Свойство | ОПИСАНИЕ | Обязательно |
| --- | --- | --- |
| **type** |Этому свойству необходимо задать значение **OnPremisesDB2**. |Yes |
| **server** |Имя сервера DB2. |Yes |
| **database** |Имя базы данных DB2. |Yes |
| **schema** |Имя схемы в базе данных DB2. Это свойство чувствительно к регистру. |Нет  |
| **authenticationType** |Тип аутентификации, используемый для подключения к базе данных DB2. Возможные значения: "Анонимная", "Обычная" и "Windows". |Yes |
| **username** |Имя для учетной записи пользователя, если используемая аутентификация имеет тип "Обычная" или "Windows". |Нет  |
| **password** |Пароль для учетной записи пользователя. |Нет  |
| **gatewayName** |Имя шлюза, который следует использовать службе фабрики данных для подключения к локальной базе данных DB2. |Yes |

## <a name="dataset-properties"></a>Свойства набора данных
Список разделов и свойств, используемых для определения наборов данных, см. в статье [Наборы данных в фабрике данных Azure](data-factory-create-datasets.md). Разделы **structure**, **availability** и **policy** для JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, хранилище BLOB-объектов, хранилище таблиц Azure и т. д.).

Раздел **typeProperties** во всех типах наборов данных разный. В нем содержатся сведения о расположении данных в хранилище данных. Раздел **typeProperties** набора данных с типом **RelationalTable**, который включает набор данных DB2, имеет следующее свойство:

| Свойство | ОПИСАНИЕ | Обязательно |
| --- | --- | --- |
| **tableName** |Имя таблицы в экземпляре базы данных DB2, на которое ссылается связанная служба. Это свойство чувствительно к регистру. |Нет (если указано свойство **query** действия копирования типа **RelationalSource**). |

## <a name="copy-activity-properties"></a>Свойства действия копирования
Список разделов и свойств, используемых для определения действий копирования, см. в статье [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md). Свойства действия копирования, такие как **имя**, **описание**, **входные** и **выходные** таблицы и **политика**, доступны для всех типов действий. Свойства, доступные в разделе действия **typeProperties**, зависят от типа действия. Для действия копирования свойства различаются в зависимости от типов источников и приемников данных.

Для действия копирования, когда источник относится к типу **RelationalSource** (который содержит DB2), в разделе **typeProperties** доступны следующие свойства:

| Свойство | ОПИСАНИЕ | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| **query** |Используйте пользовательский запрос для чтения данных. |Строка запроса SQL. Например: `"query": "select * from "MySchema"."MyTable""` |Нет (если для свойства **tableName** задано значение dataset). |

> [!NOTE]
> В именах схем и таблиц учитывается регистр. В инструкции запроса заключите имена свойств в двойные кавычки ("").

## <a name="json-example-copy-data-from-db2-to-azure-blob-storage"></a>Пример JSON. Копирование данных из DB2 в хранилище BLOB-объектов Azure
Ниже приведены примеры определений JSON, которые можно использовать для создания конвейера с помощью [портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). В примере показано, как скопировать данные из базы данных DB2 в хранилище BLOB-объектов. Тем не менее данные можно скопировать в [любой поддерживаемый тип хранилища-приемника данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью действия копирования в фабрике данных Azure.

Пример содержит следующие сущности фабрики данных.

- Связанная служба DB2 типа [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties).
- Связанная служба хранилища BLOB-объектов Azure типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
- Входной [набор данных](data-factory-create-datasets.md) типа [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties).
- Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
- [Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются свойства [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

В примере данные из результата запроса в базе данных DB2 каждый час копируются в BLOB-объект Azure. Используемые в этом примере свойства JSON описаны в разделах, следующих за определениями сущностей.

Сначала установите и настройте шлюз данных. Инструкции см. в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md).

**Связанная служба DB2**

```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

**Связанная служба хранилища BLOB-объектов Azure**

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

**Входной набор данных DB2**

В примере предполагается, что таблица MyTable уже создана в DB2 и содержит столбец timestamp для данных временных рядов.

Свойству **external** присвоено значение true. Это значение означает, что служба фабрики данных считает этот набор данных внешним по отношению к себе и не созданным в результате какого-либо действия в фабрике данных. Обратите внимание, что свойству **type** присвоено значение **RelationalTable**.


```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
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

Данные записываются в новый большой двоичный объект каждый час. Для этого свойству **frequency** присваивается значение Hour, а свойству **interval** — 1. Свойство **folderPath** для большого двоичного объекта вычисляется динамически на основе времени начала обрабатываемого среза. В пути к папке используется год, месяц, день и час времени начала.

```json
{
    "name": "AzureBlobDb2DataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/db2/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Конвейер для действия копирования**

Конвейер содержит действие копирования, которое настроено использовать указанные входной и выходной наборы данных и выполняется каждый час. В определении JSON для конвейера типу **source** присвоено значение **RelationalSource**, а типу **sink** — значение **BlobSink**. SQL-запрос, заданный для свойства **query**, выбирает данные из таблицы Orders.

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for the copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"Orders\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "Db2DataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDb2DataSet"
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
                "name": "Db2ToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-db2"></a>Сопоставление типов для DB2
Как упоминалось в статье о [действиях перемещения данных](data-factory-data-movement-activities.md), во время копирования типы источников автоматически преобразовываются в типы приемников. Такое преобразование выполняется в два этапа:

1. Преобразование собственных типов источников в тип .NET.
2. Преобразование типа .NET в собственный тип приемника.

Когда действие копирования преобразует данные из типа DB2 в тип .NET, используются следующие сопоставления:

| Тип базы данных DB2 | Тип .NET Framework |
| --- | --- |
| SmallInt |Int16 |
| Целое число  |Int32 |
| BigInt |Int64 |
| Real |Single |
| Double |Double |
| Float |Double |
| Decimal |Decimal |
| DecimalFloat |Decimal |
| Числовой |Decimal |
| Дата |Datetime |
| Время |Интервал времени |
| Timestamp |Datetime |
| xml |Byte[] |
| Char |Строка |
| VarChar |Строка |
| LongVarChar |Строка |
| DB2DynArray |Строка |
| Binary |Byte[] |
| VarBinary |Byte[] |
| LongVarBinary |Byte[] |
| Graphic |Строка |
| VarGraphic |Строка |
| LongVarGraphic |Строка |
| Clob |Строка |
| BLOB-объект |Byte[] |
| DbClob |Строка |
| SmallInt |Int16 |
| Целое число  |Int32 |
| BigInt |Int64 |
| Real |Single |
| Double |Double |
| Float |Double |
| Decimal |Decimal |
| DecimalFloat |Decimal |
| Числовой |Decimal |
| Дата |Datetime |
| Время |Интервал времени |
| Timestamp |Datetime |
| xml |Byte[] |
| Char |Строка |

## <a name="map-source-to-sink-columns"></a>Сопоставление столбцов источника и приемника
Сведения о сопоставлении столбцов в наборе данных, используемом в качестве источника, со столбцами в приемнике см. в статье [Сопоставление столбцов исходного набора данных со столбцами целевого набора данных](data-factory-map-columns.md).

## <a name="repeatable-reads-from-relational-sources"></a>Повторяющиеся операции чтения из реляционных источников
При копировании данных из реляционных хранилищ важно помнить о повторяемости, чтобы избежать непредвиденных результатов. В фабрике данных Azure можно вручную повторно выполнить срез. Вы можете также настроить для набора данных свойство **policy** повтора, чтобы при сбое срез выполнялся повторно. Убедитесь в том, что считываются те же данные, независимо от того, сколько раз и как выполняется срез. Дополнительные сведения см. в разделе [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Производительность и настройка
Сведения о ключевых факторах, влияющих на производительность действия копирования, и различных способах оптимизации этого процесса см. в статье [Руководство по настройке производительности действия копирования](data-factory-copy-activity-performance.md).
