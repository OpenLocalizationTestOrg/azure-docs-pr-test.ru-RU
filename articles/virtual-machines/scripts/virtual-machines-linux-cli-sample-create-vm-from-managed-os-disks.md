---
title: "Пример сценария CLI - aaaAzure создания виртуальной Машины путем присоединения управляемого диск как диск ОС | Документы Microsoft"
description: "Пример скрипта Azure CLI. Создание виртуальной машины путем подключения управляемого диска в качестве диска ОС"
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
ms.openlocfilehash: 71fc5c6a577c64b913cfa35e99b2b9b75dea0c31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a><span data-ttu-id="bf8c9-103">Создание виртуальной машины с помощью существующего управляемого диска ОС с использованием CLI</span><span class="sxs-lookup"><span data-stu-id="bf8c9-103">Create a virtual machine using an existing managed OS disk with CLI</span></span>

<span data-ttu-id="bf8c9-104">Этот скрипт создает виртуальную машину путем подключения существующего управляемого диска как диска ОС.</span><span class="sxs-lookup"><span data-stu-id="bf8c9-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="bf8c9-105">Используйте этот скрипт в таких сценариях:</span><span class="sxs-lookup"><span data-stu-id="bf8c9-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="bf8c9-106">создание виртуальной машины из существующего управляемого диска ОС, скопированного из управляемого диска в другой подписке;</span><span class="sxs-lookup"><span data-stu-id="bf8c9-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="bf8c9-107">создание виртуальной машины из существующего управляемого диска, который был создан из специального файла VHD;</span><span class="sxs-lookup"><span data-stu-id="bf8c9-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="bf8c9-108">создание виртуальной машины из существующего управляемого диска ОС, который был создан из моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="bf8c9-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="bf8c9-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="bf8c9-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]

## <a name="clean-up-deployment"></a><span data-ttu-id="bf8c9-110">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="bf8c9-110">Clean up deployment</span></span> 

<span data-ttu-id="bf8c9-111">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="bf8c9-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="bf8c9-112">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="bf8c9-112">Script explanation</span></span>

<span data-ttu-id="bf8c9-113">Этот скрипт использует следующие свойства диска tooget управляемых команды hello, присоединить tooa управляемого диска новой виртуальной Машины и создание виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="bf8c9-113">This script uses hello following commands tooget managed disk properties, attach a managed disk tooa new VM and create a VM.</span></span> <span data-ttu-id="bf8c9-114">Каждый элемент в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="bf8c9-114">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="bf8c9-115">Команда</span><span class="sxs-lookup"><span data-stu-id="bf8c9-115">Command</span></span> | <span data-ttu-id="bf8c9-116">Примечания</span><span class="sxs-lookup"><span data-stu-id="bf8c9-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bf8c9-117">az disk show</span><span class="sxs-lookup"><span data-stu-id="bf8c9-117">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="bf8c9-118">Получает свойства управляемого диска, используя имя диска и имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="bf8c9-118">Gets managed disk properties using disk name and resource group name.</span></span> <span data-ttu-id="bf8c9-119">Идентификатор свойства — используется tooattach tooa управляемого диска новой виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="bf8c9-119">Id property is used tooattach a managed disk tooa new VM</span></span> |
| [<span data-ttu-id="bf8c9-120">az vm create</span><span class="sxs-lookup"><span data-stu-id="bf8c9-120">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="bf8c9-121">Создает виртуальную машину с помощью управляемого диска ОС.</span><span class="sxs-lookup"><span data-stu-id="bf8c9-121">Creates a VM using a managed OS disk</span></span> |
## <a name="next-steps"></a><span data-ttu-id="bf8c9-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bf8c9-122">Next steps</span></span>

<span data-ttu-id="bf8c9-123">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bf8c9-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="bf8c9-124">Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машине Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bf8c9-124">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
