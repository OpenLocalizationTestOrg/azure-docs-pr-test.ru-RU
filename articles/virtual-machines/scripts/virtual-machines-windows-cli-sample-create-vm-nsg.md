---
title: "Пример скрипта Azure CLI. Создание двух виртуальных машин с внутренней и внешней группой безопасности сети | Документация Майкрософт"
description: "Пример скрипта Azure CLI. Создание двух виртуальных машин с внутренней и внешней группой безопасности сети"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: cc80e3fc5aaa12200e9a441db9d4a9c613c0548a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a><span data-ttu-id="9fda2-103">Защита сетевого трафика между виртуальными машинами</span><span class="sxs-lookup"><span data-stu-id="9fda2-103">Secure network traffic between virtual machines</span></span>

<span data-ttu-id="9fda2-104">Этот скрипт создает две виртуальные машины и защищает их входящий трафик.</span><span class="sxs-lookup"><span data-stu-id="9fda2-104">This script creates two virtual machines and secures incoming traffic to both.</span></span> <span data-ttu-id="9fda2-105">Одна виртуальная машина доступна через Интернет. Ее группа безопасности сети настроена таким образом, чтобы разрешать трафик на портах 3389 и 80.</span><span class="sxs-lookup"><span data-stu-id="9fda2-105">One virtual machine is accessible on the internet and has a network security group (NSG) configured to allow traffic on port 3389 and port 80.</span></span> <span data-ttu-id="9fda2-106">Вторая виртуальная машина недоступна через Интернет. Ее группа безопасности сети настроена таким образом, чтобы разрешать трафик только из первой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="9fda2-106">The second virtual machine is not accessible on the internet, and has an NSG configured to only allow traffic from the first virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9fda2-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="9fda2-107">Sample script</span></span>

<span data-ttu-id="9fda2-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-windows-vm-nsg.sh "Создание виртуальной машины с использованием группы безопасности сети")]</span><span class="sxs-lookup"><span data-stu-id="9fda2-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-windows-vm-nsg.sh "Create VM with NSG")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="9fda2-109">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="9fda2-109">Clean up deployment</span></span> 

<span data-ttu-id="9fda2-110">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="9fda2-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="9fda2-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="9fda2-111">Script explanation</span></span>

<span data-ttu-id="9fda2-112">Для создания группы ресурсов, виртуальной машины и всех связанных ресурсов этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="9fda2-112">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="9fda2-113">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="9fda2-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9fda2-114">Команда</span><span class="sxs-lookup"><span data-stu-id="9fda2-114">Command</span></span> | <span data-ttu-id="9fda2-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="9fda2-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9fda2-116">az group create</span><span class="sxs-lookup"><span data-stu-id="9fda2-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9fda2-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="9fda2-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9fda2-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="9fda2-118">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="9fda2-119">Создает виртуальную сеть и подсеть Azure.</span><span class="sxs-lookup"><span data-stu-id="9fda2-119">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="9fda2-120">az network vnet subnet create</span><span class="sxs-lookup"><span data-stu-id="9fda2-120">az network vnet subnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="9fda2-121">Создает подсеть.</span><span class="sxs-lookup"><span data-stu-id="9fda2-121">Creates a subnet.</span></span> |
| [<span data-ttu-id="9fda2-122">az vm create</span><span class="sxs-lookup"><span data-stu-id="9fda2-122">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="9fda2-123">Создает виртуальную машину и подключает ее к сетевой карте, виртуальной сети, подсети и группе безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="9fda2-123">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="9fda2-124">Эта команда также указывает образ виртуальной машины, который будет использоваться, и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="9fda2-124">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="9fda2-125">az network nsg rule update</span><span class="sxs-lookup"><span data-stu-id="9fda2-125">az network nsg rule update</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | <span data-ttu-id="9fda2-126">Обновляет правило NSG.</span><span class="sxs-lookup"><span data-stu-id="9fda2-126">Updates an NSG rule.</span></span> <span data-ttu-id="9fda2-127">В этом примере внутреннее правило обновляется, чтобы разрешить передачу трафика только из интерфейсной подсети.</span><span class="sxs-lookup"><span data-stu-id="9fda2-127">In this sample, the back-end rule is updated to pass through traffic only from the front-end subnet.</span></span> |
| [<span data-ttu-id="9fda2-128">az network nsg rule list</span><span class="sxs-lookup"><span data-stu-id="9fda2-128">az network nsg rule list</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | <span data-ttu-id="9fda2-129">Возвращает сведения о правиле группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="9fda2-129">Returns information about a network security group rule.</span></span> <span data-ttu-id="9fda2-130">В этом примере имя правила хранится в переменной для дальнейшего использования в скрипте.</span><span class="sxs-lookup"><span data-stu-id="9fda2-130">In this sample, the rule name is stored in a variable for use later in the script.</span></span> |
| [<span data-ttu-id="9fda2-131">az group delete</span><span class="sxs-lookup"><span data-stu-id="9fda2-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="9fda2-132">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="9fda2-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9fda2-133">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9fda2-133">Next steps</span></span>

<span data-ttu-id="9fda2-134">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9fda2-134">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9fda2-135">Дополнительные примеры скриптов интерфейса командной строки для виртуальных машин см. в [документации по виртуальным машинам Azure под управлением Windows](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9fda2-135">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
