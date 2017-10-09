---
title: "Azure Cosmos DB: API-интерфейс, пакет SDK Java и материалы для DocumentDB | Microsoft Docs"
description: "Узнайте о hello Java API и пакет SDK, включая даты выхода, даты выбытия и изменения, выполняемые на каждой версии hello Azure Cosmos DB DocumentDB Java SDK."
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
ms.openlocfilehash: 8ef43ebeb7ae1bfc55512c4a7489c1b7930122d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-documentdb-java-sdk-release-notes-and-resources"></a><span data-ttu-id="3c5f4-103">Azure Cosmos DB: заметки о выпуске и материалы по пакету SDK Java для DocumentDB</span><span class="sxs-lookup"><span data-stu-id="3c5f4-103">Azure Cosmos DB: DocumentDB Java SDK release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3c5f4-104">.NET</span><span class="sxs-lookup"><span data-stu-id="3c5f4-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="3c5f4-105">Веб-канал изменений в .NET</span><span class="sxs-lookup"><span data-stu-id="3c5f4-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="3c5f4-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="3c5f4-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="3c5f4-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="3c5f4-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="3c5f4-108">Java</span><span class="sxs-lookup"><span data-stu-id="3c5f4-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="3c5f4-109">Python</span><span class="sxs-lookup"><span data-stu-id="3c5f4-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="3c5f4-110">REST</span><span class="sxs-lookup"><span data-stu-id="3c5f4-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="3c5f4-111">Поставщик ресурсов REST</span><span class="sxs-lookup"><span data-stu-id="3c5f4-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="3c5f4-112">SQL</span><span class="sxs-lookup"><span data-stu-id="3c5f4-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="3c5f4-113">**Скачивание пакета SDK**</span><span class="sxs-lookup"><span data-stu-id="3c5f4-113">**SDK Download**</span></span></td><td>[<span data-ttu-id="3c5f4-114">Maven</span><span class="sxs-lookup"><span data-stu-id="3c5f4-114">Maven</span></span>](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.azure%22%20AND%20a%3A%22azure-documentdb%22)</td></tr>

<tr><td><span data-ttu-id="3c5f4-115">**Документация по API**</span><span class="sxs-lookup"><span data-stu-id="3c5f4-115">**API documentation**</span></span></td><td>[<span data-ttu-id="3c5f4-116">Справочная документация по API Java</span><span class="sxs-lookup"><span data-stu-id="3c5f4-116">Java API reference documentation</span></span>](/java/api/com.microsoft.azure.documentdb)</td></tr>

<tr><td><span data-ttu-id="3c5f4-117">**Contribute tooSDK**</span><span class="sxs-lookup"><span data-stu-id="3c5f4-117">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="3c5f4-118">GitHub</span><span class="sxs-lookup"><span data-stu-id="3c5f4-118">GitHub</span></span>](https://github.com/Azure/azure-documentdb-java/)</td></tr>

<tr><td><span data-ttu-id="3c5f4-119">**Начало работы**</span><span class="sxs-lookup"><span data-stu-id="3c5f4-119">**Get started**</span></span></td><td>[<span data-ttu-id="3c5f4-120">Приступая к работе с hello Java SDK</span><span class="sxs-lookup"><span data-stu-id="3c5f4-120">Get started with hello Java SDK</span></span>](documentdb-java-get-started.md)</td></tr>

<tr><td><span data-ttu-id="3c5f4-121">**Учебник по веб-приложениям**</span><span class="sxs-lookup"><span data-stu-id="3c5f4-121">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="3c5f4-122">Руководство по ASP.NET MVC. Разработка веб-приложений в Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="3c5f4-122">Web application development with Azure Cosmos DB</span></span>](documentdb-java-application.md)</td></tr>

<tr><td><span data-ttu-id="3c5f4-123">**Текущая поддерживаемая среда выполнения**</span><span class="sxs-lookup"><span data-stu-id="3c5f4-123">**Current supported runtime**</span></span></td><td>[<span data-ttu-id="3c5f4-124">JDK 7</span><span class="sxs-lookup"><span data-stu-id="3c5f4-124">JDK 7</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)</td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="3c5f4-125">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="3c5f4-125">Release Notes</span></span>

