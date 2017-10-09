---
title: "aaaMove данных из DB2, с помощью фабрики данных Azure | Документы Microsoft"
description: "Узнайте, как toomove данных из DB2 локальной базы данных с помощью действия копирования фабрики данных Azure"
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
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 696ac059be644cb3901c37d2fc746e0682c65a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a>Перемещение данных из DB2 с помощью действия копирования в фабрике данных Azure
В этой статье описывается, как можно использовать действие копирования фабрики данных Azure toocopy данных из хранилища данных tooa базы данных DB2 в локальной среде. Вы можете скопировать tooany хранилища данных, который указан как поддерживаемый приемник в hello [действия перемещения данных фабрики данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) статьи. В этом разделе основан на hello фабрики данных статьи, которая предоставляет обзор перемещения данных, используя действие копирования и перечислены сочетания хранилища данных hello поддерживается. 

Фабрика данных в настоящее время поддерживает только перемещение данных из базы данных DB2 tooa [поддерживаемых приемника хранилища данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats). Перемещение данных из других данных хранит tooa DB2, база данных не поддерживается.

## <a name="prerequisites"></a>Предварительные требования
Фабрика данных поддерживает подключения базы данных DB2 tooan локально с помощью hello [шлюз управления данными](data-factory-data-management-gateway.md). Пошаговые инструкции tooset hello шлюза данных конвейера toomove данные см hello [перемещения данных из локальной toocloud](data-factory-move-data-between-onprem-and-cloud.md) статьи.

Даже если hello DB2 размещается на виртуальной Машине Azure IaaS, требуется шлюз. Hello шлюз можно установить на hello же IaaS виртуальную Машину в качестве хранилища данных hello. Если шлюз hello может подключаться toohello базы данных, hello шлюз можно установить на другой виртуальной Машине.

Шлюз управления данными Hello предоставляет встроенные драйверы DB2, вам не нужно toomanually установить драйвер toocopy данных из DB2.

> [!NOTE]
> Советы по устранению неполадок шлюза проблем с соединением и см. в разделе hello [Устранение неполадок шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) статьи.


## <a name="supported-versions"></a>Поддерживаемые версии
Соединитель Hello DB2 фабрики данных поддерживает следующие платформы IBM DB2 и версии с версиями диспетчер доступа к реляционной базе данных DRDA (архитектуры распределенной) SQL, 9, 10 и 11 hello:

* IBM DB2 для z/OS версии 11.1
* IBM DB2 для z/OS версии 10.1
* IBM DB2 для i (AS400) версии 7.2
* IBM DB2 для i (AS400) версии 7.1
* IBM DB2 для Linux, UNIX и Windows (LUW) версии 11
* IBM DB2 для LUW версии 10.5
* IBM DB2 для LUW версии 10.1

> [!TIP]
> Если появляется сообщение об ошибке hello «hello пакета соответствующего tooan SQL инструкции выполнения запроса не найден. SQLSTATE = 51002 = SQLCODE-805, «hello обусловлено необходимые пакеты для hello обычного пользователя на hello ОС не создается. tooresolve эту проблему, выполните следующие действия для типа сервера DB2:
> - DB2 для i (AS400): позволяет power создания коллекции hello для hello обычного пользователя до выполнения операции копирования. Коллекция hello toocreate, используйте команду hello:`create collection <username>`
> - DB2 для z/OS или LUW: используйте учетную запись с высоким уровнем привилегий — опытного пользователя или администратора с центры пакета и ПРИВЯЗКА, BINDADD, ПРЕДОСТАВЬТЕ разрешения EXECUTE tooPUBLIC--toorun hello копирование один раз. необходимые пакеты Hello автоматически создается во время копирования hello. После этого можно переключиться назад toohello обычного пользователя для копирования последующих запусков.

## <a name="getting-started"></a>Приступая к работе
Можно создать конвейер с копирование данных toomove действия из локального хранилища данных DB2 с помощью различных средств и API-интерфейсы: 

