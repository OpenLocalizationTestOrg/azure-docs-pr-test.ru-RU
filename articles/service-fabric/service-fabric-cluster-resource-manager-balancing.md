---
title: "aaaBalance кластера Azure Service Fabric | Документы Microsoft"
description: "Введение toobalancing кластера с hello диспетчер ресурсов кластера Service Fabric."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 030b1465-6616-4c0b-8bc7-24ed47d054c0
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 5f7ad2f5cf4cfb3751a860f5293b03d2d5266d99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="balancing-your-service-fabric-cluster"></a><span data-ttu-id="847b3-103">Балансировка кластера Service Fabric</span><span class="sxs-lookup"><span data-stu-id="847b3-103">Balancing your service fabric cluster</span></span>
<span data-ttu-id="847b3-104">Hello диспетчер ресурсов кластера Service Fabric поддерживает динамическое загрузки изменений, tooadditions отклик или удаления узлов или служб.</span><span class="sxs-lookup"><span data-stu-id="847b3-104">hello Service Fabric Cluster Resource Manager supports dynamic load changes, reacting tooadditions or removals of nodes or services.</span></span> <span data-ttu-id="847b3-105">Он также автоматически исправляет нарушения ограничений и заранее балансировку hello кластера.</span><span class="sxs-lookup"><span data-stu-id="847b3-105">It also automatically corrects constraint violations, and proactively rebalances hello cluster.</span></span> <span data-ttu-id="847b3-106">Но как часто выполняются эти действия и что их инициирует?</span><span class="sxs-lookup"><span data-stu-id="847b3-106">But how often are these actions taken, and what triggers them?</span></span>

<span data-ttu-id="847b3-107">Существует три разных категории работы, hello, которое выполняет диспетчер ресурсов кластера.</span><span class="sxs-lookup"><span data-stu-id="847b3-107">There are three different categories of work that hello Cluster Resource Manager performs.</span></span> <span data-ttu-id="847b3-108">К ним относятся:</span><span class="sxs-lookup"><span data-stu-id="847b3-108">They are:</span></span>

1. <span data-ttu-id="847b3-109">Размещение: на этом этапе происходит размещение отсутствующих метрик с отслеживанием состояния или без.</span><span class="sxs-lookup"><span data-stu-id="847b3-109">Placement – this stage deals with placing any stateful replicas or stateless instances that are missing.</span></span> <span data-ttu-id="847b3-110">Размещаются как новые службы, так и реплики с отслеживанием состояния или экземпляры без отслеживания состояния, которые вызвали сбой.</span><span class="sxs-lookup"><span data-stu-id="847b3-110">Placement includes both new services and handling stateful replicas or stateless instances that have failed.</span></span> <span data-ttu-id="847b3-111">Тут выполняется удаление реплик и экземпляров.</span><span class="sxs-lookup"><span data-stu-id="847b3-111">Deleting and dropping replicas or instances are handled here.</span></span>
2. <span data-ttu-id="847b3-112">Проверяет ограничения — этот этап проверяет, а также исправляет нарушения ограничений размещения различных hello (правила) в системе hello.</span><span class="sxs-lookup"><span data-stu-id="847b3-112">Constraint Checks – this stage checks for and corrects violations of hello different placement constraints (rules) within hello system.</span></span> <span data-ttu-id="847b3-113">Примеры правил — это средства, предотвращающие избыточное использование ресурсов узлов, обеспечивающие соблюдение ограничений на размещение службы и т. п.</span><span class="sxs-lookup"><span data-stu-id="847b3-113">Examples of rules are things like ensuring that nodes are not over capacity and that a service’s placement constraints are met.</span></span>
3. <span data-ttu-id="847b3-114">Балансировка — этот этап проверяет toosee при перераспределения необходимости в зависимости от настройки hello требуемого уровня сальдо для различных показателей.</span><span class="sxs-lookup"><span data-stu-id="847b3-114">Balancing – this stage checks toosee if rebalancing is necessary based on hello configured desired level of balance for different metrics.</span></span> <span data-ttu-id="847b3-115">В этом случае он пытается toofind упорядочение в hello кластера то есть несколько взаимосвязанных.</span><span class="sxs-lookup"><span data-stu-id="847b3-115">If so it attempts toofind an arrangement in hello cluster that is more balanced.</span></span>

