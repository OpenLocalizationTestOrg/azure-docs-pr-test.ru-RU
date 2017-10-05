---
title: "Пример скрипта Azure CLI. Создание виртуальной машины Linux | Документация Майкрософт"
description: "Пример скрипта Azure CLI. Создание виртуальной машины Linux"
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
ms.openlocfilehash: dc7e7276bcea32c59c67a42dedaffcedfd0cf907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-fully-configured-virtual-machine"></a><span data-ttu-id="d6e02-103">Создание полностью настроенной виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="d6e02-103">Create a fully configured virtual machine</span></span>

<span data-ttu-id="d6e02-104">Этот сценарий создает виртуальную машину Azure с операционной системой Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="d6e02-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="d6e02-105">После выполнения сценария можно получить доступ к виртуальной машине по протоколу SSH.</span><span class="sxs-lookup"><span data-stu-id="d6e02-105">After running the script, you can access the virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d6e02-106">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="d6e02-106">Sample script</span></span>

<span data-ttu-id="d6e02-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "Быстрое создание виртуальной машины")]</span><span class="sxs-lookup"><span data-stu-id="d6e02-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d6e02-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="d6e02-108">Clean up deployment</span></span> 

<span data-ttu-id="d6e02-109">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d6e02-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d6e02-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="d6e02-110">Script explanation</span></span>

<span data-ttu-id="d6e02-111">Для создания группы ресурсов, виртуальной машины и всех связанных ресурсов этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="d6e02-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="d6e02-112">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="d6e02-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d6e02-113">Команда</span><span class="sxs-lookup"><span data-stu-id="d6e02-113">Command</span></span> | <span data-ttu-id="d6e02-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="d6e02-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d6e02-115">az group create</span><span class="sxs-lookup"><span data-stu-id="d6e02-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="d6e02-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d6e02-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d6e02-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="d6e02-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="d6e02-118">Создает виртуальную сеть и подсеть Azure.</span><span class="sxs-lookup"><span data-stu-id="d6e02-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="d6e02-119">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="d6e02-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="d6e02-120">Создает общедоступный IP-адрес со статическим IP-адресом и связанным DNS-именем.</span><span class="sxs-lookup"><span data-stu-id="d6e02-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="d6e02-121">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="d6e02-121">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="d6e02-122">Создает группу безопасности сети (NSG), которая выполняет роль периметра безопасности между Интернетом и виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="d6e02-122">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span></span> |
| [<span data-ttu-id="d6e02-123">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="d6e02-123">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="d6e02-124">Создает правило NSG, разрешающее входящий трафик.</span><span class="sxs-lookup"><span data-stu-id="d6e02-124">Creates an NSG rule to allow inbound traffic.</span></span> <span data-ttu-id="d6e02-125">В этом примере открывается порт 22 для трафика SSH.</span><span class="sxs-lookup"><span data-stu-id="d6e02-125">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="d6e02-126">az network nic create</span><span class="sxs-lookup"><span data-stu-id="d6e02-126">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="d6e02-127">Создает виртуальную сетевую карту и подключает ее к виртуальной сети, подсети и группе безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="d6e02-127">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="d6e02-128">az vm create</span><span class="sxs-lookup"><span data-stu-id="d6e02-128">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="d6e02-129">Создает виртуальную машину и подключает ее к сетевой карте, виртуальной сети, подсети и группе безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="d6e02-129">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="d6e02-130">Эта команда также указывает образ виртуальной машины, который будет использоваться, и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="d6e02-130">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="d6e02-131">az group delete</span><span class="sxs-lookup"><span data-stu-id="d6e02-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="d6e02-132">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="d6e02-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d6e02-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d6e02-133">Next steps</span></span>

<span data-ttu-id="d6e02-134">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d6e02-134">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d6e02-135">Дополнительные примеры скриптов интерфейса командной строки для виртуальных машин см. в [документации по виртуальным машинам Azure под управлением Linux](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d6e02-135">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
