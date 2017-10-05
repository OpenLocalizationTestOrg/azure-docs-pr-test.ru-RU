---
title: "Диспетчер кластерных ресурсов Service Fabric: стоимость перемещения | Документация Майкрософт"
description: "Общие сведения о стоимости перемещения служб Service Fabric."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f022f258-7bc0-4db4-aa85-8c6c8344da32
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 5de07c259d1d327d0211338c2911804445dd6b60
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="service-movement-cost"></a><span data-ttu-id="d2ddb-103">Затраты на перемещение служб</span><span class="sxs-lookup"><span data-stu-id="d2ddb-103">Service movement cost</span></span>
<span data-ttu-id="d2ddb-104">Фактором, который диспетчер кластерных ресурсов Service Fabric принимает во внимание при попытке определить, какие изменения вносить в кластер, являются общие затраты на эти изменения.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-104">A factor that the Service Fabric Cluster Resource Manager considers when trying to determine what changes to make to a cluster is the cost of those changes.</span></span> <span data-ttu-id="d2ddb-105">Понятие "затраты" соотносится со степенью улучшения кластера.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-105">The notion of "cost" is traded off against how much the cluster can be improved.</span></span> <span data-ttu-id="d2ddb-106">Затраты учитываются при перемещении служб для балансировки, дефрагментации и выполнения других требований.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-106">Cost is factored in when moving services for balancing, defragmentation, and other requirements.</span></span> <span data-ttu-id="d2ddb-107">Цель — выполнить требования с наименьшим вмешательством или затратами.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-107">The goal is to meet the requirements in the least disruptive or expensive way.</span></span> 

<span data-ttu-id="d2ddb-108">Как минимум перемещение служб требует затрат процессорного времени и пропускной способности сети.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-108">Moving services costs CPU time and network bandwidth at a minimum.</span></span> <span data-ttu-id="d2ddb-109">Для служб с отслеживанием состояния требуется копировать их состояние, что приводит к использованию дополнительных ресурсов памяти и дисков.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-109">For stateful services, it requires copying the state of those services, consuming additional memory and disk.</span></span> <span data-ttu-id="d2ddb-110">Сведение к минимуму затрат на решения, получаемые диспетчером кластерных ресурсов Azure Service Fabric, гарантирует, что ресурсы кластера не будут использоваться без необходимости.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-110">Minimizing the cost of solutions that the Azure Service Fabric Cluster Resource Manager comes up with helps ensure that the cluster's resources aren't spent unnecessarily.</span></span> <span data-ttu-id="d2ddb-111">Однако при этом не хотелось бы игнорировать решения, которые могли бы значительно улучшить выделение ресурсов кластера.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-111">However, you also don’t want to ignore solutions that would significantly improve the allocation of resources in the cluster.</span></span>

<span data-ttu-id="d2ddb-112">В диспетчере кластерных ресурсов есть два способа вычисления затрат и их ограничения, применяемые в управлении кластером.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-112">The Cluster Resource Manager has two ways of computing costs and limiting them while it tries to manage the cluster.</span></span> <span data-ttu-id="d2ddb-113">Первый механизм — это просто подсчет каждого производимого перемещения.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-113">The first mechanism is simply counting every move that it would make.</span></span> <span data-ttu-id="d2ddb-114">Если созданы два решения примерно с одинаковым распределением нагрузки (оценкой), то диспетчер кластерных ресурсов выберет решение с меньшими затратами (общим числом перемещений).</span><span class="sxs-lookup"><span data-stu-id="d2ddb-114">If two solutions are generated with about the same balance (score), then the Cluster Resource Manager prefers the one with the lowest cost (total number of moves).</span></span>

<span data-ttu-id="d2ddb-115">Эта стратегия хорошо работает.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-115">This strategy works well.</span></span> <span data-ttu-id="d2ddb-116">Но, как и в случае нагрузок по умолчанию или статических нагрузок, маловероятно, что в любой сложной системе все будут перемещения равнозначны.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-116">But as with default or static loads, it's unlikely in any complex system that all moves are equal.</span></span> <span data-ttu-id="d2ddb-117">Некоторые могут быть намного более затратными.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-117">Some are likely to be much more expensive.</span></span>