## <a name="configuring-cluster-resource-manager-timers"></a><span data-ttu-id="847b3-116">Настройка таймеров диспетчера кластерных ресурсов</span><span class="sxs-lookup"><span data-stu-id="847b3-116">Configuring Cluster Resource Manager Timers</span></span>
<span data-ttu-id="847b3-117">Первый набор элементов управления в балансировки Hello представляют собой набор таймеров.</span><span class="sxs-lookup"><span data-stu-id="847b3-117">hello first set of controls around balancing are a set of timers.</span></span> <span data-ttu-id="847b3-118">Таймеров управляют как часто hello диспетчер ресурсов кластера проверяет кластера hello и выполняет действия по исправлению.</span><span class="sxs-lookup"><span data-stu-id="847b3-118">These timers govern how often hello Cluster Resource Manager examines hello cluster and takes corrective actions.</span></span>

<span data-ttu-id="847b3-119">Каждый из этих различных типов диспетчер ресурсов кластера можно внести исправления приветствия управляется другой таймер, который управляет частотой его.</span><span class="sxs-lookup"><span data-stu-id="847b3-119">Each of these different types of corrections hello Cluster Resource Manager can make is controlled by a different timer that governs its frequency.</span></span> <span data-ttu-id="847b3-120">При каждом таймеров hello расписанию.</span><span class="sxs-lookup"><span data-stu-id="847b3-120">When each timer fires, hello task is scheduled.</span></span> <span data-ttu-id="847b3-121">По умолчанию hello диспетчера ресурсов:</span><span class="sxs-lookup"><span data-stu-id="847b3-121">By default hello Resource Manager:</span></span>

* <span data-ttu-id="847b3-122">проверяет состояние и применяет обновления (например, записывает, что узел не работает) каждые 1/10 секунды;</span><span class="sxs-lookup"><span data-stu-id="847b3-122">scans its state and applies updates (like recording that a node is down) every 1/10th of a second</span></span>
* <span data-ttu-id="847b3-123">Устанавливает флаг Проверка размещения hello</span><span class="sxs-lookup"><span data-stu-id="847b3-123">sets hello placement check flag</span></span> 
* <span data-ttu-id="847b3-124">Устанавливает флаг проверки ограничения hello каждую секунду</span><span class="sxs-lookup"><span data-stu-id="847b3-124">sets hello constraint check flag every second</span></span>
* <span data-ttu-id="847b3-125">Задает hello балансировки флаг каждые пять секунд.</span><span class="sxs-lookup"><span data-stu-id="847b3-125">sets hello balancing flag every five seconds.</span></span>

<span data-ttu-id="847b3-126">Ниже приведены примеры hello конфигурации, управляющие таймеров.</span><span class="sxs-lookup"><span data-stu-id="847b3-126">Examples of hello configuration governing these timers are below:</span></span>

<span data-ttu-id="847b3-127">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="847b3-127">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

