---
title: "наборы данных aaaCreate в фабрике данных Azure | Документы Microsoft"
description: "Узнайте, как смещение toocreate наборов данных в фабрике данных Azure, с примеры, использующие такие свойства, как и anchorDateTime."
keywords: "создание набора данных, пример набора данных, пример offset"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 0614cd24-2ff0-49d3-9301-06052fd4f92a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: shlo
ms.openlocfilehash: 181859ed250595d756df73e9ebcac08d9e7184c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="datasets-in-azure-data-factory"></a>Наборы данных в фабрике данных Azure
В этой статье описывается, какие бывают наборы данных, каким образом они определяются в формате JSON, а также как они используются в конвейерах фабрики данных Azure. Он предоставляет подробные сведения о каждом разделе (например, структуру, доступности и политики) в определение JSON набора данных hello. Hello статье также приводятся примеры использования hello **смещение**, **anchorDateTime**, и **стиль** свойства в определении JSON набора данных.

> [!NOTE]
> Новый tooData фабрики, в разделе [tooAzure введение фабрики данных](data-factory-introduction.md) Общие сведения. Если у вас практический опыт работы с Создание фабрик данных, можно получить, лучше понять путем чтения hello [учебника преобразования данных](data-factory-build-your-first-pipeline.md) и hello [учебника перемещения данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md). 

## <a name="overview"></a>Обзор
Фабрика данных может иметь один или несколько конвейеров. **Конвейер** — это логическая группа **действий**, которые вместе выполняют задачу. Hello действий в конвейере определить tooperform действия на данные. Например можно использовать копирование данных toocopy действия из локального SQL Server tooAzure хранилища больших двоичных объектов. Затем можно использовать действия Hive, которое запускает сценарий Hive на данных tooprocess кластера Azure HDInsight из tooproduce выходные данные больших двоичных объектов хранилища данных. Наконец можно использовать второй копии действия toocopy hello вывода данных tooAzure хранилище данных SQL, поверх какие бизнес-аналитики (BI), отчетов, решения создаются. Дополнительные сведения о конвейерах и действиях см. в статье [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md).

У каждого действия может быть несколько входных **наборов данных** или же ни одного, и каждое действие может производить один или несколько выходных наборов данных. Входной набор данных представляет hello входных данных для действия в конвейере hello, а выходной набор данных представляет hello выходные данные для действия "hello". Наборы данных представляют данные в разных хранилищах, например в таблицах, файлах, папках и документах. Например набор данных больших двоичных объектов Azure задает контейнер больших двоичных объектов hello и папку в хранилище больших двоичных объектов, из которого hello конвейера следует считывать данные hello. 

Перед созданием набора данных, создать **связанная служба** toolink фабрики данных toohello хранения данных. Связанные службы очень похожи на строки подключения, которые укажите сведения о подключении hello, необходимые для ресурсов tooexternal tooconnect фабрики данных. Наборы данных идентификации данных в пределах hello связаны хранилища данных, например таблиц SQL, файлы, папки и документы. Например хранилище Azure связан ссылки на службу фабрики данных toohello учетной записи хранилища. Набор данных больших двоичных объектов Azure представляет контейнер больших двоичных объектов hello и hello папку, содержащую toobe входного BLOB-объектов hello обработки. 

Ниже приведен пример сценария. toocopy данные из базы данных SQL tooa хранилища Blob, создать две связанные службы: служба хранилища Azure и базы данных SQL Azure. Затем создайте два набора данных: набор данных больших двоичных объектов Azure (которое означает toohello связанной службой хранилища Azure) и набор данных таблиц SQL Azure (которое означает службы toohello связана база данных SQL Azure). Здравствуйте, служба хранилища Azure и базы данных SQL Azure связанные службы содержат строки подключения, фабрики данных используется среда выполнения tooconnect tooyour хранилища Azure и базы данных SQL Azure, соответственно. набор данных больших двоичных объектов Azure Hello указывает контейнер больших двоичных объектов hello и больших двоичных объектов папку, содержащую hello входного BLOB-объектов в хранилище BLOB-объектов. набор данных таблиц SQL Azure Hello указывает, что таблицы SQL hello в данных hello toowhich базы данных SQL является toobe копируются.

Hello следующей схеме показаны связи hello между конвейера, действия, набор данных и связанной службы в фабрике данных. 

![Связь между конвейером, действием, набором данных и связанными службами](media/data-factory-create-datasets/relationship-between-data-factory-entities.png)

