---
title: "Пример скрипта Azure CLI. Фильтрация сетевого трафика виртуальной машины | Документация Майкрософт"
description: "Пример скрипта Azure CLI. Фильтрация входящего и исходящего сетевого трафика виртуальной машины."
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
ms.openlocfilehash: 68ee013cff4e0be15af30239e0314f779f50177a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="12b6f-103">Фильтрация входящего и исходящего сетевого трафика виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="12b6f-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="12b6f-104">В этом примере скрипта создается виртуальная сеть с интерфейсной и внутренней подсетями.</span><span class="sxs-lookup"><span data-stu-id="12b6f-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="12b6f-105">Входящий сетевой трафик в интерфейсной подсети принимается по портам HTTP, HTTPS и SSH, тогда как исходящий трафик в Интернет из внутренней подсети не разрешен.</span><span class="sxs-lookup"><span data-stu-id="12b6f-105">Inbound network traffic to the front-end subnet is limited to HTTP, HTTPS and SSH, while outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> <span data-ttu-id="12b6f-106">После выполнения скрипта у вас будет одна виртуальная машина с двумя сетевыми адаптерами.</span><span class="sxs-lookup"><span data-stu-id="12b6f-106">After running the script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="12b6f-107">Каждый сетевой адаптер подключен к другой подсети.</span><span class="sxs-lookup"><span data-stu-id="12b6f-107">Each NIC is connected to a different subnet.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="12b6f-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="12b6f-108">Sample script</span></span>


<span data-ttu-id="12b6f-109">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Фильтрация сетевого трафика виртуальной машины")]</span><span class="sxs-lookup"><span data-stu-id="12b6f-109">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="12b6f-110">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="12b6f-110">Clean up deployment</span></span> 

<span data-ttu-id="12b6f-111">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="12b6f-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="12b6f-112">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="12b6f-112">Script explanation</span></span>

<span data-ttu-id="12b6f-113">Для создания группы ресурсов, виртуальной сети и групп безопасности сети этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="12b6f-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="12b6f-114">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="12b6f-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="12b6f-115">Команда</span><span class="sxs-lookup"><span data-stu-id="12b6f-115">Command</span></span> | <span data-ttu-id="12b6f-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="12b6f-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="12b6f-117">az group create</span><span class="sxs-lookup"><span data-stu-id="12b6f-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="12b6f-118">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="12b6f-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="12b6f-119">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="12b6f-119">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="12b6f-120">Создает виртуальную сеть Azure и интерфейсную подсеть.</span><span class="sxs-lookup"><span data-stu-id="12b6f-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="12b6f-121">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="12b6f-121">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="12b6f-122">Создает внутреннюю подсеть.</span><span class="sxs-lookup"><span data-stu-id="12b6f-122">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="12b6f-123">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="12b6f-123">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update) | <span data-ttu-id="12b6f-124">Связывает группы безопасности сети с подсетями.</span><span class="sxs-lookup"><span data-stu-id="12b6f-124">Associates NSGs to subnets.</span></span> |
| [<span data-ttu-id="12b6f-125">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="12b6f-125">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="12b6f-126">Создает общедоступный IP-адрес для доступа к виртуальной машине из Интернета.</span><span class="sxs-lookup"><span data-stu-id="12b6f-126">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="12b6f-127">az network nic create</span><span class="sxs-lookup"><span data-stu-id="12b6f-127">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="12b6f-128">Создает виртуальные сетевые интерфейсы и присоединяет их к интерфейсной и внутренней подсети виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="12b6f-128">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="12b6f-129">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="12b6f-129">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="12b6f-130">Создает группы безопасности сети (NSG), которые связаны с интерфейсной и внутренней подсетями.</span><span class="sxs-lookup"><span data-stu-id="12b6f-130">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="12b6f-131">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="12b6f-131">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="12b6f-132">Создает правила групп безопасности сети, которые разрешают или блокируют определенные порты для конкретных подсетей.</span><span class="sxs-lookup"><span data-stu-id="12b6f-132">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="12b6f-133">az vm create</span><span class="sxs-lookup"><span data-stu-id="12b6f-133">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="12b6f-134">Создает виртуальные машины и присоединяет сетевой адаптер к каждой из них.</span><span class="sxs-lookup"><span data-stu-id="12b6f-134">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="12b6f-135">Эта команда также указывает образ виртуальной машины и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="12b6f-135">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="12b6f-136">az group delete</span><span class="sxs-lookup"><span data-stu-id="12b6f-136">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="12b6f-137">Удаляет группу ресурсов и все содержащиеся в ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="12b6f-137">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="12b6f-138">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="12b6f-138">Next steps</span></span>

<span data-ttu-id="12b6f-139">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="12b6f-139">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="12b6f-140">Дополнительные примеры сценариев Azure CLI для сетей Azure см. в [обзоре документации по сетям Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="12b6f-140">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>