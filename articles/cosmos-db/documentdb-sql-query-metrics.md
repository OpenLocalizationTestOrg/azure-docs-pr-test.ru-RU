---
title: "aaaSQL метрики для Azure Cosmos DB DocumentDB API | Документы Microsoft"
description: "Узнайте, как tooinstrument и отладки hello производительности запросов SQL Azure Cosmos DB запросов."
keywords: "синтаксис SQL, запрос SQL, язык запросов JSON, понятия баз данных и запросы SQL, статистические функции"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: b2fa8e8f-7291-45a3-9bd1-7284ed9077f8
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 2fee3786b7d48d254162699471943e316764b003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-query-performance-with-azure-cosmos-db"></a>Настройка производительности запросов в Azure Cosmos DB
Azure Cosmos DB предоставляет [API SQL для запроса данных](documentdb-sql-query.md) без использования схемы или вторичных индексов. Эта статья содержит следующие сведения для разработчиков hello:

* общие сведения о выполнении SQL-запросов в Azure Cosmos DB;
* сведения о заголовках запросов и ответов и параметры клиентского пакета SDK;
* советы и рекомендации по повышению производительности запросов.
* Примеры как toodebug статистики выполнения SQL tooutilize производительности запросов

## <a name="about-sql-query-execution"></a>Сведения о выполнении SQL-запросов

В базе данных Azure Cosmos, хранить данные в контейнеры, которые может увеличиваться tooany [пропускной способности размер или запрос хранилища](partition-data.md). Azure Cosmos DB легко масштабируется данных через физические секции в группе роста данных toohandle деле hello или увеличение пропускная способность. Может выдавать контейнер tooany запросы SQL, с помощью API-интерфейса REST hello или один из поддерживаемых hello [пакеты SDK DocumentDB](documentdb-sdk-dotnet.md).

Рассмотрим пример секционирования. Вы определяете ключ секции, например city, который определяет, каким образом данные разделяются на физические секции. Ключ одной секции tooa принадлежность данных (например, «Город» == «Seattle») хранится в физической секции, но обычно имеет несколько ключей секционирования в одной физической секции. При секции достигает размера хранилища, служба hello легко разделяет hello секции на две новые секции и равномерно делит ключ раздела hello в этих секциях. Поскольку разделы являются временными, hello API используют абстракцию «раздела ключа диапазона», который используется для обозначения диапазоны hello хэшей ключа секции. 

При выполнении запроса tooAzure Cosmos DB hello SDK выполняет следующие логические действия.

* Синтаксический анализ hello toodetermine запроса SQL hello плана выполнения запроса. 
* Если hello запрос содержит фильтр по ключу секции hello, такие как `SELECT * FROM c WHERE c.city = "Seattle"`, это перенаправленное tooa одна секция. Если запрос hello не имеет фильтр на ключ секционирования, то выполняется во всех секциях и результаты объединяются на стороне клиента.
* запрос Hello выполнении в каждой секции в ряду или параллельного, зависит от конфигурации клиента. В каждой секции hello запроса может внести одно или несколько циклов приема-передачи в зависимости от сложности запросов hello, настроить размер страницы и подготовка пропускной способности hello коллекции. Каждое выполнение возвращает количество hello [единиц запросов](request-units.md) статистику выполнения запросов, используемого при выполнении запроса и при необходимости. 
* Hello SDK выполняет суммирование результатов запросов hello в секциях. Например если hello запрос включает предложение ORDER BY по секциям, затем результаты из отдельных разделов являются результатами отсортированы слияния tooreturn глобально упорядоченную. Если запрос hello агрегат, такой как `COUNT`, hello количеств, из отдельных секций, суммарные tooproduce hello всего.

пакеты SDK Hello предоставляют различные параметры для выполнения запроса. Например, в .NET эти параметры доступны в hello `FeedOptions` класса. Hello следующей таблице описаны эти параметры и их влияние на время выполнения запроса. 

