---
title: "Следующий прыжок aaaFind с Azure сети наблюдателя следующего прыжка — PowerShell | Документы Microsoft"
description: "В этой статье описывается, как можно найти какие hello тип следующего прыжка — и адрес ip с помощью следующего прыжка с помощью PowerShell."
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
ms.openlocfilehash: fdb0b4a02d95fc45c103fe952fc1afa095414c18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-powershell"></a><span data-ttu-id="28d6e-103">Узнать, какой тип следующего прыжка hello является использование возможностей следующего прыжка hello в Наблюдатель сети Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="28d6e-103">Find out what hello next hop type is using hello Next Hop capability in Azure Network Watcher using PowerShell</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="28d6e-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="28d6e-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="28d6e-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="28d6e-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="28d6e-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="28d6e-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="28d6e-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="28d6e-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="28d6e-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="28d6e-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="28d6e-109">Следующий прыжок является компонентом Наблюдатель сети, который предоставляет возможность hello получить тип следующего прыжка hello и IP-адрес, на основе указанной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="28d6e-109">Next hop is a feature of Network Watcher that provides hello ability get hello next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="28d6e-110">Эта функция полезна при определении Если пакетов, отправляемых виртуальная машина проходит через шлюз, Интернет или назначения tooits tooget виртуальных сетей.</span><span class="sxs-lookup"><span data-stu-id="28d6e-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks tooget tooits destination.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="28d6e-111">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="28d6e-111">Before you begin</span></span>

<span data-ttu-id="28d6e-112">В этом сценарии используется hello тип следующего прыжка Azure портала toofind hello и IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="28d6e-112">In this scenario, you will use hello Azure portal toofind hello next hop type and IP address.</span></span>

<span data-ttu-id="28d6e-113">Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети.</span><span class="sxs-lookup"><span data-stu-id="28d6e-113">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher.</span></span> <span data-ttu-id="28d6e-114">сценарий Hello также предполагается, что группа ресурсов с действительной виртуальной машиной существует toobe используется.</span><span class="sxs-lookup"><span data-stu-id="28d6e-114">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="28d6e-115">Сценарий</span><span class="sxs-lookup"><span data-stu-id="28d6e-115">Scenario</span></span>

