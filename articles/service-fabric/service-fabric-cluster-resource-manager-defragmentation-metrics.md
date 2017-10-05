---
title: "Дефрагментация метрик в кластере Azure Service Fabric | Документация Майкрософт"
description: "Общие сведения об использовании дефрагментации или упаковки в качестве стратегии для метрик в кластере Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: e5ebfae5-c8f7-4d6c-9173-3e22a9730552
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: b253cc07066092aa82d218c9c82c8aac502245a8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="defragmentation-of-metrics-and-load-in-service-fabric"></a><span data-ttu-id="4c12f-103">Дефрагментация метрик и нагрузки в Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4c12f-103">Defragmentation of metrics and load in Service Fabric</span></span>
<span data-ttu-id="4c12f-104">По умолчанию диспетчер кластерных ресурсов Service Fabric использует для метрик нагрузки стратегию распределения нагрузки.</span><span class="sxs-lookup"><span data-stu-id="4c12f-104">The Service Fabric Cluster Resource Manager's default strategy for managing load metrics in the cluster is to distribute the load.</span></span> <span data-ttu-id="4c12f-105">Обеспечение равномерного использования узлов позволяет избежать перегруженных и недогруженных точек, которые приводят к состязанию за ресурсы и их нецелесообразной растрате.</span><span class="sxs-lookup"><span data-stu-id="4c12f-105">Ensuring that nodes are evenly utilized avoids hot and cold spots that lead to both contention and wasted resources.</span></span> <span data-ttu-id="4c12f-106">Распределение рабочих нагрузок в кластере — самый безопасный способ минимизировать риск сбоев, так как единичный сбой не сможет вывести из строя значительную часть рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="4c12f-106">Distributing workloads in the cluster is also the safest in terms of surviving failures since it ensures that a failure doesn’t take out a large percentage of a given workload.</span></span> 

<span data-ttu-id="4c12f-107">Диспетчер кластерных ресурсов Service Fabric поддерживает также другую стратегию управления нагрузкой — дефрагментацию.</span><span class="sxs-lookup"><span data-stu-id="4c12f-107">The Service Fabric Cluster Resource Manager does support a different strategy for managing load, which is defragmentation.</span></span> <span data-ttu-id="4c12f-108">Дефрагментация означает, что вместо распределения использования метрики по кластеру выполняется консолидация.</span><span class="sxs-lookup"><span data-stu-id="4c12f-108">Defragmentation means that instead of trying to distribute the utilization of a metric across the cluster, it is consolidated.</span></span> <span data-ttu-id="4c12f-109">Консолидация — это просто стратегия, обратная стратегии балансировки по умолчанию. Вместо сведения к минимуму среднего значения среднеквадратического отклонения нагрузки для метрики диспетчер кластерных ресурсов пытается увеличить это значение.</span><span class="sxs-lookup"><span data-stu-id="4c12f-109">Consolidation is just an inversion of the default balancing strategy – instead of minimizing the average standard deviation of metric load, the Cluster Resource Manager tries to increase it.</span></span>

