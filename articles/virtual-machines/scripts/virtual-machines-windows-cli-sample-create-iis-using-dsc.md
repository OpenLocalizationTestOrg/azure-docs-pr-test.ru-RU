---
title: "Образец скрипта CLI - aaaAzure создания виртуальной Машины Windows Server 2016 со службами IIS с помощью DSC | Документы Microsoft"
description: "Пример скрипта Azure CLI. Создание виртуальной машины Windows Server 2016 с IIS с помощью DSC"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.custom: mvc
ms.openlocfilehash: 9883b5925dddca3dd53d083679a0e76d0fb982e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-iis-using-dsc"></a><span data-ttu-id="9fdf6-103">Создание виртуальной машины с IIS с помощью DSC</span><span class="sxs-lookup"><span data-stu-id="9fdf6-103">Create a VM with IIS using DSC</span></span>

<span data-ttu-id="9fdf6-104">Этот скрипт создает виртуальную машину и использует tooinstall расширение пользовательского скрипта DSC виртуальной машины Azure hello и настроить службы IIS.</span><span class="sxs-lookup"><span data-stu-id="9fdf6-104">This script creates a virtual machine, and uses hello Azure Virtual Machine DSC custom script extension tooinstall and configure IIS.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9fdf6-105">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="9fdf6-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-windows-iis-using-dsc/create-windows-iis-using-dsc.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9fdf6-106">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="9fdf6-106">Clean up deployment</span></span> 

<span data-ttu-id="9fdf6-107">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="9fdf6-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="9fdf6-108">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="9fdf6-108">Script explanation</span></span>

<span data-ttu-id="9fdf6-109">Этот скрипт использует hello, следующие команды toocreate группу ресурсов виртуальной машины, и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="9fdf6-109">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="9fdf6-110">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="9fdf6-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9fdf6-111">Команда</span><span class="sxs-lookup"><span data-stu-id="9fdf6-111">Command</span></span> | <span data-ttu-id="9fdf6-112">Примечания</span><span class="sxs-lookup"><span data-stu-id="9fdf6-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9fdf6-113">az group create</span><span class="sxs-lookup"><span data-stu-id="9fdf6-113">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9fdf6-114">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="9fdf6-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9fdf6-115">az vm create</span><span class="sxs-lookup"><span data-stu-id="9fdf6-115">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="9fdf6-116">Создает виртуальную машину hello и подключает его toohello сетевой карты, виртуальной сети, подсети и NSG.</span><span class="sxs-lookup"><span data-stu-id="9fdf6-116">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="9fdf6-117">Эта команда также указывает hello toobe образа на виртуальной машине используется и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="9fdf6-117">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="9fdf6-118">az vm extension set</span><span class="sxs-lookup"><span data-stu-id="9fdf6-118">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="9fdf6-119">Добавьте виртуальную машину hello настраиваемое расширение скриптов toohello, который вызывает сценарий tooinstall IIS.</span><span class="sxs-lookup"><span data-stu-id="9fdf6-119">Add hello Custom Script Extension toohello virtual machine which invokes a script tooinstall IIS.</span></span> |
| [<span data-ttu-id="9fdf6-120">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="9fdf6-120">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="9fdf6-121">Создает tooallow правило группы безопасности сети входящий трафик.</span><span class="sxs-lookup"><span data-stu-id="9fdf6-121">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="9fdf6-122">В этом примере открывается порт 80 для трафика HTTP.</span><span class="sxs-lookup"><span data-stu-id="9fdf6-122">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="9fdf6-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="9fdf6-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="9fdf6-124">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="9fdf6-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9fdf6-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9fdf6-125">Next steps</span></span>

<span data-ttu-id="9fdf6-126">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9fdf6-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9fdf6-127">Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машины Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9fdf6-127">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
