---
title: "Балансирование нагрузки кластера Azure Service Fabric | Документация Майкрософт"
description: "Общие сведения о распределении нагрузки в кластере с помощью диспетчера кластерных ресурсов Azure Service Fabric."
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
ms.openlocfilehash: 34eacb29f324025c1d2803c9690600227d3ec457
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="balancing-your-service-fabric-cluster"></a><span data-ttu-id="d7c3f-103">Балансировка кластера Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d7c3f-103">Balancing your service fabric cluster</span></span>
<span data-ttu-id="d7c3f-104">Диспетчер кластерных ресурсов Service Fabric поддерживает динамическое изменение нагрузки, реагируя на добавление и удаление узлов или служб.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-104">The Service Fabric Cluster Resource Manager supports dynamic load changes, reacting to additions or removals of nodes or services.</span></span> <span data-ttu-id="d7c3f-105">Он также автоматически исправляет нарушения ограничений и упреждающе перераспределяет нагрузку в кластере.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-105">It also automatically corrects constraint violations, and proactively rebalances the cluster.</span></span> <span data-ttu-id="d7c3f-106">Но как часто выполняются эти действия и что их инициирует?</span><span class="sxs-lookup"><span data-stu-id="d7c3f-106">But how often are these actions taken, and what triggers them?</span></span>

<span data-ttu-id="d7c3f-107">Диспетчер кластерных ресурсов выполняет три разные категории работы.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-107">There are three different categories of work that the Cluster Resource Manager performs.</span></span> <span data-ttu-id="d7c3f-108">К ним относятся:</span><span class="sxs-lookup"><span data-stu-id="d7c3f-108">They are:</span></span>

1. <span data-ttu-id="d7c3f-109">Размещение: на этом этапе происходит размещение отсутствующих метрик с отслеживанием состояния или без.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-109">Placement – this stage deals with placing any stateful replicas or stateless instances that are missing.</span></span> <span data-ttu-id="d7c3f-110">Размещаются как новые службы, так и реплики с отслеживанием состояния или экземпляры без отслеживания состояния, которые вызвали сбой.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-110">Placement includes both new services and handling stateful replicas or stateless instances that have failed.</span></span> <span data-ttu-id="d7c3f-111">Тут выполняется удаление реплик и экземпляров.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-111">Deleting and dropping replicas or instances are handled here.</span></span>
2. <span data-ttu-id="d7c3f-112">Проверка ограничений: на этом этапе проверяются и устраняются нарушения различных ограничений (правил) размещения в системе.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-112">Constraint Checks – this stage checks for and corrects violations of the different placement constraints (rules) within the system.</span></span> <span data-ttu-id="d7c3f-113">Примеры правил — это средства, предотвращающие избыточное использование ресурсов узлов, обеспечивающие соблюдение ограничений на размещение службы и т. п.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-113">Examples of rules are things like ensuring that nodes are not over capacity and that a service’s placement constraints are met.</span></span>
3. <span data-ttu-id="d7c3f-114">Балансировка: на этом этапе проверяется необходимость перераспределения нагрузки с учетом требуемого уровня нагрузки для различных метрик.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-114">Balancing – this stage checks to see if rebalancing is necessary based on the configured desired level of balance for different metrics.</span></span> <span data-ttu-id="d7c3f-115">Если это необходимо, предпринимается попытка найти более сбалансированную схему упорядочения в кластере.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-115">If so it attempts to find an arrangement in the cluster that is more balanced.</span></span>

## <a name="configuring-cluster-resource-manager-timers"></a><span data-ttu-id="d7c3f-116">Настройка таймеров диспетчера кластерных ресурсов</span><span class="sxs-lookup"><span data-stu-id="d7c3f-116">Configuring Cluster Resource Manager Timers</span></span>
<span data-ttu-id="d7c3f-117">Первый набор элементов управления балансировкой — это набор таймеров.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-117">The first set of controls around balancing are a set of timers.</span></span> <span data-ttu-id="d7c3f-118">Они определяют, как часто диспетчер кластерных ресурсов проверяет состояние кластера и выполняет корректирующие действия.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-118">These timers govern how often the Cluster Resource Manager examines the cluster and takes corrective actions.</span></span>

