---
title: "Пример скрипта Azure CLI. Создание сети для многоуровневых приложений | Документация Майкрософт"
description: "Пример скрипта Azure CLI. Создание сети для многоуровневых приложений."
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: de65d820f2d9eea49b58185c81d815675fd76740
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="d93a3-103">Создание сети для многоуровневых приложений</span><span class="sxs-lookup"><span data-stu-id="d93a3-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="d93a3-104">В этом примере скрипта создается виртуальная сеть с интерфейсной и внутренней подсетями.</span><span class="sxs-lookup"><span data-stu-id="d93a3-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="d93a3-105">Трафик к интерфейсной подсети принимается по протоколам HTTP и SSH, в то время как трафик к внутренней подсети принимается только от MySQL по порту 3306.</span><span class="sxs-lookup"><span data-stu-id="d93a3-105">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> <span data-ttu-id="d93a3-106">После запуска скрипта у вас будет две виртуальные машины, по одной в каждой подсети, на которых вы можете развернуть веб-сервер и программное обеспечение MySQL.</span><span class="sxs-lookup"><span data-stu-id="d93a3-106">After running the script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="d93a3-107">Пример скрипта</span><span class="sxs-lookup"><span data-stu-id="d93a3-107">Sample script</span></span>


<span data-ttu-id="d93a3-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Виртуальная сеть для многоуровневого приложения")]</span><span class="sxs-lookup"><span data-stu-id="d93a3-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d93a3-109">Очистка развертывания</span><span class="sxs-lookup"><span data-stu-id="d93a3-109">Clean up deployment</span></span> 

<span data-ttu-id="d93a3-110">Выполните следующую команду, чтобы удалить группу ресурсов, виртуальную машину и все связанные с ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d93a3-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="d93a3-111">Описание скрипта</span><span class="sxs-lookup"><span data-stu-id="d93a3-111">Script explanation</span></span>

<span data-ttu-id="d93a3-112">Для создания группы ресурсов, виртуальной сети и групп безопасности сети этот скрипт использует следующие команды.</span><span class="sxs-lookup"><span data-stu-id="d93a3-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="d93a3-113">Для каждой команды в таблице приведены ссылки на соответствующую документацию.</span><span class="sxs-lookup"><span data-stu-id="d93a3-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="d93a3-114">Команда</span><span class="sxs-lookup"><span data-stu-id="d93a3-114">Command</span></span> | <span data-ttu-id="d93a3-115">Примечания</span><span class="sxs-lookup"><span data-stu-id="d93a3-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d93a3-116">az group create</span><span class="sxs-lookup"><span data-stu-id="d93a3-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="d93a3-117">Создает группу ресурсов, в которой хранятся все ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d93a3-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d93a3-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="d93a3-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="d93a3-119">Создает виртуальную сеть Azure и интерфейсную подсеть.</span><span class="sxs-lookup"><span data-stu-id="d93a3-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="d93a3-120">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="d93a3-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="d93a3-121">Создает внутреннюю подсеть.</span><span class="sxs-lookup"><span data-stu-id="d93a3-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="d93a3-122">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="d93a3-122">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="d93a3-123">Создает общедоступный IP-адрес для доступа к виртуальной машине из Интернета.</span><span class="sxs-lookup"><span data-stu-id="d93a3-123">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="d93a3-124">az network nic create</span><span class="sxs-lookup"><span data-stu-id="d93a3-124">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="d93a3-125">Создает виртуальные сетевые интерфейсы и присоединяет их к интерфейсной и внутренней подсети виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="d93a3-125">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="d93a3-126">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="d93a3-126">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="d93a3-127">Создает группы безопасности сети (NSG), которые связаны с интерфейсной и внутренней подсетями.</span><span class="sxs-lookup"><span data-stu-id="d93a3-127">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="d93a3-128">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="d93a3-128">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="d93a3-129">Создает правила групп безопасности сети, которые разрешают или блокируют определенные порты для конкретных подсетей.</span><span class="sxs-lookup"><span data-stu-id="d93a3-129">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="d93a3-130">az vm create</span><span class="sxs-lookup"><span data-stu-id="d93a3-130">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="d93a3-131">Создает виртуальные машины и присоединяет сетевой адаптер к каждой из них.</span><span class="sxs-lookup"><span data-stu-id="d93a3-131">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="d93a3-132">Эта команда также указывает образ виртуальной машины и учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="d93a3-132">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="d93a3-133">az group delete</span><span class="sxs-lookup"><span data-stu-id="d93a3-133">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="d93a3-134">Удаляет группу ресурсов и все содержащиеся в ней ресурсы.</span><span class="sxs-lookup"><span data-stu-id="d93a3-134">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d93a3-135">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d93a3-135">Next steps</span></span>

<span data-ttu-id="d93a3-136">Дополнительные сведения об Azure CLI см. в [документации по Azure CLI](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d93a3-136">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="d93a3-137">Дополнительные примеры сценариев Azure CLI для сетей Azure см. в [обзоре документации по сетям Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d93a3-137">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>