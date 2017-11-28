---
title: "Поиск следующего прыжка с помощью возможности определения следующего прыжка в Наблюдателе за сетями Azure (Azure CLI 1.0) | Документация Майкрософт"
description: "В этой статье описано, как определить тип следующего прыжка и IP-адрес, используя возможность определения следующего прыжка в Azure CLI."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: ff88e945060ae033717ceb29db1352e112f05a3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="find-out-what-the-next-hop-type-is-using-the-next-hop-capability-in-azure-network-watcher-using-azure-cli-10"></a><span data-ttu-id="be7f8-103">Определите тип следующего прыжка, используя возможность определения следующего прыжка в Наблюдателе за сетями Azure в Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="be7f8-103">Find out what the next hop type is using the Next Hop capability in Azure Network Watcher using Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="be7f8-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="be7f8-104">Azure portal</span></span>](network-watcher-check-next-hop-portal.md)
> - [<span data-ttu-id="be7f8-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="be7f8-105">PowerShell</span></span>](network-watcher-check-next-hop-powershell.md)
> - [<span data-ttu-id="be7f8-106">Интерфейс командной строки 1.0</span><span class="sxs-lookup"><span data-stu-id="be7f8-106">CLI 1.0</span></span>](network-watcher-check-next-hop-cli-nodejs.md)
> - [<span data-ttu-id="be7f8-107">CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="be7f8-107">CLI 2.0</span></span>](network-watcher-check-next-hop-cli.md)
> - [<span data-ttu-id="be7f8-108">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="be7f8-108">Azure REST API</span></span>](network-watcher-check-next-hop-rest.md)

<span data-ttu-id="be7f8-109">Определение следующего прыжка — это возможность Наблюдателя за сетями, позволяющая определить тип следующего прыжка и IP-адрес на основе указанной виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="be7f8-109">Next hop is a feature of Network Watcher that provides the ability get the next hop type and IP address based on a specified virtual machine.</span></span> <span data-ttu-id="be7f8-110">Эта возможность используется, чтобы определить путь передачи исходящего трафика виртуальной машины (шлюз, Интернет или виртуальные сети) к месту назначения.</span><span class="sxs-lookup"><span data-stu-id="be7f8-110">This feature is useful in determining if traffic leaving a virtual machine traverses a gateway, internet, or virtual networks to get to its destination.</span></span>

<span data-ttu-id="be7f8-111">В этой статье используется кроссплатформенной Azure CLI 1.0, доступный для Windows, Mac и Linux.</span><span class="sxs-lookup"><span data-stu-id="be7f8-111">This article uses cross-platform Azure CLI 1.0, which is available for Windows, Mac and Linux.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="be7f8-112">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="be7f8-112">Before you begin</span></span>

<span data-ttu-id="be7f8-113">В этом сценарии для определения типа следующего прыжка и IP-адреса используется Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="be7f8-113">In this scenario, you will use the Azure CLI to find the next hop type and IP address.</span></span>

<span data-ttu-id="be7f8-114">В этом сценарии предполагается, что вы создали Наблюдатель за сетями в соответствии с инструкциями в статье [Create a Network Watcher](network-watcher-create.md) (Создание Наблюдателя за сетями).</span><span class="sxs-lookup"><span data-stu-id="be7f8-114">This scenario assumes you have already followed the steps in [Create a Network Watcher](network-watcher-create.md) to create a Network Watcher.</span></span> <span data-ttu-id="be7f8-115">Предполагается также, что у вас есть группа ресурсов с допустимой виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="be7f8-115">The scenario also assumes that a Resource Group with a valid virtual machine exists to be used.</span></span>

## <a name="scenario"></a><span data-ttu-id="be7f8-116">Сценарий</span><span class="sxs-lookup"><span data-stu-id="be7f8-116">Scenario</span></span>

<span data-ttu-id="be7f8-117">В сценарии, описанном в этой статье, используется определение следующего прыжка — возможность Наблюдателя за сетями, которая позволяет определить тип следующего перехода и IP-адрес для ресурса.</span><span class="sxs-lookup"><span data-stu-id="be7f8-117">The scenario covered in this article uses Next Hop, a feature of Network Watcher that finds out the next hop type and IP address for a resource.</span></span> <span data-ttu-id="be7f8-118">Дополнительные сведения об определении следующего прыжка см. в [этой статье](network-watcher-next-hop-overview.md).</span><span class="sxs-lookup"><span data-stu-id="be7f8-118">To learn more about Next Hop, visit [Next Hop Overview](network-watcher-next-hop-overview.md).</span></span>


## <a name="get-next-hop"></a><span data-ttu-id="be7f8-119">Получение следующего прыжка</span><span class="sxs-lookup"><span data-stu-id="be7f8-119">Get Next Hop</span></span>

<span data-ttu-id="be7f8-120">Чтобы получить следующий прыжок, вызовите командлет `azure netowrk watcher next-hop`.</span><span class="sxs-lookup"><span data-stu-id="be7f8-120">To get the next hop we call the `azure netowrk watcher next-hop` cmdlet.</span></span> <span data-ttu-id="be7f8-121">Мы передаем в командлет группу ресурсов Наблюдателя за сетями, Наблюдатель за сетями, идентификатор виртуальной машины, IP-адрес источника и места назначения.</span><span class="sxs-lookup"><span data-stu-id="be7f8-121">We pass the cmdlet the Network Watcher resource group, the NetworkWatcher, virtual machine Id, source IP address, and destination IP address.</span></span> <span data-ttu-id="be7f8-122">В этом примере в качестве IP-адреса места назначения используется IP-адрес виртуальной машины в другой виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="be7f8-122">In this example, the destination IP address is to a VM in another virtual network.</span></span> <span data-ttu-id="be7f8-123">Между двумя виртуальными сетями находится шлюз виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="be7f8-123">There is a virtual network gateway between the two virtual networks.</span></span> 

```azurecli
azure network watcher next-hop -g resourceGroupName -n networkWatcherName -t targetResourceId -a <source-ip> -d <destination-ip>
```

> [!NOTE]
<span data-ttu-id="be7f8-124">Если в виртуальной машине есть несколько сетевых карт и на любой из них включена IP-пересылка, нужно указать параметр сетевой карты (-i nic-id).</span><span class="sxs-lookup"><span data-stu-id="be7f8-124">If the VM has multiple NICs and IP forwarding is enabled on any of the NICs, then the NIC parameter (-i nic-id) must be specified.</span></span> <span data-ttu-id="be7f8-125">В противном случае этот параметр является необязательным.</span><span class="sxs-lookup"><span data-stu-id="be7f8-125">Otherwise it is optional.</span></span>

## <a name="review-results"></a><span data-ttu-id="be7f8-126">Просмотр результатов</span><span class="sxs-lookup"><span data-stu-id="be7f8-126">Review results</span></span>

<span data-ttu-id="be7f8-127">По завершении выводятся результаты.</span><span class="sxs-lookup"><span data-stu-id="be7f8-127">When complete, the results are provided.</span></span> <span data-ttu-id="be7f8-128">Возвращается IP-адрес следующего прыжка и тип ресурса.</span><span class="sxs-lookup"><span data-stu-id="be7f8-128">The next hop IP address is returned as well as the type of resource it is.</span></span>

```
data:    Next Hop Ip Address             : 10.0.1.2
info:    network watcher next-hop command OK
```

<span data-ttu-id="be7f8-129">Ниже перечислены доступные значения NextHopType.</span><span class="sxs-lookup"><span data-stu-id="be7f8-129">The following list shows the currently available NextHopType values:</span></span>

<span data-ttu-id="be7f8-130">**Типы следующего прыжка**</span><span class="sxs-lookup"><span data-stu-id="be7f8-130">**Next Hop Type**</span></span>

* <span data-ttu-id="be7f8-131">Интернет</span><span class="sxs-lookup"><span data-stu-id="be7f8-131">Internet</span></span>
* <span data-ttu-id="be7f8-132">VirtualAppliance</span><span class="sxs-lookup"><span data-stu-id="be7f8-132">VirtualAppliance</span></span>
* <span data-ttu-id="be7f8-133">VirtualNetworkGateway</span><span class="sxs-lookup"><span data-stu-id="be7f8-133">VirtualNetworkGateway</span></span>
* <span data-ttu-id="be7f8-134">VnetLocal</span><span class="sxs-lookup"><span data-stu-id="be7f8-134">VnetLocal</span></span>
* <span data-ttu-id="be7f8-135">HyperNetGateway</span><span class="sxs-lookup"><span data-stu-id="be7f8-135">HyperNetGateway</span></span>
* <span data-ttu-id="be7f8-136">VnetPeering</span><span class="sxs-lookup"><span data-stu-id="be7f8-136">VnetPeering</span></span>
* <span data-ttu-id="be7f8-137">None</span><span class="sxs-lookup"><span data-stu-id="be7f8-137">None</span></span>

## <a name="next-steps"></a><span data-ttu-id="be7f8-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="be7f8-138">Next steps</span></span>

<span data-ttu-id="be7f8-139">Узнайте, как просмотреть параметры группы безопасности сети программным образом, в статье [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md) (Выполнение аудита групп безопасности сети с помощью Наблюдателя за сетями).</span><span class="sxs-lookup"><span data-stu-id="be7f8-139">Learn how to review your network security group settings programmatically by visiting [NSG Auditing with Network Watcher](network-watcher-nsg-auditing-powershell.md)</span></span>
