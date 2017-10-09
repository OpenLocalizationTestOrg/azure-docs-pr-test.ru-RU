---
title: "aaaData функции фабрики и системные переменные | Документы Microsoft"
description: "Содержит список функций и системных переменных фабрики данных Azure."
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
services: data-factory
ms.assetid: b6b3c2ae-b0e8-4e28-90d8-daf20421660d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: d2936c2821797947bb37d9775226a6c19c4b8ab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---functions-and-system-variables"></a>Фабрика данных Azure — функции и системные переменные
В этой статье содержатся сведения о функциях и переменных, поддерживаемых фабрикой данных Azure.

## <a name="data-factory-system-variables"></a>Системные переменные фабрики данных
| Имя переменной | Описание | Область объекта | Область JSON и примеры использования |
| --- | --- | --- | --- |
| WindowStart |Начало интервала времени для текущего окна запуска действия. |действие |<ol><li>Укажите запросы на выбор данных. См. в статьях соединитель, на которые ссылается hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи.</li> |
| WindowEnd |Конец интервала времени для текущего окна запуска действия. |действие |то же, что и WindowStart. |
| SliceStart |Начало интервала времени для формируемого среза данных. |действие<br/>набор данных |<ol><li>Укажите динамические пути к папкам и имена файлов при работе с [большими двоичными объектами Azure](data-factory-azure-blob-connector.md) и [наборами данных файловой системы](data-factory-onprem-file-system-connector.md).</li><li>Укажите входные зависимости с помощью функций фабрики данных в коллекции входных данных действия.</li></ol> |
| SliceEnd |Конец интервала времени для текущего среза данных. |действие<br/>dataset |То же, что и для SliceStart. |

> [!NOTE]
> В настоящее время фабрики данных требует, что hello запланировать hello указано в действие точно соответствует hello расписанием, заданным в доступности hello выходного набора данных. Таким образом, WindowStart, WindowEnd, а также SliceStart и SliceEnd всегда сопоставляйте toohello одновременную период и один выходной среза.
> 

### <a name="example-for-using-a-system-variable"></a>Пример использования системной переменной
В следующий пример, год, месяц, день и время hello **SliceStart** извлекаются в отдельные переменные, которые используются в **folderPath** и **fileName** свойства.

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

## <a name="data-factory-functions"></a>Функции фабрики данных
Можно использовать функции в фабрике данных, а также системные переменные для hello следующих целей:

