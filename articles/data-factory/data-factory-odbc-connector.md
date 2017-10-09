---
title: "aaaMove данные из хранилищ данных ODBC | Документы Microsoft"
description: "Дополнительные сведения о хранением данных toomove из данных ODBC с помощью фабрики данных Azure."
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
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: bf96e71da449313b6144bb194205c572d2ca2030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a>Перемещение данных из хранилищ данных ODBC с помощью фабрики данных Azure
В этой статье объясняется, как хранить hello toouse действие копирования в фабрике данных Azure toomove данных из локальных данных ODBC. Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.

Можно скопировать данные из ODBC хранилища поддерживается tooany приемник данных хранилища данных. Список данных поддерживается хранилищ, приемники действием копирования hello см hello [поддерживается хранилищ данных](data-factory-data-movement-activities.md#supported-data-stores-and-formats) таблицы. Фабрика данных в настоящее время поддерживает только при перемещении данных из объекта данных ODBC хранения tooother хранилищ данных, но не для переноса данных из другого хранилища данных сохраняет tooan данных ODBC. 

## <a name="enabling-connectivity"></a>Включение соединения
Служба фабрики данных поддерживает подключения ODBC tooon локальные источники, с помощью hello шлюз управления данными. В разделе [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) toolearn статьи о шлюз управления данными и пошаговые инструкции по настройке шлюза hello. Используйте хранилище данных ODBC tooan tooconnect hello шлюза, даже если она размещается на виртуальной Машине Azure IaaS.

Hello шлюз можно установить на hello же локального компьютера или hello виртуальную Машину Azure в качестве хранилища данных ODBC hello. Тем не менее, рекомендуется установить на отдельных машин/Azure IaaS виртуальной Машины шлюза hello tooavoid о конфликтах ресурсов и для повышения производительности. При установке шлюза hello на отдельном компьютере hello машина должна была может tooaccess hello машины с хранилищем данных ODBC hello.

Помимо hello шлюз управления данными необходимо также tooinstall hello ODBC driver для hello хранилища данных на компьютере шлюза hello.

> [!NOTE]
> Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).

## <a name="getting-started"></a>Приступая к работе
Вы можете создать конвейер с действием копирования, который перемещает данные из хранилища данных ODBC, с помощью разных инструментов и интерфейсов API.

