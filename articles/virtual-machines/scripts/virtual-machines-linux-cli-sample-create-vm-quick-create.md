---
title: "aaaAzure образец скрипта CLI - быстрое создание виртуальной Машины Linux | Документы Microsoft"
description: "Пример скрипта Azure CLI. Быстрое создание виртуальной машины Linux"
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
ms.openlocfilehash: edecf274f4e401af3603e5be37a989e2e0eb22c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine"></a><span data-ttu-id="d4a19-103">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="d4a19-103">Create a virtual machine</span></span>

<span data-ttu-id="d4a19-104">Этот скрипт создает виртуальную машину Azure с операционной системой Ubuntu, а также связанные сетевые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d4a19-104">This script creates an Azure Virtual Machine with an Ubuntu operating system and related networking resources.</span></span> <span data-ttu-id="d4a19-105">После выполнения сценария hello, доступ к виртуальной машине hello через SSH.</span><span class="sxs-lookup"><span data-stu-id="d4a19-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d4a19-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="d4a19-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-vm-quick.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d4a19-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="d4a19-107">Clean up deployment</span></span> 

<span data-ttu-id="d4a19-108">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="d4a19-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d4a19-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="d4a19-109">Script explanation</span></span>

<span data-ttu-id="d4a19-110">Этот скрипт использует hello, следующие команды toocreate группу ресурсов виртуальной машины, и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d4a19-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="d4a19-111">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="d4a19-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d4a19-112">Команда</span><span class="sxs-lookup"><span data-stu-id="d4a19-112">Command</span></span> | <span data-ttu-id="d4a19-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="d4a19-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d4a19-114">az group create</span><span class="sxs-lookup"><span data-stu-id="d4a19-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d4a19-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d4a19-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d4a19-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="d4a19-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="d4a19-117">Создает виртуальную машину hello и подключает его toohello сетевой карты, виртуальной сети, подсети и группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="d4a19-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="d4a19-118">Эта команда также указывает hello toobe образа на виртуальной машине используется и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="d4a19-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="d4a19-119">az group delete</span><span class="sxs-lookup"><span data-stu-id="d4a19-119">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="d4a19-120">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="d4a19-120">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d4a19-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d4a19-121">Next steps</span></span>

<span data-ttu-id="d4a19-122">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d4a19-122">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d4a19-123">Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машине Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d4a19-123">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
