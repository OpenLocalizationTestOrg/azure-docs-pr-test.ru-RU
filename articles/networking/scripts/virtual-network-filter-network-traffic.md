---
title: "Пример сценария CLI aaaAzure - сетевого трафика виртуальных Машин фильтр | Документы Microsoft"
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
ms.openlocfilehash: c2f14e54bc96c99420b4300d1c24a457ac8c948c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="32abe-103">Фильтрация входящего и исходящего сетевого трафика виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="32abe-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="32abe-104">В этом примере скрипта создается виртуальная сеть с интерфейсной и внутренней подсетями.</span><span class="sxs-lookup"><span data-stu-id="32abe-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="32abe-105">Входящий сетевой трафик интерфейса подсети toohello ограниченный tooHTTP, HTTPS и SSH, пока исходящего трафика toohello Интернет из внутренней подсети hello не допускается.</span><span class="sxs-lookup"><span data-stu-id="32abe-105">Inbound network traffic toohello front-end subnet is limited tooHTTP, HTTPS and SSH, while outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> <span data-ttu-id="32abe-106">После выполнения сценария hello, имеется одна виртуальная машина с двумя сетевыми адаптерами.</span><span class="sxs-lookup"><span data-stu-id="32abe-106">After running hello script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="32abe-107">Каждый сетевой Адаптер имеет подключенного tooa другой подсети.</span><span class="sxs-lookup"><span data-stu-id="32abe-107">Each NIC is connected tooa different subnet.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="32abe-108">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="32abe-108">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a><span data-ttu-id="32abe-109">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="32abe-109">Clean up deployment</span></span> 

<span data-ttu-id="32abe-110">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="32abe-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="32abe-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="32abe-111">Script explanation</span></span>

<span data-ttu-id="32abe-112">Этот скрипт использует следующие команды toocreate hello группы ресурсов, виртуальной сети и группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="32abe-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="32abe-113">Каждая команда в таблице hello связывает toocommand документации.</span><span class="sxs-lookup"><span data-stu-id="32abe-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="32abe-114">Команда</span><span class="sxs-lookup"><span data-stu-id="32abe-114">Command</span></span> | <span data-ttu-id="32abe-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="32abe-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="32abe-116">az group create</span><span class="sxs-lookup"><span data-stu-id="32abe-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="32abe-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="32abe-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="32abe-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="32abe-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="32abe-119">Создает виртуальную сеть Azure и интерфейсную подсеть.</span><span class="sxs-lookup"><span data-stu-id="32abe-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="32abe-120">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="32abe-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="32abe-121">Создает внутреннюю подсеть.</span><span class="sxs-lookup"><span data-stu-id="32abe-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="32abe-122">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="32abe-122">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update) | <span data-ttu-id="32abe-123">Связывает toosubnets Nsg.</span><span class="sxs-lookup"><span data-stu-id="32abe-123">Associates NSGs toosubnets.</span></span> |
| [<span data-ttu-id="32abe-124">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="32abe-124">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="32abe-125">Создает открытый tooaccess hello IP адрес виртуальной Машины из Интернета hello.</span><span class="sxs-lookup"><span data-stu-id="32abe-125">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="32abe-126">az network nic create</span><span class="sxs-lookup"><span data-stu-id="32abe-126">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="32abe-127">Создает виртуальными сетевыми интерфейсами и вкладывает их подсети виртуальной сети toohello внешнего и внутреннего интерфейса.</span><span class="sxs-lookup"><span data-stu-id="32abe-127">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="32abe-128">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="32abe-128">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="32abe-129">Создание группы безопасности сети (NSG), которые будут связанного toohello внешнего и внутреннего интерфейса подсети.</span><span class="sxs-lookup"><span data-stu-id="32abe-129">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="32abe-130">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="32abe-130">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="32abe-131">Создаются правила NSG, разрешать или запрещать определенные порты toospecific подсетей.</span><span class="sxs-lookup"><span data-stu-id="32abe-131">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="32abe-132">az vm create</span><span class="sxs-lookup"><span data-stu-id="32abe-132">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="32abe-133">Создает виртуальные машины и присоединяет tooeach сетевого Адаптера виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="32abe-133">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="32abe-134">Эта команда также указывает toouse образ виртуальной машины hello и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="32abe-134">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="32abe-135">az group delete</span><span class="sxs-lookup"><span data-stu-id="32abe-135">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="32abe-136">Удаляет группу ресурсов и все содержащиеся в ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="32abe-136">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="32abe-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="32abe-137">Next steps</span></span>

<span data-ttu-id="32abe-138">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="32abe-138">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="32abe-139">Дополнительные сетевые образцы сценариев CLI можно найти в hello [документации Azure Общие сведения о сети](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="32abe-139">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