## <a name="when-to-use-defragmentation"></a><span data-ttu-id="4c12f-110">Когда следует использовать дефрагментацию</span><span class="sxs-lookup"><span data-stu-id="4c12f-110">When to use defragmentation</span></span>
<span data-ttu-id="4c12f-111">При распределении нагрузки в кластере используется некоторая часть ресурсов на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="4c12f-111">Distributing load in the cluster consumes some of the resources on each node.</span></span> <span data-ttu-id="4c12f-112">Некоторые рабочие нагрузки создают огромные службы, потребляющие почти все или все ресурсы узла.</span><span class="sxs-lookup"><span data-stu-id="4c12f-112">Some workloads create services that are exceptionally large and consume most or all of a node.</span></span> <span data-ttu-id="4c12f-113">В таких случаях может оказаться, что при создании больших рабочих нагрузок ни на одном узле не будет достаточно ресурсов для их выполнения.</span><span class="sxs-lookup"><span data-stu-id="4c12f-113">In these cases, it's possible that when there are large workloads getting created that there isn't enough space on any node to run them.</span></span> <span data-ttu-id="4c12f-114">Большие рабочие нагрузки — не проблема в Service Fabric. Диспетчер кластерных ресурсов определяет, что ему нужно сделать, чтобы реорганизовать кластер и освободить место для большой рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="4c12f-114">Large workloads aren't a problem in Service Fabric; in these cases the Cluster Resource Manager determines that it needs to reorganize the cluster to make room for this large workload.</span></span> <span data-ttu-id="4c12f-115">Но тогда такой рабочей нагрузке нужно ожидать размещения в кластере.</span><span class="sxs-lookup"><span data-stu-id="4c12f-115">However, in the meantime that workload has to wait to be scheduled in the cluster.</span></span>

<span data-ttu-id="4c12f-116">Если перемещать нужно большое число служб и состояний, на размещение большой рабочей нагрузки в кластере потребуется много времени.</span><span class="sxs-lookup"><span data-stu-id="4c12f-116">If there are many services and state to move around, then it could take a long time for the large workload to be placed in the cluster.</span></span> <span data-ttu-id="4c12f-117">Это еще более вероятно, если другие рабочие нагрузки в кластере тоже большие, и их реорганизация требует много времени.</span><span class="sxs-lookup"><span data-stu-id="4c12f-117">This is more likely if other workloads in the cluster are also large and so take longer to reorganize.</span></span> <span data-ttu-id="4c12f-118">Разработчики Service Fabric замерили время создания службы, смоделировав такой сценарий.</span><span class="sxs-lookup"><span data-stu-id="4c12f-118">The Service Fabric team measured creation times in simulations of this scenario.</span></span> <span data-ttu-id="4c12f-119">Мы обнаружили, что создание больших служб занимает гораздо больше времени, когда использование кластера находится в пределах 30–50 %.</span><span class="sxs-lookup"><span data-stu-id="4c12f-119">We found that creating large services took much longer as soon as cluster utilization got above between 30% and 50%.</span></span> <span data-ttu-id="4c12f-120">Чтобы решить эту проблему, мы создали стратегию балансировки, основанную на дефрагментации.</span><span class="sxs-lookup"><span data-stu-id="4c12f-120">To handle this scenario, we introduced defragmentation as a balancing strategy.</span></span> <span data-ttu-id="4c12f-121">Мы обнаружили, что для крупных рабочих нагрузок, особенно чувствительных к задержкам при создании, дефрагментация существенно оптимизирует размещение нагрузок в кластере.</span><span class="sxs-lookup"><span data-stu-id="4c12f-121">We found that for large workloads, especially ones where creation time was important, defragmentation really helped those new workloads get scheduled in the cluster.</span></span>

<span data-ttu-id="4c12f-122">Вы можете настроить метрики дефрагментации, чтобы диспетчер кластерных ресурсов заранее группировал нагрузки служб на меньшем числе узлов.</span><span class="sxs-lookup"><span data-stu-id="4c12f-122">You can configure defragmentation metrics to have the Cluster Resource Manager to proactively try to condense the load of the services into fewer nodes.</span></span> <span data-ttu-id="4c12f-123">Это позволит практически всегда найти свободное место для больших служб без реорганизации кластера.</span><span class="sxs-lookup"><span data-stu-id="4c12f-123">This helps ensure that there is almost always room for large services without reorganizing the cluster.</span></span> <span data-ttu-id="4c12f-124">А так как отпадает необходимость реорганизовывать кластер, это позволяет быстро создавать большие рабочие нагрузки.</span><span class="sxs-lookup"><span data-stu-id="4c12f-124">Not having to reorganize the cluster allows creating large workloads quickly.</span></span>

