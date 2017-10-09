---
title: "aaaAzure образец скрипта CLI - создать две виртуальные машины с внутренними и внешними NSG | Документы Microsoft"
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
ms.openlocfilehash: f04e62d09575bee34ac4aeee949736b34000c337
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a><span data-ttu-id="413d1-103">Защита сетевого трафика между виртуальными машинами</span><span class="sxs-lookup"><span data-stu-id="413d1-103">Secure network traffic between virtual machines</span></span>

<span data-ttu-id="413d1-104">Этот скрипт создает две виртуальные машины, а также обеспечивает защиту tooboth входящего трафика.</span><span class="sxs-lookup"><span data-stu-id="413d1-104">This script creates two virtual machines and secures incoming traffic tooboth.</span></span> <span data-ttu-id="413d1-105">Здравствуйте, один виртуальный компьютер доступен по Интернету и группы безопасности сети (NSG) настроил tooallow трафика на порт 3389 и порт 80.</span><span class="sxs-lookup"><span data-stu-id="413d1-105">One virtual machine is accessible on hello internet and has a network security group (NSG) configured tooallow traffic on port 3389 and port 80.</span></span> <span data-ttu-id="413d1-106">Hello второй виртуальной машины недоступен на hello Интернета и имеет tooonly NSG настроен разрешить трафик от hello первую виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="413d1-106">hello second virtual machine is not accessible on hello internet, and has an NSG configured tooonly allow traffic from hello first virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="413d1-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="413d1-107">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-windows-vm-nsg.sh "Create VM with NSG")]

## <a name="clean-up-deployment"></a><span data-ttu-id="413d1-108">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="413d1-108">Clean up deployment</span></span> 

<span data-ttu-id="413d1-109">Выполните следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello.</span><span class="sxs-lookup"><span data-stu-id="413d1-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="413d1-110">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="413d1-110">Script explanation</span></span>

<span data-ttu-id="413d1-111">Этот скрипт использует hello, следующие команды toocreate группу ресурсов виртуальной машины, и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="413d1-111">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="413d1-112">Каждая команда в таблице hello связывает toocommand документацию.</span><span class="sxs-lookup"><span data-stu-id="413d1-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="413d1-113">Команда</span><span class="sxs-lookup"><span data-stu-id="413d1-113">Command</span></span> | <span data-ttu-id="413d1-114">Примечания</span><span class="sxs-lookup"><span data-stu-id="413d1-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="413d1-115">az group create</span><span class="sxs-lookup"><span data-stu-id="413d1-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="413d1-116">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="413d1-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="413d1-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="413d1-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="413d1-118">Создает виртуальную сеть и подсеть Azure.</span><span class="sxs-lookup"><span data-stu-id="413d1-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="413d1-119">az network vnet subnet create</span><span class="sxs-lookup"><span data-stu-id="413d1-119">az network vnet subnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="413d1-120">Создает подсеть.</span><span class="sxs-lookup"><span data-stu-id="413d1-120">Creates a subnet.</span></span> |
| [<span data-ttu-id="413d1-121">az vm create</span><span class="sxs-lookup"><span data-stu-id="413d1-121">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="413d1-122">Создает виртуальную машину hello и подключает его toohello сетевой карты, виртуальной сети, подсети и NSG.</span><span class="sxs-lookup"><span data-stu-id="413d1-122">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="413d1-123">Эта команда также указывает hello toobe образа на виртуальной машине используется и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="413d1-123">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="413d1-124">az network nsg rule update</span><span class="sxs-lookup"><span data-stu-id="413d1-124">az network nsg rule update</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | <span data-ttu-id="413d1-125">Обновляет правило NSG.</span><span class="sxs-lookup"><span data-stu-id="413d1-125">Updates an NSG rule.</span></span> <span data-ttu-id="413d1-126">В этом образце hello внутренней правило является обновленные toopass через трафик только от интерфейса подсети hello.</span><span class="sxs-lookup"><span data-stu-id="413d1-126">In this sample, hello back-end rule is updated toopass through traffic only from hello front-end subnet.</span></span> |
| [<span data-ttu-id="413d1-127">az network nsg rule list</span><span class="sxs-lookup"><span data-stu-id="413d1-127">az network nsg rule list</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | <span data-ttu-id="413d1-128">Возвращает сведения о правиле группы безопасности сети.</span><span class="sxs-lookup"><span data-stu-id="413d1-128">Returns information about a network security group rule.</span></span> <span data-ttu-id="413d1-129">В этом образце имя правила hello хранится в переменной для дальнейшего использования в скрипт hello.</span><span class="sxs-lookup"><span data-stu-id="413d1-129">In this sample, hello rule name is stored in a variable for use later in hello script.</span></span> |
| [<span data-ttu-id="413d1-130">az group delete</span><span class="sxs-lookup"><span data-stu-id="413d1-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="413d1-131">Удаляет группу ресурсов со всеми вложенными ресурсами.</span><span class="sxs-lookup"><span data-stu-id="413d1-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="413d1-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="413d1-132">Next steps</span></span>

<span data-ttu-id="413d1-133">Дополнительные сведения о hello Azure CLI см. в разделе [документации Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="413d1-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="413d1-134">Примеры сценариев CLI дополнительную виртуальную машину можно найти в hello [документации виртуальной Машины Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="413d1-134">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
