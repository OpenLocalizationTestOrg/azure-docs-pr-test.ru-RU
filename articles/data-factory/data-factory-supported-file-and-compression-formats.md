---
title: "форматы aaaFile и сжатия в фабрике данных Azure | Документы Microsoft"
description: "Дополнительные сведения о форматах файлов hello, поддерживаемых фабрикой данных Azure."
keywords: "данные BLOB-объектов, копирование BLOB-объекта Azure"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 9d40517b059fc533776bcc088db8c531ee5b003d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="file-and-compression-formats-supported-by-azure-data-factory"></a>Форматы файлов и сжатия данных, поддерживаемые фабрикой данных Azure
*В этом разделе рассматриваются следующие соединители toohello: [Amazon S3](data-factory-amazon-simple-storage-service-connector.md), [больших двоичных объектов Azure](data-factory-azure-blob-connector.md), [хранилища Озера данных Azure](data-factory-azure-datalake-connector.md), [файловой системы](data-factory-onprem-file-system-connector.md), [ FTP](data-factory-ftp-connector.md), [HDFS](data-factory-hdfs-connector.md), [HTTP](data-factory-http-connector.md), и [SFTP](data-factory-sftp-connector.md).*

Фабрика данных Azure поддерживает следующие типы формата файла hello:

* [текстовый формат](#text-format);
* [формат JSON](#json-format);
* [формат Avro](#avro-format);
* [формат ORC](#orc-format);
* [формат Parquet](#parquet-format).

## <a name="text-format"></a>Текстовый формат
Если требуется tooread из текстового файла или запись tooa текстовый файл, задайте hello `type` свойство в hello `format` части набора данных hello слишком**TextFormat**. Можно также указать следующие hello **необязательно** свойства в hello `format` раздела. В разделе [примере TextFormat](#textformat-example) раздел, в tooconfigure.

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| columnDelimiter |символ Hello использовать tooseparate столбцов в файле. Можно рассмотреть toouse редких непечатаемые char, может не скорее всего, существует в данных. Например, укажите "\u0001", что соответствует символу начала заголовка (SOH). |Допускается только один знак. Hello **по умолчанию** значение **запятая (,)**. <br/><br/>toouse символ Юникода ссылаться слишком[символов Юникода](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello соответствующий код для него. |Нет |
| rowDelimiter |символ Hello использовать tooseparate строк в файле. |Допускается только один знак. Hello **по умолчанию** значение представляет собой любой hello последующих значений на чтение: **[«\r\n», «\r», «\n»]** и **«\r\n»** при записи. |Нет |
| escapeChar |специальный символ Hello использовать tooescape разделитель столбцов в hello содержимое входного файла. <br/><br/>Для таблицы нельзя указать и escapeChar, и quoteChar. |Допускается только один знак. Значение по умолчанию отсутствует. <br/><br/>Пример: при наличии запятая («,») как разделитель столбцов hello, но его необходимо toohave hello запятая в тексте hello (пример: «Hello, world»), можно определить как hello escape-символ «$» и использовать строку «Hello$, world» в источнике hello. |Нет |
| quoteChar |использовать знак Hello tooquote строковое значение. Hello разделители столбцов и строк внутри кавычек hello будет рассматриваться как часть hello строковое значение. Это свойство является применимо tooboth ввода и вывода наборов данных.<br/><br/>Для таблицы нельзя указать и escapeChar, и quoteChar. |Допускается только один знак. Значение по умолчанию отсутствует. <br/><br/>Например, если у вас есть запятая («,») как разделитель столбцов hello, но его необходимо toohave запятая в тексте hello (пример: < Hello, world >), можно определить» (двойная кавычка) как hello знак кавычек, чтобы использовать строку hello «Hello, world» в источнике hello. |Нет |
| nullValue |Один или несколько символов используется toorepresent значение null. |Один или несколько знаков. Hello **по умолчанию** значения **«\N» и «NULL»** для чтения и **«\N»** при записи. |Нет |
| encodingName |Укажите название кодировки hello. |Допустимое имя кодировки. Ознакомьтесь с описанием свойства [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx). Пример: windows-1250 или shift_jis. Hello **по умолчанию** значение **UTF-8**. |Нет |
| firstRowAsHeader |Указывает, является ли tooconsider hello первую строку как заголовок. Фабрика данных считывает первую строку входного набора данных как заголовок. Фабрика данных записывает первую строку как заголовок в выходной набор данных. <br/><br/>Примеры сценариев см. в разделе [Сценарии использования `firstRowAsHeader` и `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount). |Да<br/><b>False (по умолчанию)</b> |Нет |
| skipLineCount |Указывает номер hello tooskip строк, при считывании данных из входных файлов. Если указаны skipLineCount и firstRowAsHeader, hello строки пропускаются сначала и затем сведения о заголовке hello считывается из входного файла hello. <br/><br/>Примеры сценариев см. в разделе [Сценарии использования `firstRowAsHeader` и `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount). |Целое число  |Нет |
| treatEmptyAsNull |Указывает, является ли tootreat null или пустую строку как строку null значения при считывании данных из входного файла. |**True (по умолчанию)**<br/>Ложь |Нет |

### <a name="textformat-example"></a>Пример TextFormat
В hello после определения JSON для набора данных задаются некоторые из дополнительных свойств hello.

```json
"typeProperties":
{
    "folderPath": "mycontainer/myfolder",
    "fileName": "myblobname",
    "format":
    {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";",
        "quoteChar": "\"",
        "NullValue": "NaN",
        "firstRowAsHeader": true,
        "skipLineCount": 0,
        "treatEmptyAsNull": true
    }
},
```

toouse `escapeChar` вместо `quoteChar`, замените строку hello с `quoteChar` с hello использовать escapeChar следующие:

```json
"escapeChar": "$",
```

### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a>Сценарии использования firstRowAsHeader и skipLineCount
* Копирование из файла источника, не являющимся файлами tooa и хотите tooadd заголовка строки, содержащей hello схемы метаданных (например: SQL-схема). Укажите `firstRowAsHeader` как true в hello выходной набор данных для этого сценария.
* Копирование из текстового файла, содержащего приемник не являющимся файлами tooa заголовка строки и хотите toodrop, строка. Укажите `firstRowAsHeader` как true во входном наборе данных hello.
* Копирование из текстового файла и хотите tooskip несколько строк в начале hello, которые не содержат данных или заголовка информации. Укажите `skipLineCount` tooindicate hello число строк toobe пропущено. Если hello остальной части файла hello содержит строку заголовка, можно указать `firstRowAsHeader`. Если оба `skipLineCount` и `firstRowAsHeader` указаны, hello строки пропускаются сначала и затем сведения о заголовке hello считывается из входного файла hello

## <a name="json-format"></a>Формат JSON
слишком**импорта и экспорта файла JSON как-в / из базы данных Azure Cosmos**, hello см. в разделе [документов JSON импорта и экспорта](data-factory-azure-documentdb-connector.md#importexport-json-documents) статьи [перемещения данных из базы данных Azure Cosmos](data-factory-azure-documentdb-connector.md) статьи.

Если требуется tooparse hello JSON-файлов или запись данных hello в формате JSON, задайте hello `type` свойство в hello `format` статьи слишком**JsonFormat**. Можно также указать следующие hello **необязательно** свойства в hello `format` раздела. В разделе [JsonFormat пример](#jsonformat-example) раздел, в tooconfigure.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| filePattern |Укажите шаблон hello данных, хранящихся в каждом файле JSON. Допустимые значения: **setOfObjects** и **arrayOfObjects**. Hello **по умолчанию** значение **setOfObjects**. Подробные сведения об этих шаблонах см. в разделе [Шаблоны файлов JSON](#json-file-patterns). |Нет |
| jsonNodeReference | Tooiterate и извлечения данных из объектов hello в массив полей с hello же шаблон, укажите путь к JSON hello этого массива. Это свойство поддерживается только в том случае, если данные копируются из JSON-файлов. | Нет |
| jsonPathDefinition | Укажите hello выражения пути JSON для каждого сопоставления столбцов с именем пользовательские столбца (начало строчных). Это свойство поддерживается только в том случае, если данные копируются из JSON-файлов и данные можно извлечь из объекта или массива. <br/><br/> Для поля в корневой объект, начинаться с $ корневой; для полей внутри массива hello выбирается программой `jsonNodeReference` свойство начинаются с Привет элемента массива. В разделе [JsonFormat пример](#jsonformat-example) раздел, в tooconfigure. | Нет |
| encodingName |Укажите название кодировки hello. Hello список допустимых названий кодировок см. в разделе: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) свойство. Например: windows-1250 или shift_jis. Hello **по умолчанию** значение: **UTF-8**. |Нет |
| nestingSeparator |Символ, используемые tooseparate уровней вложения. значение по умолчанию Hello "." (точка). |Нет |

### <a name="json-file-patterns"></a>Шаблоны файлов JSON

Действие копирования можно обработать hello следующие шаблоны файлов JSON:

- **Тип 1: setOfObjects**

    Каждый файл содержит один объект или несколько разделенных строками или объединенных объектов. Если этот параметр выбран в выходном наборе данных, то в результате копирования будет создан JSON-файл, где каждый объект будет находиться в отдельной строке (файл с разделителем-строкой).

    * **Пример единого объекта JSON**

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        ```

    * **Пример JSON-файла с разделителем-строкой**

        ```json
        {"time":"2015-04-29T07:12:20.9100000Z","callingimsi":"466920403025604","callingnum1":"678948008","callingnum2":"567834760","switch1":"China","switch2":"Germany"}
        {"time":"2015-04-29T07:13:21.0220000Z","callingimsi":"466922202613463","callingnum1":"123436380","callingnum2":"789037573","switch1":"US","switch2":"UK"}
        {"time":"2015-04-29T07:13:21.4370000Z","callingimsi":"466923101048691","callingnum1":"678901578","callingnum2":"345626404","switch1":"Germany","switch2":"UK"}
        ```

    * **Пример объединенного JSON-файла**

        ```json
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        }
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        }
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
        ```

- **Тип 2: arrayOfObjects**

    Каждый файл содержит массив объектов.

    ```json
    [
        {
            "time": "2015-04-29T07:12:20.9100000Z",
            "callingimsi": "466920403025604",
            "callingnum1": "678948008",
            "callingnum2": "567834760",
            "switch1": "China",
            "switch2": "Germany"
        },
        {
            "time": "2015-04-29T07:13:21.0220000Z",
            "callingimsi": "466922202613463",
            "callingnum1": "123436380",
            "callingnum2": "789037573",
            "switch1": "US",
            "switch2": "UK"
        },
        {
            "time": "2015-04-29T07:13:21.4370000Z",
            "callingimsi": "466923101048691",
            "callingnum1": "678901578",
            "callingnum2": "345626404",
            "switch1": "Germany",
            "switch2": "UK"
        }
    ]
    ```

### <a name="jsonformat-example"></a>Пример JsonFormat

**Вариант 1. Копирование данных из JSON-файлов**

В разделе hello, следующие два примера при копировании данных из JSON-файлов. Универсальный Hello точки toonote:

**Пример 1. Извлечение данных из объекта и массива**

В этом примере предполагается, что один корневой объект JSON, отображающий toosingle записи в табличный результат. Если имеется файл JSON с hello после содержимого:  

```json
{
    "id": "ed0e4960-d9c5-11e6-85dc-d7996816aad3",
    "context": {
        "device": {
            "type": "PC"
        },
        "custom": {
            "dimensions": [
                {
                    "TargetResourceType": "Microsoft.Compute/virtualMachines"
                },
                {
                    "ResourceManagmentProcessRunId": "827f8aaa-ab72-437c-ba48-d8917a7336a3"
                },
                {
                    "OccurrenceTime": "1/13/2017 11:24:37 AM"
                }
            ]
        }
    }
}
```
и необходимо отформатировать его в таблице Azure SQL в следующих hello, путем извлечения данных из объектов и массив toocopy:

| id | deviceType | targetResourceType | resourceManagmentProcessRunId | occurrenceTime |
| --- | --- | --- | --- | --- |
| ed0e4960-d9c5-11e6-85dc-d7996816aad3 | PC | Microsoft.Compute/virtualMachines | 827f8aaa-ab72-437c-ba48-d8917a7336a3 | 1/13/2017 11:24:37 AM |

Hello входного набора данных с **JsonFormat** тип определяется следующим образом: (частичное определение с частями hello применимо). В частности:

- `structure`раздел определяет имена столбцов настроенные hello и hello соответствующие типы данных во время преобразования данных tootabular. Этот раздел представляет **необязательно** при отсутствии необходимости toodo сопоставления столбцов. В разделе [сопоставление столбцов набора данных toodestination столбцов набора данных источника](data-factory-map-columns.md) более подробные сведения.
- `jsonPathDefinition`Указывает путь hello JSON для каждого столбца, указывающее, где tooextract hello данные из. toocopy данные из массива, можно использовать **.property массива [x]** tooextract значение hello заданного свойства из объекта xth hello, или же можно использовать  **массива [*] .property** toofind значение Hello из любого объекта, содержащего такого свойства.

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "deviceType",
            "type": "String"
        },
        {
            "name": "targetResourceType",
            "type": "String"
        },
        {
            "name": "resourceManagmentProcessRunId",
            "type": "String"
        },
        {
            "name": "occurrenceTime",
            "type": "DateTime"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonPathDefinition": {"id": "$.id", "deviceType": "$.context.device.type", "targetResourceType": "$.context.custom.dimensions[0].TargetResourceType", "resourceManagmentProcessRunId": "$.context.custom.dimensions[1].ResourceManagmentProcessRunId", "occurrenceTime": " $.context.custom.dimensions[2].OccurrenceTime"}      
        }
    }
}
```

**Пример 2: кросс-примените несколько объектов с hello же шаблон из массива**

В этом примере предполагается, что tootransform один корневой объект JSON в несколько записей в табличный результат. Если имеется файл JSON с hello после содержимого:  

```json
{
    "ordernumber": "01",
    "orderdate": "20170122",
    "orderlines": [
        {
            "prod": "p1",
            "price": 23
        },
        {
            "prod": "p2",
            "price": 13
        },
        {
            "prod": "p3",
            "price": 231
        }
    ],
    "city": [ { "sanmateo": "No 1" } ]
}
```
и отформатируйте его в таблице Azure SQL в следующих hello, выравнивание данных hello внутри массива hello toocopy перекрестное соединение с hello, общие сведения о корневой:

| ordernumber | orderdate | order_pd | order_price | city |
| --- | --- | --- | --- | --- |
| 01 | 20170122 | P1 | 23 | [{"sanmateo":"No 1"}] |
| 01 | 20170122 | P2 | 13. | [{"sanmateo":"No 1"}] |
| 01 | 20170122 | P3 | 231 | [{"sanmateo":"No 1"}] |

Hello входного набора данных с **JsonFormat** тип определяется следующим образом: (частичное определение с частями hello применимо). В частности:

- `structure`раздел определяет имена столбцов настроенные hello и hello соответствующие типы данных во время преобразования данных tootabular. Этот раздел представляет **необязательно** при отсутствии необходимости toodo сопоставления столбцов. В разделе [сопоставление столбцов набора данных toodestination столбцов набора данных источника](data-factory-map-columns.md) более подробные сведения.
- `jsonNodeReference`Указывает tooiterate и извлечения данных из объектов hello с hello же шаблон в списке **массива** orderlines.
- `jsonPathDefinition`Указывает путь hello JSON для каждого столбца, указывающее, где tooextract hello данные из. В этом примере «ordernumber», «orderdate» и «Город» находятся в корневой объект пути JSON, начиная с «$»., хотя «order_pd» и «order_price» определяются с путем, производный от элемента массива hello без «$»..

```json
"properties": {
    "structure": [
        {
            "name": "ordernumber",
            "type": "String"
        },
        {
            "name": "orderdate",
            "type": "String"
        },
        {
            "name": "order_pd",
            "type": "String"
        },
        {
            "name": "order_price",
            "type": "Int64"
        },
        {
            "name": "city",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat",
            "filePattern": "setOfObjects",
            "jsonNodeReference": "$.orderlines",
            "jsonPathDefinition": {"ordernumber": "$.ordernumber", "orderdate": "$.orderdate", "order_pd": "prod", "order_price": "price", "city": " $.city"}         
        }
    }
}
```

**Обратите внимание hello после точки.**

* Если hello `structure` и `jsonPathDefinition` не определены в наборе данных фабрики данных hello hello действие копирования обнаруживает hello схемы из первого объекта hello и одноуровневые hello объекта целиком.
* По умолчанию Если входные данные JSON hello массив, hello действие копирования преобразует весь массив значение hello в строку. Для выбора tooextract данных с помощью `jsonNodeReference` и/или `jsonPathDefinition`, или пропустить его, не указывайте его в `jsonPathDefinition`.
* При наличии дубликатов имен в Здравствуйте того же уровня, hello действие копирования выбирает hello последним.
* В именах свойств учитывается регистр. Два свойства с одинаковым именем, но в разных регистрах, рассматриваются как два отдельных свойства.

**Вариант 2: Запись файла tooJSON данных**

Если у вас есть hello в следующей таблице в базе данных SQL:

| id | order_date | order_price | order_by |
| --- | --- | --- | --- |
| 1 | 20170119 | 2000 | David |
| 2 | 20170120 | 3500 | Patrick |
| 3 | 20170121 | 4000 | Jason |

и для каждой записи, ожидается, что объект JSON tooa toowrite hello следующий формат:
```json
{
    "id": "1",
    "order": {
        "date": "20170119",
        "price": 2000,
        "customer": "David"
    }
}
```

Hello выходной набор данных с **JsonFormat** тип определяется следующим образом: (частичное определение с частями hello применимо). В частности `structure` раздел определяет имена свойств настроенные hello в конечный файл `nestingSeparator` (по умолчанию — «.»), уровень вложенности hello используется tooidentify из имени hello. Этот раздел представляет **необязательно** , если не требуется имя свойства toochange hello, сравнение с именем столбца источника или вложить некоторые свойства hello.

```json
"properties": {
    "structure": [
        {
            "name": "id",
            "type": "String"
        },
        {
            "name": "order.date",
            "type": "String"
        },
        {
            "name": "order.price",
            "type": "Int64"
        },
        {
            "name": "order.customer",
            "type": "String"
        }
    ],
    "typeProperties": {
        "folderPath": "mycontainer/myfolder",
        "format": {
            "type": "JsonFormat"
        }
    }
}
```

## <a name="avro-format"></a>Формат Avro
Если требуется tooparse hello Avro файлы или записи данных hello в формате Avro, задайте hello `format` `type` свойство слишком**AvroFormat**. Необязательно toospecify любые свойства в раздел формата hello внутри раздела typeProperties hello. Пример:

```json
"format":
{
    "type": "AvroFormat",
}
```

toouse в формате Avro в таблицу Hive можно ссылаться слишком[Apache Hive учебника](https://cwiki.apache.org/confluence/display/Hive/AvroSerDe).

Обратите внимание hello после точки.  

* [Сложные типы данных](http://avro.apache.org/docs/current/spec.html#schema_complex) (записи, перечисления, массивы, сопоставления, объединения и фиксированные данные) не поддерживаются.

## <a name="orc-format"></a>Формат ORC
Если требуется tooparse hello ORC файлы или записи данных hello в формат ORC, задайте hello `format` `type` свойство слишком**OrcFormat**. Необязательно toospecify любые свойства в раздел формата hello внутри раздела typeProperties hello. Пример:

```json
"format":
{
    "type": "OrcFormat"
}
```

> [!IMPORTANT]
> При копировании файлов ORC не **как-является** между локальными и облачными хранилищами данных, необходимо tooinstall hello JRE 8 (среда выполнения Java) на компьютере шлюза. Для 64-разрядного шлюза требуется 64-разрядная версия JRE, а для 32-разрядного шлюза — 32-разрядная версия JRE. Обе эти версии доступны [здесь](http://go.microsoft.com/fwlink/?LinkId=808605). Выберите подходящее hello.
>
>

Обратите внимание hello после точки.

* Данные сложных типов (STRUCT, MAP, LIST, UNION) не поддерживаются.
* Для ORC-файлов используется три [параметра сжатия](http://hortonworks.com/blog/orcfile-in-hdp-2-better-compression-better-performance/): NONE, ZLIB и SNAPPY. Фабрика данных поддерживает чтение данных из ORC-файла в любом из этих форматов. Она использует сжатие hello кодек находится в данных hello tooread hello метаданных. Однако при записи файла ORC tooan, фабрики данных выбирает ZLIB, который является по умолчанию hello для ORC. В настоящее время нет отсутствует параметр toooverride это поведение.

## <a name="parquet-format"></a>Формат Parquet
Если требуется tooparse hello Parquet файлы или записи данных hello в формате Parquet, задайте hello `format` `type` свойство слишком**ParquetFormat**. Необязательно toospecify любые свойства в раздел формата hello внутри раздела typeProperties hello. Пример:

```json
"format":
{
    "type": "ParquetFormat"
}
```
> [!IMPORTANT]
> При копировании файлов Parquet не **как-является** между локальными и облачными хранилищами данных, необходимо tooinstall hello JRE 8 (среда выполнения Java) на компьютере шлюза. Для 64-разрядного шлюза требуется 64-разрядная версия JRE, а для 32-разрядного шлюза — 32-разрядная версия JRE. Обе эти версии доступны [здесь](http://go.microsoft.com/fwlink/?LinkId=808605). Выберите подходящее hello.
>
>

Обратите внимание hello после точки.

* Данные сложных типов (MAP, LIST) не поддерживаются.
* Файл parquet имеет следующие параметры, связанные с сжатия hello: NONE, SNAPPY, GZIP и LZO. Фабрика данных поддерживает чтение данных из ORC-файла в любом из этих форматов. Он использует кодек сжатия hello в данных hello tooread hello метаданных. Однако при записи файла Parquet tooa, фабрики данных выбирает SNAPPY, что является по умолчанию hello для формата Parquet. В настоящее время нет отсутствует параметр toooverride это поведение.

## <a name="compression-support"></a>Поддержка сжатия
Обработка больших наборов данных может привести к возникновению узких мест ввода-вывода и сети. Таким образом, сжатых данных в хранилищах можно не только ускорения передачи данных по сети hello и сэкономить место на диске, но также перевести значительное повышение производительности при обработке больших данных. Сейчас сжатие поддерживается для файловых хранилищ данных, таких как хранилище BLOB-объектов Azure или локальная файловая система.  

Сжатие toospecify для набора данных, используйте hello **сжатия** свойство в наборе данных hello JSON и hello в следующем примере:   

```json
{  
    "name": "AzureBlobDataSet",  
    "properties": {  
        "availability": {  
            "frequency": "Day",  
              "interval": 1  
        },  
        "type": "AzureBlob",  
        "linkedServiceName": "StorageLinkedService",  
        "typeProperties": {  
            "fileName": "pagecounts.csv.gz",  
            "folderPath": "compression/file/",  
            "compression": {  
                "type": "GZip",  
                "level": "Optimal"  
            }  
        }  
    }  
}  
```

Предположим, что образец hello набора данных используется как hello выходные данные операции копирования, hello сжимает действия копирования hello выходных данных с помощью оптимальное соотношение кодека GZIP, а затем написать hello сжатых данных в файл с именем pagecounts.csv.gz в hello хранилища больших двоичных объектов.

> [!NOTE]
> Параметры сжатия не поддерживаются для данных в hello **AvroFormat**, **OrcFormat**, или **ParquetFormat**. При чтении файлов в этих форматах, фабрики данных определяет и использует кодек сжатия hello в метаданных hello. При написании toofiles в этих форматах, фабрики данных выбирает hello кодек сжатия по умолчанию для этого формата. Например, ZLIB для OrcFormat и SNAPPY для ParquetFormat.   

Hello **сжатия** раздел имеет два свойства:  

* **Тип:** hello сжатия кодека, который может быть **GZIP**, **Deflate**, **BZIP2**, или **ZipDeflate**.  
* **Уровень:** hello степени сжатия, который может быть **оптимальный** или **Fastest**.

  * **Самый быстрый:** операция сжатия hello следует выполнить как можно скорее, даже если hello получившийся файл оптимально не сжимаются.
  * **Оптимальное**: операция сжатия hello оптимального сжатия, даже если hello занимает больше времени, toocomplete время.

    Дополнительные сведения см. в разделе [Уровень сжатия](https://msdn.microsoft.com/library/system.io.compression.compressionlevel.aspx).

При указании `compression` свойства во входном наборе данных JSON конвейера hello можно считывать сжатые данные из источника hello; и при указании свойства hello в выходной набор данных JSON действие hello копирования можно написать назначения toohello сжатых данных. Ниже приведено несколько примеров сценариев:

* Прочитать GZIP сжатые данные из большого двоичного объекта Azure, распакуйте его и записи базы данных Azure SQL tooan данных результатов. Определение hello входного набора данных больших двоичных объектов Azure с hello `compression` `type` свойство JSON как GZIP.
* Чтение данных из текстового файла в локальной файловой системе, сжать формате GZip и записи tooan hello сжатых данных BLOB-объектов Azure. Определите выходной набор данных BLOB-объектов Azure с hello `compression` `type` свойство JSON как GZip.
* Чтение ZIP-файл с FTP-сервера, распаковать его файлы hello tooget внутри и перемещаться эти файлы в хранилище Озера данных Azure. Определение входного набора данных FTP с hello `compression` `type` свойства JSON в виде ZipDeflate.
* Считывать данные, сжатые GZIP из большого двоичного объекта Azure, распакуйте его, сжатие с помощью BZIP2 и записи tooan результат данных BLOB-объектов Azure. Определение hello входного набора данных больших двоичных объектов Azure с `compression` `type` задать tooGZIP и hello выходной набор данных с `compression` `type` в этом случае задайте tooBZIP2.   


## <a name="next-steps"></a>Дальнейшие действия
См. следующие статьи для хранилищ данных на основе файла, поддерживаемые фабрикой данных Azure hello.

- [Хранилище BLOB-объектов Azure](data-factory-azure-blob-connector.md)
- [Хранилище озера данных Azure](data-factory-azure-datalake-connector.md)
- [FTP](data-factory-ftp-connector.md)
- [HDFS](data-factory-hdfs-connector.md)
- [Перемещение данных в локальную файловую систему или из нее с помощью фабрики данных Azure](data-factory-onprem-file-system-connector.md)
- [Amazon S3](data-factory-amazon-simple-storage-service-connector.md)