## <a name="setting-move-costs"></a><span data-ttu-id="d2ddb-118">Настройка затрат на перемещение</span><span class="sxs-lookup"><span data-stu-id="d2ddb-118">Setting Move Costs</span></span> 
<span data-ttu-id="d2ddb-119">Можно задать затраты на перемещение по умолчанию для службы при ее создании.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-119">You can specify the default move cost for a service when it is created:</span></span>

<span data-ttu-id="d2ddb-120">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d2ddb-120">PowerShell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

<span data-ttu-id="d2ddb-121">C#:</span><span class="sxs-lookup"><span data-stu-id="d2ddb-121">C#:</span></span> 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up the rest of the ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="d2ddb-122">Можно также динамически указать или обновить затраты на перемещение для службы после ее создания.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-122">You can also specify or update MoveCost dynamically for a service after the service has been created:</span></span> 

<span data-ttu-id="d2ddb-123">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="d2ddb-123">PowerShell:</span></span> 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

<span data-ttu-id="d2ddb-124">C#:</span><span class="sxs-lookup"><span data-stu-id="d2ddb-124">C#:</span></span>

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a><span data-ttu-id="d2ddb-125">Динамическое указание затрат на перемещение на уровне реплики</span><span class="sxs-lookup"><span data-stu-id="d2ddb-125">Dynamically specifying move cost on a per-replica basis</span></span>

<span data-ttu-id="d2ddb-126">Все фрагменты кода, приведенные выше, указывают значение затрат на перемещение сразу для всей службы, причем извне этой службы.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-126">The preceding snippets are all for specifying MoveCost for a whole service at once from outside the service itself.</span></span> <span data-ttu-id="d2ddb-127">Тем не менее, затраты на перемещение удобнее всего использовать, когда их значение для определенного объекта службы изменяется на протяжении времени его существования.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-127">However, move cost is most useful is when the move cost of a specific service object changes over its lifespan.</span></span> <span data-ttu-id="d2ddb-128">Так как сами службы, вероятно, лучше всего определяют затраты на свое перемещение на определенный момент времени, предусмотрен API, с помощью которого службы могут сообщать значение собственных отдельных затрат на перемещение во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-128">Since the services themselves probably have the best idea of how costly they are to move a given time, there's an API for services to report their own individual move cost during runtime.</span></span> 

<span data-ttu-id="d2ddb-129">C#:</span><span class="sxs-lookup"><span data-stu-id="d2ddb-129">C#:</span></span>

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a><span data-ttu-id="d2ddb-130">Влияние затрат на перемещение</span><span class="sxs-lookup"><span data-stu-id="d2ddb-130">Impact of move cost</span></span>
<span data-ttu-id="d2ddb-131">MoveCost имеет четыре уровня: Zero, Low, Medium и High.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-131">MoveCost has four levels: Zero, Low, Medium, and High.</span></span> <span data-ttu-id="d2ddb-132">MoveCosts определены относительно друг друга, кроме уровня Zero.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-132">MoveCosts are relative to each other, except for Zero.</span></span> <span data-ttu-id="d2ddb-133">Стоимость перемещения Zero означает, что перемещение является бесплатным и не должно учитываться при оценке решения.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-133">Zero move cost means that movement is free and should not count against the score of the solution.</span></span> <span data-ttu-id="d2ddb-134">Если настроить стоимость перемещения High, это *не* гарантирует, что реплика не будет перемещена.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-134">Setting your move cost to High does *not* guarantee that the replica stays in one place.</span></span>

