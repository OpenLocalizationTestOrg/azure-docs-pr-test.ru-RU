---
title: "Копирование данных в базу данных Oracle и из нее с помощью фабрики данных Azure | Документация Майкрософт"
description: "Узнайте, как копировать данные из поддерживаемых исходных хранилищ в базу данных Oracle или из базы данных Oracle в поддерживаемый приемник хранилища данных с помощью фабрики данных."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2018
ms.author: jingwang
ms.openlocfilehash: 10db7959396b4ee9927e4272dec9939ac8c13580
ms.sourcegitcommit: c4cc4d76932b059f8c2657081577412e8f405478
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/11/2018
---
# <a name="copy-data-from-and-to-oracle-using-azure-data-factory"></a>Копирование данных из Oracle и обратно с помощью фабрики данных Azure
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Версия 1 — общедоступная](v1/data-factory-onprem-oracle-connector.md)
> * [Версия 2 — предварительная](connector-oracle.md)

В этой статье описывается, как с помощью действия копирования в фабрике данных Azure копировать данные в базу данных Oracle и из нее. Это продолжение [статьи об обзоре действия копирования](copy-activity-overview.md), в которой представлены общие сведения о действии копирования.

> [!NOTE]
> Эта статья относится к версии 2 фабрики данных, которая в настоящее время доступна в предварительной версии. Если используется служба фабрики данных версии 1, которая является общедоступной версией, ознакомьтесь со статьей [Копирование данных в локальную базу данных Oracle и обратно с помощью фабрики данных Azure](v1/data-factory-onprem-oracle-connector.md).

## <a name="supported-capabilities"></a>Поддерживаемые возможности

