---
title: "Пример сценария CLI - aaaAzure создайте виртуальную Машину Linux | Документы Microsoft"
description: "Пример скрипта Azure CLI. Создание виртуальной машины Linux"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c9855204a85cc0f6cd758a1d20121fbeea070943
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-configured-virtual-machine"></a><span data-ttu-id="b6c41-103">Создание полностью настроенной виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="b6c41-103">Create a fully configured virtual machine</span></span>

<span data-ttu-id="b6c41-104">Этот сценарий создает виртуальную машину Azure с операционной системой Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="b6c41-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="b6c41-105">После выполнения сценария hello, доступ к виртуальной машине hello через SSH.</span><span class="sxs-lookup"><span data-stu-id="b6c41-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b6c41-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="b6c41-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b6c41-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="b6c41-107">Clean up deployment</span></span> 

<span data-ttu-id="b6c41-108">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="b6c41-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="b6c41-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="b6c41-109">Script explanation</span></span>

<span data-ttu-id="b6c41-110">Этот скрипт использует hello, следующие команды toocreate группу ресурсов виртуальной машины, и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b6c41-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="b6c41-111">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="b6c41-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b6c41-112">Команда</span><span class="sxs-lookup"><span data-stu-id="b6c41-112">Command</span></span> | <span data-ttu-id="b6c41-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="b6c41-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b6c41-114">az group create</span><span class="sxs-lookup"><span data-stu-id="b6c41-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b6c41-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="b6c41-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b6c41-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="b6c41-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="b6c41-117">Создает виртуальную сеть и подсеть Azure.</span><span class="sxs-lookup"><span data-stu-id="b6c41-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="b6c41-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="b6c41-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="b6c41-119">Создает общедоступный IP-адрес со статическим IP-адресом и связанным DNS-именем.</span><span class="sxs-lookup"><span data-stu-id="b6c41-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="b6c41-120">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="b6c41-120">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="b6c41-121">Создание группы безопасности сети (NSG), который является границей безопасности между виртуальными машинами hello Интернет» и «hello.</span><span class="sxs-lookup"><span data-stu-id="b6c41-121">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="b6c41-122">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="b6c41-122">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="b6c41-123">Создает правило NSG tooallow входящий трафик.</span><span class="sxs-lookup"><span data-stu-id="b6c41-123">Creates an NSG rule tooallow inbound traffic.</span></span> <span data-ttu-id="b6c41-124">В этом примере открывается порт 22 для трафика SSH.</span><span class="sxs-lookup"><span data-stu-id="b6c41-124">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="b6c41-125">az network nic create</span><span class="sxs-lookup"><span data-stu-id="b6c41-125">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="b6c41-126">Создает виртуальный сетевой адаптер и присоединяет его toohello виртуальной сети, подсети и NSG.</span><span class="sxs-lookup"><span data-stu-id="b6c41-126">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="b6c41-127">az vm create</span><span class="sxs-lookup"><span data-stu-id="b6c41-127">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="b6c41-128">Создает виртуальную машину hello и подключает его toohello сетевой карты, виртуальной сети, подсети и NSG.</span><span class="sxs-lookup"><span data-stu-id="b6c41-128">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="b6c41-129">Эта команда также указывает hello toobe образа на виртуальной машине используется и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="b6c41-129">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="b6c41-130">az group delete</span><span class="sxs-lookup"><span data-stu-id="b6c41-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="b6c41-131">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="b6c41-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b6c41-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b6c41-132">Next steps</span></span>

<span data-ttu-id="b6c41-133">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b6c41-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b6c41-134">Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машине Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b6c41-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
