---
title: "aaaAzure образец скрипта CLI - быстрое создание виртуальной Машины Windows Server 2016 | Документы Microsoft"
description: "Пример скрипта Azure CLI. Быстрое создание виртуальной машины Windows Server 2016"
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
ms.author: rickstercdn
ms.openlocfilehash: 4c736ce9e2ecc9ee75b34f903cad52c9c0ee0707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="quick-create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="e37e3-103">Быстрое создание виртуальной машины с hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e37e3-103">Quick Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="e37e3-104">Этот сценарий создает виртуальную машину Azure под управлением Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="e37e3-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="e37e3-105">После выполнения сценария hello, hello виртуальной машины можно обращаться к удаленному рабочему столу.</span><span class="sxs-lookup"><span data-stu-id="e37e3-105">After running hello script, you can access hello virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e37e3-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="e37e3-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-windows-vm-quick.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e37e3-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="e37e3-107">Clean up deployment</span></span> 

<span data-ttu-id="e37e3-108">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="e37e3-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="e37e3-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="e37e3-109">Script explanation</span></span>

<span data-ttu-id="e37e3-110">Этот скрипт использует hello, следующие команды toocreate группу ресурсов виртуальной машины, и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="e37e3-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="e37e3-111">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="e37e3-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e37e3-112">Команда</span><span class="sxs-lookup"><span data-stu-id="e37e3-112">Command</span></span> | <span data-ttu-id="e37e3-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="e37e3-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e37e3-114">az group create</span><span class="sxs-lookup"><span data-stu-id="e37e3-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e37e3-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="e37e3-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e37e3-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="e37e3-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="e37e3-117">Создает виртуальную машину hello и подключает его toohello сетевой карты, виртуальной сети, подсети и группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="e37e3-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="e37e3-118">Эта команда также указывает hello toobe образа на виртуальной машине используется и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="e37e3-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="e37e3-119">az group delete</span><span class="sxs-lookup"><span data-stu-id="e37e3-119">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="e37e3-120">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="e37e3-120">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e37e3-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e37e3-121">Next steps</span></span>

<span data-ttu-id="e37e3-122">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e37e3-122">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e37e3-123">Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машины Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e37e3-123">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
