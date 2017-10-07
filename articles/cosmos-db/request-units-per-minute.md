---
title: "Единицы запросов в минуту в базе данных Azure Cosmos DB | Документация Майкрософт"
description: "Узнайте, как tooreduce стоимость за счет использования запроса единицы в минуту."
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
ms.openlocfilehash: fcc3a92b9788750a2bfba361c3a9cebdb56eee05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a><span data-ttu-id="e6d43-103">Единицы запросов в минуту в базе данных Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e6d43-103">Request units per minute in Azure Cosmos DB</span></span>

<span data-ttu-id="e6d43-104">Azure Cosmos DB — спроектированный toohelp достижения быстрого и предсказуемая производительность и масштабируемость без проблем, а также роста приложения.</span><span class="sxs-lookup"><span data-stu-id="e6d43-104">Azure Cosmos DB is designed toohelp you achieve a fast, predictable performance and scale seamlessly along with your application’s growth.</span></span> <span data-ttu-id="e6d43-105">В контейнере базы данных Cosmos DB пропускную способность можно подготавливать с ежесекундной или ежеминутной степенью детализации.</span><span class="sxs-lookup"><span data-stu-id="e6d43-105">You can provision throughput on a Cosmos DB container at both, per-second and at per-minute (RU/m) granularities.</span></span> <span data-ttu-id="e6d43-106">Hello пропускная способность на уровне гранулярности в минуту — используется toomanage непредвиденными скачками hello рабочей нагрузки, произошедших на гранулярности в секунду.</span><span class="sxs-lookup"><span data-stu-id="e6d43-106">hello provisioned throughput at per-minute granularity is used toomanage unexpected spikes in hello workload occurring at a per-second granularity.</span></span> 

<span data-ttu-id="e6d43-107">В этой статье содержатся общие сведения о том, как работает Подготовка hello единиц запросов в минуту (RU/m).</span><span class="sxs-lookup"><span data-stu-id="e6d43-107">This article provides an overview of how hello provisioning of Request Unit per Minute (RU/m) works.</span></span> <span data-ttu-id="e6d43-108">Задача Hello в виду при подготовке RU/m — tooprovide прогнозируемую производительность вокруг непредсказуемым потребностей (в особенности, если вам нужна toorun аналитика на основе операционных данных) и высоким колебаниям рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="e6d43-108">hello goal in mind with provisioning of RU/m is tooprovide a predictable performance around unpredictable needs (especially if you need toorun analytics on top of your operational data) and spiky workloads.</span></span> <span data-ttu-id="e6d43-109">Мы хотим toohave наших клиентов потребляют большую нагрузку hello, его подготовке, поэтому их можно легко масштабировать быстро с спокойствие.</span><span class="sxs-lookup"><span data-stu-id="e6d43-109">We want toohave our customers consume more hello throughput they provision so they can scale quickly with peace of mind.</span></span>

<span data-ttu-id="e6d43-110">После считывания в этой статье, можно будет tooanswer hello следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="e6d43-110">After reading this article, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="e6d43-111">Как работают единицы запросов в минуту?</span><span class="sxs-lookup"><span data-stu-id="e6d43-111">How does a Request Unit per Minute work?</span></span>
* <span data-ttu-id="e6d43-112">Что такое hello различие между запроса единицах в минуту и запросов в секунду</span><span class="sxs-lookup"><span data-stu-id="e6d43-112">What is hello difference between Request Unit per Minute and Request Unit per Second?</span></span>
* <span data-ttu-id="e6d43-113">Как tooprovision RU/m?</span><span class="sxs-lookup"><span data-stu-id="e6d43-113">How tooprovision RU/m?</span></span>
* <span data-ttu-id="e6d43-114">В каких ситуациях следует подготавливать единицы запросов с ежеминутной степенью детализации?</span><span class="sxs-lookup"><span data-stu-id="e6d43-114">Under which scenario shall I consider provisioning Request Unit per Minute?</span></span>
* <span data-ttu-id="e6d43-115">Как toouse hello портала метрики toooptimize Мой затрат и производительности?</span><span class="sxs-lookup"><span data-stu-id="e6d43-115">How toouse hello portal metrics toooptimize my cost and performance?</span></span>
* <span data-ttu-id="e6d43-116">Какие типы запросов используют единицы запросов с ежеминутной степенью детализации?</span><span class="sxs-lookup"><span data-stu-id="e6d43-116">Define which type of request can consume your RU/m budget?</span></span>