<span data-ttu-id="4c12f-125">Для большинства клиентов дефрагментация не требуется.</span><span class="sxs-lookup"><span data-stu-id="4c12f-125">Most people don’t need defragmentation.</span></span> <span data-ttu-id="4c12f-126">Обычно службы небольшие, и для них нетрудно найти свободное место в кластере.</span><span class="sxs-lookup"><span data-stu-id="4c12f-126">Services are usually be small, so it’s not hard to find room for them in the cluster.</span></span> <span data-ttu-id="4c12f-127">Когда реорганизация возможна, она происходит быстро, так как большинство служб — небольшого размера, и они могут быть перемещены быстро и параллельно.</span><span class="sxs-lookup"><span data-stu-id="4c12f-127">When reorganization is possible, it goes quickly, again because most services are small and can be moved quickly and in parallel.</span></span> <span data-ttu-id="4c12f-128">Но если вы используете большие службы, которые должны создаваться быстро, то стратегия дефрагментации создана именно для вас.</span><span class="sxs-lookup"><span data-stu-id="4c12f-128">However, if you have large services and need them created quickly then the defragmentation strategy is for you.</span></span> <span data-ttu-id="4c12f-129">Далее мы обсудим достоинства и недостатки дефрагментации.</span><span class="sxs-lookup"><span data-stu-id="4c12f-129">We'll discuss the tradeoffs of using defragmentation next.</span></span> 

## <a name="defragmentation-tradeoffs"></a><span data-ttu-id="4c12f-130">Достоинства и недостатки дефрагментации</span><span class="sxs-lookup"><span data-stu-id="4c12f-130">Defragmentation tradeoffs</span></span>
<span data-ttu-id="4c12f-131">Дефрагментация может усугубить последствия сбоев, так как на узле, на котором произошел сбой, выполняется больше служб.</span><span class="sxs-lookup"><span data-stu-id="4c12f-131">Defragmentation can increase impactfulness of failures, since more services are running on nodes that fail.</span></span> <span data-ttu-id="4c12f-132">Дефрагментация может также увеличить затраты, так как в кластере необходимо обеспечить резервные ресурсы на случай создания больших рабочих нагрузок.</span><span class="sxs-lookup"><span data-stu-id="4c12f-132">Defragmentation can also increase costs, since resources in the cluster must be held in reserve, waiting for the creation of large workloads.</span></span>

<span data-ttu-id="4c12f-133">На следующей схеме показано визуальное представление двух кластеров, один из которых дефрагментирован, а другой — нет.</span><span class="sxs-lookup"><span data-stu-id="4c12f-133">The following diagram gives a visual representation of two clusters, one that is defragmented and one that is not.</span></span> 

