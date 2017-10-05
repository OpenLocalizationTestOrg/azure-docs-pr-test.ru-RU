---
title: "Единицы запросов в минуту в базе данных Azure Cosmos DB | Документация Майкрософт"
description: "Сведения о снижении затрат за счет использования единиц запросов в минуту."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 72d60d5656ad664e42a848fc9b372cb09e49b888
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a><span data-ttu-id="29dc5-103">Единицы запросов в минуту в базе данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="29dc5-103">Request units per minute in Azure Cosmos DB</span></span>

<span data-ttu-id="29dc5-104">База данных Azure Cosmos DB позволяет обеспечивать высокую и прогнозируемую производительность, а также легко масштабируется по мере расширения вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="29dc5-104">Azure Cosmos DB is designed to help you achieve a fast, predictable performance and scale seamlessly along with your application’s growth.</span></span> <span data-ttu-id="29dc5-105">В контейнере базы данных Cosmos DB пропускную способность можно подготавливать с ежесекундной или ежеминутной степенью детализации.</span><span class="sxs-lookup"><span data-stu-id="29dc5-105">You can provision throughput on a Cosmos DB container at both, per-second and at per-minute (RU/m) granularities.</span></span> <span data-ttu-id="29dc5-106">Пропускная способность с ежеминутной степенью детализации помогает управлять пиковыми нагрузками, возникающими при ежесекундной степени детализации.</span><span class="sxs-lookup"><span data-stu-id="29dc5-106">The provisioned throughput at per-minute granularity is used to manage unexpected spikes in the workload occurring at a per-second granularity.</span></span> 

<span data-ttu-id="29dc5-107">В этой статье содержатся общие сведения о подготовке и принципах действия единиц запросов в минуту.</span><span class="sxs-lookup"><span data-stu-id="29dc5-107">This article provides an overview of how the provisioning of Request Unit per Minute (RU/m) works.</span></span> <span data-ttu-id="29dc5-108">Эти сведения помогут обеспечить прогнозируемую производительность в случае непредсказуемых событий (особенно если нужно выполнить анализ на основе операционных данных) и пиковых рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="29dc5-108">The goal in mind with provisioning of RU/m is to provide a predictable performance around unpredictable needs (especially if you need to run analytics on top of your operational data) and spiky workloads.</span></span> <span data-ttu-id="29dc5-109">Нам нужно, чтобы наши клиенты использовали больший объем пропускной способности, нежели они подготавливают. Это позволит выполнять масштабирование быстро, не беспокоясь о последствиях.</span><span class="sxs-lookup"><span data-stu-id="29dc5-109">We want to have our customers consume more the throughput they provision so they can scale quickly with peace of mind.</span></span>

<span data-ttu-id="29dc5-110">После прочтения этой статьи вы сможете ответить на следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="29dc5-110">After reading this article, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="29dc5-111">Как работают единицы запросов в минуту?</span><span class="sxs-lookup"><span data-stu-id="29dc5-111">How does a Request Unit per Minute work?</span></span>
* <span data-ttu-id="29dc5-112">В чем разница между единицами запросов с ежесекундной и ежеминутной степенью детализации?</span><span class="sxs-lookup"><span data-stu-id="29dc5-112">What is the difference between Request Unit per Minute and Request Unit per Second?</span></span>
* <span data-ttu-id="29dc5-113">Как подготовить единицы запросов в минуту?</span><span class="sxs-lookup"><span data-stu-id="29dc5-113">How to provision RU/m?</span></span>
* <span data-ttu-id="29dc5-114">В каких ситуациях следует подготавливать единицы запросов с ежеминутной степенью детализации?</span><span class="sxs-lookup"><span data-stu-id="29dc5-114">Under which scenario shall I consider provisioning Request Unit per Minute?</span></span>
* <span data-ttu-id="29dc5-115">Как оптимизировать производительность и затраты, используя метрики портала?</span><span class="sxs-lookup"><span data-stu-id="29dc5-115">How to use the portal metrics to optimize my cost and performance?</span></span>
* <span data-ttu-id="29dc5-116">Какие типы запросов используют единицы запросов с ежеминутной степенью детализации?</span><span class="sxs-lookup"><span data-stu-id="29dc5-116">Define which type of request can consume your RU/m budget?</span></span>

