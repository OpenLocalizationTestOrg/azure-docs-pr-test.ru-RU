---
title: "Статистическая обработка проводится работоспособности для объектов в aaaHow tooview Azure Service Fabric | Документы Microsoft"
description: "Описывается порядок просмотра tooquery и оценить сводной работоспособности Azure Service Fabric сущностей через запросов о работоспособности и общих запросов."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: fa34c52d-3a74-4b90-b045-ad67afa43fe5
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: add810551cac26d2b4ff81b57d94ddd780c2cc2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="view-service-fabric-health-reports"></a><span data-ttu-id="bd066-103">Просмотр отчетов о работоспособности Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bd066-103">View Service Fabric health reports</span></span>
<span data-ttu-id="bd066-104">В платформе Azure Service Fabric используется [модель работоспособности](service-fabric-health-introduction.md) с сущностями работоспособности, на основе которых компоненты системы и модули наблюдения создают отчеты о состоянии отслеживаемых локальных условий.</span><span class="sxs-lookup"><span data-stu-id="bd066-104">Azure Service Fabric introduces a [health model](service-fabric-health-introduction.md) with health entities on which system components and watchdogs can report local conditions that they are monitoring.</span></span> <span data-ttu-id="bd066-105">Hello [базе данных health store](service-fabric-health-introduction.md#health-store) агрегирует все toodetermine данных работоспособности ли сущности находятся в работоспособном состоянии.</span><span class="sxs-lookup"><span data-stu-id="bd066-105">hello [health store](service-fabric-health-introduction.md#health-store) aggregates all health data toodetermine whether entities are healthy.</span></span>

<span data-ttu-id="bd066-106">Hello кластера автоматически заполняется работоспособности отчеты, отправляемые компонентами системы hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-106">hello cluster is automatically populated with health reports sent by hello system components.</span></span> <span data-ttu-id="bd066-107">Дополнительные сведения по [tootroubleshoot отчетов работоспособности системы используйте](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span><span class="sxs-lookup"><span data-stu-id="bd066-107">Read more at [Use system health reports tootroubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).</span></span>

<span data-ttu-id="bd066-108">Service Fabric предоставляет hello суммарный работоспособности способов tooget hello сущностей:</span><span class="sxs-lookup"><span data-stu-id="bd066-108">Service Fabric provides multiple ways tooget hello aggregated health of hello entities:</span></span>

* <span data-ttu-id="bd066-109">[обозреватель Service Fabric](service-fabric-visualizing-your-cluster.md) или другие средства визуализации;</span><span class="sxs-lookup"><span data-stu-id="bd066-109">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) or other visualization tools</span></span>
* <span data-ttu-id="bd066-110">запросы работоспособности (с помощью PowerShell, API или REST);</span><span class="sxs-lookup"><span data-stu-id="bd066-110">Health queries (through PowerShell, API, or REST)</span></span>
* <span data-ttu-id="bd066-111">Общие запросов, которые возвращают список сущностей, которые имеют работоспособности в качестве одного из свойств hello (с помощью PowerShell, API или REST)</span><span class="sxs-lookup"><span data-stu-id="bd066-111">General queries that return a list of entities that have health as one of hello properties (through PowerShell, API, or REST)</span></span>

