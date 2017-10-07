---
title: "aaaAzure фабрика данных — ссылка сценария JSON | Документы Microsoft"
description: "Содержит схемы JSON для сущностей фабрики данных."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 813fd752bb0ecb1b513d022b9f302325105dac31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---json-scripting-reference"></a>Справочник по написанию скриптов JSON фабрики данных Azure
Эта статья содержит схемы JSON и примеры для определения сущностей фабрики данных Azure (конвейер, действие, набор данных и связанная служба).  

## <a name="pipeline"></a>Конвейер 
Высокоуровневая структура Hello для определения конвейера выглядит следующим образом: 

```json
{
  "name": "SamplePipeline",
  "properties": {
    "description": "Describe what pipeline does",
    "activities": [
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

Следующей таблице описаны свойства hello в определении JSON конвейера hello.

| Свойство | Описание | Обязательно
-------- | ----------- | --------
| name | Имя конвейера hello. Укажите имя, которое представляет действие hello, hello действия или конвейер — настроенное toodo<br/><ul><li>Максимальное количество знаков: 260.</li><li>Должно начинаться с буквы, цифры или символа подчеркивания (_).</li><li>Следующие знаки не допускаются: ".", "+", "?", "/", "<", ">", "*", "%", "&", ":", "\\".</li></ul> |Да |
| Описание |Текст, описывающий, какое действие hello или конвейера используется для | Нет |
| Действия | Содержит список действий. | Да |
| start |Дата и время начала для конвейера hello. Задается в [формате ISO](http://en.wikipedia.org/wiki/ISO_8601). Например: 2014-10-14T16:32:41. <br/><br/>Это возможно toospecify местное время, например время. Пример: `2016-02-27T06:00:00**-05:00`. Это 6:00 по восточному стандартному времени.<br/><br/>Hello начального и конечного свойства вместе задают активный период для конвейера hello. Срезы выходных данных создаются только в этот активный период. |Нет<br/><br/>Если указать значение для свойства окончания hello, необходимо указать значение для свойства начала hello.<br/><br/>Hello начальное и конечное время могут быть пустой toocreate конвейера. Необходимо указать оба значения tooset на активный период для конвейера toorun hello. Если не указать время начала и окончания при создании конвейера, можно установить их позже с помощью командлета Set AzureRmDataFactoryPipelineActivePeriod hello. |
| end |Дата и время окончания для конвейера hello. Не является обязательным и задается в формате ISO. Например: 2014-10-14T17:32:41 <br/><br/>Это возможно toospecify местное время, например время. Пример: `2016-02-27T06:00:00**-05:00`. Это 6:00 по восточному стандартному времени.<br/><br/>toorun hello конвейера неопределенно долгое время, укажите 9999-09-09 как hello значение для свойства окончания hello. |Нет <br/><br/>Если указать значение для свойства начала hello, необходимо указать значение для свойства окончания hello.<br/><br/>См. примечания для hello **запустить** свойство. |
| isPaused |Если набор tootrue hello конвейера не выполняется. Значение по умолчанию — false. Можно использовать это свойство tooenable или отключить. |Нет |
| pipelineMode |метод Hello планирования выполняется для hello конвейера. Допустимые значения: scheduled (по умолчанию), onetime.<br/><br/>«Запланировано» указывает, что конвейера hello запускается в заданный интервал времени в соответствии с tooits активного периода (время начала и окончания). «Onetime» указывает, что этот конвейер hello запускается только один раз. В настоящее время изменить или обновить однократные конвейеры после их создания нельзя. Подробные сведения об однократном запуске см. в разделе [Однократный конвейер](data-factory-create-pipelines.md#onetime-pipeline). |Нет |
| expirationTime; |Продолжительность времени после создания для какой hello конвейера является допустимым и должен оставаться подготовкой. Если не включает все активные сбой, или ожидающие выполнения, конвейера hello будет автоматически удалена при достижении hello время истечения срока действия. |Нет |


## <a name="activity"></a>Действие 
Высокоуровневая структура Hello для действия в рамках определения конвейера (элемент действия) выглядит следующим образом:

```json
{
    "name": "ActivityName",
    "description": "description", 
    "type": "<ActivityType>",
    "inputs":  "[]",
    "outputs":  "[]",
    "linkedServiceName": "MyLinkedService",
    "typeProperties":
    {

    },
    "policy":
    {
    }
    "scheduler":
    {
    }
}
```

Следующие таблицы описывают свойства hello в действии hello определения JSON.

| Тег | Описание | Обязательно |
| --- | --- | --- |
| name |Имя действия hello. Укажите имя, которое представляет действие hello, действие hello настроить toodo<br/><ul><li>Максимальное количество знаков: 260.</li><li>Должно начинаться с буквы, цифры или символа подчеркивания (_).</li><li>Следующие знаки не допускаются: ".", "+", "?", "/", "<", ">", "*", "%", "&", ":", "\\".</li></ul> |Да |
| Описание |Текст, описывающий, какое действие hello используется для. |Да |
| type |Указывает тип действия hello hello. . В разделе hello [ХРАНИЛИЩ данных](#data-stores) и [действия ПРЕОБРАЗОВАНИЯ данных](#data-transformation-activities) разделы для различных типов действий. |Да |
| inputs |Входные таблицы, используемые действием hello<br/><br/>`// one input table`<br/>`"inputs":  [ { "name": "inputtable1"  } ],`<br/><br/>`// two input tables` <br/>`"inputs":  [ { "name": "inputtable1"  }, { "name": "inputtable2"  } ],` |Да |
| outputs |Выходные таблицы, используемые с действия "hello".<br/><br/>`// one output table`<br/>`"outputs":  [ { "name": “outputtable1” } ],`<br/><br/>`//two output tables`<br/>`"outputs":  [ { "name": “outputtable1” }, { "name": “outputtable2” }  ],` |Да |
| linkedServiceName (имя связанной службы) |Имя hello связанной службы, используемый действием hello. <br/><br/>Действие может потребоваться указать hello связаны службы, которая связывает toohello необходимые вычислительную среду. |Да, для действий HDInsight, Машинного обучения Azure и действия хранимой процедуры. <br/><br/>Нет — для всех остальных |
| typeProperties |Свойства в разделе "typeProperties" hello, зависят от типа действия hello. |Нет |
| policy |Политики, влияющие на поведение во время выполнения hello действия "hello". Если для этого свойства не задано значение, используются стандартные политики. |Нет |
| scheduler |Свойство «планировщик» является используется toodefine требуемого планирования для действия "hello". Его подсвойства так же, как в hello hello hello [доступность свойство в наборе данных](data-factory-create-datasets.md#dataset-availability). |Нет |

### <a name="policies"></a>Политики
Политики влияют на поведение hello во время выполнения действия, особенно при обработке среза таблицы hello. Привет, в следующей таблице подробно описаны hello.

| Свойство | Допустимые значения | Значение по умолчанию | Описание |
| --- | --- | --- | --- |
| concurrency |Целое число  <br/><br/>Максимальное значение — 10 |1 |Число одновременных выполнений действия hello.<br/><br/>Он определяет hello число параллельных выполнений действия может произойти на различных срезах. Например если действие должно toogo через большого набора данных, наличие большего значения параллелизма ускоряет обработку данных hello. |
| executionPriorityOrder |NewestFirst<br/><br/>OldestFirst |OldestFirst |Определяет порядок hello срезы данных, которые обрабатываются.<br/><br/>Предположим, есть два ожидающих обработки среза (от 16:00 и от 17:00). При установке toobe hello executionpriorityorder значения NewestFirst сначала обрабатывается срез hello в 17: 00. Аналогичным образом при установке toobe hello executionpriorityorder значения OldestFIrst затем обрабатываются срез hello в 16: 00. |
| retry |Целое число <br/><br/>Максимальное значение — 10 |0 |Число повторных попыток перед hello обработки данных для hello среза помечается как ошибка. Выполнение действия для среза данных будет предпринята повторная попытка копирования toohello указанное число повторных попыток. Повторная попытка Hello выполняется как можно быстрее после сбоя hello. |
| timeout |TimeSpan |00:00:00 |Время ожидания для действия "hello". Пример: 00:10:00 (время ожидания — 10 минут).<br/><br/>Если значение не указано или равно 0, используется бесконечное время ожидания hello.<br/><br/>Если hello время обработки данных среза превышает значение времени ожидания hello, отмены и hello система пытается tooretry hello обработки. Hello число повторов зависит от свойства retry hello. При возникновении времени ожидания hello перейдет в состояние tooTimedOut. |
| delay |TimeSpan |00:00:00 |Укажите задержку hello перед обработкой данных начинается срез hello.<br/><br/>Hello выполнение действия для среза данных запускается после hello задержки прошлом hello ожидаемое время выполнения.<br/><br/>Пример: 00:10:00 (означает задержку в 10 минут). |
| longRetry |Целое число <br/><br/>Максимальное значение — 10 |1 |Hello количество длинных повторных попыток: hello выполнение среза завершается сбоем.<br/><br/>Интервал между этими попытками задается свойством longRetryInterval. Поэтому если вам требуется toospecify время между попытками повтора, следует используйте longRetry. Если указаны свойства Retry и longRetry, каждая попытка longRetry включает повторных попыток и hello максимальное число попыток повтора * longRetry.<br/><br/>Например, если у нас есть следующие параметры в политике действия hello hello:<br/>Retry: 3<br/>longRetry: 2<br/>longRetryInterval: 01:00:00<br/><br/>Предположим, что существует только один срез tooexecute (состояние ожидания) и hello действие происходит сбой выполнения каждый раз. Первые три попытки будут выполнены подряд. После каждой попытки hello состояние среза будет Retry. После первых 3 попытки через hello состояние среза станет LongRetry.<br/><br/>Через час (значение свойства longRetryInterval) будут выполнены еще три попытки подряд. После этого состояние среза hello бы сбой, и дальнейшие попытки предприниматься. Поэтому всего было предпринято 6 попыток.<br/><br/>Если любое выполнение завершится успешно, hello состояние среза будет готова, и дальнейшие попытки не предпринимаются.<br/><br/>longRetry может использоваться в ситуациях, когда данные, зависящие от поступает на неопределенное время или hello общей среды подключением отображается под какие обработки данных. В таких случаях один за другим образом повторных попыток может не позволить и таким образом через определенные интервалы времени приводит к hello требуемого выходных данных.<br/><br/>Предупреждение. Не задавайте высокие значения для свойств longRetry и longRetryInterval. Как правило, более высокие значения приводят к появлению других системных проблем. |
| longRetryInterval |TimeSpan |00:00:00 |Hello задержка между попытками longretry |

### <a name="typeproperties-section"></a>Раздел typeProperties
раздел typeProperties Hello отличается для каждого действия. Преобразование действия имеют только свойства типа hello. В разделе [ДЕЙСТВИЯ ПРЕОБРАЗОВАНИЯ ДАННЫХ](#data-transformation-activities) этой статьи представлены примеры JSON, определяющие действия преобразования в конвейере. 

**Действие копирования** имеет два подраздела в разделе typeProperties hello: **источника** и **приемник**. В разделе [ХРАНИЛИЩ данных](#data-stores) статьи в этой статье для JSON образцы, где показано, как сохранить toouse данных в качестве источника и приемника. 

### <a name="sample-copy-pipeline"></a>Пример конвейера копирования
В следующий пример конвейера hello, есть одно действие типа **копирования** в hello **действия** раздела. В этом образце hello [действие копирования](data-factory-data-movement-activities.md) копирует данные из базы данных Azure SQL tooan хранилища больших двоичных объектов Azure. 

```json
{
  "name": "CopyPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputDataset"
          }
        ],
        "outputs": [
          {
            "name": "OutputDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00",
    "end": "2016-07-13T00:00:00"
  }
} 
```

Обратите внимание hello после точки.

* В разделе "действия" hello, имеется только одно действие, **тип** задано слишком**копирования**.
* Входных данных для действия hello установлено слишком**InputDataset** и вывода для hello действия установлено слишком**OutputDataset**.
* В hello **typeProperties** разделе **BlobSource** указан в качестве типа источника hello и **SqlSink** указан как тип приемника hello.

В разделе [ХРАНИЛИЩ данных](#data-stores) статьи в этой статье для JSON образцы, где показано, как сохранить toouse данных в качестве источника и приемника.    

Полное Пошаговое руководство по созданию этого конвейера, в разделе [учебника: копирование данных из хранилища больших двоичных объектов tooSQL базы данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

### <a name="sample-transformation-pipeline"></a>Пример конвейера преобразования
В следующий пример конвейера hello, есть одно действие типа **HDInsightHive** в hello **действия** раздела. В этом образце hello [действие Hive в HDInsight](data-factory-hive-activity.md) преобразует данные из хранилища больших двоичных объектов Azure, выполнив файл скрипта Hive в кластере Azure HDInsight Hadoop. 

```json
{
    "name": "TransformPipeline",
    "properties": {
        "description": "My first Azure Data Factory pipeline",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "AzureStorageLinkedService",
                    "defines": {
                        "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                        "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Month",
                    "interval": 1
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00",
        "isPaused": false
    }
}
```

Обратите внимание hello после точки. 

* В разделе "действия" hello, имеется только одно действие, **тип** задано слишком**HDInsightHive**.
* файл скрипта Hive Hello, **partitionweblogs.hql**, хранятся в учетной записи хранилища Azure hello (определяемое scriptLinkedService hello, вызывается **AzureStorageLinkedService**) и в  **сценарий** папки в контейнере hello **adfgetstarted**.
* Hello **определяет** раздел представляет параметры среды выполнения используется toospecify hello, переданных toohello скрипт hive в качестве значения конфигурации Hive (например `${hiveconf:inputtable}`, `${hiveconf:partitionedtable}`).

В разделе [ДЕЙСТВИЯ ПРЕОБРАЗОВАНИЯ ДАННЫХ](#data-transformation-activities) этой статьи представлены примеры JSON, определяющие действия преобразования в конвейере.

Полное Пошаговое руководство по созданию этого конвейера, в разделе [учебника: построение первые данные конвейера tooprocess использование кластера Hadoop](data-factory-build-your-first-pipeline.md). 

## <a name="linked-service"></a>Связанные службы
Высокоуровневая структура Hello для определения связанной службы выглядит следующим образом:

```json
{
    "name": "<name of hello linked service>",
    "properties": {
        "type": "<type of hello linked service>",
        "typeProperties": {
        }
    }
}
```

Следующие таблицы описывают свойства hello в действии hello определения JSON.

| Свойство | Описание | Обязательно |
| -------- | ----------- | -------- | 
| name | Имя hello связанной службы. | Да | 
| properties - type | Тип hello связанной службы. Например, служба хранилища Azure, база данных SQL Azure. |
| typeProperties | раздел typeProperties Hello содержит элементы, которые различны для каждого хранилища данных или среды вычислений. В разделе [хранилищ данных](#datastores) статьи для всех данных hello хранения связанных служб и [вычислений средах](#compute-environments) hello все связанные службы вычислений |   

## <a name="dataset"></a>Выборка 
Набор данных в фабрике Azure имеет определение следующего вида.

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "external": <boolean flag tooindicate external data. only for input datasets>,
        "linkedServiceName": "<Name of hello linked service that refers tooa data store.>",
        "structure": [
            {
                "name": "<Name of hello column>",
                "type": "<Name of hello type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        },
        "availability": {
            "frequency": "<Specifies hello time unit for data slice production. Supported frequency: Minute, Hour, Day, Week, Month>",
            "interval": "<Specifies hello interval within hello defined frequency. For example, frequency set too'Hour' and interval set too1 indicates that new data slices should be produced hourly>"
        },
       "policy":
        {      
        }
    }
}
```

Привет, в следующей таблице описываются свойства в hello выше JSON:   

| Свойство | Описание | Обязательно | значение по умолчанию |
| --- | --- | --- | --- |
| name | Имя набора данных hello. Правила именования для фабрики данных Azure описаны [здесь](data-factory-naming-rules.md) . |Да |Нет данных |
| type | Тип набора данных hello. Укажите один из типов hello, поддерживаемые фабрикой данных Azure (например: AzureBlob, AzureSqlTable). В разделе [ХРАНИЛИЩ данных](#data-stores) статьи для всех hello набора данных типы, поддерживаемые фабрикой данных и хранилищ данных. | 
| structure | Схема набора данных hello. Она содержит столбцы, их типы и т. д. | Нет |Нет данных |
| typeProperties | Свойства, соответствующие toohello выбранный тип. В разделе [ХРАНИЛИЩА ДАННЫХ](#data-stores) указаны поддерживаемые типы и их свойства. |Да |Нет данных |
| external | Логический флаг toospecify ли набор данных явно созданные конвейере фабрики данных или нет. |Нет |нет |
| availability | Определяет hello обработки окна или hello Фрагментирование модели для производства hello набора данных. Дополнительные сведения о hello набора данных, Создание срезов модели см [планирования и выполнения](data-factory-scheduling-and-execution.md) статьи. |Да |Нет данных |
| policy |Определяет условия hello или hello условие, которое необходимо выполнить все фрагменты hello набора данных. <br/><br/>Дополнительные сведения см. в разделе [Политика наборов данных](#Policy). |Нет |Нет данных |

Каждый столбец в hello **структуры** раздел содержит hello следующие свойства:

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| name |Имя столбца hello. |Да |
| type |Тип данных столбца hello.  |Нет |
| culture |На базе .NET toobe языка и региональных параметров, которые используются, если указан тип и типом .NET `Datetime` или `Datetimeoffset`. Значение по умолчанию — `en-us`. |Нет |
| свойства |Формат строки toobe используются, если указан тип и типом .NET `Datetime` или `Datetimeoffset`. |Нет |

В следующем примере hello, hello набор данных содержит три столбца `slicetimestamp`, `projectname`, и `pageviews` и они имеют тип: строка, строка и десятичных соответственно.

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

Hello следующей таблице описаны свойства можно использовать в hello **доступности** раздела:

| Свойство | Описание | Обязательно | значение по умолчанию |
| --- | --- | --- | --- |
| frequency |Указывает единицу времени hello для производственного среза набора данных.<br/><br/><b>Поддерживаемые значения</b>: Minute, Hour, Day, Week, Month. |Да |Нет данных |
| interval |Задает множитель для частоты.<br/><br/>«Интервал частоты x» определяет, как часто hello срезов.<br/><br/>Если требуется hello срез в час toobe набора данных, задайте <b>частоты</b> слишком<b>час</b>, и <b>интервал</b> слишком<b>1</b>.<br/><br/><b>Примечание</b>: Если указать для частоты минуты, рекомендуется установить интервал toono hello меньше 15 |Да |Нет данных |
| style |Указывает, является ли hello срезов в hello начала и окончания интервала hello.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul><br/><br/>Если частота имеет значение tooMonth и задан стиль tooEndOfInterval, hello срезов на hello последний день месяца. Если задан tooStartOfInterval стиль hello, hello срезов на hello первый день месяца.<br/><br/>Если частота имеет значение tooDay и задан стиль tooEndOfInterval, hello срезов в hello последний час дня hello.<br/><br/>Если частота имеет значение tooHour и задан стиль tooEndOfInterval, hello срезов в конце hello hello час. Например для среза для периода с 13: 00 до 14: 00, hello срез создается в 14: 00. |Нет |EndOfInterval |
| anchorDateTime |Определяет hello абсолютное положение во времени, используемые границы фрагмента планировщика toocompute набора данных. <br/><br/><b>Примечание</b>: Если hello AnchorDateTime есть части даты, которые являются более детализированными, чем частота hello, а затем hello более детализированные части игнорируются. <br/><br/>Например, если hello <b>интервал</b> — <b>каждый час</b> (частота: час и интервал: 1) и hello <b>AnchorDateTime</b> содержит <b>минуты и секунды</b>затем hello <b>минуты и секунды</b> части hello AnchorDateTime игнорируются. |Нет |01/01/0001 |
| offset |Интервал времени, по которой hello Сдвиг начала и окончания всех фрагментов набора данных. <br/><br/><b>Примечание</b>: Если указаны значения для anchorDateTime и offset, результатом hello является shift hello вместе. |Нет |Нет данных |

Hello в следующем разделе доступности указывает, что hello выходной набор данных либо созданных каждый час (или) входные данные набор данных доступен каждый час:

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

Hello **политики** раздела в определении набора данных, определяет условия hello или необходимо выполнить условие hello, hello фрагментов набора данных.

| Имя политики | Описание | Применить слишком| Обязательно | значение по умолчанию |
| --- | --- | --- | --- | --- |
| minimumSizeMB |Проверяет, данные hello в **BLOB-объектов Azure** соответствует hello требования минимальный размер (в мегабайтах). |Большой двоичный объект Azure |Нет |Нет данных |
| minimumRows |Проверяет, данные hello в **базы данных Azure SQL** или **таблицы Azure** содержит hello минимальное количество строк. |<ul><li>База данных SQL Azure</li><li>таблице Azure</li></ul> |Нет |Нет данных |

**Пример**

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

Если набор данных не создается фабрикой данных Azure, он должен быть помечен как **external**. Этот параметр применяется обычно toohello вводов первое действие в конвейере, если не используется действие или цепочки конвейера.

| Имя | Описание | Обязательно | По умолчанию |
| --- | --- | --- | --- |
| dataDelay |Проверка времени toodelay hello на доступность hello hello внешних данных для заданного фрагмента hello. Например если hello данные будут доступны каждый час, hello проверка toosee hello внешних данных доступен и hello соответствующего среза с помощью dataDelay может быть задержано все готово.<br/><br/>Применяется toohello только текущее время.  Например если это 1:00 PM в данный момент, и это значение составляет 10 минут, проверки hello начинается в 13:10.<br/><br/>Этот параметр не влияет на срезы в прошлом hello (срезы со временем окончания среза + dataDelay < теперь) обрабатываются без задержки.<br/><br/>Время больше 23:59 часов необходимо с помощью hello toospecified `day.hours:minutes:seconds` формат. Например toospecify 24 часа, не используйте 24:00:00; Вместо этого используйте 1.00:00:00. Значение 24:00:00 обозначает 24 дня (24.00:00:00). Чтобы задать 1 день и 4 часа, укажите 1:04:00:00. |Нет |0 |
| retryInterval |время ожидания Hello между Далее повторной попыткой сбоя и hello. В случае отказа try после retryInterval могут hello следующей попытки. <br/><br/>Если это 1:00 PM прямо сейчас мы начинаем hello первой попытки. Если hello длительность toocomplete hello первой проверки — 1 минута и не удалось выполнить операцию hello, hello следующий Повтор — 1:00 + 1 минута (длительность) + 1 минута (интервал повтора) = 13:02:00. <br/><br/>Срезы в прошлом hello нет без задержки. Повторите попытку Hello происходит немедленно. |Нет |00:01:00 (1 минута) |
| retryTimeout |Здравствуйте, время ожидания для каждой повторной попытке.<br/><br/>Если это свойство имеет значение минут too10 hello toobe требованиям проверки завершена в течение 10 минут. Если он занимает больше 10 минут tooperform hello проверки, hello повторите истечением времени ожидания.<br/><br/>Если все попытки проверки hello время ожидания, срез hello помечен как TimedOut. |Нет |00:10:00 (10 минут) |
| maximumRetry |Сколько раз toocheck для обеспечения доступности hello hello внешних данных. Hello разрешен максимальное значение равно 10. |Нет |3 |


## <a name="data-stores"></a>ХРАНИЛИЩА ДАННЫХ
Hello [связанная служба](#linked-service) раздел параметров описания для распространенных типов связанных служб tooall элементы JSON. В этом разделе приводятся описания JSON элементы, которые являются определенной tooeach хранилища данных.

Hello [Dataset](#dataset) описания раздел параметров для элементов JSON, которые существуют типы tooall наборов данных. В этом разделе приводятся описания JSON элементы, которые являются определенной tooeach хранилища данных.

Hello [действия](#activity) описания раздел параметров для элементов JSON, которые существуют типы tooall действий. Этот раздел предоставляет сведения об элементах JSON, которые доступны определенной tooeach хранилища данных в том случае, когда она используется в качестве источника и приемника в действии копирования.  

Щелкните ссылку hello hello хранилища вы заинтересованы в схемах JSON hello toosee для связанной службы, набор данных и hello источника и приемника для действия копирования hello.

| Категория | Хранилище данных 
|:--- |:--- |
| **Таблицы Azure** |[хранилище BLOB-объектов Azure](#azure-blob-storage) |
| &nbsp; |[Хранилище озера данных Azure](#azure-datalake-store) |
| &nbsp; |[Azure Cosmos DB](#azure-cosmos-db) |
| &nbsp; |[База данных SQL Azure;](#azure-sql-database) |
| &nbsp; |[Хранилище данных Azure SQL](#azure-sql-data-warehouse) |
| &nbsp; |[Поиск Azure;](#azure-search) |
| &nbsp; |[Хранилище таблиц Azure](#azure-table-storage) |
| **Базы данных** |[Amazon Redshift](#amazon-redshift) |
| &nbsp; |[IBM DB2](#ibm-db2) |
| &nbsp; |[MySQL](#mysql) |
| &nbsp; |[Oracle](#oracle) |
| &nbsp; |[PostgreSQL](#postgresql) |
| &nbsp; |[SAP Business Warehouse](#sap-business-warehouse) |
| &nbsp; |[SAP HANA](#sap-hana) |
| &nbsp; |[SQL Server](#sql-server) |
| &nbsp; |[Sybase](#sybase) |
| &nbsp; |[Teradata](#teradata) |
| **NoSQL** |[Cassandra](#cassandra) |
| &nbsp; |[MongoDB](#mongodb) |
| **File** |[Amazon S3](#amazon-s3) |
| &nbsp; |[Перемещение данных в локальную файловую систему или из нее с помощью фабрики данных Azure](#file-system) |
| &nbsp; |[FTP](#ftp) |
| &nbsp; |[HDFS](#hdfs) |
| &nbsp; |[SFTP](#sftp) |
| **Прочее** |[HTTP](#http) |
| &nbsp; |[OData](#odata) |
| &nbsp; |[ODBC](#odbc) |
| &nbsp; |[Salesforce](#salesforce) |
| &nbsp; |[Веб-таблица](#web-table) |

## <a name="azure-blob-storage"></a>Хранилище больших двоичных объектов Azure

### <a name="linked-service"></a>Связанные службы
Существует два типа связанных служб: связанная служба хранилища Azure и связанная служба SAS хранилища Azure.

#### <a name="azure-storage-linked-service"></a>Связанная служба хранилища Azure
toolink фабрики данных tooa учетной записи хранилища Azure с помощью hello **ключ учетной записи**, создания связанной службой хранилища Azure. Хранилище Azure toodefine связанной службы, набор hello **тип** hello связанной службы слишком**AzureStorage**. Затем можно указать следующие свойства в hello **typeProperties** раздела:  

| Свойство | Описание | Обязательно |
|:--- |:--- |:--- |
| connectionString |Укажите сведения, необходимые для свойства connectionString hello tooconnect tooAzure хранилища. |Да |

##### <a name="example"></a>Пример  

```json
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

#### <a name="azure-storage-sas-linked-service"></a>Связанная служба SAS хранилища Azure
Hello связаны SAS хранилища Azure службы позволяет toolink фабрикой данных Azure tooan учетной записи хранилища Azure с помощью подписи общего доступа (SAS). Он предоставляет hello фабрики данных ограничен или ограниченным временем доступа ресурсов, связанных с/tooall (/ контейнер больших двоичных объектов) в хранилище hello. toolink фабрики данных tooa учетной записи хранилища Azure с помощью подписи общего доступа, создания службы связаны SAS хранилища Azure. toodefine SAS хранилища Azure связанной службы, набор hello **тип** hello связанной службы слишком**AzureStorageSas**. Затем можно указать следующие свойства в hello **typeProperties** раздела:   

| Свойство | Описание | Обязательно |
|:--- |:--- |:--- |
| sasUri |Укажите общий URI подписи доступа toohello хранилища Azure ресурсы, такие как BLOB-объекта, контейнера или таблицы. |Да |

##### <a name="example"></a>Пример

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

Дополнительные сведения об этих связанных службах см. в статье о [соединителе хранилища BLOB-объектов Azure](data-factory-azure-blob-connector.md#linked-service-properties). 

### <a name="dataset"></a>Выборка
toodefine набору данных больших двоичных объектов Azure hello набор **тип** hello набора данных слишком**AzureBlob**. Затем укажите следующие свойства конкретного BLOB-объектов Azure в hello hello **typeProperties** раздела: 

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| folderPath |Контейнер toohello путь к папке, в hello хранилище больших двоичных объектов. Пример: myblobcontainer\myblobfolder\ |Да |
| fileName |Имя большого двоичного объекта hello. Свойство fileName является необязательным и в нем учитывается регистр знаков.<br/><br/>При указании имени файла, hello деятельности (включая копирования) работает на hello определенным BLOB-объектом.<br/><br/>Если не указано имя файла, копирования включает все большие двоичные объекты в folderPath hello для входного набора данных.<br/><br/>Если имя файла не указано для выходной набор данных, имя hello hello созданный файл будет в следующем формате hello: данные. <Guid>.txt (например:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Нет |
| partitionedBy |Необязательное свойство. Можно использовать его toospecify динамического folderPath и filename для временного ряда данных. Например, путь к папке (значение folderPath) каждый час может быть другим. |Нет |
| свойства | поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Набор hello **тип** свойства в формате tooone из следующих значений. Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Если требуется слишком**скопируйте файлы как-является** между файловых хранилищ (двоичный копия), пропустите раздел формат hello в оба определения набора входных и выходных данных. |Нет |
| compression | Укажите тип hello и уровень сжатия данных hello. Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**. Поддерживаемые уровни: **Optimal** и **Fastest**. См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Нет |

#### <a name="example"></a>Пример

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
 ```


Дополнительные сведения см. в статье о [соединителе больших двоичных объектов Azure](data-factory-azure-blob-connector.md#dataset-properties).

### <a name="blobsource-in-copy-activity"></a>BlobSource в действии копирования
При копировании данных из хранилища больших двоичных объектов Azure, задайте hello **тип источника** из hello в действии копирования слишком**BlobSource**и укажите следующие свойства в hello ** источника ** раздела:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| recursive |Указывает, доступна ли для чтения рекурсивно hello данных из подпапок hello или только из указанной папки hello. |True (значение по умолчанию), False |Нет |

#### <a name="example-blobsource"></a>Пример: BlobSource **
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "SqlSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
### <a name="blobsink-in-copy-activity"></a>BlobSink в действии копирования
При копировании данных tooan хранилища больших двоичных объектов задайте hello **тип приемника** из hello в действии копирования слишком**BlobSink**и укажите следующие свойства в hello **приемник** раздела:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| copyBehavior |Определяет поведение копирования hello, когда источник hello BlobSource или файловой системы. |<b>PreserveHierarchy</b>: сохраняет hello иерархию файлов в целевой папке hello. Hello относительный путь к исходной папке toosource файла представляет идентичные toohello относительный путь папки tootarget целевого файла.<br/><br/><b>FlattenHierarchy</b>: все файлы из исходной папки hello в hello сначала уровень целевую папку. файлы целевой Hello иметь автоматически созданное имя. <br/><br/><b>MergeFiles (по умолчанию):</b> объединяет все файлы из папки tooone hello исходного файла. Если указано имя файла или большого двоичного объекта hello hello объединенный файл будет hello указанным именем. в противном случае будет автоматически формируемого имени файла. |Нет |

#### <a name="example-blobsink"></a>Пример: BlobSink

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Дополнительные сведения см. в статье о [соединителе больших двоичных объектов Azure](data-factory-azure-blob-connector.md#copy-activity-properties). 

## <a name="azure-data-lake-store"></a>Хранилище озера данных Azure

### <a name="linked-service"></a>Связанные службы
toodefine службы связаны хранилища Озера данных Azure, установить тип hello hello связанная служба слишком**AzureDataLakeStore**и укажите следующие свойства в hello **typeProperties** раздела:  

| Свойство | Описание | Обязательно |
|:--- |:--- |:--- |
| type | свойство типа Hello должно быть присвоено: **AzureDataLakeStore** | Да |
| dataLakeStoreUri | Укажите сведения об учетной записи хранилища Озера данных Azure hello. Он находится в hello следующий формат: `https://[accountname].azuredatalakestore.net/webhdfs/v1` или `adl://[accountname].azuredatalakestore.net/`. | Да |
| subscriptionId | Принадлежит подписке Azure toowhich идентификатор хранилища Озера данных. | Необходимо для приемника |
| имя_группы_ресурсов | Принадлежит toowhich имя группы ресурсов Azure хранилища Озера данных. | Необходимо для приемника |
| servicePrincipalId | Укажите идентификатор клиента приложения hello. | Да (для проверки подлинности на основе субъекта-службы) |
| servicePrincipalKey | Укажите ключ приложения hello. | Да (для проверки подлинности на основе субъекта-службы) |
| tenant | Укажите информацию о клиенте hello (имя или клиента код домена), в которой расположено приложение. Его можно получить путем наведения указателя мыши hello в правом верхнем углу hello hello портал Azure. | Да (для проверки подлинности на основе субъекта-службы) |
| authorization | Нажмите кнопку **авторизовать** кнопку в hello **редактор фабрики данных** и введите учетные данные, назначает свойство toothis hello автоматически созданный авторизации URL-адреса. | Да (для проверки подлинности на основе учетных данных пользователя)|
| sessionid | Идентификатор сеанса OAuth из сеанса авторизации OAuth hello. Каждый идентификатор сеанса является уникальным и используется только один раз. Этот параметр создается автоматически при использовании редактора фабрики данных. | Да (для проверки подлинности на основе учетных данных пользователя) |

#### <a name="example-using-service-principal-authentication"></a>Пример: использование проверки подлинности на основе субъекта-службы
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info. Example: microsoft.onmicrosoft.com>"
        }
    }
}
```

#### <a name="example-using-user-credential-authentication"></a>Пример: использование проверки подлинности на основе учетных данных пользователя
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе Azure Data Lake Store](data-factory-azure-datalake-connector.md#linked-service-properties). 

### <a name="dataset"></a>Выборка
toodefine набор хранилища Озера данных Azure hello набор **тип** hello набора данных слишком**AzureDataLakeStore**и укажите следующие свойства в hello hello **typeProperties**раздела: 

| Свойство | Описание | Обязательно |
|:--- |:--- |:--- |
| folderPath |Хранить контейнер toohello путь к папке, в hello Озера данных Azure. |Да |
| fileName |Имя файла hello в хранилище Озера данных Azure hello. Свойство fileName является необязательным и в нем учитывается регистр знаков. <br/><br/>При указании имени файла, действие hello (включая копирования) работает на конкретный файл hello.<br/><br/>Если не указано имя файла, копия включает все файлы в folderPath hello для входного набора данных.<br/><br/>Если имя файла не указано для выходной набор данных, имя hello hello созданный файл будет в следующем формате hello: данные. <Guid>.txt (например:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Нет |
| partitionedBy |Необязательное свойство. Можно использовать его toospecify динамического folderPath и filename для временного ряда данных. Например, путь к папке (значение folderPath) каждый час может быть другим. |Нет |
| свойства | поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Набор hello **тип** свойства в формате tooone из следующих значений. Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Если требуется слишком**скопируйте файлы как-является** между файловых хранилищ (двоичный копия), пропустите раздел формат hello в оба определения набора входных и выходных данных. |Нет |
| compression | Укажите тип hello и уровень сжатия данных hello. Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**. Поддерживаемые уровни: **Optimal** и **Fastest**. См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Нет |

#### <a name="example"></a>Пример
```json
{
    "name": "AzureDataLakeStoreInput",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
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

Дополнительные сведения см. в статье о [соединителе Azure Data Lake Store](data-factory-azure-datalake-connector.md#dataset-properties). 

### <a name="azure-data-lake-store-source-in-copy-activity"></a>Источник Azure Data Lake Store в действии копирования
При копировании данных из хранилища Озера данных Azure, задайте hello **тип источника** из hello в действии копирования слишком**AzureDataLakeStoreSource**и укажите следующие свойства в hello **источника**  раздела:

**AzureDataLakeStoreSource** поддерживает следующие свойства hello **typeProperties** раздела:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| recursive |Указывает, доступна ли для чтения рекурсивно hello данных из подпапок hello или только из указанной папки hello. |True (значение по умолчанию), False |Нет |

#### <a name="example-azuredatalakestoresource"></a>Пример: AzureDataLakeStoreSource

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureDakeLaketoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureDataLakeStoreInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureDataLakeStoreSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Дополнительные сведения см. в статье о [соединителе Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties).

### <a name="azure-data-lake-store-sink-in-copy-activity"></a>Приемник Azure Data Lake Store в действии копирования
При копировании хранилища Озера данных Azure tooan данных задайте hello **тип приемника** из hello в действии копирования слишком**AzureDataLakeStoreSink**и укажите следующие свойства в hello **приемник**раздела:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| copyBehavior |Задает способ копирования hello. |<b>PreserveHierarchy</b>: сохраняет hello иерархию файлов в целевой папке hello. Hello относительный путь к исходной папке toosource файла представляет идентичные toohello относительный путь папки tootarget целевого файла.<br/><br/><b>FlattenHierarchy</b>: все файлы из исходной папки hello создаются в первый уровень hello целевую папку. Hello целевые файлы создаются с автоматически создаваемым именем.<br/><br/><b>MergeFiles</b>: объединяет все файлы из папки tooone hello исходного файла. Если указано имя файла или большого двоичного объекта hello hello объединенный файл будет hello указанным именем. в противном случае будет автоматически формируемого имени файла. |Нет |

#### <a name="example-azuredatalakestoresink"></a>Пример: AzureDataLakeStoreSink
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoDataLake",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureDataLakeStoreOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureDataLakeStoreSink"
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
        }]
    }
}
```

Дополнительные сведения см. в статье о [соединителе Azure Data Lake Store](data-factory-azure-datalake-connector.md#copy-activity-properties). 

## <a name="azure-cosmos-db"></a>Azure Cosmos DB  

### <a name="linked-service"></a>Связанные службы
toodefine Cosmos Azure DB связанной службы, набор hello **тип** hello связанной службы слишком**DocumentDb**и укажите следующие свойства в hello **typeProperties** раздел:  

| **Свойство** | **Описание** | **Обязательный** |
| --- | --- | --- |
| connectionString |Укажите сведения, необходимые tooconnect tooAzure Cosmos DB, базы данных. |Да |

#### <a name="example"></a>Пример

```json
{
    "name": "CosmosDBLinkedService",
    "properties": {
        "type": "DocumentDb",
        "typeProperties": {
            "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
        }
    }
}
```
Дополнительные сведения см. в статье о [соединителе Azure Cosmos DB](data-factory-azure-documentdb-connector.md#linked-service-properties).

### <a name="dataset"></a>Выборка
toodefine набору данных Azure Cosmos DB hello набор **тип** hello набора данных слишком**DocumentDbCollection**и укажите следующие свойства в hello hello **typeProperties** раздел: 

| **Свойство** | **Описание** | **Обязательный** |
| --- | --- | --- |
| collectionName |Имя коллекции Azure Cosmos DB hello. |Да |

#### <a name="example"></a>Пример

```json
{
    "name": "PersonCosmosDBTable",
    "properties": {
        "type": "DocumentDbCollection",
        "linkedServiceName": "CosmosDBLinkedService",
        "typeProperties": {
            "collectionName": "Person"
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```
Дополнительные сведения см. в статье о [соединителе Azure Cosmos DB](data-factory-azure-documentdb-connector.md#dataset-properties).

### <a name="azure-cosmos-db-collection-source-in-copy-activity"></a>Источник коллекции Azure Cosmos DB в действии копирования
При копировании данных из базы данных Cosmos Azure задайте hello **тип источника** из hello в действии копирования слишком**DocumentDbCollectionSource**и укажите следующие свойства в hello **источника** раздела:


| **Свойство** | **Описание** | **Допустимые значения** | **Обязательный** |
| --- | --- | --- | --- |
| query |Укажите данные tooread hello запроса. |Строка запроса, поддерживаемая Azure Cosmos DB. <br/><br/>Пример: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"` |Нет <br/><br/>Если не указан, hello выполняемой инструкции SQL:`select <columns defined in structure> from mycollection` |
| nestingSeparator |Вложенные tooindicate специальный символ, который hello документа |Любой символ. <br/><br/>Azure Cosmos DB — это хранилище NoSQL для JSON-документов, в которых разрешено использовать вложенные структуры. Фабрика данных Azure позволяет пользовательская иерархия toodenote через nestingSeparator, который является «.» в hello выше примерах. Разделитель hello hello действие копирования будет создавать объект «Name» hello с тремя дочерние элементы первой, средней и Last, соответствующим too"Name.First», «Name.Middle» и «Name.Last» в hello определение таблицы. |Нет |

#### <a name="example"></a>Пример

```json
{
    "name": "DocDbToBlobPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "DocumentDbCollectionSource",
                    "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
                    "nestingSeparator": "."
                },
                "sink": {
                    "type": "BlobSink",
                    "blobWriterAddHeader": true,
                    "writeBatchSize": 1000,
                    "writeBatchTimeout": "00:00:59"
                }
            },
            "inputs": [{
                "name": "PersonCosmosDBTable"
            }],
            "outputs": [{
                "name": "PersonBlobTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromCosmosDbToBlob"
        }],
        "start": "2016-04-01T00:00:00",
        "end": "2016-04-02T00:00:00"
    }
}
```

### <a name="azure-cosmos-db-collection-sink-in-copy-activity"></a>Приемник коллекции Azure Cosmos DB в действии копирования
При копировании данных tooAzure Cosmos DB задать hello **тип приемника** из hello в действии копирования слишком**DocumentDbCollectionSink**и укажите следующие свойства в hello **приемник**раздела:

| **Свойство** | **Описание** | **Допустимые значения** | **Обязательный** |
| --- | --- | --- | --- |
| nestingSeparator |Требуется специальный символ в tooindicate имя столбца источника hello вложенном документе. <br/><br/>Пример выше: `Name.First` в выходных данных hello таблицы выводятся hello следующая структура JSON в документе Cosmos DB hello:<br/><br/>"Name": {<br/>    "First": "John"<br/>}, |Символ, используемые tooseparate уровней вложения.<br/><br/>Значение по умолчанию — `.` (точка). |Символ, используемые tooseparate уровней вложения. <br/><br/>Значение по умолчанию — `.` (точка). |
| writeBatchSize |Число используемых параллельных запросов документов toocreate tooAzure Cosmos DB службы.<br/><br/>Можно оптимизировать производительность hello, при копировании данных из базы данных Azure Cosmos при помощи этого свойства. При увеличении writeBatchSize, так как несколько параллельных запросов tooAzure Cosmos DB отправляются можно ожидать более высокую производительность. Тем не менее необходимо tooavoid регулирования, может вызывать ошибки приветственное сообщение: «частота велик» запроса.<br/><br/>Регулирование может произойти по ряду причин, включая размер документов, количество терминов в документах, политику индексации целевой коллекции и т. д. Для операций копирования, можно использовать доступной пропускной способностью большинство лучше hello toohave коллекции (например, S3) (2 500 запрос единицы в секунду). |Целое число  |Нет (значение по умолчанию — 5) |
| writeBatchTimeout |Время ожидания для операции toocomplete hello до истечения времени ожидания. |Интервал времени<br/><br/> Пример: 00:30:00 (30 минут). |Нет |

#### <a name="example"></a>Пример

```json
{
    "name": "BlobToDocDbPipeline",
    "properties": {
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "DocumentDbCollectionSink",
                    "nestingSeparator": ".",
                    "writeBatchSize": 2,
                    "writeBatchTimeout": "00:00:00"
                },
                "translator": {
                    "type": "TabularTranslator",
                    "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix"
                }
            },
            "inputs": [{
                "name": "PersonBlobTableIn"
            }],
            "outputs": [{
                "name": "PersonCosmosDbTableOut"
            }],
            "policy": {
                "concurrency": 1
            },
            "name": "CopyFromBlobToCosmosDb"
        }],
        "start": "2016-04-14T00:00:00",
        "end": "2016-04-15T00:00:00"
    }
}
```

Дополнительные сведения см. в статье о [соединителе Azure Cosmos DB](data-factory-azure-documentdb-connector.md#copy-activity-properties).

## <a name="azure-sql-database"></a>База данных SQL Azure

### <a name="linked-service"></a>Связанные службы
toodefine базы данных SQL Azure связанной службы, набор hello **тип** hello связанной службы слишком**AzureSqlDatabase**и укажите следующие свойства в hello **typeProperties**раздела:  

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| connectionString |Укажите сведения, необходимые для свойства connectionString hello экземпляр базы данных SQL Azure toohello tooconnect. |Да |

#### <a name="example"></a>Пример
```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties). 

### <a name="dataset"></a>Выборка
toodefine набор данных базы данных SQL Azure, набор hello **тип** hello набора данных слишком**AzureSqlTable**и укажите следующие свойства в hello hello **typeProperties** раздел: 

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| tableName |Имя hello таблицы или представления в экземпляр базы данных SQL Azure hello, связанная служба ссылается. |Да |

#### <a name="example"></a>Пример

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
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
Дополнительные сведения см. в статье о [соединителе Azure SQL](data-factory-azure-sql-connector.md#dataset-properties). 

### <a name="sql-source-in-copy-activity"></a>Источник SQL в действии копирования
При копировании данных из базы данных SQL Azure, задайте hello **тип источника** из hello в действии копирования слишком**SqlSource**и укажите следующие свойства в hello **источника** раздел:


| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| SqlReaderQuery |Используйте данные tooread hello пользовательского запроса. |Строка запроса SQL. Пример: `select * from MyTable`. |Нет |
| sqlReaderStoredProcedureName |Имя hello хранимой процедуры, который считывает данные из таблицы источника hello. |Имя hello хранимой процедуры. |Нет |
| storedProcedureParameters |Параметры для hello хранимой процедуры. |Пары имен и значений. Имена и регистр параметров должны совпадать имена hello и учета регистра параметров hello хранимых процедур. |Нет |

#### <a name="example"></a>Пример

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
        }]
    }
}
```
Дополнительные сведения см. в статье о [соединителе Azure SQL](data-factory-azure-sql-connector.md#copy-activity-properties). 

### <a name="sql-sink-in-copy-activity"></a>Приемник SQL в действии копирования
При копировании данных tooAzure базы данных SQL, задайте hello **тип приемника** из hello в действии копирования слишком**SqlSink**и укажите следующие свойства в hello **приемник** раздела:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| writeBatchTimeout |Время ожидания для hello пакетной вставки операции toocomplete до истечения времени ожидания. |Интервал времени<br/><br/> Пример: 00:30:00 (30 минут). |Нет |
| writeBatchSize |Вставляет данные в таблицу SQL hello, при достижении writeBatchSize размера буфера hello. |Целое число (количество строк) |Нет (значение по умолчанию — 10 000). |
| sqlWriterCleanupScript |Укажите запрос для действия копирования tooexecute таким образом, чтобы очистить данные особый срез. |Инструкция запроса. |Нет |
| sliceIdentifierColumnName |Задать имя столбца для действия копирования toofill с автоматически созданный идентификатор фрагмента, — используется tooclean копирования данных особый срез время повторного выполнения. |Имя столбца с типом данных binary(32). |Нет |
| sqlWriterStoredProcedureName |Имя hello хранимой процедуры upserts (обновления или вставки) данные в целевой таблице hello. |Имя hello хранимой процедуры. |Нет |
| storedProcedureParameters |Параметры для hello хранимой процедуры. |Пары имен и значений. Имена и регистр параметров должны совпадать имена hello и учета регистра параметров hello хранимых процедур. |Нет |
| sqlWriterTableType |Укажите имя toobe тип таблицы, используемых в hello хранимой процедуре. Действие копирования предоставляет hello данных, перемещаемых во временной таблице с этой таблицей. Кода хранимой процедуры можно объединять hello данные копируются с существующими данными. |Имя типа таблицы. |Нет |

#### <a name="example"></a>Пример

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
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
        }]
    }
}
```

Дополнительные сведения см. в статье о [соединителе Azure SQL](data-factory-azure-sql-connector.md#copy-activity-properties). 

## <a name="azure-sql-data-warehouse"></a>Хранилище данных SQL Azure

### <a name="linked-service"></a>Связанные службы
Хранилище данных SQL Azure toodefine связанной службы, набор hello **тип** hello связанной службы слишком**AzureSqlDW**и укажите следующие свойства в hello **typeProperties**раздела:  

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| connectionString |Укажите сведения, необходимые для свойства connectionString hello tooconnect toohello хранилище данных SQL Azure экземпляра. |Да |



#### <a name="example"></a>Пример

```json
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

Дополнительные сведения см. в статье о [соединителе хранилища данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties). 

### <a name="dataset"></a>Выборка
toodefine набор данных хранилище данных SQL Azure, набор hello **тип** hello набора данных слишком**AzureSqlDWTable**и укажите следующие свойства в hello hello **typeProperties**раздела: 

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| tableName |Имя hello таблицы или представления в базе данных хранилища данных SQL Azure hello, hello связанной службы относится. |Да |

#### <a name="example"></a>Пример

```json
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

Дополнительные сведения см. в статье о [соединителе хранилища данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#dataset-properties). 

### <a name="sql-dw-source-in-copy-activity"></a>Источник хранилища данных SQL в действии копирования
При копировании данных из хранилища данных SQL Azure, задайте hello **тип источника** из hello в действии копирования слишком**SqlDWSource**и укажите следующие свойства в hello **источника**раздела:


| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| SqlReaderQuery |Используйте данные tooread hello пользовательского запроса. |Строка запроса SQL. Например, `select * from MyTable`. |Нет |
| sqlReaderStoredProcedureName |Имя hello хранимой процедуры, который считывает данные из таблицы источника hello. |Имя hello хранимой процедуры. |Нет |
| storedProcedureParameters |Параметры для hello хранимой процедуры. |Пары имен и значений. Имена и регистр параметров должны совпадать имена hello и учета регистра параметров hello хранимых процедур. |Нет |

#### <a name="example"></a>Пример

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLDWtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSqlDWInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
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
        }]
    }
}
```

Дополнительные сведения см. в статье о [соединителе хранилища данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties). 

### <a name="sql-dw-sink-in-copy-activity"></a>Приемник хранилища данных SQL в действии копирования
При копировании данных tooAzure хранилище данных SQL, задайте hello **тип приемника** из hello в действии копирования слишком**SqlDWSink**и укажите следующие свойства в hello **приемник** раздел:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| sqlWriterCleanupScript |Укажите запрос для действия копирования tooexecute таким образом, чтобы очистить данные особый срез. |Инструкция запроса. |Нет |
| allowPolyBase |Указывает, является ли toouse PolyBase (если применимо), а не BULKINSERT механизм. <br/><br/> **С помощью PolyBase — hello рекомендуется как tooload данные в хранилище данных SQL.** |Да <br/>False (по умолчанию) |Нет |
| polyBaseSettings |Группа свойств, которые могут быть указаны при hello **allowPolybase** задано слишком**true**. |&nbsp; |Нет |
| rejectValue |Указывает hello число или процент строк, может быть отклонено перед hello запрос завершается ошибкой. <br/><br/>Узнайте больше о hello PolyBase отклонить параметры в hello **аргументы** раздел [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) раздела. |0 (по умолчанию), 1, 2, ... |Нет |
| rejectType |Указывает, задан ли параметр rejectValue hello в значение литерала или в процентах. |Value (по умолчанию), Percentage |Нет |
| rejectSampleValue |Определяет количество hello tooretrieve строк перед hello PolyBase повторно вычисляет процент отклоненных строк hello. |1, 2, … |Да, если **rejectType** имеет значение **percentage**. |
| useTypeDefault |Указывает, как toohandle отсутствующих значений в разделенных текстовых файлов, если PolyBase получает данные из текстового файла hello.<br/><br/>Дополнительные сведения об этом свойстве из подраздела аргументы hello [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx). |True, False (по умолчанию) |Нет |
| writeBatchSize |Вставляет данные в таблицу SQL hello, при достижении writeBatchSize размера буфера hello |Целое число (количество строк) |Нет (значение по умолчанию — 10 000). |
| writeBatchTimeout |Время ожидания для hello пакетной вставки операции toocomplete до истечения времени ожидания. |Интервал времени<br/><br/> Пример: 00:30:00 (30 минут). |Нет |

#### <a name="example"></a>Пример

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQLDW",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureSqlDWOutput"
            }],
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
        }]
    }
}
```

Дополнительные сведения см. в статье о [соединителе хранилища данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#copy-activity-properties). 

## <a name="azure-search"></a>поиск Azure;

### <a name="linked-service"></a>Связанные службы
toodefine поиска Azure связанной службы, набор hello **тип** hello связанной службы слишком**AzureSearch**и укажите следующие свойства в hello **typeProperties** раздел:  

| Свойство | Описание | Обязательно |
| -------- | ----------- | -------- |
| url | URL-адрес для службы поиска Azure hello. | Да |
| key | Ключ администратора для hello службы поиска Azure. | Да |

#### <a name="example"></a>Пример

```json
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе Поиска Azure](data-factory-azure-search-connector.md#linked-service-properties).

### <a name="dataset"></a>Выборка
toodefine набор данных поиска Azure, набор hello **тип** hello набора данных слишком**AzureSearchIndex**и укажите следующие свойства в hello hello **typeProperties** раздела : 

| Свойство | Описание | Обязательно |
| -------- | ----------- | -------- |
| type | свойство типа Hello должно быть задано слишком**AzureSearchIndex**.| Да |
| indexName | Имя индекса поиска Azure hello. Фабрика данных hello индекс не создается. Hello индекс должен существовать в поиске Azure. | Да |

#### <a name="example"></a>Пример

```json
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties": {
            "indexName": "products"
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе Поиска Azure](data-factory-azure-search-connector.md#dataset-properties).

### <a name="azure-search-index-sink-in-copy-activity"></a>Приемник индекса Поиска Azure в действии копирования
При копировании данных индекс поиска Azure tooan задать hello **тип приемника** из hello в действии копирования слишком**AzureSearchIndexSink**и укажите следующие свойства в hello **приемник**раздела:

| Свойство | Описание | Допустимые значения | Обязательно |
| -------- | ----------- | -------------- | -------- |
| WriteBehavior | Указывает ли toomerge или замены, если документ уже существует в индексе hello. | Merge (по умолчанию)<br/>Отправить| Нет |
| WriteBatchSize | Передает данные в индекс поиска Azure hello достижении writeBatchSize hello размер буфера. | 1 too1 000. Значение по умолчанию — 1000. | Нет |

#### <a name="example"></a>Пример

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoAzureSearchIndex",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureSearchIndexDataset"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "AzureSearchIndexSink"
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
        }]
    }
}
```

Дополнительные сведения см. в статье о [соединителе Поиска Azure](data-factory-azure-search-connector.md#copy-activity-properties).

## <a name="azure-table-storage"></a>Хранилище таблиц Azure

### <a name="linked-service"></a>Связанные службы
Существует два типа связанных служб: связанная служба хранилища Azure и связанная служба SAS хранилища Azure.

#### <a name="azure-storage-linked-service"></a>Связанная служба хранилища Azure
toolink фабрики данных tooa учетной записи хранилища Azure с помощью hello **ключ учетной записи**, создания связанной службой хранилища Azure. Хранилище Azure toodefine связанной службы, набор hello **тип** hello связанной службы слишком**AzureStorage**. Затем можно указать следующие свойства в hello **typeProperties** раздела:  

| Свойство | Описание | Обязательно |
|:--- |:--- |:--- |
| type |свойство типа Hello должно быть присвоено: **AzureStorage** |Да |
| connectionString |Укажите сведения, необходимые для свойства connectionString hello tooconnect tooAzure хранилища. |Да |

**Пример**  

```json
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

#### <a name="azure-storage-sas-linked-service"></a>Связанная служба SAS хранилища Azure
Hello связаны SAS хранилища Azure службы позволяет toolink фабрикой данных Azure tooan учетной записи хранилища Azure с помощью подписи общего доступа (SAS). Он предоставляет hello фабрики данных ограничен или ограниченным временем доступа ресурсов, связанных с/tooall (/ контейнер больших двоичных объектов) в хранилище hello. toolink фабрики данных tooa учетной записи хранилища Azure с помощью подписи общего доступа, создания службы связаны SAS хранилища Azure. toodefine SAS хранилища Azure связанной службы, набор hello **тип** hello связанной службы слишком**AzureStorageSas**. Затем можно указать следующие свойства в hello **typeProperties** раздела:   

| Свойство | Описание | Обязательно |
|:--- |:--- |:--- |
| type |свойство типа Hello должно быть присвоено: **AzureStorageSas** |Да |
| sasUri |Укажите общий URI подписи доступа toohello хранилища Azure ресурсы, такие как BLOB-объекта, контейнера или таблицы. |Да |

**Пример**

```json
{  
    "name": "StorageSasLinkedService",  
    "properties": {  
        "type": "AzureStorageSas",  
        "typeProperties": {  
            "sasUri": "<storageUri>?<sasToken>"   
        }  
    }  
}  
```

Дополнительные сведения об этих связанных службах см. в статье о [соединителе Хранилища таблиц Azure](data-factory-azure-table-connector.md#linked-service-properties). 

### <a name="dataset"></a>Выборка
toodefine набор таблиц Azure hello набор **тип** hello набора данных слишком**AzureTable**и укажите следующие свойства в hello hello **typeProperties** раздела: 

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| tableName |Имя таблицы hello в экземпляре базы данных таблицы Azure hello, что связанная служба ссылается. |Да. При tableName указан без azureTableSourceQuery, все записи из таблицы hello не копируются toohello назначения. Если также указан azureTableSourceQuery записи из таблицы hello, удовлетворяющий hello запроса являются скопированный toohello назначения. |

#### <a name="example"></a>Пример

```json
{
    "name": "AzureTableInput",
    "properties": {
        "type": "AzureTable",
        "linkedServiceName": "StorageLinkedService",
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

Дополнительные сведения об этих связанных службах см. в статье о [соединителе Хранилища таблиц Azure](data-factory-azure-table-connector.md#dataset-properties). 

### <a name="azure-table-source-in-copy-activity"></a>Источник таблицы Azure в действии копирования
При копировании данных из табличного хранилища Azure, задайте hello **тип источника** из hello в действии копирования слишком**AzureTableSource**и укажите следующие свойства в hello **источника**раздела:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| AzureTableSourceQuery |Используйте данные tooread hello пользовательского запроса. |Строка запроса таблицы Azure. Примеры в следующем разделе hello. |Нет. При tableName указан без azureTableSourceQuery, все записи из таблицы hello не копируются toohello назначения. Если также указан azureTableSourceQuery записи из таблицы hello, удовлетворяющий hello запроса являются скопированный toohello назначения. |
| azureTableSourceIgnoreTableNotFound |Указывают ли проглотить исключение hello таблицы не существует. |TRUE<br/>FALSE |Нет |

#### <a name="example"></a>Пример

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureTabletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "AzureTableSource",
                    "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
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
        }]
    }
}
```

Дополнительные сведения об этих связанных службах см. в статье о [соединителе Хранилища таблиц Azure](data-factory-azure-table-connector.md#copy-activity-properties). 

### <a name="azure-table-sink-in-copy-activity"></a>Приемник таблицы Azure в действии копирования
При копировании данных tooAzure хранилище таблиц задать hello **тип приемника** из hello в действии копирования слишком**AzureTableSink**и укажите следующие свойства в hello **приемник** раздел:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| azureTableDefaultPartitionKeyValue |Значение по умолчанию раздел ключа, может использоваться приемником hello. |Строковое значение. |Нет |
| azureTablePartitionKeyName |Укажите имя столбца hello, значения которых используются в качестве ключей секционирования. Если не указано, в качестве ключа секции hello используется AzureTableDefaultPartitionKeyValue. |Имя столбца. |Нет |
| azureTableRowKeyName |Укажите имя столбца hello, значение которого используются в качестве ключа строки. Если имя не указано, используйте для каждой строки идентификатор GUID. |Имя столбца. |Нет |
| azureTableInsertType |режим Hello tooinsert данные в таблицу Azure.<br/><br/>Это свойство определяет, имеют ли существующие строки в выходной диапазон hello соответствующие ключи секций и строк значениями заменить или слияние. <br/><br/>toolearn о работе этих параметров (слияния и замены) в разделе [Вставка или слияние сущности](https://msdn.microsoft.com/library/azure/hh452241.aspx) и [Вставка или замена сущности](https://msdn.microsoft.com/library/azure/hh452242.aspx) разделы. <br/><br> Этот параметр применяется на уровне строк hello, не уровне hello таблицы и ни один из параметров удаляются строки в таблице вывода hello, которые не существуют во входном файле hello. |merge (по умолчанию)<br/>replace |Нет |
| writeBatchSize |Вставляет данные в таблицу Azure hello при hello writeBatchSize или writeBatchTimeout. |Целое число (количество строк) |Нет (значение по умолчанию — 10 000). |
| writeBatchTimeout |Вставляет данные в таблицу Azure hello при hello writeBatchSize или writeBatchTimeout |Интервал времени<br/><br/>Пример: 00:20:00 (20 минут). |Нет (время ожидания по умолчанию клиент toostorage по умолчанию значение составляет 90 сек) |

#### <a name="example"></a>Пример

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoTable",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "AzureTableOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "AzureTableSink",
                    "writeBatchSize": 100,
                    "writeBatchTimeout": "01:00:00"
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
        }]
    }
}
```
Дополнительные сведения об этих связанных службах см. в статье о [соединителе Хранилища таблиц Azure](data-factory-azure-table-connector.md#copy-activity-properties). 

## <a name="amazon-redshift"></a>Amazon Redshift

### <a name="linked-service"></a>Связанные службы
toodefine Amazon Redshift связанной службы, набор hello **тип** hello связанной службы слишком**AmazonRedshift**и укажите следующие свойства в hello **typeProperties**раздела:  

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| server |IP-адрес или имя сервера Amazon Redshift hello. |Да |
| порт |Hello номер порта TCP hello hello Amazon Redshift сервер использует toolisten для клиентских подключений. |Нет, значение по умолчанию — 5439. |
| database |Имя базы данных Amazon Redshift hello. |Да |
| Имя пользователя |Имя пользователя, имеющего доступ к базе данных toohello. |Да |
| пароль |Пароль для учетной записи пользователя hello. |Да |

#### <a name="example"></a>Пример

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties": {
        "type": "AmazonRedshift",
        "typeProperties": {
            "server": "<Amazon Redshift host name or IP address>",
            "port": 5439,
            "database": "<database name>",
            "username": "user",
            "password": "password"
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе Amazon Redshift](#data-factory-amazon-redshift-connector.md#linked-service-properties). 

### <a name="dataset"></a>Выборка
toodefine набору данных Amazon Redshift hello набор **тип** hello набора данных слишком**RelationalTable**и укажите следующие свойства в hello hello **typeProperties** раздел: 

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| tableName |Имя таблицы hello в базе данных Amazon Redshift hello, связанная служба ссылается. |Нет (если для свойства **RelationalSource** задано значение **query**). |


#### <a name="example"></a>Пример

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
Дополнительные сведения см. в статье о [соединителе Amazon Redshift](#data-factory-amazon-redshift-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Реляционный источник в действии копирования 
При копировании данных из Amazon Redshift задать hello **тип источника** из hello в действии копирования слишком**RelationalSource**и укажите следующие свойства в hello **источника** раздел:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| query |Используйте данные tooread hello пользовательского запроса. |Строка запроса SQL. Например, `select * from MyTable`. |Нет (если для свойства **tableName** задано значение **dataset**). |

#### <a name="example"></a>Пример

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
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
            "inputs": [{
                "name": "AmazonRedshiftInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonRedshiftToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
Дополнительные сведения см. в статье о [соединителе Amazon Redshift](#data-factory-amazon-redshift-connector.md#copy-activity-properties).

## <a name="ibm-db2"></a>IBM DB2

### <a name="linked-service"></a>Связанные службы
toodefine IBM DB2 связанной службы, набор hello **тип** hello связанной службы слишком**OnPremisesDB2**и укажите следующие свойства в hello **typeProperties** раздела:  

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| server |Имя сервера hello DB2. |Да |
| database |Имя базы данных hello DB2. |Да |
| schema |Имя схемы hello в базе данных hello. Имя схемы Hello учитывается регистр. |Нет |
| authenticationType |Тип проверки подлинности используется база данных DB2 toohello tooconnect. Возможными значениями являются: анонимная, обычная и Windows. |Да |
| Имя пользователя |При использовании обычной проверки подлинности или проверки подлинности Windows укажите имя пользователя. |Нет |
| пароль |Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя. |Нет |
| gatewayName |Имя шлюза hello, hello служба фабрики данных следует использовать toohello для tooconnect локальной базы данных DB2. |Да |

#### <a name="example"></a>Пример
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
Дополнительные сведения см. в статье о [соединителе IBM DB2](#data-factory-onprem-db2-connector.md#linked-service-properties).

### <a name="dataset"></a>Выборка
набор данных toodefine DB2, набор hello **тип** hello набора данных слишком**RelationalTable**и укажите следующие свойства в hello hello **typeProperties** раздела:

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| tableName |Имя таблицы hello в экземпляре базы данных DB2 hello, что связанная служба ссылается. Hello tableName учитывается регистр. |Нет (если для свойства **RelationalSource** задано значение **query**). 

#### <a name="example"></a>Пример
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

Дополнительные сведения см. в статье о [соединителе IBM DB2](#data-factory-onprem-db2-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Реляционный источник в действии копирования
При копировании данных из IBM DB2, задайте hello **тип источника** из hello в действии копирования слишком**RelationalSource**и укажите следующие свойства в hello **источника** раздела:


| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| query |Используйте данные tooread hello пользовательского запроса. |Строка запроса SQL. Например, `"query": "select * from "MySchema"."MyTable""`. |Нет (если для свойства **tableName** задано значение **dataset**). |

#### <a name="example"></a>Пример
```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
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
            "inputs": [{
                "name": "Db2DataSet"
            }],
            "outputs": [{
                "name": "AzureBlobDb2DataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "Db2ToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```
Дополнительные сведения см. в статье о [соединителе IBM DB2](#data-factory-onprem-db2-connector.md#copy-activity-properties).

## <a name="mysql"></a>MySQL

### <a name="linked-service"></a>Связанные службы
toodefine MySQL связанной службы, набор hello **тип** hello связанной службы слишком**OnPremisesMySql**и укажите следующие свойства в hello **typeProperties** раздела:  

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| server |Имя сервера MySQL hello. |Да |
| database |Имя базы данных MySQL hello. |Да |
| schema |Имя схемы hello в базе данных hello. |Нет |
| authenticationType |Тип проверки подлинности используется база данных MySQL toohello tooconnect. Возможные значения: `Basic`. |Да |
| Имя пользователя |Укажите базу данных MySQL toohello tooconnect имя пользователя. |Да |
| пароль |Укажите пароль для учетной записи пользователя hello указанное. |Да |
| gatewayName |Имя шлюза hello, hello служба фабрики данных следует использовать toohello для tooconnect локальной базы данных MySQL. |Да |

#### <a name="example"></a>Пример

```json
{
    "name": "OnPremMySqlLinkedService",
    "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
            "server": "<server name>",
            "database": "<database name>",
            "schema": "<schema name>",
            "authenticationType": "<authentication type>",
            "userName": "<user name>",
            "password": "<password>",
            "gatewayName": "<gateway>"
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе MySQL](data-factory-onprem-mysql-connector.md#linked-service-properties). 

### <a name="dataset"></a>Выборка
toodefine набора данных MySQL, набор hello **тип** hello набора данных слишком**RelationalTable**и укажите следующие свойства в hello hello **typeProperties** раздела: 

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| tableName |Имя таблицы hello в экземпляр базы данных MySQL, который ссылается связанная служба hello. |Нет (если для свойства **RelationalSource** задано значение **query**). |

#### <a name="example"></a>Пример

```json
{
    "name": "MySqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremMySqlLinkedService",
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
Дополнительные сведения см. в статье о [соединителе MySQL](data-factory-onprem-mysql-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Реляционный источник в действии копирования
При копировании данных из базы данных MySQL, задайте hello **тип источника** из hello в действии копирования слишком**RelationalSource**и укажите следующие свойства в hello **источника** раздел:


| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| query |Используйте данные tooread hello пользовательского запроса. |Строка запроса SQL. Например, `select * from MyTable`. |Нет (если для свойства **tableName** задано значение **dataset**). |


#### <a name="example"></a>Пример
```json
{
    "name": "CopyMySqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
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
            "inputs": [{
                "name": "MySqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobMySqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MySqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Дополнительные сведения см. в статье о [соединителе MySQL](data-factory-onprem-mysql-connector.md#copy-activity-properties). 

## <a name="oracle"></a>Oracle 

### <a name="linked-service"></a>Связанные службы
toodefine Oracle связанной службы, набор hello **тип** hello связанной службы слишком**OnPremisesOracle**и укажите следующие свойства в hello **typeProperties** раздел:  

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| driverType | Указать, какие данные toocopy драйвер toouse из / tooOracle базы данных. Допустимые значения: **Майкрософт** или **ODP** (по умолчанию). Дополнительные сведения о драйверах см. в разделе [Поддерживаемые версии и установка](#supported-versions-and-installation). | Нет |
| connectionString | Укажите сведения, необходимые для свойства connectionString hello экземпляр базы данных Oracle toohello tooconnect. | Да |
| gatewayName | Имя шлюза hello, что является toohello tooconnect используется локальный сервер Oracle |Да |

#### <a name="example"></a>Пример
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString": "Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе Oracle](data-factory-onprem-oracle-connector.md#linked-service-properties).

### <a name="dataset"></a>Выборка
toodefine набору данных Oracle hello набор **тип** hello набора данных слишком**OracleTable**и укажите следующие свойства в hello hello **typeProperties** раздела: 

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| tableName |Имя таблицы hello в hello базы данных Oracle, hello связанной службы относится. |Нет (если указан параметр **oracleReaderQuery** объекта **OracleSource**) |

#### <a name="example"></a>Пример

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2016-02-27T12:00:00",
            "frequency": "Hour"
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
Дополнительные сведения см. в статье о [соединителе Oracle](data-factory-onprem-oracle-connector.md#dataset-properties).

### <a name="oracle-source-in-copy-activity"></a>Источник Oracle в действии копирования
При копировании данных из базы данных Oracle, задайте hello **тип источника** из hello в действии копирования слишком**OracleSource**и укажите следующие свойства в hello **источника** раздел:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| oracleReaderQuery |Используйте данные tooread hello пользовательского запроса. |Строка запроса SQL. Например: `select * from MyTable` <br/><br/>Если не указан, hello выполняемой инструкции SQL:`select * from MyTable` |Нет (если для свойства **tableName** задано значение **dataset**). |

#### <a name="example"></a>Пример

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "OracletoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " OracleInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "OracleSource",
                    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
        }]
    }
}
```

Дополнительные сведения см. в статье о [соединителе Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).

### <a name="oracle-sink-in-copy-activity"></a>Приемник Oracle в действии копирования
При копировании базы данных Oracle tooam данных задайте hello **тип приемника** из hello в действии копирования слишком**OracleSink**и укажите следующие свойства в hello **приемник** раздела:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| writeBatchTimeout |Время ожидания для hello пакетной вставки операции toocomplete до истечения времени ожидания. |Интервал времени<br/><br/> Пример: 00:30:00 (30 минут). |Нет |
| writeBatchSize |Вставляет данные в таблицу SQL hello, при достижении writeBatchSize размера буфера hello. |Целое число (количество строк) |Нет (значение по умолчанию — 100) |
| sqlWriterCleanupScript |Укажите запрос для действия копирования tooexecute таким образом, чтобы очистить данные особый срез. |Инструкция запроса. |Нет |
| sliceIdentifierColumnName |Задать имя столбца для действия копирования toofill с автоматически созданный идентификатор фрагмента, — используется tooclean копирования данных особый срез время повторного выполнения. |Имя столбца с типом данных binary(32). |Нет |

#### <a name="example"></a>Пример
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-05T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoOracle",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": "OracleOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource"
                },
                "sink": {
                    "type": "OracleSink"
                }
            },
            "scheduler": {
                "frequency": "Day",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 0,
                "timeout": "01:00:00"
            }
        }]
    }
}
```
Дополнительные сведения см. в статье о [соединителе Oracle](data-factory-onprem-oracle-connector.md#copy-activity-properties).

## <a name="postgresql"></a>PostgreSQL

### <a name="linked-service"></a>Связанные службы
toodefine PostgreSQL связанной службы, набор hello **тип** hello связанной службы слишком**OnPremisesPostgreSql**и укажите следующие свойства в hello **typeProperties**раздела:  

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| server |Имя сервера PostgreSQL hello. |Да |
| database |Имя базы данных PostgreSQL hello. |Да |
| schema |Имя схемы hello в базе данных hello. Имя схемы Hello учитывается регистр. |Нет |
| authenticationType |Тип проверки подлинности используется база данных PostgreSQL toohello tooconnect. Возможными значениями являются: анонимная, обычная и Windows. |Да |
| Имя пользователя |При использовании обычной проверки подлинности или проверки подлинности Windows укажите имя пользователя. |Нет |
| пароль |Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя. |Нет |
| gatewayName |Имя шлюза hello, hello служба фабрики данных следует использовать toohello для tooconnect локальная база данных PostgreSQL. |Да |

#### <a name="example"></a>Пример

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
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
Дополнительные сведения см. в статье о [соединителе PostgreSQL](data-factory-onprem-postgresql-connector.md#linked-service-properties).

### <a name="dataset"></a>Выборка
toodefine набора данных PostgreSQL hello набор **тип** hello набора данных слишком**RelationalTable**и укажите следующие свойства в hello hello **typeProperties** раздела: 

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| tableName |Имя таблицы hello в экземпляр базы данных PostgreSQL, который ссылается связанная служба hello. Hello tableName учитывается регистр. |Нет (если для свойства **RelationalSource** задано значение **query**). |

#### <a name="example"></a>Пример
```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
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
Дополнительные сведения см. в статье о [соединителе PostgreSQL](data-factory-onprem-postgresql-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Реляционный источник в действии копирования
При копировании данных из базы данных PostgreSQL задать hello **тип источника** из hello в действии копирования слишком**RelationalSource**и укажите следующие свойства в hello **источника**раздела:


| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| query |Используйте данные tooread hello пользовательского запроса. |Строка запроса SQL. Например, "query": "select * from \"MySchema\".\"MyTable\"". |Нет (если для свойства **tableName** задано значение **dataset**). |

#### <a name="example"></a>Пример

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from \"public\".\"usstates\""
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "PostgreSqlDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobPostgreSqlDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "PostgreSqlToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Дополнительные сведения см. в статье о [соединителе PostgreSQL](data-factory-onprem-postgresql-connector.md#copy-activity-properties).

## <a name="sap-business-warehouse"></a>SAP Business Warehouse


### <a name="linked-service"></a>Связанные службы
toodefine хранилища SAP Business (BW) связанной службы, набор hello **тип** hello связанной службы слишком**SapBw**и укажите следующие свойства в hello **typeProperties**раздела:  

Свойство | Описание | Допустимые значения | Обязательно
-------- | ----------- | -------------- | --------
server | Имя сервера hello, на какие hello SAP BW расположен экземпляр. | string | Да
systemNumber | Номер системы hello системы SAP BW. | Двузначное десятичное число, представленное в виде строки. | Да
clientid | Идентификатор клиента для клиента hello в hello системы SAP-W. | Трехзначное десятичное число, представленное в виде строки. | Да
Имя пользователя | Имя пользователя hello с сервера SAP toohello доступа | string | Да
пароль | Пароль для пользователя hello. | string | Да
gatewayName | Имя шлюза hello, hello служба фабрики данных должна использовать tooconnect toohello локальной SAP BW экземпляр. | string | Да
encryptedCredential | Строка Hello шифрования учетных данных. | string | Нет

#### <a name="example"></a>Пример

```json
{
    "name": "SapBwLinkedService",
    "properties": {
        "type": "SapBw",
        "typeProperties": {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе SAP Business Warehouse ](data-factory-sap-business-warehouse-connector.md#linked-service-properties). 

### <a name="dataset"></a>Выборка
toodefine набора данных SAP BW hello набор **тип** hello набора данных слишком**RelationalTable**. Свойства определенного типа, не поддерживается для набора данных SAP BW hello типа **RelationalTable**.  

#### <a name="example"></a>Пример

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
Дополнительные сведения см. в статье о [соединителе SAP Business Warehouse ](data-factory-sap-business-warehouse-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Реляционный источник в действии копирования
При копировании данных из SAP Business Warehouse задать hello **тип источника** из hello в действии копирования слишком**RelationalSource**и укажите следующие свойства в hello **источника**раздела:


| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| query | Указывает tooread hello многомерных Выражений запроса данных из экземпляра SAP BW hello. | Запрос многомерных выражений. | Да |

#### <a name="example"></a>Пример

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<MDX query for SAP BW>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapBwDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapBwToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

Дополнительные сведения см. в статье о [соединителе SAP Business Warehouse ](data-factory-sap-business-warehouse-connector.md#copy-activity-properties). 

## <a name="sap-hana"></a>SAP HANA

### <a name="linked-service"></a>Связанные службы
SAP HANA toodefine связанной службы, набор hello **тип** hello связанной службы слишком**SapHana**и укажите следующие свойства в hello **typeProperties** раздела:  

Свойство | Описание | Допустимые значения | Обязательно
-------- | ----------- | -------------- | --------
server | Имя сервера hello, на какие hello SAP HANA расположен экземпляр. Если ваш сервер использует настроенный порт, укажите `server:port`. | строка | Да
authenticationType | Тип проверки подлинности. | string. Basic или Windows. | Да 
Имя пользователя | Имя пользователя hello с сервера SAP toohello доступа | string | Да
пароль | Пароль для пользователя hello. | string | Да
gatewayName | Имя шлюза hello, hello служба фабрики данных должна использовать tooconnect toohello локальной SAP HANA экземпляр. | string | Да
encryptedCredential | Строка Hello шифрования учетных данных. | string | Нет

#### <a name="example"></a>Пример

```json
{
    "name": "SapHanaLinkedService",
    "properties": {
        "type": "SapHana",
        "typeProperties": {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```
Дополнительные сведения см. в статье о [соединителе SAP HANA](data-factory-sap-hana-connector.md#linked-service-properties).
 
### <a name="dataset"></a>Выборка
toodefine набора данных SAP HANA hello набор **тип** hello набора данных слишком**RelationalTable**. Свойства конкретного типа, не поддерживается для набора данных SAP HANA hello типа **RelationalTable**. 

#### <a name="example"></a>Пример

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
Дополнительные сведения см. в статье о [соединителе SAP HANA](data-factory-sap-hana-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Реляционный источник в действии копирования
При копировании данных из хранилища данных SAP HANA задать hello **тип источника** из hello в действии копирования слишком**RelationalSource**и укажите следующие свойства в hello **источника**раздела:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| query | Указывает tooread hello SQL запроса данных из экземпляра SAP HANA hello. | SQL-запрос. | Да |


#### <a name="example"></a>Пример


```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "<SQL Query for HANA>"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "SapHanaDataset"
            }],
            "outputs": [{
                "name": "AzureBlobDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SapHanaToBlob"
        }],
        "start": "2017-03-01T18:00:00",
        "end": "2017-03-01T19:00:00"
    }
}
```

Дополнительные сведения см. в статье о [соединителе SAP HANA](data-factory-sap-hana-connector.md#copy-activity-properties).


## <a name="sql-server"></a>SQL Server

### <a name="linked-service"></a>Связанные службы
Создание связанной службы типа **OnPremisesSqlServer** toolink фабрикой данных базы данных tooa в локальной среде SQL Server. Привет, в следующей таблице приводится описание JSON элементов определенного tooon локальной связанной службы SQL Server.

Привет, в следующей таблице приводится описание tooSQL определенные элементы JSON службы связанного сервера.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| type |свойство типа Hello должно быть присвоено: **OnPremisesSqlServer**. |Да |
| connectionString |Укажите сведения connectionString, необходимые tooconnect toohello локальной SQL Server базы данных с помощью проверки подлинности Windows или проверка подлинности SQL. |Да |
| gatewayName |Имя шлюза hello, hello служба фабрики данных следует использовать toohello для tooconnect локальной базы данных SQL Server. |Да |
| Имя пользователя |При использовании проверки подлинности Windows укажите имя пользователя. Например, **domainname\\username**. |Нет |
| пароль |Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя. |Нет |

Вы можете зашифровать учетные данные с помощью hello **New AzureRmDataFactoryEncryptValue** командлета и использовать их в строке подключения hello, как показано в следующий пример hello (**EncryptedCredential** свойство):  

```json
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a>Пример: JSON для использования проверки подлинности SQL

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a>Пример: JSON для использования проверки подлинности Windows

Если указаны имя пользователя и пароль, шлюз использует их tooimpersonate hello базы данных SQL Server в локальной toohello в tooconnect учетную запись указанного пользователя. В противном случае шлюз подключается toohello SQL Server непосредственно с контекстом безопасности hello шлюза (его учетная запись для запуска).

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе SQL Server](data-factory-sqlserver-connector.md#linked-service-properties). 

### <a name="dataset"></a>Выборка
toodefine набора данных SQL Server, набор hello **тип** hello набора данных слишком**SqlServerTable**и укажите следующие свойства в hello hello **typeProperties** раздела: 

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| tableName |Имя hello таблицы или представления в экземпляр базы данных SQL Server hello, связанная служба ссылается. |Да |

#### <a name="example"></a>Пример
```json
{
    "name": "SqlServerInput",
    "properties": {
        "type": "SqlServerTable",
        "linkedServiceName": "SqlServerLinkedService",
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

Дополнительные сведения см. в статье о [соединителе SQL Server](data-factory-sqlserver-connector.md#dataset-properties). 

### <a name="sql-source-in-copy-activity"></a>Источник SQL в действии копирования
При копировании данных из базы данных SQL Server, задайте hello **тип источника** из hello в действии копирования слишком**SqlSource**и укажите следующие свойства в hello **источника** раздел:


| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| SqlReaderQuery |Используйте данные tooread hello пользовательского запроса. |Строка запроса SQL. Например, `select * from MyTable`. Может ссылаться на несколько таблиц из базы данных hello ссылается hello входного набора данных. Если не указан, hello выполняемой инструкции SQL: select from MyTable. |Нет |
| sqlReaderStoredProcedureName |Имя hello хранимой процедуры, который считывает данные из таблицы источника hello. |Имя hello хранимой процедуры. |Нет |
| storedProcedureParameters |Параметры для hello хранимой процедуры. |Пары имен и значений. Имена и регистр параметров должны совпадать имена hello и учета регистра параметров hello хранимых процедур. |Нет |

Если hello **sqlReaderQuery** указан для hello SqlSource, hello действие копирования выполняет этот запрос данных hello базы данных SQL Server источника tooget hello.

Кроме того, можно указать хранимую процедуру, указав hello **sqlReaderStoredProcedureName** и **storedProcedureParameters** (если hello хранимая процедура принимает параметры).

Если вы не укажете sqlReaderQuery или sqlReaderStoredProcedureName, hello столбцы, определенные в разделе структуры hello, используемые toobuild toorun запрос select для hello базы данных SQL Server. Если определение набора данных hello не имеют структуру hello, выбраны все столбцы из таблицы hello.

> [!NOTE]
> При использовании **sqlReaderStoredProcedureName**, по-прежнему требуется toospecify значение для hello **tableName** свойство в наборе данных hello JSON. Хотя какие-либо проверки этой таблицы отсутствуют.


#### <a name="example"></a>Пример
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "SqlServertoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": " SqlServerInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
        }]
    }
}
```

В этом примере **sqlReaderQuery** указан для hello SqlSource. Действие копирования Hello этот запрос запускает hello tooget hello базы данных SQL Server исходных данных. Кроме того, можно указать хранимую процедуру, указав hello **sqlReaderStoredProcedureName** и **storedProcedureParameters** (если hello хранимая процедура принимает параметры). Hello sqlReaderQuery ссылаться на несколько таблиц в базе данных hello ссылается hello входного набора данных. Это не таблица hello ограниченный tooonly, задайте как hello typeProperty tableName набора данных.

Если вы не укажете sqlReaderQuery или sqlReaderStoredProcedureName, hello столбцы, определенные в разделе структуры hello, используется toobuild toorun запрос select для hello базы данных SQL Server. Если определение набора данных hello не имеют структуру hello, выбраны все столбцы из таблицы hello.

Дополнительные сведения см. в статье о [соединителе SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties). 

### <a name="sql-sink-in-copy-activity"></a>Приемник SQL в действии копирования
При копировании базы данных SQL Server tooa данных задайте hello **тип приемника** из hello в действии копирования слишком**SqlSink**и укажите следующие свойства в hello **приемник** раздела:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| writeBatchTimeout |Время ожидания для hello пакетной вставки операции toocomplete до истечения времени ожидания. |Интервал времени<br/><br/> Пример: 00:30:00 (30 минут). |Нет |
| writeBatchSize |Вставляет данные в таблицу SQL hello, при достижении writeBatchSize размера буфера hello. |Целое число (количество строк) |Нет (значение по умолчанию — 10 000). |
| sqlWriterCleanupScript |Укажите запрос для действия копирования tooexecute, таким образом, чтобы очистить данные особый срез. Дополнительные сведения см. в разделе о [повторяемости](#repeatability-during-copy). |Инструкция запроса. |Нет |
| sliceIdentifierColumnName |Задать имя столбца для действия копирования toofill с автоматически созданный идентификатор фрагмента, — используется tooclean копирования данных особый срез время повторного выполнения. Дополнительные сведения см. в разделе о [повторяемости](#repeatability-during-copy). |Имя столбца с типом данных binary(32). |Нет |
| sqlWriterStoredProcedureName |Имя hello хранимой процедуры upserts (обновления или вставки) данные в целевой таблице hello. |Имя hello хранимой процедуры. |Нет |
| storedProcedureParameters |Параметры для hello хранимой процедуры. |Пары имен и значений. Имена и регистр параметров должны совпадать имена hello и учета регистра параметров hello хранимых процедур. |Нет |
| sqlWriterTableType |Укажите toobe имя типа таблицы, используемых в hello хранимой процедуре. Действие копирования предоставляет hello данных, перемещаемых во временной таблице с этой таблицей. Кода хранимой процедуры можно объединять hello данные копируются с существующими данными. |Имя типа таблицы. |Нет |

#### <a name="example"></a>Пример
конвейер Hello содержит операции копирования, настроенные toouse эти наборы входных и выходных данных. она запланированных toorun каждый час. В определении JSON конвейера hello, hello **источника** тип установлен слишком**BlobSource** и **приемник** тип установлен слишком**SqlSink**.

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "AzureBlobtoSQL",
            "description": "Copy Activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureBlobInput"
            }],
            "outputs": [{
                "name": " SqlServerOutput "
            }],
            "typeProperties": {
                "source": {
                    "type": "BlobSource",
                    "blobColumnSeparators": ","
                },
                "sink": {
                    "type": "SqlSink"
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
        }]
    }
}
```

Дополнительные сведения см. в статье о [соединителе SQL Server](data-factory-sqlserver-connector.md#copy-activity-properties). 

## <a name="sybase"></a>Sybase

### <a name="linked-service"></a>Связанные службы
toodefine Sybase связанной службы, набор hello **тип** hello связанной службы слишком**OnPremisesSybase**и укажите следующие свойства в hello **typeProperties** раздел:  

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| server |Имя сервера Sybase hello. |Да |
| database |Имя базы данных Sybase hello. |Да |
| schema |Имя схемы hello в базе данных hello. |Нет |
| authenticationType |Тип проверки подлинности используется база данных Sybase toohello tooconnect. Возможными значениями являются: анонимная, обычная и Windows. |Да |
| Имя пользователя |При использовании обычной проверки подлинности или проверки подлинности Windows укажите имя пользователя. |Нет |
| пароль |Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя. |Нет |
| gatewayName |Имя шлюза hello, hello служба фабрики данных следует использовать toohello для tooconnect локальной базы данных Sybase. |Да |

#### <a name="example"></a>Пример
```json
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
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

Дополнительные сведения см. в статье о [соединителе Sybase](data-factory-onprem-sybase-connector.md#linked-service-properties). 

### <a name="dataset"></a>Выборка
toodefine набора данных Sybase hello набор **тип** hello набора данных слишком**RelationalTable**и укажите следующие свойства в hello hello **typeProperties** раздела: 

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| tableName |Имя таблицы hello в экземпляр базы данных Sybase, который ссылается связанная служба hello. |Нет (если для свойства **RelationalSource** задано значение **query**). |

#### <a name="example"></a>Пример

```json
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
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

Дополнительные сведения см. в статье о [соединителе Sybase](data-factory-onprem-sybase-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Реляционный источник в действии копирования
При копировании данных из базы данных Sybase задать hello **тип источника** из hello в действии копирования слишком**RelationalSource**и укажите следующие свойства в hello **источника** раздел:


| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| query |Используйте данные tooread hello пользовательского запроса. |Строка запроса SQL. Например, `select * from MyTable`. |Нет (если для свойства **tableName** задано значение **dataset**). |

#### <a name="example"></a>Пример

```json
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "select * from DBA.Orders"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "inputs": [{
                "name": "SybaseDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobSybaseDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "SybaseToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Дополнительные сведения см. в статье о [соединителе Sybase](data-factory-onprem-sybase-connector.md#copy-activity-properties).

## <a name="teradata"></a>Teradata

### <a name="linked-service"></a>Связанные службы
toodefine Teradata связанной службы, набор hello **тип** hello связанной службы слишком**OnPremisesTeradata**и укажите следующие свойства в hello **typeProperties** раздел:  

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| server |Имя сервера Teradata hello. |Да |
| authenticationType |Тип проверки подлинности используется база данных Teradata toohello tooconnect. Возможными значениями являются: анонимная, обычная и Windows. |Да |
| Имя пользователя |При использовании обычной проверки подлинности или проверки подлинности Windows укажите имя пользователя. |Нет |
| пароль |Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя. |Нет |
| gatewayName |Имя шлюза hello, hello служба фабрики данных следует использовать базы данных Teradata tooconnect toohello в локальной среде. |Да |

#### <a name="example"></a>Пример
```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе Teradata](data-factory-onprem-teradata-connector.md#linked-service-properties).

### <a name="dataset"></a>Выборка
toodefine набора больших двоичных объектов Teradata hello набор **тип** hello набора данных слишком**RelationalTable**. В настоящее время нет свойств типа поддерживается для набора данных Teradata hello. 

#### <a name="example"></a>Пример
```json
{
    "name": "TeradataDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
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

Дополнительные сведения см. в статье о [соединителе Teradata](data-factory-onprem-teradata-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Реляционный источник в действии копирования
При копировании данных из базы данных Teradata задать hello **тип источника** из hello в действии копирования слишком**RelationalSource**и укажите следующие свойства в hello **источника**раздела:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| query |Используйте данные tooread hello пользовательского запроса. |Строка запроса SQL. Например, `select * from MyTable`. |Да |

#### <a name="example"></a>Пример

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "TeradataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobTeradataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "TeradataToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "isPaused": false
    }
}
```

Дополнительные сведения см. в статье о [соединителе Teradata](data-factory-onprem-teradata-connector.md#copy-activity-properties).

## <a name="cassandra"></a>Cassandra


### <a name="linked-service"></a>Связанные службы
toodefine Cassandra связанной службы, набор hello **тип** hello связанной службы слишком**OnPremisesCassandra**и укажите следующие свойства в hello **typeProperties** раздел:  

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| host |Один или несколько IP-адресов или имен узлов серверов Cassandra.<br/><br/>Укажите список разделенных запятой IP-адреса или имена серверов tooall tooconnect одновременно. |Да |
| порт |TCP-порт, который hello Cassandra server Hello использует toolisten для клиентских подключений. |Нет. Значение по умолчанию — 9042 |
| authenticationType |Укажите тип Basic или Anonymous |Да |
| Имя пользователя |Укажите имя пользователя для учетной записи пользователя hello. |Да, если tooBasic authenticationType. |
| пароль |Укажите пароль для учетной записи пользователя hello. |Да, если tooBasic authenticationType. |
| gatewayName |имя шлюза hello, используемые tooconnect toohello Hello локальной Cassandra базы данных. |Да |
| encryptedCredential |Учетные данные, зашифрованные шлюзом hello. |Нет |

#### <a name="example"></a>Пример

```json
{
    "name": "CassandraLinkedService",
    "properties": {
        "type": "OnPremisesCassandra",
        "typeProperties": {
            "authenticationType": "Basic",
            "host": "<cassandra server name or IP address>",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе Cassandra](data-factory-onprem-cassandra-connector.md#linked-service-properties). 

### <a name="dataset"></a>Выборка
toodefine набора Cassandra hello набор **тип** hello набора данных слишком**CassandraTable**и укажите следующие свойства в hello hello **typeProperties** раздела: 

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| keyspace |Имя hello пространство ключей или схемы в базе данных Cassandra. |Да (если для **CassandraSource** не определено значение **query**). |
| tableName |Имя таблицы hello Cassandra базы данных. |Да (если для **CassandraSource** не определено значение **query**). |

#### <a name="example"></a>Пример

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "<key space>"
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

Дополнительные сведения см. в статье о [соединителе Cassandra](data-factory-onprem-cassandra-connector.md#dataset-properties). 

### <a name="cassandra-source-in-copy-activity"></a>Источник Cassandra в действии копирования
При копировании данных из Cassandra задать hello **тип источника** из hello в действии копирования слишком**CassandraSource**и укажите следующие свойства в hello **источника** раздела :

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| query |Используйте данные tooread hello пользовательского запроса. |Запрос SQL-92 или CQL. Ознакомьтесь со [справочником по CQL](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html). <br/><br/>При использовании SQL-запрос, укажите **keyspace name.table имя** toorepresent hello таблицу tooquery. |Нет (если в наборе данных определены свойства tableName и keyspace) |
| consistencyLevel |уровень согласованности Hello указывает, сколько реплик должен вернуть запрос чтения tooa до возвращения данных toohello клиентское приложение. Проверяет Cassandra hello указанное число реплик, для запроса на чтение данных toosatisfy hello. |ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE. Дополнительные сведения см. в статье [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) (Настройка согласованности данных). |Нет. Значение по умолчанию — ONE |

#### <a name="example"></a>Пример
  
```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "CassandraInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
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
        }]
    }
}
```

Дополнительные сведения см. в статье о [соединителе Cassandra](data-factory-onprem-cassandra-connector.md#copy-activity-properties).

## <a name="mongodb"></a>MongoDB

### <a name="linked-service"></a>Связанные службы
toodefine MongoDB связанной службы, набор hello **тип** hello связанной службы слишком**OnPremisesMongoDB**и укажите следующие свойства в hello **typeProperties** раздел:  

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| server |IP-адрес или имя сервера hello MongoDB. |Да |
| порт |TCP-порт, который hello MongoDB server использует toolisten для клиентских подключений. |Значение по умолчанию — 27017 (необязательно) |
| authenticationType |Укажите тип Basic или Anonymous |Да |
| Имя пользователя |Учетная запись пользователя, tooaccess MongoDB. |Да (если используется обычная проверка подлинности) |
| пароль |Пароль для пользователя hello. |Да (если используется обычная проверка подлинности) |
| authSource |Имя базы данных MongoDB hello, что требуется toouse toocheck учетные данные для проверки подлинности. |Необязательно (если используется обычная проверка подлинности). по умолчанию: используется учетная запись администратора hello и hello базы данных, указанный с помощью свойства databaseName. |
| databaseName |Имя базы данных MongoDB hello, которое следует tooaccess. |Да |
| gatewayName |Имя шлюза hello, который обращается к хранилищу данных hello. |Да |
| encryptedCredential |Учетные данные, зашифрованные шлюзом |Необязательно |

#### <a name="example"></a>Пример

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties": {
        "type": "OnPremisesMongoDb",
        "typeProperties": {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
            "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе MongoDB](data-factory-on-premises-mongodb-connector.md#linked-service-properties).

### <a name="dataset"></a>Выборка
toodefine набора данных MongoDB hello набор **тип** hello набора данных слишком**MongoDbCollection**и укажите следующие свойства в hello hello **typeProperties** раздела: 

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| collectionName |Имя коллекции hello базы данных MongoDB. |Да |

#### <a name="example"></a>Пример

```json
{
    "name": "MongoDbInputDataset",
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

Дополнительные сведения см. в статье о [соединителе MongoDB](data-factory-on-premises-mongodb-connector.md#dataset-properties).

#### <a name="mongodb-source-in-copy-activity"></a>Источник MongoDB в действии копирования
При копировании данных из MongoDB задать hello **тип источника** из hello в действии копирования слишком**MongoDbSource**и укажите следующие свойства в hello **источника** раздела:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| query |Используйте данные tooread hello пользовательского запроса. |Строка запроса SQL-92. Например, `select * from MyTable`. |Нет (если для свойства **collectionName** задано значение **dataset**). |

#### <a name="example"></a>Пример

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "MongoDbSource",
                    "query": "select * from MyTable"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "MongoDbInputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "MongoDBToAzureBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Дополнительные сведения см. в статье о [соединителе MongoDB](data-factory-on-premises-mongodb-connector.md#copy-activity-properties).

## <a name="amazon-s3"></a>Amazon S3


### <a name="linked-service"></a>Связанные службы
toodefine S3 Amazon связанной службы, набор hello **тип** hello связанной службы слишком**AwsAccessKey**и укажите следующие свойства в hello **typeProperties** раздела :  

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| accessKeyID |Идентификатор hello доступа секретного ключа. |string |Да |
| secretAccessKey |Hello секретный доступа самого ключа. |Зашифрованная строка секрета |Да |

#### <a name="example"></a>Пример
```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе Amazon S3](data-factory-amazon-simple-storage-service-connector.md#linked-service-properties).

### <a name="dataset"></a>Выборка
набор данных toodefine S3 Amazon, набор hello **тип** hello набора данных слишком**AmazonS3**и укажите следующие свойства в hello hello **typeProperties** раздела: 

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| bucketName |Имя сегмента Hello S3. |Строка |Да |
| key |ключ объекта Hello S3. |Строка |Нет |
| prefix |Префикс для ключа объекта S3 hello. Выбираются объекты, ключи которых начинаются с этого префикса. Применяется, только если ключ пустой. |string |Нет |
| версия |версия Hello объекта S3, если включено управление версиями S3. |Строка |Нет |
| свойства | поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Набор hello **тип** свойства в формате tooone из следующих значений. Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Если требуется слишком**скопируйте файлы как-является** между файловых хранилищ (двоичный копия), пропустите раздел формат hello в оба определения набора входных и выходных данных. |Нет | |
| compression | Укажите тип hello и уровень сжатия данных hello. Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**. уровни Hello поддерживается: **оптимальный** и **Fastest**. См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Нет | |


> [!NOTE]
> bucketName + клавиша указывает расположение hello объекта hello S3 где контейнеров — hello корневой контейнер для объектов S3 и нажата клавиша объекта tooS3 hello полный путь.

#### <a name="example-sample-dataset-with-prefix"></a>Пример: пример набора данных с префиксом

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "<S3 bucket name>",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
#### <a name="example-sample-data-set-with-version"></a>Пример: пример набора данных (с версией)

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "<S3 bucket name>",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

#### <a name="example-dynamic-paths-for-s3"></a>Пример: динамические пути для S3
В образце hello мы используем фиксированные значения для свойств ключа и bucketName в наборе данных hello Amazon S3.

```json
"key": "testFolder/test.orc",
"bucketName": "<S3 bucket name>",
```

Может иметь вычисления ключа hello и bucketName динамически во время выполнения с помощью системных переменных, например SliceStart фабрики данных.

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

Можно сделать hello же hello префикс свойства набора данных Amazon S3. В статье [Фабрика данных Azure — функции и системные переменные](data-factory-functions-variables.md) приведен список поддерживаемых функций и переменных.

Дополнительные сведения см. в статье о [соединителе Amazon S3](data-factory-amazon-simple-storage-service-connector.md#dataset-properties).

### <a name="file-system-source-in-copy-activity"></a>Источник файловой системы в действии копирования
При копировании данных из Amazon S3 задать hello **тип источника** из hello в действии копирования слишком**FileSystemSource**и укажите следующие свойства в hello **источника** раздела :


| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| recursive |Указывает объекты ли список toorecursively S3 hello в каталоге. |True или false |Нет |


#### <a name="example"></a>Пример


```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource",
                    "recursive": true
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "AmazonS3InputDataset"
            }],
            "outputs": [{
                "name": "AzureBlobOutputDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "AmazonS3ToBlob"
        }],
        "start": "2016-08-08T18:00:00",
        "end": "2016-08-08T19:00:00"
    }
}
```

Дополнительные сведения см. в статье о [соединителе Amazon S3](data-factory-amazon-simple-storage-service-connector.md#copy-activity-properties).

## <a name="file-system"></a>Файловая система


### <a name="linked-service"></a>Связанные службы
Можно связать локального файла tooan данных Azure заводе hello **файловый сервер в локальной** связанной службы. Привет, в следующей таблице приводится описание JSON элементы, которые являются определенной toohello файловый сервер в локальной связанной службы.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| type |Убедитесь, что свойство типа hello слишком**OnPremisesFileServer**. |Да |
| host |Указывает путь к корневому каталогу hello hello папке, что toocopy. Использовать hello escape-символ "\" для специальных символов в строке приветствия. Примеры приведены в разделе [Примеры определений связанной службы и набора данных](#sample-linked-service-and-dataset-definitions). |Да |
| userid |Укажите идентификатор hello hello пользователя, имеющего доступ toohello сервера. |Нет (если выбрать encryptedcredential) |
| пароль |Задать пароль hello hello пользователя (userid). |Нет (если выбрать encryptedcredential) |
| encryptedCredential |Укажите hello зашифрованные учетные данные, которые можно получить, выполнив командлет New-AzureRmDataFactoryEncryptValue hello. |Нет (Если вы выберете toospecify идентификатор пользователя и пароль в виде обычного текста) |
| gatewayName |Указывает имя фабрики данных для использования локального файла tooconnect toohello сервера шлюза hello hello. |Да |

#### <a name="sample-folder-path-definitions"></a>Пример определений пути к папке 
| Сценарий | Размещение в определении связанной службы | Путь к файлу в определении набора данных |
| --- | --- | --- |
| Локальная папка на компьютере со шлюзом управления данными. <br/><br/>Примеры: "D:\\\\*" или "D:\папка\вложенная_папка\\\*" |"D:\\\\" (для шлюза управления данными 2.0 и более поздних версий) <br/><br/> localhost (для версий, предшествующих версии 2.0 шлюза управления данными) |.\\\\ или "папка\\\\вложенная_папка" (для шлюза управления данными 2.0 и более поздних версий) <br/><br/>"D:\\\\" или "D:\\\\папка\\\\вложенная_папка" (для шлюза версии ниже 2.0) |
| Удаленная общая папка: <br/><br/>Примеры: "\\\\сервер\\общая_папка\\\*" или "\\\\сервер\\общая_папка\\папка\\вложенная_папка\\*" |\\\\\\\\сервер\\\\общая_папка |.\\\\ или "папка\\\\вложенная_папка" |


#### <a name="example-using-username-and-password-in-plain-text"></a>Пример указания имени пользователя и пароля в виде обычного текста

```json
{
    "Name": "OnPremisesFileServerLinkedService",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "\\\\Contosogame-Asia",
            "userid": "Admin",
            "password": "123456",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-encryptedcredential"></a>Пример использования encryptedcredential

```json
{
    "Name": " OnPremisesFileServerLinkedService ",
    "properties": {
        "type": "OnPremisesFileServer",
        "typeProperties": {
            "host": "D:\\",
            "encryptedCredential": "WFuIGlzIGRpc3Rpbmd1aXNoZWQsIG5vdCBvbmx5IGJ5xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе файловой системы](data-factory-onprem-file-system-connector.md#linked-service-properties).

### <a name="dataset"></a>Выборка
toodefine набора данных файловой системы, набор hello **тип** hello набора данных слишком**общей папкой**и укажите следующие свойства в hello hello **typeProperties** раздела: 

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| folderPath |Указывает папку toohello вложенным hello. Использовать hello escape-символ "\" для специальных символов в строке приветствия. Примеры приведены в разделе [Примеры определений связанной службы и набора данных](#sample-linked-service-and-dataset-definitions).<br/><br/>Можно объединять с помощью этого свойства **partitionBy** toohave пути к папке зависимости среза дат начала и окончания. |Да |
| fileName |Укажите имя файла hello hello в hello **folderPath** Если hello таблицы toorefer tooa конкретный файл в папку hello. Если не указано значение для этого свойства, таблица hello указывает tooall файлы в папке hello.<br/><br/>Если имя файла не указано для выходной набор данных, hello hello созданный файл называется в кодировке hello: <br/><br/>`Data.<Guid>.txt` (пример: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Нет |
| fileFilter |Укажите toobe фильтра используется tooselect подмножества файлов в hello folderPath, а не всех файлов. <br/><br/>Допустимые значения: `*` (несколько знаков) и `?` (один знак).<br/><br/>Пример 1: "fileFilter": "*.log"<br/>Пример 2: fileFilter: 2016-1-?.txt<br/><br/>Обратите внимание, что свойство fileFilter применяется к входному набору данных FileShare. |Нет |
| partitionedBy |PartitionedBy toospecify динамический folderPath и fileName можно использовать для временного ряда данных. Например, можно параметризовать значение folderPath для каждого часа получения данных. |Нет |
| свойства | поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Набор hello **тип** свойства в формате tooone из следующих значений. Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Если требуется слишком**скопируйте файлы как-является** между файловых хранилищ (двоичный копия), пропустите раздел формат hello в оба определения набора входных и выходных данных. |Нет |
| compression | Укажите тип hello и уровень сжатия данных hello. Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**. Поддерживаемые уровни: **Optimal** и **Fastest**. См. сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Нет |

> [!NOTE]
> Свойства filename и fileFilter невозможно использовать одновременно.

#### <a name="example"></a>Пример

```json
{
    "name": "OnpremisesFileSystemInput",
    "properties": {
        "type": " FileShare",
        "linkedServiceName": " OnPremisesFileServerLinkedService ",
        "typeProperties": {
            "folderPath": "mysharedfolder/yearno={Year}/monthno={Month}/dayno={Day}",
            "fileName": "{Hour}.csv",
            "partitionedBy": [{
                "name": "Year",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                        "format": "yyyy"
                }
            }, {
                "name": "Month",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "MM"
                }
            }, {
                "name": "Day",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "dd"
                }
            }, {
                "name": "Hour",
                "value": {
                    "type": "DateTime",
                    "date": "SliceStart",
                    "format": "HH"
                }
            }]
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

Дополнительные сведения см. в статье о [соединителе файловой системы](data-factory-onprem-file-system-connector.md#dataset-properties).

### <a name="file-system-source-in-copy-activity"></a>Источник файловой системы в действии копирования
При копировании данных из файловой системы, задайте hello **тип источника** из hello в действии копирования слишком**FileSystemSource**и укажите следующие свойства в hello **источника** раздел:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| recursive |Указывает, доступна ли для чтения рекурсивно hello данные из вложенных папок hello или только пользователей из указанной папки hello. |True, False (по умолчанию) |Нет |

#### <a name="example"></a>Пример

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T19:00:00",
        "description": "Pipeline for copy activity",
        "activities": [{
            "name": "OnpremisesFileSystemtoBlob",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "OnpremisesFileSystemInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
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
        }]
    }
}
```
Дополнительные сведения см. в статье о [соединителе файловой системы](data-factory-onprem-file-system-connector.md#copy-activity-properties).

### <a name="file-system-sink-in-copy-activity"></a>Приемник файловой системы в действии копирования
При копировании данных tooFile системы задать hello **тип приемника** из hello в действии копирования слишком**FileSystemSink**и укажите следующие свойства в hello **приемник** раздела:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| copyBehavior |Определяет поведение копирования hello, когда источник hello BlobSource или файловой системы. |**PreserveHierarchy:** сохраняет hello иерархию файлов в целевой папке hello. То есть относительный путь hello hello исходный файл toohello исходную папку hello такой же, как относительный путь hello hello целевой файл toohello целевую папку.<br/><br/>**FlattenHierarchy:** все файлы из исходной папки hello создаются в первый уровень hello целевую папку. Hello целевые файлы создаются с автоматически созданным именем.<br/><br/>**MergeFiles:** объединяет все файлы из папки tooone hello исходного файла. Если указано имя BLOB-объекта или имени файла hello hello объединенный файл называется hello указанным именем. В противном случае присваивается автоматически созданное имя файла. |Нет |
auto-

#### <a name="example"></a>Пример

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2015-06-01T18:00:00",
        "end": "2015-06-01T20:00:00",
        "description": "pipeline for copy activity",
        "activities": [{
            "name": "AzureSQLtoOnPremisesFile",
            "description": "copy activity",
            "type": "Copy",
            "inputs": [{
                "name": "AzureSQLInput"
            }],
            "outputs": [{
                "name": "OnpremisesFileSystemOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "SqlSource",
                    "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd}\\'', WindowStart, WindowEnd)"
                },
                "sink": {
                    "type": "FileSystemSink"
                }
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "OldestFirst",
                "retry": 3,
                "timeout": "01:00:00"
            }
        }]
    }
}
```

Дополнительные сведения см. в статье о [соединителе файловой системы](data-factory-onprem-file-system-connector.md#copy-activity-properties).

## <a name="ftp"></a>FTP

### <a name="linked-service"></a>Связанные службы
toodefine FTP связанной службы, набор hello **тип** hello связанной службы слишком**FTP-сервер**и укажите следующие свойства в hello **typeProperties** раздела:  

| Свойство | Описание | Обязательно | значение по умолчанию |
| --- | --- | --- | --- |
| host |Имя или IP-адрес FTP-сервера hello |Да |&nbsp; |
| authenticationType |Укажите тип аутентификации |Да |Обычная, анонимная |
| Имя пользователя |Пользователь, имеющий доступ toohello FTP сервера |Нет |&nbsp; |
| пароль |Пароль для пользователя hello (имя пользователя) |Нет |&nbsp; |
| encryptedCredential |Зашифрованных учетных данных tooaccess hello FTP-сервера |Нет |&nbsp; |
| gatewayName |Имя шлюза tooconnect hello шлюз управления данными tooan локальной FTP-сервера |Нет |&nbsp; |
| порт |Какие hello FTP сервера прослушивает порт |Нет |21 |
| enableSsl |Укажите, является ли toouse FTP через канал SSL/TLS |Нет |Да |
| enableServerCertificateValidation |Укажите, является ли сервер tooenable SSL проверку сертификата при использовании FTP по каналу SSL/TLS |Нет |Да |

#### <a name="example-using-anonymous-authentication"></a>Пример: использование анонимной проверки подлинности

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
            "typeProperties": {
            "authenticationType": "Anonymous",
            "host": "myftpserver.com"
        }
    }
}
```

#### <a name="example-using-username-and-password-in-plain-text-for-basic-authentication"></a>Пример: использование имени пользователя и пароля в виде обычного текста для обычной проверки подлинности

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "username": "Admin",
            "password": "123456"
        }
    }
}
```

#### <a name="example-using-port-enablessl-enableservercertificatevalidation"></a>Пример: использование свойств port, enableSsl, enableServerCertificateValidation

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",    
            "username": "Admin",
            "password": "123456",
            "port": "21",
            "enableSsl": true,
            "enableServerCertificateValidation": true
        }
    }
}
```

#### <a name="example-using-encryptedcredential-for-authentication-and-gateway"></a>Пример: использование свойства encryptedCredential для проверки подлинности и шлюза

```json
{
    "name": "FTPLinkedService",
    "properties": {
        "type": "FtpServer",
        "typeProperties": {
            "host": "myftpserver.com",
            "authenticationType": "Basic",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "gatewayName": "<onpremgateway>"
        }
      }
}
```

Дополнительные сведения см. в статье о [соединителе FTP](data-factory-ftp-connector.md#linked-service-properties).

### <a name="dataset"></a>Выборка
toodefine FTP набора данных, набор hello **тип** hello набора данных слишком**FileShare**и укажите следующие свойства в hello hello **typeProperties** раздел: 

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| folderPath |Путь toohello вложенной папкой. Использовать escape-символ "\" для специальных символов в строке приветствия. Примеры приведены в разделе [Примеры определений связанной службы и набора данных](#sample-linked-service-and-dataset-definitions).<br/><br/>Можно объединять с помощью этого свойства **partitionBy** toohave пути к папке зависимости среза дат начала и окончания. |Да 
| fileName |Укажите имя файла hello hello в hello **folderPath** Если hello таблицы toorefer tooa конкретный файл в папку hello. Если не указано значение для этого свойства, таблица hello указывает tooall файлы в папке hello.<br/><br/>Если имя файла не указано для выходной набор данных, имя hello hello созданный файл может быть в hello в следующем формате: <br/><br/>Data.<Guid>.txt (например, Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Нет |
| fileFilter |Укажите toobe фильтра используется tooselect подмножества файлов в hello folderPath, а не всех файлов.<br/><br/>Допустимые значения: `*` (несколько знаков) и `?` (один знак).<br/><br/>Пример 1: `"fileFilter": "*.log"`<br/>Пример 2: `"fileFilter": 2016-1-?.txt"`<br/><br/> Свойство fileFilter применяется к входному набору данных FileShare. HDFS не поддерживает это свойство. |Нет |
| partitionedBy |partitionedBy можно использовать toospecify динамического folderPath, имя файла для временного ряда данных. Например, путь к папке folderPath каждый час будет другим. |Нет |
| свойства | поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Набор hello **тип** свойства в формате tooone из следующих значений. Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Если требуется слишком**скопируйте файлы как-является** между файловых хранилищ (двоичный копия), пропустите раздел формат hello в оба определения набора входных и выходных данных. |Нет |
| compression | Укажите тип hello и уровень сжатия данных hello. Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**. Поддерживаемые уровни: **Optimal** и **Fastest**. Узнайте больше о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Нет |
| useBinaryTransfer |Укажите, использовать ли режим передачи в двоичном формате. Значение true, если использовать двоичный режим, и false, если ASCII. Значение по умолчанию: True. Это свойство можно использовать, только когда тип связанной службы является FTP-сервер. |Нет |

> [!NOTE]
> Свойства filename и fileFilter нельзя использовать одновременно.

#### <a name="example"></a>Пример

```json
{
    "name": "FTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "FTPLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
            "fileName": "test.csv",
            "useBinaryTransfer": true
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе FTP](data-factory-ftp-connector.md#dataset-properties).

### <a name="file-system-source-in-copy-activity"></a>Источник файловой системы в действии копирования
При копировании данных с сервера FTP, задайте hello **тип источника** из hello в действии копирования слишком**FileSystemSource**и укажите следующие свойства в hello **источника** раздел:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| recursive |Указывает, доступна ли для чтения рекурсивно hello данных из подпапок hello или только из указанной папки hello. |True, False (по умолчанию) |Нет |

#### <a name="example"></a>Пример

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "FTPToBlobCopy",
            "inputs": [{
                "name": "FtpFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-08-24T18:00:00",
        "end": "2016-08-24T19:00:00"
    }
}
```

Дополнительные сведения см. в статье о [соединителе FTP](data-factory-ftp-connector.md#copy-activity-properties).


## <a name="hdfs"></a>HDFS

### <a name="linked-service"></a>Связанные службы
toodefine HDFS связанной службы, набор hello **тип** hello связанной службы слишком**Hdfs**и укажите следующие свойства в hello **typeProperties** раздела:  

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| type |свойство типа Hello должно быть присвоено: **Hdfs** |Да |
| URL-адрес |URL-адрес toohello HDFS |Да |
| authenticationType |Anonymous или Windows. <br><br> toouse **проверки подлинности Kerberos** HDFS соединителя, см. в разделе слишком[в этом разделе](#use-kerberos-authentication-for-hdfs-connector) tooset вверх в локальной среде соответствующим образом. |Да |
| userName |Имя пользователя для проверки подлинности Windows. |Да (для проверки подлинности Windows) |
| пароль |Пароль для проверки подлинности Windows. |Да (для проверки подлинности Windows) |
| gatewayName |Имя шлюза hello, hello служба фабрики данных следует использовать tooconnect toohello HDFS. |Да |
| encryptedCredential |[Новый AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) выходных данных учетные данные доступа hello. |Нет |

#### <a name="example-using-anonymous-authentication"></a>Пример: использование анонимной проверки подлинности

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-windows-authentication"></a>Пример: использование проверки подлинности Windows

```json
{
    "name": "HDFSLinkedService",
    "properties": {
        "type": "Hdfs",
        "typeProperties": {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url": "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе HDFS](#data-factory-hdfs-connector.md#linked-service-properties). 

### <a name="dataset"></a>Выборка
toodefine набора HDFS hello набор **тип** hello набора данных слишком**FileShare**и укажите следующие свойства в hello hello **typeProperties** раздела: 

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| folderPath |Путь к папке toohello. Пример: `myfolder`<br/><br/>Использовать escape-символ "\" для специальных символов в строке приветствия. Например, для "папка\вложенная_папка" укажите "папка\\\\вложенная_папка", а для "d:\пример_папки" укажите "d:\\\\пример_папки".<br/><br/>Можно объединять с помощью этого свойства **partitionBy** toohave пути к папке зависимости среза дат начала и окончания. |Да |
| fileName |Укажите имя файла hello hello в hello **folderPath** Если hello таблицы toorefer tooa конкретный файл в папку hello. Если не указано значение для этого свойства, таблица hello указывает tooall файлы в папке hello.<br/><br/>Если имя файла не указано для выходной набор данных, имя hello hello созданный файл может быть в hello в следующем формате: <br/><br/>Data<Guid>.txt (например, Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.). |Нет |
| partitionedBy |partitionedBy можно использовать toospecify динамического folderPath, имя файла для временного ряда данных. Например, путь к папке (folderPath) каждый час будет другим. |Нет |
| свойства | поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Набор hello **тип** свойства в формате tooone из следующих значений. Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Если требуется слишком**скопируйте файлы как-является** между файловых хранилищ (двоичный копия), пропустите раздел формат hello в оба определения набора входных и выходных данных. |Нет |
| compression | Укажите тип hello и уровень сжатия данных hello. Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**. Поддерживаемые уровни: **Optimal** и **Fastest**. См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Нет |

> [!NOTE]
> Свойства filename и fileFilter нельзя использовать одновременно.

#### <a name="example"></a>Пример

```json
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе HDFS](#data-factory-hdfs-connector.md#dataset-properties). 

### <a name="file-system-source-in-copy-activity"></a>Источник файловой системы в действии копирования
При копировании данных из HDFS задать hello **тип источника** из hello в действии копирования слишком**FileSystemSource**и укажите следующие свойства в hello **источника** раздела:

**FileSystemSource** поддерживает hello следующие свойства:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| recursive |Указывает, доступна ли для чтения рекурсивно hello данных из подпапок hello или только из указанной папки hello. |True, False (по умолчанию) |Нет |

#### <a name="example"></a>Пример

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "HdfsToBlobCopy",
            "inputs": [{
                "name": "InputDataset"
            }],
            "outputs": [{
                "name": "OutputDataset"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
                },
                "sink": {
                    "type": "BlobSink"
                }
            },
            "policy": {
                "concurrency": 1,
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
```

Дополнительные сведения см. в статье о [соединителе HDFS](#data-factory-hdfs-connector.md#copy-activity-properties).

## <a name="sftp"></a>SFTP


### <a name="linked-service"></a>Связанные службы
toodefine SFTP связанной службы, набор hello **тип** hello связанной службы слишком**Sftp**и укажите следующие свойства в hello **typeProperties** раздела:  

| Свойство | Описание | Обязательно |
| --- | --- | --- | --- |
| host | Имя или IP-адрес SFTP-сервере hello. |Да |
| порт |Какие hello SFTP сервера прослушивает порт. значение по умолчанию Hello: 21 |Нет |
| authenticationType |Укажите тип аутентификации. Допустимые значения: **Basic**, **SshPublicKey**. <br><br> См. слишком[использование обычной проверки подлинности](#using-basic-authentication) и [с помощью открытого ключа проверки подлинности SSH](#using-ssh-public-key-authentication) разделы в дополнительные свойства и примерами JSON, соответственно. |Да |
| skipHostKeyValidation | Укажите, размещена ли tooskip ключа проверки. | Нет. Здравствуйте, значение по умолчанию: false |
| hostKeyFingerprint | Укажите отпечаток пальца hello hello узла ключа. | Да, если hello `skipHostKeyValidation` имеет значение toofalse.  |
| gatewayName |Имя tooan tooconnect шлюз управления данными hello локальной SFTP-сервере. | Да, если копирование выполняется с локального SFTP-сервера. |
| encryptedCredential | Сервер SFTP hello tooaccess зашифрованных учетных данных. Формируется автоматически при указании обычной проверки подлинности (имя пользователя + пароль) или параметры SshPublicKey проверки подлинности (имя пользователя + пути закрытого ключа или содержимое) в копирования мастера или hello ClickOnce всплывающее диалоговое окно. | Нет. Применимо, только если копирование выполняется с локального SFTP-сервера. |

#### <a name="example-using-basic-authentication"></a>Пример: использование обычной проверки подлинности

Задайте обычную проверку подлинности toouse `authenticationType` как `Basic`и укажите следующие свойства, кроме hello SFTP соединителя универсального из них, представленные в последнем разделе hello hello:

| Свойство | Описание | Обязательно |
| --- | --- | --- | --- |
| Имя пользователя | Пользователь, обладающий доступом toohello SFTP-сервере. |Да |
| пароль | Пароль для пользователя hello (имя пользователя). | Да |

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<SFTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "password": "xxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-basic-authentication-with-encrypted-credential"></a>Пример: обычная проверка подлинности с шифрованием учетных данных**

```json
{
    "name": "SftpLinkedService",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "Basic",
            "username": "xxx",
            "encryptedCredential": "xxxxxxxxxxxxxxxxx",
            "skipHostKeyValidation": false,
            "hostKeyFingerPrint": "ssh-rsa 2048 xx:00:00:00:xx:00:x0:0x:0x:0x:0x:00:00:x0:x0:00",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="using-ssh-public-key-authentication"></a>Пример: использование проверки подлинности с открытым ключом SSH**

Задайте обычную проверку подлинности toouse `authenticationType` как `SshPublicKey`и укажите следующие свойства, кроме hello SFTP соединителя универсального из них, представленные в последнем разделе hello hello:

| Свойство | Описание | Обязательно |
| --- | --- | --- | --- |
| Имя пользователя |Пользователь, имеющий доступ toohello SFTP-сервера |Да |
| privateKeyPath | Укажите абсолютный путь toohello можно получить доступ к файлу закрытого ключа этого шлюза. | Укажите либо hello `privateKeyPath` или `privateKeyContent`. <br><br> Применимо, только если копирование выполняется с локального SFTP-сервера. |
| privateKeyContent | Сериализованная строка hello закрытого ключа содержимого. Hello мастер копирования можно считать файл закрытого ключа hello и автоматически извлекать hello закрытого ключа содержимого. При использовании любой другой инструмент и SDK, используйте свойство privateKeyPath hello. | Укажите либо hello `privateKeyPath` или `privateKeyContent`. |
| passPhrase | Укажите фразу пароль toodecrypt hello hello закрытый ключ, если hello файл ключа защищен парольную фразу. | Да, если файл закрытого ключа hello защищен парольную фразу. |

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyPath",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "<FTP server name or IP address>",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyPath": "D:\\privatekey_openssh",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true,
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-sshpublickey-authentication-using-private-key-content"></a>Пример: проверка подлинности с закрытым ключом SSH, для которого указано содержимое**

```json
{
    "name": "SftpLinkedServiceWithPrivateKeyContent",
    "properties": {
        "type": "Sftp",
        "typeProperties": {
            "host": "mysftpserver.westus.cloudapp.azure.com",
            "port": 22,
            "authenticationType": "SshPublicKey",
            "username": "xxx",
            "privateKeyContent": "<base64 string of hello private key content>",
            "passPhrase": "xxx",
            "skipHostKeyValidation": true
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе SFTP](data-factory-sftp-connector.md#linked-service-properties). 

### <a name="dataset"></a>Выборка
toodefine набор SFTP hello набор **тип** hello набора данных слишком**FileShare**и укажите следующие свойства в hello hello **typeProperties** раздел: 

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| folderPath |Путь toohello вложенной папкой. Использовать escape-символ "\" для специальных символов в строке приветствия. Примеры приведены в разделе [Примеры определений связанной службы и набора данных](#sample-linked-service-and-dataset-definitions).<br/><br/>Можно объединять с помощью этого свойства **partitionBy** toohave пути к папке зависимости среза дат начала и окончания. |Да |
| fileName |Укажите имя файла hello hello в hello **folderPath** Если hello таблицы toorefer tooa конкретный файл в папку hello. Если не указано значение для этого свойства, таблица hello указывает tooall файлы в папке hello.<br/><br/>Если имя файла не указано для выходной набор данных, имя hello hello созданный файл может быть в hello в следующем формате: <br/><br/>Data.<Guid>.txt (например, Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt |Нет |
| fileFilter |Укажите toobe фильтра используется tooselect подмножества файлов в hello folderPath, а не всех файлов.<br/><br/>Допустимые значения: `*` (несколько знаков) и `?` (один знак).<br/><br/>Пример 1: `"fileFilter": "*.log"`<br/>Пример 2: `"fileFilter": 2016-1-?.txt"`<br/><br/> Свойство fileFilter применяется к входному набору данных FileShare. HDFS не поддерживает это свойство. |Нет |
| partitionedBy |partitionedBy можно использовать toospecify динамического folderPath, имя файла для временного ряда данных. Например, путь к папке folderPath каждый час будет другим. |Нет |
| свойства | поддерживаются следующие типы формата Hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Набор hello **тип** свойства в формате tooone из следующих значений. Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Если требуется слишком**скопируйте файлы как-является** между файловых хранилищ (двоичный копия), пропустите раздел формат hello в оба определения набора входных и выходных данных. |Нет |
| compression | Укажите тип hello и уровень сжатия данных hello. Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**. Поддерживаемые уровни: **Optimal** и **Fastest**. См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Нет |
| useBinaryTransfer |Укажите, использовать ли режим передачи в двоичном формате. Значение true, если использовать двоичный режим, и false, если ASCII. Значение по умолчанию: True. Это свойство можно использовать, только когда тип связанной службы является FTP-сервер. |Нет |

> [!NOTE]
> Свойства filename и fileFilter нельзя использовать одновременно.

#### <a name="example"></a>Пример

```json
{
    "name": "SFTPFileInput",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "SftpLinkedService",
        "typeProperties": {
            "folderPath": "<path tooshared folder>",
            "fileName": "test.csv"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе SFTP](data-factory-sftp-connector.md#dataset-properties). 

### <a name="file-system-source-in-copy-activity"></a>Источник файловой системы в действии копирования
При копировании данных из источника SFTP задать hello **тип источника** из hello в действии копирования слишком**FileSystemSource**и укажите следующие свойства в hello **источника** раздел:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| recursive |Указывает, доступна ли для чтения рекурсивно hello данных из подпапок hello или только из указанной папки hello. |True, False (по умолчанию) |Нет |



#### <a name="example"></a>Пример

```json
{
    "name": "pipeline",
    "properties": {
        "activities": [{
            "name": "SFTPToBlobCopy",
            "inputs": [{
                "name": "SFTPFileInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "FileSystemSource"
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
                "executionPriorityOrder": "NewestFirst",
                "retry": 1,
                "timeout": "00:05:00"
            }
        }],
        "start": "2017-02-20T18:00:00",
        "end": "2017-02-20T19:00:00"
    }
}
```

Дополнительные сведения см. в статье о [соединителе SFTP](data-factory-sftp-connector.md#copy-activity-properties).


## <a name="http"></a>HTTP

### <a name="linked-service"></a>Связанные службы
toodefine HTTP связанной службы, набор hello **тип** hello связанной службы слишком**Http**и укажите следующие свойства в hello **typeProperties** раздела:  

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| url | Базовый URL-адрес toohello веб-сервера | Да |
| authenticationType | Указывает тип проверки подлинности hello. Допустимые значения: **Anonymous**, **Basic**, **Digest**, **Windows** и **ClientCertificate**. <br><br> Относятся toosections под этой таблицей в дополнительные свойства и примерами JSON для этих типов проверки подлинности, соответственно. | Да |
| enableServerCertificateValidation | Укажите ли tooenable сервера SSL сертификата проверки, если источником является HTTPS веб-сервера | Нет. Значение по умолчанию — true. |
| gatewayName | Имя tooan tooconnect шлюз управления данными hello локального источника HTTP. | Да, если копирование выполняется из локального источника HTTP. |
| encryptedCredential | Конечная точка HTTP hello tooaccess зашифрованных учетных данных. Автоматически сгенерированный при настройке hello сведения для проверки подлинности в копирования мастера или hello ClickOnce всплывающее диалоговое окно. | Нет. Применимо, только когда копирование данных выполняется с локального HTTP-сервера. |

#### <a name="example-using-basic-digest-or-windows-authentication"></a>Пример: использование типов проверки подлинности Basic, Digest или Windows
Задать `authenticationType` как `Basic`, `Digest`, или `Windows`и укажите следующие свойства, кроме hello HTTP соединителя универсального историй, представленные выше hello:

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| Имя пользователя | Конечная точка HTTP hello tooaccess имя пользователя. | Да |
| пароль | Пароль для пользователя hello (имя пользователя). | Да |

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "basic",
            "url": "https://en.wikipedia.org/wiki/",
            "userName": "user name",
            "password": "password"
        }
    }
}
```

#### <a name="example-using-clientcertificate-authentication"></a>Пример: использование типа проверки подлинности ClientCertificate

Задайте обычную проверку подлинности toouse `authenticationType` как `ClientCertificate`и укажите следующие свойства, кроме hello HTTP соединителя универсального историй, представленные выше hello:

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| embeddedCertData | Hello кодировке Base64 содержимое двоичных данных hello файл обмена личной информацией (PFX). | Укажите либо hello `embeddedCertData` или `certThumbprint`. |
| certThumbprint | Здравствуйте, отпечаток сертификата hello, который был установлен в хранилище сертификатов на компьютере шлюза. Применимо, только когда копирование данных выполняется из локального источника HTTP. | Укажите либо hello `embeddedCertData` или `certThumbprint`. |
| пароль | Пароль, связанный с сертификатом hello. | Нет |

При использовании `certThumbprint` необходимо для проверки подлинности и hello сертификат должен быть установлен в личном хранилище локального компьютера hello hello, служба шлюза toohello разрешение на чтение hello toogrant:

1. Запустите консоль управления (MMC). Добавить hello **сертификаты** этой цели hello оснастки **локального компьютера**.
2. Разверните **Сертификаты**, **Личные**, а затем щелкните **Сертификаты**.
3. Щелкните правой кнопкой мыши hello сертификат из личного хранилища hello и выберите **все задачи**->**управление закрытыми ключами...**
3. На hello **безопасности** добавьте учетную запись пользователя hello, под которой выполняется служба узла шлюза управления данными с сертификатом toohello hello доступ для чтения.  

**Пример: с использованием клиентского сертификата:** это связанные ссылки на службу данных фабрики tooan локальной HTTP веб-сервере. Она использует сертификат клиента, которая устанавливается на компьютере hello с установлен шлюз управления данными.

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "certThumbprint": "thumbprint of certificate",
            "gatewayName": "gateway name"
        }
    }
}
```

#### <a name="example-using-client-certificate-in-a-file"></a>Пример: использование сертификата клиента в файле
Ссылки на службы связанных данных фабрики tooan локальной HTTP веб-сервере. Он использует файл сертификата клиента на компьютере hello с установлен шлюз управления данными.

```json
{
    "name": "HttpLinkedService",
    "properties": {
        "type": "Http",
        "typeProperties": {
            "authenticationType": "ClientCertificate",
            "url": "https://en.wikipedia.org/wiki/",
            "embeddedCertData": "base64 encoded cert data",
            "password": "password of cert"
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе HTTP](data-factory-http-connector.md#linked-service-properties).

### <a name="dataset"></a>Выборка
набор данных toodefine HTTP, набор hello **тип** hello набора данных слишком**Http**и укажите следующие свойства в hello hello **typeProperties** раздела: 

| Свойство | Описание | Обязательно |
|:--- |:--- |:--- |
| relativeUrl | Относительный URL-адрес toohello ресурс, содержащий данные hello. Если путь не указан, используется только hello URL-адрес, указанный в определении службы hello связаны. <br><br> tooconstruct динамического URL-адреса можно использовать [функции фабрики данных, а системные переменные](data-factory-functions-variables.md), пример: `"relativeUrl": "$$Text.Format('/my/report?month={0:yyyy}-{0:MM}&fmt=csv', SliceStart)"`. | Нет |
| requestMethod | Метод HTTP. Допустимые значения: **GET** или **POST**. | Нет. Значение по умолчанию — `GET`. |
| additionalHeaders | Дополнительные заголовки HTTP-запроса. | Нет |
| requestBody | Текст HTTP-запроса. | Нет |
| свойства | Если требуется toosimply **получения данных hello из конечной точки HTTP-является** без его синтаксического анализа пропустить этот формат параметров. <br><br> Если требуется ответ hello HTTP tooparse содержимого во время копирования, поддерживаются следующие типы формата hello: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**. Дополнительные сведения см. в разделах о [текстовом формате](data-factory-supported-file-and-compression-formats.md#text-format), [формате Json](data-factory-supported-file-and-compression-formats.md#json-format), [формате Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [формате Orc](data-factory-supported-file-and-compression-formats.md#orc-format) и [ формате Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). |Нет |
| compression | Укажите тип hello и уровень сжатия данных hello. Поддерживаемые типы: **GZip**, **Deflate**, **BZip2** и **ZipDeflate**. Поддерживаемые уровни: **Optimal** и **Fastest**. См. дополнительные сведения о [форматах файлов и сжатия данных в фабрике данных Azure](data-factory-supported-file-and-compression-formats.md#compression-support). |Нет |

#### <a name="example-using-hello-get-default-method"></a>Пример использования hello метод GET (по умолчанию)

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "XXX/test.xml",
            "additionalHeaders": "Connection: keep-alive\nUser-Agent: Mozilla/5.0\n"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

#### <a name="example-using-hello-post-method"></a>Пример: с помощью метода POST hello

```json
{
    "name": "HttpSourceDataInput",
    "properties": {
        "type": "Http",
        "linkedServiceName": "HttpLinkedService",
        "typeProperties": {
            "relativeUrl": "/XXX/test.xml",
            "requestMethod": "Post",
            "requestBody": "body for POST HTTP request"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
Дополнительные сведения см. в статье о [соединителе HTTP](data-factory-http-connector.md#dataset-properties).

### <a name="http-source-in-copy-activity"></a>Источник HTTP в действии копирования
При копировании данных из источника HTTP задать hello **тип источника** из hello в действии копирования слишком**HttpSource**и укажите следующие свойства в hello **источника** раздела:

| Свойство | Описание | Обязательно |
| -------- | ----------- | -------- |
| httpRequestTimeout | Здравствуйте, время ожидания (TimeSpan) для hello HTTP tooget ответа для запроса. Это tooget hello время ожидания ответа, не hello время ожидания tooread данные ответа. | Нет. Значение по умолчанию  — 00:01:40. |


#### <a name="example"></a>Пример

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "HttpSourceToAzureBlob",
            "description": "Copy from an HTTP source tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "HttpSourceDataInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "HttpSource"
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
        }]
    }
}
```

Дополнительные сведения см. в статье о [соединителе HTTP](data-factory-http-connector.md#copy-activity-properties).

## <a name="odata"></a>OData

### <a name="linked-service"></a>Связанные службы
toodefine OData связанной службы, набор hello **тип** hello связанной службы слишком**OData**и укажите следующие свойства в hello **typeProperties** раздела:  

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| url |URL-адрес службы OData hello. |Да |
| authenticationType |Тип проверки подлинности, используемый источник OData toohello tooconnect. <br/><br/> Возможные значения для облачной службы OData: "Анонимно", "Обычная" и "OAuth" (обратите внимание, что сейчас фабрика данных Azure поддерживает только аутентификацию OAuth на основе Azure Active Directory). <br/><br/> Для локальной службы OData возможными значениями являются "Анонимная", "Обычная" и "Windows". |Да |
| Имя пользователя |При использовании обычной проверки подлинности укажите имя пользователя. |Да (только при использовании обычной проверки подлинности) |
| пароль |Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя. |Да (только при использовании обычной проверки подлинности) |
| authorizedCredential |Если вы используете OAuth, нажмите кнопку **авторизовать** приветствия мастера копирования фабрики данных или редактор и введите учетные данные, hello значением этого свойства будет создан. |Да (только при использовании аутентификации OAuth) |
| gatewayName |Имя шлюза hello, hello служба фабрики данных следует использовать службы OData tooconnect toohello в локальной среде. Его необходимо указывать только в том случае, если вы копируете данные из источника в локальной службе OData. |Нет |

#### <a name="example---using-basic-authentication"></a>Пример: использование обычной проверки подлинности
```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

#### <a name="example---using-anonymous-authentication"></a>Пример: использование анонимной проверки подлинности

```json
{
    "name": "ODataLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

#### <a name="example---using-windows-authentication-accessing-on-premises-odata-source"></a>Пример: использование проверки подлинности Windows при получении доступа к локальному источнику OData

```json
{
    "name": "inputLinkedService",
    "properties": {
        "type": "OData",
        "typeProperties": {
            "url": "<endpoint of on-premises OData source, for example, Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example---using-oauth-authentication-accessing-cloud-odata-source"></a>Пример: использование проверки подлинности OAuth при получении доступа к облачному источнику OData
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source, for example, https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе OData](data-factory-odata-connector.md#linked-service-properties).

### <a name="dataset"></a>Выборка
toodefine набору данных OData hello набор **тип** hello набора данных слишком**ODataResource**и укажите следующие свойства в hello hello **typeProperties** раздела: 

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| path |Путь toohello ресурс OData |Нет |

#### <a name="example"></a>Пример

```json
{
    "name": "ODataDataset",
    "properties": {
        "type": "ODataResource",
        "typeProperties": {
            "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе OData](data-factory-odata-connector.md#dataset-properties).

### <a name="relational-source-in-copy-activity"></a>Реляционный источник в действии копирования
При копировании данных из источника OData задать hello **тип источника** из hello в действии копирования слишком**RelationalSource**и укажите следующие свойства в hello **источника** раздел:

| Свойство | Описание | Пример | Обязательно |
| --- | --- | --- | --- |
| query |Используйте данные tooread hello пользовательского запроса. |"?$select=Name, Description&$top=5" |Нет |

#### <a name="example"></a>Пример

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
            "type": "Copy",
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "?$select=Name, Description&$top=5"
                },
                "sink": {
                    "type": "BlobSink",
                    "writeBatchSize": 0,
                    "writeBatchTimeout": "00:00:00"
                }
            },
            "inputs": [{
                "name": "ODataDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobODataDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "ODataToBlob"
        }],
        "start": "2017-02-01T18:00:00",
        "end": "2017-02-03T19:00:00"
    }
}
```

Дополнительные сведения см. в статье о [соединителе OData](data-factory-odata-connector.md#copy-activity-properties).


## <a name="odbc"></a>ODBC


### <a name="linked-service"></a>Связанные службы
toodefine ODBC связанной службы, набор hello **тип** hello связанной службы слишком**OnPremisesOdbc**и укажите следующие свойства в hello **typeProperties** раздела:  

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| connectionString |Hello учетные данные не доступа часть строки подключения hello и необязательный шифрование учетных данных. Примеры в следующих разделах hello. |Да |
| credential |учетные данные доступа Hello часть hello строка подключения, указанная в формате значение свойства драйвера. Пример: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”. |Нет |
| authenticationType |Тип проверки подлинности используется хранилище данных tooconnect toohello ODBC. Возможными значениями являются: "Анонимная" и "Обычная". |Да |
| Имя пользователя |При использовании обычной проверки подлинности укажите имя пользователя. |Нет |
| пароль |Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя. |Нет |
| gatewayName |Имя шлюза hello, hello служба фабрики данных должна использовать хранилище данных ODBC toohello tooconnect. |Да |

#### <a name="example---using-basic-authentication"></a>Пример: использование обычной проверки подлинности

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```
#### <a name="example---using-basic-authentication-with-encrypted-credentials"></a>Пример: использование обычной проверки подлинности и шифрования учетных данных
Можно зашифровать учетные данные hello, с помощью hello [New AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (версии 1.0 Azure PowerShell) командлета или [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 или более ранней версии hello Azure PowerShell).  

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

#### <a name="example-using-anonymous-authentication"></a>Пример: использование анонимной проверки подлинности

```json
{
    "name": "ODBCLinkedService",
    "properties": {
        "type": "OnPremisesOdbc",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "<onpremgateway>"
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе ODBC](data-factory-odbc-connector.md#linked-service-properties). 

### <a name="dataset"></a>Выборка
toodefine набору данных ODBC hello набор **тип** hello набора данных слишком**RelationalTable**и укажите следующие свойства в hello hello **typeProperties** раздела: 

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| tableName |Имя таблицы hello в хранилище данных ODBC hello. |Да |


#### <a name="example"></a>Пример

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "ODBCLinkedService",
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

Дополнительные сведения см. в статье о [соединителе ODBC](data-factory-odbc-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Реляционный источник в действии копирования
При копировании данных из хранилища данных ODBC, задайте hello **тип источника** из hello в действии копирования слишком**RelationalSource**и укажите следующие свойства в hello **источника** раздел:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| query |Используйте данные tooread hello пользовательского запроса. |Строка запроса SQL. Например, `select * from MyTable`. |Да |

#### <a name="example"></a>Пример

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [{
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
            "inputs": [{
                "name": "OdbcDataSet"
            }],
            "outputs": [{
                "name": "AzureBlobOdbcDataSet"
            }],
            "policy": {
                "timeout": "01:00:00",
                "concurrency": 1
            },
            "scheduler": {
                "frequency": "Hour",
                "interval": 1
            },
            "name": "OdbcToBlob"
        }],
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00"
    }
}
``` 

Дополнительные сведения см. в статье о [соединителе ODBC](data-factory-odbc-connector.md#copy-activity-properties).

## <a name="salesforce"></a>Salesforce


### <a name="linked-service"></a>Связанные службы
toodefine Salesforce связанной службы, набор hello **тип** hello связанной службы слишком**Salesforce**и укажите следующие свойства в hello **typeProperties** раздела:  

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| environmentUrl | Укажите URL-адрес Salesforce экземпляр hello. <br><br> — URL-адрес по умолчанию — https://login.salesforce.com. <br> -toocopy данных из "песочницы", укажите «https://test.salesforce.com». <br> -задать toocopy данные из пользовательского домена, например, «https://[domain].my.salesforce.com». |Нет |
| Имя пользователя |Укажите имя пользователя для учетной записи пользователя hello. |Да |
| пароль |Укажите пароль для учетной записи пользователя hello. |Да |
| securityToken |Укажите маркер безопасности для учетной записи пользователя hello. В разделе [получение токена безопасности](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) инструкции tooreset/get маркер безопасности. toolearn о маркерах безопасности, см в разделе [безопасности и hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm). |Да |

#### <a name="example"></a>Пример

```json
{
    "name": "SalesforceLinkedService",
    "properties": {
        "type": "Salesforce",
        "typeProperties": {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе Salesforce](data-factory-salesforce-connector.md#linked-service-properties). 

### <a name="dataset"></a>Выборка
toodefine набор данных Salesforce hello набор **тип** hello набора данных слишком**RelationalTable**и укажите следующие свойства в hello hello **typeProperties** раздела: 

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| tableName |Имя таблицы hello в Salesforce. |Нет (если для свойства **RelationalSource** задано значение **query**). |

#### <a name="example"></a>Пример

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"
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

Дополнительные сведения см. в статье о [соединителе Salesforce](data-factory-salesforce-connector.md#dataset-properties). 

### <a name="relational-source-in-copy-activity"></a>Реляционный источник в действии копирования
При копировании данных из Salesforce задать hello **тип источника** из hello в действии копирования слишком**RelationalSource**и укажите следующие свойства в hello **источника** раздел:

| Свойство | Описание | Допустимые значения | Обязательно |
| --- | --- | --- | --- |
| query |Используйте данные tooread hello пользовательского запроса. |Запрос SQL-92 или запрос, написанный на [объектно-ориентированном языке запросов Salesforce (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) . Пример: `select * from MyTable__c`. |Нет (если hello **tableName** из hello **dataset** указан) |

#### <a name="example"></a>Пример  



```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "SalesforceInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"
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
        }]
    }
}
```

> [!IMPORTANT]
> для любого пользовательского объекта требуется Hello «__c» часть hello имя API.

Дополнительные сведения см. в статье о [соединителе Salesforce](data-factory-salesforce-connector.md#copy-activity-properties). 

## <a name="web-data"></a>Веб-данные 

### <a name="linked-service"></a>Связанные службы
веб-узел toodefine связанной службы, набор hello **тип** hello связанной службы слишком**Web**и укажите следующие свойства в hello **typeProperties** раздела:  

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| URL-адрес |URL-адрес toohello веб-источнику |Да |
| authenticationType |Анонимная. |Да |
 

#### <a name="example"></a>Пример


```json
{
    "name": "web",
    "properties": {
        "type": "Web",
        "typeProperties": {
            "authenticationType": "Anonymous",
            "url": "https://en.wikipedia.org/wiki/"
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе веб-таблицы](data-factory-web-table-connector.md#linked-service-properties). 

### <a name="dataset"></a>Выборка
toodefine набора Web hello набор **тип** hello набора данных слишком**таблицы WebTable**и укажите следующие свойства в hello hello **typeProperties** раздела: 

| Свойство | Описание | Обязательно |
|:--- |:--- |:--- |
| type |Тип набора данных hello. необходимо задать слишком**таблицы WebTable** |Да |
| path |Относительный URL-адрес ресурса toohello, содержащей таблицу hello. |Нет. Если путь не указан, используется только hello URL-адрес, указанный в определении службы hello связаны. |
| index |Индекс таблицы hello в ресурсе hello Hello. В разделе [Get индекс таблицы в HTML-страницу](#get-index-of-a-table-in-an-html-page) раздел для действия toogetting индекса таблицы в HTML-страницы. |Да |

#### <a name="example"></a>Пример

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе веб-таблицы](data-factory-web-table-connector.md#dataset-properties). 

### <a name="web-source-in-copy-activity"></a>Веб-источник в действии копирования
При копировании данных из веб-таблица задать hello **тип источника** из hello в действии копирования слишком**WebSource**. В настоящее время, если источник hello в действии копирования имеет тип **WebSource**, дополнительных свойств не поддерживаются.

#### <a name="example"></a>Пример

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-06-01T18:00:00",
        "end": "2016-06-01T19:00:00",
        "description": "pipeline with copy activity",
        "activities": [{
            "name": "WebTableToAzureBlob",
            "description": "Copy from a Web table tooan Azure blob",
            "type": "Copy",
            "inputs": [{
                "name": "WebTableInput"
            }],
            "outputs": [{
                "name": "AzureBlobOutput"
            }],
            "typeProperties": {
                "source": {
                    "type": "WebSource"
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
        }]
    }
}
```

Дополнительные сведения см. в статье о [соединителе веб-таблицы](data-factory-web-table-connector.md#copy-activity-properties). 

## <a name="compute-environments"></a>ВЫЧИСЛИТЕЛЬНЫЕ СРЕДЫ
Hello следующей таблице перечислены hello вычислительных сред, поддерживаемых фабрику данных и hello преобразования действий, которые можно запустить на них. Щелкните ссылку hello hello вычислений, вы заинтересованы схемы JSON hello toosee для связанной службы toolink его tooa фабрики данных. 

| Вычислительная среда | Действия |
| --- | --- |
| [Кластер HDInsight по запросу](#on-demand-azure-hdinsight-cluster) или [собственный кластер HDInsight](#existing-azure-hdinsight-cluster) |[Настраиваемое действие .NET](#net-custom-activity), [действие Hive](#hdinsight-hive-activity), [действие Pig] (#hdinsight-pig-activity), [действие MapReduce](#hdinsight-mapreduce-activity), [действие потоковой передачи Hadoop](#hdinsight-streaming-activityd), [действие Spark](#hdinsight-spark-activity) |
| [Пакетная служба Azure](#azure-batch) |[Настраиваемое действие .NET](#net-custom-activity) |
| [машинное обучение Azure](#azure-machine-learning) | [Действие выполнения пакета в службе машинного обучения](#machine-learning-batch-execution-activity), [действие обновления ресурса в службе машинного обучения](#machine-learning-update-resource-activity) |
| [Аналитика озера данных Azure](#azure-data-lake-analytics) |[Аналитика озера данных U-SQL](#data-lake-analytics-u-sql-activity) |
| [База данных Azure SQL](#azure-sql-database-1), [хранилище данных Azure SQL](#azure-sql-data-warehouse-1), [SQL Server](#sql-server-1) |[Хранимая процедура](#stored-procedure-activity) |

## <a name="on-demand-azure-hdinsight-cluster"></a>Кластер Azure HDInsight по требованию
Hello служба фабрики данных Azure можно автоматически создать на базе Windows или Linux данных по запросу для tooprocess кластера HDInsight. кластер Hello создается в одном регионе с учетной записью хранения hello (свойство linkedServiceName в hello JSON), связанные с кластером hello hello. Можно выполнить после преобразования действий на эта связанная служба hello: [настраиваемых действий .NET](#net-custom-activity), [Hive действия](#hdinsight-hive-activity), [Действие Pig] (#hdinsight pig операции, [действия MapReduce ](#hdinsight-mapreduce-activity), [Действие потоковой передачи Hadoop](#hdinsight-streaming-activityd), [усилить действия](#hdinsight-spark-activity). 

### <a name="linked-service"></a>Связанные службы 
Привет, в следующей таблице приводится описание свойств hello, используемых в определении Azure JSON hello по требованию связанной службы HDInsight.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| type |свойство типа Hello должно быть установлено слишком**HDInsightOnDemand**. |Да |
| clusterSize |Количество узлов данных рабочего процесса или в кластере hello. Создание кластера HDInsight Hello с 2 головного узла вместе с hello число рабочих узлов, которые указаны для этого свойства. Hello узлы имеют размер Standard_D3, который имеет 4 ядра, поэтому 4 рабочий узел кластера будет 24 ядра (4\*4 = 16 ядер для рабочих узлов, плюс 2\*4 = 8 ядер для головного узла). В разделе [кластеров под управлением Linux, создать Hadoop в HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) для получения сведений об hello Standard_D3 уровня. |Да |
| timeToLive |Hello допустимое время простоя для кластера HDInsight по требованию hello. Указывает, как долго кластер HDInsight по требованию hello остается активным после завершения действий при наличии других активных заданий в кластере hello.<br/><br/>Например, если при выполнении действия занимает 6 минут и timetolive установлен too5 минут, hello кластер остается активным на 5 минут после hello 6 минут обработки при выполнении действия hello. Если при выполнении другого действия выполняется с окном приветствия 6 минут, он обрабатывается hello одного кластера.<br/><br/>Создание кластера HDInsight по требованию является ресурсоемкой операцией (может потребоваться некоторое время), поэтому используйте этот параметр как необходимые tooimprove производительности фабрики данных, используя кластер HDInsight по требованию.<br/><br/>Если задать значение too0 timetolive hello кластера удаляется сразу hello выполняться действие обработанном. На hello другой стороны, если задано большое значение, hello кластера может оставаться простоя, без необходимости приведет к высокой затраты. Таким образом важно задать соответствующее значение hello зависимости от потребностей.<br/><br/>Можно совместно использовать несколько конвейеров hello же экземпляр кластера HDInsight по требованию hello, если соответствующим образом задано значение свойства timetolive hello |Да |
| версия |Версия кластера HDInsight hello. Подробные сведения см. в статье [Версии HDInsight, поддерживаемые в фабрике данных Azure](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory). |Нет |
| linkedServiceName (имя связанной службы) |Связанная служба toobe, используемой кластером по требованию hello для хранения и обработки данных хранилища Azure. <p>В настоящее время не удается создать кластер HDInsight по требованию, использующий хранилища Озера данных Azure в качестве хранилища hello. Результирующие данные hello toostore обработки в хранилище Озера данных Azure HDInsight, используйте действие копирования toocopy hello данных из хранилища больших двоичных объектов hello toohello хранилища Озера данных Azure.</p>  | Да |
| additionalLinkedServiceNames |Указывает, что дополнительные учетные записи хранения для hello HDInsight связанной службы, чтобы служба фабрики данных hello зарегистрировать их от вашего имени. |Нет |
| osType |Тип операционной системы. Допустимые значения: Windows (по умолчанию) и Linux. |Нет |
| hcatalogLinkedServiceName |Имя Hello SQL Azure связанные службы этой базы данных HCatalog toohello точки. кластер HDInsight по требованию Hello создается с помощью базы данных Azure SQL hello как метахранилище hello. |Нет |

### <a name="json-example"></a>Пример JSON-файла
Привет, следуя JSON определяет под управлением Linux по требованию связанной службы HDInsight. Hello служба фабрики данных автоматически создает **под управлением Linux** кластера HDInsight при обработке срез данных. 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "StorageLinkedService"
        }
    }
}
```

Дополнительные сведения см. в статье [Вычислительные среды, поддерживаемые фабрикой данных Azure](data-factory-compute-linked-services.md). 

## <a name="existing-azure-hdinsight-cluster"></a>Имеющийся кластер Azure HDInsight
Можно создать кластер HDInsight tooregister службы Azure HDInsight связанные с фабрикой данных. Можно запустить hello Далее эта связанная служба действия преобразования данных: [настраиваемых действий .NET](#net-custom-activity), [Hive действия](#hdinsight-hive-activity), [Действие Pig] (#hdinsight pig операции, [MapReduce Действие](#hdinsight-mapreduce-activity), [действие потоковой передачи Hadoop](#hdinsight-streaming-activityd), [усилить действия](#hdinsight-spark-activity). 

### <a name="linked-service"></a>Связанные службы
Привет, в следующей таблице приводится описание свойств hello, используемых в определении Azure JSON hello связанная служба Azure HDInsight.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| type |свойство типа Hello должно быть установлено слишком**HDInsight**. |Да |
| clusterUri |Здравствуйте, URI кластера HDInsight hello. |Да |
| Имя пользователя |Укажите имя hello toobe hello пользователя используется существующий кластер HDInsight tooconnect tooan. |Да |
| пароль |Укажите пароль для учетной записи пользователя hello. |Да |
| linkedServiceName (имя связанной службы) | Имя связанной службой хранилища Azure, ссылающийся на хранилище больших двоичных объектов toohello hello используется hello кластера HDInsight. <p>В настоящее время для этого свойства невозможно указать связанную службу Azure Data Lake Store. Может доступа к данным в hello хранилища Озера данных Azure из скриптов Hive и Pig Если кластера HDInsight hello toohello доступа хранилища Озера данных. </p>  |Да |

Список поддерживаемых версий кластеров HDInsight см. в статье [Поддерживаемые версии HDInsight](data-factory-compute-linked-services.md#supported-hdinsight-versions-in-azure-data-factory). 

#### <a name="json-example"></a>Пример JSON-файла

```json
{
    "name": "HDInsightLinkedService",
    "properties": {
        "type": "HDInsight",
        "typeProperties": {
            "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
            "userName": "admin",
            "password": "<password>",
            "linkedServiceName": "MyHDInsightStoragelinkedService"
        }
    }
}
```

## <a name="azure-batch"></a>Пакетная служба Azure
Можно создать пул пакета виртуальных машин (ВМ) tooregister службы связанной пакетной службы Azure с фабрикой данных. Пользовательские действия .NET можно выполнять с помощью пакетной службы Azure или службы Azure HDInsight. В этой связанной службе можно запустить [настраиваемое действие .NET](#net-custom-activity). 

### <a name="linked-service"></a>Связанные службы
Hello в следующей таблице приводится описание свойств hello, используемых в определении hello Azure JSON связанной пакетной службы Azure.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| type |свойство типа Hello должно быть установлено слишком**AzureBatch**. |Да |
| accountName |Имя учетной записи пакетной службы Azure hello. |Да |
| accessKey |Ключ доступа для учетной записи пакетной службы Azure hello. |Да |
| poolName |Имя пула hello виртуальных машин. |Да |
| linkedServiceName (имя связанной службы) |Имя связанной службой хранилища Azure связанные с этой связанной пакетной службы Azure hello. Эта связанная служба используется для промежуточных файлов необходимые действия toorun hello и хранения журналов выполнения действия hello. |Да |


#### <a name="json-example"></a>Пример JSON-файла

```json
{
    "name": "AzureBatchLinkedService",
    "properties": {
        "type": "AzureBatch",
        "typeProperties": {
            "accountName": "<Azure Batch account name>",
            "accessKey": "<Azure Batch account key>",
            "poolName": "<Azure Batch pool name>",
            "linkedServiceName": "<Specify associated storage linked service reference here>"
        }
    }
}
```

## <a name="azure-machine-learning"></a>Машинное обучение Azure
Создание службы машинного обучения Azure связаны tooregister конечной точки с фабрикой данных оценки пакета машинного обучения. В этой связанной службе можно выполнять два действия преобразования данных: [действие выполнения пакета в службе машинного обучения](#machine-learning-batch-execution-activity), [действие обновления ресурса службы машинного обучения](#machine-learning-update-resource-activity). 

### <a name="linked-service"></a>Связанные службы
Привет, в следующей таблице приводится описание свойств hello, используемых в определении Azure JSON hello Azure связанной службы машинного обучения.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| Тип |свойство типа Hello должно быть присвоено: **AzureML**. |Да |
| mlEndpoint |URL-адрес оценки пакета Hello. |Да |
| apiKey |Hello опубликованы API модели рабочей области. |Да |

#### <a name="json-example"></a>Пример JSON-файла

```json
{
    "name": "AzureMLLinkedService",
    "properties": {
        "type": "AzureML",
        "typeProperties": {
            "mlEndpoint": "https://[batch scoring endpoint]/jobs",
            "apiKey": "<apikey>"
        }
    }
}
```

## <a name="azure-data-lake-analytics"></a>Аналитика озера данных Azure
Вы создаете **аналитики Озера данных Azure** связанные toolink служба фабрики данных Azure compute Служба аналитики Озера данных Azure tooan перед использованием hello [действия U-SQL аналитики Озера данных](data-factory-usql-activity.md) в конвейере .

### <a name="linked-service"></a>Связанные службы

Hello в следующей таблице приводится описание свойств hello, используемых в определении JSON hello службы связаны аналитики Озера данных Azure. 

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| Тип |свойство типа Hello должно быть присвоено: **AzureDataLakeAnalytics**. |Да |
| accountName |Имя учетной записи аналитики озера данных Azure. |Да |
| dataLakeAnalyticsUri |Универсальный код ресурса (URI) аналитики озера данных Azure. |Нет |
| authorization |Код авторизации будет извлечен автоматически после щелкнув **авторизовать** кнопку в hello редактор фабрики данных и завершение входа OAuth hello. |Да |
| subscriptionId |Идентификатор подписки Azure |Нет (если не указан, подписка hello используется фабрики данных). |
| имя_группы_ресурсов |Имя группы ресурсов Azure |Нет (если не указан, группа ресурсов для hello используется фабрики данных). |
| sessionid |Идентификатор сеанса из сеанса авторизации OAuth hello. Каждый идентификатор сеанса является уникальным и используется только один раз. При использовании hello редактор фабрики данных, этот идентификатор создан автоматически. |Да |


#### <a name="json-example"></a>Пример JSON-файла
Следующий пример Hello предоставляет определение JSON для связанной аналитики Озера данных Azure службы.

```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "<account name>",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>",
            "subscriptionId": "<subscription id>",
            "resourceGroupName": "<resource group name>"
        }
    }
}
```

## <a name="azure-sql-database"></a>База данных SQL Azure
Создание связанной службой Azure SQL и использовать ее с hello [действия хранимой процедуры](#stored-procedure-activity) tooinvoke хранимой процедуры из конвейера фабрики данных. 

### <a name="linked-service"></a>Связанные службы
toodefine базы данных SQL Azure связанной службы, набор hello **тип** hello связанной службы слишком**AzureSqlDatabase**и укажите следующие свойства в hello **typeProperties**раздела:  

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| connectionString |Укажите сведения, необходимые для свойства connectionString hello экземпляр базы данных SQL Azure toohello tooconnect. |Да |

#### <a name="json-example"></a>Пример JSON-файла

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "typeProperties": {
            "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
        }
    }
}
```

Дополнительную информацию см. в статье о [связанной службе SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties).

## <a name="azure-sql-data-warehouse"></a>Хранилище данных SQL Azure
Создание службы связаны хранилища данных SQL Azure и использовать ее с hello [действия хранимой процедуры](data-factory-stored-proc-activity.md) tooinvoke хранимой процедуры из конвейера фабрики данных. 

### <a name="linked-service"></a>Связанные службы
Хранилище данных SQL Azure toodefine связанной службы, набор hello **тип** hello связанной службы слишком**AzureSqlDW**и укажите следующие свойства в hello **typeProperties**раздела:  

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| connectionString |Укажите сведения, необходимые для свойства connectionString hello tooconnect toohello хранилище данных SQL Azure экземпляра. |Да |

#### <a name="json-example"></a>Пример JSON-файла

```json
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

Дополнительные сведения см. в статье о [соединителе хранилища данных SQL Azure](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties). 

## <a name="sql-server"></a>SQL Server 
Создание связанной службы SQL Server и использовать ее с hello [действия хранимой процедуры](data-factory-stored-proc-activity.md) tooinvoke хранимой процедуры из конвейера фабрики данных. 

### <a name="linked-service"></a>Связанные службы
Создание связанной службы типа **OnPremisesSqlServer** toolink фабрикой данных базы данных tooa в локальной среде SQL Server. Привет, в следующей таблице приводится описание JSON элементов определенного tooon локальной связанной службы SQL Server.

Привет, в следующей таблице приводится описание tooSQL определенные элементы JSON службы связанного сервера.

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| type |свойство типа Hello должно быть присвоено: **OnPremisesSqlServer**. |Да |
| connectionString |Укажите сведения connectionString, необходимые tooconnect toohello локальной SQL Server базы данных с помощью проверки подлинности Windows или проверка подлинности SQL. |Да |
| gatewayName |Имя шлюза hello, hello служба фабрики данных следует использовать toohello для tooconnect локальной базы данных SQL Server. |Да |
| Имя пользователя |При использовании проверки подлинности Windows укажите имя пользователя. Например, **domainname\\username**. |Нет |
| пароль |Укажите пароль для учетной записи пользователя hello, указанное для hello имя пользователя. |Нет |

Вы можете зашифровать учетные данные с помощью hello **New AzureRmDataFactoryEncryptValue** командлета и использовать их в строке подключения hello, как показано в следующий пример hello (**EncryptedCredential** свойство):  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```


#### <a name="example-json-for-using-sql-authentication"></a>Пример: JSON для использования проверки подлинности SQL

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
#### <a name="example-json-for-using-windows-authentication"></a>Пример: JSON для использования проверки подлинности Windows

Если указаны имя пользователя и пароль, шлюз использует их tooimpersonate hello базы данных SQL Server в локальной toohello в tooconnect учетную запись указанного пользователя. В противном случае шлюз подключается toohello SQL Server непосредственно с контекстом безопасности hello шлюза (его учетная запись для запуска).

```json
{
    "Name": " MyOnPremisesSQLDB",
    "Properties": {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
            "username": "<domain\\username>",
            "password": "<password>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

Дополнительные сведения см. в статье о [соединителе SQL Server](data-factory-sqlserver-connector.md#linked-service-properties).

## <a name="data-transformation-activities"></a>Действия преобразования данных

Действие | Описание
-------- | -----------
[Действие Hive HDInsight](#hdinsight-hive-activity) | Hello действие Hive в HDInsight из конвейера фабрики данных выполняет запросы Hive самостоятельно или кластера HDInsight под управлением Windows и Linux по требованию. 
[Действие Pig HDInsight](#hdinsight-pig-activity) | Hello действие Pig с HDInsight из конвейера фабрики данных выполняет собственную запросов Pig или кластера HDInsight под управлением Windows и Linux по требованию.
[Действие MapReduce HDInsight](#hdinsight-mapreduce-activity) | Hello действие MapReduce в HDInsight из конвейера фабрики данных выполняет программ MapReduce самостоятельно или кластера HDInsight под управлением Windows и Linux по требованию.
[Действие потоковой передачи HDInsight](#hdinsight-streaming-activity) | Hello действие потоковой передачи HDInsight из конвейера фабрики данных выполняет программ потоковой передачи Hadoop на локальном или кластера HDInsight под управлением Windows и Linux по требованию.
[Действие HDInsight Spark](#hdinsight-spark-activity) | Hello действия HDInsight Spark в конвейере фабрики данных выполняет программы Spark в кластере HDInsight. 
[Действие выполнения пакета машинного обучения](#machine-learning-batch-execution-activity) | Azure позволяет фабрики данных, вы tooeasily создавать конвейеры, использующих опубликованные машинного обучения Azure веб-службы для прогнозирования. С помощью hello действие выполнения пакета в конвейере фабрики данных Azure, можно вызвать прогнозы машинного обучения веб-службы toomake на hello данных в пакете. 
[Действие "Обновить ресурс" в службе машинного обучения](#machine-learning-update-resource-activity) | Со временем hello прогнозных моделей в hello машинного обучения, оценки экспериментов требуется toobe повторное обучение с помощью нового входных наборов данных. После завершения переподготовки, вы хотите tooupdate hello оценки веб-службы с hello повторное Обучение модели машинного обучения. Hello действия ресурса обновления tooupdate hello веб-службы можно использовать с hello вновь обучения модели.
[Действие хранимой процедуры](#stored-procedure-activity) | Действие hello хранимую процедуру можно использовать в tooinvoke конвейера фабрики данных хранимой процедуры в одном hello, следуя хранилищ данных: базы данных SQL Azure, хранилище данных SQL Azure, база данных SQL Server в вашей организации или Виртуальной машине Azure. 
[Действие U-SQL в Data Lake Analytics](#data-lake-analytics-u-sql-activity) | Действие U-SQL Data Lake Analytics запускает сценарий U-SQL для кластера Azure Data Lake Analytics.  
[Настраиваемое действие .NET](#net-custom-activity) | Если требуются данные tootransform способом, не поддерживаемый фабрики данных, можно создать пользовательское действие с свою собственную логику для обработки данных и использовать hello действия в конвейере hello. Вы можете настроить toorun .NET действие hello для пользовательских с помощью пакетной службы Azure или кластере Azure HDInsight. 

     
## <a name="hdinsight-hive-activity"></a>Действие Hive HDInsight
Можно указать следующие свойства в определении JSON действия Hive hello. свойство типа Hello для действия "hello" должно быть: **HDInsightHive**. Необходимо сначала создать связанной службы HDInsight и указывать имя hello его в качестве значения для hello **linkedServiceName** свойство. Hello поддерживаются следующие свойства в hello **typeProperties** статьи при установке hello типа tooHDInsightHive действия:

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| script |Укажите встроенного скрипта Hive hello |Нет |
| script path |Хранилище hello Hive скрипт в службе хранилища BLOB-объектов Azure и предоставить файл toohello путь hello. Можно использовать либо свойство script, либо свойство scriptPath, но не оба сразу. Имя файла Hello учитывается регистр. |Нет |
| defines |Укажите параметры как пары "ключ значение" для ссылки на куст скрипте hello «hiveconf» |Нет |

Эти свойства типа, определенного toohello действие Hive. Другие свойства (за пределами hello раздел typeProperties) поддерживаются для всех действий.   

### <a name="json-example"></a>Пример JSON-файла
Привет, следуя JSON определяет действие Hive в HDInsight в конвейере.  

```json
{
    "name": "Hive Activity",
    "description": "description",
    "type": "HDInsightHive",
    "inputs": [
      {
        "name": "input tables"
      }
    ],
    "outputs": [
      {
        "name": "output tables"
      }
    ],
    "linkedServiceName": "MyHDInsightLinkedService",
    "typeProperties": {
      "script": "Hive script",
      "scriptPath": "<pathtotheHivescriptfileinAzureblobstorage>",
      "defines": {
        "param1": "param1Value"
      }
    },
   "scheduler": {
      "frequency": "Day",
      "interval": 1
    }
}
```

Дополнительные сведения см. в статье о [действии Hive](data-factory-hive-activity.md). 

## <a name="hdinsight-pig-activity"></a>Действие Pig HDInsight
Можно указать следующие свойства в определении JSON действия Pig hello. свойство типа Hello для действия "hello" должно быть: **HDInsightPig**. Необходимо сначала создать связанной службы HDInsight и указывать имя hello его в качестве значения для hello **linkedServiceName** свойство. Hello поддерживаются следующие свойства в hello **typeProperties** статьи при установке hello типа tooHDInsightPig действия: 

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| script |Укажите встроенного скрипта Pig hello |Нет |
| script path |Хранить сценарий Pig hello в службе хранилища BLOB-объектов Azure и предоставить файл toohello путь hello. Можно использовать либо свойство script, либо свойство scriptPath, но не оба сразу. Имя файла Hello учитывается регистр. |Нет |
| defines |Укажите параметры как пары "ключ значение" для ссылки в пределах hello сценарий Pig |Нет |

Эти свойства типа, определенного toohello действие Pig. Другие свойства (за пределами hello раздел typeProperties) поддерживаются для всех действий.   

### <a name="json-example"></a>Пример JSON-файла

```json
{
    "name": "HiveActivitySamplePipeline",
      "properties": {
    "activities": [
        {
            "name": "Pig Activity",
            "description": "description",
            "type": "HDInsightPig",
            "inputs": [
                  {
                    "name": "input tables"
                  }
            ],
            "outputs": [
                  {
                    "name": "output tables"
                  }
            ],
            "linkedServiceName": "MyHDInsightLinkedService",
            "typeProperties": {
                  "script": "Pig script",
                  "scriptPath": "<pathtothePigscriptfileinAzureblobstorage>",
                  "defines": {
                    "param1": "param1Value"
                  }
            },
               "scheduler": {
                  "frequency": "Day",
                  "interval": 1
            }
          }
    ]
  }
}
```

Дополнительные сведения см. в статье о [действии Pig](#data-factory-pig-activity.md). 

## <a name="hdinsight-mapreduce-activity"></a>Действие MapReduce HDInsight
Можно указать следующие свойства в определении JSON действия MapReduce hello. свойство типа Hello для действия "hello" должно быть: **HDInsightMapReduce**. Необходимо сначала создать связанной службы HDInsight и указывать имя hello его в качестве значения для hello **linkedServiceName** свойство. Hello поддерживаются следующие свойства в hello **typeProperties** статьи при установке hello типа tooHDInsightMapReduce действия: 

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| jarLinkedService | Имя hello связанной службы для hello хранилища Azure, содержащую hello JAR-файл. | Да |
| jarFilePath | Путь к файлу toohello JAR в hello хранилища Azure. | Да | 
| className | Имя основного класса hello в hello JAR-файл. | Да | 
| arguments | Список разделенных запятыми аргументов для программы MapReduce hello. Во время выполнения, появится несколько дополнительных аргументов (например: mapreduce.job.tags) на основе инфраструктуры MapReduce hello. toodifferentiate аргументов с аргументами MapReduce hello, рассмотрите использование параметра и значение в качестве аргументов, как показано в следующий пример hello (- s,--входных данных, — т. д., выходные данные будут сразу следуют значениями параметров) | Нет | 

### <a name="json-example"></a>Пример JSON-файла

```json
{
    "name": "MahoutMapReduceSamplePipeline",
    "properties": {
        "description": "Sample Pipeline tooRun a Mahout Custom Map Reduce Jar. This job calculates an Item Similarity Matrix toodetermine hello similarity between two items",
        "activities": [
            {
                "type": "HDInsightMapReduce",
                "typeProperties": {
                    "className": "org.apache.mahout.cf.taste.hadoop.similarity.item.ItemSimilarityJob",
                    "jarFilePath": "adfsamples/Mahout/jars/mahout-examples-0.9.0.2.2.7.1-34.jar",
                    "jarLinkedService": "StorageLinkedService",
                    "arguments": ["-s", "SIMILARITY_LOGLIKELIHOOD", "--input", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/input", "--output", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/output/", "--maxSimilaritiesPerItem", "500", "--tempDir", "wasb://adfsamples@spestore.blob.core.windows.net/Mahout/temp/mahout"]
                },
                "inputs": [
                    {
                        "name": "MahoutInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "MahoutOutput"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "MahoutActivity",
                "description": "Custom Map Reduce toogenerate Mahout result",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-01-03T00:00:00",
        "end": "2017-01-04T00:00:00"
    }
}
```

Дополнительные сведения см. в статье о [действии MapReduce](data-factory-map-reduce.md). 

## <a name="hdinsight-streaming-activity"></a>Действие потоковой передачи HDInsight
Можно указать следующие свойства в определении JSON действия потоковой передачи Hadoop hello. свойство типа Hello для действия "hello" должно быть: **HDInsightStreaming**. Необходимо сначала создать связанной службы HDInsight и указывать имя hello его в качестве значения для hello **linkedServiceName** свойство. Hello поддерживаются следующие свойства в hello **typeProperties** статьи при установке hello типа tooHDInsightStreaming действия: 

| Свойство | Описание | 
| --- | --- |
| mapper | Имя исполняемого файла модуля сопоставления hello. В примере hello cat.exe является исполняемого файла модуля сопоставления hello.| 
| reducer | Имя исполняемого файла редуктора hello. В примере hello wc.exe — исполняемого файла редуктора hello. | 
| input | Входной файл (в том числе расположение) для сопоставления hello. В примере hello: «wasb://adfsample@<account name>.blob.core.windows.net/example/data/gutenberg/davinci.txt»: adfsample — контейнер больших двоичных объектов hello, пример/data/Gutenberg — папка hello и davinci.txt — hello большого двоичного объекта. |
| output | Выходной файл (в том числе расположение) для hello редуктора. выходные данные задания потоковой передачи Hadoop hello Hello записывается toohello расположение, заданное для этого свойства. |
| filePaths | Пути для исполняемых файлов сопоставления и редуктора hello. В примере hello: «adfsample/example/apps/wc.exe» adfsample — hello контейнер больших двоичных объектов, example/apps — папка hello и wc.exe — hello исполняемый файл. | 
| fileLinkedService | Связанная служба, которая представляет hello хранилища Azure, содержащей hello файлы, указанные в разделе filePaths hello хранилища Azure. | 
| arguments | Список разделенных запятыми аргументов для программы MapReduce hello. Во время выполнения, появится несколько дополнительных аргументов (например: mapreduce.job.tags) на основе инфраструктуры MapReduce hello. toodifferentiate аргументов с аргументами MapReduce hello, рассмотрите использование параметра и значение в качестве аргументов, как показано в следующий пример hello (- s,--входных данных, — т. д., выходные данные будут сразу следуют значениями параметров) | 
| getDebugInfo | Необязательный элемент. Если он имеет значение tooFailure, hello журналы будут загружены только при сбое. Если он имеет значение tooAll, журналы, загружаются всегда независимо от состояния выполнения hello. | 

> [!NOTE]
> Необходимо указать выходной набор данных для hello действие потоковой передачи Hadoop для hello **выводит** свойство. Этот набор данных может быть просто пустой набор данных, необходимые toodrive hello конвейера расписание (каждый час, день, и т. д.). Если действие hello не принимает входных данных, можно пропустить, указав входного набора данных для действия "hello" для hello **входов** свойство.  

## <a name="json-example"></a>Пример JSON-файла

```json
{
    "name": "HadoopStreamingPipeline",
    "properties": {
        "description": "Hadoop Streaming Demo",
        "activities": [
            {
                "type": "HDInsightStreaming",
                "typeProperties": {
                    "mapper": "cat.exe",
                    "reducer": "wc.exe",
                    "input": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/gutenberg/davinci.txt",
                    "output": "wasb://<nameofthecluster>@spestore.blob.core.windows.net/example/data/StreamingOutput/wc.txt",
                    "filePaths": ["<nameofthecluster>/example/apps/wc.exe","<nameofthecluster>/example/apps/cat.exe"],
                    "fileLinkedService": "StorageLinkedService",
                    "getDebugInfo": "Failure"
                },
                "outputs": [
                    {
                        "name": "StreamingOutputDataset"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "RunHadoopStreamingJob",
                "description": "Run a Hadoop streaming job",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2014-01-04T00:00:00",
        "end": "2014-01-05T00:00:00"
    }
}
```

Дополнительные сведения см. в статье о [действии потоковой передачи Hadoop](data-factory-hadoop-streaming-activity.md). 

## <a name="hdinsight-spark-activity"></a>Действие HDInsight Spark
Можно указать следующие свойства в определении JSON действия Spark hello. свойство типа Hello для действия "hello" должно быть: **HDInsightSpark**. Необходимо сначала создать связанной службы HDInsight и указывать имя hello его в качестве значения для hello **linkedServiceName** свойство. Hello поддерживаются следующие свойства в hello **typeProperties** статьи при установке hello типа tooHDInsightSpark действия: 

| Свойство | Описание | Обязательно |
| -------- | ----------- | -------- |
| rootPath | контейнер больших двоичных объектов Azure Hello и папку, содержащую файл Spark hello. Имя файла Hello учитывается регистр. | Да |
| entryFilePath | Относительный путь toohello корневую папку hello пакет кода Spark. | Да |
| className | Основной класс Java или Spark приложения. | Нет | 
| arguments | Список аргументов командной строки toohello Spark программы. | Нет | 
| proxyUser | Hello учетной записи пользователя tooimpersonate tooexecute hello Spark программы | Нет | 
| sparkConfig | Свойства конфигурации Spark. | Нет | 
| getDebugInfo | Указывает при файлов журнала Spark hello скопированный toohello хранилища Azure в кластере HDInsight (или) заданные sparkJobLinkedService. Допустимые значения: None, Always или Failure. Значение по умолчанию: None. | Нет | 
| sparkJobLinkedService | Hello связанной службой хранилища Azure, содержащий файл задания Spark hello, зависимости и журналы.  Если значение этого свойства не указано, используется хранилище hello, связанное с кластером HDInsight. | Нет |

### <a name="json-example"></a>Пример JSON-файла

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-05T00:00:00",
        "end": "2017-02-06T00:00:00"
    }
}
```
Обратите внимание hello после точки. 

- Hello **тип** задано слишком**HDInsightSpark**.
- Hello **rootPath** задано слишком**adfspark\\pyFiles** где adfspark — контейнер больших двоичных объектов Azure hello и pyFiles — нормально папки в этом контейнере. В этом примере hello хранилища больших двоичных объектов — hello, связанная с кластера Spark hello. Вы можете отправить файл tooa hello другое хранилище Azure. Если сделать это, создайте toolink службы хранилища Azure связаны этой фабрики данных toohello учетной записи хранилища. Укажите имя hello hello связаны службы как значение для hello **sparkJobLinkedService** свойство. В разделе [свойства действия Spark](#spark-activity-properties) подробные сведения об этом и других свойствах, поддерживаемых hello Spark действия.
- Hello **entryFilePath** задано toohello **test.py**, который является файлом python hello. 
- Hello **getDebugInfo** задано слишком**всегда**, что означает, файлы журнала hello всегда создается (успех или сбой).  

    > [!IMPORTANT]
    > Мы рекомендуем, что не задано это свойство tooAlways в рабочей среде, если нужно устранить проблему. 
- Hello **выводит** раздел содержит один выходной набор данных. Необходимо указать выходной набор данных, даже если программа spark hello не создает никаких выходных данных. Hello выходного набора данных дисков hello расписания для конвейера hello (каждый час, день, и т. д.).

Дополнительные сведения о действии hello см. в разделе [действия Spark](data-factory-spark.md) статьи.  

## <a name="machine-learning-batch-execution-activity"></a>Действие выполнения пакета в службе машинного обучения
Можно указать следующие свойства в определении Azure ML пакетного выполнения действия JSON hello. свойство типа Hello для действия "hello" должно быть: **AzureMLBatchExecution**. Необходимо создать Azure машинного обучения связанной службы сначала и указывать имя hello его в качестве значения для hello **linkedServiceName** свойство. Hello поддерживаются следующие свойства в hello **typeProperties** статьи при установке hello типа tooAzureMLBatchExecution действия:

Свойство | Описание | Обязательно 
-------- | ----------- | --------
webServiceInput | набор данных toobe Hello передана в качестве входных данных для веб-службы машинного Обучения Azure hello. Этот набор данных также должно быть включено в hello входные данные для действия "hello". |Используйте webServiceInput или webServiceInputs. | 
webServiceInputs | Укажите toobe наборы данных, переданные как входные данные для hello веб-службы машинного Обучения Azure. Если веб-служба hello принимает несколько входов, свойство hello webServiceInputs вместо того чтобы использовать свойство webServiceInput hello. Наборы данных, на которые ссылается hello **webServiceInputs** также должны быть включены в действие hello **входов**. | Используйте webServiceInput или webServiceInputs. | 
webServiceOutputs | Hello наборы данных, которые были назначены в качестве выходных данных для веб-службы машинного Обучения Azure hello. Hello веб-служба возвращает выходные данные в этом наборе данных. | Да | 
globalParameters | Укажите значения для hello параметры веб-службы в этом разделе. | Нет | 

### <a name="json-example"></a>Пример JSON-файла
В этом примере hello действие имеет набор данных hello **MLSqlInput** в качестве входного и **MLSqlOutput** в качестве выходных данных hello. Hello **MLSqlInput** передается в качестве входного toohello веб-службы с помощью hello **webServiceInput** свойства JSON. Hello **MLSqlOutput** передается в качестве выходных данных toohello веб-службы с помощью hello **webServiceOutputs** свойства JSON. 

```json
{
   "name": "MLWithSqlReaderSqlWriter",
   "properties": {
      "description": "Azure ML model with sql azure reader/writer",
      "activities": [{
         "name": "MLSqlReaderSqlWriterActivity",
         "type": "AzureMLBatchExecution",
         "description": "test",
         "inputs": [ { "name": "MLSqlInput" }],
         "outputs": [ { "name": "MLSqlOutput" } ],
         "linkedServiceName": "MLSqlReaderSqlWriterDecisionTreeModel",
         "typeProperties":
         {
            "webServiceInput": "MLSqlInput",
            "webServiceOutputs": {
               "output1": "MLSqlOutput"
            },
            "globalParameters": {
               "Database server name": "<myserver>.database.windows.net",
               "Database name": "<database>",
               "Server user account name": "<user name>",
               "Server user account password": "<password>"
            }              
         },
         "policy": {
            "concurrency": 1,
            "executionPriorityOrder": "NewestFirst",
            "retry": 1,
            "timeout": "02:00:00"
         }
      }],
      "start": "2016-02-13T00:00:00",
       "end": "2016-02-14T00:00:00"
   }
}
```

В примере JSON hello hello развернута служба использует средство чтения и записи модуля tooread и записи данных из компьютер обучения Azure веб-tooan базы данных SQL Azure. Этот веб-служба предоставляет hello следующие четыре параметра: имя сервера, имя базы данных, имя учетной записи пользователя сервера и пароль учетной записи пользователя сервера базы данных.

> [!NOTE]
> Только входные и выходные данные действия AzureMLBatchExecution hello могут передаваться как параметры toohello веб-службы. Например в hello выше фрагменте кода JSON MLSqlInput является входной toohello AzureMLBatchExecution действия, которое передается в качестве входного toohello веб-службы через параметр webServiceInput.

## <a name="machine-learning-update-resource-activity"></a>Действие обновления ресурса в службе машинного обучения
Можно указать следующие свойства в определении Azure ML обновление ресурсов действии JSON hello. свойство типа Hello для действия "hello" должно быть: **AzureMLUpdateResource**. Необходимо создать Azure машинного обучения связанной службы сначала и указывать имя hello его в качестве значения для hello **linkedServiceName** свойство. Hello поддерживаются следующие свойства в hello **typeProperties** статьи при установке hello типа tooAzureMLUpdateResource действия:

Свойство | Описание | Обязательно 
-------- | ----------- | --------
trainedModelName | Имя hello повторное Обучение модели. | Да |  
trainedModelDatasetName | Файл набора данных указывающего toohello iLearner возвращенных hello переподготовки операции. | Да | 

### <a name="json-example"></a>Пример JSON-файла
Hello конвейера содержит два действия: **AzureMLBatchExecution** и **AzureMLUpdateResource**. Hello операции при выполнении пакета машинного Обучения Azure принимает hello обучающие данные в качестве входных данных и создает файл iLearner, как выходные данные. Действие Hello вызывает hello обучения веб-службы (эксперимента обучения в виде веб-службы) с входными данными hello обучающих данных и получает от веб-службы hello файл ilearner hello. Hello placeholderBlob является просто пустой результирующий набор данных, которые требуются для конвейера hello toorun служба фабрики данных Azure hello.


```json
{
    "name": "pipeline",
    "properties": {
        "activities": [
            {
                "name": "retraining",
                "type": "AzureMLBatchExecution",
                "inputs": [
                    {
                        "name": "trainingData"
                    }
                ],
                "outputs": [
                    {
                        "name": "trainedModelBlob"
                    }
                ],
                "typeProperties": {
                    "webServiceInput": "trainingData",
                    "webServiceOutputs": {
                        "output1": "trainedModelBlob"
                    }              
                 },
                "linkedServiceName": "trainingEndpoint",
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "02:00:00"
                }
            },
            {
                "type": "AzureMLUpdateResource",
                "typeProperties": {
                    "trainedModelName": "trained model",
                    "trainedModelDatasetName" :  "trainedModelBlob"
                },
                "inputs": [{ "name": "trainedModelBlob" }],
                "outputs": [{ "name": "placeholderBlob" }],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "AzureML Update Resource",
                "linkedServiceName": "updatableScoringEndpoint2"
            }
        ],
        "start": "2016-02-13T00:00:00",
        "end": "2016-02-14T00:00:00"
    }
}
```

## <a name="data-lake-analytics-u-sql-activity"></a>Действие U-SQL в аналитике озера данных
Можно указать следующие свойства в определении JSON действия U-SQL hello. свойство типа Hello для действия "hello" должно быть: **DataLakeAnalyticsU SQL**. Необходимо создать службу связанной аналитики Озера данных Azure и указывать имя hello его в качестве значения для hello **linkedServiceName** свойство. Hello поддерживаются следующие свойства в hello **typeProperties** статьи при установке hello типа действия tooDataLakeAnalyticsU-SQL: 

| Свойство | Описание | Обязательно |
|:--- |:--- |:--- |
| scriptPath |Toofolder путь, содержащий скрипт hello U-SQL. Имя файла hello учитывается регистр. |Нет (если используется скрипт) |
| scriptLinkedService |Связанной службы, которая связывает hello хранилища, содержащий фабрики данных toohello сценария hello |Нет (если используется скрипт) |
| script |Указание сценария непосредственно в строке вместо использования scriptPath и scriptLinkedService. Например: "script" : "CREATE DATABASE test". |Нет (при использовании scriptPath и scriptLinkedService) |
| degreeOfParallelism |Максимальное количество узлов Hello одновременно использовать toorun hello задания. |Нет |
| priority |Определяет, какие задания из всех, поставленных в очередь должна быть выбранного toorun сначала. Hello hello снижать hello более высокий приоритет hello. |Нет |
| parameters |Параметры для скрипта hello U-SQL |Нет |

### <a name="json-example"></a>Пример JSON-файла

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This pipeline computes events for en-gb locale and date less than Feb 19, 2012.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00",
        "end": "2015-08-08T01:00:00",
        "isPaused": false
    }
}
```

Дополнительные сведения см. в статье о [действии U-SQL Data Lake Analytics](data-factory-usql-activity.md). 

## <a name="stored-procedure-activity"></a>Действие хранимой процедуры
Можно указать следующие свойства в определении хранимой процедуры действии JSON hello. свойство типа Hello для действия "hello" должно быть: **SqlServerStoredProcedure**. Необходимо создать следующие связанные службы hello и указывать имя hello hello связаны службы в качестве значения для hello **linkedServiceName** свойства:

- SQL Server 
- База данных SQL Azure
- Хранилище данных SQL Azure

Hello поддерживаются следующие свойства в hello **typeProperties** статьи при установке hello типа tooSqlServerStoredProcedure действия:

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| storedProcedureName |Укажите имя hello hello хранимой процедуры в базе данных Azure SQL hello или хранилище данных SQL Azure, представленного hello связаны службы, которая hello использования выходной таблицы. |Да |
| storedProcedureParameters |Указываемые значения для параметров хранимой процедуры. Если вам требуется toopass значение null для параметра, используйте синтаксис hello: «param1»: null (все строчные). См. следующий пример toolearn об использовании этого свойства hello. |Нет |

При указании входного набора данных, он должен быть доступен (в состояние «Готово») для hello хранимой процедуры toorun действия. Hello входного набора данных не может использоваться в hello хранимой процедуре как параметр. Это только используемые toocheck hello зависимостей, до начала hello действие хранимой процедуры. Для действия хранимой процедуры необходимо указать выходной набор данных. 

Выходной набор данных указывает hello **расписание** для hello действие хранимой процедуры (каждый час, еженедельно, ежемесячно, и т. д.). Hello выходной набор данных необходимо использовать **связанная служба** , обозначающий tooan базы данных SQL Azure или хранилище данных SQL Azure или базе SQL Server, в котором нужно hello toorun хранимой процедуры. Hello выходной набор данных может служить результат hello toopass способом hello хранимые процедуры для последующей обработки другим действием ([цепочки действий](data-factory-scheduling-and-execution.md##multiple-activities-in-a-pipeline)) в конвейере hello. Однако фабрики данных вывода автоматически hello объекта dataset toothis хранимой процедуры. Это hello хранимая процедура записи таблицы tooa SQL, который hello указывает выходного набора данных. В некоторых случаях может быть выходной набор данных hello **пустой набор данных**, который используется только для hello расписание hello toospecify действие хранимой процедуры.  

### <a name="json-example"></a>Пример JSON-файла

```json
{
    "name": "SprocActivitySamplePipeline",
    "properties": {
        "activities": [
            {
                "type": "SqlServerStoredProcedure",
                "typeProperties": {
                    "storedProcedureName": "sp_sample",
                    "storedProcedureParameters": {
                        "DateTime": "$$Text.Format('{0:yyyy-MM-dd HH:mm:ss}', SliceStart)"
                    }
                },
                "outputs": [{ "name": "sprocsampleout" }],
                "name": "SprocActivitySample"
            }
        ],
         "start": "2016-08-02T00:00:00",
         "end": "2016-08-02T05:00:00",
        "isPaused": false
    }
}
```

Дополнительные сведения см. в статье о [действии хранимой процедуры](data-factory-stored-proc-activity.md). 

## <a name="net-custom-activity"></a>Настраиваемое действие .NET
Можно указать следующие свойства в настраиваемом действии .NET определения JSON hello. свойство типа Hello для действия "hello" должно быть: **DotNetActivity**. Необходимо создать связанная служба Azure HDInsight или связанной Azure пакетной службе и задайте имя hello hello связаны службы как значение для hello **linkedServiceName** свойство. Hello поддерживаются следующие свойства в hello **typeProperties** статьи при установке hello типа tooDotNetActivity действия:
 
| Свойство | Описание | Обязательно |
|:--- |:--- |:--- |
| AssemblyName | Имя сборки hello. В примере hello: **MyDotnetActivity.dll**. | Да |
| EntryPoint |Имя класса "hello", реализующий интерфейс IDotNetActivity hello. В примере hello: **MyDotNetActivityNS.MyDotNetActivity** где MyDotNetActivityNS является пространством имен hello и MyDotNetActivity является классом hello.  | Да | 
| PackageLinkedService | Имя связанной службой хранилища Azure, указывающий toohello хранилища больших двоичных объектов, содержащий ZIP-файл hello пользовательское действие hello. В примере hello: **AzureStorageLinkedService**.| Да |
| PackageFile | Имя hello ZIP-файл. В примере hello: **customactivitycontainer/MyDotNetActivity.zip**. | Да |
| extendedProperties | Расширенные свойства, которые вы можете определять и передавать на коде .NET toohello. В этом примере hello **SliceStart** переменной задано значение tooa на основании hello SliceStart системной переменной. | Нет | 

### <a name="json-example"></a>Пример JSON-файла

```json
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "AzureBatchLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00",
    "end": "2016-11-16T05:00:00",
    "isPaused": false
  }
}
```

Подробные сведения см. в статье об [использовании настраиваемых действий в фабрике данных](data-factory-use-custom-activities.md). 

## <a name="next-steps"></a>Дальнейшие действия
См. следующие учебники hello. 

- [Руководство. Создание конвейера с действием копирования с помощью портала Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
- [Руководство. Создание первой фабрики данных Azure с помощью портала Azure](data-factory-build-your-first-pipeline-using-editor.md)