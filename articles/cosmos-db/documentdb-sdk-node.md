---
title: "aaaAzure Cosmos DB Node.js API, пакет SDK ре & сурсов | Документы Microsoft"
description: "Узнайте о hello Node.js API и пакет SDK, включая даты выхода, даты выбытия и изменения, выполняемые на каждой версии пакета SDK для Node.js DB Cosmos Azure hello."
services: cosmos-db
documentationcenter: nodejs
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 9d5621fa-0e11-4619-a28b-a19d872bcf37
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d450b9a9ea7b0f4717ddae8940121fc458ea3744
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a><span data-ttu-id="ee0c5-103">Пакет SDK Node.js для Azure Cosmos DB: заметки о выпуске и ресурсы</span><span class="sxs-lookup"><span data-stu-id="ee0c5-103">Azure Cosmos DB Node.js SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ee0c5-104">.NET</span><span class="sxs-lookup"><span data-stu-id="ee0c5-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="ee0c5-105">Веб-канал изменений в .NET</span><span class="sxs-lookup"><span data-stu-id="ee0c5-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="ee0c5-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="ee0c5-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="ee0c5-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="ee0c5-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="ee0c5-108">Java</span><span class="sxs-lookup"><span data-stu-id="ee0c5-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="ee0c5-109">Python</span><span class="sxs-lookup"><span data-stu-id="ee0c5-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="ee0c5-110">REST</span><span class="sxs-lookup"><span data-stu-id="ee0c5-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="ee0c5-111">Поставщик ресурсов REST</span><span class="sxs-lookup"><span data-stu-id="ee0c5-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="ee0c5-112">SQL</span><span class="sxs-lookup"><span data-stu-id="ee0c5-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="ee0c5-113">**Скачать пакет SDK**</span><span class="sxs-lookup"><span data-stu-id="ee0c5-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="ee0c5-114">NPM</span><span class="sxs-lookup"><span data-stu-id="ee0c5-114">NPM</span></span>](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td><span data-ttu-id="ee0c5-115">**Документация по API**</span><span class="sxs-lookup"><span data-stu-id="ee0c5-115">**API documentation**</span></span></td><td>[<span data-ttu-id="ee0c5-116">Справочная документация по API Node.js</span><span class="sxs-lookup"><span data-stu-id="ee0c5-116">Node.js API reference documentation</span></span>](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td><span data-ttu-id="ee0c5-117">**Инструкции по установке пакета SDK**</span><span class="sxs-lookup"><span data-stu-id="ee0c5-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="ee0c5-118">Инструкции по установке</span><span class="sxs-lookup"><span data-stu-id="ee0c5-118">Installation instructions</span></span>](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td><span data-ttu-id="ee0c5-119">**Contribute tooSDK**</span><span class="sxs-lookup"><span data-stu-id="ee0c5-119">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="ee0c5-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="ee0c5-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td><span data-ttu-id="ee0c5-121">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="ee0c5-121">**Samples**</span></span></td><td>[<span data-ttu-id="ee0c5-122">Примеры кода Node.js</span><span class="sxs-lookup"><span data-stu-id="ee0c5-122">Node.js code samples</span></span>](documentdb-nodejs-samples.md)</td></tr>

<tr><td><span data-ttu-id="ee0c5-123">**Учебник по началу работы**</span><span class="sxs-lookup"><span data-stu-id="ee0c5-123">**Get started tutorial**</span></span></td><td>[<span data-ttu-id="ee0c5-124">Приступая к работе с hello пакет SDK для Node.js</span><span class="sxs-lookup"><span data-stu-id="ee0c5-124">Get started with hello Node.js SDK</span></span>](documentdb-nodejs-get-started.md)</td></tr>

<tr><td><span data-ttu-id="ee0c5-125">**Учебник по веб-приложениям**</span><span class="sxs-lookup"><span data-stu-id="ee0c5-125">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="ee0c5-126">Создание веб-приложения Node.js с использованием Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="ee0c5-126">Build a Node.js web application using Azure Cosmos DB</span></span>](documentdb-nodejs-application.md)</td></tr>

