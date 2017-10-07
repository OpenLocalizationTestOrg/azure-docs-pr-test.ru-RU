---
title: "Пример сценария CLI - aaaAzure создания виртуальной Машины Windows Server | Документы Microsoft"
description: "Пример скрипта Azure CLI. Создание виртуальной машины Windows Server"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: f4cb431a68c911f877f5af87c393849bd8d2676a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="2e9b5-103">Создание виртуальной машины с hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2e9b5-103">Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="2e9b5-104">Этот сценарий создает виртуальную машину Azure под управлением Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="2e9b5-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="2e9b5-105">После выполнения сценария hello, hello виртуальной машины можно обращаться к удаленному рабочему столу.</span><span class="sxs-lookup"><span data-stu-id="2e9b5-105">After running hello script, you can access hello virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2e9b5-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="2e9b5-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2e9b5-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="2e9b5-107">Clean up deployment</span></span> 

<span data-ttu-id="2e9b5-108">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="2e9b5-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="2e9b5-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="2e9b5-109">Script explanation</span></span>

<span data-ttu-id="2e9b5-110">Этот скрипт использует hello, следующие команды toocreate группу ресурсов виртуальной машины, и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="2e9b5-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="2e9b5-111">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="2e9b5-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2e9b5-112">Команда</span><span class="sxs-lookup"><span data-stu-id="2e9b5-112">Command</span></span> | <span data-ttu-id="2e9b5-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="2e9b5-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2e9b5-114">az group create</span><span class="sxs-lookup"><span data-stu-id="2e9b5-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2e9b5-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="2e9b5-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2e9b5-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="2e9b5-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="2e9b5-117">Создает виртуальную сеть и подсеть Azure.</span><span class="sxs-lookup"><span data-stu-id="2e9b5-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="2e9b5-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="2e9b5-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="2e9b5-119">Создает общедоступный IP-адрес со статическим IP-адресом и связанным DNS-именем.</span><span class="sxs-lookup"><span data-stu-id="2e9b5-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="2e9b5-120">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="2e9b5-120">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="2e9b5-121">Создание группы безопасности сети (NSG), который является границей безопасности между виртуальными машинами hello Интернет» и «hello.</span><span class="sxs-lookup"><span data-stu-id="2e9b5-121">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="2e9b5-122">az network nic create</span><span class="sxs-lookup"><span data-stu-id="2e9b5-122">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="2e9b5-123">Создает виртуальный сетевой адаптер и присоединяет его toohello виртуальной сети, подсети и NSG.</span><span class="sxs-lookup"><span data-stu-id="2e9b5-123">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="2e9b5-124">az vm create</span><span class="sxs-lookup"><span data-stu-id="2e9b5-124">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="2e9b5-125">Создает виртуальную машину hello и подключает его toohello сетевой карты, виртуальной сети, подсети и NSG.</span><span class="sxs-lookup"><span data-stu-id="2e9b5-125">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="2e9b5-126">Эта команда также указывает hello toobe образа на виртуальной машине используется и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="2e9b5-126">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="2e9b5-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="2e9b5-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="2e9b5-128">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="2e9b5-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2e9b5-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2e9b5-129">Next steps</span></span>

<span data-ttu-id="2e9b5-130">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2e9b5-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2e9b5-131">Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машины Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2e9b5-131">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
