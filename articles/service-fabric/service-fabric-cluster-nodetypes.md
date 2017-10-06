---
title: "aaaService структуры и типов узлов набора масштабирования виртуальных Машин | Документы Microsoft"
description: "Описывает, как типы узлов Service Fabric связаны наборы tooVM масштабирования и способ подключения tooremote tooa набора масштабирования виртуальных Машин экземпляра или узла кластера."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 5441e7e0-d842-4398-b060-8c9d34b07c48
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/05/2017
ms.author: chackdan
ms.openlocfilehash: 830ea2816f5864de146a77483c85de26f91c2425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="hello-relationship-between-service-fabric-node-types-and-virtual-machine-scale-sets"></a><span data-ttu-id="f875d-103">Hello связь между Service Fabric типы узлов и наборы масштабирования виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="f875d-103">hello relationship between Service Fabric node types and Virtual Machine Scale Sets</span></span>
<span data-ttu-id="f875d-104">Наборы масштабирования виртуальных машин, Azure Compute ресурсов можно использовать toodeploy и управлять коллекцией виртуальных машин как набор.</span><span class="sxs-lookup"><span data-stu-id="f875d-104">Virtual Machine Scale Sets are an Azure Compute resource you can use toodeploy and manage a collection of virtual machines as a set.</span></span> <span data-ttu-id="f875d-105">Каждый тип узла, определенный в кластере Service Fabric, настроен как отдельный набор масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="f875d-105">Every node type that is defined in a Service Fabric cluster is set up as a separate VM Scale Set.</span></span> <span data-ttu-id="f875d-106">Каждый тип узла поддерживает возможность независимого масштабирования, имеет разные наборы открытых портов и собственные метрики емкости.</span><span class="sxs-lookup"><span data-stu-id="f875d-106">Each node type can then be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>

<span data-ttu-id="f875d-107">Следующий снимок экрана приветствия показан кластер с двумя типами узлов: внешнего и внутреннего.</span><span class="sxs-lookup"><span data-stu-id="f875d-107">hello following screen shot shows a cluster that has two node types: FrontEnd and BackEnd.</span></span>  <span data-ttu-id="f875d-108">Каждый тип узла имеет пять узлов.</span><span class="sxs-lookup"><span data-stu-id="f875d-108">Each node type has five nodes each.</span></span>

![Снимок экрана с двумя типами узлов][NodeTypes]

## <a name="mapping-vm-scale-set-instances-toonodes"></a><span data-ttu-id="f875d-110">Сопоставление toonodes экземпляров набора масштабирования виртуальных Машин</span><span class="sxs-lookup"><span data-stu-id="f875d-110">Mapping VM Scale Set instances toonodes</span></span>
<span data-ttu-id="f875d-111">Как видно выше hello набора масштабирования виртуальных Машин экземпляры начинаются с экземпляра 0, а затем возрастает.</span><span class="sxs-lookup"><span data-stu-id="f875d-111">As you can see above, hello VM Scale Set instances start from instance 0 and then goes up.</span></span> <span data-ttu-id="f875d-112">Нумерация Hello отражается в имена hello.</span><span class="sxs-lookup"><span data-stu-id="f875d-112">hello numbering is reflected in hello names.</span></span> <span data-ttu-id="f875d-113">Например BackEnd_0 — экземпляр 0 hello набора масштабирования виртуальных Машин серверной части.</span><span class="sxs-lookup"><span data-stu-id="f875d-113">For example, BackEnd_0 is instance 0 of hello BackEnd VM Scale Set.</span></span> <span data-ttu-id="f875d-114">Этот конкретный масштабируемый набор ВМ имеет пять экземпляров с именами BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 и BackEnd_4.</span><span class="sxs-lookup"><span data-stu-id="f875d-114">This particular VM Scale Set has five instances, named BackEnd_0, BackEnd_1, BackEnd_2, BackEnd_3 and BackEnd_4.</span></span>

