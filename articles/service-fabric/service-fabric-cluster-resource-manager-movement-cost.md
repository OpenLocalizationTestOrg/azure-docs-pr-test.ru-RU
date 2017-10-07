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
ms.openlocfilehash: 65d4ac73efffcf7b25b1e95da6f9012a9238cb75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-movement-cost"></a><span data-ttu-id="fc7d5-103">Затраты на перемещение служб</span><span class="sxs-lookup"><span data-stu-id="fc7d5-103">Service movement cost</span></span>
<span data-ttu-id="fc7d5-104">Коэффициент, на который hello диспетчер ресурсов кластера Service Fabric считает, что при попытке toodetermine, какие изменения toomake tooa кластер находится стоимость hello этих изменений.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-104">A factor that hello Service Fabric Cluster Resource Manager considers when trying toodetermine what changes toomake tooa cluster is hello cost of those changes.</span></span> <span data-ttu-id="fc7d5-105">Hello понятие «стоимость», проданные отключение от можно повысить, сколько кластеров hello.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-105">hello notion of "cost" is traded off against how much hello cluster can be improved.</span></span> <span data-ttu-id="fc7d5-106">Затраты учитываются при перемещении служб для балансировки, дефрагментации и выполнения других требований.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-106">Cost is factored in when moving services for balancing, defragmentation, and other requirements.</span></span> <span data-ttu-id="fc7d5-107">Задача Hello — toomeet требований hello в hello наименьших нарушают работу или ресурсоемкие способом.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-107">hello goal is toomeet hello requirements in hello least disruptive or expensive way.</span></span> 

<span data-ttu-id="fc7d5-108">Как минимум перемещение служб требует затрат процессорного времени и пропускной способности сети.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-108">Moving services costs CPU time and network bandwidth at a minimum.</span></span> <span data-ttu-id="fc7d5-109">Для служб с отслеживанием состояния требуется копирование hello состояние эти службы, использование дополнительной памяти и диска.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-109">For stateful services, it requires copying hello state of those services, consuming additional memory and disk.</span></span> <span data-ttu-id="fc7d5-110">Снижают стоимость hello решений приветствия, рассматриваемых в диспетчер ресурсов Azure Service Fabric кластера гарантирует ресурсы кластера hello не затраченное без необходимости.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-110">Minimizing hello cost of solutions that hello Azure Service Fabric Cluster Resource Manager comes up with helps ensure that hello cluster's resources aren't spent unnecessarily.</span></span> <span data-ttu-id="fc7d5-111">Тем не менее также не следует tooignore решений, которые позволяет значительно улучшить hello выделения ресурсов в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-111">However, you also don’t want tooignore solutions that would significantly improve hello allocation of resources in hello cluster.</span></span>

<span data-ttu-id="fc7d5-112">Диспетчер ресурсов кластера Hello предоставляет два способа вычисления затрат и ограничить их допуск при попытке toomanage hello кластера.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-112">hello Cluster Resource Manager has two ways of computing costs and limiting them while it tries toomanage hello cluster.</span></span> <span data-ttu-id="fc7d5-113">Первый механизм Hello просто подсчет каждом переходе, он делает.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-113">hello first mechanism is simply counting every move that it would make.</span></span> <span data-ttu-id="fc7d5-114">Если два решения, создаваемые с помощью о hello же балансировку (оценка), то диспетчер ресурсов кластера hello предпочтительный hello один hello дешевый (общее число ходов).</span><span class="sxs-lookup"><span data-stu-id="fc7d5-114">If two solutions are generated with about hello same balance (score), then hello Cluster Resource Manager prefers hello one with hello lowest cost (total number of moves).</span></span>

<span data-ttu-id="fc7d5-115">Эта стратегия хорошо работает.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-115">This strategy works well.</span></span> <span data-ttu-id="fc7d5-116">Но, как и в случае нагрузок по умолчанию или статических нагрузок, маловероятно, что в любой сложной системе все будут перемещения равнозначны.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-116">But as with default or static loads, it's unlikely in any complex system that all moves are equal.</span></span> <span data-ttu-id="fc7d5-117">Некоторые, скорее всего, toobe гораздо более затратным.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-117">Some are likely toobe much more expensive.</span></span>

