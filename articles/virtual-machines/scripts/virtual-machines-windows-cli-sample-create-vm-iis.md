---
title: "aaaAzure образец скрипта CLI - установка IIS | Документы Microsoft"
description: "Пример скрипта Azure CLI. Установка IIS"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/28/2017
ms.author: nepeters
ms.openlocfilehash: 2fabc9522f424cab4c672084ba8bedfd623c87cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="quick-create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="eae02-103">Быстрое создание виртуальной машины с hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="eae02-103">Quick Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="eae02-104">Этот скрипт создает виртуальную машину Azure под управлением Windows Server 2016 и использует виртуальную машину Azure настраиваемое расширение скриптов hello tooinstall IIS.</span><span class="sxs-lookup"><span data-stu-id="eae02-104">This script creates an Azure Virtual Machine running Windows Server 2016, and uses hello Azure Virtual Machine Custom Script Extension tooinstall IIS.</span></span> <span data-ttu-id="eae02-105">После выполнения сценария hello, можно получить доступ к веб-сайт IIS по умолчанию hello на общедоступный IP-адрес hello hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="eae02-105">After running hello script, you can access hello default IIS website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="eae02-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="eae02-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-windows-iis/create-vm-windows-iis.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="eae02-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="eae02-107">Clean up deployment</span></span> 

<span data-ttu-id="eae02-108">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="eae02-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="eae02-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="eae02-109">Script explanation</span></span>

<span data-ttu-id="eae02-110">Этот скрипт использует hello, следующие команды toocreate группу ресурсов виртуальной машины, и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="eae02-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="eae02-111">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="eae02-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="eae02-112">Команда</span><span class="sxs-lookup"><span data-stu-id="eae02-112">Command</span></span> | <span data-ttu-id="eae02-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="eae02-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="eae02-114">az group create</span><span class="sxs-lookup"><span data-stu-id="eae02-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="eae02-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="eae02-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="eae02-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="eae02-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="eae02-117">Создает виртуальную машину hello и подключает его toohello сетевой карты, виртуальной сети, подсети и группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="eae02-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="eae02-118">Эта команда также указывает hello toobe образа на виртуальной машине используется и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="eae02-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="eae02-119">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="eae02-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="eae02-120">Создает tooallow правило группы безопасности сети входящий трафик.</span><span class="sxs-lookup"><span data-stu-id="eae02-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="eae02-121">В этом примере открывается порт 80 для трафика HTTP.</span><span class="sxs-lookup"><span data-stu-id="eae02-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="eae02-122">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="eae02-122">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="eae02-123">Добавляет и запускает tooa расширения виртуальной машины виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="eae02-123">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="eae02-124">В этом образце hello расширение пользовательского скрипта является используется tooinstall IIS.</span><span class="sxs-lookup"><span data-stu-id="eae02-124">In this sample, hello custom script extension is used tooinstall IIS.</span></span>|
| [<span data-ttu-id="eae02-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="eae02-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="eae02-126">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="eae02-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="eae02-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="eae02-127">Next steps</span></span>

<span data-ttu-id="eae02-128">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="eae02-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="eae02-129">Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машины Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="eae02-129">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