<span data-ttu-id="f875d-115">При увеличении масштаба масштабируемого набора ВМ создается новый экземпляр.</span><span class="sxs-lookup"><span data-stu-id="f875d-115">When you scale up a VM Scale Set a new instance is created.</span></span> <span data-ttu-id="f875d-116">Имя экземпляра нового набора масштабирования виртуальных Машин Hello обычно будет имя набора масштабирования виртуальных Машин hello + hello следующий номер экземпляра.</span><span class="sxs-lookup"><span data-stu-id="f875d-116">hello new VM Scale Set instance name will typically be hello VM Scale Set name + hello next instance number.</span></span> <span data-ttu-id="f875d-117">В нашем примере это BackEnd_5.</span><span class="sxs-lookup"><span data-stu-id="f875d-117">In our example, it is BackEnd_5.</span></span>

## <a name="mapping-vm-scale-set-load-balancers-tooeach-node-typevm-scale-set"></a><span data-ttu-id="f875d-118">Сопоставление виртуальной Машины набора масштабирования загрузить балансировки нагрузки tooeach узел типа или виртуальной Машины набора масштабирования</span><span class="sxs-lookup"><span data-stu-id="f875d-118">Mapping VM scale set load balancers tooeach node type/VM Scale Set</span></span>
<span data-ttu-id="f875d-119">Если вы развернули кластера с портала hello или использовали шаблона диспетчера ресурсов образец hello, мы предоставлен, затем при получении списка всех ресурсов в группе ресурсов вы увидите hello подсистему балансировки нагрузки для каждого типа узла или набора масштабирования виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="f875d-119">If you have deployed your cluster from hello portal or have used hello sample Resource Manager template that we provided, then when you get a list of all resources under a Resource Group then you will see hello load balancers for each VM Scale Set or node type.</span></span>

<span data-ttu-id="f875d-120">Hello имя будет примерно так: **балансировки Нагрузки -&lt;имя NodeType&gt;**.</span><span class="sxs-lookup"><span data-stu-id="f875d-120">hello name would something like: **LB-&lt;NodeType name&gt;**.</span></span> <span data-ttu-id="f875d-121">Например, LB-sfcluster4doc-0, как показано на следующем снимке экрана:</span><span class="sxs-lookup"><span data-stu-id="f875d-121">For example, LB-sfcluster4doc-0, as shown in this screenshot:</span></span>

![Ресурсы][Resources]

## <a name="remote-connect-tooa-vm-scale-set-instance-or-a-cluster-node"></a><span data-ttu-id="f875d-123">Удаленное подключение tooa набора масштабирования виртуальных Машин экземпляра или узла кластера</span><span class="sxs-lookup"><span data-stu-id="f875d-123">Remote connect tooa VM Scale Set instance or a cluster node</span></span>
<span data-ttu-id="f875d-124">Каждый тип узла, определенный в кластере, настроен как отдельный набор масштабирования виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="f875d-124">Every Node type that is defined in a cluster is set up as a separate VM Scale Set.</span></span>  <span data-ttu-id="f875d-125">Что означает hello типов узлов может масштабироваться вверх или вниз независимо друг от друга и может быть выполнен из различных конфигураций виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="f875d-125">That means hello node types can be scaled up or down independently and can be made of different VM SKUs.</span></span> <span data-ttu-id="f875d-126">В отличие от одного экземпляра виртуальные машины экземпляры набора масштабирования виртуальных Машин hello не получают виртуальный IP-адрес своих собственных.</span><span class="sxs-lookup"><span data-stu-id="f875d-126">Unlike single instance VMs, hello VM Scale Set instances do not get a virtual IP address of their own.</span></span> <span data-ttu-id="f875d-127">Поэтому он может быть немного сложной задачей, если вам нужны дополнительные IP-адреса адрес и номер порта, которые можно использовать tooremote подключения tooa конкретного экземпляра.</span><span class="sxs-lookup"><span data-stu-id="f875d-127">So it can be a bit challenging when you are looking for an IP address and port that you can use tooremote connect tooa specific instance.</span></span>

<span data-ttu-id="f875d-128">Ниже приведены шаги hello, можно выполнить toodiscover их.</span><span class="sxs-lookup"><span data-stu-id="f875d-128">Here are hello steps you can follow toodiscover them.</span></span>

