---
title: "aaaMove данных с помощью фабрики данных MongoDB | Документы Microsoft"
description: "Узнайте, как базы данных MongoDB toomove данные с помощью фабрики данных Azure."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 10ca7d9a-7715-4446-bf59-2d2876584550
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 154e85712f27b978976c7499c43dde9429f124c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a>Перемещение данных из MongoDB с помощью фабрики данных Azure
В этой статье объясняется, как toouse hello действие копирования в фабрики данных Azure toomove данные из локальной базы данных MongoDB. Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.

Можно скопировать данные из локальной MongoDB хранилища поддерживается tooany приемник данных хранилища данных. Список данных поддерживается хранилищ, приемники действием копирования hello см hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы. Фабрика данных в настоящее время поддерживает только при перемещении данных MongoDB хранения tooother хранилищ данных, но не для перемещения данных из хранилища данных MongoDB хранилищ tooan других данных. 

## <a name="prerequisites"></a>Предварительные требования
Для hello фабрики данных Azure toobe может tooconnect tooyour локальной MongoDB базы данных службы необходимо установить следующие компоненты hello:

- Поддерживаемые версии MongoDB: 2.4, 2.6, 3.0 и 3.2.
- Шлюз управления данными на hello компьютере hello узлов базы данных или на отдельный компьютер tooavoid, конкурирующие за ресурсы с базой данных hello. Шлюз управления данными — это программное обеспечение, который подключается образом безопасности и управления локальными службами toocloud источники данных. Дополнительные сведения о шлюзе управления данными см. в статье [Шлюз управления данными](data-factory-data-management-gateway.md). В разделе [перемещения данных из локальной toocloud](data-factory-move-data-between-onprem-and-cloud.md) статье пошаговые инструкции по настройке шлюза hello toomove конвейера данных.

    При установке шлюза hello автоматически устанавливает tooMongoDB tooconnect используется драйвер Microsoft MongoDB ODBC.

    > [!NOTE]
    > Необходимо toouse hello шлюза tooconnect tooMongoDB, даже если она размещается в виртуальных машинах IaaS Azure. Если вы пытаетесь экземпляр tooan tooconnect MongoDB, размещенной в облаке, также можно устанавливать экземпляр шлюза hello на hello ВМ IaaS.

## <a name="getting-started"></a>Приступая к работе
Вы можете создать конвейер с действием копирования, которое перемещает данные из локального хранилища данных MongoDB, с помощью разных инструментов и интерфейсов API.

toocreate простым способом Hello конвейера — toouse hello **мастер копирования**. В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.

Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**. В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования. 

Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello. 

1. Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.
2. Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования. 
3. Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных. 

При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически. При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.  Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из локального хранилища данных MongoDB см [пример JSON: копирования данных из tooAzure MongoDB больших двоичных объектов](#json-example-copy-data-from-mongodb-to-azure-blob) данной статьи. 

Hello в следующих разделах содержатся сведения о свойствах JSON, которые являются источником tooMongoDB определенных сущностей фабрики данных используется toodefine:

## <a name="linked-service-properties"></a>Свойства связанной службы
Hello Следующая таблица содержит описание для конкретных элементов JSON слишком**OnPremisesMongoDB** связанной службы.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| type |свойство типа Hello должно быть присвоено: **OnPremisesMongoDb** |Да |
| server |IP-адрес или имя сервера hello MongoDB. |Да |
| порт |TCP-порт, который hello MongoDB server использует toolisten для клиентских подключений. |Значение по умолчанию — 27017 (необязательно) |
| authenticationType |Укажите тип Basic или Anonymous |Да |
| Имя пользователя |Учетная запись пользователя, tooaccess MongoDB. |Да (если используется обычная проверка подлинности) |
| пароль |Пароль для пользователя hello. |Да (если используется обычная проверка подлинности) |
| authSource |Имя базы данных MongoDB hello, что требуется toouse toocheck учетные данные для проверки подлинности. |Необязательно (если используется обычная проверка подлинности). по умолчанию: используется учетная запись администратора hello и hello базы данных, указанный с помощью свойства databaseName. |
| databaseName |Имя базы данных MongoDB hello, которое следует tooaccess. |Да |
| gatewayName |Имя шлюза hello, который обращается к хранилищу данных hello. |Да |
| encryptedCredential |Учетные данные, зашифрованные шлюзом |Необязательно |

## <a name="dataset-properties"></a>Свойства набора данных
Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи. Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).

Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello. Hello typeProperties статьи для набора данных типа **MongoDbCollection** имеет hello следующие свойства:

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| collectionName |Имя коллекции hello базы данных MongoDB. |Да |