<span data-ttu-id="d7c3f-119">Каждым из типов исправлений, которые может внести Cluster Resource Manager, управляет соответствующий таймер, который определяет частоту их применения.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-119">Each of these different types of corrections the Cluster Resource Manager can make is controlled by a different timer that governs its frequency.</span></span> <span data-ttu-id="d7c3f-120">При каждом срабатывании таймера задача добавляется в расписание.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-120">When each timer fires, the task is scheduled.</span></span> <span data-ttu-id="d7c3f-121">По умолчанию диспетчер ресурсов:</span><span class="sxs-lookup"><span data-stu-id="d7c3f-121">By default the Resource Manager:</span></span>

* <span data-ttu-id="d7c3f-122">проверяет состояние и применяет обновления (например, записывает, что узел не работает) каждые 1/10 секунды;</span><span class="sxs-lookup"><span data-stu-id="d7c3f-122">scans its state and applies updates (like recording that a node is down) every 1/10th of a second</span></span>
* <span data-ttu-id="d7c3f-123">устанавливает флаг проверки размещения;</span><span class="sxs-lookup"><span data-stu-id="d7c3f-123">sets the placement check flag</span></span> 
* <span data-ttu-id="d7c3f-124">каждую секунду устанавливает флаг проверки ограничений;</span><span class="sxs-lookup"><span data-stu-id="d7c3f-124">sets the constraint check flag every second</span></span>
* <span data-ttu-id="d7c3f-125">устанавливает флаг балансировки каждые пять секунд.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-125">sets the balancing flag every five seconds.</span></span>

<span data-ttu-id="d7c3f-126">Ниже приведены примеры конфигураций, устанавливающих эти таймеры.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-126">Examples of the configuration governing these timers are below:</span></span>

<span data-ttu-id="d7c3f-127">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="d7c3f-127">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

<span data-ttu-id="d7c3f-128">Для автономных развертываний используется ClusterConfig.json, а для размещенных в Azure кластеров — Template.json.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-128">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="d7c3f-129">На сегодняшний день диспетчер кластерных ресурсов выполняет эти действия только по очереди.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-129">Today the Cluster Resource Manager only performs one of these actions at a time, sequentially.</span></span> <span data-ttu-id="d7c3f-130">Именно поэтому мы называем таймеры минимальными интервалами, а действия, которые выполняются при срабатывании таймеров, — флагами параметров.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-130">This is why we refer to these timers as “minimum intervals” and the actions that get taken when the timers go off as "setting flags".</span></span> <span data-ttu-id="d7c3f-131">Например, Cluster Resource Manager обрабатывает ожидающие запросы, чтобы создать службы перед балансировкой кластера.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-131">For example, the Cluster Resource Manager takes care of pending requests to create services before balancing the cluster.</span></span> <span data-ttu-id="d7c3f-132">Как можно видеть, заданные интервалы времени по умолчанию означают, что диспетчер кластерных ресурсов часто проверяет, какие задачи ему необходимо выполнять.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-132">As you can see by the default time intervals specified, the Cluster Resource Manager scans for anything it needs to do frequently.</span></span> <span data-ttu-id="d7c3f-133">Обычно это означает, что набор изменений, вносимых на каждом шаге, мал.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-133">Normally this means that the set of changes made during each step is small.</span></span> <span data-ttu-id="d7c3f-134">Благодаря высокой частоте внесения незначительных изменений диспетчер кластерных ресурсов чутко реагирует на то, что происходит в кластере.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-134">Making small changes frequently allows the Cluster Resource Manager to be responsive when things happen in the cluster.</span></span> <span data-ttu-id="d7c3f-135">Таймеры по умолчанию обеспечивают своего рода пакетную обработку, поскольку обычно множество событий одного типа происходят одновременно.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-135">The default timers provide some batching since many of the same types of events tend to occur simultaneously.</span></span> 

<span data-ttu-id="d7c3f-136">Например, когда происходит сбой узлов, то может выполняться одновременная обработка доменов сбоя целиком.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-136">For example, when nodes fail they can do so entire fault domains at a time.</span></span> <span data-ttu-id="d7c3f-137">Все эти сбои регистрируются во время следующего изменения состояния после *PLBRefreshGap*.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-137">All these failures are captured during the next state update after the *PLBRefreshGap*.</span></span> <span data-ttu-id="d7c3f-138">Исправления определяются во время следующих циклов размещения, проверки ограничений и балансировки нагрузки.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-138">The corrections are determined during the following placement, constraint check, and balancing runs.</span></span> <span data-ttu-id="d7c3f-139">По умолчанию Cluster Resource Manager ищет изменения в кластере, внесенные на протяжении нескольких часов, и не пытается обработать все изменения за один раз.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-139">By default the Cluster Resource Manager is not scanning through hours of changes in the cluster and trying to address all changes at once.</span></span> <span data-ttu-id="d7c3f-140">Такой подход может приводить к резкому увеличению оттока.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-140">Doing so would lead to bursts of churn.</span></span>