### <a name="a-name11201120"></a><span data-ttu-id="3c5f4-126"><a name="1.12.0"/>1.12.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-126"><a name="1.12.0"/>1.12.0</span></span>
* <span data-ttu-id="3c5f4-127">Разделяет важные исправления toorequest обработке во время секционирования.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-127">Critical bug fixes toorequest processing during partition splits.</span></span>
* <span data-ttu-id="3c5f4-128">Исправлена проблема со строгим hello и уровни согласованности BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-128">Fixed an issue with hello Strong and BoundedStaleness consistency levels.</span></span>

### <a name="a-name11101110"></a><span data-ttu-id="3c5f4-129"><a name="1.11.0"/>1.11.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-129"><a name="1.11.0"/>1.11.0</span></span>
* <span data-ttu-id="3c5f4-130">Добавлена поддержка нового уровня согласованности с именем ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-130">Added support for a new consistency level called ConsistentPrefix.</span></span>
* <span data-ttu-id="3c5f4-131">Исправлена ошибка чтения коллекции в режиме сеанса.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-131">Fixed a bug in reading collection in session mode.</span></span>

### <a name="a-name11001100"></a><span data-ttu-id="3c5f4-132"><a name="1.10.0"/>1.10.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-132"><a name="1.10.0"/>1.10.0</span></span>
* <span data-ttu-id="3c5f4-133">Включена поддержка секционированных коллекций с производительностью 2500 ЕЗ/с, а также масштабирование с шагом в 100 ЕЗ/с.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-133">Enabled support for partitioned collection with as low as 2,500 RU/sec and scale in increments of 100 RU/sec.</span></span>
* <span data-ttu-id="3c5f4-134">Исправлена ошибка в машинной сборки hello, что может вызвать исключение NullRef в некоторых запросах.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-134">Fixed a bug in hello native assembly which can cause NullRef exception in some queries.</span></span>

### <a name="a-name196196"></a><span data-ttu-id="3c5f4-135"><a name="1.9.6"/>1.9.6</span><span class="sxs-lookup"><span data-stu-id="3c5f4-135"><a name="1.9.6"/>1.9.6</span></span>
* <span data-ttu-id="3c5f4-136">Исправлена ошибка в конфигурации обработчика запросов hello, могут вызвать исключения для запросов в режиме шлюза.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-136">Fixed a bug in hello query engine configuration that may cause exceptions for queries in Gateway mode.</span></span>
* <span data-ttu-id="3c5f4-137">Исправлено несколько ошибок в контейнере hello сеанса, которые могут вызвать исключение «Владелец ресурс не найден» для запросов сразу после создания коллекции.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-137">Fixed a few bugs in hello session container that may cause an "Owner resource not found" exception for requests immediately after collection creation.</span></span>

