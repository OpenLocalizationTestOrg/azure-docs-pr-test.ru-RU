---
title: "aaaMove данные из фабрики данных с помощью Cassandra | Документы Microsoft"
description: "Узнайте, как данные toomove из Cassandra локальной базы данных с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 085cc312-42ca-4f43-aa35-535b35a102d5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 0e265d3a8439d0a2cb2a5c32e5ea8348a1617621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a>Перемещение данных из локальной базы данных Cassandra с помощью фабрики данных Azure
В этой статье объясняется, как toouse hello действие копирования в данных toomove фабрики данных Azure из Cassandra локальной базы данных. Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.

Можно скопировать данные из локальной Cassandra хранилища поддерживается tooany приемник данных хранилища данных. Список данных поддерживается хранилищ, приемники действием копирования hello см hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы. Фабрика данных в настоящее время поддерживает только при перемещении данных из данных Cassandra хранения tooother хранилищ данных, но не для перемещения данных из других данных Cassandra tooa хранилищ данных хранилища. 

## <a name="supported-versions"></a>Поддерживаемые версии
Hello Cassandra соединитель поддерживает следующие версии Cassandra hello: 2.X.

## <a name="prerequisites"></a>Предварительные требования
Для hello фабрики данных Azure toobe может tooconnect tooyour локальной Cassandra базы данных службы, необходимо установить шлюз управления данными на hello же машины, hello размещение базы данных или на отдельном компьютере tooavoid, конкурировать за ресурсы с hello База данных. Шлюз управления данными — это компонент, который подключается образом безопасности и управления локальными службами toocloud источники данных. Дополнительные сведения о шлюзе управления данными см. в статье [Шлюз управления данными](data-factory-data-management-gateway.md). В разделе [перемещения данных из локальной toocloud](data-factory-move-data-between-onprem-and-cloud.md) статье пошаговые инструкции по настройке шлюза hello toomove конвейера данных.

Необходимо использовать hello шлюза tooconnect tooa Cassandra базы данных, даже если hello база данных размещается в облаке hello, например, на виртуальной Машине Azure IaaS. Y которых имеются hello шлюза на hello одной виртуальной Машины, hello размещение базы данных или на отдельной виртуальной Машине, при условии, что шлюз hello подключения toohello базы данных.  

При установке шлюза hello автоматически устанавливает Microsoft Cassandra ODBC tooconnect драйвер, используемый tooCassandra базы данных. Таким образом, не требуется toomanually установить любой драйвер на компьютере шлюза hello при копировании данных из базы данных Cassandra hello. 

> [!NOTE]
> Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).

## <a name="getting-started"></a>Приступая к работе
Вы можете создать конвейер с действием копирования, которое перемещает данные из локального хранилища данных Cassandra, с помощью разных инструментов и интерфейсов API. 

- toocreate простым способом Hello конвейера — toouse hello **мастер копирования**. В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера. 
- Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**. В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования. 

Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.

1. Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.
2. Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования. 
3. Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных. 

При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически. При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.  Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из хранилища данных в локальной Cassandra см [пример JSON: копирования данных из Cassandra tooAzure большого двоичного объекта](#json-example-copy-data-from-cassandra-to-azure-blob) этой статьи. 

Hello в следующих разделах подробно JSON свойства, используемые toodefine фабрики данных сущностей определенного tooa Cassandra хранилища данных:

## <a name="linked-service-properties"></a>Свойства связанной службы
Hello в следующей таблице приводится описание службы конкретных tooCassandra связанные элементы JSON.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| type |свойство типа Hello должно быть присвоено: **OnPremisesCassandra** |Да |
| host |Один или несколько IP-адресов или имен узлов серверов Cassandra.<br/><br/>Укажите список разделенных запятой IP-адреса или имена серверов tooall tooconnect одновременно. |Да |
| порт |TCP-порт, который hello Cassandra server Hello использует toolisten для клиентских подключений. |Нет. Значение по умолчанию — 9042 |
| authenticationType |Укажите тип Basic или Anonymous |Да |
| Имя пользователя |Укажите имя пользователя для учетной записи пользователя hello. |Да, если tooBasic authenticationType. |
| пароль |Укажите пароль для учетной записи пользователя hello. |Да, если tooBasic authenticationType. |
| gatewayName |имя шлюза hello, используемые tooconnect toohello Hello локальной Cassandra базы данных. |Да |
| encryptedCredential |Учетные данные, зашифрованные шлюзом hello. |Нет |

## <a name="dataset-properties"></a>Свойства набора данных
Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи. Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).

Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello. Hello typeProperties статьи для набора данных типа **CassandraTable** имеет следующие свойства hello

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| keyspace |Имя hello пространство ключей или схемы в базе данных Cassandra. |Да (если для **CassandraSource** не определено значение **query**). |
| tableName |Имя таблицы hello Cassandra базы данных. |Да (если для **CassandraSource** не определено значение **query**). |

