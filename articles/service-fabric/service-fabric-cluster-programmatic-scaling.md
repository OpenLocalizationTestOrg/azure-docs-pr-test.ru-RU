---
title: "Масштабирование программный структуры службы aaaAzure | Документы Microsoft"
description: "Масштабировать кластер Azure Service Fabric in или out программными средствами, в соответствии с toocustom триггеров"
services: service-fabric
documentationcenter: .net
author: mjrousos
manager: jonjung
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: mikerou
ms.openlocfilehash: a0c6499b1a143a173006248cf8a15380632637e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a><span data-ttu-id="53e83-103">Программное масштабирование кластера Service Fabric</span><span class="sxs-lookup"><span data-stu-id="53e83-103">Scale a Service Fabric cluster programmatically</span></span> 

<span data-ttu-id="53e83-104">Основы масштабирования кластера Service Fabric в Azure рассматриваются в статье [Масштабирование кластера Service Fabric с помощью правил автомасштабирования](./service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="53e83-104">Fundamentals of scaling a Service Fabric cluster in Azure are covered in documentation on [cluster scaling](./service-fabric-cluster-scale-up-down.md).</span></span> <span data-ttu-id="53e83-105">В этой статье описано устройство кластеров Service Fabric, состоящих из масштабируемых наборов виртуальных машин. Масштабирование этих кластеров может выполняться вручную или с помощью правил автомасштабирования.</span><span class="sxs-lookup"><span data-stu-id="53e83-105">That article covers how Service Fabric clusters are built on top of virtual machine scale sets and can be scaled either manually or with auto-scale rules.</span></span> <span data-ttu-id="53e83-106">В текущем документе рассматриваются программные методы выполнения операций масштабирования Azure для более сложных сценариев.</span><span class="sxs-lookup"><span data-stu-id="53e83-106">This document looks at programmatic methods of coordinating Azure scaling operations for more advanced scenarios.</span></span> 

## <a name="reasons-for-programmatic-scaling"></a><span data-ttu-id="53e83-107">Причины для программного масштабирования</span><span class="sxs-lookup"><span data-stu-id="53e83-107">Reasons for programmatic scaling</span></span>
<span data-ttu-id="53e83-108">В большинстве сценариев масштабирование вручную или с помощью правил автомасштабирования — это оптимальное решение.</span><span class="sxs-lookup"><span data-stu-id="53e83-108">In many scenarios, scaling manually or via auto-scale rules are good solutions.</span></span> <span data-ttu-id="53e83-109">В других сценариях, они нельзя прямо размеру hello.</span><span class="sxs-lookup"><span data-stu-id="53e83-109">In other scenarios, though, they may not be hello right fit.</span></span> <span data-ttu-id="53e83-110">Потенциальные недостатки toothese подходы включают в себя:</span><span class="sxs-lookup"><span data-stu-id="53e83-110">Potential drawbacks toothese approaches include:</span></span>

- <span data-ttu-id="53e83-111">Масштабирование вручную требует toolog в явно запрос и масштабирования операций.</span><span class="sxs-lookup"><span data-stu-id="53e83-111">Manually scaling requires you toolog in and explicitly request scaling operations.</span></span> <span data-ttu-id="53e83-112">Если операции масштабирования нужно выполнять часто или в непредвиденные моменты, этот подход может оказаться не лучшим решением.</span><span class="sxs-lookup"><span data-stu-id="53e83-112">If scaling operations are required frequently or at unpredictable times, this approach may not be a good solution.</span></span>
- <span data-ttu-id="53e83-113">Если правил автоматического масштабирования удалить экземпляр из набора масштабирования виртуальных машин, они не удаляется автоматически знаний этого узла из кластера Service Fabric hello связанные Если тип узла hello имеет уровень устойчивости серебряные и золотые.</span><span class="sxs-lookup"><span data-stu-id="53e83-113">When auto-scale rules remove an instance from a virtual machine scale set, they do not automatically remove knowledge of that node from hello associated Service Fabric cluster unless hello node type has a durability level of Silver or Gold.</span></span> <span data-ttu-id="53e83-114">Поскольку правил автоматического масштабирования работают в масштабе hello, установите уровень (а не на уровне Service Fabric hello), правил автоматического масштабирования можно удалить узлы Service Fabric без верного завершения их работы.</span><span class="sxs-lookup"><span data-stu-id="53e83-114">Because auto-scale rules work at hello scale set level (rather than at hello Service Fabric level), auto-scale rules can remove Service Fabric nodes without shutting them down gracefully.</span></span> <span data-ttu-id="53e83-115">При таком грубом удалении узла остается фантомное состояние узла Service Fabric после операций уменьшения масштаба.</span><span class="sxs-lookup"><span data-stu-id="53e83-115">This rude node removal will leave 'ghost' Service Fabric node state behind after scale-in operations.</span></span> <span data-ttu-id="53e83-116">Лицо (или службы), должны tooperiodically очистки состояния удаленный узел в кластер Service Fabric hello.</span><span class="sxs-lookup"><span data-stu-id="53e83-116">An individual (or a service) would need tooperiodically clean up removed node state in hello Service Fabric cluster.</span></span>
  - <span data-ttu-id="53e83-117">Обратите внимание, что на узлах с уровнем устойчивости Gold или Silver удаленные узлы очищаются автоматически.</span><span class="sxs-lookup"><span data-stu-id="53e83-117">Note that a node type with a durability level of Gold or Silver will automatically clean up removed nodes.</span></span>  
- <span data-ttu-id="53e83-118">Правила автомасштабирования поддерживают [многие метрики](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md), но их число все еще ограниченно.</span><span class="sxs-lookup"><span data-stu-id="53e83-118">Although there are [many metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) supported by auto-scale rules, it is still a limited set.</span></span> <span data-ttu-id="53e83-119">Если в вашем сценарии требуется масштабирование на основе метрики, которой нет в этом наборе, правила автомасштабирования могут оказаться не самым подходящим вариантом.</span><span class="sxs-lookup"><span data-stu-id="53e83-119">If your scenario calls for scaling based on some metric not covered in that set, then auto-scale rules may not be a good option.</span></span>

<span data-ttu-id="53e83-120">На основании этих ограничений, вы можете tooimplement более пользовательские автоматического масштабирования модели.</span><span class="sxs-lookup"><span data-stu-id="53e83-120">Based on these limitations, you may wish tooimplement more customized automatic scaling models.</span></span> 

## <a name="scaling-apis"></a><span data-ttu-id="53e83-121">Масштабирование API-интерфейсов</span><span class="sxs-lookup"><span data-stu-id="53e83-121">Scaling APIs</span></span>
<span data-ttu-id="53e83-122">Существуют Azure интерфейсы API, которая разрешает tooprogrammatically работы приложений с кластера Service Fabric и наборы масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="53e83-122">Azure APIs exist which allow applications tooprogrammatically work with virtual machine scale sets and Service Fabric clusters.</span></span> <span data-ttu-id="53e83-123">Если существующие параметры автоматического масштабирования не работает для вашего сценария, эти API-интерфейсы позволяют возможных tooimplement пользовательской логики масштабирования.</span><span class="sxs-lookup"><span data-stu-id="53e83-123">If existing auto-scale options don't work for your scenario, these APIs make it possible tooimplement custom scaling logic.</span></span> 

<span data-ttu-id="53e83-124">Одним из подходов tooimplementing это «домашняя сделанное» автоматическое масштабирование функциональности является tooadd новый без отслеживания состояния службы toohello Service Fabric приложения toomanage масштабирования операций.</span><span class="sxs-lookup"><span data-stu-id="53e83-124">One approach tooimplementing this 'home-made' auto-scaling functionality is tooadd a new stateless service toohello Service Fabric application toomanage scaling operations.</span></span> <span data-ttu-id="53e83-125">В службе hello `RunAsync` метода набора триггеров можно определить необходимость масштабирования (включая проверки параметров, таких как максимальный размер кластера и масштабирование cooldowns).</span><span class="sxs-lookup"><span data-stu-id="53e83-125">Within hello service's `RunAsync` method, a set of triggers can determine if scaling is required (including checking parameters such as maximum cluster size and scaling cooldowns).</span></span>   

<span data-ttu-id="53e83-126">Hello API, используемый для взаимодействия на набор масштабирования виртуальной машины (оба toocheck hello текущее количество экземпляров виртуальных машин и toomodify его) — hello [fluent вычислений Azure управления библиотеки](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span><span class="sxs-lookup"><span data-stu-id="53e83-126">hello API used for virtual machine scale set interactions (both toocheck hello current number of virtual machine instances and toomodify it) is hello [fluent Azure Management Compute library](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span></span> <span data-ttu-id="53e83-127">Библиотека fluent вычислений Hello предоставляет простые в использовании API для взаимодействия с наборы масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="53e83-127">hello fluent compute library provides an easy-to-use API for interacting with virtual machine scale sets.</span></span>

<span data-ttu-id="53e83-128">использовать toointeract с кластером Service Fabric hello, [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="53e83-128">toointeract with hello Service Fabric cluster itself, use [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span></span>

<span data-ttu-id="53e83-129">Конечно, масштабирование кода hello не требует toorun как служба в масштабировании toobe кластера hello.</span><span class="sxs-lookup"><span data-stu-id="53e83-129">Of course, hello scaling code doesn't need toorun as a service in hello cluster toobe scaled.</span></span> <span data-ttu-id="53e83-130">Оба `IAzure` и `FabricClient` tootheir связанные ресурсы Azure удаленного подключения, поэтому hello масштабирование службы может легко консольное приложение или служба Windows запущена из приложения вне hello Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="53e83-130">Both `IAzure` and `FabricClient` can connect tootheir associated Azure resources remotely, so hello scaling service could easily be a console application or Windows service running from outside hello Service Fabric application.</span></span> 

## <a name="credential-management"></a><span data-ttu-id="53e83-131">Управление учетными данными</span><span class="sxs-lookup"><span data-stu-id="53e83-131">Credential management</span></span>
<span data-ttu-id="53e83-132">Одна из проблем написания масштабирование службы toohandle: hello службы должно иметь ресурсы набор масштабирования виртуальной машины может tooaccess без интерактивного входа в систему.</span><span class="sxs-lookup"><span data-stu-id="53e83-132">One challenge of writing a service toohandle scaling is that hello service must be able tooaccess virtual machine scale set resources without an interactive login.</span></span> <span data-ttu-id="53e83-133">Доступ к hello Service Fabric кластера очень просто изменяет собственное приложение Service Fabric hello масштабирование службы, но учетные данные, необходимые tooaccess hello набора масштабирования.</span><span class="sxs-lookup"><span data-stu-id="53e83-133">Accessing hello Service Fabric cluster is easy if hello scaling service is modifying its own Service Fabric application, but credentials are needed tooaccess hello scale set.</span></span> <span data-ttu-id="53e83-134">toolog в использовании [участника-службы](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) созданными hello [Azure CLI 2.0](https://github.com/azure/azure-cli).</span><span class="sxs-lookup"><span data-stu-id="53e83-134">toolog in, you can use a [service principal](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) created with hello [Azure CLI 2.0](https://github.com/azure/azure-cli).</span></span>

<span data-ttu-id="53e83-135">Можно создать участника службы с hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="53e83-135">A service principal can be created with hello following steps:</span></span>

1. <span data-ttu-id="53e83-136">Войдите в Azure CLI toohello (`az login`) как пользователя с масштабирования виртуальных машин доступа toohello задать</span><span class="sxs-lookup"><span data-stu-id="53e83-136">Log in toohello Azure CLI (`az login`) as a user with access toohello virtual machine scale set</span></span>
2. <span data-ttu-id="53e83-137">Создание участника с помощью службы hello`az ad sp create-for-rbac`</span><span class="sxs-lookup"><span data-stu-id="53e83-137">Create hello service principal with `az ad sp create-for-rbac`</span></span>
    1. <span data-ttu-id="53e83-138">Запишите appId hello (называемые «идентификатор клиента» в другом месте), имя, пароль и клиента для последующего использования.</span><span class="sxs-lookup"><span data-stu-id="53e83-138">Make note of hello appId (called 'client ID' elsewhere), name, password, and tenant for later use.</span></span>
    2. <span data-ttu-id="53e83-139">Также вам понадобится идентификатор подписки, который можно просмотреть с помощью `az account list`.</span><span class="sxs-lookup"><span data-stu-id="53e83-139">You will also need your subscription ID, which can be viewed with `az account list`</span></span>

<span data-ttu-id="53e83-140">Hello библиотеки fluent вычислений можно войти в систему с эти учетные данные следующим образом (Обратите внимание, что core fluent Azure типов, таких как `IAzure` в hello [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) пакет):</span><span class="sxs-lookup"><span data-stu-id="53e83-140">hello fluent compute library can log in using these credentials as follows (note that core fluent Azure types like `IAzure` are in hello [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package):</span></span>

```C#
var credentials = new AzureCredentials(new ServicePrincipalLoginInformation {
                ClientId = AzureClientId,
                ClientSecret = 
                AzureClientKey }, AzureTenantId, AzureEnvironment.AzureGlobalCloud);
IAzure AzureClient = Azure.Authenticate(credentials).WithSubscription(AzureSubscriptionId);

if (AzureClient?.SubscriptionId == AzureSubscriptionId)
{
    ServiceEventSource.Current.ServiceMessage(Context, "Successfully logged into Azure");
}
else
{
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed toologin tooAzure");
}
```

<span data-ttu-id="53e83-141">После входа в систему можно запросить подсчет экземпляров масштабируемого набора с помощью `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span><span class="sxs-lookup"><span data-stu-id="53e83-141">Once logged in, scale set instance count can be queried via `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span></span>

## <a name="scaling-out"></a><span data-ttu-id="53e83-142">Развертывание</span><span class="sxs-lookup"><span data-stu-id="53e83-142">Scaling out</span></span>
<span data-ttu-id="53e83-143">С помощью плавного hello вычислений Azure SDK, экземпляры могут добавляться набор с несколькими вызовами - масштабирования виртуальных машин toohello</span><span class="sxs-lookup"><span data-stu-id="53e83-143">Using hello fluent Azure compute SDK, instances can be added toohello virtual machine scale set with just a few calls -</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

<span data-ttu-id="53e83-144">Кроме того, размер масштабируемого набора виртуальных машин можно изменить с помощью командлетов PowerShell.</span><span class="sxs-lookup"><span data-stu-id="53e83-144">Alternatively, virtual machine scale set size can also be managed with PowerShell cmdlets.</span></span> <span data-ttu-id="53e83-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)можно получить объект набора масштабирования виртуальной машины hello.</span><span class="sxs-lookup"><span data-stu-id="53e83-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) can retrieve hello virtual machine scale set object.</span></span> <span data-ttu-id="53e83-146">текущая емкость Hello будет храниться в hello `.sku.capacity` свойство.</span><span class="sxs-lookup"><span data-stu-id="53e83-146">hello current capacity will be stored in hello `.sku.capacity` property.</span></span> <span data-ttu-id="53e83-147">После изменения toohello емкости hello необходимое значение, можно обновить набор в Azure масштабирования виртуальных машин hello hello [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) команды.</span><span class="sxs-lookup"><span data-stu-id="53e83-147">After changing hello capacity toohello desired value, hello virtual machine scale set in Azure can be updated with hello [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) command.</span></span>

<span data-ttu-id="53e83-148">Как при добавлении узла вручную, добавляя экземпляр набора масштабирования должно быть Service Fabric новый узел, поскольку hello в наборе шаблон включает в себя все с необходимые toostart tooautomatically расширения Присоединение нового кластера Service Fabric toohello экземпляров.</span><span class="sxs-lookup"><span data-stu-id="53e83-148">As when adding a node manually, adding a scale set instance should be all that's needed toostart a new Service Fabric node since hello scale set template includes extensions tooautomatically join new instances toohello Service Fabric cluster.</span></span> 

## <a name="scaling-in"></a><span data-ttu-id="53e83-149">Уменьшение масштаба</span><span class="sxs-lookup"><span data-stu-id="53e83-149">Scaling in</span></span>

<span data-ttu-id="53e83-150">Масштабирование в — примерно tooscaling out. Hello фактический набор виртуальных машин масштаб изменений, практически hello таким же.</span><span class="sxs-lookup"><span data-stu-id="53e83-150">Scaling in is similar tooscaling out. hello actual virtual machine scale set changes are practically hello same.</span></span> <span data-ttu-id="53e83-151">Но, как было описано ранее, служба Service Fabric автоматически очищает только удаленные узлы с уровнем устойчивости Gold или Silver.</span><span class="sxs-lookup"><span data-stu-id="53e83-151">But, as was discussed previously, Service Fabric only automatically cleans up removed nodes with a durability of Gold or Silver.</span></span> <span data-ttu-id="53e83-152">Поэтому hello бронза устойчивость масштабирования в случае, при необходимости toointeract с hello Service Fabric tooshut вниз toobe узел hello удалены, а затем tooremove его состояние кластера.</span><span class="sxs-lookup"><span data-stu-id="53e83-152">So, in hello Bronze-durability scale-in case, it's necessary toointeract with hello Service Fabric cluster tooshut down hello node toobe removed and then tooremove its state.</span></span>

<span data-ttu-id="53e83-153">Подготовка узла hello для завершения работы включает в себя поиск toobe hello узел удален (hello недавно добавленных узел) и его отключение.</span><span class="sxs-lookup"><span data-stu-id="53e83-153">Preparing hello node for shutdown involves finding hello node toobe removed (hello most recently added node) and deactivating it.</span></span> <span data-ttu-id="53e83-154">В случае с неначальными узлами более новые узлы можно найти с помощью сравнения `NodeInstanceId`.</span><span class="sxs-lookup"><span data-stu-id="53e83-154">For non-seed nodes, newer nodes can be found by comparing `NodeInstanceId`.</span></span> 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

<span data-ttu-id="53e83-155">Имейте в виду, что *начальное значение* узлы Непохоже tooalways соглашению hello сначала удалить больше идентификаторов экземпляров.</span><span class="sxs-lookup"><span data-stu-id="53e83-155">Be aware that *seed* nodes don't seem tooalways follow hello convention that greater instance IDs are removed first.</span></span>

<span data-ttu-id="53e83-156">После обнаружения toobe узел hello удалены могут быть деактивированы и удален с помощью hello же `FabricClient` экземпляра и hello `IAzure` экземпляр из более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="53e83-156">Once hello node toobe removed is found, it can be deactivated and removed using hello same `FabricClient` instance and hello `IAzure` instance from earlier.</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove hello node from hello Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up tooa timeout) for hello node toogracefully shutdown
var timeout = TimeSpan.FromMinutes(5);
var waitStart = DateTime.Now;
while ((mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Up || mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Disabling) &&
        DateTime.Now - waitStart < timeout)
{
    mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync()).FirstOrDefault(n => n.NodeName == mostRecentLiveNode.NodeName);
    await Task.Delay(10 * 1000);
}

// Decrement VMSS capacity
var newCapacity = (int)Math.Max(MinimumNodeCount, scaleSet.Capacity - 1); // Check min count 

scaleSet.Update().WithCapacity(newCapacity).Apply(); 
```

<span data-ttu-id="53e83-157">Как и при развертывании, можно использовать командлеты PowerShell для изменения емкости масштабируемого набора виртуальных машин, если подход с использованием скриптов предпочтительнее.</span><span class="sxs-lookup"><span data-stu-id="53e83-157">As with scaling out, PowerShell cmdlets for modifying virtual machine scale set capacity can also be used here if a scripting approach is preferable.</span></span> <span data-ttu-id="53e83-158">После удаления экземпляра виртуальной машины hello Service Fabric состояния узла может быть удален.</span><span class="sxs-lookup"><span data-stu-id="53e83-158">Once hello virtual machine instance is removed, Service Fabric node state can be removed.</span></span>

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a><span data-ttu-id="53e83-159">Потенциальные недостатки</span><span class="sxs-lookup"><span data-stu-id="53e83-159">Potential drawbacks</span></span>

<span data-ttu-id="53e83-160">Как показано в предшествующих фрагменты кода hello, создание масштабирования службы предоставляет наивысшую степень контроля и подлежит через приложение hello масштабирование.</span><span class="sxs-lookup"><span data-stu-id="53e83-160">As demonstrated in hello preceding code snippets, creating your own scaling service provides hello highest degree of control and customizability over your application's scaling behavior.</span></span> <span data-ttu-id="53e83-161">Это может быть полезно в сценариях, в которых необходим точный контроль над временем или способом изменения масштаба приложения. Тем не менее этот элемент управления отличается сложностью кода.</span><span class="sxs-lookup"><span data-stu-id="53e83-161">This can be useful for scenarios requiring precise control over when or how an application scales in or out. However, this control comes with a tradeoff of code complexity.</span></span> <span data-ttu-id="53e83-162">При таком подходе означает, что вы должны tooown масштабирование код, который является нетривиальной.</span><span class="sxs-lookup"><span data-stu-id="53e83-162">Using this approach means that you need tooown scaling code, which is non-trivial.</span></span>

<span data-ttu-id="53e83-163">Подход к масштабированию Service Fabric зависит от сценария.</span><span class="sxs-lookup"><span data-stu-id="53e83-163">How you should approach Service Fabric scaling depends on your scenario.</span></span> <span data-ttu-id="53e83-164">При масштабировании редко, hello возможность tooadd или удаление узлов вручную, возможно, недостаточно.</span><span class="sxs-lookup"><span data-stu-id="53e83-164">If scaling is uncommon, hello ability tooadd or remove nodes manually is probably sufficient.</span></span> <span data-ttu-id="53e83-165">Для более сложных сценариев правил автоматического масштабирования и пакеты SDK, программным путем предоставления tooscale возможность hello обеспечивают широкие возможности.</span><span class="sxs-lookup"><span data-stu-id="53e83-165">For more complex scenarios, auto-scale rules and SDKs exposing hello ability tooscale programmatically offer powerful alternatives.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53e83-166">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="53e83-166">Next steps</span></span>

<span data-ttu-id="53e83-167">использовать собственную логику автоматического масштабирования tooget ознакомиться с hello следующие основные понятия и полезные API-интерфейсы:</span><span class="sxs-lookup"><span data-stu-id="53e83-167">tooget started implementing your own auto-scaling logic, familiarize yourself with hello following concepts and useful APIs:</span></span>

- [<span data-ttu-id="53e83-168">Масштабирование кластера Service Fabric с помощью правил автомасштабирования</span><span class="sxs-lookup"><span data-stu-id="53e83-168">Scaling manually or with auto-scale rules</span></span>](./service-fabric-cluster-scale-up-down.md)
- <span data-ttu-id="53e83-169">[Свободные библиотеки управления Azure для .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (для взаимодействия с базовыми масштабируемыми наборами виртуальных машин для кластеров Service Fabric)</span><span class="sxs-lookup"><span data-stu-id="53e83-169">[Fluent Azure Management Libraries for .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (useful for interacting with a Service Fabric cluster's underlying virtual machine scale sets)</span></span>
- <span data-ttu-id="53e83-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (для взаимодействия с кластером Service Fabric и его узлами)</span><span class="sxs-lookup"><span data-stu-id="53e83-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (useful for interacting with a Service Fabric cluster and its nodes)</span></span>
