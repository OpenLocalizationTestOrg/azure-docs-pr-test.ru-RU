---
title: "aaaScheduling и выполнения с помощью фабрики данных | Документы Microsoft"
description: "Сведения об аспектах планирования и исполнения в модели приложений фабрики данных Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 088a83df-4d1b-4ac1-afb3-0787a9bd1ca5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 6114dd4896f5537c789c3b632fb90e501b694285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="data-factory-scheduling-and-execution"></a>Планирование и исполнение с использованием фабрики данных
В этой статье описываются hello планированием и выполнением аспекты модели приложения hello фабрики данных Azure. В этой статье предполагается, что вам известны основные понятия модели приложений фабрики данных: действия, конвейеры, связанные службы и наборы данных. Основные понятия фабрики данных Azure см. следующие статьи hello.

* [Введение tooData фабрики](data-factory-introduction.md)
* [Конвейеры](data-factory-create-pipelines.md)
* [Наборы данных](data-factory-create-datasets.md) 

## <a name="start-and-end-times-of-pipeline"></a>Время начала и окончания конвейера
Конвейер работает только в период активности, то есть между временем **начала** и **окончания**. Не выполняется раньше времени начала hello или после времени окончания hello. Конвейер hello приостановлена, не выполняется независимо от времени его начала и окончания. Для toorun конвейера он должен быть не приостановлен. В определении конвейера hello найти эти параметры (начала, окончания, приостановки): 

```json
"start": "2017-04-01T08:00:00Z",
"end": "2017-04-01T11:00:00Z"
"isPaused": false
```

Дополнительные сведения об этих свойствах см. в статье [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md). 


## <a name="specify-schedule-for-an-activity"></a>Указание расписания для действия
Это не hello конвейера, который выполняется. Это в конвейере hello hello операций, выполняемых в hello весь контекст hello конвейера. Можно указать повторяющееся расписание для действия с помощью hello **планировщика** раздел действия JSON. Например можно запланировать действие toorun каждый час следующим образом:  

```json
"scheduler": {
    "frequency": "Hour",
    "interval": 1
},
```

Как показано на следующая диаграмме hello, задать расписание для действия создает ряд переворачивающиеся окна с в hello конвейера начала времени и завершения. "Переворачивающиеся" окна — это ряд не перекрывающихся и не соприкасающихся интервалов фиксированного размера. Эти логические стыкующиеся окна для действия называются **окнами действия**.

![Пример планировщика действий](media/data-factory-scheduling-and-execution/scheduler-example.png)

Hello **планировщика** свойство для действия является необязательным. При указании этого свойства должно соответствовать периодичностью hello, заданные в определении hello выходного набора данных для действия "hello". В настоящее время выходной набор данных — того, какие диски hello расписания. Таким образом необходимо создать выходной набор данных, даже если hello не создает никаких выходных данных. 

## <a name="specify-schedule-for-a-dataset"></a>Указание расписания для набора данных
У каждого действия в конвейере фабрики данных может быть несколько входных **наборов данных** или же ни одного, и каждое действие может производить один или несколько выходных наборов данных. Для действия, можно указать hello последовательность в какие hello доступна входных данных или hello выходных данных производится с помощью hello **доступности** раздела hello определения наборов данных. 

**Частота** в hello **доступности** раздел указывает единицу времени hello. Hello разрешенные значения для частоты: минута, час, день, неделю и месяц. Hello **интервал** свойство раздела доступности hello указывает коэффициент периодичности. Например: Если hello частота имеет значение tooDay и интервал too1 для выходной набор данных, hello выходных данных создаются ежедневно. Если задать частоту hello минуты, рекомендуется установить интервал toono hello меньше 15. 

В следующем примере hello, входные данные hello доступен каждый час и hello выходных данных создается каждый час (`"frequency": "Hour", "interval": 1`). 

**Входной набор данных:** 

```json
{
    "name": "AzureSqlInput",
    "properties": {
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```


