---
title: "Пример скрипта Azure CLI. Создание виртуальной машины Windows Server | Документация Майкрософт"
description: "Пример скрипта Azure CLI. Создание виртуальной машины Windows Server"
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
ms.openlocfilehash: 9690e743e498a55d7339b6f51861fac37c9b0f56
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="78228-103">Создание виртуальной машины с помощью Azure CLI</span><span class="sxs-lookup"><span data-stu-id="78228-103">Create a virtual machine with the Azure CLI</span></span>

<span data-ttu-id="78228-104">Этот сценарий создает виртуальную машину Azure под управлением Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="78228-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="78228-105">После выполнения сценария можно получить доступ к виртуальной машине через подключение к удаленному рабочему столу.</span><span class="sxs-lookup"><span data-stu-id="78228-105">After running the script, you can access the virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="78228-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="78228-106">Sample script</span></span>

<span data-ttu-id="78228-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.sh "Быстрое создание виртуальной машины")]</span><span class="sxs-lookup"><span data-stu-id="78228-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="78228-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="78228-108">Clean up deployment</span></span> 

<span data-ttu-id="78228-109">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="78228-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="78228-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="78228-110">Script explanation</span></span>

<span data-ttu-id="78228-111">Для создания группы ресурсов, виртуальной машины и всех связанных ресурсов этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="78228-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="78228-112">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="78228-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="78228-113">Команда</span><span class="sxs-lookup"><span data-stu-id="78228-113">Command</span></span> | <span data-ttu-id="78228-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="78228-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="78228-115">az group create</span><span class="sxs-lookup"><span data-stu-id="78228-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="78228-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="78228-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="78228-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="78228-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="78228-118">Создает виртуальную сеть и подсеть Azure.</span><span class="sxs-lookup"><span data-stu-id="78228-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="78228-119">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="78228-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="78228-120">Создает общедоступный IP-адрес со статическим IP-адресом и связанным DNS-именем.</span><span class="sxs-lookup"><span data-stu-id="78228-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="78228-121">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="78228-121">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="78228-122">Создает группу безопасности сети (NSG), которая выполняет роль периметра безопасности между Интернетом и виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="78228-122">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span></span> |
| [<span data-ttu-id="78228-123">az network nic create</span><span class="sxs-lookup"><span data-stu-id="78228-123">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="78228-124">Создает виртуальную сетевую карту и подключает ее к виртуальной сети, подсети и группе безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="78228-124">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="78228-125">az vm create</span><span class="sxs-lookup"><span data-stu-id="78228-125">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="78228-126">Создает виртуальную машину и подключает ее к сетевой карте, виртуальной сети, подсети и группе безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="78228-126">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="78228-127">Эта команда также указывает образ виртуальной машины, который будет использоваться, и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="78228-127">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="78228-128">az group delete</span><span class="sxs-lookup"><span data-stu-id="78228-128">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="78228-129">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="78228-129">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="78228-130">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="78228-130">Next steps</span></span>

<span data-ttu-id="78228-131">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="78228-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="78228-132">Дополнительные примеры скриптов интерфейса командной строки для виртуальных машин см. в [документации по виртуальным машинам Azure под управлением Windows](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="78228-132">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
