---
title: "aaaAzure ресурсами структуры службы для контейнеров и службы | Документы Microsoft"
description: "Azure Service Fabric позволяет toospecify ограничения ресурсов для служб, выполняемых внутри или вне контейнеров."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 34e368211d98ff6b5b294c9c8b3af5ca30eeb20c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="resource-governance"></a><span data-ttu-id="cc5e7-103">управление ресурсами;</span><span class="sxs-lookup"><span data-stu-id="cc5e7-103">Resource governance</span></span> 

<span data-ttu-id="cc5e7-104">При нескольких служб hello одного узла или кластера, возможно, что одна служба может потреблять больше ресурсов, лишить другие службы.</span><span class="sxs-lookup"><span data-stu-id="cc5e7-104">When running multiple services on hello same node or cluster, it is possible that one service might consume more resources starving other services.</span></span> <span data-ttu-id="cc5e7-105">Эта проблема является ссылка tooas hello шумный сосед проблемой.</span><span class="sxs-lookup"><span data-stu-id="cc5e7-105">This problem is referred tooas hello noisy-neighbor problem.</span></span> <span data-ttu-id="cc5e7-106">Service Fabric позволяет резервирования toospecify разработчика hello и ограничения на ресурсы tooguarantee службы и также ограничить его использование ресурсов.</span><span class="sxs-lookup"><span data-stu-id="cc5e7-106">Service Fabric allows hello developer toospecify reservations and limits per service tooguarantee resources and also limit its resource usage.</span></span> 

## <a name="resource-governance-metrics"></a><span data-ttu-id="cc5e7-107">Метрики управления ресурсами</span><span class="sxs-lookup"><span data-stu-id="cc5e7-107">Resource governance metrics</span></span> 