## <a name="dataset-json"></a>JSON набора данных
Набор данных в фабрике данных определяется в формате JSON, как показано ниже.

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
| name |Имя набора данных hello. Правила именования для фабрики данных Azure описаны [здесь](data-factory-naming-rules.md) . |Да |Нет данных |
| type |Тип набора данных hello. Укажите один из типов hello, поддерживаемые фабрикой данных (например: AzureBlob, AzureSqlTable). <br/><br/>Дополнительные сведения см. в разделе [Тип набора данных](#Type). |Да |Нет данных |
| structure |Схема набора данных hello.<br/><br/>Дополнительные сведения см. в разделе [Структура набора данных](#Structure). |Нет |Нет данных |
| typeProperties | свойства типа Hello различны для каждого типа (например: BLOB-объектов Azure, таблице Azure SQL). Сведения о hello поддерживается типов и их свойств. в разделе [тип набора данных](#Type). |Да |Нет данных |
| external | Логический флаг toospecify ли набор данных явно созданные конвейере фабрики данных или нет. Если текущий конвейер hello не создается hello входного набора данных для действия, значение этого флага tootrue. Установите этот флаг tootrue для hello входного набора данных hello первое действие в конвейере hello.  |Нет |нет |
| availability | Определяет hello обработки окна (например, раз в час или каждый день) или hello Фрагментирование модели для производства hello набора данных. Каждая единица данных, потребляемых и создаваемых запуском действия, называется срезом данных. Если доступность hello выходной набор данных является набор toodaily (частота — день, интервал - 1), срез создается ежедневно. <br/><br/>Дополнительные сведения см. в разделе [Доступность набора данных](#Availability). <br/><br/>Сведения о наборе данных hello Фрагментирование модели, см. hello [планирования и выполнения](data-factory-scheduling-and-execution.md) статьи. |Да |Нет данных |
| policy |Определяет условия hello или hello условие, которое необходимо выполнить все фрагменты hello набора данных. <br/><br/>Дополнительные сведения см. в разделе hello [наборе данных политики](#Policy) раздела. |Нет |Нет данных |

## <a name="dataset-example"></a>Пример набора данных
В следующем примере hello, набор данных hello представляет таблицу с именем **MyTable** в базе данных SQL.

```json
{
    "name": "DatasetSample",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties":
        {
            "tableName": "MyTable"
        },
        "availability":
        {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

Обратите внимание hello после точки.

* **Тип** имеет значение tooAzureSqlTable.
* **tableName** свойство type (тип определенного tooAzureSqlTable) имеет значение tooMyTable.
* **linkedServiceName** ссылается tooa связанной службы типа AzureSqlDatabase, которая определена в следующем фрагменте кода JSON hello. 
* **частота доступности** задано tooDay, и **интервал** имеет значение too1. Это означает, что набор данных, hello срез создается ежедневно.  

**AzureSqlLinkedService** определяется следующим образом:

```json
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>@<servername>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

В hello предшествующий фрагмент JSON:

* **Тип** имеет значение tooAzureSqlDatabase.
* **connectionString** базы данных SQL tooa tooconnect сведения указывает тип свойства.  

Как видите, hello связанной службы определяет как база данных SQL tooa tooconnect. Hello набор данных определяет, какие таблицы используются как входные и выходные данные для действия "hello" в конвейере.   

> [!IMPORTANT]
> Если набор данных создается конвейером hello, он должен быть помечен как **внешних**. Этот параметр применяется обычно tooinputs первого действия в конвейере.   


## <a name="Type"></a>Тип набора данных
Тип Hello hello набора данных зависит от hello хранилища данных, которые можно использовать. См. в следующей таблице список хранилищ данных, поддерживаемые фабрикой данных hello. Нажмите кнопку toolearn хранилище данных как toocreate связанной службы и набор данных для их хранения.

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Хранилища данных с * могут быть локальными или в IaaS Azure. Эти хранилища данных требуется tooinstall [шлюз управления данными](data-factory-data-management-gateway.md).

В примере в предыдущем разделе hello hello hello типа hello набора данных задается слишком**AzureSqlTable**. Аналогичным образом, для набора данных больших двоичных объектов Azure, типа hello hello набора данных задается слишком**AzureBlob**, как показано в следующих JSON hello:

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

## <a name="Structure"></a>Структура набора данных
Hello **структуры** раздел является необязательным. Он определяет схему hello hello набора данных, содержащий коллекцию имена и типы данных столбцов. Используется hello структуры раздел tooprovide сведений о типах, используемых tooconvert типы и сопоставлять столбцы из hello источник toohello назначения. В следующем примере hello, hello набор данных содержит три столбца: `slicetimestamp`, `projectname`, и `pageviews`. Они имеют типы String, String и Decimal соответственно.

```json
structure:  
[
    { "name": "slicetimestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

Каждый столбец в структуре hello содержит hello следующие свойства:

| Свойство | Описание | Обязательно |
| --- | --- | --- |
| name |Имя столбца hello. |Да |
| type |Тип данных столбца hello.  |Нет |
| culture |. Toobe языка и региональных параметров на основе платформы .NET, используемый при hello тип является типом .NET: `Datetime` или `Datetimeoffset`. по умолчанию Hello — `en-us`. |Нет |
| свойства |Форматировать toobe строки, использовавшейся hello тип является типом .NET: `Datetime` или `Datetimeoffset`. |Нет |

Hello следующие рекомендации помогут определить, когда tooinclude структуры сведения и какие tooinclude в hello **структуры** раздела.

* **Для источников данных, структурированный**, укажите раздел структуры hello только в том случае, если требуется сопоставить исходные столбцы toosink столбцы, и их имена не являются одинаковыми hello. Данный тип источника структурированных данных хранит данные схемы и сведения о типе и сами данные hello. Примерами структурированных источников данных являются SQL Server, Oracle и таблица Azure. 
  
    Как сведения о типе для структурированными источниками данных, при включении раздел структуры hello не должно содержать сведения о типе.
* **Для схемы на источниках чтения данных (в частности, хранилище Blob)**, вы можете toostore данных без сохранения любой схемы или типа данных с использованием данных hello. Для этих типов источников данных включают структуры при необходимости столбцы toosink toomap исходные столбцы. Также включите структуры, когда hello набора данных включает входные данные для операции копирования, типы данных из исходного набора данных должны быть типы преобразованный toonative для приемника hello. 
    
    Фабрика данных поддерживает следующие значения для предоставления информации о типах в структуре hello: **Int16, Int32, Int64, один, Double, Decimal, Byte [], логическое значение, строка, Guid, Datetime, Datetimeoffset и Timespan**. Это значения типов на основе .NET, совместимые со спецификацией CLS.

Фабрика данных автоматически выполняет преобразования типов при перемещении данных из источника данных в хранилище tooa приемник данных. 
  

## <a name="dataset-availability"></a>Доступность набора данных
Hello **доступности** в набор данных определяет hello окно обработки (например, каждый час, ежедневно или еженедельно) для набора данных hello. Дополнительные сведения об окнах действий см. в статье [Планирование и исполнение с использованием фабрики данных](data-factory-scheduling-and-execution.md).

Hello в следующем разделе доступности указывает, что hello выходного набора данных либо создается каждый час, или входного набора данных hello доступна каждый час:

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 1    
}
```

Если конвейер hello имеет hello после времени начала и окончания.  

```json
    "start": "2016-08-25T00:00:00Z",
    "end": "2016-08-25T05:00:00Z",
```

Hello выходной набор данных создается каждый час в конвейер hello время начала и окончания. Таким образом, в этом конвейере создаются пять срезов набора данных — по одному для каждого окна действий (с 12:00 до 01:00, с 01:00 до 02:00, с 02:00 до 03:00, с 03:00 до 04:00, с 04:00 до 05:00). 

Hello следующей таблице описываются свойства, которые можно использовать в разделе доступности hello.

| Свойство | Описание | Обязательно | значение по умолчанию |
| --- | --- | --- | --- |
| frequency |Указывает единицу времени hello для производственного среза набора данных.<br/><br/><b>Поддерживаемые значения</b>: Minute, Hour, Day, Week, Month. |Да |Нет данных |
| interval |Задает множитель для частоты.<br/><br/>«Интервал частоты x» определяет, как часто hello срезов. К примеру, если требуется hello срез в час toobe набора данных, можно установить <b>частоты</b> слишком<b>час</b>, и <b>интервал</b> слишком<b>1</b>.<br/><br/>Обратите внимание, что при указании **частоты** как **минуту**, необходимо задать toono hello интервал меньше 15. |Да |Нет данных |
| style |Указывает, является ли hello срезов hello начало или конец интервал приветствия.<ul><li>StartOfInterval</li><li>EndOfInterval</li></ul>Если **частоты** задано слишком**месяц**, и **стиль** задано слишком**EndOfInterval**, hello срез создается hello последний день месяца. Если **стиль** задано слишком**StartOfInterval**, hello срезов на hello первый день месяца.<br/><br/>Если **частоты** задано слишком**день**, и **стиль** задано слишком**EndOfInterval**, hello срезов в hello последний час дня hello.<br/><br/>Если **частоты** задано слишком**час**, и **стиль** задано слишком**EndOfInterval**, hello срезов в конце hello hello час. Например для среза для hello период 13: 00 - 14 по hello срез создается в 14: 00. |Нет |EndOfInterval |
| anchorDateTime |Определяет hello абсолютное позиционирование в времени, затраченного границ фрагмента dataset toocompute планировщика hello. <br/><br/>Обратите внимание, что если этот propoerty частей даты, которые являются более детализированными, чем hello указано частоты, hello более детализированные части игнорируются. Например, если hello **интервал** — **каждый час** (частота: час и интервал: 1) и hello **anchorDateTime** содержит **минуты и секунды**, затем hello минуты и секунды части **anchorDateTime** игнорируются. |Нет |01/01/0001 |
| offset |Интервал времени, по которой hello Сдвиг начала и окончания всех фрагментов набора данных. <br/><br/>Обратите внимание, что, если оба **anchorDateTime** и **смещение** указан, результат hello shift hello вместе. |Нет |Нет данных |

### <a name="offset-example"></a>Пример смещения
По умолчанию ежедневные срезы (`"frequency": "Day", "interval": 1`) создаются в 00.00 (в формате UTC). Время hello начала времени toobe 6: 00 UTC вместо этого, установите hello смещение, как показано в следующий фрагмент кода hello: 

```json
"availability":
{
    "frequency": "Day",
    "interval": 1,
    "offset": "06:00:00"
}
```
### <a name="anchordatetime-example"></a>Пример для anchorDateTime
В следующем примере hello hello набора данных создаются каждые 23 часа. Hello первого сегмента начинается hello времени, заданного параметром **anchorDateTime**, который установлен слишком`2017-04-19T08:00:00` (UTC).

```json
"availability":    
{    
    "frequency": "Hour",        
    "interval": 23,    
    "anchorDateTime":"2017-04-19T08:00:00"    
}
```

### <a name="offsetstyle-example"></a>Пример для offset и style
Hello следующий набор данных — ежемесячно и выводятся на hello 3-й день каждого месяца в 8:00 (`3.08:00:00`):

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "offset": "3.08:00:00", 
    "style": "StartOfInterval"
}
```

## <a name="Policy"></a>Политика наборов данных
Hello **политики** в определения набора данных hello определяет критерии hello или необходимо выполнить условие hello, hello фрагментов набора данных.

### <a name="validation-policies"></a>Политики проверки
| Имя политики | Описание | Применить слишком| Обязательно | значение по умолчанию |
| --- | --- | --- | --- | --- |
| minimumSizeMB |Проверяет, данные hello в **хранилища больших двоичных объектов Azure** соответствует hello требования минимальный размер (в мегабайтах). |Хранилище больших двоичных объектов Azure |Нет |Нет данных |
| minimumRows |Проверяет, данные hello в **базы данных Azure SQL** или **таблицы Azure** содержит hello минимальное количество строк. |<ul><li>База данных SQL Azure</li><li>таблицу Azure;</li></ul> |Нет |Нет данных |

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

### <a name="external-datasets"></a>Внешние наборы данных
Внешних наборов данных являются те, которые не создают выполнение конвейера в фабрике данных hello hello. Если набор данных hello помечен как **внешних**, hello **ExternalData** политики может быть определенный tooinfluence поведение hello доступности срез hello набора данных.

Если набор данных не создается фабрикой данных, он должен быть помечен как **external**. Этот параметр обычно применяется toohello вводов первое действие в конвейере, если не используется действие или цепочки конвейера.

| Имя | Описание | Обязательно | Значение по умолчанию |
| --- | --- | --- | --- |
| dataDelay |срез указано время Hello, toodelay hello проверьте на наличие hello hello внешних данных для hello. Например, вы можете отложить ежечасную проверку с помощью этого параметра.<br/><br/>Hello параметр применяется только toohello текущего времени.  Например если это 1:00 PM в данный момент, и это значение составляет 10 минут, проверки hello начинается в 13:10.<br/><br/>Обратите внимание, что этот параметр не влияет на срезы в прошлом hello. Срезы, у которых параметры **Slice End Time**  + и **dataDelay**  < **имеют значение раньше текущего времени**, обрабатываются без задержки.<br/><br/>Раз больше 23:59 часов указывается с помощью hello `day.hours:minutes:seconds` формат. Например toospecify 24 часа, не используйте 24:00:00. Вместо этого используйте 1.00:00:00. Значение 24:00:00 обозначает 24 дня (24.00:00:00). Чтобы задать 1 день и 4 часа, укажите 1:04:00:00. |Нет |0 |
| retryInterval |время ожидания Hello между сбоя и hello следующей попытки. Этот параметр применяется toopresent времени. Если предыдущие try hello не пройден, hello следующей попытки после hello **retryInterval** период. <br/><br/>Если это 1:00 PM прямо сейчас мы начинаем hello первой попытки. Если hello длительность toocomplete hello первой проверки — 1 минута и не удалось выполнить операцию hello, hello следующий Повтор — 1:00 + 1 минута (длительность) + 1 минута (интервал повтора) = 13:02:00. <br/><br/>Срезы в прошлом hello нет без задержки. Повторите попытку Hello происходит немедленно. |Нет |00:01:00 (1 минута) |
| retryTimeout |Здравствуйте, время ожидания для каждой повторной попытке.<br/><br/>Если это свойство имеет значение минут too10 hello проверки должна быть завершена в течение 10 минут. Если он занимает больше 10 минут tooperform hello проверки, hello повторите истечением времени ожидания.<br/><br/>Если все попытки для hello истечет время ожидания, hello среза помечается как **TimedOut**. |Нет |00:10:00 (10 минут) |
| maximumRetry |Hello время toocheck для обеспечения доступности hello hello внешних данных. Hello максимальное допустимое значение — 10. |Нет |3 |


## <a name="create-datasets"></a>Создание наборов данных
Наборы данных можно создать с помощью одного из указанных ниже инструментов или пакетов SDK. 

- Мастер копирования 
- Портал Azure
- Visual Studio
- PowerShell
- Шаблон диспетчера ресурсов Azure
- Интерфейс REST API
- .NET API

См. следующие учебники пошаговые инструкции по созданию конвейеры и наборов данных с помощью одного из этих средств или пакеты SDK hello.
 
- [Учебник. Создание первого конвейера для преобразования данных с помощью кластера Hadoop](data-factory-build-your-first-pipeline.md)
- [Руководство. Копирование данных из хранилища BLOB-объектов Azure в базу данных SQL с помощью фабрики данных](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)

После создания и развертывания конвейера можно управлять и отслеживать конвейеров с помощью hello Azure портала колонках или приложение hello наблюдения и управления. См. следующие разделы для получения пошаговых инструкций hello. 

- [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью портала Azure и PowerShell](data-factory-monitor-manage-pipelines.md)
- [Мониторинг и управление ими конвейеров с помощью приложения hello мониторинг и управление](data-factory-monitor-manage-app.md)


## <a name="scoped-datasets"></a>Контекст наборов данных
Можно создать наборы данных, которые с помощью hello конвейера с областью tooa **наборы данных** свойство. Такие наборы данных могут использоваться только действиями в пределах указанного конвейера, но не действиями в других конвейерах. Следующий пример Hello определяет конвейера с помощью двух наборов данных (InputDataset rdc и OutputDataset rdc) toobe, используемых в конвейер hello.  

> [!IMPORTANT]
> Наборы с областью данных поддерживаются только при наличии одноразовый конвейеров (где **pipelineMode** задано слишком**OneTime**). Дополнительные сведения см. в разделе [Однократный конвейер](data-factory-create-pipelines.md#onetime-pipeline).
>
>

```json
{
    "name": "CopyPipeline-rdc",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-rdc"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-rdc"
                    }
                ],
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1,
                    "style": "StartOfInterval"
                },
                "name": "CopyActivity-0"
            }
        ],
        "start": "2016-02-28T00:00:00Z",
        "end": "2016-02-28T00:00:00Z",
        "isPaused": false,
        "pipelineMode": "OneTime",
        "expirationTime": "15.00:00:00",
        "datasets": [
            {
                "name": "InputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "InputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/input",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": true,
                    "policy": {}
                }
            },
            {
                "name": "OutputDataset-rdc",
                "properties": {
                    "type": "AzureBlob",
                    "linkedServiceName": "OutputLinkedService-rdc",
                    "typeProperties": {
                        "fileName": "emp.txt",
                        "folderPath": "adftutorial/output",
                        "format": {
                            "type": "TextFormat",
                            "rowDelimiter": "\n",
                            "columnDelimiter": ","
                        }
                    },
                    "availability": {
                        "frequency": "Day",
                        "interval": 1
                    },
                    "external": false,
                    "policy": {}
                }
            }
        ]
    }
}
```

## <a name="next-steps"></a>Дальнейшие действия
- Дополнительные сведения о конвейерах см. в статье [Конвейеры и действия в фабрике данных Azure](data-factory-create-pipelines.md). 
- Дополнительные сведения о планировании и выполнении конвейеров см. в статье [Планирование и исполнение с использованием фабрики данных](data-factory-scheduling-and-execution.md). 
