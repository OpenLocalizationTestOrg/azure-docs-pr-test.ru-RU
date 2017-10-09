---
title: "aaaService диспетчер ресурсов кластера структуры - групп приложений | Документы Microsoft"
description: "Общие сведения о функции группы приложений в диспетчер ресурсов кластера Service Fabric hello hello"
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
ms.openlocfilehash: b4f068862d962b53a0b3ea813b89bb13ee395681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapplication-groups"></a><span data-ttu-id="60588-103">Введение tooApplication групп</span><span class="sxs-lookup"><span data-stu-id="60588-103">Introduction tooApplication Groups</span></span>
<span data-ttu-id="60588-104">Диспетчер ресурсов кластера Service Fabric обычно управляет ресурсы кластера, распределяя нагрузки hello (представить так [метрики](service-fabric-cluster-resource-manager-metrics.md)) равномерно по всему hello кластера.</span><span class="sxs-lookup"><span data-stu-id="60588-104">Service Fabric's Cluster Resource Manager typically manages cluster resources by spreading hello load (represented via [Metrics](service-fabric-cluster-resource-manager-metrics.md)) evenly throughout hello cluster.</span></span> <span data-ttu-id="60588-105">Service Fabric управляет емкости hello hello узлов в кластер hello и кластер hello в целом через [емкость](service-fabric-cluster-resource-manager-cluster-description.md).</span><span class="sxs-lookup"><span data-stu-id="60588-105">Service Fabric manages hello capacity of hello nodes in hello cluster and hello cluster as a whole via [capacity](service-fabric-cluster-resource-manager-cluster-description.md).</span></span> <span data-ttu-id="60588-106">Метрики и емкость отлично работают для большинства рабочих нагрузок, но для структур, активно использующих разные экземпляры приложений Service Fabric, иногда возникают дополнительные требования.</span><span class="sxs-lookup"><span data-stu-id="60588-106">Metrics and capacity work great for many workloads, but patterns that make heavy use of different Service Fabric Application Instances sometimes bring in additional requirements.</span></span> <span data-ttu-id="60588-107">Например, может потребоваться следующее.</span><span class="sxs-lookup"><span data-stu-id="60588-107">For example you may want to:</span></span>

- <span data-ttu-id="60588-108">Резервирование какого hello узлах кластера hello hello службы в некоторых именованный экземпляр приложения</span><span class="sxs-lookup"><span data-stu-id="60588-108">Reserve some capacity on hello nodes in hello cluster for hello services within some named application instance</span></span>
- <span data-ttu-id="60588-109">Ограничить общее число узлов, работающих служб hello в именованный экземпляр приложения на (вместо рассредоточения их через весь кластер hello) для hello</span><span class="sxs-lookup"><span data-stu-id="60588-109">Limit hello total number of nodes that hello services within a named application instance run on (instead of spreading them out over hello entire cluster)</span></span>
- <span data-ttu-id="60588-110">Определить емкость для hello именованный экземпляр приложения сам toolimit hello число служб или общее потребление ресурсов hello служб внутри него</span><span class="sxs-lookup"><span data-stu-id="60588-110">Define capacities on hello named application instance itself toolimit hello number of services or total resource consumption of hello services inside it</span></span>

<span data-ttu-id="60588-111">toomeet эти требования hello диспетчер ресурсов кластера Service Fabric поддерживает функцию групп приложений.</span><span class="sxs-lookup"><span data-stu-id="60588-111">toomeet these requirements, hello Service Fabric Cluster Resource Manager supports a feature called Application Groups.</span></span>

## <a name="limiting-hello-maximum-number-of-nodes"></a><span data-ttu-id="60588-112">Ограничивая максимальное количество узлов hello</span><span class="sxs-lookup"><span data-stu-id="60588-112">Limiting hello maximum number of nodes</span></span>
<span data-ttu-id="60588-113">Hello простейший вариант использования емкости приложения при экземпляр приложения должен toobe ограниченную tooa определенных максимальное количество узлов.</span><span class="sxs-lookup"><span data-stu-id="60588-113">hello simplest use case for Application capacity is when an application instance needs toobe limited tooa certain maximum number of nodes.</span></span> <span data-ttu-id="60588-114">Это позволяет объединить все службы, выполняющиеся в этом экземпляре приложения, на заданном количестве компьютеров.</span><span class="sxs-lookup"><span data-stu-id="60588-114">This consolidates all services within that application instance onto a set number of machines.</span></span> <span data-ttu-id="60588-115">Консолидация полезно, когда вы пытаетесь toopredict или ограничения максимального физических ресурсов, используемых службами hello в этот именованный экземпляр приложения.</span><span class="sxs-lookup"><span data-stu-id="60588-115">Consolidation is useful when you're trying toopredict or cap physical resource use by hello services within that named application instance.</span></span> 