| Параметр | Описание |
| ------ | ----------- |
| `EnableCrossPartitionQuery` | Необходимо задать tootrue для любого запроса, требующий toobe выполняется по более чем одной секции. Это явные флаг tooenable вы toomake компромиссы обоснованное производительности во время разработки. |
| `EnableScanInQuery` | Необходимо указать tootrue, если вы отказались от индексирования, но все равно хотите toorun hello запрос через проверку. Только применяется, если индексирование для hello запрошенный путь фильтра отключена. | 
| `MaxItemCount` | Максимальное количество элементов tooreturn на каждом сервере toohello кругового пути Hello. Установив слишком-1, можно позволить hello server управлять hello количеством элементов. Также можно понизить tooretrieve это значение только небольшое количество элементов в цикл обработки. 
| `MaxBufferedItemCount` | Это значение параметра клиентские и использовать потребление памяти toolimit hello, при выполнении между разделами ORDER BY. Более высокое значение помогает сократить задержку hello сортировки между разделами. |
| `MaxDegreeOfParallelism` | Возвращает или задает номер hello одновременных операций запуска на стороне клиента во время выполнения параллельных запросов в hello службы базы данных Azure DocumentDB. Положительное значение ограничивает число одновременных операций toohello установите значение в hello. Если оно задано сборки, чем 0, hello число параллельных операций toorun автоматически выбирает система hello. |
| `PopulateQueryMetrics` | Дает возможность подробного ведения журнала статистики времени, затраченного на различных этапах выполнения запроса, например времени компиляции, цикла индекса и загрузки документа. Выходные данные статистики запросов можно предоставить проблем с производительностью запросов toodiagnose поддержки Azure. |
| `RequestContinuation` | Путем передачи в токен продолжения непрозрачный hello, возвращаемый любой запрос можно возобновить выполнение запроса. токен продолжения Hello инкапсулирует все состояния, необходимые для выполнения запроса. |
| `ResponseContinuationTokenLimitInKb` | Можно ограничить hello максимальный размер маркера продолжения hello, возвращаемом сервером hello. Может потребоваться tooset это если узла приложения есть ограничения на размер заголовка ответа. Установка этого параметра может увеличить hello общую длительность и RUs, использованных для запроса hello.  |

Например, рассмотрим пример запроса на ключ секционирования, запрошенное на коллекцию с `/city` как раздел hello ключа и она инициализируется посредством 100 000 единиц Запросов в секунду пропускной способности. Запросить этот запрос с помощью `CreateDocumentQuery<T>` в .NET hello следующим образом:

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
        MaxItemCount = -1, 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();
```

Hello SDK фрагмент кода, показанный выше, соответствует toohello после запроса REST API:

```
POST https://arramacquerymetrics-westus.documents.azure.com/dbs/db/colls/sample/docs HTTP/1.1
x-ms-continuation: 
x-ms-documentdb-isquery: True
x-ms-max-item-count: -1
x-ms-documentdb-query-enablecrosspartition: True
x-ms-documentdb-query-parallelizecrosspartitionquery: True
x-ms-documentdb-query-iscontinuationexpected: True
x-ms-documentdb-populatequerymetrics: True
x-ms-date: Tue, 27 Jun 2017 21:52:18 GMT
authorization: type%3dmaster%26ver%3d1.0%26sig%3drp1Hi83Y8aVV5V6LzZ6xhtQVXRAMz0WNMnUuvriUv%2b4%3d
x-ms-session-token: 7:8,6:2008,5:8,4:2008,3:8,2:2008,1:8,0:8,9:8,8:4008
Cache-Control: no-cache
x-ms-consistency-level: Session
User-Agent: documentdb-dotnet-sdk/1.14.1 Host/32-bit MicrosoftWindowsNT/6.2.9200.0
x-ms-version: 2017-02-22
Accept: application/json
Content-Type: application/query+json
Host: arramacquerymetrics-westus.documents.azure.com
Content-Length: 52
Expect: 100-continue