## <a name="provisioning-request-units-per-minute-rum"></a><span data-ttu-id="29dc5-117">Подготовка единиц запросов в минуту</span><span class="sxs-lookup"><span data-stu-id="29dc5-117">Provisioning request units per minute (RU/m)</span></span>

<span data-ttu-id="29dc5-118">База данных Azure Cosmos DB со второй степенью детализации предоставляет гарантию выполнения запроса с небольшой задержкой, если в течение этой секунды пропускная способность не превысила указанную емкость.</span><span class="sxs-lookup"><span data-stu-id="29dc5-118">When you provision Azure Cosmos DB at the second granularity (RU/s), you get the guarantee that your request succeeds at a low latency if your throughput has not exceeded the capacity provisioned within that second.</span></span> <span data-ttu-id="29dc5-119">При ежеминутной степени детализации время выполнения запроса не должно превышать одну минуту.</span><span class="sxs-lookup"><span data-stu-id="29dc5-119">With RU/m, the granularity is at the minute with the guarantee that your request succeeds within that minute.</span></span> <span data-ttu-id="29dc5-120">В системах с частыми скачками нагрузки это позволяет прогнозировать и планировать производительность.</span><span class="sxs-lookup"><span data-stu-id="29dc5-120">Compared to bursting systems, we make sure that the performance you get is predictable and you can plan on it.</span></span>

<span data-ttu-id="29dc5-121">Единицы запросов в минуту работают следующим образом:</span><span class="sxs-lookup"><span data-stu-id="29dc5-121">The way per minute provisioning works is simple:</span></span>

