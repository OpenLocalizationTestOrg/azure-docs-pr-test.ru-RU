---
title: "Копирование данных из Sybase с помощью фабрики данных Azure | Документация Майкрософт"
description: "Узнайте, как копировать данные из Sybase в поддерживаемые хранилища данных в качестве приемников с помощью действия копирования в конвейере фабрики данных Azure."
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
ms.date: 01/10/2018
ms.author: jingwang
ms.openlocfilehash: 47aabaf8512a7fffc189255212010efb5389f38a
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/23/2018
---
# <a name="copy-data-from-sybase-using-azure-data-factory"></a>Копирование данных из Sybase с помощью фабрики данных Azure
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Версия 1 — общедоступная](v1/data-factory-onprem-sybase-connector.md)
> * [Версия 2 — предварительная](connector-sybase.md)

В этой статье описывается, как с помощью действия копирования в фабрике данных Azure копировать данные из базы данных Sybase. Это продолжение [статьи об обзоре действия копирования](copy-activity-overview.md), в которой представлены общие сведения о действии копирования.

> [!NOTE]
> Эта статья относится к версии 2 фабрики данных, которая в настоящее время доступна в предварительной версии. Если используется служба фабрики данных версии 1, которая является общедоступной, ознакомьтесь со статьей [Перемещение данных из Sybase с помощью фабрики данных Azure](v1/data-factory-onprem-sybase-connector.md).

## <a name="supported-capabilities"></a>Поддерживаемые возможности

Вы можете скопировать данные из базы данных Sybase в любое хранилище данных, поддерживаемое в качестве приемника. Список хранилищ данных, которые поддерживаются в качестве источников и приемников для действия копирования, приведен в таблице [Поддерживаемые хранилища данных и форматы](copy-activity-overview.md#supported-data-stores-and-formats).

В частности, этот соединитель Sybase поддерживает:

- Sybase **версии 16 и выше**;
- копирование данных с использованием **базовой** проверки подлинности или проверки подлинности **Windows**.

## <a name="prerequisites"></a>предварительным требованиям

Для использования этого соединителя Sybase вам нужно:

- Настроить локальную среду выполнения интеграции. Дополнительные сведения см. в статье [Создание и настройка локальной среды выполнения интеграции](create-self-hosted-integration-runtime.md).
- Установить [поставщик данных для Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) версии 16 или более поздней на машине со средой выполнения интеграции.

## <a name="getting-started"></a>Приступая к работе

[!INCLUDE [data-factory-v2-connector-get-started](../../includes/data-factory-v2-connector-get-started.md)]

Следующие разделы содержат сведения о свойствах, которые используются для определения объектов фабрики данных, относящихся к соединителю Sybase.

## <a name="linked-service-properties"></a>Свойства связанной службы

Для связанной службы Sybase поддерживаются следующие свойства:

| Свойство | ОПИСАНИЕ | Обязательно |
|:--- |:--- |:--- |
| Тип | Для свойства type необходимо задать значение **Sybase**. | Yes |
| server | Имя сервера Sybase. |Yes |
| database | Имя базы данных Sybase. |Yes |
| schema | Имя схемы в базе данных. |Нет  |
| authenticationType | Тип проверки подлинности, используемый для подключения к базе данных Sybase.<br/>Допустимые значения: **Basic** и **Windows**. |Yes |
| Имя пользователя | Укажите имя пользователя для подключения к базе данных Sybase. |Yes |
| password | Введите пароль для учетной записи пользователя, указанной для выбранного имени пользователя. Пометьте это поле в качестве SecureString. |Yes |
| connectVia | [Среда выполнения интеграции](concepts-integration-runtime.md), используемая для подключения к хранилищу данных. Требуется локальная среда IR, как упоминалось в разделе [Предварительные требования](#prerequisites). |Yes |

**Пример.**

```json
{
    "name": "SybaseLinkedService",
    "properties": {
        "type": "Sybase",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "authenticationType": "Basic",
            "username": "<username>",
            "password": {
                "type": "SecureString",
                "value": "<password>"
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

Полный список разделов и свойств, доступных для определения наборов данных, см. в статье о наборах данных. В этом разделе содержится список свойств, поддерживаемых набором данных Sybase.

Чтобы скопировать данные из Sybase, задайте для свойства type набора данных значение **RelationalTable**. Поддерживаются следующие свойства:

| Свойство | ОПИСАНИЕ | Обязательно |
|:--- |:--- |:--- |
| Тип | Свойство type для набора данных должно иметь значение **RelationalTable**. | Yes |
| tableName | Имя таблицы в базе данных Sybase. | Нет (если свойство query указано в источнике действия) |

**Пример**

```json
{
    "name": "SybaseDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": {
            "referenceName": "<Sybase linked service name>",
            "type": "LinkedServiceReference"
        },
        "typeProperties": {}
    }
}
```

## <a name="copy-activity-properties"></a>Свойства действия копирования

Полный список разделов и свойств, используемых для определения действий, см. в статье [Конвейеры и действия в фабрике данных Azure](concepts-pipelines-activities.md). Этот раздел содержит список свойств, поддерживаемых Sybase в качестве источника.

### <a name="sybase-as-source"></a>Sybase в качестве источника

Чтобы скопировать данные из Sybase, задайте тип источника **RelationalSource** в действии копирования. В разделе **source** действия копирования поддерживаются следующие свойства:

| Свойство | ОПИСАНИЕ | Обязательно |
|:--- |:--- |:--- |
| Тип | Свойство type источника действия копирования должно иметь значение **RelationalSource**. | Yes |
| query | Используйте пользовательский SQL-запрос для чтения данных. Например, `"SELECT * FROM MyTable"`. | Нет (если для набора данных задано свойство tableName) |

**Пример.**

```json
"activities":[
    {
        "name": "CopyFromSybase",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Sybase input dataset name>",
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
                "type": "RelationalSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="data-type-mapping-for-sybase"></a>Сопоставление типов для Sybase

При копировании данных из Sybase используются сопоставления типов данных Sybase с промежуточными типами данных фабрики данных Azure. Дополнительные сведения о том, как действие копирования сопоставляет исходную схему и типы данных для приемника, см. в статье [Сопоставление схем в действии копирования](copy-activity-schema-and-type-mapping.md).

Sybase поддерживает типы T-SQL. Таблицы сопоставлений SQL типов к типам промежуточных данных фабрики данных Azure см. в разделе [Data type mapping for Azure SQL Database](connector-azure-sql-database.md#data-type-mapping-for-azure-sql-database) (Отображение типа данных для базы данных Azure SQL) статьи "Copy data to or from Azure SQL Database by using Azure Data Factory" (Копирование данных в или из базы данных Azure SQL с использованием фабрики данных Azure).


## <a name="next-steps"></a>Дополнительная информация
В таблице [Поддерживаемые хранилища данных](copy-activity-overview.md#supported-data-stores-and-formats) приведен список хранилищ данных, которые поддерживаются в качестве источников и приемников для действия копирования в фабрике данных Azure.