{"query":"SELECT * FROM c WHERE c.city = 'Seattle'"}
```

Каждая страница Выполнение запроса соответствует tooa API-интерфейса REST `POST` с hello `Accept: application/query+json` заголовок и hello SQL-запрос в тексте hello. Каждый запрос создает один или несколько округления сервер toohello приема-передачи с hello `x-ms-continuation` токен отображаться между выполнением tooresume hello клиента и сервера. параметры конфигурации Hello в FeedOptions передаются toohello сервера в виде hello заголовков запроса. Например `MaxItemCount` соответствует слишком`x-ms-max-item-count`. 

Hello запрос возвращает следующие hello (усечены для удобства чтения) ответа:

```
HTTP/1.1 200 Ok
Cache-Control: no-store, no-cache
Pragma: no-cache
Transfer-Encoding: chunked
Content-Type: application/json
Server: Microsoft-HTTPAPI/2.0
Strict-Transport-Security: max-age=31536000
x-ms-last-state-change-utc: Tue, 27 Jun 2017 21:01:57.561 GMT
x-ms-resource-quota: documentSize=10240;documentsSize=10485760;documentsCount=-1;collectionSize=10485760;
x-ms-resource-usage: documentSize=1;documentsSize=884;documentsCount=2000;collectionSize=1408;
x-ms-item-count: 2000
x-ms-schemaversion: 1.3
x-ms-alt-content-path: dbs/db/colls/sample
x-ms-content-path: +9kEANVq0wA=
x-ms-xp-role: 1
x-ms-documentdb-query-metrics: totalExecutionTimeInMs=33.67;queryCompileTimeInMs=0.06;queryLogicalPlanBuildTimeInMs=0.02;queryPhysicalPlanBuildTimeInMs=0.10;queryOptimizationTimeInMs=0.00;VMExecutionTimeInMs=32.56;indexLookupTimeInMs=0.36;documentLoadTimeInMs=9.58;systemFunctionExecuteTimeInMs=0.00;userFunctionExecuteTimeInMs=0.00;retrievedDocumentCount=2000;retrievedDocumentSize=1125600;outputDocumentCount=2000;writeOutputTimeInMs=18.10;indexUtilizationRatio=1.00
x-ms-request-charge: 604.42
x-ms-serviceversion: version=1.14.34.4
x-ms-activity-id: 0df8b5f6-83b9-4493-abda-cce6d0f91486
x-ms-session-token: 2:2008
x-ms-gatewayversion: version=1.14.33.2
Date: Tue, 27 Jun 2017 21:59:49 GMT
```

заголовки ответа ключа Hello, возвращаемых запросом hello включить hello следующие:

| Параметр | Описание |
| ------ | ----------- |
| `x-ms-item-count` | число элементов, возвращаемых в ответе hello Hello. Это зависит от hello предоставленный `x-ms-max-item-count`, hello количество элементов, которое может уместиться в размер полезных данных ответа максимальное hello, hello пропускная способность и время выполнения запроса. |  
| `x-ms-continuation:` | Hello продолжение токена tooresume выполнение запроса hello, если доступны дополнительные результаты. | 
| `x-ms-documentdb-query-metrics` | Статистика запросов Hello для выполнения hello. Это строка с разделителями, содержащий статистику времени, затраченного в hello этапах выполнения запроса. Возвращается, если `x-ms-documentdb-populatequerymetrics` задано слишком`True`. | 
| `x-ms-request-charge` | Здравствуйте, число [единиц запросов](request-units.md) занятая hello запроса. | 

Дополнительные сведения о параметрах и заголовки запроса API-интерфейса REST hello. в разделе [запросы к ресурсам с помощью DocumentDB REST API hello](https://docs.microsoft.com/rest/api/documentdb/querying-documentdb-resources-using-the-rest-api).

## <a name="best-practices-for-query-performance"></a>Рекомендации по повышению производительности запросов
Здесь представлены Hello hello наиболее распространенные факторы, которые повлиять на производительность запроса Azure Cosmos DB. Мы подробно рассмотрим каждую из этих тем в этой статье.

| Коэффициент | Подсказка | 
| ------ | -----| 
| Подготовленная пропускная способность | Измерения RU каждого запроса и убедитесь, что hello требуется пропускная способность для запросов. | 
| Секционирование и ключи секций | Предпочитать запросов со значением ключа секции hello в предложении фильтрации hello для низкой задержкой. |
| Параметры пакета SDK и запроса | Следуйте рекомендациям по работе с пакетами SDK, таким как прямое подключение, а также настройте параметры выполнения запросов на стороне клиента. |
| Задержки сети | Учетная запись для сетевых ресурсов на измерения и использовать множественной адресацией tooread API-интерфейсы из hello ближайший регион. |
| Политика индексации | Проверьте наличие необходимых hello пути/политике индексирования для запроса hello. |
| Метрики выполнения запросов | Анализ hello запроса выполнения метрики tooidentify потенциальных реструктуризации запросов и данных фигуры.  |

### <a name="provisioned-throughput"></a>Подготовленная пропускная способность
В Cosmos DB контейнеры данных создаются c зарезервированной пропускной способностью, выраженной в единицах запроса (ЕЗ) в секунду. Чтение документа 1 КБ — 1 RU, а каждая операция (включая запросы) — нормализованный tooa фиксированное число RUs, в зависимости от его сложности. Например, при наличии 1000 ЕЗ в секунду, подготовленных для контейнера, и запроса, например `SELECT * FROM c WHERE c.city = 'Seattle'`, который использует 5 ЕЗ, можно выполнить 200 таких запросов в секунду ((1000 ЕЗ/с) / (5 ЕЗ/запрос) = 200 ЕЗ). 

Если отправить более чем 200 запросов в секунду, hello служба запускает ограничение скорости входящие запросы, превышающие 200 в секунду. Hello SDK автоматически этот случай, выполняя отсрочки и повторов, таким образом можно заметить большее время задержки для таких запросов. Увеличение toohello пропускной способности hello подготовлены необходимые значение повышает запроса задержки и пропускной способности. 

toolearn Дополнительные сведения о единицах запроса см [единиц запросов](request-units.md).

### <a name="partitioning-and-partition-keys"></a>Секционирование и ключи секций
С помощью DB Cosmos Azure обычно запросы выполняют в hello последовательностью из самый быстрый и наиболее эффективного tooslower или менее эффективным. 

* запросы GET к одному ключу секции и ключу элемента;
* запрос с предложением фильтра к одному ключу секции;
* запрос без равенства или предложения диапазона фильтра для любого свойства;
* запрос без фильтров.

Запросы, необходимость tooconsult секции требуется большее время задержки и может использовать RUs выше. Поскольку каждая секция имеет автоматического индексирования для всех свойств, hello запрос может быть предоставлен эффективно из индекса hello в этом случае. Можно создать запросы, охватывающие быстрее секций с помощью параметров параллелизма hello.

toolearn Дополнительные сведения о секционировании и разделов, в разделе [секционирования в базе данных Azure Cosmos](partition-data.md).

### <a name="sdk-and-query-options"></a>Параметры пакета SDK и запроса
В разделе [советы по повышению производительности](performance-tips.md) и [тестирование производительности](performance-testing.md) для как tooget hello лучше всего производительности на стороне клиента из базы данных Azure Cosmos. Сюда относится использование hello последние пакеты SDK, конфигурациями платформой, такими как количество подключений, частоту сбора мусора по умолчанию настройки и использования упрощенных подключения вариантах, например Direct и TCP. 


#### <a name="max-item-count"></a>Максимальное количество элементов
Для запросов, hello значение `MaxItemCount` может оказать значительное влияние на время конца в конец запроса. Каждое обращение toohello сервер будет возвращать не больше, чем hello число элементов в `MaxItemCount` (по умолчанию 100 элементов). Установка этого значения выше tooa (-1, максимальное и рекомендуемые) улучшит ваш общую длительность запроса, ограничивая hello количества циклов обмена данными между сервером и клиентом, особенно при обработке запросов с большими результирующими наборами.

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxItemCount = -1, 
    }).AsDocumentQuery();
```

