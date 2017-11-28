---
title: "Поиск следующего прыжка с помощью возможности определения следующего прыжка Наблюдателя за сетями Azure (PowerShell) | Документация Майкрософт"
description: "В этой статье описано, как определить тип следующего прыжка и IP-адрес, используя возможность определения следующего прыжка с помощью PowerShell."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 6a656c55-17bd-40f1-905d-90659087639c
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 00161e7c6fb4becdb7d8eab266fa27128e50f8ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-powershell"></a><span data-ttu-id="a3592-103">Определите тип следующего прыжка, используя возможность определения следующего прыжка Наблюдателя за сетями Azure с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a3592-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="a3592-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="a3592-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="a3592-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3592-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="a3592-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="a3592-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="a3592-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a3592-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="a3592-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="a3592-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="a3592-109">Определение следующего прыжка — это возможность Наблюдателя за сетями, позволяющая определить тип следующего прыжка и IP-адрес на основе указанной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a3592-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="a3592-110">Эта возможность используется, чтобы определить путь передачи исходящего трафика виртуальной машины (шлюз, Интернет или виртуальные сети) к месту назначения.</span><span class="sxs-lookup"><span data-stu-id="a3592-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a3592-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="a3592-111">Before you begin</span></span>

<span data-ttu-id="a3592-112">В этом сценарии для определения типа следующего прыжка и IP-адреса используется портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a3592-112">In this scenario, you will use the Azure portal to find the next hop type and IP address.</span></span>

<span data-ttu-id="a3592-113">В этом сценарии предполагается, что вы создали Наблюдатель за сетями в соответствии с инструкциями в статье [Create an Azure Network Watcher instance](network-watcher-create.md) (Наблюдатель за сетями: создание экземпляра службы).</span><span class="sxs-lookup"><span data-stu-id="a3592-113">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="a3592-114">Предполагается также, что у вас есть группа ресурсов с допустимой виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="a3592-114">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="a3592-115">Сценарий</span><span class="sxs-lookup"><span data-stu-id="a3592-115">Scenario</span></span>