<span data-ttu-id="d7c3f-141">Чтобы выявить дисбаланс кластера, Cluster Resource Manager необходимы также некоторые дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-141">The Cluster Resource Manager also needs some additional information to determine if the cluster imbalanced.</span></span> <span data-ttu-id="d7c3f-142">Для этого используются два других элемента конфигурации: *пороговые значения балансировки* и *пороговые значения активности*.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-142">For that we have two other pieces of configuration: *BalancingThresholds* and *ActivityThresholds*.</span></span>

## <a name="balancing-thresholds"></a><span data-ttu-id="d7c3f-143">Пороговые значения балансировки</span><span class="sxs-lookup"><span data-stu-id="d7c3f-143">Balancing thresholds</span></span>
<span data-ttu-id="d7c3f-144">Пороговое значение балансировки — это основной элемент управления для запуска перераспределения нагрузки.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-144">A Balancing Threshold is the main control for triggering rebalancing.</span></span> <span data-ttu-id="d7c3f-145">Пороговое значение балансировки для метрики представляет собой _коэффициент_.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-145">The Balancing Threshold for a metric is a _ratio_.</span></span> <span data-ttu-id="d7c3f-146">Если нагрузка для метрики на наиболее загруженном узле, деленная на объем нагрузки на наименее загруженном узле, превышает *пороговое значение балансировки*, то кластер считается несбалансированным.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-146">If the load for a metric on the most loaded node divided by the amount of load on the least loaded node exceeds that metric's *BalancingThreshold*, then the cluster is imbalanced.</span></span> <span data-ttu-id="d7c3f-147">В результате балансировка запускается при очередной проверке службой Cluster Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-147">As a result balancing is triggered the next time the Cluster Resource Manager checks.</span></span> <span data-ttu-id="d7c3f-148">Таймер *MinLoadBalancingInterval* задает частоту, с которой диспетчер кластерных ресурсов проверяет необходимость перераспределения нагрузки.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-148">The *MinLoadBalancingInterval* timer defines how often the Cluster Resource Manager should check if rebalancing is necessary.</span></span> <span data-ttu-id="d7c3f-149">Проверка не означает, что что-то действительно произойдет.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-149">Checking doesn't mean that anything happens.</span></span> 

<span data-ttu-id="d7c3f-150">Пороговые значения балансировки задаются в определении кластера на основе метрик.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-150">Balancing Thresholds are defined on a per-metric basis as a part of the cluster definition.</span></span> <span data-ttu-id="d7c3f-151">Дополнительные сведения о метриках см. в [этой статье](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="d7c3f-151">For more information on metrics, check out [this article](service-fabric-cluster-resource-manager-metrics.md).</span></span>

<span data-ttu-id="d7c3f-152">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="d7c3f-152">ClusterManifest.xml</span></span>

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