## <a name="copy-activity-properties"></a>Свойства действия копирования
Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи. Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.

Свойства, доступные в hello **typeProperties** раздел hello действий на hello другой стороны, зависят от типа каждого действия. Для действия копирования они зависят от типов источников и приемников hello.

Если источник hello имеет тип **MongoDbSource** hello следующие свойства доступны в разделе "typeProperties":

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| query |Используйте данные tooread hello пользовательского запроса. |Строка запроса SQL-92. Например, select * from MyTable. |Нет (если для свойства **collectionName** задано значение **dataset**). |



## <a name="json-example-copy-data-from-mongodb-tooazure-blob"></a>Пример JSON: копирование данных из tooAzure MongoDB больших двоичных объектов
В этом примере представлен образец определения JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Здесь показано, как данные toocopy из tooan MongoDB локального хранилища больших двоичных объектов. Тем не менее, данные могут быть скопированный tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.

Образец Hello имеет hello, следуя сущностей фабрики данных.

1. Связанная служба типа [OnPremisesMongoDb](#linked-service-properties).
2. Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Входной [набор данных](data-factory-create-datasets.md) типа [MongoDbCollection](#dataset-properties).
4. Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. [Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [MongoDbSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Образец Hello копирует данные из результатов запроса в большом двоичном объекте tooa базы данных MongoDB каждый час. свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.

В качестве первого шага установки шлюза управления данными hello согласно инструкциям hello hello [шлюз управления данными](data-factory-data-management-gateway.md) статьи.

**Связанная служба MongoDB**

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",  
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
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

**Входной набор данных MongoDB:** параметра «external»: «true» уведомляет службу hello фабрики данных, что таблица hello внешних toohello фабрики данных и не был создан из действия в фабрике данных hello.

```json
{
     "name":  "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"    
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

**Выходной набор данных BLOB-объекта Azure**

Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1). путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается. путь к папке Hello использует года, месяца, дня и часа части времени начала hello.

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/frommongodb/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

**Действие копирования в конвейере с MongoDB в качестве источника и большим двоичным объектом в качестве приемника**

конвейер Hello содержит операции копирования, настроенные toouse hello выше входные и выходные наборы данных и запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**MongoDbSource** и **приемник** тип установлен слишком**BlobSink**. запрос SQL Hello, указанный для hello **запроса** свойство выбирает данные hello в hello за час toocopy.

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "MongoDbSource",
                        "query": "$$Text.Format('select * from  MyTable where LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "MongoDbInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
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
                "name": "MongoDBToAzureBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```


## <a name="schema-by-data-factory"></a>Схема фабрики данных
Служба фабрики данных Azure выводит схему из коллекции MongoDB с использованием hello 100 последних документов в коллекции hello. Если эти 100 документы не содержат полную схему, некоторые столбцы могут игнорироваться во время операции копирования hello.

## <a name="type-mapping-for-mongodb"></a>Сопоставление типов для MongoDB
Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, действие копирования выполняет автоматического преобразования типов toosink типы источников с hello подходе шаг 2:

1. Преобразование из типа too.NET типы собственного источника
2. Преобразовываемый тип приемника toonative тип .NET

При перемещении данных tooMongoDB hello следующие сопоставления используются из MongoDB типы too.NET типы.

| Тип MongoDB | Тип .NET Framework |
| --- | --- |
| Binary |Byte[] |
| Логический |Логический |
| Дата |DateTime |
| NumberDouble |Double |
| NumberInt |Int32 |
| NumberLong |Int64 |
| ObjectID |Строковый |
| Строковый |Строковый |
| UUID |Guid |
| Объект |Преобразованный в плоские столбцы с "_" в качестве вложенного разделителя |

> [!NOTE]
> toolearn о поддержке массивов с помощью виртуальной таблицы ссылаться слишком[поддержка сложных типов с помощью виртуальной таблицы](#support-for-complex-types-using-virtual-tables) разделе ниже.

В настоящее время не поддерживаются следующие типы данных MongoDB hello: DBPointer, JavaScript, Max и Min ключа регулярного выражения, символ, Timestamp, не определено

## <a name="support-for-complex-types-using-virtual-tables"></a>Поддержка сложных типов с помощью виртуальных таблиц
Фабрика данных Azure использует встроенные ODBC драйвера tooconnect tooand копирования данных из базы данных MongoDB. Для сложных типов, таких как массивы и объекты с различными типами в документах hello драйвер hello повторно нормализует данных в соответствующей виртуальной таблицы. В частности Если таблица содержит такие столбцы, hello драйвер создает следующие виртуальные таблицы hello:

* Объект **базовой таблицы**, который содержит hello и тех же данных как hello Настоящая таблица, за исключением столбцов сложного типа hello. Hello базовая таблица использует hello точно такое же имя в качестве hello реальную таблицу, который он представляет.
* Объект **виртуальную таблицу** для каждого столбца сложный тип, который расширяет hello вложенные данные. Виртуальные таблицы Hello именуются hello имя реальную таблицу hello, разделитель «_», имя hello hello массива или объекта.

Виртуальные таблицы ссылки toohello данные реальном таблицы hello, включение tooaccess драйвер hello hello денормализованные данные. Дополнительные сведения см. в разделе "Примеры". Можно открыть содержимое hello MongoDB массивов, запрашивая и соединение таблиц виртуальных hello.

Можно использовать hello [мастер копирования](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively представление hello список таблиц в базе данных MongoDB, включая виртуальные таблицы hello и предварительного просмотра данных hello внутри. Можно также создать запрос в приветствия мастера копирования и toosee hello результат проверки.

### <a name="example"></a>Пример
Ниже приведен пример таблицы ExampleTable в базе данных MongoDB, содержащей столбец ("Счета") с массивом объектов в каждой ячейке и столбец с массивом данных скалярных типов ("Оценки").

| _№ | Имя клиента | Счета | Уровень обслуживания | Оценки |
| --- | --- | --- | --- | --- |
| 1111 |ABC |[{счет_№:"123", товар:"тостер", цена:"456", скидка:"0,2"}, {счет_№:"124", товар:"печь", цена: "1235", скидка: "0,2"}] |Silver |[5,6] |
| 2222 |XYZ |[{счет_№: "135", товар: "холодильник", цена: "12543", скидка: "0,0"}] |Gold |[1,2] |

драйвер Hello, создает несколько toorepresent виртуальные таблицы этой таблице. первая виртуальная таблица Hello — hello базовой таблицы с именем «ExampleTable», показано ниже. Hello базовая таблица содержит все данные hello hello исходной таблицы, но hello данных из массивов hello включен и развернуты в виртуальной таблице hello.

| _№ | Имя клиента | Уровень обслуживания |
| --- | --- | --- |
| 1111 |ABC |Silver |
| 2222 |XYZ |Gold |

Hello следующих таблицах показаны hello виртуальные таблицы, представляющих исходные массивы hello в примере hello. Эти таблицы содержат следующие hello:

* Обратная ссылка toohello исходный столбец первичного ключа соответствующей toohello строке исходного массива hello (с помощью hello _id столбец)
* Значение, указывающее положение hello hello данных в пределах исходного массива hello
* данные для каждого элемента в массиве hello развернут Hello

Таблица ExampleTable_Invoices:

| _№ | ExampleTable_Invoices_dim1_idx | счет_№ | item | price | Скидка |
| --- | --- | --- | --- | --- | --- |
| 1111 |0 |123 |тостер |456 |0,2 |
| 1111 |1 |124 |печь |1235 |0,2 |
| 2222 |0 |135 |холодильник |12543 |0,0 |

Таблица ExampleTable_Ratings:

| _№ | ExampleTable_Ratings_dim1_idx | ExampleTable_Ratings |
| --- | --- | --- |
| 1111 |0 |5 |
| 1111 |1 |6 |
| 2222 |0 |1 |
| 2222 |1 |2 |

## <a name="map-source-toosink-columns"></a>Сопоставить исходные столбцы toosink
toolearn о сопоставление столбцов в toocolumns исходного набора данных в наборе данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Повторяющиеся операции чтения из реляционных источников
При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты. В фабрике данных Azure можно вручную повторно выполнить срез. Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно. При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез. Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Производительность и настройка
В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.

## <a name="next-steps"></a>Дальнейшие действия
В разделе [перемещение данных между локальными и облачными](data-factory-move-data-between-onprem-and-cloud.md) статью пошаговые инструкции для создания конвейера данных, перемещает данные из локальных данных хранилище tooan данных Azure.
