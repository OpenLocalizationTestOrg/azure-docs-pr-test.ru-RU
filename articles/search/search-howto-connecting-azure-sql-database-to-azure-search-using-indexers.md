---
title: "База данных SQL Azure aaaConnecting tooAzure поиска с помощью индексаторов | Документы Microsoft"
description: "Узнайте, как toopull данные из базы данных SQL Azure tooan поиска Azure индекс с помощью индексаторов."
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: e9bbf352-dfff-4872-9b17-b1351aae519f
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/13/2017
ms.author: eugenesh
ms.openlocfilehash: b28a11cf18ef994de99e09af90bbfeb171ef3cde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-azure-sql-database-tooazure-search-using-indexers"></a>Подключение базы данных SQL Azure tooAzure поиск с помощью индексаторов

Перед запросом [индексом службы Поиска Azure](search-what-is-an-index.md) необходимо заполнить его данными. Если в базе данных Azure SQL находятся данные hello **индексатор поиска Azure для базы данных SQL Azure** (или **индексатора Azure SQL** сокращенно) можно автоматизировать процесс индексирования hello, что означает меньшую toowrite кода и меньше Инфраструктура toocare о.

В этой статье описан механизм использования hello [индексаторы](search-indexer-overview.md), но также содержит описание возможностей доступно только для баз данных Azure SQL (например, интегрированное отслеживание изменений). 

