---
title: "Работа с поддержкой веб-канала изменений в Azure Cosmos DB | Документация Майкрософт"
description: "Используйте поддержку веб-канала изменений Azure Cosmos DB, чтобы отслеживать изменения в документах и выполнять обработку на основе событий, например триггеров, и поддерживать кэши и аналитические системы в обновленном состоянии."
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
ms.openlocfilehash: 160fbc98e0f3dcc7d17cbe0c7f7425811596a896
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="working-with-the-change-feed-support-in-azure-cosmos-db"></a><span data-ttu-id="2f019-104">Работа с поддержкой веб-канала изменений в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2f019-104">Working with the change feed support in Azure Cosmos DB</span></span>
<span data-ttu-id="2f019-105">[Azure Cosmos DB](../cosmos-db/introduction.md) — это быстрая и гибкая служба глобально реплицируемой базы данных, используемая для хранения большого объема данных транзакций и операционных данных с прогнозируемой задержкой операций чтения и записи менее 10 секунд.</span><span class="sxs-lookup"><span data-stu-id="2f019-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is a fast and flexible globally replicated database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes.</span></span> <span data-ttu-id="2f019-106">Благодаря этому она хорошо подходит для приложений Интернета вещей, розничной торговли, игр и приложений для ведения журнала операций.</span><span class="sxs-lookup"><span data-stu-id="2f019-106">This makes it well-suited for IoT, gaming, retail, and operational logging applications.</span></span> <span data-ttu-id="2f019-107">Распространенный конструктивный шаблон в этих приложениях заключается в отслеживании изменений в данных Azure Cosmos DB и обновлении материализованных представлений, выполнении аналитики в реальном времени, архивировании данных в автономном неструктурированном защищенном хранилище и активировании уведомлений для определенных событий на основе этих изменений.</span><span class="sxs-lookup"><span data-stu-id="2f019-107">A common design pattern in these applications is to track changes made to Azure Cosmos DB data, and update materialized views, perform real-time analytics, archive data to cold storage, and trigger notifications on certain events based on these changes.</span></span> <span data-ttu-id="2f019-108">**Поддержка веб-канала изменений** в Azure Cosmos DB дает возможность создавать эффективные и масштабируемые решения для каждого из этих шаблонов.</span><span class="sxs-lookup"><span data-stu-id="2f019-108">The **change feed support** in Azure Cosmos DB enables you to build efficient and scalable solutions for each of these patterns.</span></span>

<span data-ttu-id="2f019-109">Благодаря поддержке веб-канала изменений Azure Cosmos DB предоставляет отсортированный список документов в коллекции Azure Cosmos DB в том порядке, в котором они были изменены.</span><span class="sxs-lookup"><span data-stu-id="2f019-109">With change feed support, Azure Cosmos DB provides a sorted list of documents within an Azure Cosmos DB collection in the order in which they were modified.</span></span> <span data-ttu-id="2f019-110">Этот канал можно использовать для прослушивания изменений данных в коллекции и выполнения следующих операций:</span><span class="sxs-lookup"><span data-stu-id="2f019-110">This feed can be used to listen for modifications to data within the collection and perform actions such as:</span></span>

* <span data-ttu-id="2f019-111">активирование вызова API при вставке или изменении документа;</span><span class="sxs-lookup"><span data-stu-id="2f019-111">Trigger a call to an API when a document is inserted or modified</span></span>
* <span data-ttu-id="2f019-112">выполнение обработки или обновлений в режиме реального времени (поток);</span><span class="sxs-lookup"><span data-stu-id="2f019-112">Perform real-time (stream) processing on updates</span></span>
* <span data-ttu-id="2f019-113">синхронизация данных с кэшем, поисковой системой или хранилищем данных.</span><span class="sxs-lookup"><span data-stu-id="2f019-113">Synchronize data with a cache, search engine, or data warehouse</span></span>

<span data-ttu-id="2f019-114">Изменения в Azure Cosmos DB сохраняются и обрабатываются асинхронно, а также распределяются в один или несколько потребителей для параллельной обработки.</span><span class="sxs-lookup"><span data-stu-id="2f019-114">Changes in Azure Cosmos DB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing.</span></span> <span data-ttu-id="2f019-115">Рассмотрим интерфейсы API для веб-канала изменений и их использование для создания масштабируемых приложений, выполняющихся в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="2f019-115">Let's look at the APIs for change feed and how you can use them to build scalable real-time applications.</span></span> <span data-ttu-id="2f019-116">В этой статье показано, как работать с веб-каналом изменений с помощью API DocumentDB в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2f019-116">This article shows how to work with Azure Cosmos DB change feed and the DocumentDB API.</span></span> 