* <span data-ttu-id="29dc5-122">Плата за единицы запросов в минуту выставляется каждый час помимо платы за единицы запросов в секунду.</span><span class="sxs-lookup"><span data-stu-id="29dc5-122">RU/m is billed hourly and in addition to RU/s.</span></span> <span data-ttu-id="29dc5-123">Дополнительные сведения см. на [странице цен на базу данных Azure Cosmos DB](https://aka.ms/acdbpricing).</span><span class="sxs-lookup"><span data-stu-id="29dc5-123">For more details, please visit Azure Cosmos DB [pricing page](https://aka.ms/acdbpricing).</span></span>
* <span data-ttu-id="29dc5-124">Единицы запросов в минуту можно включить на уровне коллекции.</span><span class="sxs-lookup"><span data-stu-id="29dc5-124">RU/m can be enabled at collection level.</span></span> <span data-ttu-id="29dc5-125">Это можно сделать с помощью пакетов SDK (Node.js, Java или .NET) или на портале (также включает рабочие нагрузки API MongoDB).</span><span class="sxs-lookup"><span data-stu-id="29dc5-125">That can be done through the SDKs (Node.js, Java, or .Net) or through the portal (also include MongoDB API workloads)</span></span>
* <span data-ttu-id="29dc5-126">При подготовке 100 единиц запросов в секунду вы также получаете 1000 единиц запросов в минуту (соотношение составляет 1 к 10).</span><span class="sxs-lookup"><span data-stu-id="29dc5-126">When RU/m is enabled, for every 100 RU/s provisioned, you also get 1,000 RU/m provisioned (the ratio is 10x)</span></span>
* <span data-ttu-id="29dc5-127">Использование единиц запросов в минуту начинается только при превышении квоты на единицы запросов в секунду в течение заданной секунды.</span><span class="sxs-lookup"><span data-stu-id="29dc5-127">At a given second, a request unit consumes your RU/m provisioning only if you have exceeded your per second provisioning within that second</span></span>
* <span data-ttu-id="29dc5-128">По завершении 60-секундного периода (время в формате UTC) количество единиц запросов в минуту восстанавливается.</span><span class="sxs-lookup"><span data-stu-id="29dc5-128">Once the 60-second period (UTC) ends, the per minute provisioning is refilled</span></span>
* <span data-ttu-id="29dc5-129">Единицы запросов в минуту можно использовать только в коллекциях с максимум 5000 единицами запросов в секунду на секцию.</span><span class="sxs-lookup"><span data-stu-id="29dc5-129">RU/m can be enabled only for collections with a maximum provisioning of 5,000 RU/s per partition.</span></span> <span data-ttu-id="29dc5-130">При масштабировании пропускной способности и достижении высокого уровня подготовки на секцию вы получите предупреждающее сообщение.</span><span class="sxs-lookup"><span data-stu-id="29dc5-130">If you scale your throughput needs and have such a high level of provisioning per partition, you will get a warning message</span></span>

<span data-ttu-id="29dc5-131">Ниже приведен конкретный пример, где пользователь может подготовить 10 000 единиц запросов в секунду и 100 000 единиц запросов в минуту, что позволяет сократить расходы на 73 %, не подготавливая дополнительные единицы запросов в секунду для пиковых нагрузок (около 50 000 единиц), которые могут произойти в коллекции с таким же числом единиц запросов в течение 90 секунд.</span><span class="sxs-lookup"><span data-stu-id="29dc5-131">Below is a concrete example, in which a customer can provision 10kRU/s with 100kRU/m, saving 73% in cost against provisioning for peak (at 50kRU/sec) through a 90-second period on a collection that has 10,000 RU/s and 100,000 RU/m provisioned:</span></span>

* <span data-ttu-id="29dc5-132">1 секунда. Резерв единиц запросов в минуту составляет 100 000.</span><span class="sxs-lookup"><span data-stu-id="29dc5-132">1st second: The RU/m budget is set at 100,000</span></span>
* <span data-ttu-id="29dc5-133">3 секунда. В течение этой секунды было использовано 11 010 единиц запросов, на 1010 единиц больше установленного уровня подготовки в секунду.</span><span class="sxs-lookup"><span data-stu-id="29dc5-133">3rd second: During that second the consumption of Request Unit was 11,010 RUs, 1,010 RUs above the RU/s provisioning.</span></span> <span data-ttu-id="29dc5-134">Таким образом, 1010 единиц запросов было вычтено из резерва единиц запросов в минуту.</span><span class="sxs-lookup"><span data-stu-id="29dc5-134">Therefore, 1,010 RUs are deducted from the RU/m budget.</span></span> <span data-ttu-id="29dc5-135">Для следующих 57 секунд доступно 98 990 единиц запросов, которые вычитаются из резерва единиц запросов в минуту.</span><span class="sxs-lookup"><span data-stu-id="29dc5-135">98,990 RUs are available for the next 57 seconds in the RU/m budget</span></span>
* <span data-ttu-id="29dc5-136">29 секунда. В течение этой секунды произошел большой скачок нагрузки (в 4 раза больше подготовленного числа единиц запросов в секунду) и было использовано 46 920 единиц запросов.</span><span class="sxs-lookup"><span data-stu-id="29dc5-136">29th second: During that second, a large spike happened (>4x higher than provisioning per second) and the consumption of Request Unit was 46,920 RUs.</span></span> <span data-ttu-id="29dc5-137">36 920 единиц запросов были вычтены из резерва единиц запросов в минуту, число которых снизилось с 92 323 (28 секунда) до 55 403 единиц запросов (29 секунда).</span><span class="sxs-lookup"><span data-stu-id="29dc5-137">36,920 RUs are deducted from the RU/m budget that dropped from 92,323 RUs (28th second) to 55,403 RUs (29th second)</span></span>
* <span data-ttu-id="29dc5-138">61 секунда. Резерв единиц запросов в секунду снова составляет 100 000.</span><span class="sxs-lookup"><span data-stu-id="29dc5-138">61st second: RU/m budget is set back to 100,000 RUs.</span></span>
 
![График потребления и подготовки базы данных Azure Cosmos DB](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a><span data-ttu-id="29dc5-140">Указание количества единиц запросов с учетом резерва единиц запросов в минуту</span><span class="sxs-lookup"><span data-stu-id="29dc5-140">Specifying request unit capacity with RU/m</span></span>

<span data-ttu-id="29dc5-141">При создании коллекции базы данных Azure Cosmos DB необходимо указать количество единиц запросов в секунду, которое вы хотите зарезервировать.</span><span class="sxs-lookup"><span data-stu-id="29dc5-141">When creating an Azure Cosmos DB collection, you specify the number of request units per second (RU per second) you want reserved for the collection.</span></span> <span data-ttu-id="29dc5-142">Вы также можете добавить единицы запросов в минуту.</span><span class="sxs-lookup"><span data-stu-id="29dc5-142">You can also decide if you want to add RU per minute.</span></span> <span data-ttu-id="29dc5-143">Это можно сделать на портале или с помощью пакета SDK.</span><span class="sxs-lookup"><span data-stu-id="29dc5-143">This can be done through the Portal or the SDK.</span></span> 

### <a name="through-the-portal"></a><span data-ttu-id="29dc5-144">Добавление единиц запросов на портале</span><span class="sxs-lookup"><span data-stu-id="29dc5-144">Through the Portal</span></span>

<span data-ttu-id="29dc5-145">Чтобы добавить единицы запросов в минуту, необходимо просто выбрать нужный параметр при подготовке коллекции.</span><span class="sxs-lookup"><span data-stu-id="29dc5-145">Enabling or disabling RU per minute simply requires a click when provisioning a collection.</span></span> 

 ![Снимок экрана с параметром добавления единиц запросов в минуту на портале Azure](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-the-sdk"></a><span data-ttu-id="29dc5-147">Добавление единиц запросов с помощью пакета SDK</span><span class="sxs-lookup"><span data-stu-id="29dc5-147">Through the SDK</span></span>
<span data-ttu-id="29dc5-148">Единицы запросов в минуту доступны только для следующих пакетов SDK:</span><span class="sxs-lookup"><span data-stu-id="29dc5-148">First, this is important to note that RU/m is only available for the following SDKs:</span></span>

* <span data-ttu-id="29dc5-149">.NET 1.14.0;</span><span class="sxs-lookup"><span data-stu-id="29dc5-149">.Net 1.14.0</span></span>
* <span data-ttu-id="29dc5-150">Java 1.11.0;</span><span class="sxs-lookup"><span data-stu-id="29dc5-150">Java 1.11.0</span></span>
* <span data-ttu-id="29dc5-151">Node.js 1.12.0;</span><span class="sxs-lookup"><span data-stu-id="29dc5-151">Node.js 1.12.0</span></span>
* <span data-ttu-id="29dc5-152">Python 2.2.0.</span><span class="sxs-lookup"><span data-stu-id="29dc5-152">Python 2.2.0</span></span>

<span data-ttu-id="29dc5-153">Ниже приведен фрагмент кода для создания коллекции с 3000 единиц запросов в секунду и 30 000 единиц запросов в минуту с помощью пакета SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="29dc5-153">Here is a code snippet for creating a collection with 3,000 request units per second and 30,000 request units per minute using the .NET SDK:</span></span>

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set the throughput to 3,000 request units per second which will give you 30,000 request units per minute as the RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

<span data-ttu-id="29dc5-154">Ниже приведен фрагмент кода для изменения пропускной способности коллекции до 5000 единиц запросов в секунду без единиц запросов в минуту с помощью пакета SDK для .NET.</span><span class="sxs-lookup"><span data-stu-id="29dc5-154">Here is a code snippet for changing the throughput of a collection to 5,000 request units per second without provisioning RU per minute using the .NET SDK:</span></span>

```csharp
// Get the current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set the throughput to 5000 request units per second without RU/m enabled (the last parameter to OfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a><span data-ttu-id="29dc5-155">Сценарии применения</span><span class="sxs-lookup"><span data-stu-id="29dc5-155">Good fit scenarios</span></span>

<span data-ttu-id="29dc5-156">В этом разделе рассматриваются сценарии, в которых мы советуем использовать единицы запросов в минуту.</span><span class="sxs-lookup"><span data-stu-id="29dc5-156">In this section, we provide an overview of scenarios that are a good fit for enabling request units per minute.</span></span>

<span data-ttu-id="29dc5-157">**Среда разработки и тестирования.**</span><span class="sxs-lookup"><span data-stu-id="29dc5-157">**Dev/Test environment:** Good fit.</span></span> <span data-ttu-id="29dc5-158">Единицы запросов в минуту могут обеспечить гибкость на этапе разработки при тестировании приложения с использованием разных рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="29dc5-158">During the development stage, if you are testing your application with different workloads, RU/m can provide the flexibility at this stage.</span></span> <span data-ttu-id="29dc5-159">Для тестирования базы данных Azure Cosmos DB можно использовать бесплатный [эмулятор](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="29dc5-159">While the [emulator](local-emulator.md) is a great free tool to test Azure Cosmos DB.</span></span> <span data-ttu-id="29dc5-160">Но если вы хотите начать работу в облачной среде, используйте единицы запросов в минуту, так как они обеспечивают исключительную гибкость и нужную производительность.</span><span class="sxs-lookup"><span data-stu-id="29dc5-160">However if you want to start in a cloud environment, you will have a great flexibility with RU/m for your adhoc performance needs.</span></span> <span data-ttu-id="29dc5-161">Это позволит посвятить больше времени разработке, не заботясь о производительности.</span><span class="sxs-lookup"><span data-stu-id="29dc5-161">You will spend more time developing, less worrying about performance needs at first.</span></span> <span data-ttu-id="29dc5-162">Мы советуем подготовить минимальное число единиц запросов в секунду и включить единицы запросов в минуту.</span><span class="sxs-lookup"><span data-stu-id="29dc5-162">We recommend starting with the minimum RU/s provisioning and enable RU/m.</span></span>

<span data-ttu-id="29dc5-163">**Непредсказуемые события, пиковые нагрузки и потребность в ежеминутной степени детализации** (экономия расходов от 25 до 75 %).</span><span class="sxs-lookup"><span data-stu-id="29dc5-163">**Unpredictable, spiky, minute granularity needs:** Good fit – Savings: 25-75%.</span></span> <span data-ttu-id="29dc5-164">Мы рассмотрели разные сценарии, в которых единицы запросов в минуту принесли значительную пользу, и большинство рабочих сценариев входят в их число.</span><span class="sxs-lookup"><span data-stu-id="29dc5-164">We have seen large improvement from RU/m and most production scenarios are into that group.</span></span> <span data-ttu-id="29dc5-165">Если имеется рабочая нагрузка Интернета вещей с несколькими пиковыми нагрузками в минуту и запросы выполняются в системе именно в это время, вам потребуется дополнительная емкость для обработки этих пиковых нагрузок.</span><span class="sxs-lookup"><span data-stu-id="29dc5-165">If you have an IoT workload that has spike a few times in a minute, if you have queries running when your system makes mass insert at the same time, you will need extra capacity for handeling spiky needs.</span></span> <span data-ttu-id="29dc5-166">Мы советуем оптимизировать потребность в ресурсах, используя приведенный ниже подход.</span><span class="sxs-lookup"><span data-stu-id="29dc5-166">We recommend optimizing your resource needs by applying our step by step approach below.</span></span>

 ![График выполнения запросов с пятиминутной степенью детализации](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 <span data-ttu-id="29dc5-168">*Рис. Результаты измерения производительности при использовании единиц запросов*</span><span class="sxs-lookup"><span data-stu-id="29dc5-168">*Figure - RU consumption benchmark*</span></span>

<span data-ttu-id="29dc5-169">**Надежность** (экономия от 10 до 20 %).</span><span class="sxs-lookup"><span data-stu-id="29dc5-169">**Peace of mind:** Good fit – Savings: 10-20%.</span></span> <span data-ttu-id="29dc5-170">Иногда вы просто хотите быть уверенными и не беспокоиться о возможных пиковых нагрузках и регулировании.</span><span class="sxs-lookup"><span data-stu-id="29dc5-170">Sometimes, you just want to have peace of mind and not worry about potential peaks and throttling.</span></span> <span data-ttu-id="29dc5-171">Этот вариант как раз для вас.</span><span class="sxs-lookup"><span data-stu-id="29dc5-171">This feature is the right one for you.</span></span> <span data-ttu-id="29dc5-172">В этом случае мы советуем включить единицы запросов в минуту и снизить число единиц запросов в секунду.</span><span class="sxs-lookup"><span data-stu-id="29dc5-172">In that case, we recommend enabling RU/m and slightly lower your per second provisioning.</span></span> <span data-ttu-id="29dc5-173">Этот случай отличается от приведенного выше, так как вы не пытаетесь оптимизировать подготовку.</span><span class="sxs-lookup"><span data-stu-id="29dc5-173">This case is different from the above as you will not try to optimize aggressively your provisioning.</span></span> <span data-ttu-id="29dc5-174">Это подход, в большей степени ориентированный на устранение регулирования.</span><span class="sxs-lookup"><span data-stu-id="29dc5-174">This is more of a “Zero Throttling” mindset you are in.</span></span>

<span data-ttu-id="29dc5-175">Критические операции с определенными потребностями. Иногда мы советуем использовать единицы запросов в минуту только при выполнении критических операций. За счет этого эти единицы запросов не будут использоваться в произвольных или менее важных операциях.</span><span class="sxs-lookup"><span data-stu-id="29dc5-175">Critical operations with adhoc needs: We sometimes recommend to only let critical operations access RU/m budget so the budget doesn’t get consume by adhoc or less important operations.</span></span> <span data-ttu-id="29dc5-176">В разделе ниже показано, как настроить параметры использования единиц запросов в минуту.</span><span class="sxs-lookup"><span data-stu-id="29dc5-176">That can be easily defined in the section below.</span></span>

## <a name="using-the-portal-metrics-to-optimize-cost-and-performance"></a><span data-ttu-id="29dc5-177">Оптимизация производительности и затрат с использованием метрик, доступных на портале</span><span class="sxs-lookup"><span data-stu-id="29dc5-177">Using the portal metrics to optimize cost and performance</span></span>

<span data-ttu-id="29dc5-178">**В ближайшие несколько недель мы предоставим сведения о мониторинге использования единиц запросов в минуту, что позволит оптимизировать регулирование.**</span><span class="sxs-lookup"><span data-stu-id="29dc5-178">**In the coming weeks, we will further develop the content around monitoring RUs minute consumption to optimize your throughput needs.**</span></span>

<span data-ttu-id="29dc5-179">Используя метрики, доступные на портале, вы можете сравнить использование единиц запросов в секунду и единиц запросов в минуту.</span><span class="sxs-lookup"><span data-stu-id="29dc5-179">Through the portal metrics, you can see how much of regular RU seconds you consume versus RU minutes.</span></span> <span data-ttu-id="29dc5-180">Мониторинг этих метрик позволяет оптимизировать подготовку.</span><span class="sxs-lookup"><span data-stu-id="29dc5-180">Monitoring these metrics should help you optimize your provisioning.</span></span> 

<span data-ttu-id="29dc5-181">Мы советуем использовать пошаговый подход, который позволяет получить пользу от единиц запросов в минуту.</span><span class="sxs-lookup"><span data-stu-id="29dc5-181">We recommend a step by step approach on how to use RU/m to your advantage.</span></span> <span data-ttu-id="29dc5-182">При выполнении каждого шага необходимо просматривать сведения о потреблении единиц запросов, представляющие полный цикл рабочей нагрузки (часы, дни или даже недели), и анализировать использование подготавливаемых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="29dc5-182">For each step, you should have an overview of the RU consumption representing a full cycle of your workload (it could be hours, days, or even weeks) and get insights on the utilization of what you provision.</span></span>

<span data-ttu-id="29dc5-183">Принцип, который лежит в основе этого подхода, заключается в том, чтобы подготовить пропускную способность как можно точнее к точке подготовки, которая соответствует критериям производительности ниже.</span><span class="sxs-lookup"><span data-stu-id="29dc5-183">The principle behind this approach is to make your throughput provisioning as close as possible to a provisioning point that matches your performance criteria below.</span></span> 

![График выполнения запросов с пятиминутной степенью детализации](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
<span data-ttu-id="29dc5-185">Чтобы определить оптимальную точку подготовки для рабочей нагрузки, необходимо понять следующее:</span><span class="sxs-lookup"><span data-stu-id="29dc5-185">To understand the optimal provisioning point for your workload, you need to understand:</span></span>

* <span data-ttu-id="29dc5-186">Шаблоны потребления. Определите частоту пиковых нагрузок (частые, нечастые, отсутствуют), а также</span><span class="sxs-lookup"><span data-stu-id="29dc5-186">Consumption patterns: no, infrequent or sustained spikes?</span></span> <span data-ttu-id="29dc5-187">их длительность, например краткосрочные (в 2 раза меньше средних), средние или долгосрочные (в 10 раз больше средних).</span><span class="sxs-lookup"><span data-stu-id="29dc5-187">Small (2x average), medium, or large (>10x average) spikes?</span></span>
* <span data-ttu-id="29dc5-188">Процент отрегулированных запросов. Определите, хотите ли вы выполнять регулирование,</span><span class="sxs-lookup"><span data-stu-id="29dc5-188">Percent of throttled requests: do you feel comfortable if you have a bit of throttling?</span></span> <span data-ttu-id="29dc5-189">и если да, то как часто.</span><span class="sxs-lookup"><span data-stu-id="29dc5-189">If so, by how much?</span></span> 

<span data-ttu-id="29dc5-190">Определив цели, вы сможете стать ближе к вычислению оптимального уровня подготовки.</span><span class="sxs-lookup"><span data-stu-id="29dc5-190">Once you have identified what your goals are, you will be able to get closer to the optimal provisioning.</span></span>

<span data-ttu-id="29dc5-191">Чтобы помочь вам, мы планируем предоставить руководство по оптимизации подготовки на основе использования единиц запросов в минуту.</span><span class="sxs-lookup"><span data-stu-id="29dc5-191">To assist you, we want to provide an overall guidance on how to optimize your provisioning based on your RU/m consumption.</span></span> <span data-ttu-id="29dc5-192">Это руководство не применяется ко всем типам рабочих нагрузок, но оно основано на данных закрытой предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="29dc5-192">This guidance doesn’t apply to all kind of workloads but is based on the private preview knowledge.</span></span> <span data-ttu-id="29dc5-193">При более подробном изучении базовые показатели могут измениться.</span><span class="sxs-lookup"><span data-stu-id="29dc5-193">We might change such baselines as we learn more:</span></span>

|<span data-ttu-id="29dc5-194">Использование единиц запросов в минуту (%)</span><span class="sxs-lookup"><span data-stu-id="29dc5-194">RU/m % utilization</span></span>|<span data-ttu-id="29dc5-195">Степень использования единиц запросов в минуту</span><span class="sxs-lookup"><span data-stu-id="29dc5-195">Degree of utilization of RU/m</span></span>|<span data-ttu-id="29dc5-196">Рекомендуемые действия для подготовки</span><span class="sxs-lookup"><span data-stu-id="29dc5-196">Recommended actions for provisioning</span></span>|
|---|---|---|
|<span data-ttu-id="29dc5-197">0–1 %</span><span class="sxs-lookup"><span data-stu-id="29dc5-197">0-1%</span></span>|<span data-ttu-id="29dc5-198">Недоиспользование</span><span class="sxs-lookup"><span data-stu-id="29dc5-198">Under utilization</span></span>|<span data-ttu-id="29dc5-199">Уменьшите число единиц запросов в секунду, чтобы использовать больше единиц запросов в минуту.</span><span class="sxs-lookup"><span data-stu-id="29dc5-199">Lower RU/s to consume more RU/m</span></span>|
|<span data-ttu-id="29dc5-200">1–10 %</span><span class="sxs-lookup"><span data-stu-id="29dc5-200">1-10%</span></span>|<span data-ttu-id="29dc5-201">Использование в работоспособном состоянии</span><span class="sxs-lookup"><span data-stu-id="29dc5-201">Healthy use</span></span>|<span data-ttu-id="29dc5-202">Используйте тот же уровень подготовки.</span><span class="sxs-lookup"><span data-stu-id="29dc5-202">Keep the same provisioning level</span></span>|
|<span data-ttu-id="29dc5-203">Выше 10 %</span><span class="sxs-lookup"><span data-stu-id="29dc5-203">Above 10%</span></span>|<span data-ttu-id="29dc5-204">Чрезмерное использование</span><span class="sxs-lookup"><span data-stu-id="29dc5-204">Over utilization</span></span>|<span data-ttu-id="29dc5-205">Увеличьте число единиц запросов в секунду, чтобы использовать меньше единиц запросов в минуту.</span><span class="sxs-lookup"><span data-stu-id="29dc5-205">Increase RU/s to rely less on RU/m</span></span>|

## <a name="select-which-operations-can-consume-the-rum-budget"></a><span data-ttu-id="29dc5-206">Выбор операций, использующих единицы запросов в минуту</span><span class="sxs-lookup"><span data-stu-id="29dc5-206">Select which operations can consume the RU/m budget</span></span>

<span data-ttu-id="29dc5-207">Единицы запросов в минуту можно также включить на уровне запроса. Это позволяет обрабатывать запросы независимо от типа операции.</span><span class="sxs-lookup"><span data-stu-id="29dc5-207">At request level, you can also enable/disable RU/m budget to serve the request irrespective of operation type.</span></span> <span data-ttu-id="29dc5-208">Если подготовленных единиц запросов в секунду не хватило и запрос не может использовать единицы запросов в минуту, выполняется регулировка запроса.</span><span class="sxs-lookup"><span data-stu-id="29dc5-208">If regular provisioned RUs/sec budget is consumed and the request cannot consume the RU/m budget, this request will be throttled.</span></span> <span data-ttu-id="29dc5-209">По умолчанию запрос использует единицы запросов в секунду, даже если активированы единицы запроса в минуту.</span><span class="sxs-lookup"><span data-stu-id="29dc5-209">By default, any request is served by RU/m budget if RU/m throughput budget is activated.</span></span> 

<span data-ttu-id="29dc5-210">Ниже приведен фрагмент кода для отключения резерва единиц запросов в минуту с помощью API DocumentDB для CRUD и операций запросов.</span><span class="sxs-lookup"><span data-stu-id="29dc5-210">Here is a code snippet for disabling RU/m budget using the DocumentDB API for CRUD and query operations.</span></span>

```csharp
// In order to disable any CRUD request for RU/m, set DisableRUPerMinuteUsage to true in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order to disable any query request for RU/m, set DisableRUPerMinuteOnRequest to true in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a><span data-ttu-id="29dc5-211">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="29dc5-211">Next steps</span></span>

<span data-ttu-id="29dc5-212">В этой статье мы рассмотрели, как действует секционирование в базе данных Azure Cosmos DB, а также узнали, как создать секционированные коллекции и как выбрать подходящий ключ секции для приложения.</span><span class="sxs-lookup"><span data-stu-id="29dc5-212">In this article, we've described how partitioning works in Azure Cosmos DB, how you can create partitioned collections, and how you can pick a good partition key for your application.</span></span>

* <span data-ttu-id="29dc5-213">Выполняйте проверку масштабирования и производительности с помощью базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="29dc5-213">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="29dc5-214">Пример см. в статье [Проверка производительности и масштабирования с помощью Azure DocumentDB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="29dc5-214">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="29dc5-215">Приступите к созданию кода с помощью [пакетов SDK](documentdb-sdk-dotnet.md) или [REST API](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="29dc5-215">Get started coding with the [SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/).</span></span>
* <span data-ttu-id="29dc5-216">Дополнительные сведения о подготовленной пропускной способности в базе данных Azure Cosmos DB см. в [этой статье](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="29dc5-216">Learn about [provisioned throughput](request-units.md) in Azure Cosmos DB</span></span> 