<span data-ttu-id="bd066-112">такими параметрами, давайте toodemonstrate используйте локальный кластер с пятью узлами и hello [fabric: / приложения WordCount](http://aka.ms/servicefabric-wordcountapp).</span><span class="sxs-lookup"><span data-stu-id="bd066-112">toodemonstrate these options, let's use a local cluster with five nodes and hello [fabric:/WordCount application](http://aka.ms/servicefabric-wordcountapp).</span></span> <span data-ttu-id="bd066-113">Hello **fabric: / WordCount** приложение содержит две службы по умолчанию, службы с отслеживанием состояния типа `WordCountServiceType`и службы без отслеживания состояния типа `WordCountWebServiceType`.</span><span class="sxs-lookup"><span data-stu-id="bd066-113">hello **fabric:/WordCount** application contains two default services, a stateful service of type `WordCountServiceType`, and a stateless service of type `WordCountWebServiceType`.</span></span> <span data-ttu-id="bd066-114">После изменения hello `ApplicationManifest.xml` toorequire семь целевые реплики для службы с отслеживанием состояния hello и одну секцию.</span><span class="sxs-lookup"><span data-stu-id="bd066-114">I changed hello `ApplicationManifest.xml` toorequire seven target replicas for hello stateful service and one partition.</span></span> <span data-ttu-id="bd066-115">Так как существует только пять узлов в кластере hello, компоненты системы hello отчет предупреждение на hello служебного раздела, поскольку находится ниже числа целевых hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-115">Because there are only five nodes in hello cluster, hello system components report a warning on hello service partition because it is below hello target count.</span></span>

```xml
<Service Name="WordCountService">
<<<<<<< HEAD
    <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="3">
      <UniformInt64Partition PartitionCount="1" LowKey="1" HighKey="26" />
    </StatefulService>
=======
  <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="2">
    <UniformInt64Partition PartitionCount="[WordCountService_PartitionCount]" LowKey="1" HighKey="26" />
  </StatefulService>
>>>>>>> 5e84dbdd8e45a5d6b36f435a550b7433b873bf11
</Service>
```

## <a name="health-in-service-fabric-explorer"></a><span data-ttu-id="bd066-116">Работоспособность в обозревателе Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bd066-116">Health in Service Fabric Explorer</span></span>
<span data-ttu-id="bd066-117">Обозреватель Service Fabric предоставляет представление visual hello кластера.</span><span class="sxs-lookup"><span data-stu-id="bd066-117">Service Fabric Explorer provides a visual view of hello cluster.</span></span> <span data-ttu-id="bd066-118">На hello ниже рисунке можно видеть, что:</span><span class="sxs-lookup"><span data-stu-id="bd066-118">In hello image below, you can see that:</span></span>

* <span data-ttu-id="bd066-119">Здравствуйте, приложения **fabric: / WordCount** — красным (по ошибке), так как он содержит событие ошибки, о которых сообщили **MyWatchdog** свойства hello **доступности**.</span><span class="sxs-lookup"><span data-stu-id="bd066-119">hello application **fabric:/WordCount** is red (in error) because it has an error event reported by **MyWatchdog** for hello property **Availability**.</span></span>
* <span data-ttu-id="bd066-120">Одна из его служб **fabric:/WordCount/WordCountService** выделена желтым (предупреждение).</span><span class="sxs-lookup"><span data-stu-id="bd066-120">One of its services, **fabric:/WordCount/WordCountService** is yellow (in warning).</span></span> <span data-ttu-id="bd066-121">При настройке службы Hello семь реплик и hello кластера имеет пять узлов, поэтому не могут находиться два repicas.</span><span class="sxs-lookup"><span data-stu-id="bd066-121">hello service is configured with seven replicas and hello cluster has five nodes, so two repicas can't be placed.</span></span> <span data-ttu-id="bd066-122">Несмотря на то, что это не показано, из-за системных отчета из раздела службы hello желтый `System.FM` о том, что `Partition is below target replica or instance count`.</span><span class="sxs-lookup"><span data-stu-id="bd066-122">Although it's not shown here, hello service partition is yellow because of a system report from `System.FM` saying that `Partition is below target replica or instance count`.</span></span> <span data-ttu-id="bd066-123">триггеры желтый секции Hello hello желтый службы.</span><span class="sxs-lookup"><span data-stu-id="bd066-123">hello yellow partition triggers hello yellow service.</span></span>
* <span data-ttu-id="bd066-124">из-за приложения hello красный Hello кластера — красным.</span><span class="sxs-lookup"><span data-stu-id="bd066-124">hello cluster is red because of hello red application.</span></span>

<span data-ttu-id="bd066-125">Вычисление Hello использует политики по умолчанию hello манифест кластера и манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="bd066-125">hello evaluation uses default policies from hello cluster manifest and application manifest.</span></span> <span data-ttu-id="bd066-126">Это строгие политики, при которых не допускаются сбои.</span><span class="sxs-lookup"><span data-stu-id="bd066-126">They are strict policies and do not tolerate any failure.</span></span>

<span data-ttu-id="bd066-127">Представление hello кластера Service Fabric Explorer:</span><span class="sxs-lookup"><span data-stu-id="bd066-127">View of hello cluster with Service Fabric Explorer:</span></span>

![Представление hello кластера Service Fabric Explorer.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> <span data-ttu-id="bd066-129">Дополнительные сведения об [обозревателе Service Fabric](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="bd066-129">Read more about [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

## <a name="health-queries"></a><span data-ttu-id="bd066-130">Запросы о работоспособности</span><span class="sxs-lookup"><span data-stu-id="bd066-130">Health queries</span></span>
<span data-ttu-id="bd066-131">Service Fabric предоставляет запросов о работоспособности для каждого hello поддерживается [типов сущностей](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span><span class="sxs-lookup"><span data-stu-id="bd066-131">Service Fabric exposes health queries for each of hello supported [entity types](service-fabric-health-introduction.md#health-entities-and-hierarchy).</span></span> <span data-ttu-id="bd066-132">Они доступны через API-Интерфейс, с помощью методов hello [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), командлеты PowerShell и REST.</span><span class="sxs-lookup"><span data-stu-id="bd066-132">They can be accessed through hello API, using methods on [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="bd066-133">Эти запросы возвращают сведения о сущности hello завершения работоспособности: hello суммарный состояние работоспособности, события работоспособности сущности, дочерних состояний работоспособности (если применимо), оценки неисправностей (когда сущность hello неработоспособен) и статистики исправности дочерних элементов (когда применимо).</span><span class="sxs-lookup"><span data-stu-id="bd066-133">These queries return complete health information about hello entity: hello aggregated health state, entity health events, child health states (when applicable), unhealthy evaluations (when hello entity is not healthy), and children health statistics (when applicable).</span></span>

> [!NOTE]
> <span data-ttu-id="bd066-134">Сущности работоспособности возвращается в том случае, если она будет заполнена в базе данных health store hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-134">A health entity is returned when it is fully populated in hello health store.</span></span> <span data-ttu-id="bd066-135">Hello объекта должен быть активной (но не удалена) и иметь отчета системы.</span><span class="sxs-lookup"><span data-stu-id="bd066-135">hello entity must be active (not deleted) and have a system report.</span></span> <span data-ttu-id="bd066-136">Его родительской сущности hello цепочку иерархии также необходимо иметь отчеты системы.</span><span class="sxs-lookup"><span data-stu-id="bd066-136">Its parent entities on hello hierarchy chain must also have system reports.</span></span> <span data-ttu-id="bd066-137">Если любое из этих условий не выполняется, возвращаемых запросами работоспособности hello [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) с [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` , показывает, почему hello сущности не возвращаются.</span><span class="sxs-lookup"><span data-stu-id="bd066-137">If any of these conditions are not satisfied, hello health queries return a [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) with [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` that shows why hello entity is not returned.</span></span>
>
>

<span data-ttu-id="bd066-138">идентификатор сущности hello, который зависит от типа сущности hello необходимо передавать запросов о работоспособности Hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-138">hello health queries must pass in hello entity identifier, which depends on hello entity type.</span></span> <span data-ttu-id="bd066-139">запросы Hello принимают параметры политики работоспособности необязательно.</span><span class="sxs-lookup"><span data-stu-id="bd066-139">hello queries accept optional health policy parameters.</span></span> <span data-ttu-id="bd066-140">Если указаны политики работоспособности, hello [политики работоспособности](service-fabric-health-introduction.md#health-policies) hello кластера или манифест приложения, используются для оценки.</span><span class="sxs-lookup"><span data-stu-id="bd066-140">If no health policies are specified, hello [health policies](service-fabric-health-introduction.md#health-policies) from hello cluster or application manifest are used for evaluation.</span></span> <span data-ttu-id="bd066-141">Если манифесты hello не содержит определение для политики работоспособности, политик работоспособности по умолчанию hello используются для оценки.</span><span class="sxs-lookup"><span data-stu-id="bd066-141">If hello manifests don't contain a definition for health policies, hello default health policies are used for evaluation.</span></span> <span data-ttu-id="bd066-142">политики работоспособности по умолчанию Hello не допускают наличие каких-либо ошибок.</span><span class="sxs-lookup"><span data-stu-id="bd066-142">hello default health policies do not tolerate any failures.</span></span> <span data-ttu-id="bd066-143">запросы Hello также принимает фильтры для возвращения только частичные дочерние элементы или события--hello из них, учитывают hello указанным фильтрам.</span><span class="sxs-lookup"><span data-stu-id="bd066-143">hello queries also accept filters for returning only partial children or events--hello ones that respect hello specified filters.</span></span> <span data-ttu-id="bd066-144">Другой фильтр позволяет исключить статистики hello дочерних элементов.</span><span class="sxs-lookup"><span data-stu-id="bd066-144">Another filter allows excluding hello children statistics.</span></span>

> [!NOTE]
> <span data-ttu-id="bd066-145">Hello вывода фильтров на стороне сервера hello, чтобы уменьшить размер ответного сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-145">hello output filters are applied on hello server side, so hello message reply size is reduced.</span></span> <span data-ttu-id="bd066-146">Рекомендуется использовать фильтры выхода hello toolimit hello данные возвращаются, а не применять фильтры на стороне клиента hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-146">We recommended that you use hello output filters toolimit hello data returned, rather than apply filters on hello client side.</span></span>
>
>

<span data-ttu-id="bd066-147">Данные о работоспособности сущности содержат:</span><span class="sxs-lookup"><span data-stu-id="bd066-147">An entity's health contains:</span></span>

* <span data-ttu-id="bd066-148">Здравствуйте, общее состояние работоспособности hello сущности.</span><span class="sxs-lookup"><span data-stu-id="bd066-148">hello aggregated health state of hello entity.</span></span> <span data-ttu-id="bd066-149">Вычисляется по hello работоспособности хранилища на основе сущности отчеты о работоспособности, дочерних состояний работоспособности (если применимо) и политики работоспособности.</span><span class="sxs-lookup"><span data-stu-id="bd066-149">Computed by hello health store based on entity health reports, child health states (when applicable), and health policies.</span></span> <span data-ttu-id="bd066-150">См. дополнительные сведения об [оценке работоспособности сущности](service-fabric-health-introduction.md#health-evaluation).</span><span class="sxs-lookup"><span data-stu-id="bd066-150">Read more about [entity health evaluation](service-fabric-health-introduction.md#health-evaluation).</span></span>  
* <span data-ttu-id="bd066-151">события работоспособности Hello hello сущности.</span><span class="sxs-lookup"><span data-stu-id="bd066-151">hello health events on hello entity.</span></span>
* <span data-ttu-id="bd066-152">Коллекция Hello состояний работоспособности всех дочерних элементов для hello сущностей, которые могут иметь дочерние элементы.</span><span class="sxs-lookup"><span data-stu-id="bd066-152">hello collection of health states of all children for hello entities that can have children.</span></span> <span data-ttu-id="bd066-153">состояния работоспособности Hello содержать идентификаторов сущностей и hello общее состояние работоспособности.</span><span class="sxs-lookup"><span data-stu-id="bd066-153">hello health states contain entity identifiers and hello aggregated health state.</span></span> <span data-ttu-id="bd066-154">tooget завершения работоспособности для дочернего объекта, вызвать hello запросов исправности для hello дочернего объекта типа и передать идентификатор hello дочернего элемента.</span><span class="sxs-lookup"><span data-stu-id="bd066-154">tooget complete health for a child, call hello query health for hello child entity type and pass in hello child identifier.</span></span>
* <span data-ttu-id="bd066-155">оценки неисправностей Hello в этой точке toohello о том, что запускается hello состояние сущности hello, если hello сущность находится в неработоспособном состоянии.</span><span class="sxs-lookup"><span data-stu-id="bd066-155">hello unhealthy evaluations that point toohello report that triggered hello state of hello entity, if hello entity is not healthy.</span></span> <span data-ttu-id="bd066-156">Hello вычисления выполняются рекурсивно, содержащий оценки работоспособности hello дочерние элементы, которые происходят в текущем состоянии работоспособности.</span><span class="sxs-lookup"><span data-stu-id="bd066-156">hello evaluations are recursive, containing hello children health evaluations that triggered current health state.</span></span> <span data-ttu-id="bd066-157">Например, модуль наблюдения сообщил об ошибке реплики.</span><span class="sxs-lookup"><span data-stu-id="bd066-157">For example, a watchdog reported an error against a replica.</span></span> <span data-ttu-id="bd066-158">работоспособность приложения Hello показывает неработоспособное оценку из-за неработоспособности службы tooan; Hello служба неисправна из-за tooa секции в сообщение об ошибке. раздел Hello неисправна из-за tooa реплики в сообщение об ошибке. Hello реплики неисправна из-за отчет о работоспособности toohello контрольного ошибки.</span><span class="sxs-lookup"><span data-stu-id="bd066-158">hello application health shows an unhealthy evaluation due tooan unhealthy service; hello service is unhealthy due tooa partition in error; hello partition is unhealthy due tooa replica in error; hello replica is unhealthy due toohello watchdog error health report.</span></span>
* <span data-ttu-id="bd066-159">Статистика Hello работоспособности для всех типов hello сущностей, которые имеют дочерние элементы дочерних элементов.</span><span class="sxs-lookup"><span data-stu-id="bd066-159">hello health statistics for all children types of hello entities that have children.</span></span> <span data-ttu-id="bd066-160">Например работоспособность кластера показывает hello общее число приложений, служб, разделы, реплики и развертывания сущностей в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-160">For example, cluster health shows hello total number of applications, services, partitions, replicas, and deployed entities in hello cluster.</span></span> <span data-ttu-id="bd066-161">Работоспособность службы показана hello общее число разделов и реплик в группе hello задается службы.</span><span class="sxs-lookup"><span data-stu-id="bd066-161">Service health shows hello total number of partitions and replicas under hello specified service.</span></span>

## <a name="get-cluster-health"></a><span data-ttu-id="bd066-162">Получение сведений о работоспособности кластера</span><span class="sxs-lookup"><span data-stu-id="bd066-162">Get cluster health</span></span>
<span data-ttu-id="bd066-163">Возвращает hello работоспособности hello объекта кластера и содержит hello состояния работоспособности приложений и узлы (потомков hello кластера).</span><span class="sxs-lookup"><span data-stu-id="bd066-163">Returns hello health of hello cluster entity and contains hello health states of applications and nodes (children of hello cluster).</span></span> <span data-ttu-id="bd066-164">Входные данные:</span><span class="sxs-lookup"><span data-stu-id="bd066-164">Input:</span></span>

* <span data-ttu-id="bd066-165">[Необязательно] hello политика работоспособности кластера используется tooevaluate hello узлов и события кластера hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-165">[Optional] hello cluster health policy used tooevaluate hello nodes and hello cluster events.</span></span>
* <span data-ttu-id="bd066-166">[Необязательно] hello сопоставления политики работоспособности приложения, с помощью политик работоспособности hello использовать политики манифеста приложения hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="bd066-166">[Optional] hello application health policy map, with hello health policies used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="bd066-167">[Необязательно] Фильтры для событий, узлов и приложений, которые указывают, какие операции представляют интерес и должны возвращаться в результате hello (например, только ошибки или предупреждения и ошибки).</span><span class="sxs-lookup"><span data-stu-id="bd066-167">[Optional] Filters for events, nodes, and applications that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="bd066-168">Все события, узлов и приложений, используемых tooevaluate hello суммарный работоспособность, независимо от того, фильтр hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-168">All events, nodes, and applications are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="bd066-169">[Необязательно] Фильтрация статистики исправности tooexclude.</span><span class="sxs-lookup"><span data-stu-id="bd066-169">[Optional] Filter tooexclude health statistics.</span></span>
* <span data-ttu-id="bd066-170">[Необязательно] Фильтрация tooinclude fabric: / статистику работоспособности системы в hello статистики исправности.</span><span class="sxs-lookup"><span data-stu-id="bd066-170">[Optional] Filter tooinclude fabric:/System health statistics in hello health statistics.</span></span> <span data-ttu-id="bd066-171">Применяется, только если статистики исправности hello не исключаются.</span><span class="sxs-lookup"><span data-stu-id="bd066-171">Only applicable when hello health statistics are not excluded.</span></span> <span data-ttu-id="bd066-172">По умолчанию hello работоспособности Статистика включает только статистики для пользовательских приложений и не системное приложение hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-172">By default, hello health statistics include only statistics for user applications and not hello System application.</span></span>

### <a name="api"></a><span data-ttu-id="bd066-173">API</span><span class="sxs-lookup"><span data-stu-id="bd066-173">API</span></span>
<span data-ttu-id="bd066-174">tooget кластера работоспособности, создайте `FabricClient` и вызова hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) метод для его **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="bd066-174">tooget cluster health, create a `FabricClient` and call hello [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) method on its **HealthManager**.</span></span>

<span data-ttu-id="bd066-175">Hello следующий вызов возвращает hello работоспособности кластера:</span><span class="sxs-lookup"><span data-stu-id="bd066-175">hello following call gets hello cluster health:</span></span>

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

<span data-ttu-id="bd066-176">Hello следующий код возвращает hello работоспособности кластера с помощью политики работоспособности кластера пользовательские и фильтрует узлы и приложения.</span><span class="sxs-lookup"><span data-stu-id="bd066-176">hello following code gets hello cluster health by using a custom cluster health policy and filters for nodes and applications.</span></span> <span data-ttu-id="bd066-177">Он указывает, включать структуры hello статистики исправности hello: / статистику системы.</span><span class="sxs-lookup"><span data-stu-id="bd066-177">It specifies that hello health statistics include hello fabric:/System statistics.</span></span> <span data-ttu-id="bd066-178">Он создает [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), который содержит входные данные для hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-178">It creates [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), which contains hello input information.</span></span>

```csharp
var policy = new ClusterHealthPolicy()
{
    MaxPercentUnhealthyNodes = 20
};
var nodesFilter = new NodeHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error | HealthStateFilter.Warning
};
var applicationsFilter = new ApplicationHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error
};
var healthStatisticsFilter = new ClusterHealthStatisticsFilter()
{
    ExcludeHealthStatistics = false,
    IncludeSystemApplicationHealthStatistics = true
};
var queryDescription = new ClusterHealthQueryDescription()
{
    HealthPolicy = policy,
    ApplicationsFilter = applicationsFilter,
    NodesFilter = nodesFilter,
    HealthStatisticsFilter = healthStatisticsFilter
};

ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="bd066-179">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd066-179">PowerShell</span></span>
<span data-ttu-id="bd066-180">командлет tooget Hello hello-состояние кластера — [Get ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span><span class="sxs-lookup"><span data-stu-id="bd066-180">hello cmdlet tooget hello cluster health is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth).</span></span> <span data-ttu-id="bd066-181">Сначала подключите toohello кластера с помощью hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) командлета.</span><span class="sxs-lookup"><span data-stu-id="bd066-181">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="bd066-182">Hello hello кластера находится в состоянии пятью узлами, Системное приложение hello и fabric: / WordCount настроена, как описано.</span><span class="sxs-lookup"><span data-stu-id="bd066-182">hello state of hello cluster is five nodes, hello system application, and fabric:/WordCount configured as described.</span></span>

<span data-ttu-id="bd066-183">Привет, выполнив командлет возвращает работоспособности кластера с помощью политики работоспособности по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="bd066-183">hello following cmdlet gets cluster health by using default health policies.</span></span> <span data-ttu-id="bd066-184">Hello общее состояние работоспособности — предупреждение, поскольку hello fabric: / приложения WordCount находится в состоянии предупреждения.</span><span class="sxs-lookup"><span data-stu-id="bd066-184">hello aggregated health state is warning, because hello fabric:/WordCount application is in warning.</span></span> <span data-ttu-id="bd066-185">Обратите внимание на то, как оценки неисправностей hello содержат сведения о hello условий, вызвавших работоспособности hello статистическая обработка.</span><span class="sxs-lookup"><span data-stu-id="bd066-185">Note how hello unhealthy evaluations provide details on hello conditions that triggered hello aggregated health.</span></span>

```xml
PS D:\ServiceFabric> Get-ServiceFabricClusterHealth


AggregatedHealthState   : Warning
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Warning'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                          
                          
NodeHealthStates        : 
                          NodeName              : _Node_4
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_3
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_2
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_1
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_0
                          AggregatedHealthState : Ok
                          
ApplicationHealthStates : 
                          ApplicationName       : fabric:/System
                          AggregatedHealthState : Ok
                          
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Warning
                          
HealthEvents            : None
HealthStatistics        : 
                          Node                  : 5 Ok, 0 Warning, 0 Error
                          Replica               : 6 Ok, 0 Warning, 0 Error
                          Partition             : 1 Ok, 1 Warning, 0 Error
                          Service               : 1 Ok, 1 Warning, 0 Error
                          DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                          DeployedApplication   : 5 Ok, 0 Warning, 0 Error
                          Application           : 0 Ok, 1 Warning, 0 Error
```

<span data-ttu-id="bd066-186">Hello следующий командлет PowerShell возвращает состояние hello hello кластера с помощью политики пользовательское приложение.</span><span class="sxs-lookup"><span data-stu-id="bd066-186">hello following PowerShell cmdlet gets hello health of hello cluster by using a custom application policy.</span></span> <span data-ttu-id="bd066-187">Фильтрует результаты tooget только приложения и узлов в ошибку или предупреждение.</span><span class="sxs-lookup"><span data-stu-id="bd066-187">It filters results tooget only applications and nodes in error or warning.</span></span> <span data-ttu-id="bd066-188">В результате ни один узел не будет возвращен, так как все узлы работоспособны.</span><span class="sxs-lookup"><span data-stu-id="bd066-188">As a result, no nodes are returned, as they are all healthy.</span></span> <span data-ttu-id="bd066-189">Только hello fabric: / приложения WordCount соблюдает фильтра приложения hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-189">Only hello fabric:/WordCount application respects hello applications filter.</span></span> <span data-ttu-id="bd066-190">Поскольку пользовательской политики hello указывает tooconsider предупреждения как ошибки для структуры hello: / приложения WordCount, приложение hello вычисляется как ошибочное, и поэтому является hello кластера.</span><span class="sxs-lookup"><span data-stu-id="bd066-190">Because hello custom policy specifies tooconsider warnings as errors for hello fabric:/WordCount application, hello application is evaluated as in error, and so is hello cluster.</span></span>

```powershell
PS D:\ServiceFabric> $appHealthPolicy = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicy
$appHealthPolicy.ConsiderWarningAsError = $true
$appHealthPolicyMap = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicyMap
$appUri1 = New-Object -TypeName System.Uri -ArgumentList "fabric:/WordCount"
$appHealthPolicyMap.Add($appUri1, $appHealthPolicy)
Get-ServiceFabricClusterHealth -ApplicationHealthPolicyMap $appHealthPolicyMap -ApplicationsFilter "Warning,Error" -NodesFilter "Warning,Error" -ExcludeHealthStatistics


AggregatedHealthState   : Error
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Error'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                          
                          
NodeHealthStates        : None
ApplicationHealthStates : 
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Error
                          
HealthEvents            : None
```

### <a name="rest"></a><span data-ttu-id="bd066-191">REST</span><span class="sxs-lookup"><span data-stu-id="bd066-191">REST</span></span>
<span data-ttu-id="bd066-192">Можно получить состояние работоспособности кластера с помощью [запрос GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) или [запрос POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) , включающего политики работоспособности, описанные в теле hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-192">You can get cluster health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-node-health"></a><span data-ttu-id="bd066-193">Получение сведений о работоспособности узла</span><span class="sxs-lookup"><span data-stu-id="bd066-193">Get node health</span></span>
<span data-ttu-id="bd066-194">Возвращает hello работоспособности узла сущности и содержит событий работоспособности hello, о которых сообщается в узле hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-194">Returns hello health of a node entity and contains hello health events reported on hello node.</span></span> <span data-ttu-id="bd066-195">Входные данные:</span><span class="sxs-lookup"><span data-stu-id="bd066-195">Input:</span></span>

* <span data-ttu-id="bd066-196">Имя узла [обязательно] hello, указывающее узел hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-196">[Required] hello node name that identifies hello node.</span></span>
* <span data-ttu-id="bd066-197">Параметры политики работоспособности кластера [необязательно] hello используется tooevaluate работоспособности.</span><span class="sxs-lookup"><span data-stu-id="bd066-197">[Optional] hello cluster health policy settings used tooevaluate health.</span></span>
* <span data-ttu-id="bd066-198">[Необязательно] Фильтровать события, указывающие, какие операции представляют интерес и должны возвращаться в результате hello (например, только ошибки или предупреждения и ошибки).</span><span class="sxs-lookup"><span data-stu-id="bd066-198">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="bd066-199">Все события, используемые tooevaluate hello суммарный работоспособность, независимо от того, фильтр hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-199">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="bd066-200">API</span><span class="sxs-lookup"><span data-stu-id="bd066-200">API</span></span>
<span data-ttu-id="bd066-201">состояние работоспособности узла tooget через hello API, создайте `FabricClient` и вызова hello [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) метод для его HealthManager.</span><span class="sxs-lookup"><span data-stu-id="bd066-201">tooget node health through hello API, create a `FabricClient` and call hello [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="bd066-202">Hello следующий код возвращает состояние работоспособности узла hello для имени указанного узла hello:</span><span class="sxs-lookup"><span data-stu-id="bd066-202">hello following code gets hello node health for hello specified node name:</span></span>

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

<span data-ttu-id="bd066-203">Hello следующий код возвращает состояние работоспособности узла hello для hello указанное имя узла и передает в фильтр событий и пользовательской политики с помощью [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="bd066-203">hello following code gets hello node health for hello specified node name and passes in events filter and custom policy through [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):</span></span>

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="bd066-204">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd066-204">PowerShell</span></span>
<span data-ttu-id="bd066-205">состояние работоспособности узла hello Hello командлет tooget — [Get ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span><span class="sxs-lookup"><span data-stu-id="bd066-205">hello cmdlet tooget hello node health is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth).</span></span> <span data-ttu-id="bd066-206">Сначала подключите toohello кластера с помощью hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) командлета.</span><span class="sxs-lookup"><span data-stu-id="bd066-206">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>
<span data-ttu-id="bd066-207">Привет, выполнив командлет возвращает состояние работоспособности узла hello с помощью политики работоспособности по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="bd066-207">hello following cmdlet gets hello node health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNodeHealth _Node_1


NodeName              : _Node_1
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 3
                        SentAt                : 7/13/2017 4:39:23 PM
                        ReceivedAt            : 7/13/2017 4:40:47 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 4:40:47 PM, LastWarning = 1/1/0001 12:00:00 AM
```

<span data-ttu-id="bd066-208">Hello следующий командлет возвращает hello работоспособности всех узлов в кластере hello:</span><span class="sxs-lookup"><span data-stu-id="bd066-208">hello following cmdlet gets hello health of all nodes in hello cluster:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNode | Get-ServiceFabricNodeHealth | select NodeName, AggregatedHealthState | ft -AutoSize

NodeName AggregatedHealthState
-------- ---------------------
_Node_4                     Ok
_Node_3                     Ok
_Node_2                     Ok
_Node_1                     Ok
_Node_0                     Ok
```

### <a name="rest"></a><span data-ttu-id="bd066-209">REST</span><span class="sxs-lookup"><span data-stu-id="bd066-209">REST</span></span>
<span data-ttu-id="bd066-210">Можно получить состояние работоспособности узла с [запрос GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) или [запрос POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) , включающего политики работоспособности, описанные в теле hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-210">You can get node health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-application-health"></a><span data-ttu-id="bd066-211">Получение сведений о работоспособности приложения</span><span class="sxs-lookup"><span data-stu-id="bd066-211">Get application health</span></span>
<span data-ttu-id="bd066-212">Возвращает hello работоспособности приложения сущности.</span><span class="sxs-lookup"><span data-stu-id="bd066-212">Returns hello health of an application entity.</span></span> <span data-ttu-id="bd066-213">Он содержит состояние работоспособности hello hello развертывания приложения и службы дочерних элементов.</span><span class="sxs-lookup"><span data-stu-id="bd066-213">It contains hello health states of hello deployed application and service children.</span></span> <span data-ttu-id="bd066-214">Входные данные:</span><span class="sxs-lookup"><span data-stu-id="bd066-214">Input:</span></span>

* <span data-ttu-id="bd066-215">[Обязательно] hello имя приложения (URI), идентифицирующий приложение hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-215">[Required] hello application name (URI) that identifies hello application.</span></span>
* <span data-ttu-id="bd066-216">Политика работоспособности приложения hello [необязательно] использовать политики манифеста приложения hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="bd066-216">[Optional] hello application health policy used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="bd066-217">[Необязательно] Фильтры для событий, служб и развернутых приложений, которые указывают, какие операции представляют интерес и должны возвращаться в результате hello (например, только ошибки или предупреждения и ошибки).</span><span class="sxs-lookup"><span data-stu-id="bd066-217">[Optional] Filters for events, services, and deployed applications that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="bd066-218">Все события, службы и развернутых приложений, используемых tooevaluate hello суммарный работоспособность, независимо от того, фильтр hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-218">All events, services, and deployed applications are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="bd066-219">[Необязательно] Фильтрация статистики исправности tooexclude hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-219">[Optional] Filter tooexclude hello health statistics.</span></span> <span data-ttu-id="bd066-220">Если не указан, статистики исправности hello включают ОК hello, предупреждения и количество ошибок для всех дочерних элементов приложения: службы, разделы, реплики, развернутых приложений и развертывания пакетов служб.</span><span class="sxs-lookup"><span data-stu-id="bd066-220">If not specified, hello health statistics include hello ok, warning, and error count for all application children: services, partitions, replicas, deployed applications, and deployed service packages.</span></span>

### <a name="api"></a><span data-ttu-id="bd066-221">API</span><span class="sxs-lookup"><span data-stu-id="bd066-221">API</span></span>
<span data-ttu-id="bd066-222">работоспособность приложения tooget, создать `FabricClient` и вызова hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) метод для его HealthManager.</span><span class="sxs-lookup"><span data-stu-id="bd066-222">tooget application health, create a `FabricClient` and call hello [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="bd066-223">Hello следующий код возвращает работоспособности приложения hello для hello указанное имя приложения (URI):</span><span class="sxs-lookup"><span data-stu-id="bd066-223">hello following code gets hello application health for hello specified application name (URI):</span></span>

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

<span data-ttu-id="bd066-224">Hello следующий код возвращает работоспособности приложения hello для hello указанное имя приложения (URI) с фильтрами и пользовательских политик указанного с помощью [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="bd066-224">hello following code gets hello application health for hello specified application name (URI), with filters and custom policies specified via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).</span></span>

```csharp
HealthStateFilter warningAndErrors = HealthStateFilter.Error | HealthStateFilter.Warning;
var serviceTypePolicy = new ServiceTypeHealthPolicy()
{
    MaxPercentUnhealthyPartitionsPerService = 0,
    MaxPercentUnhealthyReplicasPerPartition = 5,
    MaxPercentUnhealthyServices = 0,
};
var policy = new ApplicationHealthPolicy()
{
    ConsiderWarningAsError = false,
    DefaultServiceTypeHealthPolicy = serviceTypePolicy,
    MaxPercentUnhealthyDeployedApplications = 0,
};

var queryDescription = new ApplicationHealthQueryDescription(applicationName)
{
    HealthPolicy = policy,
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = warningAndErrors },
    ServicesFilter = new ServiceHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
    DeployedApplicationsFilter = new DeployedApplicationHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
};

ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="bd066-225">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd066-225">PowerShell</span></span>
<span data-ttu-id="bd066-226">Контроль работоспособности приложения hello Hello командлет tooget [Get ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="bd066-226">hello cmdlet tooget hello application health is [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="bd066-227">Сначала подключите toohello кластера с помощью hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) командлета.</span><span class="sxs-lookup"><span data-stu-id="bd066-227">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="bd066-228">Hello следующий командлет возвращает hello работоспособности hello **fabric: / WordCount** приложения:</span><span class="sxs-lookup"><span data-stu-id="bd066-228">hello following cmdlet returns hello health of hello **fabric:/WordCount** application:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Warning
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok
                                  
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Warning
                                  
DeployedApplicationHealthStates : 
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok
                                  
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/13/2017 5:57:05 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
                                  
HealthStatistics                : 
                                  Replica               : 6 Ok, 0 Warning, 0 Error
                                  Partition             : 1 Ok, 1 Warning, 0 Error
                                  Service               : 1 Ok, 1 Warning, 0 Error
                                  DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                                  DeployedApplication   : 5 Ok, 0 Warning, 0 Error
```

<span data-ttu-id="bd066-229">Здравствуйте, следующие передает командлет PowerShell в пользовательских политик.</span><span class="sxs-lookup"><span data-stu-id="bd066-229">hello following PowerShell cmdlet passes in custom policies.</span></span> <span data-ttu-id="bd066-230">Кроме того, он выполняет фильтрацию дочерних элементов и событий.</span><span class="sxs-lookup"><span data-stu-id="bd066-230">It also filters children and events.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth -ApplicationName fabric:/WordCount -ConsiderWarningAsError $true -ServicesFilter Error -EventsFilter Error -DeployedApplicationsFilter Error -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error
                                  
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

### <a name="rest"></a><span data-ttu-id="bd066-231">REST</span><span class="sxs-lookup"><span data-stu-id="bd066-231">REST</span></span>
<span data-ttu-id="bd066-232">Вы можете получить работоспособности приложения с помощью [запрос GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) или [запрос POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) , включающего политики работоспособности, описанные в теле hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-232">You can get application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-service-health"></a><span data-ttu-id="bd066-233">Получение сведений о работоспособности службы</span><span class="sxs-lookup"><span data-stu-id="bd066-233">Get service health</span></span>
<span data-ttu-id="bd066-234">Возвращает работоспособности hello объекта службы.</span><span class="sxs-lookup"><span data-stu-id="bd066-234">Returns hello health of a service entity.</span></span> <span data-ttu-id="bd066-235">Он содержит состояния работоспособности hello секции.</span><span class="sxs-lookup"><span data-stu-id="bd066-235">It contains hello partition health states.</span></span> <span data-ttu-id="bd066-236">Входные данные:</span><span class="sxs-lookup"><span data-stu-id="bd066-236">Input:</span></span>

* <span data-ttu-id="bd066-237">[Обязательно] hello имя службы (URI), определяющий службу hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-237">[Required] hello service name (URI) that identifies hello service.</span></span>
* <span data-ttu-id="bd066-238">Политика работоспособности приложения hello [необязательно] используется политика манифеста приложения hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="bd066-238">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="bd066-239">[Необязательно] Фильтры для событий и секции, которые указывают, какие операции представляют интерес и должны возвращаться в результате hello (например, только ошибки или предупреждения и ошибки).</span><span class="sxs-lookup"><span data-stu-id="bd066-239">[Optional] Filters for events and partitions that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="bd066-240">Все события и секций, используемых tooevaluate hello суммарный работоспособность, независимо от того, фильтр hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-240">All events and partitions are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="bd066-241">[Необязательно] Фильтрация статистики исправности tooexclude.</span><span class="sxs-lookup"><span data-stu-id="bd066-241">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="bd066-242">Если не указан, hello hello Показать статистику работоспособности ОК, предупреждения и ошибки подсчета для всех секций и реплик службы hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-242">If not specified, hello health statistics show hello ok, warning, and error count for all partitions and replicas of hello service.</span></span>

### <a name="api"></a><span data-ttu-id="bd066-243">API</span><span class="sxs-lookup"><span data-stu-id="bd066-243">API</span></span>
<span data-ttu-id="bd066-244">работоспособность службы tooget через hello API, создайте `FabricClient` и вызова hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) метод для его HealthManager.</span><span class="sxs-lookup"><span data-stu-id="bd066-244">tooget service health through hello API, create a `FabricClient` and call hello [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) method on its HealthManager.</span></span>

<span data-ttu-id="bd066-245">Hello следующий пример возвращает hello работоспособности службы с указанным именем службы (URI):</span><span class="sxs-lookup"><span data-stu-id="bd066-245">hello following example gets hello health of a service with specified service name (URI):</span></span>

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

<span data-ttu-id="bd066-246">Hello следующий код возвращает работоспособность службы hello hello указанное имя службы (URI), указывая фильтры и пользовательской политики через [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span><span class="sxs-lookup"><span data-stu-id="bd066-246">hello following code gets hello service health for hello specified service name (URI), specifying filters and custom policy via [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):</span></span>

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="bd066-247">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd066-247">PowerShell</span></span>
<span data-ttu-id="bd066-248">работоспособность службы hello tooget командлет Hello — [Get ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span><span class="sxs-lookup"><span data-stu-id="bd066-248">hello cmdlet tooget hello service health is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth).</span></span> <span data-ttu-id="bd066-249">Сначала подключите toohello кластера с помощью hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) командлета.</span><span class="sxs-lookup"><span data-stu-id="bd066-249">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="bd066-250">Привет, выполнив командлет возвращает hello службы работоспособности с помощью политики работоспособности по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="bd066-250">hello following cmdlet gets hello service health by using default health policies:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricServiceHealth -ServiceName fabric:/WordCount/WordCountService


ServiceName           : fabric:/WordCount/WordCountService
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                        
                        Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                        
                            Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
PartitionHealthStates : 
                        PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                        AggregatedHealthState : Warning
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 15
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
                        Partition             : 0 Ok, 1 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="bd066-251">REST</span><span class="sxs-lookup"><span data-stu-id="bd066-251">REST</span></span>
<span data-ttu-id="bd066-252">Можно получить состояние работоспособности службы с [запрос GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) или [запрос POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) , включающего политики работоспособности, описанные в теле hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-252">You can get service health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-partition-health"></a><span data-ttu-id="bd066-253">Получение сведений о работоспособности раздела</span><span class="sxs-lookup"><span data-stu-id="bd066-253">Get partition health</span></span>
<span data-ttu-id="bd066-254">Возвращает работоспособности hello объекта секции.</span><span class="sxs-lookup"><span data-stu-id="bd066-254">Returns hello health of a partition entity.</span></span> <span data-ttu-id="bd066-255">Он содержит состояния работоспособности реплики hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-255">It contains hello replica health states.</span></span> <span data-ttu-id="bd066-256">Входные данные:</span><span class="sxs-lookup"><span data-stu-id="bd066-256">Input:</span></span>

* <span data-ttu-id="bd066-257">Секции [обязательно] hello идентификатор (GUID), который идентифицирует секцию hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-257">[Required] hello partition ID (GUID) that identifies hello partition.</span></span>
* <span data-ttu-id="bd066-258">Политика работоспособности приложения hello [необязательно] используется политика манифеста приложения hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="bd066-258">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="bd066-259">[Необязательно] Фильтры для событий и реплик, которые указывают, какие операции представляют интерес и должны возвращаться в результате hello (например, только ошибки или предупреждения и ошибки).</span><span class="sxs-lookup"><span data-stu-id="bd066-259">[Optional] Filters for events and replicas that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="bd066-260">Все события и реплики представляют используется tooevaluate hello суммарный работоспособность, независимо от того, фильтр hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-260">All events and replicas are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="bd066-261">[Необязательно] Фильтрация статистики исправности tooexclude.</span><span class="sxs-lookup"><span data-stu-id="bd066-261">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="bd066-262">Если не указан, Статистика работоспособности hello показывает, сколько реплики находятся в ОК, предупреждения и ошибки состояния.</span><span class="sxs-lookup"><span data-stu-id="bd066-262">If not specified, hello health statistics show how many replicas are in ok, warning, and error states.</span></span>

### <a name="api"></a><span data-ttu-id="bd066-263">API</span><span class="sxs-lookup"><span data-stu-id="bd066-263">API</span></span>
<span data-ttu-id="bd066-264">Создание работоспособности раздела tooget через API, hello `FabricClient` и вызова hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) метод для его HealthManager.</span><span class="sxs-lookup"><span data-stu-id="bd066-264">tooget partition health through hello API, create a `FabricClient` and call hello [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="bd066-265">Создание toospecify необязательные параметры, [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="bd066-265">toospecify optional parameters, create [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).</span></span>

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a><span data-ttu-id="bd066-266">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd066-266">PowerShell</span></span>
<span data-ttu-id="bd066-267">— работоспособности раздела hello tooget командлет Hello [Get ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span><span class="sxs-lookup"><span data-stu-id="bd066-267">hello cmdlet tooget hello partition health is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth).</span></span> <span data-ttu-id="bd066-268">Сначала подключите toohello кластера с помощью hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) командлета.</span><span class="sxs-lookup"><span data-stu-id="bd066-268">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="bd066-269">Hello следующий командлет возвращает hello работоспособности для всех секций hello **fabric: / WordCount/WordCountService** службы и отфильтровывает состояния работоспособности реплики:</span><span class="sxs-lookup"><span data-stu-id="bd066-269">hello following cmdlet gets hello health for all partitions of hello **fabric:/WordCount/WordCountService** service and filters out replica health states:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 72
                        SentAt                : 7/13/2017 5:57:29 PM
                        ReceivedAt            : 7/13/2017 5:57:48 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/P RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/S RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Ok->Warning = 7/13/2017 5:57:48 PM, LastError = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131444445174851664
                        SentAt                : 7/13/2017 6:35:17 PM
                        ReceivedAt            : 7/13/2017 6:35:18 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/13/2017 5:57:48 PM, LastOk = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="bd066-270">REST</span><span class="sxs-lookup"><span data-stu-id="bd066-270">REST</span></span>
<span data-ttu-id="bd066-271">Можно получить состояние работоспособности раздела с [запрос GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) или [запрос POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) , включающего политики работоспособности, описанные в теле hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-271">You can get partition health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-replica-health"></a><span data-ttu-id="bd066-272">Получение сведений о работоспособности реплики</span><span class="sxs-lookup"><span data-stu-id="bd066-272">Get replica health</span></span>
<span data-ttu-id="bd066-273">Возвращает hello работоспособности реплики службы с отслеживанием состояния или экземпляра службы без отслеживания состояния.</span><span class="sxs-lookup"><span data-stu-id="bd066-273">Returns hello health of a stateful service replica or a stateless service instance.</span></span> <span data-ttu-id="bd066-274">Входные данные:</span><span class="sxs-lookup"><span data-stu-id="bd066-274">Input:</span></span>

* <span data-ttu-id="bd066-275">[Обязательно] hello секции идентификатор (GUID) и реплика идентификатор, определяющий hello реплики.</span><span class="sxs-lookup"><span data-stu-id="bd066-275">[Required] hello partition ID (GUID) and replica ID that identifies hello replica.</span></span>
* <span data-ttu-id="bd066-276">Параметры политики работоспособности приложения hello [необязательно] использовать политики манифеста приложения hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="bd066-276">[Optional] hello application health policy parameters used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="bd066-277">[Необязательно] Фильтровать события, указывающие, какие операции представляют интерес и должны возвращаться в результате hello (например, только ошибки или предупреждения и ошибки).</span><span class="sxs-lookup"><span data-stu-id="bd066-277">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="bd066-278">Все события, используемые tooevaluate hello суммарный работоспособность, независимо от того, фильтр hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-278">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="bd066-279">API</span><span class="sxs-lookup"><span data-stu-id="bd066-279">API</span></span>
<span data-ttu-id="bd066-280">создать работоспособности реплики hello tooget через API, hello `FabricClient` и вызова hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) метод для его HealthManager.</span><span class="sxs-lookup"><span data-stu-id="bd066-280">tooget hello replica health through hello API, create a `FabricClient` and call hello [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) method on its HealthManager.</span></span> <span data-ttu-id="bd066-281">дополнительных параметров, используйте toospecify [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="bd066-281">toospecify advanced parameters, use [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).</span></span>

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a><span data-ttu-id="bd066-282">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd066-282">PowerShell</span></span>
<span data-ttu-id="bd066-283">Hello командлет tooget hello реплики находятся в [Get ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span><span class="sxs-lookup"><span data-stu-id="bd066-283">hello cmdlet tooget hello replica health is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth).</span></span> <span data-ttu-id="bd066-284">Сначала подключите toohello кластера с помощью hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) командлета.</span><span class="sxs-lookup"><span data-stu-id="bd066-284">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="bd066-285">Hello следующий командлет возвращает работоспособности hello hello первичной реплики для всех секций hello службы:</span><span class="sxs-lookup"><span data-stu-id="bd066-285">hello following cmdlet gets hello health of hello primary replica for all partitions of hello service:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="bd066-286">REST</span><span class="sxs-lookup"><span data-stu-id="bd066-286">REST</span></span>
<span data-ttu-id="bd066-287">Можно получить состояние работоспособности реплики с [запрос GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) или [запрос POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) , включающего политики работоспособности, описанные в теле hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-287">You can get replica health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-deployed-application-health"></a><span data-ttu-id="bd066-288">Получение сведений о работоспособности развернутого приложения</span><span class="sxs-lookup"><span data-stu-id="bd066-288">Get deployed application health</span></span>
<span data-ttu-id="bd066-289">Работоспособность hello возвращает приложение, развернутое в сущности узла.</span><span class="sxs-lookup"><span data-stu-id="bd066-289">Returns hello health of an application deployed on a node entity.</span></span> <span data-ttu-id="bd066-290">Он содержит состояния работоспособности пакета службы развернуты hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-290">It contains hello deployed service package health states.</span></span> <span data-ttu-id="bd066-291">Входные данные:</span><span class="sxs-lookup"><span data-stu-id="bd066-291">Input:</span></span>

* <span data-ttu-id="bd066-292">Имя приложения hello [обязательно] (URI) и имя узла (string), определяющие hello развернутого приложения.</span><span class="sxs-lookup"><span data-stu-id="bd066-292">[Required] hello application name (URI) and node name (string) that identify hello deployed application.</span></span>
* <span data-ttu-id="bd066-293">Политика работоспособности приложения hello [необязательно] использовать политики манифеста приложения hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="bd066-293">[Optional] hello application health policy used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="bd066-294">[Необязательно] Фильтры для событий и развернутые пакеты служб, указывающие, какие операции представляют интерес и должны возвращаться в результате hello (например, только ошибки или предупреждения и ошибки).</span><span class="sxs-lookup"><span data-stu-id="bd066-294">[Optional] Filters for events and deployed service packages that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="bd066-295">Все события и развернутые пакеты служб, используемых tooevaluate hello суммарный работоспособность, независимо от того, фильтр hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-295">All events and deployed service packages are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>
* <span data-ttu-id="bd066-296">[Необязательно] Фильтрация статистики исправности tooexclude.</span><span class="sxs-lookup"><span data-stu-id="bd066-296">[Optional] Filter tooexclude health statistics.</span></span> <span data-ttu-id="bd066-297">Если не указан, статистики исправности hello показывают hello количество развернутым пакетам в ОК, предупреждения и ошибки состояния работоспособности.</span><span class="sxs-lookup"><span data-stu-id="bd066-297">If not specified, hello health statistics show hello number of deployed service packages in ok, warning, and error health states.</span></span>

### <a name="api"></a><span data-ttu-id="bd066-298">API</span><span class="sxs-lookup"><span data-stu-id="bd066-298">API</span></span>
<span data-ttu-id="bd066-299">работоспособность hello tooget приложение, развернутое на узле через hello API, создайте `FabricClient` и вызова hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) метод для его HealthManager.</span><span class="sxs-lookup"><span data-stu-id="bd066-299">tooget hello health of an application deployed on a node through hello API, create a `FabricClient` and call hello [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) method on its HealthManager.</span></span> <span data-ttu-id="bd066-300">toospecify необязательные параметры, используйте [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="bd066-300">toospecify optional parameters, use [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).</span></span>

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a><span data-ttu-id="bd066-301">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd066-301">PowerShell</span></span>
<span data-ttu-id="bd066-302">Hello работоспособности приложения hello развернут tooget командлета — [Get ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="bd066-302">hello cmdlet tooget hello deployed application health is [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps).</span></span> <span data-ttu-id="bd066-303">Сначала подключите toohello кластера с помощью hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) командлета.</span><span class="sxs-lookup"><span data-stu-id="bd066-303">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="bd066-304">toofind, где развертывается приложение, запустите [Get ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) и рассмотрим hello развернутых приложений дочерних элементов.</span><span class="sxs-lookup"><span data-stu-id="bd066-304">toofind out where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at hello deployed application children.</span></span>

<span data-ttu-id="bd066-305">Hello следующий командлет возвращает hello работоспособности hello **fabric: / WordCount** приложение, развернутое на **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="bd066-305">hello following cmdlet gets hello health of hello **fabric:/WordCount** application deployed on **_Node_2**.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplicationHealth -ApplicationName fabric:/WordCount -NodeName _Node_0


ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_0
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
                                     ServiceManifestName   : WordCountWebServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131444422261848308
                                     SentAt                : 7/13/2017 5:57:06 PM
                                     ReceivedAt            : 7/13/2017 5:57:17 PM
                                     TTL                   : Infinite
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a><span data-ttu-id="bd066-306">REST</span><span class="sxs-lookup"><span data-stu-id="bd066-306">REST</span></span>
<span data-ttu-id="bd066-307">Вы можете получить состояние работоспособности развернутого приложения с [запрос GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) или [запрос POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) , включающего политики работоспособности, описанные в теле hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-307">You can get deployed application health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="get-deployed-service-package-health"></a><span data-ttu-id="bd066-308">Получение сведений о работоспособности развернутого пакета службы</span><span class="sxs-lookup"><span data-stu-id="bd066-308">Get deployed service package health</span></span>
<span data-ttu-id="bd066-309">Возвращает hello работоспособности развернутой службы пакета сущности.</span><span class="sxs-lookup"><span data-stu-id="bd066-309">Returns hello health of a deployed service package entity.</span></span> <span data-ttu-id="bd066-310">Входные данные:</span><span class="sxs-lookup"><span data-stu-id="bd066-310">Input:</span></span>

* <span data-ttu-id="bd066-311">Имя приложения hello [обязательно] (URI), имя узла (string) и имя манифеста службы (string), определяющие hello развернутого пакета службы.</span><span class="sxs-lookup"><span data-stu-id="bd066-311">[Required] hello application name (URI), node name (string), and service manifest name (string) that identify hello deployed service package.</span></span>
* <span data-ttu-id="bd066-312">Политика работоспособности приложения hello [необязательно] используется политика манифеста приложения hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="bd066-312">[Optional] hello application health policy used toooverride hello application manifest policy.</span></span>
* <span data-ttu-id="bd066-313">[Необязательно] Фильтровать события, указывающие, какие операции представляют интерес и должны возвращаться в результате hello (например, только ошибки или предупреждения и ошибки).</span><span class="sxs-lookup"><span data-stu-id="bd066-313">[Optional] Filters for events that specify which entries are of interest and should be returned in hello result (for example, errors only, or both warnings and errors).</span></span> <span data-ttu-id="bd066-314">Все события, используемые tooevaluate hello суммарный работоспособность, независимо от того, фильтр hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-314">All events are used tooevaluate hello entity aggregated health, regardless of hello filter.</span></span>

### <a name="api"></a><span data-ttu-id="bd066-315">API</span><span class="sxs-lookup"><span data-stu-id="bd066-315">API</span></span>
<span data-ttu-id="bd066-316">работоспособность hello tooget к развернутому пакету служб через hello API, создайте `FabricClient` и вызова hello [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) метод для его HealthManager.</span><span class="sxs-lookup"><span data-stu-id="bd066-316">tooget hello health of a deployed service package through hello API, create a `FabricClient` and call hello [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) method on its HealthManager.</span></span> <span data-ttu-id="bd066-317">toospecify необязательные параметры, используйте [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span><span class="sxs-lookup"><span data-stu-id="bd066-317">toospecify optional parameters, use [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).</span></span>

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a><span data-ttu-id="bd066-318">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd066-318">PowerShell</span></span>
<span data-ttu-id="bd066-319">Hello работоспособности пакета службы развернуты hello tooget командлета — [Get ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span><span class="sxs-lookup"><span data-stu-id="bd066-319">hello cmdlet tooget hello deployed service package health is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth).</span></span> <span data-ttu-id="bd066-320">Сначала подключите toohello кластера с помощью hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) командлета.</span><span class="sxs-lookup"><span data-stu-id="bd066-320">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span> <span data-ttu-id="bd066-321">toosee, где развертывается приложение, запустите [Get ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) и поиска hello развертывания приложений.</span><span class="sxs-lookup"><span data-stu-id="bd066-321">toosee where an application is deployed, run [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) and look at hello deployed applications.</span></span> <span data-ttu-id="bd066-322">toosee, которого пакеты обновления имеют в приложении, просмотрите hello развернуть дочерние элементы пакета службы в hello [Get ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) выходных данных.</span><span class="sxs-lookup"><span data-stu-id="bd066-322">toosee which service packages are in an application, look at hello deployed service package children in hello [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) output.</span></span>

<span data-ttu-id="bd066-323">Hello следующий командлет возвращает hello работоспособности hello **WordCountServicePkg** пакет службы hello **fabric: / WordCount** приложение, развернутое на **_Node_2**.</span><span class="sxs-lookup"><span data-stu-id="bd066-323">hello following cmdlet gets hello health of hello **WordCountServicePkg** service package of hello **fabric:/WordCount** application deployed on **_Node_2**.</span></span> <span data-ttu-id="bd066-324">Hello сущность имеет **System.Hosting** отчеты для успешной активации пакета службы и точки входа и успешной регистрации типа службы.</span><span class="sxs-lookup"><span data-stu-id="bd066-324">hello entity has **System.Hosting** reports for successful service-package and entry-point activation, and successful service-type registration.</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplication -ApplicationName fabric:/WordCount -NodeName _Node_2 | Get-ServiceFabricDeployedServicePackageHealth -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_2
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131444422267693359
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131444422267903345
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131444422272458374
                             SentAt                : 7/13/2017 5:57:07 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a><span data-ttu-id="bd066-325">REST</span><span class="sxs-lookup"><span data-stu-id="bd066-325">REST</span></span>
<span data-ttu-id="bd066-326">Вы можете получить развернутой службы работоспособности пакета с помощью [запрос GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) или [запрос POST](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) , включающего политики работоспособности, описанные в теле hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-326">You can get deployed service package health with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) that includes health policies described in hello body.</span></span>

## <a name="health-chunk-queries"></a><span data-ttu-id="bd066-327">Запросы фрагментов данных о работоспособности</span><span class="sxs-lookup"><span data-stu-id="bd066-327">Health chunk queries</span></span>
<span data-ttu-id="bd066-328">Hello работоспособности блока запросы могут возвращать детей многоуровневого кластера (рекурсивно) в фильтры входа.</span><span class="sxs-lookup"><span data-stu-id="bd066-328">hello health chunk queries can return multi-level cluster children (recursively), per input filters.</span></span> <span data-ttu-id="bd066-329">Он поддерживает расширенные фильтры, позволяющие большую гибкость в выборе дочерние элементы hello toobe возвращается.</span><span class="sxs-lookup"><span data-stu-id="bd066-329">It supports advanced filters that allow a lot of flexibility in choosing hello children toobe returned.</span></span> <span data-ttu-id="bd066-330">Hello фильтры могут определять дочерние элементы, с уникальным идентификатором hello или другие идентификаторы группы или состояния работоспособности.</span><span class="sxs-lookup"><span data-stu-id="bd066-330">hello filters can specify children by hello unique identifier or by other group identifiers and/or health states.</span></span> <span data-ttu-id="bd066-331">По умолчанию дочерние элементы не включаются, в противоположность toohealth команды, которые всегда содержит дочерние элементы первого уровня.</span><span class="sxs-lookup"><span data-stu-id="bd066-331">By default, no children are included, as opposed toohealth commands that always include first-level children.</span></span>

<span data-ttu-id="bd066-332">Hello [запросов о работоспособности](service-fabric-view-entities-aggregated-health.md#health-queries) возврата только первого уровня дочерних элементов hello указанного лица необходимые фильтры.</span><span class="sxs-lookup"><span data-stu-id="bd066-332">hello [health queries](service-fabric-view-entities-aggregated-health.md#health-queries) return only first-level children of hello specified entity per required filters.</span></span> <span data-ttu-id="bd066-333">tooget hello дочерние элементы дочерних элементов hello, необходимо вызвать дополнительные работоспособности API-интерфейсов для каждой сущности, представляющие интерес.</span><span class="sxs-lookup"><span data-stu-id="bd066-333">tooget hello children of hello children, you must call additional health APIs for each entity of interest.</span></span> <span data-ttu-id="bd066-334">Аналогичным образом tooget hello работоспособности определенных сущностей, необходимо вызвать один работоспособности API для каждого нужного объекта.</span><span class="sxs-lookup"><span data-stu-id="bd066-334">Similarly, tooget hello health of specific entities, you must call one health API for each desired entity.</span></span> <span data-ttu-id="bd066-335">Hello Расширенная фильтрация запросов блоков позволяет toorequest несколько элементов в один запрос, сводя к минимуму размер сообщения hello и hello количество сообщений.</span><span class="sxs-lookup"><span data-stu-id="bd066-335">hello chunk query advanced filtering allows you toorequest multiple items of interest in one query, minimizing hello message size and hello number of messages.</span></span>

<span data-ttu-id="bd066-336">Hello hello фрагмент запроса значение можно получить состояние работоспособности для нескольких сущностей кластера (потенциально всех кластеров сущности начиная обязательный корневой) в одном вызове.</span><span class="sxs-lookup"><span data-stu-id="bd066-336">hello value of hello chunk query is that you can get health state for more cluster entities (potentially all cluster entities starting at required root) in one call.</span></span> <span data-ttu-id="bd066-337">Например, можно составить сложный запрос на сведения о работоспособности.</span><span class="sxs-lookup"><span data-stu-id="bd066-337">You can express complex health query such as:</span></span>

* <span data-ttu-id="bd066-338">Возвращать только приложения с ошибками и включать для таких приложений все службы с предупреждением или ошибкой.</span><span class="sxs-lookup"><span data-stu-id="bd066-338">Return only applications in error, and for those applications include all services in warning or error.</span></span> <span data-ttu-id="bd066-339">Для возвращенных служб включать все разделы.</span><span class="sxs-lookup"><span data-stu-id="bd066-339">For returned services, include all partitions.</span></span>
* <span data-ttu-id="bd066-340">Возвращать только hello работоспособности четыре указанные по имени приложения.</span><span class="sxs-lookup"><span data-stu-id="bd066-340">Return only hello health of four applications, specified by their names.</span></span>
* <span data-ttu-id="bd066-341">Возвращать только hello работоспособности приложений типа нужное приложение.</span><span class="sxs-lookup"><span data-stu-id="bd066-341">Return only hello health of applications of a desired application type.</span></span>
* <span data-ttu-id="bd066-342">Возвращать все развернутые сущности на узле.</span><span class="sxs-lookup"><span data-stu-id="bd066-342">Return all deployed entities on a node.</span></span> <span data-ttu-id="bd066-343">Возвращает все приложения все развернутые на указанном узле hello и все пакеты обновления hello развернуты на этом узле.</span><span class="sxs-lookup"><span data-stu-id="bd066-343">Returns all applications, all deployed applications on hello specified node and all hello deployed service packages on that node.</span></span>
* <span data-ttu-id="bd066-344">Возвращать все реплики с ошибками.</span><span class="sxs-lookup"><span data-stu-id="bd066-344">Return all replicas in error.</span></span> <span data-ttu-id="bd066-345">Возвращает все приложения, службы, разделы и только реплики с ошибками.</span><span class="sxs-lookup"><span data-stu-id="bd066-345">Returns all applications, services, partitions, and only replicas in error.</span></span>
* <span data-ttu-id="bd066-346">Возвращать все приложения.</span><span class="sxs-lookup"><span data-stu-id="bd066-346">Return all applications.</span></span> <span data-ttu-id="bd066-347">Включить все разделы для указанной службы.</span><span class="sxs-lookup"><span data-stu-id="bd066-347">For a specified service, include all partitions.</span></span>

<span data-ttu-id="bd066-348">В настоящее время hello работоспособности фрагмент запроса предоставляется только для hello объекта кластера.</span><span class="sxs-lookup"><span data-stu-id="bd066-348">Currently, hello health chunk query is exposed only for hello cluster entity.</span></span> <span data-ttu-id="bd066-349">Этот запрос возвращает фрагмент данных о работоспособности кластера, который содержит:</span><span class="sxs-lookup"><span data-stu-id="bd066-349">It returns a cluster health chunk, which contains:</span></span>

* <span data-ttu-id="bd066-350">состояние работоспособности кластера суммарный Hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-350">hello cluster aggregated health state.</span></span>
* <span data-ttu-id="bd066-351">Hello работоспособности состояние фрагмента список узлов, которые учитывают фильтры входа.</span><span class="sxs-lookup"><span data-stu-id="bd066-351">hello health state chunk list of nodes that respect input filters.</span></span>
* <span data-ttu-id="bd066-352">Hello работоспособности состояние фрагмента список приложений, которые учитывают фильтры входа.</span><span class="sxs-lookup"><span data-stu-id="bd066-352">hello health state chunk list of applications that respect input filters.</span></span> <span data-ttu-id="bd066-353">Каждый блок состояния работоспособности приложения содержит список блоков со всеми службами, которые используют фильтры входа и список блоков со всех развернутых приложений, которые учитывают hello фильтры.</span><span class="sxs-lookup"><span data-stu-id="bd066-353">Each application health state chunk contains a chunk list with all services that respect input filters and a chunk list with all deployed applications that respect hello filters.</span></span> <span data-ttu-id="bd066-354">То же для детей hello служб и развернутых приложений.</span><span class="sxs-lookup"><span data-stu-id="bd066-354">Same for hello children of services and deployed applications.</span></span> <span data-ttu-id="bd066-355">Таким образом, все сущности в кластере hello могут потенциально возвращаться при запросе в иерархическом виде.</span><span class="sxs-lookup"><span data-stu-id="bd066-355">This way, all entities in hello cluster can be potentially returned if requested, in a hierarchical fashion.</span></span>

### <a name="cluster-health-chunk-query"></a><span data-ttu-id="bd066-356">Запрос фрагмента данных о работоспособности кластера</span><span class="sxs-lookup"><span data-stu-id="bd066-356">Cluster health chunk query</span></span>
<span data-ttu-id="bd066-357">Возвращает hello работоспособности hello объекта кластера и содержит блоки состояние работоспособности иерархических hello необходимые дочерние элементы.</span><span class="sxs-lookup"><span data-stu-id="bd066-357">Returns hello health of hello cluster entity and contains hello hierarchical health state chunks of required children.</span></span> <span data-ttu-id="bd066-358">Входные данные:</span><span class="sxs-lookup"><span data-stu-id="bd066-358">Input:</span></span>

* <span data-ttu-id="bd066-359">[Необязательно] hello политика работоспособности кластера используется tooevaluate hello узлов и события кластера hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-359">[Optional] hello cluster health policy used tooevaluate hello nodes and hello cluster events.</span></span>
* <span data-ttu-id="bd066-360">[Необязательно] hello сопоставления политики работоспособности приложения, с помощью политик работоспособности hello использовать политики манифеста приложения hello toooverride.</span><span class="sxs-lookup"><span data-stu-id="bd066-360">[Optional] hello application health policy map, with hello health policies used toooverride hello application manifest policies.</span></span>
* <span data-ttu-id="bd066-361">[Необязательно] Фильтры для узлов и приложений, которые указывают, какие операции представляют интерес и должны возвращаться в результате hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-361">[Optional] Filters for nodes and applications that specify which entries are of interest and should be returned in hello result.</span></span> <span data-ttu-id="bd066-362">фильтры Hello являются tooan определенной сущности или группу сущностей или применимо tooall сущности на этом уровне.</span><span class="sxs-lookup"><span data-stu-id="bd066-362">hello filters are specific tooan entity/group of entities or are applicable tooall entities at that level.</span></span> <span data-ttu-id="bd066-363">Hello список фильтров может содержать один общие фильтра или фильтры для сущностей особые идентификаторы toofine фрагментов данных, возвращаемых запросом hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-363">hello list of filters can contain one general filter and/or filters for specific identifiers toofine-grain entities returned by hello query.</span></span> <span data-ttu-id="bd066-364">Если не указано, по умолчанию hello дочерние элементы не возвращаются.</span><span class="sxs-lookup"><span data-stu-id="bd066-364">If empty, hello children are not returned by default.</span></span>
  <span data-ttu-id="bd066-365">Дополнительные сведения о фильтры hello [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) и [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span><span class="sxs-lookup"><span data-stu-id="bd066-365">Read more about hello filters at [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) and [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter).</span></span> <span data-ttu-id="bd066-366">Hello приложения фильтров может рекурсивно укажите расширенные фильтры для дочерних элементов.</span><span class="sxs-lookup"><span data-stu-id="bd066-366">hello application filters can recursively specify advanced filters for children.</span></span>

<span data-ttu-id="bd066-367">результат Hello фрагмента данных включает в себя hello дочерних элементов, которые учитывают hello фильтры.</span><span class="sxs-lookup"><span data-stu-id="bd066-367">hello chunk result includes hello children that respect hello filters.</span></span>

<span data-ttu-id="bd066-368">В настоящее время hello фрагмента данных запрос возвращает оценки неисправностей или события объектов.</span><span class="sxs-lookup"><span data-stu-id="bd066-368">Currently, hello chunk query does not return unhealthy evaluations or entity events.</span></span> <span data-ttu-id="bd066-369">Эти дополнительные сведения можно получить с помощью hello существующего запроса работоспособности кластера.</span><span class="sxs-lookup"><span data-stu-id="bd066-369">That extra information can be obtained using hello existing cluster health query.</span></span>

### <a name="api"></a><span data-ttu-id="bd066-370">API</span><span class="sxs-lookup"><span data-stu-id="bd066-370">API</span></span>
<span data-ttu-id="bd066-371">работоспособность кластера tooget фрагмента данных, создайте `FabricClient` и вызова hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) метод для его **HealthManager**.</span><span class="sxs-lookup"><span data-stu-id="bd066-371">tooget cluster health chunk, create a `FabricClient` and call hello [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) method on its **HealthManager**.</span></span> <span data-ttu-id="bd066-372">Можно передать в [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe политики работоспособности и дополнительные фильтры.</span><span class="sxs-lookup"><span data-stu-id="bd066-372">You can pass in [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe health policies and advanced filters.</span></span>

<span data-ttu-id="bd066-373">Hello следующий код возвращает фрагмент работоспособности кластера с расширенными фильтрами.</span><span class="sxs-lookup"><span data-stu-id="bd066-373">hello following code gets cluster health chunk with advanced filters.</span></span>

```csharp
var queryDescription = new ClusterHealthChunkQueryDescription();
queryDescription.ApplicationFilters.Add(new ApplicationHealthStateFilter()
    {
        // Return applications only if they are in error
        HealthStateFilter = HealthStateFilter.Error
    });

// Return all replicas
var wordCountServiceReplicaFilter = new ReplicaHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };

// Return all replicas and all partitions
var wordCountServicePartitionFilter = new PartitionHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };
wordCountServicePartitionFilter.ReplicaFilters.Add(wordCountServiceReplicaFilter);

// For specific service, return all partitions and all replicas
var wordCountServiceFilter = new ServiceHealthStateFilter()
{
    ServiceNameFilter = new Uri("fabric:/WordCount/WordCountService"),
};
wordCountServiceFilter.PartitionFilters.Add(wordCountServicePartitionFilter);

// Application filter: for specific application, return no services except hello ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a><span data-ttu-id="bd066-374">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bd066-374">PowerShell</span></span>
<span data-ttu-id="bd066-375">командлет tooget Hello hello-состояние кластера — [Get ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span><span class="sxs-lookup"><span data-stu-id="bd066-375">hello cmdlet tooget hello cluster health is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk).</span></span> <span data-ttu-id="bd066-376">Сначала подключите toohello кластера с помощью hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) командлета.</span><span class="sxs-lookup"><span data-stu-id="bd066-376">First, connect toohello cluster by using hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.</span></span>

<span data-ttu-id="bd066-377">Hello следующий код возвращает узлы только в том случае, если они вызывают ошибки, за исключением конкретный узел, всегда должны быть возвращены.</span><span class="sxs-lookup"><span data-stu-id="bd066-377">hello following code gets nodes only if they are in Error except for a specific node, which should always be returned.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in hello cmdlet
$nodeFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.NodeHealthStateFilter]
$nodeFilters.Add($nodeFilter1)
$nodeFilters.Add($nodeFilter2)

Get-ServiceFabricClusterHealthChunk -NodeFilters $nodeFilters


HealthState                  : Warning
NodeHealthStateChunks        : 
                               TotalCount            : 1
                               
                               NodeName              : _Node_1
                               HealthState           : Ok
                               
ApplicationHealthStateChunks : None
```

<span data-ttu-id="bd066-378">Привет, выполнив командлет возвращает фрагмент кластера с фильтрами приложения.</span><span class="sxs-lookup"><span data-stu-id="bd066-378">hello following cmdlet gets cluster chunk with application filters.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

# All replicas
$replicaFilter = New-Object System.Fabric.Health.ReplicaHealthStateFilter -Property @{HealthStateFilter=$allFilter}

# All partitions
$partitionFilter = New-Object System.Fabric.Health.PartitionHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$partitionFilter.ReplicaFilters.Add($replicaFilter)

# For WordCountService, return all partitions and all replicas
$svcFilter1 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{ServiceNameFilter="fabric:/WordCount/WordCountService"}
$svcFilter1.PartitionFilters.Add($partitionFilter)

$svcFilter2 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{HealthStateFilter=$errorFilter}

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{ApplicationNameFilter="fabric:/WordCount"}
$appFilter.ServiceFilters.Add($svcFilter1)
$appFilter.ServiceFilters.Add($svcFilter2)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)

Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 1
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               ServiceHealthStateChunks : 
                                TotalCount            : 1
                               
                                ServiceName           : fabric:/WordCount/WordCountService
                                HealthState           : Error
                                PartitionHealthStateChunks : 
                                    TotalCount            : 1
                               
                                    PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                                    HealthState           : Error
                                    ReplicaHealthStateChunks : 
                                        TotalCount            : 5
                               
                                        ReplicaOrInstanceId   : 131444422293118720
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293118721
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113678
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113679
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422260002646
                                        HealthState           : Error
```

<span data-ttu-id="bd066-379">Hello следующий командлет возвращает все развернутые сущности на узле.</span><span class="sxs-lookup"><span data-stu-id="bd066-379">hello following cmdlet returns all deployed entities on a node.</span></span>

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$dspFilter = New-Object System.Fabric.Health.DeployedServicePackageHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$daFilter =  New-Object System.Fabric.Health.DeployedApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter;NodeNameFilter="_Node_2"}
$daFilter.DeployedServicePackageFilters.Add($dspFilter)

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$appFilter.DeployedApplicationFilters.Add($daFilter)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)
Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 2
                               
                               ApplicationName       : fabric:/System
                               HealthState           : Ok
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : FAS
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
                               
                               
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : WordCountServicePkg
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
```

### <a name="rest"></a><span data-ttu-id="bd066-380">REST</span><span class="sxs-lookup"><span data-stu-id="bd066-380">REST</span></span>
<span data-ttu-id="bd066-381">Вы можете получить блок работоспособности кластера с [запрос GET](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) или [запрос POST](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) политики работоспособности, и расширенные фильтры, описанные в теле hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-381">You can get cluster health chunk with a [GET request](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) or a [POST request](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) that includes health policies and advanced filters described in hello body.</span></span>

## <a name="general-queries"></a><span data-ttu-id="bd066-382">Общие запросы</span><span class="sxs-lookup"><span data-stu-id="bd066-382">General queries</span></span>
<span data-ttu-id="bd066-383">Общие запросы возвращают перечень сущностей Service Fabric указанного типа.</span><span class="sxs-lookup"><span data-stu-id="bd066-383">General queries return a list of Service Fabric entities of a specified type.</span></span> <span data-ttu-id="bd066-384">Они доступны через hello API (посредством методов hello на **FabricClient.QueryManager**), командлеты PowerShell и REST.</span><span class="sxs-lookup"><span data-stu-id="bd066-384">They are exposed through hello API (via hello methods on **FabricClient.QueryManager**), PowerShell cmdlets, and REST.</span></span> <span data-ttu-id="bd066-385">Эти запросы состоят из вложенных запросов от нескольких компонентов.</span><span class="sxs-lookup"><span data-stu-id="bd066-385">These queries aggregate subqueries from multiple components.</span></span> <span data-ttu-id="bd066-386">Один из них — hello [базе данных health store](service-fabric-health-introduction.md#health-store), который заполняет hello суммарный состояние работоспособности для каждого результата запроса.</span><span class="sxs-lookup"><span data-stu-id="bd066-386">One of them is hello [health store](service-fabric-health-introduction.md#health-store), which populates hello aggregated health state for each query result.</span></span>  

> [!NOTE]
> <span data-ttu-id="bd066-387">Общие запросы возвращают состояние работоспособности hello суммарный hello объекта и не содержат данных о работоспособности широкие возможности.</span><span class="sxs-lookup"><span data-stu-id="bd066-387">General queries return hello aggregated health state of hello entity and do not contain rich health data.</span></span> <span data-ttu-id="bd066-388">Если объект не находится в работоспособном состоянии, можно обрабатывать с tooget запросов работоспособности все его данные работоспособности, включая события, дочерних состояний работоспособности и оценки неисправностей.</span><span class="sxs-lookup"><span data-stu-id="bd066-388">If an entity is not healthy, you can follow up with health queries tooget all its health information, including events, child health states, and unhealthy evaluations.</span></span>
>
>

<span data-ttu-id="bd066-389">Общие запросы возвращают состояние работоспособности неизвестно, для сущности, возможно, это хранилище работоспособности hello не имеет полные данные о сущности hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-389">If general queries return an unknown health state for an entity, it's possible that hello health store doesn't have complete data about hello entity.</span></span> <span data-ttu-id="bd066-390">Можно также в хранилище работоспособности toohello вложенный запрос не был успешно (например, произошла ошибка связи или базе данных health store hello подверглась регулированию).</span><span class="sxs-lookup"><span data-stu-id="bd066-390">It's also possible that a subquery toohello health store wasn't successful (for example, there was a communication error, or hello health store was throttled).</span></span> <span data-ttu-id="bd066-391">Дальнейшие с запросом работоспособности для hello сущности.</span><span class="sxs-lookup"><span data-stu-id="bd066-391">Follow up with a health query for hello entity.</span></span> <span data-ttu-id="bd066-392">Если вложенный запрос hello обнаружил временные ошибки, например неполадки с сетевым дальнейших запрос может завершиться успешно.</span><span class="sxs-lookup"><span data-stu-id="bd066-392">If hello subquery encountered transient errors, such as network issues, this follow-up query may succeed.</span></span> <span data-ttu-id="bd066-393">Он может также содержат дополнительные сведения из хранилища работоспособности hello о почему hello сущности не предоставляется.</span><span class="sxs-lookup"><span data-stu-id="bd066-393">It may also give you more details from hello health store about why hello entity is not exposed.</span></span>

<span data-ttu-id="bd066-394">Здравствуйте, запросы, содержащие **HealthState** для сущности являются:</span><span class="sxs-lookup"><span data-stu-id="bd066-394">hello queries that contain **HealthState** for entities are:</span></span>

* <span data-ttu-id="bd066-395">Список узлов: возвращает hello список узлов в кластере hello (разбиением на страницы).</span><span class="sxs-lookup"><span data-stu-id="bd066-395">Node list: Returns hello list nodes in hello cluster (paged).</span></span>
  * <span data-ttu-id="bd066-396">API — [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span><span class="sxs-lookup"><span data-stu-id="bd066-396">API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)</span></span>
  * <span data-ttu-id="bd066-397">PowerShell: Get-ServiceFabricNode.</span><span class="sxs-lookup"><span data-stu-id="bd066-397">PowerShell: Get-ServiceFabricNode</span></span>
* <span data-ttu-id="bd066-398">Список приложений: Возвращает список hello приложений в кластере hello (разбиением на страницы).</span><span class="sxs-lookup"><span data-stu-id="bd066-398">Application list: Returns hello list of applications in hello cluster (paged).</span></span>
  * <span data-ttu-id="bd066-399">API — [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="bd066-399">API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)</span></span>
  * <span data-ttu-id="bd066-400">PowerShell: Get-ServiceFabricApplication.</span><span class="sxs-lookup"><span data-stu-id="bd066-400">PowerShell: Get-ServiceFabricApplication</span></span>
* <span data-ttu-id="bd066-401">Список служб: hello возвращает список служб в приложении (разбиением на страницы).</span><span class="sxs-lookup"><span data-stu-id="bd066-401">Service list: Returns hello list of services in an application (paged).</span></span>
  * <span data-ttu-id="bd066-402">API — [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span><span class="sxs-lookup"><span data-stu-id="bd066-402">API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)</span></span>
  * <span data-ttu-id="bd066-403">PowerShell: Get-ServiceFabricService.</span><span class="sxs-lookup"><span data-stu-id="bd066-403">PowerShell: Get-ServiceFabricService</span></span>
* <span data-ttu-id="bd066-404">Список секций: Возвращает список hello секций в службе (разбиением на страницы).</span><span class="sxs-lookup"><span data-stu-id="bd066-404">Partition list: Returns hello list of partitions in a service (paged).</span></span>
  * <span data-ttu-id="bd066-405">API — [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span><span class="sxs-lookup"><span data-stu-id="bd066-405">API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)</span></span>
  * <span data-ttu-id="bd066-406">PowerShell: Get-ServiceFabricPartition.</span><span class="sxs-lookup"><span data-stu-id="bd066-406">PowerShell: Get-ServiceFabricPartition</span></span>
* <span data-ttu-id="bd066-407">Список реплик: Возвращает список hello реплик в секции (разбиением на страницы).</span><span class="sxs-lookup"><span data-stu-id="bd066-407">Replica list: Returns hello list of replicas in a partition (paged).</span></span>
  * <span data-ttu-id="bd066-408">API — [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span><span class="sxs-lookup"><span data-stu-id="bd066-408">API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)</span></span>
  * <span data-ttu-id="bd066-409">PowerShell: Get-ServiceFabricReplica.</span><span class="sxs-lookup"><span data-stu-id="bd066-409">PowerShell: Get-ServiceFabricReplica</span></span>
* <span data-ttu-id="bd066-410">Развернуть список приложений: hello возвращает список развернутых приложений на узле.</span><span class="sxs-lookup"><span data-stu-id="bd066-410">Deployed application list: Returns hello list of deployed applications on a node.</span></span>
  * <span data-ttu-id="bd066-411">API — [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span><span class="sxs-lookup"><span data-stu-id="bd066-411">API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)</span></span>
  * <span data-ttu-id="bd066-412">PowerShell: Get-ServiceFabricDeployedApplication.</span><span class="sxs-lookup"><span data-stu-id="bd066-412">PowerShell: Get-ServiceFabricDeployedApplication</span></span>
* <span data-ttu-id="bd066-413">Развернуть список пакетов службы: hello возвращает список пакетов служб в развернутом приложении.</span><span class="sxs-lookup"><span data-stu-id="bd066-413">Deployed service package list: Returns hello list of service packages in a deployed application.</span></span>
  * <span data-ttu-id="bd066-414">API — [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span><span class="sxs-lookup"><span data-stu-id="bd066-414">API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)</span></span>
  * <span data-ttu-id="bd066-415">PowerShell: Get-ServiceFabricDeployedApplication.</span><span class="sxs-lookup"><span data-stu-id="bd066-415">PowerShell: Get-ServiceFabricDeployedApplication</span></span>

> [!NOTE]
> <span data-ttu-id="bd066-416">Некоторые запросы hello возвращать результатов по страницам.</span><span class="sxs-lookup"><span data-stu-id="bd066-416">Some of hello queries return paged results.</span></span> <span data-ttu-id="bd066-417">Hello этих запросов, возвращается список, производный от [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span><span class="sxs-lookup"><span data-stu-id="bd066-417">hello return of these queries is a list derived from [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1).</span></span> <span data-ttu-id="bd066-418">Если сообщение hello результаты не соответствуют, возвращается только страница и ContinuationToken, отслеживает, когда перечисление было остановлено.</span><span class="sxs-lookup"><span data-stu-id="bd066-418">If hello results do not fit a message, only a page is returned and a ContinuationToken that tracks where enumeration stopped.</span></span> <span data-ttu-id="bd066-419">По-прежнему hello toocall же запроса и передачи в токен продолжения hello из hello предыдущих tooget Далее результаты запроса.</span><span class="sxs-lookup"><span data-stu-id="bd066-419">Continue toocall hello same query and pass in hello continuation token from hello previous query tooget next results.</span></span>
>
>

### <a name="examples"></a><span data-ttu-id="bd066-420">Примеры</span><span class="sxs-lookup"><span data-stu-id="bd066-420">Examples</span></span>
<span data-ttu-id="bd066-421">Hello следующий код возвращает hello неработоспособности приложения hello кластера:</span><span class="sxs-lookup"><span data-stu-id="bd066-421">hello following code gets hello unhealthy applications in hello cluster:</span></span>

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

<span data-ttu-id="bd066-422">Hello следующий командлет возвращает подробные сведения о приложении hello для структуры hello: / приложения WordCount.</span><span class="sxs-lookup"><span data-stu-id="bd066-422">hello following cmdlet gets hello application details for hello fabric:/WordCount application.</span></span> <span data-ttu-id="bd066-423">Обратите внимание, что состояние работоспособности — "Предупреждение".</span><span class="sxs-lookup"><span data-stu-id="bd066-423">Notice that health state is at warning.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplication -ApplicationName fabric:/WordCount

ApplicationName        : fabric:/WordCount
ApplicationTypeName    : WordCount
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Warning
ApplicationParameters  : { "WordCountWebService_InstanceCount" = "1";
                         "_WFDebugParams_" = "[{"ServiceManifestName":"WordCountWebServicePkg","CodePackageName":"Code","EntryPointType":"Main","Debug
                         ExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {74f7e5d5-71a9-47e2-a8cd-1878ec4734f1} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"},{"ServiceManifestName":"WordCountServicePkg","CodeP
                         ackageName":"Code","EntryPointType":"Main","DebugExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {2ab462e6-e0d1-4fda-a844-972f561fe751} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"}]" }
```