## <a name="copy-activity-properties"></a>Свойства действия копирования
Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи. Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.

В то время как свойства в разделе typeProperties hello hello действия зависят от типа каждого действия. Для действия копирования они зависят от типов источников и приемников hello.

Если источник имеет тип **CassandraSource**, hello следующие свойства доступны в разделе "typeProperties":

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| query |Используйте данные tooread hello пользовательского запроса. |Запрос SQL-92 или CQL. Ознакомьтесь со [справочником по CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html). <br/><br/>При использовании SQL-запрос, укажите **keyspace name.table имя** toorepresent hello таблицу tooquery. |Нет (если в наборе данных определены свойства tableName и keyspace) |
| consistencyLevel |уровень согласованности Hello указывает, сколько реплик должен вернуть запрос чтения tooa до возвращения данных toohello клиентское приложение. Проверяет Cassandra hello указанное число реплик, для запроса на чтение данных toosatisfy hello. |ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE. Дополнительные сведения см. в статье [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) (Настройка согласованности данных). |Нет. Значение по умолчанию — ONE |

## <a name="json-example-copy-data-from-cassandra-tooazure-blob"></a>Пример JSON: копирование данных из Cassandra tooAzure больших двоичных объектов
В этом примере представлен образец определения JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). В нем показано, как данные toocopy из Cassandra локальной базы данных tooan хранилища больших двоичных объектов. Тем не менее, данные могут быть скопированный tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.

> [!IMPORTANT]
> Этот пример содержит фрагменты кода JSON. Он не включает пошаговые инструкции по созданию фабрики данных hello. Эти инструкции приведены в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md) .

Образец Hello имеет hello, следуя сущностей фабрики данных.

