---
title: "Azure Cosmos DB: API-интерфейс, пакет SDK Java и материалы для DocumentDB | Microsoft Docs"
description: "Сведения о пакете SDK и API-интерфейсе Java, включая даты выхода и прекращения использования, а также изменения, внесенные в каждую версию пакета SDK Java для Azure Cosmos DB DocumentDB."
services: cosmos-db
documentationcenter: java
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 7861cadf-2a05-471a-9925-0fec0599351b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 07/11/2017
ms.author: khdang
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 15e3f7ef3bfd6b1f61fe6081a378bdb29e0a1aa2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a><span data-ttu-id="faa93-103">Azure Cosmos DB: заметки о выпуске и материалы по пакету SDK Java для DocumentDB</span><span class="sxs-lookup"><span data-stu-id="faa93-103">Azure Cosmos DB: DocumentDB Java SDK release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="faa93-104">.NET</span><span class="sxs-lookup"><span data-stu-id="faa93-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="faa93-105">Веб-канал изменений в .NET</span><span class="sxs-lookup"><span data-stu-id="faa93-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="faa93-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="faa93-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="faa93-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="faa93-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="faa93-108">Java</span><span class="sxs-lookup"><span data-stu-id="faa93-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="faa93-109">Python</span><span class="sxs-lookup"><span data-stu-id="faa93-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="faa93-110">REST</span><span class="sxs-lookup"><span data-stu-id="faa93-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="faa93-111">Поставщик ресурсов REST</span><span class="sxs-lookup"><span data-stu-id="faa93-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="faa93-112">SQL</span><span class="sxs-lookup"><span data-stu-id="faa93-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="faa93-113">**Скачивание пакета SDK**</span><span class="sxs-lookup"><span data-stu-id="faa93-113">**SDK Download**</span></span></td><td>[<span data-ttu-id="faa93-114">Maven</span><span class="sxs-lookup"><span data-stu-id="faa93-114">Maven</span></span>](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td><span data-ttu-id="faa93-115">**Документация по API**</span><span class="sxs-lookup"><span data-stu-id="faa93-115">**API documentation**</span></span></td><td>[<span data-ttu-id="faa93-116">Справочная документация по API Java</span><span class="sxs-lookup"><span data-stu-id="faa93-116">Java API reference documentation</span></span>](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td><span data-ttu-id="faa93-117">**Участие в разработке пакета SDK**</span><span class="sxs-lookup"><span data-stu-id="faa93-117">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="faa93-118">GitHub</span><span class="sxs-lookup"><span data-stu-id="faa93-118">GitHub</span></span>](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td><span data-ttu-id="faa93-119">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="faa93-119">**Get started**</span></span></td><td>[<span data-ttu-id="faa93-120">Приступая к работе с пакетом SDK для Java</span><span class="sxs-lookup"><span data-stu-id="faa93-120">Get started with the Java SDK</span></span>](documentdb-java-get-started.md)</td></tr>

<tr><td><span data-ttu-id="faa93-121">**Учебник по веб-приложениям**</span><span class="sxs-lookup"><span data-stu-id="faa93-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="faa93-122">Руководство по ASP.NET MVC. Разработка веб-приложений в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="faa93-122">Web application development with Azure Cosmos DB</span></span>](documentdb-java-application.md)</td></tr>