<span data-ttu-id="847b3-128">Для автономных развертываний используется ClusterConfig.json, а для размещенных в Azure кластеров — Template.json.</span><span class="sxs-lookup"><span data-stu-id="847b3-128">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PLBRefreshGap",
          "value": "0.10"
      },
      {
          "name": "MinPlacementInterval",
          "value": "1.0"
      },
      {
          "name": "MinConstraintCheckInterval",
          "value": "1.0"
      },
      {
          "name": "MinLoadBalancingInterval",
          "value": "5.0"
      }
    ]
  }
]
```

<span data-ttu-id="847b3-129">Сегодня hello диспетчер ресурсов кластера выполняет только одно из этих действий одновременно, последовательно.</span><span class="sxs-lookup"><span data-stu-id="847b3-129">Today hello Cluster Resource Manager only performs one of these actions at a time, sequentially.</span></span> <span data-ttu-id="847b3-130">Именно поэтому мы ссылаться таймеры toothese как «минимальный интервалы» и получить действия при таймеры hello ходить «флаги параметр» hello.</span><span class="sxs-lookup"><span data-stu-id="847b3-130">This is why we refer toothese timers as “minimum intervals” and hello actions that get taken when hello timers go off as "setting flags".</span></span> <span data-ttu-id="847b3-131">Например диспетчер ресурсов кластера берет на себя ожидающие приветствия запрашивает toocreate службы перед hello кластера балансировки.</span><span class="sxs-lookup"><span data-stu-id="847b3-131">For example, hello Cluster Resource Manager takes care of pending requests toocreate services before balancing hello cluster.</span></span> <span data-ttu-id="847b3-132">Как видите, интервал времени по умолчанию hello, указанные hello диспетчер ресурсов кластера сканирует ничего его потребности toodo часто.</span><span class="sxs-lookup"><span data-stu-id="847b3-132">As you can see by hello default time intervals specified, hello Cluster Resource Manager scans for anything it needs toodo frequently.</span></span> <span data-ttu-id="847b3-133">Обычно это означает, что hello набор изменений, внесенных на каждом шаге мал.</span><span class="sxs-lookup"><span data-stu-id="847b3-133">Normally this means that hello set of changes made during each step is small.</span></span> <span data-ttu-id="847b3-134">Часто внесения небольших изменений позволяет hello toobe диспетчер ресурсов кластера отвечать на запросы при кластера hello произойдет следующее.</span><span class="sxs-lookup"><span data-stu-id="847b3-134">Making small changes frequently allows hello Cluster Resource Manager toobe responsive when things happen in hello cluster.</span></span> <span data-ttu-id="847b3-135">Hello таймеры по умолчанию предоставляют некоторые пакетной обработки поскольку многие hello же типы событий, как правило, toooccur одновременно.</span><span class="sxs-lookup"><span data-stu-id="847b3-135">hello default timers provide some batching since many of hello same types of events tend toooccur simultaneously.</span></span> 

<span data-ttu-id="847b3-136">Например, когда происходит сбой узлов, то может выполняться одновременная обработка доменов сбоя целиком.</span><span class="sxs-lookup"><span data-stu-id="847b3-136">For example, when nodes fail they can do so entire fault domains at a time.</span></span> <span data-ttu-id="847b3-137">Все эти ошибки регистрируются во время hello следующее состояние обновления после hello *PLBRefreshGap*.</span><span class="sxs-lookup"><span data-stu-id="847b3-137">All these failures are captured during hello next state update after hello *PLBRefreshGap*.</span></span> <span data-ttu-id="847b3-138">исправления Hello определяются в ходе hello после размещения, проверки ограничений и балансировка запусков.</span><span class="sxs-lookup"><span data-stu-id="847b3-138">hello corrections are determined during hello following placement, constraint check, and balancing runs.</span></span> <span data-ttu-id="847b3-139">По умолчанию hello диспетчер ресурсов кластера не сканирования часы изменений в кластере hello и попытке tooaddress все изменения за один раз.</span><span class="sxs-lookup"><span data-stu-id="847b3-139">By default hello Cluster Resource Manager is not scanning through hours of changes in hello cluster and trying tooaddress all changes at once.</span></span> <span data-ttu-id="847b3-140">Это может привести к toobursts высок.</span><span class="sxs-lookup"><span data-stu-id="847b3-140">Doing so would lead toobursts of churn.</span></span>

<span data-ttu-id="847b3-141">Hello диспетчер ресурсов кластера необходимо также toodetermine некоторые дополнительные сведения, если кластер hello несбалансированных.</span><span class="sxs-lookup"><span data-stu-id="847b3-141">hello Cluster Resource Manager also needs some additional information toodetermine if hello cluster imbalanced.</span></span> <span data-ttu-id="847b3-142">Для этого используются два других элемента конфигурации: *пороговые значения балансировки* и *пороговые значения активности*.</span><span class="sxs-lookup"><span data-stu-id="847b3-142">For that we have two other pieces of configuration: *BalancingThresholds* and *ActivityThresholds*.</span></span>

## <a name="balancing-thresholds"></a><span data-ttu-id="847b3-143">Пороговые значения балансировки</span><span class="sxs-lookup"><span data-stu-id="847b3-143">Balancing thresholds</span></span>
<span data-ttu-id="847b3-144">Пороговое значение балансировки может hello главного элемента управления для запуска перераспределения.</span><span class="sxs-lookup"><span data-stu-id="847b3-144">A Balancing Threshold is hello main control for triggering rebalancing.</span></span> <span data-ttu-id="847b3-145">Hello балансировки пороговое значение метрики — _отношение_.</span><span class="sxs-lookup"><span data-stu-id="847b3-145">hello Balancing Threshold for a metric is a _ratio_.</span></span> <span data-ttu-id="847b3-146">Если hello нагрузки для метрики на hello наиболее загружен узел, деленное hello интенсивность нагрузки на hello бы загрузить узел превышает эта метрика *BalancingThreshold*, то hello кластера не сбалансирована.</span><span class="sxs-lookup"><span data-stu-id="847b3-146">If hello load for a metric on hello most loaded node divided by hello amount of load on hello least loaded node exceeds that metric's *BalancingThreshold*, then hello cluster is imbalanced.</span></span> <span data-ttu-id="847b3-147">В результате балансировки — триггеру hello Далее время hello проверку диспетчер ресурсов кластера.</span><span class="sxs-lookup"><span data-stu-id="847b3-147">As a result balancing is triggered hello next time hello Cluster Resource Manager checks.</span></span> <span data-ttu-id="847b3-148">Hello *MinLoadBalancingInterval* таймера определяет, как часто hello диспетчер ресурсов кластера должна проверять при необходимости перераспределения.</span><span class="sxs-lookup"><span data-stu-id="847b3-148">hello *MinLoadBalancingInterval* timer defines how often hello Cluster Resource Manager should check if rebalancing is necessary.</span></span> <span data-ttu-id="847b3-149">Проверка не означает, что что-то действительно произойдет.</span><span class="sxs-lookup"><span data-stu-id="847b3-149">Checking doesn't mean that anything happens.</span></span> 

<span data-ttu-id="847b3-150">Пороговые значения балансировки определяются на основе метрики как часть определения кластера hello.</span><span class="sxs-lookup"><span data-stu-id="847b3-150">Balancing Thresholds are defined on a per-metric basis as a part of hello cluster definition.</span></span> <span data-ttu-id="847b3-151">Дополнительные сведения о метриках см. в [этой статье](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="847b3-151">For more information on metrics, check out [this article](service-fabric-cluster-resource-manager-metrics.md).</span></span>

<span data-ttu-id="847b3-152">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="847b3-152">ClusterManifest.xml</span></span>

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

<span data-ttu-id="847b3-153">Для автономных развертываний используется ClusterConfig.json, а для размещенных в Azure кластеров — Template.json.</span><span class="sxs-lookup"><span data-stu-id="847b3-153">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "MetricBalancingThresholds",
    "parameters": [
      {
          "name": "MetricName1",
          "value": "2"
      },
      {
          "name": "MetricName2",
          "value": "3.5"
      }
    ]
  }
]
```