1. Указание запросов для выбора данных (см. в статьях соединителя ссылается hello [действия перемещения данных](data-factory-data-movement-activities.md) статьи.
   
   Здравствуйте, tooinvoke синтаксис функции фабрики данных —:  **$$ <function>**  запросы выбора данных и других свойств в действие hello и наборах данных.  
2. Указание входных зависимостей с помощью функций фабрики данных в коллекции входных данных действия.
   
    Префикс $$ не требуется при указании выражений входных зависимостей.     

В следующий пример hello **sqlReaderQuery** в файле JSON присваивается значение tooa, возвращенное hello `Text.Format` функции. В этом примере также используется системная переменная с именем **WindowStart**, который представляет hello время начала действия hello, выполните в окне.

```json
{
    "Type": "SqlSource",
    "sqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
}
```

В разделе [Строки настраиваемых форматов даты и времени](https://msdn.microsoft.com/library/8kb3ddd4.aspx) описаны различные варианты форматирования, которые можно использовать (пример: гг и гггг). 

### <a name="functions"></a>Функции
Hello в следующей таблице перечислены все функции hello в фабрике данных Azure:

| Категория | Функция | Параметры | Описание |
| --- | --- | --- | --- |
| Время |AddHours(X,Y) |X: DateTime  <br/><br/>Y: int |Добавляет Y часов toohello заданному времени X. <br/><br/>Пример: `9/5/2013 12:00:00 PM + 2 hours = 9/5/2013 2:00:00 PM` |
| Время |AddMinutes(X,Y) |X: DateTime  <br/><br/>Y: int |Добавляет Y минут tooX.<br/><br/>Пример: `9/15/2013 12: 00:00 PM + 15 minutes = 9/15/2013 12: 15:00 PM` |
| Время |StartOfHour(X) |X: DateTime  |Возвращает hello время начала для часа hello, представленного компонентом часа hello X. <br/><br/>Пример: `StartOfHour of 9/15/2013 05: 10:23 PM is 9/15/2013 05: 00:00 PM` |
| Дата |AddDays(X,Y) |X: DateTime <br/><br/>Y: int |Добавляет Y дней tooX. <br/><br/>Пример: 15.09.2013 12:00:00 + 2 дня = 17.09.2013 12:00:00.<br/><br/>Можно также вычитать дни, указав в качестве Y отрицательное число.<br/><br/>Пример: `9/15/2013 12:00:00 PM - 2 days = 9/13/2013 12:00:00 PM`. |
| Дата |AddMonths(X,Y) |X: DateTime <br/><br/>Y: int |Добавляет Y месяцев tooX.<br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 month = 10/15/2013 12:00:00 PM`.<br/><br/>Можно также вычитать месяцы, указав в качестве Y отрицательное число.<br/><br/>Пример: `9/15/2013 12:00:00 PM - 1 month = 8/15/2013 12:00:00 PM`.|
| Дата |AddQuarters(X,Y) |X: DateTime  <br/><br/>Y: int |Добавляет Y * 3 месяца tooX.<br/><br/>Пример: `9/15/2013 12:00:00 PM + 1 quarter = 12/15/2013 12:00:00 PM` |
| Дата |AddWeeks(X,Y) |X: DateTime <br/><br/>Y: int |Добавляет Y * 7 дней tooX<br/><br/>Пример: 15.09.2013 12:00:00 + 1 неделя = 22.09.2013 12:00:00.<br/><br/>Можно также вычитать недели, указав в качестве Y отрицательное число.<br/><br/>Пример: `9/15/2013 12:00:00 PM - 1 week = 9/7/2013 12:00:00 PM`. |
| Дата |AddYears(X,Y) |X: DateTime <br/><br/>Y: int |Добавляет Y лет tooX.<br/><br/>`Example: 9/15/2013 12:00:00 PM + 1 year = 9/15/2014 12:00:00 PM`<br/><br/>Можно также вычитать года, указав в качестве Y отрицательное число.<br/><br/>Пример: `9/15/2013 12:00:00 PM - 1 year = 9/15/2012 12:00:00 PM`. |
| Дата |Day(X) |X: DateTime  |Возвращает компонент дня hello X.<br/><br/>Пример: `Day of 9/15/2013 12:00:00 PM is 9`. |
| Дата |DayOfWeek(X) |X: DateTime  |Возвращает день недели Координата X hello.<br/><br/>Пример: `DayOfWeek of 9/15/2013 12:00:00 PM is Sunday`. |
| Дата |DayOfYear(X) |X: DateTime  |Возвращает день hello hello года, представленный компонентом года hello X.<br/><br/>Примеры:<br/>`12/1/2015: day 335 of 2015`<br/>`12/31/2015: day 365 of 2015`<br/>`12/31/2016: day 366 of 2016 (Leap Year)` |
| Дата |DaysInMonth(X) |X: DateTime  |Возвращает hello дней в месяце hello, представленный hello компонентом месяца параметра X.<br/><br/>Пример: `DaysInMonth of 9/15/2013 are 30 since there are 30 days in hello September month`. |
| Дата |EndOfDay(X) |X: DateTime  |Возвращает hello даты времени, представляющее конец hello hello дня (компонента дня) X.<br/><br/>Пример: `EndOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 11:59:59 PM`. |
| Дата |EndOfMonth(X) |X: DateTime  |Получает конец hello hello месяца, представленный компонентом месяца параметра X. <br/><br/>Пример: `EndOfMonth of 9/15/2013 05:10:23 PM is 9/30/2013 11:59:59 PM` (Дата и время, представляющий hello конец сентября) |
| Дата |StartOfDay(X) |X: DateTime  |Получает начало hello hello дня, представленного компонентом дня hello параметра X.<br/><br/>Пример: `StartOfDay of 9/15/2013 05:10:23 PM is 9/15/2013 12:00:00 AM`. |
| DateTime |From(X) |X: String |Синтаксический анализ строки X tooa Дата и время. |
| DateTime |Ticks(X) |X: DateTime  |Возвращает свойства параметра hello X hello тактов. Один такт равен 100 наносекунд. Hello значение этого свойства представляет hello количество тактов, прошедших с полуночи в 12:00:00, 1 января 0001 г. |
| текст |Format(X) |X: String (переменная) |Текст hello форматов (использовать `\\'` tooescape комбинации `'` символов).|

> [!IMPORTANT]
> При использовании функции в другую функцию, нет необходимости toouse  **$$**  префикс для внутренней функции hello. Например, $$Text.Format('PartitionKey eq \\'my_pkey_filter_value\\' and RowKey ge \\'{0:yyyy-MM-dd HH:mm:ss}\\'', Time.AddHours(SliceStart, -6)). Обратите внимание, что в этом примере  **$$**  префикс не используется для hello **Time.AddHours** функции. 

#### <a name="example"></a>Пример
В hello в следующем примере, входные и выходные параметры для действия Hive hello определяются с использованием hello `Text.Format` функции и SliceStart системной переменной. 

```json  
{
    "name": "HiveActivitySamplePipeline",
        "properties": {
    "activities": [
            {
            "name": "HiveActivitySample",
            "type": "HDInsightHive",
            "inputs": [
                    {
                    "name": "HiveSampleIn"
                    }
            ],
            "outputs": [
                    {
                    "name": "HiveSampleOut"
                }
            ],
            "linkedServiceName": "HDInsightLinkedService",
            "typeproperties": {
                    "scriptPath": "adfwalkthrough\\scripts\\samplehive.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Input": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/samplein/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)",
                        "Output": "$$Text.Format('wasb://adfwalkthrough@<storageaccountname>.blob.core.windows.net/sampleout/yearno={0:yyyy}/monthno={0:MM}/dayno={0:dd}/', SliceStart)"
                    },
                    "scheduler": {
                        "frequency": "Hour",
                        "interval": 1
                }
            }
            }
    ]
    }
}
```

### <a name="example-2"></a>Пример 2

В следующем примере hello hello параметра DateTime для hello действия хранимой процедуры, определяется с помощью текста hello. Функции форматирования и hello SliceStart переменной. 

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
                "outputs": [
                    {
                        "name": "sprocsampleout"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "SprocActivitySample"
            }
        ],
            "start": "2016-08-02T00:00:00Z",
            "end": "2016-08-02T05:00:00Z",
        "isPaused": false
    }
}
```

