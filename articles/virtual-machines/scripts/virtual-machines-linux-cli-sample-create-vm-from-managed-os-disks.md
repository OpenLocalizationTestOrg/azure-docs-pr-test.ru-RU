---
title: "Пример скрипта Azure CLI. Создание виртуальной машины путем подключения управляемого диска в качестве диска ОС | Документация Майкрософт"
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
ms.openlocfilehash: 18eefee869b243b35d4426c226eff5f48cd490a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a><span data-ttu-id="6d13f-103">Создание виртуальной машины с помощью существующего управляемого диска ОС с использованием CLI</span><span class="sxs-lookup"><span data-stu-id="6d13f-103">Create a virtual machine using an existing managed OS disk with CLI</span></span>

<span data-ttu-id="6d13f-104">Этот скрипт создает виртуальную машину путем подключения существующего управляемого диска как диска ОС.</span><span class="sxs-lookup"><span data-stu-id="6d13f-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="6d13f-105">Используйте этот скрипт в таких сценариях:</span><span class="sxs-lookup"><span data-stu-id="6d13f-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="6d13f-106">создание виртуальной машины из существующего управляемого диска ОС, скопированного из управляемого диска в другой подписке;</span><span class="sxs-lookup"><span data-stu-id="6d13f-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="6d13f-107">создание виртуальной машины из существующего управляемого диска, который был создан из специального файла VHD;</span><span class="sxs-lookup"><span data-stu-id="6d13f-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="6d13f-108">создание виртуальной машины из существующего управляемого диска ОС, который был создан из моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="6d13f-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6d13f-109">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="6d13f-109">Sample script</span></span>

<span data-ttu-id="6d13f-110">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Создание виртуальной машины из управляемого диска")]</span><span class="sxs-lookup"><span data-stu-id="6d13f-110">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6d13f-111">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="6d13f-111">Clean up deployment</span></span> 

<span data-ttu-id="6d13f-112">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="6d13f-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="6d13f-113">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="6d13f-113">Script explanation</span></span>

<span data-ttu-id="6d13f-114">Этот скрипт использует следующие команды для получения свойств управляемого диска, его подключения к новой виртуальной машине и создания виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="6d13f-114">This script uses the following commands to get managed disk properties, attach a managed disk to a new VM and create a VM.</span></span> <span data-ttu-id="6d13f-115">Для каждого элемента в таблице приведены ссылки на документацию по команде.</span><span class="sxs-lookup"><span data-stu-id="6d13f-115">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6d13f-116">Команда</span><span class="sxs-lookup"><span data-stu-id="6d13f-116">Command</span></span> | <span data-ttu-id="6d13f-117">Примечания</span><span class="sxs-lookup"><span data-stu-id="6d13f-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6d13f-118">az disk show</span><span class="sxs-lookup"><span data-stu-id="6d13f-118">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="6d13f-119">Получает свойства управляемого диска, используя имя диска и имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="6d13f-119">Gets managed disk properties using disk name and resource group name.</span></span> <span data-ttu-id="6d13f-120">Свойство идентификатора используется для подключения управляемого диска к новой виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="6d13f-120">Id property is used to attach a managed disk to a new VM</span></span> |
| [<span data-ttu-id="6d13f-121">az vm create</span><span class="sxs-lookup"><span data-stu-id="6d13f-121">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="6d13f-122">Создает виртуальную машину с помощью управляемого диска ОС.</span><span class="sxs-lookup"><span data-stu-id="6d13f-122">Creates a VM using a managed OS disk</span></span> |
## <a name="next-steps"></a><span data-ttu-id="6d13f-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6d13f-123">Next steps</span></span>

<span data-ttu-id="6d13f-124">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6d13f-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6d13f-125">Дополнительные примеры скриптов интерфейса командной строки для виртуальных машин см. в [документации по виртуальным машинам Azure под управлением Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6d13f-125">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