## <a name="setting-move-costs"></a><span data-ttu-id="fc7d5-118">Настройка затрат на перемещение</span><span class="sxs-lookup"><span data-stu-id="fc7d5-118">Setting Move Costs</span></span> 
<span data-ttu-id="fc7d5-119">Hello стоимость перемещения по умолчанию для службы можно указать при ее создании.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-119">You can specify hello default move cost for a service when it is created:</span></span>

<span data-ttu-id="fc7d5-120">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fc7d5-120">PowerShell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

<span data-ttu-id="fc7d5-121">C#:</span><span class="sxs-lookup"><span data-stu-id="fc7d5-121">C#:</span></span> 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up hello rest of hello ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="fc7d5-122">Также можно указать или MoveCost динамическое обновление для службы после создания службы hello:</span><span class="sxs-lookup"><span data-stu-id="fc7d5-122">You can also specify or update MoveCost dynamically for a service after hello service has been created:</span></span> 

<span data-ttu-id="fc7d5-123">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fc7d5-123">PowerShell:</span></span> 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

<span data-ttu-id="fc7d5-124">C#:</span><span class="sxs-lookup"><span data-stu-id="fc7d5-124">C#:</span></span>

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a><span data-ttu-id="fc7d5-125">Динамическое указание затрат на перемещение на уровне реплики</span><span class="sxs-lookup"><span data-stu-id="fc7d5-125">Dynamically specifying move cost on a per-replica basis</span></span>

<span data-ttu-id="fc7d5-126">Hello выше фрагменты кода, для указания MoveCost для всей службы за один раз из самой службы вне hello.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-126">hello preceding snippets are all for specifying MoveCost for a whole service at once from outside hello service itself.</span></span> <span data-ttu-id="fc7d5-127">Тем не менее, переместить затраты являются наиболее полезен при стоимость перемещения hello объекта конкретной службы меняются с течением времени его существования.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-127">However, move cost is most useful is when hello move cost of a specific service object changes over its lifespan.</span></span> <span data-ttu-id="fc7d5-128">Так как сами службы, возможно, hello hello наиболее знать о том, насколько дорогостоящим их toomove определенный момент времени, существует API-Интерфейс для службы tooreport стоимость отдельных Переход во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-128">Since hello services themselves probably have hello best idea of how costly they are toomove a given time, there's an API for services tooreport their own individual move cost during runtime.</span></span> 

<span data-ttu-id="fc7d5-129">C#:</span><span class="sxs-lookup"><span data-stu-id="fc7d5-129">C#:</span></span>

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a><span data-ttu-id="fc7d5-130">Влияние затрат на перемещение</span><span class="sxs-lookup"><span data-stu-id="fc7d5-130">Impact of move cost</span></span>
<span data-ttu-id="fc7d5-131">MoveCost имеет четыре уровня: Zero, Low, Medium и High.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-131">MoveCost has four levels: Zero, Low, Medium, and High.</span></span> <span data-ttu-id="fc7d5-132">MoveCosts — относительный tooeach другими, кроме нуля.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-132">MoveCosts are relative tooeach other, except for Zero.</span></span> <span data-ttu-id="fc7d5-133">Ноль стоимость перемещения означает, что перемещение предоставляется бесплатно и следует не подпадают оценка hello hello решения.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-133">Zero move cost means that movement is free and should not count against hello score of hello solution.</span></span> <span data-ttu-id="fc7d5-134">Параметр tooHigh стоимости и переместить *не* гарантирует, hello реплика остается в одном месте.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-134">Setting your move cost tooHigh does *not* guarantee that hello replica stays in one place.</span></span>