#### <a name="max-degree-of-parallelism"></a>Максимальная степень параллелизма
Для запросов, настройки hello `MaxDegreeOfParallelism` tooidentify hello наилучшие конфигурации для приложения, особенно в том случае, если выполнить запросы между разделами (без фильтра для значения ключа раздела hello). `MaxDegreeOfParallelism`Управляет hello максимальное число параллельных задач, т. е. более hello toobe секций посетит в параллельном режиме. 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();
```

Предположим следующее:
* D = по умолчанию максимальное число параллельных задач (= общее количество процессоров в hello клиентского компьютера)
* P — определенное пользователем максимальное число параллельных задач;
* N = число секций, которое требуется toobe посетил ответов на запросы

Ниже приведены последствия как hello параллельные запросы будут работать с различными значениями P.
* (P == 0) => последовательный режим;
* (P == 1) => не более одной задачи;
* (P > 1) => минимум (P, N) параллельных задач; 
* (P < 1) => минимум (N, D) параллельных задач.

Заметки о выпуске пакета SDK и сведения о реализованных классах и методах см. в статье [Пакет SDK для DocumentDB .NET: скачивание и заметки о выпуске](documentdb-sdk-dotnet.md).

### <a name="network-latency"></a>Задержки сети
. В разделе [глобального распространения Azure Cosmos DB](tutorial-global-distribution-documentdb.md) tooset копию глобального распространения и подключения toohello ближайший регион. Задержки в сети имеет значительное влияние на производительность запроса, когда необходимо toomake несколько циклов приема-передачи или получения больших результирующих наборов из запроса hello. 

Hello на метрик выполнения запроса объясняется, как tooretrieve hello server времени выполнения запросов ( `totalExecutionTimeInMs`), чтобы различать время, затраченное на выполнение запроса и время, затраченное в транзитной сети.

### <a name="indexing-policy"></a>Политика индексации
Чтобы узнать о путях индексирования, типах, режимах и их влиянии на выполнение запроса, перейдите к статье [Как работает индексирование данных в Azure Cosmos DB?](indexing-policies.md). По умолчанию hello политика индексирования использует хэш индексирования для строк, действующая для запросов равенства, но не для диапазона запросы/order запросами. Если вам требуется запросов в диапазоне строк, рекомендуется указывать hello диапазона тип индекса для всех строк. 

## <a name="query-execution-metrics"></a>Метрики выполнения запросов
Подробные метрики для выполнения запроса можно получить, передав ему hello необязательно `x-ms-documentdb-populatequerymetrics` заголовок (`FeedOptions.PopulateQueryMetrics` в hello .NET SDK). Здравствуйте, значение, возвращаемое в `x-ms-documentdb-query-metrics` имеет hello следующие пары ключ значение, предназначенные для дополнительной диагностики выполнения запроса. 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();

// Returns metrics by partition key range Id
IReadOnlyDictionary<string, QueryMetrics> metrics = result.QueryMetrics;

```