### <a name="step-1-find-out-hello-virtual-ip-address-for-hello-node-type-and-then-inbound-nat-rules-for-rdp"></a><span data-ttu-id="f875d-129">Шаг 1: Узнайте hello виртуальный IP-адрес для hello типа узла, а затем правила NAT для входящего трафика для протокола удаленного рабочего СТОЛА</span><span class="sxs-lookup"><span data-stu-id="f875d-129">Step 1: Find out hello virtual IP address for hello node type and then Inbound NAT rules for RDP</span></span>
<span data-ttu-id="f875d-130">В порядке tooget потребуется tooget hello NAT для входящего трафика правила значения, которые были определены как часть определения ресурса hello **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="f875d-130">In order tooget that, you need tooget hello inbound NAT rules values that were defined as a part of hello resource definition for **Microsoft.Network/loadBalancers**.</span></span>

<span data-ttu-id="f875d-131">Hello портала перейдите в колонку подсистемы балансировки нагрузки toohello и затем **параметры**.</span><span class="sxs-lookup"><span data-stu-id="f875d-131">In hello portal, navigate toohello Load balancer blade and then **Settings**.</span></span>

![LBBlade][LBBlade]

<span data-ttu-id="f875d-133">В разделе **Параметры** щелкните **Правила NAT для входящего трафика**.</span><span class="sxs-lookup"><span data-stu-id="f875d-133">In **Settings**, click on **Inbound NAT rules**.</span></span> <span data-ttu-id="f875d-134">Теперь предоставляет hello IP-адреса и порта, которые можно использовать tooremote подключения toohello первый экземпляр набора масштабирования виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="f875d-134">This now gives you hello IP address and port that you can use tooremote connect toohello first VM Scale Set instance.</span></span> <span data-ttu-id="f875d-135">В приведенном далее снимке экрана приветствия, это **104.42.106.156** и **3389**</span><span class="sxs-lookup"><span data-stu-id="f875d-135">In hello screenshot below, it is **104.42.106.156** and **3389**</span></span>

![NATRules][NATRules]

### <a name="step-2-find-out-hello-port-that-you-can-use-tooremote-connect-toohello-specific-vm-scale-set-instancenode"></a><span data-ttu-id="f875d-137">Шаг 2: Узнайте hello портов, которые можно использовать tooremote подключение toohello определенного набора масштабирования виртуальных Машин и узла экземпляра</span><span class="sxs-lookup"><span data-stu-id="f875d-137">Step 2: Find out hello port that you can use tooremote connect toohello specific VM Scale Set instance/node</span></span>
<span data-ttu-id="f875d-138">Ранее в этом документе описывалось сопоставление узлов toohello hello экземпляров набора масштабирования виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="f875d-138">Earlier in this document, I talked about how hello VM Scale Set instances map toohello nodes.</span></span> <span data-ttu-id="f875d-139">Мы будем использовать этот toofigure out hello точный номер порта.</span><span class="sxs-lookup"><span data-stu-id="f875d-139">We will use that toofigure out hello exact port.</span></span>

<span data-ttu-id="f875d-140">порты Hello выделяются в порядке возрастания hello экземпляра набора масштабирования виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="f875d-140">hello ports are allocated in ascending order of hello VM Scale Set instance.</span></span> <span data-ttu-id="f875d-141">Таким образом в нашем примере для hello интерфейсный тип узла hello портов для каждого из пяти экземпляров hello являются следующие hello.</span><span class="sxs-lookup"><span data-stu-id="f875d-141">so in my example for hello FrontEnd node type, hello ports for each of hello five instances are hello following.</span></span> <span data-ttu-id="f875d-142">Вы теперь toodo требуется hello одно сопоставление для экземпляра набора масштабирования виртуальных Машин.</span><span class="sxs-lookup"><span data-stu-id="f875d-142">you now need toodo hello same mapping for your VM Scale Set instance.</span></span>

