---
title: "aaaService диспетчер ресурсов кластера структуры - политики размещения | Документы Microsoft"
description: "Общие сведения о дополнительных политиках размещения и правилах для служб Service Fabric"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 5c2d19c6-dd40-4c4b-abd3-5c5ec0abed38
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: bb58642520085ab3000f3929cf9aea7a8f6e3070
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="placement-policies-for-service-fabric-services"></a><span data-ttu-id="7aee6-103">Политики размещения для служб Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7aee6-103">Placement policies for service fabric services</span></span>
<span data-ttu-id="7aee6-104">Политики размещения, дополнительные правила, которые могут быть используется toogovern размещение службы в некоторых конкретных, менее типичных сценариях.</span><span class="sxs-lookup"><span data-stu-id="7aee6-104">Placement policies are additional rules that can be used toogovern service placement in some specific, less-common scenarios.</span></span> <span data-ttu-id="7aee6-105">Вот несколько примеров.</span><span class="sxs-lookup"><span data-stu-id="7aee6-105">Some examples of those scenarios are:</span></span>

- <span data-ttu-id="7aee6-106">Кластер Service Fabric охватывает значительные географические расстояния. Например, он распределен между несколькими локальными центрами обработки данных или регионами Azure.</span><span class="sxs-lookup"><span data-stu-id="7aee6-106">Your Service Fabric cluster spans geographic distances, such as multiple on-premises datacenters or across Azure regions</span></span>
- <span data-ttu-id="7aee6-107">Среде охватывает несколько областей геополитические или юридическое элемента управления, или в другой ситуации при наличии границы политики необходимо tooenforce</span><span class="sxs-lookup"><span data-stu-id="7aee6-107">Your environment spans multiple areas of geopolitical or legal control, or some other case where you have policy boundaries you need tooenforce</span></span>
- <span data-ttu-id="7aee6-108">Существуют рекомендации производительность и задержка связи из-за toolarge расстояния или использование медленнее или менее надежной связи.</span><span class="sxs-lookup"><span data-stu-id="7aee6-108">There are communication performance or latency considerations due toolarge distances or use of slower or less reliable network links</span></span>
- <span data-ttu-id="7aee6-109">Требуется tookeep уверенности, что совместного размещения рабочих нагрузок, как максимум усилий с другими рабочими нагрузками или в toocustomers выражение с учетом расположения</span><span class="sxs-lookup"><span data-stu-id="7aee6-109">You need tookeep certain workloads collocated as a best effort, either with other workloads or in proximity toocustomers</span></span>

<span data-ttu-id="7aee6-110">Большинство этих требований выравнивание с физическим размещением hello кластера hello, представленные hello домены сбоя кластера hello.</span><span class="sxs-lookup"><span data-stu-id="7aee6-110">Most of these requirements align with hello physical layout of hello cluster, represented as hello fault domains of hello cluster.</span></span> 

<span data-ttu-id="7aee6-111">Hello Углубленное изучение политик, которые позволяют адрес к таким сценариям относятся:</span><span class="sxs-lookup"><span data-stu-id="7aee6-111">hello advanced placement policies that help address these scenarios are:</span></span>

1. <span data-ttu-id="7aee6-112">с недопустимыми доменами;</span><span class="sxs-lookup"><span data-stu-id="7aee6-112">Invalid domains</span></span>
2. <span data-ttu-id="7aee6-113">с обязательными доменами;</span><span class="sxs-lookup"><span data-stu-id="7aee6-113">Required domains</span></span>
3. <span data-ttu-id="7aee6-114">с предпочтительными доменами;</span><span class="sxs-lookup"><span data-stu-id="7aee6-114">Preferred domains</span></span>
4. <span data-ttu-id="7aee6-115">при запрете упаковки реплик.</span><span class="sxs-lookup"><span data-stu-id="7aee6-115">Disallowing replica packing</span></span>

<span data-ttu-id="7aee6-116">Большинство hello следующие элементы управления могут настраиваться с помощью свойства узла и ограничения размещения, но некоторые являются более сложным.</span><span class="sxs-lookup"><span data-stu-id="7aee6-116">Most of hello following controls could be configured via node properties and placement constraints, but some are more complicated.</span></span> <span data-ttu-id="7aee6-117">toomake предметах проще hello диспетчер ресурсов кластера Service Fabric предоставляет эти дополнительные размещения политики.</span><span class="sxs-lookup"><span data-stu-id="7aee6-117">toomake things simpler, hello Service Fabric Cluster Resource Manager provides these additional placement policies.</span></span> <span data-ttu-id="7aee6-118">Политики размещения настаиваются для отдельных экземпляров именованных служб.</span><span class="sxs-lookup"><span data-stu-id="7aee6-118">Placement policies are configured on a per-named service instance basis.</span></span> <span data-ttu-id="7aee6-119">Они могут также обновляться динамически.</span><span class="sxs-lookup"><span data-stu-id="7aee6-119">They can also be updated dynamically.</span></span>

