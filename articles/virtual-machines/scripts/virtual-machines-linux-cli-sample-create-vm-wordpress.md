---
title: "Пример сценария CLI - aaaAzure создания виртуальной Машины Linux с WordPress | Документы Microsoft"
description: "Пример скрипта Azure CLI. Создание виртуальной машины Linux с помощью WordPress"
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
ms.openlocfilehash: 2c5c03d08b6d5d27eb8c505b1dbd817eda5f2fc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-wordpress"></a><span data-ttu-id="2d5da-103">Создание виртуальной машины с помощью WordPress</span><span class="sxs-lookup"><span data-stu-id="2d5da-103">Create a VM with WordPress</span></span>

<span data-ttu-id="2d5da-104">Этот скрипт создает виртуальную машину, а затем использует расширение пользовательского скрипта tooinstall WordPress для hello виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="2d5da-104">This script creates a virtual machine, and then uses hello Azure Virtual Machine custom script extension tooinstall WordPress.</span></span> <span data-ttu-id="2d5da-105">После выполнения скрипта hello, можно получить доступ к hello WordPress веб-сайт конфигурации на `http://<public IP of VM>/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="2d5da-105">After running hello script, you can access hello WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2d5da-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="2d5da-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2d5da-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="2d5da-107">Clean up deployment</span></span> 

<span data-ttu-id="2d5da-108">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="2d5da-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2d5da-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="2d5da-109">Script explanation</span></span>

<span data-ttu-id="2d5da-110">Этот скрипт использует hello, следующие команды toocreate группу ресурсов виртуальной машины, и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="2d5da-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="2d5da-111">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="2d5da-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2d5da-112">Команда</span><span class="sxs-lookup"><span data-stu-id="2d5da-112">Command</span></span> | <span data-ttu-id="2d5da-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="2d5da-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2d5da-114">az group create</span><span class="sxs-lookup"><span data-stu-id="2d5da-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2d5da-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="2d5da-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2d5da-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="2d5da-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="2d5da-117">Создает виртуальную машину hello и подключает его toohello сетевой карты, виртуальной сети, подсети и NSG.</span><span class="sxs-lookup"><span data-stu-id="2d5da-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="2d5da-118">Эта команда также указывает hello toobe образа на виртуальной машине используется и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="2d5da-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="2d5da-119">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="2d5da-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="2d5da-120">Создает tooallow правило группы безопасности сети входящий трафик.</span><span class="sxs-lookup"><span data-stu-id="2d5da-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="2d5da-121">В этом примере открывается порт 80 для трафика HTTP.</span><span class="sxs-lookup"><span data-stu-id="2d5da-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="2d5da-122">az vm extension set</span><span class="sxs-lookup"><span data-stu-id="2d5da-122">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="2d5da-123">Добавьте hello настраиваемое расширение скриптов toohello виртуального компьютера, который вызывает сценарий tooinstall WordPress.</span><span class="sxs-lookup"><span data-stu-id="2d5da-123">Add hello Custom Script Extension toohello virtual machine, which invokes a script tooinstall WordPress.</span></span> |
| [<span data-ttu-id="2d5da-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="2d5da-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="2d5da-125">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="2d5da-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2d5da-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2d5da-126">Next steps</span></span>

<span data-ttu-id="2d5da-127">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2d5da-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2d5da-128">Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машине Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2d5da-128">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