<span data-ttu-id="28d6e-116">Hello сценарии, описанные в данной статье используется следующего прыжка, функция Наблюдатель сети, извлекают тип следующего прыжка hello и IP-адрес для ресурса.</span><span class="sxs-lookup"><span data-stu-id="28d6e-116">hello scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out hello next hop type and IP address for a resource.</span></span> <span data-ttu-id="28d6e-117">Посетите toolearn Дополнительные сведения о следующего прыжка [следующего прыжка Обзор](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="28d6e-117">toolearn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>

## <a name="retrieve-network-watcher"></a><span data-ttu-id="28d6e-118">Извлечение Наблюдателя за сетями</span><span class="sxs-lookup"><span data-stu-id="28d6e-118">Retrieve Network Watcher</span></span>

<span data-ttu-id="28d6e-119">Первым шагом Hello — экземпляр Наблюдатель сети tooretrieve hello.</span><span class="sxs-lookup"><span data-stu-id="28d6e-119">hello first step is tooretrieve hello Network Watcher instance.</span></span> <span data-ttu-id="28d6e-120">Hello `$networkWatcher` переменной передается toohello следующего прыжка проверка командлета.</span><span class="sxs-lookup"><span data-stu-id="28d6e-120">hello `$networkWatcher` variable is passed toohello next hop verify cmdlet.</span></span>

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="get-a-virtual-machine"></a><span data-ttu-id="28d6e-121">Получение виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="28d6e-121">Get a virtual machine</span></span>

<span data-ttu-id="28d6e-122">Следующий прыжок возвращает следующего прыжка hello и hello IP-адрес следующего прыжка hello из виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="28d6e-122">Next hop returns hello next hop and hello IP address of hello next hop from a virtual machine.</span></span> <span data-ttu-id="28d6e-123">Идентификатор виртуальной машины является обязательным для командлета hello.</span><span class="sxs-lookup"><span data-stu-id="28d6e-123">An Id of a virtual machine is required for hello cmdlet.</span></span> <span data-ttu-id="28d6e-124">Если вы уже знаете идентификатор hello toouse hello виртуальной машины, этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="28d6e-124">If you already know hello ID of hello virtual machine toouse, you can skip this step.</span></span>

```powershell
$VM = Get-AzurermVM -ResourceGroupName "testrg" -Name "testvm1"
```

> [!NOTE]
> <span data-ttu-id="28d6e-125">Следующий прыжок требуется что toorun распределения ресурсов виртуальной Машины hello.</span><span class="sxs-lookup"><span data-stu-id="28d6e-125">Next hop requires that hello VM resource is allocated toorun.</span></span>

## <a name="get-hello-network-interfaces"></a><span data-ttu-id="28d6e-126">Получить hello сетевых интерфейсов</span><span class="sxs-lookup"><span data-stu-id="28d6e-126">Get hello network interfaces</span></span>

<span data-ttu-id="28d6e-127">в этом примере мы получить hello сетевых адаптеров на виртуальной машине требуется Hello IP-адрес сетевого адаптера на виртуальной машине hello.</span><span class="sxs-lookup"><span data-stu-id="28d6e-127">hello IP address of a NIC on hello virtual machine is needed, in this example we retrieve hello NICs on a virtual machine.</span></span> <span data-ttu-id="28d6e-128">Если вы уже знаете hello IP адрес, о котором требуется tootest на виртуальной машине hello, этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="28d6e-128">If you already know hello IP address that you want tootest on hello virtual machine, you can skip this step.</span></span>

```powershell
$Nics = Get-AzureRmNetworkInterface | Where {$_.Id -eq $vm.NetworkProfile.NetworkInterfaces.Id.ForEach({$_})}
```

## <a name="get-next-hop"></a><span data-ttu-id="28d6e-129">Получение следующего прыжка</span><span class="sxs-lookup"><span data-stu-id="28d6e-129">Get Next Hop</span></span>

<span data-ttu-id="28d6e-130">Теперь мы называем hello `Get-AzureRmNetworkWatcherNextHop` командлета.</span><span class="sxs-lookup"><span data-stu-id="28d6e-130">Now we call hello `Get-AzureRmNetworkWatcherNextHop` cmdlet.</span></span> <span data-ttu-id="28d6e-131">Мы передайте hello командлет hello Наблюдатель сети виртуальной машины идентификатор, исходный IP-адрес и IP-адрес назначения.</span><span class="sxs-lookup"><span data-stu-id="28d6e-131">We pass hello cmdlet hello Network Watcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="28d6e-132">В этом примере hello конечный IP-адрес — tooa виртуальной Машины в другой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="28d6e-132">In this example, hello destination IP address is tooa VM in another virtual network.</span></span> <span data-ttu-id="28d6e-133">Нет шлюза виртуальной сети между двумя виртуальными сетями hello.</span><span class="sxs-lookup"><span data-stu-id="28d6e-133">There is a virtual network gateway between hello two virtual networks.</span></span>

```powershell
Get-AzureRmNetworkWatcherNextHop -NetworkWatcher $networkWatcher -TargetVirtualMachineId $VM.Id -SourceIPAddress $nics[0].IpConfigurations[0].PrivateIpAddress  -DestinationIPAddress 10.0.2.4 
```

## <a name="review-results"></a><span data-ttu-id="28d6e-134">Просмотр результатов</span><span class="sxs-lookup"><span data-stu-id="28d6e-134">Review results</span></span>

<span data-ttu-id="28d6e-135">По завершении приведены результаты hello.</span><span class="sxs-lookup"><span data-stu-id="28d6e-135">When complete, hello results are provided.</span></span> <span data-ttu-id="28d6e-136">а также hello тип ресурса, который является возвращается IP-адрес следующего прыжка Hello.</span><span class="sxs-lookup"><span data-stu-id="28d6e-136">hello next hop IP address is returned as well as hello type of resource it is.</span></span> <span data-ttu-id="28d6e-137">В этом случае это hello общедоступный IP-адрес шлюза виртуальной сети hello.</span><span class="sxs-lookup"><span data-stu-id="28d6e-137">In this scenario, it is hello public IP address of hello virtual network gateway.</span></span>

```
NextHopIpAddress NextHopType           RouteTableId 
---------------- -----------           ------------ 
13.78.238.92     VirtualNetworkGateway Gateway Route
```

<span data-ttu-id="28d6e-138">Hello ниже перечислены в настоящее время доступных значений NextHopType hello.</span><span class="sxs-lookup"><span data-stu-id="28d6e-138">hello following list shows hello currently available NextHopType values:</span></span>

<span data-ttu-id="28d6e-139">**Типы следующего прыжка**</span><span class="sxs-lookup"><span data-stu-id="28d6e-139">**Next Hop Type**</span></span>

* <span data-ttu-id="28d6e-140">Интернет</span><span class="sxs-lookup"><span data-stu-id="28d6e-140">Internet</span></span>
* <span data-ttu-id="28d6e-141">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="28d6e-141">VirtualAppliance</span></span>
* <span data-ttu-id="28d6e-142">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="28d6e-142">VirtualNetworkGateway</span></span>
* <span data-ttu-id="28d6e-143">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="28d6e-143">VnetLocal</span></span>
* <span data-ttu-id="28d6e-144">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="28d6e-144">HyperNetGateway</span></span>
* <span data-ttu-id="28d6e-145">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="28d6e-145">VnetPeering</span></span>
* <span data-ttu-id="28d6e-146">None</span><span class="sxs-lookup"><span data-stu-id="28d6e-146">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="28d6e-147">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="28d6e-147">Next steps</span></span>

<span data-ttu-id="28d6e-148">Узнайте, как tooreview параметров группы безопасности сети программным способом, посетив [NSG аудита и Наблюдатель сети](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="28d6e-148">Learn how tooreview your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>

