## <a name="specifying-invalid-domains"></a><span data-ttu-id="7aee6-120">Указание недопустимых доменов</span><span class="sxs-lookup"><span data-stu-id="7aee6-120">Specifying invalid domains</span></span>
<span data-ttu-id="7aee6-121">Hello **InvalidDomain** политика размещения позволяет toospecify недоступность определенного домена сбоя для конкретной службы.</span><span class="sxs-lookup"><span data-stu-id="7aee6-121">hello **InvalidDomain** placement policy allows you toospecify that a particular Fault Domain is invalid for a specific service.</span></span> <span data-ttu-id="7aee6-122">Эта политика предотвращает выполнение определенной службы в определенном регионе, что может быть связано с геополитическими причинами или корпоративной политикой организации.</span><span class="sxs-lookup"><span data-stu-id="7aee6-122">This policy ensures that a particular service never runs in a particular area, for example for geopolitical or corporate policy reasons.</span></span> <span data-ttu-id="7aee6-123">Используя отдельные политики, можно указать несколько недопустимых доменов.</span><span class="sxs-lookup"><span data-stu-id="7aee6-123">Multiple invalid domains may be specified via separate policies.</span></span>

<span data-ttu-id="7aee6-124"><center>
![Пример недопустимого домена][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="7aee6-124"><center>
![Invalid Domain Example][Image1]
</center></span></span>

<span data-ttu-id="7aee6-125">Код:</span><span class="sxs-lookup"><span data-stu-id="7aee6-125">Code:</span></span>

```csharp
ServicePlacementInvalidDomainPolicyDescription invalidDomain = new ServicePlacementInvalidDomainPolicyDescription();
invalidDomain.DomainName = "fd:/DCEast"; //regulations prohibit this workload here
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="7aee6-126">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7aee6-126">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("InvalidDomain,fd:/DCEast”)
```
## <a name="specifying-required-domains"></a><span data-ttu-id="7aee6-127">Указание обязательных доменов</span><span class="sxs-lookup"><span data-stu-id="7aee6-127">Specifying required domains</span></span>
<span data-ttu-id="7aee6-128">Размещение политика домена требует, что служба hello присутствует только в указанных доменах hello обязательные Hello.</span><span class="sxs-lookup"><span data-stu-id="7aee6-128">hello required domain placement policy requires that hello service is present only in hello specified domain.</span></span> <span data-ttu-id="7aee6-129">Используя отдельные политики, можно указать несколько обязательных доменов.</span><span class="sxs-lookup"><span data-stu-id="7aee6-129">Multiple required domains can be specified via separate policies.</span></span>

<span data-ttu-id="7aee6-130"><center>
![Пример обязательного домена][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="7aee6-130"><center>
![Required Domain Example][Image2]
</center></span></span>

<span data-ttu-id="7aee6-131">Код:</span><span class="sxs-lookup"><span data-stu-id="7aee6-131">Code:</span></span>

```csharp
ServicePlacementRequiredDomainPolicyDescription requiredDomain = new ServicePlacementRequiredDomainPolicyDescription();
requiredDomain.DomainName = "fd:/DC01/RK03/BL2";
serviceDescription.PlacementPolicies.Add(requiredDomain);
```

<span data-ttu-id="7aee6-132">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7aee6-132">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomain,fd:/DC01/RK03/BL2")
```

## <a name="specifying-a-preferred-domain-for-hello-primary-replicas-of-a-stateful-service"></a><span data-ttu-id="7aee6-133">Указание основной домен для hello основной реплики службы с отслеживанием состояния</span><span class="sxs-lookup"><span data-stu-id="7aee6-133">Specifying a preferred domain for hello primary replicas of a stateful service</span></span>
<span data-ttu-id="7aee6-134">Hello предпочитаемый основного домена указывает tooplace домена сбоя hello hello Primary in.</span><span class="sxs-lookup"><span data-stu-id="7aee6-134">hello Preferred Primary Domain specifies hello fault domain tooplace hello Primary in.</span></span> <span data-ttu-id="7aee6-135">Hello основной заканчивается в этом домене, когда все, что находится в работоспособном состоянии.</span><span class="sxs-lookup"><span data-stu-id="7aee6-135">hello Primary ends up in this domain when everything is healthy.</span></span> <span data-ttu-id="7aee6-136">Если домен hello или hello первичной реплики завершается ошибкой или завершает работу, hello основной перемещает toosome другое местоположение, в идеальном случае в hello того же домена.</span><span class="sxs-lookup"><span data-stu-id="7aee6-136">If hello domain or hello Primary replica fails or shuts down, hello Primary moves toosome other location, ideally in hello same domain.</span></span> <span data-ttu-id="7aee6-137">Если это новое местоположение не в домене предпочтительный hello, hello диспетчер ресурсов кластера переходит обратно предпочтительный домена toohello как можно быстрее.</span><span class="sxs-lookup"><span data-stu-id="7aee6-137">If this new location isn't in hello preferred domain, hello Cluster Resource Manager moves it back toohello preferred domain as soon as possible.</span></span> <span data-ttu-id="7aee6-138">Обычно этот параметр имеет смысл только для служб с отслеживанием состояния.</span><span class="sxs-lookup"><span data-stu-id="7aee6-138">Naturally this setting only makes sense for stateful services.</span></span> <span data-ttu-id="7aee6-139">Эту политику особенно полезно использовать в кластерах, которые охватывают несколько регионов Azure или центров обработки данных, но содержат службы, для которых предпочтительно размещение в определенном расположении.</span><span class="sxs-lookup"><span data-stu-id="7aee6-139">This policy is most useful in clusters that are spanned across Azure regions or multiple datacenters but have services that prefer placement in a certain location.</span></span> <span data-ttu-id="7aee6-140">Сохранение в источниках закройте tootheir пользователи или другие службы, который помогает обеспечивать более низкой задержке, особенно для операций чтения, которые обрабатываются первичные цвета по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7aee6-140">Keeping Primaries close tootheir users or other services helps provide lower latency, especially for reads, which are handled by Primaries by default.</span></span>

<span data-ttu-id="7aee6-141"><center>
![Предпочтительные домены для первичных реплик и отработка отказа][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="7aee6-141"><center>
![Preferred Primary Domains and Failover][Image3]
</center></span></span>

```csharp
ServicePlacementPreferPrimaryDomainPolicyDescription primaryDomain = new ServicePlacementPreferPrimaryDomainPolicyDescription();
primaryDomain.DomainName = "fd:/EastUS/";
serviceDescription.PlacementPolicies.Add(invalidDomain);
```

<span data-ttu-id="7aee6-142">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7aee6-142">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("PreferredPrimaryDomain,fd:/EastUS")
```

## <a name="requiring-replica-distribution-and-disallowing-packing"></a><span data-ttu-id="7aee6-143">Требование распределения реплик и запрещение группирования</span><span class="sxs-lookup"><span data-stu-id="7aee6-143">Requiring replica distribution and disallowing packing</span></span>
<span data-ttu-id="7aee6-144">Реплика — _обычно_ распределения в доменах сбоя и обновления при hello кластера находится в работоспособном состоянии.</span><span class="sxs-lookup"><span data-stu-id="7aee6-144">Replicas are _normally_ distributed across fault and upgrade domains when hello cluster is healthy.</span></span> <span data-ttu-id="7aee6-145">Тем не менее существуют ситуации, в которых более одной реплики для заданной секции может быть временно сгруппировано в одном домене.</span><span class="sxs-lookup"><span data-stu-id="7aee6-145">However, there are cases where more than one replica for a given partition may end up temporarily packed into a single domain.</span></span> <span data-ttu-id="7aee6-146">Например, предположим, что этот кластер hello имеет девять узлов в трех ошибочных доменах, fd: / 0, fd: / 1 и fd: / 2.</span><span class="sxs-lookup"><span data-stu-id="7aee6-146">For example, let's say that hello cluster has nine nodes in three fault domains, fd:/0, fd:/1, and fd:/2.</span></span> <span data-ttu-id="7aee6-147">Предположим, что у вашей службы три реплики.</span><span class="sxs-lookup"><span data-stu-id="7aee6-147">Let's also say that your service has three replicas.</span></span> <span data-ttu-id="7aee6-148">Предположим, что hello узлы, которые использовались для этих реплик в fd: / 1 и fd: / 2 вышел из строя.</span><span class="sxs-lookup"><span data-stu-id="7aee6-148">Let's say that hello nodes that were being used for those replicas in fd:/1 and fd:/2 went down.</span></span> <span data-ttu-id="7aee6-149">Обычно hello диспетчер ресурсов кластера хотите использовать другие узлы в тех же доменах сбоя.</span><span class="sxs-lookup"><span data-stu-id="7aee6-149">Normally hello Cluster Resource Manager would prefer other nodes in those same fault domains.</span></span> <span data-ttu-id="7aee6-150">В этом случае предположим, что из-за проблем с toocapacity none hello использовались другие узлы в этих доменах.</span><span class="sxs-lookup"><span data-stu-id="7aee6-150">In this case, let's say due toocapacity issues none of hello other nodes in those domains were valid.</span></span> <span data-ttu-id="7aee6-151">Если диспетчер ресурсов кластера hello построение выполнено замен для этих реплик, он будет иметь toochoose узла в fd: / 0.</span><span class="sxs-lookup"><span data-stu-id="7aee6-151">If hello Cluster Resource Manager builds replacements for those replicas, it would have toochoose nodes in fd:/0.</span></span> <span data-ttu-id="7aee6-152">Тем не менее, выполнив _,_ возникает ситуация, где нарушается ограничение домен сбоя hello.</span><span class="sxs-lookup"><span data-stu-id="7aee6-152">However, doing _that_ creates a situation where hello Fault Domain constraint is violated.</span></span> <span data-ttu-id="7aee6-153">Упаковки реплик увеличивается вероятность hello hello всей реплика может сократиться или будут утеряны.</span><span class="sxs-lookup"><span data-stu-id="7aee6-153">Packing replicas increases hello chance that hello whole replica set could go down or be lost.</span></span> 

> [!NOTE]
> <span data-ttu-id="7aee6-154">Дополнительные сведения об общих ограничениях и приоритетах ограничений см. в [этом разделе](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span><span class="sxs-lookup"><span data-stu-id="7aee6-154">For more information on constraints and constraint priorities generally, check out [this topic](service-fabric-cluster-resource-manager-management-integration.md#constraint-priorities).</span></span>
>

<span data-ttu-id="7aee6-155">Если вы увидели сообщение о работоспособности наподобие такого: `hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`, это значит, что у вас возникла описанная ошибка или сходная с ней.</span><span class="sxs-lookup"><span data-stu-id="7aee6-155">If you've ever seen a health message such as "`hello Load Balancer has detected a Constraint Violation for this Replica:fabric:/<some service name> Secondary Partition <some partition ID> is violating hello Constraint: FaultDomain`", then you've hit this condition or something like it.</span></span> <span data-ttu-id="7aee6-156">Обычно временно группируется только одна или две реплики.</span><span class="sxs-lookup"><span data-stu-id="7aee6-156">Usually only one or two replicas are packed together temporarily.</span></span> <span data-ttu-id="7aee6-157">Пока число реплик в заданном домене не превышает кворум, все в порядке.</span><span class="sxs-lookup"><span data-stu-id="7aee6-157">So long as there are fewer than a quorum of replicas in a given domain, you're safe.</span></span> <span data-ttu-id="7aee6-158">Упаковки редко, но это может случиться, и обычно такие ситуации являются временными, так как узлы hello вернуться.</span><span class="sxs-lookup"><span data-stu-id="7aee6-158">Packing is rare, but it can happen, and usually these situations are transient since hello nodes come back.</span></span> <span data-ttu-id="7aee6-159">Если узлы hello оставаться вниз и hello диспетчер ресурсов кластера должна toobuild замены, обычно существуют другие узлы в доменах сбоя идеальный hello.</span><span class="sxs-lookup"><span data-stu-id="7aee6-159">If hello nodes do stay down and hello Cluster Resource Manager needs toobuild replacements, usually there are other nodes available in hello ideal fault domains.</span></span>

<span data-ttu-id="7aee6-160">Для некоторых рабочих нагрузок предпочитаете всегда с числом hello целевой реплики, даже если они упакованы в небольшого числа доменов.</span><span class="sxs-lookup"><span data-stu-id="7aee6-160">Some workloads would prefer always having hello target number of replicas, even if they are packed into fewer domains.</span></span> <span data-ttu-id="7aee6-161">Такие рабочие нагрузки обеспечивают защиту от общего числа постоянных одновременных сбоев в домене, позволяя восстановить локальное состояние.</span><span class="sxs-lookup"><span data-stu-id="7aee6-161">These workloads are betting against total simultaneous permanent domain failures and can usually recover local state.</span></span> <span data-ttu-id="7aee6-162">Другие рабочие нагрузки вместо займет время простоя hello более ранних, чем правильность риска и потери данных.</span><span class="sxs-lookup"><span data-stu-id="7aee6-162">Other workloads would rather take hello downtime earlier than risk correctness or loss of data.</span></span> <span data-ttu-id="7aee6-163">Большинство производственных рабочих нагрузок работает больше чем с тремя репликами, больше чем с тремя доменами сбоя и множеством допустимых узлов в каждом домене сбоя.</span><span class="sxs-lookup"><span data-stu-id="7aee6-163">Most production workloads run with more than three replicas, more than three fault domains, and many valid nodes per fault domain.</span></span> <span data-ttu-id="7aee6-164">По этой причине поведение по умолчанию hello позволяет упаковки домена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7aee6-164">Because of this, hello default behavior allows domain packing by default.</span></span> <span data-ttu-id="7aee6-165">поведение по умолчанию Hello позволяет обычный балансировки и toohandle отработки отказа эти крайних случаях, даже если это означает упаковки временный домен.</span><span class="sxs-lookup"><span data-stu-id="7aee6-165">hello default behavior allows normal balancing and failover toohandle these extreme cases, even if that means temporary domain packing.</span></span>

<span data-ttu-id="7aee6-166">Если вы хотите toodisable такой способ упаковки для заданной рабочей нагрузки, можно указать hello `RequireDomainDistribution` политики службы hello.</span><span class="sxs-lookup"><span data-stu-id="7aee6-166">If you want toodisable such packing for a given workload, you can specify hello `RequireDomainDistribution` policy on hello service.</span></span> <span data-ttu-id="7aee6-167">Если этот параметр установлен, hello диспетчер ресурсов кластера гарантирует не две реплики из hello запуск одной секции в hello же ошибок или домен обновления.</span><span class="sxs-lookup"><span data-stu-id="7aee6-167">When this policy is set, hello Cluster Resource Manager ensures no two replicas from hello same partition run in hello same fault or upgrade domain.</span></span>

<span data-ttu-id="7aee6-168">Код:</span><span class="sxs-lookup"><span data-stu-id="7aee6-168">Code:</span></span>

```csharp
ServicePlacementRequireDomainDistributionPolicyDescription distributeDomain = new ServicePlacementRequireDomainDistributionPolicyDescription();
serviceDescription.PlacementPolicies.Add(distributeDomain);
```

<span data-ttu-id="7aee6-169">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7aee6-169">Powershell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -PlacementPolicy @("RequiredDomainDistribution")
```

<span data-ttu-id="7aee6-170">Теперь, было бы быть toouse возможных конфигураций службы в кластере, который не был географически охваченных?</span><span class="sxs-lookup"><span data-stu-id="7aee6-170">Now, would it be possible toouse these configurations for services in a cluster that was not geographically spanned?</span></span> <span data-ttu-id="7aee6-171">Можно, но не нужно.</span><span class="sxs-lookup"><span data-stu-id="7aee6-171">You could, but there’s not a great reason too.</span></span> <span data-ttu-id="7aee6-172">Hello конфигурации требуется, недопустимый и основного домена следует избегать, если hello сценарии требуют их.</span><span class="sxs-lookup"><span data-stu-id="7aee6-172">hello required, invalid, and preferred domain configurations should be avoided unless hello scenarios require them.</span></span> <span data-ttu-id="7aee6-173">Он не становится все tooforce tootry смысле toorun заданной рабочей нагрузки в одной стойке или tooprefer некоторых сегментов локального кластера на другой.</span><span class="sxs-lookup"><span data-stu-id="7aee6-173">It doesn't make any sense tootry tooforce a given workload toorun in a single rack, or tooprefer some segment of your local cluster over another.</span></span> <span data-ttu-id="7aee6-174">Разные аппаратные конфигурации следует распределить между доменами сбоя и обрабатывать с использованием обычных ограничений размещения и свойств узлов.</span><span class="sxs-lookup"><span data-stu-id="7aee6-174">Different hardware configurations should be spread across fault domains and handled via normal placement constraints and node properties.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7aee6-175">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7aee6-175">Next steps</span></span>
- <span data-ttu-id="7aee6-176">Дополнительные сведения о настройке служб см. в разделе [Настройка параметров Cluster Resource Manager для служб Service Fabric](service-fabric-cluster-resource-manager-configure-services.md).</span><span class="sxs-lookup"><span data-stu-id="7aee6-176">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-invalid-placement-domain.png
[Image2]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-required-placement-domain.png
[Image3]:./media/service-fabric-cluster-resource-manager-advanced-placement-rules-placement-policies/cluster-preferred-primary-domain.png