<span data-ttu-id="bd066-424">Hello следующий командлет возвращает hello службы с состоянием работоспособности ошибки:</span><span class="sxs-lookup"><span data-stu-id="bd066-424">hello following cmdlet gets hello services with a health state of error:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplication | Get-ServiceFabricService | where {$_.HealthState -eq "Error"}


ServiceName            : fabric:/WordCount/WordCountService
ServiceKind            : Stateful
ServiceTypeName        : WordCountServiceType
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
HasPersistedState      : True
ServiceStatus          : Active
HealthState            : Error
```

## <a name="cluster-and-application-upgrades"></a><span data-ttu-id="bd066-425">Обновление кластера и приложений</span><span class="sxs-lookup"><span data-stu-id="bd066-425">Cluster and application upgrades</span></span>
<span data-ttu-id="bd066-426">Во время обновления отслеживаемых hello кластера и приложения Service Fabric проверяет tooensure работоспособности, что все, что остается работоспособным.</span><span class="sxs-lookup"><span data-stu-id="bd066-426">During a monitored upgrade of hello cluster and application, Service Fabric checks health tooensure that everything remains healthy.</span></span> <span data-ttu-id="bd066-427">Если сущность неработоспособен, как вычисляется с помощью настроенными политиками работоспособности, hello обновление применяется следующее действие политики, предназначенные для обновления toodetermine hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-427">If an entity is unhealthy as evaluated by using configured health policies, hello upgrade applies upgrade-specific policies toodetermine hello next action.</span></span> <span data-ttu-id="bd066-428">Hello обновления может быть приостановлена tooallow взаимодействия с пользователем (например, исправления ошибок или изменении политик), или он может автоматически отката предыдущей версии хорошо toohello.</span><span class="sxs-lookup"><span data-stu-id="bd066-428">hello upgrade may be paused tooallow user interaction (such as fixing error conditions or changing policies), or it may automatically roll back toohello previous good version.</span></span>

<span data-ttu-id="bd066-429">Во время *кластера* обновления, вы можете получить состояние обновления кластера hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-429">During a *cluster* upgrade, you can get hello cluster upgrade status.</span></span> <span data-ttu-id="bd066-430">Состояние обновления Hello включает оценки неисправностей, в какой точке toowhat находится в неисправном состоянии, в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-430">hello upgrade status includes unhealthy evaluations, which point toowhat is unhealthy in hello cluster.</span></span> <span data-ttu-id="bd066-431">Если hello обновление выполняется откат из-за проблем с toohealth, состояние обновления hello запоминает последние неработоспособное причин hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-431">If hello upgrade is rolled back due toohealth issues, hello upgrade status remembers hello last unhealthy reasons.</span></span> <span data-ttu-id="bd066-432">Эти сведения могут помочь администраторам определить, что пошло не так, после обновления hello откат или прекращения.</span><span class="sxs-lookup"><span data-stu-id="bd066-432">This information can help administrators investigate what went wrong after hello upgrade rolled back or stopped.</span></span>

<span data-ttu-id="bd066-433">Аналогичным образом, во время *приложения* обновления, оценки неисправностей в любой находятся в состоянии обновления приложения hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-433">Similarly, during an *application* upgrade, any unhealthy evaluations are contained in hello application upgrade status.</span></span>

<span data-ttu-id="bd066-434">Hello Далее показано состояние обновления приложения hello для изменения структуры: / приложения WordCount.</span><span class="sxs-lookup"><span data-stu-id="bd066-434">hello following shows hello application upgrade status for a modified fabric:/WordCount application.</span></span> <span data-ttu-id="bd066-435">Устройство наблюдения сообщило об ошибке на одной из реплик.</span><span class="sxs-lookup"><span data-stu-id="bd066-435">A watchdog reported an error on one of its replicas.</span></span> <span data-ttu-id="bd066-436">Обновление Hello в настоящее время переходит назад, так как не накладывается ограничение на проверку работоспособности hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-436">hello upgrade is rolling back because hello health checks are not respected.</span></span>

```powershell
PS C:\> Get-ServiceFabricApplicationUpgrade fabric:/WordCount