В базах данных SQL tooAzure сложения поиска Azure предоставляет индексаторов для [Azure Cosmos DB](search-howto-index-documentdb.md), [хранилища больших двоичных объектов Azure](search-howto-indexing-azure-blob-storage.md), и [табличного хранилища Azure](search-howto-indexing-azure-tables.md). Поддержка toorequest для других источников данных, свой отзыв на hello [форуме отзывов по поиску Azure](https://feedback.azure.com/forums/263029-azure-search/).

## <a name="indexers-and-data-sources"></a>Индексаторы и источники данных

Объект **источника данных** указывает, какие данные tooindex, учетные данные для доступа к данным и политики, которые эффективного выявления изменений в данных hello (новых, измененных или удаленных строк). Он определяется как независимый ресурс, который могут использовать несколько индексаторов.

**Индексатор** — это ресурс, соединяющий один источник данных с целевым индексом поиска. Индексатор, который используется в hello следующих способов:

* Выполнение однократного копирования данных hello toopopulate индекса.
* Обновление индекса с изменениями в источнике данных hello по расписанию.
* Запустите по требованию tooupdate индекс по мере необходимости.

Один индексатор может использовать только одну таблицу или представление, но можно создать несколько индексаторов, если требуется несколько индексов поиска toopopulate. Дополнительные сведения см. в статье [Indexer operations (Azure Search Service REST API)](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations#typical-workflow) (Операции с индексаторами в REST API службы поиска Azure).

Индексатор SQL Azure можно установить и настроить с помощью:

* Мастер импорта данных в hello [портал Azure](https://portal.azure.com)
* [пакета SDK .NET для Поиска Azure](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.indexer?view=azure-dotnet);
* [REST API](https://docs.microsoft.com/en-us/rest/api/searchservice/indexer-operations) Поиска Azure;

В этой статье мы будем использовать API-Интерфейс REST toocreate hello **индексаторы** и **источники данных**.

## <a name="when-toouse-azure-sql-indexer"></a>Когда toouse индексатора SQL Azure
В зависимости от нескольких факторов, связанных данных tooyour использование hello индексатора Azure SQL может или не может подходить. Если данные соответствует hello следующие требования, можно использовать индексатор Azure SQL.

| Критерии | Сведения |
|----------|---------|
| Источником данных является отдельная таблица или представление | Если данные hello разбиты на несколько таблиц, можно создать одно представление данных hello. Однако при использовании представления не будет возможности toouse интеграции SQL Server изменения обнаружения toorefresh индекса с добавочные изменения. Дополнительные сведения см. в разделе [Запись измененных и удаленных строк](#CaptureChangedRows) ниже. |
| Типы данных совместимы | В индекс поиска Azure поддерживаются все типы SQL hello. Список см. в разделе [Сопоставление типов данных](#TypeMapping). |
| Синхронизация данных в режиме реального времени необязательна | Индексатор может выполнять повторное индексирование таблицы не чаще, чем раз в пять минут. Если изменения данных часто и hello изменения отражаются в индексе hello несколько секунд или минут один toobe необходимость, мы рекомендуем использовать hello [API-интерфейса REST](https://docs.microsoft.com/rest/api/searchservice/AddUpdate-or-Delete-Documents) или [.NET SDK](search-import-data-dotnet.md) toopush непосредственно обновленных строк. |
| Возможно добавочное индексирование | Если у вас есть большой набор данных и план toorun hello индексатора по расписанию, поиска Azure, должны иметь tooefficiently определения новых, измененных или удаленных строк. Недобавочное индексирование разрешено только при индексировании по требованию или при индексации менее 100 000 строк. Дополнительные сведения см. в разделе [Запись измененных и удаленных строк](#CaptureChangedRows) ниже. |

## <a name="create-an-azure-sql-indexer"></a>Создание индексатора SQL Azure

1. Создайте источник данных hello:

   ```
    POST https://myservice.search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:<your server>.database.windows.net,1433;Database=<your database>;User ID=<your user name>;Password=<your password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "name of hello table or view that you want tooindex" }
    }
   ```

   Можно получить строки подключения hello hello [портал Azure](https://portal.azure.com); используйте hello `ADO.NET connection string` параметр.

2. Если вы их еще нет, создайте hello целевой индекс поиска Azure. Можно создать индекс с помощью hello [портала](https://portal.azure.com) или hello [API создания индекса](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Убедитесь, что hello схемы индекса целевого совместима со схемой hello hello исходной таблицы — см. [сопоставление типов данных SQL и поиска Azure](#TypeMapping).

3. Создание индексатора hello путем указания ее имени и ссылки на исходный и целевой индекс hello данных:

    ```
    POST https://myservice.search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "name" : "myindexer",
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name"
    }
    ```

У индексатора, созданного таким образом, нет расписания. Он автоматически выполняется один раз сразу после создания. Вы можете снова выполнить его в любой момент с помощью запроса на **запуск индексатора** :

    POST https://myservice.search.windows.net/indexers/myindexer/run?api-version=2016-09-01
    api-key: admin-key

Вы можете настроить несколько аспектов поведения индексатора, например размер пакета и сколько документов можно пропустить, прежде чем выполнение индексатора завершится с ошибкой. Чтобы узнать больше, ознакомьтесь с [API создания индексатора](https://docs.microsoft.com/rest/api/searchservice/Create-Indexer).

Может потребоваться служб Azure tooconnect tooallow tooyour-базы данных. В разделе [подключении из Azure](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure) инструкции toodo.

toomonitor hello состояние индексатора и журнал выполнения (количество индексированных элементов, сбои, т. д.), используйте **состояние индексатора** запроса:

    GET https://myservice.search.windows.net/indexers/myindexer/status?api-version=2016-09-01
    api-key: admin-key

Hello ответ должен выглядеть примерно toohello следующее:

    {
        "@odata.context":"https://myservice.search.windows.net/$metadata#Microsoft.Azure.Search.V2015_02_28.IndexerExecutionInfo",
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2015-02-21T00:23:24.957Z",
            "endTime":"2015-02-21T00:36:47.752Z",
            "errors":[],
            "itemsProcessed":1599501,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        },
        "executionHistory":
        [
            {
                "status":"success",
                "errorMessage":null,
                "startTime":"2015-02-21T00:23:24.957Z",
                "endTime":"2015-02-21T00:36:47.752Z",
                "errors":[],
                "itemsProcessed":1599501,
                "itemsFailed":0,
                "initialTrackingState":null,
                "finalTrackingState":null
            },
            ... earlier history items
        ]
    }

Журнал выполнения содержит до too50 hello наиболее недавно завершенные выполнений, которые сортируются в обратном хронологическом порядке hello (при этом последнем выполнении hello идет первой в ответ hello).
Дополнительные сведения об ответе hello можно найти в [Получение состояния индексатора](http://go.microsoft.com/fwlink/p/?LinkId=528198)

## <a name="run-indexers-on-a-schedule"></a>Запуск индексаторов по расписанию
Можно также расположить toorun индексатора hello периодически по расписанию. toodo это, добавьте hello **расписание** свойства при создании или обновлении hello индексатора. Hello ниже пример индексатора hello tooupdate запрос PUT.

    PUT https://myservice.search.windows.net/indexers/myindexer?api-version=2016-09-01
    Content-Type: application/json
    api-key: admin-key

    {
        "dataSourceName" : "myazuresqldatasource",
        "targetIndexName" : "target index name",
        "schedule" : { "interval" : "PT10M", "startTime" : "2015-01-01T00:00:00Z" }
    }

Hello **интервал** является обязательным. Интервал приветствия ссылается toohello время между hello запуска двух последовательных индексатора. Разрешенная Hello наименьший интервал составляет 5 минут. самая длинная Hello — один день. Значение должно быть отформатировано как значение dayTimeDuration XSD (ограниченное подмножество значения [продолжительности ISO 8601](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) ). Hello схема выглядит следующим образом: `P(nD)(T(nH)(nM))`. Примеры: `PT15M` для каждых 15 минут, `PT2H` для каждых 2 часов.

Необязательный Hello **startTime** указывает, когда hello количество выполнений по расписанию должно начаться. Если он опущен, используется текущее время UTC hello. Это время может быть в hello за — в этом случае запланирована hello первого выполнения, как если бы hello индексатор работает непрерывно с момента hello startTime.  

Одновременно можно выполнить только один запуск выбранного индексатора. Если индексатор, который выполняется в случае запланированного выполнения, hello выполнение откладывается до этого момента hello следующее запланированное время.

Давайте рассмотрим пример toomake это более конкретный. Предположим, что мы hello следующие настроить ежечасное расписание:

    "schedule" : { "interval" : "PT1H", "startTime" : "2015-03-01T00:00:00Z" }

Происходит следующее:

1. Hello первого выполнения индексатора начинается на или вокруг 1 марта 2015 г. 00:00. Время в формате UTC.
2. Предположим, выполнение займет 20 минут (или иное количество времени в пределах часа).
3. Выполнение второго Hello начинается на или вокруг 1 марта 2015 г. 01:00.
4. Теперь предположим, что выполнение занимает более часа (например, 70 минут) и завершается около 2:10.
5. Это теперь 02:00:00 по времени для третьего toostart выполнения hello. Тем не менее поскольку hello второго выполнения с 1: 00 по-прежнему работает hello третье выполнение пропускается. начинается выполнение третий Hello в 3 часа ночи.

Вы можете добавить, изменить или удалить расписание для существующего индексатора с помощью **PUT-запроса для индексатора** .

<a name="CaptureChangedRows"></a>

## <a name="capture-new-changed-and-deleted-rows"></a>Запись новых, измененных и удаленных строк

Поиск Azure использует **Добавочное индексирование** tooavoid наличие toore индекса hello всей таблицы или представления, каждый раз при запуске индексатора. Поиск Azure предоставляет два изменения определения политик toosupport Добавочное индексирование. 

### <a name="sql-integrated-change-tracking-policy"></a>Интегрированная политика отслеживания изменений SQL
Если база данных SQL поддерживает [отслеживание изменений](https://docs.microsoft.com/sql/relational-databases/track-changes/about-change-tracking-sql-server), мы рекомендуем использовать **интегрированную политику отслеживания изменений SQL**. Это наиболее эффективный политики hello. Кроме того она позволяет tooidentify удалены строки поиска Azure без необходимости tooadd таблицу tooyour столбца явную «обратимое удаление».

#### <a name="requirements"></a>Требования 

+ Требования к версии базы данных:
  * SQL Server 2012 SP3 и более поздних версий, если вы используете SQL Server на виртуальных машинах Azure.
  * База данных SQL Azure 12, если вы используете базу данных SQL Azure.
+ Только таблицы (представлений нет). 
+ В базе данных hello [отслеживания изменений enable](https://docs.microsoft.com/sql/relational-databases/track-changes/enable-and-disable-change-tracking-sql-server) для таблицы hello. 
+ Не составной первичный ключ (значение первичного ключа, содержащее более одного столбца) в таблице hello.  

#### <a name="usage"></a>Использование

toouse эту политику, создать или обновить источник данных следующим образом:

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "connection string" },
        "container" : { "name" : "table or view name" },
        "dataChangeDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy"
      }
    }

При использовании интегрированной политики отслеживания изменений SQL не указывайте отдельную политику обнаружения удаления данных, так как она уже поддерживает выявление удаленных строк. Тем не менее для hello удалений toobe обнаружил «выполнены автоматически», ключ документа hello в индексе поиска должен быть hello аналогично hello первичного ключа в таблицы SQL hello. 

<a name="HighWaterMarkPolicy"></a>

### <a name="high-water-mark-change-detection-policy"></a>Политика обнаружения изменений максимального уровня

Эту политику обнаружения изменений зависит от столбца «пиковой» захват версии hello или время последнего обновления строки. При использовании представления следует использовать политику максимального уровня. Hello пиковой столбца должен соответствовать hello следующие требования.

#### <a name="requirements"></a>Требования 

* Все вставки укажите значение для столбца hello.
* Элемент tooan всех обновлений также изменить значение hello hello столбца.
* Hello значение этого столбца увеличивается с каждой вставки или обновления.
* Запросы с hello после WHERE и предложения ORDER BY могут выполняться эффективно:`WHERE [High Water Mark Column] > [Current High Water Mark Value] ORDER BY [High Water Mark Column]`

> [!IMPORTANT] 
> Настоятельно рекомендуется использовать hello [rowversion](https://docs.microsoft.com/sql/t-sql/data-types/rowversion-transact-sql) тип данных для столбца пиковой hello. Если используется любой другой тип данных, отслеживания изменений не гарантируется toocapture, все изменения в присутствии hello объекта транзакции, выполняемые параллельно с запросом индексатора. При использовании **rowversion** в конфигурации с репликами только для чтения, hello индексатора должен указывать на первичной реплике hello. Только первичная реплика может использоваться для сценариев синхронизации данных.

#### <a name="usage"></a>Использование

toouse политику пиковой создать или обновить источник данных следующим образом:

    {
        "name" : "myazuresqldatasource",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "connection string" },
        "container" : { "name" : "table or view name" },
        "dataChangeDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
           "highWaterMarkColumnName" : "[a rowversion or last_updated column name]"
      }
    }

> [!WARNING]
> Если hello исходная таблица имеет индекс для столбца пиковой hello, запросы, используемые hello индексатора SQL может истечь время ожидания. В частности, hello `ORDER BY [High Water Mark Column]` предложение требует toorun индекс эффективно при hello таблица содержит много строк.
>
>

При возникновении ошибки времени ожидания, можно использовать hello `queryTimeout` индексатора конфигурации параметр tooset hello значение времени ожидания запроса tooa выше, чем время ожидания hello по умолчанию 5 минут. Например время ожидания too10 tooset hello в минутах, создать или обновить индексатор hello с hello следующая конфигурация:

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

Можно также отключить hello `ORDER BY [High Water Mark Column]` предложения. Однако это не рекомендуется, поскольку если выполнения индексатора hello прерывается из-за ошибки, hello индексатора имеет toore процесса все строки выполняется позднее - даже если индексатор hello уже обработан почти все строки hello hello момент времени, когда она была прервана. toodisable hello `ORDER BY` предложение, используйте hello `disableOrderByHighWaterMarkColumn` в определение индексатора hello:  

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "disableOrderByHighWaterMarkColumn" : true } }
    }

### <a name="soft-delete-column-deletion-detection-policy"></a>Политика обнаружения обратимого удаления столбца
Когда строки удаляются из таблицы источника hello, возможно, необходимо toodelete те строки из индекса поиска hello также. Если вы используете hello SQL интегрированного политику отслеживания изменений, это работают для вас. Тем не менее политику отслеживания изменений пиковой hello не об удаленных строк. Какие toodo?

Если строки hello, физически удаляются из таблицы hello, поиска Azure имеет не способом tooinfer hello наличие записей, которые больше не существуют.  Тем не менее можно использовать без их удаления из таблицы hello hello «soft удалить» метод toologically удаления строк. Добавьте столбец tooyour таблицы или представления и пометить строки как удаленные, с помощью этого столбца.

При использовании методики soft-delete hello, можно указать политику обратимого удаления hello следующим при создании или обновлении hello источника данных:

    {
        …,
        "dataDeletionDetectionPolicy" : {
           "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
           "softDeleteColumnName" : "[a column name]",
           "softDeleteMarkerValue" : "[hello value that indicates that a row is deleted]"
        }
    }

Hello **softDeleteMarkerValue** должен быть строкой — использовать фактическое значение hello строковое представление. Например, если у вас есть целочисленный столбец, где удаленные строки будут отмечены hello значение 1, использовать `"1"`. Если у вас есть БИТОВЫЙ столбец, где удаленные строки будут отмечены hello логическое значение true, используйте `"True"`.

<a name="TypeMapping"></a>

## <a name="mapping-between-sql-and-azure-search-data-types"></a>Сопоставление типов данных SQL и Поиска Azure
| Тип данных SQL | Совместимые типы полей целевого индекса | Примечания |
| --- | --- | --- |
| bit |Edm.Boolean, Edm.String | |
| int, smallint, tinyint |Edm.Int32, Edm.Int64, Edm.String | |
| bigint |Edm.Int64, Edm.String | |
| real, float |Edm.Double, Edm.String | |
| smallmoney, money decimal numeric |Edm.String |Поиск Azure не поддерживает преобразование десятичных типов в Edm.Double, так как это отрицательно скажется на точности. |
| char, nchar, varchar, nvarchar |Edm.String<br/>Collection(Edm.String) |Строка SQL может быть используется toopopulate поле Collection(EDM.String)), если строка hello представляет массив строк JSON:`["red", "white", "blue"]` |
| smalldatetime, datetime, datetime2, date, datetimeoffset |Edm.DateTimeOffset, Edm.String | |
| uniqueidentifer |Edm.String | |
| geography |Edm.GeographyPoint |Поддерживаются только экземпляры географических объектов типа POINT с SRID 4326 (по умолчанию hello) |
| rowversion |Недоступно |Столбцы версии строк не могут храниться в индекс поиска hello, но они могут использоваться для отслеживания изменений |
| time, timespan, binary, varbinary, image, xml, geometry, CLR types |Недоступно |Не поддерживается |

## <a name="configuration-settings"></a>Параметры конфигурации
Индексатор SQL предоставляет несколько параметров конфигурации.

| Настройка | Тип данных | Назначение | Значение по умолчанию |
| --- | --- | --- | --- |
| queryTimeout |string |Здравствуйте, задает время ожидания для выполнения запроса SQL |5 мин ("00:05:00") |
| disableOrderByHighWaterMarkColumn |bool |В результате используемые hello пиковой политики tooomit hello предложение ORDER BY SQL-запроса hello. Ознакомьтесь с [политикой верхнего предела](#HighWaterMarkPolicy). |нет |

Эти параметры используются в hello `parameters.configuration` объекта в определение индексатора hello. Например минут too10 время ожидания запроса hello tooset, создать или обновить индексатор hello с hello следующая конфигурация:

    {
      ... other indexer definition properties
     "parameters" : {
            "configuration" : { "queryTimeout" : "00:10:00" } }
    }

## <a name="faq"></a>Часто задаваемые вопросы

**Вопрос. Можно ли использовать индексатор SQL Azure с базами данных SQL на виртуальных машинах IaaS в Azure?**

Да. Однако необходимо tooallow базы данных tooyour tooconnect службы поиска. Дополнительные сведения см. в разделе [настройки соединения из tooSQL индексатор поиска Azure Server на Виртуальной машине Azure](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md).

**Вопрос. Можно ли использовать индексатор SQL Azure с локальными базами данных SQL?**

Не напрямую. Мы не рекомендуем и не поддерживается прямое подключение, как для этого потребовалось бы вы tooopen трафика tooInternet баз данных. Клиенты преуспели в этом сценарии, используя технологии моста, такие как фабрика данных Azure. Дополнительные сведения см. в разделе [принудительной tooan данных поиска Azure индекс, с помощью фабрики данных Azure](https://docs.microsoft.com/azure/data-factory/data-factory-azure-search-connector).

**Вопрос. Можно ли использовать индексатор SQL Azure с базами данных в IaaS в Azure помимо баз SQL Server?**

Нет. Мы не поддерживают этот сценарий, так как мы не проверяли hello индексатора с базами данных, отличных от SQL Server.  

**Вопрос. Можно ли создать несколько индексаторов, выполняющих обработку по расписанию?**

Да. Но на одном узле одновременно может выполнять обработку только один индексатор. Если требуется несколько индексаторов, выполняемых одновременно, рассмотрите возможность вертикальное масштабирование вашей toomore службы поиска, чем одной единицы поиска.

**Вопрос. Влияет ли выполнение индексатора на рабочую нагрузку запросов?**

Да. Индексатор работает на одном из узлов hello в службе поиска и ресурсы этого узла являются общими для индексирования и обслуживающая трафик запросов и другие запросы API-интерфейса. Если при выполнении интенсивных рабочих нагрузок индексирования и запросов часто отображается ошибка 503 или увеличивается время ответа, вы можете [расширить службу поиска](search-capacity-planning.md).

**Вопрос. Можно ли использовать вторичную реплику в [отказоустойчивом кластере](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview) в качестве источника данных?**

Здесь возможны варианты в зависимости от обстоятельств. Для полной индексации таблицы или представления можно использовать вторичные реплики. 

Для добавочного индексирования Поиск Azure поддерживает две политики отслеживания изменений: интегрированная политика отслеживания изменений SQL и политика обнаружения изменений максимального уровня.

В репликах только для чтения база данных SQL не поддерживает интегрированное отслеживание изменений. Таким образом необходимо использовать политику максимального уровня. 

Стандартная рекомендуется toouse hello rowversion, тип данных для столбца пиковой hello. Однако использование rowversion зависит от функции `MIN_ACTIVE_ROWVERSION` базы данных SQL, которая не поддерживается репликами только для чтения. Таким образом должен указывать hello индексатора tooa первичная реплика, при использовании rowversion.

При попытке rowversion toouse только для чтения реплике, появится следующая ошибка hello: 

    "Using a rowversion column for change tracking is not supported on secondary (read-only) availability replicas. Please update hello datasource and specify a connection toohello primary availability replica.Current database 'Updateability' property is 'READ_ONLY'".

**Вопрос. Можно ли использовать другой столбец, не rowversion, для отслеживания изменений максимального уровня?**

Не рекомендуется. Только **rowversion** обеспечивает надежную синхронизацию данных. Но в зависимости от логики приложения это может быть безопасно, если:

+ Убедитесь, что при запуске индексатора hello нет ожидающих транзакций hello таблице, которая индексируется (например, произойти обновлений всех таблиц в виде пакета по расписанию и расписание индексатор поиска Azure hello задается tooavoid перекрывающихся с таблицей hello расписание обновления).  

+ Вы периодически toopick полную повторную индексацию до любой пропущенных строк. 