<span data-ttu-id="4c12f-134"><center>
![Сравнение методов балансировки и дефрагментации кластеров][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="4c12f-134"><center>
![Comparing Balanced and Defragmented Clusters][Image1]
</center></span></span>

<span data-ttu-id="4c12f-135">Обратите внимание на число перемещений, необходимых для размещения крупного объекта службы в сценарии с балансировкой.</span><span class="sxs-lookup"><span data-stu-id="4c12f-135">In the balanced case, consider the number of movements that would be necessary to place one of the largest service objects.</span></span> <span data-ttu-id="4c12f-136">В дефрагментированном кластере большая рабочая нагрузка может быть размещена на узле 4 или 5 без ожидания перемещения каких-либо других служб.</span><span class="sxs-lookup"><span data-stu-id="4c12f-136">In the defragmented cluster, the large workload could be placed on nodes four or five without having to wait for any other services to move.</span></span>

## <a name="defragmentation-pros-and-cons"></a><span data-ttu-id="4c12f-137">Преимущества и недостатки дефрагментации</span><span class="sxs-lookup"><span data-stu-id="4c12f-137">Defragmentation pros and cons</span></span>
<span data-ttu-id="4c12f-138">О каких компромиссах идет речь?</span><span class="sxs-lookup"><span data-stu-id="4c12f-138">So what are those other conceptual tradeoffs?</span></span> <span data-ttu-id="4c12f-139">Вот на что следует обратить внимание:</span><span class="sxs-lookup"><span data-stu-id="4c12f-139">Here’s a quick table of things to think about:</span></span>

| <span data-ttu-id="4c12f-140">Плюсы дефрагментации</span><span class="sxs-lookup"><span data-stu-id="4c12f-140">Defragmentation Pros</span></span> | <span data-ttu-id="4c12f-141">Минусы дефрагментации</span><span class="sxs-lookup"><span data-stu-id="4c12f-141">Defragmentation Cons</span></span> |
| --- | --- |
| <span data-ttu-id="4c12f-142">Позволяет ускорить создание больших служб</span><span class="sxs-lookup"><span data-stu-id="4c12f-142">Allows faster creation of large services</span></span> |<span data-ttu-id="4c12f-143">Концентрирует нагрузку на меньшем числе узлов, увеличивая, таким образом, конкуренцию за ресурсы</span><span class="sxs-lookup"><span data-stu-id="4c12f-143">Concentrates load onto fewer nodes, increasing contention</span></span> |
| <span data-ttu-id="4c12f-144">Позволяет уменьшить перемещения данных в процессе создания</span><span class="sxs-lookup"><span data-stu-id="4c12f-144">Enables lower data movement during creation</span></span> |<span data-ttu-id="4c12f-145">Сбои могут затронуть больше служб и вызвать более серьезные последствия</span><span class="sxs-lookup"><span data-stu-id="4c12f-145">Failures can impact more services and cause more churn</span></span> |
| <span data-ttu-id="4c12f-146">Обеспечивает подробное описание требований и оптимальное использование пространства</span><span class="sxs-lookup"><span data-stu-id="4c12f-146">Allows rich description of requirements and reclamation of space</span></span> |<span data-ttu-id="4c12f-147">Более сложная общая настройка управления ресурсами</span><span class="sxs-lookup"><span data-stu-id="4c12f-147">More complex overall Resource Management configuration</span></span> |

<span data-ttu-id="4c12f-148">Для одного кластера можно одновременно применять метрики дефрагментации и обычного распределения.</span><span class="sxs-lookup"><span data-stu-id="4c12f-148">You can mix defragmented and normal metrics in the same cluster.</span></span> <span data-ttu-id="4c12f-149">Диспетчер ресурсов кластера пытается объединить метрики дефрагментации, насколько это возможно, и равномерно распределить все остальные.</span><span class="sxs-lookup"><span data-stu-id="4c12f-149">The Cluster Resource Manager tries to consolidate the defragmentation metrics as much as possible while spreading out the others.</span></span> <span data-ttu-id="4c12f-150">Результаты совмещения стратегий дефрагментации и балансировки зависят от нескольких факторов, включая следующие:</span><span class="sxs-lookup"><span data-stu-id="4c12f-150">The results of mixing defragmentation and balancing strategies depends on several factors, including:</span></span>
  - <span data-ttu-id="4c12f-151">соотношение числа метрик балансировки и метрик дефрагментации;</span><span class="sxs-lookup"><span data-stu-id="4c12f-151">the number of balancing metrics vs. the number of defragmentation metrics</span></span>
  - <span data-ttu-id="4c12f-152">использует ли какие-либо службы метрики обоих типов;</span><span class="sxs-lookup"><span data-stu-id="4c12f-152">Whether any service uses both types of metrics</span></span> 
  - <span data-ttu-id="4c12f-153">веса метрик;</span><span class="sxs-lookup"><span data-stu-id="4c12f-153">the metric weights</span></span>
  - <span data-ttu-id="4c12f-154">текущая нагрузка метрик.</span><span class="sxs-lookup"><span data-stu-id="4c12f-154">current metric loads</span></span>
  
<span data-ttu-id="4c12f-155">Для поиска оптимальной конфигурации нужно экспериментировать.</span><span class="sxs-lookup"><span data-stu-id="4c12f-155">Experimentation is required to determine the exact configuration necessary.</span></span> <span data-ttu-id="4c12f-156">Мы рекомендуем тщательно измерить рабочие нагрузки, прежде чем включать метрики дефрагментации в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="4c12f-156">We recommend thorough measurement of your workloads before you enable defragmentation metrics in production.</span></span> <span data-ttu-id="4c12f-157">Это особенно важно при сочетании метрик дефрагментации и балансировки в одной и той же службе.</span><span class="sxs-lookup"><span data-stu-id="4c12f-157">This is especially true when mixing defragmentation and balanced metrics within the same service.</span></span> 

## <a name="configuring-defragmentation-metrics"></a><span data-ttu-id="4c12f-158">Настройка метрик для дефрагментации</span><span class="sxs-lookup"><span data-stu-id="4c12f-158">Configuring defragmentation metrics</span></span>
<span data-ttu-id="4c12f-159">Решение о настройке метрик дефрагментации затрагивает весь кластер. Для дефрагментации можно выбрать отдельные метрики.</span><span class="sxs-lookup"><span data-stu-id="4c12f-159">Configuring defragmentation metrics is a global decision in the cluster, and individual metrics can be selected for defragmentation.</span></span> <span data-ttu-id="4c12f-160">В следующих фрагментах конфигурации показано, как настроить метрики для дефрагментации.</span><span class="sxs-lookup"><span data-stu-id="4c12f-160">The following config snippets show how to configure metrics for defragmentation.</span></span> <span data-ttu-id="4c12f-161">В этом случае метрика Metric1 настраивается в качестве метрики дефрагментации, а балансировка метрики Metric2 будет по-прежнему осуществляться в обычном режиме.</span><span class="sxs-lookup"><span data-stu-id="4c12f-161">In this case, "Metric1" is configured as a defragmentation metric, while "Metric2" will continue to be balanced normally.</span></span> 

<span data-ttu-id="4c12f-162">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="4c12f-162">ClusterManifest.xml:</span></span>

```xml
<Section Name="DefragmentationMetrics">
    <Parameter Name="Metric1" Value="true" />
    <Parameter Name="Metric2" Value="false" />
</Section>
```

<span data-ttu-id="4c12f-163">Для автономных развертываний используется ClusterConfig.json, а для размещенных в Azure кластеров — Template.json.</span><span class="sxs-lookup"><span data-stu-id="4c12f-163">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "DefragmentationMetrics",
    "parameters": [
      {
          "name": "Metric1",
          "value": "true"
      },
      {
          "name": "Metric2",
          "value": "false"
      }
    ]
  }
]
```


## <a name="next-steps"></a><span data-ttu-id="4c12f-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4c12f-164">Next steps</span></span>
- <span data-ttu-id="4c12f-165">Диспетчер кластерных ресурсов предоставляет много параметров для описания кластера.</span><span class="sxs-lookup"><span data-stu-id="4c12f-165">The Cluster Resource Manager has man options for describing the cluster.</span></span> <span data-ttu-id="4c12f-166">Дополнительные сведения об этих параметрах см. в статье с [описанием кластера Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md).</span><span class="sxs-lookup"><span data-stu-id="4c12f-166">To find out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>
- <span data-ttu-id="4c12f-167">Метрики показывают, как диспетчер кластерных ресурсов Service Fabric управляет потреблением и емкостью в кластере.</span><span class="sxs-lookup"><span data-stu-id="4c12f-167">Metrics are how the Service Fabric Cluster Resource Manger manages consumption and capacity in the cluster.</span></span> <span data-ttu-id="4c12f-168">Чтобы узнать больше о метриках и их настройке, ознакомьтесь с [этой статьей](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="4c12f-168">To learn more about metrics and how to configure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-defragmentation-metrics/balancing-defrag-compared.png