| <span data-ttu-id="f875d-143">**Экземпляр масштабируемого набора ВМ**</span><span class="sxs-lookup"><span data-stu-id="f875d-143">**VM Scale Set Instance**</span></span> | <span data-ttu-id="f875d-144">**Порт**</span><span class="sxs-lookup"><span data-stu-id="f875d-144">**Port**</span></span> |
| --- | --- |
| <span data-ttu-id="f875d-145">FrontEnd_0</span><span class="sxs-lookup"><span data-stu-id="f875d-145">FrontEnd_0</span></span> |<span data-ttu-id="f875d-146">3389</span><span class="sxs-lookup"><span data-stu-id="f875d-146">3389</span></span> |
| <span data-ttu-id="f875d-147">FrontEnd_1</span><span class="sxs-lookup"><span data-stu-id="f875d-147">FrontEnd_1</span></span> |<span data-ttu-id="f875d-148">3390</span><span class="sxs-lookup"><span data-stu-id="f875d-148">3390</span></span> |
| <span data-ttu-id="f875d-149">FrontEnd_2</span><span class="sxs-lookup"><span data-stu-id="f875d-149">FrontEnd_2</span></span> |<span data-ttu-id="f875d-150">3391</span><span class="sxs-lookup"><span data-stu-id="f875d-150">3391</span></span> |
| <span data-ttu-id="f875d-151">FrontEnd_3</span><span class="sxs-lookup"><span data-stu-id="f875d-151">FrontEnd_3</span></span> |<span data-ttu-id="f875d-152">3392</span><span class="sxs-lookup"><span data-stu-id="f875d-152">3392</span></span> |
| <span data-ttu-id="f875d-153">FrontEnd_4</span><span class="sxs-lookup"><span data-stu-id="f875d-153">FrontEnd_4</span></span> |<span data-ttu-id="f875d-154">3393</span><span class="sxs-lookup"><span data-stu-id="f875d-154">3393</span></span> |
| <span data-ttu-id="f875d-155">FrontEnd_5</span><span class="sxs-lookup"><span data-stu-id="f875d-155">FrontEnd_5</span></span> |<span data-ttu-id="f875d-156">3394</span><span class="sxs-lookup"><span data-stu-id="f875d-156">3394</span></span> |

### <a name="step-3-remote-connect-toohello-specific-vm-scale-set-instance"></a><span data-ttu-id="f875d-157">Шаг 3: Удаленное подключение toohello конкретного экземпляра набора масштабирования виртуальных Машин</span><span class="sxs-lookup"><span data-stu-id="f875d-157">Step 3: Remote connect toohello specific VM Scale Set instance</span></span>
<span data-ttu-id="f875d-158">В следующем снимке экрана приветствия используется удаленный рабочий стол tooconnect toohello FrontEnd_1:</span><span class="sxs-lookup"><span data-stu-id="f875d-158">In hello screenshot below I use Remote Desktop Connection tooconnect toohello FrontEnd_1:</span></span>

![RDP][RDP]

## <a name="how-toochange-hello-rdp-port-range-values"></a><span data-ttu-id="f875d-160">Как toochange hello RDP-порту диапазон значений</span><span class="sxs-lookup"><span data-stu-id="f875d-160">How toochange hello RDP port range values</span></span>
### <a name="before-cluster-deployment"></a><span data-ttu-id="f875d-161">Перед развертыванием кластера</span><span class="sxs-lookup"><span data-stu-id="f875d-161">Before cluster deployment</span></span>
<span data-ttu-id="f875d-162">При настройке кластера hello, с помощью шаблона диспетчера ресурсов, можно указать диапазон hello в hello **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="f875d-162">When you are setting up hello cluster using an Resource Manager template, you can specify hello range in hello **inboundNatPools**.</span></span>

<span data-ttu-id="f875d-163">Go определения ресурса toohello **Microsoft.Network/loadBalancers**.</span><span class="sxs-lookup"><span data-stu-id="f875d-163">Go toohello resource definition for **Microsoft.Network/loadBalancers**.</span></span> <span data-ttu-id="f875d-164">В списке, найдите описание hello **inboundNatPools**.</span><span class="sxs-lookup"><span data-stu-id="f875d-164">Under that you find hello description for **inboundNatPools**.</span></span>  <span data-ttu-id="f875d-165">Замените hello *frontendPortRangeStart* и *значение frontendPortRangeEnd* значения.</span><span class="sxs-lookup"><span data-stu-id="f875d-165">Replace hello *frontendPortRangeStart* and *frontendPortRangeEnd* values.</span></span>

