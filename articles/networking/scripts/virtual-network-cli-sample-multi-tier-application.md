---
title: "сценарий CLI aaaAzure пример — создание сети многоуровневых приложений | Документы Microsoft"
description: "Пример скрипта Azure CLI. Создание сети для многоуровневых приложений."
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
ms.openlocfilehash: deeb3f459499cebd1b8ded6a299eb759d49cf08d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="bd05a-103">Создание сети для многоуровневых приложений</span><span class="sxs-lookup"><span data-stu-id="bd05a-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="bd05a-104">В этом примере скрипта создается виртуальная сеть с интерфейсной и внутренней подсетями.</span><span class="sxs-lookup"><span data-stu-id="bd05a-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="bd05a-105">Подсети интерфейса toohello трафика является ограниченной tooHTTP и SSH, при toohello трафика конечной подсети ограниченный tooMySQL, порт 3306.</span><span class="sxs-lookup"><span data-stu-id="bd05a-105">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> <span data-ttu-id="bd05a-106">После выполнения скрипта hello имеется две виртуальные машины, по одному в каждой подсети, можно развернуть веб-сервера и программное обеспечение MySQL.</span><span class="sxs-lookup"><span data-stu-id="bd05a-106">After running hello script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="bd05a-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="bd05a-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="bd05a-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="bd05a-108">Clean up deployment</span></span> 

<span data-ttu-id="bd05a-109">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="bd05a-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="bd05a-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="bd05a-110">Script explanation</span></span>

<span data-ttu-id="bd05a-111">Этот скрипт использует следующие команды toocreate hello группы ресурсов, виртуальной сети и группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="bd05a-111">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="bd05a-112">Каждая команда в таблице hello связывает toocommand документации.</span><span class="sxs-lookup"><span data-stu-id="bd05a-112">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="bd05a-113">Команда</span><span class="sxs-lookup"><span data-stu-id="bd05a-113">Command</span></span> | <span data-ttu-id="bd05a-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="bd05a-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bd05a-115">az group create</span><span class="sxs-lookup"><span data-stu-id="bd05a-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="bd05a-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="bd05a-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="bd05a-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="bd05a-117">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="bd05a-118">Создает виртуальную сеть Azure и интерфейсную подсеть.</span><span class="sxs-lookup"><span data-stu-id="bd05a-118">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="bd05a-119">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="bd05a-119">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="bd05a-120">Создает внутреннюю подсеть.</span><span class="sxs-lookup"><span data-stu-id="bd05a-120">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="bd05a-121">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="bd05a-121">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="bd05a-122">Создает открытый tooaccess hello IP адрес виртуальной Машины из Интернета hello.</span><span class="sxs-lookup"><span data-stu-id="bd05a-122">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="bd05a-123">az network nic create</span><span class="sxs-lookup"><span data-stu-id="bd05a-123">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="bd05a-124">Создает виртуальными сетевыми интерфейсами и вкладывает их подсети виртуальной сети toohello внешнего и внутреннего интерфейса.</span><span class="sxs-lookup"><span data-stu-id="bd05a-124">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="bd05a-125">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="bd05a-125">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="bd05a-126">Создание группы безопасности сети (NSG), которые будут связанного toohello внешнего и внутреннего интерфейса подсети.</span><span class="sxs-lookup"><span data-stu-id="bd05a-126">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="bd05a-127">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="bd05a-127">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="bd05a-128">Создаются правила NSG, разрешать или запрещать определенные порты toospecific подсетей.</span><span class="sxs-lookup"><span data-stu-id="bd05a-128">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="bd05a-129">az vm create</span><span class="sxs-lookup"><span data-stu-id="bd05a-129">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="bd05a-130">Создает виртуальные машины и присоединяет tooeach сетевого Адаптера виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="bd05a-130">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="bd05a-131">Эта команда также указывает toouse образ виртуальной машины hello и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="bd05a-131">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="bd05a-132">az group delete</span><span class="sxs-lookup"><span data-stu-id="bd05a-132">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="bd05a-133">Удаляет группу ресурсов и все содержащиеся в ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="bd05a-133">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bd05a-134">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bd05a-134">Next steps</span></span>

<span data-ttu-id="bd05a-135">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bd05a-135">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="bd05a-136">Дополнительные сетевые образцы сценариев CLI можно найти в hello [документации Azure Общие сведения о сети](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="bd05a-136">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