<span data-ttu-id="60588-116">Hello иллюстрации показан экземпляр приложения с и без максимальное количество узлов, определенных.</span><span class="sxs-lookup"><span data-stu-id="60588-116">hello following image shows an application instance with and without a maximum number of nodes defined:</span></span>

<span data-ttu-id="60588-117"><center>
![Определение максимального количества узлов для экземпляров приложения][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="60588-117"><center>
![Application Instance Defining Maximum Number of Nodes][Image1]
</center></span></span>

<span data-ttu-id="60588-118">В примере hello левой приложения hello не имеет максимальное количество узлов, определенных и он имеет три службы.</span><span class="sxs-lookup"><span data-stu-id="60588-118">In hello left example, hello application doesn’t have a maximum number of nodes defined, and it has three services.</span></span> <span data-ttu-id="60588-119">Hello диспетчер ресурсов кластера разбросаны все реплики шесть доступные узлы tooachieve hello оптимальный баланс в кластере hello (поведение по умолчанию hello).</span><span class="sxs-lookup"><span data-stu-id="60588-119">hello Cluster Resource Manager has spread out all replicas across six available nodes tooachieve hello best balance in hello cluster (hello default behavior).</span></span> <span data-ttu-id="60588-120">В примере справа hello, мы увидим hello того же приложения ограниченных узлов toothree.</span><span class="sxs-lookup"><span data-stu-id="60588-120">In hello right example, we see hello same application limited toothree nodes.</span></span>

<span data-ttu-id="60588-121">параметр Hello, управляющий такое поведение называется максимальное число узлов.</span><span class="sxs-lookup"><span data-stu-id="60588-121">hello parameter that controls this behavior is called MaximumNodes.</span></span> <span data-ttu-id="60588-122">Этот параметр можно задать при создании приложения или изменить для уже выполняющегося экземпляра приложения.</span><span class="sxs-lookup"><span data-stu-id="60588-122">This parameter can be set during application creation, or updated for an application instance that was already running.</span></span>

<span data-ttu-id="60588-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="60588-123">Powershell</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

<span data-ttu-id="60588-124">C#</span><span class="sxs-lookup"><span data-stu-id="60588-124">C#</span></span>

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

<span data-ttu-id="60588-125">В рамках hello набора узлов hello диспетчер ресурсов кластера не гарантирует, какие объекты службы достаточная вместе или использовать, какие узлы.</span><span class="sxs-lookup"><span data-stu-id="60588-125">Within hello set of nodes, hello Cluster Resource Manager doesn't guarantee which service objects get placed together or which nodes get used.</span></span>

## <a name="application-metrics-load-and-capacity"></a><span data-ttu-id="60588-126">Метрики, нагрузка и емкость приложения</span><span class="sxs-lookup"><span data-stu-id="60588-126">Application Metrics, Load, and Capacity</span></span>
<span data-ttu-id="60588-127">Группы приложений также позволяют toodefine показатели, связанные с данной именованный экземпляр приложения, а емкость данного экземпляра приложения для этих показателей.</span><span class="sxs-lookup"><span data-stu-id="60588-127">Application Groups also allow you toodefine metrics associated with a given named application instance, and that application instance's capacity for those metrics.</span></span> <span data-ttu-id="60588-128">Метрики приложения позволяют tootrack, резервировать и предел потребления ресурсов hello hello служб внутри данного экземпляра приложения.</span><span class="sxs-lookup"><span data-stu-id="60588-128">Application metrics allow you tootrack, reserve, and limit hello resource consumption of hello services inside that application instance.</span></span>

<span data-ttu-id="60588-129">Для каждой метрики приложения можно установить два значения.</span><span class="sxs-lookup"><span data-stu-id="60588-129">For each application metric, there are two values that can be set:</span></span>

- <span data-ttu-id="60588-130">**Общая емкость приложения** — этот параметр представляет hello общая емкость приложения hello для конкретного показателя.</span><span class="sxs-lookup"><span data-stu-id="60588-130">**Total Application Capacity** – This setting represents hello total capacity of hello application for a particular metric.</span></span> <span data-ttu-id="60588-131">Диспетчер ресурсов кластера Hello запрещает hello создания новых служб в пределах данного экземпляра приложения, которое вызовет tooexceed общую нагрузку это значение.</span><span class="sxs-lookup"><span data-stu-id="60588-131">hello Cluster Resource Manager disallows hello creation of any new services within this application instance that would cause total load tooexceed this value.</span></span> <span data-ttu-id="60588-132">Например предположим, что экземпляр приложения hello составляет 10 и уже имеется пять загрузку.</span><span class="sxs-lookup"><span data-stu-id="60588-132">For example, let's say hello application instance had a capacity of 10 and already had load of five.</span></span> <span data-ttu-id="60588-133">Hello создании службы с загрузкой по умолчанию всего 10 будет запрещено.</span><span class="sxs-lookup"><span data-stu-id="60588-133">hello creation of a service with a total default load of 10 would be disallowed.</span></span>
- <span data-ttu-id="60588-134">**Максимальная емкость узла** — этот параметр определяет максимальное hello общую нагрузку для приложения hello на одном узле.</span><span class="sxs-lookup"><span data-stu-id="60588-134">**Maximum Node Capacity** – This setting specifies hello maximum total load for hello application on a single node.</span></span> <span data-ttu-id="60588-135">Если нагрузки переходит по емкости, hello диспетчер ресурсов кластера перемещает узлы tooother реплики так, чтобы hello уменьшения нагрузки.</span><span class="sxs-lookup"><span data-stu-id="60588-135">If load goes over this capacity, hello Cluster Resource Manager moves replicas tooother nodes so that hello load decreases.</span></span>


<span data-ttu-id="60588-136">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="60588-136">Powershell:</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

<span data-ttu-id="60588-137">C#:</span><span class="sxs-lookup"><span data-stu-id="60588-137">C#:</span></span>

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

## <a name="reserving-capacity"></a><span data-ttu-id="60588-138">Резервирование емкости</span><span class="sxs-lookup"><span data-stu-id="60588-138">Reserving Capacity</span></span>
<span data-ttu-id="60588-139">Еще одно распространенное использование групп приложений является tooensure hello, ресурсов в кластере зарезервированы для экземпляров данного приложения.</span><span class="sxs-lookup"><span data-stu-id="60588-139">Another common use for application groups is tooensure that resources within hello cluster are reserved for a given application instance.</span></span> <span data-ttu-id="60588-140">При создании экземпляра приложения hello всегда резервируется место Hello.</span><span class="sxs-lookup"><span data-stu-id="60588-140">hello space is always reserved when hello application instance is created.</span></span>

<span data-ttu-id="60588-141">Резервирование пространства в кластере hello для приложения hello произойдет немедленно, даже когда:</span><span class="sxs-lookup"><span data-stu-id="60588-141">Reserving space in hello cluster for hello application happens immediately even when:</span></span>
- <span data-ttu-id="60588-142">создается экземпляр приложения Hello, но не сопоставлено ни одной службы в ней еще</span><span class="sxs-lookup"><span data-stu-id="60588-142">hello application instance is created but doesn't have any services within it yet</span></span>
- <span data-ttu-id="60588-143">Hello нескольким службам внутри экземпляра приложения hello изменяется каждый раз</span><span class="sxs-lookup"><span data-stu-id="60588-143">hello number of services within hello application instance changes every time</span></span> 
- <span data-ttu-id="60588-144">Hello службы существует, но не использует ресурсы hello</span><span class="sxs-lookup"><span data-stu-id="60588-144">hello services exist but aren't consuming hello resources</span></span> 

<span data-ttu-id="60588-145">Чтобы зарезервировать ресурсы для экземпляра приложения, следует использовать два дополнительных параметра: *MinimumNodes* и *NodeReservationCapacity*.</span><span class="sxs-lookup"><span data-stu-id="60588-145">Reserving resources for an application instance requires specifying two additional parameters: *MinimumNodes* and *NodeReservationCapacity*</span></span>

- <span data-ttu-id="60588-146">**Минимальное число узлов** -определяет hello минимальное число узлов, которые приложение hello экземпляр должен работать.</span><span class="sxs-lookup"><span data-stu-id="60588-146">**MinimumNodes** - Defines hello minimum number of nodes that hello application instance should run on.</span></span>  
- <span data-ttu-id="60588-147">**NodeReservationCapacity** -эта настройка выполняется на уровне метрики для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="60588-147">**NodeReservationCapacity** - This setting is per metric for hello application.</span></span> <span data-ttu-id="60588-148">значение Hello — hello объем эта метрика зарезервированы для приложения hello на любом узле, где, hello службами этого запуска приложения.</span><span class="sxs-lookup"><span data-stu-id="60588-148">hello value is hello amount of that metric reserved for hello application on any node where that hello services in that application run.</span></span>

<span data-ttu-id="60588-149">Объединение **минимальное число узлов** и **NodeReservationCapacity** гарантирует резервирование минимальное нагрузки для приложения hello в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="60588-149">Combining **MinimumNodes** and **NodeReservationCapacity** guarantees a minimum load reservation for hello application within hello cluster.</span></span> <span data-ttu-id="60588-150">Если осталось меньше емкости в hello кластера требуется общее резервирование hello, происходит сбой создания приложения hello.</span><span class="sxs-lookup"><span data-stu-id="60588-150">If there's less remaining capacity in hello cluster than hello total reservation required, creation of hello application fails.</span></span> 

<span data-ttu-id="60588-151">Рассмотрим пример резервирования емкости.</span><span class="sxs-lookup"><span data-stu-id="60588-151">Let's look at an example of capacity reservation:</span></span>

<span data-ttu-id="60588-152"><center>
![Определение резервируемой емкости для экземпляров приложения][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="60588-152"><center>
![Application Instances Defining Reserved Capacity][Image2]
</center></span></span>

<span data-ttu-id="60588-153">В примере hello левой приложения не все пространство приложения определены.</span><span class="sxs-lookup"><span data-stu-id="60588-153">In hello left example, applications do not have any Application Capacity defined.</span></span> <span data-ttu-id="60588-154">Диспетчер ресурсов кластера Hello сальдо все данные в соответствии с правилами toonormal.</span><span class="sxs-lookup"><span data-stu-id="60588-154">hello Cluster Resource Manager balances everything according toonormal rules.</span></span>

<span data-ttu-id="60588-155">В примере hello на правом hello Предположим, что Application1 создавался hello следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="60588-155">In hello example on hello right, let's say that Application1 was created with hello following settings:</span></span>

- <span data-ttu-id="60588-156">Tootwo набор узлов</span><span class="sxs-lookup"><span data-stu-id="60588-156">MinimumNodes set tootwo</span></span>
- <span data-ttu-id="60588-157">для приложения определена метрика со следующими значениями:</span><span class="sxs-lookup"><span data-stu-id="60588-157">An application Metric defined with</span></span>
  - <span data-ttu-id="60588-158">NodeReservationCapacity = 20;</span><span class="sxs-lookup"><span data-stu-id="60588-158">NodeReservationCapacity of 20</span></span>

<span data-ttu-id="60588-159">PowerShell</span><span class="sxs-lookup"><span data-stu-id="60588-159">Powershell</span></span>

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

<span data-ttu-id="60588-160">C#</span><span class="sxs-lookup"><span data-stu-id="60588-160">C#</span></span>

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

<span data-ttu-id="60588-161">Service Fabric резервирует мощность на двух узлах для Application1 и не допускает служб из Application2 tooconsume его емкость, даже если существуют нагрузки не поглощается hello служб внутри Application1 во время hello.</span><span class="sxs-lookup"><span data-stu-id="60588-161">Service Fabric reserves capacity on two nodes for Application1, and doesn't allow services from Application2 tooconsume that capacity even if there are no load is being consumed by hello services inside Application1 at hello time.</span></span> <span data-ttu-id="60588-162">Зарезервированные приложения емкости считается потребляет и вычитается hello оставшихся емкости на этом узле и в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="60588-162">This reserved application capacity is considered consumed  and counts against hello remaining capacity on that node and within hello cluster.</span></span>  <span data-ttu-id="60588-163">Резервирование Hello вычитается из оставшихся емкость кластера немедленно hello, однако зарезервированные hello потребление вычитается из hello емкость конкретного узла только в том случае, если по крайней мере одна служба объект помещается на нем.</span><span class="sxs-lookup"><span data-stu-id="60588-163">hello reservation is deducted from hello remaining cluster capacity immediately, however hello reserved consumption is deducted from hello capacity of a specific node only when at least one service object is placed on it.</span></span> <span data-ttu-id="60588-164">Этот второй этап резервирования позволяет более гибко и более эффективно использовать ресурсы, поскольку на конкретных узлах резервирование происходит только по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="60588-164">This later reservation allows for flexibility and better resource utilization since resources are only reserved on nodes when needed.</span></span>

## <a name="obtaining-hello-application-load-information"></a><span data-ttu-id="60588-165">Получение сведений о нагрузки приложения hello</span><span class="sxs-lookup"><span data-stu-id="60588-165">Obtaining hello application load information</span></span>
<span data-ttu-id="60588-166">Для каждого приложения, которое емкостью приложения, определенные для одну или несколько метрик можно получить hello сведения о hello суммарную нагрузку, о которых сообщили реплик службы.</span><span class="sxs-lookup"><span data-stu-id="60588-166">For each application that has an Application Capacity defined for one or more metrics you can obtain hello information about hello aggregate load reported by replicas of its services.</span></span>

<span data-ttu-id="60588-167">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="60588-167">Powershell:</span></span>

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

<span data-ttu-id="60588-168">C#</span><span class="sxs-lookup"><span data-stu-id="60588-168">C#</span></span>

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

<span data-ttu-id="60588-169">Hello ApplicationLoad запрос возвращает hello основные сведения о производительности приложения, указанная для приложения hello.</span><span class="sxs-lookup"><span data-stu-id="60588-169">hello ApplicationLoad query returns hello basic information about Application Capacity that was specified for hello application.</span></span> <span data-ttu-id="60588-170">Эти сведения включают hello минимальное и максимальное узлам сведений и hello число, которое в настоящее время занимает приложения hello.</span><span class="sxs-lookup"><span data-stu-id="60588-170">This information includes hello Minimum Nodes and Maximum Nodes info, and hello number that hello application is currently occupying.</span></span> <span data-ttu-id="60588-171">Также вы получите информацию по каждой метрике нагрузки для приложения, в том числе перечисленные ниже сведения.</span><span class="sxs-lookup"><span data-stu-id="60588-171">It also includes information about each application load metric, including:</span></span>

* <span data-ttu-id="60588-172">Имя метрики: Имя метрики hello.</span><span class="sxs-lookup"><span data-stu-id="60588-172">Metric Name: Name of hello metric.</span></span>
* <span data-ttu-id="60588-173">Емкость резервирования: Емкость кластера, зарезервированный для данного приложения в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="60588-173">Reservation Capacity: Cluster Capacity that is reserved in hello cluster for this Application.</span></span>
* <span data-ttu-id="60588-174">Application Load: общая нагрузка, создаваемая дочерними репликами этого приложения.</span><span class="sxs-lookup"><span data-stu-id="60588-174">Application Load: Total Load of this Application’s child replicas.</span></span>
* <span data-ttu-id="60588-175">Application Capacity: максимально допустимое значение нагрузки приложения.</span><span class="sxs-lookup"><span data-stu-id="60588-175">Application Capacity: Maximum permitted value of Application Load.</span></span>

## <a name="removing-application-capacity"></a><span data-ttu-id="60588-176">Удаление емкости приложения</span><span class="sxs-lookup"><span data-stu-id="60588-176">Removing Application Capacity</span></span>
<span data-ttu-id="60588-177">После настройки параметров производительности приложения hello для приложения, их можно удалить с помощью API-интерфейсы для обновления приложения или командлеты PowerShell.</span><span class="sxs-lookup"><span data-stu-id="60588-177">Once hello Application Capacity parameters are set for an application, they can be removed using Update Application APIs or PowerShell cmdlets.</span></span> <span data-ttu-id="60588-178">Например:</span><span class="sxs-lookup"><span data-stu-id="60588-178">For example:</span></span>

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

<span data-ttu-id="60588-179">Эта команда удаляет все параметры управления емкостью приложения из экземпляра приложения hello.</span><span class="sxs-lookup"><span data-stu-id="60588-179">This command removes all Application capacity management parameters from hello application instance.</span></span> <span data-ttu-id="60588-180">Включает минимальное число узлов, узлов и показатели приложения hello, если таковые имеются.</span><span class="sxs-lookup"><span data-stu-id="60588-180">This includes MinimumNodes, MaximumNodes, and hello Application's metrics, if any.</span></span> <span data-ttu-id="60588-181">Hello hello команда действует немедленно.</span><span class="sxs-lookup"><span data-stu-id="60588-181">hello effect of hello command is immediate.</span></span> <span data-ttu-id="60588-182">После выполнения этой команды, hello диспетчер ресурсов кластера использует поведение по умолчанию hello для управления приложениями.</span><span class="sxs-lookup"><span data-stu-id="60588-182">After this command completes, hello Cluster Resource Manager uses hello default behavior for managing applications.</span></span> <span data-ttu-id="60588-183">Параметры емкости приложения можно задать снова, используя команду `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span><span class="sxs-lookup"><span data-stu-id="60588-183">Application Capacity parameters can be specified again via `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span></span>

### <a name="restrictions-on-application-capacity"></a><span data-ttu-id="60588-184">Ограничения на емкость приложений</span><span class="sxs-lookup"><span data-stu-id="60588-184">Restrictions on Application Capacity</span></span>
<span data-ttu-id="60588-185">Существует ряд ограничений на параметры емкости приложений, которые необходимо соблюдать.</span><span class="sxs-lookup"><span data-stu-id="60588-185">There are several restrictions on Application Capacity parameters that must be respected.</span></span> <span data-ttu-id="60588-186">При обнаружении ошибок во время проверки изменения не применяются.</span><span class="sxs-lookup"><span data-stu-id="60588-186">If there are validation errors no changes take place.</span></span>

- <span data-ttu-id="60588-187">Все числовые параметры должны иметь неотрицательные значения.</span><span class="sxs-lookup"><span data-stu-id="60588-187">All integer parameters must be non-negative numbers.</span></span>
- <span data-ttu-id="60588-188">MinimumNodes не может иметь значение больше, чем MaximumNodes.</span><span class="sxs-lookup"><span data-stu-id="60588-188">MinimumNodes must never be greater than MaximumNodes.</span></span>
- <span data-ttu-id="60588-189">Если определены емкости для метрики нагрузки, они должны соответствовать следующим правилам.</span><span class="sxs-lookup"><span data-stu-id="60588-189">If capacities for a load metric are defined, then they must follow these rules:</span></span>
  - <span data-ttu-id="60588-190">NodeReservationCapacity не может иметь значение больше, чем MaximumNodeCapacity.</span><span class="sxs-lookup"><span data-stu-id="60588-190">Node Reservation Capacity must not be greater than Maximum Node Capacity.</span></span> <span data-ttu-id="60588-191">Например нельзя ограничить hello емкости для hello метрики «CPU» на устройствах tootwo hello узла и повторите tooreserve три единицы на каждом узле.</span><span class="sxs-lookup"><span data-stu-id="60588-191">For example, you cannot limit hello capacity for hello metric “CPU” on hello node tootwo units and try tooreserve three units on each node.</span></span>
  - <span data-ttu-id="60588-192">Если указано максимальное число узлов, затем hello продукт максимальное число узлов и максимальная емкость узла не поддерживает больше, чем общая емкость приложения.</span><span class="sxs-lookup"><span data-stu-id="60588-192">If MaximumNodes is specified, then hello product of MaximumNodes and Maximum Node Capacity must not be greater than Total Application Capacity.</span></span> <span data-ttu-id="60588-193">Например предположим, что максимальная емкость узла для метрики нагрузки «CPU» имеет значение tooeight hello.</span><span class="sxs-lookup"><span data-stu-id="60588-193">For example, let's say hello Maximum Node Capacity for load metric “CPU” is set tooeight.</span></span> <span data-ttu-id="60588-194">Также предположим, что значение hello too10 максимальное число узлов.</span><span class="sxs-lookup"><span data-stu-id="60588-194">Let's also say you set hello Maximum Nodes too10.</span></span> <span data-ttu-id="60588-195">В этом случае общая емкость приложения для этой метрики нагрузки должна быть больше 80.</span><span class="sxs-lookup"><span data-stu-id="60588-195">In this case, Total Application Capacity must be greater than 80 for this load metric.</span></span>

<span data-ttu-id="60588-196">Hello ограничения применяются как во время создания приложений и обновлений.</span><span class="sxs-lookup"><span data-stu-id="60588-196">hello restrictions are enforced both during application creation and updates.</span></span>

## <a name="how-not-toouse-application-capacity"></a><span data-ttu-id="60588-197">Как toouse емкость приложения</span><span class="sxs-lookup"><span data-stu-id="60588-197">How not toouse Application Capacity</span></span>
- <span data-ttu-id="60588-198">Не предпринимайте toouse hello группы приложений функции tooconstrain приложения hello tooa _конкретных_ ограниченного набора узлов.</span><span class="sxs-lookup"><span data-stu-id="60588-198">Do not try toouse hello Application Group features tooconstrain hello application tooa _specific_ subset of nodes.</span></span> <span data-ttu-id="60588-199">Другими словами, можно указать, что приложение hello должно выполняться не более пяти узлов, но не какие конкретных пяти узлов в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="60588-199">In other words, you can specify that hello application runs on at most five nodes, but not which specific five nodes in hello cluster.</span></span> <span data-ttu-id="60588-200">Ограничение toospecific приложения узлов может осуществляться с помощью ограничений размещения для службы.</span><span class="sxs-lookup"><span data-stu-id="60588-200">Constraining an application toospecific nodes can be achieved using placement constraints for services.</span></span>
- <span data-ttu-id="60588-201">Не предпринимайте tooensure емкость приложения hello toouse, что две службы из того же приложения размещаются на hello hello разным узлам.</span><span class="sxs-lookup"><span data-stu-id="60588-201">Do not try toouse hello Application Capacity tooensure that two services from hello same application are placed on hello same nodes.</span></span> <span data-ttu-id="60588-202">Вместо этого используйте [сходство](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) или [ограничения размещения](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span><span class="sxs-lookup"><span data-stu-id="60588-202">Instead use [affinity](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) or [placement constraints](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span></span>

## <a name="next-steps"></a><span data-ttu-id="60588-203">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="60588-203">Next steps</span></span>
- <span data-ttu-id="60588-204">Дополнительные сведения о настройке служб см. в разделе [Настройка параметров Cluster Resource Manager для служб Service Fabric](service-fabric-cluster-resource-manager-configure-services.md).</span><span class="sxs-lookup"><span data-stu-id="60588-204">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>
- <span data-ttu-id="60588-205">toofind out о управляет hello диспетчер ресурсов кластера и балансировку нагрузки в кластере hello Извлеките hello статьи на [балансировки нагрузки](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="60588-205">toofind out about how hello Cluster Resource Manager manages and balances load in hello cluster, check out hello article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
- <span data-ttu-id="60588-206">Начать с начала hello и [получить введение toohello диспетчер ресурсов кластера Service Fabric](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="60588-206">Start from hello beginning and [get an Introduction toohello Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
- <span data-ttu-id="60588-207">Дополнительные сведения об использовании метрик см. в статье [Управление потреблением ресурсов и нагрузкой в Service Fabric с помощью метрик](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="60588-207">For more information on how metrics work generally, read up on [Service Fabric Load Metrics](service-fabric-cluster-resource-manager-metrics.md)</span></span>
- <span data-ttu-id="60588-208">Hello диспетчер ресурсов кластера позволяет настраивать различные параметры для описания кластера hello.</span><span class="sxs-lookup"><span data-stu-id="60588-208">hello Cluster Resource Manager has many options for describing hello cluster.</span></span> <span data-ttu-id="60588-209">toofind подробные сведения о них, извлеките в этой статье на [описания кластера Service Fabric](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="60588-209">toofind out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
