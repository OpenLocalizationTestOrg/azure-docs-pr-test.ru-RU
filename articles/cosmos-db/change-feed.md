---
title: "aaaWorking с изменением hello веб-канал поддержки в базе данных Azure Cosmos | Документы Microsoft"
description: "DB Cosmos Azure используйте изменение канала поддержки tootrack изменений в документах и выполнение обработки на основе событий, как триггеры и поддержание систем кэши и аналитика в актуальном состоянии."
keywords: "веб-канал изменений"
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 2d7798db-857f-431a-b10f-3ccbc7d93b50
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: a4dcf4ceb476e3e08266dbcdcbee1d75e1d1eed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-hello-change-feed-support-in-azure-cosmos-db"></a>Работа с веб-канала поддержка hello изменения в базе данных Azure Cosmos
[Azure Cosmos DB](../cosmos-db/introduction.md) — это быстрая и гибкая служба глобально реплицируемой базы данных, используемая для хранения большого объема данных транзакций и операционных данных с прогнозируемой задержкой операций чтения и записи менее 10 секунд. Благодаря этому она хорошо подходит для приложений Интернета вещей, розничной торговли, игр и приложений для ведения журнала операций. Общий шаблон разработки в этих приложениях — tootrack изменения внесены tooAzure Cosmos DB данных и обновить материализованные представления, выполнения аналитика в реальном времени, toocold хранения архивных данных и активирующие создание уведомлений на определенных событий на основе этих изменений. Hello **изменение веб-канал поддержки** Azure Cosmos DB позволяют toobuild эффективных и масштабируемых решений для каждого из этих шаблонов.

Изменение веб-канал поддержки Azure Cosmos DB предоставляет упорядоченный список документов в коллекции Azure Cosmos DB в порядке hello, в котором они были изменены. Этот канал можно toolisten используется для изменения toodata в пределах коллекции hello и выполнять следующие операции:

* Активировать tooan вызов API при вставке или изменении документа
* выполнение обработки или обновлений в режиме реального времени (поток);
* синхронизация данных с кэшем, поисковой системой или хранилищем данных.

Изменения в Azure Cosmos DB сохраняются и обрабатываются асинхронно, а также распределяются в один или несколько потребителей для параллельной обработки. Давайте рассмотрим hello API-интерфейсы для изменения веб-канала и способы их масштабируемых приложений в режиме реального времени toobuild. В этой статье показано, как изменить toowork с Azure Cosmos DB веб-канал и hello DocumentDB API. 