<span data-ttu-id="d7c3f-153">Для автономных развертываний используется ClusterConfig.json, а для размещенных в Azure кластеров — Template.json.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-153">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="d7c3f-154"><center>
![Пример порогового значения балансировки][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="d7c3f-154"><center>
![Balancing Threshold Example][Image1]
</center></span></span>

<span data-ttu-id="d7c3f-155">В этом примере каждая служба использует одну единицу определенной метрики.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-155">In this example, each service is consuming one unit of some metric.</span></span> <span data-ttu-id="d7c3f-156">В верхнем примере максимальная нагрузка на узле составляет пять, а минимальная — два.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-156">In the top example, the maximum load on a node is five and the minimum is two.</span></span> <span data-ttu-id="d7c3f-157">Предположим, что пороговое значение балансировки для метрики — три.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-157">Let’s say that the balancing threshold for this metric is three.</span></span> <span data-ttu-id="d7c3f-158">Так как коэффициент для кластера 5/2 = 2,5, что меньше указанного порогового значения балансировки, равного трем, кластер сбалансирован.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-158">Since the ratio in the cluster is 5/2 = 2.5 and that is less than the specified balancing threshold of three, the cluster is balanced.</span></span> <span data-ttu-id="d7c3f-159">При очередной проверке службой Cluster Resource Manager балансировка не запускается.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-159">No balancing is triggered when the Cluster Resource Manager checks.</span></span>

<span data-ttu-id="d7c3f-160">В примере ниже максимальная нагрузка на узле составляет десять, а минимальная — два (значит, коэффициент будет равен пяти).</span><span class="sxs-lookup"><span data-stu-id="d7c3f-160">In the bottom example, the maximum load on a node is 10, while the minimum is two, resulting in a ratio of five.</span></span> <span data-ttu-id="d7c3f-161">Пять больше установленного порогового значения балансировки для этой метрики, равного трем.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-161">Five is greater than the designated balancing threshold of three for that metric.</span></span> <span data-ttu-id="d7c3f-162">В результате при следующем срабатывании таймера будет запланирован запуск перераспределения кластера.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-162">As a result, a rebalancing run will be scheduled next time the balancing timer fires.</span></span> <span data-ttu-id="d7c3f-163">В подобной ситуации часть нагрузки, как правило, распределяется на узел Node3.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-163">In a situation like this some load is usually distributed to Node3.</span></span> <span data-ttu-id="d7c3f-164">Так как диспетчер кластерных ресурсов Service Fabric не использует каскадный подход, часть нагрузки может также распределиться на узел Node2.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-164">Because the Service Fabric Cluster Resource Manager doesn't use a greedy approach, some load could also be distributed to Node2.</span></span> 

<span data-ttu-id="d7c3f-165"><center>
![Действия в примере порогового значения балансировки][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="d7c3f-165"><center>
![Balancing Threshold Example Actions][Image2]
</center></span></span>

> [!NOTE]
> <span data-ttu-id="d7c3f-166">Для управления нагрузкой в кластере применяются две разные стратегии балансировки.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-166">"Balancing" handles two different strategies for managing load in your cluster.</span></span> <span data-ttu-id="d7c3f-167">Стратегия по умолчанию, которую использует диспетчер кластерных ресурсов, заключается в распределении нагрузки между узлами в кластере.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-167">The default strategy that the Cluster Resource Manager uses is to distribute load across the nodes in the cluster.</span></span> <span data-ttu-id="d7c3f-168">Другой стратегией является [дефрагментация](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="d7c3f-168">The other strategy is [defragmentation](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span></span> <span data-ttu-id="d7c3f-169">Дефрагментация выполняется во время того же цикла балансировки.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-169">Defragmentation is performed during the same balancing run.</span></span> <span data-ttu-id="d7c3f-170">Стратегии балансировки и дефрагментации могут использоваться для различных метрик в одном и том же кластере.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-170">The balancing and defragmentation strategies can be used for different metrics within the same cluster.</span></span> <span data-ttu-id="d7c3f-171">У службы могут быть метрики балансировки и дефрагментации.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-171">A service can have both balancing and defragmentation metrics.</span></span> <span data-ttu-id="d7c3f-172">Для метрик дефрагментации коэффициент нагрузки в кластере активирует перераспределение, когда его значение _ниже_ порогового значения балансировки.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-172">For defragmentation metrics, the ratio of the loads in the cluster triggers rebalancing when it is _below_ the balancing threshold.</span></span> 
>

<span data-ttu-id="d7c3f-173">Уменьшение разницы в нагрузке ниже заданного предела — это не главная цель.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-173">Getting below the balancing threshold is not an explicit goal.</span></span> <span data-ttu-id="d7c3f-174">Пороговые значения балансировки — всего лишь *триггеры*.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-174">Balancing Thresholds are just a *trigger*.</span></span> <span data-ttu-id="d7c3f-175">При выполнении балансировки диспетчер кластерных ресурсов определяет, какие улучшения он может внести, если это возможно.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-175">When balancing runs, the Cluster Resource Manager determines what improvements it can make, if any.</span></span> <span data-ttu-id="d7c3f-176">Сам по себе запуск балансировки не означает, что что-либо будет перемещено.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-176">Just because a balancing search is kicked off doesn't mean anything moves.</span></span> <span data-ttu-id="d7c3f-177">Иногда кластер несбалансирован, но слишком ограничен для того, чтобы это можно было исправить.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-177">Sometimes the cluster is imbalanced but too constrained to correct.</span></span> <span data-ttu-id="d7c3f-178">Кроме того, для внесения улучшений требуются перемещения, которые могут быть слишком [дорогостоящими](service-fabric-cluster-resource-manager-movement-cost.md).</span><span class="sxs-lookup"><span data-stu-id="d7c3f-178">Alternatively, the improvements require movements that are too [costly](service-fabric-cluster-resource-manager-movement-cost.md)).</span></span>

## <a name="activity-thresholds"></a><span data-ttu-id="d7c3f-179">пороговые значения активности</span><span class="sxs-lookup"><span data-stu-id="d7c3f-179">Activity thresholds</span></span>
<span data-ttu-id="d7c3f-180">Иногда узлы могут быть относительно несбалансированными, даже если *общий* объем нагрузки в кластере небольшой.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-180">Sometimes, although nodes are relatively imbalanced, the *total* amount of load in the cluster is low.</span></span> <span data-ttu-id="d7c3f-181">Отсутствие нагрузки может быть связано с ее временным снижением или с тем, что кластер только что создан и проходит начальную загрузку.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-181">The lack of load could be a transient dip, or because the cluster is new and just getting bootstrapped.</span></span> <span data-ttu-id="d7c3f-182">В любом случае в такой ситуации можно не тратить время на балансировку кластера, так как это вряд ли принесет ощутимые результаты.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-182">In either case, you may not want to spend time balancing the cluster because there’s little to be gained.</span></span> <span data-ttu-id="d7c3f-183">Если кластер прошел балансировку, вы только потратите сетевые и вычислительные ресурсы на перемещение данных, а в результате не ощутите *абсолютно* никакой разницы.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-183">If the cluster underwent balancing, you’d spend network and compute resources to move things around without making any large *absolute* difference.</span></span> <span data-ttu-id="d7c3f-184">Чтобы ненужных перемещений, можно воспользоваться еще одним элементом управления под названием "Пороговые значения активности".</span><span class="sxs-lookup"><span data-stu-id="d7c3f-184">To avoid unnecessary moves, there’s another control known as Activity Thresholds.</span></span> <span data-ttu-id="d7c3f-185">С его помощью можно задать абсолютное значение нижней границы активности.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-185">Activity Thresholds allows you to specify some absolute lower bound for activity.</span></span> <span data-ttu-id="d7c3f-186">Если это пороговое значение не превышено ни для одного узла, балансировка не запускается даже при достижении ее порогового значения.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-186">If no node is over this threshold, balancing isn't triggered even if the Balancing Threshold is met.</span></span>

<span data-ttu-id="d7c3f-187">Предположим, что для этой метрики задано пороговое значение балансировки, равное 3.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-187">Let’s say that we retain our Balancing Threshold of three for this metric.</span></span> <span data-ttu-id="d7c3f-188">Также предположим, что пороговое значение активности равно 1536.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-188">Let's also say we have an Activity Threshold of 1536.</span></span> <span data-ttu-id="d7c3f-189">В первом случае согласно пороговому значению балансировки кластер несбалансирован, однако ни один из узлов не превышает пороговое значение активности, поэтому ничего не происходит.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-189">In the first case, while the cluster is imbalanced per the Balancing Threshold there's no node meets that Activity Threshold, so nothing happens.</span></span> <span data-ttu-id="d7c3f-190">В примере ниже узел Node1 превышает пороговое значение активности.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-190">In the bottom example, Node1 is over the Activity Threshold.</span></span> <span data-ttu-id="d7c3f-191">Так как для метрики превышены пороговые значения балансировки и активности, планируется балансировка.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-191">Since both the Balancing Threshold and the Activity Threshold for the metric are exceeded, balancing is scheduled.</span></span> <span data-ttu-id="d7c3f-192">Например, рассмотрим схему ниже.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-192">As an example, let's look at the following diagram:</span></span> 

<span data-ttu-id="d7c3f-193"><center>
![Пример порогового значения активности][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="d7c3f-193"><center>
![Activity Threshold Example][Image3]
</center></span></span>

<span data-ttu-id="d7c3f-194">Как и пороговые значения балансировки, пороговые значения активности определяются в определении кластера на основе метрик:</span><span class="sxs-lookup"><span data-stu-id="d7c3f-194">Just like Balancing Thresholds, Activity Thresholds are defined per-metric via the cluster definition:</span></span>

<span data-ttu-id="d7c3f-195">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="d7c3f-195">ClusterManifest.xml</span></span>

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

<span data-ttu-id="d7c3f-196">Для автономных развернутых служб используется ClusterConfig.json, а для размещенных в Azure кластеров — Template.json:</span><span class="sxs-lookup"><span data-stu-id="d7c3f-196">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="d7c3f-197">Пороговые значения балансировки и активности привязаны к определенной метрике. Балансировка запускается только тогда, когда оба эти пороговые значения превышены для одной и той же метрики.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-197">Balancing and activity thresholds are both tied to a specific metric - balancing is triggered only if both the Balancing Threshold and Activity Threshold is exceeded for the same metric.</span></span>

## <a name="balancing-services-together"></a><span data-ttu-id="d7c3f-198">Одновременная балансировка служб</span><span class="sxs-lookup"><span data-stu-id="d7c3f-198">Balancing services together</span></span>
<span data-ttu-id="d7c3f-199">Несбалансированность кластера определяется на уровне кластера.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-199">Whether the cluster is imbalanced or not is a cluster-wide decision.</span></span> <span data-ttu-id="d7c3f-200">Тем не менее она устраняется путем перемещения реплик или экземпляров отдельных служб.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-200">However, the way we go about fixing it is moving individual service replicas and instances around.</span></span> <span data-ttu-id="d7c3f-201">Звучит разумно, не правда ли?</span><span class="sxs-lookup"><span data-stu-id="d7c3f-201">This makes sense, right?</span></span> <span data-ttu-id="d7c3f-202">Если память накапливается в одном узле, это может быть вызвано сразу несколькими репликами или экземплярами.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-202">If memory is stacked up on one node, multiple replicas or instances could be contributing to it.</span></span> <span data-ttu-id="d7c3f-203">Для устранения дисбаланса может потребоваться перемещение всех реплик с отслеживанием состояния или экземпляров без отслеживания состояния, для которых используется несбалансированная метрика.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-203">Fixing the imbalance could require moving any of the stateful replicas or stateless instances that use the imbalanced metric.</span></span>

<span data-ttu-id="d7c3f-204">В отдельных случаях перемещается служба, которая сама по себе не была несбалансированной (вспомните обсуждение локальных и глобальных весов, приведенное ранее).</span><span class="sxs-lookup"><span data-stu-id="d7c3f-204">Occasionally though, a service that wasn’t itself imbalanced gets moved (remember the discussion of local and global weights earlier).</span></span> <span data-ttu-id="d7c3f-205">Почему же служба перемещается, если все ее метрики сбалансированы?</span><span class="sxs-lookup"><span data-stu-id="d7c3f-205">Why would a service get moved when all that service’s metrics were balanced?</span></span> <span data-ttu-id="d7c3f-206">Рассмотрим пример.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-206">Let’s see an example:</span></span>

- <span data-ttu-id="d7c3f-207">Возьмем для примера четыре службы: Service1, Service2, Service3 и Service4.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-207">Let's say there are four services, Service1, Service2, Service3, and Service4.</span></span> 
- <span data-ttu-id="d7c3f-208">Служба Service1 передает метрики Metric1 и Metric2.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-208">Service1 reports metrics Metric1 and Metric2.</span></span> 
- <span data-ttu-id="d7c3f-209">Служба Service2 передает метрики Metric2 и Metric3.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-209">Service2 reports metrics Metric2 and Metric3.</span></span> 
- <span data-ttu-id="d7c3f-210">Служба Service3 передает метрики Metric3 и Metric4.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-210">Service3 reports metrics Metric3 and Metric4.</span></span>
- <span data-ttu-id="d7c3f-211">Служба Service4 передает метрику Metric99.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-211">Service4 reports metric Metric99.</span></span> 

<span data-ttu-id="d7c3f-212">Понимаете, к чему все это ведет? Это же цепочка!</span><span class="sxs-lookup"><span data-stu-id="d7c3f-212">Surely you can see where we’re going here: There's a chain!</span></span> <span data-ttu-id="d7c3f-213">Мы имеем дело не с четырьмя независимыми службами, а с тремя связанными службами и одной отдельной службой.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-213">We don’t really have four independent services, we have three services that are related and one that is off on its own.</span></span>

<span data-ttu-id="d7c3f-214"><center>
![Одновременная балансировка служб][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="d7c3f-214"><center>
![Balancing Services Together][Image4]
</center></span></span>

<span data-ttu-id="d7c3f-215">Из-за этой цепочки вполне возможно, что дисбаланс в метриках Metric1–Metric4 может привести к перемещению реплик или экземпляров, относящихся к службам Service1–Service3.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-215">Because of this chain, it's possible that an imbalance in metrics 1-4 can cause replicas or instances belonging to services 1-3 to move around.</span></span> <span data-ttu-id="d7c3f-216">Кроме того, нам известно, что дисбаланс в метрике Metric1, Metric2 или Metric3 не вызовет перемещения в службе Service4.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-216">We also know that an imbalance in Metrics 1, 2, or 3 can't cause movements in Service4.</span></span> <span data-ttu-id="d7c3f-217">Это не имеет смысла, так как перемещение реплик или экземпляров службы Service4 никак не повлияет на баланс метрик Metric1–Metric3.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-217">There would be no point since moving the replicas or instances belonging to Service4 around can do absolutely nothing to impact the balance of Metrics 1-3.</span></span>

<span data-ttu-id="d7c3f-218">Диспетчер кластерных ресурсов автоматически определяет, какие службы связаны.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-218">The Cluster Resource Manager automatically figures out what services are related.</span></span> <span data-ttu-id="d7c3f-219">Добавление, удаление или изменение метрик для служб может влиять на их связи.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-219">Adding, removing, or changing the metrics for services can impact their relationships.</span></span> <span data-ttu-id="d7c3f-220">Например, между двумя циклами балансировки служба Service2 может быть изменена для удаления из нее метрики Metric2.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-220">For example, between two runs of balancing Service2 may have been updated to remove Metric2.</span></span> <span data-ttu-id="d7c3f-221">связь между службами S1 и S2 будет разорвана.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-221">This breaks the chain between Service1 and Service2.</span></span> <span data-ttu-id="d7c3f-222">В этом случае две группы связанных служб превратятся в три.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-222">Now instead of two groups of related services, there are three:</span></span>

<span data-ttu-id="d7c3f-223"><center>
![Одновременная балансировка служб][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="d7c3f-223"><center>
![Balancing Services Together][Image5]
</center></span></span>

## <a name="next-steps"></a><span data-ttu-id="d7c3f-224">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d7c3f-224">Next steps</span></span>
* <span data-ttu-id="d7c3f-225">Метрики показывают, как диспетчер кластерных ресурсов Service Fabric управляет потреблением и емкостью в кластере.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-225">Metrics are how the Service Fabric Cluster Resource Manger manages consumption and capacity in the cluster.</span></span> <span data-ttu-id="d7c3f-226">Чтобы узнать больше о метриках и их настройке, ознакомьтесь с [этой статьей](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="d7c3f-226">To learn more about metrics and how to configure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>
* <span data-ttu-id="d7c3f-227">Стоимость перемещения — один из способов сообщить диспетчеру кластерных ресурсов, что некоторые службы перемещать затратнее, чем остальные.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-227">Movement Cost is one way of signaling to the Cluster Resource Manager that certain services are more expensive to move than others.</span></span> <span data-ttu-id="d7c3f-228">Дополнительные сведения о стоимости перемещения см. в [этой статье](service-fabric-cluster-resource-manager-movement-cost.md).</span><span class="sxs-lookup"><span data-stu-id="d7c3f-228">For more about movement cost, refer to [this article](service-fabric-cluster-resource-manager-movement-cost.md)</span></span>
* <span data-ttu-id="d7c3f-229">В диспетчере кластерных ресурсов имеется несколько регулировок, которые можно настроить, чтобы замедлить отток в кластере.</span><span class="sxs-lookup"><span data-stu-id="d7c3f-229">The Cluster Resource Manager has several throttles that you can configure to slow down churn in the cluster.</span></span> <span data-ttu-id="d7c3f-230">Обычно они не требуется, но при необходимости узнать о регулировках можно [здесь](service-fabric-cluster-resource-manager-advanced-throttling.md)</span><span class="sxs-lookup"><span data-stu-id="d7c3f-230">They're not normally necessary, but if you need them you can learn about them [here](service-fabric-cluster-resource-manager-advanced-throttling.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
