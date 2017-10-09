---
title: "Пример сценария CLI - aaaAzure создания виртуальной Машины из моментального снимка | Документы Microsoft"
description: "Создание виртуальной машины из моментального снимка с помощью скрипта Azure CLI."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: ddc95289dcb8a0ca7c7854d969983f96b8f4613f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-cli"></a><span data-ttu-id="0d2f5-103">Создание виртуальной машины из моментального снимка с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="0d2f5-103">Create a virtual machine from a snapshot with CLI</span></span>

<span data-ttu-id="0d2f5-104">Этот скрипт создает виртуальную машину из моментального снимка диска ОС.</span><span class="sxs-lookup"><span data-stu-id="0d2f5-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="0d2f5-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="0d2f5-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.sh "Create VM from snapshot")]

## <a name="clean-up-deployment"></a><span data-ttu-id="0d2f5-106">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="0d2f5-106">Clean up deployment</span></span> 

<span data-ttu-id="0d2f5-107">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="0d2f5-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="0d2f5-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="0d2f5-108">Script explanation</span></span>

<span data-ttu-id="0d2f5-109">Этот скрипт использует hello, следующие команды toocreate управляемой дисковой виртуальной машины, и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="0d2f5-109">This script uses hello following commands toocreate a managed disk, virtual machine, and all related resources.</span></span> <span data-ttu-id="0d2f5-110">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="0d2f5-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0d2f5-111">Команда</span><span class="sxs-lookup"><span data-stu-id="0d2f5-111">Command</span></span> | <span data-ttu-id="0d2f5-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="0d2f5-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0d2f5-113">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="0d2f5-113">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="0d2f5-114">Возвращает моментальный снимок на основе имени моментального снимка и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0d2f5-114">Gets snapshot using snapshot name and resource group name.</span></span> <span data-ttu-id="0d2f5-115">Свойство идентификатора hello, возвращаемый объект — используется toocreate управляемого диска.</span><span class="sxs-lookup"><span data-stu-id="0d2f5-115">Id property of hello returned object is used toocreate a managed disk.</span></span>  |
| [<span data-ttu-id="0d2f5-116">az disk create</span><span class="sxs-lookup"><span data-stu-id="0d2f5-116">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="0d2f5-117">Создает управляемые диски из моментального снимка на основе идентификатора моментального снимка, имени диска, типа хранилища и размера.</span><span class="sxs-lookup"><span data-stu-id="0d2f5-117">Creates managed disks from a snapshot using snapshot Id, disk name, storage type, and size</span></span>  |
| [<span data-ttu-id="0d2f5-118">az vm create</span><span class="sxs-lookup"><span data-stu-id="0d2f5-118">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="0d2f5-119">Создает виртуальную машину с помощью управляемого диска ОС.</span><span class="sxs-lookup"><span data-stu-id="0d2f5-119">Creates a VM using a managed OS disk</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0d2f5-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0d2f5-120">Next steps</span></span>

<span data-ttu-id="0d2f5-121">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0d2f5-121">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0d2f5-122">Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машине Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0d2f5-122">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