<tr><td><span data-ttu-id="ee0c5-127">**Текущая поддерживаемая платформа**</span><span class="sxs-lookup"><span data-stu-id="ee0c5-127">**Current supported platform**</span></span></td><td> 
[<span data-ttu-id="ee0c5-128">Node.js v6.x</span><span class="sxs-lookup"><span data-stu-id="ee0c5-128">Node.js v6.x</span></span>](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[<span data-ttu-id="ee0c5-129">Node.js версии 4.2.0</span><span class="sxs-lookup"><span data-stu-id="ee0c5-129">Node.js v4.2.0</span></span>](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[<span data-ttu-id="ee0c5-130">Node.js версии 0.12</span><span class="sxs-lookup"><span data-stu-id="ee0c5-130">Node.js v0.12</span></span>](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
<span data-ttu-id="ee0c5-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span><span class="sxs-lookup"><span data-stu-id="ee0c5-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="ee0c5-132">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="ee0c5-132">Release notes</span></span>

### <span data-ttu-id="ee0c5-133"><a name="1.12.2"/>1.12.2</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-133"><a name="1.12.2"/>1.12.2</a></span></span>
*   <span data-ttu-id="ee0c5-134">Исправлена документация npm.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-134">npm documentation fixed.</span></span>

### <span data-ttu-id="ee0c5-135"><a name="1.12.1"/>1.12.1</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-135"><a name="1.12.1"/>1.12.1</a></span></span>
* <span data-ttu-id="ee0c5-136">Исправлена ошибка в executeStoredProcedure, где документы содержали специальные символы Юникода (LS, PS).</span><span class="sxs-lookup"><span data-stu-id="ee0c5-136">Fixed a bug in executeStoredProcedure where documents involved had special Unicode characters (LS, PS).</span></span>
* <span data-ttu-id="ee0c5-137">Исправлена ошибка при обработке документов с использованием символов Юникода в ключ раздела hello.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-137">Fixed a bug in handling documents with Unicode characters in hello partition key.</span></span>
* <span data-ttu-id="ee0c5-138">Фиксированный поддержку для создания коллекций с hello имя носителя.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-138">Fixed support for creating collections with hello name media.</span></span> <span data-ttu-id="ee0c5-139">Проблема GitHub 114.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-139">Github issue #114.</span></span>
* <span data-ttu-id="ee0c5-140">Исправлена поддержка маркера авторизации разрешений.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-140">Fixed support for permission authorization token.</span></span> <span data-ttu-id="ee0c5-141">Проблема GitHub 178.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-141">Github issue #178.</span></span>

### <span data-ttu-id="ee0c5-142"><a name="1.12.0"/>1.12.0</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-142"><a name="1.12.0"/>1.12.0</a></span></span>
* <span data-ttu-id="ee0c5-143">Добавлена поддержка нового [уровня согласованности](consistency-levels.md) с именем ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-143">Added support for a new [consistency level](consistency-levels.md) called ConsistentPrefix.</span></span>
* <span data-ttu-id="ee0c5-144">Добавлена поддержка UriFactory.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-144">Added support for UriFactory.</span></span>
* <span data-ttu-id="ee0c5-145">Исправлена ошибка поддержки Юникода.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-145">Fixed a Unicode support bug.</span></span> <span data-ttu-id="ee0c5-146">Проблема GitHub 171.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-146">GitHub issue #171.</span></span>

### <span data-ttu-id="ee0c5-147"><a name="1.11.0"/>1.11.0</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-147"><a name="1.11.0"/>1.11.0</a></span></span>
* <span data-ttu-id="ee0c5-148">Hello добавлена поддержка статистических запросов (COUNT, MIN, MAX, SUM и AVG).</span><span class="sxs-lookup"><span data-stu-id="ee0c5-148">Added hello support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="ee0c5-149">Добавлены hello режим управления степень параллелизма для кросс-запросы секций.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-149">Added hello option for controlling degree of parallelism for cross partition queries.</span></span>
* <span data-ttu-id="ee0c5-150">Hello добавлен параметр для отключения проверки SSL при работе с Azure Cosmos DB эмулятора.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-150">Added hello option for disabling SSL verification when running against Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="ee0c5-151">Понижено минимальная пропускная способность для секционированных коллекций из 10,100 единиц Запросов в секунду too2500 единиц Запросов в секунду.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-151">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>
* <span data-ttu-id="ee0c5-152">Фиксированный hello продолжение токена ошибки для коллекции одну секцию.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-152">Fixed hello continuation token bug for single partition collection.</span></span> <span data-ttu-id="ee0c5-153">Проблема GitHub 107.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-153">Github issue #107.</span></span>
* <span data-ttu-id="ee0c5-154">Ошибка executeStoredProcedure основных hello в обработке 0 как один параметр.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-154">Fixed hello executeStoredProcedure bug in handling 0 as single param.</span></span> <span data-ttu-id="ee0c5-155">Проблема GitHub 155.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-155">Github issue #155.</span></span>

### <span data-ttu-id="ee0c5-156"><a name="1.10.2"/>1.10.2</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-156"><a name="1.10.2"/>1.10.2</a></span></span>
* <span data-ttu-id="ee0c5-157">Версия пакета SDK hello tooinclude заголовок основных агента пользователя.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-157">Fixed user-agent header tooinclude hello SDK version.</span></span>
* <span data-ttu-id="ee0c5-158">Дополнительная очистка кода.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-158">Minor code cleanup.</span></span>

### <span data-ttu-id="ee0c5-159"><a name="1.10.1"/>1.10.1</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-159"><a name="1.10.1"/>1.10.1</a></span></span>
* <span data-ttu-id="ee0c5-160">Отключение проверки SSL, при использовании hello SDK tootarget hello emulator(hostname=localhost).</span><span class="sxs-lookup"><span data-stu-id="ee0c5-160">Disabling SSL verification when using hello SDK tootarget hello emulator(hostname=localhost).</span></span>
* <span data-ttu-id="ee0c5-161">Добавлена поддержка включения ведения журнала сценариев во время выполнения хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-161">Added support for enabling script logging during stored procedure execution.</span></span>

### <span data-ttu-id="ee0c5-162"><a name="1.10.0"/>1.10.0</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-162"><a name="1.10.0"/>1.10.0</a></span></span>
* <span data-ttu-id="ee0c5-163">Добавлена поддержка параллельных запросов между секциями.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-163">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="ee0c5-164">Добавлена поддержка запросов TOP и ORDER BY для секционированных коллекций.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-164">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>

### <span data-ttu-id="ee0c5-165"><a name="1.9.0"/>1.9.0</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-165"><a name="1.9.0"/>1.9.0</a></span></span>
* <span data-ttu-id="ee0c5-166">Добавлена поддержка политики повтора для отрегулированных запросов.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-166">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="ee0c5-167">(Отрегулированные запросы порождают исключение слишком высокой частоты запросов с кодом ошибки 429.) По умолчанию Azure Cosmos DB повторяет девяти раз для каждого запроса при обнаружении код ошибки 429, учитывая время retryAfter hello в заголовке ответа hello.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-167">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring hello retryAfter time in hello response header.</span></span> <span data-ttu-id="ee0c5-168">Интервал повторных попыток основных теперь настраивается как часть hello свойство RetryOptions hello объекта ConnectionPolicy время tooignore hello retryAfter сервер вернул между повторными попытками hello.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-168">A fixed retry interval time can now be set as part of hello RetryOptions property on hello ConnectionPolicy object if you want tooignore hello retryAfter time returned by server between hello retries.</span></span> <span data-ttu-id="ee0c5-169">Теперь Azure Cosmos DB ожидает в течение не более 30 секунд для каждого запроса, который регулируется (независимо от того, число повторных попыток) и возвращает hello ответ с кодом ошибки 429.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-169">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns hello response with error code 429.</span></span> <span data-ttu-id="ee0c5-170">Это время также могут переопределяться в hello RetryOptions свойство ConnectionPolicy объекта.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-170">This time can also be overridden in hello RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="ee0c5-171">Cosmos DB теперь возвращает x-ms регулирования число повторных попыток и x-ms-throttle-retry-wait-time-ms как заголовки ответа hello в каждый интервал повтора запроса toodenote hello count и hello совокупное время повтора запроса hello ожидания между повторными попытками hello.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-171">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as hello response headers in every request toodenote hello throttle retry count and hello cumulative time hello request waited between hello retries.</span></span>
* <span data-ttu-id="ee0c5-172">был добавлен класс RetryOptions Hello, предоставление доступа к свойству RetryOptions hello hello ConnectionPolicy класса, который может быть используется toooverride некоторые по умолчанию hello параметры повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-172">hello RetryOptions class was added, exposing hello RetryOptions property on hello ConnectionPolicy class that can be used toooverride some of hello default retry options.</span></span>

### <span data-ttu-id="ee0c5-173"><a name="1.8.0"/>1.8.0</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-173"><a name="1.8.0"/>1.8.0</a></span></span>
* <span data-ttu-id="ee0c5-174">Hello добавлена поддержка учетные записи базы данных с поддержкой нескольких регионов.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-174">Added hello support for multi-region database accounts.</span></span>

### <span data-ttu-id="ee0c5-175"><a name="1.7.0"/>1.7.0</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-175"><a name="1.7.0"/>1.7.0</a></span></span>
* <span data-ttu-id="ee0c5-176">Hello добавлена поддержка функция tooLive(TTL) времени для документов.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-176">Added hello support for Time tooLive(TTL) feature for documents.</span></span>

### <span data-ttu-id="ee0c5-177"><a name="1.6.0"/>1.6.0</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-177"><a name="1.6.0"/>1.6.0</a></span></span>
* <span data-ttu-id="ee0c5-178">Реализованы [секционированные коллекции](partition-data.md) и [определяемые пользователем уровни производительности](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="ee0c5-178">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <span data-ttu-id="ee0c5-179"><a name="1.5.6"/>1.5.6</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-179"><a name="1.5.6"/>1.5.6</a></span></span>
* <span data-ttu-id="ee0c5-180">Исправлена ошибка RangePartitionResolver.resolveForRead, где он не возвращали ссылки из-за поврежденных concat tooa результатов.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-180">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due tooa bad concat of results.</span></span>

### <span data-ttu-id="ee0c5-181"><a name="1.5.5"/>1.5.5</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-181"><a name="1.5.5"/>1.5.5</a></span></span>
* <span data-ttu-id="ee0c5-182">Исправлена ошибка метода resolveForRead() hashParitionResolver. Ранее вместо возврата списка всех зарегистрированных ссылок при отсутствии ключа раздела вызвалось исключение.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-182">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span></span>

### <span data-ttu-id="ee0c5-183"><a name="1.5.4"/>1.5.4</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-183"><a name="1.5.4"/>1.5.4</a></span></span>
* <span data-ttu-id="ee0c5-184">Устраняет проблему, [#100](https://github.com/Azure/azure-documentdb-node/issues/100) -выделенной агента HTTPS: избегать изменения глобального агента hello целях Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-184">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying hello global agent for Azure Cosmos DB purposes.</span></span> <span data-ttu-id="ee0c5-185">Используйте выделенный агента для всех запросов hello lib.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-185">Use a dedicated agent for all of hello lib’s requests.</span></span>

### <span data-ttu-id="ee0c5-186"><a name="1.5.3"/>1.5.3</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-186"><a name="1.5.3"/>1.5.3</a></span></span>
* <span data-ttu-id="ee0c5-187">Устранена проблема [№ 81](https://github.com/Azure/azure-documentdb-node/issues/81). Правильная обработка тире в идентификаторах носителей.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-187">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span></span>

### <span data-ttu-id="ee0c5-188"><a name="1.5.2"/>1.5.2</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-188"><a name="1.5.2"/>1.5.2</a></span></span>
* <span data-ttu-id="ee0c5-189">Устранена проблема [№ 95](https://github.com/Azure/azure-documentdb-node/issues/95). Предупреждение об утечке данных прослушивателя EventEmitter.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-189">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span></span>

### <span data-ttu-id="ee0c5-190"><a name="1.5.1"/>1.5.1</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-190"><a name="1.5.1"/>1.5.1</a></span></span>
* <span data-ttu-id="ee0c5-191">Устраняет проблему, [#92](https://github.com/Azure/azure-documentdb-node/issues/90) -переименовать папку toohash хэш для систем с учетом регистра.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-191">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash toohash for case-sensitive systems.</span></span>

### <span data-ttu-id="ee0c5-192"><a name="1.5.0"/>1.5.0</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-192"><a name="1.5.0"/>1.5.0</a></span></span>
* <span data-ttu-id="ee0c5-193">Реализация поддержки сегментирования за счет добавления сопоставителей секций хэша и диапазона.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-193">Implement sharding support by adding hash & range partition resolvers.</span></span>

### <span data-ttu-id="ee0c5-194"><a name="1.4.0"/>1.4.0</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-194"><a name="1.4.0"/>1.4.0</a></span></span>
* <span data-ttu-id="ee0c5-195">Реализована операция Upsert.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-195">Implement Upsert.</span></span> <span data-ttu-id="ee0c5-196">Новые методы upsertXXX в documentClient.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-196">New upsertXXX methods on documentClient.</span></span>

### <span data-ttu-id="ee0c5-197"><a name="1.3.0"/>1.3.0</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-197"><a name="1.3.0"/>1.3.0</a></span></span>
* <span data-ttu-id="ee0c5-198">Пропущена toobring номера версий, согласованные с других пакетов SDK.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-198">Skipped toobring version numbers in alignment with other SDKs.</span></span>

### <span data-ttu-id="ee0c5-199"><a name="1.2.2"/>1.2.2</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-199"><a name="1.2.2"/>1.2.2</a></span></span>
* <span data-ttu-id="ee0c5-200">Вопросы разбиения обещания репозитория toonew программы-оболочки.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-200">Split Q promises wrapper toonew repository.</span></span>
* <span data-ttu-id="ee0c5-201">Обновите файл toopackage для реестра npm.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-201">Update toopackage file for npm registry.</span></span>

### <span data-ttu-id="ee0c5-202"><a name="1.2.1"/>1.2.1</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-202"><a name="1.2.1"/>1.2.1</a></span></span>
* <span data-ttu-id="ee0c5-203">Реализована маршрутизация на основе идентификатора.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-203">Implements ID Based Routing.</span></span>
* <span data-ttu-id="ee0c5-204">Устранена проблема [№ 49](https://github.com/Azure/azure-documentdb-node/issues/49) : конфликт текущего свойства с методом current().</span><span class="sxs-lookup"><span data-stu-id="ee0c5-204">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span></span>

### <span data-ttu-id="ee0c5-205"><a name="1.2.0"/>1.2.0</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-205"><a name="1.2.0"/>1.2.0</a></span></span>
* <span data-ttu-id="ee0c5-206">Добавлена поддержка геопространственного индекса.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-206">Added support for GeoSpatial index.</span></span>
* <span data-ttu-id="ee0c5-207">Проверка свойств идентификатора для всех ресурсов.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-207">Validates id property for all resources.</span></span> <span data-ttu-id="ee0c5-208">Идентификаторы ресурсов не могут содержать символы ?, /, #, &#47;&#47; или заканчиваться пробелом.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-208">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span></span>
* <span data-ttu-id="ee0c5-209">Добавляет новый tooResourceResponse заголовок «выполняется преобразование индекса».</span><span class="sxs-lookup"><span data-stu-id="ee0c5-209">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <span data-ttu-id="ee0c5-210"><a name="1.1.0"/>1.1.0</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-210"><a name="1.1.0"/>1.1.0</a></span></span>
* <span data-ttu-id="ee0c5-211">Реализована политика индексации версии 2.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-211">Implements V2 indexing policy.</span></span>

### <span data-ttu-id="ee0c5-212"><a name="1.0.3"/>1.0.3</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-212"><a name="1.0.3"/>1.0.3</a></span></span>
* <span data-ttu-id="ee0c5-213">Проблема [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - реализации eslint grunt конфигурации ядра hello и promise SDK.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-213">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in hello core and promise SDK.</span></span>

### <span data-ttu-id="ee0c5-214"><a name="1.0.2"/>1.0.2</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-214"><a name="1.0.2"/>1.0.2</a></span></span>
* <span data-ttu-id="ee0c5-215">Устранена проблема [№ 45](https://github.com/Azure/azure-documentdb-node/issues/45) — оболочка обещаний больше не включает заголовок с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-215">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span></span>

### <span data-ttu-id="ee0c5-216"><a name="1.0.1"/>1.0.1</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-216"><a name="1.0.1"/>1.0.1</a></span></span>
* <span data-ttu-id="ee0c5-217">Реализована возможность tooquery конфликтов, добавляя readConflicts, readConflictAsync и queryConflicts.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-217">Implemented ability tooquery for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span></span>
* <span data-ttu-id="ee0c5-218">Обновлена документация по API.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-218">Updated API documentation.</span></span>
* <span data-ttu-id="ee0c5-219">Проблема [№41](https://github.com/Azure/azure-documentdb-node/issues/41) — ошибка client.createDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-219">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span></span>

### <span data-ttu-id="ee0c5-220"><a name="1.0.0"/>1.0.0</a></span><span class="sxs-lookup"><span data-stu-id="ee0c5-220"><a name="1.0.0"/>1.0.0</a></span></span>
* <span data-ttu-id="ee0c5-221">Пакет SDK общей доступности.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-221">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="ee0c5-222">Даты выпуска и выбытия</span><span class="sxs-lookup"><span data-stu-id="ee0c5-222">Release & Retirement Dates</span></span>
<span data-ttu-id="ee0c5-223">Корпорация Майкрософт предоставляет уведомления по крайней мере **12 месяцев** до снятия с учета в новой/поддерживаемой версии для hello перехода порядок toosmooth tooa пакет SDK.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-223">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="ee0c5-224">Новые функции и функциональные возможности и оптимизацию добавляются только toohello текущего пакета SDK, таким образом, рекомендуется, вы всегда обновления toohello последнюю версию пакета SDK как можно раньше.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-224">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommended that you always upgrade toohello latest SDK version as early as possible.</span></span>

<span data-ttu-id="ee0c5-225">Любой запрос, который является tooCosmos базу данных, используя удалено SDK отклонены службой hello.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-225">Any request tooCosmos DB using a retired SDK is be rejected by hello service.</span></span>

<br/>

| <span data-ttu-id="ee0c5-226">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="ee0c5-226">Version</span></span> | <span data-ttu-id="ee0c5-227">Дата выпуска</span><span class="sxs-lookup"><span data-stu-id="ee0c5-227">Release Date</span></span> | <span data-ttu-id="ee0c5-228">Дата вывода</span><span class="sxs-lookup"><span data-stu-id="ee0c5-228">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="ee0c5-229">1.12.2</span><span class="sxs-lookup"><span data-stu-id="ee0c5-229">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="ee0c5-230">10 августа 2017 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-230">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="ee0c5-231">1.12.1</span><span class="sxs-lookup"><span data-stu-id="ee0c5-231">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="ee0c5-232">10 августа 2017 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-232">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="ee0c5-233">1.12.0</span><span class="sxs-lookup"><span data-stu-id="ee0c5-233">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="ee0c5-234">10 мая 2017 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-234">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="ee0c5-235">1.11.0</span><span class="sxs-lookup"><span data-stu-id="ee0c5-235">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="ee0c5-236">16 марта 2017 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-236">March 16, 2017</span></span> |--- |
| [<span data-ttu-id="ee0c5-237">1.10.2</span><span class="sxs-lookup"><span data-stu-id="ee0c5-237">1.10.2</span></span>](#1.10.2) |<span data-ttu-id="ee0c5-238">27 января 2017 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-238">January 27, 2017</span></span> |--- |
| [<span data-ttu-id="ee0c5-239">1.10.1</span><span class="sxs-lookup"><span data-stu-id="ee0c5-239">1.10.1</span></span>](#1.10.1) |<span data-ttu-id="ee0c5-240">22 декабря 2016 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-240">December 22, 2016</span></span> |--- |
| [<span data-ttu-id="ee0c5-241">1.10.0</span><span class="sxs-lookup"><span data-stu-id="ee0c5-241">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="ee0c5-242">3 октября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-242">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="ee0c5-243">1.9.0</span><span class="sxs-lookup"><span data-stu-id="ee0c5-243">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="ee0c5-244">7 июля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-244">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="ee0c5-245">1.8.0</span><span class="sxs-lookup"><span data-stu-id="ee0c5-245">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="ee0c5-246">14 июня 2016 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-246">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="ee0c5-247">1.7.0</span><span class="sxs-lookup"><span data-stu-id="ee0c5-247">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="ee0c5-248">26 апреля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-248">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="ee0c5-249">1.6.0</span><span class="sxs-lookup"><span data-stu-id="ee0c5-249">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="ee0c5-250">29 марта 2016 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-250">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="ee0c5-251">1.5.6</span><span class="sxs-lookup"><span data-stu-id="ee0c5-251">1.5.6</span></span>](#1.5.6) |<span data-ttu-id="ee0c5-252">8 марта 2016 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-252">March 08, 2016</span></span> |--- |
| [<span data-ttu-id="ee0c5-253">1.5.5</span><span class="sxs-lookup"><span data-stu-id="ee0c5-253">1.5.5</span></span>](#1.5.5) |<span data-ttu-id="ee0c5-254">2 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-254">February 02, 2016</span></span> |--- |
| [<span data-ttu-id="ee0c5-255">1.5.4</span><span class="sxs-lookup"><span data-stu-id="ee0c5-255">1.5.4</span></span>](#1.5.4) |<span data-ttu-id="ee0c5-256">1 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-256">February 01, 2016</span></span> |--- |
| [<span data-ttu-id="ee0c5-257">1.5.2</span><span class="sxs-lookup"><span data-stu-id="ee0c5-257">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="ee0c5-258">26 января 2016 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-258">January 26, 2016</span></span> |--- |
| [<span data-ttu-id="ee0c5-259">1.5.2</span><span class="sxs-lookup"><span data-stu-id="ee0c5-259">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="ee0c5-260">22 января 2016 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-260">January 22, 2016</span></span> |--- |
| [<span data-ttu-id="ee0c5-261">1.5.1</span><span class="sxs-lookup"><span data-stu-id="ee0c5-261">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="ee0c5-262">4 января 2016 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-262">January 4, 2016</span></span> |--- |
| [<span data-ttu-id="ee0c5-263">1.5.0</span><span class="sxs-lookup"><span data-stu-id="ee0c5-263">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="ee0c5-264">31 декабря 2015 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-264">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="ee0c5-265">1.4.0</span><span class="sxs-lookup"><span data-stu-id="ee0c5-265">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="ee0c5-266">6 октября 2015 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-266">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="ee0c5-267">1.3.0</span><span class="sxs-lookup"><span data-stu-id="ee0c5-267">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="ee0c5-268">6 октября 2015 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-268">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="ee0c5-269">1.2.2</span><span class="sxs-lookup"><span data-stu-id="ee0c5-269">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="ee0c5-270">10 сентября 2015 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-270">September 10, 2015</span></span> |--- |
| [<span data-ttu-id="ee0c5-271">1.2.1</span><span class="sxs-lookup"><span data-stu-id="ee0c5-271">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="ee0c5-272">15 августа 2015 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-272">August 15, 2015</span></span> |--- |
| [<span data-ttu-id="ee0c5-273">1.2.0</span><span class="sxs-lookup"><span data-stu-id="ee0c5-273">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="ee0c5-274">5 августа 2015 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-274">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="ee0c5-275">1.1.0</span><span class="sxs-lookup"><span data-stu-id="ee0c5-275">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="ee0c5-276">9 июля 2015 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-276">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="ee0c5-277">1.0.3</span><span class="sxs-lookup"><span data-stu-id="ee0c5-277">1.0.3</span></span>](#1.0.3) |<span data-ttu-id="ee0c5-278">4 июня 2015 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-278">June 04, 2015</span></span> |--- |
| [<span data-ttu-id="ee0c5-279">1.0.2</span><span class="sxs-lookup"><span data-stu-id="ee0c5-279">1.0.2</span></span>](#1.0.2) |<span data-ttu-id="ee0c5-280">23 мая, 2015 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-280">May 23, 2015</span></span> |--- |
| [<span data-ttu-id="ee0c5-281">1.0.1</span><span class="sxs-lookup"><span data-stu-id="ee0c5-281">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="ee0c5-282">15 мая 2015 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-282">May 15, 2015</span></span> |--- |
| [<span data-ttu-id="ee0c5-283">1.0.0</span><span class="sxs-lookup"><span data-stu-id="ee0c5-283">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="ee0c5-284">8 апреля 2015 г.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-284">April 08, 2015</span></span> |--- |

## <a name="faq"></a><span data-ttu-id="ee0c5-285">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="ee0c5-285">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="ee0c5-286">См. также</span><span class="sxs-lookup"><span data-stu-id="ee0c5-286">See also</span></span>
<span data-ttu-id="ee0c5-287">toolearn Дополнительные сведения о Cosmos DB. в разделе [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) страницы службы.</span><span class="sxs-lookup"><span data-stu-id="ee0c5-287">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

