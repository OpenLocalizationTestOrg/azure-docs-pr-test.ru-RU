---
title: "службы Service Fabric aaaPartitioning | Документы Microsoft"
description: "Описывает способ служб с отслеживанием состояния toopartition Service Fabric. Секций обеспечивает хранение данных на локальных компьютерах hello, данных и вычислений может масштабироваться друг с другом."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3b7248c8-ea92-4964-85e7-6f1291b5cc7b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: msfussell
ms.openlocfilehash: 6ead48716c08f4212535202ee69d169067d5c6d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="partition-service-fabric-reliable-services"></a><span data-ttu-id="83c6b-104">Секционирование служб Reliable Services в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="83c6b-104">Partition Service Fabric reliable services</span></span>
<span data-ttu-id="83c6b-105">Эта статья содержит введение toohello основные понятия секционирования надежные службы Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="83c6b-105">This article provides an introduction toohello basic concepts of partitioning Azure Service Fabric reliable services.</span></span> <span data-ttu-id="83c6b-106">Hello исходного кода, использованной в статье hello доступна также на [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="83c6b-106">hello source code used in hello article is also available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="partitioning"></a><span data-ttu-id="83c6b-107">Секционирование</span><span class="sxs-lookup"><span data-stu-id="83c6b-107">Partitioning</span></span>
<span data-ttu-id="83c6b-108">Секционирование не является уникальным tooService структуры.</span><span class="sxs-lookup"><span data-stu-id="83c6b-108">Partitioning is not unique tooService Fabric.</span></span> <span data-ttu-id="83c6b-109">По сути, это основной способ создания масштабируемых служб.</span><span class="sxs-lookup"><span data-stu-id="83c6b-109">In fact, it is a core pattern of building scalable services.</span></span> <span data-ttu-id="83c6b-110">В более широком смысле мы подумать о секционировании как понятие деления состояние (данные) и вычислений в небольших доступны единицы tooimprove масштабируемость и производительность.</span><span class="sxs-lookup"><span data-stu-id="83c6b-110">In a broader sense, we can think about partitioning as a concept of dividing state (data) and compute into smaller accessible units tooimprove scalability and performance.</span></span> <span data-ttu-id="83c6b-111">Распространенный пример секционирования — это [секционирование данных][wikipartition], которое еще называют сегментированием.</span><span class="sxs-lookup"><span data-stu-id="83c6b-111">A well-known form of partitioning is [data partitioning][wikipartition], also known as sharding.</span></span>

### <a name="partition-service-fabric-stateless-services"></a><span data-ttu-id="83c6b-112">Секционирование служб без отслеживания состояния в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="83c6b-112">Partition Service Fabric stateless services</span></span>
<span data-ttu-id="83c6b-113">В случае со службами без отслеживания состояния секцию можно описать как логическую единицу, содержащую один или несколько экземпляров службы.</span><span class="sxs-lookup"><span data-stu-id="83c6b-113">For stateless services, you can think about a partition being a logical unit that contains one or more instances of a service.</span></span> <span data-ttu-id="83c6b-114">На рис. 1 показана служба без отслеживания состояния с пятью экземплярами, распределенными в кластере и объединенными в одну секцию.</span><span class="sxs-lookup"><span data-stu-id="83c6b-114">Figure 1 shows a stateless service with five instances distributed across a cluster using one partition.</span></span>

![Служба без отслеживания состояния](./media/service-fabric-concepts-partitioning/statelessinstances.png)

<span data-ttu-id="83c6b-116">Есть два типа решений служб без отслеживания состояния.</span><span class="sxs-lookup"><span data-stu-id="83c6b-116">There are really two types of stateless service solutions.</span></span> <span data-ttu-id="83c6b-117">Hello первого одно — это служба, которая сохраняет состояние извне, например в базе данных Azure SQL (например, веб-сайт, сохраняет данные и сведения о сеансе hello).</span><span class="sxs-lookup"><span data-stu-id="83c6b-117">hello first one is a service that persists its state externally, for example in an Azure SQL database (like a website that stores hello session information and data).</span></span> <span data-ttu-id="83c6b-118">Hello второй раз — только для вычисления служб (например, создание эскизов калькулятора или изображение), управление которыми невозможно любое постоянное состояние.</span><span class="sxs-lookup"><span data-stu-id="83c6b-118">hello second one is computation-only services (like a calculator or image thumbnailing) that do not manage any persistent state.</span></span>

<span data-ttu-id="83c6b-119">Секционирование служб без отслеживания состояния выполняется очень редко.</span><span class="sxs-lookup"><span data-stu-id="83c6b-119">In either case, partitioning a stateless service is a very rare scenario--scalability and availability are normally achieved by adding more instances.</span></span> <span data-ttu-id="83c6b-120">запрашивает Hello только время tooconsider несколько секций для экземпляров службы без отслеживания состояния — при необходимости toomeet специального маршрута.</span><span class="sxs-lookup"><span data-stu-id="83c6b-120">hello only time you want tooconsider multiple partitions for stateless service instances is when you need toomeet special routing requests.</span></span>

<span data-ttu-id="83c6b-121">Примером может быть случай, когда пользователи с идентификаторами из определенного диапазона должны обслуживаться только определенным экземпляром службы.</span><span class="sxs-lookup"><span data-stu-id="83c6b-121">As an example, consider a case where users with IDs in a certain range should only be served by a particular service instance.</span></span> <span data-ttu-id="83c6b-122">Если выполнено секционирование службы без отслеживания состояния еще один пример — у вас действительно секционированной базы данных (например сегментированной базы данных SQL), если необходимо toocontrol экземпляра данной службы следует записать toohello сегментов базы данных — или выполнять другую работу подготовки в Hello службы без отслеживания состояния, которая требует hello же сведения о секционировании, так как используется в серверном hello.</span><span class="sxs-lookup"><span data-stu-id="83c6b-122">Another example of when you could partition a stateless service is when you have a truly partitioned backend (e.g. a sharded SQL database) and you want toocontrol which service instance should write toohello database shard--or perform other preparation work within hello stateless service that requires hello same partitioning information as is used in hello backend.</span></span> <span data-ttu-id="83c6b-123">Подобные сценарии также можно решить другими способами, не требующими секционирования службы.</span><span class="sxs-lookup"><span data-stu-id="83c6b-123">Those types of scenarios can also be solved in different ways and do not necessarily require service partitioning.</span></span>

<span data-ttu-id="83c6b-124">Остаток Hello в данном пошаговом руководстве основное внимание уделяется служб с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="83c6b-124">hello remainder of this walkthrough focuses on stateful services.</span></span>

### <a name="partition-service-fabric-stateful-services"></a><span data-ttu-id="83c6b-125">Секционирование служб с отслеживанием состояния в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="83c6b-125">Partition Service Fabric stateful services</span></span>
<span data-ttu-id="83c6b-126">Service Fabric позволяет легко toodevelop масштабируемых служб с отслеживанием состояния, предлагая первого класса способом toopartition состояние (данных).</span><span class="sxs-lookup"><span data-stu-id="83c6b-126">Service Fabric makes it easy toodevelop scalable stateful services by offering a first-class way toopartition state (data).</span></span> <span data-ttu-id="83c6b-127">По существу, можно считать о разделе службы с отслеживанием состояния единица масштабирования, которую высокую степень доступности посредством [реплик](service-fabric-availability-services.md) , распространяются и равномерно распределяется по hello узлов в кластере.</span><span class="sxs-lookup"><span data-stu-id="83c6b-127">Conceptually, you can think about a partition of a stateful service as a scale unit that is highly reliable through [replicas](service-fabric-availability-services.md) that are distributed and balanced across hello nodes in a cluster.</span></span>

<span data-ttu-id="83c6b-128">Секционирование в контексте служб с отслеживанием состояния Service Fabric hello ссылается toohello процесс определения того, что раздел конкретной службы отвечает за часть полного состояния службы hello hello.</span><span class="sxs-lookup"><span data-stu-id="83c6b-128">Partitioning in hello context of Service Fabric stateful services refers toohello process of determining that a particular service partition is responsible for a portion of hello complete state of hello service.</span></span> <span data-ttu-id="83c6b-129">(Как уже говорилось ранее, секция представляет собой набор [реплик](service-fabric-availability-services.md).)</span><span class="sxs-lookup"><span data-stu-id="83c6b-129">(As mentioned before, a partition is a set of [replicas](service-fabric-availability-services.md)).</span></span> <span data-ttu-id="83c6b-130">Преимущество Service Fabric — что он помещает hello секций на разных узлах.</span><span class="sxs-lookup"><span data-stu-id="83c6b-130">A great thing about Service Fabric is that it places hello partitions on different nodes.</span></span> <span data-ttu-id="83c6b-131">Это позволяет им ограничение ресурсов toogrow tooa узла.</span><span class="sxs-lookup"><span data-stu-id="83c6b-131">This allows them toogrow tooa node's resource limit.</span></span> <span data-ttu-id="83c6b-132">По мере роста данных hello увеличиваться секций и Service Fabric балансировку секций между узлами.</span><span class="sxs-lookup"><span data-stu-id="83c6b-132">As hello data needs grow, partitions grow, and Service Fabric rebalances partitions across nodes.</span></span> <span data-ttu-id="83c6b-133">Это гарантирует, что hello продолжение эффективного использования ресурсов оборудования.</span><span class="sxs-lookup"><span data-stu-id="83c6b-133">This ensures hello continued efficient use of hardware resources.</span></span>

<span data-ttu-id="83c6b-134">toogive вы пример, предположим, вы начинаются с 5 узлами кластера и службы, настроенные toohave 10 секций и как целевой объект три реплики.</span><span class="sxs-lookup"><span data-stu-id="83c6b-134">toogive you an example, say you start with a 5-node cluster and a service that is configured toohave 10 partitions and a target of three replicas.</span></span> <span data-ttu-id="83c6b-135">В этом случае Service Fabric бы балансировки и распределить hello реплик по hello кластера — и вы появятся два основных [реплик](service-fabric-availability-services.md) на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="83c6b-135">In this case, Service Fabric would balance and distribute hello replicas across hello cluster--and you would end up with two primary [replicas](service-fabric-availability-services.md) per node.</span></span>
<span data-ttu-id="83c6b-136">Если требуется tooscale out too10 hello кластеру, Service Fabric бы балансирования hello первичный [реплик](service-fabric-availability-services.md) на всех узлах 10.</span><span class="sxs-lookup"><span data-stu-id="83c6b-136">If you now need tooscale out hello cluster too10 nodes, Service Fabric would rebalance hello primary [replicas](service-fabric-availability-services.md) across all 10 nodes.</span></span> <span data-ttu-id="83c6b-137">Аналогичным образом Если увеличили задней too5 узлов Service Fabric бы балансирования все реплики hello по узлам hello 5.</span><span class="sxs-lookup"><span data-stu-id="83c6b-137">Likewise, if you scaled back too5 nodes, Service Fabric would rebalance all hello replicas across hello 5 nodes.</span></span>  

<span data-ttu-id="83c6b-138">Рис. 2 показана hello распределение 10 секций до и после масштабирования hello кластера.</span><span class="sxs-lookup"><span data-stu-id="83c6b-138">Figure 2 shows hello distribution of 10 partitions before and after scaling hello cluster.</span></span>

![Служба с отслеживанием состояния](./media/service-fabric-concepts-partitioning/partitions.png)

<span data-ttu-id="83c6b-140">В результате масштабирования hello достигается запросы клиентов распределяются на нескольких компьютерах, поэтому повысить общую производительность приложения hello и конфликты доступа toochunks данных сокращается.</span><span class="sxs-lookup"><span data-stu-id="83c6b-140">As a result, hello scale-out is achieved since requests from clients are distributed across computers, overall performance of hello application is improved, and contention on access toochunks of data is reduced.</span></span>

## <a name="plan-for-partitioning"></a><span data-ttu-id="83c6b-141">Планирование секционирования</span><span class="sxs-lookup"><span data-stu-id="83c6b-141">Plan for partitioning</span></span>
<span data-ttu-id="83c6b-142">Перед реализацией службы, рекомендуется всегда hello, требуется tooscale out стратегию секционирования. Можно различными способами, но все они сосредоточиться на какие hello приложению tooachieve.</span><span class="sxs-lookup"><span data-stu-id="83c6b-142">Before implementing a service, you should always consider hello partitioning strategy that is required tooscale out. There are different ways, but all of them focus on what hello application needs tooachieve.</span></span> <span data-ttu-id="83c6b-143">Для контекста hello в этой статье давайте рассмотрим некоторые hello более важные аспекты.</span><span class="sxs-lookup"><span data-stu-id="83c6b-143">For hello context of this article, let's consider some of hello more important aspects.</span></span>

<span data-ttu-id="83c6b-144">Рекомендуется toothink о структуре hello hello состояния, которые toobe секционирование, в качестве первого шага hello.</span><span class="sxs-lookup"><span data-stu-id="83c6b-144">A good approach is toothink about hello structure of hello state that needs toobe partitioned, as hello first step.</span></span>

<span data-ttu-id="83c6b-145">Давайте рассмотрим простой пример.</span><span class="sxs-lookup"><span data-stu-id="83c6b-145">Let's take a simple example.</span></span> <span data-ttu-id="83c6b-146">Если toobuild службы для countywide опроса, можно создать новый раздел для каждого города в округе hello.</span><span class="sxs-lookup"><span data-stu-id="83c6b-146">If you were toobuild a service for a countywide poll, you could create a partition for each city in hello county.</span></span> <span data-ttu-id="83c6b-147">Затем можно хранить в городе hello в секции hello, соответствующий Город toothat hello голосов для каждого человека.</span><span class="sxs-lookup"><span data-stu-id="83c6b-147">Then, you could store hello votes for every person in hello city in hello partition that corresponds toothat city.</span></span> <span data-ttu-id="83c6b-148">Рис. 3 показана набор пользователей, а также hello Город, в которой они находятся.</span><span class="sxs-lookup"><span data-stu-id="83c6b-148">Figure 3 illustrates a set of people and hello city in which they reside.</span></span>

![Простой раздел](./media/service-fabric-concepts-partitioning/cities.png)

<span data-ttu-id="83c6b-150">Как заполнение hello городов сильно варьируется, может оказаться некоторые разделы, которые содержат большой объем данных (например, Seattle) и другие разделы с состоянием очень мало (например Кирклэнд).</span><span class="sxs-lookup"><span data-stu-id="83c6b-150">As hello population of cities varies widely, you may end up with some partitions that contain a lot of data (e.g. Seattle) and other partitions with very little state (e.g. Kirkland).</span></span> <span data-ttu-id="83c6b-151">Так что такое последствия hello секций с неравномерной объемов состояние?</span><span class="sxs-lookup"><span data-stu-id="83c6b-151">So what is hello impact of having partitions with uneven amounts of state?</span></span>

<span data-ttu-id="83c6b-152">Если вы думаете о примере hello еще раз, можно легко увидеть, получение hello секции, в которой размещается hello голосов для Сиэтла больше трафика, чем Кирклэнд hello один.</span><span class="sxs-lookup"><span data-stu-id="83c6b-152">If you think about hello example again, you can easily see that hello partition that holds hello votes for Seattle will get more traffic than hello Kirkland one.</span></span> <span data-ttu-id="83c6b-153">По умолчанию Service Fabric гарантирует, что имеется о hello одинаковое число первичных и вторичных реплик на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="83c6b-153">By default, Service Fabric makes sure that there is about hello same number of primary and secondary replicas on each node.</span></span> <span data-ttu-id="83c6b-154">Поэтому у вас могут получиться узлы, реплики на которых обслуживают разный объем трафика.</span><span class="sxs-lookup"><span data-stu-id="83c6b-154">So you may end up with nodes that hold replicas that serve more traffic and others that serve less traffic.</span></span> <span data-ttu-id="83c6b-155">Предпочтительно потребовалось бы tooavoid горячие и холодные перегруженные участки, как в данном в кластере.</span><span class="sxs-lookup"><span data-stu-id="83c6b-155">You would preferably want tooavoid hot and cold spots like this in a cluster.</span></span>

<span data-ttu-id="83c6b-156">Чтобы tooavoid это, необходимо сделать две вещи, с секционирования точки зрения:</span><span class="sxs-lookup"><span data-stu-id="83c6b-156">In order tooavoid this, you should do two things, from a partitioning point of view:</span></span>

* <span data-ttu-id="83c6b-157">Попробуйте toopartition hello состояния, чтобы равномерно распределяется все секции.</span><span class="sxs-lookup"><span data-stu-id="83c6b-157">Try toopartition hello state so that it is evenly distributed across all partitions.</span></span>
* <span data-ttu-id="83c6b-158">Загрузка отчета из каждой из реплик hello hello службы.</span><span class="sxs-lookup"><span data-stu-id="83c6b-158">Report load from each of hello replicas for hello service.</span></span> <span data-ttu-id="83c6b-159">(Чтобы узнать, как это сделать, прочитайте эту статью о [метриках и загрузке](service-fabric-cluster-resource-manager-metrics.md).)</span><span class="sxs-lookup"><span data-stu-id="83c6b-159">(For information on how, check out this article on [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md)).</span></span> <span data-ttu-id="83c6b-160">Service Fabric предоставляет hello возможность tooreport нагрузки на службы, такие как объем памяти или число записей.</span><span class="sxs-lookup"><span data-stu-id="83c6b-160">Service Fabric provides hello capability tooreport load consumed by services, such as amount of memory or number of records.</span></span> <span data-ttu-id="83c6b-161">На основании hello показатели, Service Fabric обнаруживает, что некоторые разделы обслуживающей более высокие нагрузки, чем другие и балансировку кластера hello скользящего реплик toomore подходящий узлами, чтобы в целом ни один узел не перегружен.</span><span class="sxs-lookup"><span data-stu-id="83c6b-161">Based on hello metrics reported, Service Fabric detects that some partitions are serving higher loads than others and rebalances hello cluster by moving replicas toomore suitable nodes, so that overall no node is overloaded.</span></span>

<span data-ttu-id="83c6b-162">В некоторых случаях невозможно заранее определить, какой объем данных будет в той или иной секции.</span><span class="sxs-lookup"><span data-stu-id="83c6b-162">Sometimes, you cannot know how much data will be in a given partition.</span></span> <span data-ttu-id="83c6b-163">Поэтому общая рекомендация toodo оба--во-первых, принимая стратегии секционирования, распространяет hello данных равномерно по hello секции во-вторых, путем загрузки отчетов.</span><span class="sxs-lookup"><span data-stu-id="83c6b-163">So a general recommendation is toodo both--first, by adopting a partitioning strategy that spreads hello data evenly across hello partitions and second, by reporting load.</span></span>  <span data-ttu-id="83c6b-164">Первый метод Hello предотвращает ситуациях, описанных в hello голосования примере хотя hello второй помогает сглаживают временные разницы в доступа или нагрузки со временем.</span><span class="sxs-lookup"><span data-stu-id="83c6b-164">hello first method prevents situations described in hello voting example, while hello second helps smooth out temporary differences in access or load over time.</span></span>

<span data-ttu-id="83c6b-165">Другим аспектом планирования раздела является toochoose hello неверное количество секций toobegin с.</span><span class="sxs-lookup"><span data-stu-id="83c6b-165">Another aspect of partition planning is toochoose hello correct number of partitions toobegin with.</span></span>
<span data-ttu-id="83c6b-166">В Service Fabric нет никаких ограничений относительно использования большего количества секций, чем требуется для тех или иных целей.</span><span class="sxs-lookup"><span data-stu-id="83c6b-166">From a Service Fabric perspective, there is nothing that prevents you from starting out with a higher number of partitions than anticipated for your scenario.</span></span>
<span data-ttu-id="83c6b-167">Фактически при условии, что hello максимального количества секций — это допустимый подход.</span><span class="sxs-lookup"><span data-stu-id="83c6b-167">In fact, assuming hello maximum number of partitions is a valid approach.</span></span>

<span data-ttu-id="83c6b-168">Большее количество секций, чем выбрано изначально, может понадобиться в редких случаях.</span><span class="sxs-lookup"><span data-stu-id="83c6b-168">In rare cases, you may end up needing more partitions than you have initially chosen.</span></span> <span data-ttu-id="83c6b-169">Число секций hello нельзя изменить после проведения hello, потребовалось бы tooapply некоторые подходы дополнительные секции, например для создания нового экземпляра службы из hello же тип службы.</span><span class="sxs-lookup"><span data-stu-id="83c6b-169">As you cannot change hello partition count after hello fact, you would need tooapply some advanced partition approaches, such as creating a new service instance of hello same service type.</span></span> <span data-ttu-id="83c6b-170">Необходимо также tooimplement некоторые клиентские логику, которая направляет hello запрашивает экземпляр toohello правильную службу, на основе набора знаний стороны клиента, необходимо обеспечить код клиента.</span><span class="sxs-lookup"><span data-stu-id="83c6b-170">You would also need tooimplement some client-side logic that routes hello requests toohello correct service instance, based on client-side knowledge that your client code must maintain.</span></span>

<span data-ttu-id="83c6b-171">Другой аспект для секционирования планирования — hello доступный компьютер ресурсы.</span><span class="sxs-lookup"><span data-stu-id="83c6b-171">Another consideration for partitioning planning is hello available computer resources.</span></span> <span data-ttu-id="83c6b-172">По мере toobe доступ и хранится состояние hello будут привязанного toofollow:</span><span class="sxs-lookup"><span data-stu-id="83c6b-172">As hello state needs toobe accessed and stored, you are bound toofollow:</span></span>

* <span data-ttu-id="83c6b-173">пропускная способность сети;</span><span class="sxs-lookup"><span data-stu-id="83c6b-173">Network bandwidth limits</span></span>
* <span data-ttu-id="83c6b-174">память системы;</span><span class="sxs-lookup"><span data-stu-id="83c6b-174">System memory limits</span></span>
* <span data-ttu-id="83c6b-175">место на диске.</span><span class="sxs-lookup"><span data-stu-id="83c6b-175">Disk storage limits</span></span>

<span data-ttu-id="83c6b-176">Что произойдет, если возникнут ограничения ресурсов в кластере выполнение? Hello ответ заключается в том, что можно просто масштабировать hello tooaccommodate hello новые требования к кластеру.</span><span class="sxs-lookup"><span data-stu-id="83c6b-176">So what happens if you run into resource constraints in a running cluster? hello answer is that you can simply scale out hello cluster tooaccommodate hello new requirements.</span></span>

<span data-ttu-id="83c6b-177">[руководство по планированию емкости Hello](service-fabric-capacity-planning.md) предлагает руководство toodetermine сколько узлов кластера требуется.</span><span class="sxs-lookup"><span data-stu-id="83c6b-177">[hello capacity planning guide](service-fabric-capacity-planning.md) offers guidance for how toodetermine how many nodes your cluster needs.</span></span>

## <a name="get-started-with-partitioning"></a><span data-ttu-id="83c6b-178">Начало секционирования</span><span class="sxs-lookup"><span data-stu-id="83c6b-178">Get started with partitioning</span></span>
<span data-ttu-id="83c6b-179">В этом разделе описывает, как tooget работу с секционирования службы.</span><span class="sxs-lookup"><span data-stu-id="83c6b-179">This section describes how tooget started with partitioning your service.</span></span>

<span data-ttu-id="83c6b-180">В Service Fabric можно выбрать одну из трех возможных схем секционирования.</span><span class="sxs-lookup"><span data-stu-id="83c6b-180">Service Fabric offers a choice of three partition schemes:</span></span>

* <span data-ttu-id="83c6b-181">Секционирование по диапазонам значений (также известное как UniformInt64Partition).</span><span class="sxs-lookup"><span data-stu-id="83c6b-181">Ranged partitioning (otherwise known as UniformInt64Partition).</span></span>
* <span data-ttu-id="83c6b-182">Секционирование по именам.</span><span class="sxs-lookup"><span data-stu-id="83c6b-182">Named partitioning.</span></span> <span data-ttu-id="83c6b-183">Как правило, данные приложений, которые используют эту модель, можно поместить в контейнер в рамках ограниченного набора данных.</span><span class="sxs-lookup"><span data-stu-id="83c6b-183">Applications using this model usually have data that can be bucketed, within a bounded set.</span></span> <span data-ttu-id="83c6b-184">Вот некоторые наиболее распространенные примеры полей данных, которые используются в качестве ключей для секционирования по именам: регионы, почтовые индексы, группы клиентов и др.</span><span class="sxs-lookup"><span data-stu-id="83c6b-184">Some common examples of data fields used as named partition keys would be regions, postal codes, customer groups, or other business boundaries.</span></span>
* <span data-ttu-id="83c6b-185">Одноэлементное секционирование.</span><span class="sxs-lookup"><span data-stu-id="83c6b-185">Singleton partitioning.</span></span> <span data-ttu-id="83c6b-186">Одноэлементный секции обычно используются при hello служба не требует какой-либо дополнительных маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="83c6b-186">Singleton partitions are typically used when hello service does not require any additional routing.</span></span> <span data-ttu-id="83c6b-187">Например, службы без отслеживания состояния используют эту схему секционирования по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="83c6b-187">For example, stateless services use this partitioning scheme by default.</span></span>

<span data-ttu-id="83c6b-188">Схемы секционирования по именам и одноэлементного секционирования являются особыми формами секционирования по диапазонам.</span><span class="sxs-lookup"><span data-stu-id="83c6b-188">Named and Singleton partitioning schemes are special forms of ranged partitions.</span></span> <span data-ttu-id="83c6b-189">По умолчанию hello шаблонов Visual Studio для использования Service Fabric циклы секционирования, как он hello наиболее распространенным и полезным один.</span><span class="sxs-lookup"><span data-stu-id="83c6b-189">By default, hello Visual Studio templates for Service Fabric use ranged partitioning, as it is hello most common and useful one.</span></span> <span data-ttu-id="83c6b-190">Hello оставшейся части этой статьи посвящена hello срез схему секционирования.</span><span class="sxs-lookup"><span data-stu-id="83c6b-190">hello remainder of this article focuses on hello ranged partitioning scheme.</span></span>

### <a name="ranged-partitioning-scheme"></a><span data-ttu-id="83c6b-191">Схема секционирования по диапазонам</span><span class="sxs-lookup"><span data-stu-id="83c6b-191">Ranged partitioning scheme</span></span>
<span data-ttu-id="83c6b-192">Это используется toospecify целое диапазона (определяемая нижний ключ и верхний ключ) и количество секций (n).</span><span class="sxs-lookup"><span data-stu-id="83c6b-192">This is used toospecify an integer range (identified by a low key and high key) and a number of partitions (n).</span></span> <span data-ttu-id="83c6b-193">Он создает n секций, каждый из которых отвечает для стадии hello неперекрывающиеся секции диапазона ключей в целом.</span><span class="sxs-lookup"><span data-stu-id="83c6b-193">It creates n partitions, each responsible for a non-overlapping subrange of hello overall partition key range.</span></span> <span data-ttu-id="83c6b-194">Например, схема секционирования по диапазонам, в которой нижний ключ равен 0, верхний ключ равен 99, а количество секций равно 4, создаст четыре секции, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="83c6b-194">For example, a ranged partitioning scheme with a low key of 0, a high key of 99, and a count of 4 would create four partitions, as shown below.</span></span>

![Секционирование по диапазону](./media/service-fabric-concepts-partitioning/range-partitioning.png)

<span data-ttu-id="83c6b-196">Наиболее распространенный подход заключается toocreate хэша, основанная на уникальный ключ в наборе данных hello.</span><span class="sxs-lookup"><span data-stu-id="83c6b-196">A common approach is toocreate a hash based on a unique key within hello data set.</span></span> <span data-ttu-id="83c6b-197">Вот некоторые наиболее распространенные примеры ключей: код идентификации транспортного средства (VIN), идентификатор сотрудника, уникальная строка и пр.</span><span class="sxs-lookup"><span data-stu-id="83c6b-197">Some common examples of keys would be a vehicle identification number (VIN), an employee ID, or a unique string.</span></span> <span data-ttu-id="83c6b-198">Используя этот уникальный ключ, будет затем создать хэш-код, диапазона ключей hello остатка от деления, toouse как ключ.</span><span class="sxs-lookup"><span data-stu-id="83c6b-198">By using this unique key, you would then generate a hash code, modulus hello key range, toouse as your key.</span></span> <span data-ttu-id="83c6b-199">Можно указать hello верхней и нижней границ допустимого диапазона ключей hello.</span><span class="sxs-lookup"><span data-stu-id="83c6b-199">You can specify hello upper and lower bounds of hello allowed key range.</span></span>

### <a name="select-a-hash-algorithm"></a><span data-ttu-id="83c6b-200">Выбор хэш-алгоритма</span><span class="sxs-lookup"><span data-stu-id="83c6b-200">Select a hash algorithm</span></span>
<span data-ttu-id="83c6b-201">Важной частью хэширования является выбор хэш-алгоритма.</span><span class="sxs-lookup"><span data-stu-id="83c6b-201">An important part of hashing is selecting your hash algorithm.</span></span> <span data-ttu-id="83c6b-202">Следует учитывать, является ли цель hello toogroup аналогичные ключи рядом друг с другом (конфиденциальные хэширования местоположению)--или если действия должен быть предоставлен широко во всех разделах (распространения хэширования), который чаще.</span><span class="sxs-lookup"><span data-stu-id="83c6b-202">A consideration is whether hello goal is toogroup similar keys near each other (locality sensitive hashing)--or if activity should be distributed broadly across all partitions (distribution hashing), which is more common.</span></span>

<span data-ttu-id="83c6b-203">Это легко toocompute, он имеет несколько конфликтов и равномерно распределяет hello ключи приведены характеристики Hello распространения хорошей хэш-алгоритма.</span><span class="sxs-lookup"><span data-stu-id="83c6b-203">hello characteristics of a good distribution hashing algorithm are that it is easy toocompute, it has few collisions, and it distributes hello keys evenly.</span></span> <span data-ttu-id="83c6b-204">Хорошим примером алгоритма хэширования эффективный — hello [FNV 1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) хэш-алгоритм.</span><span class="sxs-lookup"><span data-stu-id="83c6b-204">A good example of an efficient hash algorithm is hello [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) hash algorithm.</span></span>

<span data-ttu-id="83c6b-205">Hello является ценным ресурсом для варианты алгоритм хэширования общие кода [страницы Википедии на хэш-функции](http://en.wikipedia.org/wiki/Hash_function).</span><span class="sxs-lookup"><span data-stu-id="83c6b-205">A good resource for general hash code algorithm choices is hello [Wikipedia page on hash functions](http://en.wikipedia.org/wiki/Hash_function).</span></span>

## <a name="build-a-stateful-service-with-multiple-partitions"></a><span data-ttu-id="83c6b-206">Создание службы с отслеживанием состояния с несколькими секциями</span><span class="sxs-lookup"><span data-stu-id="83c6b-206">Build a stateful service with multiple partitions</span></span>
<span data-ttu-id="83c6b-207">Далее вы создадите свою первую службу Reliable Services с отслеживанием состояния с несколькими разделами.</span><span class="sxs-lookup"><span data-stu-id="83c6b-207">Let's create your first reliable stateful service with multiple partitions.</span></span> <span data-ttu-id="83c6b-208">В этом примере будет создать все фамилии, начинающиеся с буквы в hello hello очень простое приложение место toostore одной секции.</span><span class="sxs-lookup"><span data-stu-id="83c6b-208">In this example, you will build a very simple application where you want toostore all last names that start with hello same letter in hello same partition.</span></span>

<span data-ttu-id="83c6b-209">Прежде чем писать программный код необходим toothink о секциях hello и ключи разделов.</span><span class="sxs-lookup"><span data-stu-id="83c6b-209">Before you write any code, you need toothink about hello partitions and partition keys.</span></span> <span data-ttu-id="83c6b-210">Добавить 26 разделы (по одному для каждой буквы в алфавите hello), но что о hello низким и высоким ключей?</span><span class="sxs-lookup"><span data-stu-id="83c6b-210">You need 26 partitions (one for each letter in hello alphabet), but what about hello low and high keys?</span></span>
<span data-ttu-id="83c6b-211">Как буквально, мы хотим toohave один раздел на букву, мы используем 0 как нижний ключ hello и 25 как hello верхний ключ, как каждая буква представляет свой собственный ключ.</span><span class="sxs-lookup"><span data-stu-id="83c6b-211">As we literally want toohave one partition per letter, we can use 0 as hello low key and 25 as hello high key, as each letter is its own key.</span></span>

> [!NOTE]
> <span data-ttu-id="83c6b-212">Это упрощенное сценарий, как на самом деле бы неравномерное распределение hello.</span><span class="sxs-lookup"><span data-stu-id="83c6b-212">This is a simplified scenario, as in reality hello distribution would be uneven.</span></span> <span data-ttu-id="83c6b-213">Последний имена, начинающиеся с буквы hello «S» или «M» чаще, чем hello из них, начиная с «X» или «Y».</span><span class="sxs-lookup"><span data-stu-id="83c6b-213">Last names starting with hello letters "S" or "M" are more common than hello ones starting with "X" or "Y".</span></span>
> 
> 

1. <span data-ttu-id="83c6b-214">Выберите **Visual Studio** > **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="83c6b-214">Open **Visual Studio** > **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="83c6b-215">В hello **новый проект** диалогового окна выберите приложение hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="83c6b-215">In hello **New Project** dialog box, choose hello Service Fabric application.</span></span>
3. <span data-ttu-id="83c6b-216">Вызов hello проекта «AlphabetPartitions».</span><span class="sxs-lookup"><span data-stu-id="83c6b-216">Call hello project "AlphabetPartitions".</span></span>
4. <span data-ttu-id="83c6b-217">В hello **создать службу** диалогового окна выберите **с отслеживанием состояния** службы и назовите его «Alphabet.Processing», как показано в приведенном ниже рисунке hello.</span><span class="sxs-lookup"><span data-stu-id="83c6b-217">In hello **Create a Service** dialog box, choose **Stateful** service and call it "Alphabet.Processing" as shown in hello image below.</span></span>
       <span data-ttu-id="83c6b-218">![Диалоговое окно "Новая служба" в Visual Studio][1]</span><span class="sxs-lookup"><span data-stu-id="83c6b-218">![New service dialog in Visual Studio][1]</span></span>

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. <span data-ttu-id="83c6b-219">Задайте hello количество секций.</span><span class="sxs-lookup"><span data-stu-id="83c6b-219">Set hello number of partitions.</span></span> <span data-ttu-id="83c6b-220">Привет открыть файл Applicationmanifest.xml находится в hello ApplicationPackageRoot папки AlphabetPartitions hello проекте и обновите параметр hello too26 Processing_PartitionCount, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="83c6b-220">Open hello Applicationmanifest.xml file located in hello ApplicationPackageRoot folder of hello AlphabetPartitions project and update hello parameter Processing_PartitionCount too26 as shown below.</span></span>
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    <span data-ttu-id="83c6b-221">Необходимо также tooupdate hello LowKey и HighKey свойств элемента StatefulService hello в hello ApplicationManifest.xml, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="83c6b-221">You also need tooupdate hello LowKey and HighKey properties of hello StatefulService element in hello ApplicationManifest.xml as shown below.</span></span>
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. <span data-ttu-id="83c6b-222">Для toobe hello службы доступны открывая конечную точку на порте, добавив hello. элемент конечной точки ServiceManifest.xml (находится в папке PackageRoot hello) для hello Alphabet.Processing службы, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="83c6b-222">For hello service toobe accessible, open up an endpoint on a port by adding hello endpoint element of ServiceManifest.xml (located in hello PackageRoot folder) for hello Alphabet.Processing service as shown below:</span></span>
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    <span data-ttu-id="83c6b-223">Теперь служба hello является настроенным toolisten tooan внутренней конечной точки с 26 секций.</span><span class="sxs-lookup"><span data-stu-id="83c6b-223">Now hello service is configured toolisten tooan internal endpoint with 26 partitions.</span></span>
7. <span data-ttu-id="83c6b-224">Далее необходимо toooverride hello `CreateServiceReplicaListeners()` метод класса обработки hello.</span><span class="sxs-lookup"><span data-stu-id="83c6b-224">Next, you need toooverride hello `CreateServiceReplicaListeners()` method of hello Processing class.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="83c6b-225">В этом примере предполагается, что вы используете простой прослушиватель HttpCommunicationListener.</span><span class="sxs-lookup"><span data-stu-id="83c6b-225">For this sample, we assume that you are using a simple HttpCommunicationListener.</span></span> <span data-ttu-id="83c6b-226">Дополнительные сведения о связи надежной службы см. в разделе [модель взаимодействия hello надежной службы](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="83c6b-226">For more information on reliable service communication, see [hello Reliable Service communication model](service-fabric-reliable-services-communication.md).</span></span>
   > 
   > 
8. <span data-ttu-id="83c6b-227">Рекомендуемый шаблон для hello URL-адрес, который прослушивает реплики — hello, следующий формат: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span><span class="sxs-lookup"><span data-stu-id="83c6b-227">A recommended pattern for hello URL that a replica listens on is hello following format: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span></span>
    <span data-ttu-id="83c6b-228">Поэтому вы хотите tooconfigure ваш прослушиватель toolisten связи на hello нужных конечных точек и с этим шаблоном.</span><span class="sxs-lookup"><span data-stu-id="83c6b-228">So you want tooconfigure your communication listener toolisten on hello correct endpoints and with this pattern.</span></span>
   
    <span data-ttu-id="83c6b-229">Несколько реплик эта служба может размещаться на hello одном компьютере, поэтому этот адрес должен toobe уникальный toohello реплики.</span><span class="sxs-lookup"><span data-stu-id="83c6b-229">Multiple replicas of this service may be hosted on hello same computer, so this address needs toobe unique toohello replica.</span></span> <span data-ttu-id="83c6b-230">Именно поэтому идентификатор секции + идентификатор реплики находятся в URL-адрес hello.</span><span class="sxs-lookup"><span data-stu-id="83c6b-230">This is why   partition ID + replica ID are in hello URL.</span></span> <span data-ttu-id="83c6b-231">HttpListener может прослушивать несколько адресов на приветствия же порт, при условии, что префикс URL-адреса hello является уникальным.</span><span class="sxs-lookup"><span data-stu-id="83c6b-231">HttpListener can listen on multiple addresses on hello same port as long as hello URL prefix    is unique.</span></span>
   
    <span data-ttu-id="83c6b-232">Здравствуйте, есть ли дополнительные GUID для сложных случаях, где также прослушивания вторичные реплики для запросов только для чтения.</span><span class="sxs-lookup"><span data-stu-id="83c6b-232">hello extra GUID is there for an advanced case where secondary replicas also listen for read-only requests.</span></span> <span data-ttu-id="83c6b-233">Это случай hello, нужно убедиться, что новый уникальный адрес используется во время перехода с основной toosecondary tooforce клиентов toore resolve hello адрес toomake.</span><span class="sxs-lookup"><span data-stu-id="83c6b-233">When that's hello case, you want toomake sure that a new unique address is used when transitioning from primary toosecondary tooforce clients toore-resolve hello address.</span></span> <span data-ttu-id="83c6b-234">«+» используется как адрес hello, чтобы hello реплика прослушивает все доступные узлы в (IP, FQDM, localhost, т. д.) hello кода ниже показан пример.</span><span class="sxs-lookup"><span data-stu-id="83c6b-234">'+' is used as hello address here so that hello replica listens on all available hosts (IP, FQDM, localhost, etc.) hello code below shows an example.</span></span>
   
    ```CSharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
         return new[] { new ServiceReplicaListener(context => this.CreateInternalListener(context))};
    }
    private ICommunicationListener CreateInternalListener(ServiceContext context)
    {
   
         EndpointResourceDescription internalEndpoint = context.CodePackageActivationContext.GetEndpoint("ProcessingServiceEndpoint");
         string uriPrefix = String.Format(
                "{0}://+:{1}/{2}/{3}-{4}/",
                internalEndpoint.Protocol,
                internalEndpoint.Port,
                context.PartitionId,
                context.ReplicaOrInstanceId,
                Guid.NewGuid());
   
         string nodeIP = FabricRuntime.GetNodeContext().IPAddressOrFQDN;
   
         string uriPublished = uriPrefix.Replace("+", nodeIP);
         return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInternalRequest);
    }
    ```
   
    <span data-ttu-id="83c6b-235">Также стоит отметить, что hello опубликованные URL-адрес имеет некоторые отличия от hello прослушивания префикс URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="83c6b-235">It's also worth noting that hello published URL is slightly different from hello listening URL prefix.</span></span>
    <span data-ttu-id="83c6b-236">Hello прослушивания задан URL-адрес tooHttpListener.</span><span class="sxs-lookup"><span data-stu-id="83c6b-236">hello listening URL is given tooHttpListener.</span></span> <span data-ttu-id="83c6b-237">Здравствуйте, hello URL-адрес, опубликованный toohello служба именования Service Fabric, которая используется для обнаружения службы является URL-адрес публикации.</span><span class="sxs-lookup"><span data-stu-id="83c6b-237">hello published URL is hello URL that is published toohello Service Fabric Naming Service, which is used for service discovery.</span></span> <span data-ttu-id="83c6b-238">Клиенты будут запрашивать этот адрес с помощью службы обнаружения.</span><span class="sxs-lookup"><span data-stu-id="83c6b-238">Clients will ask for this address through that discovery service.</span></span> <span data-ttu-id="83c6b-239">адрес Hello, клиенты получают потребностей toohave hello фактических IP-адрес или полное доменное имя узла hello в tooconnect порядке.</span><span class="sxs-lookup"><span data-stu-id="83c6b-239">hello address that clients get needs toohave hello actual IP or FQDN of hello node in order tooconnect.</span></span> <span data-ttu-id="83c6b-240">Поэтому необходимо tooreplace '+' с hello узла в IP-адрес или полное доменное имя как показано выше.</span><span class="sxs-lookup"><span data-stu-id="83c6b-240">So you need tooreplace '+' with hello node's IP or FQDN as shown above.</span></span>
9. <span data-ttu-id="83c6b-241">Последний шаг Hello — hello tooadd обработки логики toohello службы, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="83c6b-241">hello last step is tooadd hello processing logic toohello service as shown below.</span></span>
   
    ```CSharp
    private async Task ProcessInternalRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        string output = null;
        string user = context.Request.QueryString["lastname"].ToString();
   
        try
        {
            output = await this.AddUserAsync(user);
        }
        catch (Exception ex)
        {
            output = ex.Message;
        }
   
        using (HttpListenerResponse response = context.Response)
        {
            if (output != null)
            {
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    private async Task<string> AddUserAsync(string user)
    {
        IReliableDictionary<String, String> dictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<String, String>>("dictionary");
   
        using (ITransaction tx = this.StateManager.CreateTransaction())
        {
            bool addResult = await dictionary.TryAddAsync(tx, user.ToUpperInvariant(), user);
   
            await tx.CommitAsync();
   
            return String.Format(
                "User {0} {1}",
                user,
                addResult ? "sucessfully added" : "already exists");
        }
    }
    ```
   
    <span data-ttu-id="83c6b-242">`ProcessInternalRequest`операции чтения hello значения секции hello toocall параметр, используемый строку hello запросов и вызовов `AddUserAsync` надежного словарь lastname hello toohello tooadd `dictionary`.</span><span class="sxs-lookup"><span data-stu-id="83c6b-242">`ProcessInternalRequest` reads hello values of hello query string parameter used toocall hello partition and calls `AddUserAsync` tooadd hello lastname toohello reliable dictionary `dictionary`.</span></span>
10. <span data-ttu-id="83c6b-243">Давайте добавим toosee проекта службы без отслеживания состояния toohello как можно вызвать заданной секции.</span><span class="sxs-lookup"><span data-stu-id="83c6b-243">Let's add a stateless service toohello project toosee how you can call a particular partition.</span></span>
    
    <span data-ttu-id="83c6b-244">Эта служба служит в качестве простого веб-интерфейса, который принимает lastname hello как параметр строки запроса, определяет ключ раздела hello и отправляет его службе Alphabet.Processing toohello для обработки.</span><span class="sxs-lookup"><span data-stu-id="83c6b-244">This service serves as a simple web interface that accepts hello lastname as a query string parameter, determines hello partition key, and sends it toohello Alphabet.Processing service for processing.</span></span>
11. <span data-ttu-id="83c6b-245">В hello **создать службу** диалогового окна выберите **Stateless** службы и назовите его «Alphabet.Web», как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="83c6b-245">In hello **Create a Service** dialog box, choose **Stateless** service and call it "Alphabet.Web" as shown below.</span></span>
    
    ![Снимок экрана, на котором изображена служба без отслеживания состояния](./media/service-fabric-concepts-partitioning/createnewstateless.png)<span data-ttu-id="83c6b-247">.</span><span class="sxs-lookup"><span data-stu-id="83c6b-247">.</span></span>
12. <span data-ttu-id="83c6b-248">Обновите сведения о конечной точке hello в hello ServiceManifest.xml tooopen службы Alphabet.WebApi hello порт, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="83c6b-248">Update hello endpoint information in hello ServiceManifest.xml of hello Alphabet.WebApi service tooopen up a port as shown below.</span></span>
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. <span data-ttu-id="83c6b-249">Необходимо tooreturn коллекцию ServiceInstanceListeners в классе hello Web.</span><span class="sxs-lookup"><span data-stu-id="83c6b-249">You need tooreturn a collection of ServiceInstanceListeners in hello class Web.</span></span> <span data-ttu-id="83c6b-250">Опять же вы можете tooimplement простой HttpCommunicationListener.</span><span class="sxs-lookup"><span data-stu-id="83c6b-250">Again, you can choose tooimplement a simple HttpCommunicationListener.</span></span>
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is hello node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. <span data-ttu-id="83c6b-251">Теперь вам требуется логика обработки tooimplement hello.</span><span class="sxs-lookup"><span data-stu-id="83c6b-251">Now you need tooimplement hello processing logic.</span></span> <span data-ttu-id="83c6b-252">Здравствуйте, вызовы HttpCommunicationListener `ProcessInputRequest` при поступлении запроса.</span><span class="sxs-lookup"><span data-stu-id="83c6b-252">hello HttpCommunicationListener calls `ProcessInputRequest` when a request comes in.</span></span> <span data-ttu-id="83c6b-253">Поэтому добавим и добавьте приведенный ниже код hello.</span><span class="sxs-lookup"><span data-stu-id="83c6b-253">So let's go ahead and add hello code below.</span></span>
    
    ```CSharp
    private async Task ProcessInputRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        String output = null;
        try
        {
            string lastname = context.Request.QueryString["lastname"];
            char firstLetterOfLastName = lastname.First();
            ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    
            ResolvedServicePartition partition = await this.servicePartitionResolver.ResolveAsync(alphabetServiceUri, partitionKey, cancelRequest);
            ResolvedServiceEndpoint ep = partition.GetEndpoint();
    
            JObject addresses = JObject.Parse(ep.Address);
            string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
            UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
            primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
            string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    
            output = String.Format(
                    "Result: {0}. <p>Partition key: '{1}' generated from hello first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
                    result,
                    partitionKey,
                    firstLetterOfLastName,
                    lastname,
                    partition.Info.Id,
                    primaryReplicaAddress);
        }
        catch (Exception ex) { output = ex.Message; }
    
        using (var response = context.Response)
        {
            if (output != null)
            {
                output = output + "added tooPartition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    <span data-ttu-id="83c6b-254">Давайте разберемся в процессе, шаг за шагом.</span><span class="sxs-lookup"><span data-stu-id="83c6b-254">Let's walk through it step by step.</span></span> <span data-ttu-id="83c6b-255">Код Hello считывает hello первую букву из параметра строки запроса hello `lastname` в тип char.</span><span class="sxs-lookup"><span data-stu-id="83c6b-255">hello code reads hello first letter of hello query string parameter `lastname` into a char.</span></span> <span data-ttu-id="83c6b-256">Затем определяет hello ключ раздела для эту букву путем вычитания hello шестнадцатеричное значение `A` из hello шестнадцатеричное значение hello фамилий первая буква.</span><span class="sxs-lookup"><span data-stu-id="83c6b-256">Then, it determines hello partition key for this letter by subtracting hello hexadecimal value of `A` from hello hexadecimal value of hello last names' first letter.</span></span>
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    <span data-ttu-id="83c6b-257">Напоминаем, что в этом примере мы используем 26 секций с одним ключом на секцию.</span><span class="sxs-lookup"><span data-stu-id="83c6b-257">Remember, for this example, we are using 26 partitions with one partition key per partition.</span></span>
    <span data-ttu-id="83c6b-258">Затем мы получим hello служебного раздела `partition` для этого ключа с помощью hello `ResolveAsync` метод hello `servicePartitionResolver` объекта.</span><span class="sxs-lookup"><span data-stu-id="83c6b-258">Next, we obtain hello service partition `partition` for this key by using hello `ResolveAsync` method on hello `servicePartitionResolver` object.</span></span> <span data-ttu-id="83c6b-259">`servicePartitionResolver` определяется так:</span><span class="sxs-lookup"><span data-stu-id="83c6b-259">`servicePartitionResolver` is defined as</span></span>
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    <span data-ttu-id="83c6b-260">Hello `ResolveAsync` URI службы hello метод принимает ключ раздела hello и токен отмены в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="83c6b-260">hello `ResolveAsync` method takes hello service URI, hello partition key, and a cancellation token as parameters.</span></span> <span data-ttu-id="83c6b-261">Здравствуйте URI службы для службы обработки hello `fabric:/AlphabetPartitions/Processing`.</span><span class="sxs-lookup"><span data-stu-id="83c6b-261">hello service URI for hello processing service is `fabric:/AlphabetPartitions/Processing`.</span></span> <span data-ttu-id="83c6b-262">Далее мы получаем конечной точки hello hello секции.</span><span class="sxs-lookup"><span data-stu-id="83c6b-262">Next, we get hello endpoint of hello partition.</span></span>
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    <span data-ttu-id="83c6b-263">Наконец мы построения URL-адрес конечной точки hello плюс строка запроса hello и вызовите hello службы обработки.</span><span class="sxs-lookup"><span data-stu-id="83c6b-263">Finally, we build hello endpoint URL plus hello querystring and call hello processing service.</span></span>
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    <span data-ttu-id="83c6b-264">После завершения обработки hello мы вывода hello обратно.</span><span class="sxs-lookup"><span data-stu-id="83c6b-264">Once hello processing is done, we write hello output back.</span></span>
15. <span data-ttu-id="83c6b-265">Последний шаг Hello — служба tootest hello.</span><span class="sxs-lookup"><span data-stu-id="83c6b-265">hello last step is tootest hello service.</span></span> <span data-ttu-id="83c6b-266">Visual Studio использует параметры приложения для локального и облачного развертываний.</span><span class="sxs-lookup"><span data-stu-id="83c6b-266">Visual Studio uses application parameters for local and cloud deployment.</span></span> <span data-ttu-id="83c6b-267">службы hello tootest с 26 секций на локальном компьютере, необходимо tooupdate hello `Local.xml` файл в папке ApplicationParameters hello hello AlphabetPartitions проекта, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="83c6b-267">tootest hello service with 26 partitions locally, you need tooupdate hello `Local.xml` file in hello ApplicationParameters folder of hello AlphabetPartitions project as shown below:</span></span>
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. <span data-ttu-id="83c6b-268">После завершения развертывания можно проверить службу hello и всех своих секций в обозреватель Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="83c6b-268">Once you finish deployment, you can check hello service and all of its partitions in hello Service Fabric Explorer.</span></span>
    
    ![Снимок экрана, на котором изображен обозреватель Service Fabric](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. <span data-ttu-id="83c6b-270">В браузере можно проверить секционирование логику, введя hello `http://localhost:8081/?lastname=somename`.</span><span class="sxs-lookup"><span data-stu-id="83c6b-270">In a browser, you can test hello partitioning logic by entering `http://localhost:8081/?lastname=somename`.</span></span> <span data-ttu-id="83c6b-271">Вы увидите, что каждой фамилии, который начинается с такой же буквой, хранящихся в hello hello одной секции.</span><span class="sxs-lookup"><span data-stu-id="83c6b-271">You will see that each last name that starts with hello same letter is being stored in hello same partition.</span></span>
    
    ![Снимок экрана, на котором изображен браузер](./media/service-fabric-concepts-partitioning/samplerunning.png)

<span data-ttu-id="83c6b-273">Hello весь исходный код образца hello доступен на [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="83c6b-273">hello entire source code of hello sample is available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="83c6b-274">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="83c6b-274">Next steps</span></span>
<span data-ttu-id="83c6b-275">Сведения о Service Fabric см. ниже hello:</span><span class="sxs-lookup"><span data-stu-id="83c6b-275">For information on Service Fabric concepts, see hello following:</span></span>

* [<span data-ttu-id="83c6b-276">Доступность служб структуры служб</span><span class="sxs-lookup"><span data-stu-id="83c6b-276">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="83c6b-277">Масштабируемость служб структуры служб</span><span class="sxs-lookup"><span data-stu-id="83c6b-277">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="83c6b-278">Планирование емкости для приложений Service Fabric</span><span class="sxs-lookup"><span data-stu-id="83c6b-278">Capacity planning for Service Fabric applications</span></span>](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png