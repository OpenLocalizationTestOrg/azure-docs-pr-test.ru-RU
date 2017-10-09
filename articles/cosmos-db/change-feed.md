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
# <a name="working-with-hello-change-feed-support-in-azure-cosmos-db"></a><span data-ttu-id="a8faf-104">Работа с веб-канала поддержка hello изменения в базе данных Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="a8faf-104">Working with hello change feed support in Azure Cosmos DB</span></span>
<span data-ttu-id="a8faf-105">[Azure Cosmos DB](../cosmos-db/introduction.md) — это быстрая и гибкая служба глобально реплицируемой базы данных, используемая для хранения большого объема данных транзакций и операционных данных с прогнозируемой задержкой операций чтения и записи менее 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="a8faf-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is a fast and flexible globally replicated database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes.</span></span> <span data-ttu-id="a8faf-106">Благодаря этому она хорошо подходит для приложений Интернета вещей, розничной торговли, игр и приложений для ведения журнала операций.</span><span class="sxs-lookup"><span data-stu-id="a8faf-106">This makes it well-suited for IoT, gaming, retail, and operational logging applications.</span></span> <span data-ttu-id="a8faf-107">Общий шаблон разработки в этих приложениях — tootrack изменения внесены tooAzure Cosmos DB данных и обновить материализованные представления, выполнения аналитика в реальном времени, toocold хранения архивных данных и активирующие создание уведомлений на определенных событий на основе этих изменений.</span><span class="sxs-lookup"><span data-stu-id="a8faf-107">A common design pattern in these applications is tootrack changes made tooAzure Cosmos DB data, and update materialized views, perform real-time analytics, archive data toocold storage, and trigger notifications on certain events based on these changes.</span></span> <span data-ttu-id="a8faf-108">Hello **изменение веб-канал поддержки** Azure Cosmos DB позволяют toobuild эффективных и масштабируемых решений для каждого из этих шаблонов.</span><span class="sxs-lookup"><span data-stu-id="a8faf-108">hello **change feed support** in Azure Cosmos DB enables you toobuild efficient and scalable solutions for each of these patterns.</span></span>

<span data-ttu-id="a8faf-109">Изменение веб-канал поддержки Azure Cosmos DB предоставляет упорядоченный список документов в коллекции Azure Cosmos DB в порядке hello, в котором они были изменены.</span><span class="sxs-lookup"><span data-stu-id="a8faf-109">With change feed support, Azure Cosmos DB provides a sorted list of documents within an Azure Cosmos DB collection in hello order in which they were modified.</span></span> <span data-ttu-id="a8faf-110">Этот канал можно toolisten используется для изменения toodata в пределах коллекции hello и выполнять следующие операции:</span><span class="sxs-lookup"><span data-stu-id="a8faf-110">This feed can be used toolisten for modifications toodata within hello collection and perform actions such as:</span></span>

* <span data-ttu-id="a8faf-111">Активировать tooan вызов API при вставке или изменении документа</span><span class="sxs-lookup"><span data-stu-id="a8faf-111">Trigger a call tooan API when a document is inserted or modified</span></span>
* <span data-ttu-id="a8faf-112">выполнение обработки или обновлений в режиме реального времени (поток);</span><span class="sxs-lookup"><span data-stu-id="a8faf-112">Perform real-time (stream) processing on updates</span></span>
* <span data-ttu-id="a8faf-113">синхронизация данных с кэшем, поисковой системой или хранилищем данных.</span><span class="sxs-lookup"><span data-stu-id="a8faf-113">Synchronize data with a cache, search engine, or data warehouse</span></span>

<span data-ttu-id="a8faf-114">Изменения в Azure Cosmos DB сохраняются и обрабатываются асинхронно, а также распределяются в один или несколько потребителей для параллельной обработки.</span><span class="sxs-lookup"><span data-stu-id="a8faf-114">Changes in Azure Cosmos DB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing.</span></span> <span data-ttu-id="a8faf-115">Давайте рассмотрим hello API-интерфейсы для изменения веб-канала и способы их масштабируемых приложений в режиме реального времени toobuild.</span><span class="sxs-lookup"><span data-stu-id="a8faf-115">Let's look at hello APIs for change feed and how you can use them toobuild scalable real-time applications.</span></span> <span data-ttu-id="a8faf-116">В этой статье показано, как изменить toowork с Azure Cosmos DB веб-канал и hello DocumentDB API.</span><span class="sxs-lookup"><span data-stu-id="a8faf-116">This article shows how toowork with Azure Cosmos DB change feed and hello DocumentDB API.</span></span> 