![Использование веб-канала изменений Azure Cosmos DB для аналитики в реальном времени и вычислений на основе событий](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> <span data-ttu-id="2f019-118">В данный момент веб-канал изменений поддерживается только в API DocumentDB. API Graph и API таблиц в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="2f019-118">Change feed support is only provided for the DocumentDB API at this time; the Graph API and Table API are not currently supported.</span></span>

## <a name="use-cases-and-scenarios"></a><span data-ttu-id="2f019-119">Варианты использования и сценарии</span><span class="sxs-lookup"><span data-stu-id="2f019-119">Use cases and scenarios</span></span>
<span data-ttu-id="2f019-120">Веб-канал изменений обеспечивает эффективную обработку больших наборов данных с большим объемом операций записи и представляет собой альтернативу отправке запросов на все наборы данных, чтобы определить, какие изменения были внесены.</span><span class="sxs-lookup"><span data-stu-id="2f019-120">Change feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative to querying entire datasets to identify what has changed.</span></span> <span data-ttu-id="2f019-121">Например, можно эффективно выполнить следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="2f019-121">For example, you can perform the following tasks efficiently:</span></span>

* <span data-ttu-id="2f019-122">Обновление кэша, индекса поиска или хранилища данными, хранящимися в Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2f019-122">Update a cache, search index, or a data warehouse with data stored in Azure Cosmos DB.</span></span>
* <span data-ttu-id="2f019-123">Реализация распределения данных по уровням и их архивирование на уровне приложений, то есть хранение "горячих данных" в Azure Cosmos DB и удаление "холодных данных" в [хранилище BLOB-объектов Azure](../storage/common/storage-introduction.md) или [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2f019-123">Implement application-level data tiering and archival, that is, store "hot data" in Azure Cosmos DB, and age out "cold data" to [Azure Blob Storage](../storage/common/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>
* <span data-ttu-id="2f019-124">Реализация пакетной аналитики для данных с помощью [Apache Hadoop](run-hadoop-with-hdinsight.md).</span><span class="sxs-lookup"><span data-stu-id="2f019-124">Implement batch analytics on data using [Apache Hadoop](run-hadoop-with-hdinsight.md).</span></span>
* <span data-ttu-id="2f019-125">Реализация [лямбда-конвейеров в Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) с помощью Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2f019-125">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with Azure Cosmos DB.</span></span> <span data-ttu-id="2f019-126">Azure Cosmos DB предоставляет масштабируемое решение базы данных, которое может обрабатывать операции приема и запроса, а также реализовывать лямбда-архитектуры с низкой совокупной стоимостью владения.</span><span class="sxs-lookup"><span data-stu-id="2f019-126">Azure Cosmos DB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span></span> 
* <span data-ttu-id="2f019-127">Выполнение переносов в другую учетную запись Azure Cosmos DB с использованием другой схемы секционирования без простоев.</span><span class="sxs-lookup"><span data-stu-id="2f019-127">Perform zero down-time migrations to another Azure Cosmos DB account with a different partitioning scheme.</span></span>

<span data-ttu-id="2f019-128">**Лямбда-конвейеры при использовании Azure Cosmos DB для приема и запроса:**</span><span class="sxs-lookup"><span data-stu-id="2f019-128">**Lambda Pipelines with Azure Cosmos DB for ingestion and query:**</span></span>

![Лямбда-конвейер для приема и запроса на основе Azure Cosmos DB](./media/change-feed/lambda.png)

<span data-ttu-id="2f019-130">Azure Cosmos DB можно использовать для получения и хранения данных о событиях с устройств, датчиков, инфраструктуры и приложений и обрабатывать эти события в реальном времени с помощью [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md) или [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2f019-130">You can use Azure Cosmos DB to receive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span></span> 

<span data-ttu-id="2f019-131">В [бессерверных](http://azure.com/serverless) веб-приложениях и мобильных приложениях вы можете отслеживать события, такие как изменения в профиле, настройке или местоположении для активирования определенных действий ,например, отправка push-уведомлений на свои устройства, с помощью [Функции Azure](../azure-functions/functions-bindings-documentdb.md) или [Службы приложений](https://azure.microsoft.com/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="2f019-131">Within your [serverless](http://azure.com/serverless) web and mobile apps, you can track events such as changes to your customer's profile, preferences, or location to trigger certain actions like sending push notifications to their devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="2f019-132">При использовании Azure Cosmos DB для создания игр веб-канал изменений можно использовать, например, для создания списков лидеров в режиме реального времени на основе очков в завершенных играх.</span><span class="sxs-lookup"><span data-stu-id="2f019-132">If you're using Azure Cosmos DB to build a game, you can, for example, use change feed to implement real-time leaderboards based on scores from completed games.</span></span>

## <a name="how-change-feed-works-in-azure-cosmos-db"></a><span data-ttu-id="2f019-133">Как работает веб-канал изменений в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="2f019-133">How change feed works in Azure Cosmos DB</span></span>
<span data-ttu-id="2f019-134">Azure Cosmos DB предоставляет возможность постепенно считывать обновления, внесенные в коллекцию Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2f019-134">Azure Cosmos DB provides the ability to incrementally read updates made to an Azure Cosmos DB collection.</span></span> <span data-ttu-id="2f019-135">Этот веб-канал изменений обладает следующими свойствами:</span><span class="sxs-lookup"><span data-stu-id="2f019-135">This change feed has the following properties:</span></span>

* <span data-ttu-id="2f019-136">Изменения сохраняются в Azure Cosmos DB и могут обрабатываться асинхронно.</span><span class="sxs-lookup"><span data-stu-id="2f019-136">Changes are persistent in Azure Cosmos DB and can be processed asynchronously.</span></span>
* <span data-ttu-id="2f019-137">Изменения в документах в коллекции сразу же становятся доступными в веб-канале изменений.</span><span class="sxs-lookup"><span data-stu-id="2f019-137">Changes to documents within a collection are available immediately in the change feed.</span></span>
* <span data-ttu-id="2f019-138">Каждое изменение в документе отображается только один раз в веб-канале изменений, а клиенты управляют логикой контрольных точек.</span><span class="sxs-lookup"><span data-stu-id="2f019-138">Each change to a document appears exactly once in the change feed, and clients manage their checkpointing logic.</span></span> <span data-ttu-id="2f019-139">Библиотека обработчика веб-канала изменений предоставляет возможность автоматического создания контрольных точек и семантику типа "не менее одного раза".</span><span class="sxs-lookup"><span data-stu-id="2f019-139">The change feed processor library provides automatic checkpointing and "at least once" semantics.</span></span>
* <span data-ttu-id="2f019-140">В журнал изменений вносится только самое последнее изменение в конкретном документе.</span><span class="sxs-lookup"><span data-stu-id="2f019-140">Only the most recent change for a given document is included in the change log.</span></span> <span data-ttu-id="2f019-141">Промежуточные изменения могут быть недоступны.</span><span class="sxs-lookup"><span data-stu-id="2f019-141">Intermediate changes may not be available.</span></span>
* <span data-ttu-id="2f019-142">Веб-канал изменений сортируется в порядке изменения в каждом значении ключа раздела.</span><span class="sxs-lookup"><span data-stu-id="2f019-142">The change feed is sorted by order of modification within each partition key value.</span></span> <span data-ttu-id="2f019-143">В значениях ключа раздела нет установленного порядка.</span><span class="sxs-lookup"><span data-stu-id="2f019-143">There is no guaranteed order across partition-key values.</span></span>
* <span data-ttu-id="2f019-144">Изменения можно синхронизировать в любой момент времени. Это означает, что фиксированный период хранения данных, для которого доступны изменения, отсутствует.</span><span class="sxs-lookup"><span data-stu-id="2f019-144">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span></span>
* <span data-ttu-id="2f019-145">Изменения доступны в виде фрагментов диапазонов ключей разделов.</span><span class="sxs-lookup"><span data-stu-id="2f019-145">Changes are available in chunks of partition key ranges.</span></span> <span data-ttu-id="2f019-146">Эта возможность позволяет нескольким потребителям и серверам параллельно обрабатывать изменения из больших коллекций.</span><span class="sxs-lookup"><span data-stu-id="2f019-146">This capability allows changes from large collections to be processed in parallel by multiple consumers/servers.</span></span>
* <span data-ttu-id="2f019-147">Приложения могут запросить несколько веб-каналов изменений в одной коллекции одновременно.</span><span class="sxs-lookup"><span data-stu-id="2f019-147">Applications can request for multiple change feeds simultaneously on the same collection.</span></span>

<span data-ttu-id="2f019-148">Веб-канал изменений Azure Cosmos DB включен по умолчанию для всех учетных записей.</span><span class="sxs-lookup"><span data-stu-id="2f019-148">Azure Cosmos DB's change feed is enabled by default for all accounts.</span></span> <span data-ttu-id="2f019-149">Вы можете использовать свою [подготовленную пропускную способность](request-units.md) в своем регионе записи или любом [регионе чтения](distribute-data-globally.md) для чтения с веб-канала изменений так же, как и любую другую операцию из Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2f019-149">You can use your [provisioned throughput](request-units.md) in your write region or any [read region](distribute-data-globally.md) to read from the change feed, just like any other operation from Azure Cosmos DB.</span></span> <span data-ttu-id="2f019-150">Веб-канал изменений также отслеживает операции вставки и обновления, внесенные в документы в коллекции.</span><span class="sxs-lookup"><span data-stu-id="2f019-150">The change feed includes inserts and update operations made to documents within the collection.</span></span> <span data-ttu-id="2f019-151">Вы можете отслеживать операции удаления, установив флажок soft-delete в документах вместо удаления.</span><span class="sxs-lookup"><span data-stu-id="2f019-151">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span></span> <span data-ttu-id="2f019-152">Кроме того, с помощью [функции срока жизни](time-to-live.md) для документов можно задать ограниченный срок действия, например 24 часа, и использовать значение этого свойства для отслеживания операций удаления.</span><span class="sxs-lookup"><span data-stu-id="2f019-152">Alternatively, you can set a finite expiration period for your documents via the [TTL capability](time-to-live.md), for example, 24 hours and use the value of that property to capture deletes.</span></span> <span data-ttu-id="2f019-153">При использовании этого решения необходимо обрабатывать изменения в течение более короткого промежутка времени, чем срок жизни.</span><span class="sxs-lookup"><span data-stu-id="2f019-153">With this solution, you have to process changes within a shorter time interval than the TTL expiration period.</span></span> <span data-ttu-id="2f019-154">Веб-канал изменений доступен для каждого диапазона ключей разделов в коллекции документов, и поэтому его можно распределить в один или несколько потребителей для параллельной обработки.</span><span class="sxs-lookup"><span data-stu-id="2f019-154">The change feed is available for each partition key range within the document collection, and thus can be distributed across one or more consumers for parallel processing.</span></span> 

![Распределенная обработка веб-канала изменений Azure Cosmos DB](./media/change-feed/changefeedvisual.png)

<span data-ttu-id="2f019-156">Есть несколько вариантов реализации веб-канала изменений в коде клиента.</span><span class="sxs-lookup"><span data-stu-id="2f019-156">You have a few options in how you implement a change feed in your client code.</span></span> <span data-ttu-id="2f019-157">В следующих разделах описывается реализация веб-канала изменений с помощью REST API для базы данных Azure Cosmos DB и пакетов SDK для DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="2f019-157">The sections that immediately follow describe how to implement the change feed using the Azure Cosmos DB REST API and the DocumentDB SDKs.</span></span> <span data-ttu-id="2f019-158">Для приложений .NET рекомендуется использовать новую [библиотеку обработчика веб-канала изменений](#change-feed-processor) для обработки событий из веб-канала изменений, так как это упрощает чтение изменений в секциях и позволяет нескольким потокам работать параллельно.</span><span class="sxs-lookup"><span data-stu-id="2f019-158">However, for .NET applications, we recommend using the new [Change feed processor library](#change-feed-processor) for processing events from the change feed as it simplifies reading changes across partitions and enables multiple threads working in parallel.</span></span> 

## <span data-ttu-id="2f019-159"><a id="rest-apis"></a>Работа с REST API и пакетами SDK для DocumentDB</span><span class="sxs-lookup"><span data-stu-id="2f019-159"><a id="rest-apis"></a>Working with the REST API and DocumentDB SDKs</span></span>
<span data-ttu-id="2f019-160">Azure Cosmos DB предоставляет эластичные контейнеры хранилища и пропускной способности, называемые **коллекциями**.</span><span class="sxs-lookup"><span data-stu-id="2f019-160">Azure Cosmos DB provides elastic containers of storage and throughput called **collections**.</span></span> <span data-ttu-id="2f019-161">Данные в коллекциях логически сгруппированы с помощью [ключей разделов](partition-data.md) для масштабируемости и производительности.</span><span class="sxs-lookup"><span data-stu-id="2f019-161">Data within collections is logically grouped using [partition keys](partition-data.md) for scalability and performance.</span></span> <span data-ttu-id="2f019-162">Azure Cosmos DB предоставляет различные интерфейсы API для доступа к этим данным, включая поиск по идентификатору (чтение или получение), запросы и чтение каналов (сканирования).</span><span class="sxs-lookup"><span data-stu-id="2f019-162">Azure Cosmos DB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans).</span></span> <span data-ttu-id="2f019-163">Веб-канал изменений можно получить путем заполнения двух новых заголовков запроса в интерфейсе API `ReadDocumentFeed` DocumentDB, и его можно обрабатывать параллельно в диапазонах ключей разделов.</span><span class="sxs-lookup"><span data-stu-id="2f019-163">The change feed can be obtained by populating two new request headers to the DocumentDB `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.</span></span>

### <a name="readdocumentfeed-api"></a><span data-ttu-id="2f019-164">Интерфейс API ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="2f019-164">ReadDocumentFeed API</span></span>
<span data-ttu-id="2f019-165">Давайте рассмотрим, как работает ReadDocumentFeed.</span><span class="sxs-lookup"><span data-stu-id="2f019-165">Let's take a brief look at how ReadDocumentFeed works.</span></span> <span data-ttu-id="2f019-166">Azure Cosmos DB поддерживает чтение веб-канала документов в коллекции через интерфейс API `ReadDocumentFeed`.</span><span class="sxs-lookup"><span data-stu-id="2f019-166">Azure Cosmos DB supports reading a feed of documents within a collection via the `ReadDocumentFeed` API.</span></span> <span data-ttu-id="2f019-167">Например, следующий запрос возвращает страницу документов внутри коллекции `serverlogs`.</span><span class="sxs-lookup"><span data-stu-id="2f019-167">For example, the following request returns a page of documents inside the `serverlogs` collection.</span></span> 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="2f019-168">Результаты можно ограничить с помощью заголовка `x-ms-max-item-count`, а операции чтения можно возобновить, повторно подав запрос с помощью заголовка `x-ms-continuation`, возвращенного в предыдущем ответе.</span><span class="sxs-lookup"><span data-stu-id="2f019-168">Results can be limited by using the `x-ms-max-item-count` header, and reads can be resumed by resubmitting the request with a `x-ms-continuation` header returned in the previous response.</span></span> <span data-ttu-id="2f019-169">При выполнении из единого клиента `ReadDocumentFeed` выполняет итерацию результатов по разделам последовательно.</span><span class="sxs-lookup"><span data-stu-id="2f019-169">When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially.</span></span> 

<span data-ttu-id="2f019-170">**Веб-канал для последовательного чтения документов**</span><span class="sxs-lookup"><span data-stu-id="2f019-170">**Serial read document feed**</span></span>

<span data-ttu-id="2f019-171">Веб-канал документов можно также получить с помощью одного из поддерживаемых [пакетов SDK для Azure Cosmos DB](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="2f019-171">You can also retrieve the feed of documents using one of the supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="2f019-172">Например, в следующем фрагменте кода показано, как использовать метод [ReadDocumentFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) в .NET.</span><span class="sxs-lookup"><span data-stu-id="2f019-172">For example, the following snippet shows how to use the [ReadDocumentFeedAsync method](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span></span>

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a><span data-ttu-id="2f019-173">Распределенное выполнение ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="2f019-173">Distributed execution of ReadDocumentFeed</span></span>
<span data-ttu-id="2f019-174">Для коллекций, содержащих терабайты данных и более или принимающих большое количество обновлений, последовательное выполнение веб-канала чтения с компьютера с одним клиентом может оказаться нецелесообразным.</span><span class="sxs-lookup"><span data-stu-id="2f019-174">For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical.</span></span> <span data-ttu-id="2f019-175">Для поддержки этих сценариев с данными большого размера Azure Cosmos DB содержит интерфейсы API для распределения вызовов `ReadDocumentFeed` по нескольким клиентским считывателям и потребителям открытым образом.</span><span class="sxs-lookup"><span data-stu-id="2f019-175">In order to support these big data scenarios, Azure Cosmos DB provides APIs to distribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers.</span></span> 

<span data-ttu-id="2f019-176">**Веб-канал для распределенного чтения документов**</span><span class="sxs-lookup"><span data-stu-id="2f019-176">**Distributed Read Document Feed**</span></span>

<span data-ttu-id="2f019-177">Чтобы обеспечить масштабируемую обработку добавочных изменений, Azure Cosmos DB поддерживает модель масштабирования для интерфейса API веб-канала изменений на основе диапазонов ключей разделов.</span><span class="sxs-lookup"><span data-stu-id="2f019-177">To provide scalable processing of incremental changes, Azure Cosmos DB supports a scale-out model for the change feed API based on ranges of partition keys.</span></span>

* <span data-ttu-id="2f019-178">Список диапазонов ключей разделов для коллекции можно получить, выполнив вызов `ReadPartitionKeyRanges`.</span><span class="sxs-lookup"><span data-stu-id="2f019-178">You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call.</span></span> 
* <span data-ttu-id="2f019-179">Для каждого диапазона ключей разделов можно выполнить `ReadDocumentFeed`, чтобы читать документы с помощью ключей разделов в пределах диапазона.</span><span class="sxs-lookup"><span data-stu-id="2f019-179">For each partition key range, you can perform a `ReadDocumentFeed` to read documents with partition keys within that range.</span></span>

### <a name="retrieving-partition-key-ranges-for-a-collection"></a><span data-ttu-id="2f019-180">Извлечение диапазонов ключей разделов для коллекции</span><span class="sxs-lookup"><span data-stu-id="2f019-180">Retrieving partition key ranges for a collection</span></span>
<span data-ttu-id="2f019-181">Диапазоны ключей секций можно получить путем запроса ресурса `pkranges` в коллекции.</span><span class="sxs-lookup"><span data-stu-id="2f019-181">You can retrieve the partition key ranges by requesting the `pkranges` resource within a collection.</span></span> <span data-ttu-id="2f019-182">Например, следующий запрос возвращает список диапазонов ключей разделов для коллекции `serverlogs`:</span><span class="sxs-lookup"><span data-stu-id="2f019-182">For example the following request retrieves the list of partition key ranges for the `serverlogs` collection:</span></span>

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

<span data-ttu-id="2f019-183">Этот запрос возвращает следующий ответ, содержащий метаданные о диапазонах ключей разделов:</span><span class="sxs-lookup"><span data-stu-id="2f019-183">This request returns the following response containing metadata about the partition key ranges:</span></span>

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


<span data-ttu-id="2f019-184">**Свойства диапазона ключей секций.** Каждый диапазон ключей секций содержит свойства метаданных, приведенные в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="2f019-184">**Partition key range properties**: Each partition key range includes the metadata properties in the following table:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="2f019-185">Имя заголовка</span><span class="sxs-lookup"><span data-stu-id="2f019-185">Header name</span></span></th>
        <th><span data-ttu-id="2f019-186">Описание</span><span class="sxs-lookup"><span data-stu-id="2f019-186">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="2f019-187">id</span><span class="sxs-lookup"><span data-stu-id="2f019-187">id</span></span></td>
        <td>
            <p><span data-ttu-id="2f019-188">Идентификатор для диапазона ключей разделов.</span><span class="sxs-lookup"><span data-stu-id="2f019-188">The ID for the partition key range.</span></span> <span data-ttu-id="2f019-189">Это стабильный и уникальный идентификатор в каждой коллекции.</span><span class="sxs-lookup"><span data-stu-id="2f019-189">This is a stable and unique ID within each collection.</span></span></p>
            <p><span data-ttu-id="2f019-190">Должен использоваться в следующем вызове для считывания изменений с помощью диапазона ключей разделов.</span><span class="sxs-lookup"><span data-stu-id="2f019-190">Must be used in the following call to read changes by partition key range.</span></span></p>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="2f019-191">maxExclusive</span><span class="sxs-lookup"><span data-stu-id="2f019-191">maxExclusive</span></span></td>
        <td><span data-ttu-id="2f019-192">Максимальное значение хэша ключа раздела для диапазона ключей разделов.</span><span class="sxs-lookup"><span data-stu-id="2f019-192">The maximum partition key hash value for the partition key range.</span></span> <span data-ttu-id="2f019-193">Для внутреннего использования.</span><span class="sxs-lookup"><span data-stu-id="2f019-193">For internal use.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2f019-194">minInclusive</span><span class="sxs-lookup"><span data-stu-id="2f019-194">minInclusive</span></span></td>
        <td><span data-ttu-id="2f019-195">Минимальное значение хэша ключа раздела для диапазона ключей разделов.</span><span class="sxs-lookup"><span data-stu-id="2f019-195">The minimum partition key hash value for the partition key range.</span></span> <span data-ttu-id="2f019-196">Для внутреннего использования.</span><span class="sxs-lookup"><span data-stu-id="2f019-196">For internal use.</span></span></td>
    </tr>       
</table>

<span data-ttu-id="2f019-197">Это можно сделать с помощью одного из поддерживаемых [пакетов SDK для Azure Cosmos DB](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="2f019-197">You can do this using one of the supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="2f019-198">Например, в следующем фрагменте кода показано, как получить диапазон ключей секций в .NET с помощью метода [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="2f019-198">For example, the following snippet shows how to retrieve partition key ranges in .NET using the [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) method.</span></span>

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

<span data-ttu-id="2f019-199">Azure Cosmos DB поддерживает получение документов в диапазоне ключей разделов путем задания необязательного заголовка `x-ms-documentdb-partitionkeyrangeid`.</span><span class="sxs-lookup"><span data-stu-id="2f019-199">Azure Cosmos DB supports retrieval of documents per partition key range by setting the optional `x-ms-documentdb-partitionkeyrangeid` header.</span></span> 

### <a name="performing-an-incremental-readdocumentfeed"></a><span data-ttu-id="2f019-200">Выполнение добавочного ReadDocumentFeed</span><span class="sxs-lookup"><span data-stu-id="2f019-200">Performing an incremental ReadDocumentFeed</span></span>
<span data-ttu-id="2f019-201">ReadDocumentFeed поддерживает следующие сценарии и задачи для добавочной обработки изменений в коллекциях Azure Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="2f019-201">ReadDocumentFeed supports the following scenarios/tasks for incremental processing of changes in Azure Cosmos DB collections:</span></span>

* <span data-ttu-id="2f019-202">Чтение всех изменений в документах с самого начала, то есть с момента создания коллекции.</span><span class="sxs-lookup"><span data-stu-id="2f019-202">Read all changes to documents from the beginning, that is, from collection creation.</span></span>
* <span data-ttu-id="2f019-203">Чтение всех изменений в будущих обновлениях документов, начиная с текущего времени, или любых изменений с указанного пользователем времени.</span><span class="sxs-lookup"><span data-stu-id="2f019-203">Read all changes to future updates to documents from current time, or any changes since a user-specified time.</span></span>
* <span data-ttu-id="2f019-204">Чтение всех изменений в документах из логической версии коллекции (ETag).</span><span class="sxs-lookup"><span data-stu-id="2f019-204">Read all changes to documents from a logical version of the collection (ETag).</span></span> <span data-ttu-id="2f019-205">Вы можете создать контрольную точку потребителей в зависимости от возвращаемого ETag из добавочных запросов на чтение канала.</span><span class="sxs-lookup"><span data-stu-id="2f019-205">You can checkpoint your consumers based on the returned ETag from incremental read-feed requests.</span></span>

<span data-ttu-id="2f019-206">Изменения включают операции вставки и обновлений в документах.</span><span class="sxs-lookup"><span data-stu-id="2f019-206">The changes include inserts and updates to documents.</span></span> <span data-ttu-id="2f019-207">Для отслеживания операций удаления в документах необходимо использовать свойство soft delete или [встроенное свойство срока жизни](time-to-live.md), чтобы обозначить отложенное удаление в веб-канале изменений.</span><span class="sxs-lookup"><span data-stu-id="2f019-207">To capture deletes, you must use a "soft delete" property within your documents, or use the [built-in TTL property](time-to-live.md) to signal a pending deletion in the change feed.</span></span>

<span data-ttu-id="2f019-208">В следующей таблице перечислены [заголовки запроса](/rest/api/documentdb/common-documentdb-rest-request-headers.md) и [ответа](/rest/api/documentdb/common-documentdb-rest-response-headers.md) для операций ReadDocumentFeed.</span><span class="sxs-lookup"><span data-stu-id="2f019-208">The following table lists the [request](/rest/api/documentdb/common-documentdb-rest-request-headers.md) and [response headers](/rest/api/documentdb/common-documentdb-rest-response-headers.md) for ReadDocumentFeed operations.</span></span>

<span data-ttu-id="2f019-209">**Заголовки запроса для добавочного ReadDocumentFeed**</span><span class="sxs-lookup"><span data-stu-id="2f019-209">**Request headers for incremental ReadDocumentFeed**:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="2f019-210">Имя заголовка</span><span class="sxs-lookup"><span data-stu-id="2f019-210">Header name</span></span></th>
        <th><span data-ttu-id="2f019-211">Описание</span><span class="sxs-lookup"><span data-stu-id="2f019-211">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="2f019-212">A-IM</span><span class="sxs-lookup"><span data-stu-id="2f019-212">A-IM</span></span></td>
        <td><span data-ttu-id="2f019-213">Для этого параметра необходимо задать значение Incremental feed (Добавочный канал) или пропустить его</span><span class="sxs-lookup"><span data-stu-id="2f019-213">Must be set to "Incremental feed", or omitted otherwise</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2f019-214">If-None-Match</span><span class="sxs-lookup"><span data-stu-id="2f019-214">If-None-Match</span></span></td>
        <td>
            <p><span data-ttu-id="2f019-215">Без заголовка: возвращает все изменения с самого начала (создание коллекции)</span><span class="sxs-lookup"><span data-stu-id="2f019-215">No header: returns all changes from the beginning (collection creation)</span></span></p>
            <p><span data-ttu-id="2f019-216">"*": возвращает все новые изменения данных в коллекции</span><span class="sxs-lookup"><span data-stu-id="2f019-216">"*": returns all new changes to data within the collection</span></span></p>           
            <p><span data-ttu-id="2f019-217">&lt;eTag&gt;: если для коллекции задать значение ETag, возвращает все изменения, внесенные с момента этой логической отметки времени</span><span class="sxs-lookup"><span data-stu-id="2f019-217">&lt;etag&gt;: If set to a collection ETag, returns all changes made since that logical timestamp</span></span></p>
        </td>
    </tr>
    <tr>    
        <td><span data-ttu-id="2f019-218">If-Modified-Since</span><span class="sxs-lookup"><span data-stu-id="2f019-218">If-Modified-Since</span></span></td> 
        <td><span data-ttu-id="2f019-219">Формат времени RFC 1123. Не учитывается, если указан заголовок If-None-Match.</span><span class="sxs-lookup"><span data-stu-id="2f019-219">RFC 1123 time format; ignored if If-None-Match is specified</span></span></td> 
    </tr> 
    <tr>
        <td><span data-ttu-id="2f019-220">x-ms-documentdb-partitionkeyrangeid</span><span class="sxs-lookup"><span data-stu-id="2f019-220">x-ms-documentdb-partitionkeyrangeid</span></span></td>
        <td><span data-ttu-id="2f019-221">Идентификатор диапазона ключей разделов для считывания данных.</span><span class="sxs-lookup"><span data-stu-id="2f019-221">The partition key range ID for reading data.</span></span></td>
    </tr>
</table>

<span data-ttu-id="2f019-222">**Заголовки ответа для добавочного ReadDocumentFeed**</span><span class="sxs-lookup"><span data-stu-id="2f019-222">**Response headers for incremental ReadDocumentFeed**:</span></span>

<table> <tr>
        <th><span data-ttu-id="2f019-223">Имя заголовка</span><span class="sxs-lookup"><span data-stu-id="2f019-223">Header name</span></span></th>
        <th><span data-ttu-id="2f019-224">Описание</span><span class="sxs-lookup"><span data-stu-id="2f019-224">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="2f019-225">etag</span><span class="sxs-lookup"><span data-stu-id="2f019-225">etag</span></span></td>
        <td>
            <p><span data-ttu-id="2f019-226">Логический порядковый номер последнего документа, возвращенного в ответе.</span><span class="sxs-lookup"><span data-stu-id="2f019-226">The logical sequence number (LSN) of last document returned in the response.</span></span></p>
            <p><span data-ttu-id="2f019-227">Добавочный ReadDocumentFeed можно возобновить, повторно задав это значение в параметре If-None-Match.</span><span class="sxs-lookup"><span data-stu-id="2f019-227">Incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</span></span></p>
        </td>
    </tr>
</table>

<span data-ttu-id="2f019-228">Ниже приведен пример запроса для возврата всех добавочных изменений в коллекции из логической версии или ETag `28535` и диапазона ключей разделов `16`.</span><span class="sxs-lookup"><span data-stu-id="2f019-228">Here's a sample request to return all incremental changes in collection from the logical version/ETag `28535` and partition key range = `16`:</span></span>

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

<span data-ttu-id="2f019-229">Изменения упорядочиваются по времени в каждом значении ключа раздела в пределах диапазона ключа раздела.</span><span class="sxs-lookup"><span data-stu-id="2f019-229">Changes are ordered by time within each partition key value within the partition key range.</span></span> <span data-ttu-id="2f019-230">В значениях ключа раздела нет установленного порядка.</span><span class="sxs-lookup"><span data-stu-id="2f019-230">There is no guaranteed order across partition-key values.</span></span> <span data-ttu-id="2f019-231">Если результатов больше, чем может поместиться на одной странице, можно прочитать следующую страницу результатов, повторно отправив запрос с заголовком `If-None-Match` со значением, равным `etag` из предыдущего ответа.</span><span class="sxs-lookup"><span data-stu-id="2f019-231">If there are more results than can fit in a single page, you can read the next page of results by resubmitting the request with the `If-None-Match` header with value equal to the `etag` from the previous response.</span></span> <span data-ttu-id="2f019-232">Если несколько документов вставлены или обновлены транзакционно в хранимой процедуре или триггере, все они будут возвращены на одной странице ответа.</span><span class="sxs-lookup"><span data-stu-id="2f019-232">If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within the same response page.</span></span>

> [!NOTE]
> <span data-ttu-id="2f019-233">С помощью веб-канала изменений можно получать на странице результатов больше элементов, чем указано в `x-ms-max-item-count`, если несколько документов были вставлены или обновлены транзакционно в хранимых процедурах или триггерах.</span><span class="sxs-lookup"><span data-stu-id="2f019-233">With change feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in the case of multiple documents inserted or updated inside a stored procedures or triggers.</span></span> 

<span data-ttu-id="2f019-234">При использовании пакета SDK для NET (1.17.0) задайте `StartTime` поля в параметрах `ChangeFeedOptions` для возвращения измененных документов с момента `StartTime` при вызове `CreateDocumentChangeFeedQuery` напрямую.</span><span class="sxs-lookup"><span data-stu-id="2f019-234">When using the .NET SDK (1.17.0), set the field `StartTime` in `ChangeFeedOptions` to directly return changed documents since `StartTime` when calling  `CreateDocumentChangeFeedQuery`.</span></span> <span data-ttu-id="2f019-235">Если указать `If-Modified-Since` с помощью API REST, запрос вернет не сами документы, а скорее маркер продолжения или `etag` в заголовке ответа.</span><span class="sxs-lookup"><span data-stu-id="2f019-235">By specifying `If-Modified-Since` using the REST API, your request will return not the documents themselves, but rather the continuation token or `etag` in the response header.</span></span> <span data-ttu-id="2f019-236">Для возврата документов, измененных в указанное время, в следующем запросе нужно использовать маркер продолжения `etag` с `If-None-Match`, чтобы вернуть фактические документы.</span><span class="sxs-lookup"><span data-stu-id="2f019-236">To return the documents modified the specified time, the continuation token `etag` must then be used in the next request with `If-None-Match` to return the actual documents.</span></span> 

<span data-ttu-id="2f019-237">Пакет SDK для .NET предоставляет вспомогательные классы [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) и [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) для доступа к изменениям, внесенным в коллекцию.</span><span class="sxs-lookup"><span data-stu-id="2f019-237">The .NET SDK provides the [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) and [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper classes to access changes made to a collection.</span></span> <span data-ttu-id="2f019-238">В следующем фрагменте кода показано, как получить все изменения с самого начала с использованием пакета SDK для .NET из одного клиента.</span><span class="sxs-lookup"><span data-stu-id="2f019-238">The following snippet shows how to retrieve all changes from the beginning using the .NET SDK from a single client.</span></span>

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
<span data-ttu-id="2f019-239">А в следующем фрагменте показано, как обрабатывать изменения в реальном времени с помощью Azure Cosmos DB, используя поддержку веб-канала изменений и предыдущую функцию.</span><span class="sxs-lookup"><span data-stu-id="2f019-239">And the following snippet shows how to process changes in real-time with Azure Cosmos DB by using the change feed support and the preceding function.</span></span> <span data-ttu-id="2f019-240">Первый вызов возвращает все документы в коллекции, а второй — только два документа, созданные с момента создания последней контрольной точки.</span><span class="sxs-lookup"><span data-stu-id="2f019-240">The first call returns all the documents in the collection, and the second only returns the two documents created that were created since the last checkpoint.</span></span>

```csharp
// Returns all documents in the collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only the two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

<span data-ttu-id="2f019-241">Вы также можете фильтровать веб-канал изменений с помощью логики на стороне клиента, чтобы обрабатывать события выборочно.</span><span class="sxs-lookup"><span data-stu-id="2f019-241">You can also filter the change feed using client side logic to selectively process events.</span></span> <span data-ttu-id="2f019-242">Например, ниже приведен фрагмент кода, в котором используется LINQ на стороне клиента для обработки только событий изменения температуры с датчиков устройств.</span><span class="sxs-lookup"><span data-stu-id="2f019-242">For example, here's a snippet that uses client side LINQ to process only temperature change events from device sensors.</span></span>

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <span data-ttu-id="2f019-243"><a id="change-feed-processor"></a>Библиотека обработчика веб-канала изменений</span><span class="sxs-lookup"><span data-stu-id="2f019-243"><a id="change-feed-processor"></a>Change Feed Processor library</span></span>
<span data-ttu-id="2f019-244">Вторым вариантом является использование [библиотеки обработчика веб-канала изменений Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), который поможет распределить обработку событий из веб-канала изменений между несколькими потребителями.</span><span class="sxs-lookup"><span data-stu-id="2f019-244">Another option is to use the [Azure Cosmos DB Change Feed Processor library](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), which can help you easily distribute event processing from a change feed across multiple consumers.</span></span> <span data-ttu-id="2f019-245">Эту библиотеку следует использовать при создании модулей чтения веб-канала изменений на платформе .NET.</span><span class="sxs-lookup"><span data-stu-id="2f019-245">The library is great for building change feed readers on the .NET platform.</span></span> <span data-ttu-id="2f019-246">Некоторые рабочие процессы, которые можно упростить с помощью библиотеки обработчика веб-канала изменений, по сравнению с методами, включенными в другие пакетах SDK для Cosmos DB:</span><span class="sxs-lookup"><span data-stu-id="2f019-246">Some workflows that would be simplified by using the Change Feed Processor library over the methods included in the other Cosmos DB SDKs include:</span></span> 

* <span data-ttu-id="2f019-247">Извлечение обновлений из веб-канала изменений, когда данные хранятся в нескольких секциях.</span><span class="sxs-lookup"><span data-stu-id="2f019-247">Pulling updates from change feed when data is stored across multiple partitions</span></span>
* <span data-ttu-id="2f019-248">Перемещение или репликация данных из одной коллекции в другую.</span><span class="sxs-lookup"><span data-stu-id="2f019-248">Moving or replicating data from one collection to another</span></span>
* <span data-ttu-id="2f019-249">Параллельное выполнение действий, запускаемых обновлениями данных и веб-каналом изменений.</span><span class="sxs-lookup"><span data-stu-id="2f019-249">Parallel execution of actions triggered by updates to data and change feed</span></span> 

<span data-ttu-id="2f019-250">Использование интерфейсов API в пакетах SDK для Cosmos обеспечивает точный доступ к обновлениям веб-канала изменений в каждой секции, а использование библиотеки обработчика веб-канала изменений упрощает считывание изменений в секциях и параллельную работу нескольких потоков.</span><span class="sxs-lookup"><span data-stu-id="2f019-250">While using the APIs in the Cosmos SDKs provides precise access to change feed updates in each partition, using the Change Feed Processor library simplifies reading changes across partitions and multiple threads working in parallel.</span></span> <span data-ttu-id="2f019-251">Вместо того чтобы считывать изменения из каждого контейнера и сохранять маркер продолжения для каждой секции вручную, обработчик веб-канала изменений автоматически управляет считыванием изменений в секциях с помощью механизма аренды.</span><span class="sxs-lookup"><span data-stu-id="2f019-251">Instead of manually reading changes from each container and saving a continuation token for each partition, the Change Feed Processor automatically manages reading changes across partitions using a lease mechanism.</span></span>

<span data-ttu-id="2f019-252">Библиотека доступна как пакет NuGet: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) и из исходного кода в виде [примера](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor) GitHub.</span><span class="sxs-lookup"><span data-stu-id="2f019-252">The library is available as a NuGet Package: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) and from source code as a Github [sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span></span> 

### <a name="understanding-change-feed-processor-library"></a><span data-ttu-id="2f019-253">Основные сведения о библиотеке обработчика веб-канала изменений</span><span class="sxs-lookup"><span data-stu-id="2f019-253">Understanding Change Feed Processor library</span></span> 

<span data-ttu-id="2f019-254">Существует четыре основных компонента реализации обработчика веб-канала изменений: отслеживаемая коллекция, коллекция аренд, узел обработчика и потребители.</span><span class="sxs-lookup"><span data-stu-id="2f019-254">There are four main components of implementing the Change Feed Processor: the monitored collection, the lease collection, the processor host, and the consumers.</span></span> 

<span data-ttu-id="2f019-255">**Отслеживаемая коллекция** — это данные, из которых формируется веб-канал изменений.</span><span class="sxs-lookup"><span data-stu-id="2f019-255">**Monitored Collection:** The monitored collection is the data from which the change feed is generated.</span></span> <span data-ttu-id="2f019-256">Все операции вставки и изменения в отслеживаемой коллекции отражаются в веб-канале изменений коллекции.</span><span class="sxs-lookup"><span data-stu-id="2f019-256">Any inserts and changes to the monitored collection are reflected in the change feed of the collection.</span></span> 

<span data-ttu-id="2f019-257">**Коллекция аренд** — это коллекция, которая координирует обработку веб-канала изменений для нескольких рабочих ролей.</span><span class="sxs-lookup"><span data-stu-id="2f019-257">**Lease Collection:** The lease collection coordinates processing the change feed across multiple workers.</span></span> <span data-ttu-id="2f019-258">Отдельная коллекция используется для хранения аренд на каждую секцию.</span><span class="sxs-lookup"><span data-stu-id="2f019-258">A separate collection is used to store the leases with one lease per partition.</span></span> <span data-ttu-id="2f019-259">Эту коллекцию аренд следует хранить в другой учетной записи, регион записи которой ближе к региону с обработчиком веб-канала изменений.</span><span class="sxs-lookup"><span data-stu-id="2f019-259">It is advantageous to store this lease collection on a different account with the write region closer to where the Change Feed Processor is running.</span></span> <span data-ttu-id="2f019-260">Объект аренды содержит следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="2f019-260">A lease object contains the following attributes:</span></span> 
* <span data-ttu-id="2f019-261">Владелец: определяет узел, которому принадлежит аренда.</span><span class="sxs-lookup"><span data-stu-id="2f019-261">Owner: Specifies the host that owns the lease</span></span>
* <span data-ttu-id="2f019-262">Продолжение: определяет положение (маркер продолжения) определенной секции в веб-канале изменений.</span><span class="sxs-lookup"><span data-stu-id="2f019-262">Continuation: Specifies the position (continuation token) in the change feed for a particular partition</span></span>
* <span data-ttu-id="2f019-263">Отметка времени: время последнего обновления аренды. Отметка времени может использоваться для проверки истечения срока действия аренды.</span><span class="sxs-lookup"><span data-stu-id="2f019-263">Timestamp: Last time lease was updated; the timestamp can be used to check whether the lease is considered expired</span></span> 

<span data-ttu-id="2f019-264">**Узел обработчика.** Каждый узел определяет, сколько секций нужно обработать в зависимости от того, сколько других экземпляров узлов имеют активные аренды.</span><span class="sxs-lookup"><span data-stu-id="2f019-264">**Processor Host:** Each host determines how many partitions to process based on how many other instances of hosts have active leases.</span></span> 
1.  <span data-ttu-id="2f019-265">После запуска узла он получает аренды для распределения рабочей нагрузки по всем узлам.</span><span class="sxs-lookup"><span data-stu-id="2f019-265">When a host starts up, it acquires leases to balance the workload across all hosts.</span></span> <span data-ttu-id="2f019-266">Узел периодически обновляет аренды, чтобы они оставалась активными.</span><span class="sxs-lookup"><span data-stu-id="2f019-266">A host periodically renews leases, so leases remain active.</span></span> 
2.  <span data-ttu-id="2f019-267">Узел сопоставляет последний маркер продолжения с арендой перед каждой операцией чтения.</span><span class="sxs-lookup"><span data-stu-id="2f019-267">A host checkpoints the last continuation token to its lease for each read.</span></span> <span data-ttu-id="2f019-268">Чтобы обеспечить безопасность параллелизма, узел проверяет значение ETag для каждого обновления аренды.</span><span class="sxs-lookup"><span data-stu-id="2f019-268">To ensure concurrency safety, a host checks the ETag for each lease update.</span></span> <span data-ttu-id="2f019-269">Также поддерживаются другие стратегии контрольных точек.</span><span class="sxs-lookup"><span data-stu-id="2f019-269">Other checkpoint strategies are also supported.</span></span>  
3.  <span data-ttu-id="2f019-270">После завершения работы узел отменяет все аренды, но сохраняет сведения о продолжении, чтобы иметь позже возможность возобновить чтение с сохраненной контрольной точки.</span><span class="sxs-lookup"><span data-stu-id="2f019-270">Upon shutdown, a host releases all leases but keeps the continuation information, so it can resume reading from the stored checkpoint later.</span></span> 

<span data-ttu-id="2f019-271">В настоящее время количество узлов не может превышать количество секций (аренд).</span><span class="sxs-lookup"><span data-stu-id="2f019-271">At this time the number of hosts cannot be greater than the number of partitions (leases).</span></span>

<span data-ttu-id="2f019-272">**Потребители:** объекты-получатели или рабочие роли являются потоками, которые выполняют обработку веб-канала изменений, инициированную каждым узлом.</span><span class="sxs-lookup"><span data-stu-id="2f019-272">**Consumers:** Consumers, or workers, are threads that perform the change feed processing initiated by each host.</span></span> <span data-ttu-id="2f019-273">Каждый узел обработчика может иметь несколько объектов-получателей.</span><span class="sxs-lookup"><span data-stu-id="2f019-273">Each processor host can have multiple consumers.</span></span> <span data-ttu-id="2f019-274">Каждый объект-получатель считывает веб-канал изменений из секции, которой он присвоен, и уведомляет узел об изменениях и окончании срока действия аренд.</span><span class="sxs-lookup"><span data-stu-id="2f019-274">Each consumer reads the change feed from the partition it is assigned to and notifies its host of changes and expired leases.</span></span>

<span data-ttu-id="2f019-275">Чтобы лучше разобраться, как взаимодействуют эти четыре элемента обработчика веб-канала изменений, давайте рассмотрим пример на схеме ниже.</span><span class="sxs-lookup"><span data-stu-id="2f019-275">To further understand how these four elements of Change Feed Processor work together, let's look at an example in the following diagram.</span></span> <span data-ttu-id="2f019-276">Отслеживаемая коллекция хранит документы и использует city в качестве ключа секции.</span><span class="sxs-lookup"><span data-stu-id="2f019-276">The monitored collection stores documents and uses the "city" as the partition key.</span></span> <span data-ttu-id="2f019-277">Мы видим, что синяя секция содержит документы с полем city от A до E и т. д.</span><span class="sxs-lookup"><span data-stu-id="2f019-277">We see that the blue partition contains documents with the "city" field from "A-E" and so on.</span></span> <span data-ttu-id="2f019-278">Существует два узла, каждый с двумя объектами-получателями, которые выполняют операцию чтения из четырех секций в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="2f019-278">There are two hosts, each with two consumers reading from the four partitions in parallel.</span></span> <span data-ttu-id="2f019-279">Стрелки показывают конкретные точки в веб-канале изменений, в которых объекты-получатели выполняют операцию чтения.</span><span class="sxs-lookup"><span data-stu-id="2f019-279">The arrows show the consumers reading from a specific spot in the change feed.</span></span> <span data-ttu-id="2f019-280">В первой секции синим цветом представлены непрочитанные изменения, а голубым — уже прочитанные изменения в веб-канале изменений.</span><span class="sxs-lookup"><span data-stu-id="2f019-280">In the first partition, the darker blue represents unread changes while the light blue represents the already read changes on the change feed.</span></span> <span data-ttu-id="2f019-281">Узлы используют коллекцию аренд для хранения значения "продолжение", чтобы отслеживать текущую позицию чтения каждого объекта-получателя.</span><span class="sxs-lookup"><span data-stu-id="2f019-281">The hosts use the lease collection to store a "continuation" value to keep track of the current reading position for each consumer.</span></span> 

![Использование узла обработчика веб-канала изменений Azure Cosmos DB](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a><span data-ttu-id="2f019-283">Использование библиотеки обработчика веб-канала изменений</span><span class="sxs-lookup"><span data-stu-id="2f019-283">Using Change Feed Processor Library</span></span> 
<span data-ttu-id="2f019-284">В следующем разделе объясняется, как использовать библиотеку обработчика веб-канала изменений в контексте репликации изменений из исходной коллекции в целевую.</span><span class="sxs-lookup"><span data-stu-id="2f019-284">The following section explains how to use the Change Feed Processor library in the context of replicating changes from a source collection to a destination collection.</span></span> <span data-ttu-id="2f019-285">В данном случае исходная коллекция — это отслеживаемая коллекция обработчика веб-канала изменений.</span><span class="sxs-lookup"><span data-stu-id="2f019-285">Here, the source collection is the monitored collection in Change Feed Processor.</span></span> 

<span data-ttu-id="2f019-286">**Установка и добавление пакета NuGet обработчика веб-канала изменений**</span><span class="sxs-lookup"><span data-stu-id="2f019-286">**Install and include the Change Feed Processor NuGet package**</span></span> 

<span data-ttu-id="2f019-287">Прежде чем устанавливать пакет NuGet обработчика веб-канала изменений, установите:</span><span class="sxs-lookup"><span data-stu-id="2f019-287">Before installing Change Feed Processor NuGet Package, first install:</span></span> 
* <span data-ttu-id="2f019-288">Библиотеку Microsoft.Azure.DocumentDB (версии 1.13.1 или выше).</span><span class="sxs-lookup"><span data-stu-id="2f019-288">Microsoft.Azure.DocumentDB, version 1.13.1 or above</span></span> 
* <span data-ttu-id="2f019-289">Newtonsoft.Json, версии 9.0.1 или более поздней версии. Установите пакет `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` и добавьте его в качестве ссылки.</span><span class="sxs-lookup"><span data-stu-id="2f019-289">Newtonsoft.Json, version 9.0.1 or above Install `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` and include it as a reference.</span></span>

<span data-ttu-id="2f019-290">**Создайте отслеживаемую коллекцию, коллекцию аренд и назначения**</span><span class="sxs-lookup"><span data-stu-id="2f019-290">**Create a monitored, lease and destination collection**</span></span> 

<span data-ttu-id="2f019-291">Чтобы использовать библиотеку обработчика веб-канала изменений, необходимо создать коллекцию аренд перед запуском узлов обработчика.</span><span class="sxs-lookup"><span data-stu-id="2f019-291">In order to use the Change Feed Processor Library, the lease collection needs to be created before running the processor host(s).</span></span> <span data-ttu-id="2f019-292">Напоминаем, что эту коллекцию аренд следует хранить в другой учетной записи, регион записи которой ближе к региону с обработчиком веб-канала изменений.</span><span class="sxs-lookup"><span data-stu-id="2f019-292">Again, we recommend storing a lease collection on a different account with a write region closer to where the Change Feed Processor is running.</span></span> <span data-ttu-id="2f019-293">В этом примере перемещения данных необходимо создать целевую коллекцию перед запуском узла обработчика веб-канала изменений.</span><span class="sxs-lookup"><span data-stu-id="2f019-293">In this data movement example, we need to create the destination collection before running the Change Feed Processor host.</span></span> <span data-ttu-id="2f019-294">В примере кода мы вызовем вспомогательный метод для создания отслеживаемой коллекции, коллекции аренд и целевой коллекции, если они еще не существуют.</span><span class="sxs-lookup"><span data-stu-id="2f019-294">In the sample code we call a helper method to create the monitored, leased, and destination collections if they do not already exist.</span></span> 

> [!WARNING]
> <span data-ttu-id="2f019-295">Создание коллекции связано с ценовыми требованиями, так как для взаимодействия с базой данных Azure Cosmos DB для приложения резервируется пропускная способность.</span><span class="sxs-lookup"><span data-stu-id="2f019-295">Creating a collection has pricing implications, as you are reserving throughput for the application to communicate with Azure Cosmos DB.</span></span> <span data-ttu-id="2f019-296">Дополнительные сведения см. на [странице цен](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="2f019-296">For more details, please visit the [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

<span data-ttu-id="2f019-297">*Создание узла обработчика*</span><span class="sxs-lookup"><span data-stu-id="2f019-297">*Creating a processor host*</span></span>

<span data-ttu-id="2f019-298">Класс `ChangeFeedProcessorHost` предоставляет потокобезопасную многопроцессную среду безопасного выполнения для реализаций обработчиков событий. Эта среда также предоставляет средства управления контрольными точками и арендой секций.</span><span class="sxs-lookup"><span data-stu-id="2f019-298">The `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.</span></span> <span data-ttu-id="2f019-299">Для использования класса `ChangeFeedProcessorHost` можно реализовать `IChangeFeedObserver`.</span><span class="sxs-lookup"><span data-stu-id="2f019-299">To use the `ChangeFeedProcessorHost` class, you can implement `IChangeFeedObserver`.</span></span> <span data-ttu-id="2f019-300">Этот интерфейс содержит три метода:</span><span class="sxs-lookup"><span data-stu-id="2f019-300">This interface contains three methods:</span></span>

* <span data-ttu-id="2f019-301">`OpenAsync` — эта функция вызывается при открытии наблюдателя веб-канала изменений.</span><span class="sxs-lookup"><span data-stu-id="2f019-301">`OpenAsync`: This function is called when change feed observer is opened.</span></span> <span data-ttu-id="2f019-302">Ее можно изменить для выполнения определенных действий при открытии объекта-получателя и наблюдателя.</span><span class="sxs-lookup"><span data-stu-id="2f019-302">It can be modified to perform a specific action when consumer/observer is opened.</span></span>  
* <span data-ttu-id="2f019-303">`CloseAsync` — эта функция вызывается при закрытии наблюдателя веб-канала изменений.</span><span class="sxs-lookup"><span data-stu-id="2f019-303">`CloseAsync`: This function is called when change feed observer is terminated.</span></span> <span data-ttu-id="2f019-304">Ее можно изменить для выполнения определенных действий при закрытии объекта-получателя и наблюдателя.</span><span class="sxs-lookup"><span data-stu-id="2f019-304">It can be modified to perform a specific action when consumer/observer is closed.</span></span>  
* <span data-ttu-id="2f019-305">`ProcessChangesAsync` — эта функция вызывается, когда новые изменения документа доступны в веб-канале изменений.</span><span class="sxs-lookup"><span data-stu-id="2f019-305">`ProcessChangesAsync`: This function is called when document new changes are available on change feed.</span></span> <span data-ttu-id="2f019-306">Ее можно изменить для выполнения определенных действий после каждого обновления веб-канала изменений.</span><span class="sxs-lookup"><span data-stu-id="2f019-306">It can be modified to perform a specific action upon every change feed update.</span></span>  

<span data-ttu-id="2f019-307">В нашем примере мы реализовали интерфейс `IChangeFeedObserver` посредством класса `DocumentFeedObserver`.</span><span class="sxs-lookup"><span data-stu-id="2f019-307">In our example, we implement the interface `IChangeFeedObserver` through the `DocumentFeedObserver` class.</span></span> <span data-ttu-id="2f019-308">Здесь функция `ProcessChangesAsync` вставляет (обновляет) документ из веб-канала изменений в коллекцию назначения.</span><span class="sxs-lookup"><span data-stu-id="2f019-308">Here, the `ProcessChangesAsync` function upserts (updates) a document from change feed into the destination collection.</span></span> <span data-ttu-id="2f019-309">Этот пример полезен для перемещения данных из одной коллекции в другую, чтобы изменить ключ секции набора данных.</span><span class="sxs-lookup"><span data-stu-id="2f019-309">This example is useful for moving data from one collection to another in order to change the partition key of a data set.</span></span> 

<span data-ttu-id="2f019-310">*Запуск узла обработчика*</span><span class="sxs-lookup"><span data-stu-id="2f019-310">*Running the Processor Host*</span></span>

<span data-ttu-id="2f019-311">Перед началом обработки событий можно настроить параметры веб-канала и узла веб-канала.</span><span class="sxs-lookup"><span data-stu-id="2f019-311">Before beginning event processing, both change feed options and change feed host options can be customized.</span></span> 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval to 15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
<span data-ttu-id="2f019-312">В следующих таблицах приведены конкретные поля, которые можно настроить.</span><span class="sxs-lookup"><span data-stu-id="2f019-312">The specific fields that can be customized are summarized in the following tables.</span></span> 

<span data-ttu-id="2f019-313">**Параметры веб-канала изменений**:</span><span class="sxs-lookup"><span data-stu-id="2f019-313">**Change Feed Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="2f019-314">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="2f019-314">Property Name</span></span></th>
        <th><span data-ttu-id="2f019-315">Описание</span><span class="sxs-lookup"><span data-stu-id="2f019-315">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="2f019-316">MaxItemCount</span><span class="sxs-lookup"><span data-stu-id="2f019-316">MaxItemCount</span></span></td>
        <td><span data-ttu-id="2f019-317">Получает или определяет максимальное количество элементов, возвращаемых в операции перечисления в службе базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2f019-317">Gets or sets the maximum number of items to be returned in the enumeration operation in the Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2f019-318">PartitionKeyRangeId</span><span class="sxs-lookup"><span data-stu-id="2f019-318">PartitionKeyRangeId</span></span></td>
        <td><span data-ttu-id="2f019-319">Получает или определяет идентификатор диапазона ключей секции для текущего запроса в службу базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2f019-319">Gets or sets the partition key range id for the current request in the Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2f019-320">RequestContinuation</span><span class="sxs-lookup"><span data-stu-id="2f019-320">RequestContinuation</span></span></td>
        <td><span data-ttu-id="2f019-321">Получает или определяет маркер продолжения запроса в службе базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2f019-321">Gets or sets the request continuation token in the Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="2f019-322">SessionToken</span><span class="sxs-lookup"><span data-stu-id="2f019-322">SessionToken</span></span></td>
        <td><span data-ttu-id="2f019-323">Получает или определяет маркер сеанса для использования с согласованностью сеансов в службе базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2f019-323">Gets or sets the session token for use with session consistency in the Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="2f019-324">StartFromBeginning</span><span class="sxs-lookup"><span data-stu-id="2f019-324">StartFromBeginning</span></span></td>
        <td><span data-ttu-id="2f019-325">Получает или определяет, откуда должен запускаться веб-канал изменений в службе базы данных Azure Cosmos DB (с самого начала (true) или из текущего положения (false)).</span><span class="sxs-lookup"><span data-stu-id="2f019-325">Gets or sets whether change feed in the Azure Cosmos DB database service should start from the beginning (true) or from current (false).</span></span> <span data-ttu-id="2f019-326">По умолчанию он начинается с текущего положения (false).</span><span class="sxs-lookup"><span data-stu-id="2f019-326">By default, it starts from current (false).</span></span></td>
    </tr>
</table>

<span data-ttu-id="2f019-327">**Параметры узла веб-канала изменений**:</span><span class="sxs-lookup"><span data-stu-id="2f019-327">**Change Feed Host Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="2f019-328">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="2f019-328">Property Name</span></span></th>
        <th><span data-ttu-id="2f019-329">Тип</span><span class="sxs-lookup"><span data-stu-id="2f019-329">Type</span></span></th>
        <th><span data-ttu-id="2f019-330">Описание</span><span class="sxs-lookup"><span data-stu-id="2f019-330">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="2f019-331">LeaseRenewInterval</span><span class="sxs-lookup"><span data-stu-id="2f019-331">LeaseRenewInterval</span></span></td>
        <td><span data-ttu-id="2f019-332">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="2f019-332">TimeSpan</span></span></td>
        <td><span data-ttu-id="2f019-333">Интервал для всех аренд секций, которые в данный момент удерживаются экземпляром ChangeFeedEventHost.</span><span class="sxs-lookup"><span data-stu-id="2f019-333">The interval for all leases for partitions currently held by the ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2f019-334">LeaseAcquireInterval</span><span class="sxs-lookup"><span data-stu-id="2f019-334">LeaseAcquireInterval</span></span></td>
        <td><span data-ttu-id="2f019-335">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="2f019-335">TimeSpan</span></span></td>
        <td><span data-ttu-id="2f019-336">Интервал для запуска задачи вычисления равномерности распределения секций между известными экземплярами узла.</span><span class="sxs-lookup"><span data-stu-id="2f019-336">The interval to kick off a task to compute whether partitions are distributed evenly among known host instances.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2f019-337">LeaseExpirationInterval</span><span class="sxs-lookup"><span data-stu-id="2f019-337">LeaseExpirationInterval</span></span></td>
        <td><span data-ttu-id="2f019-338">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="2f019-338">TimeSpan</span></span></td>
        <td><span data-ttu-id="2f019-339">Интервал, за который берется аренда, представляющая секцию.</span><span class="sxs-lookup"><span data-stu-id="2f019-339">The interval for which the lease is taken on a lease representing a partition.</span></span> <span data-ttu-id="2f019-340">Если аренда не была обновлена в течение этого интервала, она будет просрочена и владение секцией перейдет к другому экземпляру ChangeFeedEventHost.</span><span class="sxs-lookup"><span data-stu-id="2f019-340">If the lease is not renewed within this interval, it is expired and ownership of the partition moves to another ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2f019-341">FeedPollDelay</span><span class="sxs-lookup"><span data-stu-id="2f019-341">FeedPollDelay</span></span></td>
        <td><span data-ttu-id="2f019-342">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="2f019-342">TimeSpan</span></span></td>
        <td><span data-ttu-id="2f019-343">Задержка между опросами секции на наличие новых изменений в веб-канале, после того как все текущие изменения будут утеряны.</span><span class="sxs-lookup"><span data-stu-id="2f019-343">The delay between polling a partition for new changes on the feed, after all current changes are drained.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2f019-344">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="2f019-344">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="2f019-345">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="2f019-345">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="2f019-346">Частота создания контрольных точек аренд.</span><span class="sxs-lookup"><span data-stu-id="2f019-346">The frequency to checkpoint leases.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2f019-347">MinPartitionCount</span><span class="sxs-lookup"><span data-stu-id="2f019-347">MinPartitionCount</span></span></td>
        <td><span data-ttu-id="2f019-348">int</span><span class="sxs-lookup"><span data-stu-id="2f019-348">Int</span></span></td>
        <td><span data-ttu-id="2f019-349">Минимальное количество секций узла.</span><span class="sxs-lookup"><span data-stu-id="2f019-349">The minimum partition count for the host.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2f019-350">MaxPartitionCount</span><span class="sxs-lookup"><span data-stu-id="2f019-350">MaxPartitionCount</span></span></td>
        <td><span data-ttu-id="2f019-351">int</span><span class="sxs-lookup"><span data-stu-id="2f019-351">Int</span></span></td>
        <td><span data-ttu-id="2f019-352">Максимальное число секций, которые можно использовать в узле.</span><span class="sxs-lookup"><span data-stu-id="2f019-352">The maximum number of partitions the host can serve.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="2f019-353">DiscardExistingLeases</span><span class="sxs-lookup"><span data-stu-id="2f019-353">DiscardExistingLeases</span></span></td>
        <td><span data-ttu-id="2f019-354">Bool</span><span class="sxs-lookup"><span data-stu-id="2f019-354">Bool</span></span></td>
        <td><span data-ttu-id="2f019-355">При запуске узла следует удалить все существующие аренды и узел должен быть запущен с нуля.</span><span class="sxs-lookup"><span data-stu-id="2f019-355">Whether on the start of the host all existing leases should be deleted and the host should start from scratch.</span></span></td>
    </tr>
</table>


<span data-ttu-id="2f019-356">Чтобы начать обработку событий, следует создать экземпляр `ChangeFeedProcessorHost`, указав соответствующие параметры для коллекции Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2f019-356">To start event processing, instantiate `ChangeFeedProcessorHost`, providing the appropriate parameters for your Azure Cosmos DB collection.</span></span> <span data-ttu-id="2f019-357">Затем вызовите метод `RegisterObserverAsync` для регистрации вашей реализации `IChangeFeedObserver` (в этом примере DocumentFeedObserver) в среде выполнения.</span><span class="sxs-lookup"><span data-stu-id="2f019-357">Then, call `RegisterObserverAsync` to register your `IChangeFeedObserver` (DocumentFeedObserver in this example) implementation with the runtime.</span></span> <span data-ttu-id="2f019-358">На этом этапе узел попытается получить аренду для каждого диапазона ключей секций в коллекции Azure Cosmos DB, используя "жадный" алгоритм.</span><span class="sxs-lookup"><span data-stu-id="2f019-358">At this point, the host attempts to acquire a lease on every partition key range in the Azure Cosmos DB collection using a "greedy" algorithm.</span></span> <span data-ttu-id="2f019-359">Эти аренды будут продолжаться в течение заданного промежутка времени, после чего их необходимо продлить.</span><span class="sxs-lookup"><span data-stu-id="2f019-359">These leases last for a given timeframe and must then be renewed.</span></span> <span data-ttu-id="2f019-360">По мере перехода новых узлов (в нашем случае это рабочие экземпляры) в оперативный режим они размещают резервирования аренды и со временем нагрузка смещается между узлами при каждой попытке получения дополнительных аренд.</span><span class="sxs-lookup"><span data-stu-id="2f019-360">As new nodes, worker instances, in this case, come online, they place lease reservations and over time the load shifts between nodes as each host attempts to acquire more leases.</span></span> 

<span data-ttu-id="2f019-361">В примере кода мы используем класс фабрики (DocumentFeedObserverFactory.cs) для создания наблюдателя и `RegistObserverFactoryAsync`, чтобы его зарегистрировать.</span><span class="sxs-lookup"><span data-stu-id="2f019-361">In the sample code, we use a factory class (DocumentFeedObserverFactory.cs) to create an observer and the `RegistObserverFactoryAsync` to register the observer.</span></span> 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter to stop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
<span data-ttu-id="2f019-362">Со временем устанавливается равновесие.</span><span class="sxs-lookup"><span data-stu-id="2f019-362">Over time, an equilibrium is established.</span></span> <span data-ttu-id="2f019-363">Такая динамическая возможность позволяет применить к потребителям автоматическое масштабирование как вверх, так и вниз на основе использования ресурсов ЦП.</span><span class="sxs-lookup"><span data-stu-id="2f019-363">This dynamic capability enables CPU-based auto-scaling to be applied to consumers for both scale-up and scale-down.</span></span> <span data-ttu-id="2f019-364">Если события становятся доступными в Azure Cosmos DB быстрее, чем могут обработать потребители, то увеличение использования ресурсов ЦП потребителями можно использовать для автоматического масштабирования на основе числа экземпляров исполнителей.</span><span class="sxs-lookup"><span data-stu-id="2f019-364">If changes are available in Azure Cosmos DB at a faster rate than consumers can process, the CPU increase on consumers can be used to cause an auto-scale on worker instance count.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f019-365">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2f019-365">Next steps</span></span>
* <span data-ttu-id="2f019-366">Попробуйте поработать с [примерами кода веб-канала изменений Azure Cosmos DB в GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed).</span><span class="sxs-lookup"><span data-stu-id="2f019-366">Try the [Azure Cosmos DB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span></span>
* <span data-ttu-id="2f019-367">Приступите к созданию кода с помощью [пакетов SDK](documentdb-sdk-dotnet.md) или [REST API](/rest/api/documentdb/) Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="2f019-367">Get started coding with the [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/).</span></span>