<span data-ttu-id="847b3-154"><center>
![Пример порогового значения балансировки][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="847b3-154"><center>
![Balancing Threshold Example][Image1]
</center></span></span>

<span data-ttu-id="847b3-155">В этом примере каждая служба использует одну единицу определенной метрики.</span><span class="sxs-lookup"><span data-stu-id="847b3-155">In this example, each service is consuming one unit of some metric.</span></span> <span data-ttu-id="847b3-156">В примере hello top hello максимальной нагрузки на узле, равно 5, а hello минимальное значение — два.</span><span class="sxs-lookup"><span data-stu-id="847b3-156">In hello top example, hello maximum load on a node is five and hello minimum is two.</span></span> <span data-ttu-id="847b3-157">Предположим, что hello балансировки пороговое значение для этой метрики, равно трем.</span><span class="sxs-lookup"><span data-stu-id="847b3-157">Let’s say that hello balancing threshold for this metric is three.</span></span> <span data-ttu-id="847b3-158">Так как отношение hello в кластере hello 5/2 = 2.5, которое меньше, чем hello указало балансировки порогового значения трех, hello кластера сбалансирован.</span><span class="sxs-lookup"><span data-stu-id="847b3-158">Since hello ratio in hello cluster is 5/2 = 2.5 and that is less than hello specified balancing threshold of three, hello cluster is balanced.</span></span> <span data-ttu-id="847b3-159">Без балансировки срабатывает, когда проверяет hello диспетчер ресурсов кластера.</span><span class="sxs-lookup"><span data-stu-id="847b3-159">No balancing is triggered when hello Cluster Resource Manager checks.</span></span>

<span data-ttu-id="847b3-160">В примере hello нижней hello максимальной нагрузки на узле равно 10, пока hello минимальное значение — 2, приведет к соотношение пяти.</span><span class="sxs-lookup"><span data-stu-id="847b3-160">In hello bottom example, hello maximum load on a node is 10, while hello minimum is two, resulting in a ratio of five.</span></span> <span data-ttu-id="847b3-161">Пять больше указанного порога балансировки hello из трех для этой метрики.</span><span class="sxs-lookup"><span data-stu-id="847b3-161">Five is greater than hello designated balancing threshold of three for that metric.</span></span> <span data-ttu-id="847b3-162">В результате балансировки выполнения будет запланированных Далее hello время балансировки активируется таймера.</span><span class="sxs-lookup"><span data-stu-id="847b3-162">As a result, a rebalancing run will be scheduled next time hello balancing timer fires.</span></span> <span data-ttu-id="847b3-163">В подобной ситуации некоторые нагрузки — обычно распределенных tooNode3.</span><span class="sxs-lookup"><span data-stu-id="847b3-163">In a situation like this some load is usually distributed tooNode3.</span></span> <span data-ttu-id="847b3-164">Так как диспетчер ресурсов кластера Service Fabric hello не использует жадном подход, повышению нагрузки может быть распределенных tooNode2.</span><span class="sxs-lookup"><span data-stu-id="847b3-164">Because hello Service Fabric Cluster Resource Manager doesn't use a greedy approach, some load could also be distributed tooNode2.</span></span> 

<span data-ttu-id="847b3-165"><center>
![Действия в примере порогового значения балансировки][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="847b3-165"><center>
![Balancing Threshold Example Actions][Image2]
</center></span></span>

> [!NOTE]
> <span data-ttu-id="847b3-166">Для управления нагрузкой в кластере применяются две разные стратегии балансировки.</span><span class="sxs-lookup"><span data-stu-id="847b3-166">"Balancing" handles two different strategies for managing load in your cluster.</span></span> <span data-ttu-id="847b3-167">стратегии по умолчанию Hello, hello использует диспетчер ресурсов кластера представляет собой toodistribute нагрузку между узлами кластера hello hello.</span><span class="sxs-lookup"><span data-stu-id="847b3-167">hello default strategy that hello Cluster Resource Manager uses is toodistribute load across hello nodes in hello cluster.</span></span> <span data-ttu-id="847b3-168">Hello других стратегией является [дефрагментации](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="847b3-168">hello other strategy is [defragmentation](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span></span> <span data-ttu-id="847b3-169">Дефрагментация выполняется во время hello же балансировки запуска.</span><span class="sxs-lookup"><span data-stu-id="847b3-169">Defragmentation is performed during hello same balancing run.</span></span> <span data-ttu-id="847b3-170">Hello стратегии балансировки и дефрагментация может использоваться для различных показателей hello одного кластера.</span><span class="sxs-lookup"><span data-stu-id="847b3-170">hello balancing and defragmentation strategies can be used for different metrics within hello same cluster.</span></span> <span data-ttu-id="847b3-171">У службы могут быть метрики балансировки и дефрагментации.</span><span class="sxs-lookup"><span data-stu-id="847b3-171">A service can have both balancing and defragmentation metrics.</span></span> <span data-ttu-id="847b3-172">Для метрик дефрагментации hello доля hello загружает в триггерах кластера hello перераспределения, когда это _ниже_ hello балансировки пороговое значение.</span><span class="sxs-lookup"><span data-stu-id="847b3-172">For defragmentation metrics, hello ratio of hello loads in hello cluster triggers rebalancing when it is _below_ hello balancing threshold.</span></span> 
>

<span data-ttu-id="847b3-173">Получение ниже hello балансировки пороговое значение является задача.</span><span class="sxs-lookup"><span data-stu-id="847b3-173">Getting below hello balancing threshold is not an explicit goal.</span></span> <span data-ttu-id="847b3-174">Пороговые значения балансировки — всего лишь *триггеры*.</span><span class="sxs-lookup"><span data-stu-id="847b3-174">Balancing Thresholds are just a *trigger*.</span></span> <span data-ttu-id="847b3-175">При балансировку запусков, hello диспетчер ресурсов кластера определяет какие улучшения, его можно сделать, если таковые имеются.</span><span class="sxs-lookup"><span data-stu-id="847b3-175">When balancing runs, hello Cluster Resource Manager determines what improvements it can make, if any.</span></span> <span data-ttu-id="847b3-176">Сам по себе запуск балансировки не означает, что что-либо будет перемещено.</span><span class="sxs-lookup"><span data-stu-id="847b3-176">Just because a balancing search is kicked off doesn't mean anything moves.</span></span> <span data-ttu-id="847b3-177">Иногда hello кластер — toocorrect сбалансирована, но слишком ограничением.</span><span class="sxs-lookup"><span data-stu-id="847b3-177">Sometimes hello cluster is imbalanced but too constrained toocorrect.</span></span> <span data-ttu-id="847b3-178">Кроме того, улучшения hello требуют перемещений, которые являются слишком [дорогостоящих](service-fabric-cluster-resource-manager-movement-cost.md)).</span><span class="sxs-lookup"><span data-stu-id="847b3-178">Alternatively, hello improvements require movements that are too [costly](service-fabric-cluster-resource-manager-movement-cost.md)).</span></span>

## <a name="activity-thresholds"></a><span data-ttu-id="847b3-179">пороговые значения активности</span><span class="sxs-lookup"><span data-stu-id="847b3-179">Activity thresholds</span></span>
<span data-ttu-id="847b3-180">Иногда, несмотря на то, что узлы являются относительно несбалансированных, hello *общее* объем нагрузки в кластере hello невелик.</span><span class="sxs-lookup"><span data-stu-id="847b3-180">Sometimes, although nodes are relatively imbalanced, hello *total* amount of load in hello cluster is low.</span></span> <span data-ttu-id="847b3-181">отсутствие Hello нагрузки может быть временной dip, или тем, что кластер hello новый и просто начало начальной загрузки.</span><span class="sxs-lookup"><span data-stu-id="847b3-181">hello lack of load could be a transient dip, or because hello cluster is new and just getting bootstrapped.</span></span> <span data-ttu-id="847b3-182">В любом случае вы можете не toospend время hello кластера балансировки, так как имеется небольшая toobe прибыли.</span><span class="sxs-lookup"><span data-stu-id="847b3-182">In either case, you may not want toospend time balancing hello cluster because there’s little toobe gained.</span></span> <span data-ttu-id="847b3-183">Hello кластера был изменен балансировки, следует потратить сети и вычислений без внесения все большие объекты toomove ресурсов *абсолютный* различие.</span><span class="sxs-lookup"><span data-stu-id="847b3-183">If hello cluster underwent balancing, you’d spend network and compute resources toomove things around without making any large *absolute* difference.</span></span> <span data-ttu-id="847b3-184">Перемещает tooavoid ненужные, уже есть элемент управления называется пороговые значения действий.</span><span class="sxs-lookup"><span data-stu-id="847b3-184">tooavoid unnecessary moves, there’s another control known as Activity Thresholds.</span></span> <span data-ttu-id="847b3-185">Пороговые значения действий позволяет toospecify некоторые абсолютный нижняя граница для действия.</span><span class="sxs-lookup"><span data-stu-id="847b3-185">Activity Thresholds allows you toospecify some absolute lower bound for activity.</span></span> <span data-ttu-id="847b3-186">Если узел не превышает это пороговое значение, балансировки не срабатывает, даже если hello балансировки порога.</span><span class="sxs-lookup"><span data-stu-id="847b3-186">If no node is over this threshold, balancing isn't triggered even if hello Balancing Threshold is met.</span></span>

<span data-ttu-id="847b3-187">Предположим, что для этой метрики задано пороговое значение балансировки, равное 3.</span><span class="sxs-lookup"><span data-stu-id="847b3-187">Let’s say that we retain our Balancing Threshold of three for this metric.</span></span> <span data-ttu-id="847b3-188">Также предположим, что пороговое значение активности равно 1536.</span><span class="sxs-lookup"><span data-stu-id="847b3-188">Let's also say we have an Activity Threshold of 1536.</span></span> <span data-ttu-id="847b3-189">В первом случае hello хотя несбалансированных каждого hello hello кластера балансировки пороговое значение не является действие пороговое значение не соответствует требованиям узла, поэтому ничего не происходит.</span><span class="sxs-lookup"><span data-stu-id="847b3-189">In hello first case, while hello cluster is imbalanced per hello Balancing Threshold there's no node meets that Activity Threshold, so nothing happens.</span></span> <span data-ttu-id="847b3-190">В примере hello нижней Node1 превышает пороговое значение действие hello.</span><span class="sxs-lookup"><span data-stu-id="847b3-190">In hello bottom example, Node1 is over hello Activity Threshold.</span></span> <span data-ttu-id="847b3-191">Поскольку оба hello пороговое значение для балансировки и hello действия пороговое значение для показателя hello превышены, балансировки запланирован.</span><span class="sxs-lookup"><span data-stu-id="847b3-191">Since both hello Balancing Threshold and hello Activity Threshold for hello metric are exceeded, balancing is scheduled.</span></span> <span data-ttu-id="847b3-192">В качестве примера рассмотрим следующие схемы hello.</span><span class="sxs-lookup"><span data-stu-id="847b3-192">As an example, let's look at hello following diagram:</span></span> 

<span data-ttu-id="847b3-193"><center>
![Пример порогового значения активности][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="847b3-193"><center>
![Activity Threshold Example][Image3]
</center></span></span>

<span data-ttu-id="847b3-194">Как и в пороговые значения балансировки пороговые значения действий, определенных на метрики через hello определения кластера:</span><span class="sxs-lookup"><span data-stu-id="847b3-194">Just like Balancing Thresholds, Activity Thresholds are defined per-metric via hello cluster definition:</span></span>

<span data-ttu-id="847b3-195">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="847b3-195">ClusterManifest.xml</span></span>

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

<span data-ttu-id="847b3-196">Для автономных развертываний используется ClusterConfig.json, а для размещенных в Azure кластеров — Template.json.</span><span class="sxs-lookup"><span data-stu-id="847b3-196">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "MetricActivityThresholds",
    "parameters": [
      {
          "name": "Memory",
          "value": "1536"
      }
    ]
  }
]
```

<span data-ttu-id="847b3-197">Пороговые значения балансировки нагрузки и действия имеют связанные tooa конкретную метрику - балансировки запускается только в том случае, если оба hello балансировки пороговое значение и действие порогового значения для hello одинаковую метрику.</span><span class="sxs-lookup"><span data-stu-id="847b3-197">Balancing and activity thresholds are both tied tooa specific metric - balancing is triggered only if both hello Balancing Threshold and Activity Threshold is exceeded for hello same metric.</span></span>

## <a name="balancing-services-together"></a><span data-ttu-id="847b3-198">Одновременная балансировка служб</span><span class="sxs-lookup"><span data-stu-id="847b3-198">Balancing services together</span></span>
<span data-ttu-id="847b3-199">Является несбалансированных hello кластера или не является решением всего кластера.</span><span class="sxs-lookup"><span data-stu-id="847b3-199">Whether hello cluster is imbalanced or not is a cluster-wide decision.</span></span> <span data-ttu-id="847b3-200">Тем не менее здесь очень способом hello перемещается реплик отдельные службы и экземпляры вокруг.</span><span class="sxs-lookup"><span data-stu-id="847b3-200">However, hello way we go about fixing it is moving individual service replicas and instances around.</span></span> <span data-ttu-id="847b3-201">Звучит разумно, не правда ли?</span><span class="sxs-lookup"><span data-stu-id="847b3-201">This makes sense, right?</span></span> <span data-ttu-id="847b3-202">Если вертикально памяти на одном узле tooit может вызывать несколько реплик или экземпляров.</span><span class="sxs-lookup"><span data-stu-id="847b3-202">If memory is stacked up on one node, multiple replicas or instances could be contributing tooit.</span></span> <span data-ttu-id="847b3-203">Исправление hello дисбаланс может потребоваться перемещение любой из реплики с отслеживанием состояния hello или экземпляры без сохранения состояния, в которых используется несбалансированных метрика hello.</span><span class="sxs-lookup"><span data-stu-id="847b3-203">Fixing hello imbalance could require moving any of hello stateful replicas or stateless instances that use hello imbalanced metric.</span></span>

<span data-ttu-id="847b3-204">Время от времени, что службы, которой не сам несбалансированных возвращает перемещен (Вспомните обсуждение hello локальных и глобальных весовые коэффициенты, которые ранее).</span><span class="sxs-lookup"><span data-stu-id="847b3-204">Occasionally though, a service that wasn’t itself imbalanced gets moved (remember hello discussion of local and global weights earlier).</span></span> <span data-ttu-id="847b3-205">Почему же служба перемещается, если все ее метрики сбалансированы?</span><span class="sxs-lookup"><span data-stu-id="847b3-205">Why would a service get moved when all that service’s metrics were balanced?</span></span> <span data-ttu-id="847b3-206">Рассмотрим пример.</span><span class="sxs-lookup"><span data-stu-id="847b3-206">Let’s see an example:</span></span>

- <span data-ttu-id="847b3-207">Возьмем для примера четыре службы: Service1, Service2, Service3 и Service4.</span><span class="sxs-lookup"><span data-stu-id="847b3-207">Let's say there are four services, Service1, Service2, Service3, and Service4.</span></span> 
- <span data-ttu-id="847b3-208">Служба Service1 передает метрики Metric1 и Metric2.</span><span class="sxs-lookup"><span data-stu-id="847b3-208">Service1 reports metrics Metric1 and Metric2.</span></span> 
- <span data-ttu-id="847b3-209">Служба Service2 передает метрики Metric2 и Metric3.</span><span class="sxs-lookup"><span data-stu-id="847b3-209">Service2 reports metrics Metric2 and Metric3.</span></span> 
- <span data-ttu-id="847b3-210">Служба Service3 передает метрики Metric3 и Metric4.</span><span class="sxs-lookup"><span data-stu-id="847b3-210">Service3 reports metrics Metric3 and Metric4.</span></span>
- <span data-ttu-id="847b3-211">Служба Service4 передает метрику Metric99.</span><span class="sxs-lookup"><span data-stu-id="847b3-211">Service4 reports metric Metric99.</span></span> 

<span data-ttu-id="847b3-212">Понимаете, к чему все это ведет? Это же цепочка!</span><span class="sxs-lookup"><span data-stu-id="847b3-212">Surely you can see where we’re going here: There's a chain!</span></span> <span data-ttu-id="847b3-213">Мы имеем дело не с четырьмя независимыми службами, а с тремя связанными службами и одной отдельной службой.</span><span class="sxs-lookup"><span data-stu-id="847b3-213">We don’t really have four independent services, we have three services that are related and one that is off on its own.</span></span>

<span data-ttu-id="847b3-214"><center>
![Одновременная балансировка служб][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="847b3-214"><center>
![Balancing Services Together][Image4]
</center></span></span>

<span data-ttu-id="847b3-215">Из-за этой цепочке существует вероятность, что дисбаланс метрик 1-4 может привести к реплики или экземпляры, принадлежащие tooservices toomove 1 – 3 вокруг.</span><span class="sxs-lookup"><span data-stu-id="847b3-215">Because of this chain, it's possible that an imbalance in metrics 1-4 can cause replicas or instances belonging tooservices 1-3 toomove around.</span></span> <span data-ttu-id="847b3-216">Кроме того, нам известно, что дисбаланс в метрике Metric1, Metric2 или Metric3 не вызовет перемещения в службе Service4.</span><span class="sxs-lookup"><span data-stu-id="847b3-216">We also know that an imbalance in Metrics 1, 2, or 3 can't cause movements in Service4.</span></span> <span data-ttu-id="847b3-217">Бы без точки после перемещения реплик hello или экземпляры, принадлежащие tooService4 вокруг может ничего не абсолютно tooimpact баланс hello метрик 1-3.</span><span class="sxs-lookup"><span data-stu-id="847b3-217">There would be no point since moving hello replicas or instances belonging tooService4 around can do absolutely nothing tooimpact hello balance of Metrics 1-3.</span></span>

<span data-ttu-id="847b3-218">Диспетчер ресурсов кластера Hello автоматически решает, какие службы связаны.</span><span class="sxs-lookup"><span data-stu-id="847b3-218">hello Cluster Resource Manager automatically figures out what services are related.</span></span> <span data-ttu-id="847b3-219">Добавление, удаление или изменение hello метрики для службы могут повлиять на их связи.</span><span class="sxs-lookup"><span data-stu-id="847b3-219">Adding, removing, or changing hello metrics for services can impact their relationships.</span></span> <span data-ttu-id="847b3-220">Например между двумя выполнениями балансировки Service2 было обновленные tooremove Metric2.</span><span class="sxs-lookup"><span data-stu-id="847b3-220">For example, between two runs of balancing Service2 may have been updated tooremove Metric2.</span></span> <span data-ttu-id="847b3-221">Это приводит к разрыву цепочки hello между Service1 и Service2.</span><span class="sxs-lookup"><span data-stu-id="847b3-221">This breaks hello chain between Service1 and Service2.</span></span> <span data-ttu-id="847b3-222">В этом случае две группы связанных служб превратятся в три.</span><span class="sxs-lookup"><span data-stu-id="847b3-222">Now instead of two groups of related services, there are three:</span></span>

<span data-ttu-id="847b3-223"><center>
![Одновременная балансировка служб][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="847b3-223"><center>
![Balancing Services Together][Image5]
</center></span></span>

## <a name="next-steps"></a><span data-ttu-id="847b3-224">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="847b3-224">Next steps</span></span>
* <span data-ttu-id="847b3-225">Показатели, как hello диспетчера ресурсов кластера Service Fabric управляет потребления и мощность в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="847b3-225">Metrics are how hello Service Fabric Cluster Resource Manger manages consumption and capacity in hello cluster.</span></span> <span data-ttu-id="847b3-226">Дополнительные сведения о метриках toolearn как tooconfigure, извлечение и возврат [в данной статье](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="847b3-226">toolearn more about metrics and how tooconfigure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>
* <span data-ttu-id="847b3-227">Стоимость перемещения — один из способов передачи сигналов toohello диспетчер ресурсов кластера, что некоторые службы являются toomove дороже, чем другие.</span><span class="sxs-lookup"><span data-stu-id="847b3-227">Movement Cost is one way of signaling toohello Cluster Resource Manager that certain services are more expensive toomove than others.</span></span> <span data-ttu-id="847b3-228">Дополнительные сведения о стоимость перемещения ссылаться слишком[в данной статье](service-fabric-cluster-resource-manager-movement-cost.md)</span><span class="sxs-lookup"><span data-stu-id="847b3-228">For more about movement cost, refer too[this article](service-fabric-cluster-resource-manager-movement-cost.md)</span></span>
* <span data-ttu-id="847b3-229">Hello диспетчер ресурсов кластера имеет несколько регулирования, которые можно настроить tooslow вниз обработки в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="847b3-229">hello Cluster Resource Manager has several throttles that you can configure tooslow down churn in hello cluster.</span></span> <span data-ttu-id="847b3-230">Обычно они не требуется, но при необходимости узнать о регулировках можно [здесь](service-fabric-cluster-resource-manager-advanced-throttling.md)</span><span class="sxs-lookup"><span data-stu-id="847b3-230">They're not normally necessary, but if you need them you can learn about them [here](service-fabric-cluster-resource-manager-advanced-throttling.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
