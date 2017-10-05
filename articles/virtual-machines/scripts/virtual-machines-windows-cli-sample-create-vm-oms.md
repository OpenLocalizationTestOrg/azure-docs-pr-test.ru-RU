---
title: "Пример скрипта Azure CLI. Создание виртуальной машины Windows Server 2016 с использованием мониторинга OMS | Документация Майкрософт"
description: "Пример скрипта Azure CLI. Создание виртуальной машины Windows Server 2016 с использованием мониторинга OMS"
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
ms.author: rclaus
ms.openlocfilehash: ddb191163061dc47712e024c8c1d7a6f4bdf325b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="6d58a-103">Мониторинг виртуальной машины с помощью Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="6d58a-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="6d58a-104">Этот скрипт создает виртуальную машину Azure, устанавливает агент Operations Management Suite и регистрирует систему в рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="6d58a-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="6d58a-105">После выполнения скрипта виртуальная машина отобразится в консоли OMS.</span><span class="sxs-lookup"><span data-stu-id="6d58a-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6d58a-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="6d58a-106">Sample script</span></span>

<span data-ttu-id="6d58a-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-monitor-oms.sh "Быстрое создание виртуальной машины")]</span><span class="sxs-lookup"><span data-stu-id="6d58a-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-monitor-oms.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="6d58a-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="6d58a-108">Clean up deployment</span></span> 

<span data-ttu-id="6d58a-109">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="6d58a-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="6d58a-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="6d58a-110">Script explanation</span></span>

<span data-ttu-id="6d58a-111">Для создания группы ресурсов, виртуальной машины и всех связанных ресурсов этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="6d58a-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="6d58a-112">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="6d58a-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6d58a-113">Команда</span><span class="sxs-lookup"><span data-stu-id="6d58a-113">Command</span></span> | <span data-ttu-id="6d58a-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="6d58a-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6d58a-115">az group create</span><span class="sxs-lookup"><span data-stu-id="6d58a-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6d58a-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="6d58a-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6d58a-117">az vm create</span><span class="sxs-lookup"><span data-stu-id="6d58a-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="6d58a-118">Создает виртуальную машину и подключает ее к сетевой карте, виртуальной сети, подсети и группе безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="6d58a-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="6d58a-119">Эта команда также указывает образ виртуальной машины, который будет использоваться, и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="6d58a-119">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="6d58a-120">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="6d58a-120">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="6d58a-121">Выполняет расширение виртуальной машины на виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="6d58a-121">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="6d58a-122">В этом случае расширение агента Operations Management Suite используется для установки агента OMS и регистрации виртуальной машины в рабочей области OMS.</span><span class="sxs-lookup"><span data-stu-id="6d58a-122">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="6d58a-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="6d58a-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="6d58a-124">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="6d58a-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6d58a-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6d58a-125">Next steps</span></span>

<span data-ttu-id="6d58a-126">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6d58a-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6d58a-127">Дополнительные примеры скриптов интерфейса командной строки для виртуальных машин см. в [документации по виртуальным машинам Azure под управлением Windows](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6d58a-127">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