### <a name="example-3"></a>Пример 3
tooread данные из предыдущего дня вместо день представлен прошедшими hello SliceStart, используйте функции hello AddDays, как показано в следующий пример hello: 

```json
{
    "name": "SamplePipeline",
    "properties": {
        "start": "2016-01-01T08:00:00",
        "end": "2017-01-01T11:00:00",
        "description": "hive activity",
        "activities": [
            {
                "name": "SampleHiveActivity",
                "inputs": [
                    {
                        "name": "MyAzureBlobInput",
                        "startTime": "Date.AddDays(SliceStart, -1)",
                        "endTime": "Date.AddDays(SliceEnd, -1)"
                    }
                ],
                "outputs": [
                    {
                        "name": "MyAzureBlobOutput"
                    }
                ],
                "linkedServiceName": "HDInsightLinkedService",
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adftutorial\\hivequery.hql",
                    "scriptLinkedService": "StorageLinkedService",
                    "defines": {
                        "Year": "$$Text.Format('{0:yyyy}',WindowsStart)",
                        "Month": "$$Text.Format('{0:MM}',WindowStart)",
                        "Day": "$$Text.Format('{0:dd}',WindowStart)"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "policy": {
                    "concurrency": 1,
                    "executionPriorityOrder": "OldestFirst",
                    "retry": 2,
                    "timeout": "01:00:00"
                }
            }
        ]
    }
}
```

В разделе [Строки настраиваемых форматов даты и времени](https://msdn.microsoft.com/library/8kb3ddd4.aspx) описаны различные варианты форматирования, которые можно использовать (пример: гг и гггг). 