**Выходной набор данных**

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "published": false,
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mypath/{Year}/{Month}/{Day}/{Hour}",
            "format": {
                "type": "TextFormat"
            },
            "partitionedBy": [
                { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
                { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" }}
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

В настоящее время **дисков hello выходного набора данных расписания**. Другими словами hello расписанию, указанному для hello выходной набор данных — используется toorun действия во время выполнения. Таким образом необходимо создать выходной набор данных, даже если hello не создает никаких выходных данных. Если действие hello не принимает никаких входных данных, можно пропустить создание hello входного набора данных. 

В следующих hello конвейера определению hello **планировщика** свойство — используется toospecify расписание для действия "hello". Это необязательное свойство. В настоящее время hello расписание для действия "hello" должно соответствовать hello расписанием, заданным для hello выходного набора данных.
 
```json
{
    "name": "SamplePipeline",
    "properties": {
        "description": "copy activity",
        "activities": [
            {
                "type": "Copy",
                "name": "AzureSQLtoBlob",
                "description": "copy activity",
                "typeProperties": {
                    "source": {
                        "type": "SqlSource",
                        "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 100000,
                        "writeBatchTimeout": "00:05:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureSQLInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                }
            }
        ],
        "start": "2017-04-01T08:00:00Z",
        "end": "2017-04-01T11:00:00Z"
    }
}
```

В этом примере выполняется действие hello каждый час между hello время начала и окончания hello конвейера. выходные данные Hello создается каждый час для windows трех часов (8: 00 - 9 AM, 9: 00 - 10: 00 и 10 AM - 11: 00). 

Каждая единица данных, потребляемых или создаваемых запуском действия, называется **срезом данных**. Следующая схема Hello показан пример действия с одного входного набора данных и один выходной набор данных. 

![Планировщик доступности](./media/data-factory-scheduling-and-execution/availability-scheduler.png)

Hello показан hello каждый час срезы данных для hello входной и выходной набор данных. Hello диаграмме показаны три входные срезы, готовых к обработке. Действие Hello 10 11 AM идет, формирующего hello 10 11 AM вывода среза. 

Можно получить доступ к hello интервал времени, связанные с текущей срез hello в наборе данных hello JSON с помощью переменных: [SliceStart](data-factory-functions-variables.md#data-factory-system-variables) и [SliceEnd](data-factory-functions-variables.md#data-factory-system-variables). Аналогичным образом можно получить доступ к hello интервал времени, связанные с окном действия с помощью hello WindowStart и WindowEnd. расписание Hello действия должно соответствовать расписание hello hello выходного набора данных для действия "hello". Таким образом, hello SliceStart и SliceEnd значения являются hello же, как значения WindowStart и WindowEnd соответственно. Дополнительные сведения об этих переменных см. в статье [Фабрика данных Azure — функции и системные переменные](data-factory-functions-variables.md#data-factory-system-variables).  

Эти переменные можно использовать для различных целей в действии JSON. Например, их можно использовать tooselect данные из входного и выходного наборов данных, представляющий временного ряда данных (например: 8 AM too9 AM). В этом примере также используется **WindowStart** и **WindowEnd** tooselect необходимые данные для действия, запуска и скопируйте его tooa большой двоичный объект с hello соответствующие **folderPath**. Hello **folderPath** является параметризованный toohave отдельную папку для каждого часа.  

В предыдущих пример hello hello hello расписанием, заданным для входного и выходного наборов данных одинаковыми (каждый час). Если входной набор данных для действия "hello" hello другой частотой сказать каждые 15 минут, hello действие, которое создает этот выходной набор данных по-прежнему выполняется один раз в час как hello выходной набор данных является того, какие диски hello расписание действий. Дополнительные сведения см. в разделе [Моделирование наборов данных с разной частотой](#model-datasets-with-different-frequencies).

## <a name="dataset-availability-and-policies"></a>Доступность набора данных и политики
Вы уже узнали использования hello частоту и интервал свойств в разделе доступности hello определения набора данных. Существует несколько свойств, которые влияют на hello планирования и выполнения действия. 

### <a name="dataset-availability"></a>Доступность набора данных 
Hello следующей таблице описаны свойства можно использовать в hello **доступности** раздела:

| Свойство | Описание | Обязательно | значение по умолчанию |
| --- | --- | --- | --- |
| frequency |Указывает единицу времени hello для производственного среза набора данных.<br/><br/><b>Поддерживаемые значения</b>: Minute, Hour, Day, Week, Month. |Да |Нет данных |
| interval |Задает множитель для частоты.<br/><br/>«Интервал частоты x» определяет, как часто hello срезов.<br/><br/>Если требуется hello срез в час toobe набора данных, задайте <b>частоты</b> слишком<b>час</b>, и <b>интервал</b> слишком<b>1</b>.<br/><br/><b>Примечание</b>: Если указать для частоты минуты, рекомендуется установить интервал toono hello меньше 15 |Да |Нет данных |
| style |Указывает, является ли hello срезов в hello начала и окончания интервала hello.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul><br/><br/>Если частота имеет значение tooMonth и задан стиль tooEndOfInterval, hello срезов на hello последний день месяца. Если задан tooStartOfInterval стиль hello, hello срезов на hello первый день месяца.<br/><br/>Если частота имеет значение tooDay и задан стиль tooEndOfInterval, hello срезов в hello последний час дня hello.<br/><br/>Если частота имеет значение tooHour и задан стиль tooEndOfInterval, hello срезов в конце hello hello час. Например для среза для периода с 13: 00 до 14: 00, hello срез создается в 14: 00. |Нет |EndOfInterval |
| anchorDateTime |Определяет hello абсолютное положение во времени, используемые границы фрагмента планировщика toocompute набора данных. <br/><br/><b>Примечание</b>: Если hello AnchorDateTime есть части даты, которые являются более детализированными, чем частота hello, а затем hello более детализированные части игнорируются. <br/><br/>Например, если hello <b>интервал</b> — <b>каждый час</b> (частота: час и интервал: 1) и hello <b>AnchorDateTime</b> содержит <b>минуты и секунды</b>, затем hello <b>минуты и секунды</b> части hello AnchorDateTime игнорируются. |Нет |01/01/0001 |
| offset |Интервал времени, по которой hello Сдвиг начала и окончания всех фрагментов набора данных. <br/><br/><b>Примечание</b>: Если указаны значения для anchorDateTime и offset, результатом hello является shift hello вместе. |Нет |Нет данных |

### <a name="offset-example"></a>Пример смещения
По умолчанию создание ежедневных срезов (`"frequency": "Day", "interval": 1`) начинается в 00:00 (UTC). Время hello начала времени toobe 6: 00 UTC вместо этого, установите hello смещение, как показано в следующий фрагмент кода hello: 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a>Пример для anchorDateTime
В следующем примере hello hello набора данных создаются каждые 23 часа. Hello первого сегмента начинается hello времени, заданного параметром anchorDateTime hello, для которого задано слишком`2017-04-19T08:00:00` (в формате UTC).

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a>Пример для Offset и Style
Hello следующий набор данных представляет собой ежемесячные набор данных и выводятся на 3-й день каждого месяца в 8:00 (`3.08:00:00`):

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

### <a name="dataset-policy"></a>Политика набора данных
Набор данных может иметь определенные политики проверки, указывающее, как hello данные, сформированные при выполнении среза можно проверить, прежде чем он будет готов к использованию. В таких случаях после завершения выполнения, срез hello состояние среза вывода hello изменяется слишком**ожидания** с подсостояния из **проверки**. После проверки фрагменты hello изменяет состояние среза hello слишком**готовности**. Если было произведено срез данных, но не прошел проверку hello, запуске действия для подчиненные диаграммы, которые зависят от этого среза, не обрабатываются. [Мониторинг и управление ими конвейеры](data-factory-monitor-manage-pipelines.md) деле hello различные состояния срезы данных в фабрике данных.

Hello **политики** раздела в определении набора данных, определяет условия hello или необходимо выполнить условие hello, hello фрагментов набора данных. Hello следующей таблице описаны свойства можно использовать в hello **политики** раздела:

| Имя политики | Описание | Применить слишком| Обязательно | значение по умолчанию |
| --- | --- | --- | --- | --- |
| minimumSizeMB | Проверяет, данные hello в **BLOB-объектов Azure** соответствует hello требования минимальный размер (в мегабайтах). |Большой двоичный объект Azure |Нет |Нет данных |
| minimumRows | Проверяет, данные hello в **базы данных Azure SQL** или **таблицы Azure** содержит hello минимальное количество строк. |<ul><li>База данных SQL Azure</li><li>таблице Azure</li></ul> |Нет |Нет данных |

#### <a name="examples"></a>Примеры
**minimumSizeMB:**

```json
"policy":

{
    "validation":
    {
        "minimumSizeMB": 10.0
    }
}
```

**minimumRows:**

```json
"policy":
{
    "validation":
    {
        "minimumRows": 100
    }
}
```

Дополнительные сведения о наборах данных см. в статье [Наборы данных в фабрике данных Azure](data-factory-create-datasets.md). 

## <a name="activity-policies"></a>Политики действий
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

Дополнительные сведения см. в статье [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md). 

## <a name="parallel-processing-of-data-slices"></a>Параллельная обработка срезов данных
Можно задать hello дату начала для конвейера hello в последние hello. При этом фабрики данных автоматически вычисляет все срезы в прошлом hello (заливки фона) и начинает обработку их. Например: Если создать конвейер с датой начала 2017 г-04-01 и hello текущая дата — 2017 г-04-10. Если последовательность hello объекта hello выходной набор данных — каждый день, а затем фабрики данных начинает обработку всех фрагментов hello из 2017 г-04-01 too2017-04-09 немедленно так, как дата начала hello находится в последние hello. срез Hello из 2017 г-04-10 не обрабатывается еще так как значение hello свойства стиля раздела доступности hello EndOfInterval по умолчанию. Hello старые срез обрабатывается сначала по умолчанию hello executionPriorityOrder равен OldestFirst. Описание свойства style hello см. [доступности набора данных](#dataset-availability) раздела. Описание раздела executionPriorityOrder hello см. в разделе hello [политики действий](#activity-policies) раздела. 

Можно настроить toobe срезы данных заполнением назад параллельно обрабатываемых параметр hello **параллелизма** свойство в hello **политики** раздел действие hello JSON. Это свойство определяет hello число параллельных выполнений действия может произойти на различных срезах. значение свойства hello параллелизма по умолчанию Hello-1. Таким образом, по умолчанию одновременно обрабатывается один срез. Hello максимальное значение равно 10. Конвейера, когда потребуется toogo через большого набора данных, наличие большего значения параллелизма приводит к ускорению обработки данных hello. 

## <a name="rerun-a-failed-data-slice"></a>Повторное выполнение невыполненного среза данных
При возникновении ошибки во время обработки срез данных, можно выяснить причину сбоя обработки hello среза с помощью Azure портала колонках или монитора и управления приложения. Дополнительные сведения см. в статьях [Мониторинг конвейеров фабрики данных Azure и управление ими](data-factory-monitor-manage-pipelines.md) и [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью нового приложения по мониторингу и управлению](data-factory-monitor-manage-app.md).

Рассмотрим следующий пример, в котором показаны два действия hello. Activity1 и Activity2. Activity1 использует срез Dataset1 и создает срез Dataset2, который используется в качестве ввода Activity2 tooproduce срез hello окончательного набора.

![Срез, в котором произошла ошибка](./media/data-factory-scheduling-and-execution/failed-slice.png)

Hello схемы видно, что из трех последних срезов, произошла ошибка производитель hello 9 10 AM срез для Dataset2. Фабрика данных автоматически отслеживает зависимости для набора данных для ряда времени hello. В результате он не запускается при выполнении среза подчиненных 9 10 AM hello hello действия.

Средства мониторинга и управления фабрики данных позволяют toodrill в журналы диагностики hello для hello неудачных срез tooeasily поиска hello корневой вызвать hello проблемы и устранить ее. После устранения проблемы hello можно легко запустить срез неудачных hello tooproduce при выполнении действия hello. Дополнительные сведения о том, как toorerun и понять переходы состояний для срезов данных см. в разделе [мониторинг и управление конвейеров с помощью Azure портала колонках](data-factory-monitor-manage-pipelines.md) или [управление и мониторинг приложения](data-factory-monitor-manage-app.md).

После повторного запуска hello 9 10 AM среза для **Dataset2**, фабрики данных запускает hello зависимых среза hello 9 10 по выполнению hello окончательного набора.

![Повторный запуск среза, в котором произошла ошибка](./media/data-factory-scheduling-and-execution/rerun-failed-slice.png)

## <a name="multiple-activities-in-a-pipeline"></a>Несколько действий в конвейере
Конвейер может содержать сразу несколько действий. При наличии нескольких действий в конвейере и hello выходных данных действия не являются входными данными другого действия, если готовых срезы входные данные для действия hello hello действия могут выполняться параллельно.

Вы можно соединить в цепочку двух действий (Запуск одного действия другому), hello входной набор данных, из hello других действий, включив hello выходной набор данных из одного действия. Hello операции могут быть в hello же конвейера или в разных конвейеров. Hello второе действие выполняется, только в том случае, когда hello сначала один завершается успешно.

Например рассмотрим следующий случай, где содержатся два действия в конвейере hello:

1. Действие A1, для которого требуется внешний входной набор данных D1. Оно создает выходной набор данных D2.
2. Действие A2, для которого требуется ввод из набора данных D2. Оно создает выходной набор данных D3.

В этом сценарии, действия A1 и A2 в hello же конвейера. Действие Hello запуска A1 hello внешних данных и частоты запланированных hello доступности достигается при. Hello действия A2 выполняется, когда hello запланированных фрагменты из D2 становятся доступными и hello частоты запланированная доступность достигается. В случае ошибки в одном из фрагментов hello в наборе данных D2 A2 не выполняется для этого среза пока она не станет доступным.

Здравствуйте, представление диаграммы с помощью обоих действий в hello что же конвейера выглядит следующим образом hello, следующая схема:

![Цепочки действий в hello же конвейера](./media/data-factory-scheduling-and-execution/chaining-one-pipeline.png)

Как упоминалось ранее, действия hello могут находиться в разных конвейеров. В этом случае представление диаграммы hello выглядит следующим образом hello следующие схемы.

![Построение цепочки действий в двух конвейерах](./media/data-factory-scheduling-and-execution/chaining-two-pipelines.png)

. В разделе hello [скопируйте последовательно](#copy-sequentially) раздела приложение hello в качестве примера.

## <a name="model-datasets-with-different-frequencies"></a>Моделирование наборов данных с разной частотой
В образцах hello hello частоты для входного и выходного наборов данных и hello расписание окно действия были hello же. В некоторых сценариях требуется hello возможность tooproduce вывода с периодичностью, отличный от частоты hello один или несколько входных данных. Фабрика данных поддерживает моделирование таких сценариев.

### <a name="sample-1-produce-a-daily-output-report-for-input-data-that-is-available-every-hour"></a>Пример 1. Создание ежедневного выходного отчета по входным данным, которые доступны каждый час
Рассмотрим сценарий, где имеются входные данные измерений датчиков, доступные каждый час в хранилище BLOB-объектов Azure. Вы хотите tooproduce ежедневный отчет о статистических со статистическими данными, таких как среднее, максимум и минимум hello день с [действие hive в фабрике данных](data-factory-hive-activity.md).

Смоделировать этот сценарий с помощью фабрики данных можно приведенным ниже способом.

**Входной набор данных**

файлы будут удалены в папке hello для заданного дня hello каждый час входной Hello. Для входных данных устанавливается **почасовая** доступность (frequency: Hour, interval: 1).

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
**Выходной набор данных**

Один выходной файл создается каждый день в папке hello день. Для выходных данных устанавливается **ежедневная** доступность (frequency: Day, interval: 1).

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Действие: действие Hive в конвейере**

скрипт hive Hello принимает соответствующие hello *DateTime* сведения в качестве параметров, использующих hello **WindowStart** переменной, как показано в следующий фрагмент кода hello. скрипт hive Hello использует эти данные переменной tooload hello из требуемой папки hello день hello и выполнить выход hello toogenerate hello статистической обработки.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
        {
            "name": "SampleHiveActivity",
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
            "linkedServiceName": "HDInsightLinkedService",
            "type": "HDInsightHive",
            "typeProperties": {
                "scriptPath": "adftutorial\\hivequery.hql",
                "scriptLinkedService": "StorageLinkedService",
                "defines": {
                    "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
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

Hello следующей схеме показан сценарий hello с точки зрения зависимостей данных.

![Зависимость данных](./media/data-factory-scheduling-and-execution/data-dependency.png)

срез Hello выходные данные за каждый день в зависит от 24 часам фрагменты из входного набора данных. Вычисляет фабрики данных, эти зависимости автоматически, изучив hello фрагменты входные данные, попадающие в hello же период времени как hello полученных toobe фрагмент выходных данных. Если какой-либо входные срезы hello 24 не доступны, фабрики данных ожидает готовности перед началом выполнения действия день hello toobe ввода фрагмента hello.

### <a name="sample-2-specify-dependency-with-expressions-and-data-factory-functions"></a>Пример 2. Указание зависимости с использованием выражений и функций фабрики данных
Рассмотрим другой сценарий. Предположим, есть действие Hive, которое обрабатывает два входных набора данных. В одном из этих наборов новые данные появляются ежедневно, а в другом — раз в неделю. Предположим, что требуется, чтобы toodo соединение между двумя входными значениями hello и формируют выходные данные каждый день.

Hello простой подход, в котором фабрики данных автоматически решает, правый вход hello срезы tooprocess путем выравнивания вывода toohello срез данных времени периода не работает.

Необходимо указать, по при выполнении каждого действия hello фабрики данных следует использовать срез данных прошлой недели для еженедельного входного набора данных hello. Используются функции фабрики данных Azure, как показано в следующих tooimplement фрагмент кода hello это поведение.

**Входной набор 1: большой двоичный объект Azure**

Hello сначала ввода hello BLOB-объектов Azure обновляется ежедневно.

```json
{
  "name": "AzureBlobInputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Входной набор 2: большой двоичный объект Azure**

Input2 — hello BLOB-объектов Azure обновляется раз в неделю.

```json
{
  "name": "AzureBlobInputWeekly",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 7
    }
  }
}
```

**Выходной набор данных: большой двоичный объект Azure**

Один выходной файл создается в папке hello каждый день за день hello. Доступность выходных данных задано слишком**день** (частота: день, интервал: 1).

```json
{
  "name": "AzureBlobOutputDaily",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/{Year}/{Month}/{Day}/",
      "partitionedBy": [
        { "name": "Year", "value": {"type": "DateTime","date": "SliceStart","format": "yyyy"}},
        { "name": "Month","value": {"type": "DateTime","date": "SliceStart","format": "MM"}},
        { "name": "Day","value": {"type": "DateTime","date": "SliceStart","format": "dd"}}
      ],
      "format": {
        "type": "TextFormat"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Действие: действие Hive в конвейере**

Действие hive Hello принимает hello двух входных значений и создает выходные данные фрагмента каждый день. Можно указать toodepend срез выходные данные каждый день на hello ввода фрагмента предыдущей недели для еженедельного входных данных следующим образом.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2015-01-01T08:00:00",
    "end":"2015-01-01T11:00:00",
    "description":"hive activity",
    "activities": [
      {
        "name": "SampleHiveActivity",
        "inputs": [
          {
            "name": "AzureBlobInputDaily"
          },
          {
            "name": "AzureBlobInputWeekly",
            "startTime": "Date.AddDays(SliceStart, - Date.DayOfWeek(SliceStart))",
            "endTime": "Date.AddDays(SliceEnd,  -Date.DayOfWeek(SliceEnd))"  
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutputDaily"
          }
        ],
        "linkedServiceName": "HDInsightLinkedService",
        "type": "HDInsightHive",
        "typeProperties": {
          "scriptPath": "adftutorial\\hivequery.hql",
          "scriptLinkedService": "StorageLinkedService",
          "defines": {
            "Year": "$$Text.Format('{0:yyyy}',WindowStart)",
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

В статье [Фабрика данных Azure — функции и системные переменные](data-factory-functions-variables.md) приведен список функций и системных переменных, поддерживаемых фабрикой данных.

## <a name="appendix"></a>Приложение

### <a name="example-copy-sequentially"></a>Пример: последовательное копирование
Он является возможные toorun несколько операций копирования друг за другом в виде последовательных/упорядочены. Например может иметь две копии действий в конвейере (CopyActivity1 и CopyActivity2) с hello после ввода данных выходные наборы данных:   

CopyActivity1

Входные данные: Dataset. Выходные данные: Dataset2.

CopyActivity2

Входные данные: Dataset2.  Выходные данные: Dataset3.

CopyActivity2 будет выполняться только в том случае, если успешно выполнена hello CopyActivity1 и Dataset2.

Ниже приведен пример hello конвейера JSON.

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob1ToBlob2",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset3"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob2ToBlob3",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2016-08-25T01:00:00Z",
        "end": "2016-08-25T01:00:00Z",
        "isPaused": false
    }
}
```

Обратите внимание, что в примере hello hello выходного набора данных hello первой операции копирования (Dataset2) указан в качестве входного для второго действия hello. Таким образом hello второе действие выполняется только в том случае, когда hello выходной набор данных из первого действия hello готов.  

В примере hello CopyActivity2 может иметь различные данные, такие как Dataset3, но указать Dataset2 как входной tooCopyActivity2, чтобы действие hello не выполняется до завершения CopyActivity1. Например:

CopyActivity1

Входные данные: Dataset1. Выходные данные: Dataset2.

CopyActivity2

Входные данные: Dataset3, Dataset2. Выходные данные: Dataset4.

```json
{
    "name": "ChainActivities",
    "properties": {
        "description": "Run activities in sequence",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "PreserveHierarchy",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset1"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset2"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlobToBlob",
                "description": "Copy data from a blob tooanother"
            },
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "Dataset3"
                    },
                    {
                        "name": "Dataset2"
                    }
                ],
                "outputs": [
                    {
                        "name": "Dataset4"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00"
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "CopyFromBlob3ToBlob4",
                "description": "Copy data from a blob tooanother"
            }
        ],
        "start": "2017-04-25T01:00:00Z",
        "end": "2017-04-25T01:00:00Z",
        "isPaused": false
    }
}
```

Обратите внимание, что в примере hello двух входных наборов данных указаны для второго действия копирования hello. Если указано несколько входов, только hello первого входного набора данных используется для копирования данных, но другие наборы данных используются в качестве зависимости. CopyActivity2 будет начинаться только после hello выполняются следующие условия:

* Действие CopyActivity1 успешно завершено, и набор данных Dataset2 доступен. Этот набор данных не используется при копировании данных tooDataset4. Он используется только как зависимость для планирования CopyActivity2.   
* Набор данных Dataset3 доступен. Этот набор данных представляет данные hello, скопированный toohello назначения. 