<tr><td><span data-ttu-id="faa93-123">**Текущая поддерживаемая среда выполнения**</span><span class="sxs-lookup"><span data-stu-id="faa93-123">**Current supported runtime**</span></span></td><td>[<span data-ttu-id="faa93-124">JDK 7</span><span class="sxs-lookup"><span data-stu-id="faa93-124">JDK 7</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="faa93-125">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="faa93-125">Release Notes</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="faa93-126"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="faa93-126"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="faa93-127">Важные исправления для обработки запросов во время разбиения на секции.</span><span class="sxs-lookup"><span data-stu-id="faa93-127">Critical bug fixes to request processing during partition splits.</span></span>
* <span data-ttu-id="faa93-128">Исправлена проблема с уровнями согласованности Strong и BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="faa93-128">Fixed an issue with the Strong and BoundedStaleness consistency levels.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="faa93-129"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="faa93-129"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="faa93-130">Добавлена поддержка нового уровня согласованности с именем ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="faa93-130">Added support for a new consistency level called ConsistentPrefix.</span></span>
* <span data-ttu-id="faa93-131">Исправлена ошибка чтения коллекции в режиме сеанса.</span><span class="sxs-lookup"><span data-stu-id="faa93-131">Fixed a bug in reading collection in session mode.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="faa93-132"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="faa93-132"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="faa93-133">Включена поддержка секционированных коллекций с производительностью 2500 ЕЗ/с, а также масштабирование с шагом в 100 ЕЗ/с.</span><span class="sxs-lookup"><span data-stu-id="faa93-133">Enabled support for partitioned collection with as low as 2,500 RU/sec and scale in increments of 100 RU/sec.</span></span>
* <span data-ttu-id="faa93-134">Исправлена ошибка в машинной сборке, которая могла вызывать в некоторых запросах исключение NullRef.</span><span class="sxs-lookup"><span data-stu-id="faa93-134">Fixed a bug in the native assembly which can cause NullRef exception in some queries.</span></span>

### <a name="a-name196196"></a><span data-ttu-id="faa93-135"><a name="1.9.6"/>1.9.6</span><span class="sxs-lookup"><span data-stu-id="faa93-135"><a name="1.9.6"/>1.9.6</span></span>
* <span data-ttu-id="faa93-136">Исправлена ошибка в конфигурации обработчика запросов, которая могла вызывать исключения для запросов в режиме шлюза.</span><span class="sxs-lookup"><span data-stu-id="faa93-136">Fixed a bug in the query engine configuration that may cause exceptions for queries in Gateway mode.</span></span>
* <span data-ttu-id="faa93-137">Исправлены некоторые ошибки в контейнере сеансов, которые могли вызывать исключение Owner resource not found (Ресурс владельца не найден) для запросов сразу после создания коллекции.</span><span class="sxs-lookup"><span data-stu-id="faa93-137">Fixed a few bugs in the session container that may cause an "Owner resource not found" exception for requests immediately after collection creation.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="faa93-138"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="faa93-138"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="faa93-139">Добавлена поддержка статистических запросов (COUNT, MIN, MAX, SUM и AVG).</span><span class="sxs-lookup"><span data-stu-id="faa93-139">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="faa93-140">Дополнительные сведения см. в разделе [Статистические функции](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="faa93-140">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="faa93-141">Добавлена поддержка веб-канала изменений.</span><span class="sxs-lookup"><span data-stu-id="faa93-141">Added support for change feed.</span></span>
* <span data-ttu-id="faa93-142">Добавлена поддержка сведений о квотах коллекций посредством RequestOptions.setPopulateQuotaInfo.</span><span class="sxs-lookup"><span data-stu-id="faa93-142">Added support for collection quota information through RequestOptions.setPopulateQuotaInfo.</span></span>
* <span data-ttu-id="faa93-143">Добавлена поддержка ведения журнала сценариев хранимых процедур посредством RequestOptions.setScriptLoggingEnabled.</span><span class="sxs-lookup"><span data-stu-id="faa93-143">Added support for stored procedure script logging through RequestOptions.setScriptLoggingEnabled.</span></span>
* <span data-ttu-id="faa93-144">Исправлена ошибка, из-за которой запросы в режиме DirectHttps переставали отвечать при обнаружении ошибок регулирования.</span><span class="sxs-lookup"><span data-stu-id="faa93-144">Fixed a bug where query in DirectHttps mode may hang when encountering throttle failures.</span></span>
* <span data-ttu-id="faa93-145">Исправлена ошибка в режиме согласованности сеанса.</span><span class="sxs-lookup"><span data-stu-id="faa93-145">Fixed a bug in session consistency mode.</span></span>
* <span data-ttu-id="faa93-146">Исправлена ошибка, которая могла приводить к порождению исключения NullReferenceException в HttpContext при высокой частоте запросов.</span><span class="sxs-lookup"><span data-stu-id="faa93-146">Fixed a bug which may cause NullReferenceException in HttpContext when request rate is high.</span></span>
* <span data-ttu-id="faa93-147">Повышена производительность режима DirectHttps.</span><span class="sxs-lookup"><span data-stu-id="faa93-147">Improved performance of DirectHttps mode.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="faa93-148"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="faa93-148"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="faa93-149">Добавлена поддержка прокси-сервера на основе экземпляра простого клиента с помощью API ConnectionPolicy.setProxy().</span><span class="sxs-lookup"><span data-stu-id="faa93-149">Added simple client instance-based proxy support with ConnectionPolicy.setProxy() API.</span></span>
* <span data-ttu-id="faa93-150">Добавлен API DocumentClient.close() для правильного завершения работы экземпляра DocumentClient.</span><span class="sxs-lookup"><span data-stu-id="faa93-150">Added DocumentClient.close() API to properly shutdown DocumentClient instance.</span></span>
* <span data-ttu-id="faa93-151">Повышена производительность запросов в режиме прямого подключения за счет получения плана запроса от машинной сборки, а не шлюза.</span><span class="sxs-lookup"><span data-stu-id="faa93-151">Improved query performance in direct connectivity mode by deriving the query plan from the native assembly instead of the Gateway.</span></span>
* <span data-ttu-id="faa93-152">Задан параметр FAIL_ON_UNKNOWN_PROPERTIES = false, чтобы пользователям не нужно было определять JsonIgnoreProperties в POJO.</span><span class="sxs-lookup"><span data-stu-id="faa93-152">Set FAIL_ON_UNKNOWN_PROPERTIES = false so users don't need to define JsonIgnoreProperties in their POJO.</span></span>
* <span data-ttu-id="faa93-153">Выполнен рефакторинг ведения журнала для использования SLF4J.</span><span class="sxs-lookup"><span data-stu-id="faa93-153">Refactored logging to use SLF4J.</span></span>
* <span data-ttu-id="faa93-154">Исправлено несколько ошибок в модуле чтения данных согласованности.</span><span class="sxs-lookup"><span data-stu-id="faa93-154">Fixed a few other bugs in consistency reader.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="faa93-155"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="faa93-155"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="faa93-156">Исправлена ошибка в управлении подключениями для предотвращения утечек в режиме прямого подключения.</span><span class="sxs-lookup"><span data-stu-id="faa93-156">Fixed a bug in the connection management to prevent connection leaks in direct connectivity mode.</span></span>
* <span data-ttu-id="faa93-157">Исправлена ошибка в запросе TOP, которая могла порождать исключение NullReferenece.</span><span class="sxs-lookup"><span data-stu-id="faa93-157">Fixed a bug in the TOP query where it may throw NullReferenece exception.</span></span>
* <span data-ttu-id="faa93-158">Повышена производительности за счет сокращения числа сетевых вызовов к внутренним кэшам.</span><span class="sxs-lookup"><span data-stu-id="faa93-158">Improved performance by reducing the number of network call for the internal caches.</span></span>
* <span data-ttu-id="faa93-159">В DocumentClientException добавлены код состояния, ActivityID и универсальный код ресурса (URI) для более удобного устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="faa93-159">Added status code, ActivityID and Request URI in DocumentClientException for better troubleshooting.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="faa93-160"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="faa93-160"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="faa93-161">Исправлена проблема в управлении подключениями для повышения стабильности.</span><span class="sxs-lookup"><span data-stu-id="faa93-161">Fixed an issue in the connection management for stability.</span></span>

### <a name="a-name191191"></a><span data-ttu-id="faa93-162"><a name="1.9.1"/>1.9.1</span><span class="sxs-lookup"><span data-stu-id="faa93-162"><a name="1.9.1"/>1.9.1</span></span>
* <span data-ttu-id="faa93-163">Добавлена поддержка уровня согласованности BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="faa93-163">Added support for BoundedStaleness consistency level.</span></span>
* <span data-ttu-id="faa93-164">Добавлена поддержка прямого подключения для операций CRUD с секционированными коллекциями.</span><span class="sxs-lookup"><span data-stu-id="faa93-164">Added support for direct connectivity for CRUD operations for partitioned collections.</span></span>
* <span data-ttu-id="faa93-165">Исправлена ошибка, возникающая при выполнении запросов к базе данных с помощью SQL.</span><span class="sxs-lookup"><span data-stu-id="faa93-165">Fixed a bug in querying a database with SQL.</span></span>
* <span data-ttu-id="faa93-166">Исправлена ошибка в кэше сеанса, приводившая к неправильному заданию маркера сеанса.</span><span class="sxs-lookup"><span data-stu-id="faa93-166">Fixed a bug in the session cache where session token may be set incorrectly.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="faa93-167"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="faa93-167"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="faa93-168">Добавлена поддержка параллельных запросов между секциями.</span><span class="sxs-lookup"><span data-stu-id="faa93-168">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="faa93-169">Добавлена поддержка запросов TOP и ORDER BY для секционированных коллекций.</span><span class="sxs-lookup"><span data-stu-id="faa93-169">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>
* <span data-ttu-id="faa93-170">Добавлена поддержка строгой согласованности.</span><span class="sxs-lookup"><span data-stu-id="faa93-170">Added support for strong consistency.</span></span>
* <span data-ttu-id="faa93-171">Добавлена поддержка запросов по имени при использовании прямого подключения.</span><span class="sxs-lookup"><span data-stu-id="faa93-171">Added support for name based requests when using direct connectivity.</span></span>
* <span data-ttu-id="faa93-172">Внесено исправление, обеспечивающее согласованность ActivityId для всех попыток выполнения запроса.</span><span class="sxs-lookup"><span data-stu-id="faa93-172">Fixed to make ActivityId stay consistent across all request retries.</span></span>
* <span data-ttu-id="faa93-173">Исправлена ошибка, связанная с кэшем сеанса и воссозданием коллекции с тем же именем.</span><span class="sxs-lookup"><span data-stu-id="faa93-173">Fixed a bug related to the session cache when recreating a collection with the same name.</span></span>
* <span data-ttu-id="faa93-174">Добавлены типы данных Polygon и LineString и задана политика индексирования коллекций для запросов пространственных геозон.</span><span class="sxs-lookup"><span data-stu-id="faa93-174">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="faa93-175">Устранены проблемы с JavaDoc для Java 1.8.</span><span class="sxs-lookup"><span data-stu-id="faa93-175">Fixed issues with Java Doc for Java 1.8.</span></span>

### <a name="a-name181181"></a><span data-ttu-id="faa93-176"><a name="1.8.1"/>1.8.1</span><span class="sxs-lookup"><span data-stu-id="faa93-176"><a name="1.8.1"/>1.8.1</span></span>
* <span data-ttu-id="faa93-177">Исправлена ошибка в PartitionKeyDefinitionMap, из-за которой осуществлялось кэширование коллекций одной секции и не выполнялись дополнительные запросы на получение ключа секции.</span><span class="sxs-lookup"><span data-stu-id="faa93-177">Fixed a bug in PartitionKeyDefinitionMap to cache single partition collections and not make extra fetch partition key requests.</span></span>
* <span data-ttu-id="faa93-178">Исправлена ошибка, из-за которой при предоставлении неправильного ключа секции не предпринималась повторная попытка.</span><span class="sxs-lookup"><span data-stu-id="faa93-178">Fixed a bug to not retry when an incorrect partition key value is provided.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="faa93-179"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="faa93-179"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="faa93-180">Добавлена поддержка учетных записей базы данных в нескольких регионах.</span><span class="sxs-lookup"><span data-stu-id="faa93-180">Added the support for multi-region database accounts.</span></span>
* <span data-ttu-id="faa93-181">Добавлена поддержка автоматического повтора на отрегулированных запросов с параметрами для настройки максимального количества повторов и максимального время между повторами.</span><span class="sxs-lookup"><span data-stu-id="faa93-181">Added support for automatic retry on throttled requests with options to customize the max retry attempts and max retry wait time.</span></span>  <span data-ttu-id="faa93-182">Ознакомьтесь с RetryOptions и ConnectionPolicy.getRetryOptions().</span><span class="sxs-lookup"><span data-stu-id="faa93-182">See RetryOptions and ConnectionPolicy.getRetryOptions().</span></span>
* <span data-ttu-id="faa93-183">Не рекомендуется использовать IPartitionResolver на основе пользовательского кода секционирования.</span><span class="sxs-lookup"><span data-stu-id="faa93-183">Deprecated IPartitionResolver based custom partitioning code.</span></span> <span data-ttu-id="faa93-184">Используйте секционированные коллекции, чтобы увеличить возможности хранилища и пропускную способность.</span><span class="sxs-lookup"><span data-stu-id="faa93-184">Please use partitioned collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="faa93-185"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="faa93-185"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="faa93-186">Добавлена поддержка политики повтора для регулирования.</span><span class="sxs-lookup"><span data-stu-id="faa93-186">Added retry policy support for throttling.</span></span>  

### <a name="a-name170170"></a><span data-ttu-id="faa93-187"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="faa93-187"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="faa93-188">Добавлена поддержка срока жизни для документов.</span><span class="sxs-lookup"><span data-stu-id="faa93-188">Added time to live (TTL) support for documents.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="faa93-189"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="faa93-189"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="faa93-190">Реализованы [секционированные коллекции](partition-data.md) и [определяемые пользователем уровни производительности](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="faa93-190">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <a name="a-name151151"></a><span data-ttu-id="faa93-191"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="faa93-191"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="faa93-192">Исправлена ошибка в HashPartitionResolver, чтобы значения создавались с прямым порядком байтов для согласования с другими пакетами SDK.</span><span class="sxs-lookup"><span data-stu-id="faa93-192">Fixed a bug in HashPartitionResolver to generate hash values in little-endian to be consistent with other SDKs.</span></span>

### <a name="a-name150150"></a><span data-ttu-id="faa93-193"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="faa93-193"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="faa93-194">Добавьте сопоставители разделов "Хэш" и "Диапазон" для сегментирования приложений на разделы.</span><span class="sxs-lookup"><span data-stu-id="faa93-194">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="faa93-195"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="faa93-195"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="faa93-196">Реализована операция Upsert.</span><span class="sxs-lookup"><span data-stu-id="faa93-196">Implement Upsert.</span></span> <span data-ttu-id="faa93-197">Для поддержки функции Upsert добавлены новые методы upsertXXX.</span><span class="sxs-lookup"><span data-stu-id="faa93-197">New upsertXXX methods added to support Upsert feature.</span></span>
* <span data-ttu-id="faa93-198">Реализована маршрутизация на основе идентификатора.</span><span class="sxs-lookup"><span data-stu-id="faa93-198">Implement ID Based Routing.</span></span> <span data-ttu-id="faa93-199">Отсутствуют изменения общего API-интерфейса. Все изменения касаются внутреннего интерфейса.</span><span class="sxs-lookup"><span data-stu-id="faa93-199">No public API changes, all changes internal.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="faa93-200"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="faa93-200"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="faa93-201">Пропущен номер выпуска для согласованности номера версии с другими пакетами SDK.</span><span class="sxs-lookup"><span data-stu-id="faa93-201">Release skipped to bring version number in alignment with other SDKs</span></span>

### <a name="a-name120120"></a><span data-ttu-id="faa93-202"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="faa93-202"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="faa93-203">Поддержка геопространственного индекса</span><span class="sxs-lookup"><span data-stu-id="faa93-203">Supports GeoSpatial Index</span></span>
* <span data-ttu-id="faa93-204">Проверка свойств идентификатора для всех ресурсов.</span><span class="sxs-lookup"><span data-stu-id="faa93-204">Validates id property for all resources.</span></span> <span data-ttu-id="faa93-205">Идентификаторы ресурсов не могут содержать знаки ?, /, #, \, или заканчиваться пробелом.</span><span class="sxs-lookup"><span data-stu-id="faa93-205">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="faa93-206">Добавлен новый заголовок "ход выполнения преобразования индекса" в ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="faa93-206">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="faa93-207"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="faa93-207"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="faa93-208">Реализована политика индексации версии 2.</span><span class="sxs-lookup"><span data-stu-id="faa93-208">Implements V2 indexing policy</span></span>

### <a name="a-name100100"></a><span data-ttu-id="faa93-209"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="faa93-209"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="faa93-210">Пакет SDK общей доступности.</span><span class="sxs-lookup"><span data-stu-id="faa93-210">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="faa93-211">Даты выпуска и выбытия</span><span class="sxs-lookup"><span data-stu-id="faa93-211">Release & Retirement Dates</span></span>
<span data-ttu-id="faa93-212">Корпорация Майкрософт отправит уведомление минимум за **12 месяцев** до вывода пакета SDK из эксплуатации, чтобы обеспечить более плавный переход на новую или поддерживаемую версию.</span><span class="sxs-lookup"><span data-stu-id="faa93-212">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="faa93-213">Новые функции, возможности и оптимизации добавляются только в текущую версию пакета SDK, поэтому рекомендуется как можно раньше обновлять пакет SDK до последней версии.</span><span class="sxs-lookup"><span data-stu-id="faa93-213">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span></span>

<span data-ttu-id="faa93-214">Любые запросы к Cosmos DB с помощью выведенного из эксплуатации пакета SDK будут отклонены службой.</span><span class="sxs-lookup"><span data-stu-id="faa93-214">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="faa93-215">Поддержка всех версий пакета SDK DocumentDB для Java версии ниже **1.0.0** будет прекращена **29 февраля 2016 года**.</span><span class="sxs-lookup"><span data-stu-id="faa93-215">All versions of the DocumentDB SDK for Java prior to version **1.0.0** will be retired on **February 29, 2016**.</span></span>
> 
> 

<br/>

| <span data-ttu-id="faa93-216">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="faa93-216">Version</span></span> | <span data-ttu-id="faa93-217">Дата выпуска</span><span class="sxs-lookup"><span data-stu-id="faa93-217">Release Date</span></span> | <span data-ttu-id="faa93-218">Дата вывода</span><span class="sxs-lookup"><span data-stu-id="faa93-218">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="faa93-219">1.12.0</span><span class="sxs-lookup"><span data-stu-id="faa93-219">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="faa93-220">11 июля 2017 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-220">July 11, 2017</span></span> |--- |
| [<span data-ttu-id="faa93-221">1.11.0</span><span class="sxs-lookup"><span data-stu-id="faa93-221">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="faa93-222">10 мая 2017 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-222">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="faa93-223">1.10.0</span><span class="sxs-lookup"><span data-stu-id="faa93-223">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="faa93-224">11 марта 2017 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-224">March 11, 2017</span></span> |--- |
| [<span data-ttu-id="faa93-225">1.9.6</span><span class="sxs-lookup"><span data-stu-id="faa93-225">1.9.6</span></span>](#1.9.6) |<span data-ttu-id="faa93-226">21 февраля 2017 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-226">February 21, 2017</span></span> |--- |
| [<span data-ttu-id="faa93-227">1.9.5</span><span class="sxs-lookup"><span data-stu-id="faa93-227">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="faa93-228">31 января 2017 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-228">January 31, 2017</span></span> |--- |
| [<span data-ttu-id="faa93-229">1.9.4</span><span class="sxs-lookup"><span data-stu-id="faa93-229">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="faa93-230">24 ноября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-230">November 24, 2016</span></span> |--- |
| [<span data-ttu-id="faa93-231">1.9.3</span><span class="sxs-lookup"><span data-stu-id="faa93-231">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="faa93-232">30 октября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-232">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="faa93-233">1.9.2</span><span class="sxs-lookup"><span data-stu-id="faa93-233">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="faa93-234">28 октября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-234">October 28, 2016</span></span> |--- |
| [<span data-ttu-id="faa93-235">1.9.1</span><span class="sxs-lookup"><span data-stu-id="faa93-235">1.9.1</span></span>](#1.9.1) |<span data-ttu-id="faa93-236">26 октября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-236">October 26, 2016</span></span> |--- |
| [<span data-ttu-id="faa93-237">1.9.0</span><span class="sxs-lookup"><span data-stu-id="faa93-237">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="faa93-238">3 октября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-238">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="faa93-239">1.8.1</span><span class="sxs-lookup"><span data-stu-id="faa93-239">1.8.1</span></span>](#1.8.1) |<span data-ttu-id="faa93-240">30 июня 2016 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-240">June 30, 2016</span></span> |--- |
| [<span data-ttu-id="faa93-241">1.8.0</span><span class="sxs-lookup"><span data-stu-id="faa93-241">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="faa93-242">14 июня 2016 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-242">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="faa93-243">1.7.1</span><span class="sxs-lookup"><span data-stu-id="faa93-243">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="faa93-244">30 апреля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-244">April 30, 2016</span></span> |--- |
| [<span data-ttu-id="faa93-245">1.7.0</span><span class="sxs-lookup"><span data-stu-id="faa93-245">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="faa93-246">27 апреля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-246">April 27, 2016</span></span> |--- |
| [<span data-ttu-id="faa93-247">1.6.0</span><span class="sxs-lookup"><span data-stu-id="faa93-247">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="faa93-248">29 марта 2016 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-248">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="faa93-249">1.5.1</span><span class="sxs-lookup"><span data-stu-id="faa93-249">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="faa93-250">31 декабря 2015 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-250">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="faa93-251">1.5.0</span><span class="sxs-lookup"><span data-stu-id="faa93-251">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="faa93-252">4 декабря 2015 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-252">December 04, 2015</span></span> |--- |
| [<span data-ttu-id="faa93-253">1.4.0</span><span class="sxs-lookup"><span data-stu-id="faa93-253">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="faa93-254">5 октября 2015 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-254">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="faa93-255">1.3.0</span><span class="sxs-lookup"><span data-stu-id="faa93-255">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="faa93-256">5 октября 2015 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-256">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="faa93-257">1.2.0</span><span class="sxs-lookup"><span data-stu-id="faa93-257">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="faa93-258">5 августа 2015 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-258">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="faa93-259">1.1.0</span><span class="sxs-lookup"><span data-stu-id="faa93-259">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="faa93-260">9 июля 2015 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-260">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="faa93-261">1.0.1</span><span class="sxs-lookup"><span data-stu-id="faa93-261">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="faa93-262">12 мая 2015 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-262">May 12, 2015</span></span> |--- |
| [<span data-ttu-id="faa93-263">1.0.0</span><span class="sxs-lookup"><span data-stu-id="faa93-263">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="faa93-264">7 апреля 2015 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-264">April 07, 2015</span></span> |--- |
| <span data-ttu-id="faa93-265">0.9.5-prelease</span><span class="sxs-lookup"><span data-stu-id="faa93-265">0.9.5-prelease</span></span> |<span data-ttu-id="faa93-266">9 марта 2015 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-266">Mar 09, 2015</span></span> |<span data-ttu-id="faa93-267">29 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-267">February 29, 2016</span></span> |
| <span data-ttu-id="faa93-268">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="faa93-268">0.9.4-prelease</span></span> |<span data-ttu-id="faa93-269">17 февраля 2015 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-269">February 17, 2015</span></span> |<span data-ttu-id="faa93-270">29 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-270">February 29, 2016</span></span> |
| <span data-ttu-id="faa93-271">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="faa93-271">0.9.3-prelease</span></span> |<span data-ttu-id="faa93-272">13 января 2015 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-272">January 13, 2015</span></span> |<span data-ttu-id="faa93-273">29 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-273">February 29, 2016</span></span> |
| <span data-ttu-id="faa93-274">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="faa93-274">0.9.2-prelease</span></span> |<span data-ttu-id="faa93-275">19 декабря 2014 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-275">December 19, 2014</span></span> |<span data-ttu-id="faa93-276">29 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-276">February 29, 2016</span></span> |
| <span data-ttu-id="faa93-277">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="faa93-277">0.9.1-prelease</span></span> |<span data-ttu-id="faa93-278">19 декабря 2014 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-278">December 19, 2014</span></span> |<span data-ttu-id="faa93-279">29 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-279">February 29, 2016</span></span> |
| <span data-ttu-id="faa93-280">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="faa93-280">0.9.0-prelease</span></span> |<span data-ttu-id="faa93-281">10 декабря 2014 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-281">December 10, 2014</span></span> |<span data-ttu-id="faa93-282">29 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="faa93-282">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="faa93-283">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="faa93-283">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="faa93-284">См. также</span><span class="sxs-lookup"><span data-stu-id="faa93-284">See Also</span></span>
<span data-ttu-id="faa93-285">Дополнительные сведения о Cosmos DB см. на странице службы [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="faa93-285">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