<span data-ttu-id="fc7d5-135"><center>
![Влияние стоимости перемещения на выбор реплик для перемещения][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="fc7d5-135"><center>
![Move cost as a factor in selecting replicas for movement][Image1]
</center></span></span>

<span data-ttu-id="fc7d5-136">MoveCost помогает найти hello решения, что причина hello наименьших перебоев в целом и простым tooachieve при по-прежнему поступающих в эквивалентные баланс.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-136">MoveCost helps you find hello solutions that cause hello least disruption overall and are easiest tooachieve while still arriving at equivalent balance.</span></span> <span data-ttu-id="fc7d5-137">Понятие службы затраты могут быть относительные toomany сущности.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-137">A service’s notion of cost can be relative toomany things.</span></span> <span data-ttu-id="fc7d5-138">Hello наиболее распространенные факторы при расчете затрат перемещения являются:</span><span class="sxs-lookup"><span data-stu-id="fc7d5-138">hello most common factors in calculating your move cost are:</span></span>

- <span data-ttu-id="fc7d5-139">Hello объем состояния или данные, что служба hello имеет toomove.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-139">hello amount of state or data that hello service has toomove.</span></span>
- <span data-ttu-id="fc7d5-140">стоимость Hello отключения клиентов.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-140">hello cost of disconnection of clients.</span></span> <span data-ttu-id="fc7d5-141">Перемещение первичной реплики, обычно дороже, чем hello стоимость перемещения вторичной реплики.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-141">Moving a primary replica is usually more costly than hello cost of moving a secondary replica.</span></span>
- <span data-ttu-id="fc7d5-142">Hello затраты на лету операции прерывания.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-142">hello cost of interrupting an in-flight operation.</span></span> <span data-ttu-id="fc7d5-143">Некоторые операции hello данных хранения уровня или операции, выполняемые в ответ tooa клиентский вызов являются ресурсоемкими.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-143">Some operations at hello data store level or operations performed in response tooa client call are costly.</span></span> <span data-ttu-id="fc7d5-144">В определенный момент вы не хотите toostop их, если не нужно.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-144">After a certain point, you don’t want toostop them if you don’t have to.</span></span> <span data-ttu-id="fc7d5-145">Поэтому во время операции hello происходит, увеличить стоимость перемещения hello этой службы объекта tooreduce hello вероятность того, что он перемещается.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-145">So while hello operation is going on, you increase hello move cost of this service object tooreduce hello likelihood that it moves.</span></span> <span data-ttu-id="fc7d5-146">По завершении операции hello задаются задней toonormal hello затрат.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-146">When hello operation is done, you set hello cost back toonormal.</span></span>

## <a name="enabling-move-cost-in-your-cluster"></a><span data-ttu-id="fc7d5-147">Включение учета затрат на перемещение в кластере</span><span class="sxs-lookup"><span data-stu-id="fc7d5-147">Enabling move cost in your cluster</span></span>
<span data-ttu-id="fc7d5-148">Чтобы Здравствуйте более детального toobe MoveCosts принимать в расчет, MoveCost необходимо включить в кластер.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-148">In order for hello more granular MoveCosts toobe taken into account, MoveCost must be enabled in your cluster.</span></span> <span data-ttu-id="fc7d5-149">Без этого параметра режима по умолчанию hello подсчета перемещает используется для расчета MoveCost и MoveCost отчеты игнорируются.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-149">Without this setting, hello default mode of counting moves is used for calculating MoveCost, and MoveCost reports are ignored.</span></span>


<span data-ttu-id="fc7d5-150">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="fc7d5-150">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

<span data-ttu-id="fc7d5-151">Для автономных развертываний используется ClusterConfig.json, а для размещенных в Azure кластеров — Template.json.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-151">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="fc7d5-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fc7d5-152">Next steps</span></span>
- <span data-ttu-id="fc7d5-153">Диспетчера ресурсов кластера Service Fabric использует потребления toomanage метрик и емкости в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="fc7d5-153">Service Fabric Cluster Resource Manger uses metrics toomanage consumption and capacity in hello cluster.</span></span> <span data-ttu-id="fc7d5-154">Дополнительные сведения о метриках toolearn как tooconfigure, извлечение и возврат [Управление потреблением ресурсов и загрузки в Service Fabric с метриками](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="fc7d5-154">toolearn more about metrics and how tooconfigure them, check out [Managing resource consumption and load in Service Fabric with metrics](service-fabric-cluster-resource-manager-metrics.md).</span></span>
- <span data-ttu-id="fc7d5-155">toolearn о hello диспетчер ресурсов кластера управляет и балансировку нагрузки в кластере hello, извлечь [балансировки кластера Service Fabric](service-fabric-cluster-resource-manager-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="fc7d5-155">toolearn about how hello Cluster Resource Manager manages and balances load in hello cluster, check out [Balancing your Service Fabric cluster](service-fabric-cluster-resource-manager-balancing.md).</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