<span data-ttu-id="cc5e7-108">Управление ресурсами поддерживается в Service Fabric для каждого [пакета службы](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="cc5e7-108">Resource governance is supported in Service Fabric per [Service Package](service-fabric-application-model.md).</span></span> <span data-ttu-id="cc5e7-109">Hello ресурсов, назначенных tooService пакета можно разделить между пакетами кода.</span><span class="sxs-lookup"><span data-stu-id="cc5e7-109">hello resources that are assigned tooService Package can be further divided between code packages.</span></span> <span data-ttu-id="cc5e7-110">ограничения ресурсов Hello, заданные также означать hello резервирования ресурсов hello.</span><span class="sxs-lookup"><span data-stu-id="cc5e7-110">hello resource limits specified also mean hello reservation of hello resources.</span></span> <span data-ttu-id="cc5e7-111">Service Fabric поддерживает указание ЦП и памяти для каждого пакета службы с помощью двух встроенных [метрик](service-fabric-cluster-resource-manager-metrics.md):</span><span class="sxs-lookup"><span data-stu-id="cc5e7-111">Service Fabric supports specifying CPU and Memory per service package, using two built-in [metrics](service-fabric-cluster-resource-manager-metrics.md):</span></span>

* <span data-ttu-id="cc5e7-112">ЦП (Имя метрики `ServiceFabric:/_CpuCores`): лежит логического ядра, которая доступна на компьютере размещения hello и все ядра для всех узлов, считаются одинаковыми hello.</span><span class="sxs-lookup"><span data-stu-id="cc5e7-112">CPU (metric name `ServiceFabric:/_CpuCores`): A core is a logical core that is available on hello host machine, and all cores across all nodes are weighted hello same.</span></span>
* <span data-ttu-id="cc5e7-113">Память (Имя метрики `ServiceFabric:/_MemoryInMB`): памяти измеряется в мегабайтах, и он был сопоставлен toophysical памяти, которая доступна на компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="cc5e7-113">Memory (metric name `ServiceFabric:/_MemoryInMB`): Memory is expressed in megabytes, and it maps toophysical memory that is available on hello machine.</span></span>

<span data-ttu-id="cc5e7-114">Только гарантированное резервирование мягкий предоставляются - среды выполнения hello отклоняет открытия превышены доступные ресурсы пакеты новой службы.</span><span class="sxs-lookup"><span data-stu-id="cc5e7-114">Only soft reservation guarantees are provided - hello runtime rejects opening of new service packages available resources are exceeded.</span></span> <span data-ttu-id="cc5e7-115">Тем не менее другой исполняемого файла или контейнера, помещенного на узле hello, нарушить исходное гарантированное резервирование hello.</span><span class="sxs-lookup"><span data-stu-id="cc5e7-115">However, if another executable or container is placed on hello node, that may violate hello original reservation guarantees.</span></span>

<span data-ttu-id="cc5e7-116">Эти две метрики hello [диспетчер ресурсов кластера](service-fabric-cluster-resource-manager-cluster-description.md) отслеживает емкость всего кластера, hello нагрузки на каждом узле в кластере hello и оставшихся ресурсы в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="cc5e7-116">For these two metrics, hello [Cluster Resource Manager](service-fabric-cluster-resource-manager-cluster-description.md) tracks total cluster capacity, hello load on each node in hello cluster, and, remaining resources in hello cluster.</span></span> <span data-ttu-id="cc5e7-117">Эти две метрики эквивалентные tooany других пользователей или пользовательская метрика и все существующие возможности можно использовать с ними:</span><span class="sxs-lookup"><span data-stu-id="cc5e7-117">These two metrics are equivalent tooany other user or custom metric and all existing features can be used with them:</span></span>
* <span data-ttu-id="cc5e7-118">Кластер может представлять [балансировки](service-fabric-cluster-resource-manager-balancing.md) toothese двух метрики (по умолчанию) в соответствии с.</span><span class="sxs-lookup"><span data-stu-id="cc5e7-118">Cluster can be [balanced](service-fabric-cluster-resource-manager-balancing.md) according toothese two metrics (default behavior).</span></span>
* <span data-ttu-id="cc5e7-119">Кластер может представлять [дефрагментировать](service-fabric-cluster-resource-manager-defragmentation-metrics.md) toothese двух показатели в соответствии с.</span><span class="sxs-lookup"><span data-stu-id="cc5e7-119">Cluster can be [defragmented](service-fabric-cluster-resource-manager-defragmentation-metrics.md) according toothese two metrics.</span></span>
* <span data-ttu-id="cc5e7-120">При [описании кластера](service-fabric-cluster-resource-manager-cluster-description.md) для этих двух метрик можно задать емкость буфера.</span><span class="sxs-lookup"><span data-stu-id="cc5e7-120">When [describing a cluster](service-fabric-cluster-resource-manager-cluster-description.md), buffered capacity can be set for these two metrics.</span></span>

<span data-ttu-id="cc5e7-121">[Передача данных о динамической нагрузке](service-fabric-cluster-resource-manager-metrics.md) не поддерживается этими метриками, и нагрузка для них определяется во время создания.</span><span class="sxs-lookup"><span data-stu-id="cc5e7-121">[Dynamic load reporting](service-fabric-cluster-resource-manager-metrics.md) is not supported for these metrics, and loads for these metrics are defined at creation time.</span></span>

## <a name="cluster-set-up-for-enabling-resource-governance"></a><span data-ttu-id="cc5e7-122">Настройка кластера для включения управления ресурсами</span><span class="sxs-lookup"><span data-stu-id="cc5e7-122">Cluster set up for enabling resource governance</span></span>

<span data-ttu-id="cc5e7-123">Емкость должен быть определен вручную в каждом типе узла в кластере hello следующим образом:</span><span class="sxs-lookup"><span data-stu-id="cc5e7-123">Capacity should be defined manually in each node type in hello cluster as follows:</span></span>

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
<span data-ttu-id="cc5e7-124">Управление ресурсами допускается только в пользовательских службах, но не в каких-либо системных службах.</span><span class="sxs-lookup"><span data-stu-id="cc5e7-124">Resource governance is allowed only on user services and not on any system services.</span></span> <span data-ttu-id="cc5e7-125">При указании емкости некоторые ядра и память должны оставаться нераспределенными для системных служб.</span><span class="sxs-lookup"><span data-stu-id="cc5e7-125">When specifying capacity, some cores and memory must be left unallocated for system services.</span></span> <span data-ttu-id="cc5e7-126">Для достижения оптимальной производительности hello после параметра необходимо также включить в манифесте кластера hello:</span><span class="sxs-lookup"><span data-stu-id="cc5e7-126">For optimal performance, hello following setting should also be turned on in hello cluster manifest:</span></span> 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a><span data-ttu-id="cc5e7-127">Указание управления ресурсами</span><span class="sxs-lookup"><span data-stu-id="cc5e7-127">Specifying resource governance</span></span> 

<span data-ttu-id="cc5e7-128">Ограничения ресурсов системы управления указаны в манифесте приложения hello (раздел ServiceManifestImport), как показано в следующий пример hello:</span><span class="sxs-lookup"><span data-stu-id="cc5e7-128">Resource governance limits are specified in hello application manifest (ServiceManifestImport section) as shown in hello following example:</span></span>

```xml
<?xml version='1.0' encoding='UTF-8'?>
<ApplicationManifest ApplicationTypeName='TestAppTC1' ApplicationTypeVersion='vTC1' xsi:schemaLocation='http://schemas.microsoft.com/2011/01/fabric ServiceFabricServiceModel.xsd' xmlns='http://schemas.microsoft.com/2011/01/fabric' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance'>
  <Parameters>
  </Parameters>
  <!--
  ServicePackageA has hello number of CPU cores defined, but doesn't have hello MemoryInMB defined.
  In this case, Service Fabric will sum hello limits on code packages and uses hello sum as 
  hello overall ServicePackage limit.
  -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName='ServicePackageA' ServiceManifestVersion='v1'/>
    <Policies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="CodeA1" CpuShares="512" MemoryInMB="1000" />
      <ResourceGovernancePolicy CodePackageRef="CodeA2" CpuShares="256" MemoryInMB="1000" />
    </Policies>
  </ServiceManifestImport>
```
  
<span data-ttu-id="cc5e7-129">В этом примере пакет службы ServicePackageA получает одно ядро на узлах hello, где размещается.</span><span class="sxs-lookup"><span data-stu-id="cc5e7-129">In this example, service package ServicePackageA gets one core on hello nodes where it is placed.</span></span> <span data-ttu-id="cc5e7-130">Этот пакет обновления содержит два пакета кода (CodeA1 и CodeA2), и обе конечные точки задают hello `CpuShares` параметра.</span><span class="sxs-lookup"><span data-stu-id="cc5e7-130">This service package contains two code packages (CodeA1 and CodeA2), and both specify hello `CpuShares` parameter.</span></span> <span data-ttu-id="cc5e7-131">Hello долю CpuShares 512:256 делит hello core в двух пакетах кода hello.</span><span class="sxs-lookup"><span data-stu-id="cc5e7-131">hello proportion of CpuShares 512:256  divides hello core across hello two code packages.</span></span> <span data-ttu-id="cc5e7-132">Таким образом в этом примере CodeA1 возвращает две трети ядра, CodeA2 возвращает трети ядра (и резервирование программной гарантии hello же).</span><span class="sxs-lookup"><span data-stu-id="cc5e7-132">Thus, in this example, CodeA1 gets two-thirds of a core, and  CodeA2 gets one-third of a core (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="cc5e7-133">В случае, если при CpuShares для пакетов кода не указаны, Service Fabric делит ядер hello поровну между ними.</span><span class="sxs-lookup"><span data-stu-id="cc5e7-133">In case when CpuShares are not specified for code packages, Service Fabric divides hello cores equally among them.</span></span>

<span data-ttu-id="cc5e7-134">Ограничения памяти может абсолютным, поэтому оба пакета кода, ограниченный too1024 МБ памяти (и гарантии программной резервирование же hello).</span><span class="sxs-lookup"><span data-stu-id="cc5e7-134">Memory limits are absolute, so both code packages are limited too1024 MB of memory (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="cc5e7-135">Пакеты кода (контейнеров или процессов) не может tooallocate, который больше памяти, чем это ограничение, попытка toodo таким образом вызывает исключение нехватки памяти.</span><span class="sxs-lookup"><span data-stu-id="cc5e7-135">Code packages (containers or processes) are not able tooallocate more memory than this limit, and attempting toodo so results in an out-of-memory exception.</span></span> <span data-ttu-id="cc5e7-136">Toowork принудительного применения ограничения ресурсов все пакеты кода, в пакет службы должен иметь ограничения памяти.</span><span class="sxs-lookup"><span data-stu-id="cc5e7-136">For resource limit enforcement toowork, all code packages within a service package should have memory limits specified.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cc5e7-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="cc5e7-137">Next steps</span></span>
* <span data-ttu-id="cc5e7-138">toolearn более о диспетчер ресурсов кластера, см. в этой [статьи](service-fabric-cluster-resource-manager-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cc5e7-138">toolearn more about Cluster Resource Manager, read this [article](service-fabric-cluster-resource-manager-introduction.md).</span></span>
* <span data-ttu-id="cc5e7-139">прочитать этот текст toolearn Дополнительные сведения о модели приложения, пакеты обновления, пакеты кода и сопоставление реплик toothem [статьи](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="cc5e7-139">toolearn more about application model, service packages, code packages and how replicas map toothem read this [article](service-fabric-application-model.md).</span></span>
