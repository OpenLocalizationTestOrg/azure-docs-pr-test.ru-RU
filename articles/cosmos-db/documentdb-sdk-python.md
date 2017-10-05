---
title: "Пакет SDK и интерфейсы API для Python (Azure Cosmos DB) | Документация Майкрософт"
description: "Сведения о пакете SDK и интерфейсах API для Python, включая даты выхода и прекращения использования, а также изменения, внесенные в каждую версию пакета SDK для Azure Cosmos DB на Python."
services: cosmos-db
documentationcenter: python
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 3ac344a9-b2fa-4a3f-a4cc-02d287e05469
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/24/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70d2550f713ff0e9daed235eb8053589b8682633
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a><span data-ttu-id="5d352-103">Пакет SDK для Azure Cosmos DB на Python: заметки о выпуске и ресурсы</span><span class="sxs-lookup"><span data-stu-id="5d352-103">Azure Cosmos DB Python SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5d352-104">.NET</span><span class="sxs-lookup"><span data-stu-id="5d352-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="5d352-105">Веб-канал изменений в .NET</span><span class="sxs-lookup"><span data-stu-id="5d352-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="5d352-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="5d352-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="5d352-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="5d352-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="5d352-108">Java</span><span class="sxs-lookup"><span data-stu-id="5d352-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="5d352-109">Python</span><span class="sxs-lookup"><span data-stu-id="5d352-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="5d352-110">REST</span><span class="sxs-lookup"><span data-stu-id="5d352-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="5d352-111">Поставщик ресурсов REST</span><span class="sxs-lookup"><span data-stu-id="5d352-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="5d352-112">SQL</span><span class="sxs-lookup"><span data-stu-id="5d352-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="5d352-113">**Скачать пакет SDK**</span><span class="sxs-lookup"><span data-stu-id="5d352-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="5d352-114">PyPI</span><span class="sxs-lookup"><span data-stu-id="5d352-114">PyPI</span></span>](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td><span data-ttu-id="5d352-115">**Документация по API**</span><span class="sxs-lookup"><span data-stu-id="5d352-115">**API documentation**</span></span></td><td>[<span data-ttu-id="5d352-116">Справочная документация по API Python</span><span class="sxs-lookup"><span data-stu-id="5d352-116">Python API reference documentation</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td><span data-ttu-id="5d352-117">**Инструкции по установке пакета SDK**</span><span class="sxs-lookup"><span data-stu-id="5d352-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="5d352-118">Инструкции по установке пакета SDK для Python</span><span class="sxs-lookup"><span data-stu-id="5d352-118">Python SDK installation instructions</span></span>](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td><span data-ttu-id="5d352-119">**Участие в разработке пакета SDK**</span><span class="sxs-lookup"><span data-stu-id="5d352-119">**Contribute to SDK**</span></span></td><td>[<span data-ttu-id="5d352-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="5d352-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td><span data-ttu-id="5d352-121">**Приступая к работе**</span><span class="sxs-lookup"><span data-stu-id="5d352-121">**Get started**</span></span></td><td>[<span data-ttu-id="5d352-122">Приступая к работе с пакетом SDK для Python</span><span class="sxs-lookup"><span data-stu-id="5d352-122">Get started with the Python SDK</span></span>](documentdb-python-application.md)</td></tr>

<tr><td><span data-ttu-id="5d352-123">**Текущая поддерживаемая платформа**</span><span class="sxs-lookup"><span data-stu-id="5d352-123">**Current supported platform**</span></span></td><td><span data-ttu-id="5d352-124">[Python 2.7](https://www.python.org/downloads/) и [Python 3.5](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="5d352-124">[Python 2.7](https://www.python.org/downloads/) and [Python 3.5](https://www.python.org/downloads/)</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="5d352-125">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="5d352-125">Release notes</span></span>
### <a name="a-name220220"></a><span data-ttu-id="5d352-126"><a name="2.2.0"/>2.2.0</span><span class="sxs-lookup"><span data-stu-id="5d352-126"><a name="2.2.0"/>2.2.0</span></span>
* <span data-ttu-id="5d352-127">Добавлена поддержка нового уровня согласованности с именем ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="5d352-127">Added support for a new consistency level called ConsistentPrefix.</span></span>


### <a name="a-name210210"></a><span data-ttu-id="5d352-128"><a name="2.1.0"/>2.1.0</span><span class="sxs-lookup"><span data-stu-id="5d352-128"><a name="2.1.0"/>2.1.0</span></span>
* <span data-ttu-id="5d352-129">Добавлена поддержка статистических запросов (COUNT, MIN, MAX, SUM и AVG).</span><span class="sxs-lookup"><span data-stu-id="5d352-129">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="5d352-130">Добавлена возможность отключения проверки SSL при работе с эмулятором Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5d352-130">Added an option for disabling SSL verification when running against Cosmos DB Emulator.</span></span>
* <span data-ttu-id="5d352-131">Удалено ограничение, согласно которому нужно использовать модуль зависимых запросов только версии 2.10.0.</span><span class="sxs-lookup"><span data-stu-id="5d352-131">Removed the restriction of dependent requests module to be exactly 2.10.0.</span></span>
* <span data-ttu-id="5d352-132">Минимальная пропускная способность секционированных коллекций снижена с 10 100 ЕЗ/с до 2500 ЕЗ/с.</span><span class="sxs-lookup"><span data-stu-id="5d352-132">Lowered minimum throughput on partitioned collections from 10,100 RU/s to 2500 RU/s.</span></span>
* <span data-ttu-id="5d352-133">Добавлена поддержка включения ведения журнала сценариев во время выполнения хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="5d352-133">Added support for enabling script logging during stored procedure execution.</span></span>
* <span data-ttu-id="5d352-134">В этом выпуске версия REST API уменьшена до 2017-01-19.</span><span class="sxs-lookup"><span data-stu-id="5d352-134">REST API version bumped to '2017-01-19' with this release.</span></span>

### <a name="a-name201201"></a><span data-ttu-id="5d352-135"><a name="2.0.1"/>2.0.1</span><span class="sxs-lookup"><span data-stu-id="5d352-135"><a name="2.0.1"/>2.0.1</span></span>
* <span data-ttu-id="5d352-136">Внесены редакторские правки в комментарии к документации.</span><span class="sxs-lookup"><span data-stu-id="5d352-136">Made editorial changes to documentation comments.</span></span>

### <a name="a-name200200"></a><span data-ttu-id="5d352-137"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="5d352-137"><a name="2.0.0"/>2.0.0</span></span>
* <span data-ttu-id="5d352-138">Добавлена поддержка Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="5d352-138">Added support for Python 3.5.</span></span>
* <span data-ttu-id="5d352-139">Добавлена поддержка пулов подключений с использованием модуля запросов.</span><span class="sxs-lookup"><span data-stu-id="5d352-139">Added support for connection pooling using a requests module.</span></span>
* <span data-ttu-id="5d352-140">Добавлена поддержка согласованности сеанса.</span><span class="sxs-lookup"><span data-stu-id="5d352-140">Added support for session consistency.</span></span>
* <span data-ttu-id="5d352-141">Добавлена поддержка запросов TOP и ORDERBY для секционированных коллекций.</span><span class="sxs-lookup"><span data-stu-id="5d352-141">Added support for TOP/ORDERBY queries for partitioned collections.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="5d352-142"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="5d352-142"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="5d352-143">Добавлена поддержка политики повтора для отрегулированных запросов.</span><span class="sxs-lookup"><span data-stu-id="5d352-143">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="5d352-144">(Отрегулированные запросы порождают исключение слишком высокой частоты запросов с кодом ошибки 429.) По умолчанию при обнаружении кода ошибки 429 Azure Cosmos DB повторяет запрос девять раз, используя интервал retryAfter в заголовке ответа.</span><span class="sxs-lookup"><span data-stu-id="5d352-144">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring the retryAfter time in the response header.</span></span> <span data-ttu-id="5d352-145">Фиксированный интервал повтора теперь можно задать как часть свойства RetryOptions объекта ConnectionPolicy, если требуется игнорировать интервал retryAfter, возвращаемый сервером между повторными попытками.</span><span class="sxs-lookup"><span data-stu-id="5d352-145">A fixed retry interval time can now be set as part of the RetryOptions property on the ConnectionPolicy object if you want to ignore the retryAfter time returned by server between the retries.</span></span> <span data-ttu-id="5d352-146">Теперь Azure Cosmos DB ожидает до 30 секунд, пока запрос регулируется (независимо от количества повторных попыток), и возвращает ответ с кодом ошибки 429.</span><span class="sxs-lookup"><span data-stu-id="5d352-146">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns the response with error code 429.</span></span> <span data-ttu-id="5d352-147">Этот интервал также можно переопределить в свойстве RetryOptions объекта ConnectionPolicy.</span><span class="sxs-lookup"><span data-stu-id="5d352-147">This time can also be overriden in the RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="5d352-148">Теперь Cosmos DB возвращает x-ms-throttle-retry-count и x-ms-throttle-retry-wait-time-ms в заголовке ответа на каждый запрос, чтобы обозначить количество повторных попыток при регулировании и совокупное время ожидания запроса между повторами.</span><span class="sxs-lookup"><span data-stu-id="5d352-148">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as the response headers in every request to denote the throttle retry count and the cummulative time the request waited between the retries.</span></span>
* <span data-ttu-id="5d352-149">Удален класс RetryPolicy и соответствующее свойство (retry_policy), предоставляемое в классе document_client. Вместо них добавлен класс RetryOptions, предоставляющий свойство RetryOptions класса ConnectionPolicy, с помощью которого можно переопределить некоторые параметры повторных попыток по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="5d352-149">Removed the RetryPolicy class and the corresponding property (retry_policy) exposed on the document_client class and instead introduced a RetryOptions class exposing the RetryOptions property on ConnectionPolicy class that can be used to override some of the default retry options.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="5d352-150"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="5d352-150"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="5d352-151">Добавлена поддержка учетных записей базы данных в нескольких регионах.</span><span class="sxs-lookup"><span data-stu-id="5d352-151">Added the support for multi-region database accounts.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="5d352-152"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="5d352-152"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="5d352-153">Добавлена поддержка функции срока жизни для документов.</span><span class="sxs-lookup"><span data-stu-id="5d352-153">Added the support for Time To Live(TTL) feature for documents.</span></span>

### <a name="a-name161161"></a><span data-ttu-id="5d352-154"><a name="1.6.1"/>1.6.1</span><span class="sxs-lookup"><span data-stu-id="5d352-154"><a name="1.6.1"/>1.6.1</span></span>
* <span data-ttu-id="5d352-155">Исправления ошибок, связанных с секционированием на стороне сервера, которые позволяют использовать специальные знаки в пути partitionkey.</span><span class="sxs-lookup"><span data-stu-id="5d352-155">Bug fixes related to server side partitioning to allow special characters in partitionkey path.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="5d352-156"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="5d352-156"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="5d352-157">Реализованы [секционированные коллекции](partition-data.md) и [определяемые пользователем уровни производительности](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="5d352-157">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name150150"></a><span data-ttu-id="5d352-158"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="5d352-158"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="5d352-159">Добавьте сопоставители разделов "Хэш" и "Диапазон" для сегментирования приложений на разделы.</span><span class="sxs-lookup"><span data-stu-id="5d352-159">Add Hash & Range partition resolvers to assist with sharding applications across multiple partitions.</span></span>

### <a name="a-name142142"></a><span data-ttu-id="5d352-160"><a name="1.4.2"/>1.4.2</span><span class="sxs-lookup"><span data-stu-id="5d352-160"><a name="1.4.2"/>1.4.2</span></span>
* <span data-ttu-id="5d352-161">Реализована операция Upsert.</span><span class="sxs-lookup"><span data-stu-id="5d352-161">Implement Upsert.</span></span> <span data-ttu-id="5d352-162">Для поддержки функции Upsert добавлены новые методы UpsertXXX.</span><span class="sxs-lookup"><span data-stu-id="5d352-162">New UpsertXXX methods added to support Upsert feature.</span></span>
* <span data-ttu-id="5d352-163">Реализована маршрутизация на основе идентификатора.</span><span class="sxs-lookup"><span data-stu-id="5d352-163">Implement ID Based Routing.</span></span> <span data-ttu-id="5d352-164">Отсутствуют изменения общего API-интерфейса. Все изменения касаются внутреннего интерфейса.</span><span class="sxs-lookup"><span data-stu-id="5d352-164">No public API changes, all changes internal.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="5d352-165"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="5d352-165"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="5d352-166">Поддержка геопространственного индекса.</span><span class="sxs-lookup"><span data-stu-id="5d352-166">Supports GeoSpatial index.</span></span>
* <span data-ttu-id="5d352-167">Проверка свойств идентификатора для всех ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5d352-167">Validates id property for all resources.</span></span> <span data-ttu-id="5d352-168">Идентификаторы ресурсов не могут содержать знаки ?, /, #, \, или заканчиваться пробелом.</span><span class="sxs-lookup"><span data-stu-id="5d352-168">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="5d352-169">Добавлен новый заголовок "ход выполнения преобразования индекса" в ResourceResponse.</span><span class="sxs-lookup"><span data-stu-id="5d352-169">Adds new header "index transformation progress" to ResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="5d352-170"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="5d352-170"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="5d352-171">Реализована политика индексации версии 2.</span><span class="sxs-lookup"><span data-stu-id="5d352-171">Implements V2 indexing policy.</span></span>

### <a name="a-name101101"></a><span data-ttu-id="5d352-172"><a name="1.0.1"/>1.0.1</span><span class="sxs-lookup"><span data-stu-id="5d352-172"><a name="1.0.1"/>1.0.1</span></span>
* <span data-ttu-id="5d352-173">Добавлена поддержка прокси-подключения.</span><span class="sxs-lookup"><span data-stu-id="5d352-173">Supports proxy connection.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="5d352-174"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="5d352-174"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="5d352-175">Пакет SDK общей доступности.</span><span class="sxs-lookup"><span data-stu-id="5d352-175">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="5d352-176">Даты выпуска и вывода из эксплуатации</span><span class="sxs-lookup"><span data-stu-id="5d352-176">Release & retirement dates</span></span>
<span data-ttu-id="5d352-177">Корпорация Майкрософт отправит уведомление минимум за **12 месяцев** до вывода пакета SDK из эксплуатации, чтобы обеспечить более плавный переход на новую или поддерживаемую версию.</span><span class="sxs-lookup"><span data-stu-id="5d352-177">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order to smooth the transition to a newer/supported version.</span></span>

<span data-ttu-id="5d352-178">Новые функции, возможности и оптимизации добавляются только в текущую версию пакета SDK, поэтому рекомендуется как можно раньше обновлять пакет SDK до последней версии.</span><span class="sxs-lookup"><span data-stu-id="5d352-178">New features and functionality and optimizations are only added to the current SDK, as such it is  recommend that you always upgrade to the latest SDK version as early as possible.</span></span> 

<span data-ttu-id="5d352-179">Любые запросы к Cosmos DB с помощью выведенного из эксплуатации пакета SDK будут отклонены службой.</span><span class="sxs-lookup"><span data-stu-id="5d352-179">Any request to Cosmos DB using a retired SDK will be rejected by the service.</span></span>

> [!WARNING]
> <span data-ttu-id="5d352-180">Поддержка всех версий пакета SDK Azure DocumentDB для Python версии ниже **1.0.0** будет прекращена **29 февраля 2016 года**.</span><span class="sxs-lookup"><span data-stu-id="5d352-180">All versions of the Azure DocumentDB SDK for Python prior to version **1.0.0** will be retired on **February 29, 2016**.</span></span> 
> 
> 

<br/>

| <span data-ttu-id="5d352-181">Версия</span><span class="sxs-lookup"><span data-stu-id="5d352-181">Version</span></span> | <span data-ttu-id="5d352-182">Дата выпуска</span><span class="sxs-lookup"><span data-stu-id="5d352-182">Release Date</span></span> | <span data-ttu-id="5d352-183">Дата вывода</span><span class="sxs-lookup"><span data-stu-id="5d352-183">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="5d352-184">2.2.0</span><span class="sxs-lookup"><span data-stu-id="5d352-184">2.2.0</span></span>](#2.2.0) |<span data-ttu-id="5d352-185">10 мая 2017 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-185">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="5d352-186">2.1.0</span><span class="sxs-lookup"><span data-stu-id="5d352-186">2.1.0</span></span>](#2.1.0) |<span data-ttu-id="5d352-187">1 мая 2017 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-187">May 01, 2017</span></span> |--- |
| [<span data-ttu-id="5d352-188">2.0.1</span><span class="sxs-lookup"><span data-stu-id="5d352-188">2.0.1</span></span>](#2.0.1) |<span data-ttu-id="5d352-189">30 октября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-189">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="5d352-190">2.0.0</span><span class="sxs-lookup"><span data-stu-id="5d352-190">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="5d352-191">29 сентября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-191">September 29, 2016</span></span> |--- |
| [<span data-ttu-id="5d352-192">1.9.0</span><span class="sxs-lookup"><span data-stu-id="5d352-192">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="5d352-193">7 июля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-193">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="5d352-194">1.8.0</span><span class="sxs-lookup"><span data-stu-id="5d352-194">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="5d352-195">14 июня 2016 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-195">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="5d352-196">1.7.0</span><span class="sxs-lookup"><span data-stu-id="5d352-196">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="5d352-197">26 апреля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-197">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="5d352-198">1.6.1</span><span class="sxs-lookup"><span data-stu-id="5d352-198">1.6.1</span></span>](#1.6.1) |<span data-ttu-id="5d352-199">8 апреля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-199">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="5d352-200">1.6.0</span><span class="sxs-lookup"><span data-stu-id="5d352-200">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="5d352-201">29 марта 2016 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-201">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="5d352-202">1.5.0</span><span class="sxs-lookup"><span data-stu-id="5d352-202">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="5d352-203">3 января 2016 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-203">January 03, 2016</span></span> |--- |
| [<span data-ttu-id="5d352-204">1.4.2</span><span class="sxs-lookup"><span data-stu-id="5d352-204">1.4.2</span></span>](#1.4.2) |<span data-ttu-id="5d352-205">6 октября 2015 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-205">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="5d352-206">1.4.1</span><span class="sxs-lookup"><span data-stu-id="5d352-206">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="5d352-207">6 октября 2015 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-207">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="5d352-208">1.2.0</span><span class="sxs-lookup"><span data-stu-id="5d352-208">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="5d352-209">6 августа 2015 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-209">August 06, 2015</span></span> |--- |
| [<span data-ttu-id="5d352-210">1.1.0</span><span class="sxs-lookup"><span data-stu-id="5d352-210">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="5d352-211">9 июля 2015 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-211">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="5d352-212">1.0.1</span><span class="sxs-lookup"><span data-stu-id="5d352-212">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="5d352-213">25 мая 2015 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-213">May 25, 2015</span></span> |--- |
| [<span data-ttu-id="5d352-214">1.0.0</span><span class="sxs-lookup"><span data-stu-id="5d352-214">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="5d352-215">7 апреля 2015 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-215">April 07, 2015</span></span> |--- |
| <span data-ttu-id="5d352-216">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="5d352-216">0.9.4-prelease</span></span> |<span data-ttu-id="5d352-217">14 января 2015 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-217">January 14, 2015</span></span> |<span data-ttu-id="5d352-218">29 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-218">February 29, 2016</span></span> |
| <span data-ttu-id="5d352-219">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="5d352-219">0.9.3-prelease</span></span> |<span data-ttu-id="5d352-220">9 декабря 2014 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-220">December 09, 2014</span></span> |<span data-ttu-id="5d352-221">29 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-221">February 29, 2016</span></span> |
| <span data-ttu-id="5d352-222">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="5d352-222">0.9.2-prelease</span></span> |<span data-ttu-id="5d352-223">25 ноября 2014 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-223">November 25, 2014</span></span> |<span data-ttu-id="5d352-224">29 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-224">February 29, 2016</span></span> |
| <span data-ttu-id="5d352-225">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="5d352-225">0.9.1-prelease</span></span> |<span data-ttu-id="5d352-226">23 сентября 2014 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-226">September 23, 2014</span></span> |<span data-ttu-id="5d352-227">29 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-227">February 29, 2016</span></span> |
| <span data-ttu-id="5d352-228">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="5d352-228">0.9.0-prelease</span></span> |<span data-ttu-id="5d352-229">21 августа 2014 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-229">August 21, 2014</span></span> |<span data-ttu-id="5d352-230">29 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="5d352-230">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="5d352-231">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="5d352-231">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="5d352-232">См. также</span><span class="sxs-lookup"><span data-stu-id="5d352-232">See also</span></span>
<span data-ttu-id="5d352-233">Дополнительные сведения о Cosmos DB см. на странице службы [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="5d352-233">To learn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