* Связанная служба типа [OnPremisesCassandra](#linked-service-properties).
* Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Входной [набор данных](data-factory-create-datasets.md) типа [CassandraTable](#dataset-properties).
* Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* [Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [CassandraSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

**Связанная служба Cassandra**

В этом примере используется hello **Cassandra** связанной службы. В разделе [Cassandra связанная служба](#linked-service-properties) раздел для hello свойства, поддерживаемые этой связанной службы.  

```json
{
    "name": "CassandraLinkedService",
    "properties":
    {
        "type": "OnPremisesCassandra",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "host": "mycassandraserver",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

**Связанная служба хранилища Azure**

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

**Входной набор данных Cassandra**

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "mykeyspace"
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

**Выходной набор данных BLOB-объекта Azure**

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
            "folderPath": "adfgetstarted/fromcassandra"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Действие копирования в конвейере с базой данных Cassandra в качестве источника и BLOB-объектом в качестве приемника**

Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**CassandraSource** и **приемник** тип установлен слишком**BlobSink**.

В разделе [свойства типа RelationalSource](#copy-activity-properties) список свойств, поддерживаемых hello RelationalSource hello.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "CassandraInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"

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

### <a name="type-mapping-for-cassandra"></a>Сопоставление типов для Cassandra
| Тип данных Cassandra | Тип данных на основе .NET |
| --- | --- |
| ASCII |Строка |
| BIGINT |Int64 |
| BLOB |Byte[] |
| BOOLEAN |BOOLEAN |
| DECIMAL |DECIMAL |
| DOUBLE |DOUBLE |
| FLOAT |Single |
| INET |Строка |
| INT |Int32 |
| TEXT |Строка |
| TIMESTAMP |DateTime |
| TIMEUUID |Guid |
| UUID |Guid |
| VARCHAR |Строка |
| VARINT |Decimal |

> [!NOTE]
> Коллекция типов (карты, набор, список, т. д.), см. в разделе слишком[работать с Cassandra типов коллекций, с помощью виртуальной таблицы](#work-with-collections-using-virtual-table) раздела.
>
> Пользовательские типы не поддерживаются.
>
> Длина Hello длины двоичного столбца и строки столбцов не может превышать 4000.
>
>

## <a name="work-with-collections-using-virtual-table"></a>Работа с коллекциями с использованием виртуальной таблицы
Фабрика данных Azure использует встроенные ODBC драйвера tooconnect tooand копирования данных из базы данных Cassandra. Для типов коллекций, включая карты, набор и список драйвер hello сопряженный hello данных в соответствующей виртуальной таблицы. В частности Если таблица содержит коллекцию столбцов, hello драйвер создает следующие виртуальные таблицы hello:

* Объект **базовой таблицы**, который содержит hello и тех же данных как hello реальную таблицу за исключением hello коллекции столбцов. Hello базовая таблица использует hello точно такое же имя в качестве hello реальную таблицу, который он представляет.
* Объект **виртуальную таблицу** для каждого столбца в коллекции, который расширяет hello вложенные данные. Hello виртуальные таблицы, которые представляют собой коллекции именуются с использованием имени hello hello реальную таблицу с разделителем "*vt*» и hello имя столбца hello.

Виртуальные таблицы ссылки toohello данные реальном таблицы hello, включение tooaccess драйвер hello hello денормализованные данные. Дополнительные сведения см. в разделе "Пример". Можно получить доступ к hello содержимое коллекций Cassandra, запрашивая и соединение таблиц виртуальных hello.

Можно использовать hello [мастер копирования](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively представление hello список таблиц в базе данных Cassandra, включая виртуальные таблицы hello и предварительного просмотра данных hello внутри. Можно также создать запрос в приветствия мастера копирования и toosee hello результат проверки.

### <a name="example"></a>Пример
Например hello следующие «ExampleTable» является Cassandra таблицу базы данных, содержащую целочисленный столбец первичного ключа с именем «pk_int», текстовый столбец с именем value, столбца списка, столбец карты и представляющий собой набор столбцов (с именем «StringSet»).

| pk_int | Значение | список | Сопоставление | StringSet |
| --- | --- | --- | --- | --- |
| 1 |"пример значения 1" |["1", "2", "3"] |{"S1": "a", "S2": "b"} |{"A", "B", "C"} |
| 3 |"пример значения 3" |["100", "101", "102", "105"] |{"S1": "t"} |{"A", "E"} |

драйвер Hello, создает несколько toorepresent виртуальные таблицы этой таблице. Hello столбцы внешних ключей в таблицах виртуального hello ссылаться hello столбцы первичного ключа в таблице реальные hello и указать, какие реального соответствует таблице строки hello виртуальную таблицу, в строке.

первая виртуальная таблица Hello — hello базовой таблицы с именем «ExampleTable» отображается в следующей таблице hello. Hello базовая таблица содержит hello и тех же данных как hello исходной таблицы базы данных, за исключением hello коллекции, которые исключаются из этой таблицы, которые развернуты в других виртуальные таблицы.

| pk_int | Значение |
| --- | --- |
| 1 |"пример значения 1" |
| 3 |"пример значения 3" |

Hello следующих таблицах показаны hello виртуальные таблицы, которые renormalize hello данные из столбцов списка, карты и StringSet hello. Hello столбцы с именами, которые заканчиваются на «_index» или «сер_вера» укажите позицию hello hello данные в исходном списке hello или карты. Hello столбцы с именами, которые заканчиваются на «_value» содержат данные hello развернут hello коллекции.

#### <a name="table-exampletablevtlist"></a>Таблица ExampleTable_vt_List
| pk_int | List_index | List_value |
| --- | --- | --- |
| 1 |0 |1 |
| 1 |1 |2 |
| 1 |2 |3 |
| 3 |0 |100 |
| 3 |1 |101 |
| 3 |2 |102 |
| 3 |3 |103 |

#### <a name="table-exampletablevtmap"></a>Таблица ExampleTable_vt_Map
| pk_int | Map_key | Map_value |
| --- | --- | --- |
| 1 |S1 |Файл , |
| 1 |S2 |b |
| 3 |S1 |t |

#### <a name="table-exampletablevtstringset"></a>Таблица ExampleTable_vt_StringSet:
| pk_int | StringSet_value |
| --- | --- |
| 1 |Файл , |
| 1 |b |
| 1 |C |
| 3 |Файл , |
| 3 |E |

## <a name="map-source-toosink-columns"></a>Сопоставить исходные столбцы toosink
toolearn о сопоставление столбцов в toocolumns исходного набора данных в наборе данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Повторяющиеся операции чтения из реляционных источников
При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты. В фабрике данных Azure можно вручную повторно выполнить срез. Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно. При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез. Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Производительность и настройка
В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.