ApplicationName               : fabric:/WordCount
ApplicationTypeName           : WordCount
TargetApplicationTypeVersion  : 1.0.0.0
ApplicationParameters         : {}
StartTimestampUtc             : 4/21/2017 5:23:26 PM
FailureTimestampUtc           : 4/21/2017 5:23:37 PM
FailureReason                 : HealthCheck
UpgradeState                  : RollingBackInProgress
UpgradeDuration               : 00:00:23
CurrentUpgradeDomainDuration  : 00:00:00
CurrentUpgradeDomainProgress  : UD1

                                NodeName            : _Node_1
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_2
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_3
                                UpgradePhase        : PreUpgradeSafetyCheck
                                PendingSafetyChecks :
                                EnsurePartitionQuorum - PartitionId: 30db5be6-4e20-4698-8185-4bd7ca744020
NextUpgradeDomain             : UD2
UpgradeDomainsStatus          : { "UD1" = "Completed";
                                "UD2" = "Pending";
                                "UD3" = "Pending";
                                "UD4" = "Pending" }
UnhealthyEvaluations          :
                                Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.

                                      Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                      Unhealthy partition: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b', AggregatedHealthState='Error'.

                                          Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.

                                          Unhealthy replica: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b',
                                  ReplicaOrInstanceId='131031502346844058', AggregatedHealthState='Error'.

                                              Error event: SourceId='DiskWatcher', Property='Disk'.

