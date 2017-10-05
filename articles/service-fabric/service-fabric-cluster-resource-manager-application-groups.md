---
title: "Диспетчер кластерных ресурсов Service Fabric: группы приложений | Документация Майкрософт"
description: "Общие сведения о назначении групп приложений в диспетчере кластерных ресурсов службы Fabric Service"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4cae2370-77b3-49ce-bf40-030400c4260d
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 7fc61731c8df2a0c3dc5b77ae718b41c240f9233
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="introduction-to-application-groups"></a><span data-ttu-id="3d569-103">Введение в группы приложений</span><span class="sxs-lookup"><span data-stu-id="3d569-103">Introduction to Application Groups</span></span>
<span data-ttu-id="3d569-104">Диспетчер кластерных ресурсов Service Fabric, который управляет ресурсами кластера, обычно равномерно распределяет нагрузку (представленную в [метриках](service-fabric-cluster-resource-manager-metrics.md)) по всему кластеру.</span><span class="sxs-lookup"><span data-stu-id="3d569-104">Service Fabric's Cluster Resource Manager typically manages cluster resources by spreading the load (represented via [Metrics](service-fabric-cluster-resource-manager-metrics.md)) evenly throughout the cluster.</span></span> <span data-ttu-id="3d569-105">Service Fabric управляет емкостью узлов в кластере и [емкостью](service-fabric-cluster-resource-manager-cluster-description.md) кластера в целом.</span><span class="sxs-lookup"><span data-stu-id="3d569-105">Service Fabric manages the capacity of the nodes in the cluster and the cluster as a whole via [capacity](service-fabric-cluster-resource-manager-cluster-description.md).</span></span> <span data-ttu-id="3d569-106">Метрики и емкость отлично работают для большинства рабочих нагрузок, но для структур, активно использующих разные экземпляры приложений Service Fabric, иногда возникают дополнительные требования.</span><span class="sxs-lookup"><span data-stu-id="3d569-106">Metrics and capacity work great for many workloads, but patterns that make heavy use of different Service Fabric Application Instances sometimes bring in additional requirements.</span></span> <span data-ttu-id="3d569-107">Например, может потребоваться следующее.</span><span class="sxs-lookup"><span data-stu-id="3d569-107">For example you may want to:</span></span>

- <span data-ttu-id="3d569-108">Резервирование определенной емкости на узлах в кластере для служб внутри какого-либо именованного экземпляра приложения.</span><span class="sxs-lookup"><span data-stu-id="3d569-108">Reserve some capacity on the nodes in the cluster for the services within some named application instance</span></span>
- <span data-ttu-id="3d569-109">Ограничение общего числа узлов, на которых работают службы в именованном экземпляре приложения (вместо распределения по всему кластеру).</span><span class="sxs-lookup"><span data-stu-id="3d569-109">Limit the total number of nodes that the services within a named application instance run on (instead of spreading them out over the entire cluster)</span></span>
- <span data-ttu-id="3d569-110">Определение емкости для именованного экземпляра приложения, чтобы ограничить число служб в нем или общее потребление ресурсов этими службами.</span><span class="sxs-lookup"><span data-stu-id="3d569-110">Define capacities on the named application instance itself to limit the number of services or total resource consumption of the services inside it</span></span>

<span data-ttu-id="3d569-111">Для соблюдения этих требований диспетчер кластерных ресурсов Service Fabric поддерживает группы приложений.</span><span class="sxs-lookup"><span data-stu-id="3d569-111">To meet these requirements, the Service Fabric Cluster Resource Manager supports a feature called Application Groups.</span></span>

## <a name="limiting-the-maximum-number-of-nodes"></a><span data-ttu-id="3d569-112">Ограничение максимального количества узлов</span><span class="sxs-lookup"><span data-stu-id="3d569-112">Limiting the maximum number of nodes</span></span>
<span data-ttu-id="3d569-113">В простейшем варианте использования емкость приложения позволяет ограничить количество узлов, на которых создаются экземпляры приложения.</span><span class="sxs-lookup"><span data-stu-id="3d569-113">The simplest use case for Application capacity is when an application instance needs to be limited to a certain maximum number of nodes.</span></span> <span data-ttu-id="3d569-114">Это позволяет объединить все службы, выполняющиеся в этом экземпляре приложения, на заданном количестве компьютеров.</span><span class="sxs-lookup"><span data-stu-id="3d569-114">This consolidates all services within that application instance onto a set number of machines.</span></span> <span data-ttu-id="3d569-115">Консолидация удобна в тех случаях, когда вы пытаетесь спрогнозировать или ограничить использование физических ресурсов службами в этом именованном экземпляре приложения.</span><span class="sxs-lookup"><span data-stu-id="3d569-115">Consolidation is useful when you're trying to predict or cap physical resource use by the services within that named application instance.</span></span> 

