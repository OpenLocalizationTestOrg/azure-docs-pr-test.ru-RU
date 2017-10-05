---
title: "Пример скрипта Azure CLI. Создание виртуальной машины из моментального снимка | Документация Майкрософт"
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
ms.openlocfilehash: 6e47c3baebd5b68ec29d55c43dc00ae7665c81f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-cli"></a><span data-ttu-id="787d8-103">Создание виртуальной машины из моментального снимка с помощью интерфейса командной строки</span><span class="sxs-lookup"><span data-stu-id="787d8-103">Create a virtual machine from a snapshot with CLI</span></span>

<span data-ttu-id="787d8-104">Этот скрипт создает виртуальную машину из моментального снимка диска ОС.</span><span class="sxs-lookup"><span data-stu-id="787d8-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="787d8-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="787d8-105">Sample script</span></span>

<span data-ttu-id="787d8-106">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.sh "Создание виртуальной машины из моментального снимка")]</span><span class="sxs-lookup"><span data-stu-id="787d8-106">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.sh "Create VM from snapshot")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="787d8-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="787d8-107">Clean up deployment</span></span> 

<span data-ttu-id="787d8-108">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="787d8-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="787d8-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="787d8-109">Script explanation</span></span>

<span data-ttu-id="787d8-110">Для создания управляемого диска, виртуальной машины и всех связанных ресурсов этот скрипт использует указанные ниже команды.</span><span class="sxs-lookup"><span data-stu-id="787d8-110">This script uses the following commands to create a managed disk, virtual machine, and all related resources.</span></span> <span data-ttu-id="787d8-111">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="787d8-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="787d8-112">Команда</span><span class="sxs-lookup"><span data-stu-id="787d8-112">Command</span></span> | <span data-ttu-id="787d8-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="787d8-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="787d8-114">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="787d8-114">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="787d8-115">Возвращает моментальный снимок на основе имени моментального снимка и группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="787d8-115">Gets snapshot using snapshot name and resource group name.</span></span> <span data-ttu-id="787d8-116">Для создания управляемого диска используется свойство идентификатора возвращаемого объекта.</span><span class="sxs-lookup"><span data-stu-id="787d8-116">Id property of the returned object is used to create a managed disk.</span></span>  |
| [<span data-ttu-id="787d8-117">az disk create</span><span class="sxs-lookup"><span data-stu-id="787d8-117">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="787d8-118">Создает управляемые диски из моментального снимка на основе идентификатора моментального снимка, имени диска, типа хранилища и размера.</span><span class="sxs-lookup"><span data-stu-id="787d8-118">Creates managed disks from a snapshot using snapshot Id, disk name, storage type, and size</span></span>  |
| [<span data-ttu-id="787d8-119">az vm create</span><span class="sxs-lookup"><span data-stu-id="787d8-119">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="787d8-120">Создает виртуальную машину с помощью управляемого диска ОС.</span><span class="sxs-lookup"><span data-stu-id="787d8-120">Creates a VM using a managed OS disk</span></span> |

## <a name="next-steps"></a><span data-ttu-id="787d8-121">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="787d8-121">Next steps</span></span>

<span data-ttu-id="787d8-122">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="787d8-122">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="787d8-123">Дополнительные примеры скриптов интерфейса командной строки для виртуальных машин см. в [документации по виртуальным машинам Azure под управлением Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="787d8-123">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