Данные можно скопировать из любого поддерживаемого в качестве источника хранилища данных в базу данных Oracle или из базы данных Oracle в любое поддерживаемое в качестве приемника хранилище данных. Список хранилищ данных, которые поддерживаются в качестве источников и приемников для действия копирования, приведен в таблице [Поддерживаемые хранилища данных и форматы](copy-activity-overview.md#supported-data-stores-and-formats).

В частности, этот соединитель Oracle поддерживает приведенные ниже версии баз данных Oracle, а также поддерживает обычную проверку подлинности и аутентификацию OID.

- Oracle 12c R1 (12.1)
- Oracle 11g R1, R2 (11.1, 11.2)
- Oracle 10g R1, R2 (10.1, 10.2)
- Oracle 9i R1, R2 (9.0.1, 9.2)
- Oracle 8i R3 (8.1.7)

## <a name="prerequisites"></a>Необходимые компоненты

Чтобы копировать данные из базы данных Oracle, которая не является общедоступной, и в нее, необходимо настроить локальную среду IR. Дополнительные сведения см. в статье [Создание и настройка локальной среды выполнения интеграции](create-self-hosted-integration-runtime.md). Среда выполнения интеграции предоставляет встроенный драйвер Oracle, поэтому при копировании данных из Oracle вам не потребуется устанавливать драйвер вручную.

## <a name="getting-started"></a>Приступая к работе

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

Следующие разделы содержат сведения о свойствах JSON, которые используются для определения сущностей фабрики данных, относящихся к соединителю Oracle.

## <a name="linked-service-properties"></a>Свойства связанной службы

Для связанной службы Oracle поддерживаются следующие свойства:

| Свойство | ОПИСАНИЕ | Обязательное значение |
|:--- |:--- |:--- |
| Тип | Для свойства type необходимо задать значение **Oracle** | Yes |
| connectionString | Укажите сведения, необходимые для подключения к экземпляру базы данных Oracle. Пометьте это поле в качестве SecureString.<br><br>**Поддерживаемые типы подключений**: вы можете использовать **ИД безопасности Oracle** или **имя службы Oracle** для идентификации базы данных:<br>— с помощью идентификатора безопасности: `Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;`;<br>— с помощью имени службы: `Host=<host>;Port=<port>;ServiceName=<sid>;User Id=<username>;Password=<password>;`. | Yes |
| connectVia | [Среда выполнения интеграции](concepts-integration-runtime.md), используемая для подключения к хранилищу данных. Вы можете использовать локальную среду выполнения интеграции или среду выполнения интеграции Azure (если хранилище данных является общедоступным). Если не указано другое, по умолчанию используется интегрированная среда выполнения Azure. |Нет  |

**Пример.**

```json
{
    "name": "OracleLinkedService",
    "properties": {
        "type": "Oracle",
        "typeProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a>Свойства набора данных

Полный список разделов и свойств, доступных для определения наборов данных, см. в статье о наборах данных. В этом разделе содержится список свойств, поддерживаемых набором данных Oracle.

Чтобы скопировать данные из или в Oracle, установите свойство type набора данных **OracleTable**. Поддерживаются следующие свойства:

| Свойство | ОПИСАНИЕ | Обязательное значение |
|:--- |:--- |:--- |
| Тип | Свойство type для набора данных должно иметь значение **OracleTable**. | Yes |
| tableName |Имя таблицы в базе данных Oracle, на которое ссылается связанная служба. | Yes |

**Пример.**

```json
{
    "name": "OracleDataset",
    "properties":
    {
        "type": "OracleTable",
        "linkedServiceName": {
            "referenceName": "<Oracle linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {
            "tableName": "MyTable"
        }
    }
}
```

## <a name="copy-activity-properties"></a>Свойства действия копирования

Полный список разделов и свойств, используемых для определения действий, см. в статье [Конвейеры и действия в фабрике данных Azure](concepts-pipelines-activities.md). Этот раздел содержит список свойств, поддерживаемых типами источника Oracle и приемника.

### <a name="oracle-as-source"></a>Oracle в качестве источника

Чтобы копировать данные из Oracle, установите тип источника в действии копирования **OracleSource**. В разделе **source** действия копирования поддерживаются следующие свойства:

| Свойство | ОПИСАНИЕ | Обязательное значение |
|:--- |:--- |:--- |
| Тип | Свойство type источника действия копирования должно иметь значение **OracleSource**. | Yes |
| oracleReaderQuery | Используйте пользовательский SQL-запрос для чтения данных. Например, `"SELECT * FROM MyTable"`. | Нет  |

Если вы не укажете oracleReaderQuery, то для создания запроса (`select column1, column2 from mytable`) к базе данных Oracle будут использованы столбцы, определенные в разделе structure набора данных. Если в определении набора данных нет раздела structure, выбираются все столбцы из таблицы.

**Пример.**

```json
"activities":[
    {
        "name": "CopyFromOracle",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Oracle input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "OracleSource",
                "oracleReaderQuery": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

### <a name="oracle-as-sink"></a>Oracle в качестве приемника

Чтобы скопировать данные в базу данных Oracle, в операции копирования задайте тип приемника **OracleSink**. В разделе **sink** действия копирования поддерживаются следующие свойства:

| Свойство | ОПИСАНИЕ | Обязательное значение |
|:--- |:--- |:--- |
| Тип | Свойство type приемника действия копирования должно иметь значение **OracleSink**. | Yes |
| writeBatchSize | Вставляет данные в таблицу SQL, когда размер буфера достигает значения writeBatchSize.<br/>Допустимые значения: целое число (количество строк). |Нет (значение по умолчанию — 10 000) |
| writeBatchTimeout | Время ожидания до выполнения операции пакетной вставки, пока не завершится срок ее действия.<br/>Допустимые значения: промежуток времени. Пример: 00:30:00 (30 минут). | Нет  |
| preCopyScript | Перед записью данных в Oracle при каждом запуске указывайте SQL-запрос для выполнения операции копирования. Это свойство можно использовать для очистки предварительно загруженных данных. | Нет  |

**Пример.**

```json
"activities":[
    {
        "name": "CopyToOracle",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<Oracle output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "<source type>"
            },
            "sink": {
                "type": "OracleSink"
            }
        }
    }
]
```

## <a name="data-type-mapping-for-oracle"></a>Сопоставление типов данных для Oracle

При копировании данных из и в Oracle для промежуточных типов данных фабрики данных Azure используются следующие сопоставления из типов данных Oracle. Дополнительные сведения о том, как действие копирования сопоставляет исходную схему и типы данных для приемника, см. в статье [Сопоставление схем в действии копирования](copy-activity-schema-and-type-mapping.md).

| Тип данных Oracle | Тип промежуточных данных фабрики данных |
|:--- |:--- |
| BFILE |Byte[] |
| BLOB |Byte[]<br/>(поддерживается только в Oracle 10g и более поздних версий) |
| CHAR |Строка |
| CLOB |Строка |
| DATE |Datetime |
| FLOAT |десятичное число, строка (если точность больше 28) |
| INTEGER |десятичное число, строка (если точность больше 28) |
| LONG |Строка |
| LONG RAW |Byte[] |
| NCHAR |Строка |
| NCLOB |Строка |
| NUMBER |десятичное число, строка (если точность больше 28) |
| NVARCHAR2 |Строка |
| RAW |Byte[] |
| ROWID |Строка |
| TIMESTAMP |Datetime |
| TIMESTAMP WITH LOCAL TIME ZONE |Строка |
| TIMESTAMP WITH TIME ZONE |Строка |
| UNSIGNED INTEGER |NUMBER |
| VARCHAR2 |Строка |
| XML |Строка |

> [!NOTE]
> Типы данных INTERVAL YEAR TO MONTH и INTERVAL DAY TO SECOND не поддерживаются.


## <a name="next-steps"></a>Дополнительная информация
В таблице [Поддерживаемые хранилища данных](copy-activity-overview.md##supported-data-stores-and-formats) приведен список хранилищ данных, которые поддерживаются в качестве источников и приемников для действия копирования в фабрике данных Azure.