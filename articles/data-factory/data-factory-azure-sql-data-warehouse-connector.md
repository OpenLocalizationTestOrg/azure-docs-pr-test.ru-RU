---
title: "aaaCopy данных в хранилище данных SQL Azure | Документы Microsoft"
description: "Узнайте, как toocopy данные из хранилища данных SQL Azure, с помощью фабрики данных Azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: d90fa9bd-4b79-458a-8d40-e896835cfd4a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 75bfcf3c99844fc1297ca500107da23cf875e41f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-data-warehouse-using-azure-data-factory"></a>Tooand копирования данных из хранилища данных SQL Azure, с помощью фабрики данных Azure
В этой статье объясняется, как toouse hello действие копирования в фабрике данных Azure toomove данные из хранилища данных SQL Azure. Она построена на hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, которая представляет общие сведения о перемещении данных с действием копирования hello.  

> [!TIP]
> tooachieve Наилучшая производительность, используйте PolyBase tooload данных в хранилище данных SQL Azure. Hello [PolyBase используйте tooload данных в хранилище данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) раздел содержит подробные сведения. Пошаговое руководство и пример использования см. в статье [Загрузка 1 ТБ в хранилище данных SQL Azure с помощью фабрики данных Azure [мастер копирования] менее чем за 15 минут](data-factory-load-sql-data-warehouse.md).