<span data-ttu-id="3d569-116">Следующий рисунок демонстрирует экземпляры приложения, для которых определено или не определено максимальное количество узлов.</span><span class="sxs-lookup"><span data-stu-id="3d569-116">The following image shows an application instance with and without a maximum number of nodes defined:</span></span>

<span data-ttu-id="3d569-117"><center>
![Определение максимального количества узлов для экземпляров приложения][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="3d569-117"><center>
![Application Instance Defining Maximum Number of Nodes][Image1]
</center></span></span>

<span data-ttu-id="3d569-118">В примере слева для приложения с тремя службами не определено максимальное число узлов.</span><span class="sxs-lookup"><span data-stu-id="3d569-118">In the left example, the application doesn’t have a maximum number of nodes defined, and it has three services.</span></span> <span data-ttu-id="3d569-119">Менеджер кластерных ресурсов распределил реплики по всем шести доступным узлам, чтобы сбалансировать нагрузку на кластер (поведение по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="3d569-119">The Cluster Resource Manager has spread out all replicas across six available nodes to achieve the best balance in the cluster (the default behavior).</span></span> <span data-ttu-id="3d569-120">В примере справа мы видим то же приложение, но с ограничением до трех узлов.</span><span class="sxs-lookup"><span data-stu-id="3d569-120">In the right example, we see the same application limited to three nodes.</span></span>

<span data-ttu-id="3d569-121">Такое поведение управляется параметром MaximumNodes.</span><span class="sxs-lookup"><span data-stu-id="3d569-121">The parameter that controls this behavior is called MaximumNodes.</span></span> <span data-ttu-id="3d569-122">Этот параметр можно задать при создании приложения или изменить для уже выполняющегося экземпляра приложения.</span><span class="sxs-lookup"><span data-stu-id="3d569-122">This parameter can be set during application creation, or updated for an application instance that was already running.</span></span>

<span data-ttu-id="3d569-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3d569-123">Powershell</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

<span data-ttu-id="3d569-124">C#</span><span class="sxs-lookup"><span data-stu-id="3d569-124">C#</span></span>

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MaximumNodes = 3;
await fc.ApplicationManager.CreateApplicationAsync(ad);

ApplicationUpdateDescription adUpdate = new ApplicationUpdateDescription(new Uri("fabric:/AppName"));
adUpdate.MaximumNodes = 5;
await fc.ApplicationManager.UpdateApplicationAsync(adUpdate);

```

<span data-ttu-id="3d569-125">В наборе узлов диспетчер кластерных ресурсов не гарантирует, какие объекты службы размещаются вместе и какие узлы используются.</span><span class="sxs-lookup"><span data-stu-id="3d569-125">Within the set of nodes, the Cluster Resource Manager doesn't guarantee which service objects get placed together or which nodes get used.</span></span>

## <a name="application-metrics-load-and-capacity"></a><span data-ttu-id="3d569-126">Метрики, нагрузка и емкость приложения</span><span class="sxs-lookup"><span data-stu-id="3d569-126">Application Metrics, Load, and Capacity</span></span>
<span data-ttu-id="3d569-127">Группы приложений позволяют также определять метрики для конкретного именованного экземпляра приложения и устанавливать емкость экземпляра приложения для этих метрик.</span><span class="sxs-lookup"><span data-stu-id="3d569-127">Application Groups also allow you to define metrics associated with a given named application instance, and that application instance's capacity for those metrics.</span></span> <span data-ttu-id="3d569-128">Метрики приложения позволяют отслеживать, резервировать и ограничивать потребление ресурсов службами внутри конкретного экземпляра приложения.</span><span class="sxs-lookup"><span data-stu-id="3d569-128">Application metrics allow you to track, reserve, and limit the resource consumption of the services inside that application instance.</span></span>

<span data-ttu-id="3d569-129">Для каждой метрики приложения можно установить два значения.</span><span class="sxs-lookup"><span data-stu-id="3d569-129">For each application metric, there are two values that can be set:</span></span>

- <span data-ttu-id="3d569-130">**Общая емкость приложения**. Это значение представляет общую емкость всего приложения по определенной метрике.</span><span class="sxs-lookup"><span data-stu-id="3d569-130">**Total Application Capacity** – This setting represents the total capacity of the application for a particular metric.</span></span> <span data-ttu-id="3d569-131">Диспетчер кластерных ресурсов запрещает создание новых служб для этого экземпляра приложения, если такое создание приведет к превышению указанного значения общей емкости.</span><span class="sxs-lookup"><span data-stu-id="3d569-131">The Cluster Resource Manager disallows the creation of any new services within this application instance that would cause total load to exceed this value.</span></span> <span data-ttu-id="3d569-132">Рассмотрим такой пример: для экземпляра приложения указано ограничение емкости 10, а текущая нагрузка составляет 5.</span><span class="sxs-lookup"><span data-stu-id="3d569-132">For example, let's say the application instance had a capacity of 10 and already had load of five.</span></span> <span data-ttu-id="3d569-133">Создание службы, для которой указана стандартная нагрузка 10, будет запрещено.</span><span class="sxs-lookup"><span data-stu-id="3d569-133">The creation of a service with a total default load of 10 would be disallowed.</span></span>
- <span data-ttu-id="3d569-134">**Максимальная емкость узла**. Это значение определяет максимальную общую нагрузку для приложения на отдельном узле.</span><span class="sxs-lookup"><span data-stu-id="3d569-134">**Maximum Node Capacity** – This setting specifies the maximum total load for the application on a single node.</span></span> <span data-ttu-id="3d569-135">Если нагрузка превышает емкость, диспетчер кластерных ресурсов перемещает реплики на другие узлы, тем самым уменьшая нагрузку.</span><span class="sxs-lookup"><span data-stu-id="3d569-135">If load goes over this capacity, the Cluster Resource Manager moves replicas to other nodes so that the load decreases.</span></span>


<span data-ttu-id="3d569-136">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3d569-136">Powershell:</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

<span data-ttu-id="3d569-137">C#:</span><span class="sxs-lookup"><span data-stu-id="3d569-137">C#:</span></span>

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.TotalApplicationCapacity = 1000;
appMetric.MaximumNodeCapacity = 100;
ad.Metrics.Add(appMetric);
await fc.ApplicationManager.CreateApplicationAsync(ad);
```

## <a name="reserving-capacity"></a><span data-ttu-id="3d569-138">Резервирование емкости</span><span class="sxs-lookup"><span data-stu-id="3d569-138">Reserving Capacity</span></span>
<span data-ttu-id="3d569-139">Еще одно распространенное использование групп приложений — резервирование ресурсов кластера для конкретного экземпляра приложения.</span><span class="sxs-lookup"><span data-stu-id="3d569-139">Another common use for application groups is to ensure that resources within the cluster are reserved for a given application instance.</span></span> <span data-ttu-id="3d569-140">При создании экземпляра приложения всегда резервируется пространство.</span><span class="sxs-lookup"><span data-stu-id="3d569-140">The space is always reserved when the application instance is created.</span></span>

<span data-ttu-id="3d569-141">Резервирование пространства в кластере для приложения происходит немедленно, даже когда:</span><span class="sxs-lookup"><span data-stu-id="3d569-141">Reserving space in the cluster for the application happens immediately even when:</span></span>
- <span data-ttu-id="3d569-142">экземпляр приложения создан, но еще не содержит ни одной службы;</span><span class="sxs-lookup"><span data-stu-id="3d569-142">the application instance is created but doesn't have any services within it yet</span></span>
- <span data-ttu-id="3d569-143">число служб в экземпляре приложения каждый раз изменяется;</span><span class="sxs-lookup"><span data-stu-id="3d569-143">the number of services within the application instance changes every time</span></span> 
- <span data-ttu-id="3d569-144">службы существуют, но не используют ресурсы.</span><span class="sxs-lookup"><span data-stu-id="3d569-144">the services exist but aren't consuming the resources</span></span> 

<span data-ttu-id="3d569-145">Чтобы зарезервировать ресурсы для экземпляра приложения, следует использовать два дополнительных параметра: *MinimumNodes* и *NodeReservationCapacity*.</span><span class="sxs-lookup"><span data-stu-id="3d569-145">Reserving resources for an application instance requires specifying two additional parameters: *MinimumNodes* and *NodeReservationCapacity*</span></span>

- <span data-ttu-id="3d569-146">**MinimumNodes**. Этот параметр определяет минимальное количество узлов, на которых должен работать экземпляр приложения.</span><span class="sxs-lookup"><span data-stu-id="3d569-146">**MinimumNodes** - Defines the minimum number of nodes that the application instance should run on.</span></span>  
- <span data-ttu-id="3d569-147">**NodeReservationCapacity**. Этот параметр задается на уровне метрики для приложения.</span><span class="sxs-lookup"><span data-stu-id="3d569-147">**NodeReservationCapacity** - This setting is per metric for the application.</span></span> <span data-ttu-id="3d569-148">Его значение — это объем данной метрики, резервируемый для приложения на любом узле, на котором выполняются службы в этом приложении.</span><span class="sxs-lookup"><span data-stu-id="3d569-148">The value is the amount of that metric reserved for the application on any node where that the services in that application run.</span></span>

<span data-ttu-id="3d569-149">Применяя **MinimumNodes** и **NodeReservationCapacity**, можно гарантировать резервирование минимальной нагрузки для приложения в кластере.</span><span class="sxs-lookup"><span data-stu-id="3d569-149">Combining **MinimumNodes** and **NodeReservationCapacity** guarantees a minimum load reservation for the application within the cluster.</span></span> <span data-ttu-id="3d569-150">Если оставшаяся емкость в кластере меньше, чем общая требуемая резервируемая емкость, то при создании приложения происходит сбой.</span><span class="sxs-lookup"><span data-stu-id="3d569-150">If there's less remaining capacity in the cluster than the total reservation required, creation of the application fails.</span></span> 

<span data-ttu-id="3d569-151">Рассмотрим пример резервирования емкости.</span><span class="sxs-lookup"><span data-stu-id="3d569-151">Let's look at an example of capacity reservation:</span></span>

<span data-ttu-id="3d569-152"><center>
![Определение резервируемой емкости для экземпляров приложения][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="3d569-152"><center>
![Application Instances Defining Reserved Capacity][Image2]
</center></span></span>

<span data-ttu-id="3d569-153">В примере слева для приложений не определены параметры емкости.</span><span class="sxs-lookup"><span data-stu-id="3d569-153">In the left example, applications do not have any Application Capacity defined.</span></span> <span data-ttu-id="3d569-154">Диспетчер кластерных ресурсов распределяет всю нагрузку по обычным правилам.</span><span class="sxs-lookup"><span data-stu-id="3d569-154">The Cluster Resource Manager balances everything according to normal rules.</span></span>

<span data-ttu-id="3d569-155">Допустим, в примере справа приложение Application1 было создано со следующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="3d569-155">In the example on the right, let's say that Application1 was created with the following settings:</span></span>

- <span data-ttu-id="3d569-156">MinimumNodes имеет значение 2;</span><span class="sxs-lookup"><span data-stu-id="3d569-156">MinimumNodes set to two</span></span>
- <span data-ttu-id="3d569-157">для приложения определена метрика со следующими значениями:</span><span class="sxs-lookup"><span data-stu-id="3d569-157">An application Metric defined with</span></span>
  - <span data-ttu-id="3d569-158">NodeReservationCapacity = 20;</span><span class="sxs-lookup"><span data-stu-id="3d569-158">NodeReservationCapacity of 20</span></span>

<span data-ttu-id="3d569-159">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3d569-159">Powershell</span></span>

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

<span data-ttu-id="3d569-160">C#</span><span class="sxs-lookup"><span data-stu-id="3d569-160">C#</span></span>

 ``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MinimumNodes = 2;

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.NodeReservationCapacity = 20;

ad.Metrics.Add(appMetric);

await fc.ApplicationManager.CreateApplicationAsync(ad);
```

<span data-ttu-id="3d569-161">Service Fabric резервирует емкость для Application1 на двух узлах и не разрешает службам из Application2 использовать эту емкость, даже если в это время службы в Application1 не потребляют ресурсы.</span><span class="sxs-lookup"><span data-stu-id="3d569-161">Service Fabric reserves capacity on two nodes for Application1, and doesn't allow services from Application2 to consume that capacity even if there are no load is being consumed by the services inside Application1 at the time.</span></span> <span data-ttu-id="3d569-162">Зарезервированная для приложения емкость считается потребляемой и будет учитываться при определении остатка доступной емкости на этом узле или в кластере.</span><span class="sxs-lookup"><span data-stu-id="3d569-162">This reserved application capacity is considered consumed  and counts against the remaining capacity on that node and within the cluster.</span></span>  <span data-ttu-id="3d569-163">Зарезервированная емкость мгновенно вычитается из оставшейся емкости кластера, однако из емкости определенного узла она вычитается только в том случае, если в нем размещается по крайней мере один объект службы.</span><span class="sxs-lookup"><span data-stu-id="3d569-163">The reservation is deducted from the remaining cluster capacity immediately, however the reserved consumption is deducted from the capacity of a specific node only when at least one service object is placed on it.</span></span> <span data-ttu-id="3d569-164">Этот второй этап резервирования позволяет более гибко и более эффективно использовать ресурсы, поскольку на конкретных узлах резервирование происходит только по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="3d569-164">This later reservation allows for flexibility and better resource utilization since resources are only reserved on nodes when needed.</span></span>

## <a name="obtaining-the-application-load-information"></a><span data-ttu-id="3d569-165">Получение сведений о нагрузке приложения</span><span class="sxs-lookup"><span data-stu-id="3d569-165">Obtaining the application load information</span></span>
<span data-ttu-id="3d569-166">Для каждого приложения с емкостью, определенной для одной или нескольких метрик, вы можете получить сведения о суммарной нагрузке, создаваемой репликами его служб.</span><span class="sxs-lookup"><span data-stu-id="3d569-166">For each application that has an Application Capacity defined for one or more metrics you can obtain the information about the aggregate load reported by replicas of its services.</span></span>

<span data-ttu-id="3d569-167">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="3d569-167">Powershell:</span></span>

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

<span data-ttu-id="3d569-168">C#</span><span class="sxs-lookup"><span data-stu-id="3d569-168">C#</span></span>

``` csharp
var v = await fc.QueryManager.GetApplicationLoadInformationAsync("fabric:/MyApplication1");
var metrics = v.ApplicationLoadMetricInformation;
foreach (ApplicationLoadMetricInformation metric in metrics)
{
    Console.WriteLine(metric.ApplicationCapacity);  //total capacity for this metric in this application instance
    Console.WriteLine(metric.ReservationCapacity);  //reserved capacity for this metric in this application instance
    Console.WriteLine(metric.ApplicationLoad);  //current load for this metric in this application instance
}
```

<span data-ttu-id="3d569-169">Запрос ApplicationLoad возвращает основные сведения о параметрах емкости, указанных для приложения.</span><span class="sxs-lookup"><span data-stu-id="3d569-169">The ApplicationLoad query returns the basic information about Application Capacity that was specified for the application.</span></span> <span data-ttu-id="3d569-170">Сюда входят данные о минимальном и максимальном числе узлов, а также о том, сколько узлов приложение занимает в настоящее время.</span><span class="sxs-lookup"><span data-stu-id="3d569-170">This information includes the Minimum Nodes and Maximum Nodes info, and the number that the application is currently occupying.</span></span> <span data-ttu-id="3d569-171">Также вы получите информацию по каждой метрике нагрузки для приложения, в том числе перечисленные ниже сведения.</span><span class="sxs-lookup"><span data-stu-id="3d569-171">It also includes information about each application load metric, including:</span></span>

* <span data-ttu-id="3d569-172">Metric Name: имя метрики.</span><span class="sxs-lookup"><span data-stu-id="3d569-172">Metric Name: Name of the metric.</span></span>
* <span data-ttu-id="3d569-173">Reservation Capacity: емкость, зарезервированная в кластере для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="3d569-173">Reservation Capacity: Cluster Capacity that is reserved in the cluster for this Application.</span></span>
* <span data-ttu-id="3d569-174">Application Load: общая нагрузка, создаваемая дочерними репликами этого приложения.</span><span class="sxs-lookup"><span data-stu-id="3d569-174">Application Load: Total Load of this Application’s child replicas.</span></span>
* <span data-ttu-id="3d569-175">Application Capacity: максимально допустимое значение нагрузки приложения.</span><span class="sxs-lookup"><span data-stu-id="3d569-175">Application Capacity: Maximum permitted value of Application Load.</span></span>

## <a name="removing-application-capacity"></a><span data-ttu-id="3d569-176">Удаление емкости приложения</span><span class="sxs-lookup"><span data-stu-id="3d569-176">Removing Application Capacity</span></span>
<span data-ttu-id="3d569-177">Когда для приложения будут установлены параметры емкости приложения, их можно будет удалить с помощью API-интерфейсов обновления приложения или командлетов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3d569-177">Once the Application Capacity parameters are set for an application, they can be removed using Update Application APIs or PowerShell cmdlets.</span></span> <span data-ttu-id="3d569-178">Например:</span><span class="sxs-lookup"><span data-stu-id="3d569-178">For example:</span></span>

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

<span data-ttu-id="3d569-179">Эта команда удаляет все параметры управления емкостью приложения, установленные для экземпляра приложения.</span><span class="sxs-lookup"><span data-stu-id="3d569-179">This command removes all Application capacity management parameters from the application instance.</span></span> <span data-ttu-id="3d569-180">Это относится к параметрам MinimumNodes, MaximumNodes и метрикам приложения, если они были настроены.</span><span class="sxs-lookup"><span data-stu-id="3d569-180">This includes MinimumNodes, MaximumNodes, and the Application's metrics, if any.</span></span> <span data-ttu-id="3d569-181">Команда применяется немедленно.</span><span class="sxs-lookup"><span data-stu-id="3d569-181">The effect of the command is immediate.</span></span> <span data-ttu-id="3d569-182">После выполнения этой команды диспетчер кластерных ресурсов использует режим по умолчанию для управления приложениями.</span><span class="sxs-lookup"><span data-stu-id="3d569-182">After this command completes, the Cluster Resource Manager uses the default behavior for managing applications.</span></span> <span data-ttu-id="3d569-183">Параметры емкости приложения можно задать снова, используя команду `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span><span class="sxs-lookup"><span data-stu-id="3d569-183">Application Capacity parameters can be specified again via `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span></span>

### <a name="restrictions-on-application-capacity"></a><span data-ttu-id="3d569-184">Ограничения на емкость приложений</span><span class="sxs-lookup"><span data-stu-id="3d569-184">Restrictions on Application Capacity</span></span>
<span data-ttu-id="3d569-185">Существует ряд ограничений на параметры емкости приложений, которые необходимо соблюдать.</span><span class="sxs-lookup"><span data-stu-id="3d569-185">There are several restrictions on Application Capacity parameters that must be respected.</span></span> <span data-ttu-id="3d569-186">При обнаружении ошибок во время проверки изменения не применяются.</span><span class="sxs-lookup"><span data-stu-id="3d569-186">If there are validation errors no changes take place.</span></span>

- <span data-ttu-id="3d569-187">Все числовые параметры должны иметь неотрицательные значения.</span><span class="sxs-lookup"><span data-stu-id="3d569-187">All integer parameters must be non-negative numbers.</span></span>
- <span data-ttu-id="3d569-188">MinimumNodes не может иметь значение больше, чем MaximumNodes.</span><span class="sxs-lookup"><span data-stu-id="3d569-188">MinimumNodes must never be greater than MaximumNodes.</span></span>
- <span data-ttu-id="3d569-189">Если определены емкости для метрики нагрузки, они должны соответствовать следующим правилам.</span><span class="sxs-lookup"><span data-stu-id="3d569-189">If capacities for a load metric are defined, then they must follow these rules:</span></span>
  - <span data-ttu-id="3d569-190">NodeReservationCapacity не может иметь значение больше, чем MaximumNodeCapacity.</span><span class="sxs-lookup"><span data-stu-id="3d569-190">Node Reservation Capacity must not be greater than Maximum Node Capacity.</span></span> <span data-ttu-id="3d569-191">Например, вы не можете для метрики нагрузки на процессор на узле установить ограничение в две единицы и одновременно зарезервировать по три единицы этого ресурса на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="3d569-191">For example, you cannot limit the capacity for the metric “CPU” on the node to two units and try to reserve three units on each node.</span></span>
  - <span data-ttu-id="3d569-192">Если указан параметр MaximumNodes, произведение значений MaximumNodes и MaximumNodeCapacity не может быть больше, чем значение TotalApplicationCapacity.</span><span class="sxs-lookup"><span data-stu-id="3d569-192">If MaximumNodes is specified, then the product of MaximumNodes and Maximum Node Capacity must not be greater than Total Application Capacity.</span></span> <span data-ttu-id="3d569-193">Предположим, вы установили значение 8 для максимальной емкости узла для метрики нагрузки на процессор.</span><span class="sxs-lookup"><span data-stu-id="3d569-193">For example, let's say the Maximum Node Capacity for load metric “CPU” is set to eight.</span></span> <span data-ttu-id="3d569-194">При этом максимальное число узлов вы ограничили десятью.</span><span class="sxs-lookup"><span data-stu-id="3d569-194">Let's also say you set the Maximum Nodes to 10.</span></span> <span data-ttu-id="3d569-195">В этом случае общая емкость приложения для этой метрики нагрузки должна быть больше 80.</span><span class="sxs-lookup"><span data-stu-id="3d569-195">In this case, Total Application Capacity must be greater than 80 for this load metric.</span></span>

<span data-ttu-id="3d569-196">Ограничения применяются во время создания и обновления приложений.</span><span class="sxs-lookup"><span data-stu-id="3d569-196">The restrictions are enforced both during application creation and updates.</span></span>

## <a name="how-not-to-use-application-capacity"></a><span data-ttu-id="3d569-197">Как не следует использовать емкость приложения</span><span class="sxs-lookup"><span data-stu-id="3d569-197">How not to use Application Capacity</span></span>
- <span data-ttu-id="3d569-198">Не пытайтесь с помощью групп приложений сделать так, чтобы приложение выполнялось на _определенном_ подмножестве узлов.</span><span class="sxs-lookup"><span data-stu-id="3d569-198">Do not try to use the Application Group features to constrain the application to a _specific_ subset of nodes.</span></span> <span data-ttu-id="3d569-199">Другими словами, вы можете указать, что для приложения нельзя использовать больше пяти узлов, но не можете выбрать, какие именно это будут узлы в кластере.</span><span class="sxs-lookup"><span data-stu-id="3d569-199">In other words, you can specify that the application runs on at most five nodes, but not which specific five nodes in the cluster.</span></span> <span data-ttu-id="3d569-200">Чтобы прикрепить приложение к конкретным узлам, используйте ограничения на размещение для служб.</span><span class="sxs-lookup"><span data-stu-id="3d569-200">Constraining an application to specific nodes can be achieved using placement constraints for services.</span></span>
- <span data-ttu-id="3d569-201">Не пытайтесь с помощью емкости приложения разместить две службы одного приложения на одном узле.</span><span class="sxs-lookup"><span data-stu-id="3d569-201">Do not try to use the Application Capacity to ensure that two services from the same application are placed on the same nodes.</span></span> <span data-ttu-id="3d569-202">Вместо этого используйте [сходство](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) или [ограничения размещения](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span><span class="sxs-lookup"><span data-stu-id="3d569-202">Instead use [affinity](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) or [placement constraints](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d569-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3d569-203">Next steps</span></span>
- <span data-ttu-id="3d569-204">Дополнительные сведения о настройке служб см. в разделе [Настройка параметров Cluster Resource Manager для служб Service Fabric](service-fabric-cluster-resource-manager-configure-services.md).</span><span class="sxs-lookup"><span data-stu-id="3d569-204">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>
- <span data-ttu-id="3d569-205">Чтобы узнать, как диспетчер кластерных ресурсов управляет нагрузкой кластера и балансирует ее, ознакомьтесь со статьей о [балансировке нагрузки](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="3d569-205">To find out about how the Cluster Resource Manager manages and balances load in the cluster, check out the article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
- <span data-ttu-id="3d569-206">Начните с самого начала, [изучив общие сведения о диспетчере кластерных ресурсов Service Fabric](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="3d569-206">Start from the beginning and [get an Introduction to the Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
- <span data-ttu-id="3d569-207">Дополнительные сведения об использовании метрик см. в статье [Управление потреблением ресурсов и нагрузкой в Service Fabric с помощью метрик](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="3d569-207">For more information on how metrics work generally, read up on [Service Fabric Load Metrics](service-fabric-cluster-resource-manager-metrics.md)</span></span>
- <span data-ttu-id="3d569-208">Диспетчер кластерных ресурсов предоставляет много параметров для описания кластера.</span><span class="sxs-lookup"><span data-stu-id="3d569-208">The Cluster Resource Manager has many options for describing the cluster.</span></span> <span data-ttu-id="3d569-209">Дополнительные сведения об этих параметрах см. в статье с [описанием кластера Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md).</span><span class="sxs-lookup"><span data-stu-id="3d569-209">To find out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