<span data-ttu-id="d2ddb-135"><center>
![Влияние стоимости перемещения на выбор реплик для перемещения][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="d2ddb-135"><center>
![Move cost as a factor in selecting replicas for movement][Image1]
</center></span></span>

<span data-ttu-id="d2ddb-136">Параметр MoveCost помогает найти решения, которые в целом приводят к меньшему прерыванию работы и позволяют легче достичь равноценного баланса.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-136">MoveCost helps you find the solutions that cause the least disruption overall and are easiest to achieve while still arriving at equivalent balance.</span></span> <span data-ttu-id="d2ddb-137">Понятие стоимости службы может зависеть от многих факторов.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-137">A service’s notion of cost can be relative to many things.</span></span> <span data-ttu-id="d2ddb-138">Ниже перечислены наиболее распространенные факторы, учитываемые при вычислении стоимости перемещения.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-138">The most common factors in calculating your move cost are:</span></span>

- <span data-ttu-id="d2ddb-139">Объем данных состояния или информации, перемещаемой для службы.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-139">The amount of state or data that the service has to move.</span></span>
- <span data-ttu-id="d2ddb-140">Стоимость отключения клиентов.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-140">The cost of disconnection of clients.</span></span> <span data-ttu-id="d2ddb-141">Как правило, затраты на перемещение первичной реплики выше, чем затраты на перемещение вторичной реплики.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-141">Moving a primary replica is usually more costly than the cost of moving a secondary replica.</span></span>
- <span data-ttu-id="d2ddb-142">Стоимость прерывания текущих операций.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-142">The cost of interrupting an in-flight operation.</span></span> <span data-ttu-id="d2ddb-143">Некоторые операции уровня хранилища данных или операции, выполняемые по вызову клиента, являются дорогостоящими.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-143">Some operations at the data store level or operations performed in response to a client call are costly.</span></span> <span data-ttu-id="d2ddb-144">После определенного момента вы не станете останавливать их, если только это не вынужденная мера.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-144">After a certain point, you don’t want to stop them if you don’t have to.</span></span> <span data-ttu-id="d2ddb-145">Поэтому пока происходит операция, увеличьте стоимость перемещения этого объекта службы, чтобы снизить вероятность его перемещения.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-145">So while the operation is going on, you increase the move cost of this service object to reduce the likelihood that it moves.</span></span> <span data-ttu-id="d2ddb-146">А после завершения операции восстановите обычное значение стоимости перемещения.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-146">When the operation is done, you set the cost back to normal.</span></span>

## <a name="enabling-move-cost-in-your-cluster"></a><span data-ttu-id="d2ddb-147">Включение учета затрат на перемещение в кластере</span><span class="sxs-lookup"><span data-stu-id="d2ddb-147">Enabling move cost in your cluster</span></span>
<span data-ttu-id="d2ddb-148">Чтобы обеспечить учет более детализированных затрат на перемещение, в кластере нужно включить использование затрат на перемещение.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-148">In order for the more granular MoveCosts to be taken into account, MoveCost must be enabled in your cluster.</span></span> <span data-ttu-id="d2ddb-149">Если это не настроить, то для расчета затрат на перемещение используется стандартный режим подсчета перемещений и отчеты о затратах на перемещение игнорируются.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-149">Without this setting, the default mode of counting moves is used for calculating MoveCost, and MoveCost reports are ignored.</span></span>


<span data-ttu-id="d2ddb-150">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="d2ddb-150">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

<span data-ttu-id="d2ddb-151">Для автономных развертываний используется ClusterConfig.json, а для размещенных в Azure кластеров — Template.json.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-151">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "UseMoveCostReports",
          "value": "true"
      }
    ]
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="d2ddb-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d2ddb-152">Next steps</span></span>
- <span data-ttu-id="d2ddb-153">С помощью метрик диспетчер кластерных ресурсов Service Fabric управляет потреблением и емкостью в кластере.</span><span class="sxs-lookup"><span data-stu-id="d2ddb-153">Service Fabric Cluster Resource Manger uses metrics to manage consumption and capacity in the cluster.</span></span> <span data-ttu-id="d2ddb-154">Чтобы узнать больше о метрик и их настройке, ознакомьтесь с разделом [Управление потреблением ресурсов и нагрузкой в Service Fabric с помощью метрик](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="d2ddb-154">To learn more about metrics and how to configure them, check out [Managing resource consumption and load in Service Fabric with metrics](service-fabric-cluster-resource-manager-metrics.md).</span></span>
- <span data-ttu-id="d2ddb-155">Чтобы узнать, как диспетчер кластерных ресурсов управляет нагрузкой кластера и балансирует ее, ознакомьтесь со статьей [Балансировка кластера Service Fabric](service-fabric-cluster-resource-manager-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="d2ddb-155">To learn about how the Cluster Resource Manager manages and balances load in the cluster, check out [Balancing your Service Fabric cluster](service-fabric-cluster-resource-manager-balancing.md).</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