UpgradeKind                   : Rolling
RollingUpgradeMode            : UnmonitoredAuto
ForceRestart                  : False
UpgradeReplicaSetCheckTimeout : 00:15:00
```

<span data-ttu-id="bd066-437">Дополнительные сведения о hello [обновление приложения Service Fabric](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="bd066-437">Read more about hello [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="use-health-evaluations-tootroubleshoot"></a><span data-ttu-id="bd066-438">Использовать tootroubleshoot аттестации работоспособности</span><span class="sxs-lookup"><span data-stu-id="bd066-438">Use health evaluations tootroubleshoot</span></span>
<span data-ttu-id="bd066-439">При наличии проблемы с hello кластеров или приложение, взгляните на toopinpoint работоспособности кластера или приложение hello проблема.</span><span class="sxs-lookup"><span data-stu-id="bd066-439">Whenever there is an issue with hello cluster or an application, look at hello cluster or application health toopinpoint what is wrong.</span></span> <span data-ttu-id="bd066-440">оценки неисправностей Hello содержат сведения о какой триггеру hello текущего неработоспособное состояние.</span><span class="sxs-lookup"><span data-stu-id="bd066-440">hello unhealthy evaluations provide details about what triggered hello current unhealthy state.</span></span> <span data-ttu-id="bd066-441">Если необходимо, можно выполнить детализацию в неработоспособные дочерние объекты tooidentify hello основную причину.</span><span class="sxs-lookup"><span data-stu-id="bd066-441">If you need to, you can drill down into unhealthy child entities tooidentify hello root cause.</span></span>

<span data-ttu-id="bd066-442">Например предположим, что приложение неработоспособно, так как поступил отчет об ошибке в одной из ее реплик.</span><span class="sxs-lookup"><span data-stu-id="bd066-442">For example, consider an application unhealthy because there is an error report on one of its replicas.</span></span> <span data-ttu-id="bd066-443">Hello следующий командлет Powershell показано оценки неисправностей hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-443">hello following Powershell cmdlet shows hello unhealthy evaluations:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount -EventsFilter None -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.
                                  
                                        Unhealthy replica: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', ReplicaOrInstanceId='131444422260002646', AggregatedHealthState='Error'.
                                  
                                            Error event: SourceId='MyWatchdog', Property='Memory'.
                                  
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

<span data-ttu-id="bd066-444">Tooget hello реплики можно просмотреть дополнительные сведения:</span><span class="sxs-lookup"><span data-stu-id="bd066-444">You can look at hello replica tooget more information:</span></span>

```powershell
PS D:\ServiceFabric> Get-ServiceFabricReplicaHealth -ReplicaOrInstanceId 131444422260002646 -PartitionId af2e3e44-a8f8-45ac-9f31-4093eb897600


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Error
UnhealthyEvaluations  : 
                        Error event: SourceId='MyWatchdog', Property='Memory'.
                        
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
                        SourceId              : MyWatchdog
                        Property              : Memory
                        HealthState           : Error
                        SequenceNumber        : 131444451657749403
                        SentAt                : 7/13/2017 6:46:05 PM
                        ReceivedAt            : 7/13/2017 6:46:05 PM
                        TTL                   : Infinite
                        Description           : 
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 7/13/2017 6:46:05 PM, LastOk = 1/1/0001 12:00:00 AM
```

> [!NOTE]
> <span data-ttu-id="bd066-445">Hello оценки неисправностей Показать hello первый причина, по которой hello сущность является оценка toocurrent состояние работоспособности.</span><span class="sxs-lookup"><span data-stu-id="bd066-445">hello unhealthy evaluations show hello first reason hello entity is evaluated toocurrent health state.</span></span> <span data-ttu-id="bd066-446">Может быть несколько событий, которые вызывают это состояние, но они, не отражаются в hello оценок.</span><span class="sxs-lookup"><span data-stu-id="bd066-446">There may be multiple other events that trigger this state, but they are not be reflected in hello evaluations.</span></span> <span data-ttu-id="bd066-447">tooget Дополнительные сведения, детализации углублением в toofigure сущностей работоспособности hello out все отчеты неработоспособное hello в кластере hello.</span><span class="sxs-lookup"><span data-stu-id="bd066-447">tooget more information, drill down into hello health entities toofigure out all hello unhealthy reports in hello cluster.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="bd066-448">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bd066-448">Next steps</span></span>
[<span data-ttu-id="bd066-449">Использовать tootroubleshoot отчеты о работоспособности системы</span><span class="sxs-lookup"><span data-stu-id="bd066-449">Use system health reports tootroubleshoot</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[<span data-ttu-id="bd066-450">Добавление настраиваемых отчетов о работоспособности Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bd066-450">Add custom Service Fabric health reports</span></span>](service-fabric-report-health.md)

[<span data-ttu-id="bd066-451">Как tooreport и проверки службы работоспособности</span><span class="sxs-lookup"><span data-stu-id="bd066-451">How tooreport and check service health</span></span>](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[<span data-ttu-id="bd066-452">Мониторинг и диагностика состояния служб в локальной среде разработки</span><span class="sxs-lookup"><span data-stu-id="bd066-452">Monitor and diagnose services locally</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[<span data-ttu-id="bd066-453">Обновление приложения Service Fabric</span><span class="sxs-lookup"><span data-stu-id="bd066-453">Service Fabric application upgrade</span></span>](service-fabric-application-upgrade.md)