![Toopower аналитика в реальном времени и событиями сценариев вычисления с помощью изменение в базе данных Azure Cosmos канала](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> Изменение веб-канала поддержка предоставляется только для hello DocumentDB API в данный момент; Hello Graph API и API-Интерфейс таблиц в настоящее время не поддерживаются.

## <a name="use-cases-and-scenarios"></a>Варианты использования и сценарии
Изменение веб-канала позволяет для эффективной обработки больших наборов данных с большим объемом операций записи, а также предлагает tooidentify альтернативные tooquerying все наборы данных, что изменилось. Например можно выполнять следующие задачи эффективно hello:

* Обновление кэша, индекса поиска или хранилища данными, хранящимися в Azure Cosmos DB.
* Реализации уровней и архивации данных на уровне приложений, то есть хранить «горячие данные» в базе данных Azure Cosmos и удаляются с течением времени «холодных данных» слишком[хранилища больших двоичных объектов](../storage/common/storage-introduction.md) или [хранилища Озера данных Azure](../data-lake-store/data-lake-store-overview.md).
* Реализация пакетной аналитики для данных с помощью [Apache Hadoop](run-hadoop-with-hdinsight.md).
* Реализация [лямбда-конвейеров в Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) с помощью Azure Cosmos DB. Azure Cosmos DB предоставляет масштабируемое решение базы данных, которое может обрабатывать операции приема и запроса, а также реализовывать лямбда-архитектуры с низкой совокупной стоимостью владения. 
* Выполнить ноль tooanother простоя миграции учетной записи Azure Cosmos DB с другой схемы секционирования.

**Лямбда-конвейеры при использовании Azure Cosmos DB для приема и запроса:**

![Лямбда-конвейер для приема и запроса на основе Azure Cosmos DB](./media/change-feed/lambda.png)

Можно использовать базу данных Azure Cosmos tooreceive и хранения данных событий из устройств, датчиков, инфраструктуры и приложений и обработать эти события в режиме реального времени с [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), или [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md). 

В рамках вашей [без сервера](http://azure.com/serverless) веб- и мобильных приложений можно отслеживать события, такие как изменения tooyour клиента tootrigger профиль, настройки или расположения некоторых действий, таких как отправка push-уведомления tootheir устройств с помощью [Функций azure](../azure-functions/functions-bindings-documentdb.md) или [службы приложений](https://azure.microsoft.com/services/app-service/). При использовании Azure Cosmos DB toobuild игры, например, можно использовать веб-канала tooimplement в режиме реального времени изменения списки лидеров, в зависимости от оценки из завершенного игры.

## <a name="how-change-feed-works-in-azure-cosmos-db"></a>Как работает веб-канал изменений в Azure Cosmos DB
Azure Cosmos DB обеспечивает возможность tooincrementally hello считывания tooan обновления, выполненные Azure Cosmos DB коллекции. Изменение веб-канал имеет hello следующие свойства:

* Изменения сохраняются в Azure Cosmos DB и могут обрабатываться асинхронно.
* Toodocuments изменения в пределах коллекции доступны немедленно hello изменение веб-канала.
* Tooa каждого изменения документа отображается только один раз в hello изменение веб-канала, и клиенты управлять свою логику контрольные точки. Библиотека веб-канала процессора изменениями Hello предоставляет Автоматическая запись контрольных точек и «по крайней мере один раз» семантику.
* В журнал изменений hello включается только самое последнее изменение hello для данного документа. Промежуточные изменения могут быть недоступны.
* Изменение канала Hello сортируется по порядку изменения в пределах каждого значения ключа секции. В значениях ключа раздела нет установленного порядка.
* Изменения можно синхронизировать в любой момент времени. Это означает, что фиксированный период хранения данных, для которого доступны изменения, отсутствует.
* Изменения доступны в виде фрагментов диапазонов ключей разделов. Эта возможность позволяет изменения из toobe больших коллекций, при параллельной обработке несколько потребителей или серверов.
* Приложения могут запросить для изменения нескольких веб-каналов одновременно на hello же коллекции.

Веб-канал изменений Azure Cosmos DB включен по умолчанию для всех учетных записей. Можно использовать ваш [пропускная способность](request-units.md) в вашем регионе записи или любом [чтения области](distribute-data-globally.md) tooread из hello изменить веб-канал, так же, как и любой другой операции из базы данных Azure Cosmos. поток изменения Hello включает операций вставки или обновления внесенные toodocuments hello коллекции. Вы можете отслеживать операции удаления, установив флажок soft-delete в документах вместо удаления. Кроме того, можно задать ограничение срока для документов через hello [TTL возможность](time-to-live.md)для примера, 24 часа и использование hello значение этого свойства удалит toocapture. Благодаря этому решению имеется tooprocess изменения в более короткий интервал времени, чем срок ЖИЗНИ hello. Hello изменение веб-канала для каждого диапазона ключей секций в коллекции документов hello и таким образом, можно распределить между одной или более потребителей для параллельной обработки. 

![Распределенная обработка веб-канала изменений Azure Cosmos DB](./media/change-feed/changefeedvisual.png)

Есть несколько вариантов реализации веб-канала изменений в коде клиента. Hello разделы, немедленно выполните описывают, как tooimplement hello изменение веб-канал с помощью Azure Cosmos DB REST API hello и пакеты SDK DocumentDB hello. Однако для приложений .NET, мы рекомендуем использовать hello новый [изменение веб-канала библиотеки процессора](#change-feed-processor) для обработки события из hello изменить веб-канала, так как он упрощает чтение изменения в секциях и позволяющий нескольким потокам, работа в параллельном режиме. 

## <a id="rest-apis"></a>Работа с hello REST API и пакеты SDK DocumentDB
Azure Cosmos DB предоставляет эластичные контейнеры хранилища и пропускной способности, называемые **коллекциями**. Данные в коллекциях логически сгруппированы с помощью [ключей разделов](partition-data.md) для масштабируемости и производительности. Azure Cosmos DB предоставляет различные интерфейсы API для доступа к этим данным, включая поиск по идентификатору (чтение или получение), запросы и чтение каналов (сканирования). Hello изменение веб-канала можно получить путем заполнения два новых toohello заголовки запроса DocumentDB `ReadDocumentFeed` API и могут обрабатываться параллельно на диапазоны ключей секционирования.

### <a name="readdocumentfeed-api"></a>Интерфейс API ReadDocumentFeed
Давайте рассмотрим, как работает ReadDocumentFeed. Azure Cosmos DB поддерживает чтение веб-канал документов в коллекции посредством hello `ReadDocumentFeed` API. Например, hello следующий запрос возвращает страницу документов внутри hello `serverlogs` коллекции. 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

Результаты могут быть ограничены с помощью hello `x-ms-max-item-count` заголовок и операций считывания можно возобновить, повторно подав запрос hello с `x-ms-continuation` заголовок возвращается в hello предыдущего ответа. При выполнении из единого клиента `ReadDocumentFeed` выполняет итерацию результатов по разделам последовательно. 

**Веб-канал для последовательного чтения документов**

Вы также можете получить веб-канал hello документов с помощью одного из поддерживаемых hello [пакеты SDK Azure Cosmos DB](documentdb-sdk-dotnet.md). Например, hello следующем фрагменте кода показан способ toouse hello [ReadDocumentFeedAsync метод](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) в .NET.

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a>Распределенное выполнение ReadDocumentFeed
Для коллекций, содержащих терабайты данных и более или принимающих большое количество обновлений, последовательное выполнение веб-канала чтения с компьютера с одним клиентом может оказаться нецелесообразным. В порядке toosupport этих сценариях большие наборы данных Azure Cosmos DB предоставляет toodistribute API-интерфейсы `ReadDocumentFeed` вызовы прозрачно через несколько клиентских средств чтения и потребителей. 

**Веб-канал для распределенного чтения документов**

tooprovide масштабируемой обработки добавочных изменений Azure Cosmos DB поддерживает модель масштабного для изменения hello API на основе диапазонов ключей разделов веб-канала.

* Список диапазонов ключей разделов для коллекции можно получить, выполнив вызов `ReadPartitionKeyRanges`. 
* Для каждого диапазона ключей секций можно выполнить `ReadDocumentFeed` tooread документов с помощью разделов в пределах диапазона.

### <a name="retrieving-partition-key-ranges-for-a-collection"></a>Извлечение диапазонов ключей разделов для коллекции
Вы можете получить диапазонов ключей секционирования hello, запрашивающего hello `pkranges` ресурсов в пределах коллекции. Например hello следующий запрос извлекает список hello диапазонов ключа секции для hello `serverlogs` коллекции:

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

Этот запрос возвращает следующий ответ, содержащий метаданные о диапазонов ключей секционирования hello hello:

    HTTP/1.1 200 Ok
    Content-Type: application/json
    x-ms-item-count: 25
    x-ms-schemaversion: 1.1
    Date: Tue, 15 Nov 2016 07:26:51 GMT

    {
       "_rid":"qYcAAPEvJBQ=",
       "PartitionKeyRanges":[
          {
             "_rid":"qYcAAPEvJBQCAAAAAAAAUA==",
             "id":"0",
             "_etag":"\"00002800-0000-0000-0000-580ac4ea0000\"",
             "minInclusive":"",
             "maxExclusive":"05C1CFFFFFFFF8",
             "_self":"dbs\/qYcAAA==\/colls\/qYcAAPEvJBQ=\/pkranges\/qYcAAPEvJBQCAAAAAAAAUA==\/",
             "_ts":1477100776
          },
          ...
       ],
       "_count": 25
    }


**Свойства ключа диапазона секционирования**: каждый раздел диапазон включает свойства метаданных hello в hello в следующей таблице:

<table>
    <tr>
        <th>Имя заголовка</th>
        <th>Описание</th>
    </tr>
    <tr>
        <td>id</td>
        <td>
            <p>Идентификатор Hello hello диапазона ключей секций. Это стабильный и уникальный идентификатор в каждой коллекции.</p>
            <p>Должен использоваться в следующие отличия tooread вызов hello диапазона ключей секций.</p>
        </td>
    </tr>
    <tr>
        <td>maxExclusive</td>
        <td>Hello секции максимальное значение хэш ключа для диапазона ключей секций hello. Для внутреннего использования.</td>
    </tr>
    <tr>
        <td>minInclusive</td>
        <td>значение хэш ключа Hello минимальное секции для диапазона ключей секций hello. Для внутреннего использования.</td>
    </tr>       
</table>

Это можно сделать с помощью одного из поддерживаемых hello [пакеты SDK Azure Cosmos DB](documentdb-sdk-dotnet.md). Hello следующем фрагменте кода показано, как ключ раздела tooretrieve диапазоны в .NET с помощью hello [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) метод.

```csharp
string pkRangesResponseContinuation = null;
List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

do
{
    FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
        collectionUri, 
        new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

    partitionKeyRanges.AddRange(pkRangesResponse);
    pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
}
while (pkRangesResponseContinuation != null);
```

Azure Cosmos DB поддерживает получение документов по диапазона ключей секций, установка hello необязательно `x-ms-documentdb-partitionkeyrangeid` заголовок. 

### <a name="performing-an-incremental-readdocumentfeed"></a>Выполнение добавочного ReadDocumentFeed
ReadDocumentFeed поддерживает следующие сценарии и задачи для добавочной обработки изменений в коллекции Azure Cosmos DB hello:

* Чтение всех изменяет toodocuments с начала hello, то есть создание коллекции.
* Чтение всех изменений toodocuments toofuture обновлений из текущего времени или все изменения с момента времени, определяемый пользователем.
* Чтение всех изменений toodocuments из логическую версию коллекции hello (ETag). Вы можете потребителей на основании hello ETag, возвращенные добавочных запросов чтения канала контрольной точки.

Hello изменения включают в себя toodocuments вставок и обновлений. Удаляет toocapture, следует использовать свойство «обратимое удаление» по документам, или использовать hello [встроенного свойства TTL](time-to-live.md) toosignal Ожидается удаление в hello изменить веб-канала.

Здравствуйте, следующие списки hello таблицы [запроса](/rest/api/documentdb/common-documentdb-rest-request-headers.md) и [заголовки ответа](/rest/api/documentdb/common-documentdb-rest-response-headers.md) ReadDocumentFeed операций.

**Заголовки запроса для добавочного ReadDocumentFeed**

<table>
    <tr>
        <th>Имя заголовка</th>
        <th>Описание</th>
    </tr>
    <tr>
        <td>A-IM</td>
        <td>Необходимо задать слишком «Incremental канала» или опущен, в противном случае</td>
    </tr>
    <tr>
        <td>If-None-Match</td>
        <td>
            <p>Нет заголовка: возвращает все изменения из hello начиная (Создание коллекции)</p>
            <p>«*»: возвращает все новые toodata изменения в коллекции hello</p>         
            <p>&lt;eTag&gt;: Если значение коллекции tooa ETag, возвращает все изменения, внесенные с момента этого логического отметки времени</p>
        </td>
    </tr>
    <tr>    
        <td>If-Modified-Since</td> 
        <td>Формат времени RFC 1123. Не учитывается, если указан заголовок If-None-Match.</td> 
    </tr> 
    <tr>
        <td>x-ms-documentdb-partitionkeyrangeid</td>
        <td>Hello идентификатор секции диапазона ключей для считывания данных.</td>
    </tr>
</table>

**Заголовки ответа для добавочного ReadDocumentFeed**

<table> <tr>
        <th>Имя заголовка</th>
        <th>Описание</th>
    </tr>
    <tr>
        <td>etag</td>
        <td>
            <p>Hello логических порядковый номер (LSN) последней документа, возвращаемый в ответе hello.</p>
            <p>Добавочный ReadDocumentFeed можно возобновить, повторно задав это значение в параметре If-None-Match.</p>
        </td>
    </tr>
</table>

Ниже приведен пример запроса tooreturn все добавочные изменения в коллекции из логических версии в hello ETag `28535` и секции диапазона ключей = `16`:

    GET https://mydocumentdb.documents.azure.com/dbs/bigdb/colls/bigcoll/docs HTTP/1.1
    x-ms-max-item-count: 1
    If-None-Match: "28535"
    A-IM: Incremental feed
    x-ms-documentdb-partitionkeyrangeid: 16
    x-ms-date: Tue, 22 Nov 2016 20:43:01 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dzdpL2QQ8TCfiNbW%2fEcT88JHNvWeCgDA8gWeRZ%2btfN5o%3d
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

Изменения, упорядочиваются по времени в пределах каждого значения ключа секции в пределах диапазона ключей секций hello. В значениях ключа раздела нет установленного порядка. Если доступно больше результатов, чем может поместиться на одной странице, можно прочитать hello следующей страницы результатов, повторно подав запрос hello с hello `If-None-Match` заголовок с значение равно toohello `etag` из предыдущего ответа hello. Если несколько документов были вставлены или обновлены на уровне транзакций, в пределах хранимой процедуры или триггера, они все возвращается в hello же страницу "ответ".

> [!NOTE]
> С веб-каналом изменений, можно получить дополнительные элементы, которые возвращаются на странице, чем указано в `x-ms-max-item-count` в случае hello несколько документов, вставленных или обновленных в хранимых процедурах или триггерах. 

При использовании hello .NET SDK (1.17.0), задать поле hello `StartTime` в `ChangeFeedOptions` документов toodirectly возвращаемого изменены с момента `StartTime` при вызове `CreateDocumentChangeFeedQuery`. Указав `If-Modified-Since` с помощью API-интерфейса REST hello, запрос будет возвращать не hello документы сами, но вместо токен продолжения hello или `etag` в заголовке ответа hello. измененный hello указано время токен продолжения hello документы hello tooreturn `etag` необходимо использовать в запросе Далее hello с `If-None-Match` tooreturn hello фактическое документов. 

Hello .NET SDK предоставляет hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) и [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) вспомогательные классы tooaccess изменения, внесенные tooa коллекции. Hello следующий фрагмент кода показывает, как изменяется tooretrieve все с начала hello hello .NET SDK от одного клиента с помощью.

```csharp
private async Task<Dictionary<string, string>> GetChanges(
    DocumentClient client,
    string collection,
    Dictionary<string, string> checkpoints)
{
    string pkRangesResponseContinuation = null;
    List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

    do
    {
        FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
            collectionUri, 
            new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

        partitionKeyRanges.AddRange(pkRangesResponse);
        pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
    }
    while (pkRangesResponseContinuation != null);

    foreach (PartitionKeyRange pkRange in partitionKeyRanges)
    {
        string continuation = null;
        checkpoints.TryGetValue(pkRange.Id, out continuation);

        IDocumentQuery<Document> query = client.CreateDocumentChangeFeedQuery(
            collection,
            new ChangeFeedOptions
            {
                PartitionKeyRangeId = pkRange.Id,
                StartFromBeginning = true,
                RequestContinuation = continuation,
                MaxItemCount = 1
            });

        while (query.HasMoreResults)
        {
            FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

            foreach (DeviceReading changedDocument in readChangesResponse)
            {
                Console.WriteLine(changedDocument.Id);
            }

            checkpoints[pkRange.Id] = readChangesResponse.ResponseContinuation;
        }
    }

    return checkpoints;
}
```
И hello следующий фрагмент кода показывает, как изменяется tooprocess в режиме реального времени с помощью DB Cosmos Azure с помощью изменений hello канала поддержки и hello предшествующий функции. Первый вызов функции Hello возвращает все документы hello в коллекции hello и hello второй только возвращает hello двух документов, созданных, созданные с момента последней контрольной точки hello.

```csharp
// Returns all documents in hello collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only hello two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

Также можно фильтровать с помощью событий на стороне логику tooselectively процесс сервера веб-канал изменение hello. Например ниже приведен фрагмент, который использует tooprocess LINQ стороне клиента только для событий изменения температуры от датчиков устройства.

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <a id="change-feed-processor"></a>Библиотека обработчика веб-канала изменений
Другой вариант — toouse hello [библиотеки Azure Cosmos DB изменить веб-канал процессора](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), который поможет вам легко распространять событий обработки из-за изменения веб-канал по нескольким получателям. Библиотека Hello отлично подходит для создания веб-канала чтения на платформе .NET hello изменений. Некоторые рабочие процессы, которые бы упростить с помощью библиотеки hello процессора канала изменений по сравнению с методами hello, включенных в hello других пакетов SDK DB Cosmos включают: 

* Извлечение обновлений из веб-канала изменений, когда данные хранятся в нескольких секциях.
* Перемещение или репликация данных из одной коллекции tooanother
* Параллельное выполнение действий, запускаемые toodata обновлений и изменение веб-канала 

Хотя с помощью hello API-интерфейсы в hello Cosmos SDK предоставляет toochange точно управлять доступом веб-канал обновлений в каждой секции, с помощью библиотеки изменение веб-канала процессора hello упрощает чтение изменения по секции и параллельная работа нескольких потоков. Вместо вручную считывания изменений из каждого контейнера и сохранение токен продолжения для каждой секции hello изменение веб-канала процессора автоматически управляет чтения изменения в секциях с помощью механизма аренды.

Библиотека Hello доступна как пакет NuGet: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) и из исходного кода, как Github [пример](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor). 

### <a name="understanding-change-feed-processor-library"></a>Основные сведения о библиотеке обработчика веб-канала изменений 

Существует четыре основных компонентов реализации hello изменение процессора веб-канала: hello отслеживаемых коллекции, коллекции аренды hello, узел обработчика hello и потребители hello. 

**Сбор данных о наблюдаемых:** hello отслеживаемых собираются из какой hello создается изменение веб-канала данных hello. Любой коллекции toohello мониторинг операций вставки и изменения отражаются в канал передачи изменений hello hello коллекции. 

**Сбор данных аренды:** hello координаты коллекции аренды обработки изменений hello веб-канала для нескольких сотрудников. Коллекция отдельных — используется toostore hello аренды с арендой одной на каждую секцию. Это выгодно toostore этой коллекции аренды на другую учетную запись с hello записи ближе toowhere hello область которой выполняется замена процессора веб-канала. Объект аренды содержит hello следующие атрибуты: 
* Владелец: Указывает, hello узла, которому принадлежит hello аренды
* Продолжение: Определяет положение hello (токен продолжения) в веб-канала для определенного раздела Изменение hello
* Отметка времени: Время последнего обновления аренды; Отметка времени Hello может быть используется toocheck ли hello аренды считается недействительным 

**Узел обработчика:** каждого узла определяет, сколько секций tooprocess зависимости от того, сколько других экземпляров узлов имеют активную аренду. 
1.  При запуске узла, он получает рабочей нагрузки hello toobalance аренды на всех узлах. Узел периодически обновляет аренды, чтобы они оставалась активными. 
2.  Узел контрольные точки hello последнего продолжение токена tooits аренду для каждой операции чтения. tooensure параллелизма, узел проверок hello ETag для каждого обновления аренды. Также поддерживаются другие стратегии контрольных точек.  
3.  После завершения работы узел отменяет все аренды адресов, но сохраняет hello сведения о продолжении, чтобы можно было продолжить чтение из контрольной точки хранимых hello позже. 

В настоящее время hello количеством узлов не может быть больше hello количество секций (аренды).

**Потребители:** клиентов или сотрудников, являются потоки, выполняющие hello изменение веб-канал обработки, инициированных каждого узла. Каждый узел обработчика может иметь несколько объектов-получателей. Каждый потребитель считывает hello изменение веб-канала из hello секции, ей назначается tooand уведомляет ведущим изменений и окончание срока действия аренды.

toofurther понять взаимосвязи между этими четырьмя элементами, изменение канала процессора, давайте рассмотрим пример, в hello следующие схемы. Hello отслеживания документов хранилищ коллекции и использует hello «Город» в качестве ключа секции hello. Мы видим, hello синий раздел содержит документы с hello поле «Город» из «A-E» и т. д. Существует два узла, каждый с двумя потребители считывании hello четырех секций одновременно. стрелки Hello видно, что потребитель hello, чтения из конкретной точки в hello изменить веб-канала. В первом разделе hello hello темнее синий представляет непрочитанные изменения, а hello светло-синий представляет hello, прочитанные изменения на веб-канал изменение hello. Hello узлы используют hello аренды коллекции toostore за tookeep значение «продолжение» hello текущего чтения позиции для каждого объекта-получателя. 

![Изменение размера базы данных Azure Cosmos hello с помощью веб-канала процессора узла](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a>Использование библиотеки обработчика веб-канала изменений 
Hello в следующем разделе описывается, как toouse hello изменение процессора веб-канала библиотеки в контексте hello репликации изменений из источника коллекции tooa назначения коллекции. Здесь hello исходной коллекции является коллекцией hello отслеживаемых изменений процессора веб-канала. 

**Установите и включите пакет NuGet обработчика веб-канала изменение hello** 

Прежде чем устанавливать пакет NuGet обработчика веб-канала изменений, установите: 
* Библиотеку Microsoft.Azure.DocumentDB (версии 1.13.1 или выше). 
* Newtonsoft.Json, версии 9.0.1 или более поздней версии. Установите пакет `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` и добавьте его в качестве ссылки.

**Создайте отслеживаемую коллекцию, коллекцию аренд и назначения** 

В порядке toouse hello библиотеку потоков процессора изменений hello аренды коллекции должен toobe, созданные перед выполнением hello узлами процессора. Еще раз рекомендуется хранить коллекции аренды на другую учетную запись с hello записи регион ближе toowhere что выполняется замена процессора веб-канала. В этом примере перемещения данных нужно toocreate hello целевой коллекции перед запуском узел обработчика веб-канала изменение hello. В примере кода hello мы называем отслеживаемых, toocreate hello вспомогательный метод арендован и целевой коллекции, если они еще не существует. 

> [!WARNING]
> Создание коллекции имеет цены последствия, как при резервировании пропускной способности для hello toocommunicate приложений с Azure Cosmos DB. Для получения дополнительных сведений посетите hello [странице цен](https://azure.microsoft.com/pricing/details/cosmos-db/)
> 
> 

*Создание узла обработчика*

Hello `ChangeFeedProcessorHost` класс предоставляет среду выполнения потокобезопасна, несколькими процессами, безопасного для реализаций обработчиков событий, которая также обеспечивает управление аренды назначение контрольных точек и секции. toouse hello `ChangeFeedProcessorHost` , можно реализовать `IChangeFeedObserver`. Этот интерфейс содержит три метода:

* `OpenAsync` — эта функция вызывается при открытии наблюдателя веб-канала изменений. При открытии потребителя и наблюдателя может быть измененный tooperform определенное действие.  
* `CloseAsync` — эта функция вызывается при закрытии наблюдателя веб-канала изменений. Измененный tooperform определенного действия может быть при закрытии потребителя и наблюдателя.  
* `ProcessChangesAsync` — эта функция вызывается, когда новые изменения документа доступны в веб-канале изменений. Это может быть измененный tooperform определенных действий после каждого обновления изменения веб-канала.  

В нашем примере мы реализовали hello интерфейс `IChangeFeedObserver` через hello `DocumentFeedObserver` класса. Здравствуйте, `ProcessChangesAsync` функции веб-канала документа от изменений в коллекции назначения начали hello upserts (обновления). В этом примере полезен для переноса данных из одной коллекции tooanother в порядке ключ раздела hello toochange набора данных. 

*Под управлением hello процессора узла*

Перед началом обработки событий можно настроить параметры веб-канала и узла веб-канала. 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval too15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
Hello конкретных полей, которые могут быть настроены представлены в следующей таблице hello. 

**Параметры веб-канала изменений**:
<table>
    <tr>
        <th>Имя свойства</th>
        <th>Описание</th>
    </tr>
    <tr>
        <td>MaxItemCount</td>
        <td>Возвращает или задает максимальное количество hello toobe элементов, возвращаемых при операции перечисления hello в hello Azure Cosmos DB базы данных службы.</td>
    </tr>
    <tr>
        <td>PartitionKeyRangeId</td>
        <td>Возвращает или задает идентификатор hello секции диапазона ключей, для текущего запроса hello службы базы данных Azure Cosmos DB hello.</td>
    </tr>
    <tr>
        <td>RequestContinuation</td>
        <td>Возвращает или задает маркер продолжения запроса hello службы базы данных Azure Cosmos DB hello.</td>
    </tr>
        <tr>
        <td>SessionToken</td>
        <td>Возвращает или задает hello токена сеанса для использования с согласованность сеансов в hello Azure Cosmos DB базы данных службы.</td>
    </tr>
        <tr>
        <td>StartFromBeginning</td>
        <td>Возвращает или задает изменение веб-канал службы базы данных Azure Cosmos DB hello запустить из hello начиная (true) или из текущих (false). По умолчанию он начинается с текущего положения (false).</td>
    </tr>
</table>

**Параметры узла веб-канала изменений**:
<table>
    <tr>
        <th>Имя свойства</th>
        <th>Тип</th>
        <th>Описание</th>
    </tr>
    <tr>
        <td>LeaseRenewInterval</td>
        <td>TimeSpan</td>
        <td>Hello интервал для все аренды адресов для секций, удерживаемые в настоящее время экземпляр ChangeFeedEventHost hello.</td>
    </tr>
    <tr>
        <td>LeaseAcquireInterval</td>
        <td>TimeSpan</td>
        <td>Здравствуйте tookick интервал off toocompute задач ли секций распределяются равномерно между известных экземплярах.</td>
    </tr>
    <tr>
        <td>LeaseExpirationInterval</td>
        <td>TimeSpan</td>
        <td>Интервал приветствия, для которых hello аренды извлекаются аренды, представляющая раздел. Если Аренда hello не была обновлена в течение этого интервала, он будет просрочен и владения секции hello перемещает tooanother ChangeFeedEventHost экземпляра.</td>
    </tr>
    <tr>
        <td>FeedPollDelay</td>
        <td>TimeSpan</td>
        <td>Hello задержках между опросами секции для новых изменений на hello веб-канала, после все текущие изменения будут утеряны.</td>
    </tr>
    <tr>
        <td>CheckpointFrequency</td>
        <td>CheckpointFrequency</td>
        <td>Здравствуйте, частота toocheckpoint аренды.</td>
    </tr>
    <tr>
        <td>MinPartitionCount</td>
        <td>int</td>
        <td>Hello минимальное количество разделов для узла hello.</td>
    </tr>
    <tr>
        <td>MaxPartitionCount</td>
        <td>int</td>
        <td>может служить Hello максимальное количество секций hello узла.</td>
    </tr>
    <tr>
        <td>DiscardExistingLeases</td>
        <td>Bool</td>
        <td>Ли на hello запуска узла hello все существующие аренды должен быть удален и hello узла должно начинаться с нуля.</td>
    </tr>
</table>


создать экземпляр toostart обработка событий, `ChangeFeedProcessorHost`, предоставляя hello соответствующие параметры для вашей коллекции Azure Cosmos DB. Затем вызовите метод `RegisterObserverAsync` tooregister вашей `IChangeFeedObserver` реализацию hello среды выполнения (DocumentFeedObserver в этом примере). На этом этапе узел hello предпринимает tooacquire аренду для каждого диапазона ключей секций в коллекции Azure Cosmos DB hello, с помощью алгоритма «жадного». Эти аренды будут продолжаться в течение заданного промежутка времени, после чего их необходимо продлить. Когда новые узлы рабочих экземпляров, в этом случае переходит в оперативный режим, они резервируют аренды и со временем загрузки hello переходит между узлами, как каждый узел пытается tooacquire дополнительные аренды. 

В примере кода hello, мы используем фабрики класса (DocumentFeedObserverFactory.cs) toocreate наблюдателя и hello `RegistObserverFactoryAsync` tooregister hello наблюдателя. 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter toostop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
Со временем устанавливается равновесие. Эта динамическая возможность позволяет на основе ЦП автоматическое масштабирование применяется toobe tooconsumers для масштабирования вверх и вниз. Если изменения будут доступны в базе данных Azure Cosmos быстрее, чем могут обработать потребители, hello увеличить ресурсы ЦП для потребителей можно использовать toocause автоматически регулировать число экземпляров рабочих процессов.

## <a name="next-steps"></a>Дальнейшие действия
* Повторите hello [изменение в базе данных Azure Cosmos канал примеры кода на GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)
* Приступить к созданию кода с hello [пакеты SDK Azure Cosmos DB](documentdb-sdk-dotnet.md) или hello [API-интерфейса REST](/rest/api/documentdb/).
