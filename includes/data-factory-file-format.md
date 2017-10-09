## <a name="specifying-formats"></a>Указание форматов
Фабрика данных Azure поддерживает следующие типы формата hello:

* [текстовый формат](#specifying-textformat);
* [формат JSON](#specifying-jsonformat);
* [формат Avro](#specifying-avroformat);
* [формат ORC](#specifying-orcformat);
* [формат PARQUET](#specifying-parquetformat).

### <a name="specifying-textformat"></a>Определение TextFormat
Если требуется tooparse hello текстовые файлы или записи данных hello в текстовом формате, задайте hello `format` `type` свойство слишком**TextFormat**. Можно также указать следующие hello **необязательно** свойства в hello `format` раздела. В разделе [примере TextFormat](#textformat-example) раздел, в tooconfigure.

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| columnDelimiter |символ Hello использовать tooseparate столбцов в файле. Можно рассмотреть возможность toouse редких непечатаемые char, вероятно, не существует в данных: например, укажите «\u0001» который представляет запуск из заголовка (SOH). |Допускается только один знак. Hello **по умолчанию** значение **запятая (,)**. <br/><br/>toouse символ Юникода ссылаться слишком[символов Юникода](https://en.wikipedia.org/wiki/List_of_Unicode_characters) tooget hello соответствующий код для него. |Нет |
| rowDelimiter |символ Hello использовать tooseparate строк в файле. |Допускается только один знак. Hello **по умолчанию** значение представляет собой любой hello последующих значений на чтение: **[«\r\n», «\r», «\n»]** и **«\r\n»** при записи. |Нет |
| escapeChar |специальный символ Hello использовать tooescape разделитель столбцов в hello содержимое входного файла. <br/><br/>Для таблицы нельзя указать и escapeChar, и quoteChar. |Допускается только один знак. Значение по умолчанию отсутствует. <br/><br/>Пример: при наличии запятая («,») как разделитель столбцов hello, но его необходимо toohave hello запятая в тексте hello (пример: «Hello, world»), можно определить как hello escape-символ «$» и использовать строку «Hello$, world» в источнике hello. |Нет |
| quoteChar |использовать знак Hello tooquote строковое значение. Hello разделители столбцов и строк внутри кавычек hello будет рассматриваться как часть hello строковое значение. Это свойство является применимо tooboth ввода и вывода наборов данных.<br/><br/>Для таблицы нельзя указать и escapeChar, и quoteChar. |Допускается только один знак. Значение по умолчанию отсутствует. <br/><br/>Например, если у вас есть запятая («,») как разделитель столбцов hello, но его необходимо toohave запятая в тексте hello (пример: < Hello, world >), можно определить» (двойная кавычка) как hello знак кавычек, чтобы использовать строку hello «Hello, world» в источнике hello. |Нет |
| nullValue |Один или несколько символов используется toorepresent значение null. |Один или несколько знаков. Hello **по умолчанию** значения **«\N» и «NULL»** для чтения и **«\N»** при записи. |Нет |
| encodingName |Укажите название кодировки hello. |Допустимое имя кодировки. Ознакомьтесь с описанием свойства [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx). Пример: windows-1250 или shift_jis. Hello **по умолчанию** значение **UTF-8**. |Нет |
| firstRowAsHeader |Указывает, является ли tooconsider hello первую строку как заголовок. Фабрика данных считывает первую строку входного набора данных как заголовок. Фабрика данных записывает первую строку как заголовок в выходной набор данных. <br/><br/>Примеры сценариев см. в разделе [Сценарии использования `firstRowAsHeader` и `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount). |Да<br/>**False (по умолчанию)** |Нет |
| skipLineCount |Указывает номер hello tooskip строк, при считывании данных из входных файлов. Если указаны skipLineCount и firstRowAsHeader, hello строки пропускаются сначала и затем сведения о заголовке hello считывается из входного файла hello. <br/><br/>Примеры сценариев см. в разделе [Сценарии использования `firstRowAsHeader` и `skipLineCount`](#scenarios-for-using-firstrowasheader-and-skiplinecount). |Целое число  |Нет |
| treatEmptyAsNull |Указывает, является ли tootreat null или пустую строку как строку null значения при считывании данных из входного файла. |**True (по умолчанию)**<br/>Ложь |Нет |

#### <a name="textformat-example"></a>Пример TextFormat
Hello следующий пример показывает некоторые свойства формата hello для TextFormat.

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

#### <a name="scenarios-for-using-firstrowasheader-and-skiplinecount"></a>Сценарии использования firstRowAsHeader и skipLineCount
* Копирование из файла источника, не являющимся файлами tooa и хотите tooadd заголовка строки, содержащей hello схемы метаданных (например: SQL-схема). Укажите `firstRowAsHeader` как true в hello выходной набор данных для этого сценария.
* Копирование из текстового файла, содержащего приемник не являющимся файлами tooa заголовка строки и хотите toodrop, строка. Укажите `firstRowAsHeader` как true во входном наборе данных hello.
* Копирование из текстового файла и хотите tooskip несколько строк в начале hello, которые не содержат данных или заголовка информации. Укажите `skipLineCount` tooindicate hello число строк toobe пропущено. Если hello остальной части файла hello содержит строку заголовка, можно указать `firstRowAsHeader`. Если оба `skipLineCount` и `firstRowAsHeader` указаны, hello строки пропускаются сначала и затем сведения о заголовке hello считывается из входного файла hello

### <a name="specifying-jsonformat"></a>Указание JsonFormat
слишком**импорта и экспорта файлов JSON в качестве-в / из базы данных Azure Cosmos**, в разделе [документов JSON импорта и экспорта](../articles/data-factory/data-factory-azure-documentdb-connector.md#importexport-json-documents) раздела hello Azure Cosmos DB соединителя с подробными сведениями.

Если требуется tooparse hello JSON-файлов или запись данных hello в формате JSON, задайте hello `format` `type` свойство слишком**JsonFormat**. Можно также указать следующие hello **необязательно** свойства в hello `format` раздела. В разделе [JsonFormat пример](#jsonformat-example) раздел, в tooconfigure.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| filePattern |Укажите шаблон hello данных, хранящихся в каждом файле JSON. Допустимые значения: **setOfObjects** и **arrayOfObjects**. Hello **по умолчанию** значение **setOfObjects**. Подробные сведения об этих шаблонах см. в разделе [Шаблоны файлов JSON](#json-file-patterns). |Нет |
| jsonNodeReference | Tooiterate и извлечения данных из объектов hello в массив полей с hello же шаблон, укажите путь к JSON hello этого массива. Это свойство поддерживается только в том случае, если данные копируются из JSON-файлов. | Нет |
| jsonPathDefinition | Укажите hello выражения пути JSON для каждого сопоставления столбцов с именем пользовательские столбца (начало строчных). Это свойство поддерживается только в том случае, если данные копируются из JSON-файлов и данные можно извлечь из объекта или массива. <br/><br/> Для поля в корневой объект, начинаться с $ корневой; для полей внутри массива hello выбирается программой `jsonNodeReference` свойство начинаются с Привет элемента массива. В разделе [JsonFormat пример](#jsonformat-example) раздел, в tooconfigure. | Нет |
| encodingName |Укажите название кодировки hello. Hello список допустимых названий кодировок см. в разделе: [Encoding.EncodingName](https://msdn.microsoft.com/library/system.text.encoding.aspx) свойство. Например: windows-1250 или shift_jis. Hello **по умолчанию** значение: **UTF-8**. |Нет |
| nestingSeparator |Символ, используемые tooseparate уровней вложения. значение по умолчанию Hello "." (точка). |Нет |

#### <a name="json-file-patterns"></a>Шаблоны файлов JSON

Действие копирования может проанализировать приведенные ниже шаблоны JSON-файлов.

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

#### <a name="jsonformat-example"></a>Пример JsonFormat

**Вариант 1. Копирование данных из JSON-файлов**

См. ниже два вида образцы при копировании данных из JSON-файлов и hello toonote универсальных точек:

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

- `structure`раздел определяет имена столбцов настроенные hello и hello соответствующие типы данных во время преобразования данных tootabular. Этот раздел представляет **необязательно** при отсутствии необходимости toodo сопоставления столбцов. Дополнительные сведения см. в статье [Указание определения структуры для прямоугольных наборов данных](#specifying-structure-definition-for-rectangular-datasets).
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

- `structure`раздел определяет имена столбцов настроенные hello и hello соответствующие типы данных во время преобразования данных tootabular. Этот раздел представляет **необязательно** при отсутствии необходимости toodo сопоставления столбцов. Дополнительные сведения см. в статье [Указание определения структуры для прямоугольных наборов данных](#specifying-structure-definition-for-rectangular-datasets).
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

Если в базе данных SQL есть такая таблица:

| id | order_date | order_price | order_by |
| --- | --- | --- | --- |
| 1 | 20170119 | 2000 | David |
| 2 | 20170120 | 3500 | Patrick |
| 3 | 20170121 | 4000 | Jason |

и для каждой записи, предполагается, что объект JSON tooa toowrite в ниже формат:
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

Hello выходной набор данных с **JsonFormat** тип определяется следующим образом: (частичное определение с частями hello применимо). В частности `structure` раздел определяет имена свойств настроенные hello в конечный файл `nestingSeparator` (по умолчанию — «.») будет иметь уровень вложенности hello используется tooidentify из имени hello. Этот раздел представляет **необязательно** , если не требуется имя свойства toochange hello, сравнение с именем столбца источника или вложить некоторые свойства hello.

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

### <a name="specifying-avroformat"></a>Определение AvroFormat
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

### <a name="specifying-orcformat"></a>Указание OrcFormat
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

### <a name="specifying-parquetformat"></a>Указание ParquetFormat
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
