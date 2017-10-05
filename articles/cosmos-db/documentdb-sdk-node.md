---
title: "Пакет SDK и интерфейсы API для Node.js (Azure Cosmos DB) | Документация Майкрософт"
description: "Сведения об API и пакете SDK для Node.js, включая даты выхода, даты выбытия и изменения, внесенные в каждую версию пакета SDK для Azure Cosmos DB Node.js."
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
ms.openlocfilehash: 4376a5c07b5f00311ce0fe3c0056efdf79c273f9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-nodejs-sdk-release-notes-and-resources"></a><span data-ttu-id="9c0d6-103">Пакет SDK Node.js для Azure Cosmos DB: заметки о выпуске и ресурсы</span><span class="sxs-lookup"><span data-stu-id="9c0d6-103">Azure Cosmos DB Node.js SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9c0d6-104">.NET</span><span class="sxs-lookup"><span data-stu-id="9c0d6-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="9c0d6-105">Веб-канал изменений в .NET</span><span class="sxs-lookup"><span data-stu-id="9c0d6-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="9c0d6-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="9c0d6-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="9c0d6-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="9c0d6-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="9c0d6-108">Java</span><span class="sxs-lookup"><span data-stu-id="9c0d6-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="9c0d6-109">Python</span><span class="sxs-lookup"><span data-stu-id="9c0d6-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="9c0d6-110">REST</span><span class="sxs-lookup"><span data-stu-id="9c0d6-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="9c0d6-111">Поставщик ресурсов REST</span><span class="sxs-lookup"><span data-stu-id="9c0d6-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="9c0d6-112">SQL</span><span class="sxs-lookup"><span data-stu-id="9c0d6-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="9c0d6-113">**Скачать пакет SDK**</span><span class="sxs-lookup"><span data-stu-id="9c0d6-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="9c0d6-114">NPM</span><span class="sxs-lookup"><span data-stu-id="9c0d6-114">NPM</span></span>](https://www.npmjs.com/package/documentdb)</td></tr>

<tr><td><span data-ttu-id="9c0d6-115">**Документация по API**</span><span class="sxs-lookup"><span data-stu-id="9c0d6-115">**API documentation**</span></span></td><td>[<span data-ttu-id="9c0d6-116">Справочная документация по API Node.js</span><span class="sxs-lookup"><span data-stu-id="9c0d6-116">Node.js API reference documentation</span></span>](http://azure.github.io/azure-documentdb-node/DocumentClient.html)</td></tr>

<tr><td><span data-ttu-id="9c0d6-117">**Инструкции по установке пакета SDK**</span><span class="sxs-lookup"><span data-stu-id="9c0d6-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="9c0d6-118">Инструкции по установке</span><span class="sxs-lookup"><span data-stu-id="9c0d6-118">Installation instructions</span></span>](http://azure.github.io/azure-documentdb-node/)</td></tr>

<tr><td><span data-ttu-id="9c0d6-119">**Участие в разработке пакета SDK**</span><span class="sxs-lookup"><span data-stu-id="9c0d6-119">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="9c0d6-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="9c0d6-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-node/tree/master/source)</td></tr>

<tr><td><span data-ttu-id="9c0d6-121">**Примеры**</span><span class="sxs-lookup"><span data-stu-id="9c0d6-121">**Samples**</span></span></td><td>[<span data-ttu-id="9c0d6-122">Примеры кода Node.js</span><span class="sxs-lookup"><span data-stu-id="9c0d6-122">Node.js code samples</span></span>](documentdb-nodejs-samples.md)</td></tr>

<tr><td><span data-ttu-id="9c0d6-123">**Учебник по началу работы**</span><span class="sxs-lookup"><span data-stu-id="9c0d6-123">**Get started tutorial**</span></span></td><td>[<span data-ttu-id="9c0d6-124">Приступая к работе с пакетом SDK для Node.js</span><span class="sxs-lookup"><span data-stu-id="9c0d6-124">Get started with the Node.js SDK</span></span>](documentdb-nodejs-get-started.md)</td></tr>

<tr><td><span data-ttu-id="9c0d6-125">**Учебник по веб-приложениям**</span><span class="sxs-lookup"><span data-stu-id="9c0d6-125">**Web app tutorial**</span></span></td><td>[<span data-ttu-id="9c0d6-126">Создание веб-приложения Node.js с использованием Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="9c0d6-126">Build a Node.js web application using Azure Cosmos DB</span></span>](documentdb-nodejs-application.md)</td></tr>

<tr><td><span data-ttu-id="9c0d6-127">**Текущая поддерживаемая платформа**</span><span class="sxs-lookup"><span data-stu-id="9c0d6-127">**Current supported platform**</span></span></td><td> 
[<span data-ttu-id="9c0d6-128">Node.js v6.x</span><span class="sxs-lookup"><span data-stu-id="9c0d6-128">Node.js v6.x</span></span>](https://nodejs.org/en/blog/release/v6.10.3/)<br/> 
[<span data-ttu-id="9c0d6-129">Node.js версии 4.2.0</span><span class="sxs-lookup"><span data-stu-id="9c0d6-129">Node.js v4.2.0</span></span>](https://nodejs.org/en/blog/release/v4.2.0/)<br/> 
[<span data-ttu-id="9c0d6-130">Node.js версии 0.12</span><span class="sxs-lookup"><span data-stu-id="9c0d6-130">Node.js v0.12</span></span>](https://nodejs.org/en/blog/release/v0.12.0/)<br/> 
<span data-ttu-id="9c0d6-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span><span class="sxs-lookup"><span data-stu-id="9c0d6-131">[Node.js v0.10](https://nodejs.org/en/blog/release/v0.10.0/) 
</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="9c0d6-132">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="9c0d6-132">Release notes</span></span>

### <span data-ttu-id="9c0d6-133"><a name="1.12.2"/>1.12.2</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-133"><a name="1.12.2"/>1.12.2</a></span></span>
*   <span data-ttu-id="9c0d6-134">Исправлена документация npm.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-134">npm documentation fixed.</span></span>

### <span data-ttu-id="9c0d6-135"><a name="1.12.1"/>1.12.1</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-135"><a name="1.12.1"/>1.12.1</a></span></span>
* <span data-ttu-id="9c0d6-136">Исправлена ошибка в executeStoredProcedure, где документы содержали специальные символы Юникода (LS, PS).</span><span class="sxs-lookup"><span data-stu-id="9c0d6-136">Fixed a bug in executeStoredProcedure where documents involved had special Unicode characters (LS, PS).</span></span>
* <span data-ttu-id="9c0d6-137">Исправлена ошибка обработки документов с использованием символов Юникода в ключе секции.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-137">Fixed a bug in handling documents with Unicode characters in the partition key.</span></span>
* <span data-ttu-id="9c0d6-138">Исправлена поддержка создания коллекций с именем носителя.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-138">Fixed support for creating collections with the name media.</span></span> <span data-ttu-id="9c0d6-139">Проблема GitHub 114.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-139">Github issue #114.</span></span>
* <span data-ttu-id="9c0d6-140">Исправлена поддержка маркера авторизации разрешений.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-140">Fixed support for permission authorization token.</span></span> <span data-ttu-id="9c0d6-141">Проблема GitHub 178.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-141">Github issue #178.</span></span>

### <span data-ttu-id="9c0d6-142"><a name="1.12.0"/>1.12.0</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-142"><a name="1.12.0"/>1.12.0</a></span></span>
* <span data-ttu-id="9c0d6-143">Добавлена поддержка нового [уровня согласованности](consistency-levels.md) с именем ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-143">Added support for a new [consistency level](consistency-levels.md) called ConsistentPrefix.</span></span>
* <span data-ttu-id="9c0d6-144">Добавлена поддержка UriFactory.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-144">Added support for UriFactory.</span></span>
* <span data-ttu-id="9c0d6-145">Исправлена ошибка поддержки Юникода.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-145">Fixed a Unicode support bug.</span></span> <span data-ttu-id="9c0d6-146">Проблема GitHub 171.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-146">GitHub issue #171.</span></span>

### <span data-ttu-id="9c0d6-147"><a name="1.11.0"/>1.11.0</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-147"><a name="1.11.0"/>1.11.0</a></span></span>
* <span data-ttu-id="9c0d6-148">Добавлена поддержка статистических запросов (COUNT, MIN, MAX, SUM и AVG).</span><span class="sxs-lookup"><span data-stu-id="9c0d6-148">Added the support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="9c0d6-149">Добавлена возможность контролировать степень параллелизма для запросов между секциями.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-149">Added the option for controlling degree of parallelism for cross partition queries.</span></span>
* <span data-ttu-id="9c0d6-150">Добавлена возможность отключения проверки SSL при работе с эмулятором Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-150">Added the option for disabling SSL verification when running against Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="9c0d6-151">Минимальная пропускная способность секционированных коллекций снижена с 10 100 ЕЗ/с до 2500 ЕЗ/с.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-151">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>
* <span data-ttu-id="9c0d6-152">Исправлена ошибка маркера продолжения для односекционной коллекции.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-152">Fixed the continuation token bug for single partition collection.</span></span> <span data-ttu-id="9c0d6-153">Проблема GitHub 107.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-153">Github issue #107.</span></span>
* <span data-ttu-id="9c0d6-154">Исправлена ошибка выполнения хранимой процедуры (executeStoredProcedure) при обработке 0 как одного параметра.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-154">Fixed the executeStoredProcedure bug in handling 0 as single param.</span></span> <span data-ttu-id="9c0d6-155">Проблема GitHub 155.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-155">Github issue #155.</span></span>

### <span data-ttu-id="9c0d6-156"><a name="1.10.2"/>1.10.2</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-156"><a name="1.10.2"/>1.10.2</a></span></span>
* <span data-ttu-id="9c0d6-157">Теперь заголовок User-Agent включает версию пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-157">Fixed user-agent header to include the SDK version.</span></span>
* <span data-ttu-id="9c0d6-158">Дополнительная очистка кода.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-158">Minor code cleanup.</span></span>

### <span data-ttu-id="9c0d6-159"><a name="1.10.1"/>1.10.1</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-159"><a name="1.10.1"/>1.10.1</a></span></span>
* <span data-ttu-id="9c0d6-160">Отключение проверки SSL при использовании пакета SDK для emulator(hostname=localhost).</span><span class="sxs-lookup"><span data-stu-id="9c0d6-160">Disabling SSL verification when using the SDK to target the emulator(hostname=localhost).</span></span>
* <span data-ttu-id="9c0d6-161">Добавлена поддержка включения ведения журнала сценариев во время выполнения хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-161">Added support for enabling script logging during stored procedure execution.</span></span>

### <span data-ttu-id="9c0d6-162"><a name="1.10.0"/>1.10.0</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-162"><a name="1.10.0"/>1.10.0</a></span></span>
* <span data-ttu-id="9c0d6-163">Добавлена поддержка параллельных запросов между секциями.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-163">Added support for cross partition parallel queries.</span></span>
* <span data-ttu-id="9c0d6-164">Добавлена поддержка запросов TOP и ORDER BY для секционированных коллекций.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-164">Added support for TOP/ORDER BY queries for partitioned collections.</span></span>

### <span data-ttu-id="9c0d6-165"><a name="1.9.0"/>1.9.0</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-165"><a name="1.9.0"/>1.9.0</a></span></span>
* <span data-ttu-id="9c0d6-166">Добавлена поддержка политики повтора для отрегулированных запросов.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-166">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="9c0d6-167">(Отрегулированные запросы порождают исключение слишком высокой частоты запросов с кодом ошибки 429.) По умолчанию при обнаружении кода ошибки 429 Azure Cosmos DB повторяет запрос девять раз, используя интервал retryAfter в заголовке ответа.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-167">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span></span> <span data-ttu-id="9c0d6-168">Фиксированный интервал повтора теперь можно задать как часть свойства RetryOptions объекта ConnectionPolicy, если требуется игнорировать интервал retryAfter, возвращаемый сервером между повторными попытками.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-168">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span></span> <span data-ttu-id="9c0d6-169">Теперь Azure Cosmos DB ожидает до 30 секунд, пока запрос регулируется (независимо от количества повторных попыток), и возвращает ответ с кодом ошибки 429.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-169">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span></span> <span data-ttu-id="9c0d6-170">Этот интервал также можно переопределить в свойстве RetryOptions объекта ConnectionPolicy.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-170">This time can also be overridden in the RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="9c0d6-171">Теперь Cosmos DB возвращает x-ms-throttle-retry-count и x-ms-throttle-retry-wait-time-ms в заголовке ответа на каждый запрос, чтобы обозначить количество повторных попыток при регулировании и совокупное время ожидания запроса между повторами.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-171">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cumulative time the request waited between the retries.</span></span>
* <span data-ttu-id="9c0d6-172">Добавлен класс RetryOptions, предоставляющей свойство RetryOptions класса ConnectionPolicy, с помощью которого можно переопределить некоторые параметры повторных попыток по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-172">The RetryOptions class was added, exposing the RetryOptions property on the ConnectionPolicy class that can be used to override some of the default retry options.</span></span>

### <span data-ttu-id="9c0d6-173"><a name="1.8.0"/>1.8.0</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-173"><a name="1.8.0"/>1.8.0</a></span></span>
* <span data-ttu-id="9c0d6-174">Добавлена поддержка учетных записей базы данных в нескольких регионах.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-174">Added the support for multi-region database accounts.</span></span>

### <span data-ttu-id="9c0d6-175"><a name="1.7.0"/>1.7.0</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-175"><a name="1.7.0"/>1.7.0</a></span></span>
* <span data-ttu-id="9c0d6-176">Добавлена поддержка функции срока жизни для документов.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-176">Added the support for Time To Live(TTL) feature for documents.</span></span>

### <span data-ttu-id="9c0d6-177"><a name="1.6.0"/>1.6.0</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-177"><a name="1.6.0"/>1.6.0</a></span></span>
* <span data-ttu-id="9c0d6-178">Реализованы [секционированные коллекции](partition-data.md) и [определяемые пользователем уровни производительности](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="9c0d6-178">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span>

### <span data-ttu-id="9c0d6-179"><a name="1.5.6"/>1.5.6</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-179"><a name="1.5.6"/>1.5.6</a></span></span>
* <span data-ttu-id="9c0d6-180">Исправлена ошибка RangePartitionResolver.resolveForRead, связанная с невозвращением ссылок из-за некорректных результатов сцепки.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-180">Fixed RangePartitionResolver.resolveForRead bug where it was not returning links due to a bad concat of results.</span></span>

### <span data-ttu-id="9c0d6-181"><a name="1.5.5"/>1.5.5</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-181"><a name="1.5.5"/>1.5.5</a></span></span>
* <span data-ttu-id="9c0d6-182">Исправлена ошибка метода resolveForRead() hashParitionResolver. Ранее вместо возврата списка всех зарегистрированных ссылок при отсутствии ключа раздела вызвалось исключение.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-182">Fixed hashParitionResolver resolveForRead(): When no partition key supplied was throwing exception, instead of returning a list of all registered links.</span></span>

### <span data-ttu-id="9c0d6-183"><a name="1.5.4"/>1.5.4</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-183"><a name="1.5.4"/>1.5.4</a></span></span>
* <span data-ttu-id="9c0d6-184">Устранена проблема [№ 100](https://github.com/Azure/azure-documentdb-node/issues/100). Выделенный агент HTTPS: избегайте изменения глобального агента для Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-184">Fixes issue [#100](https://github.com/Azure/azure-documentdb-node/issues/100) - Dedicated HTTPS Agent: Avoid modifying the global agent for Azure Cosmos DB purposes.</span></span> <span data-ttu-id="9c0d6-185">Используйте выделенный агент для всех запросов lib.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-185">Use a dedicated agent for all of the lib’s requests.</span></span>

### <span data-ttu-id="9c0d6-186"><a name="1.5.3"/>1.5.3</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-186"><a name="1.5.3"/>1.5.3</a></span></span>
* <span data-ttu-id="9c0d6-187">Устранена проблема [№ 81](https://github.com/Azure/azure-documentdb-node/issues/81). Правильная обработка тире в идентификаторах носителей.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-187">Fixes issue [#81](https://github.com/Azure/azure-documentdb-node/issues/81) - Properly handle dashes in media ids.</span></span>

### <span data-ttu-id="9c0d6-188"><a name="1.5.2"/>1.5.2</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-188"><a name="1.5.2"/>1.5.2</a></span></span>
* <span data-ttu-id="9c0d6-189">Устранена проблема [№ 95](https://github.com/Azure/azure-documentdb-node/issues/95). Предупреждение об утечке данных прослушивателя EventEmitter.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-189">Fixes issue [#95](https://github.com/Azure/azure-documentdb-node/issues/95) - EventEmitter listener leak warning.</span></span>

### <span data-ttu-id="9c0d6-190"><a name="1.5.1"/>1.5.1</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-190"><a name="1.5.1"/>1.5.1</a></span></span>
* <span data-ttu-id="9c0d6-191">Устранена проблема [92](https://github.com/Azure/azure-documentdb-node/issues/90). Переименование папки Hash в hash для систем с учетом регистра.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-191">Fixes issue [#92](https://github.com/Azure/azure-documentdb-node/issues/90) - rename folder Hash to hash for case-sensitive systems.</span></span>

### <span data-ttu-id="9c0d6-192"><a name="1.5.0"/>1.5.0</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-192"><a name="1.5.0"/>1.5.0</a></span></span>
* <span data-ttu-id="9c0d6-193">Реализация поддержки сегментирования за счет добавления сопоставителей секций хэша и диапазона.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-193">Implement sharding support by adding hash & range partition resolvers.</span></span>

### <span data-ttu-id="9c0d6-194"><a name="1.4.0"/>1.4.0</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-194"><a name="1.4.0"/>1.4.0</a></span></span>
* <span data-ttu-id="9c0d6-195">Реализована операция Upsert.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-195">Implement Upsert.</span></span> <span data-ttu-id="9c0d6-196">Новые методы upsertXXX в documentClient.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-196">New upsertXXX methods on documentClient.</span></span>

### <span data-ttu-id="9c0d6-197"><a name="1.3.0"/>1.3.0</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-197"><a name="1.3.0"/>1.3.0</a></span></span>
* <span data-ttu-id="9c0d6-198">Номера версий пропущены для согласованности с другими пакетами SDK.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-198">Skipped to bring version numbers in alignment with other SDKs.</span></span>

### <span data-ttu-id="9c0d6-199"><a name="1.2.2"/>1.2.2</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-199"><a name="1.2.2"/>1.2.2</a></span></span>
* <span data-ttu-id="9c0d6-200">В новый репозиторий добавляется оболочка для обещаний Split Q.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-200">Split Q promises wrapper to new repository.</span></span>
* <span data-ttu-id="9c0d6-201">Обновлен файл пакета для реестра npm.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-201">Update to package file for npm registry.</span></span>

### <span data-ttu-id="9c0d6-202"><a name="1.2.1"/>1.2.1</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-202"><a name="1.2.1"/>1.2.1</a></span></span>
* <span data-ttu-id="9c0d6-203">Реализована маршрутизация на основе идентификатора.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-203">Implements ID Based Routing.</span></span>
* <span data-ttu-id="9c0d6-204">Устранена проблема [№ 49](https://github.com/Azure/azure-documentdb-node/issues/49) : конфликт текущего свойства с методом current().</span><span class="sxs-lookup"><span data-stu-id="9c0d6-204">Fixes Issue [#49](https://github.com/Azure/azure-documentdb-node/issues/49) - current property conflicts with method current().</span></span>

### <span data-ttu-id="9c0d6-205"><a name="1.2.0"/>1.2.0</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-205"><a name="1.2.0"/>1.2.0</a></span></span>
* <span data-ttu-id="9c0d6-206">Добавлена поддержка геопространственного индекса.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-206">Added support for GeoSpatial index.</span></span>
* <span data-ttu-id="9c0d6-207">Проверка свойств идентификатора для всех ресурсов.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-207">Validates id property for all resources.</span></span> <span data-ttu-id="9c0d6-208">Идентификаторы ресурсов не могут содержать символы ?, /, #, &#47;&#47; или заканчиваться пробелом.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-208">Ids for resources cannot contain ?, /, #, &#47;&#47;, characters or end with a space.</span></span>
* <span data-ttu-id="9c0d6-209">Добавлен новый заголовок "ход выполнения преобразования индекса" в ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-209">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <span data-ttu-id="9c0d6-210"><a name="1.1.0"/>1.1.0</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-210"><a name="1.1.0"/>1.1.0</a></span></span>
* <span data-ttu-id="9c0d6-211">Реализована политика индексации версии 2.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-211">Implements V2 indexing policy.</span></span>

### <span data-ttu-id="9c0d6-212"><a name="1.0.3"/>1.0.3</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-212"><a name="1.0.3"/>1.0.3</a></span></span>
* <span data-ttu-id="9c0d6-213">Устранена проблема [№ 40](https://github.com/Azure/azure-documentdb-node/issues/40). Реализованы конфигурации eslint и grunt в пакете SDK для ядра и обещаний.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-213">Issue [#40](https://github.com/Azure/azure-documentdb-node/issues/40) - Implemented eslint and grunt configurations in the core and promise SDK.</span></span>

### <span data-ttu-id="9c0d6-214"><a name="1.0.2"/>1.0.2</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-214"><a name="1.0.2"/>1.0.2</a></span></span>
* <span data-ttu-id="9c0d6-215">Устранена проблема [№ 45](https://github.com/Azure/azure-documentdb-node/issues/45) — оболочка обещаний больше не включает заголовок с ошибкой.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-215">Issue [#45](https://github.com/Azure/azure-documentdb-node/issues/45) - Promises wrapper does not include header with error.</span></span>

### <span data-ttu-id="9c0d6-216"><a name="1.0.1"/>1.0.1</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-216"><a name="1.0.1"/>1.0.1</a></span></span>
* <span data-ttu-id="9c0d6-217">Реализована возможность запрашивать конфликты, добавляя методы readConflicts, readConflictAsync и queryConflicts.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-217">Implemented ability to query for conflicts by adding readConflicts, readConflictAsync, and queryConflicts.</span></span>
* <span data-ttu-id="9c0d6-218">Обновлена документация по API.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-218">Updated API documentation.</span></span>
* <span data-ttu-id="9c0d6-219">Проблема [№41](https://github.com/Azure/azure-documentdb-node/issues/41) — ошибка client.createDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-219">Issue [#41](https://github.com/Azure/azure-documentdb-node/issues/41) - client.createDocumentAsync error.</span></span>

### <span data-ttu-id="9c0d6-220"><a name="1.0.0"/>1.0.0</a></span><span class="sxs-lookup"><span data-stu-id="9c0d6-220"><a name="1.0.0"/>1.0.0</a></span></span>
* <span data-ttu-id="9c0d6-221">Пакет SDK общей доступности.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-221">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="9c0d6-222">Даты выпуска и выбытия</span><span class="sxs-lookup"><span data-stu-id="9c0d6-222">Release & Retirement Dates</span></span>
<span data-ttu-id="9c0d6-223">Корпорация Майкрософт отправляет уведомление минимум за **12 месяцев** до вывода пакета SDK из эксплуатации, чтобы обеспечить более плавный переход на новую или поддерживаемую версию.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-223">Microsoft provides notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="9c0d6-224">Новые функции, возможности и оптимизации добавляются только в текущую версию пакета SDK, поэтому рекомендуется как можно раньше обновлять пакет SDK до последней версии.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-224">New features and functionality and optimizations are only added to the current SDK, as such it is  recommended that you always upgrade to the latest SDK version as early as possible.</span></span>

<span data-ttu-id="9c0d6-225">Любые запросы к Cosmos DB с помощью выведенного из эксплуатации пакета SDK отклоняются службой.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-225">Any request to Cosmos DB using a retired SDK is be rejected by the service.</span></span>

<br/>

| <span data-ttu-id="9c0d6-226">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="9c0d6-226">Version</span></span> | <span data-ttu-id="9c0d6-227">Дата выпуска</span><span class="sxs-lookup"><span data-stu-id="9c0d6-227">Release Date</span></span> | <span data-ttu-id="9c0d6-228">Дата вывода</span><span class="sxs-lookup"><span data-stu-id="9c0d6-228">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="9c0d6-229">1.12.2</span><span class="sxs-lookup"><span data-stu-id="9c0d6-229">1.12.2</span></span>](#1.12.2) |<span data-ttu-id="9c0d6-230">10 августа 2017 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-230">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="9c0d6-231">1.12.1</span><span class="sxs-lookup"><span data-stu-id="9c0d6-231">1.12.1</span></span>](#1.12.1) |<span data-ttu-id="9c0d6-232">10 августа 2017 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-232">August 10, 2017</span></span> |--- |
| [<span data-ttu-id="9c0d6-233">1.12.0</span><span class="sxs-lookup"><span data-stu-id="9c0d6-233">1.12.0</span></span>](#1.12.0) |<span data-ttu-id="9c0d6-234">10 мая 2017 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-234">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="9c0d6-235">1.11.0</span><span class="sxs-lookup"><span data-stu-id="9c0d6-235">1.11.0</span></span>](#1.11.0) |<span data-ttu-id="9c0d6-236">16 марта 2017 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-236">March 16, 2017</span></span> |--- |
| [<span data-ttu-id="9c0d6-237">1.10.2</span><span class="sxs-lookup"><span data-stu-id="9c0d6-237">1.10.2</span></span>](#1.10.2) |<span data-ttu-id="9c0d6-238">27 января 2017 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-238">January 27, 2017</span></span> |--- |
| [<span data-ttu-id="9c0d6-239">1.10.1</span><span class="sxs-lookup"><span data-stu-id="9c0d6-239">1.10.1</span></span>](#1.10.1) |<span data-ttu-id="9c0d6-240">22 декабря 2016 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-240">December 22, 2016</span></span> |--- |
| [<span data-ttu-id="9c0d6-241">1.10.0</span><span class="sxs-lookup"><span data-stu-id="9c0d6-241">1.10.0</span></span>](#1.10.0) |<span data-ttu-id="9c0d6-242">3 октября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-242">October 03, 2016</span></span> |--- |
| [<span data-ttu-id="9c0d6-243">1.9.0</span><span class="sxs-lookup"><span data-stu-id="9c0d6-243">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="9c0d6-244">7 июля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-244">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="9c0d6-245">1.8.0</span><span class="sxs-lookup"><span data-stu-id="9c0d6-245">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="9c0d6-246">14 июня 2016 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-246">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="9c0d6-247">1.7.0</span><span class="sxs-lookup"><span data-stu-id="9c0d6-247">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="9c0d6-248">26 апреля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-248">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="9c0d6-249">1.6.0</span><span class="sxs-lookup"><span data-stu-id="9c0d6-249">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="9c0d6-250">29 марта 2016 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-250">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="9c0d6-251">1.5.6</span><span class="sxs-lookup"><span data-stu-id="9c0d6-251">1.5.6</span></span>](#1.5.6) |<span data-ttu-id="9c0d6-252">8 марта 2016 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-252">March 08, 2016</span></span> |--- |
| [<span data-ttu-id="9c0d6-253">1.5.5</span><span class="sxs-lookup"><span data-stu-id="9c0d6-253">1.5.5</span></span>](#1.5.5) |<span data-ttu-id="9c0d6-254">2 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-254">February 02, 2016</span></span> |--- |
| [<span data-ttu-id="9c0d6-255">1.5.4</span><span class="sxs-lookup"><span data-stu-id="9c0d6-255">1.5.4</span></span>](#1.5.4) |<span data-ttu-id="9c0d6-256">1 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-256">February 01, 2016</span></span> |--- |
| [<span data-ttu-id="9c0d6-257">1.5.2</span><span class="sxs-lookup"><span data-stu-id="9c0d6-257">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="9c0d6-258">26 января 2016 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-258">January 26, 2016</span></span> |--- |
| [<span data-ttu-id="9c0d6-259">1.5.2</span><span class="sxs-lookup"><span data-stu-id="9c0d6-259">1.5.2</span></span>](#1.5.2) |<span data-ttu-id="9c0d6-260">22 января 2016 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-260">January 22, 2016</span></span> |--- |
| [<span data-ttu-id="9c0d6-261">1.5.1</span><span class="sxs-lookup"><span data-stu-id="9c0d6-261">1.5.1</span></span>](#1.5.1) |<span data-ttu-id="9c0d6-262">4 января 2016 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-262">January 4, 2016</span></span> |--- |
| [<span data-ttu-id="9c0d6-263">1.5.0</span><span class="sxs-lookup"><span data-stu-id="9c0d6-263">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="9c0d6-264">31 декабря 2015 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-264">December 31, 2015</span></span> |--- |
| [<span data-ttu-id="9c0d6-265">1.4.0</span><span class="sxs-lookup"><span data-stu-id="9c0d6-265">1.4.0</span></span>](#1.4.0) |<span data-ttu-id="9c0d6-266">6 октября 2015 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-266">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="9c0d6-267">1.3.0</span><span class="sxs-lookup"><span data-stu-id="9c0d6-267">1.3.0</span></span>](#1.3.0) |<span data-ttu-id="9c0d6-268">6 октября 2015 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-268">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="9c0d6-269">1.2.2</span><span class="sxs-lookup"><span data-stu-id="9c0d6-269">1.2.2</span></span>](#1.2.2) |<span data-ttu-id="9c0d6-270">10 сентября 2015 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-270">September 10, 2015</span></span> |--- |
| [<span data-ttu-id="9c0d6-271">1.2.1</span><span class="sxs-lookup"><span data-stu-id="9c0d6-271">1.2.1</span></span>](#1.2.1) |<span data-ttu-id="9c0d6-272">15 августа 2015 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-272">August 15, 2015</span></span> |--- |
| [<span data-ttu-id="9c0d6-273">1.2.0</span><span class="sxs-lookup"><span data-stu-id="9c0d6-273">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="9c0d6-274">5 августа 2015 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-274">August 05, 2015</span></span> |--- |
| [<span data-ttu-id="9c0d6-275">1.1.0</span><span class="sxs-lookup"><span data-stu-id="9c0d6-275">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="9c0d6-276">9 июля 2015 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-276">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="9c0d6-277">1.0.3</span><span class="sxs-lookup"><span data-stu-id="9c0d6-277">1.0.3</span></span>](#1.0.3) |<span data-ttu-id="9c0d6-278">4 июня 2015 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-278">June 04, 2015</span></span> |--- |
| [<span data-ttu-id="9c0d6-279">1.0.2</span><span class="sxs-lookup"><span data-stu-id="9c0d6-279">1.0.2</span></span>](#1.0.2) |<span data-ttu-id="9c0d6-280">23 мая, 2015 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-280">May 23, 2015</span></span> |--- |
| [<span data-ttu-id="9c0d6-281">1.0.1</span><span class="sxs-lookup"><span data-stu-id="9c0d6-281">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="9c0d6-282">15 мая 2015 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-282">May 15, 2015</span></span> |--- |
| [<span data-ttu-id="9c0d6-283">1.0.0</span><span class="sxs-lookup"><span data-stu-id="9c0d6-283">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="9c0d6-284">8 апреля 2015 г.</span><span class="sxs-lookup"><span data-stu-id="9c0d6-284">April 08, 2015</span></span> |--- |

## <a name="faq"></a><span data-ttu-id="9c0d6-285">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="9c0d6-285">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="9c0d6-286">См. также</span><span class="sxs-lookup"><span data-stu-id="9c0d6-286">See also</span></span>
<span data-ttu-id="9c0d6-287">Дополнительные сведения о Cosmos DB см. на странице службы [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="9c0d6-287">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span>