## <a name="provisioning-request-units-per-minute-rum"></a><span data-ttu-id="e6d43-117">Подготовка единиц запросов в минуту</span><span class="sxs-lookup"><span data-stu-id="e6d43-117">Provisioning request units per minute (RU/m)</span></span>

<span data-ttu-id="e6d43-118">При подготовке Azure Cosmos DB на втором уровне детализации hello (единиц Запросов в секунду), вы получаете hello гарантии, что запрос выполняется успешно с низкой задержкой, если пропускная способность не превышает емкость hello подготовлены в течение секунды.</span><span class="sxs-lookup"><span data-stu-id="e6d43-118">When you provision Azure Cosmos DB at hello second granularity (RU/s), you get hello guarantee that your request succeeds at a low latency if your throughput has not exceeded hello capacity provisioned within that second.</span></span> <span data-ttu-id="e6d43-119">С RU/m гранулярность hello находится на минуту hello с hello гарантии, что запрос выполняется успешно в течение этой минуты.</span><span class="sxs-lookup"><span data-stu-id="e6d43-119">With RU/m, hello granularity is at hello minute with hello guarantee that your request succeeds within that minute.</span></span> <span data-ttu-id="e6d43-120">По сравнению с системами toobursting мы обязательно производительности hello, вы получаете прогнозируемого и можно рассчитывать на это.</span><span class="sxs-lookup"><span data-stu-id="e6d43-120">Compared toobursting systems, we make sure that hello performance you get is predictable and you can plan on it.</span></span>

<span data-ttu-id="e6d43-121">способ Hello в минуту подготовки работает довольно простой.</span><span class="sxs-lookup"><span data-stu-id="e6d43-121">hello way per minute provisioning works is simple:</span></span>