| Метрика | Единица измерения | Описание | 
| ------ | -----| ----------- |
| `totalExecutionTimeInMs` | Миллисекунды | Время выполнения запроса | 
| `queryCompileTimeInMs` | Миллисекунды | Время компиляции запроса  | 
| `queryLogicalPlanBuildTimeInMs` | Миллисекунды | План логических запроса toobuild времени | 
| `queryPhysicalPlanBuildTimeInMs` | Миллисекунды | План физического запроса toobuild времени | 
| `queryOptimizationTimeInMs` | Миллисекунды | Время, затраченное на оптимизацию запроса | 
| `VMExecutionTimeInMs` | Миллисекунды | Время, затраченное в среде выполнения запроса | 
| `indexLookupTimeInMs` | Миллисекунды | Время, затраченное на физическом уровне индекса | 
| `documentLoadTimeInMs` | Миллисекунды | Время, затраченное на загрузку документов  | 
| `systemFunctionExecuteTimeInMs` | Миллисекунды | Общее время, затраченное на выполнение (встроенных) функций системы (в миллисекундах)  | 
| `userFunctionExecuteTimeInMs` | Миллисекунды | Общее время, затраченное на выполнение определяемых пользователем функций (в миллисекундах) | 
| `retrievedDocumentCount` | Миллисекунды | Общее число полученных документов  | 
| `retrievedDocumentSize` | Байты | Общий размер полученных документов в байтах  | 
| `outputDocumentCount` | count | Количество выходных документов | 
| `writeOutputTimeInMs` | Миллисекунды | Время выполнения запроса в миллисекундах | 
| `indexUtilizationRatio` | Коэффициент (<=1) | Отношение числа документов, совпадающих с hello фильтра toohello количество документов, загружаемых  | 