## <a name="supported-scenarios"></a>Поддерживаемые сценарии использования.
Можно скопировать данные **из хранилища данных SQL Azure** toohello следующие хранилищ данных:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Можно скопировать данные из hello, следуя хранилищ данных **tooAzure хранилище данных SQL**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> При копировании данных из SQL Server или база данных SQL Azure tooAzure хранилище данных SQL, если таблица hello не существует в конечное хранилище hello, фабрики данных можно автоматически создать hello таблицу в хранилище данных SQL с использованием схемы hello hello таблицы в источнике hello хранилище данных. Дополнительные сведения см. в разделе [Автоматическое создание таблицы](#auto-table-creation).

## <a name="supported-authentication-type"></a>Поддерживаемый тип проверки подлинности
Соединитель хранилища данных SQL Azure поддерживает обычную проверку подлинности.

## <a name="getting-started"></a>Приступая к работе
Вы можете создать конвейер с действием копирования, который перемещает данные в хранилище данных SQL Azure или из него, с помощью различных инструментов и интерфейсов API.

Hello простым способом toocreate конвейера, который копирует данные из хранилища данных SQL Azure — toouse hello копирования данных мастер. В разделе [учебника: загрузка данных в хранилище данных SQL с фабрикой данных](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) краткое Пошаговое руководство по создание с помощью мастера данных копирования hello конвейера.

Также можно использовать следующие средства toocreate конвейера hello: **портал Azure**, **Visual Studio**, **Azure PowerShell**, **шаблона диспетчера ресурсов Azure** , **.NET API**, и **API-интерфейса REST**. В разделе [учебника действия копирования](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) для toocreate пошаговые инструкции конвейера с помощью операции копирования.

Независимо от используемого hello инструменты или интерфейсы API, необходимо выполнить следующие шаги toocreate конвейера, который перемещает данные из источника данных хранилище tooa приемник данных hello.

1. Создание **фабрики данных**. Фабрика данных может содержать один или несколько конвейеров. 
2. Создание **связанные службы** toolink ввода-вывода хранилища tooyour данных фабрики данных. Например при копировании данных из хранилища данных Azure SQL tooan хранилища BLOB-объектов Azure, создается два связанных служб toolink вашей учетной записи хранилища Azure и фабрики данных tooyour хранилища данных Azure SQL. Свойства связанной службы, определенные tooAzure хранилище данных SQL, в разделе [связанные свойства службы](#linked-service-properties) раздела. 
3. Создание **наборы данных** toorepresent входных и выходных данных для hello операции копирования. В примере hello, упомянутые в последнем шаге hello создать контейнер больших двоичных объектов dataset toospecify hello и папку, содержащую hello входных данных. И создайте другую таблицу hello toospecify набора данных в хранилище данных Azure SQL hello, содержащий hello данные, скопированные из хранилища больших двоичных объектов hello. Свойства набора данных, определенных tooAzure хранилище данных SQL, в разделе [свойства набора данных](#dataset-properties) раздела.
4. Создайте **конвейер** с действием копирования, который принимает входной набор данных и возвращает выходной набор данных. В примере hello приведенные выше используются BlobSource в исходной и SqlDWSink в приемник для действия копирования hello. Аналогично при копировании из хранилища данных SQL Azure tooAzure хранилища BLOB-объектов используется SqlDWSource и BlobSink в действии копирования hello. Свойства действия копирования, определенные tooAzure хранилище данных SQL, в разделе [скопировать свойства действия](#copy-activity-properties) раздела. Дополнительные сведения о том, как toouse хранилища данных, как источник или приемник по ссылке hello в предыдущем разделе hello для источника данных.

При использовании мастера hello JSON определения для этих сущностей фабрики данных (связанные службы, наборы данных и hello конвейера) создаются автоматически. При использовании средств и API-интерфейсы (за исключением .NET API), определяются с использованием формата JSON hello этих сущностей фабрики данных.  Образцы с определениями JSON для сущностей фабрики данных, используемых toocopy данные из хранилища данных SQL Azure см. в разделе [JSON примеры](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) этой статьи.

Hello в следующих разделах содержатся сведения о JSON свойства, используемые toodefine фабрики данных сущностей определенного tooAzure хранилище данных SQL:

## <a name="linked-service-properties"></a>Свойства связанной службы
Привет, в следующей таблице приводится описание tooAzure службы хранилища данных SQL, которые связаны определенные элементы JSON.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| type |свойство типа Hello должно быть присвоено: **AzureSqlDW** |Да |
| connectionString |Укажите сведения, необходимые для свойства connectionString hello tooconnect toohello хранилище данных SQL Azure экземпляра. Поддерживается только обычная проверка подлинности. |Да |

> [!IMPORTANT]
> Настройка [брандмауэр базы данных SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) и hello сервера базы данных слишком[сервер служб Azure tooaccess hello](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure). Кроме того при копировании данных tooAzure хранилище данных SQL из внешней в Azure, включая из локальных источников данных со шлюзом фабрики данных, настройте соответствующий диапазон IP-адресов для компьютера hello, передающий данные tooAzure хранилище данных SQL.

## <a name="dataset-properties"></a>Свойства набора данных
Полный список разделов и свойства, доступные для определения наборов данных, см. в разделе hello [Создание наборов данных](data-factory-create-datasets.md) статьи. Разделы структуры, доступности и политики JSON набора данных одинаковы для всех типов наборов данных (SQL Azure, большие двоичные объекты Azure, таблицы Azure и т. д.).

раздел typeProperties Hello, отличается для каждого типа набора данных и предоставляет информацию о местоположении hello hello данных в хранилище данных hello. Hello **typeProperties** раздел для набора данных hello типа **AzureSqlDWTable** имеет hello следующие свойства:

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| tableName |Имя hello таблицы или представления в базе данных хранилища данных SQL Azure hello, hello связанной службы относится. |Да |

## <a name="copy-activity-properties"></a>Свойства действия копирования
Полный список разделов и свойства, доступные для определения действий см. в разделе hello [Создание конвейеры](data-factory-create-pipelines.md) статьи. Свойства (включая имя, описание, входные и выходные таблицы, политику и т. д.) доступны для всех типов действий.

> [!NOTE]
> Действие копирования Hello принимает только один входной параметр и выводятся только на один выход.

В то время как свойства в разделе typeProperties hello hello действия зависят от типа каждого действия. Для действия копирования они зависят от типов источников и приемников hello.

### <a name="sqldwsource"></a>SqlDWSource
Если источник имеет тип **SqlDWSource**, hello следующие свойства доступны в **typeProperties** раздела:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| SqlReaderQuery |Используйте данные tooread hello пользовательского запроса. |Строка запроса SQL. Например, select * from MyTable. |Нет |
| sqlReaderStoredProcedureName |Имя hello хранимой процедуры, который считывает данные из таблицы источника hello. |Имя hello хранимой процедуры. Hello последней инструкцией SQL должна быть инструкция SELECT в hello хранимой процедуре. |Нет |
| storedProcedureParameters |Параметры для hello хранимой процедуры. |Пары имен и значений. Имена и регистр параметров должны совпадать имена hello и учета регистра параметров hello хранимых процедур. |Нет |

Если hello **sqlReaderQuery** указан для hello SqlDWSource, hello действие копирования запускает этот запрос для hello tooget hello хранилище данных SQL Azure исходных данных.

Кроме того, можно указать хранимую процедуру, указав hello **sqlReaderStoredProcedureName** и **storedProcedureParameters** (если hello хранимая процедура принимает параметры).

Если вы не укажете sqlReaderQuery или sqlReaderStoredProcedureName, hello столбцы, определенные в разделе структуры hello hello набора данных JSON, используемые toobuild toorun запроса от hello хранилище данных SQL Azure. Пример: `select column1, column2 from mytable`. Если определение набора данных hello не имеют структуру hello, выбраны все столбцы из таблицы hello.

#### <a name="sqldwsource-example"></a>Пример SqlDWSource

```JSON
"source": {
    "type": "SqlDWSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```
**Определение Hello хранимые процедуры:**

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqldwsink"></a>SqlDWSink
**SqlDWSink** поддерживает hello следующие свойства:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| sqlWriterCleanupScript |Укажите запрос для действия копирования tooexecute таким образом, чтобы очистить данные особый срез. Дополнительные сведения см. в [разделе о повторяемости](#repeatability-during-copy). |Инструкция запроса. |Нет |
| allowPolyBase |Указывает, является ли toouse PolyBase (если применимо), а не BULKINSERT механизм. <br/><br/> **С помощью PolyBase — hello рекомендуется как tooload данные в хранилище данных SQL.** В разделе [PolyBase используйте tooload данных в хранилище данных SQL Azure](#use-polybase-to-load-data-into-azure-sql-data-warehouse) раздела для отображения сведений и ограничения. |Да <br/>False (по умолчанию) |Нет |
| polyBaseSettings |Группа свойств, которые могут быть указаны при hello **allowPolybase** задано слишком**true**. |&nbsp; |Нет |
| rejectValue |Указывает hello число или процент строк, может быть отклонено перед hello запрос завершается ошибкой. <br/><br/>Узнайте больше о hello PolyBase отклонить параметры в hello **аргументы** раздел [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) раздела. |0 (по умолчанию), 1, 2, ... |Нет |
| rejectType |Указывает, задан ли параметр rejectValue hello в значение литерала или в процентах. |Value (по умолчанию), Percentage |Нет |
| rejectSampleValue |Определяет количество hello tooretrieve строк перед hello PolyBase повторно вычисляет процент отклоненных строк hello. |1, 2, … |Да, если **rejectType** имеет значение **percentage**. |
| useTypeDefault |Указывает, как toohandle отсутствующих значений в разделенных текстовых файлов, если PolyBase получает данные из текстового файла hello.<br/><br/>Дополнительные сведения об этом свойстве из подраздела аргументы hello [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx). |True, False (по умолчанию) |Нет |
| writeBatchSize |Вставляет данные в таблицу SQL hello, при достижении writeBatchSize размера буфера hello |Целое число (количество строк) |Нет (значение по умолчанию — 10 000). |
| writeBatchTimeout |Время ожидания для hello пакетной вставки операции toocomplete до истечения времени ожидания. |Интервал времени<br/><br/> Пример: 00:30:00 (30 минут). |Нет |

#### <a name="sqldwsink-example"></a>Пример SqlDWSink

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-tooload-data-into-azure-sql-data-warehouse"></a>Использовать PolyBase tooload данные в хранилище данных SQL Azure
Применение **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** — это эффективный способ загрузки большого объема данных в хранилище данных SQL Azure с высокой пропускной способностью. Большой рост пропускной способности hello можно просмотреть с помощью PolyBase вместо механизм BULKINSERT по умолчанию hello. Подробное сравнение см. в разделе [Базовые показатели производительности](data-factory-copy-activity-performance.md#performance-reference). Пошаговое руководство и пример использования см. в статье [Загрузка 1 ТБ в хранилище данных SQL Azure с помощью фабрики данных Azure [мастер копирования] менее чем за 15 минут](data-factory-load-sql-data-warehouse.md).

* Если источник данных находится в **больших двоичных объектов Azure или хранилища Озера данных Azure**и формат hello совместим с PolyBase, можно скопировать непосредственно tooAzure хранилище данных SQL с помощью PolyBase. Дополнительные сведения см. в разделе **[Прямое копирование с помощью PolyBase](#direct-copy-using-polybase)**.
* Если хранилище данных источника и формат не поддерживается изначально PolyBase, можно использовать hello  **[копии промежуточного хранения, с помощью PolyBase](#staged-copy-using-polybase)**  вместо этого компонента. Он также позволяет повысить пропускную способность автоматически преобразования данных hello в формате, совместимом с PolyBase и хранение данных hello в хранилище больших двоичных объектов Azure. После этого данные загружаются в хранилище данных SQL.

Набор hello `allowPolyBase` свойство слишком**true** как показано в hello в следующем примере для фабрики данных Azure toouse PolyBase toocopy данных в хранилище данных SQL Azure. При установке allowPolyBase tootrue, можно указать конкретные свойства PolyBase с использованием hello `polyBaseSettings` группы свойств. в разделе hello [SqlDWSink](#SqlDWSink) подробные сведения о свойствах, которые можно использовать с polyBaseSettings см.

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true,
    "polyBaseSettings":
    {
        "rejectType": "percentage",
        "rejectValue": 10.0,
        "rejectSampleValue": 100,
        "useTypeDefault": true
    }
}
```

### <a name="direct-copy-using-polybase"></a>Прямое копирование с помощью PolyBase
PolyBase для хранилища данных SQL напрямую поддерживает хранилище BLOB-объектов Azure и Azure Data Lake Store (с использованием субъекта-службы) в качестве источника и с определенными требованиями к формату файлов. Если источник данных не отвечает требованиям hello, описанные в этом разделе, напрямую можно скопировать из источника данных хранилища tooAzure, хранилище данных SQL с помощью PolyBase. В противном случае можно использовать [промежуточное копирование с помощью PolyBase](#staged-copy-using-polybase).

> [!TIP]
> toocopy данные из хранилища Озера данных tooSQL хранилища данных эффективно, ознакомьтесь с дополнительными [фабрики данных Azure позволяет проще и удобный toouncover полезные сведения из данных, даже при использовании хранилища Озера данных с хранилищем данных SQL](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).

Если не выполняются требования к hello, фабрики данных Azure проверяет параметры hello и автоматическое переключение toohello BULKINSERT механизм для перемещения данных hello.

1. Тип **связанной службы источника** — **AzureStorage** или **AzureDataLakeStore с проверкой подлинности на основе субъекта-службы**.  
2. Hello **входного набора данных** относится к типу: **AzureBlob** или **AzureDataLakeStore**, и hello тип формата под `type` свойств является **OrcFormat** , или **TextFormat** с hello конфигурации:

   1. Параметр `rowDelimiter` должен содержать значение **\n**.
   2. `nullValue`задано слишком**пустая строка** ("»), или `treatEmptyAsNull` задано слишком**true**.
   3. `encodingName`задано слишком**utf-8**, который является **по умолчанию** значение.
   4. Параметры `escapeChar`, `quoteChar`, `firstRowAsHeader` и `skipLineCount` не указываются.
   5. Параметр `compression` может иметь значение **no compression**, **GZip** или **Deflate**.

    ```JSON
    "typeProperties": {
       "folderPath": "<blobpath>",
       "format": {
           "type": "TextFormat",     
           "columnDelimiter": "<any delimiter>",
           "rowDelimiter": "\n",       
           "nullValue": "",           
           "encodingName": "utf-8"    
       },
       "compression": {  
           "type": "GZip",  
           "level": "Optimal"  
       }  
    },
    ```

3. Имеется не `skipHeaderLineCount` в разделе **BlobSource** или **AzureDataLakeStore** для hello действие копирования в конвейере hello.
4. Имеется не `sliceIdentifierColumnName` в разделе **SqlDWSink** для hello действие копирования в конвейере hello. PolyBase гарантирует, что за один цикл выполнения либо все данные будут обновлены, либо ничего не будет обновлено. tooachieve **повторимость**, можно использовать `sqlWriterCleanupScript`).
5. Имеется не `columnMapping` , используемых в hello, связанные в действии копирования.

### <a name="staged-copy-using-polybase"></a>промежуточное копирование с помощью PolyBase
Если исходные данные не соответствуют критериям hello, представленных в предыдущем разделе hello, можно включить копирование данных через промежуточный промежуточного хранилища больших двоичных объектов (не может быть хранилище Premium). В этом случае фабрики данных Azure автоматически выполняет преобразование в hello данных toomeet данных требования к формату PolyBase, а затем используйте PolyBase tooload данных в хранилище данных SQL и в последней очистки временных данных из хранилища больших двоичных объектов hello. Подробные сведения о том, как работает копирование данных через промежуточное хранилище BLOB-объектов Azure, см. в разделе [Промежуточное копирование](data-factory-copy-activity-performance.md#staged-copy).

> [!NOTE]
> После копирования данных из объекта данных локального хранения в хранилище данных SQL Azure, используя PolyBase и промежуточного хранения, если ваша версия шлюза управления данными не ниже 2.4, требует JRE (среда выполнения Java) на шлюзе компьютеру, на котором находится источник данных используется tootransform в правильном формате. Рекомендуем обновить ваш последний tooavoid toohello шлюза такая зависимость.
>

toouse эту функцию, создайте [связанная служба хранилища Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) , обозначающий toohello учетной записи хранилища Azure с hello промежуточные BLOB-объекта хранилища, затем укажите hello `enableStaging` и `stagingSettings` свойств для действия копирования hello как показано в hello, следующий код:

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server tooSQL Data Warehouse via PolyBase",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDWOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlDwSink",
            "allowPolyBase": true
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob"
        }
    }
}
]
```

## <a name="best-practices-when-using-polybase"></a>Рекомендации по использованию PolyBase
Hello следующие разделы содержат дополнительные советы и рекомендации toohello те, которые упоминаются в [советы и рекомендации для хранилища данных SQL Azure](../sql-data-warehouse/sql-data-warehouse-best-practices.md).

### <a name="required-database-permission"></a>Необходимые разрешения базы данных
toouse PolyBase, его необходимо быть пользователем hello используется tooload данных в хранилище данных SQL имеет hello [разрешение «УПРАВЛЕНИЕ»](https://msdn.microsoft.com/library/ms191291.aspx) hello целевой базе данных. Одним из способов tooachieve, tooadd этот пользователь является членом роли «db_owner». Узнайте, как toodo, выполнив следующие [в этом разделе](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).

### <a name="row-size-and-data-type-limitation"></a>Ограничение размера строки и типа данных
Загружает Polybase ограничены tooloading строк и меньше, чем **1 МБ** и не удается загрузить tooVARCHR(MAX), NVARCHAR(MAX) или VARBINARY(MAX). См. слишком[здесь](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).

Если у вас есть источник данных со строками размером более 1 МБ, вы можете toosplit hello исходных таблиц по вертикали в несколько небольших описаний, где hello наибольший размер строки в каждой из них не превышает hello. Затем можно загрузить Hello несколько таблиц меньшего размера, с помощью PolyBase и объединяются друг с другом в хранилище данных SQL Azure.

### <a name="sql-data-warehouse-resource-class"></a>Класс ресурсов хранилища данных SQL
tooachieve лучшие возможности пропускной способности рассмотрим tooassign больше ресурсов класса toohello пользователя, используемые tooload данные в хранилище данных SQL через PolyBase. Узнайте, как toodo, выполнив следующие [измените пример класса ресурса для пользователя](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).

### <a name="tablename-in-azure-sql-data-warehouse"></a>Использование tableName в хранилище данных SQL Azure
Hello следующей таблице приведены примеры о том, как toospecify hello **tableName** свойство в наборе данных JSON для различных сочетаний схему и имя таблицы.

| Схема базы данных | Имя таблицы | Свойство tableName в JSON |
| --- | --- | --- |
| dbo |MyTable |MyTable или dbo.MyTable либо [dbo].[MyTable] |
| dbo1 |MyTable |dbo1.MyTable или [dbo1].[MyTable] |
| dbo |My.Table |[My.Table] или [dbo].[My.Table] |
| dbo1 |My.Table |[dbo1].[My.Table] |

Если появится следующая ошибка hello, это может быть проблема с hello значение, указанное для hello свойство tableName. См. таблице hello hello правильно toospecify значений свойства JSON tableName hello.  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a>Столбцы со значениями по умолчанию
В настоящее время функция в фабрике данных принимает только PolyBase hello одинаковое количество столбцов в целевой таблице hello. Предположим, у вас есть таблица с четырьмя столбцами и один из них определен со значением по умолчанию. Hello входные данные должны по-прежнему содержит четыре столбца. Предоставление 3 столбец входного набора данных были бы получены аналогичные toohello ошибки, сообщением:

```
All columns of hello table must be specified in hello INSERT BULK statement.
```
Значение NULL рассматривается как вариант значения по умолчанию. Если hello столбец допускает значения NULL, hello входных данных (в BLOB-объектов) для этого столбца может быть пустым (не может отсутствовать из входного набора данных hello). PolyBase вставит значение NULL для них в hello хранилище данных SQL Azure.  

## <a name="auto-table-creation"></a>Автоматическое создание таблицы
Если вы используете мастер копирования toocopy данные из SQL Server или база данных SQL Azure tooAzure хранилище данных SQL и hello таблицы, которая соответствует toohello исходной таблицы не существует в конечное хранилище hello, фабрики данных можно автоматически создать таблицу hello в hello хранилище данных с помощью схемы исходной таблицы hello.

Фабрика данных создает таблицу hello в конечное хранилище hello с hello, имя в хранилище данных источника hello же таблицы. Hello типы данных для столбцов выбираются основании после сопоставления типа hello. При необходимости выполняет toofix преобразования типа любые проблемы совместимости между хранилищами источника и назначения. Также используется распределение таблиц методом циклического перебора.

| Тип столбца исходной базы данных SQL | Тип столбца целевого хранилища данных SQL (ограничение размера) |
| --- | --- |
| int | int |
| BigInt | BigInt |
| SmallInt | SmallInt |
| TinyInt | TinyInt |
| Bit | Bit |
| Decimal | Decimal |
| Числовой | Decimal |
| Float | Float |
| Money | Money |
| Real | Real |
| SmallMoney | SmallMoney |
| Binary | Binary |
| Varbinary | Varbinary (вверх too8000) |
| Дата | Дата |
| DateTime | DateTime |
| DateTime2 | DateTime2 |
| Время | Время |
| DateTimeOffset | DateTimeOffset |
| SmallDateTime | SmallDateTime |
| текст | Varchar (вверх too8000) |
| NText | NVarChar (вверх too4000) |
| Образ — | VarBinary (вверх too8000) |
| UniqueIdentifier | UniqueIdentifier |
| Char | Char |
| NCHAR | NCHAR |
| VarChar | VarChar (вверх too8000) |
| NVarChar | NVarChar (вверх too4000) |
| xml | Varchar (вверх too8000) |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a>Сопоставление типов для хранилища данных SQL Azure
Как упоминалось в hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи, действие копирования выполняет автоматического преобразования типов toosink типы источников с hello подходе шаг 2:

1. Преобразование из типа too.NET типы собственного источника
2. Преобразовываемый тип приемника toonative тип .NET

При перемещении данных слишком & из хранилища данных SQL Azure, hello следующие сопоставления используются из типа too.NET типа SQL и наоборот.

сопоставление Hello — то же, что hello [сопоставление типов данных SQL Server для ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).

| Тип ядра СУБД SQL Server | Тип .NET Framework |
| --- | --- |
| bigint |Int64 |
| binary; |Byte[] |
| bit |Логический |
| char; |String, Char[] |
| дата |DateTime |
| DateTime |DateTime |
| datetime2; |DateTime |
| Datetimeoffset |Datetimeoffset |
| Decimal |Decimal |
| Атрибут FILESTREAM (varbinary(max)) |Byte[] |
| Float |Double |
| изображение |Byte[] |
| int |Int32 |
| money; |Decimal |
| nchar; |String, Char[] |
| ntext |String, Char[] |
| numeric |Decimal |
| nvarchar; |String, Char[] |
| real; |Single |
| rowversion |Byte[] |
| smalldatetime; |DateTime |
| smallint; |Int16 |
| smallmoney; |Decimal |
| sql_variant |Object * |
| text |String, Char[] |
| time |Интервал времени |
| Timestamp |Byte[] |
| tinyint; |Byte |
| uniqueidentifier |Guid |
| varbinary; |Byte[] |
| varchar. |String, Char[] |
| xml |xml |

Также можно сопоставить столбцы из источника toocolumns набора данных из набора данных приемник в определении действия копирования hello. Дополнительные сведения см. в статье [Сопоставление столбцов исходного набора данных со столбцами целевого набора данных](data-factory-map-columns.md).

## <a name="json-examples-for-copying-data-tooand-from-sql-data-warehouse"></a>Примеры JSON для копирования данных tooand из хранилища данных SQL
Hello ниже приведены примеры определения образца JSON можно использовать toocreate конвейера с помощью [портал Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) или [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) или [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Они показывают как toocopy tooand данные из хранилища данных SQL Azure и хранилища больших двоичных объектов. Тем не менее, данные можно скопировать **непосредственно** из любых источников tooany приемников hello указано [здесь](data-factory-data-movement-activities.md#supported-data-stores-and-formats) с помощью hello действие копирования в фабрике данных Azure.

### <a name="example-copy-data-from-azure-sql-data-warehouse-tooazure-blob"></a>Пример: Копирование данных из хранилища данных SQL Azure tooAzure больших двоичных объектов
Образец Hello определяет hello, следуя фабрики данных сущности:

1. Связанная служба типа [AzureSqlDW](#linked-service-properties).
2. Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Входной [набор данных](data-factory-create-datasets.md) типа [AzureSqlDWTable](#dataset-properties).
4. Выходной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Конвейер [pipeline](data-factory-create-pipelines.md) с действием копирования, в котором используются [SqlDWSource](#copy-activity-properties) и [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

Образец Hello копирует данные временных рядов (каждый час, день, т. д.) из таблицы в большом двоичном объекте tooa базы данных хранилища данных SQL Azure каждый час. свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.

**Связанная служба хранилища данных SQL Azure**

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Связанная служба хранилища BLOB-объектов Azure**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
**Входной набор данных хранилища данных SQL Azure**

Образец Hello предполагается создания таблицы «MyTable» в хранилище данных SQL Azure и содержит столбец с именем «timestampcolumn» для временного ряда данных.

Параметр «external»: «true» уведомляет службу hello фабрики данных, что набор данных hello фабрики toohello внешних данных и не был создан из действия в фабрике данных hello.

```JSON
{
  "name": "AzureSqlDWInput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

**Действие копирования в конвейере с источником SqlDWSource и приемником BlobSink**

Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**SqlDWSource** и **приемник** тип установлен слишком**BlobSink**. запрос SQL Hello, указанный для hello **SqlReaderQuery** свойство выбирает данные hello в hello за час toocopy.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLDWtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSqlDWInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlDWSource",
            "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
> [!NOTE]
> В примере hello **sqlReaderQuery** указан для hello SqlDWSource. Действие копирования Hello этот запрос запускает hello tooget hello хранилище данных SQL Azure исходных данных.
>
> Кроме того, можно указать хранимую процедуру, указав hello **sqlReaderStoredProcedureName** и **storedProcedureParameters** (если hello хранимая процедура принимает параметры).
>
> Если вы не укажете sqlReaderQuery или sqlReaderStoredProcedureName, hello столбцы, определенные в разделе структуры hello hello набора данных JSON, используемые toobuild запроса (выберите column1, column2 из mytable) toorun от hello хранилище данных SQL Azure. Если определение набора данных hello не имеют структуру hello, выбраны все столбцы из таблицы hello.
>
>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-data-warehouse"></a>Пример: Копирование данных из больших двоичных объектов Azure tooAzure хранилище данных SQL
Образец Hello определяет hello, следуя фабрики данных сущности:

1. Связанная служба типа [AzureSqlDW](#linked-service-properties).
2. Связанная служба типа [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Входной [набор данных](data-factory-create-datasets.md) типа [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Выходной [набор данных](data-factory-create-datasets.md) типа [AzureSqlDWTable](#dataset-properties).
5. Конвейер [pipeline](data-factory-create-pipelines.md) с действием копирования, которое использует [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) и [SqlDWSink](#copy-activity-properties).

Образец Hello копирует данные временных рядов (каждый час, день, т. д.) из таблицы tooa BLOB-объектов Azure в базе данных хранилища данных SQL Azure каждый час. свойства Hello JSON, используемые в этих примерах описаны в разделах, следующие примеры hello.

**Связанная служба хранилища данных SQL Azure**

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
**Связанная служба хранилища BLOB-объектов Azure**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
**Входной набор данных BLOB-объекта Azure**

Данные берутся из нового BLOB-объекта каждый час (frequency: hour, interval: 1). Hello путь и имя папки для большого двоичного объекта hello, динамически оцениваются на основе времени начала hello hello среза, который обрабатывается. путь к папке Hello использует года, месяца и дня время начала hello и имя файла hello час часть времени начала hello. «external»: параметр «true» уведомляет службу hello фабрики данных, что эта таблица является внешней toohello фабрики данных и не был создан из действия в фабрике данных hello.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
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
**Выходной набор данных хранилища данных SQL Azure**

Образец Hello копирует tooa таблицу данных, с именем «MyTable» в хранилище данных SQL Azure. Создать таблицу hello в хранилище данных SQL Azure с hello столько же столбцов, как предполагается, что файл toocontain hello CSV больших двоичных объектов. Новые строки добавляются в таблицу toohello каждый час.

```JSON
{
  "name": "AzureSqlDWOutput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**Действие копирования в конвейере с источником BlobSource и приемником SqlDWSink**

Hello конвейера содержит операции копирования, настроенные toouse hello входные и выходные наборы данных и является запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**BlobSource** и **приемник** тип установлен слишком**SqlDWSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQLDW",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlDWOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlDWSink",
            "allowPolyBase": true
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
Пошаговые инструкции см. в разделе hello. в разделе [загрузить 1 ТБ в хранилище данных SQL Azure в разделе 15 минут с фабрикой данных Azure](data-factory-load-sql-data-warehouse.md) и [загрузки данных с фабрикой данных Azure](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) статьи в hello хранилище данных SQL Azure документация.

## <a name="performance-and-tuning"></a>Производительность и настройка
В разделе [производительности для действия копирования & руководство по настройке](data-factory-copy-activity-performance.md) toolearn о ключе факторы, оказывают влияние на производительность перемещения данных (действие копирования) в фабрике данных Azure и различных способов toooptimize его.