toocreate простым способом Hello конвейера — toouse hello **мастер копирования**. В разделе [учебника: создать конвейер, с помощью мастера копирования](data-factory-copy-data-wizard-tutorial.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.

Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**. В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования. 

Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello. 

1. Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных.
2. Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования. 
3. Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных. 

При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически. При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.  Пример с определениями JSON для сущностей фабрики данных, используемых toocopy данные из хранилища данных ODBC см. в разделе [пример JSON: копирование данных из данных ODBC хранения больших двоичных объектов tooAzure](#json-example-copy-data-from-odbc-data-store-to-azure-blob) этой статьи. 

Hello в следующих разделах содержатся сведения о свойствах JSON, которые находятся в хранилище данных определенного tooODBC сущностей фабрики данных используется toodefine:

## <a name="linked-service-properties"></a>Свойства связанной службы
Hello в следующей таблице приводится описание службы конкретных tooODBC связанные элементы JSON.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| type |свойство типа Hello должно быть присвоено: **OnPremisesOdbc** |Да |
| connectionString |Hello учетные данные не доступа часть строки подключения hello и необязательный шифрование учетных данных. Примеры в следующих разделах hello. |Да |
| credential |учетные данные доступа Hello часть hello строка подключения, указанная в формате значение свойства драйвера. Пример: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”. |Нет |
| authenticationType |Тип проверки подлинности используется хранилище данных tooconnect toohello ODBC. Возможными значениями являются: "Анонимная" и "Обычная". |Да |
| Имя пользователя |При использовании обычной проверки подлинности укажите имя пользователя. |Нет |
| пароль |Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя. |Нет |
| gatewayName |Имя шлюза hello, hello служба фабрики данных должна использовать хранилище данных ODBC toohello tooconnect. |Да |

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
Можно зашифровать учетные данные hello, с помощью hello [New AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (версии 1.0 Azure PowerShell) командлета или [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 или более ранней версии hello Azure PowerShell).  

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
Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи. Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).

Hello **typeProperties** раздел отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello. Hello typeProperties статьи для набора данных типа **RelationalTable** (включает набор данных ODBC) имеет следующие свойства hello

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| tableName |Имя таблицы hello в хранилище данных ODBC hello. |Да |

## <a name="copy-activity-properties"></a>Свойства действия копирования
Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи. Свойства (такие как имя, описание, входные и выходные таблицы, политики и т. д.) доступны для всех типов действий.

Свойства, доступные в hello **typeProperties** раздел hello действий на hello другой стороны, зависят от типа каждого действия. Для действия копирования они зависят от типов источников и приемников hello.

В действии копирования, когда источник типа **RelationalSource** (включая ODBC), hello следующие свойства доступны в разделе "typeProperties":

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| query |Используйте данные tooread hello пользовательского запроса. |Строка запроса SQL. Например, select * from MyTable. |Да |


## <a name="json-example-copy-data-from-odbc-data-store-tooazure-blob"></a>Пример JSON: копирование данных из данных ODBC хранения tooAzure больших двоичных объектов
В этом примере предоставляет определения JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). В нем показано, как toocopy из ODBC источника tooan хранилища больших двоичных объектов. Тем не менее, данные могут быть скопированный tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.

Образец Hello имеет hello, следуя сущностей фабрики данных.

1. Связанная служба типа [OnPremisesOdbc](#linked-service-properties).
2. Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Входной [набор данных](data-factory-create-datasets.md) типа [RelationalTable](#dataset-properties).
4. Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. [Конвейер](data-factory-create-pipelines.md) с действием копирования, в котором используются [RelationalSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Образец Hello копирует данные из результатов запроса в большой двоичный объект ODBC tooa данных хранения каждый час. свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.

В качестве первого шага можно Настройте шлюз управления данными hello. Hello инструкции содержатся в hello [перемещение данных между расположениями локальных и облачных](data-factory-move-data-between-onprem-and-cloud.md) статьи.

**ODBC связанная служба** в этом примере используется hello обычной проверки подлинности. Сведения о различных типах аутентификации, которые можно использовать, см. в разделе [Свойства связанной службы ODBC](#linked-service-properties).

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

Образец Hello предполагается создания таблицы «MyTable» в базе данных ODBC, и она содержит столбец с именем «timestampcolumn» для временного ряда данных.

Параметр «external»: «true» уведомляет службу hello фабрики данных, что набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.

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

Записывается новый большой двоичный объект tooa каждый час (частота: час, интервал: 1). путь к папке Hello для большого двоичного объекта hello динамически вычисляется на основе времени начала hello hello среза, который обрабатывается. путь к папке Hello использует года, месяца, дня и часа части времени начала hello.

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

конвейер Hello содержит операции копирования, настроенные toouse эти наборы входных и выходных данных. она запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**RelationalSource** и **приемник** тип установлен слишком**BlobSink**. запрос SQL Hello, указанный для hello **запроса** свойство выбирает данные hello в hello за час toocopy.

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
Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, действие копирования выполняет автоматического преобразования типов toosink типы источников с подходе двухэтапный hello:

1. Преобразование из типа too.NET типы собственного источника
2. Преобразовываемый тип приемника toonative тип .NET

При перемещении данных из хранилищ данных ODBC, типы данных ODBC: too.NET сопоставленные типы, как упоминалось в hello [сопоставления типов данных ODBC](https://msdn.microsoft.com/library/cc668763.aspx) раздела.

## <a name="map-source-toosink-columns"></a>Сопоставить исходные столбцы toosink
toolearn о сопоставление столбцов в toocolumns исходного набора данных в наборе данных приемников, в разделе [сопоставление столбцов набора данных в фабрике данных Azure](data-factory-map-columns.md).

## <a name="repeatable-read-from-relational-sources"></a>Повторяющиеся операции чтения из реляционных источников
При копировании данных из хранилища реляционных данных, сохранить повторяемость в виду tooavoid непредвиденные результаты. В фабрике данных Azure можно вручную повторно выполнить срез. Вы можете также настроить для набора данных политику повтора, чтобы при сбое срез выполнялся повторно. При повторном запуске срез в любом случае необходимо toomake, hello и те же данные, что считывается независимо от того, как запустить несколько раз срез. Ознакомьтесь с разделом [Повторяющиеся операции чтения из реляционных источников](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="ge-historian-store"></a>Хранилище GE Historian
Создать ODBC связанной службы toolink [Proficy Historian GE (теперь GE Historian)](http://www.geautomation.com/products/proficy-historian) фабрики данных Azure tooan хранилище данных, как показано в следующий пример hello:

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of hello GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

Установите шлюз управления данными на локальном компьютере и зарегистрируйте шлюз hello с портала hello. установлены на компьютере локального шлюза Hello использует драйвер ODBC для hello для toohello tooconnect GE Historian GE Historian хранилища данных. Установка драйвера hello таким образом, в том случае, если он еще не установлена на компьютере шлюза hello. Подробные сведения см. в разделе [Включение соединения](#enabling-connectivity).

Прежде чем использовать hello GE Historian хранения в решении фабрики данных, проверьте подключения шлюза hello toohello хранилища данных, с помощью инструкций в следующем разделе hello.

Прочитать статью hello с начала hello подробный обзор использования ODBC данных хранятся в виде источника хранилищ данных в ходе операции копирования.  

## <a name="troubleshoot-connectivity-issues"></a>Устранение проблем подключения
проблемы с подключением tootroubleshoot использовать hello **диагностики** вкладке **диспетчера конфигурации шлюза управления данными**.

1. Запустите **диспетчер конфигурации шлюза управления данными**. Можно либо запустить «C:\Program Files\Microsoft данных управления Gateway\1.0\Shared\ConfigManager.exe» непосредственно (или) поиска для **шлюза** toofind ссылку слишком**шлюз управления данными Майкрософт** приложения, как показано в hello после изображения.

    ![Поиск шлюза](./media/data-factory-odbc-connector/search-gateway.png)
2. Переключение toohello **диагностики** вкладки.

    ![Диагностика шлюза](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. Выберите hello **тип** данных хранения (связанной службы).
4. Укажите **проверки подлинности** и введите **учетные данные** (или) введите **строка подключения** , является хранилищем данных используется tooconnect toohello.
5. Нажмите кнопку **Проверка соединения** hello подключения tootest toohello-хранилище данных.

## <a name="performance-and-tuning"></a>Производительность и настройка
В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.