- toocreate простым способом Hello конвейера — toouse hello мастер копирования фабрики данных Azure. Краткое Пошаговое руководство по созданию конвейера с помощью мастера копирования hello, в разделе hello [учебника: создать конвейер с помощью мастера копирования hello](data-factory-copy-data-wizard-tutorial.md). 
- Можно также использовать средства toocreate конвейера, включая hello портал Azure, Visual Studio, Azure PowerShell, диспетчера ресурсов Azure шаблона, hello .NET API и hello REST API. Пошаговые инструкции toocreate конвейер с операции копирования, в разделе hello [действие копирования учебника](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.

1. Создание связанных служб toolink входных и выходных данных сохраняет tooyour фабрики данных.
2. Создания наборов данных toorepresent входных и выходных данных для операции копирования hello. 
3. Создайте конвейер с действием копирования, который принимает входной набор данных и возвращает выходной набор данных. 

При использовании приветствия мастера копирования, определения JSON для службы фабрики данных связанных hello, конвейер сущностей и наборов данных автоматически создаются автоматически. При использовании средств или API-интерфейсы (за исключением hello .NET API), можно определить hello фабрики данных сущности, используя формат JSON hello. Hello [JSON пример: копирование данных из DB2 tooAzure хранилища больших двоичных объектов](#json-example-copy-data-from-db2-to-azure-blob) показаны определения JSON hello для hello сущностей фабрики данных, используемых toocopy данные из локального хранилища данных DB2.

Hello в следующих разделах содержатся сведения об hello JSON свойства, используемые toodefine hello фабрики данных сущностей, которые являются определенной tooa DB2 хранилища данных.

## <a name="db2-linked-service-properties"></a>Свойства связанной службы DB2
Привет, в следующей таблице перечислены свойства JSON hello, которые зависят от конкретного tooa DB2 связанной службы.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| **type** |Это свойство должно быть задано слишком**OnPremisesDB2**. |Да |
| **server** |Имя сервера hello DB2 Hello. |Да |
| **database** |Имя базы данных hello DB2 Hello. |Да |
| **schema** |Имя Hello hello схемы в базе данных hello DB2. Это свойство чувствительно к регистру. |Нет |
| **authenticationType** |Тип проверки подлинности, которая является базой данных toohello DB2 используется tooconnect Hello. Возможные значения Hello: анонимный, обычная проверка подлинности и Windows. |Да |
| **username** |Имя hello учетной записи пользователя при использовании проверки подлинности Basic или Windows Hello. |Нет |
| **password** |Hello пароль для учетной записи пользователя hello. |Нет |
| **gatewayName** |Имя Hello шлюза hello, hello служба фабрики данных следует использовать toohello для tooconnect локальной базы данных DB2. |Да |

## <a name="dataset-properties"></a>Свойства набора данных
Список разделов hello и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи. Разделы, таких как **структуры**, **доступности**и hello **политики** JSON набора данных, являются одинаковыми для всех типов наборов данных (SQL Azure, хранилище больших двоичных объектов Azure, таблица Azure хранилище и т. д).

Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello. Hello **typeProperties** раздел для набора данных типа **RelationalTable**, который включает набор данных hello DB2, имеет следующие свойства hello:

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| **tableName** |Имя таблицы hello в экземпляре базы данных hello DB2, hello связанной службы Hello ссылается. Это свойство чувствительно к регистру. |Нет (если hello **запроса** действия копирования типа **RelationalSource** указан) |

## <a name="copy-activity-properties"></a>Свойства действия копирования
Список разделов hello и свойства, доступные для определения действия копирования см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи. Свойства действия копирования, такие как **имя**, **описание**, **входные** и **выходные** таблицы и **политика**, доступны для всех типов действий. Здравствуйте, свойств, доступных в hello **typeProperties** раздел hello действия для каждого типа действия. Для действия копирования hello свойства зависят от типов источников данных и приемники hello.

Для действия копирования, когда источник hello типа **RelationalSource** (включая DB2), доступны следующие свойства hello в hello **typeProperties** раздела:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| **query** |Используйте tooread hello hello пользовательского запроса данных. |Строка запроса SQL. Например: `"query": "select * from "MySchema"."MyTable""` |Нет (если hello **tableName** указанного свойства набора данных) |

> [!NOTE]
> В именах схем и таблиц учитывается регистр. В инструкции запроса hello, заключите имена свойств с помощью «» (двойные кавычки). Например:
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-tooazure-blob-storage"></a>Пример JSON: копирование данных из DB2 tooAzure хранилища больших двоичных объектов
В этом примере представлен образец определения JSON можно использовать toocreate конвейера с помощью hello [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Hello примере показано, как данные toocopy из DB2 базы данных хранилища tooBlob. Тем не менее, данные можно скопировать слишком[все поддерживаемые данные хранить тип приемника](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью действия копирования фабрики данных Azure.

Образец Hello имеет hello, следуя сущностей фабрики данных.

- Связанная служба DB2 типа [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties).
- Связанная служба хранилища BLOB-объектов Azure типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
- Входной [набор данных](data-factory-create-datasets.md) типа [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties).
- Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)
- Объект [конвейера](data-factory-create-pipelines.md) действием копирования, которое использует hello [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) свойства

Образец Hello копирует данные из результатов запроса в tooan базы данных DB2 BLOB-объектов Azure каждый час. свойства Hello JSON, используемые в образце hello описаны в следующих разделах hello определений сущностей hello.

Сначала установите и настройте шлюз данных. Инструкции содержатся в hello [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) статьи.

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

Образец Hello предполагается, что вы создали таблицу в DB2, с именем «MyTable», что столбец с меткой «timestamp» для hello временного ряда данных.

Hello **внешних** задано слишком «true». Этот параметр сообщает hello служба фабрики данных, что этот набор данных является фабрикой toohello внешних данных, а не был создан из действия в фабрике данных hello. Обратите внимание, что hello **тип** задано слишком**RelationalTable**.


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

Записывается новый большой двоичный объект tooa каждый час параметр hello **частоты** свойство слишком «Час» и hello **интервал** too1 свойство. Hello **folderPath** свойства для большого двоичного объекта hello динамически вычисляется на основе hello время начала среза hello, обрабатывается. путь к папке Hello использует hello года, месяца, дня и часа части времени начала hello.

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

**Конвейер для действия копирования hello**

конвейер Hello содержит операции копирования, настроенный toouse указанного входного и выходного наборов данных, а какой запланированных toorun каждый час. В hello определения JSON для конвейера hello hello **источника** тип установлен слишком**RelationalSource** и hello **приемник** тип установлен слишком**BlobSink**. запрос SQL Hello, указанный для hello **запроса** свойство выбирает hello данные из таблицы «Заказы» hello.

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for hello copy activity",
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
Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, действие копирования выполняет автоматический тип преобразования из типа toosink тип источника, используя двухэтапный подходе hello:

1. Преобразование из типа .NET tooa тип источника
2. Преобразование из типа собственный приемник tooa тип .NET

Hello следующие сопоставления используются при действии копирования преобразует данные hello из типа DB2 tooa типа .NET.

| Тип базы данных DB2 | Тип .NET Framework |
| --- | --- |
| SmallInt |Int16 |
| Число |Int32 |
| BigInt |Int64 |
| Real |Single |
| Double |Double |
| Float |Double |
| Decimal |Decimal |
| DecimalFloat |Decimal |
| Числовой |Decimal |
| Дата |DateTime |
| Время |TimeSpan |
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
| Число |Int32 |
| BigInt |Int64 |
| Real |Single |
| Double |Double |
| Float |Double |
| Decimal |Decimal |
| DecimalFloat |Decimal |
| Числовой |Decimal |
| Дата |DateTime |
| Время |TimeSpan |
| Timestamp |Datetime |
| xml |Byte[] |
| Char |Строка |

## <a name="map-source-toosink-columns"></a>Сопоставить исходные столбцы toosink
статье toomap колонкам hello исходного набора данных toocolumns в наборе данных приемник hello, toolearn [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).

## <a name="repeatable-reads-from-relational-sources"></a>Повторяющиеся операции чтения из реляционных источников
При копировании данных из хранилища реляционных данных хранить повторяемость в виду tooavoid непредвиденные результаты. В фабрике данных Azure можно вручную повторно выполнить срез. Можно также настроить повтора hello **политики** свойства для набора данных toorerun срез, когда происходит сбой. Убедитесь, что hello и тех же данных считывается независимо от того, как много раз hello срез повторного запуска и независимо от того, как повторно запустить срез hello. Дополнительные сведения см. в разделе [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Производительность и настройка
Дополнительные сведения о ключевых факторов, влияющих на производительность hello действия копирования, а также способы toooptimize производительности в hello [производительности для действия копирования и руководство по настройке](data-factory-copy-activity-performance.md).