### <a name="a-name195195"></a><span data-ttu-id="3c5f4-138"><a name="1.9.5"/>1.9.5</span><span class="sxs-lookup"><span data-stu-id="3c5f4-138"><a name="1.9.5"/>1.9.5</span></span>
* <span data-ttu-id="3c5f4-139">Добавлена поддержка статистических запросов (COUNT, MIN, MAX, SUM и AVG).</span><span class="sxs-lookup"><span data-stu-id="3c5f4-139">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span> <span data-ttu-id="3c5f4-140">Дополнительные сведения см. в разделе [Статистические функции](documentdb-sql-query.md#Aggregates).</span><span class="sxs-lookup"><span data-stu-id="3c5f4-140">See [Aggregation support](documentdb-sql-query.md#Aggregates).</span></span>
* <span data-ttu-id="3c5f4-141">Добавлена поддержка веб-канала изменений.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-141">Added support for change feed.</span></span>
* <span data-ttu-id="3c5f4-142">Добавлена поддержка сведений о квотах коллекций посредством RequestOptions.setPopulateQuotaInfo.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-142">Added support for collection quota information through RequestOptions.setPopulateQuotaInfo.</span></span>
* <span data-ttu-id="3c5f4-143">Добавлена поддержка ведения журнала сценариев хранимых процедур посредством RequestOptions.setScriptLoggingEnabled.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-143">Added support for stored procedure script logging through RequestOptions.setScriptLoggingEnabled.</span></span>
* <span data-ttu-id="3c5f4-144">Исправлена ошибка, из-за которой запросы в режиме DirectHttps переставали отвечать при обнаружении ошибок регулирования.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-144">Fixed a bug where query in DirectHttps mode may hang when encountering throttle failures.</span></span>
* <span data-ttu-id="3c5f4-145">Исправлена ошибка в режиме согласованности сеанса.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-145">Fixed a bug in session consistency mode.</span></span>
* <span data-ttu-id="3c5f4-146">Исправлена ошибка, которая могла приводить к порождению исключения NullReferenceException в HttpContext при высокой частоте запросов.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-146">Fixed a bug which may cause NullReferenceException in HttpContext when request rate is high.</span></span>
* <span data-ttu-id="3c5f4-147">Повышена производительность режима DirectHttps.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-147">Improved performance of DirectHttps mode.</span></span>

### <a name="a-name194194"></a><span data-ttu-id="3c5f4-148"><a name="1.9.4"/>1.9.4</span><span class="sxs-lookup"><span data-stu-id="3c5f4-148"><a name="1.9.4"/>1.9.4</span></span>
* <span data-ttu-id="3c5f4-149">Добавлена поддержка прокси-сервера на основе экземпляра простого клиента с помощью API ConnectionPolicy.setProxy().</span><span class="sxs-lookup"><span data-stu-id="3c5f4-149">Added simple client instance-based proxy support with ConnectionPolicy.setProxy() API.</span></span>
* <span data-ttu-id="3c5f4-150">Добавлены DocumentClient.close() API tooproperly завершить работу DocumentClient экземпляра.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-150">Added DocumentClient.close() API tooproperly shutdown DocumentClient instance.</span></span>
* <span data-ttu-id="3c5f4-151">Увеличения производительности запросов в режиме прямой связи осуществляется на основе плана запроса hello hello сборки в машинном коде вместо hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-151">Improved query performance in direct connectivity mode by deriving hello query plan from hello native assembly instead of hello Gateway.</span></span>
* <span data-ttu-id="3c5f4-152">Задать FAIL_ON_UNKNOWN_PROPERTIES = false, поэтому пользователи не должны toodefine JsonIgnoreProperties в их POJO.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-152">Set FAIL_ON_UNKNOWN_PROPERTIES = false so users don't need toodefine JsonIgnoreProperties in their POJO.</span></span>
* <span data-ttu-id="3c5f4-153">Рефакторинг ведения журнала toouse SLF4J.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-153">Refactored logging toouse SLF4J.</span></span>
* <span data-ttu-id="3c5f4-154">Исправлено несколько ошибок в модуле чтения данных согласованности.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-154">Fixed a few other bugs in consistency reader.</span></span>

### <a name="a-name193193"></a><span data-ttu-id="3c5f4-155"><a name="1.9.3"/>1.9.3</span><span class="sxs-lookup"><span data-stu-id="3c5f4-155"><a name="1.9.3"/>1.9.3</span></span>
* <span data-ttu-id="3c5f4-156">Исправлена ошибка утечки hello подключения управления tooprevent соединение в режиме прямого подключения.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-156">Fixed a bug in hello connection management tooprevent connection leaks in direct connectivity mode.</span></span>
* <span data-ttu-id="3c5f4-157">Исправлена ошибка запроса TOP hello где он может вызвать исключение NullReferenece.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-157">Fixed a bug in hello TOP query where it may throw NullReferenece exception.</span></span>
* <span data-ttu-id="3c5f4-158">Повышенная производительность за счет сокращения числа hello для внутренних кэшей hello вызова по сети.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-158">Improved performance by reducing hello number of network call for hello internal caches.</span></span>
* <span data-ttu-id="3c5f4-159">В DocumentClientException добавлены код состояния, ActivityID и универсальный код ресурса (URI) для более удобного устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-159">Added status code, ActivityID and Request URI in DocumentClientException for better troubleshooting.</span></span>

### <a name="a-name192192"></a><span data-ttu-id="3c5f4-160"><a name="1.9.2"/>1.9.2</span><span class="sxs-lookup"><span data-stu-id="3c5f4-160"><a name="1.9.2"/>1.9.2</span></span>
* <span data-ttu-id="3c5f4-161">Устранена проблема в управлении подключениями hello для стабильности.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-161">Fixed an issue in hello connection management for stability.</span></span>

### <a name="a-name191191"></a><span data-ttu-id="3c5f4-162"><a name="1.9.1"/>1.9.1</span><span class="sxs-lookup"><span data-stu-id="3c5f4-162"><a name="1.9.1"/>1.9.1</span></span>
* <span data-ttu-id="3c5f4-163">Добавлена поддержка уровня согласованности BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-163">Added support for BoundedStaleness consistency level.</span></span>
* <span data-ttu-id="3c5f4-164">Добавлена поддержка прямого подключения для операций CRUD с секционированными коллекциями.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-164">Added support for direct connectivity for CRUD operations for partitioned collections.</span></span>
* <span data-ttu-id="3c5f4-165">Исправлена ошибка, возникающая при выполнении запросов к базе данных с помощью SQL.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-165">Fixed a bug in querying a database with SQL.</span></span>
* <span data-ttu-id="3c5f4-166">Исправлена ошибка в кэше сеанса hello, где маркер сеанса могут быть установлены неправильно.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-166">Fixed a bug in hello session cache where session token may be set incorrectly.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="3c5f4-167"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-167"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="3c5f4-168">Добавлена поддержка параллельных запросов между секциями.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-168">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="3c5f4-169">Добавлена поддержка запросов TOP и ORDER BY для секционированных коллекций.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-169">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>
* <span data-ttu-id="3c5f4-170">Добавлена поддержка строгой согласованности.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-170">Added support for strong consistency.</span></span>
* <span data-ttu-id="3c5f4-171">Добавлена поддержка запросов по имени при использовании прямого подключения.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-171">Added support for name based requests when using direct connectivity.</span></span>
* <span data-ttu-id="3c5f4-172">Фиксированный toomake ActivityId остаются согласованными по всем попыткам запроса.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-172">Fixed toomake ActivityId stay consistent across all request retries.</span></span>
* <span data-ttu-id="3c5f4-173">Исправлена ошибка, связанные с toohello кэш сеанса при повторном коллекции hello таким же именем.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-173">Fixed a bug related toohello session cache when recreating a collection with hello same name.</span></span>
* <span data-ttu-id="3c5f4-174">Добавлены типы данных Polygon и LineString и задана политика индексирования коллекций для запросов пространственных геозон.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-174">Added Polygon and LineString DataTypes while specifying collection indexing policy for geo-fencing spatial queries.</span></span>
* <span data-ttu-id="3c5f4-175">Устранены проблемы с JavaDoc для Java 1.8.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-175">Fixed issues with Java Doc for Java 1.8.</span></span>

### <a name="a-name181181"></a><span data-ttu-id="3c5f4-176"><a name="1.8.1"/>1.8.1</span><span class="sxs-lookup"><span data-stu-id="3c5f4-176"><a name="1.8.1"/>1.8.1</span></span>
* <span data-ttu-id="3c5f4-177">Исправлена ошибка в PartitionKeyDefinitionMap toocache коллекции с одной секцией и не делать дополнительные выборки секции ключа запросов.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-177">Fixed a bug in PartitionKeyDefinitionMap toocache single partition collections and not make extra fetch partition key requests.</span></span>
* <span data-ttu-id="3c5f4-178">Фиксированной повторная попытка toonot ошибки, если предоставлен неверный ключом раздела.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-178">Fixed a bug toonot retry when an incorrect partition key value is provided.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="3c5f4-179"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-179"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="3c5f4-180">Hello добавлена поддержка учетные записи базы данных с поддержкой нескольких регионов.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-180">Added hello support for multi-region database accounts.</span></span>
* <span data-ttu-id="3c5f4-181">Добавлена поддержка автоматического повтора на регулируемые запросы с max hello toocustomize параметры повторные попытки и максимальная длина время ожидания повтора.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-181">Added support for automatic retry on throttled requests with options toocustomize hello max retry attempts and max retry wait time.</span></span>  <span data-ttu-id="3c5f4-182">Ознакомьтесь с RetryOptions и ConnectionPolicy.getRetryOptions().</span><span class="sxs-lookup"><span data-stu-id="3c5f4-182">See RetryOptions and ConnectionPolicy.getRetryOptions().</span></span>
* <span data-ttu-id="3c5f4-183">Не рекомендуется использовать IPartitionResolver на основе пользовательского кода секционирования.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-183">Deprecated IPartitionResolver based custom partitioning code.</span></span> <span data-ttu-id="3c5f4-184">Используйте секционированные коллекции, чтобы увеличить возможности хранилища и пропускную способность.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-184">Please use partitioned collections for higher storage and throughput.</span></span>

### <a name="a-name171171"></a><span data-ttu-id="3c5f4-185"><a name="1.7.1"/>1.7.1</span><span class="sxs-lookup"><span data-stu-id="3c5f4-185"><a name="1.7.1"/>1.7.1</span></span>
* <span data-ttu-id="3c5f4-186">Добавлена поддержка политики повтора для регулирования.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-186">Added retry policy support for throttling.</span></span>  

### <a name="a-name170170"></a><span data-ttu-id="3c5f4-187"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-187"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="3c5f4-188">Добавлена поддержка toolive (TTL) время для документов.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-188">Added time toolive (TTL) support for documents.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="3c5f4-189"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-189"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="3c5f4-190">Реализованы [секционированные коллекции](partition-data.md) и [определяемые пользователем уровни производительности](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="3c5f4-190">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <a name="a-name151151"></a><span data-ttu-id="3c5f4-191"><a name="1.5.1"/>1.5.1</span><span class="sxs-lookup"><span data-stu-id="3c5f4-191"><a name="1.5.1"/>1.5.1</span></span>
* <span data-ttu-id="3c5f4-192">Исправлена ошибка в HashPartitionResolver toogenerate хэш-значения в прямом toobe согласуется с других пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-192">Fixed a bug in HashPartitionResolver toogenerate hash values in little-endian toobe consistent with other SDKs.</span></span>

### <a name="a-name150150"></a><span data-ttu-id="3c5f4-193"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-193"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="3c5f4-194">Добавить диапазон & хеширования tooassist распознаватели секции с приложениями сегментирования по нескольким секциям.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-194">Add Hash & Range partition resolvers tooassist with sharding applications across multiple partitions.</span></span>

### <a name="a-name140140"></a><span data-ttu-id="3c5f4-195"><a name="1.4.0"/>1.4.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-195"><a name="1.4.0"/>1.4.0</span></span>
* <span data-ttu-id="3c5f4-196">Реализована операция Upsert.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-196">Implement Upsert.</span></span> <span data-ttu-id="3c5f4-197">Новые методы upsertXXX добавлена функция toosupport Upsert.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-197">New upsertXXX methods added toosupport Upsert feature.</span></span>
* <span data-ttu-id="3c5f4-198">Реализована маршрутизация на основе идентификатора.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-198">Implement ID Based Routing.</span></span> <span data-ttu-id="3c5f4-199">Отсутствуют изменения общего API-интерфейса. Все изменения касаются внутреннего интерфейса.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-199">No public API changes, all changes internal.</span></span>

### <a name="a-name130130"></a><span data-ttu-id="3c5f4-200"><a name="1.3.0"/>1.3.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-200"><a name="1.3.0"/>1.3.0</span></span>
* <span data-ttu-id="3c5f4-201">Выпуск пропущено toobring номер версии, согласованные с других пакетов SDK</span><span class="sxs-lookup"><span data-stu-id="3c5f4-201">Release skipped toobring version number in alignment with other SDKs</span></span>

### <a name="a-name120120"></a><span data-ttu-id="3c5f4-202"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-202"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="3c5f4-203">Поддержка геопространственного индекса</span><span class="sxs-lookup"><span data-stu-id="3c5f4-203">Supports GeoSpatial Index</span></span>
* <span data-ttu-id="3c5f4-204">Проверка свойств идентификатора для всех ресурсов.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-204">Validates id property for all resources.</span></span> <span data-ttu-id="3c5f4-205">Идентификаторы ресурсов не могут содержать знаки ?, /, #, \, или заканчиваться пробелом.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-205">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="3c5f4-206">Добавляет новый tooResourceResponse заголовок «выполняется преобразование индекса».</span><span class="sxs-lookup"><span data-stu-id="3c5f4-206">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="3c5f4-207"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-207"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="3c5f4-208">Реализована политика индексации версии 2.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-208">Implements V2 indexing policy</span></span>

### <a name="a-name100100"></a><span data-ttu-id="3c5f4-209"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-209"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="3c5f4-210">Пакет SDK общей доступности.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-210">GA SDK</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="3c5f4-211">Даты выпуска и выбытия</span><span class="sxs-lookup"><span data-stu-id="3c5f4-211">Release & Retirement Dates</span></span>
<span data-ttu-id="3c5f4-212">Корпорация Майкрософт предоставляет уведомления по крайней мере **12 месяцев** до снятия с учета в новой/поддерживаемой версии для hello перехода порядок toosmooth tooa пакет SDK.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-212">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="3c5f4-213">Новые функции и функциональные возможности и оптимизацию добавляются только toohello текущего пакета SDK, поэтому рекомендуется как можно раньше, вы всегда обновления toohello последнюю версию пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-213">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommend that you always upgrade toohello latest SDK version as early as possible.</span></span>

<span data-ttu-id="3c5f4-214">Любой запрос tooCosmos базу данных, используя удалено SDK будут отклонены службой hello.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-214">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="3c5f4-215">Все версии hello DocumentDB SDK для Java предыдущих tooversion **1.0.0** будет удалено на **29 февраля 2016 г.**.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-215">All versions of hello DocumentDB SDK for Java prior tooversion **1.0.0** will be retired on **February 29, 2016**.</span></span>
> 
> 

<br/>

| <span data-ttu-id="3c5f4-216">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="3c5f4-216">Version</span></span> | <span data-ttu-id="3c5f4-217">Дата выпуска</span><span class="sxs-lookup"><span data-stu-id="3c5f4-217">Release Date</span></span> | <span data-ttu-id="3c5f4-218">Дата вывода</span><span class="sxs-lookup"><span data-stu-id="3c5f4-218">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="3c5f4-219">1.12.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-219">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="3c5f4-220">11 июля 2017 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-220">July 11, 2017</span></span> |--- |
| [<span data-ttu-id="3c5f4-221">1.11.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-221">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="3c5f4-222">10 мая 2017 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-222">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="3c5f4-223">1.10.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-223">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="3c5f4-224">11 марта 2017 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-224">March 11, 2017</span></span> |--- |
| [<span data-ttu-id="3c5f4-225">1.9.6</span><span class="sxs-lookup"><span data-stu-id="3c5f4-225">1.9.6</span></span>](#1.9.6) |<span data-ttu-id="3c5f4-226">21 февраля 2017 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-226">February 21, 2017</span></span> |--- |
| [<span data-ttu-id="3c5f4-227">1.9.5</span><span class="sxs-lookup"><span data-stu-id="3c5f4-227">1.9.5</span></span>](#1.9.5) |<span data-ttu-id="3c5f4-228">31 января 2017 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-228">January 31, 2017</span></span> |--- |
| [<span data-ttu-id="3c5f4-229">1.9.4</span><span class="sxs-lookup"><span data-stu-id="3c5f4-229">1.9.4</span></span>](#1.9.4) |<span data-ttu-id="3c5f4-230">24 ноября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-230">November 24, 2016</span></span> |--- |
| [<span data-ttu-id="3c5f4-231">1.9.3</span><span class="sxs-lookup"><span data-stu-id="3c5f4-231">1.9.3</span></span>](#1.9.3) |<span data-ttu-id="3c5f4-232">30 октября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-232">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="3c5f4-233">1.9.2</span><span class="sxs-lookup"><span data-stu-id="3c5f4-233">1.9.2</span></span>](#1.9.2) |<span data-ttu-id="3c5f4-234">28 октября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-234">October 28, 2016</span></span> |--- |
| [<span data-ttu-id="3c5f4-235">1.9.1</span><span class="sxs-lookup"><span data-stu-id="3c5f4-235">1.9.1</span></span>](#1.9.1) |<span data-ttu-id="3c5f4-236">26 октября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-236">October 26, 2016</span></span> |--- |
| [<span data-ttu-id="3c5f4-237">1.9.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-237">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="3c5f4-238">3 октября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-238">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="3c5f4-239">1.8.1</span><span class="sxs-lookup"><span data-stu-id="3c5f4-239">1.8.1</span></span>](#1.8.1) |<span data-ttu-id="3c5f4-240">30 июня 2016 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-240">June 30, 2016</span></span> |--- |
| [<span data-ttu-id="3c5f4-241">1.8.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-241">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="3c5f4-242">14 июня 2016 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-242">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="3c5f4-243">1.7.1</span><span class="sxs-lookup"><span data-stu-id="3c5f4-243">1.7.1</span></span>](#1.7.1) |<span data-ttu-id="3c5f4-244">30 апреля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-244">April 30, 2016</span></span> |--- |
| [<span data-ttu-id="3c5f4-245">1.7.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-245">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="3c5f4-246">27 апреля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-246">April 27, 2016</span></span> |--- |
| [<span data-ttu-id="3c5f4-247">1.6.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-247">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="3c5f4-248">29 марта 2016 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-248">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="3c5f4-249">1.5.1</span><span class="sxs-lookup"><span data-stu-id="3c5f4-249">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="3c5f4-250">31 декабря 2015 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-250">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="3c5f4-251">1.5.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-251">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="3c5f4-252">4 декабря 2015 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-252">December 04, 2015</span></span> |--- |
| [<span data-ttu-id="3c5f4-253">1.4.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-253">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="3c5f4-254">5 октября 2015 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-254">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="3c5f4-255">1.3.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-255">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="3c5f4-256">5 октября 2015 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-256">October 05, 2015</span></span> |--- |
| [<span data-ttu-id="3c5f4-257">1.2.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-257">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="3c5f4-258">5 августа 2015 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-258">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="3c5f4-259">1.1.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-259">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="3c5f4-260">9 июля 2015 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-260">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="3c5f4-261">1.0.1</span><span class="sxs-lookup"><span data-stu-id="3c5f4-261">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="3c5f4-262">12 мая 2015 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-262">May 12, 2015</span></span> |--- |
| [<span data-ttu-id="3c5f4-263">1.0.0</span><span class="sxs-lookup"><span data-stu-id="3c5f4-263">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="3c5f4-264">7 апреля 2015 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-264">April 07, 2015</span></span> |--- |
| <span data-ttu-id="3c5f4-265">0.9.5-prelease</span><span class="sxs-lookup"><span data-stu-id="3c5f4-265">0.9.5-prelease</span></span> |<span data-ttu-id="3c5f4-266">9 марта 2015 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-266">Mar 09, 2015</span></span> |<span data-ttu-id="3c5f4-267">29 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-267">February 29, 2016</span></span> |
| <span data-ttu-id="3c5f4-268">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="3c5f4-268">0.9.4-prelease</span></span> |<span data-ttu-id="3c5f4-269">17 февраля 2015 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-269">February 17, 2015</span></span> |<span data-ttu-id="3c5f4-270">29 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-270">February 29, 2016</span></span> |
| <span data-ttu-id="3c5f4-271">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="3c5f4-271">0.9.3-prelease</span></span> |<span data-ttu-id="3c5f4-272">13 января 2015 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-272">January 13, 2015</span></span> |<span data-ttu-id="3c5f4-273">29 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-273">February 29, 2016</span></span> |
| <span data-ttu-id="3c5f4-274">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="3c5f4-274">0.9.2-prelease</span></span> |<span data-ttu-id="3c5f4-275">19 декабря 2014 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-275">December 19, 2014</span></span> |<span data-ttu-id="3c5f4-276">29 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-276">February 29, 2016</span></span> |
| <span data-ttu-id="3c5f4-277">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="3c5f4-277">0.9.1-prelease</span></span> |<span data-ttu-id="3c5f4-278">19 декабря 2014 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-278">December 19, 2014</span></span> |<span data-ttu-id="3c5f4-279">29 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-279">February 29, 2016</span></span> |
| <span data-ttu-id="3c5f4-280">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="3c5f4-280">0.9.0-prelease</span></span> |<span data-ttu-id="3c5f4-281">10 декабря 2014 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-281">December 10, 2014</span></span> |<span data-ttu-id="3c5f4-282">29 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-282">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="3c5f4-283">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="3c5f4-283">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="3c5f4-284">См. также</span><span class="sxs-lookup"><span data-stu-id="3c5f4-284">See Also</span></span>
<span data-ttu-id="3c5f4-285">toolearn Дополнительные сведения о Cosmos DB. в разделе [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) страницы службы.</span><span class="sxs-lookup"><span data-stu-id="3c5f4-285">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

