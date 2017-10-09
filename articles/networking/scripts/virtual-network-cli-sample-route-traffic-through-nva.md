---
title: "Пример сценария CLI aaaAzure - трафик через сеть виртуального устройства | Документы Microsoft"
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
ms.openlocfilehash: 981d6073be04a7ebaf96b657fbab8a378e7a995e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="d2afc-103">Маршрутизация трафика через виртуальный сетевой модуль</span><span class="sxs-lookup"><span data-stu-id="d2afc-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="d2afc-104">В этом примере скрипта создается виртуальная сеть с интерфейсной и внутренней подсетями.</span><span class="sxs-lookup"><span data-stu-id="d2afc-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="d2afc-105">Он также создает виртуальную Машину с IP-пересылка включена tooroute трафик между двумя подсетями hello.</span><span class="sxs-lookup"><span data-stu-id="d2afc-105">It also creates a VM with IP forwarding enabled tooroute traffic between hello two subnets.</span></span> <span data-ttu-id="d2afc-106">После выполнения сценария hello можно развернуть сетевое программное обеспечение, таких как брандмауэр toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d2afc-106">After running hello script you can deploy network software, such as a firewall application, toohello VM.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="d2afc-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="d2afc-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d2afc-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="d2afc-108">Clean up deployment</span></span> 

<span data-ttu-id="d2afc-109">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="d2afc-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="d2afc-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="d2afc-110">Script explanation</span></span>

<span data-ttu-id="d2afc-111">Этот скрипт использует следующие команды toocreate hello группы ресурсов, виртуальной сети и группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="d2afc-111">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="d2afc-112">Каждая команда в таблице hello связывает toocommand документации.</span><span class="sxs-lookup"><span data-stu-id="d2afc-112">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="d2afc-113">Команда</span><span class="sxs-lookup"><span data-stu-id="d2afc-113">Command</span></span> | <span data-ttu-id="d2afc-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="d2afc-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d2afc-115">az group create</span><span class="sxs-lookup"><span data-stu-id="d2afc-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="d2afc-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d2afc-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d2afc-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="d2afc-117">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="d2afc-118">Создает виртуальную сеть Azure и интерфейсную подсеть.</span><span class="sxs-lookup"><span data-stu-id="d2afc-118">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="d2afc-119">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="d2afc-119">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="d2afc-120">Создает внутреннюю подсеть и подсеть DMZ.</span><span class="sxs-lookup"><span data-stu-id="d2afc-120">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="d2afc-121">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="d2afc-121">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="d2afc-122">Создает открытый tooaccess hello IP адрес виртуальной Машины из Интернета hello.</span><span class="sxs-lookup"><span data-stu-id="d2afc-122">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="d2afc-123">az network nic create</span><span class="sxs-lookup"><span data-stu-id="d2afc-123">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="d2afc-124">Создает виртуальный сетевой интерфейс и включает IP-пересылку для него.</span><span class="sxs-lookup"><span data-stu-id="d2afc-124">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="d2afc-125">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="d2afc-125">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="d2afc-126">Создает группу безопасности сети (NSG).</span><span class="sxs-lookup"><span data-stu-id="d2afc-126">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="d2afc-127">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="d2afc-127">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) | <span data-ttu-id="d2afc-128">Создает правила NSG, позволяющими toohello ВМ входящие порты HTTP и HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d2afc-128">Creates NSG rules that allow HTTP and HTTPS ports inbound toohello VM.</span></span> |
| [<span data-ttu-id="d2afc-129">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="d2afc-129">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update)| <span data-ttu-id="d2afc-130">Связывает hello Nsg и toosubnets таблицы маршрутов.</span><span class="sxs-lookup"><span data-stu-id="d2afc-130">Associates hello NSGs and route tables toosubnets.</span></span> |
| [<span data-ttu-id="d2afc-131">az network route-table create</span><span class="sxs-lookup"><span data-stu-id="d2afc-131">az network route-table create</span></span>](/cli/azure/network/route-table#create)| <span data-ttu-id="d2afc-132">Создает таблицу маршрутов для всех маршрутов.</span><span class="sxs-lookup"><span data-stu-id="d2afc-132">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="d2afc-133">az network route-table route create</span><span class="sxs-lookup"><span data-stu-id="d2afc-133">az network route-table route create</span></span>](/cli/azure/network/route-table/route#create)| <span data-ttu-id="d2afc-134">Создает маршруты tooroute трафика между подсетями и hello Интернета через hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="d2afc-134">Creates routes tooroute traffic between subnets and hello Internet through hello VM.</span></span> |
| [<span data-ttu-id="d2afc-135">az vm create</span><span class="sxs-lookup"><span data-stu-id="d2afc-135">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="d2afc-136">Создает виртуальную машину и присоединяет hello tooit сетевого Адаптера.</span><span class="sxs-lookup"><span data-stu-id="d2afc-136">Creates a virtual machine and attaches hello NIC tooit.</span></span> <span data-ttu-id="d2afc-137">Эта команда также указывает toouse образ виртуальной машины hello и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="d2afc-137">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="d2afc-138">az group delete</span><span class="sxs-lookup"><span data-stu-id="d2afc-138">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="d2afc-139">Удаляет группу ресурсов и все содержащиеся в ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d2afc-139">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d2afc-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d2afc-140">Next steps</span></span>

<span data-ttu-id="d2afc-141">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d2afc-141">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="d2afc-142">Дополнительные сетевые образцы сценариев CLI можно найти в hello [документации Azure Общие сведения о сети](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="d2afc-142">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
