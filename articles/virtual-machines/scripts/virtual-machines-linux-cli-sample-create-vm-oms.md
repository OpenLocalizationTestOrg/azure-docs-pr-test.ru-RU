---
title: "Образец скрипта CLI - aaaAzure создания виртуальной Машины Linux с мониторингом OMS | Документы Microsoft"
description: "Пример скрипта Azure CLI. Создание виртуальной машины Linux с использованием мониторинга OMS"
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
ms.openlocfilehash: 7a329d4f90a20e0e11faa1f5cafd0701574dc440
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="41267-103">Мониторинг виртуальной машины с помощью Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="41267-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="41267-104">Этот скрипт создает виртуальную машину Azure, устанавливает агент Operations Management Suite (OMS) hello и регистрирует hello системы с помощью рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="41267-104">This script creates an Azure Virtual Machine, installs hello Operations Management Suite (OMS) agent, and enrolls hello system with an OMS workspace.</span></span> <span data-ttu-id="41267-105">После выполнения сценария hello, будут отображаться в консоли OMS hello hello виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="41267-105">Once hello script has run, hello virtual machine will be visible in hello OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="41267-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="41267-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="41267-107">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="41267-107">Clean up deployment</span></span> 

<span data-ttu-id="41267-108">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="41267-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="41267-109">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="41267-109">Script explanation</span></span>

<span data-ttu-id="41267-110">Этот скрипт использует hello, следующие команды toocreate группу ресурсов виртуальной машины, и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="41267-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="41267-111">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="41267-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="41267-112">Команда</span><span class="sxs-lookup"><span data-stu-id="41267-112">Command</span></span> | <span data-ttu-id="41267-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="41267-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="41267-114">az group create</span><span class="sxs-lookup"><span data-stu-id="41267-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="41267-115">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="41267-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="41267-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="41267-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="41267-117">Создает виртуальную машину hello и подключает его toohello сетевой карты, виртуальной сети, подсети и NSG.</span><span class="sxs-lookup"><span data-stu-id="41267-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="41267-118">Эта команда также указывает hello toobe образа на виртуальной машине используется и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="41267-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="41267-119">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="41267-119">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="41267-120">Выполняет расширение виртуальной машины на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="41267-120">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="41267-121">В этом случае hello расширение Operations Management Suite agent — агент OMS используется tooinstall hello и зарегистрировать hello виртуальной Машины в рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="41267-121">In this case, hello Operations Management Suite agent extension is used tooinstall hello OMS agent and enroll hello VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="41267-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="41267-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="41267-123">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="41267-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="41267-124">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="41267-124">Next steps</span></span>

<span data-ttu-id="41267-125">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="41267-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="41267-126">Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машине Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="41267-126">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
