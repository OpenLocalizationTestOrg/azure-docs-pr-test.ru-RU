---
title: "Пример скрипта Azure CLI. Маршрутизация трафика через виртуальный сетевой модуль | Документация Майкрософт"
description: "Пример скрипта Azure CLI. Маршрутизация трафика через виртуальный сетевой модуль брандмауэра."
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: 78091b515c00591a4af8d807945475b6be50188a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="4530a-103">Маршрутизация трафика через виртуальный сетевой модуль</span><span class="sxs-lookup"><span data-stu-id="4530a-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="4530a-104">В этом примере скрипта создается виртуальная сеть с интерфейсной и внутренней подсетями.</span><span class="sxs-lookup"><span data-stu-id="4530a-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="4530a-105">Скрипт также создает виртуальную машину с IP-пересылкой, которая позволяет маршрутизировать трафик между двумя подсетями.</span><span class="sxs-lookup"><span data-stu-id="4530a-105">It also creates a VM with IP forwarding enabled to route traffic between the two subnets.</span></span> <span data-ttu-id="4530a-106">После выполнения скрипта вы можете развернуть на виртуальной машине программное обеспечение сети, например брандмауэр.</span><span class="sxs-lookup"><span data-stu-id="4530a-106">After running the script you can deploy network software, such as a firewall application, to the VM.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="4530a-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="4530a-107">Sample script</span></span>


<span data-ttu-id="4530a-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Маршрутизация трафика через виртуальный сетевой модуль")]</span><span class="sxs-lookup"><span data-stu-id="4530a-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="4530a-109">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="4530a-109">Clean up deployment</span></span> 

<span data-ttu-id="4530a-110">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="4530a-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="4530a-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="4530a-111">Script explanation</span></span>

<span data-ttu-id="4530a-112">Для создания группы ресурсов, виртуальной сети и групп безопасности сети этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="4530a-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="4530a-113">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="4530a-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="4530a-114">Команда</span><span class="sxs-lookup"><span data-stu-id="4530a-114">Command</span></span> | <span data-ttu-id="4530a-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="4530a-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4530a-116">az group create</span><span class="sxs-lookup"><span data-stu-id="4530a-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="4530a-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="4530a-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4530a-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="4530a-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="4530a-119">Создает виртуальную сеть Azure и интерфейсную подсеть.</span><span class="sxs-lookup"><span data-stu-id="4530a-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="4530a-120">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="4530a-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="4530a-121">Создает внутреннюю подсеть и подсеть DMZ.</span><span class="sxs-lookup"><span data-stu-id="4530a-121">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="4530a-122">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="4530a-122">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="4530a-123">Создает общедоступный IP-адрес для доступа к виртуальной машине из Интернета.</span><span class="sxs-lookup"><span data-stu-id="4530a-123">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="4530a-124">az network nic create</span><span class="sxs-lookup"><span data-stu-id="4530a-124">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="4530a-125">Создает виртуальный сетевой интерфейс и включает IP-пересылку для него.</span><span class="sxs-lookup"><span data-stu-id="4530a-125">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="4530a-126">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="4530a-126">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="4530a-127">Создает группу безопасности сети (NSG).</span><span class="sxs-lookup"><span data-stu-id="4530a-127">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="4530a-128">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="4530a-128">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) | <span data-ttu-id="4530a-129">Создает правила группы безопасности сети, которые разрешают входящий трафик по портам HTTP и HTTPS к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="4530a-129">Creates NSG rules that allow HTTP and HTTPS ports inbound to the VM.</span></span> |
| [<span data-ttu-id="4530a-130">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="4530a-130">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update)| <span data-ttu-id="4530a-131">Связывает группы безопасности сети и таблицы маршрутов с подсетями.</span><span class="sxs-lookup"><span data-stu-id="4530a-131">Associates the NSGs and route tables to subnets.</span></span> |
| [<span data-ttu-id="4530a-132">az network route-table create</span><span class="sxs-lookup"><span data-stu-id="4530a-132">az network route-table create</span></span>](/cli/azure/network/route-table#create)| <span data-ttu-id="4530a-133">Создает таблицу маршрутов для всех маршрутов.</span><span class="sxs-lookup"><span data-stu-id="4530a-133">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="4530a-134">az network route-table route create</span><span class="sxs-lookup"><span data-stu-id="4530a-134">az network route-table route create</span></span>](/cli/azure/network/route-table/route#create)| <span data-ttu-id="4530a-135">Создает маршруты для маршрутизации трафика между подсетями и Интернетом через виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="4530a-135">Creates routes to route traffic between subnets and the Internet through the VM.</span></span> |
| [<span data-ttu-id="4530a-136">az vm create</span><span class="sxs-lookup"><span data-stu-id="4530a-136">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="4530a-137">Создает виртуальную машину и присоединяет к ней сетевой адаптер.</span><span class="sxs-lookup"><span data-stu-id="4530a-137">Creates a virtual machine and attaches the NIC to it.</span></span> <span data-ttu-id="4530a-138">Эта команда также указывает образ виртуальной машины и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="4530a-138">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="4530a-139">az group delete</span><span class="sxs-lookup"><span data-stu-id="4530a-139">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="4530a-140">Удаляет группу ресурсов и все содержащиеся в ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="4530a-140">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4530a-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4530a-141">Next steps</span></span>

<span data-ttu-id="4530a-142">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4530a-142">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="4530a-143">Дополнительные примеры сценариев Azure CLI для сетей Azure см. в [обзоре документации по сетям Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4530a-143">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>