<span data-ttu-id="a3592-116">В сценарии, описанном в этой статье, используется определение следующего прыжка — возможность Наблюдателя за сетями, которая позволяет определить тип следующего перехода и IP-адрес для ресурса.</span><span class="sxs-lookup"><span data-stu-id="a3592-116">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="a3592-117">Дополнительные сведения об определении следующего прыжка см. в [этой статье](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a3592-117">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="a3592-118">Извлечение Наблюдателя за сетями</span><span class="sxs-lookup"><span data-stu-id="a3592-118">Retrieve Network Watcher</span></span>

<span data-ttu-id="a3592-119">Сначала необходимо извлечь экземпляр Наблюдателя за сетями.</span><span class="sxs-lookup"><span data-stu-id="a3592-119">The first step is to retrieve the Network Watcher instance.</span></span> <span data-ttu-id="a3592-120">Переменная `$networkWatcher` передается в командлет проверки следующего прыжка.</span><span class="sxs-lookup"><span data-stu-id="a3592-120">The `$networkWatcher` variable is passed to the next hop verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a><span data-ttu-id="a3592-121">Получение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="a3592-121">Get a virtual machine</span></span>

<span data-ttu-id="a3592-122">Функция определения следующего прыжка возвращает сведения о следующем прыжке из виртуальной машины и его IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="a3592-122">Next hop returns the next hop and the IP address of the next hop from a virtual machine.</span></span> <span data-ttu-id="a3592-123">Для командлета требуется идентификатор виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="a3592-123">An Id of a virtual machine is required for the cmdlet.</span></span> <span data-ttu-id="a3592-124">Если вы уже знаете идентификатор виртуальной машины, этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="a3592-124">If you already know the ID of the virtual machine to use, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> <span data-ttu-id="a3592-125">Для получения следующего прыжка необходимо, чтобы ресурс виртуальной машины был выделен.</span><span class="sxs-lookup"><span data-stu-id="a3592-125">Next hop requires that the VM resource is allocated to run.</span></span>

## <a name="get-the-network-interfaces"></a><span data-ttu-id="a3592-126">Получение сетевых интерфейсов</span><span class="sxs-lookup"><span data-stu-id="a3592-126">Get the network interfaces</span></span>

<span data-ttu-id="a3592-127">Вам понадобится IP-адрес сетевой карты на виртуальной машине. В этом примере мы получаем сетевые карты на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="a3592-127">The IP address of a NIC on the virtual machine is needed, in this example we retrieve the NICs on a virtual machine.</span></span> <span data-ttu-id="a3592-128">Если вы уже знаете IP-адрес, который необходимо протестировать на виртуальной машине, этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="a3592-128">If you already know the IP address that you want to test on the virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a><span data-ttu-id="a3592-129">Получение следующего прыжка</span><span class="sxs-lookup"><span data-stu-id="a3592-129">Get Next Hop</span></span>

<span data-ttu-id="a3592-130">Теперь необходимо вызвать командлет `Get-AzureRmNetworkWatcherNextHop`.</span><span class="sxs-lookup"><span data-stu-id="a3592-130">Now we call the `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span></span> <span data-ttu-id="a3592-131">Мы передаем в этот командлет Наблюдатель за сетями, идентификатор виртуальной машины, IP-адрес источника и места назначения.</span><span class="sxs-lookup"><span data-stu-id="a3592-131">We pass the cmdlet the Network Watcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="a3592-132">В этом примере в качестве IP-адреса места назначения используется IP-адрес виртуальной машины в другой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="a3592-132">In this example, the destination IP address is to a VM in another virtual network.</span></span> <span data-ttu-id="a3592-133">Между двумя виртуальными сетями находится шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="a3592-133">There is a virtual network gateway between the two virtual networks.</span></span>

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a><span data-ttu-id="a3592-134">Просмотр результатов</span><span class="sxs-lookup"><span data-stu-id="a3592-134">Review results</span></span>

<span data-ttu-id="a3592-135">По завершении выводятся результаты.</span><span class="sxs-lookup"><span data-stu-id="a3592-135">When complete, the results are provided.</span></span> <span data-ttu-id="a3592-136">Возвращается IP-адрес следующего прыжка и тип ресурса.</span><span class="sxs-lookup"><span data-stu-id="a3592-136">The next hop IP address is returned as well as the type of resource it is.</span></span> <span data-ttu-id="a3592-137">В этом случае это общедоступный IP-адрес шлюза виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="a3592-137">In this scenario, it is the public IP address of the virtual network gateway.</span></span>

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

<span data-ttu-id="a3592-138">Ниже перечислены доступные значения NextHopType.</span><span class="sxs-lookup"><span data-stu-id="a3592-138">The following list shows the currently available NextHopType values:</span></span>

<span data-ttu-id="a3592-139">**Типы следующего прыжка**</span><span class="sxs-lookup"><span data-stu-id="a3592-139">**Next Hop Type**</span></span>

* <span data-ttu-id="a3592-140">Интернет</span><span class="sxs-lookup"><span data-stu-id="a3592-140">Internet</span></span>
* <span data-ttu-id="a3592-141">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="a3592-141">VirtualAppliance</span></span>
* <span data-ttu-id="a3592-142">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="a3592-142">VirtualNetworkGateway</span></span>
* <span data-ttu-id="a3592-143">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="a3592-143">VnetLocal</span></span>
* <span data-ttu-id="a3592-144">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="a3592-144">HyperNetGateway</span></span>
* <span data-ttu-id="a3592-145">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="a3592-145">VnetPeering</span></span>
* <span data-ttu-id="a3592-146">None</span><span class="sxs-lookup"><span data-stu-id="a3592-146">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3592-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a3592-147">Next steps</span></span>

<span data-ttu-id="a3592-148">Узнайте, как просмотреть параметры группы безопасности сети программным образом, в статье [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md) (Выполнение аудита групп безопасности сети с помощью Наблюдателя за сетями).</span><span class="sxs-lookup"><span data-stu-id="a3592-148">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

