* <span data-ttu-id="e6d43-122">RU/m оплачивается каждый час и в tooRU сложения в секунду.</span><span class="sxs-lookup"><span data-stu-id="e6d43-122">RU/m is billed hourly and in addition tooRU/s.</span></span> <span data-ttu-id="e6d43-123">Дополнительные сведения см. на [странице цен на базу данных Azure Cosmos DB](https://aka.ms/acdbpricing).</span><span class="sxs-lookup"><span data-stu-id="e6d43-123">For more details, please visit Azure Cosmos DB [pricing page](https://aka.ms/acdbpricing).</span></span>
* <span data-ttu-id="e6d43-124">Единицы запросов в минуту можно включить на уровне коллекции.</span><span class="sxs-lookup"><span data-stu-id="e6d43-124">RU/m can be enabled at collection level.</span></span> <span data-ttu-id="e6d43-125">Что можно сделать через hello пакетов SDK (Node.js, Java или .net) или через портал hello (также включать рабочих нагрузок MongoDB API)</span><span class="sxs-lookup"><span data-stu-id="e6d43-125">That can be done through hello SDKs (Node.js, Java, or .Net) or through hello portal (also include MongoDB API workloads)</span></span>
* <span data-ttu-id="e6d43-126">При включении RU/m для каждого 100 единиц Запросов в секунду подготовки, вы также получаете 1 000 единиц Запросов/m подготовить (отношение hello — 10 раз)</span><span class="sxs-lookup"><span data-stu-id="e6d43-126">When RU/m is enabled, for every 100 RU/s provisioned, you also get 1,000 RU/m provisioned (hello ratio is 10x)</span></span>
* <span data-ttu-id="e6d43-127">Использование единиц запросов в минуту начинается только при превышении квоты на единицы запросов в секунду в течение заданной секунды.</span><span class="sxs-lookup"><span data-stu-id="e6d43-127">At a given second, a request unit consumes your RU/m provisioning only if you have exceeded your per second provisioning within that second</span></span>
* <span data-ttu-id="e6d43-128">Один раз Здравствуйте заканчивается 60-секундного периода (времени UTC), заполняется hello за минуты подготовки</span><span class="sxs-lookup"><span data-stu-id="e6d43-128">Once hello 60-second period (UTC) ends, hello per minute provisioning is refilled</span></span>
* <span data-ttu-id="e6d43-129">Единицы запросов в минуту можно использовать только в коллекциях с максимум 5000 единицами запросов в секунду на секцию.</span><span class="sxs-lookup"><span data-stu-id="e6d43-129">RU/m can be enabled only for collections with a maximum provisioning of 5,000 RU/s per partition.</span></span> <span data-ttu-id="e6d43-130">При масштабировании пропускной способности и достижении высокого уровня подготовки на секцию вы получите предупреждающее сообщение.</span><span class="sxs-lookup"><span data-stu-id="e6d43-130">If you scale your throughput needs and have such a high level of provisioning per partition, you will get a warning message</span></span>

<span data-ttu-id="e6d43-131">Ниже приведен конкретный пример, где пользователь может подготовить 10 000 единиц запросов в секунду и 100 000 единиц запросов в минуту, что позволяет сократить расходы на 73 %, не подготавливая дополнительные единицы запросов в секунду для пиковых нагрузок (около 50 000 единиц), которые могут произойти в коллекции с таким же числом единиц запросов в течение 90 секунд.</span><span class="sxs-lookup"><span data-stu-id="e6d43-131">Below is a concrete example, in which a customer can provision 10kRU/s with 100kRU/m, saving 73% in cost against provisioning for peak (at 50kRU/sec) through a 90-second period on a collection that has 10,000 RU/s and 100,000 RU/m provisioned:</span></span>

* <span data-ttu-id="e6d43-132">1 секунду: hello RU/m бюджета составляет 100 000</span><span class="sxs-lookup"><span data-stu-id="e6d43-132">1st second: hello RU/m budget is set at 100,000</span></span>
* <span data-ttu-id="e6d43-133">третьей секунды: во время этой второй hello потребления единицы запроса было 11,010 RUs, 1,010 RUs выше подготовки hello единиц Запросов в секунду.</span><span class="sxs-lookup"><span data-stu-id="e6d43-133">3rd second: During that second hello consumption of Request Unit was 11,010 RUs, 1,010 RUs above hello RU/s provisioning.</span></span> <span data-ttu-id="e6d43-134">Таким образом 1,010 RUs вычитаются из бюджета hello RU/m.</span><span class="sxs-lookup"><span data-stu-id="e6d43-134">Therefore, 1,010 RUs are deducted from hello RU/m budget.</span></span> <span data-ttu-id="e6d43-135">98,990 RUs доступны для hello следующих 57 секунд в бюджете RU/m hello</span><span class="sxs-lookup"><span data-stu-id="e6d43-135">98,990 RUs are available for hello next 57 seconds in hello RU/m budget</span></span>
* <span data-ttu-id="e6d43-136">29 секунду: во время этого второго произошло большой пик (> четыре раза выше, чем подготовки в секунду) и потребления hello единицы запрос был 46,920 RUs.</span><span class="sxs-lookup"><span data-stu-id="e6d43-136">29th second: During that second, a large spike happened (>4x higher than provisioning per second) and hello consumption of Request Unit was 46,920 RUs.</span></span> <span data-ttu-id="e6d43-137">36,920 RUs вычитаются из бюджета RU/m hello, удалены из 92,323 too55 RUs (28 секунда), 403 RUs (29 сек)</span><span class="sxs-lookup"><span data-stu-id="e6d43-137">36,920 RUs are deducted from hello RU/m budget that dropped from 92,323 RUs (28th second) too55,403 RUs (29th second)</span></span>
* <span data-ttu-id="e6d43-138">второй 61st: бюджета RU/m снова установить too100 000 RUs.</span><span class="sxs-lookup"><span data-stu-id="e6d43-138">61st second: RU/m budget is set back too100,000 RUs.</span></span>
 
![График показывает потребление hello и подготовка Azure Cosmos DB](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a><span data-ttu-id="e6d43-140">Указание количества единиц запросов с учетом резерва единиц запросов в минуту</span><span class="sxs-lookup"><span data-stu-id="e6d43-140">Specifying request unit capacity with RU/m</span></span>

<span data-ttu-id="e6d43-141">При создании коллекции Azure Cosmos DB, можно указать номер hello единиц запросов в секунду (единиц Запросов в секунду) требуется найти, зарезервированная для hello коллекции.</span><span class="sxs-lookup"><span data-stu-id="e6d43-141">When creating an Azure Cosmos DB collection, you specify hello number of request units per second (RU per second) you want reserved for hello collection.</span></span> <span data-ttu-id="e6d43-142">Можно решить, следует ли tooadd единиц Запросов в минуту.</span><span class="sxs-lookup"><span data-stu-id="e6d43-142">You can also decide if you want tooadd RU per minute.</span></span> <span data-ttu-id="e6d43-143">Это можно сделать с помощью hello портала или hello SDK.</span><span class="sxs-lookup"><span data-stu-id="e6d43-143">This can be done through hello Portal or hello SDK.</span></span> 

### <a name="through-hello-portal"></a><span data-ttu-id="e6d43-144">Через портал hello</span><span class="sxs-lookup"><span data-stu-id="e6d43-144">Through hello Portal</span></span>

<span data-ttu-id="e6d43-145">Чтобы добавить единицы запросов в минуту, необходимо просто выбрать нужный параметр при подготовке коллекции.</span><span class="sxs-lookup"><span data-stu-id="e6d43-145">Enabling or disabling RU per minute simply requires a click when provisioning a collection.</span></span> 

 ![Снимок экрана, показывающий как tooset RU/m в hello портал Azure](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-hello-sdk"></a><span data-ttu-id="e6d43-147">Через hello SDK</span><span class="sxs-lookup"><span data-stu-id="e6d43-147">Through hello SDK</span></span>
<span data-ttu-id="e6d43-148">Во-первых это важно toonote, RU-m доступен только для следующих пакетов SDK hello:</span><span class="sxs-lookup"><span data-stu-id="e6d43-148">First, this is important toonote that RU/m is only available for hello following SDKs:</span></span>

* <span data-ttu-id="e6d43-149">.NET 1.14.0;</span><span class="sxs-lookup"><span data-stu-id="e6d43-149">.Net 1.14.0</span></span>
* <span data-ttu-id="e6d43-150">Java 1.11.0;</span><span class="sxs-lookup"><span data-stu-id="e6d43-150">Java 1.11.0</span></span>
* <span data-ttu-id="e6d43-151">Node.js 1.12.0;</span><span class="sxs-lookup"><span data-stu-id="e6d43-151">Node.js 1.12.0</span></span>
* <span data-ttu-id="e6d43-152">Python 2.2.0.</span><span class="sxs-lookup"><span data-stu-id="e6d43-152">Python 2.2.0</span></span>

<span data-ttu-id="e6d43-153">Ниже приведен фрагмент кода для создания коллекции с 3 000 единиц запроса в единиц второй и 30 000 запросов в минуту, с помощью hello .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="e6d43-153">Here is a code snippet for creating a collection with 3,000 request units per second and 30,000 request units per minute using hello .NET SDK:</span></span>

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set hello throughput too3,000 request units per second which will give you 30,000 request units per minute as hello RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

<span data-ttu-id="e6d43-154">Ниже приведен фрагмент кода для изменения hello пропускной способности too5 коллекции, 000 единиц запросов в секунду без подготовки RU за минуту с помощью hello .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="e6d43-154">Here is a code snippet for changing hello throughput of a collection too5,000 request units per second without provisioning RU per minute using hello .NET SDK:</span></span>

```csharp
// Get hello current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput too5000 request units per second without RU/m enabled (hello last parameter tooOfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a><span data-ttu-id="e6d43-155">Сценарии применения</span><span class="sxs-lookup"><span data-stu-id="e6d43-155">Good fit scenarios</span></span>

<span data-ttu-id="e6d43-156">В этом разделе рассматриваются сценарии, в которых мы советуем использовать единицы запросов в минуту.</span><span class="sxs-lookup"><span data-stu-id="e6d43-156">In this section, we provide an overview of scenarios that are a good fit for enabling request units per minute.</span></span>

<span data-ttu-id="e6d43-157">**Среда разработки и тестирования.**</span><span class="sxs-lookup"><span data-stu-id="e6d43-157">**Dev/Test environment:** Good fit.</span></span> <span data-ttu-id="e6d43-158">На этапе разработки hello при тестировании приложения в разных рабочих нагрузок, RU-m может предоставить hello гибкость на этом этапе.</span><span class="sxs-lookup"><span data-stu-id="e6d43-158">During hello development stage, if you are testing your application with different workloads, RU/m can provide hello flexibility at this stage.</span></span> <span data-ttu-id="e6d43-159">При hello [эмулятор](local-emulator.md) имеет отличное бесплатное средство tootest Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e6d43-159">While hello [emulator](local-emulator.md) is a great free tool tootest Azure Cosmos DB.</span></span> <span data-ttu-id="e6d43-160">Тем не менее если требуется toostart в облачной среде, будут иметь гибкость с RU/m для вашим требованиям к производительности прямого соединения.</span><span class="sxs-lookup"><span data-stu-id="e6d43-160">However if you want toostart in a cloud environment, you will have a great flexibility with RU/m for your adhoc performance needs.</span></span> <span data-ttu-id="e6d43-161">Это позволит посвятить больше времени разработке, не заботясь о производительности.</span><span class="sxs-lookup"><span data-stu-id="e6d43-161">You will spend more time developing, less worrying about performance needs at first.</span></span> <span data-ttu-id="e6d43-162">Мы рекомендуем начать с hello подготовки минимальное единиц Запросов в секунду и включите RU/m.</span><span class="sxs-lookup"><span data-stu-id="e6d43-162">We recommend starting with hello minimum RU/s provisioning and enable RU/m.</span></span>

<span data-ttu-id="e6d43-163">**Непредсказуемые события, пиковые нагрузки и потребность в ежеминутной степени детализации** (экономия расходов от 25 до 75 %).</span><span class="sxs-lookup"><span data-stu-id="e6d43-163">**Unpredictable, spiky, minute granularity needs:** Good fit – Savings: 25-75%.</span></span> <span data-ttu-id="e6d43-164">Мы рассмотрели разные сценарии, в которых единицы запросов в минуту принесли значительную пользу, и большинство рабочих сценариев входят в их число.</span><span class="sxs-lookup"><span data-stu-id="e6d43-164">We have seen large improvement from RU/m and most production scenarios are into that group.</span></span> <span data-ttu-id="e6d43-165">При наличии рабочей нагрузки IoT с пик несколько раз в минуту, если у вас есть запросы, выполняемые при системы делает массовой вставки в hello же времени, вам потребуется дополнительная емкость обработку высоким колебаниям, должен.</span><span class="sxs-lookup"><span data-stu-id="e6d43-165">If you have an IoT workload that has spike a few times in a minute, if you have queries running when your system makes mass insert at hello same time, you will need extra capacity for handeling spiky needs.</span></span> <span data-ttu-id="e6d43-166">Мы советуем оптимизировать потребность в ресурсах, используя приведенный ниже подход.</span><span class="sxs-lookup"><span data-stu-id="e6d43-166">We recommend optimizing your resource needs by applying our step by step approach below.</span></span>

 ![График выполнения запросов с пятиминутной степенью детализации](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 <span data-ttu-id="e6d43-168">*Рис. Результаты измерения производительности при использовании единиц запросов*</span><span class="sxs-lookup"><span data-stu-id="e6d43-168">*Figure - RU consumption benchmark*</span></span>

<span data-ttu-id="e6d43-169">**Надежность** (экономия от 10 до 20 %).</span><span class="sxs-lookup"><span data-stu-id="e6d43-169">**Peace of mind:** Good fit – Savings: 10-20%.</span></span> <span data-ttu-id="e6d43-170">Иногда требуется toohave спокойствие и не беспокоиться о потенциальных пиковыми нагрузками и регулирования.</span><span class="sxs-lookup"><span data-stu-id="e6d43-170">Sometimes, you just want toohave peace of mind and not worry about potential peaks and throttling.</span></span> <span data-ttu-id="e6d43-171">Этот компонент является hello вправо на один для вас.</span><span class="sxs-lookup"><span data-stu-id="e6d43-171">This feature is hello right one for you.</span></span> <span data-ttu-id="e6d43-172">В этом случае мы советуем включить единицы запросов в минуту и снизить число единиц запросов в секунду.</span><span class="sxs-lookup"><span data-stu-id="e6d43-172">In that case, we recommend enabling RU/m and slightly lower your per second provisioning.</span></span> <span data-ttu-id="e6d43-173">Этот случай отличается от hello выше, как вы не будет повторять попытку toooptimize агрессивно вашей подготовки.</span><span class="sxs-lookup"><span data-stu-id="e6d43-173">This case is different from hello above as you will not try toooptimize aggressively your provisioning.</span></span> <span data-ttu-id="e6d43-174">Это подход, в большей степени ориентированный на устранение регулирования.</span><span class="sxs-lookup"><span data-stu-id="e6d43-174">This is more of a “Zero Throttling” mindset you are in.</span></span>

<span data-ttu-id="e6d43-175">Критически важные операции с потребностями adhoc: иногда рекомендуется tooonly позволяют использовать RU/m бюджета, что бюджет hello не получить доступ путем прямого соединения или менее важные операции критические операции.</span><span class="sxs-lookup"><span data-stu-id="e6d43-175">Critical operations with adhoc needs: We sometimes recommend tooonly let critical operations access RU/m budget so hello budget doesn’t get consume by adhoc or less important operations.</span></span> <span data-ttu-id="e6d43-176">Можно легко определить в разделе "hello" ниже.</span><span class="sxs-lookup"><span data-stu-id="e6d43-176">That can be easily defined in hello section below.</span></span>

## <a name="using-hello-portal-metrics-toooptimize-cost-and-performance"></a><span data-ttu-id="e6d43-177">С помощью hello портала метрики toooptimize затрат и производительности</span><span class="sxs-lookup"><span data-stu-id="e6d43-177">Using hello portal metrics toooptimize cost and performance</span></span>

<span data-ttu-id="e6d43-178">**В ближайшие недели hello мы будет доработки содержимое hello вокруг мониторинга toooptimize минуты потребления RUs должен пропускную способность.**</span><span class="sxs-lookup"><span data-stu-id="e6d43-178">**In hello coming weeks, we will further develop hello content around monitoring RUs minute consumption toooptimize your throughput needs.**</span></span>

<span data-ttu-id="e6d43-179">Посредством портала метрики hello можно увидеть, сколько регулярного секунд RU, использовать и RU минут.</span><span class="sxs-lookup"><span data-stu-id="e6d43-179">Through hello portal metrics, you can see how much of regular RU seconds you consume versus RU minutes.</span></span> <span data-ttu-id="e6d43-180">Мониторинг этих метрик позволяет оптимизировать подготовку.</span><span class="sxs-lookup"><span data-stu-id="e6d43-180">Monitoring these metrics should help you optimize your provisioning.</span></span> 

<span data-ttu-id="e6d43-181">Рекомендуемый подход шаг за шагом, о том, как toouse преимущества tooyour RU/m.</span><span class="sxs-lookup"><span data-stu-id="e6d43-181">We recommend a step by step approach on how toouse RU/m tooyour advantage.</span></span> <span data-ttu-id="e6d43-182">Для каждого шага, должны иметь общие сведения о потреблении hello RU представляющий полного цикла рабочей нагрузки (он может быть часы, дни, или даже недель) и получить представление на использование hello выполняется развертывание.</span><span class="sxs-lookup"><span data-stu-id="e6d43-182">For each step, you should have an overview of hello RU consumption representing a full cycle of your workload (it could be hours, days, or even weeks) and get insights on hello utilization of what you provision.</span></span>

<span data-ttu-id="e6d43-183">Принцип Hello этот подход является toomake к пропускной способности подготавливать закрыть как возможные tooa, точки, соответствующее условиям производительности ниже подготовки.</span><span class="sxs-lookup"><span data-stu-id="e6d43-183">hello principle behind this approach is toomake your throughput provisioning as close as possible tooa provisioning point that matches your performance criteria below.</span></span> 

![График выполнения запросов с пятиминутной степенью детализации](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
<span data-ttu-id="e6d43-185">toounderstand hello оптимальной подготовки точки для рабочей нагрузки, необходимо toounderstand:</span><span class="sxs-lookup"><span data-stu-id="e6d43-185">toounderstand hello optimal provisioning point for your workload, you need toounderstand:</span></span>

* <span data-ttu-id="e6d43-186">Шаблоны потребления. Определите частоту пиковых нагрузок (частые, нечастые, отсутствуют), а также</span><span class="sxs-lookup"><span data-stu-id="e6d43-186">Consumption patterns: no, infrequent or sustained spikes?</span></span> <span data-ttu-id="e6d43-187">их длительность, например краткосрочные (в 2 раза меньше средних), средние или долгосрочные (в 10 раз больше средних).</span><span class="sxs-lookup"><span data-stu-id="e6d43-187">Small (2x average), medium, or large (>10x average) spikes?</span></span>
* <span data-ttu-id="e6d43-188">Процент отрегулированных запросов. Определите, хотите ли вы выполнять регулирование,</span><span class="sxs-lookup"><span data-stu-id="e6d43-188">Percent of throttled requests: do you feel comfortable if you have a bit of throttling?</span></span> <span data-ttu-id="e6d43-189">и если да, то как часто.</span><span class="sxs-lookup"><span data-stu-id="e6d43-189">If so, by how much?</span></span> 

<span data-ttu-id="e6d43-190">После определения целей, можно будет tooget ближе toohello оптимальной подготовки.</span><span class="sxs-lookup"><span data-stu-id="e6d43-190">Once you have identified what your goals are, you will be able tooget closer toohello optimal provisioning.</span></span>

<span data-ttu-id="e6d43-191">tooassist, мы хотим tooprovide общих рекомендаций относительно на как toooptimize вашей подготовки на основе RU/m потребления.</span><span class="sxs-lookup"><span data-stu-id="e6d43-191">tooassist you, we want tooprovide an overall guidance on how toooptimize your provisioning based on your RU/m consumption.</span></span> <span data-ttu-id="e6d43-192">В этом руководстве не применить вид tooall рабочих нагрузок, но основана на знаний hello личной предварительной версии.</span><span class="sxs-lookup"><span data-stu-id="e6d43-192">This guidance doesn’t apply tooall kind of workloads but is based on hello private preview knowledge.</span></span> <span data-ttu-id="e6d43-193">При более подробном изучении базовые показатели могут измениться.</span><span class="sxs-lookup"><span data-stu-id="e6d43-193">We might change such baselines as we learn more:</span></span>

|<span data-ttu-id="e6d43-194">Использование единиц запросов в минуту (%)</span><span class="sxs-lookup"><span data-stu-id="e6d43-194">RU/m % utilization</span></span>|<span data-ttu-id="e6d43-195">Степень использования единиц запросов в минуту</span><span class="sxs-lookup"><span data-stu-id="e6d43-195">Degree of utilization of RU/m</span></span>|<span data-ttu-id="e6d43-196">Рекомендуемые действия для подготовки</span><span class="sxs-lookup"><span data-stu-id="e6d43-196">Recommended actions for provisioning</span></span>|
|---|---|---|
|<span data-ttu-id="e6d43-197">0–1 %</span><span class="sxs-lookup"><span data-stu-id="e6d43-197">0-1%</span></span>|<span data-ttu-id="e6d43-198">Недоиспользование</span><span class="sxs-lookup"><span data-stu-id="e6d43-198">Under utilization</span></span>|<span data-ttu-id="e6d43-199">Понизить дополнительные RU/m tooconsume единиц Запросов в секунду</span><span class="sxs-lookup"><span data-stu-id="e6d43-199">Lower RU/s tooconsume more RU/m</span></span>|
|<span data-ttu-id="e6d43-200">1–10 %</span><span class="sxs-lookup"><span data-stu-id="e6d43-200">1-10%</span></span>|<span data-ttu-id="e6d43-201">Использование в работоспособном состоянии</span><span class="sxs-lookup"><span data-stu-id="e6d43-201">Healthy use</span></span>|<span data-ttu-id="e6d43-202">Сохранить hello же подготовки уровень</span><span class="sxs-lookup"><span data-stu-id="e6d43-202">Keep hello same provisioning level</span></span>|
|<span data-ttu-id="e6d43-203">Выше 10 %</span><span class="sxs-lookup"><span data-stu-id="e6d43-203">Above 10%</span></span>|<span data-ttu-id="e6d43-204">Чрезмерное использование</span><span class="sxs-lookup"><span data-stu-id="e6d43-204">Over utilization</span></span>|<span data-ttu-id="e6d43-205">Увеличьте toorely единиц Запросов в секунду не на RU/m</span><span class="sxs-lookup"><span data-stu-id="e6d43-205">Increase RU/s toorely less on RU/m</span></span>|

## <a name="select-which-operations-can-consume-hello-rum-budget"></a><span data-ttu-id="e6d43-206">Выберите, какие операции могут потреблять hello RU/m бюджета</span><span class="sxs-lookup"><span data-stu-id="e6d43-206">Select which operations can consume hello RU/m budget</span></span>

<span data-ttu-id="e6d43-207">На уровне запроса можно также включить или отключить запрос hello tooserve RU/m бюджета независимо от типа операции.</span><span class="sxs-lookup"><span data-stu-id="e6d43-207">At request level, you can also enable/disable RU/m budget tooserve hello request irrespective of operation type.</span></span> <span data-ttu-id="e6d43-208">Если потребляется регулярного подготовленных бюджета RUs/сек, запрос hello не могут использовать бюджета RU/m hello будет регулироваться этого запроса.</span><span class="sxs-lookup"><span data-stu-id="e6d43-208">If regular provisioned RUs/sec budget is consumed and hello request cannot consume hello RU/m budget, this request will be throttled.</span></span> <span data-ttu-id="e6d43-209">По умолчанию запрос использует единицы запросов в секунду, даже если активированы единицы запроса в минуту.</span><span class="sxs-lookup"><span data-stu-id="e6d43-209">By default, any request is served by RU/m budget if RU/m throughput budget is activated.</span></span> 

<span data-ttu-id="e6d43-210">Ниже приведен фрагмент кода для отключения бюджета RU/m, с помощью hello DocumentDB API для операций CRUD и запроса.</span><span class="sxs-lookup"><span data-stu-id="e6d43-210">Here is a code snippet for disabling RU/m budget using hello DocumentDB API for CRUD and query operations.</span></span>

```csharp
// In order toodisable any CRUD request for RU/m, set DisableRUPerMinuteUsage tootrue in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order toodisable any query request for RU/m, set DisableRUPerMinuteOnRequest tootrue in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a><span data-ttu-id="e6d43-211">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e6d43-211">Next steps</span></span>

<span data-ttu-id="e6d43-212">В этой статье мы рассмотрели, как действует секционирование в базе данных Azure Cosmos DB, а также узнали, как создать секционированные коллекции и как выбрать подходящий ключ секции для приложения.</span><span class="sxs-lookup"><span data-stu-id="e6d43-212">In this article, we've described how partitioning works in Azure Cosmos DB, how you can create partitioned collections, and how you can pick a good partition key for your application.</span></span>

* <span data-ttu-id="e6d43-213">Выполняйте проверку масштабирования и производительности с помощью базы данных Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e6d43-213">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="e6d43-214">Пример см. в статье [Проверка производительности и масштабирования с помощью Azure DocumentDB](performance-testing.md).</span><span class="sxs-lookup"><span data-stu-id="e6d43-214">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="e6d43-215">Приступить к созданию кода с hello [пакетов SDK](documentdb-sdk-dotnet.md) или hello [API-интерфейса REST](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="e6d43-215">Get started coding with hello [SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/).</span></span>
* <span data-ttu-id="e6d43-216">Дополнительные сведения о подготовленной пропускной способности в базе данных Azure Cosmos DB см. в [этой статье](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="e6d43-216">Learn about [provisioned throughput](request-units.md) in Azure Cosmos DB</span></span> 