Hello клиенту пакетов SDK может внутренне выполнять несколько операций tooserve hello запроса в каждой секции. Hello клиент делает более одного вызова каждого раздела Если превышен hello всего результатов `x-ms-max-item-count`, если запрос hello превышает пропускная способность hello для секции hello, или если hello полезных данных запроса достигается максимальный размер hello на каждой странице, или если hello запрос достигает hello система выделенной предельное время ожидания. Каждое частичное выполнение запроса возвращает `x-ms-documentdb-query-metrics` такой страницы. 

Ниже приведены некоторые примеры запросов и как toointerpret некоторые показатели hello возвращенные при выполнении запроса: 

| Запрос | Образец метрики | Описание | 
| ------ | -----| ----------- |
| `SELECT TOP 100 * FROM c` | `"RetrievedDocumentCount": 101` | Hello количество документов, полученных 100 + 1 toomatch предложение TOP hello. Время запроса главным образом тратится на `WriteOutputTime` и `DocumentLoadTime`, так как он выполняет сканирование. | 
| `SELECT TOP 500 * FROM c` | `"RetrievedDocumentCount": 501` | RetrievedDocumentCount теперь является более поздней версии (500 + 1 toomatch hello предложения TOP). | 
| `SELECT * FROM c WHERE c.N = 55` | `"IndexLookupTime": "00:00:00.0009500"` | Около 0,9 мс затрачивается IndexLookupTime на поиск ключа, так как это поиск по индексу `/N/?`. | 
| `SELECT * FROM c WHERE c.N > 55` | `"IndexLookupTime": "00:00:00.0017700"` | Немного больше времени (1,7 мс) затрачивается IndexLookupTime на сканирование диапазона, так как это поиск по индексу `/N/?`. | 
| `SELECT TOP 500 c.N FROM c` | `"IndexLookupTime": "00:00:00.0017700"` | На `DocumentLoadTime` затрачивается то же время, что и в предыдущих запросах, но с меньшим `WriteOutputTime`, так как мы отображаем только одно свойство. | 
| `SELECT TOP 500 udf.toPercent(c.N) FROM c` | `"UserDefinedFunctionExecutionTime": "00:00:00.2136500"` | Около 213 ms, затраченное на `UserDefinedFunctionExecutionTime` выполнение hello определяемой пользователем функции для каждого значения `c.N`. |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(c.Name, 'Den')` | `"IndexLookupTime": "00:00:00.0006400", "SystemFunctionExecutionTime": "00:00:00.0074100"` | Около 0,6 мс затрачивается `IndexLookupTime` на `/Name/?`. Большая часть hello запроса времени выполнения (мс ~ 7) в `SystemFunctionExecutionTime`. |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(LOWER(c.Name), 'den')` | `"IndexLookupTime": "00:00:00", "RetrievedDocumentCount": 2491,  "OutputDocumentCount": 500` | Запрос выполняется как операция сканирования, так как он использует `LOWER`, и 500 из 2491 полученных документов возвращаются. |


## <a name="next-steps"></a>Дальнейшие действия
* toolearn об операторах запросов SQL поддерживается hello и ключевые слова, в разделе [SQL-запроса](documentdb-sql-query.md). 
* в разделе toolearn о единицах запроса [единиц запросов](request-units.md).
* toolearn о политике индексирования. в разделе [политика индексирования](indexing-policies.md) 


