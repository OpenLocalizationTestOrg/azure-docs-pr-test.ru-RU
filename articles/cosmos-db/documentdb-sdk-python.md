---
title: "aaaAzure Cosmos DB Python API пакета SDK ре & сурсов | Документы Microsoft"
description: "Узнайте о hello Python API и SDK, включая даты выхода, даты выбытия и изменения, выполняемые на каждой версии пакета SDK для Python DB Cosmos Azure hello."
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
ms.openlocfilehash: 1a164b72d2bd819de87df0229357b82e2177af2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-python-sdk-release-notes-and-resources"></a><span data-ttu-id="0084f-103">Пакет SDK для Azure Cosmos DB на Python: заметки о выпуске и ресурсы</span><span class="sxs-lookup"><span data-stu-id="0084f-103">Azure Cosmos DB Python SDK: Release notes and resources</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0084f-104">.NET</span><span class="sxs-lookup"><span data-stu-id="0084f-104">.NET</span></span>](documentdb-sdk-dotnet.md)
> * [<span data-ttu-id="0084f-105">Веб-канал изменений в .NET</span><span class="sxs-lookup"><span data-stu-id="0084f-105">.NET Change Feed</span></span>](documentdb-sdk-dotnet-changefeed.md)
> * [<span data-ttu-id="0084f-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="0084f-106">.NET Core</span></span>](documentdb-sdk-dotnet-core.md)
> * [<span data-ttu-id="0084f-107">Node.js</span><span class="sxs-lookup"><span data-stu-id="0084f-107">Node.js</span></span>](documentdb-sdk-node.md)
> * [<span data-ttu-id="0084f-108">Java</span><span class="sxs-lookup"><span data-stu-id="0084f-108">Java</span></span>](documentdb-sdk-java.md)
> * [<span data-ttu-id="0084f-109">Python</span><span class="sxs-lookup"><span data-stu-id="0084f-109">Python</span></span>](documentdb-sdk-python.md)
> * [<span data-ttu-id="0084f-110">REST</span><span class="sxs-lookup"><span data-stu-id="0084f-110">REST</span></span>](https://docs.microsoft.com/rest/api/documentdb/)
> * [<span data-ttu-id="0084f-111">Поставщик ресурсов REST</span><span class="sxs-lookup"><span data-stu-id="0084f-111">REST Resource Provider</span></span>](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [<span data-ttu-id="0084f-112">SQL</span><span class="sxs-lookup"><span data-stu-id="0084f-112">SQL</span></span>](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td><span data-ttu-id="0084f-113">**Скачать пакет SDK**</span><span class="sxs-lookup"><span data-stu-id="0084f-113">**Download SDK**</span></span></td><td>[<span data-ttu-id="0084f-114">PyPI</span><span class="sxs-lookup"><span data-stu-id="0084f-114">PyPI</span></span>](https://pypi.python.org/pypi/pydocumentdb)</td></tr>

<tr><td><span data-ttu-id="0084f-115">**Документация по API**</span><span class="sxs-lookup"><span data-stu-id="0084f-115">**API documentation**</span></span></td><td>[<span data-ttu-id="0084f-116">Справочная документация по API Python</span><span class="sxs-lookup"><span data-stu-id="0084f-116">Python API reference documentation</span></span>](http://azure.github.io/azure-documentdb-python/api/pydocumentdb.html)</td></tr>

<tr><td><span data-ttu-id="0084f-117">**Инструкции по установке пакета SDK**</span><span class="sxs-lookup"><span data-stu-id="0084f-117">**SDK installation instructions**</span></span></td><td>[<span data-ttu-id="0084f-118">Инструкции по установке пакета SDK для Python</span><span class="sxs-lookup"><span data-stu-id="0084f-118">Python SDK installation instructions</span></span>](http://azure.github.io/azure-documentdb-python/)</td></tr>

<tr><td><span data-ttu-id="0084f-119">**Contribute tooSDK**</span><span class="sxs-lookup"><span data-stu-id="0084f-119">**Contribute tooSDK**</span></span></td><td>[<span data-ttu-id="0084f-120">GitHub</span><span class="sxs-lookup"><span data-stu-id="0084f-120">GitHub</span></span>](https://github.com/Azure/azure-documentdb-python)</td></tr>

<tr><td><span data-ttu-id="0084f-121">**Начало работы**</span><span class="sxs-lookup"><span data-stu-id="0084f-121">**Get started**</span></span></td><td>[<span data-ttu-id="0084f-122">Начало работы с Python SDK hello</span><span class="sxs-lookup"><span data-stu-id="0084f-122">Get started with hello Python SDK</span></span>](documentdb-python-application.md)</td></tr>

<tr><td><span data-ttu-id="0084f-123">**Текущая поддерживаемая платформа**</span><span class="sxs-lookup"><span data-stu-id="0084f-123">**Current supported platform**</span></span></td><td><span data-ttu-id="0084f-124">[Python 2.7](https://www.python.org/downloads/) и [Python 3.5](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="0084f-124">[Python 2.7](https://www.python.org/downloads/) and [Python 3.5](https://www.python.org/downloads/)</span></span></td></tr>
</table></br>

## <a name="release-notes"></a><span data-ttu-id="0084f-125">Заметки о выпуске</span><span class="sxs-lookup"><span data-stu-id="0084f-125">Release notes</span></span>
### <a name="a-name220220"></a><span data-ttu-id="0084f-126"><a name="2.2.0"/>2.2.0</span><span class="sxs-lookup"><span data-stu-id="0084f-126"><a name="2.2.0"/>2.2.0</span></span>
* <span data-ttu-id="0084f-127">Добавлена поддержка нового уровня согласованности с именем ConsistentPrefix.</span><span class="sxs-lookup"><span data-stu-id="0084f-127">Added support for a new consistency level called ConsistentPrefix.</span></span>


### <a name="a-name210210"></a><span data-ttu-id="0084f-128"><a name="2.1.0"/>2.1.0</span><span class="sxs-lookup"><span data-stu-id="0084f-128"><a name="2.1.0"/>2.1.0</span></span>
* <span data-ttu-id="0084f-129">Добавлена поддержка статистических запросов (COUNT, MIN, MAX, SUM и AVG).</span><span class="sxs-lookup"><span data-stu-id="0084f-129">Added support for aggregation queries (COUNT, MIN, MAX, SUM, and AVG).</span></span>
* <span data-ttu-id="0084f-130">Добавлена возможность отключения проверки SSL при работе с эмулятором Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0084f-130">Added an option for disabling SSL verification when running against Cosmos DB Emulator.</span></span>
* <span data-ttu-id="0084f-131">Удалено ограничение hello из зависимых запросов модуля toobe точно 2.10.0.</span><span class="sxs-lookup"><span data-stu-id="0084f-131">Removed hello restriction of dependent requests module toobe exactly 2.10.0.</span></span>
* <span data-ttu-id="0084f-132">Понижено минимальная пропускная способность для секционированных коллекций из 10,100 единиц Запросов в секунду too2500 единиц Запросов в секунду.</span><span class="sxs-lookup"><span data-stu-id="0084f-132">Lowered minimum throughput on partitioned collections from 10,100 RU/s too2500 RU/s.</span></span>
* <span data-ttu-id="0084f-133">Добавлена поддержка включения ведения журнала сценариев во время выполнения хранимой процедуры.</span><span class="sxs-lookup"><span data-stu-id="0084f-133">Added support for enabling script logging during stored procedure execution.</span></span>
* <span data-ttu-id="0084f-134">Увеличить версию API-интерфейса REST один слишком "2017 г-01-19' в этом выпуске.</span><span class="sxs-lookup"><span data-stu-id="0084f-134">REST API version bumped too'2017-01-19' with this release.</span></span>

### <a name="a-name201201"></a><span data-ttu-id="0084f-135"><a name="2.0.1"/>2.0.1</span><span class="sxs-lookup"><span data-stu-id="0084f-135"><a name="2.0.1"/>2.0.1</span></span>
* <span data-ttu-id="0084f-136">Внесены редакторские изменения toodocumentation комментарии.</span><span class="sxs-lookup"><span data-stu-id="0084f-136">Made editorial changes toodocumentation comments.</span></span>

### <a name="a-name200200"></a><span data-ttu-id="0084f-137"><a name="2.0.0"/>2.0.0</span><span class="sxs-lookup"><span data-stu-id="0084f-137"><a name="2.0.0"/>2.0.0</span></span>
* <span data-ttu-id="0084f-138">Добавлена поддержка Python 3.5.</span><span class="sxs-lookup"><span data-stu-id="0084f-138">Added support for Python 3.5.</span></span>
* <span data-ttu-id="0084f-139">Добавлена поддержка пулов подключений с использованием модуля запросов.</span><span class="sxs-lookup"><span data-stu-id="0084f-139">Added support for connection pooling using a requests module.</span></span>
* <span data-ttu-id="0084f-140">Добавлена поддержка согласованности сеанса.</span><span class="sxs-lookup"><span data-stu-id="0084f-140">Added support for session consistency.</span></span>
* <span data-ttu-id="0084f-141">Добавлена поддержка запросов TOP и ORDERBY для секционированных коллекций.</span><span class="sxs-lookup"><span data-stu-id="0084f-141">Added support for TOP/ORDERBY queries for partitioned collections.</span></span>

### <a name="a-name190190"></a><span data-ttu-id="0084f-142"><a name="1.9.0"/>1.9.0</span><span class="sxs-lookup"><span data-stu-id="0084f-142"><a name="1.9.0"/>1.9.0</span></span>
* <span data-ttu-id="0084f-143">Добавлена поддержка политики повтора для отрегулированных запросов.</span><span class="sxs-lookup"><span data-stu-id="0084f-143">Added retry policy support for throttled requests.</span></span> <span data-ttu-id="0084f-144">(Отрегулированные запросы порождают исключение слишком высокой частоты запросов с кодом ошибки 429.) По умолчанию Azure Cosmos DB повторяет девяти раз для каждого запроса при обнаружении код ошибки 429, учитывая время retryAfter hello в заголовке ответа hello.</span><span class="sxs-lookup"><span data-stu-id="0084f-144">(Throttled requests receive a request rate too large exception, error code 429.) By default, Azure Cosmos DB retries nine times for each request when error code 429 is encountered, honoring hello retryAfter time in hello response header.</span></span> <span data-ttu-id="0084f-145">Интервал повторных попыток основных теперь настраивается как часть hello свойство RetryOptions hello объекта ConnectionPolicy время tooignore hello retryAfter сервер вернул между повторными попытками hello.</span><span class="sxs-lookup"><span data-stu-id="0084f-145">A fixed retry interval time can now be set as part of hello RetryOptions property on hello ConnectionPolicy object if you want tooignore hello retryAfter time returned by server between hello retries.</span></span> <span data-ttu-id="0084f-146">Теперь Azure Cosmos DB ожидает в течение не более 30 секунд для каждого запроса, который регулируется (независимо от того, число повторных попыток) и возвращает hello ответ с кодом ошибки 429.</span><span class="sxs-lookup"><span data-stu-id="0084f-146">Azure Cosmos DB now waits for a maximum of 30 seconds for each request that is being throttled (irrespective of retry count) and returns hello response with error code 429.</span></span> <span data-ttu-id="0084f-147">Это время также может быть переопределен в hello RetryOptions свойство ConnectionPolicy объекта.</span><span class="sxs-lookup"><span data-stu-id="0084f-147">This time can also be overriden in hello RetryOptions property on ConnectionPolicy object.</span></span>
* <span data-ttu-id="0084f-148">Cosmos DB теперь возвращает x-ms регулирования число повторных попыток и x-ms-throttle-retry-wait-time-ms как заголовки ответа hello в каждый интервал повтора запроса toodenote hello count и hello cummulative время повтора запроса hello ожидания между повторными попытками hello.</span><span class="sxs-lookup"><span data-stu-id="0084f-148">Cosmos DB now returns x-ms-throttle-retry-count and x-ms-throttle-retry-wait-time-ms as hello response headers in every request toodenote hello throttle retry count and hello cummulative time hello request waited between hello retries.</span></span>
* <span data-ttu-id="0084f-149">Класс RetryPolicy удален hello и соответствующего свойства hello (retry_policy) для класса document_client hello и вместо этого реализован RetryOptions класса, предоставляющего свойства RetryOptions hello ConnectionPolicy класс, который может быть используется toooverride по умолчанию hello некоторые параметры повторных попыток.</span><span class="sxs-lookup"><span data-stu-id="0084f-149">Removed hello RetryPolicy class and hello corresponding property (retry_policy) exposed on hello document_client class and instead introduced a RetryOptions class exposing hello RetryOptions property on ConnectionPolicy class that can be used toooverride some of hello default retry options.</span></span>

### <a name="a-name180180"></a><span data-ttu-id="0084f-150"><a name="1.8.0"/>1.8.0</span><span class="sxs-lookup"><span data-stu-id="0084f-150"><a name="1.8.0"/>1.8.0</span></span>
* <span data-ttu-id="0084f-151">Hello добавлена поддержка учетные записи базы данных с поддержкой нескольких регионов.</span><span class="sxs-lookup"><span data-stu-id="0084f-151">Added hello support for multi-region database accounts.</span></span>

### <a name="a-name170170"></a><span data-ttu-id="0084f-152"><a name="1.7.0"/>1.7.0</span><span class="sxs-lookup"><span data-stu-id="0084f-152"><a name="1.7.0"/>1.7.0</span></span>
* <span data-ttu-id="0084f-153">Hello добавлена поддержка функция tooLive(TTL) времени для документов.</span><span class="sxs-lookup"><span data-stu-id="0084f-153">Added hello support for Time tooLive(TTL) feature for documents.</span></span>

### <a name="a-name161161"></a><span data-ttu-id="0084f-154"><a name="1.6.1"/>1.6.1</span><span class="sxs-lookup"><span data-stu-id="0084f-154"><a name="1.6.1"/>1.6.1</span></span>
* <span data-ttu-id="0084f-155">Исправления ошибок, связанных с tooserver стороне секционирование tooallow специальные символы в пути partitionkey.</span><span class="sxs-lookup"><span data-stu-id="0084f-155">Bug fixes related tooserver side partitioning tooallow special characters in partitionkey path.</span></span>

### <a name="a-name160160"></a><span data-ttu-id="0084f-156"><a name="1.6.0"/>1.6.0</span><span class="sxs-lookup"><span data-stu-id="0084f-156"><a name="1.6.0"/>1.6.0</span></span>
* <span data-ttu-id="0084f-157">Реализованы [секционированные коллекции](partition-data.md) и [определяемые пользователем уровни производительности](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="0084f-157">Implemented [partitioned collections](partition-data.md) and [user-defined performance levels](performance-levels.md).</span></span> 

### <a name="a-name150150"></a><span data-ttu-id="0084f-158"><a name="1.5.0"/>1.5.0</span><span class="sxs-lookup"><span data-stu-id="0084f-158"><a name="1.5.0"/>1.5.0</span></span>
* <span data-ttu-id="0084f-159">Добавить диапазон & хеширования tooassist распознаватели секции с приложениями сегментирования по нескольким секциям.</span><span class="sxs-lookup"><span data-stu-id="0084f-159">Add Hash & Range partition resolvers tooassist with sharding applications across multiple partitions.</span></span>

### <a name="a-name142142"></a><span data-ttu-id="0084f-160"><a name="1.4.2"/>1.4.2</span><span class="sxs-lookup"><span data-stu-id="0084f-160"><a name="1.4.2"/>1.4.2</span></span>
* <span data-ttu-id="0084f-161">Реализована операция Upsert.</span><span class="sxs-lookup"><span data-stu-id="0084f-161">Implement Upsert.</span></span> <span data-ttu-id="0084f-162">Новые методы UpsertXXX добавлена функция toosupport Upsert.</span><span class="sxs-lookup"><span data-stu-id="0084f-162">New UpsertXXX methods added toosupport Upsert feature.</span></span>
* <span data-ttu-id="0084f-163">Реализована маршрутизация на основе идентификатора.</span><span class="sxs-lookup"><span data-stu-id="0084f-163">Implement ID Based Routing.</span></span> <span data-ttu-id="0084f-164">Отсутствуют изменения общего API-интерфейса. Все изменения касаются внутреннего интерфейса.</span><span class="sxs-lookup"><span data-stu-id="0084f-164">No public API changes, all changes internal.</span></span>

### <a name="a-name120120"></a><span data-ttu-id="0084f-165"><a name="1.2.0"/>1.2.0</span><span class="sxs-lookup"><span data-stu-id="0084f-165"><a name="1.2.0"/>1.2.0</span></span>
* <span data-ttu-id="0084f-166">Поддержка геопространственного индекса.</span><span class="sxs-lookup"><span data-stu-id="0084f-166">Supports GeoSpatial index.</span></span>
* <span data-ttu-id="0084f-167">Проверка свойств идентификатора для всех ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0084f-167">Validates id property for all resources.</span></span> <span data-ttu-id="0084f-168">Идентификаторы ресурсов не могут содержать знаки ?, /, #, \, или заканчиваться пробелом.</span><span class="sxs-lookup"><span data-stu-id="0084f-168">Ids for resources cannot contain ?, /, #, \, characters or end with a space.</span></span>
* <span data-ttu-id="0084f-169">Добавляет новый tooResourceResponse заголовок «выполняется преобразование индекса».</span><span class="sxs-lookup"><span data-stu-id="0084f-169">Adds new header "index transformation progress" tooResourceResponse.</span></span>

### <a name="a-name110110"></a><span data-ttu-id="0084f-170"><a name="1.1.0"/>1.1.0</span><span class="sxs-lookup"><span data-stu-id="0084f-170"><a name="1.1.0"/>1.1.0</span></span>
* <span data-ttu-id="0084f-171">Реализована политика индексации версии 2.</span><span class="sxs-lookup"><span data-stu-id="0084f-171">Implements V2 indexing policy.</span></span>

### <a name="a-name101101"></a><span data-ttu-id="0084f-172"><a name="1.0.1"/>1.0.1</span><span class="sxs-lookup"><span data-stu-id="0084f-172"><a name="1.0.1"/>1.0.1</span></span>
* <span data-ttu-id="0084f-173">Добавлена поддержка прокси-подключения.</span><span class="sxs-lookup"><span data-stu-id="0084f-173">Supports proxy connection.</span></span>

### <a name="a-name100100"></a><span data-ttu-id="0084f-174"><a name="1.0.0"/>1.0.0</span><span class="sxs-lookup"><span data-stu-id="0084f-174"><a name="1.0.0"/>1.0.0</span></span>
* <span data-ttu-id="0084f-175">Пакет SDK общей доступности.</span><span class="sxs-lookup"><span data-stu-id="0084f-175">GA SDK.</span></span>

## <a name="release--retirement-dates"></a><span data-ttu-id="0084f-176">Даты выпуска и вывода из эксплуатации</span><span class="sxs-lookup"><span data-stu-id="0084f-176">Release & retirement dates</span></span>
<span data-ttu-id="0084f-177">Корпорация Майкрософт предоставляет уведомления по крайней мере **12 месяцев** до снятия с учета в новой/поддерживаемой версии для hello перехода порядок toosmooth tooa пакет SDK.</span><span class="sxs-lookup"><span data-stu-id="0084f-177">Microsoft will provide notification at least **12 months** in advance of retiring an SDK in order toosmooth hello transition tooa newer/supported version.</span></span>

<span data-ttu-id="0084f-178">Новые функции и функциональные возможности и оптимизацию добавляются только toohello текущего пакета SDK, поэтому рекомендуется как можно раньше, вы всегда обновления toohello последнюю версию пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="0084f-178">New features and functionality and optimizations are only added toohello current SDK, as such it is  recommend that you always upgrade toohello latest SDK version as early as possible.</span></span> 

<span data-ttu-id="0084f-179">Любой запрос tooCosmos базу данных, используя удалено SDK будут отклонены службой hello.</span><span class="sxs-lookup"><span data-stu-id="0084f-179">Any request tooCosmos DB using a retired SDK will be rejected by hello service.</span></span>

> [!WARNING]
> <span data-ttu-id="0084f-180">Все версии hello Azure DocumentDB SDK для Python предыдущих tooversion **1.0.0** будет удалено на **29 февраля 2016 г.**.</span><span class="sxs-lookup"><span data-stu-id="0084f-180">All versions of hello Azure DocumentDB SDK for Python prior tooversion **1.0.0** will be retired on **February 29, 2016**.</span></span> 
> 
> 

<br/>

| <span data-ttu-id="0084f-181">Version (версия)</span><span class="sxs-lookup"><span data-stu-id="0084f-181">Version</span></span> | <span data-ttu-id="0084f-182">Дата выпуска</span><span class="sxs-lookup"><span data-stu-id="0084f-182">Release Date</span></span> | <span data-ttu-id="0084f-183">Дата вывода</span><span class="sxs-lookup"><span data-stu-id="0084f-183">Retirement Date</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="0084f-184">2.2.0</span><span class="sxs-lookup"><span data-stu-id="0084f-184">2.2.0</span></span>](#2.2.0) |<span data-ttu-id="0084f-185">10 мая 2017 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-185">May 10, 2017</span></span> |--- |
| [<span data-ttu-id="0084f-186">2.1.0</span><span class="sxs-lookup"><span data-stu-id="0084f-186">2.1.0</span></span>](#2.1.0) |<span data-ttu-id="0084f-187">1 мая 2017 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-187">May 01, 2017</span></span> |--- |
| [<span data-ttu-id="0084f-188">2.0.1</span><span class="sxs-lookup"><span data-stu-id="0084f-188">2.0.1</span></span>](#2.0.1) |<span data-ttu-id="0084f-189">30 октября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-189">October 30, 2016</span></span> |--- |
| [<span data-ttu-id="0084f-190">2.0.0</span><span class="sxs-lookup"><span data-stu-id="0084f-190">2.0.0</span></span>](#2.0.0) |<span data-ttu-id="0084f-191">29 сентября 2016 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-191">September 29, 2016</span></span> |--- |
| [<span data-ttu-id="0084f-192">1.9.0</span><span class="sxs-lookup"><span data-stu-id="0084f-192">1.9.0</span></span>](#1.9.0) |<span data-ttu-id="0084f-193">7 июля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-193">July 07, 2016</span></span> |--- |
| [<span data-ttu-id="0084f-194">1.8.0</span><span class="sxs-lookup"><span data-stu-id="0084f-194">1.8.0</span></span>](#1.8.0) |<span data-ttu-id="0084f-195">14 июня 2016 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-195">June 14, 2016</span></span> |--- |
| [<span data-ttu-id="0084f-196">1.7.0</span><span class="sxs-lookup"><span data-stu-id="0084f-196">1.7.0</span></span>](#1.7.0) |<span data-ttu-id="0084f-197">26 апреля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-197">April 26, 2016</span></span> |--- |
| [<span data-ttu-id="0084f-198">1.6.1</span><span class="sxs-lookup"><span data-stu-id="0084f-198">1.6.1</span></span>](#1.6.1) |<span data-ttu-id="0084f-199">8 апреля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-199">April 08, 2016</span></span> |--- |
| [<span data-ttu-id="0084f-200">1.6.0</span><span class="sxs-lookup"><span data-stu-id="0084f-200">1.6.0</span></span>](#1.6.0) |<span data-ttu-id="0084f-201">29 марта 2016 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-201">March 29, 2016</span></span> |--- |
| [<span data-ttu-id="0084f-202">1.5.0</span><span class="sxs-lookup"><span data-stu-id="0084f-202">1.5.0</span></span>](#1.5.0) |<span data-ttu-id="0084f-203">3 января 2016 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-203">January 03, 2016</span></span> |--- |
| [<span data-ttu-id="0084f-204">1.4.2</span><span class="sxs-lookup"><span data-stu-id="0084f-204">1.4.2</span></span>](#1.4.2) |<span data-ttu-id="0084f-205">6 октября 2015 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-205">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="0084f-206">1.4.1</span><span class="sxs-lookup"><span data-stu-id="0084f-206">1.4.1</span></span>](#1.4.1) |<span data-ttu-id="0084f-207">6 октября 2015 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-207">October 06, 2015</span></span> |--- |
| [<span data-ttu-id="0084f-208">1.2.0</span><span class="sxs-lookup"><span data-stu-id="0084f-208">1.2.0</span></span>](#1.2.0) |<span data-ttu-id="0084f-209">6 августа 2015 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-209">August 06, 2015</span></span> |--- |
| [<span data-ttu-id="0084f-210">1.1.0</span><span class="sxs-lookup"><span data-stu-id="0084f-210">1.1.0</span></span>](#1.1.0) |<span data-ttu-id="0084f-211">9 июля 2015 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-211">July 09, 2015</span></span> |--- |
| [<span data-ttu-id="0084f-212">1.0.1</span><span class="sxs-lookup"><span data-stu-id="0084f-212">1.0.1</span></span>](#1.0.1) |<span data-ttu-id="0084f-213">25 мая 2015 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-213">May 25, 2015</span></span> |--- |
| [<span data-ttu-id="0084f-214">1.0.0</span><span class="sxs-lookup"><span data-stu-id="0084f-214">1.0.0</span></span>](#1.0.0) |<span data-ttu-id="0084f-215">7 апреля 2015 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-215">April 07, 2015</span></span> |--- |
| <span data-ttu-id="0084f-216">0.9.4-prelease</span><span class="sxs-lookup"><span data-stu-id="0084f-216">0.9.4-prelease</span></span> |<span data-ttu-id="0084f-217">14 января 2015 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-217">January 14, 2015</span></span> |<span data-ttu-id="0084f-218">29 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-218">February 29, 2016</span></span> |
| <span data-ttu-id="0084f-219">0.9.3-prelease</span><span class="sxs-lookup"><span data-stu-id="0084f-219">0.9.3-prelease</span></span> |<span data-ttu-id="0084f-220">9 декабря 2014 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-220">December 09, 2014</span></span> |<span data-ttu-id="0084f-221">29 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-221">February 29, 2016</span></span> |
| <span data-ttu-id="0084f-222">0.9.2-prelease</span><span class="sxs-lookup"><span data-stu-id="0084f-222">0.9.2-prelease</span></span> |<span data-ttu-id="0084f-223">25 ноября 2014 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-223">November 25, 2014</span></span> |<span data-ttu-id="0084f-224">29 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-224">February 29, 2016</span></span> |
| <span data-ttu-id="0084f-225">0.9.1-prelease</span><span class="sxs-lookup"><span data-stu-id="0084f-225">0.9.1-prelease</span></span> |<span data-ttu-id="0084f-226">23 сентября 2014 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-226">September 23, 2014</span></span> |<span data-ttu-id="0084f-227">29 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-227">February 29, 2016</span></span> |
| <span data-ttu-id="0084f-228">0.9.0-prelease</span><span class="sxs-lookup"><span data-stu-id="0084f-228">0.9.0-prelease</span></span> |<span data-ttu-id="0084f-229">21 августа 2014 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-229">August 21, 2014</span></span> |<span data-ttu-id="0084f-230">29 февраля 2016 г.</span><span class="sxs-lookup"><span data-stu-id="0084f-230">February 29, 2016</span></span> |

## <a name="faq"></a><span data-ttu-id="0084f-231">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="0084f-231">FAQ</span></span>
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a><span data-ttu-id="0084f-232">См. также</span><span class="sxs-lookup"><span data-stu-id="0084f-232">See also</span></span>
<span data-ttu-id="0084f-233">toolearn Дополнительные сведения о Cosmos DB. в разделе [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) страницы службы.</span><span class="sxs-lookup"><span data-stu-id="0084f-233">toolearn more about Cosmos DB, see [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service page.</span></span> 