![inboundNatPools][InboundNatPools]

### <a name="after-cluster-deployment"></a><span data-ttu-id="f875d-167">После развертывания кластера</span><span class="sxs-lookup"><span data-stu-id="f875d-167">After cluster deployment</span></span>
<span data-ttu-id="f875d-168">Это немного сложнее и может привести к перезаписывание ВМ hello.</span><span class="sxs-lookup"><span data-stu-id="f875d-168">This is a bit more involved and may result in hello VMs getting recycled.</span></span> <span data-ttu-id="f875d-169">Теперь вы можете tooset новые значения с помощью Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f875d-169">You will now have tooset new values using Azure PowerShell.</span></span> <span data-ttu-id="f875d-170">Убедитесь, что на компьютере установлена среда Azure PowerShell 1.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="f875d-170">Make sure that Azure PowerShell 1.0 or later is installed on your machine.</span></span> <span data-ttu-id="f875d-171">Если вы не выполнили это перед, настоятельно рекомендуется выполнить hello действия, описанные в [как tooinstall и настройка Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="f875d-171">If you have not done this before, I strongly suggest that you follow hello steps outlined in [How tooinstall and configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="f875d-172">Войдите в tooyour учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="f875d-172">Sign in tooyour Azure account.</span></span> <span data-ttu-id="f875d-173">Если команды PowerShell по какой-то причине завершаются неудачно, проверьте, правильно ли установлен Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f875d-173">If this PowerShell command fails for some reason, you should check whether you have Azure PowerShell installed correctly.</span></span>

```
Login-AzureRmAccount
```

<span data-ttu-id="f875d-174">Запустите hello, приведенные ниже сведения tooget на балансировки нагрузки и отображаются значения hello hello описание **inboundNatPools**:</span><span class="sxs-lookup"><span data-stu-id="f875d-174">Run hello following tooget details on your load balancer and you see hello values for hello description for **inboundNatPools**:</span></span>

```
Get-AzureRmResource -ResourceGroupName <RGname> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load balancer name>
```

<span data-ttu-id="f875d-175">Теперь значение *значение frontendPortRangeEnd* и *frontendPortRangeStart* toohello значения, которые требуются.</span><span class="sxs-lookup"><span data-stu-id="f875d-175">Now set *frontendPortRangeEnd* and *frontendPortRangeStart* toohello values you want.</span></span>

```
$PropertiesObject = @{
    #Property = value;
}
Set-AzureRmResource -PropertyObject $PropertiesObject -ResourceGroupName <RG name> -ResourceType Microsoft.Network/loadBalancers -ResourceName <load Balancer name> -ApiVersion <use hello API version that get returned> -Force
```


## <a name="next-steps"></a><span data-ttu-id="f875d-176">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f875d-176">Next steps</span></span>
* [<span data-ttu-id="f875d-177">Обзор компонента «В любом развертывание» hello и сравнение с кластерами под управлением Azure</span><span class="sxs-lookup"><span data-stu-id="f875d-177">Overview of hello "Deploy anywhere" feature and a comparison with Azure-managed clusters</span></span>](service-fabric-deploy-anywhere.md)
* [<span data-ttu-id="f875d-178">Безопасность кластера</span><span class="sxs-lookup"><span data-stu-id="f875d-178">Cluster security</span></span>](service-fabric-cluster-security.md)
* [<span data-ttu-id="f875d-179"> Пакет SDK для Service Fabric и начало работы</span><span class="sxs-lookup"><span data-stu-id="f875d-179"> Service Fabric SDK and getting started</span></span>](service-fabric-get-started.md)

<!--Image references-->
[NodeTypes]: ./media/service-fabric-cluster-nodetypes/NodeTypes.png
[Resources]: ./media/service-fabric-cluster-nodetypes/Resources.png
[InboundNatPools]: ./media/service-fabric-cluster-nodetypes/InboundNatPools.png
[LBBlade]: ./media/service-fabric-cluster-nodetypes/LBBlade.png
[NATRules]: ./media/service-fabric-cluster-nodetypes/NATRules.png
[RDP]: ./media/service-fabric-cluster-nodetypes/RDP.png