![Toopower аналитика в реальном времени и событиями сценариев вычисления с помощью изменение в базе данных Azure Cosmos канала](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> <span data-ttu-id="a8faf-118">Изменение веб-канала поддержка предоставляется только для hello DocumentDB API в данный момент; Hello Graph API и API-Интерфейс таблиц в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="a8faf-118">Change feed support is only provided for hello DocumentDB API at this time; hello Graph API and Table API are not currently supported.</span></span>

## <a name="use-cases-and-scenarios"></a><span data-ttu-id="a8faf-119">Варианты использования и сценарии</span><span class="sxs-lookup"><span data-stu-id="a8faf-119">Use cases and scenarios</span></span>
<span data-ttu-id="a8faf-120">Изменение веб-канала позволяет для эффективной обработки больших наборов данных с большим объемом операций записи, а также предлагает tooidentify альтернативные tooquerying все наборы данных, что изменилось.</span><span class="sxs-lookup"><span data-stu-id="a8faf-120">Change feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative tooquerying entire datasets tooidentify what has changed.</span></span> <span data-ttu-id="a8faf-121">Например можно выполнять следующие задачи эффективно hello:</span><span class="sxs-lookup"><span data-stu-id="a8faf-121">For example, you can perform hello following tasks efficiently:</span></span>

* <span data-ttu-id="a8faf-122">Обновление кэша, индекса поиска или хранилища данными, хранящимися в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a8faf-122">Update a cache, search index, or a data warehouse with data stored in Azure Cosmos DB.</span></span>
* <span data-ttu-id="a8faf-123">Реализации уровней и архивации данных на уровне приложений, то есть хранить «горячие данные» в базе данных Azure Cosmos и удаляются с течением времени «холодных данных» слишком[хранилища больших двоичных объектов](../storage/common/storage-introduction.md) или [хранилища Озера данных Azure](../data-lake-store/data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a8faf-123">Implement application-level data tiering and archival, that is, store "hot data" in Azure Cosmos DB, and age out "cold data" too[Azure Blob Storage](../storage/common/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>
* <span data-ttu-id="a8faf-124">Реализация пакетной аналитики для данных с помощью [Apache Hadoop](run-hadoop-with-hdinsight.md).</span><span class="sxs-lookup"><span data-stu-id="a8faf-124">Implement batch analytics on data using [Apache Hadoop](run-hadoop-with-hdinsight.md).</span></span>
* <span data-ttu-id="a8faf-125">Реализация [лямбда-конвейеров в Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) с помощью Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a8faf-125">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with Azure Cosmos DB.</span></span> <span data-ttu-id="a8faf-126">Azure Cosmos DB предоставляет масштабируемое решение базы данных, которое может обрабатывать операции приема и запроса, а также реализовывать лямбда-архитектуры с низкой совокупной стоимостью владения.</span><span class="sxs-lookup"><span data-stu-id="a8faf-126">Azure Cosmos DB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span></span> 
* <span data-ttu-id="a8faf-127">Выполнить ноль tooanother простоя миграции учетной записи Azure Cosmos DB с другой схемы секционирования.</span><span class="sxs-lookup"><span data-stu-id="a8faf-127">Perform zero down-time migrations tooanother Azure Cosmos DB account with a different partitioning scheme.</span></span>

<span data-ttu-id="a8faf-128">**Лямбда-конвейеры при использовании Azure Cosmos DB для приема и запроса:**</span><span class="sxs-lookup"><span data-stu-id="a8faf-128">**Lambda Pipelines with Azure Cosmos DB for ingestion and query:**</span></span>

![Лямбда-конвейер для приема и запроса на основе Azure Cosmos DB](./media/change-feed/lambda.png)

<span data-ttu-id="a8faf-130">Можно использовать базу данных Azure Cosmos tooreceive и хранения данных событий из устройств, датчиков, инфраструктуры и приложений и обработать эти события в режиме реального времени с [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), или [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a8faf-130">You can use Azure Cosmos DB tooreceive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span></span> 

<span data-ttu-id="a8faf-131">В рамках вашей [без сервера](http://azure.com/serverless) веб- и мобильных приложений можно отслеживать события, такие как изменения tooyour клиента tootrigger профиль, настройки или расположения некоторых действий, таких как отправка push-уведомления tootheir устройств с помощью [Функций azure](../azure-functions/functions-bindings-documentdb.md) или [службы приложений](https://azure.microsoft.com/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="a8faf-131">Within your [serverless](http://azure.com/serverless) web and mobile apps, you can track events such as changes tooyour customer's profile, preferences, or location tootrigger certain actions like sending push notifications tootheir devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="a8faf-132">При использовании Azure Cosmos DB toobuild игры, например, можно использовать веб-канала tooimplement в режиме реального времени изменения списки лидеров, в зависимости от оценки из завершенного игры.</span><span class="sxs-lookup"><span data-stu-id="a8faf-132">If you're using Azure Cosmos DB toobuild a game, you can, for example, use change feed tooimplement real-time leaderboards based on scores from completed games.</span></span>

## <a name="how-change-feed-works-in-azure-cosmos-db"></a><span data-ttu-id="a8faf-133">Как работает веб-канал изменений в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a8faf-133">How change feed works in Azure Cosmos DB</span></span>
<span data-ttu-id="a8faf-134">Azure Cosmos DB обеспечивает возможность tooincrementally hello считывания tooan обновления, выполненные Azure Cosmos DB коллекции.</span><span class="sxs-lookup"><span data-stu-id="a8faf-134">Azure Cosmos DB provides hello ability tooincrementally read updates made tooan Azure Cosmos DB collection.</span></span> <span data-ttu-id="a8faf-135">Изменение веб-канал имеет hello следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="a8faf-135">This change feed has hello following properties:</span></span>

* <span data-ttu-id="a8faf-136">Изменения сохраняются в Azure Cosmos DB и могут обрабатываться асинхронно.</span><span class="sxs-lookup"><span data-stu-id="a8faf-136">Changes are persistent in Azure Cosmos DB and can be processed asynchronously.</span></span>
* <span data-ttu-id="a8faf-137">Toodocuments изменения в пределах коллекции доступны немедленно hello изменение веб-канала.</span><span class="sxs-lookup"><span data-stu-id="a8faf-137">Changes toodocuments within a collection are available immediately in hello change feed.</span></span>
* <span data-ttu-id="a8faf-138">Tooa каждого изменения документа отображается только один раз в hello изменение веб-канала, и клиенты управлять свою логику контрольные точки.</span><span class="sxs-lookup"><span data-stu-id="a8faf-138">Each change tooa document appears exactly once in hello change feed, and clients manage their checkpointing logic.</span></span> <span data-ttu-id="a8faf-139">Библиотека веб-канала процессора изменениями Hello предоставляет Автоматическая запись контрольных точек и «по крайней мере один раз» семантику.</span><span class="sxs-lookup"><span data-stu-id="a8faf-139">hello change feed processor library provides automatic checkpointing and "at least once" semantics.</span></span>
* <span data-ttu-id="a8faf-140">В журнал изменений hello включается только самое последнее изменение hello для данного документа.</span><span class="sxs-lookup"><span data-stu-id="a8faf-140">Only hello most recent change for a given document is included in hello change log.</span></span> <span data-ttu-id="a8faf-141">Промежуточные изменения могут быть недоступны.</span><span class="sxs-lookup"><span data-stu-id="a8faf-141">Intermediate changes may not be available.</span></span>
* <span data-ttu-id="a8faf-142">Изменение канала Hello сортируется по порядку изменения в пределах каждого значения ключа секции.</span><span class="sxs-lookup"><span data-stu-id="a8faf-142">hello change feed is sorted by order of modification within each partition key value.</span></span> <span data-ttu-id="a8faf-143">В значениях ключа раздела нет установленного порядка.</span><span class="sxs-lookup"><span data-stu-id="a8faf-143">There is no guaranteed order across partition-key values.</span></span>
* <span data-ttu-id="a8faf-144">Изменения можно синхронизировать в любой момент времени. Это означает, что фиксированный период хранения данных, для которого доступны изменения, отсутствует.</span><span class="sxs-lookup"><span data-stu-id="a8faf-144">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span></span>
* <span data-ttu-id="a8faf-145">Изменения доступны в виде фрагментов диапазонов ключей разделов.</span><span class="sxs-lookup"><span data-stu-id="a8faf-145">Changes are available in chunks of partition key ranges.</span></span> <span data-ttu-id="a8faf-146">Эта возможность позволяет изменения из toobe больших коллекций, при параллельной обработке несколько потребителей или серверов.</span><span class="sxs-lookup"><span data-stu-id="a8faf-146">This capability allows changes from large collections toobe processed in parallel by multiple consumers/servers.</span></span>
* <span data-ttu-id="a8faf-147">Приложения могут запросить для изменения нескольких веб-каналов одновременно на hello же коллекции.</span><span class="sxs-lookup"><span data-stu-id="a8faf-147">Applications can request for multiple change feeds simultaneously on hello same collection.</span></span>

<span data-ttu-id="a8faf-148">Веб-канал изменений Azure Cosmos DB включен по умолчанию для всех учетных записей.</span><span class="sxs-lookup"><span data-stu-id="a8faf-148">Azure Cosmos DB's change feed is enabled by default for all accounts.</span></span> <span data-ttu-id="a8faf-149">Можно использовать ваш [пропускная способность](request-units.md) в вашем регионе записи или любом [чтения области](distribute-data-globally.md) tooread из hello изменить веб-канал, так же, как и любой другой операции из базы данных Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="a8faf-149">You can use your [provisioned throughput](request-units.md) in your write region or any [read region](distribute-data-globally.md) tooread from hello change feed, just like any other operation from Azure Cosmos DB.</span></span> <span data-ttu-id="a8faf-150">поток изменения Hello включает операций вставки или обновления внесенные toodocuments hello коллекции.</span><span class="sxs-lookup"><span data-stu-id="a8faf-150">hello change feed includes inserts and update operations made toodocuments within hello collection.</span></span> <span data-ttu-id="a8faf-151">Вы можете отслеживать операции удаления, установив флажок soft-delete в документах вместо удаления.</span><span class="sxs-lookup"><span data-stu-id="a8faf-151">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span></span> <span data-ttu-id="a8faf-152">Кроме того, можно задать ограничение срока для документов через hello [TTL возможность](time-to-live.md)для примера, 24 часа и использование hello значение этого свойства удалит toocapture.</span><span class="sxs-lookup"><span data-stu-id="a8faf-152">Alternatively, you can set a finite expiration period for your documents via hello [TTL capability](time-to-live.md), for example, 24 hours and use hello value of that property toocapture deletes.</span></span> <span data-ttu-id="a8faf-153">Благодаря этому решению имеется tooprocess изменения в более короткий интервал времени, чем срок ЖИЗНИ hello.</span><span class="sxs-lookup"><span data-stu-id="a8faf-153">With this solution, you have tooprocess changes within a shorter time interval than hello TTL expiration period.</span></span> <span data-ttu-id="a8faf-154">Hello изменение веб-канала для каждого диапазона ключей секций в коллекции документов hello и таким образом, можно распределить между одной или более потребителей для параллельной обработки.</span><span class="sxs-lookup"><span data-stu-id="a8faf-154">hello change feed is available for each partition key range within hello document collection, and thus can be distributed across one or more consumers for parallel processing.</span></span> 

![Распределенная обработка веб-канала изменений Azure Cosmos DB](./media/change-feed/changefeedvisual.png)

<span data-ttu-id="a8faf-156">Есть несколько вариантов реализации веб-канала изменений в коде клиента.</span><span class="sxs-lookup"><span data-stu-id="a8faf-156">You have a few options in how you implement a change feed in your client code.</span></span> <span data-ttu-id="a8faf-157">Hello разделы, немедленно выполните описывают, как tooimplement hello изменение веб-канал с помощью Azure Cosmos DB REST API hello и пакеты SDK DocumentDB hello.</span><span class="sxs-lookup"><span data-stu-id="a8faf-157">hello sections that immediately follow describe how tooimplement hello change feed using hello Azure Cosmos DB REST API and hello DocumentDB SDKs.</span></span> <span data-ttu-id="a8faf-158">Однако для приложений .NET, мы рекомендуем использовать hello новый [изменение веб-канала библиотеки процессора](#change-feed-processor) для обработки события из hello изменить веб-канала, так как он упрощает чтение изменения в секциях и позволяющий нескольким потокам, работа в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="a8faf-158">However, for .NET applications, we recommend using hello new [Change feed processor library](#change-feed-processor) for processing events from hello change feed as it simplifies reading changes across partitions and enables multiple threads working in parallel.</span></span> 

## <span data-ttu-id="a8faf-159"><a id="rest-apis"></a>Работа с hello REST API и пакеты SDK DocumentDB</span><span class="sxs-lookup"><span data-stu-id="a8faf-159"><a id="rest-apis"></a>Working with hello REST API and DocumentDB SDKs</span></span>
<span data-ttu-id="a8faf-160">Azure Cosmos DB предоставляет эластичные контейнеры хранилища и пропускной способности, называемые **коллекциями**.</span><span class="sxs-lookup"><span data-stu-id="a8faf-160">Azure Cosmos DB provides elastic containers of storage and throughput called **collections**.</span></span> <span data-ttu-id="a8faf-161">Данные в коллекциях логически сгруппированы с помощью [ключей разделов](partition-data.md) для масштабируемости и производительности.</span><span class="sxs-lookup"><span data-stu-id="a8faf-161">Data within collections is logically grouped using [partition keys](partition-data.md) for scalability and performance.</span></span> <span data-ttu-id="a8faf-162">Azure Cosmos DB предоставляет различные интерфейсы API для доступа к этим данным, включая поиск по идентификатору (чтение или получение), запросы и чтение каналов (сканирования).</span><span class="sxs-lookup"><span data-stu-id="a8faf-162">Azure Cosmos DB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans).</span></span> <span data-ttu-id="a8faf-163">Hello изменение веб-канала можно получить путем заполнения два новых toohello заголовки запроса DocumentDB `ReadDocumentFeed` API и могут обрабатываться параллельно на диапазоны ключей секционирования.</span><span class="sxs-lookup"><span data-stu-id="a8faf-163">hello change feed can be obtained by populating two new request headers toohello DocumentDB `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.</span></span>

### <a name="readdocumentfeed-api"></a><span data-ttu-id="a8faf-164">Интерфейс API ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="a8faf-164">ReadDocumentFeed API</span></span>
<span data-ttu-id="a8faf-165">Давайте рассмотрим, как работает ReadDocumentFeed.</span><span class="sxs-lookup"><span data-stu-id="a8faf-165">Let's take a brief look at how ReadDocumentFeed works.</span></span> <span data-ttu-id="a8faf-166">Azure Cosmos DB поддерживает чтение веб-канал документов в коллекции посредством hello `ReadDocumentFeed` API.</span><span class="sxs-lookup"><span data-stu-id="a8faf-166">Azure Cosmos DB supports reading a feed of documents within a collection via hello `ReadDocumentFeed` API.</span></span> <span data-ttu-id="a8faf-167">Например, hello следующий запрос возвращает страницу документов внутри hello `serverlogs` коллекции.</span><span class="sxs-lookup"><span data-stu-id="a8faf-167">For example, hello following request returns a page of documents inside hello `serverlogs` collection.</span></span> 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="a8faf-168">Результаты могут быть ограничены с помощью hello `x-ms-max-item-count` заголовок и операций считывания можно возобновить, повторно подав запрос hello с `x-ms-continuation` заголовок возвращается в hello предыдущего ответа.</span><span class="sxs-lookup"><span data-stu-id="a8faf-168">Results can be limited by using hello `x-ms-max-item-count` header, and reads can be resumed by resubmitting hello request with a `x-ms-continuation` header returned in hello previous response.</span></span> <span data-ttu-id="a8faf-169">При выполнении из единого клиента `ReadDocumentFeed` выполняет итерацию результатов по разделам последовательно.</span><span class="sxs-lookup"><span data-stu-id="a8faf-169">When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially.</span></span> 

<span data-ttu-id="a8faf-170">**Веб-канал для последовательного чтения документов**</span><span class="sxs-lookup"><span data-stu-id="a8faf-170">**Serial read document feed**</span></span>

<span data-ttu-id="a8faf-171">Вы также можете получить веб-канал hello документов с помощью одного из поддерживаемых hello [пакеты SDK Azure Cosmos DB](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="a8faf-171">You can also retrieve hello feed of documents using one of hello supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="a8faf-172">Например, hello следующем фрагменте кода показан способ toouse hello [ReadDocumentFeedAsync метод](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) в .NET.</span><span class="sxs-lookup"><span data-stu-id="a8faf-172">For example, hello following snippet shows how toouse hello [ReadDocumentFeedAsync method](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span></span>

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a><span data-ttu-id="a8faf-173">Распределенное выполнение ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="a8faf-173">Distributed execution of ReadDocumentFeed</span></span>
<span data-ttu-id="a8faf-174">Для коллекций, содержащих терабайты данных и более или принимающих большое количество обновлений, последовательное выполнение веб-канала чтения с компьютера с одним клиентом может оказаться нецелесообразным.</span><span class="sxs-lookup"><span data-stu-id="a8faf-174">For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical.</span></span> <span data-ttu-id="a8faf-175">В порядке toosupport этих сценариях большие наборы данных Azure Cosmos DB предоставляет toodistribute API-интерфейсы `ReadDocumentFeed` вызовы прозрачно через несколько клиентских средств чтения и потребителей.</span><span class="sxs-lookup"><span data-stu-id="a8faf-175">In order toosupport these big data scenarios, Azure Cosmos DB provides APIs toodistribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers.</span></span> 

<span data-ttu-id="a8faf-176">**Веб-канал для распределенного чтения документов**</span><span class="sxs-lookup"><span data-stu-id="a8faf-176">**Distributed Read Document Feed**</span></span>

<span data-ttu-id="a8faf-177">tooprovide масштабируемой обработки добавочных изменений Azure Cosmos DB поддерживает модель масштабного для изменения hello API на основе диапазонов ключей разделов веб-канала.</span><span class="sxs-lookup"><span data-stu-id="a8faf-177">tooprovide scalable processing of incremental changes, Azure Cosmos DB supports a scale-out model for hello change feed API based on ranges of partition keys.</span></span>

* <span data-ttu-id="a8faf-178">Список диапазонов ключей разделов для коллекции можно получить, выполнив вызов `ReadPartitionKeyRanges`.</span><span class="sxs-lookup"><span data-stu-id="a8faf-178">You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call.</span></span> 
* <span data-ttu-id="a8faf-179">Для каждого диапазона ключей секций можно выполнить `ReadDocumentFeed` tooread документов с помощью разделов в пределах диапазона.</span><span class="sxs-lookup"><span data-stu-id="a8faf-179">For each partition key range, you can perform a `ReadDocumentFeed` tooread documents with partition keys within that range.</span></span>

### <a name="retrieving-partition-key-ranges-for-a-collection"></a><span data-ttu-id="a8faf-180">Извлечение диапазонов ключей разделов для коллекции</span><span class="sxs-lookup"><span data-stu-id="a8faf-180">Retrieving partition key ranges for a collection</span></span>
<span data-ttu-id="a8faf-181">Вы можете получить диапазонов ключей секционирования hello, запрашивающего hello `pkranges` ресурсов в пределах коллекции.</span><span class="sxs-lookup"><span data-stu-id="a8faf-181">You can retrieve hello partition key ranges by requesting hello `pkranges` resource within a collection.</span></span> <span data-ttu-id="a8faf-182">Например hello следующий запрос извлекает список hello диапазонов ключа секции для hello `serverlogs` коллекции:</span><span class="sxs-lookup"><span data-stu-id="a8faf-182">For example hello following request retrieves hello list of partition key ranges for hello `serverlogs` collection:</span></span>

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

<span data-ttu-id="a8faf-183">Этот запрос возвращает следующий ответ, содержащий метаданные о диапазонов ключей секционирования hello hello:</span><span class="sxs-lookup"><span data-stu-id="a8faf-183">This request returns hello following response containing metadata about hello partition key ranges:</span></span>

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


<span data-ttu-id="a8faf-184">**Свойства ключа диапазона секционирования**: каждый раздел диапазон включает свойства метаданных hello в hello в следующей таблице:</span><span class="sxs-lookup"><span data-stu-id="a8faf-184">**Partition key range properties**: Each partition key range includes hello metadata properties in hello following table:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="a8faf-185">Имя заголовка</span><span class="sxs-lookup"><span data-stu-id="a8faf-185">Header name</span></span></th>
        <th><span data-ttu-id="a8faf-186">Описание</span><span class="sxs-lookup"><span data-stu-id="a8faf-186">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="a8faf-187">id</span><span class="sxs-lookup"><span data-stu-id="a8faf-187">id</span></span></td>
        <td>
            <p><span data-ttu-id="a8faf-188">Идентификатор Hello hello диапазона ключей секций.</span><span class="sxs-lookup"><span data-stu-id="a8faf-188">hello ID for hello partition key range.</span></span> <span data-ttu-id="a8faf-189">Это стабильный и уникальный идентификатор в каждой коллекции.</span><span class="sxs-lookup"><span data-stu-id="a8faf-189">This is a stable and unique ID within each collection.</span></span></p>
            <p><span data-ttu-id="a8faf-190">Должен использоваться в следующие отличия tooread вызов hello диапазона ключей секций.</span><span class="sxs-lookup"><span data-stu-id="a8faf-190">Must be used in hello following call tooread changes by partition key range.</span></span></p>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="a8faf-191">maxExclusive</span><span class="sxs-lookup"><span data-stu-id="a8faf-191">maxExclusive</span></span></td>
        <td><span data-ttu-id="a8faf-192">Hello секции максимальное значение хэш ключа для диапазона ключей секций hello.</span><span class="sxs-lookup"><span data-stu-id="a8faf-192">hello maximum partition key hash value for hello partition key range.</span></span> <span data-ttu-id="a8faf-193">Для внутреннего использования.</span><span class="sxs-lookup"><span data-stu-id="a8faf-193">For internal use.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="a8faf-194">minInclusive</span><span class="sxs-lookup"><span data-stu-id="a8faf-194">minInclusive</span></span></td>
        <td><span data-ttu-id="a8faf-195">значение хэш ключа Hello минимальное секции для диапазона ключей секций hello.</span><span class="sxs-lookup"><span data-stu-id="a8faf-195">hello minimum partition key hash value for hello partition key range.</span></span> <span data-ttu-id="a8faf-196">Для внутреннего использования.</span><span class="sxs-lookup"><span data-stu-id="a8faf-196">For internal use.</span></span></td>
    </tr>       
</table>

<span data-ttu-id="a8faf-197">Это можно сделать с помощью одного из поддерживаемых hello [пакеты SDK Azure Cosmos DB](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="a8faf-197">You can do this using one of hello supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="a8faf-198">Hello следующем фрагменте кода показано, как ключ раздела tooretrieve диапазоны в .NET с помощью hello [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) метод.</span><span class="sxs-lookup"><span data-stu-id="a8faf-198">For example, hello following snippet shows how tooretrieve partition key ranges in .NET using hello [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) method.</span></span>

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

<span data-ttu-id="a8faf-199">Azure Cosmos DB поддерживает получение документов по диапазона ключей секций, установка hello необязательно `x-ms-documentdb-partitionkeyrangeid` заголовок.</span><span class="sxs-lookup"><span data-stu-id="a8faf-199">Azure Cosmos DB supports retrieval of documents per partition key range by setting hello optional `x-ms-documentdb-partitionkeyrangeid` header.</span></span> 

### <a name="performing-an-incremental-readdocumentfeed"></a><span data-ttu-id="a8faf-200">Выполнение добавочного ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="a8faf-200">Performing an incremental ReadDocumentFeed</span></span>
<span data-ttu-id="a8faf-201">ReadDocumentFeed поддерживает следующие сценарии и задачи для добавочной обработки изменений в коллекции Azure Cosmos DB hello:</span><span class="sxs-lookup"><span data-stu-id="a8faf-201">ReadDocumentFeed supports hello following scenarios/tasks for incremental processing of changes in Azure Cosmos DB collections:</span></span>

* <span data-ttu-id="a8faf-202">Чтение всех изменяет toodocuments с начала hello, то есть создание коллекции.</span><span class="sxs-lookup"><span data-stu-id="a8faf-202">Read all changes toodocuments from hello beginning, that is, from collection creation.</span></span>
* <span data-ttu-id="a8faf-203">Чтение всех изменений toodocuments toofuture обновлений из текущего времени или все изменения с момента времени, определяемый пользователем.</span><span class="sxs-lookup"><span data-stu-id="a8faf-203">Read all changes toofuture updates toodocuments from current time, or any changes since a user-specified time.</span></span>
* <span data-ttu-id="a8faf-204">Чтение всех изменений toodocuments из логическую версию коллекции hello (ETag).</span><span class="sxs-lookup"><span data-stu-id="a8faf-204">Read all changes toodocuments from a logical version of hello collection (ETag).</span></span> <span data-ttu-id="a8faf-205">Вы можете потребителей на основании hello ETag, возвращенные добавочных запросов чтения канала контрольной точки.</span><span class="sxs-lookup"><span data-stu-id="a8faf-205">You can checkpoint your consumers based on hello returned ETag from incremental read-feed requests.</span></span>

<span data-ttu-id="a8faf-206">Hello изменения включают в себя toodocuments вставок и обновлений.</span><span class="sxs-lookup"><span data-stu-id="a8faf-206">hello changes include inserts and updates toodocuments.</span></span> <span data-ttu-id="a8faf-207">Удаляет toocapture, следует использовать свойство «обратимое удаление» по документам, или использовать hello [встроенного свойства TTL](time-to-live.md) toosignal Ожидается удаление в hello изменить веб-канала.</span><span class="sxs-lookup"><span data-stu-id="a8faf-207">toocapture deletes, you must use a "soft delete" property within your documents, or use hello [built-in TTL property](time-to-live.md) toosignal a pending deletion in hello change feed.</span></span>

<span data-ttu-id="a8faf-208">Здравствуйте, следующие списки hello таблицы [запроса](/rest/api/documentdb/common-documentdb-rest-request-headers.md) и [заголовки ответа](/rest/api/documentdb/common-documentdb-rest-response-headers.md) ReadDocumentFeed операций.</span><span class="sxs-lookup"><span data-stu-id="a8faf-208">hello following table lists hello [request](/rest/api/documentdb/common-documentdb-rest-request-headers.md) and [response headers](/rest/api/documentdb/common-documentdb-rest-response-headers.md) for ReadDocumentFeed operations.</span></span>

<span data-ttu-id="a8faf-209">**Заголовки запроса для добавочного ReadDocumentFeed**</span><span class="sxs-lookup"><span data-stu-id="a8faf-209">**Request headers for incremental ReadDocumentFeed**:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="a8faf-210">Имя заголовка</span><span class="sxs-lookup"><span data-stu-id="a8faf-210">Header name</span></span></th>
        <th><span data-ttu-id="a8faf-211">Описание</span><span class="sxs-lookup"><span data-stu-id="a8faf-211">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="a8faf-212">A-IM</span><span class="sxs-lookup"><span data-stu-id="a8faf-212">A-IM</span></span></td>
        <td><span data-ttu-id="a8faf-213">Необходимо задать слишком «Incremental канала» или опущен, в противном случае</span><span class="sxs-lookup"><span data-stu-id="a8faf-213">Must be set too"Incremental feed", or omitted otherwise</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="a8faf-214">If-None-Match</span><span class="sxs-lookup"><span data-stu-id="a8faf-214">If-None-Match</span></span></td>
        <td>
            <p><span data-ttu-id="a8faf-215">Нет заголовка: возвращает все изменения из hello начиная (Создание коллекции)</span><span class="sxs-lookup"><span data-stu-id="a8faf-215">No header: returns all changes from hello beginning (collection creation)</span></span></p>
            <p><span data-ttu-id="a8faf-216">«*»: возвращает все новые toodata изменения в коллекции hello</span><span class="sxs-lookup"><span data-stu-id="a8faf-216">"*": returns all new changes toodata within hello collection</span></span></p>         
            <p><span data-ttu-id="a8faf-217">&lt;eTag&gt;: Если значение коллекции tooa ETag, возвращает все изменения, внесенные с момента этого логического отметки времени</span><span class="sxs-lookup"><span data-stu-id="a8faf-217">&lt;etag&gt;: If set tooa collection ETag, returns all changes made since that logical timestamp</span></span></p>
        </td>
    </tr>
    <tr>    
        <td><span data-ttu-id="a8faf-218">If-Modified-Since</span><span class="sxs-lookup"><span data-stu-id="a8faf-218">If-Modified-Since</span></span></td> 
        <td><span data-ttu-id="a8faf-219">Формат времени RFC 1123. Не учитывается, если указан заголовок If-None-Match.</span><span class="sxs-lookup"><span data-stu-id="a8faf-219">RFC 1123 time format; ignored if If-None-Match is specified</span></span></td> 
    </tr> 
    <tr>
        <td><span data-ttu-id="a8faf-220">x-ms-documentdb-partitionkeyrangeid</span><span class="sxs-lookup"><span data-stu-id="a8faf-220">x-ms-documentdb-partitionkeyrangeid</span></span></td>
        <td><span data-ttu-id="a8faf-221">Hello идентификатор секции диапазона ключей для считывания данных.</span><span class="sxs-lookup"><span data-stu-id="a8faf-221">hello partition key range ID for reading data.</span></span></td>
    </tr>
</table>

<span data-ttu-id="a8faf-222">**Заголовки ответа для добавочного ReadDocumentFeed**</span><span class="sxs-lookup"><span data-stu-id="a8faf-222">**Response headers for incremental ReadDocumentFeed**:</span></span>

<table> <tr>
        <th><span data-ttu-id="a8faf-223">Имя заголовка</span><span class="sxs-lookup"><span data-stu-id="a8faf-223">Header name</span></span></th>
        <th><span data-ttu-id="a8faf-224">Описание</span><span class="sxs-lookup"><span data-stu-id="a8faf-224">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="a8faf-225">etag</span><span class="sxs-lookup"><span data-stu-id="a8faf-225">etag</span></span></td>
        <td>
            <p><span data-ttu-id="a8faf-226">Hello логических порядковый номер (LSN) последней документа, возвращаемый в ответе hello.</span><span class="sxs-lookup"><span data-stu-id="a8faf-226">hello logical sequence number (LSN) of last document returned in hello response.</span></span></p>
            <p><span data-ttu-id="a8faf-227">Добавочный ReadDocumentFeed можно возобновить, повторно задав это значение в параметре If-None-Match.</span><span class="sxs-lookup"><span data-stu-id="a8faf-227">Incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</span></span></p>
        </td>
    </tr>
</table>

<span data-ttu-id="a8faf-228">Ниже приведен пример запроса tooreturn все добавочные изменения в коллекции из логических версии в hello ETag `28535` и секции диапазона ключей = `16`:</span><span class="sxs-lookup"><span data-stu-id="a8faf-228">Here's a sample request tooreturn all incremental changes in collection from hello logical version/ETag `28535` and partition key range = `16`:</span></span>

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

<span data-ttu-id="a8faf-229">Изменения, упорядочиваются по времени в пределах каждого значения ключа секции в пределах диапазона ключей секций hello.</span><span class="sxs-lookup"><span data-stu-id="a8faf-229">Changes are ordered by time within each partition key value within hello partition key range.</span></span> <span data-ttu-id="a8faf-230">В значениях ключа раздела нет установленного порядка.</span><span class="sxs-lookup"><span data-stu-id="a8faf-230">There is no guaranteed order across partition-key values.</span></span> <span data-ttu-id="a8faf-231">Если доступно больше результатов, чем может поместиться на одной странице, можно прочитать hello следующей страницы результатов, повторно подав запрос hello с hello `If-None-Match` заголовок с значение равно toohello `etag` из предыдущего ответа hello.</span><span class="sxs-lookup"><span data-stu-id="a8faf-231">If there are more results than can fit in a single page, you can read hello next page of results by resubmitting hello request with hello `If-None-Match` header with value equal toohello `etag` from hello previous response.</span></span> <span data-ttu-id="a8faf-232">Если несколько документов были вставлены или обновлены на уровне транзакций, в пределах хранимой процедуры или триггера, они все возвращается в hello же страницу "ответ".</span><span class="sxs-lookup"><span data-stu-id="a8faf-232">If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within hello same response page.</span></span>

> [!NOTE]
> <span data-ttu-id="a8faf-233">С веб-каналом изменений, можно получить дополнительные элементы, которые возвращаются на странице, чем указано в `x-ms-max-item-count` в случае hello несколько документов, вставленных или обновленных в хранимых процедурах или триггерах.</span><span class="sxs-lookup"><span data-stu-id="a8faf-233">With change feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in hello case of multiple documents inserted or updated inside a stored procedures or triggers.</span></span> 

<span data-ttu-id="a8faf-234">При использовании hello .NET SDK (1.17.0), задать поле hello `StartTime` в `ChangeFeedOptions` документов toodirectly возвращаемого изменены с момента `StartTime` при вызове `CreateDocumentChangeFeedQuery`.</span><span class="sxs-lookup"><span data-stu-id="a8faf-234">When using hello .NET SDK (1.17.0), set hello field `StartTime` in `ChangeFeedOptions` toodirectly return changed documents since `StartTime` when calling  `CreateDocumentChangeFeedQuery`.</span></span> <span data-ttu-id="a8faf-235">Указав `If-Modified-Since` с помощью API-интерфейса REST hello, запрос будет возвращать не hello документы сами, но вместо токен продолжения hello или `etag` в заголовке ответа hello.</span><span class="sxs-lookup"><span data-stu-id="a8faf-235">By specifying `If-Modified-Since` using hello REST API, your request will return not hello documents themselves, but rather hello continuation token or `etag` in hello response header.</span></span> <span data-ttu-id="a8faf-236">измененный hello указано время токен продолжения hello документы hello tooreturn `etag` необходимо использовать в запросе Далее hello с `If-None-Match` tooreturn hello фактическое документов.</span><span class="sxs-lookup"><span data-stu-id="a8faf-236">tooreturn hello documents modified hello specified time, hello continuation token `etag` must then be used in hello next request with `If-None-Match` tooreturn hello actual documents.</span></span> 

<span data-ttu-id="a8faf-237">Hello .NET SDK предоставляет hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) и [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) вспомогательные классы tooaccess изменения, внесенные tooa коллекции.</span><span class="sxs-lookup"><span data-stu-id="a8faf-237">hello .NET SDK provides hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) and [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper classes tooaccess changes made tooa collection.</span></span> <span data-ttu-id="a8faf-238">Hello следующий фрагмент кода показывает, как изменяется tooretrieve все с начала hello hello .NET SDK от одного клиента с помощью.</span><span class="sxs-lookup"><span data-stu-id="a8faf-238">hello following snippet shows how tooretrieve all changes from hello beginning using hello .NET SDK from a single client.</span></span>

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
<span data-ttu-id="a8faf-239">И hello следующий фрагмент кода показывает, как изменяется tooprocess в режиме реального времени с помощью DB Cosmos Azure с помощью изменений hello канала поддержки и hello предшествующий функции.</span><span class="sxs-lookup"><span data-stu-id="a8faf-239">And hello following snippet shows how tooprocess changes in real-time with Azure Cosmos DB by using hello change feed support and hello preceding function.</span></span> <span data-ttu-id="a8faf-240">Первый вызов функции Hello возвращает все документы hello в коллекции hello и hello второй только возвращает hello двух документов, созданных, созданные с момента последней контрольной точки hello.</span><span class="sxs-lookup"><span data-stu-id="a8faf-240">hello first call returns all hello documents in hello collection, and hello second only returns hello two documents created that were created since hello last checkpoint.</span></span>

```csharp
// Returns all documents in hello collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only hello two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

<span data-ttu-id="a8faf-241">Также можно фильтровать с помощью событий на стороне логику tooselectively процесс сервера веб-канал изменение hello.</span><span class="sxs-lookup"><span data-stu-id="a8faf-241">You can also filter hello change feed using client side logic tooselectively process events.</span></span> <span data-ttu-id="a8faf-242">Например ниже приведен фрагмент, который использует tooprocess LINQ стороне клиента только для событий изменения температуры от датчиков устройства.</span><span class="sxs-lookup"><span data-stu-id="a8faf-242">For example, here's a snippet that uses client side LINQ tooprocess only temperature change events from device sensors.</span></span>

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <span data-ttu-id="a8faf-243"><a id="change-feed-processor"></a>Библиотека обработчика веб-канала изменений</span><span class="sxs-lookup"><span data-stu-id="a8faf-243"><a id="change-feed-processor"></a>Change Feed Processor library</span></span>
<span data-ttu-id="a8faf-244">Другой вариант — toouse hello [библиотеки Azure Cosmos DB изменить веб-канал процессора](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), который поможет вам легко распространять событий обработки из-за изменения веб-канал по нескольким получателям.</span><span class="sxs-lookup"><span data-stu-id="a8faf-244">Another option is toouse hello [Azure Cosmos DB Change Feed Processor library](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), which can help you easily distribute event processing from a change feed across multiple consumers.</span></span> <span data-ttu-id="a8faf-245">Библиотека Hello отлично подходит для создания веб-канала чтения на платформе .NET hello изменений.</span><span class="sxs-lookup"><span data-stu-id="a8faf-245">hello library is great for building change feed readers on hello .NET platform.</span></span> <span data-ttu-id="a8faf-246">Некоторые рабочие процессы, которые бы упростить с помощью библиотеки hello процессора канала изменений по сравнению с методами hello, включенных в hello других пакетов SDK DB Cosmos включают:</span><span class="sxs-lookup"><span data-stu-id="a8faf-246">Some workflows that would be simplified by using hello Change Feed Processor library over hello methods included in hello other Cosmos DB SDKs include:</span></span> 

* <span data-ttu-id="a8faf-247">Извлечение обновлений из веб-канала изменений, когда данные хранятся в нескольких секциях.</span><span class="sxs-lookup"><span data-stu-id="a8faf-247">Pulling updates from change feed when data is stored across multiple partitions</span></span>
* <span data-ttu-id="a8faf-248">Перемещение или репликация данных из одной коллекции tooanother</span><span class="sxs-lookup"><span data-stu-id="a8faf-248">Moving or replicating data from one collection tooanother</span></span>
* <span data-ttu-id="a8faf-249">Параллельное выполнение действий, запускаемые toodata обновлений и изменение веб-канала</span><span class="sxs-lookup"><span data-stu-id="a8faf-249">Parallel execution of actions triggered by updates toodata and change feed</span></span> 

<span data-ttu-id="a8faf-250">Хотя с помощью hello API-интерфейсы в hello Cosmos SDK предоставляет toochange точно управлять доступом веб-канал обновлений в каждой секции, с помощью библиотеки изменение веб-канала процессора hello упрощает чтение изменения по секции и параллельная работа нескольких потоков.</span><span class="sxs-lookup"><span data-stu-id="a8faf-250">While using hello APIs in hello Cosmos SDKs provides precise access toochange feed updates in each partition, using hello Change Feed Processor library simplifies reading changes across partitions and multiple threads working in parallel.</span></span> <span data-ttu-id="a8faf-251">Вместо вручную считывания изменений из каждого контейнера и сохранение токен продолжения для каждой секции hello изменение веб-канала процессора автоматически управляет чтения изменения в секциях с помощью механизма аренды.</span><span class="sxs-lookup"><span data-stu-id="a8faf-251">Instead of manually reading changes from each container and saving a continuation token for each partition, hello Change Feed Processor automatically manages reading changes across partitions using a lease mechanism.</span></span>

<span data-ttu-id="a8faf-252">Библиотека Hello доступна как пакет NuGet: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) и из исходного кода, как Github [пример](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span><span class="sxs-lookup"><span data-stu-id="a8faf-252">hello library is available as a NuGet Package: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) and from source code as a Github [sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span></span> 

### <a name="understanding-change-feed-processor-library"></a><span data-ttu-id="a8faf-253">Основные сведения о библиотеке обработчика веб-канала изменений</span><span class="sxs-lookup"><span data-stu-id="a8faf-253">Understanding Change Feed Processor library</span></span> 

<span data-ttu-id="a8faf-254">Существует четыре основных компонентов реализации hello изменение процессора веб-канала: hello отслеживаемых коллекции, коллекции аренды hello, узел обработчика hello и потребители hello.</span><span class="sxs-lookup"><span data-stu-id="a8faf-254">There are four main components of implementing hello Change Feed Processor: hello monitored collection, hello lease collection, hello processor host, and hello consumers.</span></span> 

<span data-ttu-id="a8faf-255">**Сбор данных о наблюдаемых:** hello отслеживаемых собираются из какой hello создается изменение веб-канала данных hello.</span><span class="sxs-lookup"><span data-stu-id="a8faf-255">**Monitored Collection:** hello monitored collection is hello data from which hello change feed is generated.</span></span> <span data-ttu-id="a8faf-256">Любой коллекции toohello мониторинг операций вставки и изменения отражаются в канал передачи изменений hello hello коллекции.</span><span class="sxs-lookup"><span data-stu-id="a8faf-256">Any inserts and changes toohello monitored collection are reflected in hello change feed of hello collection.</span></span> 

<span data-ttu-id="a8faf-257">**Сбор данных аренды:** hello координаты коллекции аренды обработки изменений hello веб-канала для нескольких сотрудников.</span><span class="sxs-lookup"><span data-stu-id="a8faf-257">**Lease Collection:** hello lease collection coordinates processing hello change feed across multiple workers.</span></span> <span data-ttu-id="a8faf-258">Коллекция отдельных — используется toostore hello аренды с арендой одной на каждую секцию.</span><span class="sxs-lookup"><span data-stu-id="a8faf-258">A separate collection is used toostore hello leases with one lease per partition.</span></span> <span data-ttu-id="a8faf-259">Это выгодно toostore этой коллекции аренды на другую учетную запись с hello записи ближе toowhere hello область которой выполняется замена процессора веб-канала.</span><span class="sxs-lookup"><span data-stu-id="a8faf-259">It is advantageous toostore this lease collection on a different account with hello write region closer toowhere hello Change Feed Processor is running.</span></span> <span data-ttu-id="a8faf-260">Объект аренды содержит hello следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="a8faf-260">A lease object contains hello following attributes:</span></span> 
* <span data-ttu-id="a8faf-261">Владелец: Указывает, hello узла, которому принадлежит hello аренды</span><span class="sxs-lookup"><span data-stu-id="a8faf-261">Owner: Specifies hello host that owns hello lease</span></span>
* <span data-ttu-id="a8faf-262">Продолжение: Определяет положение hello (токен продолжения) в веб-канала для определенного раздела Изменение hello</span><span class="sxs-lookup"><span data-stu-id="a8faf-262">Continuation: Specifies hello position (continuation token) in hello change feed for a particular partition</span></span>
* <span data-ttu-id="a8faf-263">Отметка времени: Время последнего обновления аренды; Отметка времени Hello может быть используется toocheck ли hello аренды считается недействительным</span><span class="sxs-lookup"><span data-stu-id="a8faf-263">Timestamp: Last time lease was updated; hello timestamp can be used toocheck whether hello lease is considered expired</span></span> 

<span data-ttu-id="a8faf-264">**Узел обработчика:** каждого узла определяет, сколько секций tooprocess зависимости от того, сколько других экземпляров узлов имеют активную аренду.</span><span class="sxs-lookup"><span data-stu-id="a8faf-264">**Processor Host:** Each host determines how many partitions tooprocess based on how many other instances of hosts have active leases.</span></span> 
1.  <span data-ttu-id="a8faf-265">При запуске узла, он получает рабочей нагрузки hello toobalance аренды на всех узлах.</span><span class="sxs-lookup"><span data-stu-id="a8faf-265">When a host starts up, it acquires leases toobalance hello workload across all hosts.</span></span> <span data-ttu-id="a8faf-266">Узел периодически обновляет аренды, чтобы они оставалась активными.</span><span class="sxs-lookup"><span data-stu-id="a8faf-266">A host periodically renews leases, so leases remain active.</span></span> 
2.  <span data-ttu-id="a8faf-267">Узел контрольные точки hello последнего продолжение токена tooits аренду для каждой операции чтения.</span><span class="sxs-lookup"><span data-stu-id="a8faf-267">A host checkpoints hello last continuation token tooits lease for each read.</span></span> <span data-ttu-id="a8faf-268">tooensure параллелизма, узел проверок hello ETag для каждого обновления аренды.</span><span class="sxs-lookup"><span data-stu-id="a8faf-268">tooensure concurrency safety, a host checks hello ETag for each lease update.</span></span> <span data-ttu-id="a8faf-269">Также поддерживаются другие стратегии контрольных точек.</span><span class="sxs-lookup"><span data-stu-id="a8faf-269">Other checkpoint strategies are also supported.</span></span>  
3.  <span data-ttu-id="a8faf-270">После завершения работы узел отменяет все аренды адресов, но сохраняет hello сведения о продолжении, чтобы можно было продолжить чтение из контрольной точки хранимых hello позже.</span><span class="sxs-lookup"><span data-stu-id="a8faf-270">Upon shutdown, a host releases all leases but keeps hello continuation information, so it can resume reading from hello stored checkpoint later.</span></span> 

<span data-ttu-id="a8faf-271">В настоящее время hello количеством узлов не может быть больше hello количество секций (аренды).</span><span class="sxs-lookup"><span data-stu-id="a8faf-271">At this time hello number of hosts cannot be greater than hello number of partitions (leases).</span></span>

<span data-ttu-id="a8faf-272">**Потребители:** клиентов или сотрудников, являются потоки, выполняющие hello изменение веб-канал обработки, инициированных каждого узла.</span><span class="sxs-lookup"><span data-stu-id="a8faf-272">**Consumers:** Consumers, or workers, are threads that perform hello change feed processing initiated by each host.</span></span> <span data-ttu-id="a8faf-273">Каждый узел обработчика может иметь несколько объектов-получателей.</span><span class="sxs-lookup"><span data-stu-id="a8faf-273">Each processor host can have multiple consumers.</span></span> <span data-ttu-id="a8faf-274">Каждый потребитель считывает hello изменение веб-канала из hello секции, ей назначается tooand уведомляет ведущим изменений и окончание срока действия аренды.</span><span class="sxs-lookup"><span data-stu-id="a8faf-274">Each consumer reads hello change feed from hello partition it is assigned tooand notifies its host of changes and expired leases.</span></span>

<span data-ttu-id="a8faf-275">toofurther понять взаимосвязи между этими четырьмя элементами, изменение канала процессора, давайте рассмотрим пример, в hello следующие схемы.</span><span class="sxs-lookup"><span data-stu-id="a8faf-275">toofurther understand how these four elements of Change Feed Processor work together, let's look at an example in hello following diagram.</span></span> <span data-ttu-id="a8faf-276">Hello отслеживания документов хранилищ коллекции и использует hello «Город» в качестве ключа секции hello.</span><span class="sxs-lookup"><span data-stu-id="a8faf-276">hello monitored collection stores documents and uses hello "city" as hello partition key.</span></span> <span data-ttu-id="a8faf-277">Мы видим, hello синий раздел содержит документы с hello поле «Город» из «A-E» и т. д.</span><span class="sxs-lookup"><span data-stu-id="a8faf-277">We see that hello blue partition contains documents with hello "city" field from "A-E" and so on.</span></span> <span data-ttu-id="a8faf-278">Существует два узла, каждый с двумя потребители считывании hello четырех секций одновременно.</span><span class="sxs-lookup"><span data-stu-id="a8faf-278">There are two hosts, each with two consumers reading from hello four partitions in parallel.</span></span> <span data-ttu-id="a8faf-279">стрелки Hello видно, что потребитель hello, чтения из конкретной точки в hello изменить веб-канала.</span><span class="sxs-lookup"><span data-stu-id="a8faf-279">hello arrows show hello consumers reading from a specific spot in hello change feed.</span></span> <span data-ttu-id="a8faf-280">В первом разделе hello hello темнее синий представляет непрочитанные изменения, а hello светло-синий представляет hello, прочитанные изменения на веб-канал изменение hello.</span><span class="sxs-lookup"><span data-stu-id="a8faf-280">In hello first partition, hello darker blue represents unread changes while hello light blue represents hello already read changes on hello change feed.</span></span> <span data-ttu-id="a8faf-281">Hello узлы используют hello аренды коллекции toostore за tookeep значение «продолжение» hello текущего чтения позиции для каждого объекта-получателя.</span><span class="sxs-lookup"><span data-stu-id="a8faf-281">hello hosts use hello lease collection toostore a "continuation" value tookeep track of hello current reading position for each consumer.</span></span> 

![Изменение размера базы данных Azure Cosmos hello с помощью веб-канала процессора узла](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a><span data-ttu-id="a8faf-283">Использование библиотеки обработчика веб-канала изменений</span><span class="sxs-lookup"><span data-stu-id="a8faf-283">Using Change Feed Processor Library</span></span> 
<span data-ttu-id="a8faf-284">Hello в следующем разделе описывается, как toouse hello изменение процессора веб-канала библиотеки в контексте hello репликации изменений из источника коллекции tooa назначения коллекции.</span><span class="sxs-lookup"><span data-stu-id="a8faf-284">hello following section explains how toouse hello Change Feed Processor library in hello context of replicating changes from a source collection tooa destination collection.</span></span> <span data-ttu-id="a8faf-285">Здесь hello исходной коллекции является коллекцией hello отслеживаемых изменений процессора веб-канала.</span><span class="sxs-lookup"><span data-stu-id="a8faf-285">Here, hello source collection is hello monitored collection in Change Feed Processor.</span></span> 

<span data-ttu-id="a8faf-286">**Установите и включите пакет NuGet обработчика веб-канала изменение hello**</span><span class="sxs-lookup"><span data-stu-id="a8faf-286">**Install and include hello Change Feed Processor NuGet package**</span></span> 

<span data-ttu-id="a8faf-287">Прежде чем устанавливать пакет NuGet обработчика веб-канала изменений, установите:</span><span class="sxs-lookup"><span data-stu-id="a8faf-287">Before installing Change Feed Processor NuGet Package, first install:</span></span> 
* <span data-ttu-id="a8faf-288">Библиотеку Microsoft.Azure.DocumentDB (версии 1.13.1 или выше).</span><span class="sxs-lookup"><span data-stu-id="a8faf-288">Microsoft.Azure.DocumentDB, version 1.13.1 or above</span></span> 
* <span data-ttu-id="a8faf-289">Newtonsoft.Json, версии 9.0.1 или более поздней версии. Установите пакет `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` и добавьте его в качестве ссылки.</span><span class="sxs-lookup"><span data-stu-id="a8faf-289">Newtonsoft.Json, version 9.0.1 or above Install `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` and include it as a reference.</span></span>

<span data-ttu-id="a8faf-290">**Создайте отслеживаемую коллекцию, коллекцию аренд и назначения**</span><span class="sxs-lookup"><span data-stu-id="a8faf-290">**Create a monitored, lease and destination collection**</span></span> 

<span data-ttu-id="a8faf-291">В порядке toouse hello библиотеку потоков процессора изменений hello аренды коллекции должен toobe, созданные перед выполнением hello узлами процессора.</span><span class="sxs-lookup"><span data-stu-id="a8faf-291">In order toouse hello Change Feed Processor Library, hello lease collection needs toobe created before running hello processor host(s).</span></span> <span data-ttu-id="a8faf-292">Еще раз рекомендуется хранить коллекции аренды на другую учетную запись с hello записи регион ближе toowhere что выполняется замена процессора веб-канала.</span><span class="sxs-lookup"><span data-stu-id="a8faf-292">Again, we recommend storing a lease collection on a different account with a write region closer toowhere hello Change Feed Processor is running.</span></span> <span data-ttu-id="a8faf-293">В этом примере перемещения данных нужно toocreate hello целевой коллекции перед запуском узел обработчика веб-канала изменение hello.</span><span class="sxs-lookup"><span data-stu-id="a8faf-293">In this data movement example, we need toocreate hello destination collection before running hello Change Feed Processor host.</span></span> <span data-ttu-id="a8faf-294">В примере кода hello мы называем отслеживаемых, toocreate hello вспомогательный метод арендован и целевой коллекции, если они еще не существует.</span><span class="sxs-lookup"><span data-stu-id="a8faf-294">In hello sample code we call a helper method toocreate hello monitored, leased, and destination collections if they do not already exist.</span></span> 

> [!WARNING]
> <span data-ttu-id="a8faf-295">Создание коллекции имеет цены последствия, как при резервировании пропускной способности для hello toocommunicate приложений с Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a8faf-295">Creating a collection has pricing implications, as you are reserving throughput for hello application toocommunicate with Azure Cosmos DB.</span></span> <span data-ttu-id="a8faf-296">Для получения дополнительных сведений посетите hello [странице цен](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="a8faf-296">For more details, please visit hello [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

<span data-ttu-id="a8faf-297">*Создание узла обработчика*</span><span class="sxs-lookup"><span data-stu-id="a8faf-297">*Creating a processor host*</span></span>

<span data-ttu-id="a8faf-298">Hello `ChangeFeedProcessorHost` класс предоставляет среду выполнения потокобезопасна, несколькими процессами, безопасного для реализаций обработчиков событий, которая также обеспечивает управление аренды назначение контрольных точек и секции.</span><span class="sxs-lookup"><span data-stu-id="a8faf-298">hello `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.</span></span> <span data-ttu-id="a8faf-299">toouse hello `ChangeFeedProcessorHost` , можно реализовать `IChangeFeedObserver`.</span><span class="sxs-lookup"><span data-stu-id="a8faf-299">toouse hello `ChangeFeedProcessorHost` class, you can implement `IChangeFeedObserver`.</span></span> <span data-ttu-id="a8faf-300">Этот интерфейс содержит три метода:</span><span class="sxs-lookup"><span data-stu-id="a8faf-300">This interface contains three methods:</span></span>

* <span data-ttu-id="a8faf-301">`OpenAsync` — эта функция вызывается при открытии наблюдателя веб-канала изменений.</span><span class="sxs-lookup"><span data-stu-id="a8faf-301">`OpenAsync`: This function is called when change feed observer is opened.</span></span> <span data-ttu-id="a8faf-302">При открытии потребителя и наблюдателя может быть измененный tooperform определенное действие.</span><span class="sxs-lookup"><span data-stu-id="a8faf-302">It can be modified tooperform a specific action when consumer/observer is opened.</span></span>  
* <span data-ttu-id="a8faf-303">`CloseAsync` — эта функция вызывается при закрытии наблюдателя веб-канала изменений.</span><span class="sxs-lookup"><span data-stu-id="a8faf-303">`CloseAsync`: This function is called when change feed observer is terminated.</span></span> <span data-ttu-id="a8faf-304">Измененный tooperform определенного действия может быть при закрытии потребителя и наблюдателя.</span><span class="sxs-lookup"><span data-stu-id="a8faf-304">It can be modified tooperform a specific action when consumer/observer is closed.</span></span>  
* <span data-ttu-id="a8faf-305">`ProcessChangesAsync` — эта функция вызывается, когда новые изменения документа доступны в веб-канале изменений.</span><span class="sxs-lookup"><span data-stu-id="a8faf-305">`ProcessChangesAsync`: This function is called when document new changes are available on change feed.</span></span> <span data-ttu-id="a8faf-306">Это может быть измененный tooperform определенных действий после каждого обновления изменения веб-канала.</span><span class="sxs-lookup"><span data-stu-id="a8faf-306">It can be modified tooperform a specific action upon every change feed update.</span></span>  

<span data-ttu-id="a8faf-307">В нашем примере мы реализовали hello интерфейс `IChangeFeedObserver` через hello `DocumentFeedObserver` класса.</span><span class="sxs-lookup"><span data-stu-id="a8faf-307">In our example, we implement hello interface `IChangeFeedObserver` through hello `DocumentFeedObserver` class.</span></span> <span data-ttu-id="a8faf-308">Здравствуйте, `ProcessChangesAsync` функции веб-канала документа от изменений в коллекции назначения начали hello upserts (обновления).</span><span class="sxs-lookup"><span data-stu-id="a8faf-308">Here, hello `ProcessChangesAsync` function upserts (updates) a document from change feed into hello destination collection.</span></span> <span data-ttu-id="a8faf-309">В этом примере полезен для переноса данных из одной коллекции tooanother в порядке ключ раздела hello toochange набора данных.</span><span class="sxs-lookup"><span data-stu-id="a8faf-309">This example is useful for moving data from one collection tooanother in order toochange hello partition key of a data set.</span></span> 

<span data-ttu-id="a8faf-310">*Под управлением hello процессора узла*</span><span class="sxs-lookup"><span data-stu-id="a8faf-310">*Running hello Processor Host*</span></span>

<span data-ttu-id="a8faf-311">Перед началом обработки событий можно настроить параметры веб-канала и узла веб-канала.</span><span class="sxs-lookup"><span data-stu-id="a8faf-311">Before beginning event processing, both change feed options and change feed host options can be customized.</span></span> 
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
<span data-ttu-id="a8faf-312">Hello конкретных полей, которые могут быть настроены представлены в следующей таблице hello.</span><span class="sxs-lookup"><span data-stu-id="a8faf-312">hello specific fields that can be customized are summarized in hello following tables.</span></span> 

<span data-ttu-id="a8faf-313">**Параметры веб-канала изменений**:</span><span class="sxs-lookup"><span data-stu-id="a8faf-313">**Change Feed Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="a8faf-314">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="a8faf-314">Property Name</span></span></th>
        <th><span data-ttu-id="a8faf-315">Описание</span><span class="sxs-lookup"><span data-stu-id="a8faf-315">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="a8faf-316">MaxItemCount</span><span class="sxs-lookup"><span data-stu-id="a8faf-316">MaxItemCount</span></span></td>
        <td><span data-ttu-id="a8faf-317">Возвращает или задает максимальное количество hello toobe элементов, возвращаемых при операции перечисления hello в hello Azure Cosmos DB базы данных службы.</span><span class="sxs-lookup"><span data-stu-id="a8faf-317">Gets or sets hello maximum number of items toobe returned in hello enumeration operation in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="a8faf-318">PartitionKeyRangeId</span><span class="sxs-lookup"><span data-stu-id="a8faf-318">PartitionKeyRangeId</span></span></td>
        <td><span data-ttu-id="a8faf-319">Возвращает или задает идентификатор hello секции диапазона ключей, для текущего запроса hello службы базы данных Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="a8faf-319">Gets or sets hello partition key range id for hello current request in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="a8faf-320">RequestContinuation</span><span class="sxs-lookup"><span data-stu-id="a8faf-320">RequestContinuation</span></span></td>
        <td><span data-ttu-id="a8faf-321">Возвращает или задает маркер продолжения запроса hello службы базы данных Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="a8faf-321">Gets or sets hello request continuation token in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="a8faf-322">SessionToken</span><span class="sxs-lookup"><span data-stu-id="a8faf-322">SessionToken</span></span></td>
        <td><span data-ttu-id="a8faf-323">Возвращает или задает hello токена сеанса для использования с согласованность сеансов в hello Azure Cosmos DB базы данных службы.</span><span class="sxs-lookup"><span data-stu-id="a8faf-323">Gets or sets hello session token for use with session consistency in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="a8faf-324">StartFromBeginning</span><span class="sxs-lookup"><span data-stu-id="a8faf-324">StartFromBeginning</span></span></td>
        <td><span data-ttu-id="a8faf-325">Возвращает или задает изменение веб-канал службы базы данных Azure Cosmos DB hello запустить из hello начиная (true) или из текущих (false).</span><span class="sxs-lookup"><span data-stu-id="a8faf-325">Gets or sets whether change feed in hello Azure Cosmos DB database service should start from hello beginning (true) or from current (false).</span></span> <span data-ttu-id="a8faf-326">По умолчанию он начинается с текущего положения (false).</span><span class="sxs-lookup"><span data-stu-id="a8faf-326">By default, it starts from current (false).</span></span></td>
    </tr>
</table>

<span data-ttu-id="a8faf-327">**Параметры узла веб-канала изменений**:</span><span class="sxs-lookup"><span data-stu-id="a8faf-327">**Change Feed Host Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="a8faf-328">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="a8faf-328">Property Name</span></span></th>
        <th><span data-ttu-id="a8faf-329">Тип</span><span class="sxs-lookup"><span data-stu-id="a8faf-329">Type</span></span></th>
        <th><span data-ttu-id="a8faf-330">Описание</span><span class="sxs-lookup"><span data-stu-id="a8faf-330">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="a8faf-331">LeaseRenewInterval</span><span class="sxs-lookup"><span data-stu-id="a8faf-331">LeaseRenewInterval</span></span></td>
        <td><span data-ttu-id="a8faf-332">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a8faf-332">TimeSpan</span></span></td>
        <td><span data-ttu-id="a8faf-333">Hello интервал для все аренды адресов для секций, удерживаемые в настоящее время экземпляр ChangeFeedEventHost hello.</span><span class="sxs-lookup"><span data-stu-id="a8faf-333">hello interval for all leases for partitions currently held by hello ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="a8faf-334">LeaseAcquireInterval</span><span class="sxs-lookup"><span data-stu-id="a8faf-334">LeaseAcquireInterval</span></span></td>
        <td><span data-ttu-id="a8faf-335">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a8faf-335">TimeSpan</span></span></td>
        <td><span data-ttu-id="a8faf-336">Здравствуйте tookick интервал off toocompute задач ли секций распределяются равномерно между известных экземплярах.</span><span class="sxs-lookup"><span data-stu-id="a8faf-336">hello interval tookick off a task toocompute whether partitions are distributed evenly among known host instances.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="a8faf-337">LeaseExpirationInterval</span><span class="sxs-lookup"><span data-stu-id="a8faf-337">LeaseExpirationInterval</span></span></td>
        <td><span data-ttu-id="a8faf-338">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a8faf-338">TimeSpan</span></span></td>
        <td><span data-ttu-id="a8faf-339">Интервал приветствия, для которых hello аренды извлекаются аренды, представляющая раздел.</span><span class="sxs-lookup"><span data-stu-id="a8faf-339">hello interval for which hello lease is taken on a lease representing a partition.</span></span> <span data-ttu-id="a8faf-340">Если Аренда hello не была обновлена в течение этого интервала, он будет просрочен и владения секции hello перемещает tooanother ChangeFeedEventHost экземпляра.</span><span class="sxs-lookup"><span data-stu-id="a8faf-340">If hello lease is not renewed within this interval, it is expired and ownership of hello partition moves tooanother ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="a8faf-341">FeedPollDelay</span><span class="sxs-lookup"><span data-stu-id="a8faf-341">FeedPollDelay</span></span></td>
        <td><span data-ttu-id="a8faf-342">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a8faf-342">TimeSpan</span></span></td>
        <td><span data-ttu-id="a8faf-343">Hello задержках между опросами секции для новых изменений на hello веб-канала, после все текущие изменения будут утеряны.</span><span class="sxs-lookup"><span data-stu-id="a8faf-343">hello delay between polling a partition for new changes on hello feed, after all current changes are drained.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="a8faf-344">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="a8faf-344">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="a8faf-345">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="a8faf-345">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="a8faf-346">Здравствуйте, частота toocheckpoint аренды.</span><span class="sxs-lookup"><span data-stu-id="a8faf-346">hello frequency toocheckpoint leases.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="a8faf-347">MinPartitionCount</span><span class="sxs-lookup"><span data-stu-id="a8faf-347">MinPartitionCount</span></span></td>
        <td><span data-ttu-id="a8faf-348">int</span><span class="sxs-lookup"><span data-stu-id="a8faf-348">Int</span></span></td>
        <td><span data-ttu-id="a8faf-349">Hello минимальное количество разделов для узла hello.</span><span class="sxs-lookup"><span data-stu-id="a8faf-349">hello minimum partition count for hello host.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="a8faf-350">MaxPartitionCount</span><span class="sxs-lookup"><span data-stu-id="a8faf-350">MaxPartitionCount</span></span></td>
        <td><span data-ttu-id="a8faf-351">int</span><span class="sxs-lookup"><span data-stu-id="a8faf-351">Int</span></span></td>
        <td><span data-ttu-id="a8faf-352">может служить Hello максимальное количество секций hello узла.</span><span class="sxs-lookup"><span data-stu-id="a8faf-352">hello maximum number of partitions hello host can serve.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="a8faf-353">DiscardExistingLeases</span><span class="sxs-lookup"><span data-stu-id="a8faf-353">DiscardExistingLeases</span></span></td>
        <td><span data-ttu-id="a8faf-354">Bool</span><span class="sxs-lookup"><span data-stu-id="a8faf-354">Bool</span></span></td>
        <td><span data-ttu-id="a8faf-355">Ли на hello запуска узла hello все существующие аренды должен быть удален и hello узла должно начинаться с нуля.</span><span class="sxs-lookup"><span data-stu-id="a8faf-355">Whether on hello start of hello host all existing leases should be deleted and hello host should start from scratch.</span></span></td>
    </tr>
</table>


<span data-ttu-id="a8faf-356">создать экземпляр toostart обработка событий, `ChangeFeedProcessorHost`, предоставляя hello соответствующие параметры для вашей коллекции Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="a8faf-356">toostart event processing, instantiate `ChangeFeedProcessorHost`, providing hello appropriate parameters for your Azure Cosmos DB collection.</span></span> <span data-ttu-id="a8faf-357">Затем вызовите метод `RegisterObserverAsync` tooregister вашей `IChangeFeedObserver` реализацию hello среды выполнения (DocumentFeedObserver в этом примере).</span><span class="sxs-lookup"><span data-stu-id="a8faf-357">Then, call `RegisterObserverAsync` tooregister your `IChangeFeedObserver` (DocumentFeedObserver in this example) implementation with hello runtime.</span></span> <span data-ttu-id="a8faf-358">На этом этапе узел hello предпринимает tooacquire аренду для каждого диапазона ключей секций в коллекции Azure Cosmos DB hello, с помощью алгоритма «жадного».</span><span class="sxs-lookup"><span data-stu-id="a8faf-358">At this point, hello host attempts tooacquire a lease on every partition key range in hello Azure Cosmos DB collection using a "greedy" algorithm.</span></span> <span data-ttu-id="a8faf-359">Эти аренды будут продолжаться в течение заданного промежутка времени, после чего их необходимо продлить.</span><span class="sxs-lookup"><span data-stu-id="a8faf-359">These leases last for a given timeframe and must then be renewed.</span></span> <span data-ttu-id="a8faf-360">Когда новые узлы рабочих экземпляров, в этом случае переходит в оперативный режим, они резервируют аренды и со временем загрузки hello переходит между узлами, как каждый узел пытается tooacquire дополнительные аренды.</span><span class="sxs-lookup"><span data-stu-id="a8faf-360">As new nodes, worker instances, in this case, come online, they place lease reservations and over time hello load shifts between nodes as each host attempts tooacquire more leases.</span></span> 

<span data-ttu-id="a8faf-361">В примере кода hello, мы используем фабрики класса (DocumentFeedObserverFactory.cs) toocreate наблюдателя и hello `RegistObserverFactoryAsync` tooregister hello наблюдателя.</span><span class="sxs-lookup"><span data-stu-id="a8faf-361">In hello sample code, we use a factory class (DocumentFeedObserverFactory.cs) toocreate an observer and hello `RegistObserverFactoryAsync` tooregister hello observer.</span></span> 

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
<span data-ttu-id="a8faf-362">Со временем устанавливается равновесие.</span><span class="sxs-lookup"><span data-stu-id="a8faf-362">Over time, an equilibrium is established.</span></span> <span data-ttu-id="a8faf-363">Эта динамическая возможность позволяет на основе ЦП автоматическое масштабирование применяется toobe tooconsumers для масштабирования вверх и вниз.</span><span class="sxs-lookup"><span data-stu-id="a8faf-363">This dynamic capability enables CPU-based auto-scaling toobe applied tooconsumers for both scale-up and scale-down.</span></span> <span data-ttu-id="a8faf-364">Если изменения будут доступны в базе данных Azure Cosmos быстрее, чем могут обработать потребители, hello увеличить ресурсы ЦП для потребителей можно использовать toocause автоматически регулировать число экземпляров рабочих процессов.</span><span class="sxs-lookup"><span data-stu-id="a8faf-364">If changes are available in Azure Cosmos DB at a faster rate than consumers can process, hello CPU increase on consumers can be used toocause an auto-scale on worker instance count.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8faf-365">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a8faf-365">Next steps</span></span>
* <span data-ttu-id="a8faf-366">Повторите hello [изменение в базе данных Azure Cosmos канал примеры кода на GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span><span class="sxs-lookup"><span data-stu-id="a8faf-366">Try hello [Azure Cosmos DB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span></span>
* <span data-ttu-id="a8faf-367">Приступить к созданию кода с hello [пакеты SDK Azure Cosmos DB](documentdb-sdk-dotnet.md) или hello [API-интерфейса REST](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="a8faf-367">Get started coding with hello [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/).</span></span>
